# Transferring Files To and From Your Instance

This page explains how to move data between your own computer and your MorphoCloud
instance. There are two methods — pick based on how much you're moving:

| Method | Best for | Needs |
|--------|----------|-------|
| **Guacamole side toolbar** | A few small files, quick drag-and-drop in the browser | Just the web-connect link |
| **`scp` / `sftp` / `rsync`** | Bulk data, large datasets, whole folders | A terminal (or an SFTP app) + the SSH info from your email |

> **Save into your persistent storage.** Always transfer files into
> **`/media/volume/MyData`** (or anywhere in your home directory `~`, which also
> lives on that volume). Files placed there survive `/delete_instance` + `/create`.
> Anything written elsewhere (e.g. `/tmp` or the root disk) is **lost** when the
> instance is deleted or recreated.

> **Your instance must be online**, and its address **changes every session**.
> Each time the instance comes online you receive a new credential email — always
> use the address and passphrase from the **most recent** email.

---

## Method 1 — Guacamole (in-browser, small files)

When you connect through the **Web connect** link (the Guacamole interface), a
hidden side toolbar gives you upload/download and clipboard.

1. Open the side toolbar with **`Ctrl`+`Alt`+`Shift`** (Windows/Linux) or
   **`Cmd`+`Alt`+`Shift`** (macOS). The same shortcut hides it again.
2. **Upload:** in the toolbar's **Devices** section, click the shared drive and
   use **Upload Files**, or drag files onto the panel. Uploaded files land in the
   Guacamole shared drive on the desktop.
3. **Download:** files you copy into the shared drive on the instance can be saved
   back to your computer from the same panel.
4. The toolbar also exposes a **clipboard** field for copy/paste between your
   machine and the instance.

**One file at a time.** Guacamole transfers individual files only — you **cannot
upload or download a whole folder**. To move a directory, either **zip it first**
and transfer the single archive (then unzip it on the instance), or use
**`scp`/`sftp`** (Method 2 below). Guacamole is also slow for large or numerous
files, so reserve it for a few small ones.

---

## Method 2 — `scp` / `sftp` / `rsync` (command line, bulk)

Your instance also accepts SSH connections, which is the fast way to move large
datasets or whole folders. Use the details from your credential email:

- **Host:** the instance IP shown on the **SSH** line of the email
  (`ssh exouser@<instance-ip>`)
- **Username:** `exouser`
- **Password:** the **passphrase** from the email (the same one used for the desktop)
- **Port:** default `22`

Replace `<instance-ip>` below with the IP from your most recent email.

**Copy a folder up to the instance (into persistent storage):**
```bash
scp -r ./my-dataset exouser@<instance-ip>:/media/volume/MyData/
```

**Copy results back down to your computer:**
```bash
scp -r exouser@<instance-ip>:/media/volume/MyData/results ./
```

**Interactive transfer with `sftp`:**
```bash
sftp exouser@<instance-ip>
# then, at the sftp> prompt:
#   cd /media/volume/MyData
#   put -r my-dataset      # upload
#   get -r results         # download
```

**Large or resumable transfers — use `rsync`** (re-runs only copy what changed, and
`-P` lets an interrupted transfer resume):
```bash
rsync -avP ./my-dataset exouser@<instance-ip>:/media/volume/MyData/
```

### Windows

- **Graphical:** [WinSCP](https://winscp.net) or [FileZilla](https://filezilla-project.org)
  — choose **SFTP**, Host = the instance IP, Port = `22`, Username = `exouser`,
  Password = the passphrase. Then drag files into `/media/volume/MyData`.
- **Command line:** `scp` / `sftp` work in PowerShell exactly as shown above.

---

## Tips

- **Confirm where it landed:** after a transfer, open the **MyData** shortcut on the
  instance desktop (or `ls /media/volume/MyData` over SSH) to verify your files.
- **Address changed?** If a transfer is refused, your instance probably shelved and
  came back with a new IP — grab the latest one from the newest credential email
  (or re-send it with `/email`).
- **Permissions:** you connect as `exouser`, which owns `/media/volume/MyData` and
  your home directory, so no `sudo` is needed for normal file transfers.

---

*[Back to the User Guide](README.md) | See also: [Connecting to your instance](connecting.md) ·
[Where your data is stored](data-and-storage.md)*
