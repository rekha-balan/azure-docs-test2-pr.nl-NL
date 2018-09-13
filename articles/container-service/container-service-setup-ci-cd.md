---
title: CI/CD with Azure Container Service and DC/OS | Microsoft Docs
description: How to fully automate building and deploying a multi-container Docker app to an Azure Container Service cluster running DC/OS.
services: container-service
documentationcenter: ''
author: spboyer
manager: wpickett
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.assetid: b16b767a-2eaa-418a-becc-8c032713a1f2
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/14/2016
ms.author: johnsta
ms.openlocfilehash: 25426ebb5a488972b4c8c9ce8c1743077a4192b0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549917"
---
# <a name="continuous-integration-and-deployment-of-multi-container-docker-applications-to-azure-container-service"></a><span data-ttu-id="0dec6-104">Continuous Integration and Deployment of Multi-Container Docker Applications to Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="0dec6-104">Continuous Integration and Deployment of Multi-Container Docker Applications to Azure Container Service</span></span> 
<span data-ttu-id="0dec6-105">In this tutorial, we cover how to fully automate building and deploying a multi-container Docker app to an Azure Container Service cluster running DC/OS.</span><span class="sxs-lookup"><span data-stu-id="0dec6-105">In this tutorial, we cover how to fully automate building and deploying a multi-container Docker app to an Azure Container Service cluster running DC/OS.</span></span> <span data-ttu-id="0dec6-106">While the benefits of continuous integration and deployment (CI/CD) are known, there are new considerations when integrating containers into your workflow.</span><span class="sxs-lookup"><span data-stu-id="0dec6-106">While the benefits of continuous integration and deployment (CI/CD) are known, there are new considerations when integrating containers into your workflow.</span></span> <span data-ttu-id="0dec6-107">Using the new Azure Container Registry and CLI commands, we set up an end-to-end flow, which you can customize.</span><span class="sxs-lookup"><span data-stu-id="0dec6-107">Using the new Azure Container Registry and CLI commands, we set up an end-to-end flow, which you can customize.</span></span>

## <a name="get-started"></a><span data-ttu-id="0dec6-108">Get started</span><span class="sxs-lookup"><span data-stu-id="0dec6-108">Get started</span></span>
<span data-ttu-id="0dec6-109">You can run this walkthrough on OS X, Windows, or Linux.</span><span class="sxs-lookup"><span data-stu-id="0dec6-109">You can run this walkthrough on OS X, Windows, or Linux.</span></span>
- <span data-ttu-id="0dec6-110">You need an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0dec6-110">You need an Azure subscription.</span></span> <span data-ttu-id="0dec6-111">If you don't have one, you can [sign up for an account](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="0dec6-111">If you don't have one, you can [sign up for an account](https://azure.microsoft.com/).</span></span>
- <span data-ttu-id="0dec6-112">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="0dec6-112">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

## <a name="what-well-create"></a><span data-ttu-id="0dec6-113">What we'll create</span><span class="sxs-lookup"><span data-stu-id="0dec6-113">What we'll create</span></span>
<span data-ttu-id="0dec6-114">Let's touch on some key aspects of the app and its deployment flow that we are setting up:</span><span class="sxs-lookup"><span data-stu-id="0dec6-114">Let's touch on some key aspects of the app and its deployment flow that we are setting up:</span></span>
* <span data-ttu-id="0dec6-115">**The application is composed of multiple services**.</span><span class="sxs-lookup"><span data-stu-id="0dec6-115">**The application is composed of multiple services**.</span></span> <span data-ttu-id="0dec6-116">Docker assets, Dockerfile, and docker-compose.yml, to define the services in our app, each running in separate containers.</span><span class="sxs-lookup"><span data-stu-id="0dec6-116">Docker assets, Dockerfile, and docker-compose.yml, to define the services in our app, each running in separate containers.</span></span> <span data-ttu-id="0dec6-117">These enable parts of the app to scale independently, and each service can be written in a different programming language and framework.</span><span class="sxs-lookup"><span data-stu-id="0dec6-117">These enable parts of the app to scale independently, and each service can be written in a different programming language and framework.</span></span> <span data-ttu-id="0dec6-118">The app's code can be hosted across one or more Git source repositories (the tools currently support GitHub or Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="0dec6-118">The app's code can be hosted across one or more Git source repositories (the tools currently support GitHub or Visual Studio Team Services).</span></span>

* <span data-ttu-id="0dec6-119">The app runs in an **ACS cluster configured with DC/OS**.</span><span class="sxs-lookup"><span data-stu-id="0dec6-119">The app runs in an **ACS cluster configured with DC/OS**.</span></span> <span data-ttu-id="0dec6-120">The container orchestrator can manage the health of our cluster and ensure our required number of container instances keep running.</span><span class="sxs-lookup"><span data-stu-id="0dec6-120">The container orchestrator can manage the health of our cluster and ensure our required number of container instances keep running.</span></span> 

* <span data-ttu-id="0dec6-121">The process of **building and deploying container images fully automate with zero-downtime**.</span><span class="sxs-lookup"><span data-stu-id="0dec6-121">The process of **building and deploying container images fully automate with zero-downtime**.</span></span> <span data-ttu-id="0dec6-122">We want developers on the team to 'git push' to a branch, which automatically triggers an integration process.</span><span class="sxs-lookup"><span data-stu-id="0dec6-122">We want developers on the team to 'git push' to a branch, which automatically triggers an integration process.</span></span> <span data-ttu-id="0dec6-123">That is, build and tag container images, run tests on each container, and push those images to a Docker private registry.</span><span class="sxs-lookup"><span data-stu-id="0dec6-123">That is, build and tag container images, run tests on each container, and push those images to a Docker private registry.</span></span> <span data-ttu-id="0dec6-124">From there, new images are automatically deployed to a shared pre-production environment on an ACS cluster for further testing.</span><span class="sxs-lookup"><span data-stu-id="0dec6-124">From there, new images are automatically deployed to a shared pre-production environment on an ACS cluster for further testing.</span></span>

* <span data-ttu-id="0dec6-125">**Promote a release from one environment to the next**, for example from Dev -> Test -> Staging -> Production.</span><span class="sxs-lookup"><span data-stu-id="0dec6-125">**Promote a release from one environment to the next**, for example from Dev -> Test -> Staging -> Production.</span></span> <span data-ttu-id="0dec6-126">Each time we promote to a downstream environment, we will not need to rebuild our container images to ensure we deploy the same images tested in a prior environment.</span><span class="sxs-lookup"><span data-stu-id="0dec6-126">Each time we promote to a downstream environment, we will not need to rebuild our container images to ensure we deploy the same images tested in a prior environment.</span></span> <span data-ttu-id="0dec6-127">This process is the concept of *immutable services*, and reduces the likelihood of undetected errors creeping into production.</span><span class="sxs-lookup"><span data-stu-id="0dec6-127">This process is the concept of *immutable services*, and reduces the likelihood of undetected errors creeping into production.</span></span>

* <span data-ttu-id="0dec6-128">To most effectively utilize compute resources in our ACS cluster, we utilize the same cluster to run build tasks fully containerizing build and deploy steps.</span><span class="sxs-lookup"><span data-stu-id="0dec6-128">To most effectively utilize compute resources in our ACS cluster, we utilize the same cluster to run build tasks fully containerizing build and deploy steps.</span></span> <span data-ttu-id="0dec6-129">The cluster also hosts our multiple dev/test/production environments.</span><span class="sxs-lookup"><span data-stu-id="0dec6-129">The cluster also hosts our multiple dev/test/production environments.</span></span>


