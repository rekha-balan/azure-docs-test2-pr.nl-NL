---
title: Create and manage integration accounts for B2B solutions - Azure Logic Apps | Microsoft Docs
description: Create, link, move, and delete integration accounts for enterprise integration and B2B solutions with Azure Logic Apps
services: logic-apps
documentationcenter: ''
author: ecfan
manager: jeconnoc
editor: ''
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: logic-apps
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: article
ms.date: 04/30/2018
ms.author: estfan
ms.openlocfilehash: 2a1fe501386884e02657d4b6cbef58ffc533fa33
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44777107"
---
# <a name="create-and-manage-integration-accounts-for-b2b-solutions-with-logic-apps"></a><span data-ttu-id="dd2dd-103">Create and manage integration accounts for B2B solutions with logic apps</span><span class="sxs-lookup"><span data-stu-id="dd2dd-103">Create and manage integration accounts for B2B solutions with logic apps</span></span>

<span data-ttu-id="dd2dd-104">Before you can build [enterprise integration and B2B solutions](../logic-apps/logic-apps-enterprise-integration-overview.md) with [Azure Logic Apps](../logic-apps/logic-apps-overview.md), you must first have an integration account, which is where you create, store, and manage B2B artifacts, such as trading partners, agreements, maps, schemas, certificates, and so on.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-104">Before you can build [enterprise integration and B2B solutions](../logic-apps/logic-apps-enterprise-integration-overview.md) with [Azure Logic Apps](../logic-apps/logic-apps-overview.md), you must first have an integration account, which is where you create, store, and manage B2B artifacts, such as trading partners, agreements, maps, schemas, certificates, and so on.</span></span> <span data-ttu-id="dd2dd-105">Before your logic app can work with the artifacts in your integration account and use the Logic Apps B2B connectors, such as XML validation, you must [link your integration account](#link-account) to your logic app.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-105">Before your logic app can work with the artifacts in your integration account and use the Logic Apps B2B connectors, such as XML validation, you must [link your integration account](#link-account) to your logic app.</span></span> <span data-ttu-id="dd2dd-106">To link them, both your integration account and logic app must have the *same* Azure location, or region.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-106">To link them, both your integration account and logic app must have the *same* Azure location, or region.</span></span>

<span data-ttu-id="dd2dd-107">This article shows you how to perform these tasks:</span><span class="sxs-lookup"><span data-stu-id="dd2dd-107">This article shows you how to perform these tasks:</span></span>

* <span data-ttu-id="dd2dd-108">Create your integration account.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-108">Create your integration account.</span></span>
* <span data-ttu-id="dd2dd-109">Link your integration account to a logic app.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-109">Link your integration account to a logic app.</span></span>
* <span data-ttu-id="dd2dd-110">Move your integration account to another Azure resource group or subscription.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-110">Move your integration account to another Azure resource group or subscription.</span></span>
* <span data-ttu-id="dd2dd-111">Delete your integration account.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-111">Delete your integration account.</span></span>

<span data-ttu-id="dd2dd-112">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-112">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="dd2dd-113">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="dd2dd-113">Sign in to the Azure portal</span></span>

<span data-ttu-id="dd2dd-114">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-114">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with your Azure account credentials.</span></span>

## <a name="create-integration-account"></a><span data-ttu-id="dd2dd-115">Create integration account</span><span class="sxs-lookup"><span data-stu-id="dd2dd-115">Create integration account</span></span>

1. <span data-ttu-id="dd2dd-116">From the main Azure menu, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-116">From the main Azure menu, select **All services**.</span></span> <span data-ttu-id="dd2dd-117">In the search box, enter "integration accounts" as your filter, and select **Integration accounts**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-117">In the search box, enter "integration accounts" as your filter, and select **Integration accounts**.</span></span>

   ![Find integration accounts](./media/logic-apps-enterprise-integration-create-integration-account/create-integration-account.png)

2. <span data-ttu-id="dd2dd-119">Under **Integration accounts**, choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-119">Under **Integration accounts**, choose **Add**.</span></span>

   ![Choose "Add" to create integration account](./media/logic-apps-enterprise-integration-create-integration-account/add-integration-account.png)

3. <span data-ttu-id="dd2dd-121">Provide information about your integration account:</span><span class="sxs-lookup"><span data-stu-id="dd2dd-121">Provide information about your integration account:</span></span> 

   ![Provide details for your integration account](./media/logic-apps-enterprise-integration-create-integration-account/integration-account-details.png)

   | <span data-ttu-id="dd2dd-123">Property</span><span class="sxs-lookup"><span data-stu-id="dd2dd-123">Property</span></span> | <span data-ttu-id="dd2dd-124">Required</span><span class="sxs-lookup"><span data-stu-id="dd2dd-124">Required</span></span> | <span data-ttu-id="dd2dd-125">Example value</span><span class="sxs-lookup"><span data-stu-id="dd2dd-125">Example value</span></span> | <span data-ttu-id="dd2dd-126">Description</span><span class="sxs-lookup"><span data-stu-id="dd2dd-126">Description</span></span> | 
   |----------|----------|---------------|-------------|
   | <span data-ttu-id="dd2dd-127">Name</span><span class="sxs-lookup"><span data-stu-id="dd2dd-127">Name</span></span> | <span data-ttu-id="dd2dd-128">Yes</span><span class="sxs-lookup"><span data-stu-id="dd2dd-128">Yes</span></span> | <span data-ttu-id="dd2dd-129">test-integration-account</span><span class="sxs-lookup"><span data-stu-id="dd2dd-129">test-integration-account</span></span> | <span data-ttu-id="dd2dd-130">The name for your integration account.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-130">The name for your integration account.</span></span> <span data-ttu-id="dd2dd-131">For this example, use the specified name.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-131">For this example, use the specified name.</span></span> | 
   | <span data-ttu-id="dd2dd-132">Subscription</span><span class="sxs-lookup"><span data-stu-id="dd2dd-132">Subscription</span></span> | <span data-ttu-id="dd2dd-133">Yes</span><span class="sxs-lookup"><span data-stu-id="dd2dd-133">Yes</span></span> | <span data-ttu-id="dd2dd-134"><*Azure-subscription-name*></span><span class="sxs-lookup"><span data-stu-id="dd2dd-134"><*Azure-subscription-name*></span></span> | <span data-ttu-id="dd2dd-135">The name for the Azure subscription to use</span><span class="sxs-lookup"><span data-stu-id="dd2dd-135">The name for the Azure subscription to use</span></span> | 
   | <span data-ttu-id="dd2dd-136">Resource group</span><span class="sxs-lookup"><span data-stu-id="dd2dd-136">Resource group</span></span> | <span data-ttu-id="dd2dd-137">Yes</span><span class="sxs-lookup"><span data-stu-id="dd2dd-137">Yes</span></span> | <span data-ttu-id="dd2dd-138">test-integration-account-rg</span><span class="sxs-lookup"><span data-stu-id="dd2dd-138">test-integration-account-rg</span></span> | <span data-ttu-id="dd2dd-139">The name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) used to organize related resources.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-139">The name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) used to organize related resources.</span></span> <span data-ttu-id="dd2dd-140">For this example, create a new resource group with the specified name.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-140">For this example, create a new resource group with the specified name.</span></span> | 
   | <span data-ttu-id="dd2dd-141">Pricing Tier</span><span class="sxs-lookup"><span data-stu-id="dd2dd-141">Pricing Tier</span></span> | <span data-ttu-id="dd2dd-142">Yes</span><span class="sxs-lookup"><span data-stu-id="dd2dd-142">Yes</span></span> | <span data-ttu-id="dd2dd-143">Free</span><span class="sxs-lookup"><span data-stu-id="dd2dd-143">Free</span></span> | <span data-ttu-id="dd2dd-144">The pricing tier that you want to use.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-144">The pricing tier that you want to use.</span></span> <span data-ttu-id="dd2dd-145">For this example, select **Free**, but for more information, see [Logic Apps limits and configuration](../logic-apps/logic-apps-limits-and-config.md) and [Logic Apps pricing](https://azure.microsoft.com/pricing/details/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="dd2dd-145">For this example, select **Free**, but for more information, see [Logic Apps limits and configuration](../logic-apps/logic-apps-limits-and-config.md) and [Logic Apps pricing](https://azure.microsoft.com/pricing/details/logic-apps/).</span></span> | 
   | <span data-ttu-id="dd2dd-146">Location</span><span class="sxs-lookup"><span data-stu-id="dd2dd-146">Location</span></span> | <span data-ttu-id="dd2dd-147">Yes</span><span class="sxs-lookup"><span data-stu-id="dd2dd-147">Yes</span></span> | <span data-ttu-id="dd2dd-148">West US</span><span class="sxs-lookup"><span data-stu-id="dd2dd-148">West US</span></span> | <span data-ttu-id="dd2dd-149">The region where to store your integration account information.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-149">The region where to store your integration account information.</span></span> <span data-ttu-id="dd2dd-150">Either select the same location as your logic app, or create a logic app in the same location as your integration account.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-150">Either select the same location as your logic app, or create a logic app in the same location as your integration account.</span></span> | 
   | <span data-ttu-id="dd2dd-151">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="dd2dd-151">Log Analytics</span></span> | <span data-ttu-id="dd2dd-152">No</span><span class="sxs-lookup"><span data-stu-id="dd2dd-152">No</span></span> | <span data-ttu-id="dd2dd-153">Off</span><span class="sxs-lookup"><span data-stu-id="dd2dd-153">Off</span></span> | <span data-ttu-id="dd2dd-154">Keep the **Off** setting for diagnostic logging.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-154">Keep the **Off** setting for diagnostic logging.</span></span> | 
   ||||| 

