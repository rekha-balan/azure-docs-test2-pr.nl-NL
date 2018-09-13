---
title: Manage logic apps with Visual Studio - Azure Logic Apps | Microsoft Docs
description: Manage logic apps and other Azure assets with Visual Studio Cloud Explorer
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: article
ms.custom: mvc
ms.date: 03/15/2018
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: d4de75238e48b8eb955095b5a3823f2fed799fae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866688"
---
# <a name="manage-logic-apps-with-visual-studio"></a><span data-ttu-id="9801b-103">Manage logic apps with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9801b-103">Manage logic apps with Visual Studio</span></span>

<span data-ttu-id="9801b-104">Although you can create, edit, manage, and deploy logic apps in the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, you can also use Visual Studio when you want to add logic apps to source control, publish different versions, and create [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) templates for different deployment environments.</span><span class="sxs-lookup"><span data-stu-id="9801b-104">Although you can create, edit, manage, and deploy logic apps in the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, you can also use Visual Studio when you want to add logic apps to source control, publish different versions, and create [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) templates for different deployment environments.</span></span> <span data-ttu-id="9801b-105">With Visual Studio Cloud Explorer, you can find and manage your logic apps along with other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="9801b-105">With Visual Studio Cloud Explorer, you can find and manage your logic apps along with other Azure resources.</span></span> <span data-ttu-id="9801b-106">For example, you can open, download, edit, run, view run history, disable, and enable logic apps that are already deployed in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9801b-106">For example, you can open, download, edit, run, view run history, disable, and enable logic apps that are already deployed in the Azure portal.</span></span> <span data-ttu-id="9801b-107">If you're new to working with Azure Logic Apps in Visual Studio, learn [how to create logic apps with Visual Studio](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9801b-107">If you're new to working with Azure Logic Apps in Visual Studio, learn [how to create logic apps with Visual Studio](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9801b-108">Deploying or publishing a logic app from Visual Studio overwrites the version of that app in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9801b-108">Deploying or publishing a logic app from Visual Studio overwrites the version of that app in the Azure portal.</span></span> <span data-ttu-id="9801b-109">So if you make changes in the Azure portal that you want to keep, make sure that you [refresh the logic app in Visual Studio](#refresh) from the Azure portal before the next time you deploy or publish from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9801b-109">So if you make changes in the Azure portal that you want to keep, make sure that you [refresh the logic app in Visual Studio](#refresh) from the Azure portal before the next time you deploy or publish from Visual Studio.</span></span>

<a name="requirements"></a>

## <a name="prerequisites"></a><span data-ttu-id="9801b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9801b-110">Prerequisites</span></span>

* <span data-ttu-id="9801b-111">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="9801b-111">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span>

* <span data-ttu-id="9801b-112">Download and install these tools, if you don't have them already:</span><span class="sxs-lookup"><span data-stu-id="9801b-112">Download and install these tools, if you don't have them already:</span></span> 

  * <span data-ttu-id="9801b-113"><a href="https://www.visualstudio.com/downloads" target="_blank">Visual Studio 2017 or Visual Studio 2015 - Community edition or greater</a>.</span><span class="sxs-lookup"><span data-stu-id="9801b-113"><a href="https://www.visualstudio.com/downloads" target="_blank">Visual Studio 2017 or Visual Studio 2015 - Community edition or greater</a>.</span></span> 
  <span data-ttu-id="9801b-114">This quickstart uses Visual Studio Community 2017, which is free.</span><span class="sxs-lookup"><span data-stu-id="9801b-114">This quickstart uses Visual Studio Community 2017, which is free.</span></span>

  * <span data-ttu-id="9801b-115"><a href="https://azure.microsoft.com/downloads/" target="_blank">Azure SDK (2.9.1 or later)</a> and <a href="https://github.com/Azure/azure-powershell#installation" target="_blank">Azure PowerShell</a></span><span class="sxs-lookup"><span data-stu-id="9801b-115"><a href="https://azure.microsoft.com/downloads/" target="_blank">Azure SDK (2.9.1 or later)</a> and <a href="https://github.com/Azure/azure-powershell#installation" target="_blank">Azure PowerShell</a></span></span>

  * <span data-ttu-id="9801b-116"><a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551" target="_blank">Azure Logic Apps Tools for Visual Studio 2017</a> or the <a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio" target="_blank">Visual Studio 2015 version</a></span><span class="sxs-lookup"><span data-stu-id="9801b-116"><a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551" target="_blank">Azure Logic Apps Tools for Visual Studio 2017</a> or the <a href="https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio" target="_blank">Visual Studio 2015 version</a></span></span> 
  
    <span data-ttu-id="9801b-117">You can either download and install Azure Logic Apps Tools directly from the Visual Studio Marketplace, or learn <a href="https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions" target="_blank">how to install this extension from inside Visual Studio</a>.</span><span class="sxs-lookup"><span data-stu-id="9801b-117">You can either download and install Azure Logic Apps Tools directly from the Visual Studio Marketplace, or learn <a href="https://docs.microsoft.com/visualstudio/ide/finding-and-using-visual-studio-extensions" target="_blank">how to install this extension from inside Visual Studio</a>.</span></span> 
    <span data-ttu-id="9801b-118">Make sure that you restart Visual Studio after you finish installing.</span><span class="sxs-lookup"><span data-stu-id="9801b-118">Make sure that you restart Visual Studio after you finish installing.</span></span>

