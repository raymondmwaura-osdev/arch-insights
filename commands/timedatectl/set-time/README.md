# `set-time`

## Overview

The `set-time` sub‑command of timedatectl is used to manually set the system clock (software clock), and (at the same time) update the hardware clock (RTC, Real‑Time Clock) to match the new time.

This sub‑command is typically employed when automatic synchronization (via NTP) is disabled, or when immediate manual correction of clock/time is required; for example, after hardware clock drift, incorrect system time on initial setup, or when operating in a network‑disconnected environment. It fits within the broader workflow of `timedatectl` as the manual override mechanism to set the clock, as opposed to automatic synchronization or timezone adjustments.  

Executing `set-time` changes both the “system clock” (the time the operating system uses) and the hardware clock time. Because the hardware clock persists across reboots and power cycles, this ensures that the corrected time remains consistent after restarts.

---

## Syntax

```
timedatectl set-time [TIME]
```

Where `[TIME]` may be provided in one of the following formats (depending on which components you set):  

- `HH:MM:SS`; to set time only (hours, minutes, seconds)
- `YYYY-MM-DD`; to set date only (year, month, day), which implicitly sets time to 00:00:00.
- `"YYYY-MM-DD HH:MM:SS"`; to set both date and time.

The TIME parameter must comply with the timestamp format recognized by systemd / `timedatectl`.

Because this operation modifies system time and hardware clock, administrative (root) privileges are required.

---

## Operational Notes

- Before invoking `set-time`, if automatic time synchronization via NTP (or other time sync service) is active, it should ideally be disabled; otherwise the manual setting may be overridden by the synchronization service.
- On success, both the system clock and the hardware clock (RTC) are updated to the specified time.
- Because `set-time` writes direct time values, any reliance on network time sync or other time services will be temporarily suspended until synchronization is re‑enabled (if desired).  
- After execution, queries via `timedatectl status` (or simply `timedatectl`) will reflect the new system time and RTC time accordingly.

---

## Example

```bash
sudo timedatectl set-time "2025-11-27 14:30:00"
````

This command sets the system’s date and time to 27 November 2025, 14:30:00, and updates the hardware clock to the same timestamp.

```bash
timedatectl
```

will then reflect this updated time in its output.

```text
               Local time: Thu 2025-11-27 14:30:00 EAT
           Universal time: Thu 2025-11-27 11:30:00 UTC
                 RTC time: Thu 2025-11-27 11:30:00
                Time zone: Africa/Nairobi (EAT, +0300)
    System clock synchronized: no
              NTP service: inactive
          RTC in local TZ: no
```

```text
# (Alternatively, to set just the time of day)
sudo timedatectl set-time 23:26:00
```

This sets the system clock to 23:26:00 (keeping the current date unchanged) and updates RTC accordingly.

---
