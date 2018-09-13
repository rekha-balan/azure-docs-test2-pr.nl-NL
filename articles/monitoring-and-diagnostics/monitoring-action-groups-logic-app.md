---
title: How to trigger complex actions with Azure Monitor alerts
description: Learn how to create a logic app action to process Azure Monitor alerts.
author: dkamstra
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 07/18/2018
ms.author: dukek
ms.component: alerts
ms.openlocfilehash: 034e708b79bbdf15d7fa628f388402998f49c0d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866967"
---
# <a name="how-to-trigger-complex-actions-with-azure-monitor-alerts"></a><span data-ttu-id="837fc-103">How to trigger complex actions with Azure Monitor alerts</span><span class="sxs-lookup"><span data-stu-id="837fc-103">How to trigger complex actions with Azure Monitor alerts</span></span>

<span data-ttu-id="837fc-104">This article shows you how to set up and trigger a logic app to create a conversation in Microsoft Teams when an alert fires.</span><span class="sxs-lookup"><span data-stu-id="837fc-104">This article shows you how to set up and trigger a logic app to create a conversation in Microsoft Teams when an alert fires.</span></span>

## <a name="overview"></a><span data-ttu-id="837fc-105">Overview</span><span class="sxs-lookup"><span data-stu-id="837fc-105">Overview</span></span>
<span data-ttu-id="837fc-106">When an Azure Monitor alert triggers, it calls an [action group](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="837fc-106">When an Azure Monitor alert triggers, it calls an [action group](monitoring-action-groups.md).</span></span> <span data-ttu-id="837fc-107">Action groups allow you to trigger one or more actions to notify others about an alert and also remediate it.</span><span class="sxs-lookup"><span data-stu-id="837fc-107">Action groups allow you to trigger one or more actions to notify others about an alert and also remediate it.</span></span>

<span data-ttu-id="837fc-108">The general process is:</span><span class="sxs-lookup"><span data-stu-id="837fc-108">The general process is:</span></span>

-   <span data-ttu-id="837fc-109">Create the logic app for the respective alert type.</span><span class="sxs-lookup"><span data-stu-id="837fc-109">Create the logic app for the respective alert type.</span></span>

-   <span data-ttu-id="837fc-110">Import the schema for the respective alert type into the logic app.</span><span class="sxs-lookup"><span data-stu-id="837fc-110">Import the schema for the respective alert type into the logic app.</span></span>

-   <span data-ttu-id="837fc-111">Define the logic app behavior.</span><span class="sxs-lookup"><span data-stu-id="837fc-111">Define the logic app behavior.</span></span>

-   <span data-ttu-id="837fc-112">Copy the HTTP endpoint of the logic app into an Azure action group.</span><span class="sxs-lookup"><span data-stu-id="837fc-112">Copy the HTTP endpoint of the logic app into an Azure action group.</span></span>

<span data-ttu-id="837fc-113">The process is similar if you want the logic app to perform a different action.</span><span class="sxs-lookup"><span data-stu-id="837fc-113">The process is similar if you want the logic app to perform a different action.</span></span>

## <a name="create-an-activity-log-alert-administrative"></a><span data-ttu-id="837fc-114">Create an activity log alert: Administrative</span><span class="sxs-lookup"><span data-stu-id="837fc-114">Create an activity log alert: Administrative</span></span>

1.  <span data-ttu-id="837fc-115">In the Azure portal, select **Create a resource** in the upper-left corner.</span><span class="sxs-lookup"><span data-stu-id="837fc-115">In the Azure portal, select **Create a resource** in the upper-left corner.</span></span>

2.  <span data-ttu-id="837fc-116">Search for and select **Logic App**, then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="837fc-116">Search for and select **Logic App**, then select **Create**.</span></span>

3.  <span data-ttu-id="837fc-117">Give your logic app a **Name**, choose a **Resource group**, and so on.</span><span class="sxs-lookup"><span data-stu-id="837fc-117">Give your logic app a **Name**, choose a **Resource group**, and so on.</span></span>

    <span data-ttu-id="837fc-118">![Create a logic app](media/monitoring-action-groups/create-logic-app-dialog.png "Create a logic app")</span><span class="sxs-lookup"><span data-stu-id="837fc-118">![Create a logic app](media/monitoring-action-groups/create-logic-app-dialog.png "Create a logic app")</span></span>

4.  <span data-ttu-id="837fc-119">Select **Create** to create the logic app.</span><span class="sxs-lookup"><span data-stu-id="837fc-119">Select **Create** to create the logic app.</span></span> <span data-ttu-id="837fc-120">A pop-up message indicates that the logic app is created.</span><span class="sxs-lookup"><span data-stu-id="837fc-120">A pop-up message indicates that the logic app is created.</span></span> <span data-ttu-id="837fc-121">Select **Launch Resource** to open the **Logic Apps Designer**.</span><span class="sxs-lookup"><span data-stu-id="837fc-121">Select **Launch Resource** to open the **Logic Apps Designer**.</span></span>

5.  <span data-ttu-id="837fc-122">Select the trigger: **When a HTTP request is received**.</span><span class="sxs-lookup"><span data-stu-id="837fc-122">Select the trigger: **When a HTTP request is received**.</span></span>

    <span data-ttu-id="837fc-123">![Logic app triggers](media/monitoring-action-groups/logic-app-triggers.png "Logic app triggers")</span><span class="sxs-lookup"><span data-stu-id="837fc-123">![Logic app triggers](media/monitoring-action-groups/logic-app-triggers.png "Logic app triggers")</span></span>

6.  <span data-ttu-id="837fc-124">Select **Edit** to change the HTTP request trigger.</span><span class="sxs-lookup"><span data-stu-id="837fc-124">Select **Edit** to change the HTTP request trigger.</span></span>

    <span data-ttu-id="837fc-125">![HTTP request triggers](media/monitoring-action-groups/http-request-trigger-shape.png "HTTP request triggers")</span><span class="sxs-lookup"><span data-stu-id="837fc-125">![HTTP request triggers](media/monitoring-action-groups/http-request-trigger-shape.png "HTTP request triggers")</span></span>

7.  <span data-ttu-id="837fc-126">Select **Use sample payload to generate schema**.</span><span class="sxs-lookup"><span data-stu-id="837fc-126">Select **Use sample payload to generate schema**.</span></span>

    <span data-ttu-id="837fc-127">![Use a sample payload](media/monitoring-action-groups/use-sample-payload-button.png "Use a sample payload")</span><span class="sxs-lookup"><span data-stu-id="837fc-127">![Use a sample payload](media/monitoring-action-groups/use-sample-payload-button.png "Use a sample payload")</span></span>

8.  <span data-ttu-id="837fc-128">Copy and paste the following sample schema into the dialog box:</span><span class="sxs-lookup"><span data-stu-id="837fc-128">Copy and paste the following sample schema into the dialog box:</span></span>

    ```json
        {
            "schemaId": "Microsoft.Insights/activityLogs",
            "data": {
                "status": "Activated",
                "context": {
                "activityLog": {
                    "authorization": {
                    "action": "microsoft.insights/activityLogAlerts/write",
                    "scope": "/subscriptions/…"
                    },
                    "channels": "Operation",
                    "claims": "…",
                    "caller": "logicappdemo@contoso.com",
                    "correlationId": "91ad2bac-1afa-4932-a2ce-2f8efd6765a3",
                    "description": "",
                    "eventSource": "Administrative",
                    "eventTimestamp": "2018-04-03T22:33:11.762469+00:00",
                    "eventDataId": "ec74c4a2-d7ae-48c3-a4d0-2684a1611ca0",
                    "level": "Informational",
                    "operationName": "microsoft.insights/activityLogAlerts/write",
                    "operationId": "61f59fc8-1442-4c74-9f5f-937392a9723c",
                    "resourceId": "/subscriptions/…",
                    "resourceGroupName": "LOGICAPP-DEMO",
                    "resourceProviderName": "microsoft.insights",
                    "status": "Succeeded",
                    "subStatus": "",
                    "subscriptionId": "…",
                    "submissionTimestamp": "2018-04-03T22:33:36.1068742+00:00",
                    "resourceType": "microsoft.insights/activityLogAlerts"
                }
                },
                "properties": {}
            }
        }
    ```

9. <span data-ttu-id="837fc-129">The **Logic App Designer** displays a pop-up window to remind you that the request sent to the logic app must set the **Content-Type** header to **application/json**.</span><span class="sxs-lookup"><span data-stu-id="837fc-129">The **Logic App Designer** displays a pop-up window to remind you that the request sent to the logic app must set the **Content-Type** header to **application/json**.</span></span> <span data-ttu-id="837fc-130">Close the pop-up window.</span><span class="sxs-lookup"><span data-stu-id="837fc-130">Close the pop-up window.</span></span> <span data-ttu-id="837fc-131">The Azure Monitor alert sets the header.</span><span class="sxs-lookup"><span data-stu-id="837fc-131">The Azure Monitor alert sets the header.</span></span>

    <span data-ttu-id="837fc-132">![Set the Content-Type header](media/monitoring-action-groups/content-type-header.png "Set the Content-Type header")</span><span class="sxs-lookup"><span data-stu-id="837fc-132">![Set the Content-Type header](media/monitoring-action-groups/content-type-header.png "Set the Content-Type header")</span></span>

10. <span data-ttu-id="837fc-133">Select **+** **New step** and then choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="837fc-133">Select **+** **New step** and then choose **Add an action**.</span></span>

    <span data-ttu-id="837fc-134">![Add an action](media/monitoring-action-groups/add-action.png "Add an action")</span><span class="sxs-lookup"><span data-stu-id="837fc-134">![Add an action](media/monitoring-action-groups/add-action.png "Add an action")</span></span>

11. <span data-ttu-id="837fc-135">Search for and select the Microsoft Teams connector.</span><span class="sxs-lookup"><span data-stu-id="837fc-135">Search for and select the Microsoft Teams connector.</span></span> <span data-ttu-id="837fc-136">Choose the **Microsoft Teams – Post message** action.</span><span class="sxs-lookup"><span data-stu-id="837fc-136">Choose the **Microsoft Teams – Post message** action.</span></span>

    <span data-ttu-id="837fc-137">![Microsoft Teams actions](media/monitoring-action-groups/microsoft-teams-actions.png "Microsoft Teams actions")</span><span class="sxs-lookup"><span data-stu-id="837fc-137">![Microsoft Teams actions](media/monitoring-action-groups/microsoft-teams-actions.png "Microsoft Teams actions")</span></span>

12. <span data-ttu-id="837fc-138">Configure the Microsoft Teams action.</span><span class="sxs-lookup"><span data-stu-id="837fc-138">Configure the Microsoft Teams action.</span></span> <span data-ttu-id="837fc-139">The **Logic Apps Designer** asks you to authenticate to your Office 365 account.</span><span class="sxs-lookup"><span data-stu-id="837fc-139">The **Logic Apps Designer** asks you to authenticate to your Office 365 account.</span></span> <span data-ttu-id="837fc-140">Choose the **Team ID** and **Channel ID** to send the message to.</span><span class="sxs-lookup"><span data-stu-id="837fc-140">Choose the **Team ID** and **Channel ID** to send the message to.</span></span>

13. <span data-ttu-id="837fc-141">Configure the message by using a combination of static text and references to the \<fields\> in the dynamic content.</span><span class="sxs-lookup"><span data-stu-id="837fc-141">Configure the message by using a combination of static text and references to the \<fields\> in the dynamic content.</span></span> <span data-ttu-id="837fc-142">Copy and paste the following text into the **Message** field:</span><span class="sxs-lookup"><span data-stu-id="837fc-142">Copy and paste the following text into the **Message** field:</span></span>

    ```text
      Activity Log Alert: <eventSource>
      operationName: <operationName>
      status: <status>
      resourceId: <resourceId>
    ```

    <span data-ttu-id="837fc-143">Then search for and replace the \<fields\> with dynamic content tags of the same name.</span><span class="sxs-lookup"><span data-stu-id="837fc-143">Then search for and replace the \<fields\> with dynamic content tags of the same name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="837fc-144">There are two dynamic fields that are named **status**.</span><span class="sxs-lookup"><span data-stu-id="837fc-144">There are two dynamic fields that are named **status**.</span></span> <span data-ttu-id="837fc-145">Add both of these fields to the message.</span><span class="sxs-lookup"><span data-stu-id="837fc-145">Add both of these fields to the message.</span></span> <span data-ttu-id="837fc-146">Use the field that's in the **activityLog** property bag and delete the other field.</span><span class="sxs-lookup"><span data-stu-id="837fc-146">Use the field that's in the **activityLog** property bag and delete the other field.</span></span> <span data-ttu-id="837fc-147">Hover your cursor over the **status** field to see the fully qualified field reference, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="837fc-147">Hover your cursor over the **status** field to see the fully qualified field reference, as shown in the following screenshot:</span></span>

    <span data-ttu-id="837fc-148">![Microsoft Teams action: Post a message](media/monitoring-action-groups/teams-action-post-message.png "Microsoft Teams action: Post a message")</span><span class="sxs-lookup"><span data-stu-id="837fc-148">![Microsoft Teams action: Post a message](media/monitoring-action-groups/teams-action-post-message.png "Microsoft Teams action: Post a message")</span></span>

14. <span data-ttu-id="837fc-149">At the top of the **Logic Apps Designer**, select **Save** to save your logic app.</span><span class="sxs-lookup"><span data-stu-id="837fc-149">At the top of the **Logic Apps Designer**, select **Save** to save your logic app.</span></span>

15. <span data-ttu-id="837fc-150">Open your existing action group and add an action to reference the logic app.</span><span class="sxs-lookup"><span data-stu-id="837fc-150">Open your existing action group and add an action to reference the logic app.</span></span> <span data-ttu-id="837fc-151">If you don’t have an existing action group, see [Create and manage action groups in the Azure portal](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-action-groups) to create one.</span><span class="sxs-lookup"><span data-stu-id="837fc-151">If you don’t have an existing action group, see [Create and manage action groups in the Azure portal](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-action-groups) to create one.</span></span> <span data-ttu-id="837fc-152">Don’t forget to save your changes.</span><span class="sxs-lookup"><span data-stu-id="837fc-152">Don’t forget to save your changes.</span></span>

    <span data-ttu-id="837fc-153">![Update the action group](media/monitoring-action-groups/update-action-group.png "Update the action group")</span><span class="sxs-lookup"><span data-stu-id="837fc-153">![Update the action group](media/monitoring-action-groups/update-action-group.png "Update the action group")</span></span>

<span data-ttu-id="837fc-154">The next time an alert calls your action group, your logic app is called.</span><span class="sxs-lookup"><span data-stu-id="837fc-154">The next time an alert calls your action group, your logic app is called.</span></span>

## <a name="create-a-service-health-alert"></a><span data-ttu-id="837fc-155">Create a service health alert</span><span class="sxs-lookup"><span data-stu-id="837fc-155">Create a service health alert</span></span>

<span data-ttu-id="837fc-156">Azure Service Health entries are part of the activity log.</span><span class="sxs-lookup"><span data-stu-id="837fc-156">Azure Service Health entries are part of the activity log.</span></span> <span data-ttu-id="837fc-157">The process for creating the alert is similar to [creating an activity log alert](#create-an-activity-log-alert-administrative), but with a few changes:</span><span class="sxs-lookup"><span data-stu-id="837fc-157">The process for creating the alert is similar to [creating an activity log alert](#create-an-activity-log-alert-administrative), but with a few changes:</span></span>

- <span data-ttu-id="837fc-158">Steps 1 through 7 are the same.</span><span class="sxs-lookup"><span data-stu-id="837fc-158">Steps 1 through 7 are the same.</span></span>
- <span data-ttu-id="837fc-159">For step 8, use the following sample schema for the HTTP request trigger:</span><span class="sxs-lookup"><span data-stu-id="837fc-159">For step 8, use the following sample schema for the HTTP request trigger:</span></span>

    ```json
    {
        "schemaId": "Microsoft.Insights/activityLogs",
        "data": {
            "status": "Activated",
            "context": {
                "activityLog": {
                    "channels": "Admin",
                    "correlationId": "e416ed3c-8874-4ec8-bc6b-54e3c92a24d4",
                    "description": "…",
                    "eventSource": "ServiceHealth",
                    "eventTimestamp": "2018-04-03T22:44:43.7467716+00:00",
                    "eventDataId": "9ce152f5-d435-ee31-2dce-104228486a6d",
                    "level": "Informational",
                    "operationName": "Microsoft.ServiceHealth/incident/action",
                    "operationId": "e416ed3c-8874-4ec8-bc6b-54e3c92a24d4",
                    "properties": {
                        "title": "…",
                        "service": "…",
                        "region": "Global",
                        "communication": "…",
                        "incidentType": "Incident",
                        "trackingId": "…",
                        "impactStartTime": "2018-03-22T21:40:00.0000000Z",
                        "impactMitigationTime": "2018-03-22T21:41:00.0000000Z",
                        "impactedServices": "[{"ImpactedRegions"}]",
                        "defaultLanguageTitle": "…",
                        "defaultLanguageContent": "…",
                        "stage": "Active",
                        "communicationId": "11000001466525",
                        "version": "0.1.1"
                    },
                    "status": "Active",
                    "subscriptionId": "…",
                    "submissionTimestamp": "2018-04-03T22:44:50.8013523+00:00"
                }
            },
            "properties": {}
        }
    }
    ```

-  <span data-ttu-id="837fc-160">Steps 9 and 10 are the same.</span><span class="sxs-lookup"><span data-stu-id="837fc-160">Steps 9 and 10 are the same.</span></span>
-  <span data-ttu-id="837fc-161">For steps 11 through 14, use the following process:</span><span class="sxs-lookup"><span data-stu-id="837fc-161">For steps 11 through 14, use the following process:</span></span>

   1. <span data-ttu-id="837fc-162">Select **+** **New step** and then choose **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="837fc-162">Select **+** **New step** and then choose **Add a condition**.</span></span> <span data-ttu-id="837fc-163">Set the following conditions so the logic app executes only when the input data matches the values below.</span><span class="sxs-lookup"><span data-stu-id="837fc-163">Set the following conditions so the logic app executes only when the input data matches the values below.</span></span>  <span data-ttu-id="837fc-164">When entering the version value into the text box, put quotes around it ("0.1.1") to make sure that it's evaluated as a string and not a numeric type.</span><span class="sxs-lookup"><span data-stu-id="837fc-164">When entering the version value into the text box, put quotes around it ("0.1.1") to make sure that it's evaluated as a string and not a numeric type.</span></span>  <span data-ttu-id="837fc-165">The system does not show the quotes if you return to the page, but the underlying code still maintains the string type.</span><span class="sxs-lookup"><span data-stu-id="837fc-165">The system does not show the quotes if you return to the page, but the underlying code still maintains the string type.</span></span>   
       - `schemaId == Microsoft.Insights/activityLogs`
       - `eventSource == ServiceHealth`
       - `version == "0.1.1"`

      <span data-ttu-id="837fc-166">!["Service Health payload condition"](media/monitoring-action-groups/service-health-payload-condition.png "Service Health payload condition")</span><span class="sxs-lookup"><span data-stu-id="837fc-166">!["Service Health payload condition"](media/monitoring-action-groups/service-health-payload-condition.png "Service Health payload condition")</span></span>

   1. <span data-ttu-id="837fc-167">In the **if true** condition, follow the instructions in steps 11 through 13 in [Create an activity log alert](#create-an-activity-log-alert-administrative) to add the Microsoft Teams action.</span><span class="sxs-lookup"><span data-stu-id="837fc-167">In the **if true** condition, follow the instructions in steps 11 through 13 in [Create an activity log alert](#create-an-activity-log-alert-administrative) to add the Microsoft Teams action.</span></span>

   1. <span data-ttu-id="837fc-168">Define the message by using a combination of HTML and dynamic content.</span><span class="sxs-lookup"><span data-stu-id="837fc-168">Define the message by using a combination of HTML and dynamic content.</span></span> <span data-ttu-id="837fc-169">Copy and paste the following content into the **Message** field.</span><span class="sxs-lookup"><span data-stu-id="837fc-169">Copy and paste the following content into the **Message** field.</span></span> <span data-ttu-id="837fc-170">Replace the `[incidentType]`, `[trackingID]`, `[title]`, and `[communication]` fields with dynamic content tags of the same name:</span><span class="sxs-lookup"><span data-stu-id="837fc-170">Replace the `[incidentType]`, `[trackingID]`, `[title]`, and `[communication]` fields with dynamic content tags of the same name:</span></span>

       ```html
       <p>
       <b>Alert Type:</b>&nbsp;<strong>[incidentType]</strong>&nbsp;
       <strong>Tracking ID:</strong>&nbsp;[trackingId]&nbsp;
       <strong>Title:</strong>&nbsp;[title]</p>
       <p>
       <a href="https://ms.portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/serviceIssues">For details, log in to the Azure Service Health dashboard.</a>
       </p>
       <p>[communication]</p>
       ```

       <span data-ttu-id="837fc-171">!["Service Health true condition post action"](media/monitoring-action-groups/service-health-true-condition-post-action.png "Service Health true condition post action")</span><span class="sxs-lookup"><span data-stu-id="837fc-171">!["Service Health true condition post action"](media/monitoring-action-groups/service-health-true-condition-post-action.png "Service Health true condition post action")</span></span>

   1. <span data-ttu-id="837fc-172">For the **If false** condition, provide a useful message:</span><span class="sxs-lookup"><span data-stu-id="837fc-172">For the **If false** condition, provide a useful message:</span></span>

       ```html
       <p><strong>Service Health Alert</strong></p>
       <p><b>Unrecognized alert schema</b></p>
       <p><a href="https://ms.portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/serviceIssues">For details, log in to the Azure Service Health dashboard.\</a></p>
       ```

       <span data-ttu-id="837fc-173">!["Service Health false condition post action"](media/monitoring-action-groups/service-health-false-condition-post-action.png "Service Health false condition post action")</span><span class="sxs-lookup"><span data-stu-id="837fc-173">!["Service Health false condition post action"](media/monitoring-action-groups/service-health-false-condition-post-action.png "Service Health false condition post action")</span></span>

- <span data-ttu-id="837fc-174">Step 15 is the same.</span><span class="sxs-lookup"><span data-stu-id="837fc-174">Step 15 is the same.</span></span> <span data-ttu-id="837fc-175">Follow the instructions to save your logic app and update your action group.</span><span class="sxs-lookup"><span data-stu-id="837fc-175">Follow the instructions to save your logic app and update your action group.</span></span>

## <a name="create-a-metric-alert"></a><span data-ttu-id="837fc-176">Create a metric alert</span><span class="sxs-lookup"><span data-stu-id="837fc-176">Create a metric alert</span></span>

<span data-ttu-id="837fc-177">The process for creating a metric alert is similar to [creating an activity log alert](#create-an-activity-log-alert-administrative), but with a few changes:</span><span class="sxs-lookup"><span data-stu-id="837fc-177">The process for creating a metric alert is similar to [creating an activity log alert](#create-an-activity-log-alert-administrative), but with a few changes:</span></span>

- <span data-ttu-id="837fc-178">Steps 1 through 7 are the same.</span><span class="sxs-lookup"><span data-stu-id="837fc-178">Steps 1 through 7 are the same.</span></span>
- <span data-ttu-id="837fc-179">For step 8, use the following sample schema for the HTTP request trigger:</span><span class="sxs-lookup"><span data-stu-id="837fc-179">For step 8, use the following sample schema for the HTTP request trigger:</span></span>

    ```json
    {
    "schemaId": "AzureMonitorMetricAlert",
    "data": {
        "version": "2.0",
        "status": "Activated",
        "context": {
        "timestamp": "2018-04-09T19:00:07.7461615Z",
        "id": "…",
        "name": "TEST-VM CPU Utilization",
        "description": "",
        "conditionType": "SingleResourceMultipleMetricCriteria",
        "condition": {
            "windowSize": "PT15M",
            "allOf": [
                {
                    "metricName": "Percentage CPU",
                    "dimensions": [
                    {
                        "name": "ResourceId",
                        "value": "d92fc5cb-06cf-4309-8c9a-538eea6a17a6"
                    }
                ],
                "operator": "GreaterThan",
                "threshold": "5",
                "timeAggregation": "PT15M",
                "metricValue": 1.0
            }
            ]
        },
        "subscriptionId": "…",
        "resourceGroupName": "TEST",
        "resourceName": "test-vm",
        "resourceType": "Microsoft.Compute/virtualMachines",
        "resourceId": "…",
        "portalLink": "…"
        },
        "properties": {}
    }
    }
    ```

- <span data-ttu-id="837fc-180">Steps 9 and 10 are the same.</span><span class="sxs-lookup"><span data-stu-id="837fc-180">Steps 9 and 10 are the same.</span></span>
- <span data-ttu-id="837fc-181">For steps 11 through 14, use the following process:</span><span class="sxs-lookup"><span data-stu-id="837fc-181">For steps 11 through 14, use the following process:</span></span>

   1. <span data-ttu-id="837fc-182">Select **+** **New step** and then choose **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="837fc-182">Select **+** **New step** and then choose **Add a condition**.</span></span> <span data-ttu-id="837fc-183">Set the following conditions so the logic app executes only when the input data matches these values below.</span><span class="sxs-lookup"><span data-stu-id="837fc-183">Set the following conditions so the logic app executes only when the input data matches these values below.</span></span> <span data-ttu-id="837fc-184">When entering the version value into the text box, put quotes around it ("2.0") to makes sure that it's evaluated as a string and not a numeric type.</span><span class="sxs-lookup"><span data-stu-id="837fc-184">When entering the version value into the text box, put quotes around it ("2.0") to makes sure that it's evaluated as a string and not a numeric type.</span></span>  <span data-ttu-id="837fc-185">The system does not show the quotes if you return to the page, but the underlying code still maintains the string type.</span><span class="sxs-lookup"><span data-stu-id="837fc-185">The system does not show the quotes if you return to the page, but the underlying code still maintains the string type.</span></span> 
       - `schemaId == AzureMonitorMetricAlert`
       - `version == "2.0"`
       
       <span data-ttu-id="837fc-186">!["Metric alert payload condition"](media/monitoring-action-groups/metric-alert-payload-condition.png "Metric alert payload condition")</span><span class="sxs-lookup"><span data-stu-id="837fc-186">!["Metric alert payload condition"](media/monitoring-action-groups/metric-alert-payload-condition.png "Metric alert payload condition")</span></span>

   1. <span data-ttu-id="837fc-187">In the **if true** condition, add a **For each** loop and the Microsoft Teams action.</span><span class="sxs-lookup"><span data-stu-id="837fc-187">In the **if true** condition, add a **For each** loop and the Microsoft Teams action.</span></span> <span data-ttu-id="837fc-188">Define the message by using a combination of HTML and dynamic content.</span><span class="sxs-lookup"><span data-stu-id="837fc-188">Define the message by using a combination of HTML and dynamic content.</span></span>

       <span data-ttu-id="837fc-189">!["Metric alert true condition post action"](media/monitoring-action-groups/metric-alert-true-condition-post-action.png "Metric alert true condition post action")</span><span class="sxs-lookup"><span data-stu-id="837fc-189">!["Metric alert true condition post action"](media/monitoring-action-groups/metric-alert-true-condition-post-action.png "Metric alert true condition post action")</span></span>

   1. <span data-ttu-id="837fc-190">In the **If false** condition, define a Microsoft Teams action to communicate that the metric alert doesn’t match the expectations of the logic app.</span><span class="sxs-lookup"><span data-stu-id="837fc-190">In the **If false** condition, define a Microsoft Teams action to communicate that the metric alert doesn’t match the expectations of the logic app.</span></span> <span data-ttu-id="837fc-191">Include the JSON payload.</span><span class="sxs-lookup"><span data-stu-id="837fc-191">Include the JSON payload.</span></span> <span data-ttu-id="837fc-192">Notice how to reference the `triggerBody` dynamic content in the `json()` expression.</span><span class="sxs-lookup"><span data-stu-id="837fc-192">Notice how to reference the `triggerBody` dynamic content in the `json()` expression.</span></span>

       <span data-ttu-id="837fc-193">!["Metric alert false condition post action"](media/monitoring-action-groups/metric-alert-false-condition-post-action.png "Metric alert false condition post action")</span><span class="sxs-lookup"><span data-stu-id="837fc-193">!["Metric alert false condition post action"](media/monitoring-action-groups/metric-alert-false-condition-post-action.png "Metric alert false condition post action")</span></span>

- <span data-ttu-id="837fc-194">Step 15 is the same.</span><span class="sxs-lookup"><span data-stu-id="837fc-194">Step 15 is the same.</span></span> <span data-ttu-id="837fc-195">Follow the instructions to save your logic app and update your action group.</span><span class="sxs-lookup"><span data-stu-id="837fc-195">Follow the instructions to save your logic app and update your action group.</span></span>

## <a name="calling-other-applications-besides-microsoft-teams"></a><span data-ttu-id="837fc-196">Calling other applications besides Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="837fc-196">Calling other applications besides Microsoft Teams</span></span>
<span data-ttu-id="837fc-197">Logic Apps has a number of different connectors that allow you to trigger actions in a wide range of applications and databases.</span><span class="sxs-lookup"><span data-stu-id="837fc-197">Logic Apps has a number of different connectors that allow you to trigger actions in a wide range of applications and databases.</span></span> <span data-ttu-id="837fc-198">Slack, SQL Server, Oracle, Salesforce, are just some examples.</span><span class="sxs-lookup"><span data-stu-id="837fc-198">Slack, SQL Server, Oracle, Salesforce, are just some examples.</span></span> <span data-ttu-id="837fc-199">For more information about connectors, see [Logic App connectors](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="837fc-199">For more information about connectors, see [Logic App connectors](../connectors/apis-list.md).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="837fc-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="837fc-200">Next steps</span></span>
* <span data-ttu-id="837fc-201">Get an [overview of Azure activity log alerts](monitoring-overview-alerts.md) and learn how to receive alerts.</span><span class="sxs-lookup"><span data-stu-id="837fc-201">Get an [overview of Azure activity log alerts](monitoring-overview-alerts.md) and learn how to receive alerts.</span></span>  
* <span data-ttu-id="837fc-202">Learn how to [configure alerts when an Azure Service Health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="837fc-202">Learn how to [configure alerts when an Azure Service Health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
* <span data-ttu-id="837fc-203">Learn more about [action groups](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="837fc-203">Learn more about [action groups](monitoring-action-groups.md).</span></span>
