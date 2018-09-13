---
title: Deploy the remote monitoring solution locally - Azure | Microsoft Docs
description: This tutorial shows you how to deploy the remote monitoring solution accelerator to your local machine for testing and development.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 03/07/2018
ms.topic: conceptual
ms.openlocfilehash: 21bc8c27a44c940279b0c5bdcdbe04e579dc4bfa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865998"
---
# <a name="deploy-the-remote-monitoring-solution-accelerator-locally"></a><span data-ttu-id="f3e87-103">Deploy the Remote Monitoring solution accelerator locally</span><span class="sxs-lookup"><span data-stu-id="f3e87-103">Deploy the Remote Monitoring solution accelerator locally</span></span>

<span data-ttu-id="f3e87-104">This article shows you how to deploy the Remote Monitoring solution accelerator to your local machine for testing and development.</span><span class="sxs-lookup"><span data-stu-id="f3e87-104">This article shows you how to deploy the Remote Monitoring solution accelerator to your local machine for testing and development.</span></span> <span data-ttu-id="f3e87-105">This approach deploys the microservices to a local Docker container and uses IoT Hub, Cosmos DB, and Azure storage services in the cloud.</span><span class="sxs-lookup"><span data-stu-id="f3e87-105">This approach deploys the microservices to a local Docker container and uses IoT Hub, Cosmos DB, and Azure storage services in the cloud.</span></span> <span data-ttu-id="f3e87-106">You use the solution accelerators (PCS) CLI to deploy the Azure cloud services.</span><span class="sxs-lookup"><span data-stu-id="f3e87-106">You use the solution accelerators (PCS) CLI to deploy the Azure cloud services.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3e87-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f3e87-107">Prerequisites</span></span>

<span data-ttu-id="f3e87-108">To deploy the Azure services used by the Remote Monitoring solution accelerator, you need an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f3e87-108">To deploy the Azure services used by the Remote Monitoring solution accelerator, you need an active Azure subscription.</span></span>

