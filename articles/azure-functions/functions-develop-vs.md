---
title: Develop Azure Functions using Visual Studio  | Microsoft Docs
description: Learn how to develop and test Azure Functions by using Azure Functions Tools for Visual Studio 2017.
services: functions
documentationcenter: .net
author: ggailey777
manager: jeconnoc
ms.service: azure-functions
ms.custom: vs-azure
ms.topic: conceptual
ms.date: 05/23/2018
ms.author: glenga
ms.openlocfilehash: 39745991f7ab3b181f892bbaa59283d92737ecf3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867464"
---
# <a name="develop-azure-functions-using-visual-studio"></a><span data-ttu-id="3fa81-103">Develop Azure Functions using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3fa81-103">Develop Azure Functions using Visual Studio</span></span>  

<span data-ttu-id="3fa81-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions to Azure.</span><span class="sxs-lookup"><span data-stu-id="3fa81-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions to Azure.</span></span> <span data-ttu-id="3fa81-105">If this experience is your first with Azure Functions, you can learn more at [An introduction to Azure Functions](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3fa81-105">If this experience is your first with Azure Functions, you can learn more at [An introduction to Azure Functions](functions-overview.md).</span></span>

<span data-ttu-id="3fa81-106">The Azure Functions Tools provides the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3fa81-106">The Azure Functions Tools provides the following benefits:</span></span> 

* <span data-ttu-id="3fa81-107">Edit, build, and run functions on your local development computer.</span><span class="sxs-lookup"><span data-stu-id="3fa81-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="3fa81-108">Publish your Azure Functions project directly to Azure.</span><span class="sxs-lookup"><span data-stu-id="3fa81-108">Publish your Azure Functions project directly to Azure.</span></span> 
* <span data-ttu-id="3fa81-109">Use WebJobs attributes to declare function bindings directly in the C# code instead of maintaining a separate function.json for binding definitions.</span><span class="sxs-lookup"><span data-stu-id="3fa81-109">Use WebJobs attributes to declare function bindings directly in the C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="3fa81-110">Develop and deploy pre-compiled C# functions.</span><span class="sxs-lookup"><span data-stu-id="3fa81-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="3fa81-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span><span class="sxs-lookup"><span data-stu-id="3fa81-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="3fa81-112">Code your functions in C# while having all of the benefits of Visual Studio development.</span><span class="sxs-lookup"><span data-stu-id="3fa81-112">Code your functions in C# while having all of the benefits of Visual Studio development.</span></span> 

<span data-ttu-id="3fa81-113">This article shows you how to use the Azure Functions Tools for Visual Studio 2017 to develop your functions in C#.</span><span class="sxs-lookup"><span data-stu-id="3fa81-113">This article shows you how to use the Azure Functions Tools for Visual Studio 2017 to develop your functions in C#.</span></span> <span data-ttu-id="3fa81-114">You also learn how to publish your project to Azure as a .NET assembly.</span><span class="sxs-lookup"><span data-stu-id="3fa81-114">You also learn how to publish your project to Azure as a .NET assembly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3fa81-115">Don't mix local development with portal development in the same function app.</span><span class="sxs-lookup"><span data-stu-id="3fa81-115">Don't mix local development with portal development in the same function app.</span></span> <span data-ttu-id="3fa81-116">When you publish from a local project to a function app, the deployment process overwrites any functions that you developed in the portal.</span><span class="sxs-lookup"><span data-stu-id="3fa81-116">When you publish from a local project to a function app, the deployment process overwrites any functions that you developed in the portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fa81-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3fa81-117">Prerequisites</span></span>

<span data-ttu-id="3fa81-118">Azure Functions Tools is included in the Azure development workload of [Visual Studio 2017 version 15.5](https://www.visualstudio.com/vs/), or a later version.</span><span class="sxs-lookup"><span data-stu-id="3fa81-118">Azure Functions Tools is included in the Azure development workload of [Visual Studio 2017 version 15.5](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="3fa81-119">Make sure you include the **Azure development** workload in your Visual Studio 2017 installation:</span><span class="sxs-lookup"><span data-stu-id="3fa81-119">Make sure you include the **Azure development** workload in your Visual Studio 2017 installation:</span></span>

![Install Visual Studio 2017 with the Azure development workload](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="3fa81-121">Make sure that your Visual Studio is up-to-date and that you are using the [most recent version](#check-your-tools-version) of the Azure Functions tools.</span><span class="sxs-lookup"><span data-stu-id="3fa81-121">Make sure that your Visual Studio is up-to-date and that you are using the [most recent version](#check-your-tools-version) of the Azure Functions tools.</span></span>

### <a name="other-requirements"></a><span data-ttu-id="3fa81-122">Other requirements</span><span class="sxs-lookup"><span data-stu-id="3fa81-122">Other requirements</span></span>

<span data-ttu-id="3fa81-123">To create and deploy functions, you also need:</span><span class="sxs-lookup"><span data-stu-id="3fa81-123">To create and deploy functions, you also need:</span></span>

* <span data-ttu-id="3fa81-124">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3fa81-124">An active Azure subscription.</span></span> <span data-ttu-id="3fa81-125">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span><span class="sxs-lookup"><span data-stu-id="3fa81-125">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="3fa81-126">An Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="3fa81-126">An Azure Storage account.</span></span> <span data-ttu-id="3fa81-127">To create a storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="3fa81-127">To create a storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md).</span></span>

### <a name="check-your-tools-version"></a><span data-ttu-id="3fa81-128">Check your tools version</span><span class="sxs-lookup"><span data-stu-id="3fa81-128">Check your tools version</span></span>

1. <span data-ttu-id="3fa81-129">From the **Tools** menu, choose **Extensions and Updates**.</span><span class="sxs-lookup"><span data-stu-id="3fa81-129">From the **Tools** menu, choose **Extensions and Updates**.</span></span> <span data-ttu-id="3fa81-130">Expand **Installed** > **Tools** and choose **Azure Functions and Web Jobs Tools**.</span><span class="sxs-lookup"><span data-stu-id="3fa81-130">Expand **Installed** > **Tools** and choose **Azure Functions and Web Jobs Tools**.</span></span>

    ![Verify the Functions tools version](./media/functions-develop-vs/functions-vstools-check-functions-tools.png)

2. <span data-ttu-id="3fa81-132">Note the installed **Version**.</span><span class="sxs-lookup"><span data-stu-id="3fa81-132">Note the installed **Version**.</span></span> <span data-ttu-id="3fa81-133">You can compare this version with the latest version listed [in the release notes](https://github.com/Azure/Azure-Functions/blob/master/VS-AzureTools-ReleaseNotes.md).</span><span class="sxs-lookup"><span data-stu-id="3fa81-133">You can compare this version with the latest version listed [in the release notes](https://github.com/Azure/Azure-Functions/blob/master/VS-AzureTools-ReleaseNotes.md).</span></span> 

3. <span data-ttu-id="3fa81-134">If your version is older, update your tools in Visual Studio as shown in the following section.</span><span class="sxs-lookup"><span data-stu-id="3fa81-134">If your version is older, update your tools in Visual Studio as shown in the following section.</span></span>

### <a name="update-your-tools"></a><span data-ttu-id="3fa81-135">Update your tools</span><span class="sxs-lookup"><span data-stu-id="3fa81-135">Update your tools</span></span>

1. <span data-ttu-id="3fa81-136">In the **Extensions and Updates** dialog, expand **Updates** > **Visual Studio Marketplace**, choose **Azure Functions and Web Jobs Tools** and select **Update**.</span><span class="sxs-lookup"><span data-stu-id="3fa81-136">In the **Extensions and Updates** dialog, expand **Updates** > **Visual Studio Marketplace**, choose **Azure Functions and Web Jobs Tools** and select **Update**.</span></span>

    ![Update the Functions tools version](./media/functions-develop-vs/functions-vstools-update-functions-tools.png)   

2. <span data-ttu-id="3fa81-138">After the tools update is downloaded, close Visual Studio to trigger the tools update using the VSIX installer.</span><span class="sxs-lookup"><span data-stu-id="3fa81-138">After the tools update is downloaded, close Visual Studio to trigger the tools update using the VSIX installer.</span></span>

3. <span data-ttu-id="3fa81-139">In the installer, choose **OK** to start and then **Modify** to update the tools.</span><span class="sxs-lookup"><span data-stu-id="3fa81-139">In the installer, choose **OK** to start and then **Modify** to update the tools.</span></span> 

4. <span data-ttu-id="3fa81-140">After the update is complete, choose **Close** and restart Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fa81-140">After the update is complete, choose **Close** and restart Visual Studio.</span></span>

## <a name="create-an-azure-functions-project"></a><span data-ttu-id="3fa81-141">Create an Azure Functions project</span><span class="sxs-lookup"><span data-stu-id="3fa81-141">Create an Azure Functions project</span></span>

[!INCLUDE [Create a project using the Azure Functions](../../includes/functions-vstools-create.md)]

<span data-ttu-id="3fa81-142">The project template creates a C# project, installs the `Microsoft.NET.Sdk.Functions` NuGet package, and sets the target framework.</span><span class="sxs-lookup"><span data-stu-id="3fa81-142">The project template creates a C# project, installs the `Microsoft.NET.Sdk.Functions` NuGet package, and sets the target framework.</span></span> <span data-ttu-id="3fa81-143">Functions 1.x targets the .NET Framework, and Functions 2.x targets .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="3fa81-143">Functions 1.x targets the .NET Framework, and Functions 2.x targets .NET Standard.</span></span> <span data-ttu-id="3fa81-144">The new project has the following files:</span><span class="sxs-lookup"><span data-stu-id="3fa81-144">The new project has the following files:</span></span>

* <span data-ttu-id="3fa81-145">**host.json**: Lets you configure the Functions host.</span><span class="sxs-lookup"><span data-stu-id="3fa81-145">**host.json**: Lets you configure the Functions host.</span></span> <span data-ttu-id="3fa81-146">These settings apply both when running locally and in Azure.</span><span class="sxs-lookup"><span data-stu-id="3fa81-146">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="3fa81-147">For more information, see [host.json reference](functions-host-json.md).</span><span class="sxs-lookup"><span data-stu-id="3fa81-147">For more information, see [host.json reference](functions-host-json.md).</span></span>

* <span data-ttu-id="3fa81-148">**local.settings.json**: Maintains settings used when running functions locally.</span><span class="sxs-lookup"><span data-stu-id="3fa81-148">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="3fa81-149">These settings are not used by Azure, they are used by the [Azure Functions Core Tools](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="3fa81-149">These settings are not used by Azure, they are used by the [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="3fa81-150">Use this file to specify app settings for variables required by your functions.</span><span class="sxs-lookup"><span data-stu-id="3fa81-150">Use this file to specify app settings for variables required by your functions.</span></span> <span data-ttu-id="3fa81-151">Add a new item to the **Values** array for each connection required by the functions bindings in your project.</span><span class="sxs-lookup"><span data-stu-id="3fa81-151">Add a new item to the **Values** array for each connection required by the functions bindings in your project.</span></span> <span data-ttu-id="3fa81-152">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in the Azure Functions Core Tools article.</span><span class="sxs-lookup"><span data-stu-id="3fa81-152">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in the Azure Functions Core Tools article.</span></span>

<span data-ttu-id="3fa81-153">For more information, see [Functions class library project](functions-dotnet-class-library.md#functions-class-library-project).</span><span class="sxs-lookup"><span data-stu-id="3fa81-153">For more information, see [Functions class library project](functions-dotnet-class-library.md#functions-class-library-project).</span></span>

## <a name="configure-the-project-for-local-development"></a><span data-ttu-id="3fa81-154">Configure the project for local development</span><span class="sxs-lookup"><span data-stu-id="3fa81-154">Configure the project for local development</span></span>

<span data-ttu-id="3fa81-155">The Functions runtime uses an Azure Storage account internally.</span><span class="sxs-lookup"><span data-stu-id="3fa81-155">The Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="3fa81-156">For all trigger types other than HTTP and webhooks, you must set the **Values.AzureWebJobsStorage** key to a valid Azure Storage account connection string.</span><span class="sxs-lookup"><span data-stu-id="3fa81-156">For all trigger types other than HTTP and webhooks, you must set the **Values.AzureWebJobsStorage** key to a valid Azure Storage account connection string.</span></span> <span data-ttu-id="3fa81-157">Your function app can also use the [Azure storage emulator](../storage/common/storage-use-emulator.md) for the **AzureWebJobsStorage** connection setting that is required by the project.</span><span class="sxs-lookup"><span data-stu-id="3fa81-157">Your function app can also use the [Azure storage emulator](../storage/common/storage-use-emulator.md) for the **AzureWebJobsStorage** connection setting that is required by the project.</span></span> <span data-ttu-id="3fa81-158">To use the emulator, set the value of **AzureWebJobsStorage** to `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="3fa81-158">To use the emulator, set the value of **AzureWebJobsStorage** to `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="3fa81-159">You must change this setting to an actual storage connection before deployment.</span><span class="sxs-lookup"><span data-stu-id="3fa81-159">You must change this setting to an actual storage connection before deployment.</span></span>

<span data-ttu-id="3fa81-160">To set the storage account connection string:</span><span class="sxs-lookup"><span data-stu-id="3fa81-160">To set the storage account connection string:</span></span>

1. <span data-ttu-id="3fa81-161">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy the **Primary Connection String** value.</span><span class="sxs-lookup"><span data-stu-id="3fa81-161">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy the **Primary Connection String** value.</span></span>

2. <span data-ttu-id="3fa81-162">In your project, open the local.settings.json file and set the value of the **AzureWebJobsStorage** key to the connection string you copied.</span><span class="sxs-lookup"><span data-stu-id="3fa81-162">In your project, open the local.settings.json file and set the value of the **AzureWebJobsStorage** key to the connection string you copied.</span></span>

3. <span data-ttu-id="3fa81-163">Repeat the previous step to add unique keys to the **Values** array for any other connections required by your functions.</span><span class="sxs-lookup"><span data-stu-id="3fa81-163">Repeat the previous step to add unique keys to the **Values** array for any other connections required by your functions.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="3fa81-164">Create a function</span><span class="sxs-lookup"><span data-stu-id="3fa81-164">Create a function</span></span>

<span data-ttu-id="3fa81-165">In pre-compiled functions, the bindings used by the function are defined by applying attributes in the code.</span><span class="sxs-lookup"><span data-stu-id="3fa81-165">In pre-compiled functions, the bindings used by the function are defined by applying attributes in the code.</span></span> <span data-ttu-id="3fa81-166">When you use the Azure Functions Tools to create your functions from the provided templates, these attributes are applied for you.</span><span class="sxs-lookup"><span data-stu-id="3fa81-166">When you use the Azure Functions Tools to create your functions from the provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="3fa81-167">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span><span class="sxs-lookup"><span data-stu-id="3fa81-167">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="3fa81-168">Select **Azure Function**, type a **Name** for the class, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="3fa81-168">Select **Azure Function**, type a **Name** for the class, and click **Add**.</span></span>

2. <span data-ttu-id="3fa81-169">Choose your trigger, set the binding properties, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3fa81-169">Choose your trigger, set the binding properties, and click **Create**.</span></span> <span data-ttu-id="3fa81-170">The following example shows the settings when creating a Queue storage triggered function.</span><span class="sxs-lookup"><span data-stu-id="3fa81-170">The following example shows the settings when creating a Queue storage triggered function.</span></span> 

    ![Create a queue triggered function](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)

    <span data-ttu-id="3fa81-172">This trigger example uses a connection string with a key named **QueueStorage**.</span><span class="sxs-lookup"><span data-stu-id="3fa81-172">This trigger example uses a connection string with a key named **QueueStorage**.</span></span> <span data-ttu-id="3fa81-173">This connection string setting must be defined in the [local.settings.json file](functions-run-local.md#local-settings-file).</span><span class="sxs-lookup"><span data-stu-id="3fa81-173">This connection string setting must be defined in the [local.settings.json file](functions-run-local.md#local-settings-file).</span></span>

3. <span data-ttu-id="3fa81-174">Examine the newly added class.</span><span class="sxs-lookup"><span data-stu-id="3fa81-174">Examine the newly added class.</span></span> <span data-ttu-id="3fa81-175">You see a static **Run** method, that is attributed with the **FunctionName** attribute.</span><span class="sxs-lookup"><span data-stu-id="3fa81-175">You see a static **Run** method, that is attributed with the **FunctionName** attribute.</span></span> <span data-ttu-id="3fa81-176">This attribute indicates that the method is the entry point for the function.</span><span class="sxs-lookup"><span data-stu-id="3fa81-176">This attribute indicates that the method is the entry point for the function.</span></span>

    <span data-ttu-id="3fa81-177">For example, the following C# class represents a basic Queue storage triggered function:</span><span class="sxs-lookup"><span data-stu-id="3fa81-177">For example, the following C# class represents a basic Queue storage triggered function:</span></span>

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;

    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    }
    ````
    <span data-ttu-id="3fa81-178">A binding-specific attribute is applied to each binding parameter supplied to the entry point method.</span><span class="sxs-lookup"><span data-stu-id="3fa81-178">A binding-specific attribute is applied to each binding parameter supplied to the entry point method.</span></span> <span data-ttu-id="3fa81-179">The attribute takes the binding information as parameters.</span><span class="sxs-lookup"><span data-stu-id="3fa81-179">The attribute takes the binding information as parameters.</span></span> <span data-ttu-id="3fa81-180">In the previous example, the first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span><span class="sxs-lookup"><span data-stu-id="3fa81-180">In the previous example, the first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="3fa81-181">The queue name and connection string setting name are passed as parameters to the **QueueTrigger** attribute.</span><span class="sxs-lookup"><span data-stu-id="3fa81-181">The queue name and connection string setting name are passed as parameters to the **QueueTrigger** attribute.</span></span> <span data-ttu-id="3fa81-182">For more information, see [Azure Queue storage bindings for Azure Functions](functions-bindings-storage-queue.md#trigger---c-example).</span><span class="sxs-lookup"><span data-stu-id="3fa81-182">For more information, see [Azure Queue storage bindings for Azure Functions](functions-bindings-storage-queue.md#trigger---c-example).</span></span>
    
<span data-ttu-id="3fa81-183">You can use the above procedure to add more functions to your function app project.</span><span class="sxs-lookup"><span data-stu-id="3fa81-183">You can use the above procedure to add more functions to your function app project.</span></span> <span data-ttu-id="3fa81-184">Each function in the project can have a different trigger, but a function must have exactly one trigger.</span><span class="sxs-lookup"><span data-stu-id="3fa81-184">Each function in the project can have a different trigger, but a function must have exactly one trigger.</span></span> <span data-ttu-id="3fa81-185">For more information, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="3fa81-185">For more information, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

## <a name="add-bindings"></a><span data-ttu-id="3fa81-186">Add bindings</span><span class="sxs-lookup"><span data-stu-id="3fa81-186">Add bindings</span></span>

<span data-ttu-id="3fa81-187">As with triggers, input and output bindings are added to your function as binding attributes.</span><span class="sxs-lookup"><span data-stu-id="3fa81-187">As with triggers, input and output bindings are added to your function as binding attributes.</span></span> <span data-ttu-id="3fa81-188">Add bindings to a function as follows:</span><span class="sxs-lookup"><span data-stu-id="3fa81-188">Add bindings to a function as follows:</span></span>

1. <span data-ttu-id="3fa81-189">Make sure you have [configured the project for local development](#configure-the-project-for-local-development).</span><span class="sxs-lookup"><span data-stu-id="3fa81-189">Make sure you have [configured the project for local development](#configure-the-project-for-local-development).</span></span>

2. <span data-ttu-id="3fa81-190">Add the appropriate NuGet extension package for the specific binding.</span><span class="sxs-lookup"><span data-stu-id="3fa81-190">Add the appropriate NuGet extension package for the specific binding.</span></span> <span data-ttu-id="3fa81-191">For more information, see [Local C# development using Visual Studio](functions-triggers-bindings.md#local-csharp) in the Triggers and Bindings article.</span><span class="sxs-lookup"><span data-stu-id="3fa81-191">For more information, see [Local C# development using Visual Studio](functions-triggers-bindings.md#local-csharp) in the Triggers and Bindings article.</span></span> <span data-ttu-id="3fa81-192">The binding-specific NuGet package requirements are found in the reference article for the binding.</span><span class="sxs-lookup"><span data-stu-id="3fa81-192">The binding-specific NuGet package requirements are found in the reference article for the binding.</span></span> <span data-ttu-id="3fa81-193">For example, find package requirements for the Event Hubs trigger in the [Event Hubs binding reference article](functions-bindings-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="3fa81-193">For example, find package requirements for the Event Hubs trigger in the [Event Hubs binding reference article](functions-bindings-event-hubs.md).</span></span>

3. <span data-ttu-id="3fa81-194">If there are app settings that the binding needs, add them to the **Values** collection in the [local setting file](functions-run-local.md#local-settings-file).</span><span class="sxs-lookup"><span data-stu-id="3fa81-194">If there are app settings that the binding needs, add them to the **Values** collection in the [local setting file](functions-run-local.md#local-settings-file).</span></span> <span data-ttu-id="3fa81-195">These values are used when the function runs locally.</span><span class="sxs-lookup"><span data-stu-id="3fa81-195">These values are used when the function runs locally.</span></span> <span data-ttu-id="3fa81-196">When the function runs in the function app in Azure, the [function app settings](#function-app-settings) are used.</span><span class="sxs-lookup"><span data-stu-id="3fa81-196">When the function runs in the function app in Azure, the [function app settings](#function-app-settings) are used.</span></span>

4. <span data-ttu-id="3fa81-197">Add the appropriate binding attribute to the method signature.</span><span class="sxs-lookup"><span data-stu-id="3fa81-197">Add the appropriate binding attribute to the method signature.</span></span> <span data-ttu-id="3fa81-198">In the following example, a queue message triggers the function, and the output binding creates a new queue message with the same text in a different queue.</span><span class="sxs-lookup"><span data-stu-id="3fa81-198">In the following example, a queue message triggers the function, and the output binding creates a new queue message with the same text in a different queue.</span></span>

    ```csharp
    public static class SimpleExampleWithOutput
    {
        [FunctionName("CopyQueueMessage")]
        public static void Run(
            [QueueTrigger("myqueue-items-source", Connection = "AzureWebJobsStorage")] string myQueueItem, 
            [Queue("myqueue-items-destination", Connection = "AzureWebJobsStorage")] out string myQueueItemCopy,
            TraceWriter log)
        {
            log.Info($"CopyQueueMessage function processed: {myQueueItem}");
            myQueueItemCopy = myQueueItem;
        }
    }
    ```
<span data-ttu-id="3fa81-199">The connection to Queue storage is obtained from the `AzureWebJobsStorage` setting.</span><span class="sxs-lookup"><span data-stu-id="3fa81-199">The connection to Queue storage is obtained from the `AzureWebJobsStorage` setting.</span></span> <span data-ttu-id="3fa81-200">For more information, see the reference article for the specific binding.</span><span class="sxs-lookup"><span data-stu-id="3fa81-200">For more information, see the reference article for the specific binding.</span></span> 

[!INCLUDE [Supported triggers and bindings](../../includes/functions-bindings.md)]

## <a name="testing-functions"></a><span data-ttu-id="3fa81-201">Testing functions</span><span class="sxs-lookup"><span data-stu-id="3fa81-201">Testing functions</span></span>

<span data-ttu-id="3fa81-202">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span><span class="sxs-lookup"><span data-stu-id="3fa81-202">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="3fa81-203">You are prompted to install these tools the first time you start a function from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fa81-203">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>

<span data-ttu-id="3fa81-204">To test your function, press F5.</span><span class="sxs-lookup"><span data-stu-id="3fa81-204">To test your function, press F5.</span></span> <span data-ttu-id="3fa81-205">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span><span class="sxs-lookup"><span data-stu-id="3fa81-205">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span> <span data-ttu-id="3fa81-206">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="3fa81-206">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

<span data-ttu-id="3fa81-207">With the project running, you can test your code as you would test deployed function.</span><span class="sxs-lookup"><span data-stu-id="3fa81-207">With the project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="3fa81-208">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span><span class="sxs-lookup"><span data-stu-id="3fa81-208">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="3fa81-209">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span><span class="sxs-lookup"><span data-stu-id="3fa81-209">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="3fa81-210">For an example of how to test a queue triggered function, see the [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span><span class="sxs-lookup"><span data-stu-id="3fa81-210">For an example of how to test a queue triggered function, see the [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="3fa81-211">To learn more about using the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="3fa81-211">To learn more about using the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-to-azure"></a><span data-ttu-id="3fa81-212">Publish to Azure</span><span class="sxs-lookup"><span data-stu-id="3fa81-212">Publish to Azure</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

## <a name="function-app-settings"></a><span data-ttu-id="3fa81-213">Function app settings</span><span class="sxs-lookup"><span data-stu-id="3fa81-213">Function app settings</span></span>

<span data-ttu-id="3fa81-214">Any settings you added in the local.settings.json must be also added to the function app in Azure.</span><span class="sxs-lookup"><span data-stu-id="3fa81-214">Any settings you added in the local.settings.json must be also added to the function app in Azure.</span></span> <span data-ttu-id="3fa81-215">These settings are not uploaded automatically when you publish the project.</span><span class="sxs-lookup"><span data-stu-id="3fa81-215">These settings are not uploaded automatically when you publish the project.</span></span>

<span data-ttu-id="3fa81-216">The easiest way to upload the required settings to your function app in Azure is to use the **Manage Application Settings...** link that is displayed after you successfully publish your project.</span><span class="sxs-lookup"><span data-stu-id="3fa81-216">The easiest way to upload the required settings to your function app in Azure is to use the **Manage Application Settings...** link that is displayed after you successfully publish your project.</span></span> 

![](./media/functions-develop-vs/functions-vstools-app-settings.png)

<span data-ttu-id="3fa81-217">This displays the **Application Settings** dialog for the function app, where you can add new application settings or modify existing ones.</span><span class="sxs-lookup"><span data-stu-id="3fa81-217">This displays the **Application Settings** dialog for the function app, where you can add new application settings or modify existing ones.</span></span>

![](./media/functions-develop-vs/functions-vstools-app-settings2.png)

<span data-ttu-id="3fa81-218">You can also manage application settings in one of these other ways:</span><span class="sxs-lookup"><span data-stu-id="3fa81-218">You can also manage application settings in one of these other ways:</span></span>

* <span data-ttu-id="3fa81-219">[Using the Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="3fa81-219">[Using the Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
* <span data-ttu-id="3fa81-220">[Using the `--publish-local-settings` publish option in the Azure Functions Core Tools](functions-run-local.md#publish).</span><span class="sxs-lookup"><span data-stu-id="3fa81-220">[Using the `--publish-local-settings` publish option in the Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
* <span data-ttu-id="3fa81-221">[Using the Azure CLI](/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set).</span><span class="sxs-lookup"><span data-stu-id="3fa81-221">[Using the Azure CLI](/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3fa81-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="3fa81-222">Next steps</span></span>

<span data-ttu-id="3fa81-223">For more information about Azure Functions Tools, see the Common Questions section of the [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span><span class="sxs-lookup"><span data-stu-id="3fa81-223">For more information about Azure Functions Tools, see the Common Questions section of the [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="3fa81-224">To learn more about the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="3fa81-224">To learn more about the Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

<span data-ttu-id="3fa81-225">To learn more about developing functions as .NET class libraries, see [Azure Functions C# developer reference](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="3fa81-225">To learn more about developing functions as .NET class libraries, see [Azure Functions C# developer reference](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="3fa81-226">This article also links to examples of how to use attributes to declare the various types of bindings supported by Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3fa81-226">This article also links to examples of how to use attributes to declare the various types of bindings supported by Azure Functions.</span></span>    
