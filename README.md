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

- **`start_date`**: ISO-8601 datetime when the course begins.
- **`student_id`**: Label for your student identifier (e.g., NetID).
- **`letter_grades`**: Map of letter → minimum numeric score.
- **`grading_policy`**: Human-readable policy summary.

## Assessment Fields

Each entry in `assessments:` uses a **list** of key-value pairs.

- **`type`**: one of `checkpoint`, `due`, `manual`, `extra`, `helpfulness`, `memes`.
- **`id`**: matches a module’s ID in your `dojo.yml`.
- **`date`**: deadline for on-time credit.
- **`weight`**: fraction of overall grade (sum should be ≤ 1.0).

### Additional for `checkpoint`
- `grace_period`: hours allowed after `date` before late punishments.
- `percent_required`: fraction of challenges to solve.

### Additional for `due`
- `late_penalty`: 0–1 multiplier per late day.
- `extra_late_date`: final cutoff date (optional).
- `extra_late_penalty`: 0–1 multiplier after `extra_late_date` (optional).
- `extensions`: map of student ID → extra late days.

### Other Types
- **`manual`**: specify `progress` and `credit` directly.
- **`extra`**: extra-credit component via `credit`.
- **`helpfulness`**: community credit via `method`, `unique`, `max_credit`.
- **`memes`**: social credit via `value` and `max_credit`.

## Linking Module & Challenge IDs

Assessment `id` keys must correspond to module IDs defined in `dojo.yml`. For details on module/challenge configuration, see:

- [Example Dojo](https://github.com/pwncollege/example-dojo)
- [Import Dojo Example](https://github.com/pwncollege/example-import-dojo)

---
