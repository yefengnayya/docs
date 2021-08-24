## Requirements
* Move Festivus from EBS to ECS.
* Deployment workflow will be triggered when code merged to master branch. (CI/CD)

## Sub-tasks
* Create Dockerfile
* Create a Github action to trigger deployment workflow which will checkout code, create image and push image to ECR.
* Create new ECS service based on Shared-infra code

## Github action trigger deploy  
![Component Diagram](images/workflow.png?raw=true)  


## Introduce Terraform
### What terraform can do?
* using terraform script to create/destroy AWS resource.
* Store AWS resource's status in server side and local machine.

### Key concepts in Terraform
* Module  
Root module, child module, module block  
Module like a function, it has parameters, return values and can call other module.  
Root module like a entry point of a framework.  
Child module like a function that be called by other function(module).  
![Component Diagram](images/module.png?raw=true)  
https://www.terraform.io/docs/language/modules/index.html  
https://learn.hashicorp.com/tutorials/terraform/module?in=terraform/modules  

* Variables  
Input variable, output variable, local variable  
Input variables like parameters of a function.  
Output variable like return values of a function(module)  
![Component Diagram](images/variables.png?raw=true)  
https://www.terraform.io/docs/language/values/index.html

* Resource, Resource block:
![Component Diagram](images/resource.png?raw=true)  
https://www.terraform.io/docs/language/resources/index.html  


### Config environment variables
* Config credentials: AWS credential, Terraform Token
* Config ecs related: environment, app name, domain
* Config ecs container related fields: image ARN, cpu, memory, desired_capacity
Above three type are configed in action's yml file using "TF_VAR_" prefix
![Component Diagram](images/terraform.png?raw=true)  

* Config application related: BEARER_TOKEN, CMK, LOG_LEVEL, NEW_CLAIMS_SQS_URL, SENTRY_DSN...
Env variable name is configed in festivus.ecs.locals.secret_vars. Env variable value is stored in SSM.
![Component Diagram](images/local.png?raw=true)  
![Component Diagram](images/containerdef.png?raw=true)  
![Component Diagram](images/SSM.png?raw=true)  
