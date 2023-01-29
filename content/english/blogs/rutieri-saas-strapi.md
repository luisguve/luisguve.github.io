---
title: "How I Built A SaaS On Top Of Strapi, And Why You Should Too"
description: "In this post I am going to share my experience on building a SaaS using the headless CMS Strapi as the Backend, React Native and other technologies."
images:
  - "images/post/03.webp"
date: 2023-01-01T12:21:25+06:00
tags: ["Strapi", "React Native", "Typescript"]
categories: ["Projects"]
draft: false
slug: "how-i-built-a-saas-on-top-of-strapi-and-why-you-should-too"
---

In this post I&rsquo;m going to share my experience on building a SaaS using the [headless CMS Strapi](https://strapi.io/) as the Backend, React Native and other technologies.

### Outline
- Introduction
- What is SaaS?
- The problem
- What is Strapi?
- Developing features in Strapi
- The frontend: How to get content
- Conclusion
- Landing Page

### Introduction

Very often, developers, product and project managers, testers and pretty much the entire team share their ideas to decide what language and which framework they'll use to build their next project. Some considerations must be taken into account, from which in my opinion there are three that are the most important:

1. Developer experience and ease of use

  Does the language and framework chosen provide a good developer experience? Is the langauge the same for the backend and frontend?

2. Deadlines

  Is there a deadline to finish the project? if so, there is a good chance to finish the project on time if the team chooses the language they have more experience in.
  
3. Maintainability

  As there will be usually more than one person working on the same part at the same time, if everything is kept organised, the whole development process will be frictionless.

With that in mind, developers and project managers will have a better insight on which language/framework to use.

Other aspects should also be considered such as what the data structure will look like.

In my case, as it is usual, the backend of my project needs a database for users and their roles among other entities and their relations and a dashboard to allow admins to manage the data, and I was lucky to find out Strapi, as it includes a lot of these features out of the box with one single line of command to get started.

### What is SaaS?

SaaS stands for Software-as-a-Service and it just means that a software is provided as a service in the cloud and it gives a solution to a specific problem, for which the users are willing to pay either monthly or annual subscription.

### The problem

Before starting to write a single line of code, it is generally a good idea to think about the problem, it's limitations and whether or not it has already been solved by someone else (AKA competitors).

The problem I was looking into had to do with the way in which public and private transportation companies manage their routes, drivers and users. After a little bit of research, I could only find one platform that provides a similiar solution but for their own company.

So the platform I built needed the following content types:

- Organizations to group routes, drivers and users
- Routes
- Two user roles: drivers and users (passengers)

As I said before, Strapi makes the creation of these content types and the relationships between them really easy, but let's first see what is Strapi and how it turns the API development into a satisfactory and fun experience.

### What is Strapi?

Strapi is an open source headless CMS that allows developers to build complete RESTful APIs in just a couple of days instead of months. It includes a lot of useful features as plugins out of the box. Users and Roles management, Media library and an interface to create, view, edit and delete content are just some of them.

Regarding the API, how does it makes the development faster?

First of all, it enforces a specific folder structure, which helps to keep everything well organised and clean.

Secondly, all database schemas are generated automatically and queries are made in JSON format, which really saves a lot of time.

Lastly, we can add more features to our Strapi application very easily via plugins from the marketplace.

It's also worth noting that Strapi is a self-hosted CMS, which means that we can host it in whatever cloud platform we want, as well as test it locally in our computers before deploying it to the cloud.

### Developing features in Strapi

Creating and configuring endpoints in Strapi is as straightforward as declaring a JSON in a single file:

![endpoints](/images/post/endpoints.png)

Creating controllers is straightforward as well:

![controllers](/images/post/controllers.png)

Every controller gets all the data related to the request in the `ctx` parameter and it's also used to send the response. This keeps everything in one place and really helps to improve the readability.

Once the API endpoints are defined, the next step is to enable the permissions for the specific user roles to have access to these endpoints:

![driver role permissions](/images/post/permissions_driver.png)

![passenger role permissions](/images/post/permissions_passenger.png)

### The frontend: how to get content

Since Strapi is a headless CMS, it'll only provide content through the API. That means that the content can be consumed from anywhere. In our case, this content will be used in two applications: one for the organization owners and one for the users and drivers.

The application for the organization owners is a dashboard where administrators can create organizations, routes, accept drivers and users in the organization and assign routes to drivers. This is just a React Application:

![dashboard](/images/post/dashboard.png)

The application for drivers and users is a mobile application built in React Native. Firebase was used to synchronise geolocation data in real time between drivers and users and display this information in a Map from Google Maps:

<div class="w-50">
  <img src="/images/post/step6-2-mobile.webp" alt="mobile" />
</div>

### Conclusion

Using a CMS as the backend can make the development a lot faster than building the API from scratch and with Strapi this is specially true. Furthermore, this becomes more important when building a brand-new product, as it's usually recommended to launch as soon as possible to gather feedback from the users and validate the idea.

### Project landing page:

https://rutieri.netlify.app

























