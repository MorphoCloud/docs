# MorphoCloud Course Instructor Instructions

This guide walks course instructors through everything needed to set up and run
a MorphoCloud per-course allocation — from obtaining an ACCESS allocation to
managing student instances during the semester.

---

## Overview

MorphoCloud provides each course with its own dedicated pool of GPU-enabled
cloud instances running on [JetStream2 (JS2)](https://jetstream-cloud.org/),
a nationally shared research cloud funded by NSF. Each student in your course
gets their own instance with [3D Slicer](https://download.slicer.org/),
[SlicerMorph](https://slicermorph.org/), and related tools pre-installed,
accessible from any web browser.

Each approved course gets its own private GitHub repository (`MC-<course-id>`)
that serves as the control plane — students request and manage instances by
opening GitHub issues in that repo.

---

## Step 1 — Create an ACCESS Account

If you do not already have one, register for a free ACCESS account:

**https://identity.access-ci.org/new-user**

ACCESS accounts are free and open to any US-based researcher or educator. No
NSF award is required. Resources are compeletely free-of-charge to eligible researchers.

---

## Step 2 — Obtain an ACCESS Allocation for Your Course

MorphoCloud requires a dedicated **Explore ACCESS** allocation (or larger) for
each course. This gives your course its own isolated pool of JS2 credits,
separate from the MorphoCloud shared allocation.

### Choose the right allocation type

| Type | Credits | Best for |
|------|---------|----------|
| [**Explore ACCESS**](https://allocations.access-ci.org/project-types) | 400,000 | Courses up to ~30 students, ≤ one semester |
| [**Discover ACCESS**](https://allocations.access-ci.org/project-types) | 1,500,000 | Larger courses or multi-semester use |
| [**Accelerate ACCESS**](https://allocations.access-ci.org/project-types) | 3,000,000 | Multiple concurrent courses |

For most courses, **Explore ACCESS** is the right starting point. Use the
[JS2 Usage Estimation Calculator](https://docs.jetstream-cloud.org/alloc/estimator/)
to estimate how many credits you will need based on your enrollment and
instance duration.

A `g3.large` instance uses 32 SU/h. For a class of 30 (students + instructors + TAs) using MorphoCloud an average of 10 h/week over a 16-week semester:

> 32 SU/h × 30 instances × 10 h/week × 16 weeks ≈ **154,000 SU** — well within an Explore allocation.

You will also need approximately **5,400 SU** for the dedicated runner VM that manages course automation (2 SU/h × 24 h × 7 days × 16 weeks).

If you plan to share data with your class, request a small storage allocation on JS2 as well.

### Apply for your allocation

Go to: **https://allocations.access-ci.org/get-your-first-project**

For guidance on what to include in the application, see:
[Prepare Requests](https://allocations.access-ci.org/prepare-requests)

An Explore allocation does not require extensive documentation. You can cite the existing MorphoCloud paper and note that you want to leverage the existing MorphoCloud infrastructure for your course.

---

## Step 3 — Request Both `g3` and `m3` Resource Types on JS2

> ⚠️ **Do this at application time — adding resource types later takes 24–72 hours
> and will delay your course setup.**

MorphoCloud course instances use **`g3` (GPU)** flavors for student work. The self-hosted runner VM that manages automation uses an **`m3` (CPU-only)** flavor. You must secure both resource types on your JS2 allocation before course setup can proceed.

When submitting or managing your JS2 allocation via the
[ACCESS allocations portal](https://allocations.access-ci.org/), request:

- **`jetstream2.indiana.access-ci.org`** (main JS2 IU compute resource)
- Include both `g3` and `m3` instance types in your resource request

JS2 resource details: **https://allocations.access-ci.org/resources/jetstream2.indiana.access-ci.org**

If you already have an allocation but need to add `m3` or `g3` access, submit
a supplement request:
**https://allocations.access-ci.org/how-to#request-more-credits**

---

## Step 4 — Add MorphoCloud to Your ACCESS Allocation

Once your allocation is approved and active on ACCESS, add the **magalab** account as an allocation manager and assign it to manage the JS2 resources only (if you have resources from other providers, do not include those). This is a mandatory step before you can submit the course creation form.

---

## Step 5 — Submit the MorphoCloud Course Intake Form

Once your ACCESS allocation is active and magalab has been added as allocation manager, submit the intake form:

**https://docs.google.com/forms/d/e/1FAIpQLSdbH8hcd6bJlNjcJQb21mK-MvjL-lLkzHwDfuvmO-h1YjsHEQ/viewform**

You will be asked for:

| Field | Notes |
|-------|-------|
| ACCESS Allocation ID | The allocation ID shown in your ACCESS portal (e.g. `TRA250020`) |
|Acknowledgment | that you added magalab as an allocation manager |
| Instructor name and email | Must match your GitHub account email |
| GitHub username | Your personal GitHub handle |
| Institution | Used to generate the course ID (e.g. `ETSU`) |
| Course name | E.g. `BIOL 100` |
| Expected enrollment | Number of students + instructors|
| Instance duration | How many days students need access | 
| Instance flavor | `g3.large` is strongly recommended — `g3.xl` has historically had very limited availability on JS2 |

> **Note:** The instance flavor is fixed for the entire course — all students share the same flavor.

After submission, a MorphoCloud admin will review your request and email you
when it is approved (typically within 1–2 business days).

---

## Step 6 — Prepare Your Student Roster Spreadsheet

When the course starts, you need to create an enrollment roster spreadsheet
that MorphoCloud uses to look up student email addresses for sending instance
credentials. Collect this information during your first class meeting and enter into the form linked below.

1. **Make a copy** of the MorphoCloud roster template:\
   **https://docs.google.com/spreadsheets/d/1N_av-7BGzXoCSx9K7LaiADmeEP9JGcRVZHFSwdNaHt0/copy**

2. Fill in your roster:
   - **Column A (`github_handle`)** — student GitHub usernames (without `@`)
   - **Column B (`email`)** — student email addresses
   - Include your own GitHub handle and email in the roster (or anyone else involved with the course)

3. **Share the sheet read-only** with `morphocloudportal@gmail.com`
   (This is a service account. This account is not checked. Do not try to contact or email anything to this address.)

4. **Note your sheet ID** — the long string between `/d/` and `/edit` in the
   Google Sheets URL. MorphoCloud admins will ask this when setting up your repository.

The roster is dynamic — you can add or remove students at any time.

---

## Step 7 — Post-Approval: Provide Your Roster Sheet ID

After receiving the approval email, contact the MorphoCloud admins (portal@morphocloud.org) with your **Google Sheet roster ID** and the course repo name (from Step 6). The admin will configure your course repo to use it for email
lookups.

---

## Step 8 — Enroll Students in the Course GitHub Team

After the admin confirms setup is complete, you will have access to your course
GitHub repo (`MC-<course-id>`).

To enroll students:

1. Open `students.txt` in your course repo (it is pre-created with instructions)
2. Copy the `github_handle` column from your roster spreadsheet
3. Add the handles below the comment lines, one per line — comments are automatically ignored
4. Commit and push — enrollment runs automatically via GitHub Actions
5. Students will receive a GitHub invitation to the MorphoCloud org and course
   team; they must accept it before requesting instances

To add students later in the semester, update `students.txt` and push again. This automatically triggers a GitHub Action that invites the new students to the MorphoCloud organization and the course team.

> **Important:** Students must accept both invitations within **7 days** or they will expire. To accept, students go to their GitHub profile → **Organizations** and click Accept on each pending invitation.

---

## Step 9 — Students Request Instances

Once enrolled, students can request a course instance by opening an issue in
the course repo using the **Course Instance Request** issue template. They will
receive credential emails when their instance is ready.

Students can control their instance by posting commands as issue comments:
| Command | Action |
|---------|--------|
| `/create` | Create the instance and storage volume from scratch |
| `/shelve` | Pause the instance (preserves work, stops billing) |
| `/unshelve` | Resume a shelved instance |
| `/email` | Resend the credential email |
| `/delete_instance` | Remove a stuck or inaccessible instance — must be followed by `/create` to start fresh |

Students can ask for help by mentioning `@<instructor-handle>` or `@MorphoCloud/morphocloud-admins` in an issue comment.

## Contact information for MorphoCloud
If you have questions or concerns, please get in touch with us at portal@morphocloud.org

---

## Useful Links

| Resource | URL |
|----------|-----|
| ACCESS new user registration | https://identity.access-ci.org/new-user |
| ACCESS allocations portal | https://allocations.access-ci.org/ |
| ACCESS project types | https://allocations.access-ci.org/project-types |
| Get your first project | https://allocations.access-ci.org/get-your-first-project |
| JS2 resources page | https://allocations.access-ci.org/resources/jetstream2.indiana.access-ci.org |
| JS2 usage estimation calculator | https://docs.jetstream-cloud.org/alloc/estimator/ |
| JS2 instance flavors | https://docs.jetstream-cloud.org/general/instance-flavors/ |
| Exosphere (JS2 web UI) | https://jetstream2.exosphere.app |
| MorphoCloud roster template | https://docs.google.com/spreadsheets/d/1N_av-7BGzXoCSx9K7LaiADmeEP9JGcRVZHFSwdNaHt0/copy |
| MorphoCloud course intake form | https://docs.google.com/forms/d/e/1FAIpQLSdbH8hcd6bJlNjcJQb21mK-MvjL-lLkzHwDfuvmO-h1YjsHEQ/viewform |
| JS2 allocations overview | https://docs.jetstream-cloud.org/alloc/overview/ |
| ACCESS help / support tickets | https://support.access-ci.org/open-a-ticket |