<span data-ttu-id="f3e87-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="f3e87-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f3e87-110">For details, see [Azure Free Trial](http://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3e87-110">For details, see [Azure Free Trial](http://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="f3e87-111">To complete the local deployment, you need the following tools installed on your local development machine:</span><span class="sxs-lookup"><span data-stu-id="f3e87-111">To complete the local deployment, you need the following tools installed on your local development machine:</span></span>

* [<span data-ttu-id="f3e87-112">Git</span><span class="sxs-lookup"><span data-stu-id="f3e87-112">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="f3e87-113">Docker</span><span class="sxs-lookup"><span data-stu-id="f3e87-113">Docker</span></span>](https://www.docker.com)
* [<span data-ttu-id="f3e87-114">Docker compose</span><span class="sxs-lookup"><span data-stu-id="f3e87-114">Docker compose</span></span>](https://docs.docker.com/compose/install/)
* <span data-ttu-id="f3e87-115">[Node.js](https://nodejs.org/) - this software is a prerequisite for the PCS CLI.</span><span class="sxs-lookup"><span data-stu-id="f3e87-115">[Node.js](https://nodejs.org/) - this software is a prerequisite for the PCS CLI.</span></span>
* <span data-ttu-id="f3e87-116">PCS CLI</span><span class="sxs-lookup"><span data-stu-id="f3e87-116">PCS CLI</span></span>
* <span data-ttu-id="f3e87-117">Local repository of the source code</span><span class="sxs-lookup"><span data-stu-id="f3e87-117">Local repository of the source code</span></span>

> [!NOTE]
> <span data-ttu-id="f3e87-118">These tools are available on many platforms, including Windows, Linux, and iOS.</span><span class="sxs-lookup"><span data-stu-id="f3e87-118">These tools are available on many platforms, including Windows, Linux, and iOS.</span></span>

### <a name="install-the-pcs-cli"></a><span data-ttu-id="f3e87-119">Install the PCS CLI</span><span class="sxs-lookup"><span data-stu-id="f3e87-119">Install the PCS CLI</span></span>

<span data-ttu-id="f3e87-120">To install the PCS CLI via npm, run the following command in your command-line environment:</span><span class="sxs-lookup"><span data-stu-id="f3e87-120">To install the PCS CLI via npm, run the following command in your command-line environment:</span></span>

```cmd/sh
npm install iot-solutions -g
```

<span data-ttu-id="f3e87-121">For more information about the CLI, see [How to use the CLI](https://github.com/Azure/pcs-cli/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="f3e87-121">For more information about the CLI, see [How to use the CLI](https://github.com/Azure/pcs-cli/blob/master/README.md).</span></span>

### <a name="download-the-source-code"></a><span data-ttu-id="f3e87-122">Download the source code</span><span class="sxs-lookup"><span data-stu-id="f3e87-122">Download the source code</span></span>

 <span data-ttu-id="f3e87-123">The Remote Monitoring source code repository includes the Docker configuration files you need to download, configure, and run the Docker images that contain the microservices.</span><span class="sxs-lookup"><span data-stu-id="f3e87-123">The Remote Monitoring source code repository includes the Docker configuration files you need to download, configure, and run the Docker images that contain the microservices.</span></span> <span data-ttu-id="f3e87-124">To clone and create a local version of the repository, navigate to a suitable folder on your local machine through your favorite command line or terminal and run one of the following commands:</span><span class="sxs-lookup"><span data-stu-id="f3e87-124">To clone and create a local version of the repository, navigate to a suitable folder on your local machine through your favorite command line or terminal and run one of the following commands:</span></span>

<span data-ttu-id="f3e87-125">To install the Java implementations of the microservices, run:</span><span class="sxs-lookup"><span data-stu-id="f3e87-125">To install the Java implementations of the microservices, run:</span></span>

```cmd/sh
git clone --recursive https://github.com/Azure/azure-iot-pcs-remote-monitoring-java
```

<span data-ttu-id="f3e87-126">To install the .Net implementations of the microservices, run:</span><span class="sxs-lookup"><span data-stu-id="f3e87-126">To install the .Net implementations of the microservices, run:</span></span>

```cmd\sh
git clone --recursive https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet
```

<span data-ttu-id="f3e87-127">Remote Monioring Preconfigured Solution repo & submodules [ [Java](https://github.com/Azure/azure-iot-pcs-remote-monitoring-java) | [.Net](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet) ]</span><span class="sxs-lookup"><span data-stu-id="f3e87-127">Remote Monioring Preconfigured Solution repo & submodules [ [Java](https://github.com/Azure/azure-iot-pcs-remote-monitoring-java) | [.Net](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet) ]</span></span>

> [!NOTE]
> <span data-ttu-id="f3e87-128">These commands download the source code for all the microservices.</span><span class="sxs-lookup"><span data-stu-id="f3e87-128">These commands download the source code for all the microservices.</span></span> <span data-ttu-id="f3e87-129">Although you don't need the source code to run the microservices in Docker, the source code is useful if you later plan to modify the preconfigured solution and test your changes locally.</span><span class="sxs-lookup"><span data-stu-id="f3e87-129">Although you don't need the source code to run the microservices in Docker, the source code is useful if you later plan to modify the preconfigured solution and test your changes locally.</span></span>

## <a name="deploy-the-azure-services"></a><span data-ttu-id="f3e87-130">Deploy the Azure services</span><span class="sxs-lookup"><span data-stu-id="f3e87-130">Deploy the Azure services</span></span>

<span data-ttu-id="f3e87-131">Although this article shows you how to run the microservices locally, they depend on three Azure services running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="f3e87-131">Although this article shows you how to run the microservices locally, they depend on three Azure services running in the cloud.</span></span> <span data-ttu-id="f3e87-132">You can deploy these Azure services [manually through the Azure portal](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Manual-steps-to-create-azure-resources-for-local-setup), or use the PCS CLI.</span><span class="sxs-lookup"><span data-stu-id="f3e87-132">You can deploy these Azure services [manually through the Azure portal](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Manual-steps-to-create-azure-resources-for-local-setup), or use the PCS CLI.</span></span> <span data-ttu-id="f3e87-133">This article shows you how to use the `pcs` tool.</span><span class="sxs-lookup"><span data-stu-id="f3e87-133">This article shows you how to use the `pcs` tool.</span></span>

### <a name="sign-in-to-the-cli"></a><span data-ttu-id="f3e87-134">Sign in to the CLI</span><span class="sxs-lookup"><span data-stu-id="f3e87-134">Sign in to the CLI</span></span>

<span data-ttu-id="f3e87-135">Before you can deploy the solution accelerator, you must sign in to your Azure subscription using the CLI as follows:</span><span class="sxs-lookup"><span data-stu-id="f3e87-135">Before you can deploy the solution accelerator, you must sign in to your Azure subscription using the CLI as follows:</span></span>

```cmd/sh
pcs login
```

<span data-ttu-id="f3e87-136">Follow the on-screen instructions to complete the sign-in process.</span><span class="sxs-lookup"><span data-stu-id="f3e87-136">Follow the on-screen instructions to complete the sign-in process.</span></span> <span data-ttu-id="f3e87-137">Make sure that you don't click anywhere in the inside the CLI or the login can fail.</span><span class="sxs-lookup"><span data-stu-id="f3e87-137">Make sure that you don't click anywhere in the inside the CLI or the login can fail.</span></span> <span data-ttu-id="f3e87-138">You will see a successful login message in the CLI if you have completed login.</span><span class="sxs-lookup"><span data-stu-id="f3e87-138">You will see a successful login message in the CLI if you have completed login.</span></span> 

### <a name="run-a-local-deployment"></a><span data-ttu-id="f3e87-139">Run a local deployment</span><span class="sxs-lookup"><span data-stu-id="f3e87-139">Run a local deployment</span></span>

<span data-ttu-id="f3e87-140">Use the following command to start the local deployment.</span><span class="sxs-lookup"><span data-stu-id="f3e87-140">Use the following command to start the local deployment.</span></span> <span data-ttu-id="f3e87-141">This will create the required azure resources and print out environment variables to the console.</span><span class="sxs-lookup"><span data-stu-id="f3e87-141">This will create the required azure resources and print out environment variables to the console.</span></span> 

```cmd/pcs
pcs -s local
```

<span data-ttu-id="f3e87-142">The script prompts you for the following information:</span><span class="sxs-lookup"><span data-stu-id="f3e87-142">The script prompts you for the following information:</span></span>

* <span data-ttu-id="f3e87-143">A solution name.</span><span class="sxs-lookup"><span data-stu-id="f3e87-143">A solution name.</span></span>
* <span data-ttu-id="f3e87-144">The Azure subscription to use.</span><span class="sxs-lookup"><span data-stu-id="f3e87-144">The Azure subscription to use.</span></span>
* <span data-ttu-id="f3e87-145">The location of the Azure datacenter to use.</span><span class="sxs-lookup"><span data-stu-id="f3e87-145">The location of the Azure datacenter to use.</span></span>

> [!NOTE]
> <span data-ttu-id="f3e87-146">The script creates an IoT Hub instance, a Cosmos DB instance, and an Azure storage account in a resource group in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f3e87-146">The script creates an IoT Hub instance, a Cosmos DB instance, and an Azure storage account in a resource group in your Azure subscription.</span></span> <span data-ttu-id="f3e87-147">The name of the resource group is the name of the solution you chose when you ran the `pcs` tool above.</span><span class="sxs-lookup"><span data-stu-id="f3e87-147">The name of the resource group is the name of the solution you chose when you ran the `pcs` tool above.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f3e87-148">The script takes several minutes to run.</span><span class="sxs-lookup"><span data-stu-id="f3e87-148">The script takes several minutes to run.</span></span> <span data-ttu-id="f3e87-149">When it completes, you see a message `Copy the following environment variables to /scripts/local/.env file:`.</span><span class="sxs-lookup"><span data-stu-id="f3e87-149">When it completes, you see a message `Copy the following environment variables to /scripts/local/.env file:`.</span></span> <span data-ttu-id="f3e87-150">Copy down the environment variable definitions following the message, you will use them in a later step.</span><span class="sxs-lookup"><span data-stu-id="f3e87-150">Copy down the environment variable definitions following the message, you will use them in a later step.</span></span>

## <a name="run-the-microservices-in-docker"></a><span data-ttu-id="f3e87-151">Run the microservices in Docker</span><span class="sxs-lookup"><span data-stu-id="f3e87-151">Run the microservices in Docker</span></span>

<span data-ttu-id="f3e87-152">To run the microservices in Docker, first edit the **scripts\\local\\.env** file in your local copy of the repository you cloned in an earlier step above.</span><span class="sxs-lookup"><span data-stu-id="f3e87-152">To run the microservices in Docker, first edit the **scripts\\local\\.env** file in your local copy of the repository you cloned in an earlier step above.</span></span> <span data-ttu-id="f3e87-153">Replace the entire contents of the file with the environment variable definitions you made a note of when you ran the `pcs` command in the last step.</span><span class="sxs-lookup"><span data-stu-id="f3e87-153">Replace the entire contents of the file with the environment variable definitions you made a note of when you ran the `pcs` command in the last step.</span></span> <span data-ttu-id="f3e87-154">These environment variables enable the microservices in the Docker container to connect to the Azure services created by the `pcs` tool.</span><span class="sxs-lookup"><span data-stu-id="f3e87-154">These environment variables enable the microservices in the Docker container to connect to the Azure services created by the `pcs` tool.</span></span>

<span data-ttu-id="f3e87-155">To run the solution accelerator, navigate to the **scripts\local** folder in your command-line environment and run the following command:</span><span class="sxs-lookup"><span data-stu-id="f3e87-155">To run the solution accelerator, navigate to the **scripts\local** folder in your command-line environment and run the following command:</span></span>

```cmd\sh
docker-compose up
```

<span data-ttu-id="f3e87-156">The first time you run this command, Docker downloads the microservice images from Docker hub to build the containers locally.</span><span class="sxs-lookup"><span data-stu-id="f3e87-156">The first time you run this command, Docker downloads the microservice images from Docker hub to build the containers locally.</span></span> <span data-ttu-id="f3e87-157">On subsequent runs, Docker runs the containers immediately.</span><span class="sxs-lookup"><span data-stu-id="f3e87-157">On subsequent runs, Docker runs the containers immediately.</span></span>

<span data-ttu-id="f3e87-158">You can use a separate shell to view the logs from the container.</span><span class="sxs-lookup"><span data-stu-id="f3e87-158">You can use a separate shell to view the logs from the container.</span></span> <span data-ttu-id="f3e87-159">First find the container ID using the `docker ps -a` command.</span><span class="sxs-lookup"><span data-stu-id="f3e87-159">First find the container ID using the `docker ps -a` command.</span></span> <span data-ttu-id="f3e87-160">Then use `docker logs {container-id} --tail 1000` to view the last 1000 log entries for the specified container.</span><span class="sxs-lookup"><span data-stu-id="f3e87-160">Then use `docker logs {container-id} --tail 1000` to view the last 1000 log entries for the specified container.</span></span>

<span data-ttu-id="f3e87-161">To access the Remote Monitoring solution dashboard, navigate to [http://localhost:8080](http://localhost:8080) in your browser.</span><span class="sxs-lookup"><span data-stu-id="f3e87-161">To access the Remote Monitoring solution dashboard, navigate to [http://localhost:8080](http://localhost:8080) in your browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="f3e87-162">Clean up</span><span class="sxs-lookup"><span data-stu-id="f3e87-162">Clean up</span></span>

<span data-ttu-id="f3e87-163">To avoid unnecessary charges, when you have finished your testing, remove the cloud services from your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f3e87-163">To avoid unnecessary charges, when you have finished your testing, remove the cloud services from your Azure subscription.</span></span> <span data-ttu-id="f3e87-164">The easiest way to remove the services is to navigate to the [Azure portal](https://ms.portal.azure.com) and delete the resource group you created via the `pcs` tool.</span><span class="sxs-lookup"><span data-stu-id="f3e87-164">The easiest way to remove the services is to navigate to the [Azure portal](https://ms.portal.azure.com) and delete the resource group you created via the `pcs` tool.</span></span>

<span data-ttu-id="f3e87-165">Use the `docker-compose down --rmi all` command to remove the Docker images and free up space on your local machine.</span><span class="sxs-lookup"><span data-stu-id="f3e87-165">Use the `docker-compose down --rmi all` command to remove the Docker images and free up space on your local machine.</span></span> <span data-ttu-id="f3e87-166">You can also delete the local copy of the Remote Monitoring repository created when you cloned the source code from GitHub.</span><span class="sxs-lookup"><span data-stu-id="f3e87-166">You can also delete the local copy of the Remote Monitoring repository created when you cloned the source code from GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3e87-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3e87-167">Next steps</span></span>

<span data-ttu-id="f3e87-168">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="f3e87-168">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3e87-169">Set up a local development environment</span><span class="sxs-lookup"><span data-stu-id="f3e87-169">Set up a local development environment</span></span>
> * <span data-ttu-id="f3e87-170">Configure the solution accelerator</span><span class="sxs-lookup"><span data-stu-id="f3e87-170">Configure the solution accelerator</span></span>
> * <span data-ttu-id="f3e87-171">Deploy the solution accelerator</span><span class="sxs-lookup"><span data-stu-id="f3e87-171">Deploy the solution accelerator</span></span>
> * <span data-ttu-id="f3e87-172">Sign in to the solution accelerator</span><span class="sxs-lookup"><span data-stu-id="f3e87-172">Sign in to the solution accelerator</span></span>

<span data-ttu-id="f3e87-173">Now that you have deployed the Remote Monitoring solution, the next step is to [explore the capabilities of the solution dashboard](quickstart-remote-monitoring-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f3e87-173">Now that you have deployed the Remote Monitoring solution, the next step is to [explore the capabilities of the solution dashboard](quickstart-remote-monitoring-deploy.md).</span></span>

<!-- Next tutorials in the sequence -->