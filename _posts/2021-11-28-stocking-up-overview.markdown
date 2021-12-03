---
title: "Stocking Up: An Overview"
date: 2021-11-28 02:23:43 +1000
categories: posts
tags:
  - azure
  - react
toc: true
toc_label: "Sections"
toc_icon: "cog"
gallery:
  - image_path: /assets/images/stocking-up-screenshots/board-concept.png
    url: /assets/images/stocking-up-screenshots/board-concept.png
    alt: "Discussion Board View Concept"
    title: "Discussion Board Mock"
  - image_path: /assets/images/stocking-up-screenshots/friends-concept.png
    url: /assets/images/stocking-up-screenshots/friends-concept.png
    alt: "Friends View Screenshot"
    title: "Friends View Mock"
  - image_path: /assets/images/stocking-up-screenshots/portfolio-concept.png
    url: /assets/images/stocking-up-screenshots/portfolio-concept.png
    alt: "Portfolio View Concept"
    title: "Portfolio Mock"
---

{% include head.html %}
![Stocking Up portfolio view screenshot](/assets/images/posts-snippet/stocking-up.png "The Stocking Up portfolio view.")
_The Stocking Up portfolio view._

## Introduction

### Why V2?

Well, let's start from the beginning. The original Stocking Up was a Visual Basic + .NET WinForms application that I had created in high school.

![Screenshot of Stocking Up V1](/assets/images/stocking-up-screenshots/su-v1.png "Stocking Up V1.")

The crux of the application was simple: a virtual stock market where users (students in this case) could trade within, and thereby learn about, the stock market. The application features were quite simple: a portfolio management system, near real-time price data from the ASX, a tutorial system, interactive graphs and local save data. I was immensely proud of the result, especially considering that this was my first time utilising VB .NET (as in the past my high school forced us to use Visual Basic 6).

![Visual Basic 6](/assets/images/stocking-up-screenshots/vb6.png "Visual Basic 6")
_I remember seeing this screen everyday for months._

However, even throughout the development process, I felt there was something truly missing in the application: social interaction. At this point, I had been working on the project for 6 months and I really didn't have that much time to fundamentally change my application. After completing the project, the thoughts of a shared virtual stock market application continued to fester in my mind. Throughout university, being exposed to more modern technologies/concepts such as Software as a Service and Hybrid Web Applications allowed me to conceptualise how this shared virtual stock market would operate. Finally, for the subject Advanced Software Development, we were presented with the opportunity to develop a full-stack application of our own choosing. My group and I were very excited to build Stocking Up V2. However, we quickly realised things weren't going to be that easy.

### Hitting the ground somewhat running

On very first day of this project, I quickly realised how big of a venture this would take. We decided, in accordance with our university's policies of plagiarism and such, that not a single resource, line of code, or even user interface design from Stocking Up was going to be used - everything would have to be built from scratch (just thinking about it now, converting a VB. NET code base to JavaScript would've been a nightmare).

We first came up with of a list of desirable features for our application, and then assigned two of them to each group member. We all then hopped onto a shared Figma document where each group member designed the UX/UI for their respective features. During this process we constantly communicated with each other on the overall look/feel of the user interface. After spending an entirety of one of our 2 hours meeting deciding on a colour theme, we finally finished our user interface designs (some of which you can see below).

{% include gallery caption="Some of Stocking Up V2 mock designs" %}

## The tech stack

As the two people in the group with the most software development experience, James and I were presented with the difficult task of selecting the tech stack we were going to use throughout the project. Luckily, we both had experience utilising React, Express and Node.js in a previous university assignment.

### React

![React](/assets/images/stocking-up-screenshots/react.png "React")

As you can see with some of mock designs, there are a lot of commonalities between each screen's UI. This is why we chose React because of it's focus on reusable components. We also chose React because of it's easiness to learn and use, especially seeing as most of our group had no prior experience with React.

### Express and Node.js

We knew from the beginning that, if we were going to create a JavaScript webapp, that we'd be utilising Node.js. We chose Node.js, not only because of our familiarity with it, but we also saw the benefits of using npm throughout the development of our application, especially when it came to integrating unit testing frameworks.

We also chose Express because it allows us to quickly serve our "built" React page, quickly incorporate other middleware modules and define various routes for our application.

In regards to our choice of platform for hosting our application, we chose Microsoft Azure which I'll be detailing in the following section.

## Microsoft Azure

