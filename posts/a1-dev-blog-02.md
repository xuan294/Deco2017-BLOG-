---
title: Planning Structure, Constraints, and Feasibility for the Meetup Prototype
date: 2026-03-27
author: xuan
summary: Uses site structure, user flow, and data modelling to evaluate the implementation path of a restaurant meetup community website and assess the feasibility of its MVP within the course constraints.
tags:
  - A1
  - feasibility
  - architecture
  - htmx
---
After defining the core functions of my restaurant meetup website, the next step is to test whether the idea is actually practical within the course constraints. In this blog post, I use three planning tools to organise the concept: a site structure, a user flow, and a basic data model. Instead of only describing what I want to build, these tools help me analyse whether I can build it and which parts should be prioritised first.

## Key project constraints

According to the design brief, there are several constraints that cannot be ignored:

1. The core technology stack must use MojoJS, SQLite, and HTMX.
2. User authentication is handled by BlaBla Corp, so I should rely on session data rather than rebuilding the registration system.
3. The website must support both desktop and mobile devices.
4. Accessibility needs to meet AA standard or higher.
5. Cookie and tracking behaviour must comply with EU policies.
6. Ideal load times should be below 1 second and must not exceed 3 seconds.

These constraints directly affect design decisions. For example, since the course already specifies the stack, I should not introduce a heavy front-end framework because that would add complexity and risk moving away from the assignment requirements. In the same way, because the username can be accessed through the session stash, I should avoid unnecessary repeated database queries.

## Site structure planning

My current site structure is intentionally simple:

```mermaid
flowchart TD
    A[Home Feed] --> B[Meetup Detail]
    A --> C[Create Meetup]
    A --> D[Filtered Meetup Results]
    L[Login] --> A
    B --> E[Join Meetup]
    B --> F[Leave Meetup]
```

This structure covers the main tasks without becoming too difficult to implement. The home feed works as the central entry point of the whole website. From there, users can browse current meetup cards, open the creation form, or refine results through filters. The meetup detail page becomes the main interaction area because joining, leaving, and reading the full plan all happen there.

## Core user flow

I believe the most important flow in this prototype is:

1. The user opens the home feed.
2. The user chooses to create a new meetup.
3. The user submits the restaurant, time, photo URL, seat count, payment mode, and safety acknowledgement.
4. The system saves the meetup and returns the user to the meetup detail page.
5. Other users browse the meetup and decide whether to join or leave.

This flow matters because it shows the core value of the platform. If creating and joining a meetup feels clear and reliable, then the main concept of the website works. On the other hand, if the flow is confusing or if seat information becomes inaccurate, the prototype will struggle even if many extra features are added.

## Initial data model

To check whether the database structure is manageable, I broke the system into several main entities:

```mermaid
erDiagram
    USERS ||--o{ MEETUPS : creates
    USERS ||--o{ MEETUP_PARTICIPANTS : joins
    MEETUPS ||--o{ MEETUP_PARTICIPANTS : contains
```

Based on this model, I expect to need at least the following tables:

- `users`
- `meetups`
- `meetup_participants`

This structure is feasible in SQLite and is strong enough to support the MVP without becoming overdesigned. The relationships between the tables are also clear, which should make it easier later to render the home feed, count participation, and stop duplicate joins.

## Feasibility analysis

I believe the project itself is feasible. The real risk is not whether I can build an image upload and browsing system, but whether the scope becomes too large. In other words, the problem is less about technical possibility and more about trying to do too much and ending up with incomplete features.

For example, direct messaging, identity verification systems, recommendation logic, and complex moderation dashboards are all attractive ideas, but they would quickly increase the number of routes, database relationships, and interface states. If I try to include all of them during the prototype stage, development time will be spread too thin and the core experience may become less stable.

For that reason, a more realistic MVP should include:

- a recent meetup feed
- a meetup creation form
- a meetup detail page
- join and leave actions
- filter controls for practical criteria
- responsive layout

This feature set is enough to test whether the concept of a restaurant meetup community website works, while also creating a good balance between technical complexity and user value.

## Technical approach

HTMX is especially useful for this project because I can apply progressive enhancement only where smoother interaction matters most, such as:

- dynamically replacing the feed during filtering
- progressively enhancing join and leave actions
- reducing full page refreshes for simple state updates later

This approach supports performance goals, stays lighter than a full single-page application, and fits the required course stack more closely. In other words, I am not avoiding MojoJS and HTMX, but using them to improve interaction in a practical way.

SQLite is also a good fit for this project because the data relationships are not too deep. A meetup belongs to one organiser, and a participation record links one user to one meetup. This is simple enough to model clearly while still allowing useful behaviour such as counting seats, detecting full meetups, and blocking duplicate participation.

## Accessibility and quality considerations

Accessibility needs to be considered from the beginning rather than added at the end. Because this platform depends on users reading practical planning information and completing forms, I need to pay particular attention to:

- meaningful text labels for forms and controls
- readable error messages during meetup creation
- colour contrast in the interface
- keyboard accessibility for forms and buttons
- clear communication of seat counts and participation status

Because the project involves in-person meetings, I also need to consider responsible implementation. This means the prototype should avoid collecting unnecessary sensitive information and should make public-venue safety guidance visible in the interface.

This is not only a formal requirement from the brief, but also a core usability issue. If users cannot navigate the interface smoothly or understand the meetup information clearly, the community experience will break down.

## Current conclusion

From the current planning, this prototype is achievable and aligns well with the brief, as long as I focus on the primary experiences of creating, browsing, and joining meetups rather than introducing complex social features too early. The most important insight at this stage is that information structure and user flow are just as important as visual design. If the home feed, meetup detail page, and creation process are clear, the project will already have a stable foundation for A2 development.
