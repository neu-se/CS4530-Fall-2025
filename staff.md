---
layout: page
title: Staff
description: A listing of all the course staff members.
nav_order: 6
---

# Staff

For technical questions related to the codebase, please check piazza first (or post a query there). For discussing the course material or the individual projects, please feel free to attend whichever TA's office hours are convenient. For project-related questions, please coordinate a time to chat directly with your assigned project mentor.

## Office Hours 
All TA office hours will be held virtually. We will explore the options of holding in-person office hours too, subject to interest from students/TAs and availability of a room. Instructor office hours may be held in-person or remotely.  

TA Office Hours are hosted on Microsoft Teams, using the [Khoury Office Hours app](https://officehours.khoury.northeastern.edu/). Please see the user guide for information on how to log in and ask questions.

**We usually do not hold office hours during school holidays (Indigenous Peoples' Day, Veteran's Day and Thanksgiving Break)**

## Schedule
{% include officeHours.html %}

## Instructors
{% assign instructors = site.staffers | where: 'role', 'Instructor' %}
{% for staffer in instructors %}
{{ staffer }}
{% endfor %}

{% assign teaching_assistants = site.staffers | where: 'role', 'Teaching Assistant' %}
{% assign num_teaching_assistants = teaching_assistants | size %}
{% if num_teaching_assistants != 0 %}
## Teaching Assistants
{% for staffer in teaching_assistants %}
{{ staffer }}
{% endfor %}
{% endif %}



