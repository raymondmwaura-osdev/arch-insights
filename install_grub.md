# Installing Grub

+  Install Required Packages

```
pacman -S grub efibootmgr
```

+ Install grub

```
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
```

+ Generate the configuration

```
grub-mkconfig -o /boot/grub/grub.cfg
```

+ Exit and reboot
