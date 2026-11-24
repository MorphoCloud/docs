# Managing Your Instance

You manage your instance with the buttons on its card on the
[portal](https://portal.morphocloud.org). You have one instance at a time, and your
storage must exist before you create it.

## States

| State | Meaning |
|-------|---------|
| **Running** | Active; the card shows the access details |
| **Shelved** | Stopped and kept; your files are safe |
| **Unreachable** | Running, but not answering on the network (see below) |

## Shelve and Unshelve

- **Shelve** stops the instance and keeps it. Shelve it when you are done for the
  day.
- **Unshelve** starts it again. The address changes; the card shows the new one.

Every Unshelve, like every Create, needs a free machine of that type on JetStream2.
The line at the top of the portal shows how many are free.

## Sessions

A running instance shelves itself when its session ends.

- A session is **4 hours**, or **2 hours** on `g3.xl`, `g4.xl`, `r3.large` and
  `r3.xl`.
- The card counts down to it ("Shelves automatically in …").
- To start a new session, press **Extend session** on the card, or **Yes** on the
  reminder that appears on the instance's desktop.
- Unshelve starts a new session.

Running programs are closed when the instance shelves. Save your work in
Desktop, Documents or Downloads.

## Unreachable

"Unreachable" on the card means the instance is running but not answering. The
way out is **Shelve**, then **Unshelve**. After about 30 minutes the portal shelves
it automatically.

## Delete

**Delete** removes the instance. Your storage is not affected; anything saved
only on the instance is lost. You can create a new instance at any time.

**To change the instance type:** Delete, then Create with the new type. Your
storage comes back on the new instance. See
[choosing a type](gpu-and-known-issues.md#how-to-choose-a-gpu-instance).

## Automatic deletion

- **Shelved for more than 28 days:** the instance is deleted, in a weekly run.
  Your files in MyDrive are safe, and you can create a new instance at any time.
- **End of your storage term:** the instance is deleted. See
  [how long your storage is kept](data-and-storage.md#how-long-your-storage-is-kept).

## Workshop instances

Workshop instances stay online for the duration of the workshop and are not
shelved after a session.

---

*[Back to the User Guide](README.md) | See also: [Your storage](data-and-storage.md) · [Connecting](connecting.md)*
