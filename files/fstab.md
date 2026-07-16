# `/etc/fstab`

**Note:** This document contains a summary of the `/etc/fstab` file. It's not complete. Read official documentation for more the complete documentation.

+ This file contains descriptive information about the filesystems the system can mount.
+ It is only read by programs, and not written; it is the duty of the system admin to properly create and maintain the file.

**Note:** On systemd-based systems, it's recommended to use `systemctl daemon-reload` after `fstab` modification, because systemd has daemons that use fstab.

## Format

- Each filesystem is described on a separate line.
- Fields are separated by tabs or spaces.
- Any spaces or tabs within the fields must be escaped using `\040` or `\011`, even within quoted strings (e.g. LABEL="foo\040bar").
- Example:
  ```
  LABEL=t-home2    /home    etx4    defaults,auto_da_alloc    0 2
  ```

### The first field (fs_spec)

+ This field describes the block special device to be mounted, or swap file or swap device to be enabled.
+ `LABEL=<label>` or `UUID=<uuid>` may be given instead of a device name. **This is the recommended method, as device names are often a coincidence of hardware detection order, and can change when other disks are added or removed.**
+ It's also possible to use `PARTUUID=` and `PARTLABEL=`. These are supported in GPT disks.
+ Use `lsblk -o +UUID` to get the UUID of partitions.

### The second field (fs_file)

+ This field describes the mount point for the filesystem.
+ For swap area, this field should be specified as `none`.

### The third field (fs_vfstype)

+ This field describes the type of filesystem. Example: ext4, vfat, etc.
+ An entry `swap` denotes a file or partition to be used for swapping.
+ An entry `none` is useful for bind or move mounts.
+ More than one type may be specified in a comma-separated list.

### The fourth field (fs_mntops)

+ This field describes the mount options associated with the filesystem.
+ It is formatted as a comma-separated list of options.
+ It is optional for `mount` or `swapon`.
+ The usual convention is to use at least `defaults` keyword there.
+ Basic filesystem independent options:
  - `defaults`: Use default options. The default depends on the kernel and the filesystem.
  - `noauto`: Do not mount when `mount -a` is given (e.g., at boot time).
  - `user`: Allow a user to mount.
  - `owner`: Allow device owner to mount.
  - `nofail`: Do not report errors for this device if it doesn't exist.

### The fifth field (fs_freq)

+ This field is used by `dump` to determine which filesystems need to be dumped.
+ Defaults to zero (don't dump) if not present.

### The sixth field (fs_passno)

+ This field is used by `fsck` to determine the order in which filesystem checks are done at boot time.
+ The root filesystem should be specified with `fs_passno` of 1.
+ Other filesystems should have a `fs_passno` of 2.
+ Defaults to 0 (don't check the filesystem) if not present.
+ Filesystems within a drive will be checked sequentially, but filesystems on different drives will be checked at the same time to utilize parallelism available in the hardware.

---