We chose Microsoft Azure to host our application mainly due our collective knowledge on setting up App Services to host Node.js/React web applications. As you'll read later, we also decided that Microsoft Azure would be a great platform to use as we needed to utilise Azure DevOps to host our CI/CD pipelines, repos and kanban boards. We also needed Azure Functions for some of our data logic (which will be discussed in a latter section).

### Azure App Service

Setting up the Azure App Service was quite simple. We chose the Basic pricing tier - opting for a B2 Linux instance which comes with 2 cores, 3.5GB of RAM and 10GB of storage. We decided that Stocking Up V2, being a university assignment, would not needed complex auto scaling or traffic management, so this was perfect for our use case.

We selected our stack to be Node, as decided earlier, setting our major version to be Node 14 and our minor version being Node 14 LTS. We were also learnt that you can expose environment variables with the application settings of the App Service. These environment variables are encrypted at rest and trasnmitted over an encrypted channel. These variables allowed us to access important key-value data within our code such as our database connection strings and database username and password.

### SQL Database

![Database storage amount](/assets/images/stocking-up-screenshots/db.png "Database storage amount"){: .align-left}
With our SQL database, we went with the Standard service tier, with 10GB of storage and 10 DTUs. It roughly amounted to $23 AUD every month and was more than enough to store our predominantly integer data. In the end our program only utilised 66MB of storage! (It's interesting to consider that our application stored historical price data for the past day, 5 days, two weeks and month + other data which still only amounted to 66MB of data)

### CI/CD with Azure DevOps

![Pipelines Setup](/assets/images/stocking-up-screenshots/pipelines-setup.png "Pipelines Setup")

Setting up CI/CD with Azure DevOps was quite the learning experience. James and I thought it would be quite simple: follow the guided setup and everything will be fine!

It was quite the opposite. First, we had an issue with getting our pipeline running and were being presented with "No hosted parallelism has been purchased or granted." After a lot of confusion, we learnt that Microsoft changed their policies on granting free CI/CD to all projects. As we were using a private repo, we needed to request the free tier.

A day or two after submitting the form, our request was approved and we were back on track - or so we thought. We faced a new error and for days James and I stared that this error wondering what we had done wrong:

![The error](/assets/images/stocking-up-screenshots/azure-error.png)

This was quite weird, as when we SSH'ed into our App Service instance, we could clearly see a the index.html file in it's corresponding directory. After many days of debugging, frustrations and even recreating the App Service, we decided to rewrite the Pipeline yaml to include the building of the front-end during the deployment, and suprisingly, this solved the problem.

#### Building + Testing + Deployment

Below you can see the Building, Testing and Deployment stages of our azure-pipelines.yml file. Some key things to note: We set success conditions on the Deploy and Test stages so that they were dependant on their previous stages. We also generated a junit.xml file that allowed our test results to be nicely displayed on the Azure Pipelines' test screen!

```yaml
- stage: Build
  displayName: Build stage
  jobs:
    - job: Build
      displayName: Build
      pool:
        vmImage: $(vmImageName)
      steps:
        - task: Npm@1
          displayName: "NPM Install Server"
          inputs:
            command: "install"
            workingDir: "server"
        - task: ArchiveFiles@2
          displayName: "Archive files"
          inputs:
            rootFolderOrFile: "$(System.DefaultWorkingDirectory)"
            includeRootFolder: false
            archiveType: zip
            archiveFile: $(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip
            replaceExistingArchive: true
        - upload: $(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip
          artifact: drop

- stage: Test
    displayName: Test stage
    dependsOn: Build
    condition: succeeded()
    jobs:
      - job: Test
        displayName: Test
        pool:
          vmImage: $(vmImageName)

        steps:
          - task: NodeTool@0
            inputs:
              versionSpec: "14.17.6"
            displayName: "Install Node.js"

          - script: |
              cd server && npm install && npm run test:ci
            displayName: "npm install and output test results"

          - task: PublishTestResults@2
            displayName: "supply npm test results to pipelines"
            condition: succeededOrFailed()
            inputs:
              testResultsFiles: "server/junit.xml"

- stage: Deploy
  displayName: Deploy stage
  dependsOn: Test
  condition: succeeded()
  jobs:
    - deployment: Deploy
      displayName: Deploy
      environment: $(environmentName)
      pool:
        vmImage: $(vmImageName)
      strategy:
        runOnce:
          deploy:
            steps:
              - task: AzureRmWebAppDeployment@4
                displayName: "Azure App Service Deploy: stocking-up"
                inputs:
                  azureSubscription: $(azureSubscription)
                  appType: webAppLinux
                  WebAppName: $(webAppName)
                  packageForLinux: "$(Pipeline.Workspace)/drop/$(Build.BuildId).zip"
                  RuntimeStack: "NODE|14-lts"
                  StartupCommand: "npm run start"
                  ScriptType: "Inline Script"
                  InlineScript: |
                    npm run build
```

## Front-end tech and structure

![Client folder structure](/assets/images/stocking-up-screenshots/client.png "Client folder structure"){: .align-right}

For our application's front-end, we followed the traditional setup of a React application, sectioning off our components and pages into separate folders within the src folder. For our other resources, such as images and css, we kept them within an assets folder with the src folder.

### Class React components

There are two approaches to creating components in React: Functional and Class. Our group predominantly used Class React components within Stocking Up V2 as we wanted to access the React lifecycle methods and have direct control over the logic and states. Below you can see an small example of one of our Class components:

```javascript
import React from "react";

class FriendHeading extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <>
        <h2 className="FriendHeading">{this.props.title}</h2>
      </>
    );
  }
}

export default FriendHeading;
```

### Backend for Frontend

We decided to directly integrate our 'Backend for Frontend' functionality into our componenet files. This made understanding the data flow a lot easier instead of calling a helper method from another file to retrieve the data for us. Below you can see an example of how this looked:

```javascript
  componentDidMount() {
    fetch("/api/investor" + "?id=" + this.props.userId, {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
      },
    }).then((res) => {
      res.json().then((body) => {
        this.setState({
          username: body.Username,
        });
      });
    });
  }
```

### Cool packages/resources we used!

For the front-end of our application, we utilised quite a few nifty packages and resources that made the development experience a whole lot easier!

For example, we utilised React Bootstrap for key UI components such as the Navigation Bar and some of the buttons. We also used Bootstrap to get more control over the themeing of our application.

## Back-end tech and structure

![Server folder structure](/assets/images/stocking-up-screenshots/server.png "Server folder structure"){: .align-right}

Our back-end 'server' folder had 4 main sections: the db folder (for database and model stuff), the functions folder (which contained controllers for each of the models), the routes folder (which defined our application endpoints for the API and their corresponding tests) and finally the root, where we stored our core server files (which acts the as the foundation for our backend).

### Sequelize

We chose Sequelize to be our back-end's ORM as it is a promised-based Node.js ORM that works with Microsoft SQL Server. In Sequelise, models represent our database tables and allows us to interact with the data within these tables. Below is model that I defined for Investors:

```javascript
export const Investor = db.define(
  "Investor",
  {
    InvestorID: {
      type: DataTypes.UUID,
      defaultValue: DataTypes.UUIDV4,
      primaryKey: true,
    },
    InvestorFName: DataTypes.TEXT,
    InvestorLName: DataTypes.TEXT,
    InvestorEmail: DataTypes.STRING,
    InvestorPassword: DataTypes.TEXT,
    Username: DataTypes.TEXT,
    NetWorth: DataTypes.DECIMAL(20, 2),
    InvestorRanking: DataTypes.INTEGER,
    InvestorDifficulty: DataTypes.TEXT,
    DateJoined: DataTypes.DATEONLY,
    Title: DataTypes.TEXT,
    Funds: DataTypes.DECIMAL(20, 2),
  },
  { sequelize: db, tableName: "Investor", timestamps: false }
);
```

As you can see, we mimic our table. This way, we can directly call methods that interact with our database tables such as findByPk or findOne. These methods offer a lot of customisability, especially for tougher, more complicated queries. We often would wrap these complicated queries into functions that would be stored in our functions folder. For example, here is a function I wrote that utilises Sequelize models and methods to get all the current friends for a user.

```javascript
//Gets all CURRENT friends based on the corresponding user id
export async function getAllCurrentFriendsForUser(id) {
  return await Friends.findAll({
    where: {
      [Op.or]: [{ RequestingUsername: id }, { AcceptingUsername: id }],
      Status: 1,
    },
  });
}
```

### Unit Testing

### Crazy API stuff!

#### Price Data

I was responsible for devising a method to

#### News Feed

Vishaal was responsible for getting the news data for the application

### Order Queues

## Fun tidbits

## Concluding thoughts
