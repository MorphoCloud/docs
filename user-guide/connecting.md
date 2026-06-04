# Connecting to Your Instance

When your instance is ready you receive an email with connection credentials.
**Each time your instance comes back online after shelving, a new email is sent —
the connection addresses can change between sessions**, so always use the most
recent email. Lost it? Post `/email` on your issue to resend it.

You have two ways to reach the graphical desktop; most people use both.

## Option 1 — Web browser (Guacamole)

Click the **Web connect** link in the email. No software to install. Guacamole
provides a side toolbar (`Ctrl`/`Cmd`+`Alt`+`Shift`) for clipboard access and
[file transfers](file-transfer.md). The desktop includes shortcuts to 3D Slicer,
SlicerMorph, and your MyData storage, plus a right-click menu for display and
resolution settings.

*Limitations:* font and display scaling can be imprecise, and the clipboard is
cumbersome to use.

## Option 2 — TurboVNC (recommended for visualization)

Download and install [TurboVNC](https://github.com/TurboVNC/turbovnc/releases/tag/3.2.1)
(expand **Assets** and pick the package for your OS). Connect using the **VNC
address** and passphrase from the credentials email. The passphrase is the same one
used for the web (Guacamole) connection.

*Benefits:* much better image quality, proper display scaling, and native
copy/paste. *Limitation:* no file transfer — use Guacamole or `scp` for that.

**Best practice:** use both in tandem — Guacamole for file transfers, TurboVNC for
interactive 3D visualization.

> **Save your work** inside your home directory (Desktop, Documents, Downloads, or
> anywhere under `~`) or in `/media/volume/MyData`. See
> [Where your data is stored](data-and-storage.md).

---

*[Back to the User Guide](README.md) | See also: [Transferring files](file-transfer.md)*
