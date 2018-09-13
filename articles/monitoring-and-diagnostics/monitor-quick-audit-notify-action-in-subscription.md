---
title: Audit and receive notifications about important actions in your Azure subscription
description: Understand the history of resource management, service health, and other subscription activity in the Activity Log, then use an Activity Log alert to receive an email notification when a highly-privileged operation is performed in your subscription.
author: johnkemnetz
services: azure-monitor
ms.service: azure-monitor
ms.topic: quickstart
ms.date: 09/25/2017
ms.author: johnkem
ms.custom: mvc
ms.component: alerts
ms.openlocfilehash: 5a6f4d7ab978543a6871eb0ac3926fa25fb65ad2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856569"
---
# <a name="audit-and-receive-notifications-about-important-actions-in-your-azure-subscription"></a><span data-ttu-id="f37aa-103">Audit and receive notifications about important actions in your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="f37aa-103">Audit and receive notifications about important actions in your Azure subscription</span></span>

<span data-ttu-id="f37aa-104">The **Azure Activity Log** provides a history of subscription-level events in Azure.</span><span class="sxs-lookup"><span data-stu-id="f37aa-104">The **Azure Activity Log** provides a history of subscription-level events in Azure.</span></span> <span data-ttu-id="f37aa-105">It offers information about *who* created, updated, or deleted *what* resources and *when* they did it.</span><span class="sxs-lookup"><span data-stu-id="f37aa-105">It offers information about *who* created, updated, or deleted *what* resources and *when* they did it.</span></span> <span data-ttu-id="f37aa-106">You can create an **Activity Log alert** to receive email, SMS, or webhook notifications when an activity occurs that match your alert conditions.</span><span class="sxs-lookup"><span data-stu-id="f37aa-106">You can create an **Activity Log alert** to receive email, SMS, or webhook notifications when an activity occurs that match your alert conditions.</span></span> <span data-ttu-id="f37aa-107">This Quickstart steps through creating a simple network security group, browsing the Activity Log to understand the event that occurred, and then authoring an Activity Log alert to become notified when any network security group is created going forwards.</span><span class="sxs-lookup"><span data-stu-id="f37aa-107">This Quickstart steps through creating a simple network security group, browsing the Activity Log to understand the event that occurred, and then authoring an Activity Log alert to become notified when any network security group is created going forwards.</span></span>

<span data-ttu-id="f37aa-108">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="f37aa-108">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="f37aa-109">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f37aa-109">Log in to the Azure portal</span></span>

<span data-ttu-id="f37aa-110">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f37aa-110">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-network-security-group"></a><span data-ttu-id="f37aa-111">Create a network security group</span><span class="sxs-lookup"><span data-stu-id="f37aa-111">Create a network security group</span></span>

1. <span data-ttu-id="f37aa-112">Click the **Create a resource** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f37aa-112">Click the **Create a resource** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="f37aa-113">Select **Networking**, select **Network security group**.</span><span class="sxs-lookup"><span data-stu-id="f37aa-113">Select **Networking**, select **Network security group**.</span></span>

3. <span data-ttu-id="f37aa-114">Enter "myNetworkSG" as the **Name** and create a new resource group named **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="f37aa-114">Enter "myNetworkSG" as the **Name** and create a new resource group named **myResourceGroup**.</span></span> <span data-ttu-id="f37aa-115">Click the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="f37aa-115">Click the **Create** button.</span></span>

    ![Create a network security group in the portal](./media/monitor-quick-audit-notify-action-in-subscription/create-network-security-group.png)

## <a name="browse-the-activity-log-in-the-portal"></a><span data-ttu-id="f37aa-117">Browse the Activity Log in the portal</span><span class="sxs-lookup"><span data-stu-id="f37aa-117">Browse the Activity Log in the portal</span></span>

<span data-ttu-id="f37aa-118">An event has now been added to the Activity Log that describes the creation of the network security group.</span><span class="sxs-lookup"><span data-stu-id="f37aa-118">An event has now been added to the Activity Log that describes the creation of the network security group.</span></span> <span data-ttu-id="f37aa-119">Use the following instructions to identify that event.</span><span class="sxs-lookup"><span data-stu-id="f37aa-119">Use the following instructions to identify that event.</span></span>

1. <span data-ttu-id="f37aa-120">Click the **Monitor** button found on the left-hand navigation list.</span><span class="sxs-lookup"><span data-stu-id="f37aa-120">Click the **Monitor** button found on the left-hand navigation list.</span></span> <span data-ttu-id="f37aa-121">It opens to the Activity Log section.</span><span class="sxs-lookup"><span data-stu-id="f37aa-121">It opens to the Activity Log section.</span></span> <span data-ttu-id="f37aa-122">This section contains a history of all actions that users have performed on resources in your subscription, filterable by several properties such as the **Resource Group**, **Timespan**, and **Category**.</span><span class="sxs-lookup"><span data-stu-id="f37aa-122">This section contains a history of all actions that users have performed on resources in your subscription, filterable by several properties such as the **Resource Group**, **Timespan**, and **Category**.</span></span>

