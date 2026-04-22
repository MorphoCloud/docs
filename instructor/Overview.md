# MorphoCloud Course Instances: Overview

MorphoCloud provides on-demand, GPU-accelerated virtual desktops for courses that require computationally intensive 3D visualization and analysis software (3D Slicer, SlicerMorph). Instructors maintain a class roster in a Google Sheet, and MorphoCloud automatically provisions and manages dedicated JetStream2 cloud instances for each student — accessible via any modern web browser. Instance lifecycle (creation, start, stop, deletion) is fully automated through GitHub, requiring no cloud computing expertise from the instructor or students. 

## What You Need to Get Started

1. **A Google account** — to manage your class roster via Google Sheets
2. **A GitHub account** — [https://github.com/signup](https://github.com/signup)
3. **An ACCESS allocation on JetStream2** — see [Getting Your Own ACCESS Explore Allocation](access.md)

## What Your Students Need

- **A GitHub account** — [https://github.com/signup](https://github.com/signup)

## Steps to Get Your MorphoCloud Course Repository Created

1. [Obtain your ACCESS Explore allocation and add MorphoCloud to it](access.md).
2. [Fill out the MorphoCloud course intake form](https://course.morphocloud.org) — do this **at least four weeks before the start of the course** so we have time to review and set up your environment.
3. Follow the instructions provided by the MorphoCloud admin team, including joining the MorphoCloud GitHub Organization and your course-specific repository.
4. Once your course repository is created, follow the [post-repo setup guide](post-repo.md) to configure your roster, review settings, test your instance, and enroll students.

## Course Day 1 Actions

See the [post-repo setup guide](post-repo.md) for detailed steps. In summary:

1. Collect your students' GitHub usernames and their corresponding email addresses. Enter them into your copy of the course roster template.
2. Edit `Students.txt` in your course repository and add each student's GitHub username (one per line). This will automatically invite them to your course repository and the MorphoCloud Organization.
3. Show students how to accept the GitHub invitation to join the MorphoCloud Organization and the course repository.
4. Walk them through how to create and access their instances (e.g., file transfer, copy/paste, TurboVNC viewer for better visuals).

## Maintaining Enrollment

- **Adding students:** If a student joins your course late, add their GitHub username and email to the roster sheet, then add their username to `Students.txt`. The invitation is sent automatically — they just need to accept it to start using the platform.
- **Removing students:** If a student drops the course, you need to remove their GitHub username from the course team list, which is independent of the Students.txt in your repo. Removing them from Students.txt will not be enough. Contact the MorphoCloud admins at [portal@morphocloud.org](mailto:portal@morphocloud.org) for instructions on how to do this.
- **Checking usage:** MorphoCloud provides tools to check which students on your roster have already onboarded (i.e., accepted invitation and joined the course repo). Ask MorphoCloud admins how to access and use it.

## Need Help?

Contact the MorphoCloud team at [portal@morphocloud.org](mailto:portal@morphocloud.org).
