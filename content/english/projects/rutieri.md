---
title: "SaaS platform: Rutieri"
description: "In this post I am going to share my experience on building a SaaS platform using the headless CMS Strapi as the Backend and React Native."
images:
  - "images/post/03.webp"
date: 2023-01-30T12:14:25+06:00
tags: ["Strapi", "React Native", "React", "Typescript", "Firebase"]
categories: ["Projects"]
draft: false
slug: "saas-platform-rutieri"
---

Rutieri is a SaaS platform built with [Strapi](https://strapi.io/), React Native, Typescript and other technologies.

### Outline

- The idea
- Platform features
- The stack
- The API
- The frontend
- The mobile app
- Conclusion
- Landing Page

### The idea

Before starting to write a single line of code, it is generally a good idea to think about the problem, it's limitations and whether or not it has already been solved by someone else (AKA competitors).

The problem I was looking into had to do with the way in which public and private transportation companies manage their routes, drivers and users. This process is generally carried out on paper, e.g. not digital, hence this could be problematic in case of new drivers joining the organization or in case of restricting access to data to only specific users.

After a little bit of research, I could only find one platform that provides a similiar solution but for their own company.

So the platform I built needed the following content types:

- Organizations to group routes, drivers and users
- Routes
- Two user roles: drivers and users (passengers)

As I said before, Strapi makes the creation of these content types and the relationships between them really easy, but let's first see what is Strapi and how it turns the API development into a satisfactory and fun experience.

### Platform features and user stories

The following user stories illustrates the desired features the platform should have in order to solve the aforementioned problems.

#### As an administrator user

1. As an administrator, I want to login in the admin panel.
1. As an administrator, I want to create an organization.
1. As an administrator, I want to create routes in the organization.
1. As an administrator, I want to invite drivers and users to the organization.
1. As an administrator, I want to manage requests to join the organization.
1. As an administrator, I want to assign routes to drivers in the organization.
1. As an administrator, I want to see in real time the drivers and users currently active in the map of the different routes.

#### As a driver

1. As a driver, I want to login in the mobile app.
1. As a driver, I want to join an organization by entering the code in the search bar.
1. As a driver, I want to see my route on the map.
1. As a driver, I want to become visible to passengers on the road.
1. As a driver, I want to see the passengers waiting on the road.
1. As a driver, I want to remove my visibility and finish my run.

#### As a user

1. As a user, I want to login in the mobile app.
1. As a user, I want to join an organization by entering the code in the search bar.
1. As a user, I want to see the different routes of my organization in the map.
1. As a user, I want to search for a destination and get the available routes that pass nearby.
1. As a user, I want to see the drivers currently active on the routes in real time.
1. As a user, I want to become visible to drivers of a route.

### The stack

The backend requires to handle user authentication, permissions, different data structures as content types and define relations between them. It's also necessary to synchronise passengers and drivers and view them on a map real time in the administration panel as well as in the mobile app.

The administration panel is a web page that fetches data from the backend as well as from the real time data provider and it's goal is to provide a way for administrators to manage their organization and users. We're talking about a Single Page Application built in React.

As for the mobile application, there isn't a better choice nowadays than React Native and it works just fine in this case.

### The API

Since all of the features involve authentication, permissions and roles, and because there is no need to reinvent the wheel, I chose to use Strapi to build the backend for it's simplicity, ease of use and great developer experience, whereas for realtime data, I used Firebase.

The instance of Strapi and the Postgres database it requires was deployed in the cloud hosting platform https://fly.io.

Strapi is good for managing users, content that's typically updated and fetched via CRUD API, and relations between content types.

The platform needs the following content types:

- Organizations to group routes, drivers and users
- Routes
- Two user roles: drivers and users (passengers)

Below are some screenshots of the overview of these content types

![routes](/images/project/rutieri/backend/routes_content_type.png)
![organisations](/images/project/rutieri/backend/organization_content_type.png)
![user](/images/project/rutieri/backend/user_content_type.png)

As I said before, Strapi makes the creation of these content types and the relationships between them really straightforward.

However, not everything related to the API can be provided by Strapi. Some realtime features need to be addressed with other solutions, such as geolocation data in real time for drivers and users to synchronise each other, maps and the ability to search for places. Such features were implemented using Firebase, Google Maps and Google Places.

### The frontend

The platform where users are able to login as administrators and manage their organizations and users is a single page web application built in React. Among the features of this project that I think stand out are:

- State managed by Context API
- Interface styled with Bootstrap
- React Router for pages
- [Leaflet](https://react-leaflet.js.org) to display the map
- [GeoFire library](https://www.npmjs.com/package/geofire) to synchronise geolocation data in real time with Firebase
- Use of localStorage to save user session

Below are some sample screenshots of how this app looks like

![login](/images/project/rutieri/frontend/login.png)
![homepage](/images/project/rutieri/frontend/homepage.png)
![routes](/images/project/rutieri/frontend/routes.png)
![drivers](/images/project/rutieri/frontend/drivers.png)
![users](/images/project/rutieri/frontend/users.png)

### The mobile application

This one is by far the most complex part of this project.

The project was bootstraped with [Infinitered's Ignite](https://github.com/infinitered/ignite), which provides a great boilerplate and surely saved me of what would have been between 1-2 months of work.

Ignite's boilerplate includes many features out of the box, including:

- React Native and Typescript (of course)
- React Navigation
- MobX-State-Tree for state management
- Expo SDK for developer experience
- AsyncStorage for persistence
- apisauce as REST client

And some other libraries and features that make React Native apps super powerful and a joy to work on.

It consists of three screens:

1. Welcome screen
2. Login screen
3. Map screen

In the welcome screen, users are able to go to the login screen if not logged in. Otherwise, if they're in an organisation, it shows their role and org's information, and if they're not, they are able to enter the organisation code and request to join as driver or as passenger.

If the user is a driver in an organisation, the welcome screen also shows the route assigned to them. By tapping on it, it takes them to the map, where they can see themselves and start the tour, becoming visible to passengers on the road but being able to see passengers on the road as well.

Drivers can finish the tour at any time by pressing the button stop.

If the user is a passenger in an organisation, the welcome screen shows the different routes available in the organisation. By tapping on them, they are taken to the map where they can see themselves, the route and the drivers on the road.

Passengers are able to navigate between the available routes and search for the location they want to go to by using the search bar at the top of the map screen, filtering out the routes that pass nearby (less than 200 meters), if there are. [Google Places API](https://developers.google.com/maps/documentation/places/web-service/overview?hl=es-419) and [turf library](https://www.npmjs.com/package/@turf/turf) work together in this search process.

Passengers become visible to drivers on the road by pressing the button `wait` and if they press the button again, they stop waiting and are removed from the driver's map.

The start/wait and finish buttons dispatch actions that update their location in firebase, so that passengers are able to see the bus on the map as it moves in real time and viceversa.

As for the state management, the project consists of two models and three stores from `Mobx-State-Tree` library: `User` and `Route` models, `user-status`, `route-store` and `root-store` stores.

#### User model

Located in `/app/models/user/user.ts`

```ts
const OrganizationModel = types.model({
  name: types.string,
  code: types.string,
  id: types.identifierNumber,
  drivers: types.number,
  rutas: types.array(RouteModel)
})

const UserModel = types
  .model("User")
  .props({
    id: types.identifierNumber,
    username: types.string,
    email: types.string,
    token: types.string,
    role: types.union(types.literal("passenger"), types.literal("driver")),
    ruta: types.maybeNull(RouteModel),
    organization: types.maybeNull(OrganizationModel),
    pending_request: types.maybeNull(OrganizationModel),
  })
```

#### Route model

Located in `/app/models/route/route.ts`

This model follows the GeoJSON format for routes.

```ts
const RouteModel = types
  .model("Ruta")
  .props({
    id: types.identifierNumber,
    name: types.string,
    latlong: types.maybeNull(types.model({
      lat: types.number,
      longt: types.number
    })),
    coords: types.model({
      type: FeatureTypes,
      features: types.array(types.model({
        type: types.string,
        geometry: types.model({
          type: types.string,
          coordinates: types.union(types.array(types.number), types.array(types.array(types.number)))
        }),
        properties: types.model({
          name: types.string
        })
      }))
    })
  })
```

#### user-status store

Located in `/app/models/user-status/user-status.ts`

This store is responsible for managing the state of the user. It stores the user once it's logged in and removes it when the user logs out. It also has some `views` to get the user key for firebase purposes, get the role and get the route in case of a driver.

This store has some methods that get the user location from the device's GPS, displays the user icon on the map and sends it to firebase.

```ts
const UserStatusModel = types
  .model("UserStatus")
  .extend(withEnvironment)
  .props({
    user: types.maybeNull(UserModel),
    location: types.maybeNull(
      types.model({latitude: types.number, longitude: types.number})
    ),
    visibility: types.maybeNull(types.number)
  })
```

#### route-store store

Located in `/app/models/route-store/route-store.ts`

This store is responsible for managing the state of the available routes. It stores the routes, drivers and passengers on the different routes. It also has some `view` methods to filter the routes that pass nearby a destination specified by the user, get passengers waiting on a given route and get drivers active in a specific route.

This store initializes a [GeoQuery](https://firebase.google.com/docs/firestore/solutions/geoqueries) from [Geofire library](https://www.npmjs.com/package/geofire) and listens for events to set, update and remove drivers and passengers from the map as they move.

```ts
const RouteStoreModel = types
  .model("RouteStore")
  .props({
    routes: types.array(RouteModel),
    passengers: types.map(types.model({
      key: types.identifier,
      location: types.array(types.number)
    })),
    drivers: types.map(types.model({
      key: types.identifier,
      location: types.array(types.number)
    })),
    destinationAddress: types.maybeNull(types.model({
      name: types.string,
      coords: types.array(types.number)
    }))
  })
```

#### Conclusion and final thoughts

Using a CMS as the backend can make the development a lot faster than building the API from scratch and with Strapi this is specially true. On the other hand, Strapi doesn't really make a good fit for real time applications, therefore, Firebase is the way to go in this case.

As of the client side, React always works very good for pretty much any kind of application, and because React Native uses React under the hood, it is so convenient for us React developers and ir works pretty good for almost any kind of application as well.

However, one thing that I didn't mention in this post was the use of Typescript; I find this quote by Brice Wilson pretty good to point out the whole purpose and motivation to learn and use (well) this powerful language and tool ecosystem:

"You won't have to wait for a frustrated user to report the error. All of this means that you provide value to your users faster, and that's really what it's all about."

All in all, I got a lot of learning by building this project, both in languages/frameworks used and production stuff such as infrastructure, cloud hosting and cloud-based APIs.

### Project landing page:

https://rutieri.netlify.app
