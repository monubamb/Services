Applications and their set of user expectations continue to evolve over the last few years. We have seen various trends like microservices and containerization become mainstream. The enterprises are beginning to realize the cost savings and other benefits of these technologies. It therefore becomes incumbent to build applications and service with this mindset. In this blog post, I will explain some of the foundational aspects of containerization and showcase ‘Docker for Windows’ Visual Studio Tooling. Along with that, we will see how to build ASP.NET core application with Docker Support Tooling

Before talking about containers, let’s take a moment to understand Microservices. Microservices and micro services style architecture is about decomposing monolithic application into smaller services. This enables versioning and deploying these services independently. Building microservices based applications helps accelerates agile delivery within an agile engineering teams.

Now let’s talk about containers. Containers provide a mechanism to run software reliably when moved from one computing environment to another. Simply put, containers are a portable unit of application and its underlying dependencies packaged (container image) together. By containerizing the application and its dependencies, the OS and underlying infrastructure differences are abstracted away. Containers isolate applications from each other on a shared OS. Additionally, we can get more isolation using Hyper V Containers. The micro services based services are a perfect fit for containerized applications.

Why should we be interested in containers? Let’s look at some of the value proposition around it.

– The containers enable ‘write-once, run anywhere’ apps.

– They enable microservices style architecture.

– It is also great for dev/test of apps and services.

– From the operations standpoint, this is great from portability and enables higher compute density. We can also scale up and down containers in response to the business needs.

Docker is platform for running these containerized applications. Docker is becoming the standard for implementing containers across the industry. There are different ways to run hosting containers within Docker.

 
1.Docker for Windows, which uses Hyper V to run the MobyLinux VM or Windows Containers
2.Docker for Mac
3.Boot2Docker and Virtual Box for older scenarios.

In this post, I want to give a quick overview on how to run Docker applications locally using ‘Docker for Windows’ using Visual Studio Tooling for an ASP.NET Core application.

Prerequisites: 

– Install Docker Tooling for Visual Studio 2015.

– ASP.NET Core

– Install Docker for Windows

Step 1:

Create ASP.NET Core Web Application using Visual Studio 2015


Steps 2:

Right Click on the Web Application we just created and Add – Docker Support. Upon adding Docker support, Visual Studio Tooling automatically creates various Docker files for you to use.

Step 3:

Review various Docker Files

a- Docker-compose.yml- This yml file is a Docker compose file. Docker compose is a tool which can be used to build multi-container applications. You can have more than one service defined in the docker compose file.


version: ‘2’

 

services:

  webapplication2:

    image: username/webapplication2

    build:

      context: .

      dockerfile: Dockerfile

    ports:

      – “8088:8088”
 

b- Docker File. This file is used to build the docker images using the instructions in this file.


FROM microsoft/dotnet:1.0.0-core

 

# Set the Working Directory

WORKDIR /app

 

# Configure the listening port to 8088

ENV ASPNETCORE_URLS http://*:8088

EXPOSE 8088

 

# Copy the app

COPY . /app

 

# Start the app

ENTRYPOINT dotnet WebApplication2.dll
 

Step 4 :

All you need now is to run your Visual Studio Application and you are up and running with your ASP.NET Core application running on a Docker container. We can take a look at the running container using the “docker ps -a” command.

In the next follow up blog post, we will explore How to deploy applications on Docker on Windows using Windows Server 2016 TP5
