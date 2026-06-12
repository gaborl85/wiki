---
title: "Firmware Update Failure: fwupd Permission Denied on Read-Only ESP"
created: 2026-06-12
last_updated: 2026-06-12
type: synthesis
tags: [troubleshooting, firmware, fwupd, efi, linux, case-study]
sources: ["2026-06-12-fwupd-update-failure-ubuntu-seed-permission-denied.md"]
related: ["[[Systematic Linux Troubleshooting Methodology]]", "[[fwupd]]", "[[EFI System Partition]]", "[[Ubuntu Snapd architecture]]"]
query_date: 2026-06-12
---

# Firmware Update Failure: fwupd Permission Denied on Read-Only ESP

## Problem Statement

**System:** Dell Latitude 5521 / Precision 3561 running Ubuntu with Snapd  
**Command:** `sudo fwupdmgr update` to apply System Firmware `1.42.0` → `1.43.0`  
**Error:** `failed to write-firmware: Failed to create '/run/mnt/ubuntu-seed/EFI/fwupd/fw': Permission denied`  
**Impact:** Firmware update cannot proceed; user stuck on older firmware version.

## Investigation Methodology

This case demonstrates **systematic Linux troubleshooting**: layered verification of assumptions from high-level operation down to filesystem constraints.

### Step 1: Verify Expected Mount Points Persist
**Assumption:** Temporary mount points created by `fwupd` (`/run/mnt/ubuntu-seed/`) persist after error.  
**Investigation:** `findmnt /run/mnt/ubuntu-seed /boot/efi`  
**Result:** No output — mount points not available post-execution.  
**Interpretation:** Temporary mounts are cleaned up; cannot inspect directly. Need to find the underlying persistent mount.

### Step 2: Verify Boot Mode & Hardware
**Assumption:** System is UEFI-based with proper EFI partitions.  
**Investigation:** Checked boot mode, ran `lsblk` for partition layout  
**Result:** 
- System confirmed in **UEFI mode**
- Partition `nvme0n1p2` identified as FAT/EFI type, labeled as `ubuntu-seed`
- Size: ~4.9G (consistent with ESP)

**Interpretation:** Hardware is correctly configured for EFI-based firmware updates.

### Step 3: Verify Actual Mount Options
**Assumption:** The EFI partition should be writable to allow firmware capsule staging.  
**Investigation:** `findmnt -no SOURCE,TARGET,OPTIONS /var/lib/snapd/seed`  
**Result:** 
```
/dev/nvme0n1p2 /var/lib/snapd/seed ro,relatime,...,errors=remount-ro
```

**Critical Finding:** The EFI System Partition backing `ubuntu-seed` is mounted **`ro` (read-only)**.

## Root Cause Analysis

**fwupd's requirement:** Write access to EFI System Partition to create firmware capsule files.

**What's happening:**
1. User runs `fwupdmgr update` with sudo (authentication succeeds)
2. fwupd identifies the EFI partition to stage firmware: `/dev/nvme0n1p2`
3. fwupd creates temporary mount at `/run/mnt/ubuntu-seed/`
4. fwupd attempts to create `/run/mnt/ubuntu-seed/EFI/fwupd/fw`
5. The backing filesystem `/dev/nvme0n1p2` is mounted read-only (`ro`)
6. File creation denied: **Permission denied**

**Root cause:** The EFI System Partition is mounted read-only by Ubuntu's Snapd architecture, but fwupd requires write access to stage firmware updates.

**Why this is by design:** Snapd mounts the seed partition read-only to maintain system integrity and prevent accidental modifications to the boot/firmware layer. This is a security design choice, not a misconfiguration.

## Confidence Assessment

**High confidence (directly evidenced):**
- Exact mount options confirmed via `findmnt`
- fwupd target path in error message matches temporary mount scheme
- Read-only mount is the sole barrier to file creation
- No authentication or FDE (Full Disk Encryption) issues present

## Remediation Options

### Option 1: Live USB Update (Preferred, Safest)

Perform firmware update from Ubuntu live USB where ESP is writable:
1. Boot from Ubuntu live USB
2. Run `sudo fwupdmgr update`
3. Reboot to apply

**Advantages:**
- ESP is mounted read-write on live USB
- Bypasses Snapd architecture constraints
- Clean, standard firmware update path
- No risk to running system

**Disadvantages:**
- Requires USB creation and reboot
- Takes longer than in-place update

### Option 2: In-Place Remount (Optional, May Fail)

Attempt to remount ESP read-write:
1. `sudo mount -o remount,rw /var/lib/snapd/seed`
2. `sudo fwupdmgr --verbose update`
3. `sudo mount -o remount,ro /var/lib/snapd/seed`

**Advantages:**
- No reboot or USB required
- Faster if successful

**Disadvantages:**
- Remount may be denied by system policy
- Violates Snapd's design intent (read-only seed)
- If remount succeeds but fwupd still references `ubuntu-seed` with permission errors, wastes time
- Should only attempt if comfortable bypassing design constraints

**Expectation:** This option will likely fail on a properly configured Snapd system. Use live USB method if remount fails.

## Key Lessons

1. **Error messages describe symptoms, not causes** — "Permission denied" is the symptom; the root cause is a read-only mount.

2. **Verify actual system state** — Don't assume mounts, permissions, or architecture. Use tools to expose reality.

3. **Distinguish design constraints from configuration errors** — A read-only seed partition is intentional (Snapd security design), not a misconfiguration.

4. **Follow tool requirements through system layers** — fwupd needs write access → ESP must be writable → Snapd architecture makes it read-only → solution must work with (or around) that design.

5. **Propose solutions with trade-offs explicit** — Live USB is safest; in-place remount is faster but risky and likely to fail.

## Status

- **Update state:** Not applied (blocked by read-only ESP)
- **System health:** No damage; all layers working as designed
- **Next step:** Use live USB method to apply firmware update safely
