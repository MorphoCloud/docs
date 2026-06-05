# MorphoCloud User Guide

Already have a MorphoCloud instance? This guide covers day-to-day use. New here, or
want to know what MorphoCloud is and how to get access? Start with the
[overview](../README.md).

## Getting started
- [Requesting and creating your instance](getting-started.md) — open an issue, run `/create`, get your credentials.

## Using your instance
- [Connecting](connecting.md) — web browser (Guacamole) vs. the TurboVNC client.
- [Transferring files](file-transfer.md) — Guacamole drag-and-drop, and `scp`/`sftp`/`rsync` for bulk data.
- [Where your data is stored](data-and-storage.md) — 100 GB persistent user storage.

## Managing your instance
- [Commands](commands.md) — `/create`, `/shelve`, `/unshelve`, `/renew`, delete, and more.
- [Instance lifecycle](instance-lifecycle.md) — running, shelving, expiration, renewal.

## Reference
- [Choosing & changing a GPU flavor](gpu-and-known-issues.md) — pick the right GPU instance, and switch flavor without losing your data.

## Known issues
- [Large-volume rendering on GPU instances](gpu-and-known-issues.md#large-volume-rendering-stalls-gpu-instances--4096-voxels) — 3D Slicer stalls when volume-rendering a volume ≥ 4096 voxels on any axis.
- [Availability can block creating or unshelving](gpu-and-known-issues.md#availability-can-block-creating-or-unshelving) — JetStream2 is shared, so scarce flavors (especially g3.xl) can fail to start.

## Need help?
Email [portal@morphocloud.org](mailto:portal@morphocloud.org), or tag
`@MorphoCloud/morphocloud-admins` in a comment on your instance issue.
