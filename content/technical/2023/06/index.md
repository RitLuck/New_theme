---
title: "Deploying an app service (web app) using Azure DevOps"
date: 2023-07-25T09:46:17+04:00
draft: true
---

Recently, I had the opportunity to work on a project that utilized an [Azure DevOps build pipeline](https://learn.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops) to deploy an [app service](https://learn.microsoft.com/en-us/azure/app-service/overview). Even though I don't really like Azure and am trying to focus more on AWS, I couldn't pass up the chance to learn new things. 

Since I didn't have a personal Azure Account, and Azure doesn't accept Visa cards during registration, I had to explore alternative solutions. Fortunately, I discovered that university students could create free accounts using their email addresses without the requirement of adding any credit card information.   More details can be found [here](https://azure.microsoft.com/en-us/free/students). Luckily, I had a friend who was in her third year at UOM, and with her kind assistance, I managed to overcome this hurdle 😅.
Thanks [Divya](https://mu.linkedin.com/in/divya-rampersad-328a10231).


## What is an Web App

In case you're new to Azure, [Microsoft Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/overview) offers a fully managed platform designed to facilitate the building, deployment, and scaling of web apps. As a Platform as a Service (PaaS), it eliminates the need to worry about infrastructure and performance, allowing quick and seamless app deployment. With support for various programming languages, including .NET, .NET Core, Java, Ruby, Node.js, PHP, and Python, developers can work with their preferred language. The flexibility extends to both Windows and Linux-based environments, enabling easy running and scaling of applications. 

Azure App Service goes beyond providing the capabilities of Microsoft Azure, incorporating features such as security, load balancing, autoscaling, and automated management into your application. Additionally, it leverages the DevOps capabilities, including continuous deployment from Azure DevOps, to further streamline the development process.

### What is Azure Devops

[Azure Devops](https://learn.microsoft.com/en-us/azure/devops/get-started/?view=azure-devops) is a comprehensive set of development and collaboration tools provided by Microsoft as a part of the Azure cloud platform. It offers a range of services to facilitate application development, continuous integration, continuous delivery (CI/CD), and project management. Azure DevOps is designed to streamline the entire software development lifecycle, from planning and coding to testing, deployment, and monitoring.

Okay, so enough of the boring part and lets get our hand dirty.

## Node.js application

Given that I'm still learning Node.js, I asked ChatGPT to write a simple and easy-to-understand Node.js app for me. I went for a Dad joke generator app because why not? The code was tested and works locally. Now, let's hope it works when it is added to the cloud. The code can be found on my GitHub repository.

![](./images/1.png)

## Creating App Service

1. Go to the Azure portal, search for App service and create a new Web app
2. Fill in the information by adding : 
    - Select your Subscription(mine is Azure for Students)
    - Choose Resource Group (if you don’t have one, you can click create new and specify the name).
    - Name of the Web App
    - Runtime stack. Specify the app service language. In this example, I chose Node 18 LTS.
    - OS (I Chose Linux)
    - Region (East US by default)
    - Princing Plan (Free F1, because this is just for demo purposes)

    ![](./images/2.png)

3. The remaining configurations can be left as default. 
4. Click Review + Create button, and wait until the app is deployed successfully.
    ![](./images/3.png)

5. Go to your resource and click the URL to ensure your app is running.
    ![](./images/4.png)

## Creating Service Principle

Since we're on the Azure Portal, let's create an App Registration because we don't want to encounter any errors later when trying to establish the service connection (been there).

1. Go to Active Directory
2. Click on App registrations

    ![](./images/5.png)

3. Once created, go the **Certificates & Secrets** and create a Secret. Make sure to store the Secret Value somewhere.
    ![](./images/6.png)


## Creating Devops Environment

