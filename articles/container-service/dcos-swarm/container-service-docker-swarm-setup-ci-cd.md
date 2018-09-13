---
title: CI/CD with Azure Container Service and Swarm
description: Use Azure Container Service with Docker Swarm, an Azure Container Registry, and Azure DevOps to deliver continuously a multi-container .NET Core application
services: container-service
author: jcorioland
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 3b91c269104e740add1d3a5b8ecaee93ca269188
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869353"
---
# <a name="full-cicd-pipeline-to-deploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-azure-devops-services"></a><span data-ttu-id="50aa9-103">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="50aa9-103">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Azure DevOps Services</span></span>

<span data-ttu-id="50aa9-104">One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span><span class="sxs-lookup"><span data-stu-id="50aa9-104">One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span></span> <span data-ttu-id="50aa9-105">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Azure Pipelines management.</span><span class="sxs-lookup"><span data-stu-id="50aa9-105">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Azure Pipelines management.</span></span>

<span data-ttu-id="50aa9-106">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="50aa9-106">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="50aa9-107">The application is composed of four different services: three web APIs and one web front end:</span><span class="sxs-lookup"><span data-stu-id="50aa9-107">The application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop sample application](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="50aa9-109">The objective is to deliver this application continuously in a Docker Swarm cluster, using Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="50aa9-109">The objective is to deliver this application continuously in a Docker Swarm cluster, using Azure DevOps Services.</span></span> <span data-ttu-id="50aa9-110">The following figure details this continuous delivery pipeline:</span><span class="sxs-lookup"><span data-stu-id="50aa9-110">The following figure details this continuous delivery pipeline:</span></span>

![MyShop sample application](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="50aa9-112">Here is a brief explanation of the steps:</span><span class="sxs-lookup"><span data-stu-id="50aa9-112">Here is a brief explanation of the steps:</span></span>

1. <span data-ttu-id="50aa9-113">Code changes are committed to the source code repository (here, GitHub)</span><span class="sxs-lookup"><span data-stu-id="50aa9-113">Code changes are committed to the source code repository (here, GitHub)</span></span> 
1. <span data-ttu-id="50aa9-114">GitHub triggers a build in Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="50aa9-114">GitHub triggers a build in Azure DevOps Services</span></span> 
1. <span data-ttu-id="50aa9-115">Azure DevOps Services gets the latest version of the sources and builds all the images that compose the application</span><span class="sxs-lookup"><span data-stu-id="50aa9-115">Azure DevOps Services gets the latest version of the sources and builds all the images that compose the application</span></span> 
1. <span data-ttu-id="50aa9-116">Azure DevOps Services pushes each image to a Docker registry created using the Azure Container Registry service</span><span class="sxs-lookup"><span data-stu-id="50aa9-116">Azure DevOps Services pushes each image to a Docker registry created using the Azure Container Registry service</span></span> 
1. <span data-ttu-id="50aa9-117">Azure DevOps Services triggers a new release</span><span class="sxs-lookup"><span data-stu-id="50aa9-117">Azure DevOps Services triggers a new release</span></span> 
1. <span data-ttu-id="50aa9-118">The release runs some commands using SSH on the Azure container service cluster master node</span><span class="sxs-lookup"><span data-stu-id="50aa9-118">The release runs some commands using SSH on the Azure container service cluster master node</span></span> 
1. <span data-ttu-id="50aa9-119">Docker Swarm on the cluster pulls the latest version of the images</span><span class="sxs-lookup"><span data-stu-id="50aa9-119">Docker Swarm on the cluster pulls the latest version of the images</span></span> 
1. <span data-ttu-id="50aa9-120">The new version of the application is deployed using Docker Compose</span><span class="sxs-lookup"><span data-stu-id="50aa9-120">The new version of the application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="50aa9-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="50aa9-121">Prerequisites</span></span>

<span data-ttu-id="50aa9-122">Before starting this tutorial, you need to complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="50aa9-122">Before starting this tutorial, you need to complete the following tasks:</span></span>

- [<span data-ttu-id="50aa9-123">Create a Swarm cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="50aa9-123">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="50aa9-124">Connect with the Swarm cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="50aa9-124">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="50aa9-125">Create an Azure container registry</span><span class="sxs-lookup"><span data-stu-id="50aa9-125">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="50aa9-126">Have an Azure DevOps Services organization and project created</span><span class="sxs-lookup"><span data-stu-id="50aa9-126">Have an Azure DevOps Services organization and project created</span></span>](https://docs.microsoft.com/azure/devops/organizations/accounts/create-organization-msa-or-work-student)
- [<span data-ttu-id="50aa9-127">Fork the GitHub repository to your GitHub account</span><span class="sxs-lookup"><span data-stu-id="50aa9-127">Fork the GitHub repository to your GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="50aa9-128">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span><span class="sxs-lookup"><span data-stu-id="50aa9-128">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="50aa9-129">This machine is used by Azure DevOps Services during the Azure Pipelines processes.</span><span class="sxs-lookup"><span data-stu-id="50aa9-129">This machine is used by Azure DevOps Services during the Azure Pipelines processes.</span></span> <span data-ttu-id="50aa9-130">One way to create this machine is to use the image available in the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="50aa9-130">One way to create this machine is to use the image available in the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-azure-devops-services-organization"></a><span data-ttu-id="50aa9-131">Step 1: Configure your Azure DevOps Services organization</span><span class="sxs-lookup"><span data-stu-id="50aa9-131">Step 1: Configure your Azure DevOps Services organization</span></span> 

<span data-ttu-id="50aa9-132">In this section, you configure your Azure DevOps Services organization.</span><span class="sxs-lookup"><span data-stu-id="50aa9-132">In this section, you configure your Azure DevOps Services organization.</span></span>

### <a name="configure-an-azure-devops-services-linux-build-agent"></a><span data-ttu-id="50aa9-133">Configure an Azure DevOps Services Linux build agent</span><span class="sxs-lookup"><span data-stu-id="50aa9-133">Configure an Azure DevOps Services Linux build agent</span></span>

<span data-ttu-id="50aa9-134">To create Docker images and push these images into an Azure container registry from an Azure DevOps Services build, you need to register a Linux agent.</span><span class="sxs-lookup"><span data-stu-id="50aa9-134">To create Docker images and push these images into an Azure container registry from an Azure DevOps Services build, you need to register a Linux agent.</span></span> <span data-ttu-id="50aa9-135">You have these installation options:</span><span class="sxs-lookup"><span data-stu-id="50aa9-135">You have these installation options:</span></span>

* [<span data-ttu-id="50aa9-136">Deploy an agent on Linux</span><span class="sxs-lookup"><span data-stu-id="50aa9-136">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="50aa9-137">Use Docker to run the Azure DevOps Services agent</span><span class="sxs-lookup"><span data-stu-id="50aa9-137">Use Docker to run the Azure DevOps Services agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-the-docker-integration-azure-devops-services-extension"></a><span data-ttu-id="50aa9-138">Install the Docker Integration Azure DevOps Services extension</span><span class="sxs-lookup"><span data-stu-id="50aa9-138">Install the Docker Integration Azure DevOps Services extension</span></span>

<span data-ttu-id="50aa9-139">Microsoft provides an Azure DevOps Services extension to work with Docker in Azure Pipelines processes.</span><span class="sxs-lookup"><span data-stu-id="50aa9-139">Microsoft provides an Azure DevOps Services extension to work with Docker in Azure Pipelines processes.</span></span> <span data-ttu-id="50aa9-140">This extension is available in the [Azure DevOps Services Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="50aa9-140">This extension is available in the [Azure DevOps Services Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="50aa9-141">Click **Install** to add this extension to your Azure DevOps Services organization:</span><span class="sxs-lookup"><span data-stu-id="50aa9-141">Click **Install** to add this extension to your Azure DevOps Services organization:</span></span>

![Install the Docker Integration](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="50aa9-143">You are asked to connect to your Azure DevOps Services organization using your credentials.</span><span class="sxs-lookup"><span data-stu-id="50aa9-143">You are asked to connect to your Azure DevOps Services organization using your credentials.</span></span> 

### <a name="connect-azure-devops-services-and-github"></a><span data-ttu-id="50aa9-144">Connect Azure DevOps Services and GitHub</span><span class="sxs-lookup"><span data-stu-id="50aa9-144">Connect Azure DevOps Services and GitHub</span></span>

<span data-ttu-id="50aa9-145">Set up a connection between your Azure DevOps Services project and your GitHub account.</span><span class="sxs-lookup"><span data-stu-id="50aa9-145">Set up a connection between your Azure DevOps Services project and your GitHub account.</span></span>

1. <span data-ttu-id="50aa9-146">In your Azure DevOps Services project, click the **Settings** icon in the toolbar, and select **Services**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-146">In your Azure DevOps Services project, click the **Settings** icon in the toolbar, and select **Services**.</span></span>

    ![Azure DevOps Services - External Connection](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

1. <span data-ttu-id="50aa9-148">On the left, click **New Service Endpoint** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-148">On the left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Azure DevOps Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

1. <span data-ttu-id="50aa9-150">To authorize Azure DevOps Services to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span><span class="sxs-lookup"><span data-stu-id="50aa9-150">To authorize Azure DevOps Services to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span></span>

    ![Azure DevOps Services - Authorize GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-azure-devops-services-to-your-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="50aa9-152">Connect Azure DevOps Services to your Azure container registry and Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="50aa9-152">Connect Azure DevOps Services to your Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="50aa9-153">The last steps before getting into the CI/CD pipeline are to configure external connections to your container registry and your Docker Swarm cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="50aa9-153">The last steps before getting into the CI/CD pipeline are to configure external connections to your container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="50aa9-154">In the **Services** settings of your Azure DevOps Services project, add a service endpoint of type **Docker Registry**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-154">In the **Services** settings of your Azure DevOps Services project, add a service endpoint of type **Docker Registry**.</span></span> 

1. <span data-ttu-id="50aa9-155">In the popup that opens, enter the URL and the credentials of your Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="50aa9-155">In the popup that opens, enter the URL and the credentials of your Azure container registry.</span></span>

    ![Azure DevOps Services - Docker Registry](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

1. <span data-ttu-id="50aa9-157">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-157">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="50aa9-158">Then enter the SSH connection information of your Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="50aa9-158">Then enter the SSH connection information of your Swarm cluster.</span></span>

    ![Azure DevOps Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="50aa9-160">All the configuration is done now.</span><span class="sxs-lookup"><span data-stu-id="50aa9-160">All the configuration is done now.</span></span> <span data-ttu-id="50aa9-161">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="50aa9-161">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span></span> 

## <a name="step-2-create-the-build-pipeline"></a><span data-ttu-id="50aa9-162">Step 2: Create the build pipeline</span><span class="sxs-lookup"><span data-stu-id="50aa9-162">Step 2: Create the build pipeline</span></span>

<span data-ttu-id="50aa9-163">In this step, you set up a build pipeline for your Azure DevOps Services project and define the build workflow for your container images</span><span class="sxs-lookup"><span data-stu-id="50aa9-163">In this step, you set up a build pipeline for your Azure DevOps Services project and define the build workflow for your container images</span></span>

### <a name="initial-pipeline-setup"></a><span data-ttu-id="50aa9-164">Initial pipeline setup</span><span class="sxs-lookup"><span data-stu-id="50aa9-164">Initial pipeline setup</span></span>

1. <span data-ttu-id="50aa9-165">To create a build pipeline, connect to your Azure DevOps Services project and click **Build & Release**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-165">To create a build pipeline, connect to your Azure DevOps Services project and click **Build & Release**.</span></span> 

1. <span data-ttu-id="50aa9-166">In the **Build definitions** section, click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-166">In the **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="50aa9-167">Select the **Empty** template.</span><span class="sxs-lookup"><span data-stu-id="50aa9-167">Select the **Empty** template.</span></span>

    ![Azure DevOps - New Build Pipeline](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

1. <span data-ttu-id="50aa9-169">Configure the new build with a GitHub repository source, check **Continuous integration**, and select the agent queue where you registered your Linux agent.</span><span class="sxs-lookup"><span data-stu-id="50aa9-169">Configure the new build with a GitHub repository source, check **Continuous integration**, and select the agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="50aa9-170">Click **Create** to create the build pipeline.</span><span class="sxs-lookup"><span data-stu-id="50aa9-170">Click **Create** to create the build pipeline.</span></span>

    ![Azure DevOps Services - Create Build Pipeline](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

1. <span data-ttu-id="50aa9-172">On the **Build Definitions** page, first open the **Repository** tab and configure the build to use the fork of the MyShop project that you created in the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="50aa9-172">On the **Build Definitions** page, first open the **Repository** tab and configure the build to use the fork of the MyShop project that you created in the prerequisites.</span></span> <span data-ttu-id="50aa9-173">Make sure that you select *acs-docs* as the **Default branch**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-173">Make sure that you select *acs-docs* as the **Default branch**.</span></span>

    ![Azure DevOps Services - Build Repository Configuration](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

1. <span data-ttu-id="50aa9-175">On the **Triggers** tab, configure the build to be triggered after each commit.</span><span class="sxs-lookup"><span data-stu-id="50aa9-175">On the **Triggers** tab, configure the build to be triggered after each commit.</span></span> <span data-ttu-id="50aa9-176">Select **Continuous integration** and **Batch changes**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-176">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Azure DevOps Services - Build Trigger Configuration](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-the-build-workflow"></a><span data-ttu-id="50aa9-178">Define the build workflow</span><span class="sxs-lookup"><span data-stu-id="50aa9-178">Define the build workflow</span></span>
<span data-ttu-id="50aa9-179">The next steps define the build workflow.</span><span class="sxs-lookup"><span data-stu-id="50aa9-179">The next steps define the build workflow.</span></span> <span data-ttu-id="50aa9-180">There are five container images to build for the *MyShop* application.</span><span class="sxs-lookup"><span data-stu-id="50aa9-180">There are five container images to build for the *MyShop* application.</span></span> <span data-ttu-id="50aa9-181">Each image is built using the Dockerfile located in the project folders:</span><span class="sxs-lookup"><span data-stu-id="50aa9-181">Each image is built using the Dockerfile located in the project folders:</span></span>

* <span data-ttu-id="50aa9-182">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="50aa9-182">ProductsApi</span></span>
* <span data-ttu-id="50aa9-183">Proxy</span><span class="sxs-lookup"><span data-stu-id="50aa9-183">Proxy</span></span>
* <span data-ttu-id="50aa9-184">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="50aa9-184">RatingsApi</span></span>
* <span data-ttu-id="50aa9-185">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="50aa9-185">RecommandationsApi</span></span>
* <span data-ttu-id="50aa9-186">ShopFront</span><span class="sxs-lookup"><span data-stu-id="50aa9-186">ShopFront</span></span>

<span data-ttu-id="50aa9-187">You need to add two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="50aa9-187">You need to add two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span></span> 

1. <span data-ttu-id="50aa9-188">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-188">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Azure DevOps Services - Add Build Steps](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

1. <span data-ttu-id="50aa9-190">For each image, configure one step that uses the `docker build` command.</span><span class="sxs-lookup"><span data-stu-id="50aa9-190">For each image, configure one step that uses the `docker build` command.</span></span>

    ![Azure DevOps Services - Docker Build](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="50aa9-192">For the build operation, select your Azure container registry, the **Build an image** action, and the Dockerfile that defines each image.</span><span class="sxs-lookup"><span data-stu-id="50aa9-192">For the build operation, select your Azure container registry, the **Build an image** action, and the Dockerfile that defines each image.</span></span> <span data-ttu-id="50aa9-193">Set the **Build context** as the Dockerfile root directory, and define the **Image Name**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-193">Set the **Build context** as the Dockerfile root directory, and define the **Image Name**.</span></span> 
    
    <span data-ttu-id="50aa9-194">As shown on the preceding screen, start the image name with the URI of your Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="50aa9-194">As shown on the preceding screen, start the image name with the URI of your Azure container registry.</span></span> <span data-ttu-id="50aa9-195">(You can also use a build variable to parameterize the tag of the image, such as the build identifier in this example.)</span><span class="sxs-lookup"><span data-stu-id="50aa9-195">(You can also use a build variable to parameterize the tag of the image, such as the build identifier in this example.)</span></span>

1. <span data-ttu-id="50aa9-196">For each image, configure a second step that uses the `docker push` command.</span><span class="sxs-lookup"><span data-stu-id="50aa9-196">For each image, configure a second step that uses the `docker push` command.</span></span>

    ![Azure DevOps Services - Docker Push](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="50aa9-198">For the push operation, select your Azure container registry, the **Push an image** action, and enter the **Image Name** that is built in the previous step.</span><span class="sxs-lookup"><span data-stu-id="50aa9-198">For the push operation, select your Azure container registry, the **Push an image** action, and enter the **Image Name** that is built in the previous step.</span></span>

1. <span data-ttu-id="50aa9-199">After you configure the build and push steps for each of the five images, add two more steps in the build workflow.</span><span class="sxs-lookup"><span data-stu-id="50aa9-199">After you configure the build and push steps for each of the five images, add two more steps in the build workflow.</span></span>

    <span data-ttu-id="50aa9-200">a.</span><span class="sxs-lookup"><span data-stu-id="50aa9-200">a.</span></span> <span data-ttu-id="50aa9-201">A command-line task that uses a bash script to replace the *BuildNumber* occurrence in the docker-compose.yml file with the current build Id. See the following screen for details.</span><span class="sxs-lookup"><span data-stu-id="50aa9-201">A command-line task that uses a bash script to replace the *BuildNumber* occurrence in the docker-compose.yml file with the current build Id. See the following screen for details.</span></span>

    ![Azure DevOps Services - Update Compose file](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="50aa9-203">b.</span><span class="sxs-lookup"><span data-stu-id="50aa9-203">b.</span></span> <span data-ttu-id="50aa9-204">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span><span class="sxs-lookup"><span data-stu-id="50aa9-204">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span></span> <span data-ttu-id="50aa9-205">See the following screen for details.</span><span class="sxs-lookup"><span data-stu-id="50aa9-205">See the following screen for details.</span></span>

    ![Azure DevOps Services - Publish Compose file](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

1. <span data-ttu-id="50aa9-207">Click **Save** and name your build pipeline.</span><span class="sxs-lookup"><span data-stu-id="50aa9-207">Click **Save** and name your build pipeline.</span></span>

## <a name="step-3-create-the-release-pipeline"></a><span data-ttu-id="50aa9-208">Step 3: Create the release pipeline</span><span class="sxs-lookup"><span data-stu-id="50aa9-208">Step 3: Create the release pipeline</span></span>

<span data-ttu-id="50aa9-209">Azure DevOps Services allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="50aa9-209">Azure DevOps Services allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="50aa9-210">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span><span class="sxs-lookup"><span data-stu-id="50aa9-210">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="50aa9-211">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="50aa9-211">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Azure DevOps Services - Release to ACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="50aa9-213">Initial release setup</span><span class="sxs-lookup"><span data-stu-id="50aa9-213">Initial release setup</span></span>

1. <span data-ttu-id="50aa9-214">To create a release pipeline, click **Releases** > **+ Release**</span><span class="sxs-lookup"><span data-stu-id="50aa9-214">To create a release pipeline, click **Releases** > **+ Release**</span></span>

1. <span data-ttu-id="50aa9-215">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-215">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="50aa9-216">Here, link this new release pipeline to the build that you defined in the previous step.</span><span class="sxs-lookup"><span data-stu-id="50aa9-216">Here, link this new release pipeline to the build that you defined in the previous step.</span></span> <span data-ttu-id="50aa9-217">By doing this, the docker-compose.yml file is available in the release process.</span><span class="sxs-lookup"><span data-stu-id="50aa9-217">By doing this, the docker-compose.yml file is available in the release process.</span></span>

    ![Azure DevOps Services - Release Artifacts](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

1. <span data-ttu-id="50aa9-219">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span><span class="sxs-lookup"><span data-stu-id="50aa9-219">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="50aa9-220">Set the trigger on the same artifact source.</span><span class="sxs-lookup"><span data-stu-id="50aa9-220">Set the trigger on the same artifact source.</span></span> <span data-ttu-id="50aa9-221">This setting ensures that a new release starts as soon as the build completes successfully.</span><span class="sxs-lookup"><span data-stu-id="50aa9-221">This setting ensures that a new release starts as soon as the build completes successfully.</span></span>

    ![Azure DevOps Services - Release Triggers](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-the-release-workflow"></a><span data-ttu-id="50aa9-223">Define the release workflow</span><span class="sxs-lookup"><span data-stu-id="50aa9-223">Define the release workflow</span></span>

<span data-ttu-id="50aa9-224">The release workflow is composed of two tasks that you add.</span><span class="sxs-lookup"><span data-stu-id="50aa9-224">The release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="50aa9-225">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span><span class="sxs-lookup"><span data-stu-id="50aa9-225">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span></span> <span data-ttu-id="50aa9-226">See the following screen for details.</span><span class="sxs-lookup"><span data-stu-id="50aa9-226">See the following screen for details.</span></span>

    ![Azure DevOps Services - Release SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

1. <span data-ttu-id="50aa9-228">Configure a second task to execute a bash command to run `docker` and `docker-compose` commands on the master node.</span><span class="sxs-lookup"><span data-stu-id="50aa9-228">Configure a second task to execute a bash command to run `docker` and `docker-compose` commands on the master node.</span></span> <span data-ttu-id="50aa9-229">See the following screen for details.</span><span class="sxs-lookup"><span data-stu-id="50aa9-229">See the following screen for details.</span></span>

    ![Azure DevOps Services - Release Bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="50aa9-231">The command executed on the master use the Docker CLI and the Docker-Compose CLI to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="50aa9-231">The command executed on the master use the Docker CLI and the Docker-Compose CLI to do the following tasks:</span></span>

    - <span data-ttu-id="50aa9-232">Login to the Azure container registry (it uses three build variab\`les that are defined in the **Variables** tab)</span><span class="sxs-lookup"><span data-stu-id="50aa9-232">Login to the Azure container registry (it uses three build variab\`les that are defined in the **Variables** tab)</span></span>
    - <span data-ttu-id="50aa9-233">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span><span class="sxs-lookup"><span data-stu-id="50aa9-233">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="50aa9-234">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span><span class="sxs-lookup"><span data-stu-id="50aa9-234">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span></span> 
    - <span data-ttu-id="50aa9-235">Execute `docker-compose` commands that pull the new images, stop the services, remove the services, and create the containers.</span><span class="sxs-lookup"><span data-stu-id="50aa9-235">Execute `docker-compose` commands that pull the new images, stop the services, remove the services, and create the containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="50aa9-236">As shown on the preceding screen, leave the **Fail on STDERR** checkbox unchecked.</span><span class="sxs-lookup"><span data-stu-id="50aa9-236">As shown on the preceding screen, leave the **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="50aa9-237">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span><span class="sxs-lookup"><span data-stu-id="50aa9-237">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span></span> <span data-ttu-id="50aa9-238">If you check the checkbox, Azure DevOps Services reports that errors occurred during the release, even if all goes well.</span><span class="sxs-lookup"><span data-stu-id="50aa9-238">If you check the checkbox, Azure DevOps Services reports that errors occurred during the release, even if all goes well.</span></span>
    >
1. <span data-ttu-id="50aa9-239">Save this new release pipeline.</span><span class="sxs-lookup"><span data-stu-id="50aa9-239">Save this new release pipeline.</span></span>


>[!NOTE]
><span data-ttu-id="50aa9-240">This deployment includes some downtime because we are stopping the old services and running the new one.</span><span class="sxs-lookup"><span data-stu-id="50aa9-240">This deployment includes some downtime because we are stopping the old services and running the new one.</span></span> <span data-ttu-id="50aa9-241">It is possible to avoid this by doing a blue-green deployment.</span><span class="sxs-lookup"><span data-stu-id="50aa9-241">It is possible to avoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-the-cicd-pipeline"></a><span data-ttu-id="50aa9-242">Step 4.</span><span class="sxs-lookup"><span data-stu-id="50aa9-242">Step 4.</span></span> <span data-ttu-id="50aa9-243">Test the CI/CD pipeline</span><span class="sxs-lookup"><span data-stu-id="50aa9-243">Test the CI/CD pipeline</span></span>

<span data-ttu-id="50aa9-244">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span><span class="sxs-lookup"><span data-stu-id="50aa9-244">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span></span> <span data-ttu-id="50aa9-245">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="50aa9-245">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span></span> <span data-ttu-id="50aa9-246">A few seconds after you push the code, you will see a new build running in Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="50aa9-246">A few seconds after you push the code, you will see a new build running in Azure DevOps Services.</span></span> <span data-ttu-id="50aa9-247">Once completed successfully, a new release will be triggered and will deploy the new version of the application on the Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="50aa9-247">Once completed successfully, a new release will be triggered and will deploy the new version of the application on the Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50aa9-248">Next Steps</span><span class="sxs-lookup"><span data-stu-id="50aa9-248">Next Steps</span></span>

* <span data-ttu-id="50aa9-249">For more information about CI/CD with Azure DevOps Services, see the [Azure DevOps Services Build overview](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="50aa9-249">For more information about CI/CD with Azure DevOps Services, see the [Azure DevOps Services Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
