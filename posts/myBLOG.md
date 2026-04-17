---
title: Defining Functional Requirements for an Image Sharing Community Hub
date: 2026-03-20
author: Your Name
summary: Analyze the target users, core tasks, and MVP feature requirements of the image sharing community website, and explain the reasons behind the priority of the features
tags:
  - A1
  - requirements
  - planning
  - image-sharing
---
For my A2 prototype, I plan to build an image sharing community hub for people who want to post, browse, and discuss visual content around a shared interest. At this stage, my focus is not on building every possible social feature. Instead, I need to assess what functions are necessary for the site to be useful, realistic, and aligned with the BlaBla Corp brief.

## Project idea

My concept is a community hub where logged-in users can share images, organise them with captions and tags, and interact with other posts. The platform is designed for people who want a simple space to publish visuals and discover content from others in the same community.

This idea fits the brief because the central value of the site is information shared by members. In this case, the main information object is an image post, supported by text metadata such as a caption, tags, author name, and upload date.

## Target users

The main audience is active community members who want to:

- upload their own images quickly
- browse recent posts from other members
- search or filter content by tag
- view post details and comments
- interact with content in a lightweight way

Because the brief states that users are already logged in through BlaBla Corp, I do not need to build full account registration. This reduces scope and lets me focus on the content-sharing workflow.

## Core functional requirements

I used a simple MoSCoW-style priority list to separate essential features from desirable extras.

### Must have

1. Logged-in users can view a home feed of image posts.
2. Logged-in users can upload a new post with an image, title or caption, and tags.
3. Users can open a post detail page to view the image and related information.
4. Users can leave comments on a post.
5. Users can filter or search posts by tag.
6. The layout works on desktop and mobile.

### Should have

1. Users can like or favourite a post.
2. Users can delete their own post.
3. Users can view a simple profile page showing their uploaded images.

### Could have

1. Infinite scroll or asynchronous feed updates with HTMX.
2. Notifications for new comments or likes.
3. Image collections or albums.

### Will not have for the prototype

1. Complex image editing tools.
2. Real-time chat.
3. Advanced recommendation algorithms.
4. Full multi-community management.

These exclusions are important because the project is a prototype, and the brief also warns against placeholder-heavy or unrealistic features. A strong prototype should demonstrate a clear and functional core, not a large number of unfinished extras.

## User stories

To keep the design user-centred, I translated the requirements into short user stories:

- As a logged-in user, I want to upload an image with a caption so I can share it with the community.
- As a browsing user, I want to filter posts by tag so I can find content I care about.
- As a community member, I want to comment on a post so I can respond to what others share.
- As a mobile user, I want the interface to remain readable and usable on a small screen.

These stories show that the system is not only about storing images. It also needs to support discovery, feedback, and accessibility.

## Main design decisions so far

One early decision is to keep interaction patterns lightweight. Since the required stack includes MojoJS, SQLite, and HTMX, I can design the application so that key actions such as posting comments, filtering by tag, or liking a post can happen with partial page updates instead of full page reloads.

Another decision is to treat metadata as essential. A raw image feed is not enough for a community hub, because users need context to understand why an image matters. Captions, tags, author names, and timestamps therefore become part of the functional requirements, not optional decoration.

## Why these requirements are feasible

The selected core features are realistic within the template constraints because they map directly to common CRUD operations:

- create a post
- read posts and post details
- create comments
- filter posts by tag

This makes the prototype achievable using SQLite tables and server-rendered views enhanced by HTMX. It also supports clear testing later in A3, especially around usability, accessibility, and performance.

At this point, I believe the strongest MVP is a site that does a small number of things well: upload, browse, filter, and discuss images. That gives the project a clear purpose and stays closely aligned with LO1, because I am assessing which functions are essential for the application to work for its intended users.
