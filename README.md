# Azure-CI-CD-Pipeline-With-Docker Project

Azure terraform and CI/CD Pipeline example using Azure web app

**Project Overview**
This project demonstrates how the use of CI/CD pipeline to automate the build and deployment of a containerized web application using Github Actions and Azure Container Registry(ACR).This was a challenging project for where I learnt a lot.

**Architecture/Design decisions**
Preperation: 

<img width="1919" height="827" alt="image" src="https://github.com/user-attachments/assets/e1e2feab-94de-4ca2-8e0e-3a18cfcdb523" />

above shows using azure container registry I will be using a premade general main resource group(Lk_Res)

Deployment Flow:

Local folder development --> Github Repository configuration --> Azure Container Registry --> Azure web app and required resources creation


Containerization: Docker

CI/CD: GitHub Actions

Container Registry: Azure Container Registry(ACR)

Host and cloud provider: Azure

**What I learnt**

**Application containerization**
For this demonstration I had produced a demo Tech Review Website, I used Docker to containerize this website.

**Production of Dockerfile**
<img width="1919" height="838" alt="image" src="https://github.com/user-attachments/assets/1964127e-8ee2-4322-8bfe-75c41921d40e" />

I tested the container locally by using the following commands

docker build -t lkreviews-container-app
docker run -p 8080:80 lkreviews-container-app

CHECK

**Design of CI/CD pipeline**

CI/CD workflow configured using GitHub Actions

Pipeline steps

1. Push to main branch(pipeline only runs when you push to main)

<img width="911" height="571" alt="image" src="https://github.com/user-attachments/assets/39f14264-7a93-4613-a471-ae10cbdd89ff" />

2. Authenticate to azure using github service principal credentials

3. Log into Azure Container Registry wuthout this this project cannot be completed de to errors which will occur

Commands: az acr login --name Lkreviewsregistry

4. Build Docker Image(Previously shown)

<img width="958" height="1007" alt="image" src="https://github.com/user-attachments/assets/45b438ce-d84a-4f95-8d52-894b24e1275b" />

Important to locally testing the Dockerfile

<img width="1919" height="982" alt="image" src="https://github.com/user-attachments/assets/8c4c5d01-a515-4319-a174-9d1ceb612e98" />

I connected via a browser using http://local host:8080

5. Image tagged(lkreviews_demo)

Essentially keeps track of the image version as a demonstration I named this Lkreviews_demo but, under a longer project I would rename this to v1 if required but, putting ${{github.sha}} automatically assigns a tag

6. Image is then pushed to ACR

This was done automatically as part of the pipeline the section of code that this relates to is

<img width="1205" height="94" alt="image" src="https://github.com/user-attachments/assets/6d4718eb-c604-4a1c-837f-509747cf4c0d" />

**Web App Configuration**

<img width="1172" height="868" alt="image" src="https://github.com/user-attachments/assets/038bdfaf-e385-40e6-92bc-681de2356bfe" />

index.html file being created( My example for this project was a Tech Review company)

**Issues Encountered**

Error that occurred was I shouldnt have included tags within the docker file

<img width="1919" height="830" alt="image" src="https://github.com/user-attachments/assets/802c2646-126e-4890-9086-e39b8fda7bc4" />

Above shows two errors one being that the name of the credentials was case sensitive and the second error saying missing subscription registration

<img width="1919" height="1009" alt="image" src="https://github.com/user-attachments/assets/3ddec6e5-4aac-433f-af58-8c0d389af22b" />

As this was my first time troubleshooting an error like this I did some reserach using microsoft resources to help identify the solution.

The solution was to go to the resource provider

One of the other issues that occured was that I was missing multiple subscription resource providers. below shows a screenshot of me registring for one of these resource providers.

<img width="1919" height="827" alt="image" src="https://github.com/user-attachments/assets/2c7a152e-6c72-4573-aeca-b8a118f96582" />

I then produced a Azure Container Registry(acr) along with updating the registry to ensure admin permissions are enabled 

I then created a service plan for the Web Application

<img width="946" height="197" alt="image" src="https://github.com/user-attachments/assets/e4621928-2eab-487e-a8a3-85d9b49443e8" />

then created a webapp using the previously provisioned resources and plans

Produced a contributor role allowing data to be accessed from github

<img width="1270" height="113" alt="image" src="https://github.com/user-attachments/assets/24748c87-b82c-400a-bb5c-893b13496450" />

needed to get ACR credentials for github actions(allowing deploy.yml to function correctly)
az acr credential show
--name lkreviewsregistry
as well as copying the JSON file content resulted from the following commands:
az acr show \
--resource-group Lk_res \
--name lkreviewsregistry

In my local lkreviews-container-app folder I created a deploy.yml, this file gave instructions in what needed to be carried out for the project to work

<img width="1919" height="1005" alt="image" src="https://github.com/user-attachments/assets/3d0981aa-ada6-4fe5-9669-8e7b48e8612f" />

This information needed to be copied over to the github repository i was using

using git bash I first changed the directory to the location of my local project folder(lkreviews-container-app), then git add ., then git commit -m "intial commit" as shown below

**Clarifcation**
git init produces a .git file(stands for initialze)

git add . specfies that all following files should be added to this directory

git commit -m "Initial commit" saves a snapshot -m standing for message

<img width="941" height="850" alt="image" src="https://github.com/user-attachments/assets/98839037-6361-4734-91bf-5429f547436a" />

Final Result website running automated deployment through github workflows successfully

<img width="1919" height="826" alt="image" src="https://github.com/user-attachments/assets/919e925e-e7fb-427d-a2da-e39e410f4199" />

**Cleanup and Cost Management**
