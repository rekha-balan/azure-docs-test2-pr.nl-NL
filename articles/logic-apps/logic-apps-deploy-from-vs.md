---
title: Create, build, and deploy logic apps in Visual Studio - Azure Logic Apps | Microsoft Docs
description: Create Visual Studio projects so you can design, build, and deploy Azure Logic Apps.
author: jeffhollan
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: jehollan
ms.openlocfilehash: 336f3d2d78ab5883443be03f41fc7030a3c21b23
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554901"
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="91fa5-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="91fa5-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="91fa5-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to create and manage Azure Logic Apps, you might want to use Visual Studio for designing, building, and deploying your logic apps.</span><span class="sxs-lookup"><span data-stu-id="91fa5-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to create and manage Azure Logic Apps, you might want to use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="91fa5-105">Visual Studio provides rich tools like the Logic App Designer for you to create logic apps, configure deployment and automation templates, and deploy to any environment.</span><span class="sxs-lookup"><span data-stu-id="91fa5-105">Visual Studio provides rich tools like the Logic App Designer for you to create logic apps, configure deployment and automation templates, and deploy to any environment.</span></span> 

<span data-ttu-id="91fa5-106">To get started with Azure Logic Apps, learn [how to create your first logic app in the Azure portal](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="91fa5-106">To get started with Azure Logic Apps, learn [how to create your first logic app in the Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="91fa5-107">Installation steps</span><span class="sxs-lookup"><span data-stu-id="91fa5-107">Installation steps</span></span>

<span data-ttu-id="91fa5-108">To install and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="91fa5-108">To install and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="91fa5-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91fa5-109">Prerequisites</span></span>

* <span data-ttu-id="91fa5-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="91fa5-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="91fa5-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span><span class="sxs-lookup"><span data-stu-id="91fa5-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="91fa5-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="91fa5-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="91fa5-113">Access to the web when using the embedded designer</span><span class="sxs-lookup"><span data-stu-id="91fa5-113">Access to the web when using the embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="91fa5-114">Install Visual Studio tools for Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="91fa5-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="91fa5-115">After you install the prerequisites:</span><span class="sxs-lookup"><span data-stu-id="91fa5-115">After you install the prerequisites:</span></span>

1. <span data-ttu-id="91fa5-116">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="91fa5-116">Open Visual Studio.</span></span> <span data-ttu-id="91fa5-117">On the **Tools** menu, select **Extensions and Updates**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-117">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="91fa5-118">Expand the **Online** category so you can search online.</span><span class="sxs-lookup"><span data-stu-id="91fa5-118">Expand the **Online** category so you can search online.</span></span>
3. <span data-ttu-id="91fa5-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="91fa5-120">To download and install the extension, click **Download**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-120">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="91fa5-121">Restart Visual Studio after installation.</span><span class="sxs-lookup"><span data-stu-id="91fa5-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="91fa5-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and the [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from the Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="91fa5-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and the [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from the Visual Studio Marketplace.</span></span>

<span data-ttu-id="91fa5-123">After you finish installation, you can use the Azure Resource Group project with Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="91fa5-123">After you finish installation, you can use the Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="91fa5-124">Create your project</span><span class="sxs-lookup"><span data-stu-id="91fa5-124">Create your project</span></span>

1. <span data-ttu-id="91fa5-125">On the **File** menu, go to **New**, and select **Project**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-125">On the **File** menu, go to **New**, and select **Project**.</span></span> <span data-ttu-id="91fa5-126">Or to add your project to an existing solution, go to **Add**, and select **New Project**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-126">Or to add your project to an existing solution, go to **Add**, and select **New Project**.</span></span>

    ![File menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="91fa5-128">In the **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-128">In the **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="91fa5-129">Name your project, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-129">Name your project, and click **OK**.</span></span>

    ![Add new project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="91fa5-131">Select the **Logic App** template, which creates a blank logic app deployment template for you to use.</span><span class="sxs-lookup"><span data-stu-id="91fa5-131">Select the **Logic App** template, which creates a blank logic app deployment template for you to use.</span></span> <span data-ttu-id="91fa5-132">After you select your template, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-132">After you select your template, click **OK**.</span></span>

    ![Select Logic App template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="91fa5-134">You've now added your logic app project to your solution.</span><span class="sxs-lookup"><span data-stu-id="91fa5-134">You've now added your logic app project to your solution.</span></span> 
    <span data-ttu-id="91fa5-135">In the Solution Explorer, your deployment file should appear.</span><span class="sxs-lookup"><span data-stu-id="91fa5-135">In the Solution Explorer, your deployment file should appear.</span></span>

    ![Deployment file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="91fa5-137">Create your logic app with Logic App Designer</span><span class="sxs-lookup"><span data-stu-id="91fa5-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="91fa5-138">When you have an Azure Resource Group project that contains a logic app, you can open the Logic App Designer in Visual Studio to create your workflow.</span><span class="sxs-lookup"><span data-stu-id="91fa5-138">When you have an Azure Resource Group project that contains a logic app, you can open the Logic App Designer in Visual Studio to create your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="91fa5-139">The designer requires an internet connection to query connectors for available properties and data.</span><span class="sxs-lookup"><span data-stu-id="91fa5-139">The designer requires an internet connection to query connectors for available properties and data.</span></span> <span data-ttu-id="91fa5-140">For example, if you use the Dynamics CRM Online connector, the designer queries your CRM instance to show available custom and default properties.</span><span class="sxs-lookup"><span data-stu-id="91fa5-140">For example, if you use the Dynamics CRM Online connector, the designer queries your CRM instance to show available custom and default properties.</span></span>

1. <span data-ttu-id="91fa5-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="91fa5-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="91fa5-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="91fa5-143">Choose your Azure subscription, resource group, and location for your deployment template.</span><span class="sxs-lookup"><span data-stu-id="91fa5-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="91fa5-144">Designing a logic app creates API Connection resources that query for properties during design.</span><span class="sxs-lookup"><span data-stu-id="91fa5-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="91fa5-145">Visual Studio uses your selected resource group to create those connections during design time.</span><span class="sxs-lookup"><span data-stu-id="91fa5-145">Visual Studio uses your selected resource group to create those connections during design time.</span></span> <span data-ttu-id="91fa5-146">To view or change any API Connections, go to the Azure portal, and browse for **API Connections**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-146">To view or change any API Connections, go to the Azure portal, and browse for **API Connections**.</span></span>

    ![Subscription picker](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="91fa5-148">The designer uses the definition in the `<template>.json` file for rendering.</span><span class="sxs-lookup"><span data-stu-id="91fa5-148">The designer uses the definition in the `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="91fa5-149">Create and design your logic app.</span><span class="sxs-lookup"><span data-stu-id="91fa5-149">Create and design your logic app.</span></span> <span data-ttu-id="91fa5-150">Your deployment template is updated with your changes.</span><span class="sxs-lookup"><span data-stu-id="91fa5-150">Your deployment template is updated with your changes.</span></span>

    ![Logic App Designer in Visual Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="91fa5-152">Visual Studio adds `Microsoft.Web/connections` resources to your resource file for any connections your logic app needs to function.</span><span class="sxs-lookup"><span data-stu-id="91fa5-152">Visual Studio adds `Microsoft.Web/connections` resources to your resource file for any connections your logic app needs to function.</span></span> <span data-ttu-id="91fa5-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="91fa5-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in the Azure portal.</span></span>

### <a name="switch-to-json-code-view"></a><span data-ttu-id="91fa5-154">Switch to JSON code view</span><span class="sxs-lookup"><span data-stu-id="91fa5-154">Switch to JSON code view</span></span>

<span data-ttu-id="91fa5-155">To show the JSON representation for your logic app, select the **Code View** tab at the bottom of the designer.</span><span class="sxs-lookup"><span data-stu-id="91fa5-155">To show the JSON representation for your logic app, select the **Code View** tab at the bottom of the designer.</span></span>

<span data-ttu-id="91fa5-156">To switch back to the full resource JSON, right-click the `<template>.json` file, and select **Open**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-156">To switch back to the full resource JSON, right-click the `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-to-visual-studio-deployment-templates"></a><span data-ttu-id="91fa5-157">Add references for dependent resources to Visual Studio deployment templates</span><span class="sxs-lookup"><span data-stu-id="91fa5-157">Add references for dependent resources to Visual Studio deployment templates</span></span>

<span data-ttu-id="91fa5-158">When you want your logic app to reference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions), like parameters, in your logic app deployment template.</span><span class="sxs-lookup"><span data-stu-id="91fa5-158">When you want your logic app to reference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions), like parameters, in your logic app deployment template.</span></span> <span data-ttu-id="91fa5-159">For example, you might want your logic app to reference an Azure Function or integration account that you want to deploy alongside your logic app.</span><span class="sxs-lookup"><span data-stu-id="91fa5-159">For example, you might want your logic app to reference an Azure Function or integration account that you want to deploy alongside your logic app.</span></span> <span data-ttu-id="91fa5-160">Follow these guidelines about how to use parameters in your deployment template so that the Logic App Designer renders correctly.</span><span class="sxs-lookup"><span data-stu-id="91fa5-160">Follow these guidelines about how to use parameters in your deployment template so that the Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="91fa5-161">You can use logic app parameters in these kinds of triggers and actions:</span><span class="sxs-lookup"><span data-stu-id="91fa5-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="91fa5-162">Child workflow</span><span class="sxs-lookup"><span data-stu-id="91fa5-162">Child workflow</span></span>
*   <span data-ttu-id="91fa5-163">Function app</span><span class="sxs-lookup"><span data-stu-id="91fa5-163">Function app</span></span>
*   <span data-ttu-id="91fa5-164">APIM call</span><span class="sxs-lookup"><span data-stu-id="91fa5-164">APIM call</span></span>
*   <span data-ttu-id="91fa5-165">API connection runtime URL</span><span class="sxs-lookup"><span data-stu-id="91fa5-165">API connection runtime URL</span></span>

<span data-ttu-id="91fa5-166">And you can use these template functions: list below, includes parameters, variables, resourceId, concat, and so on.</span><span class="sxs-lookup"><span data-stu-id="91fa5-166">And you can use these template functions: list below, includes parameters, variables, resourceId, concat, and so on.</span></span> <span data-ttu-id="91fa5-167">For example, here's how you can replace the Azure Function resource ID:</span><span class="sxs-lookup"><span data-stu-id="91fa5-167">For example, here's how you can replace the Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
    "type":"string",
    "minLength":1,
    "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="91fa5-168">And where you'd use parameters:</span><span class="sxs-lookup"><span data-stu-id="91fa5-168">And where you'd use parameters:</span></span>

```
"MyFunction": {
        "type": "Function",
        "inputs": {
        "body":{},
        "function":{
        "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```

> [!NOTE] 
> <span data-ttu-id="91fa5-169">For the Logic App Designer to work when you use parameters, you must provide default values, for example:</span><span class="sxs-lookup"><span data-stu-id="91fa5-169">For the Logic App Designer to work when you use parameters, you must provide default values, for example:</span></span>
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a><span data-ttu-id="91fa5-170">Save your logic app</span><span class="sxs-lookup"><span data-stu-id="91fa5-170">Save your logic app</span></span>

<span data-ttu-id="91fa5-171">To save your logic app at anytime, go to **File** > **Save**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-171">To save your logic app at anytime, go to **File** > **Save**.</span></span> <span data-ttu-id="91fa5-172">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="91fa5-172">(`Ctrl+S`)</span></span> 

<span data-ttu-id="91fa5-173">If your logic app has any errors when you save your app, they appear in the Visual Studio **Outputs** window.</span><span class="sxs-lookup"><span data-stu-id="91fa5-173">If your logic app has any errors when you save your app, they appear in the Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="91fa5-174">Deploy your logic app from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="91fa5-174">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="91fa5-175">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span><span class="sxs-lookup"><span data-stu-id="91fa5-175">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="91fa5-176">In Solution Explorer, right-click your project, and go to **Deploy** > **New Deployment...**</span><span class="sxs-lookup"><span data-stu-id="91fa5-176">In Solution Explorer, right-click your project, and go to **Deploy** > **New Deployment...**</span></span>

    ![New deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="91fa5-178">When you're prompted, sign in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="91fa5-178">When you're prompted, sign in to your Azure subscription.</span></span> 

3. <span data-ttu-id="91fa5-179">Now you must select the details for the resource group where you want to deploy your logic app.</span><span class="sxs-lookup"><span data-stu-id="91fa5-179">Now you must select the details for the resource group where you want to deploy your logic app.</span></span> <span data-ttu-id="91fa5-180">When you're done, select **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-180">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="91fa5-181">Make sure that you select the correct template and parameters file for the resource group.</span><span class="sxs-lookup"><span data-stu-id="91fa5-181">Make sure that you select the correct template and parameters file for the resource group.</span></span> <span data-ttu-id="91fa5-182">For example, if you want to deploy to a production environment, choose the production parameters file.</span><span class="sxs-lookup"><span data-stu-id="91fa5-182">For example, if you want to deploy to a production environment, choose the production parameters file.</span></span>

    ![Deploy to resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="91fa5-184">The deployment status appears in the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="91fa5-184">The deployment status appears in the **Output** window.</span></span> 
    <span data-ttu-id="91fa5-185">You might have to select **Azure Provisioning** in the **Show output from** list.</span><span class="sxs-lookup"><span data-stu-id="91fa5-185">You might have to select **Azure Provisioning** in the **Show output from** list.</span></span>

    ![Deployment status output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="91fa5-187">In the future, you can edit your logic app in source control, and use Visual Studio to deploy new versions.</span><span class="sxs-lookup"><span data-stu-id="91fa5-187">In the future, you can edit your logic app in source control, and use Visual Studio to deploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="91fa5-188">If you change the definition in the Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span><span class="sxs-lookup"><span data-stu-id="91fa5-188">If you change the definition in the Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-to-an-existing-resource-group-project"></a><span data-ttu-id="91fa5-189">Add your logic app to an existing Resource Group project</span><span class="sxs-lookup"><span data-stu-id="91fa5-189">Add your logic app to an existing Resource Group project</span></span>

<span data-ttu-id="91fa5-190">If you have an existing Resource Group project, you can add your logic app to that project in the JSON Outline window.</span><span class="sxs-lookup"><span data-stu-id="91fa5-190">If you have an existing Resource Group project, you can add your logic app to that project in the JSON Outline window.</span></span> <span data-ttu-id="91fa5-191">You can also add another logic app alongside the app you previously created.</span><span class="sxs-lookup"><span data-stu-id="91fa5-191">You can also add another logic app alongside the app you previously created.</span></span>

1. <span data-ttu-id="91fa5-192">Open the `<template>.json` file.</span><span class="sxs-lookup"><span data-stu-id="91fa5-192">Open the `<template>.json` file.</span></span>

2. <span data-ttu-id="91fa5-193">To open the JSON Outline window, go to **View** > **Other Windows** > **JSON Outline**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-193">To open the JSON Outline window, go to **View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="91fa5-194">To add a resource to the template file, click **Add Resource** at the top of the JSON Outline window.</span><span class="sxs-lookup"><span data-stu-id="91fa5-194">To add a resource to the template file, click **Add Resource** at the top of the JSON Outline window.</span></span> <span data-ttu-id="91fa5-195">Or in the JSON Outline window, right-click **resources**, and select **Add New Resource**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-195">Or in the JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![JSON Outline window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="91fa5-197">In the **Add Resource** dialog box, find and select **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-197">In the **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="91fa5-198">Name your logic app, and choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="91fa5-198">Name your logic app, and choose **Add**.</span></span>

    ![Add resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="91fa5-200">Next Steps</span><span class="sxs-lookup"><span data-stu-id="91fa5-200">Next Steps</span></span>

* [<span data-ttu-id="91fa5-201">Manage logic apps with Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="91fa5-201">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="91fa5-202">View common examples and scenarios</span><span class="sxs-lookup"><span data-stu-id="91fa5-202">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="91fa5-203">Learn how to automate business processes with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="91fa5-203">Learn how to automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="91fa5-204">Learn how to integrate your systems with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="91fa5-204">Learn how to integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)











