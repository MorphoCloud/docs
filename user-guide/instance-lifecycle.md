# Instance Lifecycle

## States

| State | Meaning |
|-------|---------|
| **Running** | Active and accessible via the connection URL |
| **Shelved** | Paused and not consuming compute resources; your data is preserved |
| **Deleted** | Instance and/or volume permanently removed |

## Automatic shelving

For **individual and course instances**, once online the instance stays active for
**4 hours**. As the limit approaches, a reminder popup appears on the desktop — if
you dismiss it or don't respond, the instance shelves itself. You can extend at any
time by clicking the session-extension icon on the desktop, which resets the 4-hour
countdown. Resume any time with `/unshelve` — your data is intact, though running
applications are closed.

**Workshop instances** stay online continuously for the duration of the workshop
and are not subject to the 4-hour auto-shelving policy.

## Expiration

Each instance has an expiration label (e.g. `expiration:60d`) applied when it is
created. As the date approaches:

- **Individual** users receive a renewal notification and can use `/renew` to extend
  the instance — once, up to the maximum lifespan.
- **Course and workshop** instances expire on the schedule set at registration and
  cannot be renewed.
- After expiration the instance is shelved, then deleted after a grace period.

> Availability on JetStream2 varies — check
> [real-time availability](https://morphocloud.org)
> before `/create` or `/unshelve`. See [GPU notes & known issues](gpu-and-known-issues.md).

---

*[Back to the User Guide](README.md) | See also: [Commands](commands.md) · [Where your data is stored](data-and-storage.md)*