4. <span data-ttu-id="dd2dd-155">When you're ready, select **Pin to dashboard**, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-155">When you're ready, select **Pin to dashboard**, and choose **Create**.</span></span>

   <span data-ttu-id="dd2dd-156">After Azure deploys your integration account to the selected location, which usually finishes within one minute, Azure opens your integration account.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-156">After Azure deploys your integration account to the selected location, which usually finishes within one minute, Azure opens your integration account.</span></span>

   ![Azure opens your integration account](./media/logic-apps-enterprise-integration-create-integration-account/integration-account-created.png)

<span data-ttu-id="dd2dd-158">Now, before your logic app can use your integration account, you must link the integration account to your logic app.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-158">Now, before your logic app can use your integration account, you must link the integration account to your logic app.</span></span>

<a name="link-account"></a>

## <a name="link-to-logic-app"></a><span data-ttu-id="dd2dd-159">Link to logic app</span><span class="sxs-lookup"><span data-stu-id="dd2dd-159">Link to logic app</span></span>

<span data-ttu-id="dd2dd-160">To give your logic apps access to an integration account that contains your B2B artifacts, such as trading partners, agreements, maps, and schemas, you must link your integration account to your logic app.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-160">To give your logic apps access to an integration account that contains your B2B artifacts, such as trading partners, agreements, maps, and schemas, you must link your integration account to your logic app.</span></span> 