2. <span data-ttu-id="f37aa-123">In the **Activity Log** section, click the **Resource Group** dropdown and select **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="f37aa-123">In the **Activity Log** section, click the **Resource Group** dropdown and select **myResourceGroup**.</span></span> <span data-ttu-id="f37aa-124">Change the **Timespan** dropdown to **Last 1 hour**.</span><span class="sxs-lookup"><span data-stu-id="f37aa-124">Change the **Timespan** dropdown to **Last 1 hour**.</span></span> <span data-ttu-id="f37aa-125">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="f37aa-125">Click **Apply**.</span></span>

    ![Filter the Activity Log](./media/monitor-quick-audit-notify-action-in-subscription/browse-activity-log.png)

3. <span data-ttu-id="f37aa-127">Click on the **Write NetworkSecurityGroups** event in the table of events shown.</span><span class="sxs-lookup"><span data-stu-id="f37aa-127">Click on the **Write NetworkSecurityGroups** event in the table of events shown.</span></span>

## <a name="browse-an-event-in-the-activity-log"></a><span data-ttu-id="f37aa-128">Browse an event in the Activity Log</span><span class="sxs-lookup"><span data-stu-id="f37aa-128">Browse an event in the Activity Log</span></span>

<span data-ttu-id="f37aa-129">The section that appears contains basic details of the operation that was performed, including the name, the timestamp, and the user or application that performed it.</span><span class="sxs-lookup"><span data-stu-id="f37aa-129">The section that appears contains basic details of the operation that was performed, including the name, the timestamp, and the user or application that performed it.</span></span>

![View event summary in the Activity Log](./media/monitor-quick-audit-notify-action-in-subscription/activity-log-summary.png)

<span data-ttu-id="f37aa-131">Click on the **JSON** tab to view the full event details.</span><span class="sxs-lookup"><span data-stu-id="f37aa-131">Click on the **JSON** tab to view the full event details.</span></span> <span data-ttu-id="f37aa-132">This includes the details of how the user or application was authorized to perform the operation, the event category and level, and the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="f37aa-132">This includes the details of how the user or application was authorized to perform the operation, the event category and level, and the status of the operation.</span></span>

![View event details in the Activity Log](./media/monitor-quick-audit-notify-action-in-subscription/activity-log-json.png)

## <a name="create-an-activity-log-alert"></a><span data-ttu-id="f37aa-134">Create an Activity Log alert</span><span class="sxs-lookup"><span data-stu-id="f37aa-134">Create an Activity Log alert</span></span>

1. <span data-ttu-id="f37aa-135">Click on the **Summary** tab to return to the event summary.</span><span class="sxs-lookup"><span data-stu-id="f37aa-135">Click on the **Summary** tab to return to the event summary.</span></span>

2. <span data-ttu-id="f37aa-136">In the summary section that appears, click **Add activity log alert**.</span><span class="sxs-lookup"><span data-stu-id="f37aa-136">In the summary section that appears, click **Add activity log alert**.</span></span>

    ![Create a network security group in the portal](./media/monitor-quick-audit-notify-action-in-subscription/activity-log-summary.png)

3. <span data-ttu-id="f37aa-138">In the section that appears, give the Activity Log alert a name and description.</span><span class="sxs-lookup"><span data-stu-id="f37aa-138">In the section that appears, give the Activity Log alert a name and description.</span></span>

4. <span data-ttu-id="f37aa-139">Under **Criteria** ensure that **Event category** is set to **Administrative**, **Resource type** is set to **Network security groups**, **Operation name** is set to **Create or Update Network Security Group**, **Status** is set to **Succeeded** and all other criteria fields are either blank or set to **All**.</span><span class="sxs-lookup"><span data-stu-id="f37aa-139">Under **Criteria** ensure that **Event category** is set to **Administrative**, **Resource type** is set to **Network security groups**, **Operation name** is set to **Create or Update Network Security Group**, **Status** is set to **Succeeded** and all other criteria fields are either blank or set to **All**.</span></span> <span data-ttu-id="f37aa-140">The criteria define the rules used to determine whether the alert should be activated when a new event appears in the Activity Log.</span><span class="sxs-lookup"><span data-stu-id="f37aa-140">The criteria define the rules used to determine whether the alert should be activated when a new event appears in the Activity Log.</span></span>

    ![Create a network security group in the portal](./media/monitor-quick-audit-notify-action-in-subscription/activity-log-alert-criteria.png)

