# Firmware Update Failure Summary (fwupd)

## Context
- **Date:** 2026-06-12
- **Host/User:** `gaborl@gabor-topdesk`
- **Command executed:** `sudo fwupdmgr update`
- **Target update:** System Firmware `1.42.0` -> `1.43.0`
- **Device family shown by updater:** Dell Latitude 5521 / Precision 3561

## What happened
The firmware update flow started normally:
1. User accepted the firmware upgrade prompt.
2. User acknowledged the Full Disk Encryption warning.
3. Authentication succeeded and the report upload completed.

The process then failed at the firmware staging step with:

`failed to write-firmware: Failed to create '/run/mnt/ubuntu-seed/EFI/fwupd/fw': Permission denied`

## Investigation performed
### 1. Checked expected mount points
`findmnt /run/mnt/ubuntu-seed /boot/efi` returned no output after the failed run.

Interpretation: temporary mount points used by `fwupd` are not guaranteed to persist after the command exits.

### 2. Verified boot mode and EFI partitions
System confirmed in **UEFI mode**.

Disk/partition output showed:
- `nvme0n1p2` (FAT/EFI type)
- label/usage aligned with `ubuntu-seed`
- partition type: `EFI System`
- size: `~4.9G`

### 3. Verified actual mount options
Command:
`findmnt -no SOURCE,TARGET,OPTIONS /var/lib/snapd/seed`

Output:
`/dev/nvme0n1p2 /var/lib/snapd/seed ro,relatime,...,errors=remount-ro`

Key finding: the EFI partition in use is mounted **read-only (`ro`)**.

## Root cause
`fwupd` attempted to stage firmware capsule files under an EFI path derived from the `ubuntu-seed` partition:
- `/run/mnt/ubuntu-seed/EFI/fwupd/fw`

That backing partition (`/dev/nvme0n1p2`) is mounted read-only at `/var/lib/snapd/seed`, so file creation is denied.

Therefore, the update failure is due to **ESP write access/mount mode**, not authentication and not the FDE prompt itself.

## Why the error is consistent
- `fwupd` requires write access to an EFI System Partition to stage updates.
- Current environment exposes only a seed-mounted ESP in `ro` mode.
- Attempting to create `EFI/fwupd/fw` on a read-only filesystem reliably yields permission denied.

## Recommended remediation path
### Preferred (safest)
Perform firmware update from an environment where the internal ESP is writable (e.g., Ubuntu live USB), then reboot.

### Optional in-place attempt (may fail by design on seed-based layout)
1. `sudo mount -o remount,rw /var/lib/snapd/seed`
2. `sudo fwupdmgr --verbose update`
3. `sudo mount -o remount,ro /var/lib/snapd/seed`

If remount to RW is denied or update still references `ubuntu-seed` with permission errors, use live USB method.

## Final status
- **Update state:** Not applied
- **Blocking condition:** EFI partition mounted read-only
- **Confidence in diagnosis:** High (directly evidenced by mount options and fwupd target path)
