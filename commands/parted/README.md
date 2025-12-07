# `parted`

## Overview

The GNU Parted command‑line tool is a utility for creating, inspecting, and modifying the partition layout on block storage devices (hard disks, SSDs, flash drives, etc.) under Linux and other Unix-like systems. Its core business value lies in its ability to manage partition tables (disk labels), create, delete, resize, and reorganize partitions; enabling flexible disk management, multi‑OS setups, filesystem layout changes, and storage reconfiguration without needing graphical tools. From a systems operations perspective, it is strategic for provisioning new storage, migrating data, repartitioning disks for virtual machines or servers, and automating disk setup in scripts.

Typical deployment scenarios for `parted` include:

* Preparing a new disk for use (initial partitioning, setting up GPT or MBR labels).
* Resizing or reorganizing partitions (e.g. shrinking or expanding a partition, adding new partitions).
* Cleaning or re‑labeling a disk (e.g. switching partition table format, wiping partitions).
* Automating partitioning in scripts for deployment, server provisioning, or disk cloning.

---

## Syntax

```bash
parted [options] [device [command [arguments...]]]
```

---

## Usage Workflow

1. **Invoke `parted` with a target device**; the device is typically a block device like `/dev/sda`, `/dev/sdb`, etc.
2. **Select a mode of operation**:

   * *Interactive mode*: run `parted /dev/sdX` with no command, entering commands at a prompt.
   * *Non‑interactive / scripted mode*: supply a command (or multiple commands) directly on the command line.
3. **Issue partition‑management commands**: create partition tables (`mklabel`), make partitions (`mkpart`), delete partitions (`rm`), view layout (`print`), set flags (`set`), resize partitions (`resizepart`), or rescue deleted partitions (`rescue`).
4. **Commit changes**: commands generally apply immediately (especially in interactive mode). There is no “staging” buffer that waits for an explicit “write” as in some other tools.
5. **Exit** with `quit` (interactive) or let the command complete (non‑interactive).

The expected input is a valid device name plus appropriate command arguments (partition numbers, start/end offsets or sizes, partition type, filesystem type, etc.). The output is a modified partition table, or printed partition layout, depending on the command.

---

## Example

Here is a reproducible example in non‑interactive mode:

```bash
sudo parted /dev/sdb mklabel gpt mkpart primary ext4 1MiB 100%
```

This command does the following:

* Targets the block device `/dev/sdb`.
* Creates a new partition table of type GPT.
* Creates a primary partition that spans from 1 MiB after the start of the disk to the end (100% of remaining space), intended for an ext4 filesystem.

After this, you would typically format the new partition with a filesystem tool (e.g. `mkfs.ext4 /dev/sdb1`).

Alternatively, in interactive mode:

```bash
sudo parted /dev/sdb
(parted) mklabel gpt
(parted) mkpart primary ext4 1MiB 100%
(parted) print
(parted) quit
```

---

## Implementation Considerations

* `parted` directly modifies the partition table of the storage device; changes are typically **committed immediately** (especially in interactive mode). There is no “preview then write” stage. This implies high risk: mistakes may be irreversible or require recovery tools.
* Before modifying partitions on a disk, **any mounted partitions must be unmounted**, and **swap disabled** if a partition is used as swap. Additionally, **back up data** on any disk you will modify; partitioning operations can corrupt or destroy existing data.
* `parted` supports multiple disk-label (partition‑table) types; e.g. MBR (msdos), GPT, and others (BSD, SUN, etc.) depending on system, making it more flexible than simpler tools.
* When specifying partition start and end, you must consider units (sectors, bytes, MiB/GiB, percentages, etc.). Mis‑specifying units or offsets can lead to overlapping or unusable partitions.
* Because changes are immediate, automation or scripting with `parted` requires caution; testing on non‑critical or virtual devices (disk images, VM disks) is advisable before applying to production disks.

---
