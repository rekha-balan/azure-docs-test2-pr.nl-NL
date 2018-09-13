---
title: Extend alerts from Log Analytcs to Azure
description: This article describes the tools and API by which you can extend alerts from Log Analytics to Azure Alerts.
author: msvijayn
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 06/04/2018
ms.author: vinagara
ms.component: alerts
ms.openlocfilehash: 21ba95a7b3efff177afe63d22da3f6ba9848ded2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856440"
---
# <a name="extend-alerts-from-log-analytics-into-azure-alerts"></a><span data-ttu-id="bf18e-103">Extend alerts from Log Analytics into Azure Alerts</span><span class="sxs-lookup"><span data-stu-id="bf18e-103">Extend alerts from Log Analytics into Azure Alerts</span></span>
<span data-ttu-id="bf18e-104">The alerts feature in Azure Log Analytics is being replaced by Azure Alerts.</span><span class="sxs-lookup"><span data-stu-id="bf18e-104">The alerts feature in Azure Log Analytics is being replaced by Azure Alerts.</span></span> <span data-ttu-id="bf18e-105">As part of this transition, alerts that you originally configured in Log Analytics will be extended into Azure.</span><span class="sxs-lookup"><span data-stu-id="bf18e-105">As part of this transition, alerts that you originally configured in Log Analytics will be extended into Azure.</span></span> <span data-ttu-id="bf18e-106">If you don't want to wait for them to be automatically moved into Azure, you can initiate the process:</span><span class="sxs-lookup"><span data-stu-id="bf18e-106">If you don't want to wait for them to be automatically moved into Azure, you can initiate the process:</span></span>

- <span data-ttu-id="bf18e-107">Manually from the Operations Management Suite portal.</span><span class="sxs-lookup"><span data-stu-id="bf18e-107">Manually from the Operations Management Suite portal.</span></span> 
- <span data-ttu-id="bf18e-108">Programmatically by using the AlertsVersion API.</span><span class="sxs-lookup"><span data-stu-id="bf18e-108">Programmatically by using the AlertsVersion API.</span></span>  

> [!NOTE]
> <span data-ttu-id="bf18e-109">Microsoft will automatically extend alerts created in Log Analytics to Azure Alerts, starting on May 14, 2018, in a recurring series until completed.</span><span class="sxs-lookup"><span data-stu-id="bf18e-109">Microsoft will automatically extend alerts created in Log Analytics to Azure Alerts, starting on May 14, 2018, in a recurring series until completed.</span></span> <span data-ttu-id="bf18e-110">Microsoft schedules migrating the alerts to Azure, and during this transition, alerts can be managed from both the Operations Management Suite portal and the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bf18e-110">Microsoft schedules migrating the alerts to Azure, and during this transition, alerts can be managed from both the Operations Management Suite portal and the Azure portal.</span></span> <span data-ttu-id="bf18e-111">This process is not destructive or interruptive.</span><span class="sxs-lookup"><span data-stu-id="bf18e-111">This process is not destructive or interruptive.</span></span>  

## <a name="option-1-initiate-from-the-operations-management-suite-portal"></a><span data-ttu-id="bf18e-112">Option 1: Initiate from the Operations Management Suite portal</span><span class="sxs-lookup"><span data-stu-id="bf18e-112">Option 1: Initiate from the Operations Management Suite portal</span></span>
<span data-ttu-id="bf18e-113">The following steps describe how to extend alerts for the workspace from the Operations Management Suite portal.</span><span class="sxs-lookup"><span data-stu-id="bf18e-113">The following steps describe how to extend alerts for the workspace from the Operations Management Suite portal.</span></span>  

