# After Your Course Repository Is Created

Once the MorphoCloud team approves your intake form, you will receive an email with access to your course GitHub repository (`MC-<course-id>`). Follow these steps to prepare for your course.

## Step 1: Accept Your GitHub Invitations

You should have received invitations to join the MorphoCloud Organization and your course repository. Go to your GitHub profile icon → **Your Organizations** and accept the pending invitations. (These instructions are also in the email sent by the MorphoCloud team.)

You will not be able to access your course repository until you accept.

## Step 2: Prepare Your Student Roster Spreadsheet

MorphoCloud uses a Google Sheet to look up student email addresses for sending instance credentials.

1. **Make a copy** of the roster template:\
   [roster.morphocloud.org](https://roster.morphocloud.org)

2. Fill in the roster:
   - **Column A (`github_handle`)** — student GitHub usernames (without `@`)
   - **Column B (`email`)** — student email addresses
   - Include yourself and any TAs in the roster (you can enroll the students later -see below)

3. **Share the sheet read-only** with `morphocloudportal@gmail.com`\
   (This is an automated service account — do not email this address.)

4. **Copy your spreadsheet URL** — you will need it in the next step.

## Step 3: Set the Roster Sheet URL in Your Course Repository

1. Go to your course repo on GitHub → **Settings → Secrets and variables → Actions → Variables**
2. Find `MORPHOCLOUD_STUDENT_ROSTER_SHEET_ID` (it is pre-created but blank)
3. Click the ✏️ pencil icon next to the variable
4. Paste the full Google Sheets URL from Step 2 (MorphoCloud extracts the sheet ID automatically)
5. Click **Save**

Without this, instance credential emails cannot be sent to students.

## Step 4: Review Course Settings (Before Creating Any Instances)

Your course repository has configuration variables you can adjust. **Review these before creating any instances** — changing them afterward requires running `/delete_all` and having all students recreate their instances from scratch.

Go to your course repo → **Settings → Secrets and variables → Actions → Variables**.

| Variable | Default | Description |
|---|---|---|
| `VOLUME_SIZE_GB` | `100` | Storage volume size per student (in GB). If your course uses large datasets, increase this. Make sure your allocation has enough storage for all students (e.g., 35 students × 200 GB = 7 TB). By default, MorphoCloud admins exchange 10,000 SU for 10 TB of JS2 storage. If you need more, request an additional storage exchange on your ACCESS allocation. |
| `INSTANCE_SHELVING_TIMEOUT_HRS` | `4` | Hours before an idle instance is automatically shelved. Increase if your labs regularly exceed 4 hours. Students can extend their session by 4 hours using the in-browser popup that appears 30 minutes before shelving. |

To change: click the variable name → ✏️ pencil icon → update → **Save**. Changes take effect within 5 minutes.

> **These settings are optional** — the defaults work well for most courses. But if you need to change them, do so before anyone runs `/create`.

### Changing the Instance Flavor

If you want to change the instance flavor from what you requested at intake time (e.g., switch from `g3.large` to `g3.xl`), you can edit the `COURSE_FLAVOR` variable the same way. However, the new flavor must already be approved on your ACCESS allocation, and your Explore credits must be sufficient for the higher SU rate. **Coordinate this change with the MorphoCloud admins** at [portal@morphocloud.org](mailto:portal@morphocloud.org) before making it, so we can verify everything checks out.

## Step 5: Test Your Own Instance

Before the semester starts, create your own instance to verify everything works:

1. Go to your course repository on GitHub.
2. Open a new issue using the **Course Instance Request** template.
3. Post `/create` as a comment on the issue. This provisions your instance and storage volume.
4. Wait for the automation to complete — you will receive a credential email with your instance URL and login details.
5. Log in to your instance via the web browser link in the email.
6. Practice the commands you will later teach your students:
   - `/shelve` — pause the instance (saves work, stops billing)
   - `/unshelve` — resume a shelved instance
   - `/email` — resend the credential email if you lose it
   - `/delete_instance` — remove the instance entirely (follow with `/create` to start fresh)
7. Get familiar with file transfer, copy/paste, and using the TurboVNC viewer for improved visuals.
## Step 6: Enroll Students

Make sure each student's GitHub username and email are already in your roster spreadsheet (Step 2) before proceeding.

1. Open `Students.txt` in your course repository (it is pre-created with instructions).
2. Add each student's GitHub username, one per line. Comment lines (starting with `#`) are ignored.
3. Commit and push — a GitHub Action runs automatically to invite students to the MorphoCloud Organization and your course team.

> **Important:** Students must accept the GitHub invitation within **7 days** or it will expire. To accept, students go to their GitHub notifications or to **GitHub → Your Organizations** and click Accept.

To add students later in the semester, simply add their usernames to `Students.txt` and push again.

## Step 7: Students Request Instances

Once enrolled, students create their own instances by opening an issue in the course repository using the **Course Instance Request** template and posting the `/create` command. They will receive a credential email when their instance is ready.

Students manage their instances by posting commands as issue comments:

| Command | Action |
|---|---|
| `/create` | Create the instance and storage volume |
| `/shelve` | Pause the instance (preserves work, stops billing) |
| `/unshelve` | Resume a shelved instance |
| `/email` | Resend the credential email |
| `/delete_instance` | Remove a stuck instance — must be followed by `/create` to start fresh |

Students can ask for help by mentioning you (`@<your-github-handle>`) or `@MorphoCloud/morphocloud-admins` in an issue comment.

More information on connecting to instances: [MorphoCloud docs](https://github.com/MorphoCloud/docs?tab=readme-ov-file#connecting-to-your-instance)

## Maintaining Enrollment

- **Adding students:** Add their GitHub username and email to the roster sheet, then add their username to `Students.txt` and push. The invitation is sent automatically.
- **Removing students:** Remove their GitHub username from the team list. Contact the MorphoCloud admins at [portal@morphocloud.org](mailto:portal@morphocloud.org) for instructions.

## Need Help?

Contact the MorphoCloud team at [portal@morphocloud.org](mailto:portal@morphocloud.org).
