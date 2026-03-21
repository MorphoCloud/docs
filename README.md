# MorphoCloud User Guide

## What is MorphoCloud?

MorphoCloud provides on-demand, high-performance cloud computing instances to support computational morphology, 3D morphometrics, and biomedical imaging research. Instances run on [JetStream2](https://jetstream-cloud.org/), a national research cloud operated by Indiana University and funded through [ACCESS](https://access-ci.org/). Each instance comes pre-loaded with [3D Slicer](https://download.slicer.org/), [SlicerMorph](https://slicermorph.org/), and a suite of additional tools (see [Installed Software](#installed-software) below), and is accessible from any web browser — no local installation required.

Instances are managed entirely through GitHub Issues. You request, control, and monitor your instance by opening an issue and posting commands as comments. All you need is a [GitHub account](https://github.com), request to become a member of the MorphoCloud organization on github and agree to the [Usage Terms](). 

---

## Access Pathways

MorphoCloud has three access pathways depending on how you will use it.

### 1. Individual Access

For researchers and students who want a personal instance for their own work.

**How to get access:**
1. Fill out the [MorphoCloud Intake Form](https://docs.google.com/forms/d/e/1FAIpQLSez2afddl8G-zM7iGYEFUGuk3221NhuswSpk20hmOTyVS0xOA/viewform), select **Individually**, and provide your contact information, GitHub account name, and your use cases. (note that your email will be added to low volume MorphoCloud mailing list, which is used to report outages, updates to the workflow and upcoming events.)

2. You will receive a GitHub org invitation by email — accept it
3. Once you are a member of the MorphoCloud organization, you can a new issue using the **Instance Request** template in the [MorphoCloud Instances repository](https://github.com/MorphoCloud/MorphoCloudInstancesTest)
4. A validation check runs automatically. Once it passes, post `/create` as a comment to provision your instance
5. You will receive an email with the connection URL when your instance is online.

**Instance lifespan:** 60 days by default, renewable once to 120 days using `/renew`.

---

### 2. Workshop Access

For instructors or organizers running a short workshop (maximum 5 days) where all participants need simultaneous access.

**How to get access:**
1. The workshop organizer fills out the [MorphoCloud Intake Form](https://docs.google.com/forms/d/e/1FAIpQLSez2afddl8G-zM7iGYEFUGuk3221NhuswSpk20hmOTyVS0xOA/viewform) and selects **Organize a Workshop**
2. The MorphoCloud team reviews the submission and, if approved, adds the organizer to the **WorkshopOrganizers** GitHub team
3. The organizer then opens a **Workshop Request** issue in the MorphoCloud Instances repository and fills in the workshop details (dates, number of participants, instance flavor)
4. Once the workshop request is approved, instances are provisioned for each participant — the organizer receives all connection credentials by email and is responsible for distributing them to participants.

**Instance lifespan:** Set per workshop by the MorphoCloud team.

---

### 3. Course Access (Semester/Class)

This is for instructors who want their students to use MorphoCloud routinely as part of their course. This is different than each individual student applying for an instance. It is a two-step process and instructors are responsible collecting students github accounts so that a course specific team can be created by the MorphoCloud admins.  

**How to get access (instructor):**
1. The instructor fills out the [Course Registration Form](https://docs.google.com/forms/d/e/1FAIpQLSe0i03kZw0mdtB-PTMAMONWmfOrJubX8B2kuyCPhWt_E0KGrA/viewform)
2. Once approved, the instructor receives:
   - The **Course Team Slug** (e.g., `morphocloud-course-usu-herpetology`) — share this with students
   - A link to the [MorphoCloud Intake Form](https://docs.google.com/forms/d/e/1FAIpQLSez2afddl8G-zM7iGYEFUGuk3221NhuswSpk20hmOTyVS0xOA/viewform) — students fill this out to self-enroll; no roster submission is needed from the instructor
   - A pre-filled **Instance Request link** — share this with students so they can open their own instance requests after enrollment

**How to get access (student):**
1. Fill out the [MorphoCloud Intake Form](https://docs.google.com/forms/d/e/1FAIpQLSez2afddl8G-zM7iGYEFUGuk3221NhuswSpk20hmOTyVS0xOA/viewform), select **Part of an academic course**, and enter the Course Team Slug provided by your instructor
2. Click the email verification link you receive — this triggers your GitHub org invitation
3. Accept the GitHub organization invitation
4. Use the link provided by your instructor to open a **Course Instance Request** in the MorphoCloud Instances repository — this opens the same GitHub issue form you would find under New Issue, but with the Course Team Slug field already filled in for you
5. A validation check runs automatically. Once it passes, post `/create` as a comment to provision your instance

**Instance lifespan:** Set by the instructor at course registration (e.g., the length of the semester).

> **Note:** Course access is separate from individual access. If you want a personal instance for your own research outside the course — before, during, or after it — fill out the [MorphoCloud Intake Form](https://docs.google.com/forms/d/e/1FAIpQLSez2afddl8G-zM7iGYEFUGuk3221NhuswSpk20hmOTyVS0xOA/viewform) and select **Individually**.
>
> **Privacy note:** Course students fill the MorphoCloud Intake Form using the course path — only their name, email, institution, GitHub username, and course team slug are collected. Your email is used solely to deliver instance credentials and is not shared outside MorphoCloud. At the end of the course, GitHub accounts associated with the course are removed from the MorphoCloud organization (unless the student also applied for a personal individual instance).

---

## Instance Types

All instances include a persistent attached volume (your **My-Data** volume, 100 GB) mounted at `/media/volume/MyData`. This is where you should keep all your files — the root filesystem (Desktop, Documents, Downloads) is small and not persistent across instance recreations.

| Flavor | RAM | CPUs | GPU | Best for |
|--------|----:|-----:|-----|----------|
| `g3.large` | 60 GB | 16 | A100 (20 GB) | General-purpose morphology and morphometrics, 3D Slicer, most SlicerMorph workflows |
| `g4.xl` | 125 GB | 32 | L40S | Photogrammetry, NNInteractive, AI-assisted segmentation, large GPU workloads |
| `m3.xl` | 125 GB | 32 | — | Computationally intensive tasks that don't require a GPU (e.g., image registration with ANTsPy) |
| `r3.large` | 500 GB | 64 | — | Image registration with large datasets |
| `r3.xl` | 1000 GB | 128 | — | Image registration with very large datasets |

**When in doubt, start with `g3.large`.** It is the default flavor, covers the majority of SlicerMorph workflows, and is typically the most available. Move up only if you encounter memory or compute limits.

> **Note on GPU instances:** Performance of 3D Slicer (especially volume rendering) degrades significantly on GPU instances when any dimension of the volume is ≥ 4096 voxels. For such large volumes, consider `m3.xl` or a large-memory flavor instead.

> **Check availability:** JetStream2 resources are shared nationally. Before creating or unshelving an instance, check [real-time resource availability](https://docs.jetstream-cloud.org/overview/status/#availability-of-scarce-resources) to avoid long waits.

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

## Instance Lifecycle

### States

| State | Meaning |
|-------|---------|
| **Running** | Instance is active and accessible via the connection URL |
| **Shelved** | Instance is paused and not consuming compute resources; your data is preserved |
| **Deleted** | Instance and/or volume have been permanently removed |

### Automatic shelving

For **individual and course instances**, once online the instance stays active for **4 hours**. As the session limit approaches, a reminder popup appears on the desktop — if you dismiss it or do not respond, the instance shelves itself. You can also manually extend your session at any time by clicking the session-extension icon on the desktop, which resets the 4-hour countdown. You can unshelve at any time using `/unshelve` — your data remains intact, though your running applications will be closed.

**Workshop instances** stay online continuously for the duration of the workshop and are not subject to the 4-hour auto-shelving policy.

### Expiration

Each instance has an expiration label (e.g., `expiration:60d`) applied when it is created. When the expiration date approaches:

- Individual users receive a renewal notification and can use `/renew` to extend their instance (once, up to the maximum lifespan)
- Course and workshop instances expire on the schedule set at registration
- After expiration the instance is shelved, then deleted after a grace period

### Your data volume

Your **My-Data** volume persists independently of the instance. Even if your instance is shelved or deleted, the volume remains until you explicitly delete it with `/delete_volume` or `/delete_all`.

---

## Commands

Post any of the following as a comment on your instance issue. Only one command per comment.

### Individual instances

| Command | What it does |
|---------|-------------|
| `/create` | Provision the instance and volume |
| `/shelve` | Shelve the instance (preserves data) |
| `/unshelve` | Resume a shelved instance |
| `/email` | Re-send the connection URL to your email |
| `/renew` | Extend the instance lifespan (if renewal is available) |
| `/delete_instance` | Permanently delete the instance (volume kept) |
| `/delete_volume` | Permanently delete the data volume (instance kept) |
| `/delete_all` | Permanently delete both instance and volume |

### Course instances

Same as above **except `/renew`** — course instances expire on the fixed course schedule and cannot be individually renewed.

---

## Connecting to Your Instance

When your instance is ready, you will receive an email with connection credentials. Each time your instance comes back online after shelving, a new email is sent — connection addresses can change between sessions.

You have two options for connecting to the graphical desktop:

### Option 1 — Web browser (Guacamole)

Click the **Web connect** link in the email. No software installation needed. Guacamole provides a side toolbar (`Ctrl`/`Cmd`+`Alt`+`Shift`) for clipboard access and file transfers. The desktop includes shortcuts to 3D Slicer, SlicerMorph, and your MyData storage, and a right-click menu for display/resolution settings.

Limitations: font and display scaling can be imprecise; clipboard is cumbersome to use.

### Option 2 — TurboVNC (recommended for visualization)

Download and install [TurboVNC](https://github.com/TurboVNC/turbovnc/releases/tag/3.2.1) (expand Assets → find the package for your OS). Use the **VNC address** and passphrase from the credentials email to connect.

Benefits: much better image quality, proper display scaling, and native copy/paste. Limitation: no file transfer (use Guacamole for that).

**Best practice:** use both in tandem — Guacamole for file transfers, TurboVNC for interactive 3D visualization.

> **Important:** Always save your work to `/media/volume/MyData`. The root filesystem (Desktop, Documents, Downloads) is not persistent — if your instance is deleted and recreated, only the MyData volume is retained.

---

## Important Notes

1. **Opening an issue does not provision an instance.** After you open an instance request issue, an automatic validation runs first. Once it posts a ✅ confirmation comment on your issue, you must then post `/create` to actually provision the instance.
2. **You cannot change instance types** after an issue is created and approved. If you need a different flavor, open a new issue.
3. **Resource availability varies.** JetStream2 is a shared national resource. If `/create` or `/unshelve` hangs, check [availability](https://docs.jetstream-cloud.org/overview/status/#availability-of-scarce-resources) and try again later. Particularly for courses we cannot guarantee there will be instances available for everyone at the meeting time of the course. As such MorphoCloud is best used as an asynchronous learning tool in classroom. 
4. **Save everything to MyData.** The root disk is small and ephemeral. All important files must go in `/media/volume/MyData`.

---

## Getting Help

- **Email:** morphocloudportal@gmail.com
- **GitHub Issues:** Open an issue in the MorphoCloud Instances repository for access or technical problems

---

## Funding & Acknowledgment

MorphoCloud is supported by the National Science Foundation (DBI/2301405) and the National Institutes of Health (NICHD/HD104435). Infrastructure is provided by JetStream2 (OAC/2005506) and Exosphere (TI/2229642).

If you use MorphoCloud for your research, please cite the platform article and include the following acknowledgment statement.

**Citation:**

> Maga AM and Fillion-Robin J-C. MorphoCloud: Democratizing Access to High-Performance Computing for Morphological Data Analysis. *F1000Research* 2026, **15**:53. https://doi.org/10.12688/f1000research.159365.1

**Acknowledgment statement:**

> This study relied on cyberinfrastructure supported by grants from the National Science Foundation (MorphoCloud: DBI/2301405; JetStream2: OAC/2005506; Exosphere: TI/2229642) and the National Institutes of Health (MorphoCloud: NICHD HD104435).
