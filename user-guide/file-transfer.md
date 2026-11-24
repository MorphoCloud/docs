# Transferring Files To and From Your Storage

There are two ways to move files between your computer and your storage (MyDrive):

| Method | Best for | Needs |
|--------|----------|-------|
| **Open my files** on the portal | Most uploads and downloads, with or without an instance | A web browser |
| **`scp` / `sftp` / `rsync`** | Bulk data, very large datasets | A running instance, a terminal (or an SFTP app), and the SSH details on the card |

To bring in datasets from MorphoSource, use the
[MorphoSource Media Cart](data-and-storage.md#morphosource-media-cart).

---

## Method 1 — Open my files (on the portal)

1. On the [portal](https://portal.morphocloud.org), press **Open my files**.
2. **Upload:** drag files or folders onto the page. If an upload is interrupted,
   drop the same files again and it resumes.
3. **Download:** open a folder and click a file.
4. You can also rename, move and delete files and folders on this page.

This works at any time, whether or not your instance is running. There is no
search.

---

## Method 2 — `scp` / `sftp` / `rsync` (command line, bulk)

Your instance accepts SSH connections, which is the fast way to move large
datasets. Use the details on your instance's card:

- **Host:** the address on the **SSH** line (`ssh exouser@<address>`)
- **Username:** `exouser`
- **Password:** the **passphrase** on the card
- **Port:** default `22`

The address changes every time the instance is unshelved; use the one on the card.
Always copy into **`/media/share/MyDrive`** (or Desktop, Documents or Downloads,
which are in it). Anything written elsewhere is lost when the instance is deleted.

**Copy a folder up to your storage:**
```bash
scp -r ./my-dataset exouser@<address>:/media/share/MyDrive/
```

**Copy results back down to your computer:**
```bash
scp -r exouser@<address>:/media/share/MyDrive/results ./
```

**Interactive transfer with `sftp`:**
```bash
sftp exouser@<address>
# then, at the sftp> prompt:
#   cd /media/share/MyDrive
#   put -r my-dataset      # upload
#   get -r results         # download
```

**Large or resumable transfers — use `rsync`** (re-runs only copy what changed, and
`-P` lets an interrupted transfer resume):
```bash
rsync -avP ./my-dataset exouser@<address>:/media/share/MyDrive/
```

### Windows

- **Graphical:** [WinSCP](https://winscp.net) or [FileZilla](https://filezilla-project.org)
  — choose **SFTP**, Host = the address, Port = `22`, Username = `exouser`,
  Password = the passphrase. Then drag files into `/media/share/MyDrive`.
- **Command line:** `scp` / `sftp` work in PowerShell exactly as shown above.

---

## Tips

- **Confirm where it landed:** look in **Open my files** on the portal, or run
  `ls /media/share/MyDrive` over SSH.
- **Connection refused?** The instance may be shelved, or it was unshelved and
  has a new address. Check the card.

---

*[Back to the User Guide](README.md) | See also: [Connecting to your instance](connecting.md) ·
[Your storage](data-and-storage.md)*
