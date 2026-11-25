# Your Storage (MyDrive)

Each member has one storage space, **MyDrive**: 100 GB that stays when an
instance is deleted. **There is no backup.** Keep your own copy of anything
important.

You create it once on the [portal](https://portal.morphocloud.org) with **Create
my storage**. You need it before you can create an instance.

## What is kept, and what isn't

On an instance, MyDrive is at **`/media/share/MyDrive`**. Your **Desktop**,
**Documents** and **Downloads** folders are in it.

- **Kept:** everything in Desktop, Documents, Downloads, and anywhere else in
  `/media/share/MyDrive`. It stays when the instance is shelved or deleted.
- **Lost when the instance is deleted:** everything saved anywhere else, including
  other folders in your home directory, and the Slicer extensions you install.

3D Slicer saves to Documents by default.

## On the portal

- **Open my files** uploads and downloads files at any time, with or without an
  instance. See [Transferring files](file-transfer.md).
- **Reset my storage** deletes every file and folder in your storage. It cannot be
  undone. It is available only while your instance is shelved or deleted.

## How long your storage is kept

The portal shows how much space you use and the date your storage expires
("Expires on …"); this guide calls it the end date. Storage is kept for
**120 days** from the day it is created.

- **Reminders:** we email you 14 days, 7 days and 1 day before the end date.
- **Ask to keep my storage:** from 14 days before the end date, the portal offers
  this button. Write why you need more time. A MorphoCloud admin approves or
  declines. An approval gives 120 more days, counted from the end date or from the
  day of approval, whichever is later.
- **After the end date:**
  - your instance is deleted;
  - your storage is **read-only for 15 days**. You can download your files with
    **Open my files**, but you can't upload, reset or add anything, and you can't
    create an instance;
  - **Ask to keep my storage** is still available. An approval makes your storage
    writable again.
- **After the 15 days** your storage and all its files are deleted. You can then
  create a new, empty storage.

## If you had files in MorphoCloud before November 2026

Your storage was created for you, with your files in it. Your Desktop,
Documents and Downloads are in MyDrive under the same names. Everything else from your earlier storage is in the **`MyOldData`** folder in
MyDrive. These were not copied: the old Slicer installation, R libraries, and
hidden settings folders in the home directory.

## MorphoSource Media Cart

The **MorphoSource Media Cart** card on the portal downloads the datasets in your
[MorphoSource media cart](https://www.morphosource.org/dashboard/my/cart) straight
into MyDrive, in the `MorphoSource` folder. No instance needs to be running. Each
dataset is saved as one zip file. You connect the card once with your MorphoSource
API key (on your [MorphoSource dashboard](https://www.morphosource.org/dashboard),
open Profile, then View API Key).

---

*[Back to the User Guide](README.md) | See also: [Transferring files](file-transfer.md) · [Managing your instance](instance-lifecycle.md)*
