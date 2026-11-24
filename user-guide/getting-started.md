# Getting Started

Once you have accepted your GitHub organization invitation (see
[how to join](../README.md#1-individual-access)), everything happens on the portal.

1. **Sign in.** Go to [portal.morphocloud.org](https://portal.morphocloud.org)
   and sign in with GitHub. The first time, GitHub asks you to authorize the
   **MorphoCloud Portal** app; press **Authorize**.
2. **Create your storage.** Press **Create my storage**. You do this once. Your
   storage, MyDrive, holds 100 GB and stays when an instance is deleted. See
   [Your storage](data-and-storage.md). If you were a member before
   November 2026, your storage already exists.
3. **Create your instance.** Choose an instance type and press **Create
   instance**. We advise the default, `g3.large`; see
   [choosing a type](gpu-and-known-issues.md#how-to-choose-a-gpu-instance).
   - When a machine of that type is free, the instance is ready in 5 to 10
     minutes. When other requests are queued ahead, it takes longer.
   - The card shows the setup steps, and an email tells you when the instance is
     ready.
4. **Connect.** The card shows the access details. See [Connecting](connecting.md).

You have one instance at a time. You use only the portal's buttons; you don't
type commands on GitHub.

**Resource availability:** JetStream2 is a shared national resource, so Create
and Unshelve can wait or fail when no machine of that type is free. The line at
the top of the portal shows how many machines of each type are free. See
[GPU notes & known issues](gpu-and-known-issues.md#availability-can-block-creating-or-unshelving).

> **Workshop participants** don't create instances: the workshop organizer
> gives you the connection details.

---

*[Back to the User Guide](README.md) | Next: [Connecting to your instance](connecting.md)*
