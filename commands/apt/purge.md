# `apt purge`

## Overview

The `apt purge` sub-command is a **comprehensive removal action** in the Debian/Ubuntu APT package management system that **uninstalls a specified package and deletes associated system configuration files**. Unlike `apt remove`, which only removes the installed binaries and leaves configuration files intact, `apt purge` ensures that **both the package and its system-level configuration artifacts are removed** from the system. This makes it a preferred choice when the objective is to eliminate residual settings or cleanly reset a package’s footprint prior to reinstallation or removal.

In the context of a broader package management workflow, `apt purge` is typically employed as the final step in package lifecycle management when an administrator intends to completely remove a software package and its configuration state. It fits logically after package discovery, potential removal via `apt remove`, and may be followed by dependency cleanup (e.g., `apt autoremove`).

---

## Syntax

```bash
sudo apt purge <package>[ ...]
```

* **`<package>`**; One or more package names to be purged.

**Essential elements:**

* At least one package name is required; omission results in a usage error.
* The target package(s) must be installed or known to the package database for the purge to proceed.

**Optional considerations:**

* Flags such as `-y` (assume “yes” to prompts) can streamline scripted or non-interactive execution.
* Multiple packages can be purged in a single invocation by listing them separated by spaces.

---

## Operational Notes

**Preconditions**

* **Administrative privileges** are mandatory; running without `sudo` (or equivalent root access) will fail due to insufficient permissions.
* **A valid package state** must exist for the named package: it must have been previously installed or tracked by the package database.

**Behavior Compared to Similar Commands**

* When `apt purge` is executed, it **removes not only the package but also its system-level configuration files**, typically stored under directories like `/etc`. This differentiates it from `apt remove`, which intentionally preserves config files for later reuse.
* This operation **does not automatically remove user-specific configuration files stored in user home directories**; such files are outside APT’s purview since they are not tracked by the package database.

**Dependencies and System Impact**

* Purging a package may affect other packages that depend on it; in such cases, APT will indicate dependency implications and may prevent the action or require additional confirmations.
* After purging, **orphaned dependencies** (packages installed solely to satisfy the purged package’s requirements) may remain; administrators commonly run `apt autoremove` to clean these up.

**Sequencing in Workflow**

* Best practice is to ensure the local package index is current (`apt update`) before purging, though index freshness is **less critical** than for install/upgrade commands.
* `apt purge` is typically paired with maintenance tasks like `apt autoremove` and may precede a fresh `apt install` if the intent is reinstallation.
* The purge process results in a **cleaner removal state** than `remove`, making it preferable when configuration remnants would otherwise interfere with subsequent installations or when returning the system to a minimal state.

**System Feedback and State Changes**

* During execution, APT displays the list of packages slated for purge and any additional packages impacted by dependency resolution.
* A confirmation prompt appears by default, unless automation flags are used.
* Upon completion, the specified package’s installed files and associated system configuration are deleted; record of this action is logged in APT history.

---

## Example

```bash
sudo apt purge nginx
```

In this invocation:

* **`sudo`** elevates privileges.
* **`apt purge nginx`** instructs the package manager to remove the `nginx` web server package and all its system configuration files tracked by APT.

This example demonstrates the canonical use of `apt purge` for complete removal of a software package’s system footprint.

---
