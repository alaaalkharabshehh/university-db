
# Database Schema Fixes

## 1. Students Primary Key
The students table was missing a primary key on the id column.
This was a problem because each student needs a unique identifier.
Added [pk] to the id column.

## 2. Student Email Uniqueness
The students email column did not enforce unique values.
This could allow two students to share the same email.
Added [unique] to the email column.

## 3. Date of Birth Data Type
The date_of_birth column used varchar.
This was incorrect because the column stores dates, not general text.
Changed its type to date.

## 4. Instructor Name Convention
The instructors table used FullName instead of the naming convention used by the other columns.
Renamed it to full_name.

## 5. Course Credit Hours Data Type
The credit_hours column used varchar.
Credit hours should be stored as a number.
Changed its type to integer.

## 6. Enrollment Student ID Data Type
The enrollments.student_id column used varchar while students.id uses integer.
Changed student_id to integer to match the referenced primary key.

## 7. Course Instructor Requirement
The courses.instructor_id column was nullable.
Every course must be taught by one instructor.
Added [not null].

## 8. Department-Course Relationship Direction
The relationship between departments and courses pointed in the wrong direction.
Changed it to Ref: courses.department_id > departments.id.

## 9. Instructor-Department Relationship
The instructors.department_id column was missing a foreign key relationship.
Added Ref: instructors.department_id > departments.id.

## 10. Enrollment-Course Reference
The enrollment relationship referenced courses.course_id, which does not exist.
Changed it to reference courses.id.

## 11. Student-Course Many-to-Many Relationship
The courses table contained a student_id column, which incorrectly represented the many-to-many relationship.
Removed it because enrollments is the middle table connecting students and courses.

## 12. Duplicate Instructor Information
The courses table contained instructor_name even though instructor information is already stored in the instructors table.
Removed instructor_name to avoid duplicated data.
