# AGENTS.md

Instructions for coding agents, and the people driving them, working in malachite's
vendor tree. The general rules (branches, commits, license headers, testing) are in the
[device tree's AGENTS.md](https://github.com/malachite-project/android_device_xiaomi_malachite/blob/lineage-23.2/AGENTS.md)
and apply here too, including working as an official LineageOS maintainer would: fix
causes properly, never with workarounds.

## This repository is generated

- Everything under `proprietary/` comes unchanged from stock Xiaomi firmware. Never edit,
  hex-patch, add or replace a file here by hand.
- `Android.bp`, `Android.mk`, `BoardConfigVendor.mk` and `malachite-vendor.mk` are written
  by `setup-makefiles.py` in the device tree. Don't edit them by hand either.
- To change anything, change the device tree's `proprietary-files.txt` or the fixups in its
  `extract-files.py`, then re-extract from a stock dump:
  ```
  ./extract-files.py <stock dump> --no-cleanup --section '<exact section name>'
  ```
  Commit the device tree change and this repository's result together, and check that the
  diff here contains only the files you meant to change.
- Name the stock build you extracted from in the commit body (for example
  `OS3.0.10.0.WOOMIXM`).

## Git LFS

Large blobs are stored with Git LFS (`.gitattributes`). Keep new large files under LFS, and
make sure the LFS objects are pushed with the commit: a commit whose LFS objects are missing
breaks every checkout.

## Commits

Same format as the device tree:

```
malachite: add stock's Bluetooth session libraries for its HAL
malachite: use stock's global audio tuning set
```
