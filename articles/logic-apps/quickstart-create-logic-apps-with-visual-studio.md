---
title: Create logic apps that automate workflows with Visual Studio - Azure Logic Apps | Microsoft Docs
description: Quickstart for how to automate tasks, processes, and workflows with Azure Logic Apps in Visual Studio
services: logic-apps
ms.service: logic-apps
ms.workload: azure-vs
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: quickstart
ms.custom: mvc
ms.reviewer: klam, LADocs
ms.suite: integration
ms.date: 07/31/2018
ms.openlocfilehash: b8961edebd80d5f36d844734e3c93a4bd3b1f0cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866327"
---
# <a name="quickstart-create-and-automate-tasks-processes-and-workflows-with-azure-logic-apps---visual-studio"></a><span data-ttu-id="48c54-103">Quickstart: Create and automate tasks, processes, and workflows with Azure Logic Apps - Visual Studio</span><span class="sxs-lookup"><span data-stu-id="48c54-103">Quickstart: Create and automate tasks, processes, and workflows with Azure Logic Apps - Visual Studio</span></span>

<span data-ttu-id="48c54-104">With [Azure Logic Apps](../logic-apps/logic-apps-overview.md) and Visual Studio, you can create workflows for automating tasks and processes that integrate apps, data, systems, and services across enterprises and organizations.</span><span class="sxs-lookup"><span data-stu-id="48c54-104">With [Azure Logic Apps](../logic-apps/logic-apps-overview.md) and Visual Studio, you can create workflows for automating tasks and processes that integrate apps, data, systems, and services across enterprises and organizations.</span></span> <span data-ttu-id="48c54-105">This quickstart shows how you can design and build these workflows by creating logic apps in Visual Studio and deploying those apps to <a href="https://docs.microsoft.com/azure/guides/developer/azure-developer-guide" target="_blank">Azure</a> in the cloud.</span><span class="sxs-lookup"><span data-stu-id="48c54-105">This quickstart shows how you can design and build these workflows by creating logic apps in Visual Studio and deploying those apps to <a href="https://docs.microsoft.com/azure/guides/developer/azure-developer-guide" target="_blank">Azure</a> in the cloud.</span></span> <span data-ttu-id="48c54-106">And although you can perform these tasks in the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, Visual Studio lets you add logic apps to source control, publish different versions, and create Azure Resource Manager templates for different deployment environments.</span><span class="sxs-lookup"><span data-stu-id="48c54-106">And although you can perform these tasks in the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, Visual Studio lets you add logic apps to source control, publish different versions, and create Azure Resource Manager templates for different deployment environments.</span></span> 

<span data-ttu-id="48c54-107">If you're new to Azure Logic Apps and just want the basic concepts, try the [quickstart for creating a logic app in the Azure portal](../logic-apps/quickstart-create-first-logic-app-workflow.md) instead.</span><span class="sxs-lookup"><span data-stu-id="48c54-107">If you're new to Azure Logic Apps and just want the basic concepts, try the [quickstart for creating a logic app in the Azure portal](../logic-apps/quickstart-create-first-logic-app-workflow.md) instead.</span></span> <span data-ttu-id="48c54-108">The Logic App Designer in both the Azure portal and Visual Studio work similarly.</span><span class="sxs-lookup"><span data-stu-id="48c54-108">The Logic App Designer in both the Azure portal and Visual Studio work similarly.</span></span> 

<span data-ttu-id="48c54-109">Here, you create the same logic app as in the Azure portal quickstart but with Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="48c54-109">Here, you create the same logic app as in the Azure portal quickstart but with Visual Studio.</span></span> <span data-ttu-id="48c54-110">This logic app monitors a website's RSS feed and sends email for each new item posted on the site.</span><span class="sxs-lookup"><span data-stu-id="48c54-110">This logic app monitors a website's RSS feed and sends email for each new item posted on the site.</span></span> <span data-ttu-id="48c54-111">When you're done, your logic app looks like this high-level workflow:</span><span class="sxs-lookup"><span data-stu-id="48c54-111">When you're done, your logic app looks like this high-level workflow:</span></span>

