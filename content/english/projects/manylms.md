---
title: "ManyLMS: E-Learning platform"
description: "In this post I am going to share my experience on building an e-learning platform using the headless CMS Strapi as the Backend and React Router 7."
images:
  - "/images/project/manylms/frontend/course_overview.png"
date: 2025-11-22
tags: ["Strapi", "React", "React Router 7", "Typescript", "Mux"]
categories: ["Projects"]
draft: false
slug: "e-learning-platform-maestro-lms"
---

ManyLMS is an e-learning platform built on top of [Strapi](https://strapi.io/), React Router 7, Typescript and other technologies.

### Outline

- The idea
- Platform features
- The stack
- The API
- The frontend
- Conclusion
- Landing Page

### The idea

This project doesn't necessarily bring a huge amount of innovation on the e-learning platforms that already exists, but it's just another way of doing this type of application.

The main idea is to apply a JAMstack approach in this application, where the platform is a static website, and the backend is just an API that serves static content only once to build the website and just adds the dynamism that's necessary to allow users to authenticate, create orders, confirm payments and take courses.

If we compare this approach to a WordPress website, we are taking out most of the overhead that implies rendering the pages everytime a user visits them. Despite that there are plugins for caching that may improve the performance, it's still never going to be faster and more efficient than just static content served by a CDN. That's why React Router 7 and Headless CMSs are so popular right now.

### Platform features and user stories

The following user stories illustrates the desired features the platform should have.

#### As an administrator, I want to:

1. **login** in the admin panel.
1. **create** categories.
1. **create** courses.
1. **upload** lectures.
1. **organise** courses into categories.
1. **assign lectures** to courses.

#### As a student, I want to:

1. **login** in the platform.
1. **view** the available courses.
1. **add** courses to the shopping cart.
1. **review** the shopping cart.
1. **create** an order.
1. **pay** with credit card or paypal.
1. **view** the courses i've purchased in my learning page.
1. **go to** the course page from my learning page and watch the videos.
1. **mark** lectures as seen.
1. **come back later** and resume where I left.

### The requirements

The backend requires to handle user authentication, permissions, different data structures as content types and define relationships between them. It also requires to allow uploading videos to some third party platform that supports streaming on demand.

The frontend is a web platform where users can register and login, view and buy courses, leave comments and reviews and take courses.

### The API

Since all of the features involve authentication, permissions and roles, and because there is no need to reinvent the wheel, I chose to use Strapi to build the backend for it's simplicity, ease of use and great developer experience, whereas for streaming videos on demand, I chose to use [Mux.com](https://mux.com).

The instance of Strapi and the Postgres database it requires was deployed in the cloud hosting platform https://fly.io.

Strapi is good for managing users, content that's typically updated and fetched via CRUD API, and setting up relations between content types.

The platform needs the following content types:

- Category to group courses
- Course
- Lecture
- Module to group lectures
- Order
- Student: has many courses
- Student-Course: stores a student's current lecture of a course
- Video

Strapi makes the creation of these content types and setting up relationships between them really straightforward.

Below are some screenshots of these content types and the relationships between them:

![category](/images/project/eula/backend/category.png)
![course](/images/project/eula/backend/course.png)
![lecture](/images/project/eula/backend/lecture.png)
![module](/images/project/eula/backend/module.png)
![order](/images/project/eula/backend/order.png)
![student](/images/project/eula/backend/student.png)
![student-course](/images/project/eula/backend/student_course.png)
![video](/images/project/eula/backend/video.png)

### The frontend

The platform where users are able to login, view, buy and view courses is a web application built with React Router 7. Among the features of this application are:

- State managed by Context API
- Interface styled with Bootstrap
- Play streaming videos with [@mux/mux-player-react](www.npmjs.com/package/@mux/mux-player-react) library
- Use of localStorage to save user session

Below are some sample screenshots of how this app looks like

![homepage](/images/project/manylms/frontend/home.png)
![login](/images/project/manylms/frontend/login.png)
![course overview](/images/project/manylms/frontend/course_overview.png)
![couse curriculum](/images/project/manylms/frontend/course_curriculum.png)
![payment page](/images/project/manylms/frontend/stripe_payment_page.png)
![successful payment](/images/project/manylms/frontend/successful_payment.png)
![successful payment 2](/images/project/manylms/frontend/successful_payment-2.png)
![learning page](/images/project/manylms/frontend/profile.png)
![course lecture](/images/project/manylms/frontend/course_lecture.png)

#### Conclusion and final thoughts

While building this project, I learned:

- How streaming on demand works and how to use a streaming provider
- How to statically build websites with React Router 7 and Strapi
- How to setup dynamic pages in React Router 7
- How to process payments with Stripe and Paypal
- How to build custom plugins in Strapi
- How to publish packages to NPM

### Project source codes:

https://github.com/luisguve/maestro-backend

https://github.com/luisguve/new-lms-remix
