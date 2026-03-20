# MorphoCloud Course Intake Redesign — Design Document

**Date:** March 20, 2026  
**Status:** Design finalized — pending implementation  
**Scope:** Replaces the course roster (Form B) approach; unifies all three intake paths into a single form; resolves the course student credential delivery problem.

---

## Problem Statement

The original course intake design (as described in [Discussion #163](https://github.com/MorphoCloud/MorphoCloudWorkflow/discussions/163)) had two unresolved issues:

### 1. Credential delivery to course students

There is no reliable way to deliver instance credentials (IP address + passphrase) to course students using the current architecture. All candidate approaches were evaluated and rejected:

| Approach | Why it fails |
|---|---|
| GitHub issue comment | All course students have Read access to the private repo via their course team — any student can navigate to another student's issue and read their credentials |
| Email via Google Sheet lookup | No student email is stored — course students bypass the intake form, so no Sheet row exists for them |
| GitHub noreply address (`{id}+{username}@users.noreply.github.com`) | This is an outbound-only alias. GitHub's internal notification system uses it, but external SMTP (morphocloudportal@gmail.com) cannot deliver to it — tested and confirmed: mail silently drops |
| Instructor relay | Impractical — credentials (IP + passphrase) change on every `/create` and `/unshelve`. Instructor cannot relay per-student credentials throughout a semester |
| Email relay service (e.g., Cloudflare) | Requires a custom domain, per-student manual routing rules, and still requires the instructor to provide student emails to MorphoCloud — which is the FERPA concern |
| Institutional login (CILogon) | Would require a full web application (not GAS), OAuth App registration, and an identity mapping problem between CILogon `sub` and GitHub username. Valid future direction but not suitable for the current GAS + GitHub Actions architecture |

**Root constraint:** MorphoCloud cannot collect student emails without student consent. The instructor holds student emails by virtue of the educational relationship, but forwarding them to a third party (MorphoCloud) without student consent violates FERPA.

### 2. Credential delivery is not a one-time event

Because IP addresses and passphrases can change on every `/create` and `/unshelve`, credential delivery must work reliably for the entire semester — not just at provisioning time. Any solution that works "once" is insufficient.

---

## Solution: Students Self-Onboard via the Unified Intake Form

The solution is to have course students go through the same individual intake flow that every MorphoCloud user goes through — they fill a form, provide their email with consent, receive an org invite, and then use the standard email-based credential delivery. This eliminates the delivery problem entirely.

The key change to make this practical is **merging all three intake forms into one** with conditional sections, so the experience is streamlined per use case.

---

## Unified Intake Form Design

A single Google Form replaces the existing Individual Intake Form and Workshop Organizer Intake Form. The Course Registration Form A (instructor) is unchanged.

### Page 1 — Terms and Use Case (everyone)

- Agreement to MorphoCloud Terms of Use and NSF Acknowledgment *(required checkbox)*
- **"How will you use MorphoCloud?"** *(required, select one)*
  - `Individually`
  - `Part of an academic course`
  - `Organize a Workshop`

Based on the selection, the form routes to one of three pages.

---

### Page 2A — Individually

| Field | Notes |
|---|---|
| Full name | Required |
| Email | Required |
| Institution / Affiliation | Required |
| Career stage | Required (undergraduate / graduate / postdoc / faculty / industry / other) |
| ORCID | Optional |
| GitHub username | Required |
| What will you be using the MorphoCloud for | Required (select all that apply) |

On submission: GAS sends email verification → after verification, invites to **`MorphoCloudUsers`** only.

---

### Page 2B — Part of an academic course

| Field | Notes |
|---|---|
| Full name | Required |
| Email | Required |
| Institution / Affiliation | Required |
| GitHub username | Required |
| Course Team Slug | Required — hint text: *"Your instructor will provide this (e.g., `morphocloud-course-usu-herpetology`)"* |

No career stage. No ORCID. NSF demographic reporting for the course is satisfied by the instructor's Form A submission — we do not need per-student demographics.

On submission: GAS sends email verification → after verification, validates the course team slug (`GET /orgs/{org}/teams/{slug}`, must start with `morphocloud-course-`) → invites to **course team only** (not `MorphoCloudUsers`).

---

### Page 2C — Organize a Workshop

| Field | Notes |
|---|---|
| Full name | Required |
| Email | Required |
| Institution / Affiliation | Required |
| Career stage | Required |
| ORCID | Optional |
| GitHub username | Required |
| Brief statement of intended use | Required |

On submission: GAS sends email verification → after verification, invites to **`MorphoCloudUsers` + `MorphoCloudWorkshopOrganizers`**.

---

## Team Membership Semantics

| Team | Who is in it | How they get in |
|---|---|---|
| `MorphoCloudUsers` | Individual researchers + workshop organizers | Unified intake form (Individual or Workshop path) |
| `MorphoCloudWorkshopOrganizers` | Workshop organizers only | Unified intake form (Workshop path) |
| `morphocloud-course-*` | Course students only | Unified intake form (Course path) |

**Course students are never added to `MorphoCloudUsers`.** That team remains semantically clean — it contains only people who consented to share their information.

If a student later wants individual access (before, during, or after a course), they submit the form again selecting "Individually" — demographics are captured at that point with explicit consent.

---

## Course Registration (Form A) Changes

The instructor Course Registration Form A gains one field:

- **Required Instance Flavor** *(dropdown — same options as the instance template: `g3.large`, `g4.xl`, `m3.xl`, etc.)*

The instructor chooses flavor once for the entire class. This ensures all students run the same environment, prevents flavor drift across student issues, and removes the flavor choice from the student issue template entirely.

`course-registration.gs` stores flavor in the GitHub team description alongside duration:

```
MorphoCloud course: <name> | duration:<N>d | flavor:<f>
```

Example:
```
MorphoCloud course: USU Herpetology 2026 | duration:120d | flavor:g4.xl
```

The instructor approval email changes to:
- Remove all references to the Student Roster Form (Form B) — it no longer exists
- Provide the **Course Team Slug** (same as before)
- Provide a direct link to the **Unified Intake Form** with a note: *"Tell students to select 'Part of an academic course' and enter the Course Team Slug: `morphocloud-course-xxx`"*
- Provide the **pre-filled course issue URL** (same as before — students use this after their org invite is accepted)

---

## Instructor Workflow (New)

1. Fill the Course Registration Form A (including instance flavor and duration)
2. MorphoCloud admin approves → GitHub team auto-created, instructor added as Team Maintainer
3. Instructor receives approval email with:
   - Course Team Slug
   - Link to Unified Intake Form (to forward to students)
   - Pre-filled course issue URL (to forward to students)
4. Instructor sends students ONE email: *"Fill this form [link], then use this link [link] to request your instance."*
5. Students trickle in on their own — no roster submission needed, no second step from the instructor

---

## Student Workflow (New)

1. Click the intake form link from their instructor
2. Select "Part of an academic course"
3. Fill: name, email, institution, GitHub username, Course Team Slug (from instructor)
4. Receive email verification link → click it
5. GAS validates the course team, sends GitHub org invite
6. Accept GitHub org invite (from `github.com/settings/organizations`)
7. Click the pre-filled course issue URL from instructor → open a course instance request
8. Post `/create` → receive credentials by email (standard delivery — email is now in the Sheet)

---

## Course Instance Issue Template Changes

The `course-instance-request.yml` template **removes the flavor dropdown**. Students only fill:
- What will you be using the MorphoCloud for
- *(Course team slug is pre-filled via URL parameter — not typed by students)*

`on-request-opened.yml` reads both `duration` and `flavor` from the team description and applies:
- `timeout:<hours>hrs`
- `expiration:<days>d`
- `flavor:<f>`
- renames the issue title something like `MC-Course-XXXX-001` (so that even if students enters some private information, we discard it. And it is easier for instructors to sort issues related to their courses.)

All automatically, with no student input.

---

## End-of-Course Cleanup

End-of-course teardown logic is unchanged from Discussion #163:

```
for each member of morphocloud-course-* team:
  if member is also in MorphoCloudUsers:
    → remove from course team only (they have individual access; keep org membership)
  else:
    → remove from course team AND from org entirely (no personal stake; fully scrub)
```

Because course students are never added to `MorphoCloudUsers`, this check is clean and unambiguous.

---

## Implementation Plan

### Phase 1 — Unified Intake Form + Script

| Task | Type |
|---|---|
| Restructure Google Form into conditional sections (Pages 1, 2A, 2B, 2C) | Google Forms UI |
| Add `intake_type` and `course_team_slug` columns to the existing Individual Intake Sheet | Google Sheets UI |
| Write `unified-intake.gs` replacing `individual-intake.gs` and `workshop-intake.gs` | New GAS script |
| Deploy `unified-intake.gs` as a new web app → obtain new `WEBAPP_URL` | GAS deployment |
| Update `MORPHOCLOUD_EMAIL_LOOKUP_URL` and `MORPHOCLOUD_WORKSHOP_EMAIL_LOOKUP_URL` secrets to single `MORPHOCLOUD_UNIFIED_EMAIL_LOOKUP_URL` in both `MorphoCloudInstances` and `MorphoCloudInstancesTest` | GitHub repo secrets |
| Update all workflows that reference the old lookup URL env vars | GitHub Actions |
| Add "This form has moved" notice to old Individual and Workshop forms | Google Forms UI |
| Remove `onFormSubmit` triggers from `individual-intake.gs` and `workshop-intake.gs` (keep `doGet` lookup endpoints alive for transition) | GAS triggers |

**`unified-intake.gs` key logic:**

- `onFormSubmit`: reads `intake_type` field, sends verification email (identical flow for all three)
- `handleEmailVerification → sendGitHubOrgInvite(intakeType, courseTeamSlug)`:
  - `individual` → invite to `MorphoCloudUsers`
  - `workshop` → invite to `MorphoCloudUsers` + `MorphoCloudWorkshopOrganizers`
  - `course` → validate slug (must be a real team prefixed `morphocloud-course-`) → invite to course team only
  - On invalid slug: clear error message in the verification page, do not invite
- `handleEmailLookup`: searches unified sheet; falls back to old individual and workshop sheets during transition period (~6 months); remove fallback after all active users have flowed through the unified form
- `scrubUnverified`: updated PII column list to match new field names

---

### Phase 2 — Course Registration Script

| Task | Type |
|---|---|
| Add "Required Instance Flavor" dropdown to Course Registration Form A | Google Forms UI |
| Update `course-registration.gs`: parse `flavor` from submission | GAS |
| Update `course-registration.gs`: team description format → `MorphoCloud course: <name> \| duration:<N>d \| flavor:<f>` | GAS |
| Update instructor approval email: remove Form B / roster references; add unified intake form link and course team slug | GAS |
| Remove `onFormSubmit` trigger from `course-roster.gs`; archive Form B with notice | GAS + Google Forms UI |

---

### Phase 3 — GitHub Actions

| Task | File(s) |
|---|---|
| Remove flavor dropdown field from course issue template | `.github/ISSUE_TEMPLATE/course-instance-request.yml` |
| Parse `flavor` from team description in `on-request-opened.yml` (extend existing `duration` regex to also capture flavor); apply `flavor:<f>` label automatically | `.github/workflows/on-request-opened.yml` |
| Replace `MORPHOCLOUD_EMAIL_LOOKUP_URL` / `MORPHOCLOUD_WORKSHOP_EMAIL_LOOKUP_URL` references with `MORPHOCLOUD_UNIFIED_EMAIL_LOOKUP_URL` | All workflows that perform email lookup |
| Remove any `skip_email` / graceful-fallback logic added for missing course student emails — no longer needed | `create-course-instance.yml` (or equivalent) |

**Team description parse (regex):**
```
MorphoCloud course: .+ \| duration:(\d+)d \| flavor:(.+)
```

---

### Phase 4 — Transition / Cutover

| Task | Timing |
|---|---|
| Announce unified form URL to existing users via mailing list | At go-live |
| Existing individual/workshop users: no action needed (fallback lookup covers their emails) | Ongoing |
| After ~6 months: remove fallback lookup from `unified-intake.gs` | Post go-live |
| Decommission old `individual-intake.gs`, `workshop-intake.gs` web app deployments | Post go-live + 6 months |

---

## Files Affected

### MorphoCloudAppsScripts

| File | Change |
|---|---|
| `unified-intake.gs` | **New** — handles all three intake paths |
| `course-registration.gs` | **Modified** — flavor field, updated team description, updated emails, remove Form B |
| `individual-intake.gs` | **Retired** — remove `onFormSubmit` trigger; keep `doGet` lookup endpoint during transition |
| `workshop-intake.gs` | **Retired** — remove `onFormSubmit` trigger; keep `doGet` lookup endpoint during transition |
| `course-roster.gs` | **Eliminated** — remove trigger; archive file |

### MorphoCloudWorkflow

| File | Change |
|---|---|
| `.github/ISSUE_TEMPLATE/course-instance-request.yml` | Remove flavor dropdown field |
| `.github/workflows/on-request-opened.yml` | Parse `flavor` from team description; apply `flavor:<f>` label automatically |
| `.github/workflows/create-course-instance.yml` | Use `MORPHOCLOUD_UNIFIED_EMAIL_LOOKUP_URL`; remove email skip/fallback logic |
| Any workflow using `MORPHOCLOUD_EMAIL_LOOKUP_URL` or `MORPHOCLOUD_WORKSHOP_EMAIL_LOOKUP_URL` | Replace with `MORPHOCLOUD_UNIFIED_EMAIL_LOOKUP_URL` |

### MorphoCloudInstances / MorphoCloudInstancesTest

| Item | Change |
|---|---|
| Repository secret `MORPHOCLOUD_EMAIL_LOOKUP_URL` | Replace with `MORPHOCLOUD_UNIFIED_EMAIL_LOOKUP_URL` |
| Repository secret `MORPHOCLOUD_WORKSHOP_EMAIL_LOOKUP_URL` | Replace with `MORPHOCLOUD_UNIFIED_EMAIL_LOOKUP_URL` |

---

## What Does NOT Change

- Individual instance provisioning, lifecycle, and command workflows — unchanged
- Workshop creation, approval, and lifecycle — unchanged
- `course-registration.gs` approval/rejection flow and GitHub team creation — unchanged (flavor field is additive)
- Google Sheet for course registration — unchanged
- `check-approval` action for workshops — unchanged
- End-of-course teardown logic — unchanged from Discussion #163 design
