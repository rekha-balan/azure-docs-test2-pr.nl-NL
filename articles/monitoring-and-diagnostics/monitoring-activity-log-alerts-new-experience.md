---
title: Use activity log alerts in the new Azure Monitor alerts experience
description: How to create activity log alerts from Alerts (Preview) tab under Azure Monitor. This article details the new user experience for this feature.
author: jyothirmaisuri
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 02/05/2018
ms.author: v-jysur
ms.component: alerts
ms.openlocfilehash: 10cd4e2ea14ab66a44ba2123e025b3d1b91f385c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969510"
---
# <a name="create-activity-log-alerts-using-the-new-alerts-experience"></a><span data-ttu-id="ddeef-104">Create activity log alerts using the new alerts experience</span><span class="sxs-lookup"><span data-stu-id="ddeef-104">Create activity log alerts using the new alerts experience</span></span>

<span data-ttu-id="ddeef-105">Activity log alerts are the alerts that get activated when a new activity log event occurs that matches the conditions specified in the alert.</span><span class="sxs-lookup"><span data-stu-id="ddeef-105">Activity log alerts are the alerts that get activated when a new activity log event occurs that matches the conditions specified in the alert.</span></span>

<span data-ttu-id="ddeef-106">These alerts are for Azure resources, can be created by using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="ddeef-106">These alerts are for Azure resources, can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="ddeef-107">They also can be created, updated, or deleted in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ddeef-107">They also can be created, updated, or deleted in the Azure portal.</span></span> <span data-ttu-id="ddeef-108">This article introduces the concepts behind activity log alerts.</span><span class="sxs-lookup"><span data-stu-id="ddeef-108">This article introduces the concepts behind activity log alerts.</span></span> <span data-ttu-id="ddeef-109">It then shows you how to use the Azure portal to set up an alert on activity log events using the new experience in [Azure Alerts](monitoring-overview-unified-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ddeef-109">It then shows you how to use the Azure portal to set up an alert on activity log events using the new experience in [Azure Alerts](monitoring-overview-unified-alerts.md).</span></span>

<span data-ttu-id="ddeef-110">Typically, you create activity log alerts to receive notifications when specific changes occur on resources in your Azure subscription, often scoped to particular resource groups or resource.</span><span class="sxs-lookup"><span data-stu-id="ddeef-110">Typically, you create activity log alerts to receive notifications when specific changes occur on resources in your Azure subscription, often scoped to particular resource groups or resource.</span></span> <span data-ttu-id="ddeef-111">For example, you might want to be notified when any virtual machine in (sample resource group) **myProductionResourceGroup** is deleted, or you might want to get notified if any new roles are assigned to a user in your subscription.</span><span class="sxs-lookup"><span data-stu-id="ddeef-111">For example, you might want to be notified when any virtual machine in (sample resource group) **myProductionResourceGroup** is deleted, or you might want to get notified if any new roles are assigned to a user in your subscription.</span></span>

<span data-ttu-id="ddeef-112">You can configure an activity log alert based on any top-level property in the JSON object for an activity log event.</span><span class="sxs-lookup"><span data-stu-id="ddeef-112">You can configure an activity log alert based on any top-level property in the JSON object for an activity log event.</span></span> <span data-ttu-id="ddeef-113">However, the portal shows the most common options as detailed in the following sections:</span><span class="sxs-lookup"><span data-stu-id="ddeef-113">However, the portal shows the most common options as detailed in the following sections:</span></span>

>[!NOTE]

> <span data-ttu-id="ddeef-114">When the category is "administrative", You must specify at least one of the preceding criteria in your alert.</span><span class="sxs-lookup"><span data-stu-id="ddeef-114">When the category is "administrative", You must specify at least one of the preceding criteria in your alert.</span></span> <span data-ttu-id="ddeef-115">You may not create an alert that activates every time an event is created in the activity logs.</span><span class="sxs-lookup"><span data-stu-id="ddeef-115">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
>

