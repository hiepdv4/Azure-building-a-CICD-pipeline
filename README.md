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
- Deploy project to web service using Azure Cloud Shell
  - az webapp up --name azureproject2 --resource-group Azuredevops --runtime "PYTHON:3.7"
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/3.azure_build_webapp.png)
- Prediction run against a working deployed Azure Application
- Update new URL 
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/4.update_make_predict_azure_app.png)
- Run ./make_predict_azure_app.sh
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/5.run_prediction_az.png)

3. [CI] Setup Github Action:
- Enable it in your Github https://github.com/marketplace/azure-pipelines
- Verify github apps
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/19.github_action1.png)
- File workflow CI github https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/.github/workflows/main.yml
- Check CI test code successfully.
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/17.github_action.png)
4. [CD] Setup Azure pipeline
- Configure the Linux VM as an Azure DevOps Build Agent
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/6.VM_agent.png)
- SSH into the VM agent
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/7.ssh_agent.png)
- Config agent
  - curl -O https://vstsagentpackage.azureedge.net/agent/2.202.1/vsts-agent-linux-x64-2.202.1.tar.gz
  - mkdir myagent && cd myagent
  - tar zxvf ../vsts-agent-linux-x64-2.202.1.tar.gz
  - ./config.sh # Configure the agent
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/8.config_agent.png)
  - sudo ./svc.sh install
  - sudo ./svc.sh start
- Check service agent on VM
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/20.service_agent.png)
- Confirm that the self-hosted agent is online on dev.azure.com
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/9.agent_pool.png)
- Create service connection
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/10.service_connection.png)
- Add repo source code python to azure pipeline
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/11.add_repo_github.png)
- Config pipeline azure YAML
  - Update azureServiceConnectionId
  - Update webAppName
  - Update environmentName
https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/azure-pipelines.yml
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/12.azure_pipeline.png)
- Pipeline azure trigged after new code push to repo
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/13.az_pipeline.png)
- Log pipeline azure
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/14.deploy_webapp.png)
- New code deployed to azure web app
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/16.URL.png)
- Run script ./make_predict_azure_app.sh to check azure app working
![alt text](https://github.com/hiepdv4/Azure-building-a-CICD-pipeline/blob/main/images/15.test_app.png)

# Enhancements
- Deploy project using Docker or Kubernetes

# Demo
https://www.youtube.com/watch?v=nXLFr0ICjkU








