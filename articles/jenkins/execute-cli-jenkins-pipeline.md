---
title: Execute the Azure CLI with Jenkins
description: Learn how to use Azure CLI to deploy a Java web app to Azure in Jenkins Pipeline
ms.service: jenkins
keywords: jenkins, azure, devops, app service, cli
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.topic: tutorial
ms.date: 6/7/2017
ms.openlocfilehash: b3d2f100f8837ad67a8dbd813c6e51255c78ad38
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865551"
---
# <a name="deploy-to-azure-app-service-with-jenkins-and-the-azure-cli"></a><span data-ttu-id="86098-104">Deploy to Azure App Service with Jenkins and the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="86098-104">Deploy to Azure App Service with Jenkins and the Azure CLI</span></span>
<span data-ttu-id="86098-105">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="86098-105">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="86098-106">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span><span class="sxs-lookup"><span data-stu-id="86098-106">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="86098-107">Create a Jenkins VM</span><span class="sxs-lookup"><span data-stu-id="86098-107">Create a Jenkins VM</span></span>
> * <span data-ttu-id="86098-108">Configure Jenkins</span><span class="sxs-lookup"><span data-stu-id="86098-108">Configure Jenkins</span></span>
> * <span data-ttu-id="86098-109">Create a web app in Azure</span><span class="sxs-lookup"><span data-stu-id="86098-109">Create a web app in Azure</span></span>
> * <span data-ttu-id="86098-110">Prepare a GitHub repository</span><span class="sxs-lookup"><span data-stu-id="86098-110">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="86098-111">Create Jenkins pipeline</span><span class="sxs-lookup"><span data-stu-id="86098-111">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="86098-112">Run the pipeline and verify the web app</span><span class="sxs-lookup"><span data-stu-id="86098-112">Run the pipeline and verify the web app</span></span>

<span data-ttu-id="86098-113">This tutorial requires the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="86098-113">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="86098-114">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="86098-114">To find the version, run `az --version`.</span></span> <span data-ttu-id="86098-115">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="86098-115">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="86098-116">Create and Configure Jenkins instance</span><span class="sxs-lookup"><span data-stu-id="86098-116">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="86098-117">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes the required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span><span class="sxs-lookup"><span data-stu-id="86098-117">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes the required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="86098-118">The Azure Credential plugin allows you to store Microsoft Azure service principal credentials in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="86098-118">The Azure Credential plugin allows you to store Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="86098-119">In version 1.2, we added the support so that Jenkins Pipeline can get the Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="86098-119">In version 1.2, we added the support so that Jenkins Pipeline can get the Azure credentials.</span></span> 

<span data-ttu-id="86098-120">Ensure you have version 1.2 or later:</span><span class="sxs-lookup"><span data-stu-id="86098-120">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="86098-121">Within the Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span><span class="sxs-lookup"><span data-stu-id="86098-121">Within the Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="86098-122">Update the plugin if the version is earlier than 1.2.</span><span class="sxs-lookup"><span data-stu-id="86098-122">Update the plugin if the version is earlier than 1.2.</span></span>

<span data-ttu-id="86098-123">Java JDK and Maven are also required in the Jenkins master.</span><span class="sxs-lookup"><span data-stu-id="86098-123">Java JDK and Maven are also required in the Jenkins master.</span></span> <span data-ttu-id="86098-124">To install, sign in to Jenkins master using SSH and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="86098-124">To install, sign in to Jenkins master using SSH and run the following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="86098-125">Add Azure service principal to Jenkins credential</span><span class="sxs-lookup"><span data-stu-id="86098-125">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="86098-126">An Azure credential is needed to execute Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="86098-126">An Azure credential is needed to execute Azure CLI.</span></span>

