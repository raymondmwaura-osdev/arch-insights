# `parted`

+ `parted` is a program to manipulate disk partitions.
+ It supports both MS-DOS, and GPT partitioning schemes.

```
parted [options] [device [command [options]]]
```

+ `[device]`: The block device to be used. When none is given, parted will use the first block device it finds.
+ `[command [options]]`: Specifies the command to be executed. If no command is given, parted will present a command prompt.

---

## Commands

**Note**: Not all commands are documented. I only documented the ones I use.

### `help [command]`

Print general help, or help on `command` if specified.

### `mklabel label-type`

Create a new disklabel (partition table) of `label-type`. `label-type` should be one of: "gpt", "msdos", among others.

### `mkpart [part-type name fs-type] start end`

+ Create a new partition.
+ `part-type` is used only with `msdos` and `dvh` partition tables. Can be: "primary", "logical", or "extended".
+ `name` is required for `gpt` partition tables.
+ `fs-type` is optional. It can be one of: "ext4", "fat32", "linux-swap", "ntfs", among others.

### `name partition name`

+ Set the name of `partition` to `name`.
+ Works only on Mac, PC98, and GPT disklabels.

### `print print-type`

+ Display the partition table.
+ `print-type` is optional. It can be one of: "devices", "free", "list" or "all".

### `quit`

Exit from parted.

### `rm partition`

Delete `partition`.

---