<span data-ttu-id="ddeef-116">When an activity log alert is activated, it uses an action group to generate actions or notifications.</span><span class="sxs-lookup"><span data-stu-id="ddeef-116">When an activity log alert is activated, it uses an action group to generate actions or notifications.</span></span> <span data-ttu-id="ddeef-117">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span><span class="sxs-lookup"><span data-stu-id="ddeef-117">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="ddeef-118">The receivers can be referenced from multiple alerts to centralize and group your notification channels.</span><span class="sxs-lookup"><span data-stu-id="ddeef-118">The receivers can be referenced from multiple alerts to centralize and group your notification channels.</span></span> <span data-ttu-id="ddeef-119">When you define your activity log alert, you have two options.</span><span class="sxs-lookup"><span data-stu-id="ddeef-119">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="ddeef-120">You can:</span><span class="sxs-lookup"><span data-stu-id="ddeef-120">You can:</span></span>

* <span data-ttu-id="ddeef-121">Use an existing action group in your activity log alert.</span><span class="sxs-lookup"><span data-stu-id="ddeef-121">Use an existing action group in your activity log alert.</span></span>
* <span data-ttu-id="ddeef-122">Create a new action group.</span><span class="sxs-lookup"><span data-stu-id="ddeef-122">Create a new action group.</span></span>

