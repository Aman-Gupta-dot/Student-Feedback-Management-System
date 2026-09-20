# Relationships — Lab Assignment 4

| # | Source | Target | Type | Multiplicity | Justification |
|---|---|---|---|---|---|
| 1 | User | CourseAllocation | Association | 1 → 0..* | A faculty user can be assigned to multiple course allocations. |
| 2 | Course | CourseAllocation | Aggregation | 1 → 0..* | Allocations reference a course while the course exists independently. |
| 3 | CourseAllocation | Enrollment | Association | 1 → 0..* | Enrollments reference a course allocation. |
| 4 | User | Enrollment | Association | 1 → 0..* | A student can have multiple enrollments across sessions. |
| 5 | User | Survey | Association | 1 → 0..* | An authorized administrator/HoD creates survey templates. |
| 6 | Survey | SurveyQuestion | Composition | 1 → 1..* | Questions belong to the survey and have no independent survey meaning. |
| 7 | SurveyQuestion | QuestionOption | Composition | 1 → 0..* | Choice options belong to their question; text questions may have none. |
| 8 | Survey | SurveyTrackingRecord | Association | 1 → 0..* | Tracking records are created by submissions and are separate from response content. |
| 9 | User | SurveyTrackingRecord | Association | 1 → 0..* | A student accumulates tracking records across surveys. |
| 10 | Survey | SurveyResponsePayload | Composition | 1 → 0..* | Anonymous response payloads exist in the context of a survey. |
| 11 | SurveyResponsePayload | AnswerEntry | Composition | 1 → 1..* | Answer entries form a submission payload. |
| 12 | SurveyQuestion | AnswerEntry | Association | 1 → 0..* | Each answer corresponds to one survey question. |
| 13 | CourseAllocation | FeedbackAggregate | Association | 1 → 0..* | Aggregates are derived/cacheable analytical results, not owned parts. |
| 14 | FeedbackAggregate | AnswerEntry | Dependency | — | Analytics computation reads answer values without maintaining a persistent answer reference. |

## Generalization
No inheritance relationship is used. Assignment 2 models users through one `User` class with a role attribute, and the three selected use cases differentiate access through role/permission checks rather than subclass-specific behaviour.

## Anonymity Boundary
`User` and `SurveyTrackingRecord` are never directly associated with `SurveyResponsePayload` or `AnswerEntry`. The tracking side records only that a student submitted a particular survey, while the response side stores the submitted values without a student identity reference. `Survey` is shared as the survey definition, but it contains no per-student identity information.