1. <span data-ttu-id="bf18e-114">In the Azure portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="bf18e-114">In the Azure portal, select **All services**.</span></span> <span data-ttu-id="bf18e-115">In the list of resources, type **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="bf18e-115">In the list of resources, type **Log Analytics**.</span></span> <span data-ttu-id="bf18e-116">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="bf18e-116">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="bf18e-117">Select **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="bf18e-117">Select **Log Analytics**.</span></span>
2. <span data-ttu-id="bf18e-118">In the Log Analytics subscriptions pane, select a workspace, and then select the **OMS Portal** tile.</span><span class="sxs-lookup"><span data-stu-id="bf18e-118">In the Log Analytics subscriptions pane, select a workspace, and then select the **OMS Portal** tile.</span></span>
<span data-ttu-id="bf18e-119">![Screenshot of Log Analytics subscription pane, with OMS Portal tile highlighted](./media/monitor-alerts-extend/azure-portal-01.png)</span><span class="sxs-lookup"><span data-stu-id="bf18e-119">![Screenshot of Log Analytics subscription pane, with OMS Portal tile highlighted](./media/monitor-alerts-extend/azure-portal-01.png)</span></span> 
3. <span data-ttu-id="bf18e-120">After you are redirected to the Operations Management Suite portal, select the **Settings** icon.</span><span class="sxs-lookup"><span data-stu-id="bf18e-120">After you are redirected to the Operations Management Suite portal, select the **Settings** icon.</span></span>
<span data-ttu-id="bf18e-121">![Screenshot of Operations Management Suite portal, with Settings icon highlighted](./media/monitor-alerts-extend/oms-portal-settings-option.png)</span><span class="sxs-lookup"><span data-stu-id="bf18e-121">![Screenshot of Operations Management Suite portal, with Settings icon highlighted](./media/monitor-alerts-extend/oms-portal-settings-option.png)</span></span> 
4. <span data-ttu-id="bf18e-122">From the **Settings** page, select **Alerts**.</span><span class="sxs-lookup"><span data-stu-id="bf18e-122">From the **Settings** page, select **Alerts**.</span></span>  
5. <span data-ttu-id="bf18e-123">Select **Extend into Azure**.</span><span class="sxs-lookup"><span data-stu-id="bf18e-123">Select **Extend into Azure**.</span></span>
<span data-ttu-id="bf18e-124">![Screenshot of Operations Management Suite portal Alert Settings page, with Extend into Azure highlighted](./media/monitor-alerts-extend/ExtendInto.png)</span><span class="sxs-lookup"><span data-stu-id="bf18e-124">![Screenshot of Operations Management Suite portal Alert Settings page, with Extend into Azure highlighted](./media/monitor-alerts-extend/ExtendInto.png)</span></span>
6. <span data-ttu-id="bf18e-125">A three-step wizard appears in the **Alerts** pane.</span><span class="sxs-lookup"><span data-stu-id="bf18e-125">A three-step wizard appears in the **Alerts** pane.</span></span> <span data-ttu-id="bf18e-126">Read the overview, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf18e-126">Read the overview, and select **Next**.</span></span>
<span data-ttu-id="bf18e-127">![Screenshot of step 1 of the wizard](./media/monitor-alerts-extend/ExtendStep1.png)</span><span class="sxs-lookup"><span data-stu-id="bf18e-127">![Screenshot of step 1 of the wizard](./media/monitor-alerts-extend/ExtendStep1.png)</span></span>  
7. <span data-ttu-id="bf18e-128">In the second step, you see a summary of proposed changes, listing appropriate [action groups](monitoring-action-groups.md) for the alerts.</span><span class="sxs-lookup"><span data-stu-id="bf18e-128">In the second step, you see a summary of proposed changes, listing appropriate [action groups](monitoring-action-groups.md) for the alerts.</span></span> <span data-ttu-id="bf18e-129">If similar actions are seen across more than one alert, the wizard proposes to associate a single action group with all of them.</span><span class="sxs-lookup"><span data-stu-id="bf18e-129">If similar actions are seen across more than one alert, the wizard proposes to associate a single action group with all of them.</span></span>  <span data-ttu-id="bf18e-130">The naming convention is as follows: *WorkspaceName_AG_#Number*.</span><span class="sxs-lookup"><span data-stu-id="bf18e-130">The naming convention is as follows: *WorkspaceName_AG_#Number*.</span></span> <span data-ttu-id="bf18e-131">To proceed, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf18e-131">To proceed, select **Next**.</span></span>
<span data-ttu-id="bf18e-132">![Screenshot of step 2 of the wizard](./media/monitor-alerts-extend/ExtendStep2.png)</span><span class="sxs-lookup"><span data-stu-id="bf18e-132">![Screenshot of step 2 of the wizard](./media/monitor-alerts-extend/ExtendStep2.png)</span></span>  
8. <span data-ttu-id="bf18e-133">In the last step of wizard, select **Finish**, and confirm when prompted to initiate the process.</span><span class="sxs-lookup"><span data-stu-id="bf18e-133">In the last step of wizard, select **Finish**, and confirm when prompted to initiate the process.</span></span> <span data-ttu-id="bf18e-134">Optionally, you can provide an email address, so that you are notified when the process completes and all alerts have been successfully moved to Azure Alerts.</span><span class="sxs-lookup"><span data-stu-id="bf18e-134">Optionally, you can provide an email address, so that you are notified when the process completes and all alerts have been successfully moved to Azure Alerts.</span></span>
<span data-ttu-id="bf18e-135">![Screenshot of step 3 of the wizard](./media/monitor-alerts-extend/ExtendStep3.png)</span><span class="sxs-lookup"><span data-stu-id="bf18e-135">![Screenshot of step 3 of the wizard](./media/monitor-alerts-extend/ExtendStep3.png)</span></span>

<span data-ttu-id="bf18e-136">When the wizard is finished, on the **Alert Settings** page, the option to extend alerts to Azure is removed.</span><span class="sxs-lookup"><span data-stu-id="bf18e-136">When the wizard is finished, on the **Alert Settings** page, the option to extend alerts to Azure is removed.</span></span> <span data-ttu-id="bf18e-137">In the background, your alerts are moved into Azure, and this can take some time.</span><span class="sxs-lookup"><span data-stu-id="bf18e-137">In the background, your alerts are moved into Azure, and this can take some time.</span></span> <span data-ttu-id="bf18e-138">During the operation, you can't make changes to alerts from the Operations Management Suite portal.</span><span class="sxs-lookup"><span data-stu-id="bf18e-138">During the operation, you can't make changes to alerts from the Operations Management Suite portal.</span></span> <span data-ttu-id="bf18e-139">You can see the current status from the banner at the top of the portal.</span><span class="sxs-lookup"><span data-stu-id="bf18e-139">You can see the current status from the banner at the top of the portal.</span></span> <span data-ttu-id="bf18e-140">If you provided an email address earlier, you receive an email when the process has successfully completed.</span><span class="sxs-lookup"><span data-stu-id="bf18e-140">If you provided an email address earlier, you receive an email when the process has successfully completed.</span></span>  


<span data-ttu-id="bf18e-141">Alerts continue to be listed in Operations Management Suite portal, even after they are successfully moved into Azure.</span><span class="sxs-lookup"><span data-stu-id="bf18e-141">Alerts continue to be listed in Operations Management Suite portal, even after they are successfully moved into Azure.</span></span>
<span data-ttu-id="bf18e-142">![Screenshot of Operations Management Suite portal Alert Settings page](./media/monitor-alerts-extend/PostExtendList.png)</span><span class="sxs-lookup"><span data-stu-id="bf18e-142">![Screenshot of Operations Management Suite portal Alert Settings page](./media/monitor-alerts-extend/PostExtendList.png)</span></span>