![Finished logic app](./media/quickstart-create-logic-apps-with-visual-studio/overview.png)

<a name="prerequisites"></a>

<span data-ttu-id="48c54-113">Before you start, make sure that you have these items:</span><span class="sxs-lookup"><span data-stu-id="48c54-113">Before you start, make sure that you have these items:</span></span>

* <span data-ttu-id="48c54-114">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="48c54-114">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span>

* <span data-ttu-id="48c54-115">Download and install these tools, if you don't have them already:</span><span class="sxs-lookup"><span data-stu-id="48c54-115">Download and install these tools, if you don't have them already:</span></span> 

  * <span data-ttu-id="48c54-116"><a href="https://www.visualstudio.com/downloads" target="_blank">Visual Studio 2017 or Visual Studio 2015 - Community edition or greater</a>.</span><span class="sxs-lookup"><span data-stu-id="48c54-116"><a href="https://www.visualstudio.com/downloads" target="_blank">Visual Studio 2017 or Visual Studio 2015 - Community edition or greater</a>.</span></span> 
  <span data-ttu-id="48c54-117">This quickstart uses Visual Studio Community 2017, which is free.</span><span class="sxs-lookup"><span data-stu-id="48c54-117">This quickstart uses Visual Studio Community 2017, which is free.</span></span>

  * <span data-ttu-id="48c54-118"><a href="https://azure.microsoft.com/downloads/" target="_blank">Microsoft Azure SDK for .NET (2.9.1 or later)</a> and <a href="https://github.com/Azure/azure-powershell#installation" target="_blank">Azure PowerShell</a>.</span><span class="sxs-lookup"><span data-stu-id="48c54-118"><a href="https://azure.microsoft.com/downloads/" target="_blank">Microsoft Azure SDK for .NET (2.9.1 or later)</a> and <a href="https://github.com/Azure/azure-powershell#installation" target="_blank">Azure PowerShell</a>.</span></span> 
  <span data-ttu-id="48c54-119">Learn more about <a href="https://docs.microsoft.com/dotnet/azure/dotnet-tools?view=azure-dotnet">Azure SDK for .NET</a>.</span><span class="sxs-lookup"><span data-stu-id="48c54-119">Learn more about <a href="https://docs.microsoft.com/dotnet/azure/dotnet-tools?view=azure-dotnet">Azure SDK for .NET</a>.</span></span>

  * <span data-ttu-id="48c54-120"><a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551" target="_blank">Azure Logic Apps Tools for Visual Studio 2017</a> or the <a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio" target="_blank">Visual Studio 2015 version</a></span><span class="sxs-lookup"><span data-stu-id="48c54-120"><a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551" target="_blank">Azure Logic Apps Tools for Visual Studio 2017</a> or the <a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio" target="_blank">Visual Studio 2015 version</a></span></span>
  
    <span data-ttu-id="48c54-121">You can either download and install Azure Logic Apps Tools directly from the Visual Studio Marketplace, or learn <a href="https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions" target="_blank">how to install this extension from inside Visual Studio</a>.</span><span class="sxs-lookup"><span data-stu-id="48c54-121">You can either download and install Azure Logic Apps Tools directly from the Visual Studio Marketplace, or learn <a href="https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions" target="_blank">how to install this extension from inside Visual Studio</a>.</span></span> 
    <span data-ttu-id="48c54-122">Make sure that you restart Visual Studio after you finish installing.</span><span class="sxs-lookup"><span data-stu-id="48c54-122">Make sure that you restart Visual Studio after you finish installing.</span></span>

