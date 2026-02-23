# Azure-Terraform-CI-CD-Pipeline-Project

Azure terraform and CI/CD Pipeline example using Azure web app

**Project Overview**

**Architecture/Design decisions**
**Issues Encountered**
**What I learnt**

<img width="957" height="1024" alt="image" src="https://github.com/user-attachments/assets/2bc8428e-c203-415e-b5e0-5c2447870b02" />

Image of the console and the making of a directory(Folder) (Named Devops-Container-App)

<img width="327" height="45" alt="image" src="https://github.com/user-attachments/assets/b7f83d39-fd5d-4829-9923-f850d47fcd43" />

Image of devops container folder being created

<img width="421" height="181" alt="image" src="https://github.com/user-attachments/assets/67ea4b9b-bcab-4106-a7d7-1d8e310b56b4" />

Production of structure for the project using GIT Bash

<img width="1172" height="868" alt="image" src="https://github.com/user-attachments/assets/038bdfaf-e385-40e6-92bc-681de2356bfe" />

index.html file being created( My example for this project was a Tech Review company)

<img width="1919" height="838" alt="image" src="https://github.com/user-attachments/assets/472dbdef-037d-4157-b369-6f622c45c686" />

Produced a Dockerfile by essentially making a text file and remove the txt exentsion you can also achieve this via bash(git bash)

<img width="1919" height="1006" alt="image" src="https://github.com/user-attachments/assets/e51676d0-76d2-4990-abf6-5e454e723f09" />

Commands put into Dockerfile(has to be named this exactly), this copies index.html to the nginx image

ALTERNATIVE METHOD


Demonstration of achieving this via bash

error that occurred was I shouldnt have included tags within the docker file

<img width="958" height="1007" alt="image" src="https://github.com/user-attachments/assets/45b438ce-d84a-4f95-8d52-894b24e1275b" />
Above shows locally testing the Dockerfile

<img width="1919" height="982" alt="image" src="https://github.com/user-attachments/assets/8c4c5d01-a515-4319-a174-9d1ceb612e98" />

above shows the actual testing as you can see the local testing was sucessful, I connected via a browser using http://local host:8080

next was to go to azure

<img width="1919" height="827" alt="image" src="https://github.com/user-attachments/assets/e1e2feab-94de-4ca2-8e0e-3a18cfcdb523" />

above shows using azure container registry I will be using a premade general main resource group(Lk_Res)

<img width="1919" height="830" alt="image" src="https://github.com/user-attachments/assets/802c2646-126e-4890-9086-e39b8fda7bc4" />

Issues occured above shows first there was no caps allowed second was that my subscription did not have container registry service(az means using azure CLI)

<img width="1919" height="1009" alt="image" src="https://github.com/user-attachments/assets/3ddec6e5-4aac-433f-af58-8c0d389af22b" />

above shows the troubleshooting page

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

after this in my local lkreviews-container-app folder I created a deploy.yml, this file gave instructions in what needed to be carried out for the project to work

<img width="1919" height="1005" alt="image" src="https://github.com/user-attachments/assets/3d0981aa-ada6-4fe5-9669-8e7b48e8612f" />

This information needed to be copied over to the github repository i was using

using git bash I first changed the directory to the location of my local project folder(lkreviews-container-app), then git add ., then git commit -m "intial commit" as shown below
**Clarifcation**
git init produces a .git file(stands for initialze)

git add . specfies that all following files should be added to this directory

git commit -m "Initial commit" saves a snapshot -m standing for message

<img width="941" height="850" alt="image" src="https://github.com/user-attachments/assets/98839037-6361-4734-91bf-5429f547436a" />



**Cleanup and Cost Management**