* <span data-ttu-id="9801b-119">Access to the web while using the embedded Logic Apps Designer</span><span class="sxs-lookup"><span data-stu-id="9801b-119">Access to the web while using the embedded Logic Apps Designer</span></span>

  <span data-ttu-id="9801b-120">The designer requires an internet connection to create resources in Azure and to read the properties and data from connectors in your logic app.</span><span class="sxs-lookup"><span data-stu-id="9801b-120">The designer requires an internet connection to create resources in Azure and to read the properties and data from connectors in your logic app.</span></span> 
  <span data-ttu-id="9801b-121">For example, if you use the Dynamics CRM Online connector, the designer checks your CRM instance for available default and custom properties.</span><span class="sxs-lookup"><span data-stu-id="9801b-121">For example, if you use the Dynamics CRM Online connector, the designer checks your CRM instance for available default and custom properties.</span></span>

<a name="find-logic-apps-vs"></a>

## <a name="find-your-logic-apps"></a><span data-ttu-id="9801b-122">Find your logic apps</span><span class="sxs-lookup"><span data-stu-id="9801b-122">Find your logic apps</span></span>

<span data-ttu-id="9801b-123">In Visual Studio, you can find all the logic apps that are associated with your Azure subscription and are deployed in the Azure portal by using Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="9801b-123">In Visual Studio, you can find all the logic apps that are associated with your Azure subscription and are deployed in the Azure portal by using Cloud Explorer.</span></span>

1. <span data-ttu-id="9801b-124">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9801b-124">Open Visual Studio.</span></span> <span data-ttu-id="9801b-125">On the **View** menu, select **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9801b-125">On the **View** menu, select **Cloud Explorer**.</span></span>

2. <span data-ttu-id="9801b-126">In Cloud Explorer, choose **Account Management**.</span><span class="sxs-lookup"><span data-stu-id="9801b-126">In Cloud Explorer, choose **Account Management**.</span></span> <span data-ttu-id="9801b-127">Select the Azure subscription associated with your logic apps, then choose **Apply**.</span><span class="sxs-lookup"><span data-stu-id="9801b-127">Select the Azure subscription associated with your logic apps, then choose **Apply**.</span></span> <span data-ttu-id="9801b-128">For example:</span><span class="sxs-lookup"><span data-stu-id="9801b-128">For example:</span></span>

   ![Choose "Account Management"](./media/manage-logic-apps-with-visual-studio/account-management-select-Azure-subscription.png)

