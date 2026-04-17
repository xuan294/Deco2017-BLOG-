---
title: Defining Functional Requirements for an Image Sharing Community Hub
date: 2026-03-20
author: xuan
summary: Analyses the target users, core tasks, and MVP feature requirements of an image sharing community website, and explains the reasoning behind feature priorities.
tags:
  - A1
  - requirements
  - planning
  - image-sharing
---
My A2 prototype will be an image sharing community website where users with a common interest can upload pictures, browse content, and interact around visual posts. At this stage, the goal is not to build every possible social feature. Instead, I need to identify which functions are truly necessary and which ideas only appear attractive but are not suitable for the prototype stage. According to the course brief, this phase is about assessing functional requirements, so I am starting with user goals and core tasks.

## Project concept

My website idea is a community hub for a specific interest group. Logged-in users can publish images, add a title or caption, assign tags, and view content from other users. Unlike a simple static gallery, this platform focuses on information exchange within a community. The image is the core content item, but the tags, comments, author details, and upload time are also important parts of the experience.

This direction fits the BlaBla Corp brief well because the brief clearly states that the central value of the platform comes from information shared by members. In my project, the most important information object is the image post rather than a profile page or advertising feature.

## Target users

My main user group is community members who want to consistently upload and browse image-based content. They want to:

- upload their own image posts quickly
- browse recent content from other users
- filter topics through tags
- open individual posts and read comments
- interact with others in a lightweight way

Because the brief explains that users are already logged in through BlaBla Corp, I do not need to design a full registration system. This is important because it reduces the project scope and allows me to focus on the content-sharing workflow instead of account management.

## Core functional requirements

To make the requirements clearer, I used a MoSCoW-style priority approach so the prototype scope does not grow beyond what is realistic.

### Must have

1. Logged-in users can view a home feed of image posts.
2. Logged-in users can upload a new image with a title or caption and tags.
3. Users can open a post detail page to view the image and related information.
4. Users can leave comments on a post.
5. Users can search or filter posts by tag.
6. The interface works on both desktop and mobile devices.

### Should have

1. Users can like or favourite a post.
2. Users can delete their own posts.
3. Users can view a simple profile page showing the images they have uploaded.

### Could have

1. Smoother asynchronous feed updates using HTMX.
2. Notifications for new comments or likes.
3. Image collections or album features.

### Will not have for the prototype

1. Advanced image editing tools.
2. Real-time chat.
3. Complex recommendation algorithms.
4. Multi-community management dashboards.

These exclusions are just as important as the included features. This course project is a prototype, not a commercial-scale product. If I try to include too many features, the result may rely on too much placeholder data, contain incomplete workflows, and weaken the core user experience. A strong prototype should first do the most valuable tasks well.

## User stories

To make the requirements more realistic, I translated the core functions into user stories:

- As a logged-in user, I want to upload an image with a caption so I can share it with the community.
- As a browsing user, I want to filter posts by tag so I can find the content I care about more quickly.
- As a community member, I want to comment on a post so I can respond to other users.
- As a mobile user, I want the interface to remain clear and usable on a small screen.

These user stories show that the system is not only about storing images. It also needs to support content discovery, user feedback, and basic accessibility, otherwise the community aspect becomes much weaker.

## Current design decisions

My first major design decision is to keep interaction patterns lightweight. Because the required technology stack is MojoJS, SQLite, and HTMX, I do not need to introduce a heavier front-end framework. Actions such as posting comments, filtering by tag, and liking a post can be handled through partial updates with HTMX instead of refreshing the entire page every time.

My second decision is to treat metadata as part of the core functionality. A simple image feed cannot fully support a community hub, because users need to know what a post is about, who posted it, when it was posted, and how other people responded to it. For that reason, captions, tags, authors, and timestamps all need to be clearly supported in both the database structure and the interface.

## Why these requirements are feasible

The core functions I selected are feasible because they map clearly to standard CRUD operations:

- create image posts
- read the feed and post detail pages
- create comments
- filter posts by tag

This makes them suitable for implementation with SQLite tables and server-rendered templates, enhanced by HTMX for better interaction. The scope is realistic for the A2 prototype and will also make it easier to discuss usability, accessibility, and performance later in the A3 reflection.

At this point, the most reasonable MVP is not a website with many features, but a website that handles uploading, browsing, filtering, and discussion smoothly. This approach aligns well with LO1 because it focuses on identifying the functions that are genuinely necessary for the application to work for its intended users.
