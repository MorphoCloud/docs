# Where Your Data Is Stored

Every instance includes a persistent **MyData** volume (100 GB). The instance user's
**entire home directory (`~exouser`) is mapped onto this volume**, mounted at
**`/media/volume/MyData`** — so everything under your home (Desktop, Documents,
Downloads, and every other folder) lives on persistent storage.

## What persists, and what doesn't

- **Persists:** anything in your home directory or `/media/volume/MyData`. It
  survives a `/delete_instance` + `/create` cycle and remains while the instance is
  shelved or deleted.
- **Does *not* persist:** files written outside your home directory (e.g. `/tmp` or
  the root disk). The instance's root disk is **ephemeral** — treat it as scratch space.

The MyData volume is independent of the instance: it stays until you explicitly
remove it with `/delete_volume` or `/delete_all`.

> **Always save into your home directory or `/media/volume/MyData`.** Then deleting
> and recreating your instance never loses your work.

---

*[Back to the User Guide](README.md) | See also: [Transferring files](file-transfer.md) · [Commands](commands.md)*
