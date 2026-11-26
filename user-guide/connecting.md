# Connecting to Your Instance

When your instance is ready, its card on the
[portal](https://portal.morphocloud.org) shows the access details:

- **Web connect:** press **Open in browser** to open the desktop in your browser.
- **SSH:** `ssh exouser@<address>`
- **TurboVNC:** `<address>:1`
- **Username:** `exouser`
- **Passphrase:** press **Show** to see it. The whole phrase, spaces included, is
  the passphrase.

The address changes every time the instance is unshelved. Always use the one on
the card.

## Option 1 — Web connect (in the browser)

Press **Open in browser** on the card. No software to install. Web connect signs
you in by itself; if it shows a sign-in page instead, the desktop was not ready
yet: sign in with `exouser` and the passphrase.

The desktop shows **3D Slicer** and your **Home** folder in its top-left corner.

**Copy and paste** between your computer and the desktop works in **Chrome** and
**Edge**. The first time, the browser asks whether the site may use the
clipboard; press **Allow**. Copy and paste does not work in **Firefox** or
**Safari**; there, use TurboVNC (below) when you need it.

*Limitations:* font and display scaling can be imprecise. To move files, use
**Open my files** on the portal ([Transferring files](file-transfer.md)).

## Option 2 — TurboVNC (recommended for visualization)

Download and install [TurboVNC](https://github.com/TurboVNC/turbovnc/releases)
(expand **Assets** and pick the package for your OS); the **TurboVNC** link on the
card opens the same page. Connect to the TurboVNC address on the card
(`<address>:1`) with the passphrase.

*Benefits:* better image quality and responsiveness, and native
copy/paste.

## SSH

Connect with `ssh exouser@<address>` and the passphrase. You can also copy
files over SSH with `scp`, `sftp` or `rsync`; see
[Transferring files](file-transfer.md).

> **Save your work** in Desktop, Documents or Downloads. These folders are in your
> storage and are kept when the instance is deleted. See
> [Your storage](data-and-storage.md).

---

*[Back to the User Guide](README.md) | See also: [Transferring files](file-transfer.md)*
