---
title: Create workflows from templates - Azure Logic Apps | Microsoft Docs
description: Build workflows faster by using logic app templates in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: kevinlam1
ms.author: klam
ms.reviewer: estfan, LADocs
ms.topic: article
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.date: 10/15/2017
ms.openlocfilehash: 10191a4fbab325dcd5134b082f050188c6798079
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865893"
---
# <a name="create-logic-app-workflows-from-prebuilt-templates"></a><span data-ttu-id="56d02-103">Create logic app workflows from prebuilt templates</span><span class="sxs-lookup"><span data-stu-id="56d02-103">Create logic app workflows from prebuilt templates</span></span>

<span data-ttu-id="56d02-104">To get you started creating workflows more quickly, Logic Apps provides templates, which are prebuilt logic apps that follow commonly used patterns.</span><span class="sxs-lookup"><span data-stu-id="56d02-104">To get you started creating workflows more quickly, Logic Apps provides templates, which are prebuilt logic apps that follow commonly used patterns.</span></span> <span data-ttu-id="56d02-105">Use these templates as provided or edit them to fit your scenario.</span><span class="sxs-lookup"><span data-stu-id="56d02-105">Use these templates as provided or edit them to fit your scenario.</span></span>

<span data-ttu-id="56d02-106">Here are some template categories:</span><span class="sxs-lookup"><span data-stu-id="56d02-106">Here are some template categories:</span></span>

| <span data-ttu-id="56d02-107">Template type</span><span class="sxs-lookup"><span data-stu-id="56d02-107">Template type</span></span> | <span data-ttu-id="56d02-108">Description</span><span class="sxs-lookup"><span data-stu-id="56d02-108">Description</span></span> | 
| ------------- | ----------- | 
| <span data-ttu-id="56d02-109">Enterprise cloud templates</span><span class="sxs-lookup"><span data-stu-id="56d02-109">Enterprise cloud templates</span></span> | <span data-ttu-id="56d02-110">For integrating Azure Blob, Dynamics CRM, Salesforce, Box, and includes other connectors for your enterprise cloud needs.</span><span class="sxs-lookup"><span data-stu-id="56d02-110">For integrating Azure Blob, Dynamics CRM, Salesforce, Box, and includes other connectors for your enterprise cloud needs.</span></span> <span data-ttu-id="56d02-111">For example, you can use these templates to organize business leads or back up your corporate file data.</span><span class="sxs-lookup"><span data-stu-id="56d02-111">For example, you can use these templates to organize business leads or back up your corporate file data.</span></span> | 
| <span data-ttu-id="56d02-112">Personal productivity templates</span><span class="sxs-lookup"><span data-stu-id="56d02-112">Personal productivity templates</span></span> | <span data-ttu-id="56d02-113">Improve personal productivity by setting daily reminders, turning important work items into to-do lists, and automating lengthy tasks down to a single user approval step.</span><span class="sxs-lookup"><span data-stu-id="56d02-113">Improve personal productivity by setting daily reminders, turning important work items into to-do lists, and automating lengthy tasks down to a single user approval step.</span></span> | 
| <span data-ttu-id="56d02-114">Consumer cloud templates</span><span class="sxs-lookup"><span data-stu-id="56d02-114">Consumer cloud templates</span></span> | <span data-ttu-id="56d02-115">For integrating social media services such as Twitter, Slack, and email.</span><span class="sxs-lookup"><span data-stu-id="56d02-115">For integrating social media services such as Twitter, Slack, and email.</span></span> <span data-ttu-id="56d02-116">Useful for strengthening social media marketing initiatives.</span><span class="sxs-lookup"><span data-stu-id="56d02-116">Useful for strengthening social media marketing initiatives.</span></span> <span data-ttu-id="56d02-117">These templates also include tasks such as cloud copying, which increases productivity by saving time on traditionally repetitive tasks.</span><span class="sxs-lookup"><span data-stu-id="56d02-117">These templates also include tasks such as cloud copying, which increases productivity by saving time on traditionally repetitive tasks.</span></span> | 
| <span data-ttu-id="56d02-118">Enterprise integration pack templates</span><span class="sxs-lookup"><span data-stu-id="56d02-118">Enterprise integration pack templates</span></span> | <span data-ttu-id="56d02-119">For configuring VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming to XML, and handling X12, EDIFACT, and AS2 messages.</span><span class="sxs-lookup"><span data-stu-id="56d02-119">For configuring VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming to XML, and handling X12, EDIFACT, and AS2 messages.</span></span> | 
| <span data-ttu-id="56d02-120">Protocol pattern templates</span><span class="sxs-lookup"><span data-stu-id="56d02-120">Protocol pattern templates</span></span> | <span data-ttu-id="56d02-121">For implementing protocol patterns such as request-response over HTTP and integrations across FTP and SFTP.</span><span class="sxs-lookup"><span data-stu-id="56d02-121">For implementing protocol patterns such as request-response over HTTP and integrations across FTP and SFTP.</span></span> <span data-ttu-id="56d02-122">Use these templates as provided, or build on them for complex protocol patterns.</span><span class="sxs-lookup"><span data-stu-id="56d02-122">Use these templates as provided, or build on them for complex protocol patterns.</span></span> | 
||| 

