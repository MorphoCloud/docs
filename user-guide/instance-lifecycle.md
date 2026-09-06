# Instance Lifecycle

## States

| State | Meaning |
|-------|---------|
| **Running** | Active and accessible via the connection URL |
| **Shelved** | Paused and not consuming compute resources; your data is preserved |
| **Deleted** | Instance and/or volume permanently removed |

## Automatic shelving

For **individual and course instances**, once online the instance stays active for a
set number of hours — **4 by default**, and larger flavors are shorter. Course
instructors can set a different limit for their own course. A reminder popup appears
on the desktop 30 minutes before the limit; if you dismiss it or don't respond, the
instance shelves itself. You can extend at any time by clicking the
session-extension icon on the desktop, which restarts the full countdown. Resume any
time with `/unshelve` — your data is intact, though running applications are closed.

**Workshop instances** stay online for the duration of the workshop and are not
subject to this auto-shelving policy.

**Closing your request issue** does not delete anything: if your instance is
running it is shelved (data and volume preserved), and a comment explains how
to continue. Reopen the issue and comment `/unshelve` to resume, or comment
`/delete_all` to release the instance and volume permanently.

## Expiration

Each instance has an expiration label (e.g. `expiration:60d`) applied when it is
created. As the date approaches:

- **Individual** users receive a renewal notification and can use `/renew` to extend
  the instance — once, up to the maximum lifespan.
- **Course** instances expire a fixed number of days after the request issue was
  opened — **120 by default** — independently of your course end date, and cannot
  be renewed.
- **Workshop** instances expire on the workshop schedule and cannot be renewed.
- At expiration the instance **and its MyData volume are both deleted immediately** —
  there is no grace period and no shelved intermediate state. Save anything you need
  off the instance before then.

> Availability on JetStream2 varies — check
> [real-time availability](https://morphocloud.org)
> before `/create` or `/unshelve`. See [GPU notes & known issues](gpu-and-known-issues.md).

---

*[Back to the User Guide](README.md) | See also: [Commands](commands.md) · [Where your data is stored](data-and-storage.md)*
