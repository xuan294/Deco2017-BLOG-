---
title: "Reflecting on TableTogether: Performance, Usability, and Lessons Learned"
date: 2026-06-05
author: xuan
summary: "A critical evaluation of the TableTogether prototype, assessing its performance on a live deployment, evaluating user experience and accessibility, and reflecting on the original functional requirements from A1."
tags:
  - A3
  - evaluation
  - reflection
  - performance
  - accessibility
---

Developing a functional web application is part of the picture – knowing how it is going to perform in the users' hands and in the real world can make the difference between this being a coding exercise and proper software development. For this final reflection, I am going to be analysing TableTogether – a prototype of a community hub where people can organise and participate in small group meetups at restaurants. 

Unlike my A1 posts that were focused on planning and requirements, this is a retrospective post. I will evaluate the performance of my deployed application, try to perform a user experience (UX) and accessibility evaluation, and then reflect on my decisions and change my initial functional requirements based on the actual prototype that I built.

## 1. Evaluation of Performance and Technical Behaviour

To assess the actual performance of the application, I uploaded the prototype to Render, a widely used cloud-hosting platform, with one Node.js runtime and a persistent SQLite database. This gave me the chance to cross the "it works on my machine" barrier and to run the app in real network environments.

To collect objective evidence, I used Google Chrome's Lighthouse audits for the deployed home page and meetup creation page.

![Lighthouse Score](/assets/lighthouse_report.png)
> **Evidence 1:** Lighthouse performance audit showing scores for Performance (100), Accessibility (95), Best Practices (100), and SEO (90).

**What Performs Well**
The overall performance of the application (speed and responsiveness) is excellent, scoring 100 in the Lighthouse Performance category. A major benefit that emerged was the decision to opt for a server-side framework like MojoJS for HTML templates rather than a framework that is heavier on the front end, like React. The initial First Contentful Paint (FCP) is very fast due to the browser getting fully formed HTML straight from the server.

Filtering performance also was improved through HTMX integration. Instead of reloading the whole page whenever the user switches a filter, he/she is sent a “lightweight” asynchronous request (such as "split bill" meetups). The server only returns the updated meetup-list HTML fragment; interactions remain fast, and complex JSON API is avoided.

**Where it Struggles**
However, there was an issue with image handling when it was deployed. In order to make the MVP simple, I used external photo URLs rather than uploading photos locally so that page load would be dependent on the hosting server. Images from slow servers may take a long time to load and could make layout shifts. The free tier of Render also introduces the concept of “cold starts," where the container can take a few seconds to wake up after 15 minutes of the site's inactivity, demonstrating an infrastructure limitation, rather than code inefficiency.

## 2. Evaluation of User Experience and Accessibility

If users are not able to perform their tasks easily, then a technically fast application becomes useless. I evaluated some of the core user flows—browsing meetups, creating a plan, and joining events.

![Mobile View](/assets/test1-moblie.png)
![Create Meetup Validation](/assets/test2-blank-restaurant-name.png)
> **Evidence 2:** Screenshots demonstrating the responsive design of the meetup cards on a mobile viewport and clear form validation states.

**Navigation and Interaction Flow**
The flow of interaction is simple. “Create Meetup” stands out in the home feed, and the detail page is structured so that meetup information is separated from participants, and “Join” or “Leave” are easy to see. HTMX filtering enhances user experience by real-time updating of the feed as the user experiments with different filters, fostering engagement and exploration.

![Filter Interaction](/assets/test3-apply-filter.png)
> **Evidence 3:** The filter panel allowing users to refine the meetup feed smoothly using HTMX.

**Usability and Feedback**
One aspect of this UI that I really like is the way that it handles errors when creating the meetup. Should one of the fields on the form be left blank or invalid, the browser and server recognize that something is wrong and present the user with a clear validation message next to the error field, as you can see when the user leaves the restaurant name field blank in Evidence 2. No confusion, immediate feedback.

**Accessibility (WCAG AA)**
I focused on semantic HTML to assure basic accessibility. The application is fully keyboard navigable using the appropriate <form>, <label>, and <button> tags. Users navigate, filter, and fill forms without using a mouse. I also made sure that there is good contrast between text and background, for instance, dark gray in the text with a soft surface background, in order to achieve WCAG AA, which is reflected in the Lighthouse Accessibility score of 95.

But there was one small accessibility issue uncovered in the testing: the visual focus state for keyboard navigation was available via the default browser outline but could be made more robust. Some of the buttons have a less-than-ideal focus indicator for the element under focus, which may be problematic for keyboard-only users.

## 3. Critical Reflection and Improvement Planning

Most importantly, the big difference is that TableTogether has a simple scope. MojoJS with SQLite and HTMX was a clash with standard HTTP requests and relational data instead of complex state management.

**Connecting Problems to Decisions**
One problem that was discovered as part of the testing process was the absence of an “Empty State” design. A user can receive a blank feed if they filter for something that is not available in a match. This was a direct outcome of paying attention to backend filtering logic and ignoring the usefulness of a fallback UI. The user may assume that there is something wrong with the application and not realize that there were no meetups to fit what they were searching for.

One of the problems is related to the data model of an image. As mentioned in the performance section, external URLs ensure an unpredictable loading experience. 

**Improvement Plan**
If I still had some development to do, the things I'd work on would be targeted and realistic:
1. **Implement robust Empty States:** Update the MojoJS controller to pass a flag when no meetups are found with the filters and display a friendly message like “No meetups found for these filters—try adjusting your search!” with a button to clear filters.
2. **Image Fallbacks:** I would load a default "placeholder" image in the CSS or template, which comes up almost instantly, to preserve layout if an external photo URL fails or is slow.
3. **Enhanced Focus Styles:** I would re-implement the :focus-visible styling with a thick, high-contrast outline around interactive elements for better keyboard interactivity.

These updates fix issues at a core level, such as unhandled UI edge cases and external dependencies, and do not introduce cosmetic changes.

## 4. Retrospective Assessment of Functional Requirements

During my A1 planning phase, I produced a MoSCoW priority list. Some of the features I wanted were a “home feed," the ability to create meetups and detail pages, 'join' and ‘leave’ buttons, the ability to filter, and responsive design.

In retrospect, my first requirements were reasonable and well-prioritized. I used all of the “must-have" requirements. The common features, such as offering a way for users to create and join dining plans, with reasonable payment and safety expectations, are working as they were designed.

But a few assumptions were a bit off-topic. In A1, I added DMS as a “Will not have.” This was the right focusing choice to make; otherwise, a chat system would have slowed down the MVP. However, during UX testing, I noticed that for the organizer, once the users join the meetup, they cannot be informed about the changes at the last moment, like the reservation delay.

While I don't regret the fact that I had removed direct messaging, there's one thing that I missed, which is a simple field in the detail page that could only be edited by the organizer, called “Announcement” or "Update," in order to notify participants. This demonstrates that although the requirements were adequate for the prototype, there are quickly identified communication gaps that must be addressed to allow for practical use in the real world.

## Conclusion

The development of TableTogether was a great all-round full-stack exercise. I used MojoJS, SQLite, and HTMX to discover how to create a responsive application with lots of dynamicity without relying on a big front-end framework. Deploying it to Render and critically testing it taught me that performance and UX go beyond “code that runs” to trade-offs, edge cases, and the user that's using the app.