> [!NOTE]
> <span data-ttu-id="dd2dd-161">Your integration account and logic app must exist in the same region.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-161">Your integration account and logic app must exist in the same region.</span></span>

1. <span data-ttu-id="dd2dd-162">In the Azure portal, find and open your logic app.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-162">In the Azure portal, find and open your logic app.</span></span>

2. <span data-ttu-id="dd2dd-163">On your logic app's menu, under **Settings**, select **Workflow settings**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-163">On your logic app's menu, under **Settings**, select **Workflow settings**.</span></span> <span data-ttu-id="dd2dd-164">In the **Select an Integration account** list, select the integration account to link to your logic app.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-164">In the **Select an Integration account** list, select the integration account to link to your logic app.</span></span>

   ![Select your integration account](./media/logic-apps-enterprise-integration-create-integration-account/linkaccount-2.png)

3. <span data-ttu-id="dd2dd-166">To finish linking, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-166">To finish linking, choose **Save**.</span></span>

   ![Select your integration account](./media/logic-apps-enterprise-integration-create-integration-account/linkaccount-3.png)

   <span data-ttu-id="dd2dd-168">When your integration account is successfully linked, Azure shows a confirmation message.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-168">When your integration account is successfully linked, Azure shows a confirmation message.</span></span> 

   ![Azure confirms successful link](./media/logic-apps-enterprise-integration-create-integration-account/linkaccount-5.png)

