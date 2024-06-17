---
layout: post
title: Definition of Done
date: 2024-06-17 11:17 +0200
categories: [Knowledge, DoD, Agile, Scrum, Kanban, SWAT]
tags: [docker, docker-compose, swat]
description: This post is about the DoD (Definition of Done).
---
# Definition of Done (DoD)
The Definition of Done (DoD) is a list of requirements that a user story must meet before it can be considered complete.
Mostly it is used in Agile software development, especially in Scrum and Kanban.
It's defined by the SCRUM-Team and will be continuously updated and improved.
From Sprint to Sprint, the DoD should be reviewed and updated if necessary.



## Goals
- Ensure that the development team has completed the work on a user story.
- Ensure that the formal requirements for a user story of the product owner are met.
- Ensure a fast and efficient workflow and project management meetings.
- Ensure what is meant by "done" for every PBI is clear to everyone involved in the project.

## Difference to Acceptance Criteria
The DoD is often confused with the acceptance criteria.
The acceptance criteria are the requirements that a user story must meet to be accepted by the product owner.
The DoD, on the other hand,
is a list of requirements that a user story must meet before it can be considered complete.  

Basically, the DoD is a superset of the acceptance criteria that are aimed at the user story itself
and are only administrative in nature,
whereby the acceptance criteria are aimed at the task described in the user story.

## Example
The DoD can vary from project to project.
Here is an example of elements that could be included in a DoD:
- The code is written according to the coding guidelines.
- The code is reviewed by a team member.
- The code is tested by the developer.
- The test coverage is at least 60%.
- The code passes the CI pipeline.
- The code is deployed to the test environment.
- The code is documented as far as necessary.
- No open sonarlint issues, except the ones that are not relevant. (The List of the irrelevant issues is documented)
- The corporate design guidelines are followed.
- Every text from a foreign language is translated by the company's translation service.

(the percentage is project-specific, 100% makes no sense at all, because anyone can test that testing has been done. In the end, there should only be useful tests)

## Conclusion
The Definition of Done is a crucial part of the Agile development process.
It ensures that the development team and the product owner are on the same page about what it means for a user story to be complete.
It also helps to ensure that the development team is following best practices and producing high-quality code.
By defining and enforcing a DoD, the development team can improve their workflow and deliver better products to their customers.
It is done by the development team and should be reviewed and updated regularly.


## Sources
- [Atlassian: Definition of Done](https://www.atlassian.com/agile/scrum/definition-of-done)
- [Agile Scrum Group](https://agilescrumgroup.de/definition-of-done/)
