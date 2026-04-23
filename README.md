# MOS IT87 Drivers

mos-it87-driver provides a **MOS plugin** for managing the IT87 driver.

---

## Overview

This repository contains the **MOS plugin implementation**, optional helper
functions required to integrate IT87 driver management into MOS.

The plugin enables MOS to download and install IT87 driver on demand directly
onto the system.

Driver Source

- IT87: https://github.com/frankcrawford/it87

---

## Build & Automation

This repository includes a **GitHub Actions workflow** used to build and package
the plugin for MOS.

The build process is fully automated and produces artifacts that can be consumed
by the MOS Hub or MOS release tooling.

---

## Licensing

The contents of this repository (plugin code, scripts, and configuration)
are licensed under **GPL-3.0**.

Downloaded IT87 drivers remain licensed under their respective upstream licenses
and are not part of this repository.
