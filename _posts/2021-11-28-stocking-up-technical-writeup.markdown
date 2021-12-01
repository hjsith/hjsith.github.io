---
title: "Stocking Up: A Technical Write-Up"
date: 2021-11-28 02:23:43 +1000
categories: posts
tags:
  - azure
  - react
toc: true
toc_label: "Sections"
toc_icon: "cog"
gallery:
  - image-path: /assets/images/stocking-up-screenshots/portfolio-concept.png
    url: /assets/images/stocking-up-screenshots/portfolio-concept.png
    alt: "Portfolio View Concept"
    title: "Portfolio View Mock"
  - image_path: /assets/images/stocking-up-screenshots/board-concept.png
    url: /assets/images/stocking-up-screenshots/board-concept.png
    alt: "Discussion Board View Concept"
    title: "Discussion Board Mock"
  - image_path: /assets/images/stocking-up-screenshots/friends-concept.png
    url: /assets/images/stocking-up-screenshots/friends-concept.png
    alt: "Friends View Screenshot"
    title: "Friends View Mock"
---
{% include head.html %}
![Stocking Up portfolio view screenshot](/assets/images/posts-snippet/stocking-up.png "The Stocking Up portfolio view.")
*The Stocking Up portfolio view.*
## Introduction
### Why V2?
Well, let's start from the beginning. The original Stocking Up was a Visual Basic + .NET WinForms application that I had created in high school.

![Screenshot of Stocking Up V1]

The crux of the application was simple: a virtual stock market where users (students in this case) could trade within, and thereby learn about, the stock market. The features of the application were quite simple: a portfolio management system, near real-time price data from the ASX, a tutorial system, interactive graphs and local save data. I was immensely proud of the result, especially considering that this was my first time utilising VB .NET (as in the past my high school forced us to use Visual Basic 6). 

However, even throughout the development process, I felt there was something truly missing in the application: social interaction. At this point, I had been working on the project for 6 months and I really didn't have that much time to fundamentally change my application. After completing the project, the thoughts of a shared virtual stock market application continued to fester in my mind. Throughout university, being exposed to more modern technologies/concepts such as Software as a Service and Hybrid Web Applications allowed me to conceptualise how this shared virtual stock market would operate. Finally, for the subject Advanced Software Development, we were presented with the opportunity to develop a full-stack application of our own choosing. My group and I were very excited to build Stocking Up V2. However, we quickly realised things weren't going to be that easy.

### Hitting the ground somewhat running

On very first day of this project, I quickly realised how big of a venture this would take. We decided, in accordance with our university's policies of plagiarism and such, that not a single resource, line of code, or even user interface design from Stocking Up was going to be used - everything would have to be built from scratch (just thinking about it now, converting a VB. NET code base to JavaScript would've been a nightmare). 

We first came up with of a list of desirable features for our application, and then assigned two of them to each group member. We all then hopped onto a shared Figma document where each group member designed the UX/UI for their respective features. During this process we constantly communicated with each other on the overall look/feel of the user interface. After spending an entirety of one of our 2 hours meeting deciding on a colour theme, we finally finished our user interface designs (some of which you can see below).

{% include gallery caption="Some of Stocking Up V2 mock designs"%}

## The tech stack

As the two people in the group with the most software development experience, James and I were presented with the difficult task of selecting the tech stack we were going to use throughout the project. Luckily, we both had experience utilising React, Express and Node.js in a previous university assignment. We also saw the benefits of using npm throughout the development of our application, especially when it came to integrating unit testing frameworks.

## Microsoft Azure

### All the resources!!!

### CI/CD with Azure Devops

#### Building + Deployment

#### Testing

## Front-end tech and structure

### Functional React components

### Backend for Frontend

### Cool packages we used!

## Back-end tech and structure

### Sequelize

### Unit Testing

### Crazy API stuff!

#### News Feed

#### Price Data

### Order Queues
 
## Fun tidbits

## Concluding thoughts

