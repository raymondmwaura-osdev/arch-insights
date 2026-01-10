# Time

Use `timedatectl` to set the time.

```sh
sudo timedatectl set-time "YYYY-MM-DD HH:MM:SS"
```

Enable network time synchronization.

```sh
sudo timedatectl set-ntp true
```

+ This uses `systemd-timesyncd.service`. Make sure the service is enabled, and running.
+ Use `timedatectl timesync-status` to show the current status of `systemd-timesyncd.service`.
+ Optionally, use `timedatectl status` and check the "System clock synchronized" and "NTP service" fields.

---
