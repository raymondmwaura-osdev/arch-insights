## Read-Only

### Driver

Linux has 2 drivers for mounting ntfs partitions:

1. Kernel NTFS driver (`ntfs`): Mostly read-only. Write support is experimental and dangerous.
2. `ntfs-3g` (FUSE-based): Has full read/write support.

Use the `ntfs-3g` driver for full read/write access.

```bash
sudo pacman -S install ntfs-3g

mount -t ntfs-3g /dev/sdXN /mnt
```

---
