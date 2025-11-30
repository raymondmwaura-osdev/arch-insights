# `df`

## Overview

The `df` command in Linux (and other Unix-like systems) provides a snapshot of storage capacity across mounted file systems. It reports total, used, and available space; enabling system administrators and operators to monitor disk usage, identify storage constraints, and plan capacity growth or cleanup. Strategically, `df` is fundamental for system maintenance, capacity planning, and ensuring that services depending on disk space continue uninterrupted (e.g. logging, database operations, file storage).

Typical use-cases for `df` include: checking overall available space after installing software, before writing large data sets; monitoring free space across partitions; auditing mounted file systems on servers; and integrating into scripts for regular capacity reporting.

---

## Syntax

```
df [arguments]
```

---

## Usage Workflow

1. Invoke `df` without arguments to obtain a comprehensive view of all currently mounted file systems.
2. The command collects metadata from the operating system about each mounted file system (from files such as `/proc/mounts` or `/etc/mtab`).
3. It outputs a table summarizing the total size, used space, available space, usage percentage, and mount point.
4. Optionally, one may supply a specific file or mount point path to restrict the report to the file system containing that path.

---

## Example

Run:

```bash
df
```

Possible output:

```text
Filesystem     1K-blocks      Used Available Use% Mounted on
/dev/sda1       20480000   1024000  19456000   5% /
tmpfs            1024000         0   1024000   0% /run
```

This indicates that `/dev/sda1` (mounted at `/`) has 20,480,000 1K-blocks in total, 1,024,000 are used, and 19,456,000 remain available (≈ 5% used). `tmpfs` likewise shows its usage status.

---

## Implementation Considerations

* `df` reports only on **mounted** file systems; unmounted partitions or devices are not represented.
* By default, sizes are expressed in block units (commonly 1-kilobyte or 512-byte blocks depending on system settings).
* Because output reflects global filesystem metadata (not individual file-by-file usage), `df` might show space consumed by hidden, system or privileged files; so totals may not match what a user sees via directory-level commands.
* `df` is efficient for high-level capacity checks and suitable for automation (e.g. scripts that monitor storage thresholds), but not ideal for analyzing which directories or files are consuming space (for which one uses other tools).

---