<span data-ttu-id="ddeef-123">To learn more about action groups, see [Create and manage action groups in the Azure portal](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="ddeef-123">To learn more about action groups, see [Create and manage action groups in the Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="ddeef-124">To learn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="ddeef-124">To learn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>


## <a name="whats-new-in-alerts-for-activity-logs"></a><span data-ttu-id="ddeef-125">What's new in alerts for activity logs?</span><span class="sxs-lookup"><span data-stu-id="ddeef-125">What's new in alerts for activity logs?</span></span>

<span data-ttu-id="ddeef-126">[Azure Alerts](monitoring-overview-unified-alerts.md) now provides enhanced user experience for Activity log alerts.</span><span class="sxs-lookup"><span data-stu-id="ddeef-126">[Azure Alerts](monitoring-overview-unified-alerts.md) now provides enhanced user experience for Activity log alerts.</span></span> <span data-ttu-id="ddeef-127">With the [enhanced user experience for Alerts](monitoring-overview-unified-alerts.md), you can now:</span><span class="sxs-lookup"><span data-stu-id="ddeef-127">With the [enhanced user experience for Alerts](monitoring-overview-unified-alerts.md), you can now:</span></span>

- <span data-ttu-id="ddeef-128">[Create](#create-an-alert-rule-for-an-activity-log) and [manage](#view-and-manage-activity-log-alert-rules) the Activity log alert rules, from **Monitor** > **Alerts** blade.</span><span class="sxs-lookup"><span data-stu-id="ddeef-128">[Create](#create-an-alert-rule-for-an-activity-log) and [manage](#view-and-manage-activity-log-alert-rules) the Activity log alert rules, from **Monitor** > **Alerts** blade.</span></span> <span data-ttu-id="ddeef-129">Learn more about [Activity logs](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ddeef-129">Learn more about [Activity logs](monitoring-overview-activity-logs.md).</span></span>

- <span data-ttu-id="ddeef-130">**New options for Alerts Target**:  While creating a new activity log alert rule, you can now select a target resource or a resource group or a subscription.</span><span class="sxs-lookup"><span data-stu-id="ddeef-130">**New options for Alerts Target**:  While creating a new activity log alert rule, you can now select a target resource or a resource group or a subscription.</span></span>


## <a name="create-an-alert-rule-for-an-activity-log"></a><span data-ttu-id="ddeef-131">Create an alert rule for an activity log</span><span class="sxs-lookup"><span data-stu-id="ddeef-131">Create an alert rule for an activity log</span></span>

> [!NOTE]

>  <span data-ttu-id="ddeef-132">While creating the alert rules, ensure the following:</span><span class="sxs-lookup"><span data-stu-id="ddeef-132">While creating the alert rules, ensure the following:</span></span>

> - <span data-ttu-id="ddeef-133">Subscription in the scope is not different from the subscription where the alert is created.</span><span class="sxs-lookup"><span data-stu-id="ddeef-133">Subscription in the scope is not different from the subscription where the alert is created.</span></span>
- <span data-ttu-id="ddeef-134">Criteria must be level/status/ caller/ resource group/ resource id/ resource type/ event category on which the alert is configured.</span><span class="sxs-lookup"><span data-stu-id="ddeef-134">Criteria must be level/status/ caller/ resource group/ resource id/ resource type/ event category on which the alert is configured.</span></span>
- <span data-ttu-id="ddeef-135">There is no  “anyOf” condition or nested conditions in the alert configuration JSON (basically, only one allOf is allowed with no further allOf/anyOf).</span><span class="sxs-lookup"><span data-stu-id="ddeef-135">There is no  “anyOf” condition or nested conditions in the alert configuration JSON (basically, only one allOf is allowed with no further allOf/anyOf).</span></span>


<span data-ttu-id="ddeef-136">Use the following procedure:</span><span class="sxs-lookup"><span data-stu-id="ddeef-136">Use the following procedure:</span></span>

1. <span data-ttu-id="ddeef-137">From Azure portal, select **Monitor** > **Alerts**</span><span class="sxs-lookup"><span data-stu-id="ddeef-137">From Azure portal, select **Monitor** > **Alerts**</span></span>
2. <span data-ttu-id="ddeef-138">Click **New Alert Rule** at the top of the **Alerts** window.</span><span class="sxs-lookup"><span data-stu-id="ddeef-138">Click **New Alert Rule** at the top of the **Alerts** window.</span></span>

     ![new alert rule](./media/monitoring-activity-log-alerts-new-experience/create-new-alert-rule.png)

     <span data-ttu-id="ddeef-140">The **Create rule** window appears.</span><span class="sxs-lookup"><span data-stu-id="ddeef-140">The **Create rule** window appears.</span></span>

      ![new alert rule options](./media/monitoring-activity-log-alerts-new-experience/create-new-alert-rule-options.png)

3. <span data-ttu-id="ddeef-142">**Under Define Alert condition,** provide the following information, and click **Done**.</span><span class="sxs-lookup"><span data-stu-id="ddeef-142">**Under Define Alert condition,** provide the following information, and click **Done**.</span></span>

    - <span data-ttu-id="ddeef-143">**Alert Target:** To view and select the target for the new alert, use **Filter by subscription** / **Filter by resource type** and select the resource or resource group from the list displayed.</span><span class="sxs-lookup"><span data-stu-id="ddeef-143">**Alert Target:** To view and select the target for the new alert, use **Filter by subscription** / **Filter by resource type** and select the resource or resource group from the list displayed.</span></span>

    > [!NOTE]

    > <span data-ttu-id="ddeef-144">you can select a resource, resource group, or an entire subscription.</span><span class="sxs-lookup"><span data-stu-id="ddeef-144">you can select a resource, resource group, or an entire subscription.</span></span>

    <span data-ttu-id="ddeef-145">**Alert target sample view**</span><span class="sxs-lookup"><span data-stu-id="ddeef-145">**Alert target sample view**</span></span>

     ![Select Target](./media/monitoring-activity-log-alerts-new-experience/select-target.png)

    - <span data-ttu-id="ddeef-147">Under **Target Criteria**, click **add criteria** select the signal type as **Activity log**.</span><span class="sxs-lookup"><span data-stu-id="ddeef-147">Under **Target Criteria**, click **add criteria** select the signal type as **Activity log**.</span></span>

    - <span data-ttu-id="ddeef-148">Select the signal from the list displayed.</span><span class="sxs-lookup"><span data-stu-id="ddeef-148">Select the signal from the list displayed.</span></span>

    <span data-ttu-id="ddeef-149">You can select the log history timeline and the corresponding alert logic for this target signal:</span><span class="sxs-lookup"><span data-stu-id="ddeef-149">You can select the log history timeline and the corresponding alert logic for this target signal:</span></span>

    <span data-ttu-id="ddeef-150">**Add criteria screen**</span><span class="sxs-lookup"><span data-stu-id="ddeef-150">**Add criteria screen**</span></span>

    ![add criteria](./media/monitoring-activity-log-alerts-new-experience/add-criteria.png)

    <span data-ttu-id="ddeef-152">**History time**: Over the last 6/12/24 hours, Over the last Week.</span><span class="sxs-lookup"><span data-stu-id="ddeef-152">**History time**: Over the last 6/12/24 hours, Over the last Week.</span></span>

    <span data-ttu-id="ddeef-153">**Alert logic**:</span><span class="sxs-lookup"><span data-stu-id="ddeef-153">**Alert logic**:</span></span>

     - <span data-ttu-id="ddeef-154">**Event Level**- The severity level of the event.**Verbose,Informational, Warning, Error**, or **Critical**.</span><span class="sxs-lookup"><span data-stu-id="ddeef-154">**Event Level**- The severity level of the event.**Verbose,Informational, Warning, Error**, or **Critical**.</span></span>
     - <span data-ttu-id="ddeef-155">**Status**: The status of the event.**Started, Failed**, or **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="ddeef-155">**Status**: The status of the event.**Started, Failed**, or **Succeeded**.</span></span>
     - <span data-ttu-id="ddeef-156">**Event initiated by**: Also known as the caller; The email address or Azure Active Directory identifier of the user who performed the operation.</span><span class="sxs-lookup"><span data-stu-id="ddeef-156">**Event initiated by**: Also known as the caller; The email address or Azure Active Directory identifier of the user who performed the operation.</span></span>

        <span data-ttu-id="ddeef-157">**Sample signal graph with alert logic applied** :</span><span class="sxs-lookup"><span data-stu-id="ddeef-157">**Sample signal graph with alert logic applied** :</span></span>

        ![ <span data-ttu-id="ddeef-158">criteria selected</span><span class="sxs-lookup"><span data-stu-id="ddeef-158">criteria selected</span></span>](./media/monitoring-activity-log-alerts-new-experience/criteria-selected.png)

4. <span data-ttu-id="ddeef-159">Under **define alert rules details**, provide the following details:</span><span class="sxs-lookup"><span data-stu-id="ddeef-159">Under **define alert rules details**, provide the following details:</span></span>

    - <span data-ttu-id="ddeef-160">**Alert rule name** – Name for the new alert rule</span><span class="sxs-lookup"><span data-stu-id="ddeef-160">**Alert rule name** – Name for the new alert rule</span></span>
    - <span data-ttu-id="ddeef-161">**Description** – Description for the new alert rule</span><span class="sxs-lookup"><span data-stu-id="ddeef-161">**Description** – Description for the new alert rule</span></span>
    - <span data-ttu-id="ddeef-162">**Save alert to resource group** – Select the Resource group, where you want to save this new rule.</span><span class="sxs-lookup"><span data-stu-id="ddeef-162">**Save alert to resource group** – Select the Resource group, where you want to save this new rule.</span></span>

5. <span data-ttu-id="ddeef-163">Under **Action group**, from the drop-down menu, specify the action group that you want to assign to this new alert rule.</span><span class="sxs-lookup"><span data-stu-id="ddeef-163">Under **Action group**, from the drop-down menu, specify the action group that you want to assign to this new alert rule.</span></span> <span data-ttu-id="ddeef-164">Alternatively, [create a new action group](monitoring-action-groups.md) and assign to the new rule.</span><span class="sxs-lookup"><span data-stu-id="ddeef-164">Alternatively, [create a new action group](monitoring-action-groups.md) and assign to the new rule.</span></span> <span data-ttu-id="ddeef-165">To create a new group, click **+ New group**.</span><span class="sxs-lookup"><span data-stu-id="ddeef-165">To create a new group, click **+ New group**.</span></span>

6. <span data-ttu-id="ddeef-166">To enable the rules after you create it, click **Yes** for **Enable rule upon creation** option.</span><span class="sxs-lookup"><span data-stu-id="ddeef-166">To enable the rules after you create it, click **Yes** for **Enable rule upon creation** option.</span></span>
7. <span data-ttu-id="ddeef-167">Click **Create alert rule**.</span><span class="sxs-lookup"><span data-stu-id="ddeef-167">Click **Create alert rule**.</span></span>

    <span data-ttu-id="ddeef-168">The new alert rule for the activity log is created and a confirmation message appears at the top right of the window.</span><span class="sxs-lookup"><span data-stu-id="ddeef-168">The new alert rule for the activity log is created and a confirmation message appears at the top right of the window.</span></span>

    ![ <span data-ttu-id="ddeef-169">alert rule created</span><span class="sxs-lookup"><span data-stu-id="ddeef-169">alert rule created</span></span>](./media/monitoring-activity-log-alerts-new-experience/alert-created.png)

    <span data-ttu-id="ddeef-170">You can enable, disable, edit or delete a rule.</span><span class="sxs-lookup"><span data-stu-id="ddeef-170">You can enable, disable, edit or delete a rule.</span></span> <span data-ttu-id="ddeef-171">[Learn more](#view-and-manage-activity-log-alert-rules) about managing activity log rules.</span><span class="sxs-lookup"><span data-stu-id="ddeef-171">[Learn more](#view-and-manage-activity-log-alert-rules) about managing activity log rules.</span></span>

## <a name="view-and-manage-activity-log-alert-rules"></a><span data-ttu-id="ddeef-172">View and manage activity log alert rules</span><span class="sxs-lookup"><span data-stu-id="ddeef-172">View and manage activity log alert rules</span></span>

1. <span data-ttu-id="ddeef-173">From Azure portal, click **Monitor** > **Alerts** and click **Manage rules** at the top left of the window.</span><span class="sxs-lookup"><span data-stu-id="ddeef-173">From Azure portal, click **Monitor** > **Alerts** and click **Manage rules** at the top left of the window.</span></span>

    ![ <span data-ttu-id="ddeef-174">manage alert rules</span><span class="sxs-lookup"><span data-stu-id="ddeef-174">manage alert rules</span></span>](./media/monitoring-activity-log-alerts-new-experience/manage-alert-rules.png)

    <span data-ttu-id="ddeef-175">The list of available rules appears.</span><span class="sxs-lookup"><span data-stu-id="ddeef-175">The list of available rules appears.</span></span>

2. <span data-ttu-id="ddeef-176">Search the Activity log rule to modify.</span><span class="sxs-lookup"><span data-stu-id="ddeef-176">Search the Activity log rule to modify.</span></span>

    ![ <span data-ttu-id="ddeef-177">search activity log alert rules</span><span class="sxs-lookup"><span data-stu-id="ddeef-177">search activity log alert rules</span></span>](./media/monitoring-activity-log-alerts-new-experience/searth-activity-log-rule-to-edit.png)

    <span data-ttu-id="ddeef-178">You can use the available filters - **Subscription**, **Resource group**, or **Resource** to find the activity rule that you want to edit.</span><span class="sxs-lookup"><span data-stu-id="ddeef-178">You can use the available filters - **Subscription**, **Resource group**, or **Resource** to find the activity rule that you want to edit.</span></span>

    > [!NOTE]

    > <span data-ttu-id="ddeef-179">You can only edit **Description** , **Target criteria** and **Action groups**.</span><span class="sxs-lookup"><span data-stu-id="ddeef-179">You can only edit **Description** , **Target criteria** and **Action groups**.</span></span>

3.  <span data-ttu-id="ddeef-180">Select the rule and double-click to edit the rule options.</span><span class="sxs-lookup"><span data-stu-id="ddeef-180">Select the rule and double-click to edit the rule options.</span></span> <span data-ttu-id="ddeef-181">Make the required changes and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ddeef-181">Make the required changes and then click **Save**.</span></span>

    ![ <span data-ttu-id="ddeef-182">manage alert rules</span><span class="sxs-lookup"><span data-stu-id="ddeef-182">manage alert rules</span></span>](./media/monitoring-activity-log-alerts-new-experience/activity-log-rule-edit-page.png)

4.  <span data-ttu-id="ddeef-183">You can disable, enable, or delete a rule.</span><span class="sxs-lookup"><span data-stu-id="ddeef-183">You can disable, enable, or delete a rule.</span></span> <span data-ttu-id="ddeef-184">Select the appropriate option at the top of the window, after selecting the rule as detailed in step 2.</span><span class="sxs-lookup"><span data-stu-id="ddeef-184">Select the appropriate option at the top of the window, after selecting the rule as detailed in step 2.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ddeef-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="ddeef-185">Next steps</span></span>

- [<span data-ttu-id="ddeef-186">Archive Activity log alerts</span><span class="sxs-lookup"><span data-stu-id="ddeef-186">Archive Activity log alerts</span></span>](monitoring-archive-activity-log.md)
- [<span data-ttu-id="ddeef-187">Stream Activity logs to Event hubs</span><span class="sxs-lookup"><span data-stu-id="ddeef-187">Stream Activity logs to Event hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
- [<span data-ttu-id="ddeef-188">Migrate to Activity logs</span><span class="sxs-lookup"><span data-stu-id="ddeef-188">Migrate to Activity logs</span></span>](monitoring-migrate-management-alerts.md)
