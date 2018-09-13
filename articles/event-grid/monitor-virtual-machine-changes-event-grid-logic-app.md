---
title: Monitor virtual machine changes - Azure Event Grid & Logic Apps | Microsoft Docs
description: Check for config changes in virtual machines (VMs) by using Azure Event Grid and Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.topic: tutorial
ms.date: 11/30/2017
ms.openlocfilehash: 29b28b0d81314d062c1b334092979cc9bccbeb31
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864623"
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a><span data-ttu-id="02f23-103">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span><span class="sxs-lookup"><span data-stu-id="02f23-103">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>

<span data-ttu-id="02f23-104">You can start an automated [logic app workflow](../logic-apps/logic-apps-overview.md) when specific events happen in Azure resources or third-party resources.</span><span class="sxs-lookup"><span data-stu-id="02f23-104">You can start an automated [logic app workflow](../logic-apps/logic-apps-overview.md) when specific events happen in Azure resources or third-party resources.</span></span> <span data-ttu-id="02f23-105">These resources can publish those events to an [Azure event grid](../event-grid/overview.md).</span><span class="sxs-lookup"><span data-stu-id="02f23-105">These resources can publish those events to an [Azure event grid](../event-grid/overview.md).</span></span> <span data-ttu-id="02f23-106">In turn, the event grid pushes those events to subscribers that have queues, webhooks, or [event hubs](../event-hubs/event-hubs-what-is-event-hubs.md) as endpoints.</span><span class="sxs-lookup"><span data-stu-id="02f23-106">In turn, the event grid pushes those events to subscribers that have queues, webhooks, or [event hubs](../event-hubs/event-hubs-what-is-event-hubs.md) as endpoints.</span></span> <span data-ttu-id="02f23-107">As a subscriber, your logic app can wait for those events from the event grid before running automated workflows to perform tasks - without you writing any code.</span><span class="sxs-lookup"><span data-stu-id="02f23-107">As a subscriber, your logic app can wait for those events from the event grid before running automated workflows to perform tasks - without you writing any code.</span></span>

<span data-ttu-id="02f23-108">For example, here are some events that publishers can send to subscribers through the Azure Event Grid service:</span><span class="sxs-lookup"><span data-stu-id="02f23-108">For example, here are some events that publishers can send to subscribers through the Azure Event Grid service:</span></span>

* <span data-ttu-id="02f23-109">Create, read, update, or delete a resource.</span><span class="sxs-lookup"><span data-stu-id="02f23-109">Create, read, update, or delete a resource.</span></span> <span data-ttu-id="02f23-110">For example, you can monitor changes that might incur charges on your Azure subscription and affect your bill.</span><span class="sxs-lookup"><span data-stu-id="02f23-110">For example, you can monitor changes that might incur charges on your Azure subscription and affect your bill.</span></span> 
* <span data-ttu-id="02f23-111">Add or remove a person from an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="02f23-111">Add or remove a person from an Azure subscription.</span></span>
* <span data-ttu-id="02f23-112">Your app performs a particular action.</span><span class="sxs-lookup"><span data-stu-id="02f23-112">Your app performs a particular action.</span></span>
* <span data-ttu-id="02f23-113">A new message appears in a queue.</span><span class="sxs-lookup"><span data-stu-id="02f23-113">A new message appears in a queue.</span></span>

<span data-ttu-id="02f23-114">This tutorial creates a logic app that monitors changes to a virtual machine and sends emails about those changes.</span><span class="sxs-lookup"><span data-stu-id="02f23-114">This tutorial creates a logic app that monitors changes to a virtual machine and sends emails about those changes.</span></span> <span data-ttu-id="02f23-115">When you create a logic app with an event subscription for an Azure resource, events flow from that resource through an event grid to the logic app.</span><span class="sxs-lookup"><span data-stu-id="02f23-115">When you create a logic app with an event subscription for an Azure resource, events flow from that resource through an event grid to the logic app.</span></span> <span data-ttu-id="02f23-116">The tutorial walks you through building this logic app:</span><span class="sxs-lookup"><span data-stu-id="02f23-116">The tutorial walks you through building this logic app:</span></span>