## <a name="option-2-use-the-alertsversion-api"></a><span data-ttu-id="bf18e-143">Option 2: Use the AlertsVersion API</span><span class="sxs-lookup"><span data-stu-id="bf18e-143">Option 2: Use the AlertsVersion API</span></span>
<span data-ttu-id="bf18e-144">You can use the Log Analytics AlertsVersion API to extend alerts from Log Analytics into Azure Alerts from any client that can call a REST API.</span><span class="sxs-lookup"><span data-stu-id="bf18e-144">You can use the Log Analytics AlertsVersion API to extend alerts from Log Analytics into Azure Alerts from any client that can call a REST API.</span></span> <span data-ttu-id="bf18e-145">You can access the API from PowerShell by using [ARMClient](https://github.com/projectkudu/ARMClient), an open-source command-line tool.</span><span class="sxs-lookup"><span data-stu-id="bf18e-145">You can access the API from PowerShell by using [ARMClient](https://github.com/projectkudu/ARMClient), an open-source command-line tool.</span></span> <span data-ttu-id="bf18e-146">You can output the results in JSON.</span><span class="sxs-lookup"><span data-stu-id="bf18e-146">You can output the results in JSON.</span></span>  

<span data-ttu-id="bf18e-147">To use the API, you first create a GET request.</span><span class="sxs-lookup"><span data-stu-id="bf18e-147">To use the API, you first create a GET request.</span></span> <span data-ttu-id="bf18e-148">This evaluates and returns a summary of the proposed changes, before you attempt to actually extend into Azure by using a POST request.</span><span class="sxs-lookup"><span data-stu-id="bf18e-148">This evaluates and returns a summary of the proposed changes, before you attempt to actually extend into Azure by using a POST request.</span></span> <span data-ttu-id="bf18e-149">The results list your alerts and a proposed list of [action groups](monitoring-action-groups.md), in JSON format.</span><span class="sxs-lookup"><span data-stu-id="bf18e-149">The results list your alerts and a proposed list of [action groups](monitoring-action-groups.md), in JSON format.</span></span> <span data-ttu-id="bf18e-150">If similar actions are seen across more than one alert, the service proposes to associate all of them with a single action group.</span><span class="sxs-lookup"><span data-stu-id="bf18e-150">If similar actions are seen across more than one alert, the service proposes to associate all of them with a single action group.</span></span> <span data-ttu-id="bf18e-151">The naming convention is as follows: *WorkspaceName_AG_#Number*.</span><span class="sxs-lookup"><span data-stu-id="bf18e-151">The naming convention is as follows: *WorkspaceName_AG_#Number*.</span></span>

```
armclient GET  /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.OperationalInsights/workspaces/<workspaceName>/alertsversion?api-version=2017-04-26-preview
```

<span data-ttu-id="bf18e-152">If the GET request is successful, an HTTP status code 200 is returned, along with a list of alerts and proposed action groups in the JSON data.</span><span class="sxs-lookup"><span data-stu-id="bf18e-152">If the GET request is successful, an HTTP status code 200 is returned, along with a list of alerts and proposed action groups in the JSON data.</span></span> <span data-ttu-id="bf18e-153">The following is an example response:</span><span class="sxs-lookup"><span data-stu-id="bf18e-153">The following is an example response:</span></span>

```json
{
    "version": 1,
    "migrationSummary": {
        "alertsCount": 2,
        "actionGroupsCount": 2,
        "alerts": [
            {
                "alertName": "DemoAlert_1",
                "alertId": " /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.OperationalInsights/workspaces/<workspaceName>/savedSearches/<savedSearchId>/schedules/<scheduleId>/actions/<actionId>",
                "actionGroupName": "<workspaceName>_AG_1"
            },
            {
                "alertName": "DemoAlert_2",
                "alertId": " /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.OperationalInsights/workspaces/<workspaceName>/savedSearches/<savedSearchId>/schedules/<scheduleId>/actions/<actionId>",
                "actionGroupName": "<workspaceName>_AG_2"
            }
        ],
        "actionGroups": [
            {
                "actionGroupName": "<workspaceName>_AG_1",
                "actionGroupResourceId": "/subscriptions/<subscriptionid>/resourceGroups/<resourceGroupName>/providers/microsoft.insights/actionGroups/<workspaceName>_AG_1",
                "actions": {
                    "emailIds": [
                        "JohnDoe@mail.com"
                    ],
                    "webhookActions": [
                        {
                            "name": "Webhook_1",
                            "serviceUri": "http://test.com"
                        }
                    ],
                    "itsmAction": {}
                }
            },
            {
                "actionGroupName": "<workspaceName>_AG_1",
                "actionGroupResourceId": "/subscriptions/<subscriptionid>/resourceGroups/<resourceGroupName>/providers/microsoft.insights/actionGroups/<workspaceName>_AG_1",
                 "actions": {
                    "emailIds": [
                        "test1@mail.com",
                          "test2@mail.com"
                    ],
                    "webhookActions": [],
                    "itsmAction": {
                        "connectionId": "<Guid>",
                        "templateInfo":"{\"PayloadRevision\":0,\"WorkItemType\":\"Incident\",\"UseTemplate\":false,\"WorkItemData\":\"{\\\"contact_type\\\":\\\"email\\\",\\\"impact\\\":\\\"3\\\",\\\"urgency\\\":\\\"2\\\",\\\"category\\\":\\\"request\\\",\\\"subcategory\\\":\\\"password\\\"}\",\"CreateOneWIPerCI\":false}"
                    }
                }
            }
        ]
    }
}

```
<span data-ttu-id="bf18e-154">If the specified workspace does not have any alert rules defined, the JSON data returns the following:</span><span class="sxs-lookup"><span data-stu-id="bf18e-154">If the specified workspace does not have any alert rules defined, the JSON data returns the following:</span></span>

```json
{
    "version": 1,
    "Message": "No Alerts found in the workspace for migration."
}
```

<span data-ttu-id="bf18e-155">If all alert rules in the specified workspace have already been extended to Azure, the response to the GET request is:</span><span class="sxs-lookup"><span data-stu-id="bf18e-155">If all alert rules in the specified workspace have already been extended to Azure, the response to the GET request is:</span></span>

```json
{
    "version": 2
}
```

<span data-ttu-id="bf18e-156">To initiate migrating the alerts to Azure, initiate a POST response.</span><span class="sxs-lookup"><span data-stu-id="bf18e-156">To initiate migrating the alerts to Azure, initiate a POST response.</span></span> <span data-ttu-id="bf18e-157">The POST response confirms your intent, as well as acceptance, to have alerts extended from Log Analytics to Azure Alerts.</span><span class="sxs-lookup"><span data-stu-id="bf18e-157">The POST response confirms your intent, as well as acceptance, to have alerts extended from Log Analytics to Azure Alerts.</span></span> <span data-ttu-id="bf18e-158">The activity is scheduled and the alerts are processed as indicated, based on the results when you performed the GET response earlier.</span><span class="sxs-lookup"><span data-stu-id="bf18e-158">The activity is scheduled and the alerts are processed as indicated, based on the results when you performed the GET response earlier.</span></span> <span data-ttu-id="bf18e-159">Optionally, you can provide a list of email addresses to which Log Analytics sends a report when the scheduled background process of migrating the alerts completes successfully.</span><span class="sxs-lookup"><span data-stu-id="bf18e-159">Optionally, you can provide a list of email addresses to which Log Analytics sends a report when the scheduled background process of migrating the alerts completes successfully.</span></span> <span data-ttu-id="bf18e-160">You can use the following request example:</span><span class="sxs-lookup"><span data-stu-id="bf18e-160">You can use the following request example:</span></span>

```
$emailJSON = “{‘Recipients’: [‘a@b.com’, ‘b@a.com’]}”
armclient POST  /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.OperationalInsights/workspaces/<workspaceName>/alertsversion?api-version=2017-04-26-preview $emailJSON
```

> [!NOTE]
> <span data-ttu-id="bf18e-161">The result of migrating alerts into Azure Alerts might vary based on the summary provided by GET response.</span><span class="sxs-lookup"><span data-stu-id="bf18e-161">The result of migrating alerts into Azure Alerts might vary based on the summary provided by GET response.</span></span> <span data-ttu-id="bf18e-162">When scheduled, alerts in Log Analytics are temporarily unavailable for modification in the Operations Management Suite portal.</span><span class="sxs-lookup"><span data-stu-id="bf18e-162">When scheduled, alerts in Log Analytics are temporarily unavailable for modification in the Operations Management Suite portal.</span></span> <span data-ttu-id="bf18e-163">However, you can create new alerts.</span><span class="sxs-lookup"><span data-stu-id="bf18e-163">However, you can create new alerts.</span></span> 

<span data-ttu-id="bf18e-164">If the POST request is successful, it returns an HTTP 200 OK status, along with the following response:</span><span class="sxs-lookup"><span data-stu-id="bf18e-164">If the POST request is successful, it returns an HTTP 200 OK status, along with the following response:</span></span>

```json
{
    "version": 2
}
```

<span data-ttu-id="bf18e-165">This response indicates the alerts have been successfully extended into Azure Alerts.</span><span class="sxs-lookup"><span data-stu-id="bf18e-165">This response indicates the alerts have been successfully extended into Azure Alerts.</span></span> <span data-ttu-id="bf18e-166">The  version property is only for checking if alerts have been extended to Azure, and have no relation to the [Log Analytics Search API](../log-analytics/log-analytics-api-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="bf18e-166">The  version property is only for checking if alerts have been extended to Azure, and have no relation to the [Log Analytics Search API](../log-analytics/log-analytics-api-alerts.md).</span></span> <span data-ttu-id="bf18e-167">When the alerts are extended to Azure successfully, any email addresses provided with the POST request are sent a report.</span><span class="sxs-lookup"><span data-stu-id="bf18e-167">When the alerts are extended to Azure successfully, any email addresses provided with the POST request are sent a report.</span></span> <span data-ttu-id="bf18e-168">If all the alerts in the specified workspace are already scheduled to be extended, the response to your POST request is that the attempt was forbidden (a 403 status code).</span><span class="sxs-lookup"><span data-stu-id="bf18e-168">If all the alerts in the specified workspace are already scheduled to be extended, the response to your POST request is that the attempt was forbidden (a 403 status code).</span></span> <span data-ttu-id="bf18e-169">To view any error message or understand if the process is stuck, you can submit a GET request.</span><span class="sxs-lookup"><span data-stu-id="bf18e-169">To view any error message or understand if the process is stuck, you can submit a GET request.</span></span> <span data-ttu-id="bf18e-170">If there is an error message, it is returned, along with the summary information.</span><span class="sxs-lookup"><span data-stu-id="bf18e-170">If there is an error message, it is returned, along with the summary information.</span></span>

```json
{
    "version": 1,
    "message": "OMS was unable to extend your alerts into Azure, Error: The subscription is not registered to use the namespace 'microsoft.insights'. OMS will schedule extending your alerts, once remediation steps illustrated in the troubleshooting guide are done.",
    "recipients": [
       "john.doe@email.com",
       "jane.doe@email.com"
     ],
    "migrationSummary": {
        "alertsCount": 2,
        "actionGroupsCount": 2,
        "alerts": [
            {
                "alertName": "DemoAlert_1",
                "alertId": " /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.OperationalInsights/workspaces/<workspaceName>/savedSearches/<savedSearchId>/schedules/<scheduleId>/actions/<actionId>",
                "actionGroupName": "<workspaceName>_AG_1"
            },
            {
                "alertName": "DemoAlert_2",
                "alertId": " /subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.OperationalInsights/workspaces/<workspaceName>/savedSearches/<savedSearchId>/schedules/<scheduleId>/actions/<actionId>",
                "actionGroupName": "<workspaceName>_AG_2"
            }
        ],
        "actionGroups": [
            {
                "actionGroupName": "<workspaceName>_AG_1",
                "actionGroupResourceId": "/subscriptions/<subscriptionid>/resourceGroups/<resourceGroupName>/providers/microsoft.insights/actionGroups/<workspaceName>_AG_1",
                "actions": {
                    "emailIds": [
                        "JohnDoe@mail.com"
                    ],
                    "webhookActions": [
                        {
                            "name": "Webhook_1",
                            "serviceUri": "http://test.com"
                        }
                    ],
                    "itsmAction": {}
                }
            },
            {
                "actionGroupName": "<workspaceName>_AG_1",
                "actionGroupResourceId": "/subscriptions/<subscriptionid>/resourceGroups/<resourceGroupName>/providers/microsoft.insights/actionGroups/<workspaceName>_AG_1",
                 "actions": {
                    "emailIds": [
                        "test1@mail.com",
                          "test2@mail.com"
                    ],
                    "webhookActions": [],
                    "itsmAction": {
                        "connectionId": "<Guid>",
                        "templateInfo":"{\"PayloadRevision\":0,\"WorkItemType\":\"Incident\",\"UseTemplate\":false,\"WorkItemData\":\"{\\\"contact_type\\\":\\\"email\\\",\\\"impact\\\":\\\"3\\\",\\\"urgency\\\":\\\"2\\\",\\\"category\\\":\\\"request\\\",\\\"subcategory\\\":\\\"password\\\"}\",\"CreateOneWIPerCI\":false}"
                    }
                }
            }
        ]
    }
}              

```


## <a name="option-3-use-a-custom-powershell-script"></a><span data-ttu-id="bf18e-171">Option 3: Use a custom PowerShell script</span><span class="sxs-lookup"><span data-stu-id="bf18e-171">Option 3: Use a custom PowerShell script</span></span>
 <span data-ttu-id="bf18e-172">If Microsoft has not successfully extended your alerts from the Operations Management Suite portal to Azure, you can do so manually until July 5, 2018.</span><span class="sxs-lookup"><span data-stu-id="bf18e-172">If Microsoft has not successfully extended your alerts from the Operations Management Suite portal to Azure, you can do so manually until July 5, 2018.</span></span> <span data-ttu-id="bf18e-173">The two options for manual extension are covered in the previous two sections.</span><span class="sxs-lookup"><span data-stu-id="bf18e-173">The two options for manual extension are covered in the previous two sections.</span></span>

<span data-ttu-id="bf18e-174">After July 5, 2018, all alerts from the Operations Management Suite portal are extended into Azure.</span><span class="sxs-lookup"><span data-stu-id="bf18e-174">After July 5, 2018, all alerts from the Operations Management Suite portal are extended into Azure.</span></span> <span data-ttu-id="bf18e-175">Users who didn't take the [necessary remediation steps suggested](#troubleshooting) will have their alerts running without firing actions or notifications, due to the lack of associated [action groups](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="bf18e-175">Users who didn't take the [necessary remediation steps suggested](#troubleshooting) will have their alerts running without firing actions or notifications, due to the lack of associated [action groups](monitoring-action-groups.md).</span></span> 

<span data-ttu-id="bf18e-176">To create [action groups](monitoring-action-groups.md) for alerts manually in Log Analytics, use the following sample script:</span><span class="sxs-lookup"><span data-stu-id="bf18e-176">To create [action groups](monitoring-action-groups.md) for alerts manually in Log Analytics, use the following sample script:</span></span>
```PowerShell
########## Input Parameters Begin ###########


$subscriptionId = ""
$resourceGroup = ""
$workspaceName = "" 


########## Input Parameters End ###########

armclient login

try
{
    $workspace = armclient get /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/"$workspaceName"?api-version=2015-03-20 | ConvertFrom-Json
    $workspaceId = $workspace.properties.customerId
    $resourceLocation = $workspace.location
}
catch
{
    "Please enter valid input parameters i.e. Subscription Id, Resource Group and Workspace Name !!"
    exit
}

# Get Extend Summary of the Alerts
"`nGetting Extend Summary of Alerts for the workspace...`n"
try
{

    $value = armclient get /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/alertsversion?api-version=2017-04-26-preview

    "Extend preview summary"
    "=========================`n"

    $value

    $result = $value | ConvertFrom-Json
}
catch
{

    $ErrorMessage = $_.Exception.Message
    "Error occured while fetching/parsing Extend summary: $ErrorMessage"
    exit 
}

if ($result.version -eq 2)
{
    "`nThe alerts in this workspace have already been extended to Azure."
    exit
}

$in = Read-Host -Prompt "`nDo you want to continue extending the alerts to Azure? (Y/N)"

if ($in.ToLower() -ne "y")
{
    exit
} 


# Check for resource provider registration
try
{
    $val = armclient get subscriptions/$subscriptionId/providers/microsoft.insights/?api-version=2017-05-10 | ConvertFrom-Json
    if ($val.registrationState -eq "NotRegistered")
    {
        $val = armclient post subscriptions/$subscriptionId/providers/microsoft.insights/register/?api-version=2017-05-10
    }
}
catch
{
    "`nThe user does not have required access to register the resource provider. Please try with user having Contributor/Owner role in the subscription"
    exit
}

$actionGroupsMap = @{}
try
{
    "`nCreating new action groups for alerts extension...`n"
    foreach ($actionGroup in $result.migrationSummary.actionGroups)
    {
        $actionGroupName = $actionGroup.actionGroupName
        $actions = $actionGroup.actions
        if ($actionGroupsMap.ContainsKey($actionGroupName))
        {
            continue
        } 
        
        # Create action group payload
        $shortName = $actionGroupName.Substring($actionGroupName.LastIndexOf("AG_"))
        $properties = @{"groupShortName"= $shortName; "enabled" = $true}
        $emailReceivers = New-Object Object[] $actions.emailIds.Count
        $webhookReceivers = New-Object Object[] $actions.webhookActions.Count
        
        $count = 0
        foreach ($email in $actions.emailIds)
        {
            $emailReceivers[$count] = @{"name" = "Email$($count+1)"; "emailAddress" = "$email"}
            $count++
        }

        $count = 0
        foreach ($webhook in $actions.webhookActions)
        {
            $webhookReceivers[$count] = @{"name" = "$($webhook.name)"; "serviceUri" = "$($webhook.serviceUri)"}
            $count++
        }

        $itsmAction = $actions.itsmAction
        if ($itsmAction.connectionId -ne $null)
        {
            $val = @{
            "name" = "ITSM"
            "workspaceId" = "$subscriptionId|$workspaceId"
            "connectionId" = "$($itsmAction.connectionId)"
            "ticketConfiguration" = $itsmAction.templateInfo
            "region" = "$resourceLocation"
            }
            $properties["itsmReceivers"] = @($val)  
        }

        $properties["emailReceivers"] = @($emailReceivers)
        $properties["webhookReceivers"] = @($webhookReceivers)
        $armPayload = @{"properties" = $properties; "location" = "Global"} | ConvertTo-Json -Compress -Depth 4

    
        # Azure Resource Manager call to create action group
        $response = $armPayload | armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.insights/actionGroups/$actionGroupName/?api-version=2017-04-01

        "Created Action Group with name $actionGroupName" 
        $actionGroupsMap[$actionGroupName] = $actionGroup.actionGroupResourceId.ToLower()
        $index++
    }

    "`nSuccessfully created all action groups!!"
}
catch
{
    $ErrorMessage = $_.Exception.Message

    #Delete all action groups in case of failure
    "`nDeleting newly created action groups if any as some error happened..."
    
    foreach ($actionGroup in $actionGroupsMap.Keys)
    {
        $response = armclient delete /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.insights/actionGroups/$actionGroup/?api-version=2017-04-01      
    }

    "`nError: $ErrorMessage"
    "`nExiting..."
    exit
}

# Update all alerts configuration to the new version
"`nExtending OMS alerts to Azure...`n"

try
{
    $index = 1
    foreach ($alert in $result.migrationSummary.alerts)
    {
        $uri = $alert.alertId + "?api-version=2015-03-20"
        $config = armclient get $uri | ConvertFrom-Json
        $aznsNotification = @{
            "GroupIds" = @($actionGroupsMap[$alert.actionGroupName])
        }
        if ($alert.customWebhookPayload)
        {
            $aznsNotification.Add("CustomWebhookPayload", $alert.customWebhookPayload)
        }
        if ($alert.customEmailSubject)
        {
            $aznsNotification.Add("CustomEmailSubject", $alert.customEmailSubject)
        }      

        # Update alert version
        $config.properties.Version = 2

        $config.properties | Add-Member -MemberType NoteProperty -Name "AzNsNotification" -Value $aznsNotification
        $payload = $config | ConvertTo-Json -Depth 4
        $response = $payload | armclient put $uri
    
        "Extended alert with name $($alert.alertName)"
        $index++
    }
}
catch
{
    $ErrorMessage = $_.Exception.Message   
    if ($index -eq 1)
    {
        "`nDeleting all newly created action groups as no alerts got extended..."
        foreach ($actionGroup in $actionGroupsMap.Keys)
        {
            $response = armclient delete /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.insights/actionGroups/$actionGroup/?api-version=2017-04-01      
        }
        "`nDeleted all action groups."  
    }
    
    "`nError: $ErrorMessage"
    "`nPlease resolve the issue and try extending again!!"
    "`nExiting..."
    exit
}

"`nSuccessfully extended all OMS alerts to Azure!!" 

# Update version of workspace to indicate extension
"`nUpdating alert version information in OMS workspace..." 

$response = armclient post "/subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/alertsversion?api-version=2017-04-26-preview&iversion=2"

"`nExtension complete!!"
```


### <a name="about-the-custom-powershell-script"></a><span data-ttu-id="bf18e-177">About the custom PowerShell script</span><span class="sxs-lookup"><span data-stu-id="bf18e-177">About the custom PowerShell script</span></span> 
<span data-ttu-id="bf18e-178">The following is important information about using the script:</span><span class="sxs-lookup"><span data-stu-id="bf18e-178">The following is important information about using the script:</span></span>
- <span data-ttu-id="bf18e-179">A prerequisite is the installation of [ARMclient](https://github.com/projectkudu/ARMClient), an open-source command-line tool that simplifies invoking the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="bf18e-179">A prerequisite is the installation of [ARMclient](https://github.com/projectkudu/ARMClient), an open-source command-line tool that simplifies invoking the Azure Resource Manager API.</span></span>
- <span data-ttu-id="bf18e-180">To run the script, you must have a contributor or owner role in the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="bf18e-180">To run the script, you must have a contributor or owner role in the Azure subscription.</span></span>
- <span data-ttu-id="bf18e-181">You must provide the following parameters:</span><span class="sxs-lookup"><span data-stu-id="bf18e-181">You must provide the following parameters:</span></span>
    - <span data-ttu-id="bf18e-182">$subscriptionId: The Azure Subscription ID associated with the Operations Management Suite Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="bf18e-182">$subscriptionId: The Azure Subscription ID associated with the Operations Management Suite Log Analytics workspace.</span></span>
    - <span data-ttu-id="bf18e-183">$resourceGroup: The Azure Resource Group for Operations Management Suite Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="bf18e-183">$resourceGroup: The Azure Resource Group for Operations Management Suite Log Analytics workspace.</span></span>
    - <span data-ttu-id="bf18e-184">$workspaceName: The name of the Operations Management Suite Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="bf18e-184">$workspaceName: The name of the Operations Management Suite Log Analytics workspace.</span></span>

### <a name="output-of-the-custom-powershell-script"></a><span data-ttu-id="bf18e-185">Output of the custom PowerShell script</span><span class="sxs-lookup"><span data-stu-id="bf18e-185">Output of the custom PowerShell script</span></span>
<span data-ttu-id="bf18e-186">The script is verbose, and outputs the steps as it runs:</span><span class="sxs-lookup"><span data-stu-id="bf18e-186">The script is verbose, and outputs the steps as it runs:</span></span> 
- <span data-ttu-id="bf18e-187">It displays the summary, which contains the information about the existing Operations Management Suite Log Analytics alerts in the workspace.</span><span class="sxs-lookup"><span data-stu-id="bf18e-187">It displays the summary, which contains the information about the existing Operations Management Suite Log Analytics alerts in the workspace.</span></span> <span data-ttu-id="bf18e-188">The summary also contains information about the Azure action groups to be created for the actions associated with them.</span><span class="sxs-lookup"><span data-stu-id="bf18e-188">The summary also contains information about the Azure action groups to be created for the actions associated with them.</span></span> 
- <span data-ttu-id="bf18e-189">You are prompted to go ahead with the extension, or exit after viewing the summary.</span><span class="sxs-lookup"><span data-stu-id="bf18e-189">You are prompted to go ahead with the extension, or exit after viewing the summary.</span></span>
- <span data-ttu-id="bf18e-190">If you go ahead with the extension, new Azure action groups are created, and all the existing alerts are associated with them.</span><span class="sxs-lookup"><span data-stu-id="bf18e-190">If you go ahead with the extension, new Azure action groups are created, and all the existing alerts are associated with them.</span></span> 
- <span data-ttu-id="bf18e-191">The script exits by displaying the message "Extension complete!"</span><span class="sxs-lookup"><span data-stu-id="bf18e-191">The script exits by displaying the message "Extension complete!"</span></span> <span data-ttu-id="bf18e-192">In case of any intermediate failures, the script displays subsequent errors.</span><span class="sxs-lookup"><span data-stu-id="bf18e-192">In case of any intermediate failures, the script displays subsequent errors.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bf18e-193">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="bf18e-193">Troubleshooting</span></span> 
<span data-ttu-id="bf18e-194">During the process of extending alerts, problems can prevent the system from creating the necessary [action groups](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="bf18e-194">During the process of extending alerts, problems can prevent the system from creating the necessary [action groups](monitoring-action-groups.md).</span></span> <span data-ttu-id="bf18e-195">In such cases, you see an error message in a banner in the **Alert** section of the Operations Management Suite portal, or in the GET call done to the API.</span><span class="sxs-lookup"><span data-stu-id="bf18e-195">In such cases, you see an error message in a banner in the **Alert** section of the Operations Management Suite portal, or in the GET call done to the API.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf18e-196">If you don't take the following remediation steps before July 5, 2018, alerts will run in Azure but will not fire any action or notification.</span><span class="sxs-lookup"><span data-stu-id="bf18e-196">If you don't take the following remediation steps before July 5, 2018, alerts will run in Azure but will not fire any action or notification.</span></span> <span data-ttu-id="bf18e-197">To get notifications for alerts, you must manually edit and add [action groups](monitoring-action-groups.md), or use the preceding [custom PowerShell script](#option-3---using-custom-powershell-script).</span><span class="sxs-lookup"><span data-stu-id="bf18e-197">To get notifications for alerts, you must manually edit and add [action groups](monitoring-action-groups.md), or use the preceding [custom PowerShell script](#option-3---using-custom-powershell-script).</span></span>

<span data-ttu-id="bf18e-198">Here are the remediation steps for each error:</span><span class="sxs-lookup"><span data-stu-id="bf18e-198">Here are the remediation steps for each error:</span></span>
- <span data-ttu-id="bf18e-199">**Error: Scope Lock is present at subscription/resource group level for write operations**:   ![Screenshot of the Operations Management Suite portal Alert Settings page, with Scope Lock error message highlighted](./media/monitor-alerts-extend/ErrorScopeLock.png)</span><span class="sxs-lookup"><span data-stu-id="bf18e-199">**Error: Scope Lock is present at subscription/resource group level for write operations**:   ![Screenshot of the Operations Management Suite portal Alert Settings page, with Scope Lock error message highlighted](./media/monitor-alerts-extend/ErrorScopeLock.png)</span></span>

    <span data-ttu-id="bf18e-200">When Scope Lock is enabled, the feature restricts any new change in the subscription or resource group that contains the Log Analytics (Operations Management Suite) workspace.</span><span class="sxs-lookup"><span data-stu-id="bf18e-200">When Scope Lock is enabled, the feature restricts any new change in the subscription or resource group that contains the Log Analytics (Operations Management Suite) workspace.</span></span> <span data-ttu-id="bf18e-201">The system is unable to extend alerts into Azure and create necessary action groups.</span><span class="sxs-lookup"><span data-stu-id="bf18e-201">The system is unable to extend alerts into Azure and create necessary action groups.</span></span>
    
    <span data-ttu-id="bf18e-202">To resolve, delete the *ReadOnly* lock on your subscription or resource group that contains the workspace.</span><span class="sxs-lookup"><span data-stu-id="bf18e-202">To resolve, delete the *ReadOnly* lock on your subscription or resource group that contains the workspace.</span></span> <span data-ttu-id="bf18e-203">You can do this by using the Azure portal, PowerShell, Azure CLI, or the API.</span><span class="sxs-lookup"><span data-stu-id="bf18e-203">You can do this by using the Azure portal, PowerShell, Azure CLI, or the API.</span></span> <span data-ttu-id="bf18e-204">To learn more, see [resource lock usage](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="bf18e-204">To learn more, see [resource lock usage](../azure-resource-manager/resource-group-lock-resources.md).</span></span> 
    
    <span data-ttu-id="bf18e-205">When you resolve the error by using the steps illustrated in the article, Operations Management Suite extends your alerts into Azure within the next day's scheduled run.</span><span class="sxs-lookup"><span data-stu-id="bf18e-205">When you resolve the error by using the steps illustrated in the article, Operations Management Suite extends your alerts into Azure within the next day's scheduled run.</span></span> <span data-ttu-id="bf18e-206">You don't need to take any further action or initiate anything.</span><span class="sxs-lookup"><span data-stu-id="bf18e-206">You don't need to take any further action or initiate anything.</span></span>

- <span data-ttu-id="bf18e-207">**Error: Policy is present at subscription/resource group level**:   ![Screenshot of the Operations Management Suite portal Alert Settings page, with Policy error message highlighted](./media/monitor-alerts-extend/ErrorPolicy.png)</span><span class="sxs-lookup"><span data-stu-id="bf18e-207">**Error: Policy is present at subscription/resource group level**:   ![Screenshot of the Operations Management Suite portal Alert Settings page, with Policy error message highlighted](./media/monitor-alerts-extend/ErrorPolicy.png)</span></span>

    <span data-ttu-id="bf18e-208">When [Azure Policy](../azure-policy/azure-policy-introduction.md) is applied, it restricts any new resource in a subscription or resource group that contains the Log Analytics (Operations Management Suite) workspace.</span><span class="sxs-lookup"><span data-stu-id="bf18e-208">When [Azure Policy](../azure-policy/azure-policy-introduction.md) is applied, it restricts any new resource in a subscription or resource group that contains the Log Analytics (Operations Management Suite) workspace.</span></span> <span data-ttu-id="bf18e-209">The system is unable to extend alerts into Azure and create necessary action groups.</span><span class="sxs-lookup"><span data-stu-id="bf18e-209">The system is unable to extend alerts into Azure and create necessary action groups.</span></span>
    
    <span data-ttu-id="bf18e-210">To resolve, edit the policy that's causing the *[RequestDisallowedByPolicy](../azure-resource-manager/resource-manager-policy-requestdisallowedbypolicy-error.md)* error, which prevents creation of new resources on your subscription or resource group that contains the workspace.</span><span class="sxs-lookup"><span data-stu-id="bf18e-210">To resolve, edit the policy that's causing the *[RequestDisallowedByPolicy](../azure-resource-manager/resource-manager-policy-requestdisallowedbypolicy-error.md)* error, which prevents creation of new resources on your subscription or resource group that contains the workspace.</span></span> <span data-ttu-id="bf18e-211">You can do this by using the Azure portal, PowerShell, Azure CLI, or the API.</span><span class="sxs-lookup"><span data-stu-id="bf18e-211">You can do this by using the Azure portal, PowerShell, Azure CLI, or the API.</span></span> <span data-ttu-id="bf18e-212">You can audit actions to find the appropriate policy that's causing failure.</span><span class="sxs-lookup"><span data-stu-id="bf18e-212">You can audit actions to find the appropriate policy that's causing failure.</span></span> <span data-ttu-id="bf18e-213">To learn more, see [viewing activity logs to audit actions](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="bf18e-213">To learn more, see [viewing activity logs to audit actions](../azure-resource-manager/resource-group-audit.md).</span></span> 
    
    <span data-ttu-id="bf18e-214">When you resolve the error by using the steps illustrated in the article, Operations Management Suite extends your alerts into Azure within the next day's scheduled run.</span><span class="sxs-lookup"><span data-stu-id="bf18e-214">When you resolve the error by using the steps illustrated in the article, Operations Management Suite extends your alerts into Azure within the next day's scheduled run.</span></span> <span data-ttu-id="bf18e-215">You don't need to take any further action or initiate anything.</span><span class="sxs-lookup"><span data-stu-id="bf18e-215">You don't need to take any further action or initiate anything.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bf18e-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="bf18e-216">Next steps</span></span>

* <span data-ttu-id="bf18e-217">Learn more about the new [Azure Alerts experience](monitoring-overview-unified-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="bf18e-217">Learn more about the new [Azure Alerts experience](monitoring-overview-unified-alerts.md).</span></span>
* <span data-ttu-id="bf18e-218">Learn about [log alerts in Azure Alerts](monitor-alerts-unified-log.md).</span><span class="sxs-lookup"><span data-stu-id="bf18e-218">Learn about [log alerts in Azure Alerts](monitor-alerts-unified-log.md).</span></span>
