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

I then produced a Azure Container Registry along with updating the registry to ensure admin permissions are enabled 


**Cleanup and Cost Management**
