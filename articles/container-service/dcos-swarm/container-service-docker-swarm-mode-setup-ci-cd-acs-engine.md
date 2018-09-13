---
title: CI/CD with Azure Container Service Engine and Swarm Mode
description: Use Azure Container Service Engine with Docker Swarm Mode, an Azure Container Registry, and Azure DevOps to deliver continuously a multi-container .NET Core application
services: container-service
author: diegomrtnzg
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 296c097ee3302eaa39210274b16c6352866eac8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965688"
---
# <a name="full-cicd-pipeline-to-deploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-azure-devops"></a><span data-ttu-id="09263-103">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="09263-103">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Azure DevOps</span></span>

<span data-ttu-id="09263-104">*This article is based on [Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Azure DevOps](container-service-docker-swarm-setup-ci-cd.md) documentation*</span><span class="sxs-lookup"><span data-stu-id="09263-104">*This article is based on [Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Azure DevOps](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="09263-105">Nowadays, One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span><span class="sxs-lookup"><span data-stu-id="09263-105">Nowadays, One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span></span> <span data-ttu-id="09263-106">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using:</span><span class="sxs-lookup"><span data-stu-id="09263-106">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="09263-107">Azure Container Service Engine with Docker Swarm Mode</span><span class="sxs-lookup"><span data-stu-id="09263-107">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="09263-108">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="09263-108">Azure Container Registry</span></span>
* <span data-ttu-id="09263-109">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="09263-109">Azure DevOps</span></span>

<span data-ttu-id="09263-110">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="09263-110">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="09263-111">The application is composed of four different services: three web APIs and one web front end:</span><span class="sxs-lookup"><span data-stu-id="09263-111">The application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop sample application](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="09263-113">The objective is to deliver this application continuously in a Docker Swarm Mode cluster, using Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="09263-113">The objective is to deliver this application continuously in a Docker Swarm Mode cluster, using Azure DevOps.</span></span> <span data-ttu-id="09263-114">The following figure details this continuous delivery pipeline:</span><span class="sxs-lookup"><span data-stu-id="09263-114">The following figure details this continuous delivery pipeline:</span></span>

![MyShop sample application](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="09263-116">Here is a brief explanation of the steps:</span><span class="sxs-lookup"><span data-stu-id="09263-116">Here is a brief explanation of the steps:</span></span>

1. <span data-ttu-id="09263-117">Code changes are committed to the source code repository (here, GitHub)</span><span class="sxs-lookup"><span data-stu-id="09263-117">Code changes are committed to the source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="09263-118">GitHub triggers a build in Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="09263-118">GitHub triggers a build in Azure DevOps</span></span> 
3. <span data-ttu-id="09263-119">Azure DevOps gets the latest version of the sources and builds all the images that compose the application</span><span class="sxs-lookup"><span data-stu-id="09263-119">Azure DevOps gets the latest version of the sources and builds all the images that compose the application</span></span> 
4. <span data-ttu-id="09263-120">Azure DevOps pushes each image to a Docker registry created using the Azure Container Registry service</span><span class="sxs-lookup"><span data-stu-id="09263-120">Azure DevOps pushes each image to a Docker registry created using the Azure Container Registry service</span></span> 
5. <span data-ttu-id="09263-121">Azure DevOps triggers a new release</span><span class="sxs-lookup"><span data-stu-id="09263-121">Azure DevOps triggers a new release</span></span> 
6. <span data-ttu-id="09263-122">The release runs some commands using SSH on the Azure container service cluster master node</span><span class="sxs-lookup"><span data-stu-id="09263-122">The release runs some commands using SSH on the Azure container service cluster master node</span></span> 
7. <span data-ttu-id="09263-123">Docker Swarm Mode on the cluster pulls the latest version of the images</span><span class="sxs-lookup"><span data-stu-id="09263-123">Docker Swarm Mode on the cluster pulls the latest version of the images</span></span> 
8. <span data-ttu-id="09263-124">The new version of the application is deployed using Docker Stack</span><span class="sxs-lookup"><span data-stu-id="09263-124">The new version of the application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="09263-125">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="09263-125">Prerequisites</span></span>

<span data-ttu-id="09263-126">Before starting this tutorial, you need to complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="09263-126">Before starting this tutorial, you need to complete the following tasks:</span></span>

- [<span data-ttu-id="09263-127">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span><span class="sxs-lookup"><span data-stu-id="09263-127">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="09263-128">Connect with the Swarm cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="09263-128">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="09263-129">Create an Azure container registry</span><span class="sxs-lookup"><span data-stu-id="09263-129">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="09263-130">Have an Azure DevOps organization and project created</span><span class="sxs-lookup"><span data-stu-id="09263-130">Have an Azure DevOps organization and project created</span></span>](https://docs.microsoft.com/azure/devops/organizations/accounts/create-organization-msa-or-work-student)
- [<span data-ttu-id="09263-131">Fork the GitHub repository to your GitHub account</span><span class="sxs-lookup"><span data-stu-id="09263-131">Fork the GitHub repository to your GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="09263-132">The Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span><span class="sxs-lookup"><span data-stu-id="09263-132">The Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="09263-133">Currently, the integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="09263-133">Currently, the integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="09263-134">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in the [Azure Marketplace](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="09263-134">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in the [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-azure-devops-organization"></a><span data-ttu-id="09263-135">Step 1: Configure your Azure DevOps organization</span><span class="sxs-lookup"><span data-stu-id="09263-135">Step 1: Configure your Azure DevOps organization</span></span> 

<span data-ttu-id="09263-136">In this section, you configure your Azure DevOps organization.</span><span class="sxs-lookup"><span data-stu-id="09263-136">In this section, you configure your Azure DevOps organization.</span></span> <span data-ttu-id="09263-137">To configure Azure DevOps Services Endpoints, in your Azure DevOps project, click the **Settings** icon in the toolbar, and select **Services**.</span><span class="sxs-lookup"><span data-stu-id="09263-137">To configure Azure DevOps Services Endpoints, in your Azure DevOps project, click the **Settings** icon in the toolbar, and select **Services**.</span></span>

![Open Services Endpoint](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-azure-devops-and-azure-account"></a><span data-ttu-id="09263-139">Connect Azure DevOps and Azure account</span><span class="sxs-lookup"><span data-stu-id="09263-139">Connect Azure DevOps and Azure account</span></span>

<span data-ttu-id="09263-140">Set up a connection between your Azure DevOps project and your Azure account.</span><span class="sxs-lookup"><span data-stu-id="09263-140">Set up a connection between your Azure DevOps project and your Azure account.</span></span>

1. <span data-ttu-id="09263-141">On the left, click **New Service Endpoint** > **Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="09263-141">On the left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="09263-142">To authorize Azure DevOps to work with your Azure account, select your **Subscription** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="09263-142">To authorize Azure DevOps to work with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Azure DevOps - Authorize Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-azure-devops-and-github"></a><span data-ttu-id="09263-144">Connect Azure DevOps and GitHub</span><span class="sxs-lookup"><span data-stu-id="09263-144">Connect Azure DevOps and GitHub</span></span>

<span data-ttu-id="09263-145">Set up a connection between your Azure DevOps project and your GitHub account.</span><span class="sxs-lookup"><span data-stu-id="09263-145">Set up a connection between your Azure DevOps project and your GitHub account.</span></span>

1. <span data-ttu-id="09263-146">On the left, click **New Service Endpoint** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="09263-146">On the left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="09263-147">To authorize Azure DevOps to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span><span class="sxs-lookup"><span data-stu-id="09263-147">To authorize Azure DevOps to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span></span>

    ![Azure DevOps - Authorize GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-azure-devops-to-your-azure-container-service-cluster"></a><span data-ttu-id="09263-149">Connect Azure DevOps to your Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="09263-149">Connect Azure DevOps to your Azure Container Service cluster</span></span>

<span data-ttu-id="09263-150">The last steps before getting into the CI/CD pipeline are to configure external connections to your Docker Swarm cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="09263-150">The last steps before getting into the CI/CD pipeline are to configure external connections to your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="09263-151">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span><span class="sxs-lookup"><span data-stu-id="09263-151">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="09263-152">Then enter the SSH connection information of your Swarm cluster (master node).</span><span class="sxs-lookup"><span data-stu-id="09263-152">Then enter the SSH connection information of your Swarm cluster (master node).</span></span>

    ![Azure DevOps - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="09263-154">All the configuration is done now.</span><span class="sxs-lookup"><span data-stu-id="09263-154">All the configuration is done now.</span></span> <span data-ttu-id="09263-155">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="09263-155">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span></span> 

## <a name="step-2-create-the-build-pipeline"></a><span data-ttu-id="09263-156">Step 2: Create the build pipeline</span><span class="sxs-lookup"><span data-stu-id="09263-156">Step 2: Create the build pipeline</span></span>

<span data-ttu-id="09263-157">In this step, you set up a build pipeline for your Azure DevOps project and define the build workflow for your container images</span><span class="sxs-lookup"><span data-stu-id="09263-157">In this step, you set up a build pipeline for your Azure DevOps project and define the build workflow for your container images</span></span>

### <a name="initial-pipeline-setup"></a><span data-ttu-id="09263-158">Initial pipeline setup</span><span class="sxs-lookup"><span data-stu-id="09263-158">Initial pipeline setup</span></span>

1. <span data-ttu-id="09263-159">To create a build pipeline, connect to your Azure DevOps project and click **Build & Release**.</span><span class="sxs-lookup"><span data-stu-id="09263-159">To create a build pipeline, connect to your Azure DevOps project and click **Build & Release**.</span></span> <span data-ttu-id="09263-160">In the **Build definitions** section, click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="09263-160">In the **Build definitions** section, click **+ New**.</span></span> 

    ![Azure DevOps - New Build Pipeline](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="09263-162">Select the **Empty process**.</span><span class="sxs-lookup"><span data-stu-id="09263-162">Select the **Empty process**.</span></span>

    ![Azure DevOps - New Empty Build Pipeline](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="09263-164">Then, click the **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="09263-164">Then, click the **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="09263-165">Paste the values of your Registry and Cluster Agents DNS.</span><span class="sxs-lookup"><span data-stu-id="09263-165">Paste the values of your Registry and Cluster Agents DNS.</span></span>

    ![Azure DevOps - Build Variables Configuration](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="09263-167">On the **Build Definitions** page, open the **Triggers** tab and configure the build to use continuous integration with the fork of the MyShop project that you created in the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="09263-167">On the **Build Definitions** page, open the **Triggers** tab and configure the build to use continuous integration with the fork of the MyShop project that you created in the prerequisites.</span></span> <span data-ttu-id="09263-168">Then, select **Batch changes**.</span><span class="sxs-lookup"><span data-stu-id="09263-168">Then, select **Batch changes**.</span></span> <span data-ttu-id="09263-169">Make sure that you select *docker-linux* as the **Branch specification**.</span><span class="sxs-lookup"><span data-stu-id="09263-169">Make sure that you select *docker-linux* as the **Branch specification**.</span></span>

    ![Azure DevOps - Build Repository Configuration](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="09263-171">Finally, click the **Options** tab and configure the Default agent queue to **Hosted Linux Preview**.</span><span class="sxs-lookup"><span data-stu-id="09263-171">Finally, click the **Options** tab and configure the Default agent queue to **Hosted Linux Preview**.</span></span>

    ![Azure DevOps - Host Agent Configuration](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-the-build-workflow"></a><span data-ttu-id="09263-173">Define the build workflow</span><span class="sxs-lookup"><span data-stu-id="09263-173">Define the build workflow</span></span>
<span data-ttu-id="09263-174">The next steps define the build workflow.</span><span class="sxs-lookup"><span data-stu-id="09263-174">The next steps define the build workflow.</span></span> <span data-ttu-id="09263-175">First, you need to configure the source of the code.</span><span class="sxs-lookup"><span data-stu-id="09263-175">First, you need to configure the source of the code.</span></span> <span data-ttu-id="09263-176">To do it, select **GitHub** and your **repository** and **branch** (docker-linux).</span><span class="sxs-lookup"><span data-stu-id="09263-176">To do it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Azure DevOps - Configure code source](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="09263-178">There are five container images to build for the *MyShop* application.</span><span class="sxs-lookup"><span data-stu-id="09263-178">There are five container images to build for the *MyShop* application.</span></span> <span data-ttu-id="09263-179">Each image is built using the Dockerfile located in the project folders:</span><span class="sxs-lookup"><span data-stu-id="09263-179">Each image is built using the Dockerfile located in the project folders:</span></span>

* <span data-ttu-id="09263-180">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="09263-180">ProductsApi</span></span>
* <span data-ttu-id="09263-181">Proxy</span><span class="sxs-lookup"><span data-stu-id="09263-181">Proxy</span></span>
* <span data-ttu-id="09263-182">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="09263-182">RatingsApi</span></span>
* <span data-ttu-id="09263-183">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="09263-183">RecommandationsApi</span></span>
* <span data-ttu-id="09263-184">ShopFront</span><span class="sxs-lookup"><span data-stu-id="09263-184">ShopFront</span></span>

<span data-ttu-id="09263-185">You need two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="09263-185">You need two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span></span> 

1. <span data-ttu-id="09263-186">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span><span class="sxs-lookup"><span data-stu-id="09263-186">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Azure DevOps - Add Build Steps](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="09263-188">For each image, configure one step that uses the `docker build` command.</span><span class="sxs-lookup"><span data-stu-id="09263-188">For each image, configure one step that uses the `docker build` command.</span></span>

    ![Azure DevOps - Docker Build](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="09263-190">For the build operation, select your Azure Container Registry, the **Build an image** action, and the Dockerfile that defines each image.</span><span class="sxs-lookup"><span data-stu-id="09263-190">For the build operation, select your Azure Container Registry, the **Build an image** action, and the Dockerfile that defines each image.</span></span> <span data-ttu-id="09263-191">Set the **Working Directory** as the Dockerfile root directory, define the **Image Name**, and select **Include Latest Tag**.</span><span class="sxs-lookup"><span data-stu-id="09263-191">Set the **Working Directory** as the Dockerfile root directory, define the **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="09263-192">The Image Name has to be in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="09263-192">The Image Name has to be in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="09263-193">Replace **[NAME]** with the image name:</span><span class="sxs-lookup"><span data-stu-id="09263-193">Replace **[NAME]** with the image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="09263-194">For each image, configure a second step that uses the `docker push` command.</span><span class="sxs-lookup"><span data-stu-id="09263-194">For each image, configure a second step that uses the `docker push` command.</span></span>

    ![Azure DevOps - Docker Push](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="09263-196">For the push operation, select your Azure container registry, the **Push an image** action, enter the **Image Name** that is built in the previous step and select **Include Latest Tag**.</span><span class="sxs-lookup"><span data-stu-id="09263-196">For the push operation, select your Azure container registry, the **Push an image** action, enter the **Image Name** that is built in the previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="09263-197">After you configure the build and push steps for each of the five images, add three more steps in the build workflow.</span><span class="sxs-lookup"><span data-stu-id="09263-197">After you configure the build and push steps for each of the five images, add three more steps in the build workflow.</span></span>

   ![Azure DevOps - Add Command-Line Task](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="09263-199">A command-line task that uses a bash script to replace the *RegistryURL* occurrence in the docker-compose.yml file with the RegistryURL variable.</span><span class="sxs-lookup"><span data-stu-id="09263-199">A command-line task that uses a bash script to replace the *RegistryURL* occurrence in the docker-compose.yml file with the RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Azure DevOps - Update Compose file with Registry URL](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="09263-201">A command-line task that uses a bash script to replace the *AgentURL* occurrence in the docker-compose.yml file with the AgentURL variable.</span><span class="sxs-lookup"><span data-stu-id="09263-201">A command-line task that uses a bash script to replace the *AgentURL* occurrence in the docker-compose.yml file with the AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="09263-202">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span><span class="sxs-lookup"><span data-stu-id="09263-202">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span></span> <span data-ttu-id="09263-203">See the following screen for details.</span><span class="sxs-lookup"><span data-stu-id="09263-203">See the following screen for details.</span></span>

         ![Azure DevOps - Publish Artifact](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Azure DevOps - Publish Compose file](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="09263-206">Click **Save & queue** to test your build pipeline.</span><span class="sxs-lookup"><span data-stu-id="09263-206">Click **Save & queue** to test your build pipeline.</span></span>

   ![Azure DevOps - Save and queue](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Azure DevOps - New Queue](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="09263-209">If the **Build** is correct, you have to see this screen:</span><span class="sxs-lookup"><span data-stu-id="09263-209">If the **Build** is correct, you have to see this screen:</span></span>

  ![Azure DevOps - Build succeeded](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-the-release-pipeline"></a><span data-ttu-id="09263-211">Step 3: Create the release pipeline</span><span class="sxs-lookup"><span data-stu-id="09263-211">Step 3: Create the release pipeline</span></span>

<span data-ttu-id="09263-212">Azure DevOps allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="09263-212">Azure DevOps allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="09263-213">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span><span class="sxs-lookup"><span data-stu-id="09263-213">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="09263-214">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span><span class="sxs-lookup"><span data-stu-id="09263-214">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Azure DevOps - Release to ACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="09263-216">Initial release setup</span><span class="sxs-lookup"><span data-stu-id="09263-216">Initial release setup</span></span>

1. <span data-ttu-id="09263-217">To create a release pipeline, click **Releases** > **+ Release**</span><span class="sxs-lookup"><span data-stu-id="09263-217">To create a release pipeline, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="09263-218">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span><span class="sxs-lookup"><span data-stu-id="09263-218">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="09263-219">Here, link this new release pipeline to the build that you defined in the previous step.</span><span class="sxs-lookup"><span data-stu-id="09263-219">Here, link this new release pipeline to the build that you defined in the previous step.</span></span> <span data-ttu-id="09263-220">After that, the docker-compose.yml file is available in the release process.</span><span class="sxs-lookup"><span data-stu-id="09263-220">After that, the docker-compose.yml file is available in the release process.</span></span>

    ![Azure DevOps - Release Artifacts](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="09263-222">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span><span class="sxs-lookup"><span data-stu-id="09263-222">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="09263-223">Set the trigger on the same artifact source.</span><span class="sxs-lookup"><span data-stu-id="09263-223">Set the trigger on the same artifact source.</span></span> <span data-ttu-id="09263-224">This setting ensures that a new release starts when the build completes successfully.</span><span class="sxs-lookup"><span data-stu-id="09263-224">This setting ensures that a new release starts when the build completes successfully.</span></span>

    ![Azure DevOps - Release Triggers](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="09263-226">To configure the release variables, click **Variables** and select **+Variable** to create three new variables with the info of the registry: **docker.username**, **docker.password**, and **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="09263-226">To configure the release variables, click **Variables** and select **+Variable** to create three new variables with the info of the registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="09263-227">Paste the values of your Registry and Cluster Agents DNS.</span><span class="sxs-lookup"><span data-stu-id="09263-227">Paste the values of your Registry and Cluster Agents DNS.</span></span>

    ![Azure DevOps - Build Repository Configuration](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="09263-229">As shown on the previous screen, click the **Lock** checkbox in docker.password.</span><span class="sxs-lookup"><span data-stu-id="09263-229">As shown on the previous screen, click the **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="09263-230">This setting is important to restrict the password.</span><span class="sxs-lookup"><span data-stu-id="09263-230">This setting is important to restrict the password.</span></span>
    >

### <a name="define-the-release-workflow"></a><span data-ttu-id="09263-231">Define the release workflow</span><span class="sxs-lookup"><span data-stu-id="09263-231">Define the release workflow</span></span>

<span data-ttu-id="09263-232">The release workflow is composed of two tasks that you add.</span><span class="sxs-lookup"><span data-stu-id="09263-232">The release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="09263-233">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span><span class="sxs-lookup"><span data-stu-id="09263-233">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span></span> <span data-ttu-id="09263-234">See the following screen for details.</span><span class="sxs-lookup"><span data-stu-id="09263-234">See the following screen for details.</span></span>
    
    <span data-ttu-id="09263-235">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="09263-235">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Azure DevOps - Release SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="09263-237">Configure a second task to execute a bash command to run `docker` and `docker stack deploy` commands on the master node.</span><span class="sxs-lookup"><span data-stu-id="09263-237">Configure a second task to execute a bash command to run `docker` and `docker stack deploy` commands on the master node.</span></span> <span data-ttu-id="09263-238">See the following screen for details.</span><span class="sxs-lookup"><span data-stu-id="09263-238">See the following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Azure DevOps - Release Bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="09263-240">The command executed on the master uses the Docker CLI and the Docker-Compose CLI to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="09263-240">The command executed on the master uses the Docker CLI and the Docker-Compose CLI to do the following tasks:</span></span>

    - <span data-ttu-id="09263-241">Log in to the Azure container registry (it uses three build variables that are defined in the **Variables** tab)</span><span class="sxs-lookup"><span data-stu-id="09263-241">Log in to the Azure container registry (it uses three build variables that are defined in the **Variables** tab)</span></span>
    - <span data-ttu-id="09263-242">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span><span class="sxs-lookup"><span data-stu-id="09263-242">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="09263-243">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span><span class="sxs-lookup"><span data-stu-id="09263-243">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span></span> 
    - <span data-ttu-id="09263-244">Execute `docker stack deploy` commands that pull the new images and create the containers.</span><span class="sxs-lookup"><span data-stu-id="09263-244">Execute `docker stack deploy` commands that pull the new images and create the containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="09263-245">As shown on the previous screen, leave the **Fail on STDERR** checkbox unchecked.</span><span class="sxs-lookup"><span data-stu-id="09263-245">As shown on the previous screen, leave the **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="09263-246">This setting allows us to complete the release process due to `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span><span class="sxs-lookup"><span data-stu-id="09263-246">This setting allows us to complete the release process due to `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span></span> <span data-ttu-id="09263-247">If you check the checkbox, Azure DevOps reports that errors occurred during the release, even if all goes well.</span><span class="sxs-lookup"><span data-stu-id="09263-247">If you check the checkbox, Azure DevOps reports that errors occurred during the release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="09263-248">Save this new release pipeline.</span><span class="sxs-lookup"><span data-stu-id="09263-248">Save this new release pipeline.</span></span>

## <a name="step-4-test-the-cicd-pipeline"></a><span data-ttu-id="09263-249">Step 4: Test the CI/CD pipeline</span><span class="sxs-lookup"><span data-stu-id="09263-249">Step 4: Test the CI/CD pipeline</span></span>

<span data-ttu-id="09263-250">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span><span class="sxs-lookup"><span data-stu-id="09263-250">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span></span> <span data-ttu-id="09263-251">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="09263-251">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span></span> <span data-ttu-id="09263-252">A few seconds after you push the code, you will see a new build running in Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="09263-252">A few seconds after you push the code, you will see a new build running in Azure DevOps.</span></span> <span data-ttu-id="09263-253">Once completed successfully, a new release is triggered and deployed the new version of the application on the Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="09263-253">Once completed successfully, a new release is triggered and deployed the new version of the application on the Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09263-254">Next steps</span><span class="sxs-lookup"><span data-stu-id="09263-254">Next steps</span></span>

* <span data-ttu-id="09263-255">For more information about CI/CD with Azure DevOps, see the [Azure DevOps Build overview](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="09263-255">For more information about CI/CD with Azure DevOps, see the [Azure DevOps Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="09263-256">For more information about ACS Engine, see the [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="09263-256">For more information about ACS Engine, see the [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="09263-257">For more information about Docker Swarm mode, see the [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span><span class="sxs-lookup"><span data-stu-id="09263-257">For more information about Docker Swarm mode, see the [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
