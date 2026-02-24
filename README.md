# Azure-CI-CD-Pipeline-With-Docker Project

Azure terraform and CI/CD Pipeline example using Azure web app

**Project Overview**
This project demonstrates how the use of a CI/CD pipeline to automate the build and deployment of a containerized web application using GitHub Actions and Azure Container Registry(ACR). This was a challenging project for where I learnt a great deal about automation and cloud deployment.

**Architecture/Design decisions**
Preparation: 

<img width="1919" height="827" alt="container registry" src="https://github.com/user-attachments/assets/4d698b64-c433-44af-8a77-921d79c71ce8" />

above shows using Azure container registry I will be using a premade general main resource group(Lk_Res)

Deployment Flow:

Local folder development --> GitHub Repository configuration --> Azure Container Registry --> Azure web app and required resources creation


Containerization: Docker

CI/CD: GitHub Actions

Container Registry: Azure Container Registry(ACR)

Host and cloud provider: Azure

**What I learnt**

**Application containerization**
For this demonstration I produced a demo tech review website and used Docker to containerize the application.
**Production of Dockerfile**

<img width="1919" height="838" alt="dockerfile creating" src="https://github.com/user-attachments/assets/a5cb3055-a375-444c-87c5-5085e664c52f" />

I tested the container locally by using the following commands

docker build -t lkreviews-container-app
docker run -p 8080:80 lkreviews-container-app

**Design of CI/CD pipeline**

CI/CD workflow configured using GitHub Actions

Pipeline steps

1. Push to main branch(pipeline only runs when you push to main)

2. Authenticate to Azure using GitHub service principal credentials

3. Log into Azure Container Registry without this step, the project cannot be completed due to authentication errors.

Commands: az ACR login --name lkreviewsregistry

4. Build Docker Image(Previously shown)

<img width="958" height="1007" alt="build docker png" src="https://github.com/user-attachments/assets/86b6ab17-5c94-4c96-a3ae-a15fbc4c7518" />

It is important to locally test the Dockerfile before deploying

<img width="1919" height="982" alt="Local testing" src="https://github.com/user-attachments/assets/64241d7f-69d5-41bf-9b97-1cf1485724ab" />

I connected via a browser using http://localhost:8080

5. Image tagged(lkreviews_demo)

The image tag helps track versions. For this demonstration I used lkreviews_demo. In a larger project, I would rename this to v1 and keep a consistent sequence or I would put ${{GitHub.sha}} which automatically assigns a tag

6. Image is then pushed to ACR

This was done automatically as part of the pipeline. The section of code that this relates to is

<img width="1205" height="94" alt="pushing docker image" src="https://github.com/user-attachments/assets/fa1ae9c4-d112-4a06-8fd1-abb38e2f64aa" />

**Web App Configuration**

I then produced an Azure Container Registry(ACR) along with updating the registry to ensure admin permissions are enabled 

I then created a service plan for the Web Application

<img width="946" height="197" alt="app service plan" src="https://github.com/user-attachments/assets/6590f196-0cb9-4f3f-b95b-b8b5b8e4b365" />

Created a webapp using the previously provisioned resources and plans

I created a Contributor role assignment to allow GitHub to securely access Azure resources

<img width="1270" height="113" alt="creating role" src="https://github.com/user-attachments/assets/644e23c2-047a-46d6-b0cd-d3179eea741e" />

I needed to get ACR credentials for GitHub actions(allowing deploy.yml to function correctly)
az acr credential show
--name lkreviewsregistry
as well as copying the JSON file content resulted from the following commands:
az acr show \
--resource-group Lk_res \
--name lkreviewsregistry

In my local lkreviews-container-app folder I created a deploy.yml, this file gave instructions in what needed to be carried out for the project to work

<img width="1919" height="1005" alt="deploy" src="https://github.com/user-attachments/assets/88f93a11-04dd-4a39-ada7-75ecff9260c2" />

This information needed to be copied over to the GitHub repository i was using

using git bash I first changed the directory to the location of my local project folder(lkreviews-container-app), then git add ., then git commit -m "initial commit" as shown below

**Clarification**
git init produces a .git file(stands for initialize)

git add . specifies that all following files should be added to this directory

git commit -m "Initial commit" saves a snapshot

<img width="941" height="850" alt="upload" src="https://github.com/user-attachments/assets/dc1bf9e4-1935-4607-bb9e-019933af2f6e" />

<img width="1172" height="868" alt="index" src="https://github.com/user-attachments/assets/db8e0017-42e5-46e7-9056-723689cfc54b" />

index.html file being created( My example for this project was a Tech Review company)

**Issues Encountered**

Error that occurred was I shouldn't have included tags within the docker file

<img width="1919" height="830" alt="Issue" src="https://github.com/user-attachments/assets/30adc78c-9c94-4fb9-967e-2b44478529ad" />

Above shows two errors one being that the name of the credentials was case sensitive and the second error saying missing subscription registration

<img width="1919" height="1009" alt="Troubleshoot" src="https://github.com/user-attachments/assets/55388776-99f3-4427-84c2-6713399dc304" />

As this was my first time troubleshooting an error like this I did some research using microsoft resources to help identify the solution.

The solution was to go to the resource provider within the subscription settings. I later discovered other registries were missing such as Active Directory.

<img width="1919" height="827" alt="Azure sub 1" src="https://github.com/user-attachments/assets/aa3fa498-f9ee-4108-8ed2-dc3489a87b54" />

**Final Product**
Result was website running automated deployment through GitHub workflows successfully

<img width="1919" height="826" alt="Web final" src="https://github.com/user-attachments/assets/d46c9ba9-e7cc-45de-83d3-6807493f610b" />

**Cleanup and Cost Management**

As with my other projects, I deleted all provisioned resources after completion. This reduced costs and prevents unnecessary resource clutter, allowing me to prepare for my next project.
