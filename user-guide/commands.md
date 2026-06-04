# Commands

Post any of the following as a comment on your instance issue. **One command per
comment.**

## Individual instances

| Command | What it does |
|---------|-------------|
| `/create` | Provision the instance and volume |
| `/shelve` | Shelve the instance (preserves data) |
| `/unshelve` | Resume a shelved instance |
| `/email` | Re-send the connection URL to your email |
| `/renew` | Extend the instance lifespan (if renewal is available) |
| `/delete_instance` | Permanently delete the instance (volume kept) |
| `/delete_volume` | Permanently delete the data volume (instance kept) |
| `/delete_all` | Permanently delete both instance and volume |

## Course instances

Same as above **except `/renew`** — course instances expire on the fixed course
schedule and cannot be renewed.

## Workshop instances

Workshop instances are **managed in bulk by the workshop organizer**, not by
individual participants. The organizer provisions instances for everyone from the
workshop request issue and distributes the credentials; participants simply connect
to the instance they're given and do not run `/` commands themselves.

## Changing instance flavor

You can't change a flavor in place. Tag `@MorphoCloud/morphocloud-admins` in a
comment on your issue; an admin deletes the current instance (your data volume is
untouched), updates the flavor label, and you `/create` again. See
[GPU notes & known issues](gpu-and-known-issues.md) for choosing a flavor.

---

*[Back to the User Guide](README.md) | See also: [Instance lifecycle](instance-lifecycle.md) · [Where your data is stored](data-and-storage.md)*
