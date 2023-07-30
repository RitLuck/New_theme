---
title: "Deploying an app service (web app) using Azure DevOps"
date: 2023-07-25T09:46:17+04:00
draft: true
---

Recently, I had the opportunity to work on a project that utilized an [Azure DevOps build pipeline](https://learn.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops) to deploy an [app service](https://learn.microsoft.com/en-us/azure/app-service/overview). Azure DevOps pipelines have a lot of options and configurations and can be involved to dive into.

Since I didn't have a personal Azure Account, and Azure doesn't accept Visa cards during registration, I had to find a university student who could create a free account using their email address without the need to add any credit card information.  More details can be found [here](https://azure.microsoft.com/en-us/free/students). Luckily, I have friend who is in her third year at UOM, and I kinda took advantage of her 😅. Thanks [Divya](https://mu.linkedin.com/in/divya-rampersad-328a10231).


## Configuration for sample Node.js application

Since I'm still learning node.js. I asked ChatGPT to write a simple node js app for me. I installed dotenv so I could work with variables in my sample script and prepare for using them in the Azure build pipeline.