* <span data-ttu-id="86098-127">Within the Jenkins dashboard, click **Credentials -> System ->**.</span><span class="sxs-lookup"><span data-stu-id="86098-127">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="86098-128">Click **Global credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="86098-128">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="86098-129">Click **Add Credentials** to add a [Microsoft Azure service principal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span><span class="sxs-lookup"><span data-stu-id="86098-129">Click **Add Credentials** to add a [Microsoft Azure service principal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="86098-130">Provide an ID for use in subsequent step.</span><span class="sxs-lookup"><span data-stu-id="86098-130">Provide an ID for use in subsequent step.</span></span>

![Add Credentials](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-the-java-web-app"></a><span data-ttu-id="86098-132">Create an Azure App Service for deploying the Java web app</span><span class="sxs-lookup"><span data-stu-id="86098-132">Create an Azure App Service for deploying the Java web app</span></span>

<span data-ttu-id="86098-133">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#az-appservice-plan-create) CLI command.</span><span class="sxs-lookup"><span data-stu-id="86098-133">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#az-appservice-plan-create) CLI command.</span></span> <span data-ttu-id="86098-134">The appservice plan defines the physical resources used to host your apps.</span><span class="sxs-lookup"><span data-stu-id="86098-134">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="86098-135">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span><span class="sxs-lookup"><span data-stu-id="86098-135">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="86098-136">When the plan is ready, the Azure CLI shows similar output to the following example:</span><span class="sxs-lookup"><span data-stu-id="86098-136">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="86098-137">Create an Azure Web app</span><span class="sxs-lookup"><span data-stu-id="86098-137">Create an Azure Web app</span></span>

 <span data-ttu-id="86098-138">Use the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span><span class="sxs-lookup"><span data-stu-id="86098-138">Use the [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="86098-139">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span><span class="sxs-lookup"><span data-stu-id="86098-139">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="86098-140">Substitute the `<app_name>` placeholder with your own unique app name.</span><span class="sxs-lookup"><span data-stu-id="86098-140">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="86098-141">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="86098-141">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="86098-142">You can map a custom domain name entry to the web app before you expose it to your users.</span><span class="sxs-lookup"><span data-stu-id="86098-142">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="86098-143">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="86098-143">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="86098-144">Configure Java</span><span class="sxs-lookup"><span data-stu-id="86098-144">Configure Java</span></span> 

<span data-ttu-id="86098-145">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/webapp/config#az-appservice-web-config-update) command.</span><span class="sxs-lookup"><span data-stu-id="86098-145">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/webapp/config#az-appservice-web-config-update) command.</span></span>

<span data-ttu-id="86098-146">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="86098-146">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="86098-147">Prepare a GitHub Repository</span><span class="sxs-lookup"><span data-stu-id="86098-147">Prepare a GitHub Repository</span></span>
<span data-ttu-id="86098-148">Open the [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span><span class="sxs-lookup"><span data-stu-id="86098-148">Open the [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="86098-149">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span><span class="sxs-lookup"><span data-stu-id="86098-149">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

* <span data-ttu-id="86098-150">In GitHub web UI, open **Jenkinsfile** file.</span><span class="sxs-lookup"><span data-stu-id="86098-150">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="86098-151">Click the pencil icon to edit this file to update the resource group and name of your web app on line 20 and 21 respectively.</span><span class="sxs-lookup"><span data-stu-id="86098-151">Click the pencil icon to edit this file to update the resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="86098-152">Change line 23 to update credential ID in your Jenkins instance</span><span class="sxs-lookup"><span data-stu-id="86098-152">Change line 23 to update credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="86098-153">Create Jenkins pipeline</span><span class="sxs-lookup"><span data-stu-id="86098-153">Create Jenkins pipeline</span></span>
<span data-ttu-id="86098-154">Open Jenkins in a web browser, click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="86098-154">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="86098-155">Provide a name for the job and select **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="86098-155">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="86098-156">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="86098-156">Click **OK**.</span></span>
* <span data-ttu-id="86098-157">Click the **Pipeline** tab next.</span><span class="sxs-lookup"><span data-stu-id="86098-157">Click the **Pipeline** tab next.</span></span> 
* <span data-ttu-id="86098-158">For **Definition**, select **Pipeline script from SCM**.</span><span class="sxs-lookup"><span data-stu-id="86098-158">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="86098-159">For **SCM**, select **Git**.</span><span class="sxs-lookup"><span data-stu-id="86098-159">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="86098-160">Enter the GitHub URL for your forked repo: https:\<your forked repo\>.git</span><span class="sxs-lookup"><span data-stu-id="86098-160">Enter the GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="86098-161">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="86098-161">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="86098-162">Test your pipeline</span><span class="sxs-lookup"><span data-stu-id="86098-162">Test your pipeline</span></span>
* <span data-ttu-id="86098-163">Go to the pipeline you created, click **Build Now**</span><span class="sxs-lookup"><span data-stu-id="86098-163">Go to the pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="86098-164">A build should succeed in a few seconds, and you can go to the build and click **Console Output** to see the details</span><span class="sxs-lookup"><span data-stu-id="86098-164">A build should succeed in a few seconds, and you can go to the build and click **Console Output** to see the details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="86098-165">Verify your web app</span><span class="sxs-lookup"><span data-stu-id="86098-165">Verify your web app</span></span>
<span data-ttu-id="86098-166">To verify the WAR file is deployed successfully to your web app.</span><span class="sxs-lookup"><span data-stu-id="86098-166">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="86098-167">Open a web browser:</span><span class="sxs-lookup"><span data-stu-id="86098-167">Open a web browser:</span></span>

* <span data-ttu-id="86098-168">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="86098-168">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="86098-169">You see:</span><span class="sxs-lookup"><span data-stu-id="86098-169">You see:</span></span>

        Welcome to Java Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="86098-170">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span><span class="sxs-lookup"><span data-stu-id="86098-170">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>

![Calculator: add](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-to-azure-web-app-on-linux"></a><span data-ttu-id="86098-172">Deploy to Azure Web App on Linux</span><span class="sxs-lookup"><span data-stu-id="86098-172">Deploy to Azure Web App on Linux</span></span>
<span data-ttu-id="86098-173">Now that you know how to use Azure CLI in your Jenkins pipeline, you can modify the script to deploy to an Azure Web App on Linux.</span><span class="sxs-lookup"><span data-stu-id="86098-173">Now that you know how to use Azure CLI in your Jenkins pipeline, you can modify the script to deploy to an Azure Web App on Linux.</span></span>

<span data-ttu-id="86098-174">Web App on Linux supports a different way to do the deployment, which is to use Docker.</span><span class="sxs-lookup"><span data-stu-id="86098-174">Web App on Linux supports a different way to do the deployment, which is to use Docker.</span></span> <span data-ttu-id="86098-175">To deploy, you need to provide a Dockerfile that packages your web app with service runtime into a Docker image.</span><span class="sxs-lookup"><span data-stu-id="86098-175">To deploy, you need to provide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="86098-176">The plugin will then build the image, push it to a Docker registry and deploy the image to your web app.</span><span class="sxs-lookup"><span data-stu-id="86098-176">The plugin will then build the image, push it to a Docker registry and deploy the image to your web app.</span></span>

* <span data-ttu-id="86098-177">Follow the steps [here](../app-service/containers/quickstart-nodejs.md) to create an Azure Web App running on Linux.</span><span class="sxs-lookup"><span data-stu-id="86098-177">Follow the steps [here](../app-service/containers/quickstart-nodejs.md) to create an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="86098-178">Install Docker on your Jenkins instance by following the instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="86098-178">Install Docker on your Jenkins instance by following the instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="86098-179">Create a Container Registry in the Azure portal by using the steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="86098-179">Create a Container Registry in the Azure portal by using the steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="86098-180">In the same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit the **Jenkinsfile2** file:</span><span class="sxs-lookup"><span data-stu-id="86098-180">In the same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit the **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="86098-181">Line 18-21, update to the names of your resource group, web app, and ACR respectively.</span><span class="sxs-lookup"><span data-stu-id="86098-181">Line 18-21, update to the names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="86098-182">Line 24, update \<azsrvprincipal\> to your credential ID</span><span class="sxs-lookup"><span data-stu-id="86098-182">Line 24, update \<azsrvprincipal\> to your credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="86098-183">Create a new Jenkins pipeline as you did when deploying to Azure web app in Windows, only this time, use **Jenkinsfile2** instead.</span><span class="sxs-lookup"><span data-stu-id="86098-183">Create a new Jenkins pipeline as you did when deploying to Azure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="86098-184">Run your new job.</span><span class="sxs-lookup"><span data-stu-id="86098-184">Run your new job.</span></span>
* <span data-ttu-id="86098-185">To verify, in Azure CLI, run:</span><span class="sxs-lookup"><span data-stu-id="86098-185">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="86098-186">You get the following result:</span><span class="sxs-lookup"><span data-stu-id="86098-186">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="86098-187">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="86098-187">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="86098-188">You see the message:</span><span class="sxs-lookup"><span data-stu-id="86098-188">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="86098-189">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span><span class="sxs-lookup"><span data-stu-id="86098-189">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="86098-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="86098-190">Next steps</span></span>
<span data-ttu-id="86098-191">In this tutorial, you configured a Jenkins pipeline that checks out the source code in GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="86098-191">In this tutorial, you configured a Jenkins pipeline that checks out the source code in GitHub repo.</span></span> <span data-ttu-id="86098-192">Runs Maven to build a war file and then uses Azure CLI to deploy to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="86098-192">Runs Maven to build a war file and then uses Azure CLI to deploy to Azure App Service.</span></span> <span data-ttu-id="86098-193">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="86098-193">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="86098-194">Create a Jenkins VM</span><span class="sxs-lookup"><span data-stu-id="86098-194">Create a Jenkins VM</span></span>
> * <span data-ttu-id="86098-195">Configure Jenkins</span><span class="sxs-lookup"><span data-stu-id="86098-195">Configure Jenkins</span></span>
> * <span data-ttu-id="86098-196">Create a web app in Azure</span><span class="sxs-lookup"><span data-stu-id="86098-196">Create a web app in Azure</span></span>
> * <span data-ttu-id="86098-197">Prepare a GitHub repository</span><span class="sxs-lookup"><span data-stu-id="86098-197">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="86098-198">Create Jenkins pipeline</span><span class="sxs-lookup"><span data-stu-id="86098-198">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="86098-199">Run the pipeline and verify the web app</span><span class="sxs-lookup"><span data-stu-id="86098-199">Run the pipeline and verify the web app</span></span>
