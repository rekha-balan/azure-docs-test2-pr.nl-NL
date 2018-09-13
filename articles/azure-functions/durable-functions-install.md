---
title: Install the Durable Functions extension and samples - Azure
description: Learn how to install the Durable Functions extension for Azure Functions, for portal development or Visual Studio development.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 08/31/2018
ms.author: azfuncdf
ms.openlocfilehash: 3f9bdcb67628a6780e42ef16acea2b91ca9817d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871308"
---
# <a name="install-the-durable-functions-extension-and-samples-azure-functions"></a><span data-ttu-id="3cce6-103">Install the Durable Functions extension and samples (Azure Functions)</span><span class="sxs-lookup"><span data-stu-id="3cce6-103">Install the Durable Functions extension and samples (Azure Functions)</span></span>

<span data-ttu-id="3cce6-104">The [Durable Functions](durable-functions-overview.md) extension for Azure Functions is provided in the NuGet package [Microsoft.Azure.WebJobs.Extensions.DurableTask](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask).</span><span class="sxs-lookup"><span data-stu-id="3cce6-104">The [Durable Functions](durable-functions-overview.md) extension for Azure Functions is provided in the NuGet package [Microsoft.Azure.WebJobs.Extensions.DurableTask](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask).</span></span> <span data-ttu-id="3cce6-105">This article shows how to install the package and a set of samples for the following development environments:</span><span class="sxs-lookup"><span data-stu-id="3cce6-105">This article shows how to install the package and a set of samples for the following development environments:</span></span>

