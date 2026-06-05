# MorphoCloud

## What is MorphoCloud?

MorphoCloud provides on-demand, high-performance cloud computing instances to support computational morphology, 3D morphometrics, and biomedical imaging research. Instances run on [JetStream2](https://jetstream-cloud.org/), a national research cloud operated by Indiana University and funded through [ACCESS](https://access-ci.org/). Each instance comes pre-loaded with [3D Slicer](https://download.slicer.org/), [SlicerMorph](https://slicermorph.org/), and a suite of additional tools (see [Installed Software](#installed-software) below), and is accessible from any web browser — no local installation required.

Instances are managed entirely through GitHub Issues. You request, control, and monitor your instance by opening an issue and posting commands as comments. To get started you'll need an [ORCID iD](https://orcid.org) (free to create), a [GitHub account](https://github.com), and you must agree to the [Usage Terms](./terms.MD).

> **Important:** MorphoCloud membership grants you access to request instances, but does not guarantee that compute resources will be available at any given time. Instance availability depends on the current capacity of [JetStream2](https://jetstream-cloud.org/), a nationally shared research cloud. Before creating or unshelving an instance, we recommend always checking the [real-time resource availability](https://morphocloud.org) dashboard.

---

## Access Pathways

MorphoCloud has three access pathways depending on how you will use it.

### 1. Individual Access

For researchers and students who want a personal instance for their own work.

**How to get access:**
1. Go to [join.morphocloud.org](https://join.morphocloud.org).
2. Sign in with your [ORCID iD](https://orcid.org) — the free, portable researcher identifier. (If you don't have one already, you can create one in about 30 seconds during the signup.)
3. Fill in the form: your email address, institution, GitHub username, career stage, intended use, and accept the Terms of Use.
4. Confirm your email by clicking the link we send you. Your GitHub organization invitation is sent automatically once your email is verified.
5. Accept the GitHub organization invitation from your [GitHub organizations page](https://github.com/settings/organizations).

> Your email is added to a low-volume MorphoCloud announcement list (outages, workflow updates, upcoming events).

**Instance lifespan:** 60 days by default, renewable once to 120 days using `/renew`.

---

### 2. Workshop Access

For instructors or organizers running a short workshop (5 days max) where all participants need simultaneous access.

**How to get access:**
1. The workshop organizer registers at [join.morphocloud.org/workshop](https://join.morphocloud.org/workshop) and signs in with their [ORCID iD](https://orcid.org). Once verified, they are added to the **WorkshopOrganizers** GitHub team.
2. The organizer opens a **Workshop Request** issue in the [MorphoCloud Instances repository](https://github.com/MorphoCloud/Instances/issues/new/choose) and fills in the workshop details (dates, number of participants, instance flavor).
3. Once the MorphoCloud team approves the request, instances are provisioned for each participant — the organizer receives all connection credentials by email and is responsible for distributing them to participants.

**Instance lifespan:** Set per workshop by the MorphoCloud team.

---

### 3. Use MorphoCloud For an Academic Course

This is for instructors who want their students to use MorphoCloud routinely as part of their course. The course is set up as a dedicated and private repository only accessible to instructor(s) and the students they invite. Repository is removed 30 days after the course concludes. Instructors can tailor the platform to better align with specific course objectives and actively maintain the course enrollment.

If you are interested, please [review the instructions](./instructor/README.md).
Questions? Contact us at [portal@morphocloud.org](mailto:portal@morphocloud.org).

---

## Using MorphoCloud

Once you have access and have accepted your GitHub organization invitation, the **[User Guide](./user-guide/)** covers day-to-day use:

- **[Requesting and creating your instance](./user-guide/getting-started.md)** — open an issue and run `/create`.
- **[Connecting](./user-guide/connecting.md)** — web browser (Guacamole) or the TurboVNC client.
- **[Transferring files](./user-guide/file-transfer.md)** — Guacamole drag-and-drop, and `scp`/`sftp`/`rsync` for bulk data.
- **[Where your data is stored](./user-guide/data-and-storage.md)** — the MyData volume and what survives deletion.
- **[Commands](./user-guide/commands.md)** — `/create`, `/shelve`, `/unshelve`, `/renew`, delete, and more.
- **[Instance lifecycle](./user-guide/instance-lifecycle.md)** — running, shelving, expiration, renewal.
- **[GPU notes & known issues](./user-guide/gpu-and-known-issues.md)** — GPU behavior on JetStream2 and resource availability.

Instructors setting up a course should follow the **[instructor guide](./instructor/README.md)**.

---

## Instance Types

All instances include a persistent attached volume (your **MyData** volume, 100 GB) mounted at `/media/volume/MyData`. Your entire home directory — Desktop, Documents, Downloads, and all other home folders — is stored on this volume, so files you save anywhere in your home directory survive instance deletion and recreation ([details](./user-guide/data-and-storage.md)).

| Flavor | RAM | CPUs | GPU | Best for |
|--------|----:|-----:|-----|----------|
| `g3.large` | 60 GB | 16 | A100 (½, 20 GB) | **Default.** Most 3D Slicer / SlicerMorph workflows — best availability |
| `g4.xl` | 120 GB | 12 | L40S (48 GB) | When you need **more GPU memory or RAM** than g3.large (fewer vCPUs, slower than a full A100) |
| `g3.xl` | 120 GB | 32 | A100 (full, 40 GB) | **Heaviest / fastest GPU work** — full A100, ~2× g4.xl |
| `m3.xl` | 125 GB | 32 | — | Computationally intensive tasks that don't require a GPU (e.g., image registration with ANTsPy) |
| `r3.large` | 500 GB | 64 | — | Image registration with large datasets |
| `r3.xl` | 1000 GB | 128 | — | Image registration with very large datasets |

**When in doubt, start with `g3.large`.** It is the default flavor, covers the majority of SlicerMorph workflows, and is typically the most available. Move up only if you encounter memory or compute limits — see [GPU notes & known issues](./user-guide/gpu-and-known-issues.md) for which flavor to pick.

> **Note on GPU instances:** Performance of 3D Slicer (especially volume rendering) degrades significantly on GPU instances when any dimension of the volume is ≥ 4096 voxels. For such large volumes, consider `m3.xl` or a large-memory flavor instead — see [GPU notes & known issues](./user-guide/gpu-and-known-issues.md).

> **Check availability:** JetStream2 resources are shared nationally. Before creating or unshelving an instance, check [real-time resource availability](https://morphocloud.org) to avoid long waits.

---

## Installed Software

| Software | Details |
|----------|---------|
| 3D Slicer | v5.10 |
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

For general inquiries send us an email at **portal@morphocloud.org**.

For instance support, tag `@MorphoCloud/morphocloud-admins` in your specific issue page and explain what you need help with.

---

## Funding & Acknowledgment

MorphoCloud is supported by the National Science Foundation (DBI/2301405) and the National Institutes of Health (NICHD/HD104435). Infrastructure is provided by JetStream2 (OAC/2005506) and Exosphere (TI/2229642).

If you use MorphoCloud for your research, please cite the platform article and include the following acknowledgment statement.

**Citation:**

> Maga AM and Fillion-Robin J-C. MorphoCloud: Democratizing Access to High-Performance Computing for Morphological Data Analysis. *F1000Research* 2026, **15**:53. https://doi.org/10.12688/f1000research.176328.1

**Acknowledgment statement:**

> This study relied on cyberinfrastructure supported by grants from the National Science Foundation (MorphoCloud: DBI/2301405; JetStream2: OAC/2005506; Exosphere: TI/2229642) and the National Institutes of Health (MorphoCloud: NICHD HD104435).
