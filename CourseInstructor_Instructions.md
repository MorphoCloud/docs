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
NSF award is required.

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

### Apply for your allocation

Go to: **https://allocations.access-ci.org/get-your-first-project**

For guidance on what to include in the application, see:
[Prepare Requests](https://allocations.access-ci.org/prepare-requests)

---

## Step 3 — Request Both `g3` and `m3` Resource Types on JS2

> ⚠️ **Do this at application time — adding resource types later takes 24–72 hours
> and will delay your course setup.**

MorphoCloud course instances use **`g3` (GPU)** flavors for student work. The
self-hosted runner VM that manages automation uses an **`m3` (CPU-only)** flavor.
You need both enabled on your JS2 allocation before setup can proceed.

When submitting or managing your JS2 allocation via the
[ACCESS allocations portal](https://allocations.access-ci.org/), request:

- **`jetstream2.indiana.access-ci.org`** (main JS2 IU compute resource)
- Include both `g3` and `m3` instance types in your resource request

JS2 resource details: **https://allocations.access-ci.org/resources/jetstream2.indiana.access-ci.org**

If you already have an allocation but need to add `m3` or `g3` access, submit
a supplement request:
**https://allocations.access-ci.org/how-to#request-more-credits**

---

## Step 4 — Set Up Your Allocation in Exosphere

Once your allocation is approved and active, log in to Exosphere with your
ACCESS credentials:

**https://jetstream2.exosphere.app**

Confirm that your allocation appears and that you can see both `g3` and `m3`
instance flavors when creating an instance.

---

## Step 5 — Prepare Your Student Roster Spreadsheet

Before submitting the MorphoCloud intake form, set up the roster spreadsheet
that MorphoCloud uses to look up student email addresses for sending instance
credentials.

1. **Make a copy** of the MorphoCloud roster template:\
   **https://docs.google.com/spreadsheets/d/1N_av-7BGzXoCSx9K7LaiADmeEP9JGcRVZHFSwdNaHt0/copy**

2. Fill in your roster:
   - **Column A (`github_handle`)** — student GitHub usernames (without `@`)
   - **Column B (`email`)** — student email addresses
   - Include your own GitHub handle and email in the roster

3. **Share the sheet read-only** with `morphocloudportal@gmail.com`
   (MorphoCloud's service account)

4. **Note your sheet ID** — the long string between `/d/` and `/edit` in the
   Google Sheets URL. You will provide this to the MorphoCloud admin after
   approval.

---

## Step 6 — Submit the MorphoCloud Course Intake Form

Once your ACCESS allocation is active and your roster sheet is ready, submit
the intake form:

**https://docs.google.com/forms/d/e/1FAIpQLSdbH8hcd6bJlNjcJQb21mK-MvjL-lLkzHwDfuvmO-h1YjsHEQ/viewform**

You will be asked for:

| Field | Notes |
|-------|-------|
| Instructor name and email | Must match your GitHub account email |
| GitHub username | Your personal GitHub handle |
| Institution | Used to generate the course ID (e.g. `ETSU-A100`) |
| Course name | E.g. `BIOL A100` |
| Expected enrollment | Number of students |
| Instance duration | How many days students need access |
| Instance flavor | Select the GPU flavor appropriate for your software needs |
| ACCESS Allocation ID | The allocation ID shown in your ACCESS portal (e.g. `TRA250020`) |

After submission, a MorphoCloud admin will review your request and email you
when it is approved (typically within 1–2 business days).

---

## Step 7 — Post-Approval: Provide Your Roster Sheet ID

After receiving the approval email, reply with your **Google Sheet roster ID**
(from Step 5). The admin will configure your course repo to use it for email
lookups.

---

## Step 8 — Enroll Students in the Course GitHub Team

After the admin confirms setup is complete, you will have access to your course
GitHub repo (`MC-<course-id>`).

To enroll students:

1. Open the `students.txt` file in your course repo
2. Copy the `github_handle` column from your roster spreadsheet
3. Paste the handles into `students.txt`, one per line
4. Commit and push — enrollment runs automatically via GitHub Actions
5. Students will receive a GitHub invitation to the MorphoCloud org and course
   team; they must accept it before requesting instances

To add students later in the semester, update `students.txt` and push again.

---

## Step 9 — Students Request Instances

Once enrolled, students can request a course instance by opening an issue in
the course repo using the **Course Instance Request** issue template. They will
receive credential emails when their instance is ready.

Students can control their instance by posting commands as issue comments:
- `/shelve` — pause the instance (preserves work, stops billing)
- `/unshelve` — resume a shelved instance
- `/email` — resend credential email

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
