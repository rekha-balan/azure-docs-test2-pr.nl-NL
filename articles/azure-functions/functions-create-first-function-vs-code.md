---
title: Create your first function in Azure using Visual Studio Code
description: Create and publish to Azure a simple HTTP triggered function by using Azure Functions extension in Visual Studio Code.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, compute, serverless architecture
ms.service: azure-functions
ms.devlang: multiple
ms.topic: quickstart
ms.date: 09/07/2018
ms.author: glenga
ms.custom: mvc, devcenter
ms.openlocfilehash: 614ac06e92efd906950dd7fac85095cc4acc4a53
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865319"
---
# <a name="create-your-first-function-using-visual-studio-code"></a><span data-ttu-id="40efb-104">Create your first function using Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="40efb-104">Create your first function using Visual Studio Code</span></span>

<span data-ttu-id="40efb-105">Azure Functions lets you execute your code in a [serverless](https://azure.microsoft.com/overview/serverless-computing/) environment without having to first create a VM or publish a web application.</span><span class="sxs-lookup"><span data-stu-id="40efb-105">Azure Functions lets you execute your code in a [serverless](https://azure.microsoft.com/overview/serverless-computing/) environment without having to first create a VM or publish a web application.</span></span>

<span data-ttu-id="40efb-106">In this article, you learn how to use the [Azure Functions extension for Visual Studio Code] to create and test a "hello world" function on your local computer using Microsoft Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="40efb-106">In this article, you learn how to use the [Azure Functions extension for Visual Studio Code] to create and test a "hello world" function on your local computer using Microsoft Visual Studio Code.</span></span> <span data-ttu-id="40efb-107">You then publish the function code to Azure from Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="40efb-107">You then publish the function code to Azure from Visual Studio Code.</span></span>

![Azure Functions code in a Visual Studio project](./media/functions-create-first-function-vs-code/functions-vscode-intro.png)

<span data-ttu-id="40efb-109">The extension currently supports C#, JavaScript, and Java functions.</span><span class="sxs-lookup"><span data-stu-id="40efb-109">The extension currently supports C#, JavaScript, and Java functions.</span></span> <span data-ttu-id="40efb-110">The steps in this article may vary depending on your choice of language for your Azure Functions project.</span><span class="sxs-lookup"><span data-stu-id="40efb-110">The steps in this article may vary depending on your choice of language for your Azure Functions project.</span></span> <span data-ttu-id="40efb-111">The extension is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="40efb-111">The extension is currently in preview.</span></span> <span data-ttu-id="40efb-112">To learn more, see the [Azure Functions extension for Visual Studio Code] extension page.</span><span class="sxs-lookup"><span data-stu-id="40efb-112">To learn more, see the [Azure Functions extension for Visual Studio Code] extension page.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40efb-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="40efb-113">Prerequisites</span></span>

<span data-ttu-id="40efb-114">To complete this quickstart:</span><span class="sxs-lookup"><span data-stu-id="40efb-114">To complete this quickstart:</span></span>

* <span data-ttu-id="40efb-115">Install [Visual Studio Code](https://code.visualstudio.com/) on one of the [supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).</span><span class="sxs-lookup"><span data-stu-id="40efb-115">Install [Visual Studio Code](https://code.visualstudio.com/) on one of the [supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).</span></span> <span data-ttu-id="40efb-116">This article was developed and tested on a device running macOS (High Sierra).</span><span class="sxs-lookup"><span data-stu-id="40efb-116">This article was developed and tested on a device running macOS (High Sierra).</span></span>

* <span data-ttu-id="40efb-117">Install version 2.x of the [Azure Functions Core Tools](functions-run-local.md#v2), which is still in preview.</span><span class="sxs-lookup"><span data-stu-id="40efb-117">Install version 2.x of the [Azure Functions Core Tools](functions-run-local.md#v2), which is still in preview.</span></span>

* <span data-ttu-id="40efb-118">Install the specific requirements for your chosen language:</span><span class="sxs-lookup"><span data-stu-id="40efb-118">Install the specific requirements for your chosen language:</span></span>

    | <span data-ttu-id="40efb-119">Language</span><span class="sxs-lookup"><span data-stu-id="40efb-119">Language</span></span> | <span data-ttu-id="40efb-120">Extension</span><span class="sxs-lookup"><span data-stu-id="40efb-120">Extension</span></span> |
    | -------- | --------- |
    | <span data-ttu-id="40efb-121">**C#**</span><span class="sxs-lookup"><span data-stu-id="40efb-121">**C#**</span></span> | [<span data-ttu-id="40efb-122">C# for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="40efb-122">C# for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)<br/><span data-ttu-id="40efb-123">[.NET Core CLI tools](https://docs.microsoft.com/dotnet/core/tools/?tabs=netcore2x)\*</span><span class="sxs-lookup"><span data-stu-id="40efb-123">[.NET Core CLI tools](https://docs.microsoft.com/dotnet/core/tools/?tabs=netcore2x)\*</span></span>   |
    | <span data-ttu-id="40efb-124">**Java**</span><span class="sxs-lookup"><span data-stu-id="40efb-124">**Java**</span></span> | [<span data-ttu-id="40efb-125">Debugger for Java</span><span class="sxs-lookup"><span data-stu-id="40efb-125">Debugger for Java</span></span>](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debug)<br/>[<span data-ttu-id="40efb-126">JDK 1.8</span><span class="sxs-lookup"><span data-stu-id="40efb-126">JDK 1.8</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)<br/>[<span data-ttu-id="40efb-127">Maven 3+</span><span class="sxs-lookup"><span data-stu-id="40efb-127">Maven 3+</span></span>](https://maven.apache.org/) |
    | <span data-ttu-id="40efb-128">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="40efb-128">**JavaScript**</span></span> | [<span data-ttu-id="40efb-129">Node 8.0+</span><span class="sxs-lookup"><span data-stu-id="40efb-129">Node 8.0+</span></span>](https://nodejs.org/)  |

    <span data-ttu-id="40efb-130">\* Also required by Core Tools.</span><span class="sxs-lookup"><span data-stu-id="40efb-130">\* Also required by Core Tools.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="install-the-azure-function-extension"></a><span data-ttu-id="40efb-131">Install the Azure Function extension</span><span class="sxs-lookup"><span data-stu-id="40efb-131">Install the Azure Function extension</span></span>

<span data-ttu-id="40efb-132">The Azure Functions extension is used to create, test, and deploy functions to Azure.</span><span class="sxs-lookup"><span data-stu-id="40efb-132">The Azure Functions extension is used to create, test, and deploy functions to Azure.</span></span>

1. <span data-ttu-id="40efb-133">In Visual Studio Code, open **Extensions** and search for `azure functions`, or [open this link in Visual Studio Code](vscode:extension/ms-azuretools.vscode-azurefunctions).</span><span class="sxs-lookup"><span data-stu-id="40efb-133">In Visual Studio Code, open **Extensions** and search for `azure functions`, or [open this link in Visual Studio Code](vscode:extension/ms-azuretools.vscode-azurefunctions).</span></span>

1. <span data-ttu-id="40efb-134">Select **Install** to install the extension to Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="40efb-134">Select **Install** to install the extension to Visual Studio Code.</span></span> 

    ![Install the extension for Azure Functions](./media/functions-create-first-function-vs-code/vscode-install-extension.png)

1. <span data-ttu-id="40efb-136">Restart Visual Studio Code and select the Azure icon on the Activity bar.</span><span class="sxs-lookup"><span data-stu-id="40efb-136">Restart Visual Studio Code and select the Azure icon on the Activity bar.</span></span> <span data-ttu-id="40efb-137">You should see an Azure Functions area in the Side Bar.</span><span class="sxs-lookup"><span data-stu-id="40efb-137">You should see an Azure Functions area in the Side Bar.</span></span>

    ![Azure Functions area in the Side Bar](./media/functions-create-first-function-vs-code/azure-functions-window-vscode.png)

## <a name="create-an-azure-functions-project"></a><span data-ttu-id="40efb-139">Create an Azure Functions project</span><span class="sxs-lookup"><span data-stu-id="40efb-139">Create an Azure Functions project</span></span>

<span data-ttu-id="40efb-140">The Azure Functions project template in Visual Studio Code creates a project that can be published to a function app in Azure.</span><span class="sxs-lookup"><span data-stu-id="40efb-140">The Azure Functions project template in Visual Studio Code creates a project that can be published to a function app in Azure.</span></span> <span data-ttu-id="40efb-141">A function app lets you group functions as a logical unit for management, deployment, and sharing of resources.</span><span class="sxs-lookup"><span data-stu-id="40efb-141">A function app lets you group functions as a logical unit for management, deployment, and sharing of resources.</span></span>

1. <span data-ttu-id="40efb-142">In Visual Studio Code, select the Azure logo to display the **Azure: Functions** area, and then select the Create New Project icon.</span><span class="sxs-lookup"><span data-stu-id="40efb-142">In Visual Studio Code, select the Azure logo to display the **Azure: Functions** area, and then select the Create New Project icon.</span></span>

    ![Create a function app project](./media/functions-create-first-function-vs-code/create-function-app-project.png)

1. <span data-ttu-id="40efb-144">Choose a location for your project workspace and choose **Select**.</span><span class="sxs-lookup"><span data-stu-id="40efb-144">Choose a location for your project workspace and choose **Select**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="40efb-145">This article was designed to be completed outside of a workspace.</span><span class="sxs-lookup"><span data-stu-id="40efb-145">This article was designed to be completed outside of a workspace.</span></span> <span data-ttu-id="40efb-146">In this case, do not select a project folder that is part of a workspace.</span><span class="sxs-lookup"><span data-stu-id="40efb-146">In this case, do not select a project folder that is part of a workspace.</span></span>

1. <span data-ttu-id="40efb-147">Select the language for your function app project.</span><span class="sxs-lookup"><span data-stu-id="40efb-147">Select the language for your function app project.</span></span> <span data-ttu-id="40efb-148">In this article, JavaScript is used.</span><span class="sxs-lookup"><span data-stu-id="40efb-148">In this article, JavaScript is used.</span></span>
    <span data-ttu-id="40efb-149">![Choose project language](./media/functions-create-first-function-vs-code/create-function-app-project-language.png)</span><span class="sxs-lookup"><span data-stu-id="40efb-149">![Choose project language](./media/functions-create-first-function-vs-code/create-function-app-project-language.png)</span></span>

1. <span data-ttu-id="40efb-150">When prompted, choose **Add to workspace**.</span><span class="sxs-lookup"><span data-stu-id="40efb-150">When prompted, choose **Add to workspace**.</span></span>

<span data-ttu-id="40efb-151">Visual Studio Code creates the function app project in a new workspace.</span><span class="sxs-lookup"><span data-stu-id="40efb-151">Visual Studio Code creates the function app project in a new workspace.</span></span> <span data-ttu-id="40efb-152">This project contains the [host.json](functions-host-json.md) and [local.settings.json](functions-run-local.md#local-settings-file) configuration files, plus any language-specific project files.</span><span class="sxs-lookup"><span data-stu-id="40efb-152">This project contains the [host.json](functions-host-json.md) and [local.settings.json](functions-run-local.md#local-settings-file) configuration files, plus any language-specific project files.</span></span> <span data-ttu-id="40efb-153">You also get a new Git repository in the project folder.</span><span class="sxs-lookup"><span data-stu-id="40efb-153">You also get a new Git repository in the project folder.</span></span>

## <a name="create-an-http-triggered-function"></a><span data-ttu-id="40efb-154">Create an HTTP triggered function</span><span class="sxs-lookup"><span data-stu-id="40efb-154">Create an HTTP triggered function</span></span>

1. <span data-ttu-id="40efb-155">From **Azure: Functions**, choose the Create Function icon.</span><span class="sxs-lookup"><span data-stu-id="40efb-155">From **Azure: Functions**, choose the Create Function icon.</span></span>

    ![Create a function](./media/functions-create-first-function-vs-code/create-function.png)

1. <span data-ttu-id="40efb-157">Select the folder with your function app project and select the **HTTP trigger** function template.</span><span class="sxs-lookup"><span data-stu-id="40efb-157">Select the folder with your function app project and select the **HTTP trigger** function template.</span></span>

    ![Choose the HTTP trigger template](./media/functions-create-first-function-vs-code/create-function-choose-template.png)

1. <span data-ttu-id="40efb-159">Type `HTTPTrigger` for the function name and press Enter, then select **Anonymous** authentication.</span><span class="sxs-lookup"><span data-stu-id="40efb-159">Type `HTTPTrigger` for the function name and press Enter, then select **Anonymous** authentication.</span></span>

    ![Choose anonymous authentication](./media/functions-create-first-function-vs-code/create-function-anonymous-auth.png)

    <span data-ttu-id="40efb-161">A function is created in your chosen language using the template for an HTTP-triggered function.</span><span class="sxs-lookup"><span data-stu-id="40efb-161">A function is created in your chosen language using the template for an HTTP-triggered function.</span></span>

    ![HTTP triggered function template in Visual Studio Code](./media/functions-create-first-function-vs-code/new-function-full.png)

<span data-ttu-id="40efb-163">You can add input and output bindings to your function by modifying the function.json file.</span><span class="sxs-lookup"><span data-stu-id="40efb-163">You can add input and output bindings to your function by modifying the function.json file.</span></span> <span data-ttu-id="40efb-164">For more information, see  [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="40efb-164">For more information, see  [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

<span data-ttu-id="40efb-165">Now that you've created your function project and an HTTP-triggered function, you can test it on your local computer.</span><span class="sxs-lookup"><span data-stu-id="40efb-165">Now that you've created your function project and an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-the-function-locally"></a><span data-ttu-id="40efb-166">Test the function locally</span><span class="sxs-lookup"><span data-stu-id="40efb-166">Test the function locally</span></span>

<span data-ttu-id="40efb-167">Azure Functions Core Tools lets you run an Azure Functions project on your local development computer.</span><span class="sxs-lookup"><span data-stu-id="40efb-167">Azure Functions Core Tools lets you run an Azure Functions project on your local development computer.</span></span> <span data-ttu-id="40efb-168">You're prompted to install these tools the first time you start a function from Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="40efb-168">You're prompted to install these tools the first time you start a function from Visual Studio Code.</span></span>  

1. <span data-ttu-id="40efb-169">To test your function, set a breakpoint in the function code and press F5 to start the function app project.</span><span class="sxs-lookup"><span data-stu-id="40efb-169">To test your function, set a breakpoint in the function code and press F5 to start the function app project.</span></span> <span data-ttu-id="40efb-170">Output from Core Tools is displayed in the **Terminal** panel.</span><span class="sxs-lookup"><span data-stu-id="40efb-170">Output from Core Tools is displayed in the **Terminal** panel.</span></span>

1. <span data-ttu-id="40efb-171">In the **Terminal** panel, copy the URL endpoint of your HTTP-triggered function.</span><span class="sxs-lookup"><span data-stu-id="40efb-171">In the **Terminal** panel, copy the URL endpoint of your HTTP-triggered function.</span></span>

    ![Azure local output](./media/functions-create-first-function-vs-code/functions-vscode-f5.png)

1. <span data-ttu-id="40efb-173">Paste the URL for the HTTP request into your browser's address bar.</span><span class="sxs-lookup"><span data-stu-id="40efb-173">Paste the URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="40efb-174">Append the query string `?name=<yourname>` to this URL and execute the request.</span><span class="sxs-lookup"><span data-stu-id="40efb-174">Append the query string `?name=<yourname>` to this URL and execute the request.</span></span> <span data-ttu-id="40efb-175">Execution is paused when the breakpoint is hit.</span><span class="sxs-lookup"><span data-stu-id="40efb-175">Execution is paused when the breakpoint is hit.</span></span>

    ![Function hitting breakpoint in Visual Studio Code](./media/functions-create-first-function-vs-code/function-debug-vscode-js.png)

1. <span data-ttu-id="40efb-177">When you continue the execution, the following shows the response in the browser to the GET request:</span><span class="sxs-lookup"><span data-stu-id="40efb-177">When you continue the execution, the following shows the response in the browser to the GET request:</span></span>

    ![Function localhost response in the browser](./media/functions-create-first-function-vs-code/functions-test-local-browser.png)

1. <span data-ttu-id="40efb-179">To stop debugging, press Shift + F1.</span><span class="sxs-lookup"><span data-stu-id="40efb-179">To stop debugging, press Shift + F1.</span></span>

<span data-ttu-id="40efb-180">After you've verified that the function runs correctly on your local computer, it's time to publish the project to Azure.</span><span class="sxs-lookup"><span data-stu-id="40efb-180">After you've verified that the function runs correctly on your local computer, it's time to publish the project to Azure.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="40efb-181">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="40efb-181">Sign in to Azure</span></span>

<span data-ttu-id="40efb-182">Before you can publish your app, you must sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="40efb-182">Before you can publish your app, you must sign in to Azure.</span></span>

1. <span data-ttu-id="40efb-183">In the **Azure: Functions** area, choose **Sign in to Azure...**. If you don't already have one, you can **Create a free Azure account**.</span><span class="sxs-lookup"><span data-stu-id="40efb-183">In the **Azure: Functions** area, choose **Sign in to Azure...**. If you don't already have one, you can **Create a free Azure account**.</span></span>

    ![Function localhost response in the browser](./media/functions-create-first-function-vs-code/functions-sign-into-azure.png)

1. <span data-ttu-id="40efb-185">When prompted, select **Copy & Open**, or copy the displayed code and open <https://aka.ms/devicelogin> in your browser.</span><span class="sxs-lookup"><span data-stu-id="40efb-185">When prompted, select **Copy & Open**, or copy the displayed code and open <https://aka.ms/devicelogin> in your browser.</span></span>

1. <span data-ttu-id="40efb-186">Paste the copied code in the **Device Login** page, verify the sign-in for Visual Studio Code, then select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="40efb-186">Paste the copied code in the **Device Login** page, verify the sign-in for Visual Studio Code, then select **Continue**.</span></span>  

1. <span data-ttu-id="40efb-187">Complete the sign-in using your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="40efb-187">Complete the sign-in using your Azure account credentials.</span></span> <span data-ttu-id="40efb-188">After you have successfully signed in, you can close the browser.</span><span class="sxs-lookup"><span data-stu-id="40efb-188">After you have successfully signed in, you can close the browser.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="40efb-189">Publish the project to Azure</span><span class="sxs-lookup"><span data-stu-id="40efb-189">Publish the project to Azure</span></span>

<span data-ttu-id="40efb-190">Visual Studio Code lets you publish your functions project directly to Azure.</span><span class="sxs-lookup"><span data-stu-id="40efb-190">Visual Studio Code lets you publish your functions project directly to Azure.</span></span> <span data-ttu-id="40efb-191">In the process, you create a function app and related resources in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="40efb-191">In the process, you create a function app and related resources in your Azure subscription.</span></span> <span data-ttu-id="40efb-192">The function app provides an execution context for your functions.</span><span class="sxs-lookup"><span data-stu-id="40efb-192">The function app provides an execution context for your functions.</span></span> <span data-ttu-id="40efb-193">The project is packaged and deployed to the new function app in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="40efb-193">The project is packaged and deployed to the new function app in your Azure subscription.</span></span> 

<span data-ttu-id="40efb-194">This article assumes that you are creating a new function app.</span><span class="sxs-lookup"><span data-stu-id="40efb-194">This article assumes that you are creating a new function app.</span></span> <span data-ttu-id="40efb-195">Publishing to an existing function app overwrites the content of that app in Azure.</span><span class="sxs-lookup"><span data-stu-id="40efb-195">Publishing to an existing function app overwrites the content of that app in Azure.</span></span>

1. <span data-ttu-id="40efb-196">In the **Azure: Functions** area, select the Deploy to Function App icon.</span><span class="sxs-lookup"><span data-stu-id="40efb-196">In the **Azure: Functions** area, select the Deploy to Function App icon.</span></span>

    ![Function app settings](./media/functions-create-first-function-vs-code/function-app-publish-project.png)

1. <span data-ttu-id="40efb-198">Choose the project folder, which is your current workspace.</span><span class="sxs-lookup"><span data-stu-id="40efb-198">Choose the project folder, which is your current workspace.</span></span>

1. <span data-ttu-id="40efb-199">If you have more than one subscription, choose the one you want to host your function app, then choose **+ Create New Function App**.</span><span class="sxs-lookup"><span data-stu-id="40efb-199">If you have more than one subscription, choose the one you want to host your function app, then choose **+ Create New Function App**.</span></span>

1. <span data-ttu-id="40efb-200">Type a globally unique name that identifies your function app and press Enter.</span><span class="sxs-lookup"><span data-stu-id="40efb-200">Type a globally unique name that identifies your function app and press Enter.</span></span> <span data-ttu-id="40efb-201">Valid characters for a function app name are `a-z`, `0-9`, and `-`.</span><span class="sxs-lookup"><span data-stu-id="40efb-201">Valid characters for a function app name are `a-z`, `0-9`, and `-`.</span></span>

1. <span data-ttu-id="40efb-202">Choose **+ Create New Resource Group**, type a resource group name, like `myResourceGroup`, and press enter.</span><span class="sxs-lookup"><span data-stu-id="40efb-202">Choose **+ Create New Resource Group**, type a resource group name, like `myResourceGroup`, and press enter.</span></span> <span data-ttu-id="40efb-203">You can also use an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="40efb-203">You can also use an existing resource group.</span></span>

1. <span data-ttu-id="40efb-204">Choose **+Create New Storage Account**, type a globally unique name of the new storage account used by your function app and press Enter.</span><span class="sxs-lookup"><span data-stu-id="40efb-204">Choose **+Create New Storage Account**, type a globally unique name of the new storage account used by your function app and press Enter.</span></span> <span data-ttu-id="40efb-205">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span><span class="sxs-lookup"><span data-stu-id="40efb-205">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> <span data-ttu-id="40efb-206">You can also use an existing account.</span><span class="sxs-lookup"><span data-stu-id="40efb-206">You can also use an existing account.</span></span>

1. <span data-ttu-id="40efb-207">Choose a location in a [region](https://azure.microsoft.com/regions/) near you or near other services your functions access.</span><span class="sxs-lookup"><span data-stu-id="40efb-207">Choose a location in a [region](https://azure.microsoft.com/regions/) near you or near other services your functions access.</span></span>

    <span data-ttu-id="40efb-208">Function app creation starts after you choose your location.</span><span class="sxs-lookup"><span data-stu-id="40efb-208">Function app creation starts after you choose your location.</span></span> <span data-ttu-id="40efb-209">A notification is displayed after your function app is created and the deployment package is applied.</span><span class="sxs-lookup"><span data-stu-id="40efb-209">A notification is displayed after your function app is created and the deployment package is applied.</span></span>

1. <span data-ttu-id="40efb-210">Select **View Output** in the notifications to view the creation and deployment results, including the Azure resources that you created.</span><span class="sxs-lookup"><span data-stu-id="40efb-210">Select **View Output** in the notifications to view the creation and deployment results, including the Azure resources that you created.</span></span>

    ![Function app creation output](./media/functions-create-first-function-vs-code/function-create-notifications.png)

1. <span data-ttu-id="40efb-212">Make a note of the URL of the new function app in Azure.</span><span class="sxs-lookup"><span data-stu-id="40efb-212">Make a note of the URL of the new function app in Azure.</span></span> <span data-ttu-id="40efb-213">You use this to test your function after the project is published to Azure.</span><span class="sxs-lookup"><span data-stu-id="40efb-213">You use this to test your function after the project is published to Azure.</span></span>

    ![Function app creation output](./media/functions-create-first-function-vs-code/function-create-output.png)

1. <span data-ttu-id="40efb-215">Back in the **Azure: Functions** area, you see the new function app displayed under your subscription.</span><span class="sxs-lookup"><span data-stu-id="40efb-215">Back in the **Azure: Functions** area, you see the new function app displayed under your subscription.</span></span> <span data-ttu-id="40efb-216">When you expand this node, you see the functions in the function app, as well as application settings and function proxies.</span><span class="sxs-lookup"><span data-stu-id="40efb-216">When you expand this node, you see the functions in the function app, as well as application settings and function proxies.</span></span>

    ![Function app settings](./media/functions-create-first-function-vs-code/function-app-project-settings.png)

    <span data-ttu-id="40efb-218">From your function app node, type Ctrl and click (right-click) to choose to perform various management and configuration tasks against the function app in Azure.</span><span class="sxs-lookup"><span data-stu-id="40efb-218">From your function app node, type Ctrl and click (right-click) to choose to perform various management and configuration tasks against the function app in Azure.</span></span> <span data-ttu-id="40efb-219">You can also choose to view the function app in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="40efb-219">You can also choose to view the function app in the Azure portal.</span></span>

## <a name="test-your-function-in-azure"></a><span data-ttu-id="40efb-220">Test your function in Azure</span><span class="sxs-lookup"><span data-stu-id="40efb-220">Test your function in Azure</span></span>

1. <span data-ttu-id="40efb-221">Copy the URL of the HTTP trigger from the **Output** panel.</span><span class="sxs-lookup"><span data-stu-id="40efb-221">Copy the URL of the HTTP trigger from the **Output** panel.</span></span> <span data-ttu-id="40efb-222">As before, make sure to add the query string `?name=<yourname>` to the end of this URL and execute the request.</span><span class="sxs-lookup"><span data-stu-id="40efb-222">As before, make sure to add the query string `?name=<yourname>` to the end of this URL and execute the request.</span></span>

    <span data-ttu-id="40efb-223">The URL that calls your HTTP-triggered function should be in the following format:</span><span class="sxs-lookup"><span data-stu-id="40efb-223">The URL that calls your HTTP-triggered function should be in the following format:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

1. <span data-ttu-id="40efb-224">Paste this new URL for the HTTP request into your browser's address bar.</span><span class="sxs-lookup"><span data-stu-id="40efb-224">Paste this new URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="40efb-225">The following shows the response in the browser to the remote GET request returned by the function:</span><span class="sxs-lookup"><span data-stu-id="40efb-225">The following shows the response in the browser to the remote GET request returned by the function:</span></span> 

    ![Function response in the browser](./media/functions-create-first-function-vs-code/functions-test-remote-browser.png)

## <a name="next-steps"></a><span data-ttu-id="40efb-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="40efb-227">Next steps</span></span>

<span data-ttu-id="40efb-228">You have used Visual Studio Code to create a function app with a simple HTTP-triggered function.</span><span class="sxs-lookup"><span data-stu-id="40efb-228">You have used Visual Studio Code to create a function app with a simple HTTP-triggered function.</span></span> <span data-ttu-id="40efb-229">To learn more about developing functions in a specific language, see the language reference guides for [JavaScript](functions-reference-node.md), [.NET](functions-dotnet-class-library.md), or [Java](functions-reference-java.md).</span><span class="sxs-lookup"><span data-stu-id="40efb-229">To learn more about developing functions in a specific language, see the language reference guides for [JavaScript](functions-reference-node.md), [.NET](functions-dotnet-class-library.md), or [Java](functions-reference-java.md).</span></span>

<span data-ttu-id="40efb-230">Next you may want to learn more about local testing and debugging from the Terminal or command prompt using the Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="40efb-230">Next you may want to learn more about local testing and debugging from the Terminal or command prompt using the Azure Functions Core Tools.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="40efb-231">Code and test locally</span><span class="sxs-lookup"><span data-stu-id="40efb-231">Code and test locally</span></span>](functions-run-local.md)

[Azure Functions Core Tools]: functions-run-local.md
[Azure Functions extension for Visual Studio Code]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions
