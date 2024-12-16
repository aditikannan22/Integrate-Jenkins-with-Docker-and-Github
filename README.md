## Integrate Jenkins with Docker and Github

## Overview

This project demonstrates how to integrate Jenkins with GitHub, Docker, and Docker Hub to automate the process of building, testing, dockerizing, and deploying a Java application.

## Prerequisites
- Docker
- Jenkins
- GitHub account
- Docker Hub account
- Java Development Kit (JDK)
- Apache Maven

## Build and Run Jenkins Docker Container
docker build -t jenkins-docker jenkins-docker-files/
docker run -it -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --restart unless-stopped jenkins-docker
Jenkins Configuration
2.1 Access Jenkins
Visit http://localhost:8080

Use the initial password from /var/jenkins_home/secrets/initialAdminPassword

## Install Necessary Plugins
Docker

Git

Maven Integration

CloudBees Docker Build and Publish

Docker Pipeline

## Configure Global Tools
JDK: Add JAVA_HOME path

Maven: Add Maven home directory

## Create Jenkins Freestyle Project
Source Code Management (SCM)
Select Git
Add GitHub repository URL

Build Triggers
Select Poll SCM
Set schedule: H/5 * * * *

Set Git and Docker Credentials as Environment Variables in the Build Environment

## Build Steps
Create a step with execute shell to change the directory to src

Invoke a maven target with goal as "-f src/pom.xml clean install"

Invoke another maven target with goals as "-f src/pom.xml test"

Create a step with execute shell to login to DockerHub with the provided credentials, build the image with the correct tag and push it to DockerHub
Click on Save

## Building the Project
Any changed pushed to the repository will trigger a build. Jenkins polls for changes every 5 minutes.
