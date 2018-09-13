---
title: Deploy the Java Remote Monitoring solution - Azure | Microsoft Docs
description: This tutorial shows you how to provision the Remote Monitoring solution accelerator using the CLI.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 01/29/2018
ms.topic: conceptual
ms.openlocfilehash: dd696330c9ee78ef84ac9fcf85946c837ad5b824
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857572"
---
# <a name="deploy-the-remote-monitoring-solution-accelerator-using-the-cli"></a><span data-ttu-id="77a81-103">Deploy the Remote Monitoring solution accelerator using the CLI</span><span class="sxs-lookup"><span data-stu-id="77a81-103">Deploy the Remote Monitoring solution accelerator using the CLI</span></span>

<span data-ttu-id="77a81-104">This tutorial shows you how to provision the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="77a81-104">This tutorial shows you how to provision the Remote Monitoring solution accelerator.</span></span> <span data-ttu-id="77a81-105">You deploy the solution using the CLI.</span><span class="sxs-lookup"><span data-stu-id="77a81-105">You deploy the solution using the CLI.</span></span> <span data-ttu-id="77a81-106">You can also deploy the solution using the web-based UI at azureiotsuite.com, to learn about this option see [Deploy the Remote Monitoring solution accelerator](quickstart-remote-monitoring-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="77a81-106">You can also deploy the solution using the web-based UI at azureiotsuite.com, to learn about this option see [Deploy the Remote Monitoring solution accelerator](quickstart-remote-monitoring-deploy.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77a81-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="77a81-107">Prerequisites</span></span>

<span data-ttu-id="77a81-108">To deploy the Remote Monitoring solution accelerator, you need an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="77a81-108">To deploy the Remote Monitoring solution accelerator, you need an active Azure subscription.</span></span>

<span data-ttu-id="77a81-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="77a81-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="77a81-110">For details, see [Azure Free Trial](http://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77a81-110">For details, see [Azure Free Trial](http://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="77a81-111">To run the CLI, you need [Node.js](https://nodejs.org/) installed on your local machine.</span><span class="sxs-lookup"><span data-stu-id="77a81-111">To run the CLI, you need [Node.js](https://nodejs.org/) installed on your local machine.</span></span>

## <a name="install-the-cli"></a><span data-ttu-id="77a81-112">Install the CLI</span><span class="sxs-lookup"><span data-stu-id="77a81-112">Install the CLI</span></span>

<span data-ttu-id="77a81-113">To install the CLI, run the following command in your command-line environment:</span><span class="sxs-lookup"><span data-stu-id="77a81-113">To install the CLI, run the following command in your command-line environment:</span></span>

```cmd/sh
npm install iot-solutions -g
```

## <a name="sign-in-to-the-cli"></a><span data-ttu-id="77a81-114">Sign in to the CLI</span><span class="sxs-lookup"><span data-stu-id="77a81-114">Sign in to the CLI</span></span>

<span data-ttu-id="77a81-115">Before you can deploy the solution accelerator, you must sign in to your Azure subscription using the CLI as follows:</span><span class="sxs-lookup"><span data-stu-id="77a81-115">Before you can deploy the solution accelerator, you must sign in to your Azure subscription using the CLI as follows:</span></span>

```cmd/sh
pcs login
```

<span data-ttu-id="77a81-116">Follow the on-screen instructions to complete the sign-in process.</span><span class="sxs-lookup"><span data-stu-id="77a81-116">Follow the on-screen instructions to complete the sign-in process.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="77a81-117">Deployment options</span><span class="sxs-lookup"><span data-stu-id="77a81-117">Deployment options</span></span>

<span data-ttu-id="77a81-118">When you deploy the solution accelerator, there are several options that configure the deployment process:</span><span class="sxs-lookup"><span data-stu-id="77a81-118">When you deploy the solution accelerator, there are several options that configure the deployment process:</span></span>

| <span data-ttu-id="77a81-119">Option</span><span class="sxs-lookup"><span data-stu-id="77a81-119">Option</span></span> | <span data-ttu-id="77a81-120">Values</span><span class="sxs-lookup"><span data-stu-id="77a81-120">Values</span></span> | <span data-ttu-id="77a81-121">Description</span><span class="sxs-lookup"><span data-stu-id="77a81-121">Description</span></span> |
| ------ | ------ | ----------- |
| <span data-ttu-id="77a81-122">SKU</span><span class="sxs-lookup"><span data-stu-id="77a81-122">SKU</span></span>    | <span data-ttu-id="77a81-123">`basic`, `standard`, `local`</span><span class="sxs-lookup"><span data-stu-id="77a81-123">`basic`, `standard`, `local`</span></span> | <span data-ttu-id="77a81-124">A _basic_ deployment is intended for test and demonstrations, it deploys all the microservices to a single virtual machine.</span><span class="sxs-lookup"><span data-stu-id="77a81-124">A _basic_ deployment is intended for test and demonstrations, it deploys all the microservices to a single virtual machine.</span></span> <span data-ttu-id="77a81-125">A _standard_ deployment is intended for production, it deploys the microservices to multiple virtual machines.</span><span class="sxs-lookup"><span data-stu-id="77a81-125">A _standard_ deployment is intended for production, it deploys the microservices to multiple virtual machines.</span></span> <span data-ttu-id="77a81-126">A _local_ deployment configures a Docker container to run the microservices on your local machine, and uses Azure services, such as storage and Cosmos DB, in the cloud.</span><span class="sxs-lookup"><span data-stu-id="77a81-126">A _local_ deployment configures a Docker container to run the microservices on your local machine, and uses Azure services, such as storage and Cosmos DB, in the cloud.</span></span> |
| <span data-ttu-id="77a81-127">Runtime</span><span class="sxs-lookup"><span data-stu-id="77a81-127">Runtime</span></span> | <span data-ttu-id="77a81-128">`dotnet`, `java`</span><span class="sxs-lookup"><span data-stu-id="77a81-128">`dotnet`, `java`</span></span> | <span data-ttu-id="77a81-129">Selects the language implementation of the microservices.</span><span class="sxs-lookup"><span data-stu-id="77a81-129">Selects the language implementation of the microservices.</span></span> |

<span data-ttu-id="77a81-130">To learn about how to use the local deployment, see [Running the Remote Monitoring solution locally](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Running-the-Remote-Monitoring-Solution-Locally#deploy-azure-services-and-set-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="77a81-130">To learn about how to use the local deployment, see [Running the Remote Monitoring solution locally](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Running-the-Remote-Monitoring-Solution-Locally#deploy-azure-services-and-set-environment-variables).</span></span>

## <a name="basic-vs-standard-deployments"></a><span data-ttu-id="77a81-131">Basic vs. Standard Deployments</span><span class="sxs-lookup"><span data-stu-id="77a81-131">Basic vs. Standard Deployments</span></span>

### <a name="basic"></a><span data-ttu-id="77a81-132">Basic</span><span class="sxs-lookup"><span data-stu-id="77a81-132">Basic</span></span>
<span data-ttu-id="77a81-133">Basic deployment is geared toward showcasing the solution.</span><span class="sxs-lookup"><span data-stu-id="77a81-133">Basic deployment is geared toward showcasing the solution.</span></span> <span data-ttu-id="77a81-134">To reduce the cost of this demonstration, all the microservices are deployed in a single virtual machine; this is not considered a production-ready architecture.</span><span class="sxs-lookup"><span data-stu-id="77a81-134">To reduce the cost of this demonstration, all the microservices are deployed in a single virtual machine; this is not considered a production-ready architecture.</span></span>

<span data-ttu-id="77a81-135">Our Standard deployment option should be used when you are ready to customize a production-ready architecture, built for scale and extensibility.</span><span class="sxs-lookup"><span data-stu-id="77a81-135">Our Standard deployment option should be used when you are ready to customize a production-ready architecture, built for scale and extensibility.</span></span>

<span data-ttu-id="77a81-136">Creating a Basic solution will result in the following Azure services being provisioned into your Azure subscription at cost:</span><span class="sxs-lookup"><span data-stu-id="77a81-136">Creating a Basic solution will result in the following Azure services being provisioned into your Azure subscription at cost:</span></span> 

| <span data-ttu-id="77a81-137">Count</span><span class="sxs-lookup"><span data-stu-id="77a81-137">Count</span></span> | <span data-ttu-id="77a81-138">Resource</span><span class="sxs-lookup"><span data-stu-id="77a81-138">Resource</span></span>                       | <span data-ttu-id="77a81-139">Type</span><span class="sxs-lookup"><span data-stu-id="77a81-139">Type</span></span>         | <span data-ttu-id="77a81-140">Used For</span><span class="sxs-lookup"><span data-stu-id="77a81-140">Used For</span></span> |
|-------|--------------------------------|--------------|----------|
| <span data-ttu-id="77a81-141">1</span><span class="sxs-lookup"><span data-stu-id="77a81-141">1</span></span>     | [<span data-ttu-id="77a81-142">Linux Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="77a81-142">Linux Virtual Machine</span></span>](https://azure.microsoft.com/services/virtual-machines/) | <span data-ttu-id="77a81-143">Standard D1 V2</span><span class="sxs-lookup"><span data-stu-id="77a81-143">Standard D1 V2</span></span>  | <span data-ttu-id="77a81-144">Hosting microservices</span><span class="sxs-lookup"><span data-stu-id="77a81-144">Hosting microservices</span></span> |
| <span data-ttu-id="77a81-145">1</span><span class="sxs-lookup"><span data-stu-id="77a81-145">1</span></span>     | [<span data-ttu-id="77a81-146">Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="77a81-146">Azure IoT Hub</span></span>](https://azure.microsoft.com/services/iot-hub/)                  | <span data-ttu-id="77a81-147">S1 – Standard tier</span><span class="sxs-lookup"><span data-stu-id="77a81-147">S1 – Standard tier</span></span> | <span data-ttu-id="77a81-148">Device management and communication</span><span class="sxs-lookup"><span data-stu-id="77a81-148">Device management and communication</span></span> |
| <span data-ttu-id="77a81-149">1</span><span class="sxs-lookup"><span data-stu-id="77a81-149">1</span></span>     | [<span data-ttu-id="77a81-150">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="77a81-150">Azure Cosmos DB</span></span>](https://azure.microsoft.com/services/cosmos-db/)              | <span data-ttu-id="77a81-151">Standard</span><span class="sxs-lookup"><span data-stu-id="77a81-151">Standard</span></span>        | <span data-ttu-id="77a81-152">Storing configuration data, and device telemetry like rules, alarms, and messages</span><span class="sxs-lookup"><span data-stu-id="77a81-152">Storing configuration data, and device telemetry like rules, alarms, and messages</span></span> |  
| <span data-ttu-id="77a81-153">1</span><span class="sxs-lookup"><span data-stu-id="77a81-153">1</span></span>     | [<span data-ttu-id="77a81-154">Azure Storage Account</span><span class="sxs-lookup"><span data-stu-id="77a81-154">Azure Storage Account</span></span>](https://docs.microsoft.com/azure/storage/common/storage-introduction#types-of-storage-accounts)  | <span data-ttu-id="77a81-155">Standard</span><span class="sxs-lookup"><span data-stu-id="77a81-155">Standard</span></span>        | <span data-ttu-id="77a81-156">Storage for VM and streaming checkpoints</span><span class="sxs-lookup"><span data-stu-id="77a81-156">Storage for VM and streaming checkpoints</span></span> |
| <span data-ttu-id="77a81-157">1</span><span class="sxs-lookup"><span data-stu-id="77a81-157">1</span></span>     | [<span data-ttu-id="77a81-158">Web Application</span><span class="sxs-lookup"><span data-stu-id="77a81-158">Web Application</span></span>](https://azure.microsoft.com/services/app-service/web/)        |                 | <span data-ttu-id="77a81-159">Hosting front-end web application</span><span class="sxs-lookup"><span data-stu-id="77a81-159">Hosting front-end web application</span></span> |

### <a name="standard"></a><span data-ttu-id="77a81-160">Standard</span><span class="sxs-lookup"><span data-stu-id="77a81-160">Standard</span></span>
<span data-ttu-id="77a81-161">The standard deployment is a production-ready deployment a developer can customize and extend to meet their needs.</span><span class="sxs-lookup"><span data-stu-id="77a81-161">The standard deployment is a production-ready deployment a developer can customize and extend to meet their needs.</span></span> <span data-ttu-id="77a81-162">For reliability and scale, application microservices are built as Docker containers and deployed using an orchestrator ([Kubernetes](https://kubernetes.io/) by default).</span><span class="sxs-lookup"><span data-stu-id="77a81-162">For reliability and scale, application microservices are built as Docker containers and deployed using an orchestrator ([Kubernetes](https://kubernetes.io/) by default).</span></span> <span data-ttu-id="77a81-163">The orchestrator is responsible for deployment, scaling, and management of the application.</span><span class="sxs-lookup"><span data-stu-id="77a81-163">The orchestrator is responsible for deployment, scaling, and management of the application.</span></span>

<span data-ttu-id="77a81-164">Creating a Standard solution will result in the following Azure services being provisioned into your Azure subscription at cost:</span><span class="sxs-lookup"><span data-stu-id="77a81-164">Creating a Standard solution will result in the following Azure services being provisioned into your Azure subscription at cost:</span></span>

| <span data-ttu-id="77a81-165">Count</span><span class="sxs-lookup"><span data-stu-id="77a81-165">Count</span></span> | <span data-ttu-id="77a81-166">Resource</span><span class="sxs-lookup"><span data-stu-id="77a81-166">Resource</span></span>                                     | <span data-ttu-id="77a81-167">SKU / Size</span><span class="sxs-lookup"><span data-stu-id="77a81-167">SKU / Size</span></span>      | <span data-ttu-id="77a81-168">Used For</span><span class="sxs-lookup"><span data-stu-id="77a81-168">Used For</span></span> |
|-------|----------------------------------------------|-----------------|----------|
| <span data-ttu-id="77a81-169">4</span><span class="sxs-lookup"><span data-stu-id="77a81-169">4</span></span>     | [<span data-ttu-id="77a81-170">Linux Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="77a81-170">Linux Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)   | <span data-ttu-id="77a81-171">Standard D2 V2</span><span class="sxs-lookup"><span data-stu-id="77a81-171">Standard D2 V2</span></span>  | <span data-ttu-id="77a81-172">1 master and 3 agents for hosting microservices with redundancy</span><span class="sxs-lookup"><span data-stu-id="77a81-172">1 master and 3 agents for hosting microservices with redundancy</span></span> |
| <span data-ttu-id="77a81-173">1</span><span class="sxs-lookup"><span data-stu-id="77a81-173">1</span></span>     | [<span data-ttu-id="77a81-174">Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="77a81-174">Azure Container Service</span></span>](https://azure.microsoft.com/services/container-service/) |                 | <span data-ttu-id="77a81-175">[Kubernetes](https://kubernetes.io) orchestrator</span><span class="sxs-lookup"><span data-stu-id="77a81-175">[Kubernetes](https://kubernetes.io) orchestrator</span></span> |
| <span data-ttu-id="77a81-176">1</span><span class="sxs-lookup"><span data-stu-id="77a81-176">1</span></span>     | <span data-ttu-id="77a81-177">[Azure IoT Hub][https://azure.microsoft.com/services/iot-hub/]</span><span class="sxs-lookup"><span data-stu-id="77a81-177">[Azure IoT Hub][https://azure.microsoft.com/services/iot-hub/]</span></span>                     | <span data-ttu-id="77a81-178">S2 – Standard tier</span><span class="sxs-lookup"><span data-stu-id="77a81-178">S2 – Standard tier</span></span> | <span data-ttu-id="77a81-179">Device management, command and control</span><span class="sxs-lookup"><span data-stu-id="77a81-179">Device management, command and control</span></span> |
| <span data-ttu-id="77a81-180">1</span><span class="sxs-lookup"><span data-stu-id="77a81-180">1</span></span>     | [<span data-ttu-id="77a81-181">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="77a81-181">Azure Cosmos DB</span></span>](https://azure.microsoft.com/services/cosmos-db/)                 | <span data-ttu-id="77a81-182">Standard</span><span class="sxs-lookup"><span data-stu-id="77a81-182">Standard</span></span>        | <span data-ttu-id="77a81-183">Storing configuration data, and device telemetry like rules, alarms, and messages</span><span class="sxs-lookup"><span data-stu-id="77a81-183">Storing configuration data, and device telemetry like rules, alarms, and messages</span></span> |
| <span data-ttu-id="77a81-184">5</span><span class="sxs-lookup"><span data-stu-id="77a81-184">5</span></span>     | [<span data-ttu-id="77a81-185">Azure Storage Accounts</span><span class="sxs-lookup"><span data-stu-id="77a81-185">Azure Storage Accounts</span></span>](https://docs.microsoft.com/azure/storage/common/storage-introduction#types-of-storage-accounts)    | <span data-ttu-id="77a81-186">Standard</span><span class="sxs-lookup"><span data-stu-id="77a81-186">Standard</span></span>        | <span data-ttu-id="77a81-187">4 for VM storage, and 1 for the streaming checkpoints</span><span class="sxs-lookup"><span data-stu-id="77a81-187">4 for VM storage, and 1 for the streaming checkpoints</span></span> |
| <span data-ttu-id="77a81-188">1</span><span class="sxs-lookup"><span data-stu-id="77a81-188">1</span></span>     | [<span data-ttu-id="77a81-189">App Service</span><span class="sxs-lookup"><span data-stu-id="77a81-189">App Service</span></span>](https://azure.microsoft.com/services/app-service/web/)             | <span data-ttu-id="77a81-190">S1 Standard</span><span class="sxs-lookup"><span data-stu-id="77a81-190">S1 Standard</span></span>     | <span data-ttu-id="77a81-191">Application gateway over SSL</span><span class="sxs-lookup"><span data-stu-id="77a81-191">Application gateway over SSL</span></span> |

> <span data-ttu-id="77a81-192">Pricing information for these services can be found [here](https://azure.microsoft.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="77a81-192">Pricing information for these services can be found [here](https://azure.microsoft.com/pricing).</span></span> <span data-ttu-id="77a81-193">Usage amounts and billing details for your subscription can be found in the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="77a81-193">Usage amounts and billing details for your subscription can be found in the [Azure Portal](https://portal.azure.com/).</span></span>

## <a name="deploy-the-solution-accelerator"></a><span data-ttu-id="77a81-194">Deploy the solution accelerator</span><span class="sxs-lookup"><span data-stu-id="77a81-194">Deploy the solution accelerator</span></span>

### <a name="example-deploy-net-version"></a><span data-ttu-id="77a81-195">Example: deploy .NET version</span><span class="sxs-lookup"><span data-stu-id="77a81-195">Example: deploy .NET version</span></span>

<span data-ttu-id="77a81-196">The following example shows how to deploy the basic, .NET version of the Remote Monitoring solution accelerator:</span><span class="sxs-lookup"><span data-stu-id="77a81-196">The following example shows how to deploy the basic, .NET version of the Remote Monitoring solution accelerator:</span></span>

```cmd/sh
pcs -t remotemonitoring -s basic -r dotnet
```

### <a name="example-deploy-java-version"></a><span data-ttu-id="77a81-197">Example: deploy Java version</span><span class="sxs-lookup"><span data-stu-id="77a81-197">Example: deploy Java version</span></span>

<span data-ttu-id="77a81-198">The following example shows how to deploy the standard, Java version of the Remote Monitoring solution accelerator:</span><span class="sxs-lookup"><span data-stu-id="77a81-198">The following example shows how to deploy the standard, Java version of the Remote Monitoring solution accelerator:</span></span>

```cmd/sh
pcs -t remotemonitoring -s standard -r java
```

### <a name="pcs-command-options"></a><span data-ttu-id="77a81-199">pcs command options</span><span class="sxs-lookup"><span data-stu-id="77a81-199">pcs command options</span></span>

<span data-ttu-id="77a81-200">When you run the `pcs` command to deploy a solution, you are asked for:</span><span class="sxs-lookup"><span data-stu-id="77a81-200">When you run the `pcs` command to deploy a solution, you are asked for:</span></span>

- <span data-ttu-id="77a81-201">A name for your solution.</span><span class="sxs-lookup"><span data-stu-id="77a81-201">A name for your solution.</span></span> <span data-ttu-id="77a81-202">This name must be unique.</span><span class="sxs-lookup"><span data-stu-id="77a81-202">This name must be unique.</span></span>
- <span data-ttu-id="77a81-203">The Azure subscription to use.</span><span class="sxs-lookup"><span data-stu-id="77a81-203">The Azure subscription to use.</span></span>
- <span data-ttu-id="77a81-204">A location.</span><span class="sxs-lookup"><span data-stu-id="77a81-204">A location.</span></span>
- <span data-ttu-id="77a81-205">Credentials for the virtual machines that host the microservices.</span><span class="sxs-lookup"><span data-stu-id="77a81-205">Credentials for the virtual machines that host the microservices.</span></span> <span data-ttu-id="77a81-206">You can use these credentials to access the virtual machines for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="77a81-206">You can use these credentials to access the virtual machines for troubleshooting.</span></span>

<span data-ttu-id="77a81-207">When the `pcs` command finishes, it displays the URL of your new solution accelerator deployment.</span><span class="sxs-lookup"><span data-stu-id="77a81-207">When the `pcs` command finishes, it displays the URL of your new solution accelerator deployment.</span></span> <span data-ttu-id="77a81-208">The `pcs` command also creates a file `{deployment-name}-output.json` with additional information such as the name of the IoT Hub that was provisioned for you.</span><span class="sxs-lookup"><span data-stu-id="77a81-208">The `pcs` command also creates a file `{deployment-name}-output.json` with additional information such as the name of the IoT Hub that was provisioned for you.</span></span>

<span data-ttu-id="77a81-209">For more information about the command-line parameters, run:</span><span class="sxs-lookup"><span data-stu-id="77a81-209">For more information about the command-line parameters, run:</span></span>

```cmd/sh
pcs -h
```

<span data-ttu-id="77a81-210">For more information about the CLI, see [How to use the CLI](https://github.com/Azure/pcs-cli/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="77a81-210">For more information about the CLI, see [How to use the CLI](https://github.com/Azure/pcs-cli/blob/master/README.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="77a81-211">Next steps</span><span class="sxs-lookup"><span data-stu-id="77a81-211">Next steps</span></span>

<span data-ttu-id="77a81-212">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="77a81-212">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="77a81-213">Configure the solution accelerator</span><span class="sxs-lookup"><span data-stu-id="77a81-213">Configure the solution accelerator</span></span>
> * <span data-ttu-id="77a81-214">Deploy the solution accelerator</span><span class="sxs-lookup"><span data-stu-id="77a81-214">Deploy the solution accelerator</span></span>
> * <span data-ttu-id="77a81-215">Sign in to the solution accelerator</span><span class="sxs-lookup"><span data-stu-id="77a81-215">Sign in to the solution accelerator</span></span>

<span data-ttu-id="77a81-216">Now that you have deployed the Remote Monitoring solution, the next step is to [explore the capabilities of the solution dashboard](./quickstart-remote-monitoring-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="77a81-216">Now that you have deployed the Remote Monitoring solution, the next step is to [explore the capabilities of the solution dashboard](./quickstart-remote-monitoring-deploy.md).</span></span>

<!-- Next tutorials in the sequence -->
