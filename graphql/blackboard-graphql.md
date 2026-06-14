# Blackboard GraphQL Schema

## Overview

This document describes a conceptual GraphQL schema for the Blackboard (Anthology) Learn LMS REST API. Blackboard Learn exposes its capabilities through a REST API at https://developer.blackboard.com/portal/displayApi, covering courses, users, grades, content, announcements, discussions, groups, attendance, calendar events, LTI placements, and system administration.

The schema below maps the primary REST resources into GraphQL types, queries, and mutations to provide a unified graph interface over the Blackboard Learn platform.

## Provider

- **Name**: Blackboard (Anthology)
- **Developer Portal**: https://developer.blackboard.com/
- **REST API Reference**: https://developer.blackboard.com/portal/displayApi
- **Product Suite**: Blackboard Learn, Anthology Ally, Anthology Student

## Schema Source

This GraphQL schema is derived from the Blackboard Learn REST API documentation. Blackboard does not publish a native GraphQL endpoint; this schema represents a conceptual mapping of REST endpoints to GraphQL types and resolvers.

## Key Resource Areas

### Courses
Courses are the central resource in Blackboard Learn. The API supports full CRUD operations on courses, enrollment, availability, templates, and terms.

### Users
User management covers creating, updating, and retrieving user accounts, personal info, contact info, and system roles.

### Grades
The grading subsystem exposes grade columns, attempts, gradebook entries, rubrics, rubric criteria, and grading periods.

### Content
Course content is organized into folders and items: documents, attachments, assignments, tests, and assessments.

### Announcements and Discussions
Announcements can be scoped to courses or system-wide. Discussions are organized into forums, threads, and posts.

### Groups
Courses can contain groups with their own membership lists.

### Attendance
Attendance records are tracked per meeting and per student.

### Calendar
Calendar events are associated with courses or institutions.

### LTI
LTI placements allow external tools to be embedded in courses.

### Webhooks and OAuth
Webhooks deliver event notifications. OAuth tokens and API keys control access.

## Types Summary

| Type | Description |
|---|---|
| Course | Core course record |
| CourseDetails | Extended course metadata |
| CourseEnrollment | Enrollment record linking a user to a course |
| CourseAvailability | Availability window for a course |
| CourseCatalog | Catalog-level course listing |
| CourseTerm | Term associated with a course |
| CourseTemplate | Template used to create courses |
| Grade | Single grade value |
| GradeColumn | Column definition in a gradebook |
| GradeColumnAttempt | A student attempt on a grade column |
| GradeAttemptDetails | Detailed attempt metadata |
| ContentItem | Generic content item in a course |
| ContentFolder | Folder grouping content items |
| Document | Document content item |
| Attachment | File attached to a content item |
| Assignment | Assignment content item |
| TestDetails | Metadata for a test/quiz |
| Assessment | Assessment record |
| Announcement | Course or system announcement |
| AnnouncementCourse | Course-scoped announcement |
| Discussion | Discussion resource |
| Forum | Discussion forum |
| Thread | Thread within a forum |
| Post | Individual post in a thread |
| PostDetails | Extended post metadata |
| UserDetails | Extended user metadata |
| User | Core user account |
| UserPersonInfo | Personal information for a user |
| UserContactInfo | Contact information for a user |
| EnrollmentDetails | Detailed enrollment record |
| Membership | Group or course membership |
| Instructor | Instructor role record |
| Student | Student role record |
| GradebookEntry | Entry in the gradebook |
| GradebookColumn | Gradebook column definition |
| Rubric | Grading rubric |
| RubricDetails | Extended rubric metadata |
| RubricCriterion | Individual criterion in a rubric |
| GradingPeriod | Grading period definition |
| Group | Course group |
| GroupMembership | Membership record for a group |
| Institution | Top-level institution record |
| Term | Academic term |
| TermEnrollment | Enrollment scoped to a term |
| Meeting | Course meeting/session |
| Attendance | Attendance summary |
| AttendanceRecord | Individual attendance record |
| Calendar | Calendar resource |
| CalendarEvent | Event on a calendar |
| LTI | LTI configuration |
| LTIPlacement | Placement of an LTI tool in a course |
| Webhook | Webhook subscription |
| WebhookEvent | Event delivered by a webhook |
| OAuth | OAuth configuration |
| APIKey | API key credential |
| Token | OAuth access token |
| Role | System or course role |
| Permission | Permission attached to a role |
| SystemRole | System-level role assignment |
| CourseRole | Course-level role assignment |
| SISData | SIS integration data record |
| DataSource | Data source mapping for SIS integrations |

## Queries

- `course(id: ID!)`: Fetch a single course by ID
- `courses(filter: CourseFilter)`: List courses with optional filters
- `user(id: ID!)`: Fetch a single user
- `users(filter: UserFilter)`: List users
- `enrollment(courseId: ID!, userId: ID!)`: Fetch a specific enrollment
- `enrollments(courseId: ID!)`: List all enrollments for a course
- `gradeColumn(courseId: ID!, columnId: ID!)`: Fetch a grade column
- `gradeColumns(courseId: ID!)`: List grade columns for a course
- `contentItem(courseId: ID!, contentId: ID!)`: Fetch a content item
- `contentItems(courseId: ID!, folderId: ID)`: List content items
- `announcement(courseId: ID!, announcementId: ID!)`: Fetch an announcement
- `announcements(courseId: ID!)`: List announcements
- `forum(courseId: ID!, forumId: ID!)`: Fetch a discussion forum
- `forums(courseId: ID!)`: List forums
- `group(courseId: ID!, groupId: ID!)`: Fetch a group
- `groups(courseId: ID!)`: List groups
- `term(id: ID!)`: Fetch a term
- `terms`: List all terms
- `calendarEvent(id: ID!)`: Fetch a calendar event
- `calendarEvents(filter: CalendarFilter)`: List calendar events
- `webhook(id: ID!)`: Fetch a webhook
- `webhooks`: List all webhooks

## Mutations

- `createCourse(input: CourseInput!)`: Create a new course
- `updateCourse(id: ID!, input: CourseInput!)`: Update a course
- `deleteCourse(id: ID!)`: Delete a course
- `createEnrollment(input: EnrollmentInput!)`: Enroll a user in a course
- `deleteEnrollment(courseId: ID!, userId: ID!)`: Remove an enrollment
- `createGradeColumn(courseId: ID!, input: GradeColumnInput!)`: Create a grade column
- `updateGrade(courseId: ID!, columnId: ID!, userId: ID!, input: GradeInput!)`: Update a grade
- `createAnnouncement(courseId: ID!, input: AnnouncementInput!)`: Create an announcement
- `createPost(courseId: ID!, forumId: ID!, threadId: ID!, input: PostInput!)`: Create a post
- `createGroup(courseId: ID!, input: GroupInput!)`: Create a group
- `createWebhook(input: WebhookInput!)`: Register a webhook
- `deleteWebhook(id: ID!)`: Delete a webhook