5. <span data-ttu-id="f37aa-142">Under **Alert via** select **New** action group and provide a **name** and **short name** for the action group.</span><span class="sxs-lookup"><span data-stu-id="f37aa-142">Under **Alert via** select **New** action group and provide a **name** and **short name** for the action group.</span></span> <span data-ttu-id="f37aa-143">The action group defines the set of actions taken when the alert is activated (when the criteria match a new event).</span><span class="sxs-lookup"><span data-stu-id="f37aa-143">The action group defines the set of actions taken when the alert is activated (when the criteria match a new event).</span></span>

6. <span data-ttu-id="f37aa-144">Under **Actions** add 1 or more actions by providing a **Name** for the action, the **Action type** (for example, email, SMS, or webhook), and **Details** for that particular action type (for example, a webhook URL, email address, or SMS number).</span><span class="sxs-lookup"><span data-stu-id="f37aa-144">Under **Actions** add 1 or more actions by providing a **Name** for the action, the **Action type** (for example, email, SMS, or webhook), and **Details** for that particular action type (for example, a webhook URL, email address, or SMS number).</span></span>

    ![Create a network security group in the portal](./media/monitor-quick-audit-notify-action-in-subscription/activity-log-alert-actions.png)

7. <span data-ttu-id="f37aa-146">Click **Ok** to save the Activity Log alert.</span><span class="sxs-lookup"><span data-stu-id="f37aa-146">Click **Ok** to save the Activity Log alert.</span></span>

## <a name="test-the-activity-log-alert"></a><span data-ttu-id="f37aa-147">Test the Activity Log alert</span><span class="sxs-lookup"><span data-stu-id="f37aa-147">Test the Activity Log alert</span></span>

> [!NOTE]
> <span data-ttu-id="f37aa-148">It takes approximately 5 minutes for an Activity Log alert to become fully enabled.</span><span class="sxs-lookup"><span data-stu-id="f37aa-148">It takes approximately 5 minutes for an Activity Log alert to become fully enabled.</span></span> <span data-ttu-id="f37aa-149">New events that occur before the Activity Log alert is fully enabled do not generate notifications.</span><span class="sxs-lookup"><span data-stu-id="f37aa-149">New events that occur before the Activity Log alert is fully enabled do not generate notifications.</span></span>
>
>

<span data-ttu-id="f37aa-150">To test the alert, repeat the preceding section to **Create a network security group**, but give this network security group a different name and reuse the existing resource group.</span><span class="sxs-lookup"><span data-stu-id="f37aa-150">To test the alert, repeat the preceding section to **Create a network security group**, but give this network security group a different name and reuse the existing resource group.</span></span> <span data-ttu-id="f37aa-151">Within a few minutes, you will receive a notification that the network security group was created.</span><span class="sxs-lookup"><span data-stu-id="f37aa-151">Within a few minutes, you will receive a notification that the network security group was created.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="f37aa-152">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f37aa-152">Clean up resources</span></span>

<span data-ttu-id="f37aa-153">When no longer needed, delete the resource group and network security group.</span><span class="sxs-lookup"><span data-stu-id="f37aa-153">When no longer needed, delete the resource group and network security group.</span></span> <span data-ttu-id="f37aa-154">To do so, type the name of the resource group you created into the search box at the top of the portal, and click on the name of the resource group.</span><span class="sxs-lookup"><span data-stu-id="f37aa-154">To do so, type the name of the resource group you created into the search box at the top of the portal, and click on the name of the resource group.</span></span> <span data-ttu-id="f37aa-155">In the section that is displayed, click the **Delete resource group** button, type the name of the resource group, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f37aa-155">In the section that is displayed, click the **Delete resource group** button, type the name of the resource group, and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f37aa-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="f37aa-156">Next steps</span></span>

<span data-ttu-id="f37aa-157">In this quick start, you performed an operation to generate an Activity Log event and then created an Activity Log alert to become notified when this operation occurs again in the future.</span><span class="sxs-lookup"><span data-stu-id="f37aa-157">In this quick start, you performed an operation to generate an Activity Log event and then created an Activity Log alert to become notified when this operation occurs again in the future.</span></span> <span data-ttu-id="f37aa-158">You then tested the alert by performing that operation again.</span><span class="sxs-lookup"><span data-stu-id="f37aa-158">You then tested the alert by performing that operation again.</span></span> <span data-ttu-id="f37aa-159">Azure makes available Activity Log events from the past 90 days.</span><span class="sxs-lookup"><span data-stu-id="f37aa-159">Azure makes available Activity Log events from the past 90 days.</span></span> <span data-ttu-id="f37aa-160">If you need to retain events longer than 90 days, try archiving your Activity Log data alongside your other monitoring data.</span><span class="sxs-lookup"><span data-stu-id="f37aa-160">If you need to retain events longer than 90 days, try archiving your Activity Log data alongside your other monitoring data.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f37aa-161">Archive monitoring data</span><span class="sxs-lookup"><span data-stu-id="f37aa-161">Archive monitoring data</span></span>](./monitor-tutorial-archive-monitoring-data.md)
