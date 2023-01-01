---
title: "How To Enable And Manage Comments In Your Strapi Application."
description: "In this post we'll learn how to enable comments in a strapi application as well as displaying comments in the frontend with React"
images:
  - "images/post/strapilogo.jpg"
date: 2023-01-01T12:21:25+06:00
tags: ["Strapi", "Strapi tutorials"]
categories: ["Tutorial"]
draft: true
---

Enable comments in a Strapi application and display them in the frontend with React

### Outline
- Introduction
- Prerequisites
- What is Strapi Comment Manager?
- Installation
- Configuration
- Display comments on the frontend
    - Installation of Strapi Comments Client
    - Usage of Strapi Comments Client
- Plugin settings
- Manage comments
- Full source code of the frontend
- Conclusion


### Introduction

A comment system comes in very handy for pretty much any kind of website. In the JAMstack ecosystem, while it's ok to rely on third party solutions hosted on their own platform such as Disqus to enable comments, you usually want to keep your content and all the stuff related to it in the same admin dashboard.

In this article, I'll show you how to enable and manage comments for your content very easily using the [Comment Manager](https://npmjs.com/package/strapi-plugin-comment-manager) plugin, and display them in your frontend application.

### Prerequisites

You should have a basic understanding of the following.

1. Basic knowledge of JavaScript
2. Basic knowledge of React (OPTIONAL)
3. Basic understanding of Strapi - [get started here](https://docs.strapi.io/developer-docs/latest/getting-started/quick-start.html).
4. Your Strapi V4 project setup

### What is Strapi Comment Manager?

Strapi Comment Manager is a plugin that enables comments for pretty much any kind of content. It allows your users to post comments and anyone can get the comments associated with a given slug.

With this plugin, admin users can view and manage very easily all the comments from the Strapi administration dashboard. Within the dashboard, you will be able to delete comments and subcomments and leave replies on comments.

### Installation

Once into the Strapi project root, you can install the plugin by running the following command:

```bash
npm install strapi-plugin-comment-manager
```

Next, build the project to see the new plugin in the dashboard with the following command:

```bash
npm run build
```

And that's it! If everything runs correctly, the plugin should now be installed.

### Configuration

Now you need to enable some permissions so that the frontend can access the endpoints to post and fetch comments.

In your Strapi admin dashboard, head over to **Settings**, then over to **Roles** under **Users & Permissions Plugin**.

Let's first setup the Public API; click on **Public** and hit the dropdown button of **Comment Manager**.
Now check **count**, **find** and **getPageSize**, then hit the **Save** button.
Below is a screenshot of a proper configuration:


![](https://paper-attachments.dropbox.com/s_F4A7EDBFDC720B4F2CC6430400928FC7049E297EEFCE8056A718FCD5F4317077_1640914179294_public-api.png)


Now let's setup the Authenticated API. Go back to **Roles** and click on **Authenticated**.
Open the dropdown for **Comment Manager** and mark as checked the option **create** on both **Comment** and **Subcomment**.
Below is a screenshot of a proper configuration:


![](https://paper-attachments.dropbox.com/s_F4A7EDBFDC720B4F2CC6430400928FC7049E297EEFCE8056A718FCD5F4317077_1640914092651_imagen_2021-12-30_212811.png)


With this configuration, the frontend should now be able to make requests to get and post comments.

### Display comments on the frontend

The plugin exposes an API to get and post comments if you want to have fine-grained control over the workflow of your comments system and you can check the documentation on the [package page](https://npmjs.com/package/strapi-comments-client), but this plugin also comes with a purpose-built React component library that makes it super easy to get up and running without getting your hands dirty.

This components library is called [strapi-comments-client](https://npmjs.com/package/strapi-comments-client), fully supports typescript and it handles for you all of the complexity of fetching and posting comments and subcomments for every content ID that you pass to it.

###### Installation of Strapi Comments Client

You will need to have installed **react ^17.0.2**, **react-dom ^17.0.2** and **react-router-dom ^5.2.0**.

Inside of your React project, run this command:


```bash
npm install strapi-comments-client --save
```

###### Usage of Strapi Comments Client

Using this library is very easy!

This library exports three main components:

- CommentsProvider
- Comments
- CommentForm

And you can import them this way:

```ts
import {
  CommentsProvider,
  Comments,
  CommentForm
} from "strapi-comments-client"
```

All you have to do is wrap your **App** component into the **CommentsProvider** component.
Then you will be able to place anywhere in your app the **Comments** component to render a list of comments for a given content ID and the **CommentForm** component to render a form to post comments.

For example, this could be your index.js or main.js file:

```ts
import React from 'react'
import ReactDOM from 'react-dom'

// The address of your strapi backend instance
const STRAPI = "http://localhost:1337"

ReactDOM.render(
  <React.StrictMode>
    <CommentsProvider apiURL={STRAPI}>
      <App />
    </CommentsProvider>
  </React.StrictMode>,
  document.getElementById('root')
)
```

Where **apiURL** is the URL of your running Strapi application, and this property is **required**.

This way, the comments provider will do all the magic of fetching and posting comments for you!

This library also exports an utility **React.Context** to update some of the parameters for fetching and posting comments:

```ts
import { CommentsConfigContext } from "strapi-comments-client"
```

This **CommentsConfigContext** exposes two setter functions: **setUser** and **setContentID**

With **setContentID** you can load the comments for a given content and post comments to it. It receives a single parameter of type **string** and must be URLized, i.e. no spaces.

With **setUser** you can set the credentials of a given user to authorize the posting of comments. It receives a single parameter of type **IUser**, with the following **Typescript interface**:

```ts
interface IUser {
  username: string,
  email: string,
  id: string,
  token: string // This is a JWT
}
```

It's a little confusing but we'll see how to use it in a component:

```ts
const App = () => {
  const { setUser, setContentID } = useContext(CommentsConfigContext)
  // The following data should come from Strapi Users and Permissions Plugin
  // for authenticated requests
  const user = {
    username: "John Doe",
    email: "jhohndoe@gmail.com",
    id: 5,
    token: "this_should_be_a_JWT"
  }
  if (user) {
    setUser(user)
  }
  setContentID("sample-content-1") // Load comments for this content
  return (
    <>
      {
        !user && <Login />
      }
      <CommentForm />
      <Comments />
    </>
  )
}
```

And that's it!

After setting the content ID through **setContentID**, **CommentsProvider** will start loading the comments for the given content ID and the **CommentForm** will render an input to post comments related to the given content ID **if** there is a user. Otherwise, it will display the message **Login to post a comment**.

Here's how the interface looks like so far:


![](https://paper-attachments.dropbox.com/s_F4A7EDBFDC720B4F2CC6430400928FC7049E297EEFCE8056A718FCD5F4317077_1640914973004_comment.PNG)


There's also a button to **Leave a reply**, which will open a form to post a subcomment associated with the parent comment.

This library exports one more component: **ErrorBox**

```ts
import { ErrorBox } from "strapi-comments-client"
```

.It's useful if you'd like to display error messages when things go wrong fetching or posting comments.

You can place this component wherever you want, for example in between the **CommentForm** and the **Comments** components.

If you're wondering how this error box looks like, here you have a sample:

![](https://paper-attachments.dropbox.com/s_F4A7EDBFDC720B4F2CC6430400928FC7049E297EEFCE8056A718FCD5F4317077_1640915088338_error.PNG)

### General settings

You can customize the page size, i.e. specify how many comments are returned at once.

In the Strapi admin panel, head over to **Settings**, then select **Pagination** under **Comment Manager Plugin**.

Here you'll find an input to set the page size, which defaults to 10.

![](https://paper-attachments.dropbox.com/s_F4A7EDBFDC720B4F2CC6430400928FC7049E297EEFCE8056A718FCD5F4317077_1640915323050_imagen_2021-12-30_214840.png)

### Manage comments

Once you've got the plugin up an running, as users start to post comments, you can manage and reply to them as admin from the Comment Manager section of the left sidebar in the Strapi admin dashboard.

Here you can see two tabs: one for the latest comments and one for comments grouped by content ID.


![](https://paper-attachments.dropbox.com/s_F4A7EDBFDC720B4F2CC6430400928FC7049E297EEFCE8056A718FCD5F4317077_1640915958244_latest-comments.png)



![](https://paper-attachments.dropbox.com/s_F4A7EDBFDC720B4F2CC6430400928FC7049E297EEFCE8056A718FCD5F4317077_1640915483765_grouped-comments.png)


In both of them you can delete comments and subcomments as well as leave replies.


### Example project

You can find a full working example of a React App using the Strapi Comments Client Library in [this repo](https://github.com/luisguve/strapi-comments-client-example)

### Conclusion

With this plugin you can enable and manage comments for any content with little effort and even use a component library to display the comments in your frontend application made with React.

And that's it! The features are pretty basic at the moment but if there's interest, I'm willing to work on more features as well as improve the UI/UX.
