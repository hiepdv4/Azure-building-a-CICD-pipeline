# Overview
This is project Azure devops building a CICD pipeline for a Python-base application
### Project Plan
1. Trello board for the project
  . https://trello.com/b/F6Gw1XNA/udacity-azure-project2
2. Spreadsheet for the project that include task and estimated task.
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/0.plan.png)

# Instructions
- System diagram CICD azure devops

![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/18.diagram.png)
- Instructions for running the Python project. How could a user run project without manual processes. Developer pull/push code to repo github, github action will listen and trigger build CI for test code. After test successfully, Azure pipeline will trigger CD build code, push to artifacts and deploy to azure webapp.

1. Clone project into Azure Cloud Shell
- Open Azure Cloud Shell, create a SSH key pair **ssh-keygen -t rsa**
- Add public SSH key to your Github. This is guide https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent 
- Clone source code to Azure Cloud Shell
  - Git clone git@github.com:hiepdv4/Azure-building-a-CICD-pipeline.git
2. Deploy app on Azure App Service
- Go to folder **Azure-building-a-CICD-pipeline**
- Create the Python Virtual Environment
  - make setup
  - source ~/.udacity-devops-project2/bin/active
  - make all
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/1.setup_python_env.png)
  - Result test coverage
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/2.test_coverage.png)
