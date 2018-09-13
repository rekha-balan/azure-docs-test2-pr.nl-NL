---
title: CI/CD with Azure Container Service and Swarm | Microsoft Docs
description: Use Azure Container Service with Docker Swarm, an Azure Container Registry, and Visual Studio Team Services to deliver continuously a multi-container .NET Core application
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Swarm, Azure, Visual Studio Team Services, DevOps
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.openlocfilehash: c416faa2e0eb4309b0746578138ff1f4e8f3f557
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564645"
---
# <a name="full-cicd-pipeline-to-deploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="b4ea3-104">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="b4ea3-104">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="b4ea3-105">One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-105">One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span></span> <span data-ttu-id="b4ea3-106">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-106">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="b4ea3-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="b4ea3-108">The application is composed of four different services: three web APIs and one web front end:</span><span class="sxs-lookup"><span data-stu-id="b4ea3-108">The application is composed of four different services: three web APIs and one web front end:</span></span>

![MyShop sample application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="b4ea3-110">The objective is to deliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-110">The objective is to deliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="b4ea3-111">The following figure details this continuous delivery pipeline:</span><span class="sxs-lookup"><span data-stu-id="b4ea3-111">The following figure details this continuous delivery pipeline:</span></span>

![MyShop sample application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="b4ea3-113">Here is a brief explanation of the steps:</span><span class="sxs-lookup"><span data-stu-id="b4ea3-113">Here is a brief explanation of the steps:</span></span>

1. <span data-ttu-id="b4ea3-114">Code changes are committed to the source code repository (here, GitHub)</span><span class="sxs-lookup"><span data-stu-id="b4ea3-114">Code changes are committed to the source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="b4ea3-115">GitHub triggers a build in Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="b4ea3-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="b4ea3-116">Visual Studio Team Services gets the latest version of the sources and builds all the images that compose the application</span><span class="sxs-lookup"><span data-stu-id="b4ea3-116">Visual Studio Team Services gets the latest version of the sources and builds all the images that compose the application</span></span> 
4. <span data-ttu-id="b4ea3-117">Visual Studio Team Services pushes each image to a Docker registry created using the Azure Container Registry service</span><span class="sxs-lookup"><span data-stu-id="b4ea3-117">Visual Studio Team Services pushes each image to a Docker registry created using the Azure Container Registry service</span></span> 
5. <span data-ttu-id="b4ea3-118">Visual Studio Team Services triggers a new release</span><span class="sxs-lookup"><span data-stu-id="b4ea3-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="b4ea3-119">The release runs some commands using SSH on the Azure container service cluster master node</span><span class="sxs-lookup"><span data-stu-id="b4ea3-119">The release runs some commands using SSH on the Azure container service cluster master node</span></span> 
7. <span data-ttu-id="b4ea3-120">Docker Swarm on the cluster pulls the latest version of the images</span><span class="sxs-lookup"><span data-stu-id="b4ea3-120">Docker Swarm on the cluster pulls the latest version of the images</span></span> 
8. <span data-ttu-id="b4ea3-121">The new version of the application is deployed using Docker Compose</span><span class="sxs-lookup"><span data-stu-id="b4ea3-121">The new version of the application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b4ea3-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b4ea3-122">Prerequisites</span></span>

<span data-ttu-id="b4ea3-123">Before starting this tutorial, you need to complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="b4ea3-123">Before starting this tutorial, you need to complete the following tasks:</span></span>

- [<span data-ttu-id="b4ea3-124">Create a Swarm cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="b4ea3-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="b4ea3-125">Connect with the Swarm cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="b4ea3-125">Connect with the Swarm cluster in Azure Container Service</span></span>](container-service-connect.md)
- [<span data-ttu-id="b4ea3-126">Create an Azure container registry</span><span class="sxs-lookup"><span data-stu-id="b4ea3-126">Create an Azure container registry</span></span>](../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="b4ea3-127">Have a Visual Studio Team Services account and team project created</span><span class="sxs-lookup"><span data-stu-id="b4ea3-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="b4ea3-128">Fork the GitHub repository to your GitHub account</span><span class="sxs-lookup"><span data-stu-id="b4ea3-128">Fork the GitHub repository to your GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

<span data-ttu-id="b4ea3-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="b4ea3-130">This machine is used by Visual Studio Team Services during the build and release processes.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-130">This machine is used by Visual Studio Team Services during the build and release processes.</span></span> <span data-ttu-id="b4ea3-131">One way to create this machine is to use the image available in the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="b4ea3-131">One way to create this machine is to use the image available in the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="b4ea3-132">Step 1: Configure your Visual Studio Team Services account</span><span class="sxs-lookup"><span data-stu-id="b4ea3-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="b4ea3-133">In this section, you configure your Visual Studio Team Services account.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="b4ea3-134">Configure a Visual Studio Team Services Linux build agent</span><span class="sxs-lookup"><span data-stu-id="b4ea3-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="b4ea3-135">To create Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need to register a Linux agent.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-135">To create Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need to register a Linux agent.</span></span> <span data-ttu-id="b4ea3-136">You have these installation options:</span><span class="sxs-lookup"><span data-stu-id="b4ea3-136">You have these installation options:</span></span>

* [<span data-ttu-id="b4ea3-137">Deploy an agent on Linux</span><span class="sxs-lookup"><span data-stu-id="b4ea3-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="b4ea3-138">Use Docker to run the VSTS agent</span><span class="sxs-lookup"><span data-stu-id="b4ea3-138">Use Docker to run the VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-the-docker-integration-vsts-extension"></a><span data-ttu-id="b4ea3-139">Install the Docker Integration VSTS extension</span><span class="sxs-lookup"><span data-stu-id="b4ea3-139">Install the Docker Integration VSTS extension</span></span>

<span data-ttu-id="b4ea3-140">Microsoft provides a VSTS extension to work with Docker in build and release processes.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-140">Microsoft provides a VSTS extension to work with Docker in build and release processes.</span></span> <span data-ttu-id="b4ea3-141">This extension is available in the [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="b4ea3-141">This extension is available in the [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="b4ea3-142">Click **Install** to add this extension to your VSTS account:</span><span class="sxs-lookup"><span data-stu-id="b4ea3-142">Click **Install** to add this extension to your VSTS account:</span></span>

![Install the Docker Integration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="b4ea3-144">You are asked to connect to your VSTS account using your credentials.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-144">You are asked to connect to your VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="b4ea3-145">Connect Visual Studio Team Services and GitHub</span><span class="sxs-lookup"><span data-stu-id="b4ea3-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="b4ea3-146">Set up a connection between your VSTS project and your GitHub account.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="b4ea3-147">In your Visual Studio Team Services project, click the **Settings** icon in the toolbar, and select **Services**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-147">In your Visual Studio Team Services project, click the **Settings** icon in the toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services - External Connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="b4ea3-149">On the left, click **New Service Endpoint** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-149">On the left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services - GitHub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="b4ea3-151">To authorize VSTS to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-151">To authorize VSTS to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span></span>

    ![Visual Studio Team Services - Authorize GitHub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-to-your-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="b4ea3-153">Connect VSTS to your Azure container registry and Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="b4ea3-153">Connect VSTS to your Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="b4ea3-154">The last steps before getting into the CI/CD pipeline are to configure external connections to your container registry and your Docker Swarm cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-154">The last steps before getting into the CI/CD pipeline are to configure external connections to your container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="b4ea3-155">In the **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-155">In the **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="b4ea3-156">In the popup that opens, enter the URL and the credentials of your Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-156">In the popup that opens, enter the URL and the credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services - Docker Registry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="b4ea3-158">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-158">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="b4ea3-159">Then enter the SSH connection information of your Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-159">Then enter the SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services - SSH](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="b4ea3-161">All the configuration is done now.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-161">All the configuration is done now.</span></span> <span data-ttu-id="b4ea3-162">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-162">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span></span> 

## <a name="step-2-create-the-build-definition"></a><span data-ttu-id="b4ea3-163">Step 2: Create the build definition</span><span class="sxs-lookup"><span data-stu-id="b4ea3-163">Step 2: Create the build definition</span></span>

<span data-ttu-id="b4ea3-164">In this step, you set up a build definitionfor your VSTS project and define the build workflow for your container images</span><span class="sxs-lookup"><span data-stu-id="b4ea3-164">In this step, you set up a build definitionfor your VSTS project and define the build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="b4ea3-165">Initial definition setup</span><span class="sxs-lookup"><span data-stu-id="b4ea3-165">Initial definition setup</span></span>

1. <span data-ttu-id="b4ea3-166">To create a build definition, connect to your Visual Studio Team Services project and click **Build & Release**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-166">To create a build definition, connect to your Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="b4ea3-167">In the **Build definitions** section, click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-167">In the **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="b4ea3-168">Select the **Empty** template.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-168">Select the **Empty** template.</span></span>

    ![Visual Studio Team Services - New Build Definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="b4ea3-170">Configure the new build with a GitHub repository source, check **Continuous integration**, and select the agent queue where you registered your Linux agent.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-170">Configure the new build with a GitHub repository source, check **Continuous integration**, and select the agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="b4ea3-171">Click **Create** to create the build definition.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-171">Click **Create** to create the build definition.</span></span>

    ![Visual Studio Team Services - Create Build Definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="b4ea3-173">On the **Build Definitions** page, first open the **Repository** tab and configure the build to use the fork of the MyShop project that you created in the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-173">On the **Build Definitions** page, first open the **Repository** tab and configure the build to use the fork of the MyShop project that you created in the prerequisites.</span></span> <span data-ttu-id="b4ea3-174">Make sure that you select *acs-docs* as the **Default branch**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-174">Make sure that you select *acs-docs* as the **Default branch**.</span></span>

    ![Visual Studio Team Services - Build Repository Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="b4ea3-176">On the **Triggers** tab, configure the build to be triggered after each commit.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-176">On the **Triggers** tab, configure the build to be triggered after each commit.</span></span> <span data-ttu-id="b4ea3-177">Select **Continuous integration** and **Batch changes**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services - Build Trigger Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-the-build-workflow"></a><span data-ttu-id="b4ea3-179">Define the build workflow</span><span class="sxs-lookup"><span data-stu-id="b4ea3-179">Define the build workflow</span></span>
<span data-ttu-id="b4ea3-180">The next steps define the build workflow.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-180">The next steps define the build workflow.</span></span> <span data-ttu-id="b4ea3-181">There are five container images to build for the *MyShop* application.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-181">There are five container images to build for the *MyShop* application.</span></span> <span data-ttu-id="b4ea3-182">Each image is built using the Dockerfile located in the project folders:</span><span class="sxs-lookup"><span data-stu-id="b4ea3-182">Each image is built using the Dockerfile located in the project folders:</span></span>

* <span data-ttu-id="b4ea3-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="b4ea3-183">ProductsApi</span></span>
* <span data-ttu-id="b4ea3-184">Proxy</span><span class="sxs-lookup"><span data-stu-id="b4ea3-184">Proxy</span></span>
* <span data-ttu-id="b4ea3-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="b4ea3-185">RatingsApi</span></span>
* <span data-ttu-id="b4ea3-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="b4ea3-186">RecommandationsApi</span></span>
* <span data-ttu-id="b4ea3-187">ShopFront</span><span class="sxs-lookup"><span data-stu-id="b4ea3-187">ShopFront</span></span>

<span data-ttu-id="b4ea3-188">You need to add two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-188">You need to add two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span></span> 

1. <span data-ttu-id="b4ea3-189">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-189">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - Add Build Steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="b4ea3-191">For each image, configure one step that uses the `docker build` command.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-191">For each image, configure one step that uses the `docker build` command.</span></span>

    ![Visual Studio Team Services - Docker Build](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="b4ea3-193">For the build operation, select your Azure container registry, the **Build an image** action, and the Dockerfile that defines each image.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-193">For the build operation, select your Azure container registry, the **Build an image** action, and the Dockerfile that defines each image.</span></span> <span data-ttu-id="b4ea3-194">Set the **Build context** as the Dockerfile root directory, and define the **Image Name**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-194">Set the **Build context** as the Dockerfile root directory, and define the **Image Name**.</span></span> 
    
    <span data-ttu-id="b4ea3-195">As shown on the preceding screen, start the image name with the URI of your Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-195">As shown on the preceding screen, start the image name with the URI of your Azure container registry.</span></span> <span data-ttu-id="b4ea3-196">(You can also use a build variable to parameterize the tag of the image, such as the build identifier in this example.)</span><span class="sxs-lookup"><span data-stu-id="b4ea3-196">(You can also use a build variable to parameterize the tag of the image, such as the build identifier in this example.)</span></span>

3. <span data-ttu-id="b4ea3-197">For each image, configure a second step that uses the `docker push` command.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-197">For each image, configure a second step that uses the `docker push` command.</span></span>

    ![Visual Studio Team Services - Docker Push](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="b4ea3-199">For the push operation, select your Azure container registry, the **Push an image** action, and enter the **Image Name** that is built in the previous step.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-199">For the push operation, select your Azure container registry, the **Push an image** action, and enter the **Image Name** that is built in the previous step.</span></span>

4. <span data-ttu-id="b4ea3-200">After you configure the build and push steps for each of the five images, add two more steps in the build workflow.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-200">After you configure the build and push steps for each of the five images, add two more steps in the build workflow.</span></span>

    <span data-ttu-id="b4ea3-201">a.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-201">a.</span></span> <span data-ttu-id="b4ea3-202">A command-line task that uses a bash script to replace the *BuildNumber* occurence in the docker-compose.yml file with the current build Id. See the following screen for details.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-202">A command-line task that uses a bash script to replace the *BuildNumber* occurence in the docker-compose.yml file with the current build Id. See the following screen for details.</span></span>

    ![Visual Studio Team Services - Update Compose file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="b4ea3-204">b.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-204">b.</span></span> <span data-ttu-id="b4ea3-205">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-205">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span></span> <span data-ttu-id="b4ea3-206">See the following screen for details.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-206">See the following screen for details.</span></span>

    ![Visual Studio Team Services - Publish Compose file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="b4ea3-208">Click **Save** and name your build definition.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-the-release-definition"></a><span data-ttu-id="b4ea3-209">Step 3: Create the release definition</span><span class="sxs-lookup"><span data-stu-id="b4ea3-209">Step 3: Create the release definition</span></span>

<span data-ttu-id="b4ea3-210">Visual Studio Team Services allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="b4ea3-210">Visual Studio Team Services allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="b4ea3-211">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-211">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="b4ea3-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services - Release to ACS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="b4ea3-214">Initial release setup</span><span class="sxs-lookup"><span data-stu-id="b4ea3-214">Initial release setup</span></span>

1. <span data-ttu-id="b4ea3-215">To create a release definition, click **Releases** > **+ Release**</span><span class="sxs-lookup"><span data-stu-id="b4ea3-215">To create a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="b4ea3-216">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-216">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="b4ea3-217">Here, link this new release definition to the build that you defined in the previous step.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-217">Here, link this new release definition to the build that you defined in the previous step.</span></span> <span data-ttu-id="b4ea3-218">By doing this, the docker-compose.yml file is available in the release process.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-218">By doing this, the docker-compose.yml file is available in the release process.</span></span>

    ![Visual Studio Team Services - Release Artifacts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="b4ea3-220">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-220">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="b4ea3-221">Set the trigger on the same artifact source.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-221">Set the trigger on the same artifact source.</span></span> <span data-ttu-id="b4ea3-222">This setting ensures that a new release starts as soon as the build completes successfully.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-222">This setting ensures that a new release starts as soon as the build completes successfully.</span></span>

    ![Visual Studio Team Services - Release Triggers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-the-release-workflow"></a><span data-ttu-id="b4ea3-224">Define the release workflow</span><span class="sxs-lookup"><span data-stu-id="b4ea3-224">Define the release workflow</span></span>

<span data-ttu-id="b4ea3-225">The release workflow is composed of two tasks that you add.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-225">The release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="b4ea3-226">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-226">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span></span> <span data-ttu-id="b4ea3-227">See the following screen for details.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-227">See the following screen for details.</span></span>

    ![Visual Studio Team Services - Release SCP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="b4ea3-229">Configure a second task to execute a bash command to run `docker` and `docker-compose` commands on the master node.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-229">Configure a second task to execute a bash command to run `docker` and `docker-compose` commands on the master node.</span></span> <span data-ttu-id="b4ea3-230">See the following screen for details.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-230">See the following screen for details.</span></span>

    ![Visual Studio Team Services - Release Bash](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="b4ea3-232">The command executed on the master use the Docker CLI and the Docker-Compose CLI to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="b4ea3-232">The command executed on the master use the Docker CLI and the Docker-Compose CLI to do the following tasks:</span></span>

    - <span data-ttu-id="b4ea3-233">Login to the Azure container registry (it uses three build variab\`les that are defined in the **Variables** tab)</span><span class="sxs-lookup"><span data-stu-id="b4ea3-233">Login to the Azure container registry (it uses three build variab\`les that are defined in the **Variables** tab)</span></span>
    - <span data-ttu-id="b4ea3-234">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span><span class="sxs-lookup"><span data-stu-id="b4ea3-234">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="b4ea3-235">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span><span class="sxs-lookup"><span data-stu-id="b4ea3-235">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span></span> 
    - <span data-ttu-id="b4ea3-236">Execute `docker-compose` commands that pull the new images, stop the services, remove the services, and create the containers.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-236">Execute `docker-compose` commands that pull the new images, stop the services, remove the services, and create the containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="b4ea3-237">As shown on the preceding screen, leave the **Fail on STDERR** checkbox unchecked.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-237">As shown on the preceding screen, leave the **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="b4ea3-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span></span> <span data-ttu-id="b4ea3-239">If you check the checkbox, Visual Studio Team Services reports that errors occurred during the release, even if all goes well.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-239">If you check the checkbox, Visual Studio Team Services reports that errors occurred during the release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="b4ea3-240">Save this new release definition.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="b4ea3-241">This deployment includes some downtime because we are stopping the old services and running the new one.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-241">This deployment includes some downtime because we are stopping the old services and running the new one.</span></span> <span data-ttu-id="b4ea3-242">It is possible to avoid this by doing a blue-green deployment.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-242">It is possible to avoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-the-cicd-pipeline"></a><span data-ttu-id="b4ea3-243">Step 4.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-243">Step 4.</span></span> <span data-ttu-id="b4ea3-244">Test the CI/CD pipeline</span><span class="sxs-lookup"><span data-stu-id="b4ea3-244">Test the CI/CD pipeline</span></span>

<span data-ttu-id="b4ea3-245">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-245">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span></span> <span data-ttu-id="b4ea3-246">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-246">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span></span> <span data-ttu-id="b4ea3-247">A few seconds after you push the code, you will see a new build running in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-247">A few seconds after you push the code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="b4ea3-248">Once completed successfully, a new release will be triggered and will deploy the new version of the application on the Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="b4ea3-248">Once completed successfully, a new release will be triggered and will deploy the new version of the application on the Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4ea3-249">Next Steps</span><span class="sxs-lookup"><span data-stu-id="b4ea3-249">Next Steps</span></span>

* <span data-ttu-id="b4ea3-250">For more information about CI/CD with Visual Studio Team Services, see the [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="b4ea3-250">For more information about CI/CD with Visual Studio Team Services, see the [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>





















