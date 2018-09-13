---
title: Enable logging & alerts, check the run history, track inputs and outputs - Azure Logic Apps | Microsoft Docs
description: Monitor the status of your logic app workflows using logging, tracking, and viewing the history and diagnostics
author: jeffhollan
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: jehollan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14b0c017dd5ce5c7cc3e77a15f1e7ad64497838f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552508"
---
# <a name="check-the-performance-and-start-diagnostic-logging-and-alerts-of-your-workflows-in-logic-apps"></a><span data-ttu-id="d3b05-103">Check the performance, and start diagnostic logging and alerts of your workflows in logic apps</span><span class="sxs-lookup"><span data-stu-id="d3b05-103">Check the performance, and start diagnostic logging and alerts of your workflows in logic apps</span></span>
<span data-ttu-id="d3b05-104">After you [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can see the full history of its execution in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d3b05-104">After you [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can see the full history of its execution in the Azure portal.</span></span>  <span data-ttu-id="d3b05-105">You can also set up services like Azure Diagnostics and Azure Alerts to monitor events real-time, and alert you for events like "when more than 5 runs fail within an hour."</span><span class="sxs-lookup"><span data-stu-id="d3b05-105">You can also set up services like Azure Diagnostics and Azure Alerts to monitor events real-time, and alert you for events like "when more than 5 runs fail within an hour."</span></span>

## <a name="monitor-in-the-azure-portal"></a><span data-ttu-id="d3b05-106">Monitor in the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d3b05-106">Monitor in the Azure Portal</span></span>
<span data-ttu-id="d3b05-107">To view the history, select **Browse**, and select **Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="d3b05-107">To view the history, select **Browse**, and select **Logic Apps**.</span></span> <span data-ttu-id="d3b05-108">A list of all logic apps in your subscription is displayed.</span><span class="sxs-lookup"><span data-stu-id="d3b05-108">A list of all logic apps in your subscription is displayed.</span></span>  <span data-ttu-id="d3b05-109">Select the logic app you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="d3b05-109">Select the logic app you want to monitor.</span></span>  <span data-ttu-id="d3b05-110">You will see a list of all actions and triggers that have occurred for this logic app.</span><span class="sxs-lookup"><span data-stu-id="d3b05-110">You will see a list of all actions and triggers that have occurred for this logic app.</span></span>

![Overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-your-logic-apps/overview.png)

<span data-ttu-id="d3b05-112">There are a few sections on this blade that are helpful:</span><span class="sxs-lookup"><span data-stu-id="d3b05-112">There are a few sections on this blade that are helpful:</span></span>

* <span data-ttu-id="d3b05-113">**Summary** lists **All runs** and the **Trigger History**</span><span class="sxs-lookup"><span data-stu-id="d3b05-113">**Summary** lists **All runs** and the **Trigger History**</span></span>
  * <span data-ttu-id="d3b05-114">**All runs** list the latest logic app runs.</span><span class="sxs-lookup"><span data-stu-id="d3b05-114">**All runs** list the latest logic app runs.</span></span>  <span data-ttu-id="d3b05-115">You can click any row for details on the run, or click on the tile to list more runs.</span><span class="sxs-lookup"><span data-stu-id="d3b05-115">You can click any row for details on the run, or click on the tile to list more runs.</span></span>
  * <span data-ttu-id="d3b05-116">**Trigger History** lists all the trigger activity for this logic app.</span><span class="sxs-lookup"><span data-stu-id="d3b05-116">**Trigger History** lists all the trigger activity for this logic app.</span></span>  <span data-ttu-id="d3b05-117">Trigger activity could be a "Skipped" check for new data (e.g. looking to see if a new file was added to FTP), "Succeeded" meaning data was returned to fire a logic app, or "Failed" corresponding an error in configuration.</span><span class="sxs-lookup"><span data-stu-id="d3b05-117">Trigger activity could be a "Skipped" check for new data (e.g. looking to see if a new file was added to FTP), "Succeeded" meaning data was returned to fire a logic app, or "Failed" corresponding an error in configuration.</span></span>
* <span data-ttu-id="d3b05-118">**Diagnostics** allows you to view runtime details and events, and subscribe to [Azure Alerts](#adding-azure-alerts)</span><span class="sxs-lookup"><span data-stu-id="d3b05-118">**Diagnostics** allows you to view runtime details and events, and subscribe to [Azure Alerts](#adding-azure-alerts)</span></span>

> [!NOTE]
> <span data-ttu-id="d3b05-119">All runtime details and events are encrypted at rest within the Logic App service.</span><span class="sxs-lookup"><span data-stu-id="d3b05-119">All runtime details and events are encrypted at rest within the Logic App service.</span></span> <span data-ttu-id="d3b05-120">They are only decrypted upon a view request from a user.</span><span class="sxs-lookup"><span data-stu-id="d3b05-120">They are only decrypted upon a view request from a user.</span></span> <span data-ttu-id="d3b05-121">Access to these events can also be controlled by Azure Role-Based Access Control (RBAC).</span><span class="sxs-lookup"><span data-stu-id="d3b05-121">Access to these events can also be controlled by Azure Role-Based Access Control (RBAC).</span></span>
> 
> 

### <a name="view-the-run-details"></a><span data-ttu-id="d3b05-122">View the run details</span><span class="sxs-lookup"><span data-stu-id="d3b05-122">View the run details</span></span>
<span data-ttu-id="d3b05-123">This list of runs shows the **Status**, the **Start Time**, and the **Duration** of the particular run.</span><span class="sxs-lookup"><span data-stu-id="d3b05-123">This list of runs shows the **Status**, the **Start Time**, and the **Duration** of the particular run.</span></span> <span data-ttu-id="d3b05-124">Select any row to see details on that run.</span><span class="sxs-lookup"><span data-stu-id="d3b05-124">Select any row to see details on that run.</span></span>

<span data-ttu-id="d3b05-125">The monitoring view shows you each step of the run, the inputs and outputs, and any error messages that may have occurre.</span><span class="sxs-lookup"><span data-stu-id="d3b05-125">The monitoring view shows you each step of the run, the inputs and outputs, and any error messages that may have occurre.</span></span>

![Run and Actions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-your-logic-apps/monitor-view.png)

<span data-ttu-id="d3b05-127">If you need any additional details like the run **Correlation ID** (that can be used for the REST API), you can click the **Run Details** button.</span><span class="sxs-lookup"><span data-stu-id="d3b05-127">If you need any additional details like the run **Correlation ID** (that can be used for the REST API), you can click the **Run Details** button.</span></span>  <span data-ttu-id="d3b05-128">This includes all steps, status, and inputs/outputs for the run.</span><span class="sxs-lookup"><span data-stu-id="d3b05-128">This includes all steps, status, and inputs/outputs for the run.</span></span>

## <a name="azure-diagnostics-and-alerts"></a><span data-ttu-id="d3b05-129">Azure Diagnostics and alerts</span><span class="sxs-lookup"><span data-stu-id="d3b05-129">Azure Diagnostics and alerts</span></span>
<span data-ttu-id="d3b05-130">In addition to the details provided by the Azure Portal and REST API above, you can configure your logic app to use Azure Diagnostics for more rich details and debugging.</span><span class="sxs-lookup"><span data-stu-id="d3b05-130">In addition to the details provided by the Azure Portal and REST API above, you can configure your logic app to use Azure Diagnostics for more rich details and debugging.</span></span>

1. <span data-ttu-id="d3b05-131">Click the **Diagnostics** section of the logic app blade</span><span class="sxs-lookup"><span data-stu-id="d3b05-131">Click the **Diagnostics** section of the logic app blade</span></span>
2. <span data-ttu-id="d3b05-132">Click to configure the **Diagnostic Settings**</span><span class="sxs-lookup"><span data-stu-id="d3b05-132">Click to configure the **Diagnostic Settings**</span></span>
3. <span data-ttu-id="d3b05-133">Configure an Event Hub or Storage Account to emit data to</span><span class="sxs-lookup"><span data-stu-id="d3b05-133">Configure an Event Hub or Storage Account to emit data to</span></span>
   
    ![Azure Diagnostics settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-your-logic-apps/diagnostics.png)

### <a name="adding-azure-alerts"></a><span data-ttu-id="d3b05-135">Adding Azure Alerts</span><span class="sxs-lookup"><span data-stu-id="d3b05-135">Adding Azure Alerts</span></span>
<span data-ttu-id="d3b05-136">Once diagnostics are configured, you can add Azure Alerts to fire when certain thresholds are crossed.</span><span class="sxs-lookup"><span data-stu-id="d3b05-136">Once diagnostics are configured, you can add Azure Alerts to fire when certain thresholds are crossed.</span></span>  <span data-ttu-id="d3b05-137">In the **Diagnostics** blade, select the **Alerts** tile and **Add alert**.</span><span class="sxs-lookup"><span data-stu-id="d3b05-137">In the **Diagnostics** blade, select the **Alerts** tile and **Add alert**.</span></span>  <span data-ttu-id="d3b05-138">This will walk you through configuring an alert based on a number of thresholds and metrics.</span><span class="sxs-lookup"><span data-stu-id="d3b05-138">This will walk you through configuring an alert based on a number of thresholds and metrics.</span></span>

![Azure Alert Metrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-your-logic-apps/alerts.png)

<span data-ttu-id="d3b05-140">You can configure the **Condition**, **Threshold**, and **Period** as desired.</span><span class="sxs-lookup"><span data-stu-id="d3b05-140">You can configure the **Condition**, **Threshold**, and **Period** as desired.</span></span>  <span data-ttu-id="d3b05-141">Finally, you can configure an email address to send a notification to, or configure a webhook.</span><span class="sxs-lookup"><span data-stu-id="d3b05-141">Finally, you can configure an email address to send a notification to, or configure a webhook.</span></span>  <span data-ttu-id="d3b05-142">You can use the [request trigger](../connectors/connectors-native-reqres.md) in a logic app to run on an alert as well (to do things like [post to Slack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app), [send a text](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app), or [add a message to a queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)).</span><span class="sxs-lookup"><span data-stu-id="d3b05-142">You can use the [request trigger](../connectors/connectors-native-reqres.md) in a logic app to run on an alert as well (to do things like [post to Slack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app), [send a text](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app), or [add a message to a queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)).</span></span>

### <a name="azure-diagnostics-settings"></a><span data-ttu-id="d3b05-143">Azure Diagnostics Settings</span><span class="sxs-lookup"><span data-stu-id="d3b05-143">Azure Diagnostics Settings</span></span>
<span data-ttu-id="d3b05-144">Each of these events contains details about the logic app and event like status.</span><span class="sxs-lookup"><span data-stu-id="d3b05-144">Each of these events contains details about the logic app and event like status.</span></span>  <span data-ttu-id="d3b05-145">Here is an example of a *ActionCompleted* event:</span><span class="sxs-lookup"><span data-stu-id="d3b05-145">Here is an example of a *ActionCompleted* event:</span></span>

```javascript
{
            "time": "2016-07-09T17:09:54.4773148Z",
            "workflowId": "/SUBSCRIPTIONS/80D4FE69-ABCD-EFGH-A938-9250F1C8AB03/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
            "resourceId": "/SUBSCRIPTIONS/80D4FE69-ABCD-EFGH-A938-9250F1C8AB03/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-06-01",
                "startTime": "2016-07-09T17:09:53.4336305Z",
                "endTime": "2016-07-09T17:09:53.5430281Z",
                "status": "Succeeded",
                "code": "OK",
                "resource": {
                    "subscriptionId": "80d4fe69-ABCD-EFGH-a938-9250f1c8ab03",
                    "resourceGroupName": "MyResourceGroup",
                    "workflowId": "cff00d5458f944d5a766f2f9ad142553",
                    "workflowName": "MyLogicApp",
                    "runId": "08587361146922712057",
                    "location": "eastus",
                    "actionName": "Http"
                },
                "correlation": {
                    "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
                    "clientTrackingId": "my-custom-tracking-id"
                },
                "trackedProperties": {
                    "myProperty": "<value>"
                }
            }
        }
```

<span data-ttu-id="d3b05-146">The two properties that are especially useful for tracking and monitoring are *clientTrackingId* and *trackedProperties*.</span><span class="sxs-lookup"><span data-stu-id="d3b05-146">The two properties that are especially useful for tracking and monitoring are *clientTrackingId* and *trackedProperties*.</span></span>  

#### <a name="client-tracking-id"></a><span data-ttu-id="d3b05-147">Client tracking ID</span><span class="sxs-lookup"><span data-stu-id="d3b05-147">Client tracking ID</span></span>
<span data-ttu-id="d3b05-148">The client tracking ID is a value that will correlate events across a logic app run, including any nested workflows called as a part of a logic app.</span><span class="sxs-lookup"><span data-stu-id="d3b05-148">The client tracking ID is a value that will correlate events across a logic app run, including any nested workflows called as a part of a logic app.</span></span>  <span data-ttu-id="d3b05-149">This ID will be auto-generated if not provided, but you can manually specify the client tracking ID from a trigger by passing a `x-ms-client-tracking-id` header with the ID value in the trigger request (request trigger, HTTP trigger, or webhook trigger).</span><span class="sxs-lookup"><span data-stu-id="d3b05-149">This ID will be auto-generated if not provided, but you can manually specify the client tracking ID from a trigger by passing a `x-ms-client-tracking-id` header with the ID value in the trigger request (request trigger, HTTP trigger, or webhook trigger).</span></span>

#### <a name="tracked-properties"></a><span data-ttu-id="d3b05-150">Tracked properties</span><span class="sxs-lookup"><span data-stu-id="d3b05-150">Tracked properties</span></span>
<span data-ttu-id="d3b05-151">Tracked properties can be added onto actions in the workflow definition to track inputs or outputs in diagnostics data.</span><span class="sxs-lookup"><span data-stu-id="d3b05-151">Tracked properties can be added onto actions in the workflow definition to track inputs or outputs in diagnostics data.</span></span>  <span data-ttu-id="d3b05-152">This can be useful if you wish to track data like an "order ID" in your telemetry.</span><span class="sxs-lookup"><span data-stu-id="d3b05-152">This can be useful if you wish to track data like an "order ID" in your telemetry.</span></span>  <span data-ttu-id="d3b05-153">To add a tracked property, include the `trackedProperties` property on an action.</span><span class="sxs-lookup"><span data-stu-id="d3b05-153">To add a tracked property, include the `trackedProperties` property on an action.</span></span>  <span data-ttu-id="d3b05-154">Tracked properties can only track a single actions inputs and outputs, but you can use the `correlation` properties of the events to correlate across actions in a run.</span><span class="sxs-lookup"><span data-stu-id="d3b05-154">Tracked properties can only track a single actions inputs and outputs, but you can use the `correlation` properties of the events to correlate across actions in a run.</span></span>

```javascript
{
    "myAction": {
        "type": "http",
        "inputs": {
            "uri": "http://uri",
            "headers": {
                "Content-Type": "application/json"
            },
            "body": "@triggerBody()"
        },
        "trackedProperties":{
            "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
            "myActionHTTPValue": "@action()['outputs']['body']['foo']",
            "transactionId": "@action()['inputs']['body']['bar']"
        }
    }
}
```

### <a name="extending-your-solutions"></a><span data-ttu-id="d3b05-155">Extending your solutions</span><span class="sxs-lookup"><span data-stu-id="d3b05-155">Extending your solutions</span></span>
<span data-ttu-id="d3b05-156">You can leverage this telemetry from the Event Hub or Storage into other services like [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite), [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/), and [Power BI](https://powerbi.com) to have real time monitoring of your integration workflows.</span><span class="sxs-lookup"><span data-stu-id="d3b05-156">You can leverage this telemetry from the Event Hub or Storage into other services like [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite), [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/), and [Power BI](https://powerbi.com) to have real time monitoring of your integration workflows.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3b05-157">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d3b05-157">Next Steps</span></span>
* [<span data-ttu-id="d3b05-158">Common examples and scenarios for logic apps</span><span class="sxs-lookup"><span data-stu-id="d3b05-158">Common examples and scenarios for logic apps</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="d3b05-159">Creating a Logic App Deployment Template</span><span class="sxs-lookup"><span data-stu-id="d3b05-159">Creating a Logic App Deployment Template</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="d3b05-160">Enterprise integration features</span><span class="sxs-lookup"><span data-stu-id="d3b05-160">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)