* <span data-ttu-id="3cce6-106">Visual Studio 2017 (Recommended for C#)</span><span class="sxs-lookup"><span data-stu-id="3cce6-106">Visual Studio 2017 (Recommended for C#)</span></span> 
* <span data-ttu-id="3cce6-107">Visual Studio Code (Recommended for JavaScript)</span><span class="sxs-lookup"><span data-stu-id="3cce6-107">Visual Studio Code (Recommended for JavaScript)</span></span>
* <span data-ttu-id="3cce6-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3cce6-108">Azure portal</span></span>

## <a name="visual-studio-2017"></a><span data-ttu-id="3cce6-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3cce6-109">Visual Studio 2017</span></span>

<span data-ttu-id="3cce6-110">Visual Studio currently provides the best experience for developing apps that use Durable Functions.</span><span class="sxs-lookup"><span data-stu-id="3cce6-110">Visual Studio currently provides the best experience for developing apps that use Durable Functions.</span></span>  <span data-ttu-id="3cce6-111">Your functions can be run locally and can also be published to Azure.</span><span class="sxs-lookup"><span data-stu-id="3cce6-111">Your functions can be run locally and can also be published to Azure.</span></span> <span data-ttu-id="3cce6-112">You can start with an empty project or with a set of sample functions.</span><span class="sxs-lookup"><span data-stu-id="3cce6-112">You can start with an empty project or with a set of sample functions.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3cce6-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3cce6-113">Prerequisites</span></span>

* <span data-ttu-id="3cce6-114">Install the [latest version of Visual Studio](https://www.visualstudio.com/downloads/) (version 15.6 or greater).</span><span class="sxs-lookup"><span data-stu-id="3cce6-114">Install the [latest version of Visual Studio](https://www.visualstudio.com/downloads/) (version 15.6 or greater).</span></span> <span data-ttu-id="3cce6-115">Include the **Azure development** workload in your setup options.</span><span class="sxs-lookup"><span data-stu-id="3cce6-115">Include the **Azure development** workload in your setup options.</span></span>

### <a name="start-with-sample-functions"></a><span data-ttu-id="3cce6-116">Start with sample functions</span><span class="sxs-lookup"><span data-stu-id="3cce6-116">Start with sample functions</span></span> 

1. <span data-ttu-id="3cce6-117">Download the [Sample App .zip file for Visual Studio](https://azure.github.io/azure-functions-durable-extension/files/VSDFSampleApp.zip).</span><span class="sxs-lookup"><span data-stu-id="3cce6-117">Download the [Sample App .zip file for Visual Studio](https://azure.github.io/azure-functions-durable-extension/files/VSDFSampleApp.zip).</span></span> <span data-ttu-id="3cce6-118">You don't need to add the NuGet reference because the sample project already has it.</span><span class="sxs-lookup"><span data-stu-id="3cce6-118">You don't need to add the NuGet reference because the sample project already has it.</span></span>
2. <span data-ttu-id="3cce6-119">Install and run [Azure Storage Emulator](https://docs.microsoft.com/azure/storage/storage-use-emulator) version 5.6 or later.</span><span class="sxs-lookup"><span data-stu-id="3cce6-119">Install and run [Azure Storage Emulator](https://docs.microsoft.com/azure/storage/storage-use-emulator) version 5.6 or later.</span></span> <span data-ttu-id="3cce6-120">Alternatively, you can update the *local.appsettings.json* file with real Azure Storage connection strings.</span><span class="sxs-lookup"><span data-stu-id="3cce6-120">Alternatively, you can update the *local.appsettings.json* file with real Azure Storage connection strings.</span></span>
3. <span data-ttu-id="3cce6-121">Open the project in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3cce6-121">Open the project in Visual Studio 2017.</span></span> 
4. <span data-ttu-id="3cce6-122">For instructions on how to run the sample, start with [Function chaining - Hello sequence sample](durable-functions-sequence.md).</span><span class="sxs-lookup"><span data-stu-id="3cce6-122">For instructions on how to run the sample, start with [Function chaining - Hello sequence sample](durable-functions-sequence.md).</span></span> <span data-ttu-id="3cce6-123">The sample can be run locally or published to Azure.</span><span class="sxs-lookup"><span data-stu-id="3cce6-123">The sample can be run locally or published to Azure.</span></span>

### <a name="start-with-an-empty-project"></a><span data-ttu-id="3cce6-124">Start with an empty project</span><span class="sxs-lookup"><span data-stu-id="3cce6-124">Start with an empty project</span></span>
 
<span data-ttu-id="3cce6-125">Follow the same directions as for starting with the sample, but do the following steps instead of downloading the *.zip* file:</span><span class="sxs-lookup"><span data-stu-id="3cce6-125">Follow the same directions as for starting with the sample, but do the following steps instead of downloading the *.zip* file:</span></span>

1. <span data-ttu-id="3cce6-126">Create a Function App project.</span><span class="sxs-lookup"><span data-stu-id="3cce6-126">Create a Function App project.</span></span>
2. <span data-ttu-id="3cce6-127">Search for the following NuGet package reference using *Manage NuGet Packages* and add it to the project: Microsoft.Azure.WebJobs.Extensions.DurableTask v1.6.0</span><span class="sxs-lookup"><span data-stu-id="3cce6-127">Search for the following NuGet package reference using *Manage NuGet Packages* and add it to the project: Microsoft.Azure.WebJobs.Extensions.DurableTask v1.6.0</span></span>
   
## <a name="visual-studio-code"></a><span data-ttu-id="3cce6-128">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3cce6-128">Visual Studio Code</span></span>

<span data-ttu-id="3cce6-129">Visual Studio Code provides a local development experience covering all major platforms - Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="3cce6-129">Visual Studio Code provides a local development experience covering all major platforms - Windows, macOS, and Linux.</span></span>  <span data-ttu-id="3cce6-130">Your functions can be run locally and also be published to Azure.</span><span class="sxs-lookup"><span data-stu-id="3cce6-130">Your functions can be run locally and also be published to Azure.</span></span> <span data-ttu-id="3cce6-131">You can start with an empty project or with a set of sample functions.</span><span class="sxs-lookup"><span data-stu-id="3cce6-131">You can start with an empty project or with a set of sample functions.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3cce6-132">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3cce6-132">Prerequisites</span></span>

* <span data-ttu-id="3cce6-133">Install the [latest version of Visual Studio Code](https://code.visualstudio.com/Download)</span><span class="sxs-lookup"><span data-stu-id="3cce6-133">Install the [latest version of Visual Studio Code](https://code.visualstudio.com/Download)</span></span> 

* <span data-ttu-id="3cce6-134">Follow the instructions under "Install the Azure Functions Core Tools" at [Code and test Azure Functions locally](https://docs.microsoft.com/azure/azure-functions/functions-run-local)</span><span class="sxs-lookup"><span data-stu-id="3cce6-134">Follow the instructions under "Install the Azure Functions Core Tools" at [Code and test Azure Functions locally](https://docs.microsoft.com/azure/azure-functions/functions-run-local)</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="3cce6-135">If you already have the Azure Functions Cross Platform Tools, update them to the latest available version.</span><span class="sxs-lookup"><span data-stu-id="3cce6-135">If you already have the Azure Functions Cross Platform Tools, update them to the latest available version.</span></span>

    >[!IMPORTANT]
    ><span data-ttu-id="3cce6-136">Durable Functions in JavaScript requires version 2.x of the Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="3cce6-136">Durable Functions in JavaScript requires version 2.x of the Azure Functions Core Tools.</span></span>

*  <span data-ttu-id="3cce6-137">If you are on a Windows machine, install and run [Azure Storage Emulator](https://docs.microsoft.com/azure/storage/storage-use-emulator) version 5.6 or later.</span><span class="sxs-lookup"><span data-stu-id="3cce6-137">If you are on a Windows machine, install and run [Azure Storage Emulator](https://docs.microsoft.com/azure/storage/storage-use-emulator) version 5.6 or later.</span></span> <span data-ttu-id="3cce6-138">Alternatively, you can update the *local.appsettings.json* file with real Azure Storage connection.</span><span class="sxs-lookup"><span data-stu-id="3cce6-138">Alternatively, you can update the *local.appsettings.json* file with real Azure Storage connection.</span></span> 


### <a name="start-with-sample-functions"></a><span data-ttu-id="3cce6-139">Start with sample functions</span><span class="sxs-lookup"><span data-stu-id="3cce6-139">Start with sample functions</span></span>

#### <a name="c"></a><span data-ttu-id="3cce6-140">C#</span><span class="sxs-lookup"><span data-stu-id="3cce6-140">C#</span></span>

1. <span data-ttu-id="3cce6-141">Clone the [Durable Functions repository](https://github.com/Azure/azure-functions-durable-extension.git).</span><span class="sxs-lookup"><span data-stu-id="3cce6-141">Clone the [Durable Functions repository](https://github.com/Azure/azure-functions-durable-extension.git).</span></span>
2. <span data-ttu-id="3cce6-142">Navigate on your machine to the [C# script samples folder](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/csx).</span><span class="sxs-lookup"><span data-stu-id="3cce6-142">Navigate on your machine to the [C# script samples folder](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/csx).</span></span> 
3. <span data-ttu-id="3cce6-143">Install Azure Functions Durable Extension by running the following in a command prompt / terminal window:</span><span class="sxs-lookup"><span data-stu-id="3cce6-143">Install Azure Functions Durable Extension by running the following in a command prompt / terminal window:</span></span>

    ```bash
    func extensions install -p Microsoft.Azure.WebJobs.Extensions.DurableTask -v 1.6.0
    ```
4. <span data-ttu-id="3cce6-144">Install Azure Functions Twilio Extension by running the following in a command prompt / terminal window:</span><span class="sxs-lookup"><span data-stu-id="3cce6-144">Install Azure Functions Twilio Extension by running the following in a command prompt / terminal window:</span></span>

    ```bash
    func extensions install -p Microsoft.Azure.WebJobs.Extensions.Twilio -v 3.0.0-beta8
    ```
5. <span data-ttu-id="3cce6-145">Run Azure Storage Emulator or update the *local.appsettings.json* file with real Azure Storage connection string.</span><span class="sxs-lookup"><span data-stu-id="3cce6-145">Run Azure Storage Emulator or update the *local.appsettings.json* file with real Azure Storage connection string.</span></span>
6. <span data-ttu-id="3cce6-146">Open the project in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3cce6-146">Open the project in Visual Studio Code.</span></span> 
7. <span data-ttu-id="3cce6-147">For instructions on how to run the sample, start with [Function chaining - Hello sequence sample](durable-functions-sequence.md).</span><span class="sxs-lookup"><span data-stu-id="3cce6-147">For instructions on how to run the sample, start with [Function chaining - Hello sequence sample](durable-functions-sequence.md).</span></span> <span data-ttu-id="3cce6-148">The sample can be run locally or published to Azure.</span><span class="sxs-lookup"><span data-stu-id="3cce6-148">The sample can be run locally or published to Azure.</span></span>
8. <span data-ttu-id="3cce6-149">Start the project by running in command prompt / terminal the following command:</span><span class="sxs-lookup"><span data-stu-id="3cce6-149">Start the project by running in command prompt / terminal the following command:</span></span>
    ```bash
    func host start
    ```

#### <a name="javascript-functions-v2-only"></a><span data-ttu-id="3cce6-150">JavaScript (Functions v2 only)</span><span class="sxs-lookup"><span data-stu-id="3cce6-150">JavaScript (Functions v2 only)</span></span>

1. <span data-ttu-id="3cce6-151">Clone the [Durable Functions repository](https://github.com/Azure/azure-functions-durable-extension.git).</span><span class="sxs-lookup"><span data-stu-id="3cce6-151">Clone the [Durable Functions repository](https://github.com/Azure/azure-functions-durable-extension.git).</span></span>
2. <span data-ttu-id="3cce6-152">Navigate on your machine to the [JavaScript samples folder](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/javascript).</span><span class="sxs-lookup"><span data-stu-id="3cce6-152">Navigate on your machine to the [JavaScript samples folder](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/javascript).</span></span> 
3. <span data-ttu-id="3cce6-153">Install Azure Functions Durable Extension by running the following in a command prompt / terminal window:</span><span class="sxs-lookup"><span data-stu-id="3cce6-153">Install Azure Functions Durable Extension by running the following in a command prompt / terminal window:</span></span>

    ```bash
    func extensions install -p Microsoft.Azure.WebJobs.Extensions.DurableTask -v 1.6.0
    ```
4. <span data-ttu-id="3cce6-154">Restore the npm packages by running the following in a command prompt / terminal window:</span><span class="sxs-lookup"><span data-stu-id="3cce6-154">Restore the npm packages by running the following in a command prompt / terminal window:</span></span>
    
    ```bash
    npm install
    ``` 
5. <span data-ttu-id="3cce6-155">Update the *local.appsettings.json* file with the real Azure Storage connection string.</span><span class="sxs-lookup"><span data-stu-id="3cce6-155">Update the *local.appsettings.json* file with the real Azure Storage connection string.</span></span>
6. <span data-ttu-id="3cce6-156">Open the project in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3cce6-156">Open the project in Visual Studio Code.</span></span> 
7. <span data-ttu-id="3cce6-157">For instructions on how to run the sample, start with [Function chaining - Hello sequence sample](durable-functions-sequence.md).</span><span class="sxs-lookup"><span data-stu-id="3cce6-157">For instructions on how to run the sample, start with [Function chaining - Hello sequence sample](durable-functions-sequence.md).</span></span> <span data-ttu-id="3cce6-158">The sample can be run locally or published to Azure.</span><span class="sxs-lookup"><span data-stu-id="3cce6-158">The sample can be run locally or published to Azure.</span></span>
8. <span data-ttu-id="3cce6-159">Start the project by running in command prompt / terminal the following command:</span><span class="sxs-lookup"><span data-stu-id="3cce6-159">Start the project by running in command prompt / terminal the following command:</span></span>
    ```bash
    func host start
    ```

### <a name="start-with-an-empty-project"></a><span data-ttu-id="3cce6-160">Start with an empty project</span><span class="sxs-lookup"><span data-stu-id="3cce6-160">Start with an empty project</span></span>
 
1. <span data-ttu-id="3cce6-161">In command prompt / terminal navigate to the folder that will host your function app.</span><span class="sxs-lookup"><span data-stu-id="3cce6-161">In command prompt / terminal navigate to the folder that will host your function app.</span></span>
2. <span data-ttu-id="3cce6-162">Install the Azure Functions Durable Extension by running the following in a command prompt / terminal window:</span><span class="sxs-lookup"><span data-stu-id="3cce6-162">Install the Azure Functions Durable Extension by running the following in a command prompt / terminal window:</span></span>

    ```bash
    func extensions install -p Microsoft.Azure.WebJobs.Extensions.DurableTask -v 1.6.0
    ```
3. <span data-ttu-id="3cce6-163">Create a Function App project by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3cce6-163">Create a Function App project by running the following command:</span></span>

    ```bash
    func init
    ``` 
4. <span data-ttu-id="3cce6-164">Run Azure Storage Emulator or update the *local.appsettings.json* file with real Azure Storage connection string.</span><span class="sxs-lookup"><span data-stu-id="3cce6-164">Run Azure Storage Emulator or update the *local.appsettings.json* file with real Azure Storage connection string.</span></span>
5. <span data-ttu-id="3cce6-165">Next, create a new function by running the following command and follow the wizard steps:</span><span class="sxs-lookup"><span data-stu-id="3cce6-165">Next, create a new function by running the following command and follow the wizard steps:</span></span>

    ```bash
    func new
    ```
    >[!IMPORTANT]
    > <span data-ttu-id="3cce6-166">Currently the Durable Function template is not available but you can start with one of the supported options and then modify the code.</span><span class="sxs-lookup"><span data-stu-id="3cce6-166">Currently the Durable Function template is not available but you can start with one of the supported options and then modify the code.</span></span> <span data-ttu-id="3cce6-167">Use for reference the samples for [Orchestration Client](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/csx/HttpStart), [Orchestration Trigger](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/csx/E1_HelloSequence), and [Activity Trigger](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/csx/E1_HelloSequence).</span><span class="sxs-lookup"><span data-stu-id="3cce6-167">Use for reference the samples for [Orchestration Client](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/csx/HttpStart), [Orchestration Trigger](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/csx/E1_HelloSequence), and [Activity Trigger](https://github.com/Azure/azure-functions-durable-extension/tree/master/samples/csx/E1_HelloSequence).</span></span>

6. <span data-ttu-id="3cce6-168">Open the project folder in Visual Studio Code and continue by modifying the template code.</span><span class="sxs-lookup"><span data-stu-id="3cce6-168">Open the project folder in Visual Studio Code and continue by modifying the template code.</span></span> 
7. <span data-ttu-id="3cce6-169">Start the project by running in command prompt / terminal the following command:</span><span class="sxs-lookup"><span data-stu-id="3cce6-169">Start the project by running in command prompt / terminal the following command:</span></span>
    ```bash
    func host start
    ```

## <a name="azure-portal"></a><span data-ttu-id="3cce6-170">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3cce6-170">Azure portal</span></span>

<span data-ttu-id="3cce6-171">If you prefer, you can use the [Azure portal](https://portal.azure.com) for Durable Functions development.</span><span class="sxs-lookup"><span data-stu-id="3cce6-171">If you prefer, you can use the [Azure portal](https://portal.azure.com) for Durable Functions development.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3cce6-172">Durable Functions in JavaScript are not yet available in the portal.</span><span class="sxs-lookup"><span data-stu-id="3cce6-172">Durable Functions in JavaScript are not yet available in the portal.</span></span>

### <a name="create-an-orchestrator-function"></a><span data-ttu-id="3cce6-173">Create an orchestrator function</span><span class="sxs-lookup"><span data-stu-id="3cce6-173">Create an orchestrator function</span></span>

1. <span data-ttu-id="3cce6-174">Create a new function app in the portal, as shown in the [Functions quickstart article](functions-create-first-azure-function.md#create-a-function-app).</span><span class="sxs-lookup"><span data-stu-id="3cce6-174">Create a new function app in the portal, as shown in the [Functions quickstart article](functions-create-first-azure-function.md#create-a-function-app).</span></span>

2. <span data-ttu-id="3cce6-175">Configure the function app to [use the 2.0 runtime version](set-runtime-version.md).</span><span class="sxs-lookup"><span data-stu-id="3cce6-175">Configure the function app to [use the 2.0 runtime version](set-runtime-version.md).</span></span>

   <span data-ttu-id="3cce6-176">The Durable Functions extension works on both the 1.X runtime and the 2.0 runtime, but the Azure Portal templates are only available when targeting the 2.0 runtime.</span><span class="sxs-lookup"><span data-stu-id="3cce6-176">The Durable Functions extension works on both the 1.X runtime and the 2.0 runtime, but the Azure Portal templates are only available when targeting the 2.0 runtime.</span></span>

3. <span data-ttu-id="3cce6-177">Create a new function by selecting **"create your own custom function."**.</span><span class="sxs-lookup"><span data-stu-id="3cce6-177">Create a new function by selecting **"create your own custom function."**.</span></span>

4. <span data-ttu-id="3cce6-178">Change the **Language** to **C#**, **Scenario** to **Durable Functions** and select the **Durable Functions Http Starter - C#** template.</span><span class="sxs-lookup"><span data-stu-id="3cce6-178">Change the **Language** to **C#**, **Scenario** to **Durable Functions** and select the **Durable Functions Http Starter - C#** template.</span></span>

5. <span data-ttu-id="3cce6-179">Under **Extensions not installed**, click **Install** to download the extension from NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="3cce6-179">Under **Extensions not installed**, click **Install** to download the extension from NuGet.org.</span></span> 

6. <span data-ttu-id="3cce6-180">After the installation is complete, proceed with the creation of an orchestration client function – **“HttpStart”** that is created by selecting **Durable Functions Http Starter - C#** template.</span><span class="sxs-lookup"><span data-stu-id="3cce6-180">After the installation is complete, proceed with the creation of an orchestration client function – **“HttpStart”** that is created by selecting **Durable Functions Http Starter - C#** template.</span></span>

7. <span data-ttu-id="3cce6-181">Now, create an orchestration function **“HelloSequence”** from **Durable Functions Orchestrator - C#** template.</span><span class="sxs-lookup"><span data-stu-id="3cce6-181">Now, create an orchestration function **“HelloSequence”** from **Durable Functions Orchestrator - C#** template.</span></span>

8. <span data-ttu-id="3cce6-182">And the last function will be called **“Hello”** from **Durable Functions Activity - C#** template.</span><span class="sxs-lookup"><span data-stu-id="3cce6-182">And the last function will be called **“Hello”** from **Durable Functions Activity - C#** template.</span></span>

9. <span data-ttu-id="3cce6-183">Go to **"HttpStart"** function and copy its URL.</span><span class="sxs-lookup"><span data-stu-id="3cce6-183">Go to **"HttpStart"** function and copy its URL.</span></span>

10. <span data-ttu-id="3cce6-184">Use Postman or cURL to call the durable function.</span><span class="sxs-lookup"><span data-stu-id="3cce6-184">Use Postman or cURL to call the durable function.</span></span> <span data-ttu-id="3cce6-185">Before testing, replace in the URL **{functionName}** with the orchestrator function name - **HelloSequence**.</span><span class="sxs-lookup"><span data-stu-id="3cce6-185">Before testing, replace in the URL **{functionName}** with the orchestrator function name - **HelloSequence**.</span></span>  <span data-ttu-id="3cce6-186">No data is required, just use POST verb.</span><span class="sxs-lookup"><span data-stu-id="3cce6-186">No data is required, just use POST verb.</span></span> 

    ```bash
    curl -X POST https://{your function app name}.azurewebsites.net/api/orchestrators/HelloSequence
    ```

11. <span data-ttu-id="3cce6-187">Then, call the **“statusQueryGetUri”** endpoint and you see the current status of the Durable Function</span><span class="sxs-lookup"><span data-stu-id="3cce6-187">Then, call the **“statusQueryGetUri”** endpoint and you see the current status of the Durable Function</span></span>

    ```json
        {
            "runtimeStatus": "Running",
            "input": null,
            "output": null,
            "createdTime": "2017-12-01T05:37:33Z",
            "lastUpdatedTime": "2017-12-01T05:37:36Z"
        }
    ```

12. <span data-ttu-id="3cce6-188">Continue calling the **“statusQueryGetUri”** endpoint until the status changes to **"Completed"**</span><span class="sxs-lookup"><span data-stu-id="3cce6-188">Continue calling the **“statusQueryGetUri”** endpoint until the status changes to **"Completed"**</span></span> 

    ```json
    {
            "runtimeStatus": "Completed",
            "input": null,
            "output": [
                "Hello Tokyo!",
                "Hello Seattle!",
                "Hello London!"
            ],
            "createdTime": "2017-12-01T05:38:22Z",
            "lastUpdatedTime": "2017-12-01T05:38:28Z"
        }
    ```

<span data-ttu-id="3cce6-189">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="3cce6-189">Congratulations!</span></span> <span data-ttu-id="3cce6-190">Your first durable function is up and running in Azure Portal!</span><span class="sxs-lookup"><span data-stu-id="3cce6-190">Your first durable function is up and running in Azure Portal!</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cce6-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="3cce6-191">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cce6-192">Run the function chaining sample</span><span class="sxs-lookup"><span data-stu-id="3cce6-192">Run the function chaining sample</span></span>](durable-functions-sequence.md)
