---
title: Build serverless apps with Visual Studio | Microsoft Docs
description: Build, deploy, and manage your first serverless app with Azure Logic Apps and Azure Functions in Visual Studio
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.custom: vs-azure
ms.topic: article
ms.date: 08/01/2018
ms.openlocfilehash: f5555d9a60934529bf8fed6db6a18dd783f46075
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870592"
---
# <a name="build-your-first-serverless-app-with-azure-logic-apps-and-azure-functions---visual-studio"></a><span data-ttu-id="15e9b-103">Build your first serverless app with Azure Logic Apps and Azure Functions - Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15e9b-103">Build your first serverless app with Azure Logic Apps and Azure Functions - Visual Studio</span></span>

<span data-ttu-id="15e9b-104">You can quickly develop and deploy cloud apps by using the serverless tools and capabilities in Azure such as [Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Azure Functions](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15e9b-104">You can quickly develop and deploy cloud apps by using the serverless tools and capabilities in Azure such as [Azure Logic Apps](../logic-apps/logic-apps-overview.md) and [Azure Functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="15e9b-105">This article shows how to start building a serverless app, which uses a logic app that calls an Azure function, in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15e9b-105">This article shows how to start building a serverless app, which uses a logic app that calls an Azure function, in Visual Studio.</span></span> <span data-ttu-id="15e9b-106">To learn more about serverless solutions in Azure, see [Azure Serverless with Functions and Logic Apps](../logic-apps/logic-apps-serverless-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15e9b-106">To learn more about serverless solutions in Azure, see [Azure Serverless with Functions and Logic Apps](../logic-apps/logic-apps-serverless-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15e9b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="15e9b-107">Prerequisites</span></span>

<span data-ttu-id="15e9b-108">To build a serverless app in Visual Studio, you need these items:</span><span class="sxs-lookup"><span data-stu-id="15e9b-108">To build a serverless app in Visual Studio, you need these items:</span></span>

* <span data-ttu-id="15e9b-109">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="15e9b-109">An Azure subscription.</span></span> <span data-ttu-id="15e9b-110">If you don't have an Azure subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="15e9b-110">If you don't have an Azure subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/).</span></span>

* <span data-ttu-id="15e9b-111">[Visual Studio 2017](https://www.visualstudio.com/vs/) or Visual Studio 2015 - Community, Professional, or Enterprise</span><span class="sxs-lookup"><span data-stu-id="15e9b-111">[Visual Studio 2017](https://www.visualstudio.com/vs/) or Visual Studio 2015 - Community, Professional, or Enterprise</span></span>

* <span data-ttu-id="15e9b-112">[Microsoft Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or later)</span><span class="sxs-lookup"><span data-stu-id="15e9b-112">[Microsoft Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or later)</span></span>

* [<span data-ttu-id="15e9b-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="15e9b-113">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)

* <span data-ttu-id="15e9b-114">[Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) or the [Visual Studio 2015 version](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio)</span><span class="sxs-lookup"><span data-stu-id="15e9b-114">[Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) or the [Visual Studio 2015 version](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio)</span></span>

  <span data-ttu-id="15e9b-115">You can either download and install Azure Logic Apps Tools directly from the Visual Studio Marketplace, or [learn how to install this extension from inside Visual Studio](https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions).</span><span class="sxs-lookup"><span data-stu-id="15e9b-115">You can either download and install Azure Logic Apps Tools directly from the Visual Studio Marketplace, or [learn how to install this extension from inside Visual Studio](https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions).</span></span> 
  <span data-ttu-id="15e9b-116">Make sure you restart Visual Studio after you finish installing.</span><span class="sxs-lookup"><span data-stu-id="15e9b-116">Make sure you restart Visual Studio after you finish installing.</span></span> 

* <span data-ttu-id="15e9b-117">[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools) for locally debugging Functions</span><span class="sxs-lookup"><span data-stu-id="15e9b-117">[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools) for locally debugging Functions</span></span>

* <span data-ttu-id="15e9b-118">Access to the web while using the Logic App Designer embedded in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15e9b-118">Access to the web while using the Logic App Designer embedded in Visual Studio</span></span>

  <span data-ttu-id="15e9b-119">The designer requires an internet connection to create resources in Azure and to read the properties and data from connectors in your logic app.</span><span class="sxs-lookup"><span data-stu-id="15e9b-119">The designer requires an internet connection to create resources in Azure and to read the properties and data from connectors in your logic app.</span></span> 
  <span data-ttu-id="15e9b-120">For example, if you use the Dynamics CRM Online connector, the designer checks your CRM instance for available default and custom properties.</span><span class="sxs-lookup"><span data-stu-id="15e9b-120">For example, if you use the Dynamics CRM Online connector, the designer checks your CRM instance for available default and custom properties.</span></span>

## <a name="create-resource-group-project"></a><span data-ttu-id="15e9b-121">Create resource group project</span><span class="sxs-lookup"><span data-stu-id="15e9b-121">Create resource group project</span></span>

<span data-ttu-id="15e9b-122">To get started, create an [Azure Resource Group project](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) for your serverless app.</span><span class="sxs-lookup"><span data-stu-id="15e9b-122">To get started, create an [Azure Resource Group project](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) for your serverless app.</span></span> <span data-ttu-id="15e9b-123">In Azure, you create resources within a resource group, which is a logical collection you use for organizing, managing, and deploying resources for an entire app as a single asset.</span><span class="sxs-lookup"><span data-stu-id="15e9b-123">In Azure, you create resources within a resource group, which is a logical collection you use for organizing, managing, and deploying resources for an entire app as a single asset.</span></span> <span data-ttu-id="15e9b-124">For a serverless app in Azure, your resource group includes resources for both Azure Logic Apps and Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="15e9b-124">For a serverless app in Azure, your resource group includes resources for both Azure Logic Apps and Azure Functions.</span></span> <span data-ttu-id="15e9b-125">Learn more about [Azure resource groups and resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15e9b-125">Learn more about [Azure resource groups and resources](../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="15e9b-126">Start Visual Studio, and sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="15e9b-126">Start Visual Studio, and sign in with your Azure account.</span></span> 

1. <span data-ttu-id="15e9b-127">On the **File** menu, select **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-127">On the **File** menu, select **New** > **Project**.</span></span> 

   ![Create new project in Visual Studio](./media/logic-apps-serverless-get-started-vs/create-new-project-visual-studio.png)

1. <span data-ttu-id="15e9b-129">Under **Installed**, select **Visual C#** or **Visual Basic**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-129">Under **Installed**, select **Visual C#** or **Visual Basic**.</span></span> <span data-ttu-id="15e9b-130">Select **Cloud** > **Azure Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-130">Select **Cloud** > **Azure Resource Group**.</span></span>

   <span data-ttu-id="15e9b-131">If the **Cloud** category or **Azure Resource Group** project doesn't exist, make sure you installed the Azure SDK for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15e9b-131">If the **Cloud** category or **Azure Resource Group** project doesn't exist, make sure you installed the Azure SDK for Visual Studio.</span></span>

1. <span data-ttu-id="15e9b-132">Give your project a name and a location, and then choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-132">Give your project a name and a location, and then choose **OK**.</span></span> 

   <span data-ttu-id="15e9b-133">Visual Studio prompts you to select a template.</span><span class="sxs-lookup"><span data-stu-id="15e9b-133">Visual Studio prompts you to select a template.</span></span> 
   <span data-ttu-id="15e9b-134">You can start with a blank, Logic App, or other template, but this example uses an Azure Quickstart Template for building a serverless app that includes a logic app and a call to an Azure function.</span><span class="sxs-lookup"><span data-stu-id="15e9b-134">You can start with a blank, Logic App, or other template, but this example uses an Azure Quickstart Template for building a serverless app that includes a logic app and a call to an Azure function.</span></span>

   <span data-ttu-id="15e9b-135">To create only a logic app in Visual Studio, select the **Logic App** template.</span><span class="sxs-lookup"><span data-stu-id="15e9b-135">To create only a logic app in Visual Studio, select the **Logic App** template.</span></span> <span data-ttu-id="15e9b-136">This template creates an empty logic app that opens in the Logic App Designer without having to predeploy your solution into an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="15e9b-136">This template creates an empty logic app that opens in the Logic App Designer without having to predeploy your solution into an Azure resource group.</span></span>

1. <span data-ttu-id="15e9b-137">Under **Show templates from this location**, select **Azure Quickstart (github/Azure/azure-quickstart-templates)**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-137">Under **Show templates from this location**, select **Azure Quickstart (github/Azure/azure-quickstart-templates)**.</span></span> 

1. <span data-ttu-id="15e9b-138">In the search box, enter "logic-app" as your filter, and select this serverless quickstart template and choose **OK**: **101-logic-app-and-function-app**</span><span class="sxs-lookup"><span data-stu-id="15e9b-138">In the search box, enter "logic-app" as your filter, and select this serverless quickstart template and choose **OK**: **101-logic-app-and-function-app**</span></span>

   ![Select Azure quickstart template](./media/logic-apps-serverless-get-started-vs/select-template.png)

   <span data-ttu-id="15e9b-140">Visual Studio creates and opens a solution for your resource group project.</span><span class="sxs-lookup"><span data-stu-id="15e9b-140">Visual Studio creates and opens a solution for your resource group project.</span></span> 
   <span data-ttu-id="15e9b-141">The quickstart template you selected creates a deployment template named `azuredeploy.json` inside your resource group project.</span><span class="sxs-lookup"><span data-stu-id="15e9b-141">The quickstart template you selected creates a deployment template named `azuredeploy.json` inside your resource group project.</span></span> 
   <span data-ttu-id="15e9b-142">This deployment template includes the definition for a simple logic app that triggers on an HTTP request, calls an Azure function, and returns the result as an HTTP response.</span><span class="sxs-lookup"><span data-stu-id="15e9b-142">This deployment template includes the definition for a simple logic app that triggers on an HTTP request, calls an Azure function, and returns the result as an HTTP response.</span></span> 
   
   ![New serverless solution](./media/logic-apps-serverless-get-started-vs/create-serverless-solution.png)

1. <span data-ttu-id="15e9b-144">Next, you must deploy your solution to Azure before you can open the deployment template and review the resources for your serverless app.</span><span class="sxs-lookup"><span data-stu-id="15e9b-144">Next, you must deploy your solution to Azure before you can open the deployment template and review the resources for your serverless app.</span></span> 

## <a name="deploy-your-solution"></a><span data-ttu-id="15e9b-145">Deploy your solution</span><span class="sxs-lookup"><span data-stu-id="15e9b-145">Deploy your solution</span></span>

<span data-ttu-id="15e9b-146">Before you can open your logic app with the Logic App Designer in Visual Studio, you must have an Azure resource group that's already deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="15e9b-146">Before you can open your logic app with the Logic App Designer in Visual Studio, you must have an Azure resource group that's already deployed in Azure.</span></span> <span data-ttu-id="15e9b-147">The designer can then create connections to resources and services in your logic app.</span><span class="sxs-lookup"><span data-stu-id="15e9b-147">The designer can then create connections to resources and services in your logic app.</span></span> <span data-ttu-id="15e9b-148">For this task, deploy your solution from Visual Studio to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="15e9b-148">For this task, deploy your solution from Visual Studio to the Azure portal.</span></span>

1. <span data-ttu-id="15e9b-149">In Solution Explorer, open your resource project's shortcut menu, and then select **Deploy** > **New**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-149">In Solution Explorer, open your resource project's shortcut menu, and then select **Deploy** > **New**.</span></span>

   ![Create new deployment for resource group](./media/logic-apps-serverless-get-started-vs/deploy.png)

1. <span data-ttu-id="15e9b-151">If not already selected, select your Azure subscription and the resource group to where you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="15e9b-151">If not already selected, select your Azure subscription and the resource group to where you want to deploy.</span></span> <span data-ttu-id="15e9b-152">Choose **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-152">Choose **Deploy**.</span></span>

   ![Deployment settings](./media/logic-apps-serverless-get-started-vs/deploy-to-resource-group.png)

1. <span data-ttu-id="15e9b-154">If the **Edit Parameters** box appears, provide the resource name to use for your logic app and your Azure function app at deployment, and then save your settings.</span><span class="sxs-lookup"><span data-stu-id="15e9b-154">If the **Edit Parameters** box appears, provide the resource name to use for your logic app and your Azure function app at deployment, and then save your settings.</span></span> <span data-ttu-id="15e9b-155">Make sure you use a globally unique name for your function app.</span><span class="sxs-lookup"><span data-stu-id="15e9b-155">Make sure you use a globally unique name for your function app.</span></span>

   ![Provide names for your logic app and function app](./media/logic-apps-serverless-get-started-vs/logic-function-app-name-parameters.png)

   <span data-ttu-id="15e9b-157">When Visual Studio starts deployment to your specified resource group, your solution's deployment status appears in the Visual Studio **Output** window.</span><span class="sxs-lookup"><span data-stu-id="15e9b-157">When Visual Studio starts deployment to your specified resource group, your solution's deployment status appears in the Visual Studio **Output** window.</span></span> 
   <span data-ttu-id="15e9b-158">After deployment finishes, your logic app is live in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="15e9b-158">After deployment finishes, your logic app is live in the Azure portal.</span></span>

## <a name="edit-logic-app-in-visual-studio"></a><span data-ttu-id="15e9b-159">Edit logic app in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15e9b-159">Edit logic app in Visual Studio</span></span>

<span data-ttu-id="15e9b-160">Now that your solution is deployed to your resource group, open your logic app with the Logic App Designer so you can edit and change your logic app.</span><span class="sxs-lookup"><span data-stu-id="15e9b-160">Now that your solution is deployed to your resource group, open your logic app with the Logic App Designer so you can edit and change your logic app.</span></span>

1. <span data-ttu-id="15e9b-161">In Solution Explorer, open the `azuredeploy.json` file's shortcut menu, and then select **Open With Logic App Designer**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-161">In Solution Explorer, open the `azuredeploy.json` file's shortcut menu, and then select **Open With Logic App Designer**.</span></span>

   ![Open "azuredeploy.json" in Logic App Designer](./media/logic-apps-serverless-get-started-vs/open-logic-app-designer.png)

1. <span data-ttu-id="15e9b-163">After the **Logic App Properties** box appears and if not already selected, under **Subscription**, select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="15e9b-163">After the **Logic App Properties** box appears and if not already selected, under **Subscription**, select your Azure subscription.</span></span> <span data-ttu-id="15e9b-164">Under **Resource Group**, select the resource group and location where you deployed your solution, and then choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-164">Under **Resource Group**, select the resource group and location where you deployed your solution, and then choose **OK**.</span></span>

   ![Logic app properties](./media/logic-apps-serverless-get-started-vs/logic-app-properties.png)

   <span data-ttu-id="15e9b-166">After the Logic App Designer opens, you can continue adding steps or change the workflow, and save your updates.</span><span class="sxs-lookup"><span data-stu-id="15e9b-166">After the Logic App Designer opens, you can continue adding steps or change the workflow, and save your updates.</span></span>

   ![Opened logic app in Logic App Designer](./media/logic-apps-serverless-get-started-vs/opened-logic-app.png)

## <a name="create-azure-functions-project"></a><span data-ttu-id="15e9b-168">Create Azure Functions project</span><span class="sxs-lookup"><span data-stu-id="15e9b-168">Create Azure Functions project</span></span>

<span data-ttu-id="15e9b-169">To create your Functions project and function with JavaScript, Python, F#, PowerShell, Batch, or Bash, follow the steps in the article, [Work with Azure Functions Core Tools](../azure-functions/functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="15e9b-169">To create your Functions project and function with JavaScript, Python, F#, PowerShell, Batch, or Bash, follow the steps in the article, [Work with Azure Functions Core Tools](../azure-functions/functions-run-local.md).</span></span> <span data-ttu-id="15e9b-170">To develop your Azure function with C# inside your solution, you can use a C# class library by following the steps in the article, [Publish a .NET class library as a Function App](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/).</span><span class="sxs-lookup"><span data-stu-id="15e9b-170">To develop your Azure function with C# inside your solution, you can use a C# class library by following the steps in the article, [Publish a .NET class library as a Function App](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/).</span></span>

## <a name="deploy-functions-from-visual-studio"></a><span data-ttu-id="15e9b-171">Deploy functions from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15e9b-171">Deploy functions from Visual Studio</span></span>

<span data-ttu-id="15e9b-172">Your deployment template deploys any Azure functions that you have in your solution from the Git repo that's specified by variables in the `azuredeploy.json` file.</span><span class="sxs-lookup"><span data-stu-id="15e9b-172">Your deployment template deploys any Azure functions that you have in your solution from the Git repo that's specified by variables in the `azuredeploy.json` file.</span></span> <span data-ttu-id="15e9b-173">If you create and author your Functions project in your solution, you can check that project into Git source control, for example, GitHub or Azure DevOps, and then update the `repo` variable so that the template deploys your Azure function.</span><span class="sxs-lookup"><span data-stu-id="15e9b-173">If you create and author your Functions project in your solution, you can check that project into Git source control, for example, GitHub or Azure DevOps, and then update the `repo` variable so that the template deploys your Azure function.</span></span>

## <a name="manage-logic-apps-and-view-run-history"></a><span data-ttu-id="15e9b-174">Manage logic apps and view run history</span><span class="sxs-lookup"><span data-stu-id="15e9b-174">Manage logic apps and view run history</span></span>

<span data-ttu-id="15e9b-175">For logic apps already deployed in Azure, you can still edit, manage, view run history, and disable those apps from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15e9b-175">For logic apps already deployed in Azure, you can still edit, manage, view run history, and disable those apps from Visual Studio.</span></span> 

1. <span data-ttu-id="15e9b-176">From the **View** menu in Visual Studio, open **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-176">From the **View** menu in Visual Studio, open **Cloud Explorer**.</span></span> 

1. <span data-ttu-id="15e9b-177">Under **All subscriptions**, select the Azure subscription associated with the logic apps you want to manage, and choose **Apply**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-177">Under **All subscriptions**, select the Azure subscription associated with the logic apps you want to manage, and choose **Apply**.</span></span>

1. <span data-ttu-id="15e9b-178">Under **Logic Apps**, select your logic app.</span><span class="sxs-lookup"><span data-stu-id="15e9b-178">Under **Logic Apps**, select your logic app.</span></span> <span data-ttu-id="15e9b-179">From that app's shortcut menu, select **Open with Logic App Editor**.</span><span class="sxs-lookup"><span data-stu-id="15e9b-179">From that app's shortcut menu, select **Open with Logic App Editor**.</span></span> 

<span data-ttu-id="15e9b-180">You can now download the already published logic app into your resource group project.</span><span class="sxs-lookup"><span data-stu-id="15e9b-180">You can now download the already published logic app into your resource group project.</span></span> <span data-ttu-id="15e9b-181">So although you might have started a logic app in the Azure portal, you can still import and manage that app in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15e9b-181">So although you might have started a logic app in the Azure portal, you can still import and manage that app in Visual Studio.</span></span> <span data-ttu-id="15e9b-182">For more information, see [Manage logic apps with Visual Studio](../logic-apps/manage-logic-apps-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="15e9b-182">For more information, see [Manage logic apps with Visual Studio](../logic-apps/manage-logic-apps-with-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="15e9b-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="15e9b-183">Next steps</span></span>

* [<span data-ttu-id="15e9b-184">Build a serverless social dashboard</span><span class="sxs-lookup"><span data-stu-id="15e9b-184">Build a serverless social dashboard</span></span>](logic-apps-scenario-social-serverless.md)
* [<span data-ttu-id="15e9b-185">Manage logic apps with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15e9b-185">Manage logic apps with Visual Studio</span></span>](manage-logic-apps-with-visual-studio.md)
* [<span data-ttu-id="15e9b-186">Logic App workflow definition language</span><span class="sxs-lookup"><span data-stu-id="15e9b-186">Logic App workflow definition language</span></span>](logic-apps-workflow-definition-language.md)