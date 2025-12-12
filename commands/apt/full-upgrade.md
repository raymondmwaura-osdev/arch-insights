# `apt full-upgrade`

## Overview

The `apt full-upgrade` sub‑command is a **comprehensive system upgrade action** within the Debian/Ubuntu APT package management suite that performs package updates while also intelligently resolving dependency change; even when that resolution requires **installing additional packages or removing existing ones**. It is effectively the modern equivalent of the historical `apt‑get dist‑upgrade` command and is documented as the appropriate step for major system upgrades, such as when transitioning between stable releases or when package dependency changes cannot be satisfied by a conservative upgrade alone.

In the broader `apt` workflow, `full‑upgrade` is typically invoked **after refreshing the package index** with `apt update` and is used when a standard `apt upgrade` cannot complete all pending upgrades due to dependency alterations. Its **default behavior** is more assertive than `apt upgrade`: it not only updates packages to their latest versions but also **accommodates changes that require installing new packages or removing conflicting or obsolete packages in order to complete the upgrade process**.

---

## Syntax

```bash
sudo apt full-upgrade
```

**Essential elements:**

* No positional arguments are required; by default, the command applies to all installed packages and their upgrades according to the current package index.
* A valid and up‑to‑date package index (via `apt update`) is strongly recommended prior to execution.

**Optional modifications (beyond core syntax):**

* Flags (e.g., `‑y`) can automate response prompts for non‑interactive use.
* Proxy or configuration flags can modify environmental behavior but are not part of the canonical structure.

---

## Operational Notes

**Preconditions and Dependencies**

* The local package index should be current, which is accomplished by running `apt update` prior to `full‑upgrade`.
* Network access to all configured repositories is necessary to download upgraded packages and any additional dependencies.
* Administrative privileges (e.g., `sudo`) are required to apply changes to system‑wide packages and dependencies.

**Behavioral Characteristics**

* **Dependency resolution**: Unlike the more conservative `apt upgrade`, `full‑upgrade` will install new packages or remove existing ones if necessary to satisfy the dependency chains of upgraded packages.
* **Package removal**: This sub‑command may remove obsolete or conflicting packages that cannot be reconciled with newer versions under the current package configuration.
* **Usage context**: It is the recommended upgrade mechanism for **major distribution upgrades or scenarios with complex dependency changes**; for routine, minimal updates, `apt upgrade` is usually sufficient.

**Sequencing and System State**

* `apt full‑upgrade` should be executed **after** an `apt update`.
* Suggested workflow for major system maintenance:

  1. `sudo apt update`
  2. `sudo apt full‑upgrade`
  3. Evaluate proposed changes carefully before confirming execution.
* After execution, the system will have upgraded packages to their latest available versions from the configured repositories, and its installed package set may have changed (packages added or removed) to satisfy dependency requirements.

**User/System Feedback**

* The command output lists all packages to be upgraded, installed, or removed.
* The utility typically prompts for user confirmation before applying changes unless overridden by automation flags.
* System logs of the operation are recorded under APT history and terminal logs, providing traceability of actions taken.

---