## <a name="create-an-azure-container-service-cluster-configured-with-dcos"></a><span data-ttu-id="0dec6-130">Create an Azure Container Service cluster configured with DC/OS</span><span class="sxs-lookup"><span data-stu-id="0dec6-130">Create an Azure Container Service cluster configured with DC/OS</span></span>

>[!IMPORTANT]
> <span data-ttu-id="0dec6-131">To create a secure cluster you pass your SSH public key file to pass when you call `az acs create` .</span><span class="sxs-lookup"><span data-stu-id="0dec6-131">To create a secure cluster you pass your SSH public key file to pass when you call `az acs create` .</span></span> <span data-ttu-id="0dec6-132">Either you can have the Azure CLI 2.0 generate the keys for you and pass them at the same time using the `--generate-ssh-keys` option, or you can pass the path to your keys using the `--ssh-key-value` option (the default location on Linux is `~/.ssh/id_rsa.pub` and on Windows `%HOMEPATH%\.ssh\id_rsa.pub`, but this can be changed).</span><span class="sxs-lookup"><span data-stu-id="0dec6-132">Either you can have the Azure CLI 2.0 generate the keys for you and pass them at the same time using the `--generate-ssh-keys` option, or you can pass the path to your keys using the `--ssh-key-value` option (the default location on Linux is `~/.ssh/id_rsa.pub` and on Windows `%HOMEPATH%\.ssh\id_rsa.pub`, but this can be changed).</span></span>
<span data-ttu-id="0dec6-133"><!---Loc Comment: What do you mean by "you pass your SSH public key file to pass"? Thank you.---> To create SSH public and private key files on Linux, see [Create SSH keys on Linux and Mac](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fcontainer-services%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0dec6-133"><!---Loc Comment: What do you mean by "you pass your SSH public key file to pass"? Thank you.---> To create SSH public and private key files on Linux, see [Create SSH keys on Linux and Mac](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fcontainer-services%2ftoc.json).</span></span> <span data-ttu-id="0dec6-134">To create SSH public and private key files on Windows, see [Create SSH keys on Windows](../virtual-machines/linux/ssh-from-windows.md?toc=%2fazure%2fcontainer-services%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0dec6-134">To create SSH public and private key files on Windows, see [Create SSH keys on Windows](../virtual-machines/linux/ssh-from-windows.md?toc=%2fazure%2fcontainer-services%2ftoc.json).</span></span> 

1. <span data-ttu-id="0dec6-135">First, type the [az login](/cli/azure/#login) command in a terminal window to log in to your Azure subscription with the Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="0dec6-135">First, type the [az login](/cli/azure/#login) command in a terminal window to log in to your Azure subscription with the Azure CLI:</span></span> 

    `az login`

1. <span data-ttu-id="0dec6-136">Create a resource group in which we place our cluster using [az group create](/cli/azure/group#create):</span><span class="sxs-lookup"><span data-stu-id="0dec6-136">Create a resource group in which we place our cluster using [az group create](/cli/azure/group#create):</span></span>
    
    `az group create --name myacs-rg --location westus`

    <span data-ttu-id="0dec6-137">You may want to specify the [Azure datacenter region](https://azure.microsoft.com/regions) closest to you.</span><span class="sxs-lookup"><span data-stu-id="0dec6-137">You may want to specify the [Azure datacenter region](https://azure.microsoft.com/regions) closest to you.</span></span> 

1. <span data-ttu-id="0dec6-138">Create an ACS cluster with default settings using [az acs create](/cli/azure/acs#create) and passing the path to you public SSH key file:</span><span class="sxs-lookup"><span data-stu-id="0dec6-138">Create an ACS cluster with default settings using [az acs create](/cli/azure/acs#create) and passing the path to you public SSH key file:</span></span> 

    ```azurecli
    az acs create \
    --resource-group myacs-rg 
    --name myacs \
    --dns-prefix myacs \
    --ssh-key-value ~/.ssh/id_rsa.pub
    ```
    
<span data-ttu-id="0dec6-139">This step takes several minutes, so feel free to read on.</span><span class="sxs-lookup"><span data-stu-id="0dec6-139">This step takes several minutes, so feel free to read on.</span></span>  <span data-ttu-id="0dec6-140">The `acs create` command returns information about the newly created cluster (or you can list the ACS clusters in your subscription with `az acs list`).</span><span class="sxs-lookup"><span data-stu-id="0dec6-140">The `acs create` command returns information about the newly created cluster (or you can list the ACS clusters in your subscription with `az acs list`).</span></span> <span data-ttu-id="0dec6-141">For more ACS configuration options, [read more about creating and configuring an ACS cluster](container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="0dec6-141">For more ACS configuration options, [read more about creating and configuring an ACS cluster](container-service-deployment.md).</span></span>

## <a name="set-up-sample-code"></a><span data-ttu-id="0dec6-142">Set up sample code</span><span class="sxs-lookup"><span data-stu-id="0dec6-142">Set up sample code</span></span>
<span data-ttu-id="0dec6-143">While the cluster is being created, we can set up sample code that we deploy to ACS.</span><span class="sxs-lookup"><span data-stu-id="0dec6-143">While the cluster is being created, we can set up sample code that we deploy to ACS.</span></span>

1. <span data-ttu-id="0dec6-144">[Fork](https://help.github.com/articles/fork-a-repo/) the sample GitHub repository so that you have your own copy: [https://github.com/azure-samples/container-service-dotnet-continuous-integration-multi-container.git](https://github.com/azure-samples/container-service-dotnet-continuous-integration-multi-container.git).</span><span class="sxs-lookup"><span data-stu-id="0dec6-144">[Fork](https://help.github.com/articles/fork-a-repo/) the sample GitHub repository so that you have your own copy: [https://github.com/azure-samples/container-service-dotnet-continuous-integration-multi-container.git](https://github.com/azure-samples/container-service-dotnet-continuous-integration-multi-container.git).</span></span> <span data-ttu-id="0dec6-145">The app is essentially a multi-container version of "hello world."</span><span class="sxs-lookup"><span data-stu-id="0dec6-145">The app is essentially a multi-container version of "hello world."</span></span>
1. <span data-ttu-id="0dec6-146">Once you have created a fork in your own GitHub account, locally clone the repository on your computer:</span><span class="sxs-lookup"><span data-stu-id="0dec6-146">Once you have created a fork in your own GitHub account, locally clone the repository on your computer:</span></span>

    ```bash
    git clone  https://github.com/your-github-account/container-service-dotnet-continuous-integration-multi-container.git
    cd container-service-dotnet-continuous-integration-multi-container
    ```
    
<span data-ttu-id="0dec6-147">Let's take a closer look at the code:</span><span class="sxs-lookup"><span data-stu-id="0dec6-147">Let's take a closer look at the code:</span></span>
* <span data-ttu-id="0dec6-148">`/service-a` is an Angular.js-based web app with a Node.js backend.</span><span class="sxs-lookup"><span data-stu-id="0dec6-148">`/service-a` is an Angular.js-based web app with a Node.js backend.</span></span>
* <span data-ttu-id="0dec6-149">`/service-b` is a .NET Core service, and is called by `service-a` via REST.</span><span class="sxs-lookup"><span data-stu-id="0dec6-149">`/service-b` is a .NET Core service, and is called by `service-a` via REST.</span></span>
* <span data-ttu-id="0dec6-150">Both `service-a` and `service-b` contain a `Dockerfile` in each of their directories that respectively describe Node.js- and .NET Core-based container images.</span><span class="sxs-lookup"><span data-stu-id="0dec6-150">Both `service-a` and `service-b` contain a `Dockerfile` in each of their directories that respectively describe Node.js- and .NET Core-based container images.</span></span> 
* <span data-ttu-id="0dec6-151">`docker-compose.yml` declares the set of services that are built and deployed.</span><span class="sxs-lookup"><span data-stu-id="0dec6-151">`docker-compose.yml` declares the set of services that are built and deployed.</span></span>
* <span data-ttu-id="0dec6-152">In addition to `service-a` and `service-b`, a third service named `cache` runs a Redis cache that `service-a` can use.</span><span class="sxs-lookup"><span data-stu-id="0dec6-152">In addition to `service-a` and `service-b`, a third service named `cache` runs a Redis cache that `service-a` can use.</span></span> <span data-ttu-id="0dec6-153">`cache` differs from the first two services in that we don't have code for it in our source repository.</span><span class="sxs-lookup"><span data-stu-id="0dec6-153">`cache` differs from the first two services in that we don't have code for it in our source repository.</span></span> <span data-ttu-id="0dec6-154">Instead, we fetch a pre-made `redis:alpine` image from Docker Hub and deploy it to ACS.</span><span class="sxs-lookup"><span data-stu-id="0dec6-154">Instead, we fetch a pre-made `redis:alpine` image from Docker Hub and deploy it to ACS.</span></span>
* <span data-ttu-id="0dec6-155">`/service-a/server.js` contains code where `service-a` calls both `service-b` and `cache`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-155">`/service-a/server.js` contains code where `service-a` calls both `service-b` and `cache`.</span></span> <span data-ttu-id="0dec6-156">Notice that `service-a` code references `service-b` and `cache` by how they are named in `docker-compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-156">Notice that `service-a` code references `service-b` and `cache` by how they are named in `docker-compose.yml`.</span></span> <span data-ttu-id="0dec6-157">If we run these services on our local machine via `docker-compose`, Docker ensures the services are all networked appropriately to find each other by name.</span><span class="sxs-lookup"><span data-stu-id="0dec6-157">If we run these services on our local machine via `docker-compose`, Docker ensures the services are all networked appropriately to find each other by name.</span></span> <span data-ttu-id="0dec6-158">Running the services in a cluster environment with load-balanced networking typically makes it much more complex than running locally.</span><span class="sxs-lookup"><span data-stu-id="0dec6-158">Running the services in a cluster environment with load-balanced networking typically makes it much more complex than running locally.</span></span> <span data-ttu-id="0dec6-159">The good news is the Azure CLI commands set up a CI/CD flow that ensures this straight-forward service discovery code continues to run as-is in ACS.</span><span class="sxs-lookup"><span data-stu-id="0dec6-159">The good news is the Azure CLI commands set up a CI/CD flow that ensures this straight-forward service discovery code continues to run as-is in ACS.</span></span> 

    ![Multi-container sample app overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/multi-container-sample-app-overview.PNG)

## <a name="set-up-continuous-integration-and-deployment"></a><span data-ttu-id="0dec6-161">Set up continuous integration and deployment</span><span class="sxs-lookup"><span data-stu-id="0dec6-161">Set up continuous integration and deployment</span></span>
1. <span data-ttu-id="0dec6-162">Ensure the ACS cluster is ready: run [az acs list](/cli/azure/acs#list) and confirm that our ACS cluster is listed.</span><span class="sxs-lookup"><span data-stu-id="0dec6-162">Ensure the ACS cluster is ready: run [az acs list](/cli/azure/acs#list) and confirm that our ACS cluster is listed.</span></span> <span data-ttu-id="0dec6-163">(Note: ACS must be running DC/OS 1.8 or greater.)</span><span class="sxs-lookup"><span data-stu-id="0dec6-163">(Note: ACS must be running DC/OS 1.8 or greater.)</span></span>

1. <span data-ttu-id="0dec6-164">[Create a GitHub personal access token](https://help.github.com/articles/creating-an-access-token-for-command-line-use/), granting it at least the `repo` scope.</span><span class="sxs-lookup"><span data-stu-id="0dec6-164">[Create a GitHub personal access token](https://help.github.com/articles/creating-an-access-token-for-command-line-use/), granting it at least the `repo` scope.</span></span>  <span data-ttu-id="0dec6-165">Don't forget to copy the token to your clipboard, as we'll use it in the next command (it will set up a [webhook](https://help.github.com/articles/about-webhooks/) on our GitHub repo).</span><span class="sxs-lookup"><span data-stu-id="0dec6-165">Don't forget to copy the token to your clipboard, as we'll use it in the next command (it will set up a [webhook](https://help.github.com/articles/about-webhooks/) on our GitHub repo).</span></span> 

1. <span data-ttu-id="0dec6-166">Set your current directory to the root of your cloned source repository, and create a build and release pipeline, using the _&lt;GitHubPersonalAccessToken&gt; that you just created:</span><span class="sxs-lookup"><span data-stu-id="0dec6-166">Set your current directory to the root of your cloned source repository, and create a build and release pipeline, using the _&lt;GitHubPersonalAccessToken&gt; that you just created:</span></span>
    
    `cd container-service-dotnet-continuous-integration-multi-container`

    ```azurecli
    az container release create \
    --target-name myacs \
    --target-resource-group myacs-rg \
    --remote-access-token <GitHubPersonalAccessToken>
    ```

    <span data-ttu-id="0dec6-167">Where `--target-name` is the name of your ACS cluster, and `--target-resource-group` is the ACS cluster's resource group name.</span><span class="sxs-lookup"><span data-stu-id="0dec6-167">Where `--target-name` is the name of your ACS cluster, and `--target-resource-group` is the ACS cluster's resource group name.</span></span>

<span data-ttu-id="0dec6-168">On first run, this command may take a minute or so to complete.</span><span class="sxs-lookup"><span data-stu-id="0dec6-168">On first run, this command may take a minute or so to complete.</span></span> <span data-ttu-id="0dec6-169">Once completed, important information is returned regarding the build and release pipeline it created:</span><span class="sxs-lookup"><span data-stu-id="0dec6-169">Once completed, important information is returned regarding the build and release pipeline it created:</span></span>
* <span data-ttu-id="0dec6-170">`sourceRepo`: a [webhook](https://help.github.com/articles/about-webhooks/) is configured for the source repository so that the build and release pipeline is automatically triggered whenever source code is pushed to it.</span><span class="sxs-lookup"><span data-stu-id="0dec6-170">`sourceRepo`: a [webhook](https://help.github.com/articles/about-webhooks/) is configured for the source repository so that the build and release pipeline is automatically triggered whenever source code is pushed to it.</span></span>  
* <span data-ttu-id="0dec6-171">`vstsProject`: [Visual Studio Team Services](https://www.visualstudio.com/team-services/) (VSTS) is configured to *drive* the workflow (the actual build and deployment tasks run within containers in ACS).</span><span class="sxs-lookup"><span data-stu-id="0dec6-171">`vstsProject`: [Visual Studio Team Services](https://www.visualstudio.com/team-services/) (VSTS) is configured to *drive* the workflow (the actual build and deployment tasks run within containers in ACS).</span></span> <span data-ttu-id="0dec6-172">If you would like to use a specific VSTS account and project, you can define using the `--vsts-account-name` and `--vsts-project-name` parameters.</span><span class="sxs-lookup"><span data-stu-id="0dec6-172">If you would like to use a specific VSTS account and project, you can define using the `--vsts-account-name` and `--vsts-project-name` parameters.</span></span>
* <span data-ttu-id="0dec6-173">`buildDefinition`: defines the tasks that run for each build.</span><span class="sxs-lookup"><span data-stu-id="0dec6-173">`buildDefinition`: defines the tasks that run for each build.</span></span> <span data-ttu-id="0dec6-174">Container images are produced for each service defined in the docker-compose.yml, and then pushed to a Docker container registry.</span><span class="sxs-lookup"><span data-stu-id="0dec6-174">Container images are produced for each service defined in the docker-compose.yml, and then pushed to a Docker container registry.</span></span> 
* <span data-ttu-id="0dec6-175">`containerRegistry`: The Azure Container Registry is a managed service that runs a Docker container registry.</span><span class="sxs-lookup"><span data-stu-id="0dec6-175">`containerRegistry`: The Azure Container Registry is a managed service that runs a Docker container registry.</span></span> <span data-ttu-id="0dec6-176">A new Azure Container Registry is created with a default name or you can alternatively specify an Azure Container Registry name via the `--registry-name` parameter.</span><span class="sxs-lookup"><span data-stu-id="0dec6-176">A new Azure Container Registry is created with a default name or you can alternatively specify an Azure Container Registry name via the `--registry-name` parameter.</span></span>
* <span data-ttu-id="0dec6-177">`releaseDefinition`: defines the tasks that are run for each deployment.</span><span class="sxs-lookup"><span data-stu-id="0dec6-177">`releaseDefinition`: defines the tasks that are run for each deployment.</span></span> <span data-ttu-id="0dec6-178">Container images for the services defined in docker-compose.yml are pulled from the container registry, and deployed to the ACS cluster.</span><span class="sxs-lookup"><span data-stu-id="0dec6-178">Container images for the services defined in docker-compose.yml are pulled from the container registry, and deployed to the ACS cluster.</span></span> <span data-ttu-id="0dec6-179">By default, three environments are created: *Dev*, *Test*, and *Production*.</span><span class="sxs-lookup"><span data-stu-id="0dec6-179">By default, three environments are created: *Dev*, *Test*, and *Production*.</span></span> <span data-ttu-id="0dec6-180">The release definition is configured by default to automatically deploy to *Dev* each time a build completes successfully.</span><span class="sxs-lookup"><span data-stu-id="0dec6-180">The release definition is configured by default to automatically deploy to *Dev* each time a build completes successfully.</span></span> <span data-ttu-id="0dec6-181">A release can be promoted to *Test* or *Production* manually without requiring a rebuild.</span><span class="sxs-lookup"><span data-stu-id="0dec6-181">A release can be promoted to *Test* or *Production* manually without requiring a rebuild.</span></span> <span data-ttu-id="0dec6-182">The default flow can be customized in VSTS.</span><span class="sxs-lookup"><span data-stu-id="0dec6-182">The default flow can be customized in VSTS.</span></span> 
* <span data-ttu-id="0dec6-183">`containerService`: the target ACS cluster (must be running DC/OS 1.8).</span><span class="sxs-lookup"><span data-stu-id="0dec6-183">`containerService`: the target ACS cluster (must be running DC/OS 1.8).</span></span>


<span data-ttu-id="0dec6-184">The following snippet is an example command you would type if you already have an existing Azure Container Registry named `myregistry`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-184">The following snippet is an example command you would type if you already have an existing Azure Container Registry named `myregistry`.</span></span> <span data-ttu-id="0dec6-185">Create and build release definitions with a VSTS account at `myvstsaccount.visualstudio.com`, and an existing VSTS project `myvstsproject`:</span><span class="sxs-lookup"><span data-stu-id="0dec6-185">Create and build release definitions with a VSTS account at `myvstsaccount.visualstudio.com`, and an existing VSTS project `myvstsproject`:</span></span>
        
```azurecli
az container release create \
--target-name myacs \
--target-resource-group myacs-rg \
--registry-name myregistry \
--vsts-account-name myvstsaccount \
--vsts-project-name myvstsproject \
--remote-access-token <GitHubPersonalAccessToken>
```

## <a name="view-deployment-pipeline-progress"></a><span data-ttu-id="0dec6-186">View deployment pipeline progress</span><span class="sxs-lookup"><span data-stu-id="0dec6-186">View deployment pipeline progress</span></span>
<span data-ttu-id="0dec6-187">Once the pipeline is created, a first-time build and deployment is kicked off automatically.</span><span class="sxs-lookup"><span data-stu-id="0dec6-187">Once the pipeline is created, a first-time build and deployment is kicked off automatically.</span></span> <span data-ttu-id="0dec6-188">Subsequent builds are triggered each time code is pushed to the source repository.</span><span class="sxs-lookup"><span data-stu-id="0dec6-188">Subsequent builds are triggered each time code is pushed to the source repository.</span></span> <span data-ttu-id="0dec6-189">You can check progress of a build and/or release by opening your browser to the build definition or release definition URLs.</span><span class="sxs-lookup"><span data-stu-id="0dec6-189">You can check progress of a build and/or release by opening your browser to the build definition or release definition URLs.</span></span>

<span data-ttu-id="0dec6-190">You can always find the release definition URL associated with an ACS cluster by running this command:</span><span class="sxs-lookup"><span data-stu-id="0dec6-190">You can always find the release definition URL associated with an ACS cluster by running this command:</span></span>

```azurecli
az container release list \
--target-name myacs \
--target-resource-group myacs-rg
``` 

![VSTS Build](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/vsts-build.PNG)

<span data-ttu-id="0dec6-192">*VSTS screenshot showing CI results of our multi-container app*</span><span class="sxs-lookup"><span data-stu-id="0dec6-192">*VSTS screenshot showing CI results of our multi-container app*</span></span>

![VSTS Release](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/vsts-release.PNG)

<span data-ttu-id="0dec6-194">*VSTS docker-compose release with multiple environments*</span><span class="sxs-lookup"><span data-stu-id="0dec6-194">*VSTS docker-compose release with multiple environments*</span></span>

## <a name="view-the-application"></a><span data-ttu-id="0dec6-195">View the application</span><span class="sxs-lookup"><span data-stu-id="0dec6-195">View the application</span></span>
<span data-ttu-id="0dec6-196">At this point, our application is deployed to our shared dev environment and is not publicly exposed.</span><span class="sxs-lookup"><span data-stu-id="0dec6-196">At this point, our application is deployed to our shared dev environment and is not publicly exposed.</span></span> <span data-ttu-id="0dec6-197">In the meantime, use the DC/OS dashboard to view and manage our services and [create an SSH tunnel to the DC/OS-related endpoints](https://azure.microsoft.com/documentation/articles/container-service-connect/) or run a convenience command provided by the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0dec6-197">In the meantime, use the DC/OS dashboard to view and manage our services and [create an SSH tunnel to the DC/OS-related endpoints](https://azure.microsoft.com/documentation/articles/container-service-connect/) or run a convenience command provided by the Azure CLI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0dec6-198">On a first-time deployment, confirm the VSTS release successfully deployed before proceeding.</span><span class="sxs-lookup"><span data-stu-id="0dec6-198">On a first-time deployment, confirm the VSTS release successfully deployed before proceeding.</span></span>

> [!NOTE]
> <span data-ttu-id="0dec6-199">Windows Only:  You need to set up [Pageant](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to complete this section.</span><span class="sxs-lookup"><span data-stu-id="0dec6-199">Windows Only:  You need to set up [Pageant](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to complete this section.</span></span>
> 
>* <span data-ttu-id="0dec6-200">Launch *PuttyGen* and load the private SSH key used to create the ACS cluster (%homepath%\id_rsa).</span><span class="sxs-lookup"><span data-stu-id="0dec6-200">Launch *PuttyGen* and load the private SSH key used to create the ACS cluster (%homepath%\id_rsa).</span></span>
>* <span data-ttu-id="0dec6-201">Save the private SSH key as `id_rsa.ppk` in the same folder.</span><span class="sxs-lookup"><span data-stu-id="0dec6-201">Save the private SSH key as `id_rsa.ppk` in the same folder.</span></span>
>* <span data-ttu-id="0dec6-202">Launch *Pageant* - it will start running and display an icon in your bottom-right system tray.</span><span class="sxs-lookup"><span data-stu-id="0dec6-202">Launch *Pageant* - it will start running and display an icon in your bottom-right system tray.</span></span>
>* <span data-ttu-id="0dec6-203">Right-click the system tray icon and select *Add Key*.</span><span class="sxs-lookup"><span data-stu-id="0dec6-203">Right-click the system tray icon and select *Add Key*.</span></span>
>* <span data-ttu-id="0dec6-204">Add the `id_rsa.ppk` file.</span><span class="sxs-lookup"><span data-stu-id="0dec6-204">Add the `id_rsa.ppk` file.</span></span>
> 
> 

1. <span data-ttu-id="0dec6-205">Open the ACS cluster's DC/OS dashboard using the Azure CLI convenience command:</span><span class="sxs-lookup"><span data-stu-id="0dec6-205">Open the ACS cluster's DC/OS dashboard using the Azure CLI convenience command:</span></span>
    
    `az acs dcos browse -g myacs-rg -n myacs`

    * <span data-ttu-id="0dec6-206">`-g` is the resource group name of the target ACS cluster</span><span class="sxs-lookup"><span data-stu-id="0dec6-206">`-g` is the resource group name of the target ACS cluster</span></span>
    * <span data-ttu-id="0dec6-207">`-n` is the name of the target ACS cluster.</span><span class="sxs-lookup"><span data-stu-id="0dec6-207">`-n` is the name of the target ACS cluster.</span></span>
    * <span data-ttu-id="0dec6-208">You may be prompted for your local account password, since this command requires administrator privilege.</span><span class="sxs-lookup"><span data-stu-id="0dec6-208">You may be prompted for your local account password, since this command requires administrator privilege.</span></span> <span data-ttu-id="0dec6-209">The command creates an SSH tunnel to a DC/OS endpoint, opens your default browser to that endpoint, and temporarily configures the browser's web proxy.</span><span class="sxs-lookup"><span data-stu-id="0dec6-209">The command creates an SSH tunnel to a DC/OS endpoint, opens your default browser to that endpoint, and temporarily configures the browser's web proxy.</span></span> 

    > [!TIP]
    > <span data-ttu-id="0dec6-210">If you need to look up the name of your ACS cluster, you can list all ACS clusters in your subscription by running `az acs list`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-210">If you need to look up the name of your ACS cluster, you can list all ACS clusters in your subscription by running `az acs list`.</span></span> 

1. <span data-ttu-id="0dec6-211">In the DC/OS dashboard, click **Services** on the left navigation menu ([http://localhost/#/services](http://localhost/#/services)).</span><span class="sxs-lookup"><span data-stu-id="0dec6-211">In the DC/OS dashboard, click **Services** on the left navigation menu ([http://localhost/#/services](http://localhost/#/services)).</span></span> <span data-ttu-id="0dec6-212">Services deployed via our pipeline are grouped under a root folder named *dev* (named after the environment in the VSTS release definition).</span><span class="sxs-lookup"><span data-stu-id="0dec6-212">Services deployed via our pipeline are grouped under a root folder named *dev* (named after the environment in the VSTS release definition).</span></span> 

![Marathon UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/marathon-ui.png)

<span data-ttu-id="0dec6-214">You can perform many useful things in the DC/OS dashboard</span><span class="sxs-lookup"><span data-stu-id="0dec6-214">You can perform many useful things in the DC/OS dashboard</span></span>

* <span data-ttu-id="0dec6-215">tracking deployment status for each service</span><span class="sxs-lookup"><span data-stu-id="0dec6-215">tracking deployment status for each service</span></span>
* <span data-ttu-id="0dec6-216">viewing CPU and Memory requirements</span><span class="sxs-lookup"><span data-stu-id="0dec6-216">viewing CPU and Memory requirements</span></span>
* <span data-ttu-id="0dec6-217">viewing logs</span><span class="sxs-lookup"><span data-stu-id="0dec6-217">viewing logs</span></span>
* <span data-ttu-id="0dec6-218">scaling the number of instances for each service</span><span class="sxs-lookup"><span data-stu-id="0dec6-218">scaling the number of instances for each service</span></span>

<span data-ttu-id="0dec6-219">**To view the web application for service-a**: start at the *dev* root folder, then drill down the folder hierarchy until you reach `service-a`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-219">**To view the web application for service-a**: start at the *dev* root folder, then drill down the folder hierarchy until you reach `service-a`.</span></span> <span data-ttu-id="0dec6-220">This view lists the running tasks (or container instances) for `service-a`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-220">This view lists the running tasks (or container instances) for `service-a`.</span></span>

![service a](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/service-a.png)

<span data-ttu-id="0dec6-222">Click a task to open its view, then click one of its available endpoints.</span><span class="sxs-lookup"><span data-stu-id="0dec6-222">Click a task to open its view, then click one of its available endpoints.</span></span>

![service a task](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/service-a-task.PNG)

<span data-ttu-id="0dec6-224">Our simple web app calls `service-a`, which calls `service-b`, and returns a hello world message.</span><span class="sxs-lookup"><span data-stu-id="0dec6-224">Our simple web app calls `service-a`, which calls `service-b`, and returns a hello world message.</span></span> <span data-ttu-id="0dec6-225">A counter is incremented on Redis each time a request is made.</span><span class="sxs-lookup"><span data-stu-id="0dec6-225">A counter is incremented on Redis each time a request is made.</span></span>

![service a web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/service-a-web-app.PNG)

### <a name="optional-reaching-a-service-from-the-command-line"></a><span data-ttu-id="0dec6-227">(Optional) Reaching a service from the command line</span><span class="sxs-lookup"><span data-stu-id="0dec6-227">(Optional) Reaching a service from the command line</span></span>
<span data-ttu-id="0dec6-228">If you want to reach a service via curl from the command line:</span><span class="sxs-lookup"><span data-stu-id="0dec6-228">If you want to reach a service via curl from the command line:</span></span>

1. <span data-ttu-id="0dec6-229">Run `az acs dcos browse --verbose -g myacs-rg -n myacs`, and take note of the line that reads "Proxy running on <ip-address>:<port>" after you enter your password.</span><span class="sxs-lookup"><span data-stu-id="0dec6-229">Run `az acs dcos browse --verbose -g myacs-rg -n myacs`, and take note of the line that reads "Proxy running on <ip-address>:<port>" after you enter your password.</span></span>
1. <span data-ttu-id="0dec6-230">In a new terminal window, type:</span><span class="sxs-lookup"><span data-stu-id="0dec6-230">In a new terminal window, type:</span></span>

    `export http_proxy=http://<web-proxy-service-ip>:<portnumber>`

    <span data-ttu-id="0dec6-231">For example: `export http_proxy=http://127.0.0.1:55405`</span><span class="sxs-lookup"><span data-stu-id="0dec6-231">For example: `export http_proxy=http://127.0.0.1:55405`</span></span>

1. <span data-ttu-id="0dec6-232">Now you can curl against your service endpoint, `curl http://service-url`, where `service-url` is the address you see when you navigate to your service endpoint from Marathon UI.</span><span class="sxs-lookup"><span data-stu-id="0dec6-232">Now you can curl against your service endpoint, `curl http://service-url`, where `service-url` is the address you see when you navigate to your service endpoint from Marathon UI.</span></span> <span data-ttu-id="0dec6-233">To unset the http_proxy variable from your command line, type `unset http_proxy`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-233">To unset the http_proxy variable from your command line, type `unset http_proxy`.</span></span>
 

## <a name="scale-services"></a><span data-ttu-id="0dec6-234">Scale services</span><span class="sxs-lookup"><span data-stu-id="0dec6-234">Scale services</span></span>
<span data-ttu-id="0dec6-235">While we're in the DC/OS dashboard, let's scale our services.</span><span class="sxs-lookup"><span data-stu-id="0dec6-235">While we're in the DC/OS dashboard, let's scale our services.</span></span>
1. <span data-ttu-id="0dec6-236">Navigate to the application in the *dev* subfolder.</span><span class="sxs-lookup"><span data-stu-id="0dec6-236">Navigate to the application in the *dev* subfolder.</span></span>
1. <span data-ttu-id="0dec6-237">Hover over `service-b`, click the gear icon, and select **Scale**.</span><span class="sxs-lookup"><span data-stu-id="0dec6-237">Hover over `service-b`, click the gear icon, and select **Scale**.</span></span>

    ![Action menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/marathon-ui-action-menu.PNG)

1. <span data-ttu-id="0dec6-239">Increase the number to 3 and click **Scale Service**.</span><span class="sxs-lookup"><span data-stu-id="0dec6-239">Increase the number to 3 and click **Scale Service**.</span></span>

    ![Scale services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/marathon-ui-scale-service.png)

1. <span data-ttu-id="0dec6-241">Navigate back to the running web app, and repeatedly click the *Say It Again* button.</span><span class="sxs-lookup"><span data-stu-id="0dec6-241">Navigate back to the running web app, and repeatedly click the *Say It Again* button.</span></span> <span data-ttu-id="0dec6-242">Notice that `service-b` invocations begin to round-robin across a collection of hostnames, while the single instance of `service-a` continues to report the same host.</span><span class="sxs-lookup"><span data-stu-id="0dec6-242">Notice that `service-b` invocations begin to round-robin across a collection of hostnames, while the single instance of `service-a` continues to report the same host.</span></span>   

## <a name="promote-a-release-to-downstream-environments-without-rebuilding-container-images"></a><span data-ttu-id="0dec6-243">Promote a release to downstream environments without rebuilding container images</span><span class="sxs-lookup"><span data-stu-id="0dec6-243">Promote a release to downstream environments without rebuilding container images</span></span>
<span data-ttu-id="0dec6-244">Our VSTS release pipeline set up three environments by default: *Dev*, *Test*, and *Production*.</span><span class="sxs-lookup"><span data-stu-id="0dec6-244">Our VSTS release pipeline set up three environments by default: *Dev*, *Test*, and *Production*.</span></span> <span data-ttu-id="0dec6-245">So far we've deployed to *Dev*.</span><span class="sxs-lookup"><span data-stu-id="0dec6-245">So far we've deployed to *Dev*.</span></span> <span data-ttu-id="0dec6-246">Let's look at how we can promote a release to the next downstream environment, *Test*, without rebuilding our container images.</span><span class="sxs-lookup"><span data-stu-id="0dec6-246">Let's look at how we can promote a release to the next downstream environment, *Test*, without rebuilding our container images.</span></span> <span data-ttu-id="0dec6-247">This workflow ensures we're deploying the exact same images we tested in the prior environment and is the concept of *immutable services*, and reduces the likelihood of undetected errors creeping into production.</span><span class="sxs-lookup"><span data-stu-id="0dec6-247">This workflow ensures we're deploying the exact same images we tested in the prior environment and is the concept of *immutable services*, and reduces the likelihood of undetected errors creeping into production.</span></span>

1. <span data-ttu-id="0dec6-248">In the VSTS web UI, navigate to **Releases**</span><span class="sxs-lookup"><span data-stu-id="0dec6-248">In the VSTS web UI, navigate to **Releases**</span></span>

    ![VSTS Releases menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/vsts-releases-menu.PNG)

1. <span data-ttu-id="0dec6-250">Open the most recent release.</span><span class="sxs-lookup"><span data-stu-id="0dec6-250">Open the most recent release.</span></span>

1. <span data-ttu-id="0dec6-251">In the release definition's menu bar, click **Deploy**, then select **Test** as the next environment we want to deploy to start a new deployment, reusing the same images that were previously deployed to *Dev*.</span><span class="sxs-lookup"><span data-stu-id="0dec6-251">In the release definition's menu bar, click **Deploy**, then select **Test** as the next environment we want to deploy to start a new deployment, reusing the same images that were previously deployed to *Dev*.</span></span> <span data-ttu-id="0dec6-252">Click **Logs** if you want to follow along the deployment in more detail.</span><span class="sxs-lookup"><span data-stu-id="0dec6-252">Click **Logs** if you want to follow along the deployment in more detail.</span></span>

    ![VSTS promotes release](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/vsts-promote-release.PNG)

<span data-ttu-id="0dec6-254">Once deployment to *Test* has succeeded, a new root folder in Marathon UI named *test* that contains the running services for that environment.</span><span class="sxs-lookup"><span data-stu-id="0dec6-254">Once deployment to *Test* has succeeded, a new root folder in Marathon UI named *test* that contains the running services for that environment.</span></span> 

![Subfolders for each environment in DC/OS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/marathon-ui-dev-test-environments.png)

## <a name="trigger-a-new-build-and-deployment"></a><span data-ttu-id="0dec6-256">Trigger a new build and deployment</span><span class="sxs-lookup"><span data-stu-id="0dec6-256">Trigger a new build and deployment</span></span>
<span data-ttu-id="0dec6-257">Let's simulate what would happen if a developer on our team pushed a code change to the source repository.</span><span class="sxs-lookup"><span data-stu-id="0dec6-257">Let's simulate what would happen if a developer on our team pushed a code change to the source repository.</span></span>

1. <span data-ttu-id="0dec6-258">Back in the code editor, open `service-a/public/index.html`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-258">Back in the code editor, open `service-a/public/index.html`.</span></span> 
1. <span data-ttu-id="0dec6-259">Modify this line of code:</span><span class="sxs-lookup"><span data-stu-id="0dec6-259">Modify this line of code:</span></span>

    `<h2>Server Says</h2>`

    <span data-ttu-id="0dec6-260">to something like:</span><span class="sxs-lookup"><span data-stu-id="0dec6-260">to something like:</span></span>

    `<h2>Server Says Hello</h2>`

1. <span data-ttu-id="0dec6-261">Save the file, then commit and push the code change to your source repository.</span><span class="sxs-lookup"><span data-stu-id="0dec6-261">Save the file, then commit and push the code change to your source repository.</span></span>

    ```bash
    git commit -am 'updated title'
    git push
    ```

<span data-ttu-id="0dec6-262">The commit automatically kicks off a new build, and a new release to be deployed to *Dev*.</span><span class="sxs-lookup"><span data-stu-id="0dec6-262">The commit automatically kicks off a new build, and a new release to be deployed to *Dev*.</span></span> <span data-ttu-id="0dec6-263">Services in downstream environments (*Test* or *Production*) remains unchanged until we decide to promote a specific release to that environment.</span><span class="sxs-lookup"><span data-stu-id="0dec6-263">Services in downstream environments (*Test* or *Production*) remains unchanged until we decide to promote a specific release to that environment.</span></span>

<span data-ttu-id="0dec6-264">If you open the build definition in VSTS, you'll see something like this:</span><span class="sxs-lookup"><span data-stu-id="0dec6-264">If you open the build definition in VSTS, you'll see something like this:</span></span> 

![New build triggered by git push](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/new-build.png)



## <a name="expose-public-endpoint-for-production"></a><span data-ttu-id="0dec6-266">Expose public endpoint for production</span><span class="sxs-lookup"><span data-stu-id="0dec6-266">Expose public endpoint for production</span></span>

1. <span data-ttu-id="0dec6-267">Add the following yaml code to a new file named `docker-compose.env.production.yml` at the root folder of your source repository.</span><span class="sxs-lookup"><span data-stu-id="0dec6-267">Add the following yaml code to a new file named `docker-compose.env.production.yml` at the root folder of your source repository.</span></span> <span data-ttu-id="0dec6-268">This adds a label that causes a public endpoint to be exposed for `service-a`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-268">This adds a label that causes a public endpoint to be exposed for `service-a`.</span></span> 
    
    ```yaml
    version: "2"
    services:
      service-a:
        labels:
          com.microsoft.acs.dcos.marathon.vhost: "<FQDN, or custom domain>"
    ```

    * <span data-ttu-id="0dec6-269">For the label value, you can either specify the URL of your ACS agent's fully qualified domain name (FQDN), or a custom domain (for example, app.contoso.com).</span><span class="sxs-lookup"><span data-stu-id="0dec6-269">For the label value, you can either specify the URL of your ACS agent's fully qualified domain name (FQDN), or a custom domain (for example, app.contoso.com).</span></span> <span data-ttu-id="0dec6-270">To find your ACS agent's FQDN, run the command `az acs list`, and check the property for `agentPoolProfiles.fqdn`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-270">To find your ACS agent's FQDN, run the command `az acs list`, and check the property for `agentPoolProfiles.fqdn`.</span></span> <span data-ttu-id="0dec6-271">For example, `myacsagents.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-271">For example, `myacsagents.westus.cloudapp.azure.com`.</span></span>
    * <span data-ttu-id="0dec6-272">The sample app by default is listening on port 80, for those who have their docker applications listening on other ports, for instance `port 8080` or `443`, attach the port number to the FQDN.</span><span class="sxs-lookup"><span data-stu-id="0dec6-272">The sample app by default is listening on port 80, for those who have their docker applications listening on other ports, for instance `port 8080` or `443`, attach the port number to the FQDN.</span></span> <span data-ttu-id="0dec6-273">For example, `myacsagents.westus.cloudapp.azure.com:8080`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-273">For example, `myacsagents.westus.cloudapp.azure.com:8080`.</span></span> <span data-ttu-id="0dec6-274">However when you try to access the application from outside, you will need to query it at port 80.</span><span class="sxs-lookup"><span data-stu-id="0dec6-274">However when you try to access the application from outside, you will need to query it at port 80.</span></span>
    * <span data-ttu-id="0dec6-275">By following the filename convention docker-compose.env.*environment-name*.yml, these settings only affect the named environment (in this case, the environment named *Production*).</span><span class="sxs-lookup"><span data-stu-id="0dec6-275">By following the filename convention docker-compose.env.*environment-name*.yml, these settings only affect the named environment (in this case, the environment named *Production*).</span></span> <span data-ttu-id="0dec6-276">Inspect the release definition in VSTS, each environment's deployment task is set up to read from a docker-compose file named after this convention.</span><span class="sxs-lookup"><span data-stu-id="0dec6-276">Inspect the release definition in VSTS, each environment's deployment task is set up to read from a docker-compose file named after this convention.</span></span>

1. <span data-ttu-id="0dec6-277">Commit and push the file to your master source repository to start another build.</span><span class="sxs-lookup"><span data-stu-id="0dec6-277">Commit and push the file to your master source repository to start another build.</span></span>

    ```bash
    git add .
    git commit -am "expose public port for service-a"
    git push
    ```

1. <span data-ttu-id="0dec6-278">Wait until the update has been built and deployed to *Dev*, then promote it to *Test*, and then promote it to *Production*.</span><span class="sxs-lookup"><span data-stu-id="0dec6-278">Wait until the update has been built and deployed to *Dev*, then promote it to *Test*, and then promote it to *Production*.</span></span> <span data-ttu-id="0dec6-279">(For the purposes of this tutorial, you can deploy directly to *Production* but it is good to get in the practice of only deploying to the next downstream environment.)</span><span class="sxs-lookup"><span data-stu-id="0dec6-279">(For the purposes of this tutorial, you can deploy directly to *Production* but it is good to get in the practice of only deploying to the next downstream environment.)</span></span>

1. <span data-ttu-id="0dec6-280">(Optional) **If you specified a custom domain** for vhost (for example, app.contoso.com), add a DNS record in your domain provider's settings.</span><span class="sxs-lookup"><span data-stu-id="0dec6-280">(Optional) **If you specified a custom domain** for vhost (for example, app.contoso.com), add a DNS record in your domain provider's settings.</span></span> <span data-ttu-id="0dec6-281">Log in to your domain provider's administrative UI and add a DNS record as follows:</span><span class="sxs-lookup"><span data-stu-id="0dec6-281">Log in to your domain provider's administrative UI and add a DNS record as follows:</span></span>

    * <span data-ttu-id="0dec6-282">Type: CNAME</span><span class="sxs-lookup"><span data-stu-id="0dec6-282">Type: CNAME</span></span>
    * <span data-ttu-id="0dec6-283">Host: Your custom domain, for example, app.contoso.com</span><span class="sxs-lookup"><span data-stu-id="0dec6-283">Host: Your custom domain, for example, app.contoso.com</span></span>
    * <span data-ttu-id="0dec6-284">Answer: ACS agent FQDN, for example, myacsagents.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="0dec6-284">Answer: ACS agent FQDN, for example, myacsagents.westus.cloudapp.azure.com</span></span>
    * <span data-ttu-id="0dec6-285">TTL (Optional): Sometimes, your domain provider gives you the ability to edit the TTL.</span><span class="sxs-lookup"><span data-stu-id="0dec6-285">TTL (Optional): Sometimes, your domain provider gives you the ability to edit the TTL.</span></span> <span data-ttu-id="0dec6-286">A lower value results in a DNS record update to be propagated more quickly.</span><span class="sxs-lookup"><span data-stu-id="0dec6-286">A lower value results in a DNS record update to be propagated more quickly.</span></span>   

1. <span data-ttu-id="0dec6-287">Once the release has been deployed to *Production*, that version is accessible to anyone.</span><span class="sxs-lookup"><span data-stu-id="0dec6-287">Once the release has been deployed to *Production*, that version is accessible to anyone.</span></span> <span data-ttu-id="0dec6-288">Open your browser to the URL you specified for the `com.microsoft.acs.dcos.marathon.vhost` label.</span><span class="sxs-lookup"><span data-stu-id="0dec6-288">Open your browser to the URL you specified for the `com.microsoft.acs.dcos.marathon.vhost` label.</span></span> <span data-ttu-id="0dec6-289">(Note: releases to pre-production environments continue to be private).</span><span class="sxs-lookup"><span data-stu-id="0dec6-289">(Note: releases to pre-production environments continue to be private).</span></span>

## <a name="summary"></a><span data-ttu-id="0dec6-290">Summary</span><span class="sxs-lookup"><span data-stu-id="0dec6-290">Summary</span></span>
<span data-ttu-id="0dec6-291">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="0dec6-291">Congratulations!</span></span> <span data-ttu-id="0dec6-292">You learned how to create an ACS cluster with DC/OS, and set up a fully automated and containerized build and deployment pipeline for a multi-container app.</span><span class="sxs-lookup"><span data-stu-id="0dec6-292">You learned how to create an ACS cluster with DC/OS, and set up a fully automated and containerized build and deployment pipeline for a multi-container app.</span></span>

<span data-ttu-id="0dec6-293">Some next steps to explore:</span><span class="sxs-lookup"><span data-stu-id="0dec6-293">Some next steps to explore:</span></span>
* <span data-ttu-id="0dec6-294">**Scale VSTS Agents.**</span><span class="sxs-lookup"><span data-stu-id="0dec6-294">**Scale VSTS Agents.**</span></span> <span data-ttu-id="0dec6-295">If you need more throughput for running build and release tasks, you can increase the number of VSTS agent instances.</span><span class="sxs-lookup"><span data-stu-id="0dec6-295">If you need more throughput for running build and release tasks, you can increase the number of VSTS agent instances.</span></span> <span data-ttu-id="0dec6-296">Navigate to **Services** in the DC/OS Dashboard, open the vsts-agents folder, and experiment with scaling the number of VSTS agent instances.</span><span class="sxs-lookup"><span data-stu-id="0dec6-296">Navigate to **Services** in the DC/OS Dashboard, open the vsts-agents folder, and experiment with scaling the number of VSTS agent instances.</span></span>
* <span data-ttu-id="0dec6-297">**Integrate unit tests.**</span><span class="sxs-lookup"><span data-stu-id="0dec6-297">**Integrate unit tests.**</span></span> <span data-ttu-id="0dec6-298">This GitHub repository shows how to make unit tests and integration tests run in containers and include them in the build tasks: [https://github.com/mindaro/sample-app](https://github.com/mindaro/sample-app).</span><span class="sxs-lookup"><span data-stu-id="0dec6-298">This GitHub repository shows how to make unit tests and integration tests run in containers and include them in the build tasks: [https://github.com/mindaro/sample-app](https://github.com/mindaro/sample-app).</span></span> 
    * <span data-ttu-id="0dec6-299">Hint: look at these files in the repository: `service-a/unit-tests.js`, `service-a/service-tests.js`, `docker-compose.ci.unit-tests.yml`, and `docker-compose.ci.service-tests.yml`.</span><span class="sxs-lookup"><span data-stu-id="0dec6-299">Hint: look at these files in the repository: `service-a/unit-tests.js`, `service-a/service-tests.js`, `docker-compose.ci.unit-tests.yml`, and `docker-compose.ci.service-tests.yml`.</span></span>

## <a name="clean-up"></a><span data-ttu-id="0dec6-300">Clean up</span><span class="sxs-lookup"><span data-stu-id="0dec6-300">Clean up</span></span>
<span data-ttu-id="0dec6-301">To limit your compute charges related to this tutorial, run the following command and take note of the deployment pipeline resources that are related to an ACS cluster:</span><span class="sxs-lookup"><span data-stu-id="0dec6-301">To limit your compute charges related to this tutorial, run the following command and take note of the deployment pipeline resources that are related to an ACS cluster:</span></span>

```azurecli 
az container release list --resource-name myacs --resource-group myacs-rg
```

<span data-ttu-id="0dec6-302">Delete the ACS cluster:</span><span class="sxs-lookup"><span data-stu-id="0dec6-302">Delete the ACS cluster:</span></span>
1. <span data-ttu-id="0dec6-303">Sign into the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="0dec6-303">Sign into the [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="0dec6-304">Look up the resource group that contains your ACS cluster.</span><span class="sxs-lookup"><span data-stu-id="0dec6-304">Look up the resource group that contains your ACS cluster.</span></span>
1. <span data-ttu-id="0dec6-305">Open the resource group's blade UI, and click **Delete** in the blade's command bar.</span><span class="sxs-lookup"><span data-stu-id="0dec6-305">Open the resource group's blade UI, and click **Delete** in the blade's command bar.</span></span>

<span data-ttu-id="0dec6-306">Delete the Azure Container Registry: In the Azure portal, search for the Azure Container Registry, and delete it.</span><span class="sxs-lookup"><span data-stu-id="0dec6-306">Delete the Azure Container Registry: In the Azure portal, search for the Azure Container Registry, and delete it.</span></span> 

<span data-ttu-id="0dec6-307">The [Visual Studio Team Services account offers free Basic Access Level for the first five users](https://azure.microsoft.com/en-us/pricing/details/visual-studio-team-services/), but you can delete the build and release definitions.</span><span class="sxs-lookup"><span data-stu-id="0dec6-307">The [Visual Studio Team Services account offers free Basic Access Level for the first five users](https://azure.microsoft.com/en-us/pricing/details/visual-studio-team-services/), but you can delete the build and release definitions.</span></span>

<span data-ttu-id="0dec6-308">Delete the VSTS Build Definition:</span><span class="sxs-lookup"><span data-stu-id="0dec6-308">Delete the VSTS Build Definition:</span></span>
        
1. <span data-ttu-id="0dec6-309">Open the Build Definition URL in your browser, then click on the **Build Definitions** link (next to the name of the build definition you are currently viewing).</span><span class="sxs-lookup"><span data-stu-id="0dec6-309">Open the Build Definition URL in your browser, then click on the **Build Definitions** link (next to the name of the build definition you are currently viewing).</span></span>
2. <span data-ttu-id="0dec6-310">Click the action menu beside the build definition you want to delete, and select **Delete Definition**</span><span class="sxs-lookup"><span data-stu-id="0dec6-310">Click the action menu beside the build definition you want to delete, and select **Delete Definition**</span></span>

`![Delete VSTS Build Definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/vsts-delete-build-def.png) 

<span data-ttu-id="0dec6-312">Delete the VSTS Release Definition:</span><span class="sxs-lookup"><span data-stu-id="0dec6-312">Delete the VSTS Release Definition:</span></span>

1. <span data-ttu-id="0dec6-313">Open the Release Definition URL in your browser.</span><span class="sxs-lookup"><span data-stu-id="0dec6-313">Open the Release Definition URL in your browser.</span></span>
2. <span data-ttu-id="0dec6-314">In the Release Definitions list on the left-hand side, click the drop-down beside the release definition you want to delete, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="0dec6-314">In the Release Definitions list on the left-hand side, click the drop-down beside the release definition you want to delete, and select **Delete**.</span></span>

`![Delete VSTS Release Definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-setup-ci-cd/vsts-delete-release-def.png)















