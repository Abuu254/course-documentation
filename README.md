# Adding Course Dojo

To configure a dojo as a course, create a `course.yml` file in the root directory of your dojo repository. This file defines important course details and assessments.

## Example `course.yml`

```yaml
start_date: "2025-01-15"
student_id: "NetID"

letter_grades:
  A: 0.9
  B: 0.8
  C: 0.7
  D: 0.6
  F: 0.0

assessments:
  - type: checkpoint
    id: hello
    date: "2025-02-01T23:59:59"
    grace_period: 24
    percent_required: 0.5
    weight: 0.2

  - type: due
    id: hello
    date: "2025-03-01T23:59:59"
    late_penalty: 0.1
    weight: 0.2

  - type: due
    id: world
    date: "2025-04-17T02:30:59"
    late_penalty: 0.1
    weight: 0.5
    extensions:
      student123: 3

grading_policy: "Complete all modules and assessments for full credit."
```

## Fields Explanation

- `start_date`: Course start date in ISO format.
- `student_id`: Identifier used (e.g., university NetID).
- `letter_grades`: Defines grade thresholds.

### Assessments

There are other assessment types supported (manual, extra, helpfulness, memes), but this example includes only two types.

Supported types include:

- `checkpoint`: A mid-course assessment with partial completion allowed.
  - `date`: Due date and time.
  - `grace_period`: Additional hours allowed after the due date.
  - `percent_required`: Percentage completion required to pass.
  - `weight`: Assessment's weight in overall grading.

- `due`: Final assessment with penalties for late submissions.
  - `date`: Final due date.
  - `late_penalty`: Penalty applied per late day.
  - `challenge_weights`: Individual challenge weighting within the assessment.
  - `extensions`: Specific extensions allowed for students (keyed by student ID).

### Assessment IDs and Dojos

Assessment IDs reference specific dojos. Adding dojo modules is done in `dojo.yml`. For information on adding dojos and importing modules and challenges, refer to:

- [Example Dojo](https://github.com/pwncollege/example-dojo)
- [Example Import Dojo](https://github.com/pwncollege/example-import-dojo)

