# `apt show`

## Overview

The `apt show` sub-command is a **package metadata inspection utility** in the Debian/Ubuntu APT ecosystem that retrieves and displays detailed information about a specified package from the **local package index**. It presents critical metadata (such as version, repository source, installed size, dependencies, and descriptive fields) allowing system administrators to **evaluate package characteristics prior to installation, upgrade, or removal decisions**. Unlike commands that alter system state (`install`, `remove`, etc.), `apt show` is **read-only and informational**.

In standard workflows, `apt show` is typically invoked **after a package search (`apt search`)** and before installation (`apt install`) to confirm that the candidate package aligns with requirements (e.g., version, origin, dependencies). Accurate metadata visibility supports planning and risk assessment in change management processes.

---

## Syntax

```bash
apt show <package>[ ...]
```

* **`<package>`**: One or more exact package names to inspect.

**Essential elements:**

* At least one **exact package name** is required; approximate or fuzzy names will not yield the expected result.
* The local package index must contain metadata for the package (e.g., after `apt update`).

**Optional elements:**

* Multiple package names can be supplied in a single invocation to view information for several packages sequentially.
* There is **no requirement for elevated privileges (sudo)** because the command does not modify the system.

---

## Operational Notes

**Preconditions**

* **Local package index freshness:** While not mandatory for execution, running `apt update` beforehand ensures that the metadata shown reflects the latest information from all enabled repositories.
* **Package existence:** The specified package must exist in the local index; otherwise, `apt show` will report that the package could not be found.

**Behavioral Characteristics**

* `apt show` outputs fields including:

  * **Package** and **Version**,
  * **Priority** and **Section**,
  * **Origin** and **Maintainer**,
  * **Dependencies** (and reverse relationships if relevant),
  * **Installed and Download Size**,
  * **APT sources** (repository location),
  * **Description** (detailed explanatory text).
* By default, only the version that would be installed according to the current policy is shown. An optional `-a` flag (e.g., `apt show -a <package>`) can reveal **all versions across sources**, which is particularly useful in multi-release or pinning scenarios.
* This command **does not alter the system state**; it solely reads and displays metadata.

**Sequencing and Context**

* Frequently used **after `apt search`** to drill down on candidate packages that match a search term.
* Often used before `apt install` to **confirm version compatibility, dependency requirements, or source authenticity**.

**System Feedback**

* The terminal output is a multi-field display of the selected package’s metadata.
* If multiple packages are specified, outputs are separated by package blocks.
* If a package is not found in the local index, an explicit “package not found” message is returned.

---

## Example

```bash
apt show nginx
```

In this representative invocation:

* The `apt show` sub-command retrieves detailed metadata about the `nginx` package (e.g., version, dependencies, installed and download size, repository source, and description).
* The command does not require `sudo` because it does not change the system state.
* This inspection assists in determining whether the package meets the administrator’s requirements before further actions such as installation or upgrade.

---
