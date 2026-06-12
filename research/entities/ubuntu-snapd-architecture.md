---
title: "Ubuntu Snapd Architecture"
created: 2026-06-12
last_updated: 2026-06-12
type: entity
tags: [ubuntu, snapd, system-design, security, immutable-infrastructure]
sources: ["2026-06-12-fwupd-update-failure-ubuntu-seed-permission-denied.md"]
related: ["[[EFI System Partition]]", "[[fwupd]]"]
---

# Ubuntu Snapd Architecture

**What is it?** Ubuntu's Snapd is a system architecture for running containerized applications (snaps) and managing the Ubuntu Core OS. It uses an immutable seed partition mounted read-only to maintain system integrity and enable transactional updates.

## Key Design Principles

1. **Immutability** — Critical system partitions (seed, boot) are mounted read-only by default to prevent accidental corruption
2. **Transactional updates** — System updates are atomic; either fully applied or fully rolled back
3. **Security** — Read-only boot and firmware layers prevent tampering

## System Layout

- **Seed partition** — Contains boot files, firmware references, and system metadata
- **Mount point:** `/var/lib/snapd/seed`
- **Mount options:** `ro,relatime,...,errors=remount-ro` (read-only)
- **EFI location:** Snapd system's EFI partition backing the seed mount

## Constraints and Trade-Offs

**Constraint:** Read-only seed partition by design.  
**Impact on [[fwupd]]:** Standard in-place firmware updates fail because fwupd requires write access to ESP.  
**Workaround:** Use live USB environment where ESP is writable.

## Related Concepts

- [[Ubuntu Core]] — immutable Linux distribution powered by Snapd
- [[Immutable infrastructure]] — system design pattern
- [[EFI System Partition]] — firmware partition affected by read-only constraint

## Known Limitations

- **Firmware updates in-place blocked** — See [[fwupd permission denied case study|fwupd-permission-denied-case-study]]
- **Direct seed modifications blocked** — By design; ensures system integrity