<span data-ttu-id="dd2dd-170">Now your logic app can use any and all the artifacts in your integration account plus the B2B connectors, such as XML validation and flat file encoding or decoding.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-170">Now your logic app can use any and all the artifacts in your integration account plus the B2B connectors, such as XML validation and flat file encoding or decoding.</span></span>  

## <a name="unlink-from-logic-app"></a><span data-ttu-id="dd2dd-171">Unlink from logic app</span><span class="sxs-lookup"><span data-stu-id="dd2dd-171">Unlink from logic app</span></span>

<span data-ttu-id="dd2dd-172">To link your logic app to another integration account, or no longer use an integration account with your logic app, you can delete the link through Azure Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-172">To link your logic app to another integration account, or no longer use an integration account with your logic app, you can delete the link through Azure Resource Explorer.</span></span>

1. <span data-ttu-id="dd2dd-173">In your browser, go to <a href="https://resources.azure.com" target="_blank">Azure Resource Explorer (https://resources.azure.com)</a>.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-173">In your browser, go to <a href="https://resources.azure.com" target="_blank">Azure Resource Explorer (https://resources.azure.com)</a>.</span></span> <span data-ttu-id="dd2dd-174">Make sure that you're signed in with the same Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-174">Make sure that you're signed in with the same Azure credentials.</span></span>

   ![Azure Resource Explorer](./media/logic-apps-enterprise-integration-create-integration-account/resource-explorer.png)

2. <span data-ttu-id="dd2dd-176">In the search box, enter your logic app's name, then find and select your logic app.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-176">In the search box, enter your logic app's name, then find and select your logic app.</span></span>

   ![Find and select logic app](./media/logic-apps-enterprise-integration-create-integration-account/resource-explorer-find-logic-app.png)

3. <span data-ttu-id="dd2dd-178">On the explorer title bar, choose **Read/Write**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-178">On the explorer title bar, choose **Read/Write**.</span></span>

   ![Turn on "Read/Write" mode](./media/logic-apps-enterprise-integration-create-integration-account/resource-explorer-choose-read-write-mode.png)

4. <span data-ttu-id="dd2dd-180">On the **Data** tab, choose **Edit**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-180">On the **Data** tab, choose **Edit**.</span></span>

   ![On "Data" tab, choose "Edit"](./media/logic-apps-enterprise-integration-create-integration-account/resource-explorer-choose-edit.png)

5. <span data-ttu-id="dd2dd-182">In the editor, find the `integrationAccount` property for the integration account and delete that property, which has this format:</span><span class="sxs-lookup"><span data-stu-id="dd2dd-182">In the editor, find the `integrationAccount` property for the integration account and delete that property, which has this format:</span></span>

   ```json
   "integrationAccount": {
      "name": "<integration-account-name>",
      "id": "<integration-account-resource-ID>",
      "type": "Microsoft.Logic/integrationAccounts"  
   },
   ```

   <span data-ttu-id="dd2dd-183">For example:</span><span class="sxs-lookup"><span data-stu-id="dd2dd-183">For example:</span></span>

   ![Find "integrationAccount" property definition](./media/logic-apps-enterprise-integration-create-integration-account/resource-explorer-delete-integration-account.png)

6. <span data-ttu-id="dd2dd-185">On the **Data** tab, choose **Put** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-185">On the **Data** tab, choose **Put** to save your changes.</span></span> 

   ![Choose "Put" to save changes](./media/logic-apps-enterprise-integration-create-integration-account/resource-explorer-save-changes.png)

7. <span data-ttu-id="dd2dd-187">In the Azure portal, under your logic app's **Workflow settings**, check that the **Integration account** property now appears empty.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-187">In the Azure portal, under your logic app's **Workflow settings**, check that the **Integration account** property now appears empty.</span></span>

   ![Check that integration account is not linked](./media/logic-apps-enterprise-integration-create-integration-account/unlinked-account.png)

## <a name="move-integration-account"></a><span data-ttu-id="dd2dd-189">Move integration account</span><span class="sxs-lookup"><span data-stu-id="dd2dd-189">Move integration account</span></span>

<span data-ttu-id="dd2dd-190">You can move your integration account to another Azure subscription or resource group.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-190">You can move your integration account to another Azure subscription or resource group.</span></span>

1. <span data-ttu-id="dd2dd-191">On the main Azure menu, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-191">On the main Azure menu, select **All services**.</span></span> <span data-ttu-id="dd2dd-192">In the search box, enter "integration accounts" as your filter, and select **Integration accounts**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-192">In the search box, enter "integration accounts" as your filter, and select **Integration accounts**.</span></span>

   ![Find your integration account](./media/logic-apps-enterprise-integration-create-integration-account/create-integration-account.png)

2. <span data-ttu-id="dd2dd-194">Under **Integration accounts**, select the integration account that you want to move.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-194">Under **Integration accounts**, select the integration account that you want to move.</span></span> <span data-ttu-id="dd2dd-195">On your integration account menu, under **Settings**, choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-195">On your integration account menu, under **Settings**, choose **Properties**.</span></span>

   ![Under "Settings", choose "Properties"](./media/logic-apps-enterprise-integration-create-integration-account/integration-account-properties.png)

3. <span data-ttu-id="dd2dd-197">Change either the Azure resource group or subscription for your integration account.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-197">Change either the Azure resource group or subscription for your integration account.</span></span>

   ![Choose "Change resource group" or "Change subscription"](./media/logic-apps-enterprise-integration-create-integration-account/change-resource-group-subscription.png)

4. <span data-ttu-id="dd2dd-199">When you're done, make sure that you update any and all scripts with the new resource IDs for your artifacts.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-199">When you're done, make sure that you update any and all scripts with the new resource IDs for your artifacts.</span></span>  

## <a name="delete-integration-account"></a><span data-ttu-id="dd2dd-200">Delete integration account</span><span class="sxs-lookup"><span data-stu-id="dd2dd-200">Delete integration account</span></span>

1. <span data-ttu-id="dd2dd-201">On the main Azure menu, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-201">On the main Azure menu, select **All services**.</span></span> <span data-ttu-id="dd2dd-202">In the search box, enter "integration accounts" as your filter, and select **Integration accounts**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-202">In the search box, enter "integration accounts" as your filter, and select **Integration accounts**.</span></span>

   ![Find your integration account](./media/logic-apps-enterprise-integration-create-integration-account/create-integration-account.png)

2. <span data-ttu-id="dd2dd-204">Under **Integration accounts**, select the integration account that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-204">Under **Integration accounts**, select the integration account that you want to delete.</span></span> <span data-ttu-id="dd2dd-205">On the integration account menu, choose **Overview**, then choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-205">On the integration account menu, choose **Overview**, then choose **Delete**.</span></span> 

   ![Select integration account.](./media/logic-apps-enterprise-integration-create-integration-account/delete-integration-account.png)

3. <span data-ttu-id="dd2dd-208">To confirm that you want to delete your integration account, choose **Yes**.</span><span class="sxs-lookup"><span data-stu-id="dd2dd-208">To confirm that you want to delete your integration account, choose **Yes**.</span></span>

   ![To confirm delete, choose "Yes"](./media/logic-apps-enterprise-integration-create-integration-account/confirm-delete.png)

## <a name="next-steps"></a><span data-ttu-id="dd2dd-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd2dd-210">Next steps</span></span>

* [<span data-ttu-id="dd2dd-211">Create trading partners</span><span class="sxs-lookup"><span data-stu-id="dd2dd-211">Create trading partners</span></span>](../logic-apps/logic-apps-enterprise-integration-partners.md)
* [<span data-ttu-id="dd2dd-212">Create agreements</span><span class="sxs-lookup"><span data-stu-id="dd2dd-212">Create agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md)