* <span data-ttu-id="48c54-123">An email account that's supported by Logic Apps, such as Office 365 Outlook, Outlook.com, or Gmail.</span><span class="sxs-lookup"><span data-stu-id="48c54-123">An email account that's supported by Logic Apps, such as Office 365 Outlook, Outlook.com, or Gmail.</span></span> <span data-ttu-id="48c54-124">For other providers, <a href="https://docs.microsoft.com/connectors/" target="_blank">review the connectors list here</a>.</span><span class="sxs-lookup"><span data-stu-id="48c54-124">For other providers, <a href="https://docs.microsoft.com/connectors/" target="_blank">review the connectors list here</a>.</span></span> <span data-ttu-id="48c54-125">This logic app uses Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="48c54-125">This logic app uses Office 365 Outlook.</span></span> <span data-ttu-id="48c54-126">If you use a different provider, the overall steps are the same, but your UI might slightly differ.</span><span class="sxs-lookup"><span data-stu-id="48c54-126">If you use a different provider, the overall steps are the same, but your UI might slightly differ.</span></span>

* <span data-ttu-id="48c54-127">Access to the web while using the embedded Logic App Designer</span><span class="sxs-lookup"><span data-stu-id="48c54-127">Access to the web while using the embedded Logic App Designer</span></span>

  <span data-ttu-id="48c54-128">The designer requires an internet connection to create resources in Azure and to read the properties and data from connectors in your logic app.</span><span class="sxs-lookup"><span data-stu-id="48c54-128">The designer requires an internet connection to create resources in Azure and to read the properties and data from connectors in your logic app.</span></span> 
  <span data-ttu-id="48c54-129">For example, if you use the Dynamics CRM Online connector, the designer checks your CRM instance for available default and custom properties.</span><span class="sxs-lookup"><span data-stu-id="48c54-129">For example, if you use the Dynamics CRM Online connector, the designer checks your CRM instance for available default and custom properties.</span></span>

## <a name="create-azure-resource-group-project"></a><span data-ttu-id="48c54-130">Create Azure resource group project</span><span class="sxs-lookup"><span data-stu-id="48c54-130">Create Azure resource group project</span></span>