![Overview - monitor virtual machine with event grid and logic app](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

<span data-ttu-id="02f23-118">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="02f23-118">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="02f23-119">Create a logic app that monitors events from an event grid.</span><span class="sxs-lookup"><span data-stu-id="02f23-119">Create a logic app that monitors events from an event grid.</span></span>
> * <span data-ttu-id="02f23-120">Add a condition that specifically checks for virtual machine changes.</span><span class="sxs-lookup"><span data-stu-id="02f23-120">Add a condition that specifically checks for virtual machine changes.</span></span>
> * <span data-ttu-id="02f23-121">Send email when your virtual machine changes.</span><span class="sxs-lookup"><span data-stu-id="02f23-121">Send email when your virtual machine changes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02f23-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="02f23-122">Prerequisites</span></span>

* <span data-ttu-id="02f23-123">An email account from [any email provider supported by Azure Logic Apps](../connectors/apis-list.md), such as Office 365 Outlook, Outlook.com, or Gmail, for sending notifications.</span><span class="sxs-lookup"><span data-stu-id="02f23-123">An email account from [any email provider supported by Azure Logic Apps](../connectors/apis-list.md), such as Office 365 Outlook, Outlook.com, or Gmail, for sending notifications.</span></span> <span data-ttu-id="02f23-124">This tutorial uses Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="02f23-124">This tutorial uses Office 365 Outlook.</span></span>

* <span data-ttu-id="02f23-125">A [virtual machine](https://azure.microsoft.com/services/virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="02f23-125">A [virtual machine](https://azure.microsoft.com/services/virtual-machines).</span></span> <span data-ttu-id="02f23-126">If you haven't already done so, create a virtual machine through a [Create a VM tutorial](https://docs.microsoft.com/azure/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="02f23-126">If you haven't already done so, create a virtual machine through a [Create a VM tutorial](https://docs.microsoft.com/azure/virtual-machines/).</span></span> <span data-ttu-id="02f23-127">To make the virtual machine publish events, you [don't need to do anything else](../event-grid/overview.md).</span><span class="sxs-lookup"><span data-stu-id="02f23-127">To make the virtual machine publish events, you [don't need to do anything else](../event-grid/overview.md).</span></span>

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a><span data-ttu-id="02f23-128">Create a logic app that monitors events from an event grid</span><span class="sxs-lookup"><span data-stu-id="02f23-128">Create a logic app that monitors events from an event grid</span></span>

<span data-ttu-id="02f23-129">First, create a logic app and add an Event grid trigger that monitors the resource group for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="02f23-129">First, create a logic app and add an Event grid trigger that monitors the resource group for your virtual machine.</span></span> 

1. <span data-ttu-id="02f23-130">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02f23-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span> 

2. <span data-ttu-id="02f23-131">From the upper left corner of the main Azure menu, choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="02f23-131">From the upper left corner of the main Azure menu, choose **Create a resource** > **Enterprise Integration** > **Logic App**.</span></span>

   ![Create logic app](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. <span data-ttu-id="02f23-133">Create your logic app with the settings specified in the following table:</span><span class="sxs-lookup"><span data-stu-id="02f23-133">Create your logic app with the settings specified in the following table:</span></span>

   ![Provide logic app details](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | <span data-ttu-id="02f23-135">Setting</span><span class="sxs-lookup"><span data-stu-id="02f23-135">Setting</span></span> | <span data-ttu-id="02f23-136">Suggested value</span><span class="sxs-lookup"><span data-stu-id="02f23-136">Suggested value</span></span> | <span data-ttu-id="02f23-137">Description</span><span class="sxs-lookup"><span data-stu-id="02f23-137">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="02f23-138">**Name**</span><span class="sxs-lookup"><span data-stu-id="02f23-138">**Name**</span></span> | <span data-ttu-id="02f23-139">*{your-logic-app-name}*</span><span class="sxs-lookup"><span data-stu-id="02f23-139">*{your-logic-app-name}*</span></span> | <span data-ttu-id="02f23-140">Provide a unique logic app name.</span><span class="sxs-lookup"><span data-stu-id="02f23-140">Provide a unique logic app name.</span></span> | 
   | <span data-ttu-id="02f23-141">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="02f23-141">**Subscription**</span></span> | <span data-ttu-id="02f23-142">*{your-Azure-subscription}*</span><span class="sxs-lookup"><span data-stu-id="02f23-142">*{your-Azure-subscription}*</span></span> | <span data-ttu-id="02f23-143">Select the same Azure subscription for all services in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="02f23-143">Select the same Azure subscription for all services in this tutorial.</span></span> | 
   | <span data-ttu-id="02f23-144">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="02f23-144">**Resource group**</span></span> | <span data-ttu-id="02f23-145">*{your-Azure-resource-group}*</span><span class="sxs-lookup"><span data-stu-id="02f23-145">*{your-Azure-resource-group}*</span></span> | <span data-ttu-id="02f23-146">Select the same Azure resource group for all services in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="02f23-146">Select the same Azure resource group for all services in this tutorial.</span></span> | 
   | <span data-ttu-id="02f23-147">**Location**</span><span class="sxs-lookup"><span data-stu-id="02f23-147">**Location**</span></span> | <span data-ttu-id="02f23-148">*{your-Azure-region}*</span><span class="sxs-lookup"><span data-stu-id="02f23-148">*{your-Azure-region}*</span></span> | <span data-ttu-id="02f23-149">Select the same region for all services in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="02f23-149">Select the same region for all services in this tutorial.</span></span> | 
   | | | 

4. <span data-ttu-id="02f23-150">When you're ready, select **Pin to dashboard**, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="02f23-150">When you're ready, select **Pin to dashboard**, and choose **Create**.</span></span>

   <span data-ttu-id="02f23-151">You've now created an Azure resource for your logic app.</span><span class="sxs-lookup"><span data-stu-id="02f23-151">You've now created an Azure resource for your logic app.</span></span> 
   <span data-ttu-id="02f23-152">After Azure deploys your logic app, the Logic Apps Designer shows you templates for common patterns so you can get started faster.</span><span class="sxs-lookup"><span data-stu-id="02f23-152">After Azure deploys your logic app, the Logic Apps Designer shows you templates for common patterns so you can get started faster.</span></span>

   > [!NOTE] 
   > <span data-ttu-id="02f23-153">When you select **Pin to dashboard**, your logic app automatically opens in Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="02f23-153">When you select **Pin to dashboard**, your logic app automatically opens in Logic Apps Designer.</span></span> <span data-ttu-id="02f23-154">Otherwise, you can manually find and open your logic app.</span><span class="sxs-lookup"><span data-stu-id="02f23-154">Otherwise, you can manually find and open your logic app.</span></span>

5. <span data-ttu-id="02f23-155">Now choose a logic app template.</span><span class="sxs-lookup"><span data-stu-id="02f23-155">Now choose a logic app template.</span></span> <span data-ttu-id="02f23-156">Under **Templates**, choose **Blank Logic App** so you can build your logic app from scratch.</span><span class="sxs-lookup"><span data-stu-id="02f23-156">Under **Templates**, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

   ![Choose logic app template](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   <span data-ttu-id="02f23-158">The Logic Apps Designer now shows you [*connectors*](../connectors/apis-list.md) and [*triggers*](../logic-apps/logic-apps-overview.md#logic-app-concepts) that you can use to start your logic app, and also actions that you can add after a trigger to perform tasks.</span><span class="sxs-lookup"><span data-stu-id="02f23-158">The Logic Apps Designer now shows you [*connectors*](../connectors/apis-list.md) and [*triggers*](../logic-apps/logic-apps-overview.md#logic-app-concepts) that you can use to start your logic app, and also actions that you can add after a trigger to perform tasks.</span></span> <span data-ttu-id="02f23-159">A trigger is an event that creates a logic app instance and starts your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="02f23-159">A trigger is an event that creates a logic app instance and starts your logic app workflow.</span></span> 
   <span data-ttu-id="02f23-160">Your logic app needs a trigger as the first item.</span><span class="sxs-lookup"><span data-stu-id="02f23-160">Your logic app needs a trigger as the first item.</span></span>

6. <span data-ttu-id="02f23-161">In the search box, enter "event grid" as your filter.</span><span class="sxs-lookup"><span data-stu-id="02f23-161">In the search box, enter "event grid" as your filter.</span></span> <span data-ttu-id="02f23-162">Select this trigger: **Azure Event Grid - On a resource event**</span><span class="sxs-lookup"><span data-stu-id="02f23-162">Select this trigger: **Azure Event Grid - On a resource event**</span></span>

   ![Select this trigger: "Azure Event Grid - On a resource event"](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. <span data-ttu-id="02f23-164">When prompted, sign in to Azure Event Grid with your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="02f23-164">When prompted, sign in to Azure Event Grid with your Azure credentials.</span></span>

   ![Sign in with your Azure credentials](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > <span data-ttu-id="02f23-166">If you're signed in with a personal Microsoft account, such as @outlook.com or @hotmail.com, the Event Grid trigger might not appear correctly.</span><span class="sxs-lookup"><span data-stu-id="02f23-166">If you're signed in with a personal Microsoft account, such as @outlook.com or @hotmail.com, the Event Grid trigger might not appear correctly.</span></span> <span data-ttu-id="02f23-167">As a workaround, choose [Connect with Service Principal](../azure-resource-manager/resource-group-create-service-principal-portal.md), or authenticate as a member of the Azure Active Directory that's associated with your Azure subscription, for example, *user-name*@emailoutlook.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="02f23-167">As a workaround, choose [Connect with Service Principal](../azure-resource-manager/resource-group-create-service-principal-portal.md), or authenticate as a member of the Azure Active Directory that's associated with your Azure subscription, for example, *user-name*@emailoutlook.onmicrosoft.com.</span></span>

8. <span data-ttu-id="02f23-168">Now subscribe your logic app to publisher events.</span><span class="sxs-lookup"><span data-stu-id="02f23-168">Now subscribe your logic app to publisher events.</span></span> <span data-ttu-id="02f23-169">Provide the details for your event subscription as specified in the following table:</span><span class="sxs-lookup"><span data-stu-id="02f23-169">Provide the details for your event subscription as specified in the following table:</span></span>

   ![Provide details for event subscription](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | <span data-ttu-id="02f23-171">Setting</span><span class="sxs-lookup"><span data-stu-id="02f23-171">Setting</span></span> | <span data-ttu-id="02f23-172">Suggested value</span><span class="sxs-lookup"><span data-stu-id="02f23-172">Suggested value</span></span> | <span data-ttu-id="02f23-173">Description</span><span class="sxs-lookup"><span data-stu-id="02f23-173">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="02f23-174">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="02f23-174">**Subscription**</span></span> | <span data-ttu-id="02f23-175">*{virtual-machine-Azure-subscription}*</span><span class="sxs-lookup"><span data-stu-id="02f23-175">*{virtual-machine-Azure-subscription}*</span></span> | <span data-ttu-id="02f23-176">Select the event publisher's Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="02f23-176">Select the event publisher's Azure subscription.</span></span> <span data-ttu-id="02f23-177">For this tutorial, select the Azure subscription for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="02f23-177">For this tutorial, select the Azure subscription for your virtual machine.</span></span> | 
   | <span data-ttu-id="02f23-178">**Resource Type**</span><span class="sxs-lookup"><span data-stu-id="02f23-178">**Resource Type**</span></span> | <span data-ttu-id="02f23-179">Microsoft.Resources.resourceGroups</span><span class="sxs-lookup"><span data-stu-id="02f23-179">Microsoft.Resources.resourceGroups</span></span> | <span data-ttu-id="02f23-180">Select the event publisher's resource type.</span><span class="sxs-lookup"><span data-stu-id="02f23-180">Select the event publisher's resource type.</span></span> <span data-ttu-id="02f23-181">For this tutorial, select the specified value so your logic app monitors only resource groups.</span><span class="sxs-lookup"><span data-stu-id="02f23-181">For this tutorial, select the specified value so your logic app monitors only resource groups.</span></span> | 
   | <span data-ttu-id="02f23-182">**Resource Name**</span><span class="sxs-lookup"><span data-stu-id="02f23-182">**Resource Name**</span></span> | <span data-ttu-id="02f23-183">*{virtual-machine-resource-group-name}*</span><span class="sxs-lookup"><span data-stu-id="02f23-183">*{virtual-machine-resource-group-name}*</span></span> | <span data-ttu-id="02f23-184">Select the publisher's resource name.</span><span class="sxs-lookup"><span data-stu-id="02f23-184">Select the publisher's resource name.</span></span> <span data-ttu-id="02f23-185">For this tutorial, select the name of the resource group for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="02f23-185">For this tutorial, select the name of the resource group for your virtual machine.</span></span> | 
   | <span data-ttu-id="02f23-186">For optional settings, choose **Show advanced options**.</span><span class="sxs-lookup"><span data-stu-id="02f23-186">For optional settings, choose **Show advanced options**.</span></span> | <span data-ttu-id="02f23-187">*{see descriptions}*</span><span class="sxs-lookup"><span data-stu-id="02f23-187">*{see descriptions}*</span></span> | <span data-ttu-id="02f23-188">\* **Prefix Filter**: For this tutorial, leave this setting empty.</span><span class="sxs-lookup"><span data-stu-id="02f23-188">\* **Prefix Filter**: For this tutorial, leave this setting empty.</span></span> <span data-ttu-id="02f23-189">The default behavior matches all values.</span><span class="sxs-lookup"><span data-stu-id="02f23-189">The default behavior matches all values.</span></span> <span data-ttu-id="02f23-190">However, you can specify a prefix string as a filter, for example, a path and a parameter for a specific resource.</span><span class="sxs-lookup"><span data-stu-id="02f23-190">However, you can specify a prefix string as a filter, for example, a path and a parameter for a specific resource.</span></span> <p><span data-ttu-id="02f23-191">\* **Suffix Filter**: For this tutorial, leave this setting empty.</span><span class="sxs-lookup"><span data-stu-id="02f23-191">\* **Suffix Filter**: For this tutorial, leave this setting empty.</span></span> <span data-ttu-id="02f23-192">The default behavior matches all values.</span><span class="sxs-lookup"><span data-stu-id="02f23-192">The default behavior matches all values.</span></span> <span data-ttu-id="02f23-193">However, you can specify a suffix string as a filter, for example, a file name extension, when you want only specific file types.</span><span class="sxs-lookup"><span data-stu-id="02f23-193">However, you can specify a suffix string as a filter, for example, a file name extension, when you want only specific file types.</span></span><p><span data-ttu-id="02f23-194">\* **Subscription Name**: Provide a unique name for your event subscription.</span><span class="sxs-lookup"><span data-stu-id="02f23-194">\* **Subscription Name**: Provide a unique name for your event subscription.</span></span> |
   | | | 

   <span data-ttu-id="02f23-195">When you're done, your event grid trigger might look like this example:</span><span class="sxs-lookup"><span data-stu-id="02f23-195">When you're done, your event grid trigger might look like this example:</span></span>
   
   ![Example event grid trigger details](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. <span data-ttu-id="02f23-197">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="02f23-197">Save your logic app.</span></span> <span data-ttu-id="02f23-198">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="02f23-198">On the designer toolbar, choose **Save**.</span></span> <span data-ttu-id="02f23-199">To collapse and hide an action's details in your logic app, choose the action's title bar.</span><span class="sxs-lookup"><span data-stu-id="02f23-199">To collapse and hide an action's details in your logic app, choose the action's title bar.</span></span>

   ![Save your logic app](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   <span data-ttu-id="02f23-201">When you save your logic app with an event grid trigger, Azure automatically creates an event subscription for your logic app to your selected resource.</span><span class="sxs-lookup"><span data-stu-id="02f23-201">When you save your logic app with an event grid trigger, Azure automatically creates an event subscription for your logic app to your selected resource.</span></span> <span data-ttu-id="02f23-202">So when the resource publishes an event to the event grid, that event grid automatically pushes the event to your logic app.</span><span class="sxs-lookup"><span data-stu-id="02f23-202">So when the resource publishes an event to the event grid, that event grid automatically pushes the event to your logic app.</span></span> <span data-ttu-id="02f23-203">This event triggers your logic app, then creates and runs an instance of the workflow that you define in these next steps.</span><span class="sxs-lookup"><span data-stu-id="02f23-203">This event triggers your logic app, then creates and runs an instance of the workflow that you define in these next steps.</span></span>

<span data-ttu-id="02f23-204">Your logic app is now live and listens to events from the event grid, but doesn't do anything until you add actions to the workflow.</span><span class="sxs-lookup"><span data-stu-id="02f23-204">Your logic app is now live and listens to events from the event grid, but doesn't do anything until you add actions to the workflow.</span></span> 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a><span data-ttu-id="02f23-205">Add a condition that checks for virtual machine changes</span><span class="sxs-lookup"><span data-stu-id="02f23-205">Add a condition that checks for virtual machine changes</span></span>

<span data-ttu-id="02f23-206">To run your logic app workflow only when a specific event happens, add a condition that checks for virtual machine "write" operations.</span><span class="sxs-lookup"><span data-stu-id="02f23-206">To run your logic app workflow only when a specific event happens, add a condition that checks for virtual machine "write" operations.</span></span> <span data-ttu-id="02f23-207">When this condition is true, your logic app sends you email with details about the updated virtual machine.</span><span class="sxs-lookup"><span data-stu-id="02f23-207">When this condition is true, your logic app sends you email with details about the updated virtual machine.</span></span>

1. <span data-ttu-id="02f23-208">In Logic App Designer, under the event grid trigger, choose **New step** > **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="02f23-208">In Logic App Designer, under the event grid trigger, choose **New step** > **Add a condition**.</span></span>

   ![Add a condition to your logic app](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   <span data-ttu-id="02f23-210">The Logic App Designer adds an empty condition to your workflow, including action paths to follow based whether the condition is true or false.</span><span class="sxs-lookup"><span data-stu-id="02f23-210">The Logic App Designer adds an empty condition to your workflow, including action paths to follow based whether the condition is true or false.</span></span>

   ![Empty condition](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. <span data-ttu-id="02f23-212">In the **Condition** box, choose **Edit in advanced mode**.</span><span class="sxs-lookup"><span data-stu-id="02f23-212">In the **Condition** box, choose **Edit in advanced mode**.</span></span>
<span data-ttu-id="02f23-213">Enter this expression:</span><span class="sxs-lookup"><span data-stu-id="02f23-213">Enter this expression:</span></span>

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   <span data-ttu-id="02f23-214">Your condition now looks like this example:</span><span class="sxs-lookup"><span data-stu-id="02f23-214">Your condition now looks like this example:</span></span>

   ![Empty condition](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   <span data-ttu-id="02f23-216">This expression checks the event `body` for a `data` object where the `operationName` property is the `Microsoft.Compute/virtualMachines/write` operation.</span><span class="sxs-lookup"><span data-stu-id="02f23-216">This expression checks the event `body` for a `data` object where the `operationName` property is the `Microsoft.Compute/virtualMachines/write` operation.</span></span> 
   <span data-ttu-id="02f23-217">Learn more about [Event Grid event schema](../event-grid/event-schema.md).</span><span class="sxs-lookup"><span data-stu-id="02f23-217">Learn more about [Event Grid event schema](../event-grid/event-schema.md).</span></span>

3. <span data-ttu-id="02f23-218">To provide a description for the condition, choose the **ellipses** (**...**) button on the condition shape, then choose **Rename**.</span><span class="sxs-lookup"><span data-stu-id="02f23-218">To provide a description for the condition, choose the **ellipses** (**...**) button on the condition shape, then choose **Rename**.</span></span>

   > [!NOTE] 
   > <span data-ttu-id="02f23-219">The later examples in this tutorial also provide descriptions for steps in the logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="02f23-219">The later examples in this tutorial also provide descriptions for steps in the logic app workflow.</span></span>

4. <span data-ttu-id="02f23-220">Now choose **Edit in basic mode** so that the expression automatically resolves as shown:</span><span class="sxs-lookup"><span data-stu-id="02f23-220">Now choose **Edit in basic mode** so that the expression automatically resolves as shown:</span></span>

   ![Logic app condition](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. <span data-ttu-id="02f23-222">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="02f23-222">Save your logic app.</span></span>

## <a name="send-email-when-your-virtual-machine-changes"></a><span data-ttu-id="02f23-223">Send email when your virtual machine changes</span><span class="sxs-lookup"><span data-stu-id="02f23-223">Send email when your virtual machine changes</span></span>

<span data-ttu-id="02f23-224">Now add an [*action*](../logic-apps/logic-apps-overview.md#logic-app-concepts) so that you get an email when the specified condition is true.</span><span class="sxs-lookup"><span data-stu-id="02f23-224">Now add an [*action*](../logic-apps/logic-apps-overview.md#logic-app-concepts) so that you get an email when the specified condition is true.</span></span>

1. <span data-ttu-id="02f23-225">In the condition's **If true** box, choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="02f23-225">In the condition's **If true** box, choose **Add an action**.</span></span>

   ![Add action for when condition is true](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. <span data-ttu-id="02f23-227">In the search box, enter "email" as your filter.</span><span class="sxs-lookup"><span data-stu-id="02f23-227">In the search box, enter "email" as your filter.</span></span> <span data-ttu-id="02f23-228">Based on your email provider, find and select the matching connector.</span><span class="sxs-lookup"><span data-stu-id="02f23-228">Based on your email provider, find and select the matching connector.</span></span> <span data-ttu-id="02f23-229">Then select the "send email" action for your connector.</span><span class="sxs-lookup"><span data-stu-id="02f23-229">Then select the "send email" action for your connector.</span></span> <span data-ttu-id="02f23-230">For example:</span><span class="sxs-lookup"><span data-stu-id="02f23-230">For example:</span></span> 

   * <span data-ttu-id="02f23-231">For an Azure work or school account, select the Office 365 Outlook connector.</span><span class="sxs-lookup"><span data-stu-id="02f23-231">For an Azure work or school account, select the Office 365 Outlook connector.</span></span> 
   * <span data-ttu-id="02f23-232">For personal Microsoft accounts, select the Outlook.com connector.</span><span class="sxs-lookup"><span data-stu-id="02f23-232">For personal Microsoft accounts, select the Outlook.com connector.</span></span> 
   * <span data-ttu-id="02f23-233">For Gmail accounts, select the Gmail connector.</span><span class="sxs-lookup"><span data-stu-id="02f23-233">For Gmail accounts, select the Gmail connector.</span></span> 

   <span data-ttu-id="02f23-234">We're going to continue with the Office 365 Outlook connector.</span><span class="sxs-lookup"><span data-stu-id="02f23-234">We're going to continue with the Office 365 Outlook connector.</span></span> 
   <span data-ttu-id="02f23-235">If you use a different provider, the steps remain the same, but your UI might appear different.</span><span class="sxs-lookup"><span data-stu-id="02f23-235">If you use a different provider, the steps remain the same, but your UI might appear different.</span></span> 

   ![Select "send email" action](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. <span data-ttu-id="02f23-237">If you don't already have a connection for your email provider, sign in to your email account when you're asked for authentication.</span><span class="sxs-lookup"><span data-stu-id="02f23-237">If you don't already have a connection for your email provider, sign in to your email account when you're asked for authentication.</span></span>

4. <span data-ttu-id="02f23-238">Provide details for the email as specified in the following table:</span><span class="sxs-lookup"><span data-stu-id="02f23-238">Provide details for the email as specified in the following table:</span></span>

   ![Empty email action](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > <span data-ttu-id="02f23-240">To select from fields available in your workflow, click in an edit box so that the **Dynamic content** list opens, or choose **Add dynamic content**.</span><span class="sxs-lookup"><span data-stu-id="02f23-240">To select from fields available in your workflow, click in an edit box so that the **Dynamic content** list opens, or choose **Add dynamic content**.</span></span> <span data-ttu-id="02f23-241">For more fields, choose **See more** for each section in the list.</span><span class="sxs-lookup"><span data-stu-id="02f23-241">For more fields, choose **See more** for each section in the list.</span></span> <span data-ttu-id="02f23-242">To close the **Dynamic content** list, choose **Add dynamic content**.</span><span class="sxs-lookup"><span data-stu-id="02f23-242">To close the **Dynamic content** list, choose **Add dynamic content**.</span></span>

   | <span data-ttu-id="02f23-243">Setting</span><span class="sxs-lookup"><span data-stu-id="02f23-243">Setting</span></span> | <span data-ttu-id="02f23-244">Suggested value</span><span class="sxs-lookup"><span data-stu-id="02f23-244">Suggested value</span></span> | <span data-ttu-id="02f23-245">Description</span><span class="sxs-lookup"><span data-stu-id="02f23-245">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="02f23-246">**To**</span><span class="sxs-lookup"><span data-stu-id="02f23-246">**To**</span></span> | <span data-ttu-id="02f23-247">*{recipient-email-address}*</span><span class="sxs-lookup"><span data-stu-id="02f23-247">*{recipient-email-address}*</span></span> |<span data-ttu-id="02f23-248">Enter the recipient's email address.</span><span class="sxs-lookup"><span data-stu-id="02f23-248">Enter the recipient's email address.</span></span> <span data-ttu-id="02f23-249">For testing purposes, you can use your own email address.</span><span class="sxs-lookup"><span data-stu-id="02f23-249">For testing purposes, you can use your own email address.</span></span> | 
   | <span data-ttu-id="02f23-250">**Subject**</span><span class="sxs-lookup"><span data-stu-id="02f23-250">**Subject**</span></span> | <span data-ttu-id="02f23-251">Resource updated: **Subject**</span><span class="sxs-lookup"><span data-stu-id="02f23-251">Resource updated: **Subject**</span></span>| <span data-ttu-id="02f23-252">Enter the content for the email's subject.</span><span class="sxs-lookup"><span data-stu-id="02f23-252">Enter the content for the email's subject.</span></span> <span data-ttu-id="02f23-253">For this tutorial, enter the suggested text and select the event's **Subject** field.</span><span class="sxs-lookup"><span data-stu-id="02f23-253">For this tutorial, enter the suggested text and select the event's **Subject** field.</span></span> <span data-ttu-id="02f23-254">Here, your email subject includes the name for the updated resource (virtual machine).</span><span class="sxs-lookup"><span data-stu-id="02f23-254">Here, your email subject includes the name for the updated resource (virtual machine).</span></span> | 
   | <span data-ttu-id="02f23-255">**Body**</span><span class="sxs-lookup"><span data-stu-id="02f23-255">**Body**</span></span> | <span data-ttu-id="02f23-256">Resource group: **Topic**</span><span class="sxs-lookup"><span data-stu-id="02f23-256">Resource group: **Topic**</span></span> <p><span data-ttu-id="02f23-257">Event type: **Event Type**</span><span class="sxs-lookup"><span data-stu-id="02f23-257">Event type: **Event Type**</span></span><p><span data-ttu-id="02f23-258">Event ID: **ID**</span><span class="sxs-lookup"><span data-stu-id="02f23-258">Event ID: **ID**</span></span><p><span data-ttu-id="02f23-259">Time: **Event Time**</span><span class="sxs-lookup"><span data-stu-id="02f23-259">Time: **Event Time**</span></span> | <span data-ttu-id="02f23-260">Enter the content for the email's body.</span><span class="sxs-lookup"><span data-stu-id="02f23-260">Enter the content for the email's body.</span></span> <span data-ttu-id="02f23-261">For this tutorial, enter the suggested text and select the event's **Topic**, **Event Type**, **ID**, and **Event Time** fields so that your email includes the resource group name, event type, event timestamp, and event ID for the update.</span><span class="sxs-lookup"><span data-stu-id="02f23-261">For this tutorial, enter the suggested text and select the event's **Topic**, **Event Type**, **ID**, and **Event Time** fields so that your email includes the resource group name, event type, event timestamp, and event ID for the update.</span></span> <p><span data-ttu-id="02f23-262">To add blank lines in your content, press Shift + Enter.</span><span class="sxs-lookup"><span data-stu-id="02f23-262">To add blank lines in your content, press Shift + Enter.</span></span> | 
   | | | 

   > [!NOTE] 
   > <span data-ttu-id="02f23-263">If you select a field that represents an array, the designer automatically adds a **For each** loop around the action that references the array.</span><span class="sxs-lookup"><span data-stu-id="02f23-263">If you select a field that represents an array, the designer automatically adds a **For each** loop around the action that references the array.</span></span> <span data-ttu-id="02f23-264">That way, your logic app performs that action on each array item.</span><span class="sxs-lookup"><span data-stu-id="02f23-264">That way, your logic app performs that action on each array item.</span></span>

   <span data-ttu-id="02f23-265">Now, your email action might look like this example:</span><span class="sxs-lookup"><span data-stu-id="02f23-265">Now, your email action might look like this example:</span></span>

   ![Select outputs to include in email](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   <span data-ttu-id="02f23-267">And your finished logic app might look like this example:</span><span class="sxs-lookup"><span data-stu-id="02f23-267">And your finished logic app might look like this example:</span></span>

   ![Finished logic app](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. <span data-ttu-id="02f23-269">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="02f23-269">Save your logic app.</span></span> <span data-ttu-id="02f23-270">To collapse and hide each action's details in your logic app, choose the action's title bar.</span><span class="sxs-lookup"><span data-stu-id="02f23-270">To collapse and hide each action's details in your logic app, choose the action's title bar.</span></span>

   ![Save your logic app](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   <span data-ttu-id="02f23-272">Your logic app is now live, but waits for changes to your virtual machine before doing anything.</span><span class="sxs-lookup"><span data-stu-id="02f23-272">Your logic app is now live, but waits for changes to your virtual machine before doing anything.</span></span> 
   <span data-ttu-id="02f23-273">To test your logic app now, continue to the next section.</span><span class="sxs-lookup"><span data-stu-id="02f23-273">To test your logic app now, continue to the next section.</span></span>

## <a name="test-your-logic-app-workflow"></a><span data-ttu-id="02f23-274">Test your logic app workflow</span><span class="sxs-lookup"><span data-stu-id="02f23-274">Test your logic app workflow</span></span>

1. <span data-ttu-id="02f23-275">To check that your logic app is getting the specified events, update your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="02f23-275">To check that your logic app is getting the specified events, update your virtual machine.</span></span> 

   <span data-ttu-id="02f23-276">For example, you can resize your virtual machine in the Azure portal or [resize your VM with Azure PowerShell](../virtual-machines/windows/resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="02f23-276">For example, you can resize your virtual machine in the Azure portal or [resize your VM with Azure PowerShell](../virtual-machines/windows/resize-vm.md).</span></span> 

   <span data-ttu-id="02f23-277">After a few moments, you should get an email.</span><span class="sxs-lookup"><span data-stu-id="02f23-277">After a few moments, you should get an email.</span></span> <span data-ttu-id="02f23-278">For example:</span><span class="sxs-lookup"><span data-stu-id="02f23-278">For example:</span></span>

   ![Email about virtual machine update](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. <span data-ttu-id="02f23-280">To review the runs and trigger history for your logic app, on your logic app menu, choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="02f23-280">To review the runs and trigger history for your logic app, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="02f23-281">To view more details about a run, choose the row for that run.</span><span class="sxs-lookup"><span data-stu-id="02f23-281">To view more details about a run, choose the row for that run.</span></span>

   ![Logic app runs history](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. <span data-ttu-id="02f23-283">To view the inputs and outputs for each step, expand the step that you want to review.</span><span class="sxs-lookup"><span data-stu-id="02f23-283">To view the inputs and outputs for each step, expand the step that you want to review.</span></span> <span data-ttu-id="02f23-284">This information can help you diagnose and debug problems in your logic app.</span><span class="sxs-lookup"><span data-stu-id="02f23-284">This information can help you diagnose and debug problems in your logic app.</span></span>
 
   ![Logic app run history details](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

<span data-ttu-id="02f23-286">Congratulations, you've created and run a logic app that monitors resource events through an event grid and emails you when those events happen.</span><span class="sxs-lookup"><span data-stu-id="02f23-286">Congratulations, you've created and run a logic app that monitors resource events through an event grid and emails you when those events happen.</span></span> <span data-ttu-id="02f23-287">You also learned how easily you can create workflows that automate processes and integrate systems and cloud services.</span><span class="sxs-lookup"><span data-stu-id="02f23-287">You also learned how easily you can create workflows that automate processes and integrate systems and cloud services.</span></span>

<span data-ttu-id="02f23-288">You can monitor other configuration changes with event grids and logic apps, for example:</span><span class="sxs-lookup"><span data-stu-id="02f23-288">You can monitor other configuration changes with event grids and logic apps, for example:</span></span>

* <span data-ttu-id="02f23-289">A virtual machine gets role-based access control (RBAC) rights.</span><span class="sxs-lookup"><span data-stu-id="02f23-289">A virtual machine gets role-based access control (RBAC) rights.</span></span>
* <span data-ttu-id="02f23-290">Changes are made to a network security group (NSG) on a network interface (NIC).</span><span class="sxs-lookup"><span data-stu-id="02f23-290">Changes are made to a network security group (NSG) on a network interface (NIC).</span></span>
* <span data-ttu-id="02f23-291">Disks for a virtual machine are added or removed.</span><span class="sxs-lookup"><span data-stu-id="02f23-291">Disks for a virtual machine are added or removed.</span></span>
* <span data-ttu-id="02f23-292">A public IP address is assigned to a virtual machine NIC.</span><span class="sxs-lookup"><span data-stu-id="02f23-292">A public IP address is assigned to a virtual machine NIC.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="02f23-293">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="02f23-293">Clean up resources</span></span>

<span data-ttu-id="02f23-294">This tutorial uses resources and performs actions that incur charges on your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="02f23-294">This tutorial uses resources and performs actions that incur charges on your Azure subscription.</span></span> <span data-ttu-id="02f23-295">So when you're done with the tutorial and testing, make sure that you disable or delete any resources where you don't want to incur charges.</span><span class="sxs-lookup"><span data-stu-id="02f23-295">So when you're done with the tutorial and testing, make sure that you disable or delete any resources where you don't want to incur charges.</span></span>

* <span data-ttu-id="02f23-296">To stop running your logic app without deleting your work, disable your app.</span><span class="sxs-lookup"><span data-stu-id="02f23-296">To stop running your logic app without deleting your work, disable your app.</span></span> <span data-ttu-id="02f23-297">On your logic app menu, choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="02f23-297">On your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="02f23-298">On the toolbar, choose **Disable**.</span><span class="sxs-lookup"><span data-stu-id="02f23-298">On the toolbar, choose **Disable**.</span></span>

  ![Turn off your logic app](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

  > [!TIP]
  > <span data-ttu-id="02f23-300">If you don't see the logic app menu, try returning to the Azure dashboard, and reopen your logic app.</span><span class="sxs-lookup"><span data-stu-id="02f23-300">If you don't see the logic app menu, try returning to the Azure dashboard, and reopen your logic app.</span></span>

* <span data-ttu-id="02f23-301">To permanently delete your logic app, on the logic app menu, choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="02f23-301">To permanently delete your logic app, on the logic app menu, choose **Overview**.</span></span> <span data-ttu-id="02f23-302">On the toolbar, choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="02f23-302">On the toolbar, choose **Delete**.</span></span> <span data-ttu-id="02f23-303">Confirm that you want to delete your logic app, then choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="02f23-303">Confirm that you want to delete your logic app, then choose **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02f23-304">Next steps</span><span class="sxs-lookup"><span data-stu-id="02f23-304">Next steps</span></span>

* [<span data-ttu-id="02f23-305">Create and route custom events with Event Grid</span><span class="sxs-lookup"><span data-stu-id="02f23-305">Create and route custom events with Event Grid</span></span>](../event-grid/custom-event-quickstart.md)
