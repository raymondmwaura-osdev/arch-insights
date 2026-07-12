# Installing Arch Linux

## Verify the boot mode

Check UEFI bitness:

```
cat /sys/firmware/efi/fw_platform_size
```

+ If `64`, the system is booted in UEFI mode and has a 64-bit x64 UEFI.
+ If `32`, the system is booted in UEFI mode and has 32-bit IA32 UEFI.
+ If `No such file or directory`, the system may be booted in BIOS mode.

---

## Connect to the internet

**Note**: In the installation image, `sytemd-networkd`, `systemd-resolved`, `iwd` and ModemManager are preconfigured and enabled by default.

1. Ensure your network interface is listed and enabled, for example using `ip-link`. For wireless interfaces, make sure the card is not blocked with `rfkill`.
    ```
    ip link
    rfkill list
    ```
2. **Connect to the internet.** Authenticate to the wireless network using `iwctl`.
    ```
    # In iwctl's prompts.
    station wlan0 scan
    station wlan0 get-networks
    station wlan0 connect <network-name>
    station wlan0 show
    ```
3. **Configure your network connection.** Dynamic IP addresses and DNS server assignment (provided by `systemd-networkd` and `systemd-resolved`) should work out of the box for Ethernet, WLAN, and WWAN network interfaces.
4. **Verify the connection** using `ping`.

---

## Update the system clock

The clock needs to be accurate to prevent package signature verification failures and TLS certificate errors.

`systemd-timesyncd` is enabled in the live environment. The time will be synchronized automatically once a connection is established. Confirm this using `timedatectl`.

---

## Partition the disks

**This section is not documented because I didn't need to partition the disk when I wrote this guide. Refer to the arch wiki and man pages for info on this.**

The following partitions are required:
  + EFI system partition (500MB to 1GB).
  + A partition for the root directory: `/`

---

## Format the partitions

Each **newly** created partition must be formatted with an appropriate file system.

```
# The partition for the root directory.
mkfs.ext4 /dev/root_partition

# Partition for the swap space.
mkswap /dev/swap_partition

# EFI partition
mkfs.fat -F 32 /dev/efi_system_partition
```

**NOTE:** Only format the EFI system partition if you created it during the partition step. If there already was an EFI system partition on disk beforehand, reformatting it can destroy the boot loaders for other installed operating systems.

---

## Mount the filesystems

Mount the root volume to `/mnt`. Then mount the efi swap partition to `/mnt/boot`.

```
mount /dev/root_partition /mnt

mount --mkdir /dev/efi_system_partition /mnt/boot
```

If you created a swap volume, enable it.

```
swapon /dev/swap_partition
```

`genfstab` will later detect mounted file systems and swap space.

---

## Select the mirrors

- Packages to be installed must be downloaded from mirror servers.
- Mirror servers are defined in `/etc/pacman.d/mirrorlist`.
- High priority mirrors are placed higher on the list.
- In the live system, all HTTPS mirrors are enabled (i.e. uncommented). The topmost mirror is a worldwide mirror which should be fast enough for most people.
- You can edit the file by moving other mirrors higher on the list to give them more priority.
- You can alternatively use reflector to create a mirror list file based on various criteria.

**Note**: This file will later be copied to the new system by `pacstrap`. No configuration (except for `/etc/pacman.d/mirrorlist`) gets carried over from the live environment to the installed system.

---

## Install essential packages

- The only mandatory package to install is `base`, which does not include all tools from the live installation.
- To install more packages or package groups, append the names to the `pacstrap` command below (space separated) or use `pacman` to install them while chrooted into the new system.
  ```
  pacstrap -K /mnt base linux linux-firmware
  ```

**Tips**:
  - You can substitute `linux` with a kernel package of your choice, or you could omit it entirely when installing in a container.
  - You could omit the installation of the firmware package when installing in a virtual machine or container.

---

## Configure the system

### Fstab

To get needed file systems mounted on startup, generate an `fstab` file with persistent block device naming using `genfstab` (reference file systems by their UUIDs with `-U`).

```
genfstab -U /mnt >> /mnt/etc/fstab
```

### Chroot

To directly interact with the new system's environment, tools, and configurations for the next steps as if you were booted into it, change root into the new system.

```
arch-chroot /mnt
```

**Note**: Some systemd tools like `hostnamectl`, `localectl`, and `timedatectl` cannot be used inside `chroot`, because they require an active `dbus` connection.

### Time

Set the time zone:

```
ln -sf /usr/share/zoneinfo/Area/Location /etc/localtime
```

Run `hwclock` to generate `/ect/adjtime`:

```
hwclock --systohc
```

- This command assumes the hardware clock is set to UTC.
- To prevent clock drift and ensure accurate time, set up time synchronization using a Network Time Protocol (NTP) client such as `systemd-timesyncd`.

---

## Installing Additional Packages

These are the packages I've installed after installing arch linux.

+ `iwd`: For connecting to wireless networks
+ `man-db`: Package with the `man` command.
+ `imv`: Image viewer for X11 and Wayland, aimed at users of tiling window managers.
+ `wl-clipboard`: Copy paste type shii. Keystash needs this.
+ Self-explanatory ones: `git`, `firefox`, `tmux`, `which`, `sway`, `alacritty`, `ssh`, `wofi`, `nvim`, `waybar`, `sudo`
+ **Python**: `python-virtualenv`, `python-pip`
