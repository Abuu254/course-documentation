# Adding Course Dojo

To configure a dojo as a course, create a `course.yml` file in the root of your dojo repository. This file defines course metadata and assessment rules.

## Example `course.yml`

```yaml
start_date: "2025-01-15T00:00:00Z"
student_id: "NetID"

letter_grades:
  A: 0.9
  B: 0.8
  C: 0.7

assessments:
  - type: checkpoint
    id: hello
    date: "2025-02-01T23:59:59Z"
    grace_period: 24          # hours after due date
    percent_required: 0.5     # 50% of challenges
    weight: 0.2               # 20% of course grade

  - type: due
    id: hello
    date: "2025-03-01T23:59:59Z"
    late_penalty: 0.1         # 10% penalty per late day
    weight: 0.2               # 20% of course grade

  - type: due
    id: world
    date: "2025-04-17T02:30:59Z"
    late_penalty: 0.1
    weight: 0.5               # 50% of course grade
    extensions:
      student123: 3           # 3 extra late days for student123

  - type: helpfulness
    method: log50
    unique: true
    max_credit: 0.05

grading_policy: "Complete all modules and assessments for full credit."
```

## Course Fields

- **`start_date` (datetime):** When the course officially begins.  
- **`student_id` (string):** The label shown for each student’s identifier (e.g., “NetID”; defaults to “Identity”).  
- **`letter_grades` (map [string → float]):** Minimum numeric score required for each letter (e.g., A: 0.93, B: 0.85, …).  
- **`assessments` (list [map]):** One entry per graded component.
  
---

## Assessment Map Keys

Each entry under `assessments:` must include:

- **`type` (string):** One of `checkpoint`, `due`, `manual`, `extra`, `helpfulness`, or `memes`.  
- **`id` (string):** The module identifier, matching a module in `dojo.yml`.  
- **`date` (datetime):** Deadline for on-time credit.  
- **`weight` (float):** Fraction of the overall grade (sum ≤ 1.0).  
- **`late_penalty` (float):** Multiplier (0–1) applied per late day (only for `due`).

---

## Supported Assessment Types

- **due:** A deadline-based assessment—students must solve all required challenges in the module by its due date for full credit.  
- **checkpoint:** An early-progress milestone requiring a subset of a module’s challenges by the checkpoint date.  
- **manual:** Instructor-graded work (e.g., writeups or projects) where credit is entered by hand.  
- **extra:** Optional bonus challenges outside the core grading scheme.  
- **helpfulness:** Community participation credit based on “thank you” posts in Discord.  
- **memes:** Social engagement credit for posting memes in Discord.  

> Although Dojo supports all of these types, for our course we focused primarily on **due**-type assessments.

---

## Linking Module & Challenge IDs

Assessment `id` keys must correspond to module IDs defined in `dojo.yml`. For details on module/challenge configuration, see:

- [Example Dojo](https://github.com/pwncollege/example-dojo)
- [Import Dojo Example](https://github.com/pwncollege/example-import-dojo)

---

## Why This File Is Needed

The official Dojo docs didn’t clearly explain how to configure a course. By examining the code, we discovered that **every** course must have a top-level `course.yml` defining its metadata and assessments. Without it, no grading or course UI features will be enabled.

---

## Contributing Back

It’s my goal to upstream these documentation improvements into the main project. Currently, most Dojo setup docs live in separate repositories—so I’ll identify the correct repo or docs directory, fork it, and submit a pull request to centralize this guidance.  
```
