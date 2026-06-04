# Requesting and Creating Your Instance

Once you've accepted your GitHub organization invitation, requesting and using an
instance is the same for all access types.

1. Open a new issue in the [Instances repository](https://github.com/MorphoCloud/Instances/issues/new/choose) using the **Instance Request** template (individual users).
2. An automatic validation check runs on your issue. **Opening the issue does not provision anything** — once the check posts a ✅ confirmation comment, post `/create` as a comment to provision your instance.
3. When your instance is online you'll receive an email with the connection URL and credentials. See [Connecting](connecting.md).

> **Workshop participants** do not open individual issues — the workshop organizer provisions instances for everyone and distributes the credentials.

**Concurrent-instance limit:** an organization member can have at most **two** instances at once — e.g. two personal instances, or one course and one personal instance.

**Resource availability:** JetStream2 is a shared national resource, so `/create` (and `/unshelve`) can wait when a flavor is at capacity. Check [real-time availability](https://morphocloud.org) before you start. See [GPU notes & known issues](gpu-and-known-issues.md).

---

*[Back to the User Guide](README.md) | Next: [Connecting to your instance](connecting.md)*
