---
title: Connect to Dynamics 365 (online) from Azure Logic Apps | Microsoft Docs
description: Create logic app workflows that manage Dynamics 365 (online) entities through the API provided by the Dynamics 365 connector
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: ''
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 1f16ab66f24840963927fc285330423f65a0c5c2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564608"
---
# <a name="connect-to-dynamics-365-from-logic-app-workflows"></a><span data-ttu-id="a3e1d-103">Connect to Dynamics 365 from logic app workflows</span><span class="sxs-lookup"><span data-stu-id="a3e1d-103">Connect to Dynamics 365 from logic app workflows</span></span>

<span data-ttu-id="a3e1d-104">With Logic Apps, you can connect to Dynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-104">With Logic Apps, you can connect to Dynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="a3e1d-105">With the Dynamics 365 connector, you can:</span><span class="sxs-lookup"><span data-stu-id="a3e1d-105">With the Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="a3e1d-106">Build your business flow based on the data you get from Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="a3e1d-106">Build your business flow based on the data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="a3e1d-107">Use actions that get a response and then make the output available for other actions.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-107">Use actions that get a response and then make the output available for other actions.</span></span> <span data-ttu-id="a3e1d-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="a3e1d-109">This topic shows you how to create a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-109">This topic shows you how to create a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3e1d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a3e1d-110">Prerequisites</span></span>
* <span data-ttu-id="a3e1d-111">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-111">An Azure account.</span></span>
* <span data-ttu-id="a3e1d-112">A Dynamics 365 (online) account.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="a3e1d-113">Create a task when a new lead is created in Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="a3e1d-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="a3e1d-114">[Sign in to Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3e1d-114">[Sign in to Azure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="a3e1d-115">In the Azure search box, type `Logic apps`, and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-115">In the Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Find Logic Apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="a3e1d-117">Under **Logic apps**, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-117">Under **Logic apps**, click **Add**.</span></span>

      ![LogicApp add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="a3e1d-119">To create the logic app, complete the **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-119">To create the logic app, complete the **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="a3e1d-120">Select the new logic app.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-120">Select the new logic app.</span></span> <span data-ttu-id="a3e1d-121">When you receive the **Deployment Succeeded** notification, click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-121">When you receive the **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="a3e1d-122">Under **Development Tools**, click **Logic App Designer**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="a3e1d-123">In the template list, click **Blank Logic App**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-123">In the template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="a3e1d-124">In the search box, type `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-124">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="a3e1d-125">From the Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-125">From the Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="a3e1d-126">If you are prompted to sign in to Dynamics 365, do so now.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-126">If you are prompted to sign in to Dynamics 365, do so now.</span></span>

9.  <span data-ttu-id="a3e1d-127">In the trigger details, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="a3e1d-127">In the trigger details, enter the following information:</span></span>

  * <span data-ttu-id="a3e1d-128">**Organization Name**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-128">**Organization Name**.</span></span> <span data-ttu-id="a3e1d-129">Select the Dynamics 365 instance that you want the logic app to listen to.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-129">Select the Dynamics 365 instance that you want the logic app to listen to.</span></span>

  * <span data-ttu-id="a3e1d-130">**Entity Name**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-130">**Entity Name**.</span></span> <span data-ttu-id="a3e1d-131">Select the entity that you want to listen to.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-131">Select the entity that you want to listen to.</span></span> <span data-ttu-id="a3e1d-132">This event acts as a trigger to start the logic app.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-132">This event acts as a trigger to start the logic app.</span></span> 
  <span data-ttu-id="a3e1d-133">In this walkthrough, **Leads** is selected.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="a3e1d-134">**How often do you want to check for items?**</span><span class="sxs-lookup"><span data-stu-id="a3e1d-134">**How often do you want to check for items?**</span></span> <span data-ttu-id="a3e1d-135">These values set how often the logic app checks for updates related to the trigger.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-135">These values set how often the logic app checks for updates related to the trigger.</span></span> <span data-ttu-id="a3e1d-136">The default setting is to check for updates every three minutes.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-136">The default setting is to check for updates every three minutes.</span></span>

    * <span data-ttu-id="a3e1d-137">**Frequency**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-137">**Frequency**.</span></span> <span data-ttu-id="a3e1d-138">Select seconds, minutes, hours, or days.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="a3e1d-139">**Interval**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-139">**Interval**.</span></span> <span data-ttu-id="a3e1d-140">Enter the number of seconds, minutes, hours, or days that you want to pass before the next check.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-140">Enter the number of seconds, minutes, hours, or days that you want to pass before the next check.</span></span>

      ![Logic App Trigger details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="a3e1d-142">Click **New step**, and then click **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="a3e1d-143">In the search box, type `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-143">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="a3e1d-144">From the actions list, select **Dynamics 365 – Create a new record**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-144">From the actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="a3e1d-145">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="a3e1d-145">Enter the following information:</span></span>

    * <span data-ttu-id="a3e1d-146">**Organization Name**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-146">**Organization Name**.</span></span> <span data-ttu-id="a3e1d-147">Select the Dynamics 365 instance where you want the flow to create the record.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-147">Select the Dynamics 365 instance where you want the flow to create the record.</span></span> 
    <span data-ttu-id="a3e1d-148">Notice that this instance doesn’t have to be the same instance where the event is triggered from.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-148">Notice that this instance doesn’t have to be the same instance where the event is triggered from.</span></span>

    * <span data-ttu-id="a3e1d-149">**Entity Name**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-149">**Entity Name**.</span></span> <span data-ttu-id="a3e1d-150">Select the entity that you want to create a record when the event is triggered.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-150">Select the entity that you want to create a record when the event is triggered.</span></span> 
    <span data-ttu-id="a3e1d-151">In this walkthrough, **Tasks** is selected.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="a3e1d-152">Click in the **Subject** box that appears.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-152">Click in the **Subject** box that appears.</span></span> <span data-ttu-id="a3e1d-153">From the dynamic content list that appears, you can select either of these fields:</span><span class="sxs-lookup"><span data-stu-id="a3e1d-153">From the dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="a3e1d-154">**Last Name**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-154">**Last Name**.</span></span> <span data-ttu-id="a3e1d-155">Selecting this field inserts the last name for the lead into the Subject field for the task, when the task record is created.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-155">Selecting this field inserts the last name for the lead into the Subject field for the task, when the task record is created.</span></span>
    * <span data-ttu-id="a3e1d-156">**Topic**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-156">**Topic**.</span></span> <span data-ttu-id="a3e1d-157">Selecting this field inserts the Topic field for the lead into the Subject field for the task, when the task record is created.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-157">Selecting this field inserts the Topic field for the lead into the Subject field for the task, when the task record is created.</span></span> 
    <span data-ttu-id="a3e1d-158">Click **Topic** to add that to the **Subject** box.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-158">Click **Topic** to add that to the **Subject** box.</span></span>

      ![Logic App Create new record details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="a3e1d-160">On the Logic App Designer toolbar, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-160">On the Logic App Designer toolbar, click **Save**.</span></span>

    ![Logic App Designer toolbar Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="a3e1d-162">To start the Logic App, click **Run**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-162">To start the Logic App, click **Run**.</span></span>

    ![Logic App Designer toolbar Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="a3e1d-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span><span class="sxs-lookup"><span data-stu-id="a3e1d-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="a3e1d-165">Set advanced options for a logic app step</span><span class="sxs-lookup"><span data-stu-id="a3e1d-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="a3e1d-166">To specify how to filter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-166">To specify how to filter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="a3e1d-167">For example, you can use a filter query to get only active accounts and order by the account name.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-167">For example, you can use a filter query to get only active accounts and order by the account name.</span></span> <span data-ttu-id="a3e1d-168">To perform this task, enter the OData filter query `statuscode eq 1`, and select **Account Name** from the dynamic content list.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-168">To perform this task, enter the OData filter query `statuscode eq 1`, and select **Account Name** from the dynamic content list.</span></span> <span data-ttu-id="a3e1d-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="a3e1d-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Logic app advanced options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="a3e1d-171">Best practices when using advanced options</span><span class="sxs-lookup"><span data-stu-id="a3e1d-171">Best practices when using advanced options</span></span>

<span data-ttu-id="a3e1d-172">When you add a value to a field, you must match the field type whether you type a value or select a value from the dynamic content list.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-172">When you add a value to a field, you must match the field type whether you type a value or select a value from the dynamic content list.</span></span>

<span data-ttu-id="a3e1d-173">Field type</span><span class="sxs-lookup"><span data-stu-id="a3e1d-173">Field type</span></span>  |<span data-ttu-id="a3e1d-174">How to use</span><span class="sxs-lookup"><span data-stu-id="a3e1d-174">How to use</span></span>  |<span data-ttu-id="a3e1d-175">Where to find</span><span class="sxs-lookup"><span data-stu-id="a3e1d-175">Where to find</span></span>  |<span data-ttu-id="a3e1d-176">Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-176">Name</span></span>  |<span data-ttu-id="a3e1d-177">Data type</span><span class="sxs-lookup"><span data-stu-id="a3e1d-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="a3e1d-178">Text fields</span><span class="sxs-lookup"><span data-stu-id="a3e1d-178">Text fields</span></span>|<span data-ttu-id="a3e1d-179">Text fields require a single line of text or dynamic content that is a text type field.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="a3e1d-180">Examples include the Category and Sub-Category fields.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-180">Examples include the Category and Sub-Category fields.</span></span>|<span data-ttu-id="a3e1d-181">Settings > Customizations > Customize the System > Entities > Task > Fields</span><span class="sxs-lookup"><span data-stu-id="a3e1d-181">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="a3e1d-182">category</span><span class="sxs-lookup"><span data-stu-id="a3e1d-182">category</span></span> |<span data-ttu-id="a3e1d-183">Single Line of Text</span><span class="sxs-lookup"><span data-stu-id="a3e1d-183">Single Line of Text</span></span>        
<span data-ttu-id="a3e1d-184">Integer fields</span><span class="sxs-lookup"><span data-stu-id="a3e1d-184">Integer fields</span></span> | <span data-ttu-id="a3e1d-185">Some fields require integer or dynamic content that is an integer type field.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="a3e1d-186">Examples include Percent Complete and Duration.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="a3e1d-187">Settings > Customizations > Customize the System > Entities > Task > Fields</span><span class="sxs-lookup"><span data-stu-id="a3e1d-187">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="a3e1d-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="a3e1d-188">percentcomplete</span></span> |<span data-ttu-id="a3e1d-189">Whole Number</span><span class="sxs-lookup"><span data-stu-id="a3e1d-189">Whole Number</span></span>         
<span data-ttu-id="a3e1d-190">Date fields</span><span class="sxs-lookup"><span data-stu-id="a3e1d-190">Date fields</span></span> | <span data-ttu-id="a3e1d-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="a3e1d-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="a3e1d-193">Settings > Customizations > Customize the System > Entities > Task > Fields</span><span class="sxs-lookup"><span data-stu-id="a3e1d-193">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="a3e1d-194">createdon</span><span class="sxs-lookup"><span data-stu-id="a3e1d-194">createdon</span></span> |<span data-ttu-id="a3e1d-195">Date and Time</span><span class="sxs-lookup"><span data-stu-id="a3e1d-195">Date and Time</span></span>
<span data-ttu-id="a3e1d-196">Fields that require both a record ID and lookup type</span><span class="sxs-lookup"><span data-stu-id="a3e1d-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="a3e1d-197">Some fields that reference another entity record require both the record ID and the lookup type.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-197">Some fields that reference another entity record require both the record ID and the lookup type.</span></span> |<span data-ttu-id="a3e1d-198">Settings > Customizations > Customize the System > Entities > Account > Fields</span><span class="sxs-lookup"><span data-stu-id="a3e1d-198">Settings > Customizations > Customize the System > Entities > Account > Fields</span></span>  | <span data-ttu-id="a3e1d-199">accountid</span><span class="sxs-lookup"><span data-stu-id="a3e1d-199">accountid</span></span>  | <span data-ttu-id="a3e1d-200">Primary Key</span><span class="sxs-lookup"><span data-stu-id="a3e1d-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="a3e1d-201">More examples of fields that require both a record ID and lookup type</span><span class="sxs-lookup"><span data-stu-id="a3e1d-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="a3e1d-202">Expanding on the previous table, here are more examples of fields that don't work with values selected from the dynamic content list.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-202">Expanding on the previous table, here are more examples of fields that don't work with values selected from the dynamic content list.</span></span> <span data-ttu-id="a3e1d-203">Instead, these fields require both a record ID and lookup type entered into the fields in PowerApps.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-203">Instead, these fields require both a record ID and lookup type entered into the fields in PowerApps.</span></span>  
* <span data-ttu-id="a3e1d-204">Owner and Owner Type.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-204">Owner and Owner Type.</span></span> <span data-ttu-id="a3e1d-205">The Owner field must be a valid user or team record ID.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-205">The Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="a3e1d-206">The Owner Type must be either **systemusers** or **teams**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-206">The Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="a3e1d-207">Customer and Customer Type.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-207">Customer and Customer Type.</span></span> <span data-ttu-id="a3e1d-208">The Customer field must be a valid account or contact record ID.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-208">The Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="a3e1d-209">The Owner Type must be either **accounts** or **contacts**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-209">The Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="a3e1d-210">Regarding and Regarding Type.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="a3e1d-211">The Regarding field must be a valid record ID, such as an account or contact record ID.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-211">The Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="a3e1d-212">The Regarding Type must be the lookup type for the record, such as **accounts** or **contacts**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-212">The Regarding Type must be the lookup type for the record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="a3e1d-213">The following task creation action example adds an account record that corresponds to the record ID adding it to the regarding field of the task.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-213">The following task creation action example adds an account record that corresponds to the record ID adding it to the regarding field of the task.</span></span>

![Flow recordId and type account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="a3e1d-215">This example also assigns the task to a specific user based on the user's record ID.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-215">This example also assigns the task to a specific user based on the user's record ID.</span></span>

![Flow recordId and type account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="a3e1d-217">To find a record's ID, see the following section: *Find the record ID*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-217">To find a record's ID, see the following section: *Find the record ID*</span></span>

## <a name="find-the-record-id"></a><span data-ttu-id="a3e1d-218">Find the record ID</span><span class="sxs-lookup"><span data-stu-id="a3e1d-218">Find the record ID</span></span>

1. <span data-ttu-id="a3e1d-219">Open a record, such as an account record.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="a3e1d-220">On the actions toolbar, click **Pop Out** ![popout record](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="a3e1d-220">On the actions toolbar, click **Pop Out** ![popout record](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="a3e1d-221">Alternatively, on the actions toolbar, to copy the full URL into your default email program, click **EMAIL A LINK**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-221">Alternatively, on the actions toolbar, to copy the full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="a3e1d-222">The record ID is displayed in between the %7b and %7d encoding characters of the URL.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-222">The record ID is displayed in between the %7b and %7d encoding characters of the URL.</span></span>

   ![Flow recordId and type account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="a3e1d-224">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="a3e1d-224">Troubleshooting</span></span>
<span data-ttu-id="a3e1d-225">To troubleshoot a failed step in a logic app, view the status details of the event.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-225">To troubleshoot a failed step in a logic app, view the status details of the event.</span></span>

1. <span data-ttu-id="a3e1d-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="a3e1d-227">The Summary area is shown and provides the run status for the logic app.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-227">The Summary area is shown and provides the run status for the logic app.</span></span> 

   ![Logic app run status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="a3e1d-229">To view more information about any failed runs, click the failed event.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-229">To view more information about any failed runs, click the failed event.</span></span> <span data-ttu-id="a3e1d-230">To expand a failed step, click that step.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-230">To expand a failed step, click that step.</span></span>

   ![Expand failed step](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="a3e1d-232">The step details appear and can help troubleshoot the cause of the failure.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-232">The step details appear and can help troubleshoot the cause of the failure.</span></span>

   ![Failed step details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="a3e1d-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="a3e1d-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="technical-details"></a><span data-ttu-id="a3e1d-235">Technical Details</span><span class="sxs-lookup"><span data-stu-id="a3e1d-235">Technical Details</span></span>
## <a name="triggers"></a><span data-ttu-id="a3e1d-236">Triggers</span><span class="sxs-lookup"><span data-stu-id="a3e1d-236">Triggers</span></span>
| <span data-ttu-id="a3e1d-237">Trigger</span><span class="sxs-lookup"><span data-stu-id="a3e1d-237">Trigger</span></span> | <span data-ttu-id="a3e1d-238">Description</span><span class="sxs-lookup"><span data-stu-id="a3e1d-238">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3e1d-239">When a record is created</span><span class="sxs-lookup"><span data-stu-id="a3e1d-239">When a record is created</span></span> |<span data-ttu-id="a3e1d-240">Triggers a flow when an object is created in Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-240">Triggers a flow when an object is created in Dynamics 365.</span></span> |
| <span data-ttu-id="a3e1d-241">When a record is updated</span><span class="sxs-lookup"><span data-stu-id="a3e1d-241">When a record is updated</span></span> |<span data-ttu-id="a3e1d-242">Triggers a flow when an object is modified in Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-242">Triggers a flow when an object is modified in Dynamics 365.</span></span> |
| <span data-ttu-id="a3e1d-243">When a record is deleted</span><span class="sxs-lookup"><span data-stu-id="a3e1d-243">When a record is deleted</span></span> |<span data-ttu-id="a3e1d-244">Triggers a flow when an object is deleted in Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-244">Triggers a flow when an object is deleted in Dynamics 365.</span></span> |

## <a name="actions"></a><span data-ttu-id="a3e1d-245">Actions</span><span class="sxs-lookup"><span data-stu-id="a3e1d-245">Actions</span></span>
| <span data-ttu-id="a3e1d-246">Action</span><span class="sxs-lookup"><span data-stu-id="a3e1d-246">Action</span></span> | <span data-ttu-id="a3e1d-247">Description</span><span class="sxs-lookup"><span data-stu-id="a3e1d-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3e1d-248">List records</span><span class="sxs-lookup"><span data-stu-id="a3e1d-248">List records</span></span> |<span data-ttu-id="a3e1d-249">This operation gets the records for an entity.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-249">This operation gets the records for an entity.</span></span> |
| <span data-ttu-id="a3e1d-250">Create a new record</span><span class="sxs-lookup"><span data-stu-id="a3e1d-250">Create a new record</span></span> |<span data-ttu-id="a3e1d-251">This operation creates a new record of an entity.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-251">This operation creates a new record of an entity.</span></span> |
| <span data-ttu-id="a3e1d-252">Get record</span><span class="sxs-lookup"><span data-stu-id="a3e1d-252">Get record</span></span> |<span data-ttu-id="a3e1d-253">This operation gets the specified record for an entity.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-253">This operation gets the specified record for an entity.</span></span> |
| <span data-ttu-id="a3e1d-254">Delete a record</span><span class="sxs-lookup"><span data-stu-id="a3e1d-254">Delete a record</span></span> |<span data-ttu-id="a3e1d-255">This operation deletes a record from an entity collection.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-255">This operation deletes a record from an entity collection.</span></span> |
| <span data-ttu-id="a3e1d-256">Update a record</span><span class="sxs-lookup"><span data-stu-id="a3e1d-256">Update a record</span></span> |<span data-ttu-id="a3e1d-257">This operation updates an existing record for an entity.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-257">This operation updates an existing record for an entity.</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="a3e1d-258">Trigger and Action details</span><span class="sxs-lookup"><span data-stu-id="a3e1d-258">Trigger and Action details</span></span>
<span data-ttu-id="a3e1d-259">In this section, see the specific details about each trigger and action, including any required or optional input properties, and any corresponding output associated with the connector.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-259">In this section, see the specific details about each trigger and action, including any required or optional input properties, and any corresponding output associated with the connector.</span></span>

#### <a name="when-a-record-is-created"></a><span data-ttu-id="a3e1d-260">When a record is created</span><span class="sxs-lookup"><span data-stu-id="a3e1d-260">When a record is created</span></span>
<span data-ttu-id="a3e1d-261">Triggers a flow when an object is created in Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-261">Triggers a flow when an object is created in Dynamics 365.</span></span>

| <span data-ttu-id="a3e1d-262">Property name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-262">Property name</span></span> | <span data-ttu-id="a3e1d-263">Display name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-263">Display name</span></span> | <span data-ttu-id="a3e1d-264">Description</span><span class="sxs-lookup"><span data-stu-id="a3e1d-264">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3e1d-265">dataset\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-265">dataset\*</span></span> |<span data-ttu-id="a3e1d-266">Organization Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-266">Organization Name</span></span> |<span data-ttu-id="a3e1d-267">Name of the Dynamics 365 organization like Contoso</span><span class="sxs-lookup"><span data-stu-id="a3e1d-267">Name of the Dynamics 365 organization like Contoso</span></span> |
| <span data-ttu-id="a3e1d-268">table\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-268">table\*</span></span> |<span data-ttu-id="a3e1d-269">Entity Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-269">Entity Name</span></span> |<span data-ttu-id="a3e1d-270">Name of the entity</span><span class="sxs-lookup"><span data-stu-id="a3e1d-270">Name of the entity</span></span> |
| <span data-ttu-id="a3e1d-271">$filter</span><span class="sxs-lookup"><span data-stu-id="a3e1d-271">$filter</span></span> |<span data-ttu-id="a3e1d-272">Filter Query</span><span class="sxs-lookup"><span data-stu-id="a3e1d-272">Filter Query</span></span> |<span data-ttu-id="a3e1d-273">An ODATA filter query to restrict the entries returned</span><span class="sxs-lookup"><span data-stu-id="a3e1d-273">An ODATA filter query to restrict the entries returned</span></span> |
| <span data-ttu-id="a3e1d-274">$orderby</span><span class="sxs-lookup"><span data-stu-id="a3e1d-274">$orderby</span></span> |<span data-ttu-id="a3e1d-275">Order By</span><span class="sxs-lookup"><span data-stu-id="a3e1d-275">Order By</span></span> |<span data-ttu-id="a3e1d-276">An ODATA orderBy query for specifying the order of entries</span><span class="sxs-lookup"><span data-stu-id="a3e1d-276">An ODATA orderBy query for specifying the order of entries</span></span> |

<span data-ttu-id="a3e1d-277">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-277">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="a3e1d-278">Output Details</span><span class="sxs-lookup"><span data-stu-id="a3e1d-278">Output Details</span></span>
<span data-ttu-id="a3e1d-279">ItemsList</span><span class="sxs-lookup"><span data-stu-id="a3e1d-279">ItemsList</span></span>

| <span data-ttu-id="a3e1d-280">Property Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-280">Property Name</span></span> | <span data-ttu-id="a3e1d-281">Data Type</span><span class="sxs-lookup"><span data-stu-id="a3e1d-281">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="a3e1d-282">value</span><span class="sxs-lookup"><span data-stu-id="a3e1d-282">value</span></span> |<span data-ttu-id="a3e1d-283">array</span><span class="sxs-lookup"><span data-stu-id="a3e1d-283">array</span></span> |

#### <a name="when-a-record-is-updated"></a><span data-ttu-id="a3e1d-284">When a record is updated</span><span class="sxs-lookup"><span data-stu-id="a3e1d-284">When a record is updated</span></span>
<span data-ttu-id="a3e1d-285">Triggers a flow when an object is modified in Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-285">Triggers a flow when an object is modified in Dynamics 365.</span></span>

| <span data-ttu-id="a3e1d-286">Property name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-286">Property name</span></span> | <span data-ttu-id="a3e1d-287">Display name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-287">Display name</span></span> | <span data-ttu-id="a3e1d-288">Description</span><span class="sxs-lookup"><span data-stu-id="a3e1d-288">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3e1d-289">dataset\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-289">dataset\*</span></span> |<span data-ttu-id="a3e1d-290">Organization Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-290">Organization Name</span></span> |<span data-ttu-id="a3e1d-291">Name of the Dynamics 365 organization like Contoso</span><span class="sxs-lookup"><span data-stu-id="a3e1d-291">Name of the Dynamics 365 organization like Contoso</span></span> |
| <span data-ttu-id="a3e1d-292">table\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-292">table\*</span></span> |<span data-ttu-id="a3e1d-293">Entity Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-293">Entity Name</span></span> |<span data-ttu-id="a3e1d-294">Name of the entity</span><span class="sxs-lookup"><span data-stu-id="a3e1d-294">Name of the entity</span></span> |

<span data-ttu-id="a3e1d-295">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-295">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="a3e1d-296">Output Details</span><span class="sxs-lookup"><span data-stu-id="a3e1d-296">Output Details</span></span>
<span data-ttu-id="a3e1d-297">ItemsList</span><span class="sxs-lookup"><span data-stu-id="a3e1d-297">ItemsList</span></span>

| <span data-ttu-id="a3e1d-298">Property Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-298">Property Name</span></span> | <span data-ttu-id="a3e1d-299">Data Type</span><span class="sxs-lookup"><span data-stu-id="a3e1d-299">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="a3e1d-300">value</span><span class="sxs-lookup"><span data-stu-id="a3e1d-300">value</span></span> |<span data-ttu-id="a3e1d-301">array</span><span class="sxs-lookup"><span data-stu-id="a3e1d-301">array</span></span> |

#### <a name="when-a-record-is-deleted"></a><span data-ttu-id="a3e1d-302">When a record is deleted</span><span class="sxs-lookup"><span data-stu-id="a3e1d-302">When a record is deleted</span></span>
<span data-ttu-id="a3e1d-303">Triggers a flow when an object is deleted in Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-303">Triggers a flow when an object is deleted in Dynamics 365.</span></span>

| <span data-ttu-id="a3e1d-304">Property name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-304">Property name</span></span> | <span data-ttu-id="a3e1d-305">Display name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-305">Display name</span></span> | <span data-ttu-id="a3e1d-306">Description</span><span class="sxs-lookup"><span data-stu-id="a3e1d-306">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3e1d-307">dataset\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-307">dataset\*</span></span> |<span data-ttu-id="a3e1d-308">Organization Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-308">Organization Name</span></span> |<span data-ttu-id="a3e1d-309">Name of the Dynamics 365 organization like Contoso</span><span class="sxs-lookup"><span data-stu-id="a3e1d-309">Name of the Dynamics 365 organization like Contoso</span></span> |
| <span data-ttu-id="a3e1d-310">table\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-310">table\*</span></span> |<span data-ttu-id="a3e1d-311">Entity Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-311">Entity Name</span></span> |<span data-ttu-id="a3e1d-312">Name of the entity</span><span class="sxs-lookup"><span data-stu-id="a3e1d-312">Name of the entity</span></span> |


<span data-ttu-id="a3e1d-313">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-313">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="a3e1d-314">Output Details</span><span class="sxs-lookup"><span data-stu-id="a3e1d-314">Output Details</span></span>
<span data-ttu-id="a3e1d-315">ItemsList</span><span class="sxs-lookup"><span data-stu-id="a3e1d-315">ItemsList</span></span>

| <span data-ttu-id="a3e1d-316">Property Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-316">Property Name</span></span> | <span data-ttu-id="a3e1d-317">Data Type</span><span class="sxs-lookup"><span data-stu-id="a3e1d-317">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="a3e1d-318">value</span><span class="sxs-lookup"><span data-stu-id="a3e1d-318">value</span></span> |<span data-ttu-id="a3e1d-319">array</span><span class="sxs-lookup"><span data-stu-id="a3e1d-319">array</span></span> |

#### <a name="list-records"></a><span data-ttu-id="a3e1d-320">List records</span><span class="sxs-lookup"><span data-stu-id="a3e1d-320">List records</span></span>
<span data-ttu-id="a3e1d-321">This operation gets the records for an entity.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-321">This operation gets the records for an entity.</span></span>

| <span data-ttu-id="a3e1d-322">Property name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-322">Property name</span></span> | <span data-ttu-id="a3e1d-323">Display name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-323">Display name</span></span> | <span data-ttu-id="a3e1d-324">Description</span><span class="sxs-lookup"><span data-stu-id="a3e1d-324">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3e1d-325">dataset\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-325">dataset\*</span></span> |<span data-ttu-id="a3e1d-326">Organization Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-326">Organization Name</span></span> |<span data-ttu-id="a3e1d-327">Name of the Dynamics 365 organization like Contoso</span><span class="sxs-lookup"><span data-stu-id="a3e1d-327">Name of the Dynamics 365 organization like Contoso</span></span> |
| <span data-ttu-id="a3e1d-328">table\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-328">table\*</span></span> |<span data-ttu-id="a3e1d-329">Entity Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-329">Entity Name</span></span> |<span data-ttu-id="a3e1d-330">Name of the entity</span><span class="sxs-lookup"><span data-stu-id="a3e1d-330">Name of the entity</span></span> |
| <span data-ttu-id="a3e1d-331">$filter</span><span class="sxs-lookup"><span data-stu-id="a3e1d-331">$filter</span></span> |<span data-ttu-id="a3e1d-332">Filter Query</span><span class="sxs-lookup"><span data-stu-id="a3e1d-332">Filter Query</span></span> |<span data-ttu-id="a3e1d-333">An ODATA filter query to restrict the entries returned</span><span class="sxs-lookup"><span data-stu-id="a3e1d-333">An ODATA filter query to restrict the entries returned</span></span> |
| <span data-ttu-id="a3e1d-334">$orderby</span><span class="sxs-lookup"><span data-stu-id="a3e1d-334">$orderby</span></span> |<span data-ttu-id="a3e1d-335">Order By</span><span class="sxs-lookup"><span data-stu-id="a3e1d-335">Order By</span></span> |<span data-ttu-id="a3e1d-336">An ODATA orderBy query for specifying the order of entries</span><span class="sxs-lookup"><span data-stu-id="a3e1d-336">An ODATA orderBy query for specifying the order of entries</span></span> |

<span data-ttu-id="a3e1d-337">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-337">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="a3e1d-338">Output Details</span><span class="sxs-lookup"><span data-stu-id="a3e1d-338">Output Details</span></span>
<span data-ttu-id="a3e1d-339">ItemsList</span><span class="sxs-lookup"><span data-stu-id="a3e1d-339">ItemsList</span></span>

| <span data-ttu-id="a3e1d-340">Property Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-340">Property Name</span></span> | <span data-ttu-id="a3e1d-341">Data Type</span><span class="sxs-lookup"><span data-stu-id="a3e1d-341">Data Type</span></span> |
| --- | --- |
| <span data-ttu-id="a3e1d-342">value</span><span class="sxs-lookup"><span data-stu-id="a3e1d-342">value</span></span> |<span data-ttu-id="a3e1d-343">array</span><span class="sxs-lookup"><span data-stu-id="a3e1d-343">array</span></span> |

#### <a name="create-a-new-record"></a><span data-ttu-id="a3e1d-344">Create a new record</span><span class="sxs-lookup"><span data-stu-id="a3e1d-344">Create a new record</span></span>
<span data-ttu-id="a3e1d-345">This operation creates a new record of an entity.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-345">This operation creates a new record of an entity.</span></span>

| <span data-ttu-id="a3e1d-346">Property name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-346">Property name</span></span> | <span data-ttu-id="a3e1d-347">Display name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-347">Display name</span></span> | <span data-ttu-id="a3e1d-348">Description</span><span class="sxs-lookup"><span data-stu-id="a3e1d-348">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3e1d-349">dataset\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-349">dataset\*</span></span> |<span data-ttu-id="a3e1d-350">Organization Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-350">Organization Name</span></span> |<span data-ttu-id="a3e1d-351">Name of the Dynamics 365 organization like Contoso</span><span class="sxs-lookup"><span data-stu-id="a3e1d-351">Name of the Dynamics 365 organization like Contoso</span></span> |
| <span data-ttu-id="a3e1d-352">table\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-352">table\*</span></span> |<span data-ttu-id="a3e1d-353">Entity Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-353">Entity Name</span></span> |<span data-ttu-id="a3e1d-354">Name of the entity</span><span class="sxs-lookup"><span data-stu-id="a3e1d-354">Name of the entity</span></span> |

<span data-ttu-id="a3e1d-355">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-355">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="a3e1d-356">Output Details</span><span class="sxs-lookup"><span data-stu-id="a3e1d-356">Output Details</span></span>
<span data-ttu-id="a3e1d-357">None.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-357">None.</span></span>

#### <a name="get-record"></a><span data-ttu-id="a3e1d-358">Get record</span><span class="sxs-lookup"><span data-stu-id="a3e1d-358">Get record</span></span>
<span data-ttu-id="a3e1d-359">This operation gets the specified record for an entity.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-359">This operation gets the specified record for an entity.</span></span>

| <span data-ttu-id="a3e1d-360">Property name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-360">Property name</span></span> | <span data-ttu-id="a3e1d-361">Display name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-361">Display name</span></span> | <span data-ttu-id="a3e1d-362">Description</span><span class="sxs-lookup"><span data-stu-id="a3e1d-362">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3e1d-363">dataset\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-363">dataset\*</span></span> |<span data-ttu-id="a3e1d-364">Organization Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-364">Organization Name</span></span> |<span data-ttu-id="a3e1d-365">Name of the Dynamics 365 organization like Contoso</span><span class="sxs-lookup"><span data-stu-id="a3e1d-365">Name of the Dynamics 365 organization like Contoso</span></span> |
| <span data-ttu-id="a3e1d-366">table\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-366">table\*</span></span> |<span data-ttu-id="a3e1d-367">Entity Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-367">Entity Name</span></span> |<span data-ttu-id="a3e1d-368">Name of the entity</span><span class="sxs-lookup"><span data-stu-id="a3e1d-368">Name of the entity</span></span> |
| <span data-ttu-id="a3e1d-369">id\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-369">id\*</span></span> |<span data-ttu-id="a3e1d-370">Item identifier</span><span class="sxs-lookup"><span data-stu-id="a3e1d-370">Item identifier</span></span> |<span data-ttu-id="a3e1d-371">Specify the Identifier for the record</span><span class="sxs-lookup"><span data-stu-id="a3e1d-371">Specify the Identifier for the record</span></span> |

<span data-ttu-id="a3e1d-372">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-372">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="a3e1d-373">Output Details</span><span class="sxs-lookup"><span data-stu-id="a3e1d-373">Output Details</span></span>
<span data-ttu-id="a3e1d-374">None.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-374">None.</span></span>

#### <a name="delete-a-record"></a><span data-ttu-id="a3e1d-375">Delete a record</span><span class="sxs-lookup"><span data-stu-id="a3e1d-375">Delete a record</span></span>
<span data-ttu-id="a3e1d-376">This operation deletes a record from an entity collection.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-376">This operation deletes a record from an entity collection.</span></span>

| <span data-ttu-id="a3e1d-377">Property name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-377">Property name</span></span> | <span data-ttu-id="a3e1d-378">Display name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-378">Display name</span></span> | <span data-ttu-id="a3e1d-379">Description</span><span class="sxs-lookup"><span data-stu-id="a3e1d-379">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3e1d-380">dataset\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-380">dataset\*</span></span> |<span data-ttu-id="a3e1d-381">Organization Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-381">Organization Name</span></span> |<span data-ttu-id="a3e1d-382">Name of the Dynamics 365 organization like Contoso</span><span class="sxs-lookup"><span data-stu-id="a3e1d-382">Name of the Dynamics 365 organization like Contoso</span></span> |
| <span data-ttu-id="a3e1d-383">table\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-383">table\*</span></span> |<span data-ttu-id="a3e1d-384">Entity Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-384">Entity Name</span></span> |<span data-ttu-id="a3e1d-385">Name of the entity</span><span class="sxs-lookup"><span data-stu-id="a3e1d-385">Name of the entity</span></span> |
| <span data-ttu-id="a3e1d-386">id\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-386">id\*</span></span> |<span data-ttu-id="a3e1d-387">Item identifier</span><span class="sxs-lookup"><span data-stu-id="a3e1d-387">Item identifier</span></span> |<span data-ttu-id="a3e1d-388">Specify the identifier for the record</span><span class="sxs-lookup"><span data-stu-id="a3e1d-388">Specify the identifier for the record</span></span> |

<span data-ttu-id="a3e1d-389">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-389">An asterisk (\*) means the property is required.</span></span>

#### <a name="update-a-record"></a><span data-ttu-id="a3e1d-390">Update a record</span><span class="sxs-lookup"><span data-stu-id="a3e1d-390">Update a record</span></span>
<span data-ttu-id="a3e1d-391">This operation updates an existing record for an entity.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-391">This operation updates an existing record for an entity.</span></span>

| <span data-ttu-id="a3e1d-392">Property name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-392">Property name</span></span> | <span data-ttu-id="a3e1d-393">Display name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-393">Display name</span></span> | <span data-ttu-id="a3e1d-394">Description</span><span class="sxs-lookup"><span data-stu-id="a3e1d-394">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3e1d-395">dataset\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-395">dataset\*</span></span> |<span data-ttu-id="a3e1d-396">Organization Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-396">Organization Name</span></span> |<span data-ttu-id="a3e1d-397">Name of the Dynamics 365 organization like Contoso</span><span class="sxs-lookup"><span data-stu-id="a3e1d-397">Name of the Dynamics 365 organization like Contoso</span></span> |
| <span data-ttu-id="a3e1d-398">table\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-398">table\*</span></span> |<span data-ttu-id="a3e1d-399">Entity Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-399">Entity Name</span></span> |<span data-ttu-id="a3e1d-400">Name of the entity</span><span class="sxs-lookup"><span data-stu-id="a3e1d-400">Name of the entity</span></span> |
| <span data-ttu-id="a3e1d-401">id\*</span><span class="sxs-lookup"><span data-stu-id="a3e1d-401">id\*</span></span> |<span data-ttu-id="a3e1d-402">Record identifier</span><span class="sxs-lookup"><span data-stu-id="a3e1d-402">Record identifier</span></span> |<span data-ttu-id="a3e1d-403">Specify the identifier for the record</span><span class="sxs-lookup"><span data-stu-id="a3e1d-403">Specify the identifier for the record</span></span> |

<span data-ttu-id="a3e1d-404">An asterisk (\*) means the property is required.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-404">An asterisk (\*) means the property is required.</span></span>

##### <a name="output-details"></a><span data-ttu-id="a3e1d-405">Output Details</span><span class="sxs-lookup"><span data-stu-id="a3e1d-405">Output Details</span></span>
<span data-ttu-id="a3e1d-406">None.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-406">None.</span></span>

## <a name="http-responses"></a><span data-ttu-id="a3e1d-407">HTTP responses</span><span class="sxs-lookup"><span data-stu-id="a3e1d-407">HTTP responses</span></span>
<span data-ttu-id="a3e1d-408">The actions and triggers can return one or more of the following HTTP status codes:</span><span class="sxs-lookup"><span data-stu-id="a3e1d-408">The actions and triggers can return one or more of the following HTTP status codes:</span></span>

| <span data-ttu-id="a3e1d-409">Name</span><span class="sxs-lookup"><span data-stu-id="a3e1d-409">Name</span></span> | <span data-ttu-id="a3e1d-410">Description</span><span class="sxs-lookup"><span data-stu-id="a3e1d-410">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3e1d-411">200</span><span class="sxs-lookup"><span data-stu-id="a3e1d-411">200</span></span> |<span data-ttu-id="a3e1d-412">OK</span><span class="sxs-lookup"><span data-stu-id="a3e1d-412">OK</span></span> |
| <span data-ttu-id="a3e1d-413">202</span><span class="sxs-lookup"><span data-stu-id="a3e1d-413">202</span></span> |<span data-ttu-id="a3e1d-414">Accepted</span><span class="sxs-lookup"><span data-stu-id="a3e1d-414">Accepted</span></span> |
| <span data-ttu-id="a3e1d-415">400</span><span class="sxs-lookup"><span data-stu-id="a3e1d-415">400</span></span> |<span data-ttu-id="a3e1d-416">Bad Request</span><span class="sxs-lookup"><span data-stu-id="a3e1d-416">Bad Request</span></span> |
| <span data-ttu-id="a3e1d-417">401</span><span class="sxs-lookup"><span data-stu-id="a3e1d-417">401</span></span> |<span data-ttu-id="a3e1d-418">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="a3e1d-418">Unauthorized</span></span> |
| <span data-ttu-id="a3e1d-419">403</span><span class="sxs-lookup"><span data-stu-id="a3e1d-419">403</span></span> |<span data-ttu-id="a3e1d-420">Forbidden</span><span class="sxs-lookup"><span data-stu-id="a3e1d-420">Forbidden</span></span> |
| <span data-ttu-id="a3e1d-421">404</span><span class="sxs-lookup"><span data-stu-id="a3e1d-421">404</span></span> |<span data-ttu-id="a3e1d-422">Not Found</span><span class="sxs-lookup"><span data-stu-id="a3e1d-422">Not Found</span></span> |
| <span data-ttu-id="a3e1d-423">500</span><span class="sxs-lookup"><span data-stu-id="a3e1d-423">500</span></span> |<span data-ttu-id="a3e1d-424">Internal Server Error.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-424">Internal Server Error.</span></span> <span data-ttu-id="a3e1d-425">Unknown error occurred.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-425">Unknown error occurred.</span></span> |
| <span data-ttu-id="a3e1d-426">default</span><span class="sxs-lookup"><span data-stu-id="a3e1d-426">default</span></span> |<span data-ttu-id="a3e1d-427">Operation Failed.</span><span class="sxs-lookup"><span data-stu-id="a3e1d-427">Operation Failed.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a3e1d-428">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3e1d-428">Next steps</span></span>
<span data-ttu-id="a3e1d-429">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a3e1d-429">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>














