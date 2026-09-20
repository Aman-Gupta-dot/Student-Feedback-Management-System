# Object Model — Lab Assignment 4

## Selected Scenario
**UC-008 — Submit Course Feedback**

The object diagram is a snapshot immediately after a student's feedback has been accepted. The identified side contains the user, enrollment, course allocation and survey tracking record. Separately, the survey owns an anonymous response payload containing an answer entry for a survey question. No direct object link connects the user/tracking record to the response payload or answer entry, preserving the anonymity requirement.

## Representative Objects

| Object | Class | Representative values |
|---|---|---|
| u | User | user_id = U205; role = Student |
| tr | SurveyTrackingRecord | tracking_id = TRK-4471; student_id = U205; survey_id = SUR-0031; has_submitted = true |
| en | Enrollment | enrollment_id = ENR-501; student_id = U205; allocation_id = ALLOC-12 |
| ca | CourseAllocation | allocation_id = ALLOC-12; section = B |
| sv | Survey | survey_id = SUR-0031; title = Mid-Sem Feedback - CS314-B; status = Active |
| rp | SurveyResponsePayload | response_id = RESP-0091; submitted_at = 2026-09-15 10:42 |
| ae | AnswerEntry | answer_id = ANS-1183; answer_value = 4 |
| q | SurveyQuestion | question_id = Q-118; question_text = Rate pace of lectures; question_type = LikertScale |

## Anonymity Note
The object diagram deliberately contains no line from `u : User` or `tr : SurveyTrackingRecord` to `rp : SurveyResponsePayload` or `ae : AnswerEntry`. Tracking identifies only the fact of submission; response data remain structurally separate from respondent identity.
