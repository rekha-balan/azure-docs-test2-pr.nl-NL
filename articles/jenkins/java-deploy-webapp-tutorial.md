---
title: Use Jenkins to deploy your web apps to Azure
description: Set up continuous integration from GitHub to Azure App Service for your Java web apps using Jenkins and Docker.
ms.service: jenkins
keywords: jenkins, azure, devops, app service, continuous integration, ci, continuous deployment, cd
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.topic: tutorial
ms.date: 07/31/2018
ms.openlocfilehash: b1af82060d316a18cd6427f70695ca4fa982064d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871617"
---
# <a name="set-up-continuous-integration-and-deployment-to-azure-app-service-with-jenkins"></a><span data-ttu-id="53d5c-104">Set up continuous integration and deployment to Azure App Service with Jenkins</span><span class="sxs-lookup"><span data-stu-id="53d5c-104">Set up continuous integration and deployment to Azure App Service with Jenkins</span></span>

<span data-ttu-id="53d5c-105">This tutorial sets up continuous integration and deployment (CI/CD) of a sample Java web app developed with the [Spring Boot](http://projects.spring.io/spring-boot/) framework to [Azure App Service Web App on Linux](/azure/app-service/containers/app-service-linux-intro) using Jenkins.</span><span class="sxs-lookup"><span data-stu-id="53d5c-105">This tutorial sets up continuous integration and deployment (CI/CD) of a sample Java web app developed with the [Spring Boot](http://projects.spring.io/spring-boot/) framework to [Azure App Service Web App on Linux](/azure/app-service/containers/app-service-linux-intro) using Jenkins.</span></span>

<span data-ttu-id="53d5c-106">You will perform the following tasks in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="53d5c-106">You will perform the following tasks in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="53d5c-107">Install the Jenkins plug-ins needed to deploy to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="53d5c-107">Install the Jenkins plug-ins needed to deploy to Azure App Service.</span></span>
> * <span data-ttu-id="53d5c-108">Define a Jenkins job to build Docker images from a GitHub repo when a new commit is pushed.</span><span class="sxs-lookup"><span data-stu-id="53d5c-108">Define a Jenkins job to build Docker images from a GitHub repo when a new commit is pushed.</span></span>
> * <span data-ttu-id="53d5c-109">Define a new Azure Web App for Linux and configure it to deploy Docker images pushed to Azure Container registry.</span><span class="sxs-lookup"><span data-stu-id="53d5c-109">Define a new Azure Web App for Linux and configure it to deploy Docker images pushed to Azure Container registry.</span></span>
> * <span data-ttu-id="53d5c-110">Configure the Azure App Service Jenkins plug-in.</span><span class="sxs-lookup"><span data-stu-id="53d5c-110">Configure the Azure App Service Jenkins plug-in.</span></span>
> * <span data-ttu-id="53d5c-111">Deploy the sample app to Azure App Service with a manual build.</span><span class="sxs-lookup"><span data-stu-id="53d5c-111">Deploy the sample app to Azure App Service with a manual build.</span></span>
> * <span data-ttu-id="53d5c-112">Trigger a Jenkins build and update the web app by pushing changes to GitHub.</span><span class="sxs-lookup"><span data-stu-id="53d5c-112">Trigger a Jenkins build and update the web app by pushing changes to GitHub.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="53d5c-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="53d5c-113">Before you begin</span></span>

<span data-ttu-id="53d5c-114">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="53d5c-114">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="53d5c-115">[Jenkins](https://jenkins.io/) with JDK and Maven tools configured.</span><span class="sxs-lookup"><span data-stu-id="53d5c-115">[Jenkins](https://jenkins.io/) with JDK and Maven tools configured.</span></span> <span data-ttu-id="53d5c-116">If you don't have a Jenkins system, create one now in Azure from the [Jenkins solution template](/azure/jenkins/install-jenkins-solution-template).</span><span class="sxs-lookup"><span data-stu-id="53d5c-116">If you don't have a Jenkins system, create one now in Azure from the [Jenkins solution template](/azure/jenkins/install-jenkins-solution-template).</span></span>
* <span data-ttu-id="53d5c-117">A [GitHub](https://github.com) account.</span><span class="sxs-lookup"><span data-stu-id="53d5c-117">A [GitHub](https://github.com) account.</span></span>
* <span data-ttu-id="53d5c-118">[Azure CLI 2.0](/cli/azure), either from your local command line or in the [Azure Cloud Shell](/azure/cloud-shell/overview)</span><span class="sxs-lookup"><span data-stu-id="53d5c-118">[Azure CLI 2.0](/cli/azure), either from your local command line or in the [Azure Cloud Shell](/azure/cloud-shell/overview)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="install-jenkins-plug-ins"></a><span data-ttu-id="53d5c-119">Install Jenkins plug-ins</span><span class="sxs-lookup"><span data-stu-id="53d5c-119">Install Jenkins plug-ins</span></span>

1. <span data-ttu-id="53d5c-120">Open a web browser to your Jenkins web console and select **Manage Jenkins** from the left-hand menu, then select **Manage Plugins**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-120">Open a web browser to your Jenkins web console and select **Manage Jenkins** from the left-hand menu, then select **Manage Plugins**.</span></span>
2. <span data-ttu-id="53d5c-121">Select the **Available** tab.</span><span class="sxs-lookup"><span data-stu-id="53d5c-121">Select the **Available** tab.</span></span>
3. <span data-ttu-id="53d5c-122">Search for and select the checkbox next to the following plug-ins:</span><span class="sxs-lookup"><span data-stu-id="53d5c-122">Search for and select the checkbox next to the following plug-ins:</span></span>   

    - [<span data-ttu-id="53d5c-123">Azure App Service Plug-in</span><span class="sxs-lookup"><span data-stu-id="53d5c-123">Azure App Service Plug-in</span></span>](https://plugins.jenkins.io/azure-app-service)
    - [<span data-ttu-id="53d5c-124">GitHub Branch Source Plug-in</span><span class="sxs-lookup"><span data-stu-id="53d5c-124">GitHub Branch Source Plug-in</span></span>](https://plugins.jenkins.io/github-branch-source)

    <span data-ttu-id="53d5c-125">If the plugins do not appear, make sure they aren't already installed by checking the **Installed** tab.</span><span class="sxs-lookup"><span data-stu-id="53d5c-125">If the plugins do not appear, make sure they aren't already installed by checking the **Installed** tab.</span></span>

1. <span data-ttu-id="53d5c-126">Select **Download now and install after restart** to enable the plugins in your Jenkins configuration.</span><span class="sxs-lookup"><span data-stu-id="53d5c-126">Select **Download now and install after restart** to enable the plugins in your Jenkins configuration.</span></span>

## <a name="configure-github-and-jenkins"></a><span data-ttu-id="53d5c-127">Configure GitHub and Jenkins</span><span class="sxs-lookup"><span data-stu-id="53d5c-127">Configure GitHub and Jenkins</span></span>

<span data-ttu-id="53d5c-128">Set up Jenkins to receive [GitHub webhooks](https://developer.github.com/webhooks/) when new commits are pushed to a repo in your account.</span><span class="sxs-lookup"><span data-stu-id="53d5c-128">Set up Jenkins to receive [GitHub webhooks](https://developer.github.com/webhooks/) when new commits are pushed to a repo in your account.</span></span>

1. <span data-ttu-id="53d5c-129">Select **Manage Jenkins**, then **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-129">Select **Manage Jenkins**, then **Configure System**.</span></span> <span data-ttu-id="53d5c-130">In the **GitHub** section, make sure **Manage hooks** is selected and then select **Manage additional GitHub actions** and choose **Convert login and password to token**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-130">In the **GitHub** section, make sure **Manage hooks** is selected and then select **Manage additional GitHub actions** and choose **Convert login and password to token**.</span></span>
2. <span data-ttu-id="53d5c-131">Select the **From login and password** radio button and enter your GitHub username and password.</span><span class="sxs-lookup"><span data-stu-id="53d5c-131">Select the **From login and password** radio button and enter your GitHub username and password.</span></span> <span data-ttu-id="53d5c-132">Select **Create token credentials** to create a new [GitHub Personal Access Token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/).</span><span class="sxs-lookup"><span data-stu-id="53d5c-132">Select **Create token credentials** to create a new [GitHub Personal Access Token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/).</span></span>   
   <span data-ttu-id="53d5c-133">![Create GitHub PAT from login and password](media/jenkins-java-quickstart/create_github_credentials.png)</span><span class="sxs-lookup"><span data-stu-id="53d5c-133">![Create GitHub PAT from login and password](media/jenkins-java-quickstart/create_github_credentials.png)</span></span>
3.  <span data-ttu-id="53d5c-134">Select the newly created token from the **Credentials** drop down in the GitHub Servers configuration.</span><span class="sxs-lookup"><span data-stu-id="53d5c-134">Select the newly created token from the **Credentials** drop down in the GitHub Servers configuration.</span></span> <span data-ttu-id="53d5c-135">Select **Test connection** to verify that the authentication is working.</span><span class="sxs-lookup"><span data-stu-id="53d5c-135">Select **Test connection** to verify that the authentication is working.</span></span>   
   <span data-ttu-id="53d5c-136">![Verify connection to GitHub once PAT is configured](media/jenkins-java-quickstart/verify_github_connection.png)</span><span class="sxs-lookup"><span data-stu-id="53d5c-136">![Verify connection to GitHub once PAT is configured](media/jenkins-java-quickstart/verify_github_connection.png)</span></span>

> [!NOTE]
> <span data-ttu-id="53d5c-137">If your GitHub account has two-factor authentication enabled,  create the token on GitHub and configure Jenkins to use it.</span><span class="sxs-lookup"><span data-stu-id="53d5c-137">If your GitHub account has two-factor authentication enabled,  create the token on GitHub and configure Jenkins to use it.</span></span> <span data-ttu-id="53d5c-138">Review the [Jenkins GitHub plug-in](https://wiki.jenkins.io/display/JENKINS/Github+Plugin) documentation for full details.</span><span class="sxs-lookup"><span data-stu-id="53d5c-138">Review the [Jenkins GitHub plug-in](https://wiki.jenkins.io/display/JENKINS/Github+Plugin) documentation for full details.</span></span>

## <a name="fork-the-sample-repo-and-create-a-jenkins-job"></a><span data-ttu-id="53d5c-139">Fork the sample repo and create a Jenkins job</span><span class="sxs-lookup"><span data-stu-id="53d5c-139">Fork the sample repo and create a Jenkins job</span></span> 

1. <span data-ttu-id="53d5c-140">Open the [Spring Boot sample application repo](https://github.com/spring-guides/gs-spring-boot-docker) and fork it to your own GitHub account by selecting **Fork** in the top right-hand corner.</span><span class="sxs-lookup"><span data-stu-id="53d5c-140">Open the [Spring Boot sample application repo](https://github.com/spring-guides/gs-spring-boot-docker) and fork it to your own GitHub account by selecting **Fork** in the top right-hand corner.</span></span>   
    <span data-ttu-id="53d5c-141">![Fork from GitHub](media/jenkins-java-quickstart/fork_github_repo.png)</span><span class="sxs-lookup"><span data-stu-id="53d5c-141">![Fork from GitHub](media/jenkins-java-quickstart/fork_github_repo.png)</span></span>
1. <span data-ttu-id="53d5c-142">In the Jenkins web console, select **New Item**, give it a name **MyJavaApp**, select **Freestyle project**, then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-142">In the Jenkins web console, select **New Item**, give it a name **MyJavaApp**, select **Freestyle project**, then select **OK**.</span></span>   
    <span data-ttu-id="53d5c-143">![New Jenkins Freestyle Project](media/jenkins-java-quickstart/jenkins_freestyle.png)</span><span class="sxs-lookup"><span data-stu-id="53d5c-143">![New Jenkins Freestyle Project](media/jenkins-java-quickstart/jenkins_freestyle.png)</span></span>
2. <span data-ttu-id="53d5c-144">Under the **General** section, select **GitHub** project and enter your forked repo URL such as https://github.com/raisa/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="53d5c-144">Under the **General** section, select **GitHub** project and enter your forked repo URL such as https://github.com/raisa/gs-spring-boot-docker</span></span>
3. <span data-ttu-id="53d5c-145">Under the **Source code management**  section, select **Git**, enter your forked repo `.git` URL such as https://github.com/raisa/gs-spring-boot-docker.git</span><span class="sxs-lookup"><span data-stu-id="53d5c-145">Under the **Source code management**  section, select **Git**, enter your forked repo `.git` URL such as https://github.com/raisa/gs-spring-boot-docker.git</span></span>
4. <span data-ttu-id="53d5c-146">Under the **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-146">Under the **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
5. <span data-ttu-id="53d5c-147">Under the **Build** section, select **Add build step** and choose **Invoke top-level Maven targets**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-147">Under the **Build** section, select **Add build step** and choose **Invoke top-level Maven targets**.</span></span> <span data-ttu-id="53d5c-148">Enter `package` in the **Goals** field.</span><span class="sxs-lookup"><span data-stu-id="53d5c-148">Enter `package` in the **Goals** field.</span></span>
6. <span data-ttu-id="53d5c-149">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-149">Select **Save**.</span></span> <span data-ttu-id="53d5c-150">You can test your job by selecting **Build Now** from the project page.</span><span class="sxs-lookup"><span data-stu-id="53d5c-150">You can test your job by selecting **Build Now** from the project page.</span></span>

## <a name="configure-azure-app-service"></a><span data-ttu-id="53d5c-151">Configure Azure App Service</span><span class="sxs-lookup"><span data-stu-id="53d5c-151">Configure Azure App Service</span></span> 

1. <span data-ttu-id="53d5c-152">Using the Azure CLI or [Cloud Shell](/azure/cloud-shell/overview), create a new [Web App on Linux](/azure/app-service/containers/app-service-linux-intro).</span><span class="sxs-lookup"><span data-stu-id="53d5c-152">Using the Azure CLI or [Cloud Shell](/azure/cloud-shell/overview), create a new [Web App on Linux](/azure/app-service/containers/app-service-linux-intro).</span></span> <span data-ttu-id="53d5c-153">The web app name in this tutorial is `myJavaApp`, but you need to use a unique name for your own app.</span><span class="sxs-lookup"><span data-stu-id="53d5c-153">The web app name in this tutorial is `myJavaApp`, but you need to use a unique name for your own app.</span></span>
   
    ```azurecli-interactive
    az group create --name myResourceGroupJenkins --location westus
    az appservice plan create --is-linux --name myLinuxAppServicePlan --resource-group myResourceGroupJenkins 
    az webapp create --name myJavaApp --resource-group myResourceGroupJenkins --plan myLinuxAppServicePlan --runtime "java|1.8|Tomcat|8.5"
    ```

2. <span data-ttu-id="53d5c-154">Create an [Azure Container Registry](/azure/container-registry/container-registry-intro) to store the Docker images built by Jenkins.</span><span class="sxs-lookup"><span data-stu-id="53d5c-154">Create an [Azure Container Registry](/azure/container-registry/container-registry-intro) to store the Docker images built by Jenkins.</span></span> <span data-ttu-id="53d5c-155">The container registry name used in this tutorial is `jenkinsregistry`, but you need to use a unique name for your own container registry.</span><span class="sxs-lookup"><span data-stu-id="53d5c-155">The container registry name used in this tutorial is `jenkinsregistry`, but you need to use a unique name for your own container registry.</span></span> 

    ```azurecli-interactive
    az acr create --name jenkinsregistry --resource-group myResourceGroupJenkins --sku Basic --admin-enabled
    ```
3. <span data-ttu-id="53d5c-156">Configure the web app to run Docker images pushed to the container registry and specify that the app running in the container listens for requests on port 8080.</span><span class="sxs-lookup"><span data-stu-id="53d5c-156">Configure the web app to run Docker images pushed to the container registry and specify that the app running in the container listens for requests on port 8080.</span></span>   

    ```azurecli-interactive
    az webapp config container set -c jenkinsregistry/webapp --resource-group myResourceGroupJenkins --name myJavaApp
    az webapp config appsettings set --resource-group myResourceGroupJenkins --name myJavaApp --settings PORT=8080
    ```

## <a name="configure-the-azure-app-service-jenkins-plug-in"></a><span data-ttu-id="53d5c-157">Configure the Azure App Service Jenkins plug-in</span><span class="sxs-lookup"><span data-stu-id="53d5c-157">Configure the Azure App Service Jenkins plug-in</span></span>

1. <span data-ttu-id="53d5c-158">In the Jenkins web console, select the **MyJavaApp** job you created and then select **Configure** on the left hand of the page.</span><span class="sxs-lookup"><span data-stu-id="53d5c-158">In the Jenkins web console, select the **MyJavaApp** job you created and then select **Configure** on the left hand of the page.</span></span>
2. <span data-ttu-id="53d5c-159">Scroll down to **Post-build Actions**, select **Add post-build action**, and choose **Publish an Azure Web App**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-159">Scroll down to **Post-build Actions**, select **Add post-build action**, and choose **Publish an Azure Web App**.</span></span>
3. <span data-ttu-id="53d5c-160">Under **Azure Profile Configuration**, select **Add** next to **Azure Credentials** and choose **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-160">Under **Azure Profile Configuration**, select **Add** next to **Azure Credentials** and choose **Jenkins**.</span></span>
4. <span data-ttu-id="53d5c-161">In the **Add Credentials** dialog, select **Microsoft Azure Service Principal** from the **Kind** drop-down.</span><span class="sxs-lookup"><span data-stu-id="53d5c-161">In the **Add Credentials** dialog, select **Microsoft Azure Service Principal** from the **Kind** drop-down.</span></span>
5. <span data-ttu-id="53d5c-162">Create an Active Directory Service principal from the Azure CLI or [Cloud Shell](/azure/cloud-shell/overview).</span><span class="sxs-lookup"><span data-stu-id="53d5c-162">Create an Active Directory Service principal from the Azure CLI or [Cloud Shell](/azure/cloud-shell/overview).</span></span>
    
    ```azurecli-interactive
    az ad sp create-for-rbac --name jenkins_sp --password secure_password
    ```

    ```json
    {
        "appId": "BBBBBBBB-BBBB-BBBB-BBBB-BBBBBBBBBBB",
        "displayName": "jenkins_sp",
        "name": "http://jenkins_sp",
        "password": "secure_password",
        "tenant": "CCCCCCCC-CCCC-CCCC-CCCCCCCCCCC"
    }
    ```
6. <span data-ttu-id="53d5c-163">Enter the credentials from the service principal into the **Add credentials** dialog.</span><span class="sxs-lookup"><span data-stu-id="53d5c-163">Enter the credentials from the service principal into the **Add credentials** dialog.</span></span> <span data-ttu-id="53d5c-164">If you don't know your Azure subscription ID, you can query it from the CLI:</span><span class="sxs-lookup"><span data-stu-id="53d5c-164">If you don't know your Azure subscription ID, you can query it from the CLI:</span></span>
     
     ```azurecli-interactive
     az account list
     ```

     ```json
        {
            "cloudName": "AzureCloud",
            "id": "AAAAAAAA-AAAA-AAAA-AAAA-AAAAAAAAAAAA",
            "isDefault": true,
            "name": "Visual Studio Enterprise",
            "state": "Enabled",
            "tenantId": "CCCCCCCC-CCCC-CCCC-CCCC-CCCCCCCCCCC",
            "user": {
            "name": "raisa@fabrikam.com",
            "type": "user"
            }
     ```

    ![Configure Azure Service Principal](media/jenkins-java-quickstart/azure_service_principal.png)
6. <span data-ttu-id="53d5c-166">Verify the service principal authenticates with Azure by selecting **Verify Service Principal**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-166">Verify the service principal authenticates with Azure by selecting **Verify Service Principal**.</span></span> 
7. <span data-ttu-id="53d5c-167">Select **Add** to save the credentials.</span><span class="sxs-lookup"><span data-stu-id="53d5c-167">Select **Add** to save the credentials.</span></span>
8. <span data-ttu-id="53d5c-168">Select the service principal credential you just added from the **Azure Credentials** drop-down when you are back to the **Publish an Azure Web App** configuration.</span><span class="sxs-lookup"><span data-stu-id="53d5c-168">Select the service principal credential you just added from the **Azure Credentials** drop-down when you are back to the **Publish an Azure Web App** configuration.</span></span>
9. <span data-ttu-id="53d5c-169">In **App Configuration**, choose your resource group and web app name from the drop-down.</span><span class="sxs-lookup"><span data-stu-id="53d5c-169">In **App Configuration**, choose your resource group and web app name from the drop-down.</span></span>
10. <span data-ttu-id="53d5c-170">Select the **Publish via Docker** radio button.</span><span class="sxs-lookup"><span data-stu-id="53d5c-170">Select the **Publish via Docker** radio button.</span></span>
11. <span data-ttu-id="53d5c-171">Enter `complete/Dockerfile` for **Dockerfile path**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-171">Enter `complete/Dockerfile` for **Dockerfile path**.</span></span>
12. <span data-ttu-id="53d5c-172">Enter `https://jenkinsregistry.azurecr.io` in the **Docker registry URL** field.</span><span class="sxs-lookup"><span data-stu-id="53d5c-172">Enter `https://jenkinsregistry.azurecr.io` in the **Docker registry URL** field.</span></span>
13. <span data-ttu-id="53d5c-173">Select **Add** next to **Registry Credentials**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-173">Select **Add** next to **Registry Credentials**.</span></span> 
14. <span data-ttu-id="53d5c-174">Enter the admin username for the Azure Container Registry you created for the **Username**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-174">Enter the admin username for the Azure Container Registry you created for the **Username**.</span></span>
15. <span data-ttu-id="53d5c-175">Enter the password for the Azure Container registry in the **Password** field.</span><span class="sxs-lookup"><span data-stu-id="53d5c-175">Enter the password for the Azure Container registry in the **Password** field.</span></span> <span data-ttu-id="53d5c-176">You can get your username and password from the Azure portal or through the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="53d5c-176">You can get your username and password from the Azure portal or through the following CLI command:</span></span>

    ```azurecli-interactive
    az acr credential show -n jenkinsregistry
    ```
    ![Add your container registry credentials](media/jenkins-java-quickstart/enter_acr_credentials.png)
15. <span data-ttu-id="53d5c-178">Select **Add** to save the credential.</span><span class="sxs-lookup"><span data-stu-id="53d5c-178">Select **Add** to save the credential.</span></span>
16. <span data-ttu-id="53d5c-179">Select the newly created credential from the **Registry credentials** drop-down in the **App Configuration** panel for the **Publish an Azure Web App**.</span><span class="sxs-lookup"><span data-stu-id="53d5c-179">Select the newly created credential from the **Registry credentials** drop-down in the **App Configuration** panel for the **Publish an Azure Web App**.</span></span> <span data-ttu-id="53d5c-180">The finished post-build action should look like the following image:</span><span class="sxs-lookup"><span data-stu-id="53d5c-180">The finished post-build action should look like the following image:</span></span>   
    <span data-ttu-id="53d5c-181">![Post build action configuration for Azure App Service Deploy](media/jenkins-java-quickstart/appservice_plugin_configuration.png)</span><span class="sxs-lookup"><span data-stu-id="53d5c-181">![Post build action configuration for Azure App Service Deploy](media/jenkins-java-quickstart/appservice_plugin_configuration.png)</span></span>
17. <span data-ttu-id="53d5c-182">Select **Save** to save the job configuration.</span><span class="sxs-lookup"><span data-stu-id="53d5c-182">Select **Save** to save the job configuration.</span></span>

## <a name="deploy-the-app-from-github"></a><span data-ttu-id="53d5c-183">Deploy the app from GitHub</span><span class="sxs-lookup"><span data-stu-id="53d5c-183">Deploy the app from GitHub</span></span>

1. <span data-ttu-id="53d5c-184">From the Jenkins project, select **Build Now** to deploy the sample app to Azure.</span><span class="sxs-lookup"><span data-stu-id="53d5c-184">From the Jenkins project, select **Build Now** to deploy the sample app to Azure.</span></span>
2. <span data-ttu-id="53d5c-185">Once the build completes, your app is live on Azure at its publishing URL, for example http://myjavaapp.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="53d5c-185">Once the build completes, your app is live on Azure at its publishing URL, for example http://myjavaapp.azurewebsites.net.</span></span>   
   ![View your deployed app on Azure](media/jenkins-java-quickstart/hello_docker_world_unedited.png)

## <a name="push-changes-and-redeploy"></a><span data-ttu-id="53d5c-187">Push changes and redeploy</span><span class="sxs-lookup"><span data-stu-id="53d5c-187">Push changes and redeploy</span></span>

1. <span data-ttu-id="53d5c-188">From your Github fork, browse on the web to  `complete/src/main/java/Hello/Application.java`.</span><span class="sxs-lookup"><span data-stu-id="53d5c-188">From your Github fork, browse on the web to  `complete/src/main/java/Hello/Application.java`.</span></span> <span data-ttu-id="53d5c-189">Select the **Edit this file** link from the right-hand side of the GitHub interface.</span><span class="sxs-lookup"><span data-stu-id="53d5c-189">Select the **Edit this file** link from the right-hand side of the GitHub interface.</span></span>
2. <span data-ttu-id="53d5c-190">Make the following change to the `home()` method and commit the change to the repo's master branch.</span><span class="sxs-lookup"><span data-stu-id="53d5c-190">Make the following change to the `home()` method and commit the change to the repo's master branch.</span></span>
   
    ```java
    return "Hello Docker World on Azure";
    ```
3. <span data-ttu-id="53d5c-191">A new build starts in Jenkins, triggered by the new commit on the `master` branch of the repo.</span><span class="sxs-lookup"><span data-stu-id="53d5c-191">A new build starts in Jenkins, triggered by the new commit on the `master` branch of the repo.</span></span> <span data-ttu-id="53d5c-192">Once it completes, reload your app on Azure.</span><span class="sxs-lookup"><span data-stu-id="53d5c-192">Once it completes, reload your app on Azure.</span></span>     
      <span data-ttu-id="53d5c-193">![View your deployed app on Azure](media/jenkins-java-quickstart/hello_docker_world.png)</span><span class="sxs-lookup"><span data-stu-id="53d5c-193">![View your deployed app on Azure](media/jenkins-java-quickstart/hello_docker_world.png)</span></span>

## <a name="troubleshooting-the-jenkins-plugin"></a><span data-ttu-id="53d5c-194">Troubleshooting the Jenkins plugin</span><span class="sxs-lookup"><span data-stu-id="53d5c-194">Troubleshooting the Jenkins plugin</span></span>

<span data-ttu-id="53d5c-195">If you encounter any bugs with the Jenkins plugins, file an issue in the [Jenkins JIRA](https://issues.jenkins-ci.org/) for the specific component.</span><span class="sxs-lookup"><span data-stu-id="53d5c-195">If you encounter any bugs with the Jenkins plugins, file an issue in the [Jenkins JIRA](https://issues.jenkins-ci.org/) for the specific component.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53d5c-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="53d5c-196">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="53d5c-197">Use Azure VMs as build agents</span><span class="sxs-lookup"><span data-stu-id="53d5c-197">Use Azure VMs as build agents</span></span>](/azure/jenkins/jenkins-azure-vm-agents)