2. <span data-ttu-id="9801b-130">Based on whether you're searching by **Resource Groups** or **Resource Types**, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="9801b-130">Based on whether you're searching by **Resource Groups** or **Resource Types**, follow these steps:</span></span>

   * <span data-ttu-id="9801b-131">**Resource Groups**: Under your Azure subscription, Cloud Explorer shows all the resource groups that are associated with that subscription.</span><span class="sxs-lookup"><span data-stu-id="9801b-131">**Resource Groups**: Under your Azure subscription, Cloud Explorer shows all the resource groups that are associated with that subscription.</span></span> 
   <span data-ttu-id="9801b-132">Expand the resource group that contains your logic app, then select your logic app.</span><span class="sxs-lookup"><span data-stu-id="9801b-132">Expand the resource group that contains your logic app, then select your logic app.</span></span>

   * <span data-ttu-id="9801b-133">**Resource Types**: Under your Azure subscription, expand **Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="9801b-133">**Resource Types**: Under your Azure subscription, expand **Logic Apps**.</span></span> <span data-ttu-id="9801b-134">After Cloud Explorer shows all the deployed logic apps that are associated with your subscription, select your logic app.</span><span class="sxs-lookup"><span data-stu-id="9801b-134">After Cloud Explorer shows all the deployed logic apps that are associated with your subscription, select your logic app.</span></span>

<a name="open-designer"></a>

## <a name="open-in-visual-studio"></a><span data-ttu-id="9801b-135">Open in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9801b-135">Open in Visual Studio</span></span>

<span data-ttu-id="9801b-136">In Visual Studio, you can open logic apps previously created and deployed either directly through the Azure portal or as Azure Resource Manager projects with Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9801b-136">In Visual Studio, you can open logic apps previously created and deployed either directly through the Azure portal or as Azure Resource Manager projects with Visual Studio.</span></span>

1. <span data-ttu-id="9801b-137">Open Cloud Explorer, and find your logic app.</span><span class="sxs-lookup"><span data-stu-id="9801b-137">Open Cloud Explorer, and find your logic app.</span></span> 

