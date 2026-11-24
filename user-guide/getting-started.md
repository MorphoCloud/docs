# Getting Started

Everything starts at [morphocloud.org](https://morphocloud.org).

## Join MorphoCloud (new members)

You need an [ORCID iD](https://orcid.org/register) and a
[GitHub account](https://github.com/signup). Both are free.

1. On [morphocloud.org](https://morphocloud.org), click **New user? Join →**. It
   opens [join.morphocloud.org](https://join.morphocloud.org).
2. Click **Sign in with ORCID**. After ORCID, GitHub asks you to sign in too:
   choose the GitHub account you will use for MorphoCloud. Both sign-ins are
   required.
3. Fill in the form:
   - your email address, twice;
   - your institution's full name, without abbreviations;
   - your career stage, what you will use MorphoCloud for, and a short
     description of your project (at least 20 characters);
   - tick the two boxes: the ORCID iD and GitHub account are your own, and you
     agree to the [Terms of Use](../terms.MD).

   Then press **Submit**.
4. Open the email from no-reply@morphocloud.org and click the verification link.
   The link expires after 7 days. Clicking it sends your invitation to the
   MorphoCloud organization on GitHub.
5. On the page that opens, click **Sign in to the portal**, then **Sign in with
   GitHub**. The portal shows your invitation: click **Accept the invitation**
   and accept it on GitHub. The portal page then opens your dashboard by itself.
   Invitations expire after 7 days. If yours has, sign in at
   [join.morphocloud.org](https://join.morphocloud.org) again to get a new one.

After you accept the invitation, a welcome email arrives from
no-reply@morphocloud.org.

Each ORCID iD can be registered with one GitHub account, and each GitHub account
with one ORCID iD.

## Sign in (members)

Click **Go to the portal** on [morphocloud.org](https://morphocloud.org), or go to
[portal.morphocloud.org](https://portal.morphocloud.org), and click **Sign in with
GitHub**. The first time, GitHub asks you to authorize the **MorphoCloud Portal**
app; press **Authorize**.

You don't register again. If the portal says your account is not in the group
yet, click **Continue at join** and sign in with ORCID and GitHub.

## Your first steps on the portal

1. **Storage.** If you had files in MorphoCloud before November 2026, your
   storage is already there, with your files (see
   [Your storage](data-and-storage.md)). Otherwise press **Create my storage**;
   it takes one to two minutes. You do this once.
2. **Instance.** Choose an instance type and press **Create instance**. We advise
   the default, `g3.large`; see
   [choosing a type](gpu-and-known-issues.md#how-to-choose-a-gpu-instance).
   - The portal first checks your request (usually a minute or two). Creating
     the instance then usually takes about 10 minutes, sometimes 20 minutes or
     more, and longer when other requests are queued ahead.
   - The card shows the setup steps, and an email tells you when the instance is
     ready.
3. **Connect.** The card shows the access details. See [Connecting](connecting.md).

You have one instance at a time. You use only the portal's buttons; you don't
type commands on GitHub.

**Resource availability:** JetStream2 is a shared national resource, so Create
and Unshelve can wait or fail when no machine of that type is free. The line at
the top of the portal shows how many machines of each type are free. See
[GPU notes & known issues](gpu-and-known-issues.md#availability-can-block-creating-or-unshelving).

> **Workshop participants** don't join or create instances: the workshop
> organizer gives you the connection details.

---

*[Back to the User Guide](README.md) | Next: [Connecting to your instance](connecting.md)*
