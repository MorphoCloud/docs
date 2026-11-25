# Copying Files From Google Drive, Dropbox, Box or OneDrive

This tutorial shows how to copy your own files from a cloud storage account
(Google Drive, Dropbox, Box or OneDrive) into your storage (MyDrive), using the
free tool [rclone](https://rclone.org) on your instance.

The data moves straight from the cloud account to your instance. It does not go
through your computer.

> **Copy in only.** Everything on this page **reads** from your cloud account and
> writes to MyDrive. Nothing here changes or deletes files in your cloud account.
> rclone can also change and delete files in your cloud account, so use only the
> commands shown here. See [Commands to avoid](#commands-to-avoid).

You need:
- a running instance, opened with **Open in browser** (Web connect) or TurboVNC.
  You sign in to your cloud account in a browser on the instance, so use the
  desktop, not SSH;
- your cloud account's username and password.

rclone and its settings are saved on the instance, not in MyDrive. **When the
instance is deleted, rclone and your cloud account connection are deleted with
it.** On a new instance, repeat steps 1 to 3.

---

## Step 1 — Install rclone

On the instance desktop, open the **Terminal** app and run:

```bash
sudo apt update
sudo apt install -y rclone fuse3
```

It does not ask for a password. If apt says it is waiting for a lock, the
instance is still installing updates in the background; wait a few minutes and run
the command again.

## Step 2 — Make every mount read-only

This setting makes every rclone mount (see [Step 5](#step-5-optional--browse-your-cloud-files-as-a-folder))
read-only, even if you forget `--read-only` on the command line. Run this once:

```bash
echo 'export RCLONE_READ_ONLY=true' >> ~/.bashrc
source ~/.bashrc
```

## Step 3 — Connect your cloud account

Run:

```bash
rclone config
```

rclone asks a series of questions in the terminal. Type the answer and press
**Enter**. For each question not listed below, press **Enter** to keep the
default. The questions and their order can differ slightly between rclone
versions; read each one before answering.

| Question | Answer |
|----------|--------|
| `n) New remote` … `e/n/d/r/c/s/q>` | `n` |
| `name>` | a short name for this account, used in every command below: `gdrive`, `dropbox`, `box` or `onedrive` |
| `Storage>` | the type, as a word: `drive` (Google Drive), `dropbox`, `box` or `onedrive` |
| `client_id>` and `client_secret>` | leave empty, press **Enter** |
| `scope>` (Google Drive only) | `drive.readonly` — rclone can then only read your Google Drive |
| `Edit advanced config?` | `n` |
| `Use web browser to automatically authenticate rclone with remote?` (or `Use auto config?`) | `y` |

A browser opens **on the instance**. Sign in to your cloud account there and
press **Allow** (or **Accept**). The browser then shows *Success*; go back to the
terminal.

The last questions depend on the service:
- **Google Drive:** `Configure this as a Shared Drive (Team Drive)?` — `n` for
  your own files. Answer `y` only to copy from a Shared Drive, then pick it from
  the list.
- **OneDrive:** pick `onedrive` (OneDrive Personal or Business), then confirm the
  drive rclone finds.

Finally answer `y` to `Keep this "…" remote?`, then `q` to quit.

Only Google Drive lets rclone ask for read-only access. For Dropbox, Box and
OneDrive, the access you grant also allows changes, so use only the commands on
this page.

**Check that it works** (use the name you chose):

```bash
rclone lsd gdrive:
```

This lists the folders at the top of your cloud account.

> **University accounts:** some universities don't let members connect outside
> apps to their Google, Box or Microsoft accounts. If the sign-in page says an
> administrator must approve the app, ask your university's IT office. Until
> then, download the files to your computer and upload them with **Open my
> files** ([Transferring files](file-transfer.md)).

## Step 4 — Copy files into MyDrive

**1. Find the folder.** List the folders inside a folder:

```bash
rclone lsd gdrive:Projects
```

List the files in a folder, with sizes in bytes:

```bash
rclone ls gdrive:Projects/CT-scans
```

Folder names with spaces need quotes: `"gdrive:My Scans"`.

**2. Check the size.** MyDrive holds 100 GB. Compare the total with the free
space the portal shows:

```bash
rclone size gdrive:Projects/CT-scans
```

**3. Copy.** Copy into a **new folder** in MyDrive. The cloud account always
comes **first**, MyDrive **second**:

```bash
rclone copy gdrive:Projects/CT-scans /media/share/MyDrive/FromCloud/CT-scans -P
```

- `-P` shows progress. Large copies take time; keep the terminal open.
- Folders that don't exist yet in MyDrive are created.
- **If the copy stops** (closed terminal, lost connection), run the same command
  again. rclone copies only the files that are missing or different, and skips
  the ones already done.
- **Running it again replaces** files in the destination folder that differ
  from the cloud copy. Don't edit files inside that folder; save your work
  somewhere else in MyDrive.
- To see what would be copied without copying anything, add `--dry-run`.

To copy a single file, use `copyto` with the file name on both sides:

```bash
rclone copyto gdrive:Projects/skull.nrrd /media/share/MyDrive/FromCloud/skull.nrrd -P
```

When the copy finishes, the files are in **`/media/share/MyDrive/FromCloud`** on
the instance, and in **Open my files** on the portal.

## Step 5 (optional) — Browse your cloud files as a folder

To look through your cloud files in the Files app or in 3D Slicer before deciding
what to copy, mount the account as a **read-only** folder:

```bash
mkdir -p ~/CloudDrives/gdrive
rclone mount gdrive: ~/CloudDrives/gdrive --read-only
```

- Keep this terminal open; the folder works while the command runs.
- Open **Home → CloudDrives → gdrive** in the Files app. You can open and copy
  files, but you can't change, rename or delete them.
- Opening a file reads it from the cloud each time, so large files are slow. To
  work on a file, copy it into MyDrive with `rclone copy` (Step 4); that is
  faster and resumes after an interruption.
- **To stop:** press **Ctrl+C** in that terminal. If the folder still shows an
  error afterward, run `fusermount3 -u ~/CloudDrives/gdrive`.
- Stop the mount before you shelve the instance.

Keep the mount folder in your home directory, as shown, not inside MyDrive.

---

## Commands to avoid

These commands **change or delete files in your cloud account** or in MyDrive.
This tutorial does not use them:

| Command | What it does |
|---------|--------------|
| `rclone sync` | makes the destination match the source, **deleting** files in the destination that aren't in the source |
| `rclone move`, `rclone moveto` | copies, then **deletes** the original in your cloud account |
| `rclone delete`, `rclone deletefile`, `rclone purge`, `rclone rmdir`, `rclone rmdirs` | **deletes** files or folders |
| `rclone copy /media/share/MyDrive/… gdrive:…` | the cloud account second = copies **into** your cloud account and can **replace** files there |
| `rclone mount` without `--read-only` | a folder where changes and deletions go straight to your cloud account |

---

## Disconnect your cloud account

To remove the connection from the instance (use the name you chose):

```bash
rclone config delete gdrive
```

Deleting the instance also removes it. To revoke rclone's access completely, also
remove **rclone** from the connected apps in your cloud account's security
settings.

---

*[Back to the User Guide](README.md) | See also: [Transferring files](file-transfer.md) ·
[Your storage (MyDrive)](data-and-storage.md)*
