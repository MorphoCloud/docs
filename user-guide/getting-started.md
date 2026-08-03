# Requesting and Creating Your Instance

Once you've accepted your GitHub invitations, the commands are the same for everyone —
but **where you open your issue depends on how you got access.**

- **Individual users** — open a new issue in the [Instances repository](https://github.com/MorphoCloud/Instances/issues/new/choose) using the **Instance Request** template.
- **Course students** — open a new issue in **your own course repository** (`MC-<course-id>`, the private repo your instructor invited you to) using the **Course Instance Request** template. Don't open issues in the Instances repository.
- **Workshop participants** — don't open issues at all; the workshop organizer provisions instances for everyone and distributes the credentials.

Then, in whichever repository applies to you:

1. An automatic validation check runs on your issue. **Opening the issue does not provision anything** — once the check posts a ✅ confirmation comment, post `/create` as a comment to provision your instance.
2. When your instance is online you'll receive an email with the connection URL and credentials. See [Connecting](connecting.md).

**Concurrent-instance limit:** you may hold **two** instances at once in the Instances repository, and **one** in a course repository.

**Resource availability:** JetStream2 is a shared national resource, so `/create` (and `/unshelve`) can wait when a flavor is at capacity. Check [real-time availability](https://morphocloud.org) before you start. See [GPU notes & known issues](gpu-and-known-issues.md).

---

*[Back to the User Guide](README.md) | Next: [Connecting to your instance](connecting.md)*
