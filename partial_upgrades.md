# Partial Upgrades

A partial upgrade is when you update the package database without updating the installed packages on the system. This is done by running `pacman -Sy` without the `-u` option.
    - `-S`: Sync/install packages.
    - `-y`: Refresh the package database from the repositories.
    - `-u`: System upgrade.

This should not be done because, when you try to install a new package after `pacman -Sy`, it looks at your **updated database** to determine dependencies. But your **actual system** has old versions. I got this error when installing nodejs and npm after a partial upgrade.

```
nodejs-nopt-9.0.0-1-any                                       13.8 KiB  20.6 KiB/s 00:01 [####################################################] 100%
 nodejs-25.9.0-1-x86_64                                        15.8 MiB  1534 KiB/s 00:11 [####################################################] 100%
 Total (9/9)                                                   19.7 MiB  1878 KiB/s 00:11 [####################################################] 100%
(9/9) checking keys in keyring                                                            [####################################################] 100%
(9/9) checking package integrity                                                          [####################################################] 100%
(9/9) loading package files                                                               [####################################################] 100%
(9/9) checking for file conflicts                                                         [####################################################] 100%
error: failed to commit transaction (conflicting files)
libgcc: /usr/lib/libgcc_s.so exists in filesystem (owned by gcc-libs)
libgcc: /usr/lib/libgcc_s.so.1 exists in filesystem (owned by gcc-libs)
libgcc: /usr/share/licenses/gcc-libs/RUNTIME.LIBRARY.EXCEPTION exists in filesystem (owned by gcc-libs)
libstdc++: /usr/lib/libstdc++.so exists in filesystem (owned by gcc-libs)
libstdc++: /usr/lib/libstdc++.so.6 exists in filesystem (owned by gcc-libs)
libstdc++: /usr/lib/libstdc++.so.6.0.34 exists in filesystem (owned by gcc-libs)
libstdc++: /usr/share/locale/de/LC_MESSAGES/libstdc++.mo exists in filesystem (owned by gcc-libs)
libstdc++: /usr/share/locale/fr/LC_MESSAGES/libstdc++.mo exists in filesystem (owned by gcc-libs)
Errors occurred, no packages were upgraded.
```

This error means that nodejs needs `libgcc` (version 14.2.0 for instance), but the actual system has `libgcc` (version 12.1.0 for instance) from `gcc-libs` installed. Pacman then tries to install the new version of `libgcc` but encounters an error because `/usr/lib/libgcc_s.so` is already owned by the old `gcc-libs`. This error causes pacman to quit without installing nodejs and npm.

**The Solution:** Never use `pacman -Sy` alone. Always upgrade fully.

---
