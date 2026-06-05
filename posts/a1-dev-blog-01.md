---
title: Defining Functional Requirements for a Restaurant Meetup Community Hub
date: 2026-03-20
author: xuan
summary: Analyses the target users, core tasks, and MVP feature requirements of a restaurant meetup community website, and explains the reasoning behind feature priorities.
tags:
  - A1
  - requirements
  - planning
  - meetup-planning
---
My A2 prototype will be a community hub for arranging small group restaurant meetups. Instead of building a broad social network, I want to focus on one clear activity: helping logged-in users create public dining plans, state their expectations, and let other users join those plans. At this stage, the task is not to imagine every possible feature, but to decide which functions are genuinely necessary for the prototype. According to the course brief, this phase is about defining functional requirements, so I am starting with user goals and core tasks.

## Project concept

My website idea is a community hub where users can organise restaurant meetups with other members of the BlaBla Corp network. A logged-in user can create a meetup by providing the restaurant name, the date and time, a photo URL, the number of seats, the payment arrangement, and optional notes. Other users can browse current meetups, open a detail page, and decide whether to join or leave.

This direction fits the BlaBla Corp brief well because the brief states that the core value of a community hub comes from information and shared experience. In my project, the key information object is not an image post or a profile page, but a meetup plan. Users are exchanging practical information that helps them gather in person: where to meet, when to meet, how many seats are available, and what payment expectations apply.

## Target users

My main user group is BlaBla Corp members who want to make casual restaurant plans with clearer expectations and lower coordination effort. They want to:

- create a meetup quickly without writing long messages
- browse current dining plans from other users
- understand the practical details before joining
- join or leave a meetup without confusion
- filter options to find plans that suit their availability or preferences

Because the brief explains that users are already logged in through BlaBla Corp, I do not need to design a full registration system. This is important because it reduces the project scope and allows me to focus on the meetup workflow rather than account management.

## Core functional requirements

To make the requirements clearer, I used a MoSCoW-style priority approach so the prototype scope does not grow beyond what is realistic.

### Must have

1. Logged-in users can view a home feed of current restaurant meetups.
2. Logged-in users can create a new meetup with key details such as venue, time, seats, photo URL, and payment mode.
3. Users can open a meetup detail page to view the full plan and current participant status.
4. Users can join a meetup if seats are still available.
5. Users can leave a meetup if they change their mind.
6. Users can filter meetups by practical criteria such as payment mode, open spots, preference, or time window.
7. The interface works on both desktop and mobile devices.

### Should have

1. The system should prevent duplicate joining and over-capacity bookings.
2. The interface should provide clear safety guidance for in-person meetings.
3. The form should provide validation feedback before invalid meetup data is accepted.

### Could have

1. Smoother asynchronous filtering using HTMX.
2. A richer profile history of meetups created or joined.
3. Lightweight reminders or notifications before a scheduled meetup.

### Will not have for the prototype

1. Direct messaging between users.
2. Real-time chat.
3. Background identity verification.
4. Complex recommendation or matching algorithms.

These exclusions are just as important as the included features. This course project is a prototype, not a commercial-scale product. If I try to include too many features, the result may rely on too much placeholder data, contain incomplete workflows, and weaken the core user experience. A strong prototype should first do the most valuable tasks well.

## User stories

To make the requirements more realistic, I translated the core functions into user stories:

- As a logged-in user, I want to create a meetup with clear practical details so other people know what I am inviting them to.
- As a browsing user, I want to filter meetup options so I can find plans that fit my time and expectations.
- As a participant, I want to join or leave a meetup easily so I can manage my plans without messaging the organiser separately.
- As a cautious user, I want visible safety guidance so I feel more confident about meeting in person.
- As a mobile user, I want the interface to remain clear and usable on a small screen.

These user stories show that the system is not only about storing meetup records in a database. It also needs to support content discovery, clear decision making, and responsible communication, otherwise the community aspect becomes much weaker.

## Current design decisions

My first major design decision is to keep the interaction pattern lightweight. Because the required technology stack is MojoJS, SQLite, and HTMX, I do not need to introduce a heavier front-end framework. A server-rendered home feed, detail page, and create form are enough for the MVP, while HTMX can be used later to improve filtering or partial updates if needed.

My second decision is to treat planning information as part of the core functionality. A simple list of restaurant names would not be enough for users to decide whether to join. They need to know the time, organiser, seat count, payment mode, and any notes about the plan. For that reason, these data fields need to be clearly supported in both the database structure and the interface.

My third decision is to include responsible implementation from the beginning. Because the project involves meeting strangers or semi-strangers in person, I need to think carefully about what data is actually necessary. For example, I do not need phone numbers, private addresses, or file uploads. A simple photo URL is enough for a visual reference, and the design should encourage public venues and clear expectations.

## Why these requirements are feasible

The core functions I selected are feasible because they map clearly to standard CRUD operations:

- create meetup records
- read the home feed and meetup detail pages
- create participation records
- delete participation records when users leave
- filter meetups by selected criteria

This makes them suitable for implementation with SQLite tables and server-rendered templates, enhanced by HTMX where smoother interaction is useful. The scope is realistic for the A2 prototype and will also make it easier to discuss usability, accessibility, performance, and responsible implementation later in the A3 reflection.

At this point, the most reasonable MVP is not a social website with many features, but a website that handles creating, browsing, joining, and filtering meetup plans smoothly. This approach aligns well with LO1 because it focuses on identifying the functions that are genuinely necessary for the application to work for its intended users.
