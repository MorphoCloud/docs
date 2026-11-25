# MorphoCloud

## What is MorphoCloud?

MorphoCloud provides on-demand, high-performance cloud computing instances to support computational morphology, 3D morphometrics, and biomedical imaging research. Instances run on [JetStream2](https://jetstream-cloud.org/), a national research cloud operated by Indiana University and funded through [ACCESS](https://access-ci.org/). Each instance comes pre-loaded with [3D Slicer](https://download.slicer.org/), [SlicerMorph](https://slicermorph.org/), and a suite of additional tools (see [Installed Software](#installed-software) below), and is accessible from any web browser — no local installation required.

You manage your instance and your files on the MorphoCloud portal, [portal.morphocloud.org](https://portal.morphocloud.org). To join you need an [ORCID iD](https://orcid.org) (free to create) and a [GitHub account](https://github.com), and you must agree to the [Usage Terms](./terms.MD).

> **Important:** MorphoCloud membership lets you request instances, but does not guarantee that compute resources are available at any given time. Instances run on [JetStream2](https://jetstream-cloud.org/), a nationally shared research cloud, and GPU machines are often scarce. The line at the top of the [portal](https://portal.morphocloud.org) shows how many machines of each type are free; check it before you create or unshelve an instance.

---

## Access Pathways

MorphoCloud has three access pathways depending on how you will use it.

### 1. Individual Access

For researchers and students who want a personal instance for their own work.

**How to get access:**
1. On [morphocloud.org](https://morphocloud.org), click **New user? Join →**. It opens [join.morphocloud.org](https://join.morphocloud.org).
2. Click **Sign in with ORCID**. After ORCID, sign in with GitHub. Both sign-ins are required.
3. Fill in the form and press **Submit**.
4. Click the verification link in the email we send you. This sends your GitHub invitation.
5. Sign in to the [portal](https://portal.morphocloud.org) with GitHub. The portal shows your invitation; accept it, and the portal opens your dashboard.

The [Getting started](./user-guide/getting-started.md) page has every step in detail.

---

### 2. Workshop Access

For instructors or organizers running a short workshop (5 days max) where all participants need simultaneous access.

**How to get access:**
1. The workshop organizer, who must already be a MorphoCloud member, clicks **MorphoCloud in Workshops →** on [morphocloud.org](https://morphocloud.org). It opens [join.morphocloud.org/workshop](https://join.morphocloud.org/workshop). There they sign in with their [ORCID iD](https://orcid.org) and are added to the **MorphoCloudWorkshopOrganizers** team on GitHub.
2. The organizer opens a **Workshop Request** issue in the [MorphoCloud Instances repository](https://github.com/MorphoCloud/Instances/issues/new/choose) and fills in the workshop details (dates, number of participants).
3. Once the MorphoCloud team approves the request, instances are provisioned for each participant — the organizer receives all connection credentials by email and is responsible for distributing them to participants.

**Instance lifespan:** Set per workshop by the MorphoCloud team.

---

### 3. Use MorphoCloud For an Academic Course

This is for instructors who want their students to use MorphoCloud routinely as part of their course. The course is set up as a dedicated and private repository only accessible to instructor(s) and the students they invite. Repository is removed 30 days after the course concludes. Instructors can tailor the platform to better align with specific course objectives and actively maintain the course enrollment.

If you are interested, please [review the instructions](./instructor/README.md).
Questions? Contact us at [portal@morphocloud.org](mailto:portal@morphocloud.org).

---

## Using MorphoCloud

Once you have joined, the **[User Guide](./user-guide/)** covers day-to-day use:

- **[Getting started](./user-guide/getting-started.md)** — sign in to the portal, create your storage and your instance.
- **[Connecting](./user-guide/connecting.md)** — Web connect in the browser, TurboVNC, and SSH.
- **[Your storage (MyDrive)](./user-guide/data-and-storage.md)** — what is kept, how long, and the MorphoSource Media Cart.
- **[Transferring files](./user-guide/file-transfer.md)** — Open my files on the portal, and `scp`/`sftp`/`rsync` for bulk data.
- **[Copying from cloud storage](./user-guide/cloud-storage-rclone.md)** — copy your files from Google Drive, Dropbox, Box or OneDrive into MyDrive with rclone.
- **[Managing your instance](./user-guide/instance-lifecycle.md)** — Shelve, Unshelve, sessions, Delete, and changing the instance type.
- **[GPU notes & known issues](./user-guide/gpu-and-known-issues.md)** — choosing an instance type, and known problems.

Instructors setting up a course should follow the **[instructor guide](./instructor/README.md)**.

---

## Instance Types

Your files are kept in your storage, **MyDrive** (100 GB, no backup), not on the instance. On an instance, MyDrive is at `/media/share/MyDrive`, and your Desktop, Documents and Downloads folders are in it. Everything in MyDrive is kept when the instance is deleted; anything saved anywhere else is lost with the instance ([details](./user-guide/data-and-storage.md)).

| Type | RAM | CPUs | GPU | Best for |
|--------|----:|-----:|-----|----------|
| `g3.medium` | 30 GB | 8 | A100 (¼, 10 GB) | Datasets up to about 3 GB. Often free when `g3.large` is not |
| `g3.large` | 60 GB | 16 | A100 (½, 20 GB) | **Default.** Most 3D Slicer / SlicerMorph workflows |
| `g4.xl` | 120 GB | 12 | L40S (48 GB) | When you need **more GPU memory or RAM** than g3.large (fewer vCPUs, slower than a full A100) |
| `g3.xl` | 120 GB | 32 | A100 (full, 40 GB) | **Heaviest / fastest GPU work** — full A100, ~2× g4.xl |
| `m3.xl` | 125 GB | 32 | — | Computationally intensive tasks that don't require a GPU (e.g., image registration with ANTsPy) |
| `r3.large` | 500 GB | 64 | — | Image registration with large datasets. Only for members of the large-memory team |
| `r3.xl` | 1000 GB | 128 | — | Image registration with very large datasets. Only for members of the large-memory team |

**When in doubt, start with `g3.large`.** It is the default type and covers the majority of SlicerMorph workflows. Move up only if you encounter memory or compute limits — see [GPU notes & known issues](./user-guide/gpu-and-known-issues.md) for which type to pick.

> **Note on GPU instances:** Performance of 3D Slicer (especially volume rendering) degrades significantly on GPU instances when any dimension of the volume is ≥ 4096 voxels. For such large volumes, consider `m3.xl` or a large-memory type instead — see [GPU notes & known issues](./user-guide/gpu-and-known-issues.md).

---

## Installed Software

| Software | Details |
|----------|---------|
| 3D Slicer | v5.12.4 |
| SlicerMorph | ImageStacks, GPA, ALPACA, and other morphometrics tools |
| DeCA | Morphometrics via dense correspondence analysis |
| Photogrammetry | Generate textured 3D models from photographs |
| MorphoDepot | Collaborative segmentation and data sharing |
| MEMOs | AI-based organ segmentation for E15 mouse embryos |
| NNInteractive | AI-assisted interactive segmentation |
| PyTorch | GPU-accelerated tensor library for AI tools |
| R / RStudio | Provided by JetStream2 |
| Python 3 | Provided by JetStream2 |

---

## Getting Help

- **MorphoCloud Chatbot:** on the [portal](https://portal.morphocloud.org). It answers questions about MorphoCloud, your instance and 3D Slicer. Its **Send to the MorphoCloud team** button sends the conversation to the team.
- **Email:** [portal@morphocloud.org](mailto:portal@morphocloud.org).
- **Community:** [MorphoCloud Discussions](https://github.com/orgs/MorphoCloud/discussions), for members only: sign in to GitHub first, or the page shows 404. Ask in **Q&A**, and watch **Announcements** for service updates.

MorphoCloud's emails come from **no-reply@morphocloud.org**; add it to your safe senders.

---

## Funding & Acknowledgment

MorphoCloud is supported by the National Science Foundation (DBI/2301405) and the National Institutes of Health (NICHD/HD104435). Infrastructure is provided by JetStream2 (OAC/2005506) and Exosphere (TI/2229642).

If you use MorphoCloud for your research, please cite the platform article and include the following acknowledgment statement.

**Citation:**

> Maga AM and Fillion-Robin J-C. MorphoCloud: Democratizing Access to High-Performance Computing for Morphological Data Analysis. *F1000Research* 2026, **15**:53. https://doi.org/10.12688/f1000research.176328.1

**Acknowledgment statement:**

> This study relied on cyberinfrastructure supported by grants from the National Science Foundation (MorphoCloud: DBI/2301405; JetStream2: OAC/2005506; Exosphere: TI/2229642) and the National Institutes of Health (MorphoCloud: NICHD HD104435).
