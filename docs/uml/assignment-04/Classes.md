# Classes — Lab Assignment 4

## Project Identification
- **Project:** Student Feedback Management System
- **Team ID:** T037
- **Course:** Software Development Laboratory (CS314)
- **Use cases:** UC-003 Create Survey Template; UC-008 Submit Course Feedback; UC-012 View Course Analytics & Charts

## Final Class List

| # | Class | Responsibility | Traceability |
|---|---|---|---|
| 1 | User | Represents authenticated users and their roles. | Assignment 2; UC-003, UC-008, UC-012 |
| 2 | Course | Represents an academic course. | Assignment 2; UC-003, UC-012 |
| 3 | CourseAllocation | Assigns faculty to a course section. | Assignment 2; UC-003, UC-012 |
| 4 | Enrollment | Links a student to a course allocation. | Assignment 2; UC-008 |
| 5 | Survey | Represents a feedback survey/template and its lifecycle. | Assignment 2; UC-003, UC-008, UC-012 |
| 6 | SurveyQuestion | Represents a question belonging to a survey. | Assignment 2; UC-003, UC-008 |
| 7 | QuestionOption | Represents selectable options for choice-type questions. | Assignment 2 question-option data; UC-003 |
| 8 | SurveyTrackingRecord | Records that a student submitted a survey, without answer content. | Assignment 2; UC-008 |
| 9 | SurveyResponsePayload | Anonymous submission envelope. | Assignment 2; UC-008 |
| 10 | AnswerEntry | Stores an answer value for a survey question. | Assignment 2; UC-008 |
| 11 | FeedbackAggregate | Stores computed feedback statistics and threshold state. | Assignment 2; UC-012 |

## Class Specifications

### User
**Attributes:** user_id, full_name, institutional_email, role, department, account_status.  
**Operations:** authenticate(credentials), logout().

### Course
**Attributes:** course_id, course_title, department, semester, academic_year.

### CourseAllocation
**Attributes:** allocation_id, course_id, faculty_id, section.

### Enrollment
**Attributes:** enrollment_id, student_id, allocation_id, academic_session.

### Survey
**Attributes:** survey_id, title, description, survey_type, target_entity_id, status, start_timestamp, end_timestamp, created_by.  
**Operations:** createTemplate(), publish(), close(), validate().

### SurveyQuestion
**Attributes:** question_id, question_text, question_type, is_mandatory, order_index.  
**Operation:** addOption(text).

### QuestionOption
**Attributes:** option_id, option_text, order_index.

### SurveyTrackingRecord
**Attributes:** tracking_id, survey_id, student_id, has_submitted, submitted_at.  
**Operations:** markSubmitted(), isDuplicate().

### SurveyResponsePayload
**Attributes:** response_id, submitted_at.  
**Operation:** recordAnswer(question, value).

### AnswerEntry
**Attributes:** answer_id, answer_value.

### FeedbackAggregate
**Attributes:** aggregate_id, average_rating, std_deviation, response_count, computed_at.  
**Operations:** computeMetrics(), isBelowThreshold().

## Modelling Note
The `QuestionOption` class is a UML-level decomposition of the choice-option data represented in the earlier data model; it does not introduce a new feature. The `User` class retains the role attribute rather than introducing an inheritance hierarchy, preserving the established data model.