<span data-ttu-id="56d02-123">If you don't have an Azure subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="56d02-123">If you don't have an Azure subscription, [sign up for a free Azure account](https://azure.microsoft.com/free/) before you begin.</span></span> <span data-ttu-id="56d02-124">For more information about building a logic app, see [Create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="56d02-124">For more information about building a logic app, see [Create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

## <a name="create-logic-apps-from-templates"></a><span data-ttu-id="56d02-125">Create logic apps from templates</span><span class="sxs-lookup"><span data-stu-id="56d02-125">Create logic apps from templates</span></span>

1. <span data-ttu-id="56d02-126">If you haven't already, sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="56d02-126">If you haven't already, sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="56d02-127">From the main Azure menu, choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="56d02-127">From the main Azure menu, choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span></span>

   ![Azure portal, New, Enterprise Integration, Logic App](./media/logic-apps-create-logic-apps-from-templates/azure-portal-create-logic-app.png)

3. <span data-ttu-id="56d02-129">Create your logic app with the settings in the table under this image:</span><span class="sxs-lookup"><span data-stu-id="56d02-129">Create your logic app with the settings in the table under this image:</span></span>

   ![Provide logic app details](./media/logic-apps-create-logic-apps-from-templates/logic-app-settings.png)

   | <span data-ttu-id="56d02-131">Setting</span><span class="sxs-lookup"><span data-stu-id="56d02-131">Setting</span></span> | <span data-ttu-id="56d02-132">Value</span><span class="sxs-lookup"><span data-stu-id="56d02-132">Value</span></span> | <span data-ttu-id="56d02-133">Description</span><span class="sxs-lookup"><span data-stu-id="56d02-133">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="56d02-134">**Name**</span><span class="sxs-lookup"><span data-stu-id="56d02-134">**Name**</span></span> | <span data-ttu-id="56d02-135">*your-logic-app-name*</span><span class="sxs-lookup"><span data-stu-id="56d02-135">*your-logic-app-name*</span></span> | <span data-ttu-id="56d02-136">Provide a unique logic app name.</span><span class="sxs-lookup"><span data-stu-id="56d02-136">Provide a unique logic app name.</span></span> | 
   | <span data-ttu-id="56d02-137">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="56d02-137">**Subscription**</span></span> | <span data-ttu-id="56d02-138">*your-Azure-subscription-name*</span><span class="sxs-lookup"><span data-stu-id="56d02-138">*your-Azure-subscription-name*</span></span> | <span data-ttu-id="56d02-139">Select the Azure subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="56d02-139">Select the Azure subscription that you want to use.</span></span> | 
   | <span data-ttu-id="56d02-140">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="56d02-140">**Resource group**</span></span> | <span data-ttu-id="56d02-141">*your-Azure-resource-group-name*</span><span class="sxs-lookup"><span data-stu-id="56d02-141">*your-Azure-resource-group-name*</span></span> | <span data-ttu-id="56d02-142">Create or select an [Azure resource group](../azure-resource-manager/resource-group-overview.md) for this logic app and to organize all resources associated with this app.</span><span class="sxs-lookup"><span data-stu-id="56d02-142">Create or select an [Azure resource group](../azure-resource-manager/resource-group-overview.md) for this logic app and to organize all resources associated with this app.</span></span> | 
   | <span data-ttu-id="56d02-143">**Location**</span><span class="sxs-lookup"><span data-stu-id="56d02-143">**Location**</span></span> | <span data-ttu-id="56d02-144">*your-Azure-datacenter-region*</span><span class="sxs-lookup"><span data-stu-id="56d02-144">*your-Azure-datacenter-region*</span></span> | <span data-ttu-id="56d02-145">Select the datacenter region for deploying your logic app, for example, West US.</span><span class="sxs-lookup"><span data-stu-id="56d02-145">Select the datacenter region for deploying your logic app, for example, West US.</span></span> | 
   | <span data-ttu-id="56d02-146">**Log Analytics**</span><span class="sxs-lookup"><span data-stu-id="56d02-146">**Log Analytics**</span></span> | <span data-ttu-id="56d02-147">**Off** (default) or **On**</span><span class="sxs-lookup"><span data-stu-id="56d02-147">**Off** (default) or **On**</span></span> | <span data-ttu-id="56d02-148">Turn on [diagnostic logging](../logic-apps/logic-apps-monitor-your-logic-apps.md#turn-on-diagnostics-logging-for-your-logic-app) for your logic app through [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="56d02-148">Turn on [diagnostic logging](../logic-apps/logic-apps-monitor-your-logic-apps.md#turn-on-diagnostics-logging-for-your-logic-app) for your logic app through [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="56d02-149">Requires that you already have a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="56d02-149">Requires that you already have a Log Analytics workspace.</span></span> | 
   |||| 

4. <span data-ttu-id="56d02-150">When you're ready, select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="56d02-150">When you're ready, select **Pin to dashboard**.</span></span> <span data-ttu-id="56d02-151">That way, your logic app automatically appears on your Azure dashboard and opens after deployment.</span><span class="sxs-lookup"><span data-stu-id="56d02-151">That way, your logic app automatically appears on your Azure dashboard and opens after deployment.</span></span> <span data-ttu-id="56d02-152">Choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="56d02-152">Choose **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="56d02-153">If you don't want to pin your logic app, you must manually find and open your logic app after deployment so you can continue.</span><span class="sxs-lookup"><span data-stu-id="56d02-153">If you don't want to pin your logic app, you must manually find and open your logic app after deployment so you can continue.</span></span>

   <span data-ttu-id="56d02-154">After Azure deploys your logic app, the Logic Apps Designer opens and shows a page with an introduction video.</span><span class="sxs-lookup"><span data-stu-id="56d02-154">After Azure deploys your logic app, the Logic Apps Designer opens and shows a page with an introduction video.</span></span> 
   <span data-ttu-id="56d02-155">Under the video, you can find templates for common logic app patterns.</span><span class="sxs-lookup"><span data-stu-id="56d02-155">Under the video, you can find templates for common logic app patterns.</span></span> 

5. <span data-ttu-id="56d02-156">Scroll past the introduction video and common triggers to **Templates**.</span><span class="sxs-lookup"><span data-stu-id="56d02-156">Scroll past the introduction video and common triggers to **Templates**.</span></span> <span data-ttu-id="56d02-157">Choose a prebuilt template.</span><span class="sxs-lookup"><span data-stu-id="56d02-157">Choose a prebuilt template.</span></span> <span data-ttu-id="56d02-158">For example:</span><span class="sxs-lookup"><span data-stu-id="56d02-158">For example:</span></span>

   ![Choose a logic app template](./media/logic-apps-create-logic-apps-from-templates/choose-logic-app-template.png)

   > [!TIP]
   > <span data-ttu-id="56d02-160">To create your logic app from scratch, choose **Blank Logic App**.</span><span class="sxs-lookup"><span data-stu-id="56d02-160">To create your logic app from scratch, choose **Blank Logic App**.</span></span>

   <span data-ttu-id="56d02-161">When you select a prebuilt template, you can view more information about that template.</span><span class="sxs-lookup"><span data-stu-id="56d02-161">When you select a prebuilt template, you can view more information about that template.</span></span> 
   <span data-ttu-id="56d02-162">For example:</span><span class="sxs-lookup"><span data-stu-id="56d02-162">For example:</span></span>

   ![Choose a prebuilt template](./media/logic-apps-create-logic-apps-from-templates/logic-app-choose-prebuilt-template.png)

6. <span data-ttu-id="56d02-164">To continue with the selected template, choose **Use this template**.</span><span class="sxs-lookup"><span data-stu-id="56d02-164">To continue with the selected template, choose **Use this template**.</span></span> 

7. <span data-ttu-id="56d02-165">Based on the connectors in the template, you are prompted to perform any of these steps:</span><span class="sxs-lookup"><span data-stu-id="56d02-165">Based on the connectors in the template, you are prompted to perform any of these steps:</span></span>

   * <span data-ttu-id="56d02-166">Sign in with your credentials to systems or services that are referenced by the template.</span><span class="sxs-lookup"><span data-stu-id="56d02-166">Sign in with your credentials to systems or services that are referenced by the template.</span></span>

   * <span data-ttu-id="56d02-167">Create connections for any services or systems referenced by the template.</span><span class="sxs-lookup"><span data-stu-id="56d02-167">Create connections for any services or systems referenced by the template.</span></span> <span data-ttu-id="56d02-168">To create a connection, provide a name for your connection, and if necessary, select the resource that you want to use.</span><span class="sxs-lookup"><span data-stu-id="56d02-168">To create a connection, provide a name for your connection, and if necessary, select the resource that you want to use.</span></span> 

   * <span data-ttu-id="56d02-169">If you already set up these connections, choose **Continue**.</span><span class="sxs-lookup"><span data-stu-id="56d02-169">If you already set up these connections, choose **Continue**.</span></span>

   <span data-ttu-id="56d02-170">For example:</span><span class="sxs-lookup"><span data-stu-id="56d02-170">For example:</span></span>

   ![Create connections](./media/logic-apps-create-logic-apps-from-templates/logic-app-create-connection.png)

   <span data-ttu-id="56d02-172">When you're done, your logic app opens and appears in the Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="56d02-172">When you're done, your logic app opens and appears in the Logic Apps Designer.</span></span>

   > [!TIP]
   > <span data-ttu-id="56d02-173">To return to the template viewer, choose **Templates** on the designer toolbar.</span><span class="sxs-lookup"><span data-stu-id="56d02-173">To return to the template viewer, choose **Templates** on the designer toolbar.</span></span> <span data-ttu-id="56d02-174">This action discards any unsaved changes, so a warning message appears to confirm your request.</span><span class="sxs-lookup"><span data-stu-id="56d02-174">This action discards any unsaved changes, so a warning message appears to confirm your request.</span></span>

8. <span data-ttu-id="56d02-175">Continue building your logic app.</span><span class="sxs-lookup"><span data-stu-id="56d02-175">Continue building your logic app.</span></span>

   > [!NOTE] 
   > <span data-ttu-id="56d02-176">Many templates include connectors that might already have prepopulated required properties.</span><span class="sxs-lookup"><span data-stu-id="56d02-176">Many templates include connectors that might already have prepopulated required properties.</span></span> <span data-ttu-id="56d02-177">However, some templates might still require that you provide values before you can properly deploy the logic app.</span><span class="sxs-lookup"><span data-stu-id="56d02-177">However, some templates might still require that you provide values before you can properly deploy the logic app.</span></span> <span data-ttu-id="56d02-178">If you try to deploy without completing the missing property fields, you get an error message.</span><span class="sxs-lookup"><span data-stu-id="56d02-178">If you try to deploy without completing the missing property fields, you get an error message.</span></span> 

## <a name="update-logic-apps-with-templates"></a><span data-ttu-id="56d02-179">Update logic apps with templates</span><span class="sxs-lookup"><span data-stu-id="56d02-179">Update logic apps with templates</span></span>

1. <span data-ttu-id="56d02-180">In the [Azure portal](https://portal.azure.com "Azure portal"), find and open your logic app in th Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="56d02-180">In the [Azure portal](https://portal.azure.com "Azure portal"), find and open your logic app in th Logic App Designer.</span></span>

2. <span data-ttu-id="56d02-181">On the designer toolbar, choose **Templates**.</span><span class="sxs-lookup"><span data-stu-id="56d02-181">On the designer toolbar, choose **Templates**.</span></span> <span data-ttu-id="56d02-182">This action discards any unsaved changes, so a warning message appears so you can confirm that you want to continue.</span><span class="sxs-lookup"><span data-stu-id="56d02-182">This action discards any unsaved changes, so a warning message appears so you can confirm that you want to continue.</span></span> <span data-ttu-id="56d02-183">To confirm, choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="56d02-183">To confirm, choose **OK**.</span></span> <span data-ttu-id="56d02-184">For example:</span><span class="sxs-lookup"><span data-stu-id="56d02-184">For example:</span></span>

   ![Choose "Templates"](./media/logic-apps-create-logic-apps-from-templates/logic-app-update-existing-with-template.png)

3. <span data-ttu-id="56d02-186">Scroll past the introduction video and common triggers to **Templates**.</span><span class="sxs-lookup"><span data-stu-id="56d02-186">Scroll past the introduction video and common triggers to **Templates**.</span></span> <span data-ttu-id="56d02-187">Choose a prebuilt template.</span><span class="sxs-lookup"><span data-stu-id="56d02-187">Choose a prebuilt template.</span></span> <span data-ttu-id="56d02-188">For example:</span><span class="sxs-lookup"><span data-stu-id="56d02-188">For example:</span></span>

   ![Choose a logic app template](./media/logic-apps-create-logic-apps-from-templates/choose-logic-app-template.png)

   <span data-ttu-id="56d02-190">When you select a prebuilt template, you can view more information about that template.</span><span class="sxs-lookup"><span data-stu-id="56d02-190">When you select a prebuilt template, you can view more information about that template.</span></span> 
   <span data-ttu-id="56d02-191">For example:</span><span class="sxs-lookup"><span data-stu-id="56d02-191">For example:</span></span>

   ![Choose a prebuilt template](./media/logic-apps-create-logic-apps-from-templates/logic-app-choose-prebuilt-template.png)

4. <span data-ttu-id="56d02-193">To continue with the selected template, choose **Use this template**.</span><span class="sxs-lookup"><span data-stu-id="56d02-193">To continue with the selected template, choose **Use this template**.</span></span> 

5. <span data-ttu-id="56d02-194">Based on the connectors in the template, you are prompted to perform any of these steps:</span><span class="sxs-lookup"><span data-stu-id="56d02-194">Based on the connectors in the template, you are prompted to perform any of these steps:</span></span>

   * <span data-ttu-id="56d02-195">Sign in with your credentials to systems or services that are referenced by the template.</span><span class="sxs-lookup"><span data-stu-id="56d02-195">Sign in with your credentials to systems or services that are referenced by the template.</span></span>

   * <span data-ttu-id="56d02-196">Create connections for any services or systems referenced by the template.</span><span class="sxs-lookup"><span data-stu-id="56d02-196">Create connections for any services or systems referenced by the template.</span></span> <span data-ttu-id="56d02-197">To create a connection, provide a name for your connection, and if necessary, select the resource that you want to use.</span><span class="sxs-lookup"><span data-stu-id="56d02-197">To create a connection, provide a name for your connection, and if necessary, select the resource that you want to use.</span></span> 

   * <span data-ttu-id="56d02-198">If you already set up these connections, choose **Continue**.</span><span class="sxs-lookup"><span data-stu-id="56d02-198">If you already set up these connections, choose **Continue**.</span></span>

   ![Create connections](./media/logic-apps-create-logic-apps-from-templates/logic-app-create-connection.png)

   <span data-ttu-id="56d02-200">Your logic app now opens and appears in the Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="56d02-200">Your logic app now opens and appears in the Logic Apps Designer.</span></span>

8. <span data-ttu-id="56d02-201">Continue building your logic app.</span><span class="sxs-lookup"><span data-stu-id="56d02-201">Continue building your logic app.</span></span> 

   > [!TIP]
   > <span data-ttu-id="56d02-202">If you haven't saved your changes, you can discard your work and return to your previous logic app.</span><span class="sxs-lookup"><span data-stu-id="56d02-202">If you haven't saved your changes, you can discard your work and return to your previous logic app.</span></span> <span data-ttu-id="56d02-203">On the designer toolbar, choose **Discard**.</span><span class="sxs-lookup"><span data-stu-id="56d02-203">On the designer toolbar, choose **Discard**.</span></span>

> [!NOTE] 
> <span data-ttu-id="56d02-204">Many templates include connectors that might have already pre-populated required properties.</span><span class="sxs-lookup"><span data-stu-id="56d02-204">Many templates include connectors that might have already pre-populated required properties.</span></span> <span data-ttu-id="56d02-205">However, some templates might still require that you provide values before you can properly deploy the logic app.</span><span class="sxs-lookup"><span data-stu-id="56d02-205">However, some templates might still require that you provide values before you can properly deploy the logic app.</span></span> <span data-ttu-id="56d02-206">If you try to deploy without completing the missing property fields, you get an error message.</span><span class="sxs-lookup"><span data-stu-id="56d02-206">If you try to deploy without completing the missing property fields, you get an error message.</span></span>

## <a name="deploy-logic-apps-built-from-templates"></a><span data-ttu-id="56d02-207">Deploy logic apps built from templates</span><span class="sxs-lookup"><span data-stu-id="56d02-207">Deploy logic apps built from templates</span></span>

<span data-ttu-id="56d02-208">After you make your changes to the template, you can save your changes.</span><span class="sxs-lookup"><span data-stu-id="56d02-208">After you make your changes to the template, you can save your changes.</span></span> <span data-ttu-id="56d02-209">This action also automatically publishes your logic app.</span><span class="sxs-lookup"><span data-stu-id="56d02-209">This action also automatically publishes your logic app.</span></span>

<span data-ttu-id="56d02-210">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="56d02-210">On the designer toolbar, choose **Save**.</span></span>

![Save and publish your logic app](./media/logic-apps-create-logic-apps-from-templates/logic-app-save.png)  

## <a name="get-support"></a><span data-ttu-id="56d02-212">Get support</span><span class="sxs-lookup"><span data-stu-id="56d02-212">Get support</span></span>

* <span data-ttu-id="56d02-213">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="56d02-213">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="56d02-214">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="56d02-214">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="56d02-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="56d02-215">Next steps</span></span>

<span data-ttu-id="56d02-216">Learn about building logic apps through examples, scenarios, customer stories, and walkthroughs.</span><span class="sxs-lookup"><span data-stu-id="56d02-216">Learn about building logic apps through examples, scenarios, customer stories, and walkthroughs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="56d02-217">Review logic app examples, scenarios, and walkthroughs</span><span class="sxs-lookup"><span data-stu-id="56d02-217">Review logic app examples, scenarios, and walkthroughs</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)