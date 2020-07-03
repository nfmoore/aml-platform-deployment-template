# Getting Started

### 1. Create a new GitHub repository

1. Login to your GitHub account, navigate to the [AML Platform Deployment Template repository](https://github.com/nfmoore/aml-platform-deployment-template) and create a new repository from this template. Use [these](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template) instructions for more details about creating a repository from a template.

### 2. Create and configure a new Azure DevOps Project

1. Create a new project in Azure DevOps. Use [these](https://docs.microsoft.com/en-us/azure/devops/organizations/projects/create-project?view=azure-devops&tabs=preview-page#create-a-project) instructions for more details about creating a project in Azure DevOps.

2. Create an Azure Resource Manager Service connection. This is needed so Azure Devops can connect to your subscription and create/manage resources.

   1. Click on `project settings` (found at the bottom-left of the portal).
   2. Click on `Service Connections` (found on the sidebar).
   3. Click `New Service Connection` (found at the top-right of the portal).
   4. Select `Azure Resource Manager` and click `Next`.
   5. Select `Service principal (automatic)` and click `Next`.
   6. Leave `Subscription` as the scope level and select your `subscription` from the dropdown.
   7. In the `Service connection name` textbox enter `azure-service-connection`. Note: you can enter another name for your service connection but this will require editing the [`variables.yml`](../.pipelines/templates/variables.yml) file.
   8. Leave the `Allow all pipelines to use this connection` checkbox selected and click `Next`.

   The above steps assume you have `Contributor` or `Owner` access to the subscription or resource group.

   See [these](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints#create-a-service-connection) instructions for more details about creating an Azure Resource Manager Service connection.

### 3. Deploy the platform

1. In your GitHub repository, edit the any variables in the [`variables.yml`](../.pipelines/templates/variables.yml) you wish to change for your deployment. Remember to change the values for `service_connection` or `resource_group_name` if you have selected something different in section 2 step 2 above.

2. In your Azure DevOps project, create a build pipeline from your forked repository.

   1. Select the `Pipelines` tab from the `Pipelines` section (found on the sidebar).
   2. Click on `New Pipeline` (found at the top-right of the portal).
   3. Select `GitHub` (authenticate if necessary).
   4. Select your GitHub repository from the list of repositories (authenticate if necessary).
   5. Select `Existing Azure Pipelines YAML File`.
   6. Select the `master` branch and enter `/.pipeline/main.yml` as the path or select it from the dropdown and click `Continue`.
   7. Select `Run` from the top-right of the protal to execute the pipeline and deploy the platform.

   See [these](https://docs.microsoft.com/en-us/azure/devops/pipelines/create-first-pipeline) instructions for more details about creating a pipeline in Azrue DevOps.

## Use the platform

- In your [Azure Portal](https://www.portal.azure.com) you should now have a resource group with an Azure Machine Learning workspace with [associated resources](https://docs.microsoft.com/en-us/azure/machine-learning/concept-workspace#resources) and an [AKS cluster](https://docs.microsoft.com/en-us/azure/aks/intro-kubernetes). Your workspace should have a registered [dataset](https://docs.microsoft.com/en-us/azure/machine-learning/concept-data#datasets), a [compute cluster](https://docs.microsoft.com/en-us/azure/machine-learning/concept-compute-target#azure-machine-learning-compute-managed) and the [AKS cluster](https://docs.microsoft.com/en-us/azure/aks/intro-kubernetes) should be attached to the workspace as an inference cluster.
- To launch the Azure Machine Learning studio workspace select the resource from your resource group and click `Launch Now`. Alternatively, navigate to [ml.azure.com](https://ml.azure.com/) and select the your directory, subscription, and workspace.
