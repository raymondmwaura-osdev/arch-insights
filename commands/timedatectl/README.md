# `timedatectl`

## Overview

`timedatectl` is a command-line utility that comes with systemd (on systemd-based Linux distributions). It provides a unified interface to view and manipulate system time, date, time zone, and clock synchronization settings. Internally, it interacts with the service systemd‑timedated to apply changes.

In modern distributions, timekeeping involves multiple clocks: the software (system) clock, and the hardware clock (RTC; real-time clock) which persists even when the machine is powered off. `timedatectl` allows managing both, plus the system time zone, and whether the clock should be synchronized automatically (e.g. via network). This ensures consistency, avoids drift, and simplifies administration.

---

## Syntax and Commands

When you run `timedatectl`, you generally specify a **command** (or sub-command) and sometimes **arguments**. If no command is given, the default is `status`.

General form:

```
timedatectl [COMMAND] [ARGUMENTS...]
```

Below is a breakdown of the most common commands and their arguments:

* **`status`**
  Displays the system’s current time configuration, including local time, UTC, RTC time, time zone, and NTP status. This is also the default operation when no command is provided.

* **`show`**
  Produces the same information as `status` but in a machine-readable format suitable for scripting and automated workflows, with optional flags for expanded output.

* **`list-timezones`**
  Lists all valid time zone identifiers from the system’s time zone database, one per line, and is commonly used to select a valid zone before reconfiguration.

* **`set-timezone TIMEZONE`**
  Sets the system’s time zone to a specified identifier from `list-timezones`. This operation updates the underlying system configuration and may propagate to the hardware clock depending on RTC settings.

* **`set-time "YYYY-MM-DD HH:MM:SS"`**
  Sets the system’s software clock to an explicit date and time. If the RTC mirrors system time, the hardware clock is updated accordingly.

* **`set-local-rtc BOOL`**
  Determines whether the hardware clock stores time in local time (`TRUE`/`1`) or UTC (`FALSE`/`0`). UTC is generally recommended to avoid issues with daylight saving changes and multi-zone environments.

* **`set-ntp BOOL`**
  Enables or disables network time synchronization. When enabled, the system relies on NTP or a compatible service to maintain accurate time and prevent clock drift.

---

## Typical Usage Examples

```bash
# Display current date/time configuration (human-readable)
sudo timedatectl status

# List all available time zones
sudo timedatectl list-timezones

# Set the system time zone (for example, to Africa/Nairobi)
sudo timedatectl set-timezone Africa/Nairobi

# Turn on network time synchronization
sudo timedatectl set-ntp yes

# (If needed) set the system clock manually
sudo timedatectl set-time "2025-11-27 14:30:00"
```

After changing timezone or clock settings, `timedatectl status` can be used again to verify the result.

---

## Underlying Components and Considerations

* The `timedatectl` command communicates with `systemd-timedated`, a service that implements the underlying changes to the system clock, RTC, timezone files, and synchronization settings.
* The system’s timezone configuration typically relies on a file (e.g. `/etc/localtime`) which is a symbolic link to a timezone data file, usually under `/usr/share/zoneinfo`. Changing timezone updates this symlink accordingly.
* While it is possible to set the system clock manually, most modern systems benefit from enabling NTP synchronization: this prevents clock drift and ensures consistency across distributed systems, logs, scheduling, backups, etc.

---