2. <span data-ttu-id="9801b-138">On the logic app's shortcut menu, select **Open with Logic App Editor**.</span><span class="sxs-lookup"><span data-stu-id="9801b-138">On the logic app's shortcut menu, select **Open with Logic App Editor**.</span></span>

   <span data-ttu-id="9801b-139">This example shows logic apps by resource type, so your logic apps appear under the **Logic Apps** section.</span><span class="sxs-lookup"><span data-stu-id="9801b-139">This example shows logic apps by resource type, so your logic apps appear under the **Logic Apps** section.</span></span>

  ![Open deployed logic app from Azure portal](./media/manage-logic-apps-with-visual-studio/open-logic-app-in-editor.png)

   <span data-ttu-id="9801b-141">After the logic app opens in Logic Apps Designer, at the bottom of the designer, you can choose **Code View** so that you can review the underlying logic app definition structure.</span><span class="sxs-lookup"><span data-stu-id="9801b-141">After the logic app opens in Logic Apps Designer, at the bottom of the designer, you can choose **Code View** so that you can review the underlying logic app definition structure.</span></span> 
   <span data-ttu-id="9801b-142">If you want to create a deployment template for the logic app, learn [how to download an Azure Resource Manager template](#download-logic-app) for that logic app.</span><span class="sxs-lookup"><span data-stu-id="9801b-142">If you want to create a deployment template for the logic app, learn [how to download an Azure Resource Manager template](#download-logic-app) for that logic app.</span></span> <span data-ttu-id="9801b-143">Learn more about [Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment).</span><span class="sxs-lookup"><span data-stu-id="9801b-143">Learn more about [Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment).</span></span>

<a name="download-logic-app"></a>

## <a name="download-from-azure"></a><span data-ttu-id="9801b-144">Download from Azure</span><span class="sxs-lookup"><span data-stu-id="9801b-144">Download from Azure</span></span>

<span data-ttu-id="9801b-145">You can download logic apps from the <a href="https://portal.azure.com" target="_blank">Azure portal</a> and save them as [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) templates.</span><span class="sxs-lookup"><span data-stu-id="9801b-145">You can download logic apps from the <a href="https://portal.azure.com" target="_blank">Azure portal</a> and save them as [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) templates.</span></span> <span data-ttu-id="9801b-146">You can then locally edit the templates with Visual Studio and customize logic apps for different deployment environments.</span><span class="sxs-lookup"><span data-stu-id="9801b-146">You can then locally edit the templates with Visual Studio and customize logic apps for different deployment environments.</span></span> <span data-ttu-id="9801b-147">Downloading logic apps automatically *parameterizes* their definitions inside [Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment), which also use JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="9801b-147">Downloading logic apps automatically *parameterizes* their definitions inside [Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment), which also use JavaScript Object Notation (JSON).</span></span>

1. <span data-ttu-id="9801b-148">In Visual Studio, open Cloud Explorer, then find and select the logic app that you want to download from Azure.</span><span class="sxs-lookup"><span data-stu-id="9801b-148">In Visual Studio, open Cloud Explorer, then find and select the logic app that you want to download from Azure.</span></span>

2. <span data-ttu-id="9801b-149">On that app's shortcut menu, select **Open with Logic App Editor**.</span><span class="sxs-lookup"><span data-stu-id="9801b-149">On that app's shortcut menu, select **Open with Logic App Editor**.</span></span>

   <span data-ttu-id="9801b-150">The Logic App Designer opens and shows the logic app.</span><span class="sxs-lookup"><span data-stu-id="9801b-150">The Logic App Designer opens and shows the logic app.</span></span> 
   <span data-ttu-id="9801b-151">To review logic app's underlying definition and structure, at the bottom of the designer, choose **Code View**.</span><span class="sxs-lookup"><span data-stu-id="9801b-151">To review logic app's underlying definition and structure, at the bottom of the designer, choose **Code View**.</span></span> 

3. <span data-ttu-id="9801b-152">On the designer toolbar, choose **Download**.</span><span class="sxs-lookup"><span data-stu-id="9801b-152">On the designer toolbar, choose **Download**.</span></span>

   ![Choose "Download"](./media/manage-logic-apps-with-visual-studio/download-logic-app.png)

4. <span data-ttu-id="9801b-154">When you're prompted for a location, browse to that location and save the Resource Manager template for the logic app definition in JSON (.json) file format.</span><span class="sxs-lookup"><span data-stu-id="9801b-154">When you're prompted for a location, browse to that location and save the Resource Manager template for the logic app definition in JSON (.json) file format.</span></span> 

<span data-ttu-id="9801b-155">Your logic app definition appears in the `resources` subsection inside the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="9801b-155">Your logic app definition appears in the `resources` subsection inside the Resource Manager template.</span></span> <span data-ttu-id="9801b-156">You can now edit the logic app definition and Resource Manager template with Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9801b-156">You can now edit the logic app definition and Resource Manager template with Visual Studio.</span></span> <span data-ttu-id="9801b-157">You can also add the template as an Azure Resource Manager project to a Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="9801b-157">You can also add the template as an Azure Resource Manager project to a Visual Studio solution.</span></span> <span data-ttu-id="9801b-158">Learn about [Resource Manager projects for logic apps in Visual Studio](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9801b-158">Learn about [Resource Manager projects for logic apps in Visual Studio](../logic-apps/quickstart-create-logic-apps-with-visual-studio.md).</span></span> 

<a name="refresh"></a>

## <a name="refresh-from-azure"></a><span data-ttu-id="9801b-159">Refresh from Azure</span><span class="sxs-lookup"><span data-stu-id="9801b-159">Refresh from Azure</span></span>

<span data-ttu-id="9801b-160">If you edit your logic app in the Azure portal and want to keep those changes, make sure that you refresh that app's version in Visual Studio with those changes.</span><span class="sxs-lookup"><span data-stu-id="9801b-160">If you edit your logic app in the Azure portal and want to keep those changes, make sure that you refresh that app's version in Visual Studio with those changes.</span></span> 

* <span data-ttu-id="9801b-161">In Visual Studio, on the Logic App Designer toolbar, choose **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="9801b-161">In Visual Studio, on the Logic App Designer toolbar, choose **Refresh**.</span></span>

  <span data-ttu-id="9801b-162">-or-</span><span class="sxs-lookup"><span data-stu-id="9801b-162">-or-</span></span>

* <span data-ttu-id="9801b-163">In Visual Studio Cloud Explorer, open your logic app's shortcut menu, and select **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="9801b-163">In Visual Studio Cloud Explorer, open your logic app's shortcut menu, and select **Refresh**.</span></span> 

![Refresh logic app with updates](./media/manage-logic-apps-with-visual-studio/refresh-logic-app.png)

## <a name="publish-logic-app-updates"></a><span data-ttu-id="9801b-165">Publish logic app updates</span><span class="sxs-lookup"><span data-stu-id="9801b-165">Publish logic app updates</span></span>

<span data-ttu-id="9801b-166">When you're ready to deploy your logic app updates from Visual Studio to Azure, on the Logic App Designer toolbar, choose **Publish**.</span><span class="sxs-lookup"><span data-stu-id="9801b-166">When you're ready to deploy your logic app updates from Visual Studio to Azure, on the Logic App Designer toolbar, choose **Publish**.</span></span>

![Publish updated logic app](./media/manage-logic-apps-with-visual-studio/publish-logic-app.png)

## <a name="manually-run-your-logic-app"></a><span data-ttu-id="9801b-168">Manually run your logic app</span><span class="sxs-lookup"><span data-stu-id="9801b-168">Manually run your logic app</span></span>

<span data-ttu-id="9801b-169">You can manually trigger a logic app deployed in Azure from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9801b-169">You can manually trigger a logic app deployed in Azure from Visual Studio.</span></span> <span data-ttu-id="9801b-170">On the Logic App Designer toolbar, choose **Run Trigger**.</span><span class="sxs-lookup"><span data-stu-id="9801b-170">On the Logic App Designer toolbar, choose **Run Trigger**.</span></span>

![Manually run logic app](./media/manage-logic-apps-with-visual-studio/manually-run-logic-app.png)

## <a name="review-run-history"></a><span data-ttu-id="9801b-172">Review run history</span><span class="sxs-lookup"><span data-stu-id="9801b-172">Review run history</span></span>

<span data-ttu-id="9801b-173">To check the status and diagnose problems with logic app runs, you can review the details, such as inputs and outputs, for those runs in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9801b-173">To check the status and diagnose problems with logic app runs, you can review the details, such as inputs and outputs, for those runs in Visual Studio.</span></span>

1. <span data-ttu-id="9801b-174">In Cloud Explorer, open your logic app's shortcut menu, and select **Open run history**.</span><span class="sxs-lookup"><span data-stu-id="9801b-174">In Cloud Explorer, open your logic app's shortcut menu, and select **Open run history**.</span></span>

   ![Open run history](./media/manage-logic-apps-with-visual-studio/view-run-history.png)

2. <span data-ttu-id="9801b-176">To view the details for a specific run, double-click a run.</span><span class="sxs-lookup"><span data-stu-id="9801b-176">To view the details for a specific run, double-click a run.</span></span> <span data-ttu-id="9801b-177">For example:</span><span class="sxs-lookup"><span data-stu-id="9801b-177">For example:</span></span>

   ![Detailed run history](./media/manage-logic-apps-with-visual-studio/view-run-history-details.png)
  
   > [!TIP]
   > <span data-ttu-id="9801b-179">To sort the table by property, choose the column header for that property.</span><span class="sxs-lookup"><span data-stu-id="9801b-179">To sort the table by property, choose the column header for that property.</span></span> 

3. <span data-ttu-id="9801b-180">Expand the steps whose inputs and outputs you want to review.</span><span class="sxs-lookup"><span data-stu-id="9801b-180">Expand the steps whose inputs and outputs you want to review.</span></span> <span data-ttu-id="9801b-181">For example:</span><span class="sxs-lookup"><span data-stu-id="9801b-181">For example:</span></span>

   ![View inputs and outputs for each step](./media/manage-logic-apps-with-visual-studio/run-inputs-outputs.png)

## <a name="disable-or-enable-logic-app"></a><span data-ttu-id="9801b-183">Disable or enable logic app</span><span class="sxs-lookup"><span data-stu-id="9801b-183">Disable or enable logic app</span></span>

<span data-ttu-id="9801b-184">Without deleting your logic app, you can stop the trigger from firing the next time when the trigger condition is met.</span><span class="sxs-lookup"><span data-stu-id="9801b-184">Without deleting your logic app, you can stop the trigger from firing the next time when the trigger condition is met.</span></span> <span data-ttu-id="9801b-185">Disabling your logic app prevents the Logic Apps engine from creating and running future workflow instances for your logic app.</span><span class="sxs-lookup"><span data-stu-id="9801b-185">Disabling your logic app prevents the Logic Apps engine from creating and running future workflow instances for your logic app.</span></span>
<span data-ttu-id="9801b-186">In Cloud Explorer, open your logic app's shortcut menu, and select **Disable**.</span><span class="sxs-lookup"><span data-stu-id="9801b-186">In Cloud Explorer, open your logic app's shortcut menu, and select **Disable**.</span></span>

![Disable your logic app](./media/manage-logic-apps-with-visual-studio/disable-logic-app.png)

> [!NOTE]
> <span data-ttu-id="9801b-188">When you disable a logic app, no new runs are instantiated.</span><span class="sxs-lookup"><span data-stu-id="9801b-188">When you disable a logic app, no new runs are instantiated.</span></span> <span data-ttu-id="9801b-189">All in-progress and pending runs will continue until they finish, which might take time to complete.</span><span class="sxs-lookup"><span data-stu-id="9801b-189">All in-progress and pending runs will continue until they finish, which might take time to complete.</span></span> 

<span data-ttu-id="9801b-190">When you're ready for your logic app to resume operation, you can reactivate your logic app.</span><span class="sxs-lookup"><span data-stu-id="9801b-190">When you're ready for your logic app to resume operation, you can reactivate your logic app.</span></span> <span data-ttu-id="9801b-191">In Cloud Explorer, open your logic app's shortcut menu, and select **Enable**.</span><span class="sxs-lookup"><span data-stu-id="9801b-191">In Cloud Explorer, open your logic app's shortcut menu, and select **Enable**.</span></span>

![Enable your logic app](./media/manage-logic-apps-with-visual-studio/enable-logic-app.png)

## <a name="delete-your-logic-app"></a><span data-ttu-id="9801b-193">Delete your logic app</span><span class="sxs-lookup"><span data-stu-id="9801b-193">Delete your logic app</span></span>

<span data-ttu-id="9801b-194">To delete your logic app from the Azure portal, in Cloud Explorer, open your logic app's shortcut menu, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="9801b-194">To delete your logic app from the Azure portal, in Cloud Explorer, open your logic app's shortcut menu, and select **Delete**.</span></span>

![Delete your logic app](./media/manage-logic-apps-with-visual-studio/delete-logic-app.png)

> [!NOTE]
> <span data-ttu-id="9801b-196">When you delete a logic app, no new runs are instantiated.</span><span class="sxs-lookup"><span data-stu-id="9801b-196">When you delete a logic app, no new runs are instantiated.</span></span> <span data-ttu-id="9801b-197">All in-progress and pending runs are canceled.</span><span class="sxs-lookup"><span data-stu-id="9801b-197">All in-progress and pending runs are canceled.</span></span> <span data-ttu-id="9801b-198">If you have thousands of runs, cancellation might take significant time to complete.</span><span class="sxs-lookup"><span data-stu-id="9801b-198">If you have thousands of runs, cancellation might take significant time to complete.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9801b-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="9801b-199">Next steps</span></span>

<span data-ttu-id="9801b-200">In this article, you learned how to manage deployed logic apps with Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9801b-200">In this article, you learned how to manage deployed logic apps with Visual Studio.</span></span> <span data-ttu-id="9801b-201">Next, learn about customizing logic app definitions for deployment:</span><span class="sxs-lookup"><span data-stu-id="9801b-201">Next, learn about customizing logic app definitions for deployment:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9801b-202">Author logic app definitions in JSON</span><span class="sxs-lookup"><span data-stu-id="9801b-202">Author logic app definitions in JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
