---
layout: post
title: OO Design - Course Enrollment System
---

I made an object-oriented design of course enrollment system. See the whole project [here](https://github.com/zhtiansweet/CourseEnrollment).

## Enrollment Rules
* Each course has three status: open, wl(waiting list) and close. When initialized, a course's status will be set as "open".
* Each course has two student lists. One is for students that have been enrolled successfully, and the other is for students on the waiting list. 
* When a student adds a course, (s)he will be prior added to the first list. When it is full, the course status will be set as "wl", and students will be added to the waiting list then. And when the waiting list is full, the course status will be set as "close", and students couldn't select this course anymore.
* When a student delete a course, (s)he will be deleted from the lists. And if there appears a position on the "enrolled" list, the first student on the waiting list will be enrolled. Besides, the course status will change correspondingly.
* A student could select as many as 4 courses. Duplicated courses couldn't be selected.
* Undergraduate students could only select courses with id under 400, and Graduate students could only select courses with id over 300.