<span data-ttu-id="48c54-131">To get started, create an [Azure Resource Group project](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="48c54-131">To get started, create an [Azure Resource Group project](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span> <span data-ttu-id="48c54-132">Learn more about [Azure resource groups and resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48c54-132">Learn more about [Azure resource groups and resources](../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="48c54-133">Start Visual Studio and sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="48c54-133">Start Visual Studio and sign in with your Azure account.</span></span>

2. <span data-ttu-id="48c54-134">On the **File** menu, select **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="48c54-134">On the **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="48c54-135">(Keyboard: Ctrl+Shift+N)</span><span class="sxs-lookup"><span data-stu-id="48c54-135">(Keyboard: Ctrl+Shift+N)</span></span>

   ![On "File" menu, select "New" > "Project"](./media/quickstart-create-logic-apps-with-visual-studio/create-new-visual-studio-project.png)

3. <span data-ttu-id="48c54-137">Under **Installed**, select **Visual C#** or **Visual Basic**.</span><span class="sxs-lookup"><span data-stu-id="48c54-137">Under **Installed**, select **Visual C#** or **Visual Basic**.</span></span> <span data-ttu-id="48c54-138">Select **Cloud** > **Azure Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="48c54-138">Select **Cloud** > **Azure Resource Group**.</span></span> <span data-ttu-id="48c54-139">Name your project, for example:</span><span class="sxs-lookup"><span data-stu-id="48c54-139">Name your project, for example:</span></span>

   ![Create Azure Resource Group project](./media/quickstart-create-logic-apps-with-visual-studio/create-azure-cloud-service-project.png)

4. <span data-ttu-id="48c54-141">Select the **Logic App** template.</span><span class="sxs-lookup"><span data-stu-id="48c54-141">Select the **Logic App** template.</span></span> 

   ![Select Logic App template](./media/quickstart-create-logic-apps-with-visual-studio/select-logic-app-template.png)

   <span data-ttu-id="48c54-143">After Visual Studio creates your project, Solution Explorer opens and shows your solution.</span><span class="sxs-lookup"><span data-stu-id="48c54-143">After Visual Studio creates your project, Solution Explorer opens and shows your solution.</span></span> 

   ![Solution Explorer shows new logic app solution and deployment file](./media/quickstart-create-logic-apps-with-visual-studio/logic-app-solution-created.png)

   <span data-ttu-id="48c54-145">In your solution, the **LogicApp.json** file not only stores the definition for your logic app but is also an Azure Resource Manager template that you can set up for deployment.</span><span class="sxs-lookup"><span data-stu-id="48c54-145">In your solution, the **LogicApp.json** file not only stores the definition for your logic app but is also an Azure Resource Manager template that you can set up for deployment.</span></span>

## <a name="create-blank-logic-app"></a><span data-ttu-id="48c54-146">Create blank logic app</span><span class="sxs-lookup"><span data-stu-id="48c54-146">Create blank logic app</span></span>

<span data-ttu-id="48c54-147">After you create your Azure Resource Group project, create and build your logic app starting from the **Blank Logic App** template.</span><span class="sxs-lookup"><span data-stu-id="48c54-147">After you create your Azure Resource Group project, create and build your logic app starting from the **Blank Logic App** template.</span></span>

1. <span data-ttu-id="48c54-148">In Solution Explorer, open the shortcut menu for the **LogicApp.json** file.</span><span class="sxs-lookup"><span data-stu-id="48c54-148">In Solution Explorer, open the shortcut menu for the **LogicApp.json** file.</span></span> <span data-ttu-id="48c54-149">Select **Open With Logic App Designer**.</span><span class="sxs-lookup"><span data-stu-id="48c54-149">Select **Open With Logic App Designer**.</span></span> <span data-ttu-id="48c54-150">(Keyboard: Ctrl+L)</span><span class="sxs-lookup"><span data-stu-id="48c54-150">(Keyboard: Ctrl+L)</span></span>

   ![Open logic app .json file with Logic App Designer](./media/quickstart-create-logic-apps-with-visual-studio/open-logic-app-designer.png)

2. <span data-ttu-id="48c54-152">For **Subscription**, select the Azure subscription that you to use.</span><span class="sxs-lookup"><span data-stu-id="48c54-152">For **Subscription**, select the Azure subscription that you to use.</span></span> <span data-ttu-id="48c54-153">For **Resource Group**, select **Create New...**, which creates a new Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="48c54-153">For **Resource Group**, select **Create New...**, which creates a new Azure resource group.</span></span> 

   ![Select Azure subscription, resource group, and resource location](./media/quickstart-create-logic-apps-with-visual-studio/select-azure-subscription-resource-group-location.png)

   <span data-ttu-id="48c54-155">Visual Studio needs your Azure subscription and a resource group for creating and deploying resources associated with your logic app and connections.</span><span class="sxs-lookup"><span data-stu-id="48c54-155">Visual Studio needs your Azure subscription and a resource group for creating and deploying resources associated with your logic app and connections.</span></span> 

   | <span data-ttu-id="48c54-156">Setting</span><span class="sxs-lookup"><span data-stu-id="48c54-156">Setting</span></span> | <span data-ttu-id="48c54-157">Example value</span><span class="sxs-lookup"><span data-stu-id="48c54-157">Example value</span></span> | <span data-ttu-id="48c54-158">Description</span><span class="sxs-lookup"><span data-stu-id="48c54-158">Description</span></span> | 
   | ------- | ------------- | ----------- | 
   | <span data-ttu-id="48c54-159">User profile list</span><span class="sxs-lookup"><span data-stu-id="48c54-159">User profile list</span></span> | <span data-ttu-id="48c54-160">Contoso</span><span class="sxs-lookup"><span data-stu-id="48c54-160">Contoso</span></span> <br> jamalhartnett@contoso.com | <span data-ttu-id="48c54-161">By default, the account that you used to sign in</span><span class="sxs-lookup"><span data-stu-id="48c54-161">By default, the account that you used to sign in</span></span> | 
   | <span data-ttu-id="48c54-162">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="48c54-162">**Subscription**</span></span> | <span data-ttu-id="48c54-163">Pay-As-You-Go</span><span class="sxs-lookup"><span data-stu-id="48c54-163">Pay-As-You-Go</span></span> <br> <span data-ttu-id="48c54-164">(jamalhartnett@contoso.com)</span><span class="sxs-lookup"><span data-stu-id="48c54-164">(jamalhartnett@contoso.com)</span></span> | <span data-ttu-id="48c54-165">The name for your Azure subscription and associated account</span><span class="sxs-lookup"><span data-stu-id="48c54-165">The name for your Azure subscription and associated account</span></span> |
   | <span data-ttu-id="48c54-166">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="48c54-166">**Resource Group**</span></span> | <span data-ttu-id="48c54-167">MyLogicApp-RG</span><span class="sxs-lookup"><span data-stu-id="48c54-167">MyLogicApp-RG</span></span> <br> <span data-ttu-id="48c54-168">(West US)</span><span class="sxs-lookup"><span data-stu-id="48c54-168">(West US)</span></span> | <span data-ttu-id="48c54-169">The Azure resource group and location for storing and deploying resources for your logic app</span><span class="sxs-lookup"><span data-stu-id="48c54-169">The Azure resource group and location for storing and deploying resources for your logic app</span></span> | 
   | <span data-ttu-id="48c54-170">**Location**</span><span class="sxs-lookup"><span data-stu-id="48c54-170">**Location**</span></span> | <span data-ttu-id="48c54-171">MyLogicApp-RG2</span><span class="sxs-lookup"><span data-stu-id="48c54-171">MyLogicApp-RG2</span></span> <br> <span data-ttu-id="48c54-172">(West US)</span><span class="sxs-lookup"><span data-stu-id="48c54-172">(West US)</span></span> | <span data-ttu-id="48c54-173">A different location if you don't want to use the resource group location</span><span class="sxs-lookup"><span data-stu-id="48c54-173">A different location if you don't want to use the resource group location</span></span> |
   ||||

3. <span data-ttu-id="48c54-174">The Logic Apps Designer opens and shows a page with an introduction video and commonly used triggers.</span><span class="sxs-lookup"><span data-stu-id="48c54-174">The Logic Apps Designer opens and shows a page with an introduction video and commonly used triggers.</span></span> <span data-ttu-id="48c54-175">Scroll past the video and triggers.</span><span class="sxs-lookup"><span data-stu-id="48c54-175">Scroll past the video and triggers.</span></span> <span data-ttu-id="48c54-176">Under **Templates**, select **Blank Logic App**.</span><span class="sxs-lookup"><span data-stu-id="48c54-176">Under **Templates**, select **Blank Logic App**.</span></span>

   ![Select "Blank Logic App"](./media/quickstart-create-logic-apps-with-visual-studio/choose-blank-logic-app-template.png)

## <a name="build-logic-app-workflow"></a><span data-ttu-id="48c54-178">Build logic app workflow</span><span class="sxs-lookup"><span data-stu-id="48c54-178">Build logic app workflow</span></span>

<span data-ttu-id="48c54-179">Next, add a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) that fires when a new RSS feed item appears.</span><span class="sxs-lookup"><span data-stu-id="48c54-179">Next, add a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) that fires when a new RSS feed item appears.</span></span> <span data-ttu-id="48c54-180">Every logic app must start with a trigger, which fires when specific criteria is met.</span><span class="sxs-lookup"><span data-stu-id="48c54-180">Every logic app must start with a trigger, which fires when specific criteria is met.</span></span> <span data-ttu-id="48c54-181">Each time the trigger fires, the Logic Apps engine creates a logic app instance that runs your workflow.</span><span class="sxs-lookup"><span data-stu-id="48c54-181">Each time the trigger fires, the Logic Apps engine creates a logic app instance that runs your workflow.</span></span>

1. <span data-ttu-id="48c54-182">In Logic App Designer, enter "rss" in the search box.</span><span class="sxs-lookup"><span data-stu-id="48c54-182">In Logic App Designer, enter "rss" in the search box.</span></span> <span data-ttu-id="48c54-183">Select this trigger: **When a feed item is published**</span><span class="sxs-lookup"><span data-stu-id="48c54-183">Select this trigger: **When a feed item is published**</span></span>

   ![Build your logic app by adding a trigger and actions](./media/quickstart-create-logic-apps-with-visual-studio/add-trigger-logic-app.png)

   <span data-ttu-id="48c54-185">The trigger now appears in the designer:</span><span class="sxs-lookup"><span data-stu-id="48c54-185">The trigger now appears in the designer:</span></span>

   ![RSS trigger appears in Logic App Designer](./media/quickstart-create-logic-apps-with-visual-studio/rss-trigger-logic-app.png)

2. <span data-ttu-id="48c54-187">To finish building the logic app, follow the workflow steps in the [Azure portal quickstart](../logic-apps/quickstart-create-first-logic-app-workflow.md#add-rss-trigger), then return to this article.</span><span class="sxs-lookup"><span data-stu-id="48c54-187">To finish building the logic app, follow the workflow steps in the [Azure portal quickstart](../logic-apps/quickstart-create-first-logic-app-workflow.md#add-rss-trigger), then return to this article.</span></span>

   <span data-ttu-id="48c54-188">When you're done, your logic app looks like this example:</span><span class="sxs-lookup"><span data-stu-id="48c54-188">When you're done, your logic app looks like this example:</span></span> 

   ![Finished logic app](./media/quickstart-create-logic-apps-with-visual-studio/finished-logic-app.png)

3. <span data-ttu-id="48c54-190">To save your logic app, save your Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="48c54-190">To save your logic app, save your Visual Studio solution.</span></span> <span data-ttu-id="48c54-191">(Keyboard: Ctrl + S)</span><span class="sxs-lookup"><span data-stu-id="48c54-191">(Keyboard: Ctrl + S)</span></span>

<span data-ttu-id="48c54-192">Now, before you can test your logic app, deploy your app to Azure.</span><span class="sxs-lookup"><span data-stu-id="48c54-192">Now, before you can test your logic app, deploy your app to Azure.</span></span>

## <a name="deploy-logic-app-to-azure"></a><span data-ttu-id="48c54-193">Deploy logic app to Azure</span><span class="sxs-lookup"><span data-stu-id="48c54-193">Deploy logic app to Azure</span></span>

<span data-ttu-id="48c54-194">Before you can run your logic app, deploy the app from Visual Studio to Azure, which just takes a few steps.</span><span class="sxs-lookup"><span data-stu-id="48c54-194">Before you can run your logic app, deploy the app from Visual Studio to Azure, which just takes a few steps.</span></span>

1. <span data-ttu-id="48c54-195">In Solution Explorer, on your project's shortcut menu, select **Deploy** > **New**.</span><span class="sxs-lookup"><span data-stu-id="48c54-195">In Solution Explorer, on your project's shortcut menu, select **Deploy** > **New**.</span></span> <span data-ttu-id="48c54-196">If prompted, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="48c54-196">If prompted, sign in with your Azure account.</span></span>

   ![Create logic app deployment](./media/quickstart-create-logic-apps-with-visual-studio/create-logic-app-deployment.png)

2. <span data-ttu-id="48c54-198">For this deployment, keep the Azure subscription, resource group, and other default settings.</span><span class="sxs-lookup"><span data-stu-id="48c54-198">For this deployment, keep the Azure subscription, resource group, and other default settings.</span></span> <span data-ttu-id="48c54-199">When you're ready, choose **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="48c54-199">When you're ready, choose **Deploy**.</span></span> 

   ![Deploy logic app to Azure resource group](./media/quickstart-create-logic-apps-with-visual-studio/select-azure-subscription-resource-group-deployment.png)

3. <span data-ttu-id="48c54-201">If the **Edit Parameters** box appears, provide the resource name for the logic app to use at deployment, then save your settings, for example:</span><span class="sxs-lookup"><span data-stu-id="48c54-201">If the **Edit Parameters** box appears, provide the resource name for the logic app to use at deployment, then save your settings, for example:</span></span>

   ![Provide deployment name for logic app](./media/quickstart-create-logic-apps-with-visual-studio/edit-parameters-deployment.png)

   <span data-ttu-id="48c54-203">When deployment starts, your app's deployment status appears in the Visual Studio **Output** window.</span><span class="sxs-lookup"><span data-stu-id="48c54-203">When deployment starts, your app's deployment status appears in the Visual Studio **Output** window.</span></span> 
   <span data-ttu-id="48c54-204">If the status doesn't appear, open the **Show output from** list, and select your Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="48c54-204">If the status doesn't appear, open the **Show output from** list, and select your Azure resource group.</span></span>

   ![Deployment status output](./media/quickstart-create-logic-apps-with-visual-studio/logic-app-output-window.png)

   <span data-ttu-id="48c54-206">After deployment finishes, your logic app is live in the Azure portal and checks the RSS feed based on your specified schedule (every minute).</span><span class="sxs-lookup"><span data-stu-id="48c54-206">After deployment finishes, your logic app is live in the Azure portal and checks the RSS feed based on your specified schedule (every minute).</span></span> 
   <span data-ttu-id="48c54-207">If the RSS feed has new items, your logic app sends an email for each new item.</span><span class="sxs-lookup"><span data-stu-id="48c54-207">If the RSS feed has new items, your logic app sends an email for each new item.</span></span> 
   <span data-ttu-id="48c54-208">Otherwise, your logic app waits until the next interval before checking again.</span><span class="sxs-lookup"><span data-stu-id="48c54-208">Otherwise, your logic app waits until the next interval before checking again.</span></span> 

   <span data-ttu-id="48c54-209">For example, here are sample emails that this logic app sends.</span><span class="sxs-lookup"><span data-stu-id="48c54-209">For example, here are sample emails that this logic app sends.</span></span> 
   <span data-ttu-id="48c54-210">If you don't get any emails, check your junk email folder.</span><span class="sxs-lookup"><span data-stu-id="48c54-210">If you don't get any emails, check your junk email folder.</span></span> 

   ![Outlook sends email for each new RSS item](./media/quickstart-create-logic-apps-with-visual-studio/outlook-email.png)

   <span data-ttu-id="48c54-212">Technically, when the trigger checks the RSS feed and finds new items, the trigger fires, and the Logic Apps engine creates an instance of your logic app workflow that runs the actions in the workflow.</span><span class="sxs-lookup"><span data-stu-id="48c54-212">Technically, when the trigger checks the RSS feed and finds new items, the trigger fires, and the Logic Apps engine creates an instance of your logic app workflow that runs the actions in the workflow.</span></span>
   <span data-ttu-id="48c54-213">If the trigger doesn't find new items, the trigger doesn't fire and "skips" instantiating the workflow.</span><span class="sxs-lookup"><span data-stu-id="48c54-213">If the trigger doesn't find new items, the trigger doesn't fire and "skips" instantiating the workflow.</span></span>

<span data-ttu-id="48c54-214">Congratulations, you've now successfully built and deployed your logic app with Visual Studio!</span><span class="sxs-lookup"><span data-stu-id="48c54-214">Congratulations, you've now successfully built and deployed your logic app with Visual Studio!</span></span> <span data-ttu-id="48c54-215">To manage your logic app and review its run history, see [Manage logic apps with Visual Studio](../logic-apps/manage-logic-apps-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="48c54-215">To manage your logic app and review its run history, see [Manage logic apps with Visual Studio](../logic-apps/manage-logic-apps-with-visual-studio.md).</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="48c54-216">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="48c54-216">Clean up resources</span></span>

<span data-ttu-id="48c54-217">When no longer needed, delete the resource group that contains your logic app and related resources.</span><span class="sxs-lookup"><span data-stu-id="48c54-217">When no longer needed, delete the resource group that contains your logic app and related resources.</span></span>

1. <span data-ttu-id="48c54-218">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with the same account used to create your logic app.</span><span class="sxs-lookup"><span data-stu-id="48c54-218">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with the same account used to create your logic app.</span></span> 

2. <span data-ttu-id="48c54-219">On the main Azure menu, select **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="48c54-219">On the main Azure menu, select **Resource groups**.</span></span>
<span data-ttu-id="48c54-220">Select the resource group for your logic app, and then select **Overview**.</span><span class="sxs-lookup"><span data-stu-id="48c54-220">Select the resource group for your logic app, and then select **Overview**.</span></span>

3. <span data-ttu-id="48c54-221">On the **Overview** page, choose **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="48c54-221">On the **Overview** page, choose **Delete resource group**.</span></span> <span data-ttu-id="48c54-222">Enter the resource group name as confirmation, and choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="48c54-222">Enter the resource group name as confirmation, and choose **Delete**.</span></span>

   !["Resource groups" > "Overview" > "Delete resource group"](./media/quickstart-create-logic-apps-with-visual-studio/delete-resource-group.png)

4. <span data-ttu-id="48c54-224">Delete the Visual Studio solution from your local computer.</span><span class="sxs-lookup"><span data-stu-id="48c54-224">Delete the Visual Studio solution from your local computer.</span></span>

## <a name="get-support"></a><span data-ttu-id="48c54-225">Get support</span><span class="sxs-lookup"><span data-stu-id="48c54-225">Get support</span></span>

* <span data-ttu-id="48c54-226">For questions, visit the <a href="https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps" target="_blank">Azure Logic Apps forum</a>.</span><span class="sxs-lookup"><span data-stu-id="48c54-226">For questions, visit the <a href="https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps" target="_blank">Azure Logic Apps forum</a>.</span></span>
* <span data-ttu-id="48c54-227">To submit or vote on feature ideas, visit the <a href="http://aka.ms/logicapps-wish" target="_blank">Logic Apps user feedback site</a>.</span><span class="sxs-lookup"><span data-stu-id="48c54-227">To submit or vote on feature ideas, visit the <a href="http://aka.ms/logicapps-wish" target="_blank">Logic Apps user feedback site</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48c54-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="48c54-228">Next steps</span></span>

<span data-ttu-id="48c54-229">In this article, you built, deployed, and ran your logic app with Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="48c54-229">In this article, you built, deployed, and ran your logic app with Visual Studio.</span></span> <span data-ttu-id="48c54-230">To learn more about managing and performing advanced deployment for logic apps with Visual Studio, see these articles:</span><span class="sxs-lookup"><span data-stu-id="48c54-230">To learn more about managing and performing advanced deployment for logic apps with Visual Studio, see these articles:</span></span>

> [!div class="nextstepaction"]
> * [<span data-ttu-id="48c54-231">Manage logic apps with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="48c54-231">Manage logic apps with Visual Studio</span></span>](../logic-apps/manage-logic-apps-with-visual-studio.md)
> * [<span data-ttu-id="48c54-232">Create deployment templates for logic apps with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="48c54-232">Create deployment templates for logic apps with Visual Studio</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
