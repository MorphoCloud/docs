# MorphoCloud User Guide

This guide covers day-to-day use of MorphoCloud. New here, or want to know what
MorphoCloud is and how to join? Start with the [overview](../README.md).

Everything happens on the portal: [portal.morphocloud.org](https://portal.morphocloud.org).

## Getting started
- [Your first steps](getting-started.md) — sign in to the portal, create your storage and your instance.

## Using your instance
- [Connecting](connecting.md) — Web connect in the browser, TurboVNC, and SSH.
- [Your storage (MyDrive)](data-and-storage.md) — 100 GB that stays when an instance is deleted, how long it is kept, and the MorphoSource Media Cart.
- [Transferring files](file-transfer.md) — Open my files on the portal, and `scp`/`sftp`/`rsync` for bulk data.
- [Copying from cloud storage](cloud-storage-rclone.md) — copy your files from Google Drive, Dropbox, Box or OneDrive into MyDrive with rclone.

## Managing your instance
- [Managing your instance](instance-lifecycle.md) — Shelve, Unshelve, sessions, Delete, and changing the instance type.

## Reference
- [Choosing & changing an instance type](gpu-and-known-issues.md) — pick the right GPU instance, and switch type without losing your files.

## Known issues
- [Large-volume rendering on GPU instances](gpu-and-known-issues.md#large-volume-rendering-stalls-gpu-instances--4096-voxels) — 3D Slicer stalls when volume-rendering a volume ≥ 4096 voxels on any axis.
- [Availability can block creating or unshelving](gpu-and-known-issues.md#availability-can-block-creating-or-unshelving) — JetStream2 is shared, so scarce types (especially g3.xl) can fail to start.

## Need help?
Ask the **MorphoCloud Chatbot** on the [portal](https://portal.morphocloud.org);
its **Send to the MorphoCloud team** button sends the conversation to the team.
You can also email [portal@morphocloud.org](mailto:portal@morphocloud.org) or ask
in [MorphoCloud Discussions](https://github.com/orgs/MorphoCloud/discussions) (members only: sign in to
GitHub first).
