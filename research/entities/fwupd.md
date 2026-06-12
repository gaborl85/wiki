---
title: "fwupd"
created: 2026-06-12
last_updated: 2026-06-12
type: entity
tags: [firmware, linux, system-tools, ubuntu]
sources: ["2026-06-12-fwupd-update-failure-ubuntu-seed-permission-denied.md"]
related: ["[[Systematic Linux Troubleshooting Methodology]]", "[[EFI System Partition]]"]
---

# fwupd

**What is it?** `fwupd` (firmware update daemon/tool) is a Linux system utility for updating device firmware (BIOS, EC, peripherals) through a standardized interface. It stages firmware capsule files to the EFI System Partition (ESP) for application at reboot.

## Key Characteristics

- **Tool name:** `fwupdmgr` (command-line interface)
- **Service:** `fwupd` (daemon)
- **Function:** Discover available firmware updates, stage capsules to ESP, apply at boot
- **Requirements:** UEFI/EFI system, write access to EFI System Partition, Full Disk Encryption support

## Operational Details

- Stages firmware by creating files under ESP path (typically `/EFI/fwupd/fw`)
- Uses temporary mount points during update (e.g., `/run/mnt/ubuntu-seed/`)
- Requires write access to underlying partition; fails with "Permission denied" if ESP is read-only
- Supports authentication and hardware security module integration

## Known Constraints

- **Read-only ESP:** On systems where ESP is mounted read-only (e.g., Ubuntu Snapd layout), standard in-place updates will fail
- **Architecture-dependent:** Snapd-based systems mount ESP at `/var/lib/snapd/seed` in `ro` mode by design, blocking capsule staging

## Related Topics

- [[EFI System Partition]] — boot partition, firmware update staging location
- [[Ubuntu Snapd architecture]] — system design that can constrain fwupd operation
- [[Systematic Linux Troubleshooting Methodology]] — methodology for diagnosing fwupd failures

## Troubleshooting References

- [[fwupd permission denied case study|fwupd-permission-denied-case-study]] — Full diagnosis of permission failure in read-only ESP scenario
