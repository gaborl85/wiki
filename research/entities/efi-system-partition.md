---
title: "EFI System Partition"
created: 2026-06-12
last_updated: 2026-06-12
type: entity
tags: [efi, uefi, boot, firmware, filesystem]
sources: ["2026-06-12-fwupd-update-failure-ubuntu-seed-permission-denied.md"]
related: ["[[fwupd]]", "[[Ubuntu Snapd architecture]]"]
---

# EFI System Partition (ESP)

**What is it?** The EFI System Partition (ESP) is a special-purpose FAT32 partition on UEFI systems that stores boot loaders, firmware updates, and other firmware-related files. It is the staging location for firmware updates that apply at reboot.

## Key Characteristics

- **Format:** FAT32
- **Location:** Physical partition on disk (e.g., `/dev/nvme0n1p2`)
- **Mount point(s):** May be mounted at `/boot/efi`, `/efi`, or in Snapd systems at `/var/lib/snapd/seed`
- **Partition type:** EFI System Partition (GUID: C12A7328-F81F-11D2-BA4B-00A0C93EC93B)
- **Size:** Typically 256 MB – 4.9 GB depending on system and firmware update frequency
- **Access:** Usually mounted read-only to prevent accidental corruption; must be writable during firmware updates

## Role in Firmware Updates

- **Staging location** — Firmware update tools (like [[fwupd]]) write capsule files to ESP (typically under `/EFI/fwupd/fw`)
- **Update delivery** — At next boot, UEFI firmware reads capsule files from ESP and applies updates
- **Persistence** — Changes to ESP persist across reboots and are accessed by firmware before OS loads

## Mount Options and Constraints

- **Standard mount:** `ro,relatime` (read-only for safety)
- **During updates:** Must be remounted `rw` or updated from an environment where it's already writable
- **Snapd systems:** Mounted at `/var/lib/snapd/seed` in read-only mode by design; this can block in-place firmware updates

## Related Concepts

- [[UEFI boot]] — boot mechanism that uses ESP
- [[Firmware updates]] — the primary use case for ESP write access
- [[Ubuntu Snapd architecture]] — system design that may mount ESP read-only
- [[fwupd]] — firmware update tool that requires ESP write access

## Known Issues

- **Permission denied on read-only ESP** — See [[fwupd permission denied case study|fwupd-permission-denied-case-study]] for diagnosis and remediation
- **Snapd constraints** — On Ubuntu Snapd systems, ESP mounted read-only; live USB method required for firmware updates
