# `apt list`

## Overview

The `apt list` sub-command is a **package listing utility** in the Debian/Ubuntu Advanced Package Tool (APT) suite that **displays a catalogue of packages based on specified criteria**. It queries the **local package index** (which should be refreshed with `apt update` to reflect current repository state) and prints package identifiers along with versions and architectures. This command does **not alter system state**; instead it provides visibility into both installed and available packages, making it useful for audits, inventories, and planning subsequent package management actions.

Administrators typically use `apt list` to inspect:
* all known packages in configured repositories,
* currently installed packages,
* packages with available upgrades,
* specific patterns or subsets based on filters.

---

## Syntax

```bash
apt list [options] [<pattern>]
```

* **`[options]`**; Flags that filter which packages are displayed (e.g., installed only).
* **`[<pattern>]`**; Optional pattern (globbing supported) to limit output to matching package names.

**Essential elements:**

* The command can be run with **no arguments** to list all packages known from the local index.
* Users may include one or more **pattern arguments** (e.g., `nginx`, `lib*`) to filter results by name.
* Unlike many APT actions, **administrative privileges (`sudo`) are not required** for basic listing since no package state is modified.

**Common options:**

* `--installed`; limit the list to currently installed packages.
* `--upgradeable`; show only packages that have newer versions available.
* `--all-versions`; display every known version from repositories for each package.

---

## Operational Notes

**Preconditions**

* **Local package index presence:** The command reads from the available local package index. For accurate and comprehensive lists, running `apt update` beforehand is recommended.

**Behavior and Filtering**

* Without filters, `apt list` shows package names, available versions, and architecture for all packages known from the configured repositories and local package state.
* When **patterns** are provided, the output is restricted to packages that match the glob pattern (e.g., `apt list 'lib*'`).
* With **filter options**, the output is scoped:

  * `--installed` displays only those packages currently installed.
  * `--upgradeable` shows only packages with pending upgrades according to the local index.
  * `--all-versions` enumerates all repository versions available rather than only the candidate version.

**Effect on System and Usage Context**

* `apt list` **does not install, upgrade, or remove** packages; it is strictly informational.
* Output is typically piped to utilities like `grep` or `less` for searching or pagination due to potentially large result sets.
* In package management workflows, `apt list` is often used **before installation (`apt install`) or upgrades (`apt upgrade`)** to identify candidate packages or verify state.

---

## Example

```bash
apt list --upgradeable
```

In this representative invocation:

* `apt list` lists packages from the local index.
* The `--upgradeable` option filters the output to show only those packages for which newer versions are available in the repositories.

This example exemplifies how `apt list` assists in **assessing pending updates** before actions like `apt upgrade`.

---
