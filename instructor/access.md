# Getting Your Own ACCESS Explore Allocation for JetStream2

## Step 1: Create an ACCESS Account

Go to [https://identity.access-ci.org/new-user](https://identity.access-ci.org/new-user) and register.

- Select your university/institution from the list and log in with your institutional credentials (federated login via CILogon).
- **If your institution is not listed:** Choose "ACCESS CI" as the identity provider and create a local ACCESS account with a username and password. You can link your institutional identity later.
- **You must use your institutional email address** (e.g., `you@university.edu`). Gmail, Yahoo, and other personal email domains are **not allowed**.

## Step 2: Check Your Eligibility

Full policy: [https://allocations.access-ci.org/allocations-policy#eligibility](https://allocations.access-ci.org/allocations-policy#eligibility)

**You are eligible to be PI** on an Explore allocation if you are:

- A researcher or educator at a **U.S.-based** academic institution, nonprofit, FFRDC, or military academy

**Not eligible:** Undergraduates, unaffiliated/self-employed individuals, or international researchers without a U.S.-based PI.

## Step 3: Browse Available Resources

This step is **optional**, as we specifically require you to apply for an allocation on JetStream2 at Indiana University. However, you may find it useful to explore what other resources are available for your research.

- **Browse resources:** [https://allocations.access-ci.org/resources](https://allocations.access-ci.org/resources)
- **ACCESS Resource Advisor** (helps match your needs): [https://ara.access-ci.org/](https://ara.access-ci.org/)
- **Credit Exchange Calculator** (see how many resource units your credits buy): [https://allocations.access-ci.org/exchange_calculator](https://allocations.access-ci.org/exchange_calculator)

## Step 4: Prepare Your Explore Request

Review requirements: [https://allocations.access-ci.org/prepare-requests](https://allocations.access-ci.org/prepare-requests)

An Explore allocation:
- Provides up to **400,000 ACCESS Credits** (200K SU is awarded upon approval, second half is awarded after a short progress report is completed)
- Requires only a **short abstract** (see boilerplate below)
- Is accepted **anytime** (no deadlines)
- Is typically reviewed and processed within **1–2 business days**
- Lasts for **12 months**
- You can submit **multiple** Explore requests

### Boilerplate Abstract

Below is a template you can adapt for your Explore request. Replace all `[PLACEHOLDER]` fields with your information.

---

**Project Title:** Leveraging MorphoCloud for `[COURSE NAME]`

**Principal Investigator:** `[Your Name, Title, Department, Institution]`

**Resource Requested:** JetStream2 (GPU, normal, and storage)

**Allocation Category:** Explore (Education/Instructional)

This allocation supports `[COURSE NAME/NUMBER]` at `[INSTITUTION]`. The course requires students to perform computationally intensive 3D visualization, segmentation, and morphometric analysis using software (3D Slicer, SlicerMorph) that exceeds the capabilities of standard student laptops.

We will use the MorphoCloud platform ([morphocloud.org](https://morphocloud.org)) to provision GPU-accelerated JetStream2 virtual machines accessible via web browser. Each student receives a pre-configured environment with all necessary software and a persistent storage volume for their datasets and projects. MorphoCloud's automated instance management ensures a seamless classroom experience. For details, see Maga & Fillion-Robin (2026), F1000Research 15:53 ([doi:10.12688/f1000research.176328.1](https://doi.org/10.12688/f1000research.176328.1)).

A dedicated allocation provides administrative autonomy for the instructor to manage provisioning, ensures student data privacy, and guarantees resource availability during class hours.

The course enrolls approximately `[N]` students over a `[N]`-week semester, with an estimated `[N]` hours of active computing per student per week using `g3.large` instances (32 SU/h), for an estimated total of `[TOTAL SU]` SU.

---

### Is 400K Service Units sufficient for my course? 

On JetStream2, the `g3.large` (GPU) flavor consumes **32 SU per hour** of runtime. To estimate your total needs:

```
Total SU = 32 SU/h × (number of students + instructors) × average weekly hours × number of weeks
```

**Example:** A course with 30 students + 2 instructors, averaging 8 hours/week over 15 weeks:

```
32 × 32 × 8 × 15 = 122,880 SU
```

This is well within the 400,000 credit Explore limit. Adjust the weekly hours and participant count to fit your course. If you plan to use a different instance flavor, adjust the Service Units accordingly. 


## Step 5: Submit Your Request

1. Log in at [https://allocations.access-ci.org/](https://allocations.access-ci.org/)
2. Click **"Get Your First Project"** or go to [https://allocations.access-ci.org/get-your-first-project](https://allocations.access-ci.org/get-your-first-project)
3. Select **Explore ACCESS** as the project type
4. Fill in the request form:
   - **Project Title** — e.g., "Leveraging MorphoCloud for [COURSE NAME]"
   - **Public overview** — paste the boilerplate abstract from Step 4 (adapted with your details)
   - **Keywords** — e.g., `MorphoCloud, 3D Slicer, SlicerMorph, morphometrics, cloud computing`
   - **How do you plan to use this project?** — select **Classroom / Training**
   - **Fields of Science** — select the primary field that best matches your course (e.g., Biology, Anatomy)
   - Supporting grant info (if any — a grant is **not required**)
5. In the **Related Personnel** section, add **magalab** as an **Allocation Manager**. This gives the MorphoCloud team the access needed to provision and manage instances on your behalf.
6. In the **Available Resources** section, check **ACCESS Credits**.
7. Submit

## Step 6: Exchange Credits for JetStream2 Time

After your request is approved:

1. Go to your project at [https://allocations.access-ci.org/](https://allocations.access-ci.org/)
2. **Exchange** your ACCESS Credits for an allocation on **JetStream2**
3. The Resource Provider (Indiana University) reviews and approves the exchange (usually quick) 
