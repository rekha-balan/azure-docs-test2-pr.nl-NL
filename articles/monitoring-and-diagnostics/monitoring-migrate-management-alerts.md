---
title: Migrate Azure alerts on management events to Activity Log alerts
description: Alerts on management events will be removed on October 1. Prepare by migrating exisiting alerts.
author: johnkemnetz
services: monitoring
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 08/14/2017
ms.author: johnkem
ms.component: alerts
ms.openlocfilehash: 9e4302b780d0c08afbc791a0aec6bfd806aba161
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870582"
---
# <a name="migrate-azure-alerts-on-management-events-to-activity-log-alerts"></a><span data-ttu-id="e799d-104">Migrate Azure alerts on management events to Activity Log alerts</span><span class="sxs-lookup"><span data-stu-id="e799d-104">Migrate Azure alerts on management events to Activity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="e799d-105">Alerts on management events will be turned off on or after October 1.</span><span class="sxs-lookup"><span data-stu-id="e799d-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="e799d-106">Use the directions below to understand if you have these alerts and migrate them if so.</span><span class="sxs-lookup"><span data-stu-id="e799d-106">Use the directions below to understand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="e799d-107">What is changing</span><span class="sxs-lookup"><span data-stu-id="e799d-107">What is changing</span></span>

<span data-ttu-id="e799d-108">Azure Monitor (formerly Azure Insights) offered a capability to create an alert that triggered off of management events and generated notifications to a webhook URL or email addresses.</span><span class="sxs-lookup"><span data-stu-id="e799d-108">Azure Monitor (formerly Azure Insights) offered a capability to create an alert that triggered off of management events and generated notifications to a webhook URL or email addresses.</span></span> <span data-ttu-id="e799d-109">You may have created one of these alerts any of these ways:</span><span class="sxs-lookup"><span data-stu-id="e799d-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="e799d-110">In the Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set to “Events”</span><span class="sxs-lookup"><span data-stu-id="e799d-110">In the Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set to “Events”</span></span>
* <span data-ttu-id="e799d-111">By running the Add-AzureRmLogAlertRule PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="e799d-111">By running the Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="e799d-112">By directly using [the alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span><span class="sxs-lookup"><span data-stu-id="e799d-112">By directly using [the alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="e799d-113">The following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as the conditions set on each alert.</span><span class="sxs-lookup"><span data-stu-id="e799d-113">The following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as the conditions set on each alert.</span></span>

```powershell
Connect-AzureRmAccount
$alerts = $null
foreach ($rg in Get-AzureRmResourceGroup ) {
  $alerts += Get-AzureRmAlertRule -ResourceGroup $rg.ResourceGroupName
}
foreach ($alert in $alerts) {
  if($alert.Properties.Condition.DataSource.GetType().Name.Equals("RuleManagementEventDataSource")) {
    "Alert Name: " + $alert.Name
    "Alert Resource ID: " + $alert.Id
    "Alert conditions:"
    $alert.Properties.Condition.DataSource
    "---------------------------------"
  }
} 
```

<span data-ttu-id="e799d-114">If you have no alerts on management events, the PowerShell cmdlet above will output a series of warning messages like this one:</span><span class="sxs-lookup"><span data-stu-id="e799d-114">If you have no alerts on management events, the PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: The output of this cmdlet will be flattened, i.e. elimination of the properties field, in a future release to improve the user experience.`

<span data-ttu-id="e799d-115">These warning messages can be ignored.</span><span class="sxs-lookup"><span data-stu-id="e799d-115">These warning messages can be ignored.</span></span> <span data-ttu-id="e799d-116">If you do have alerts on management events, the output of this PowerShell cmdlet will look like this:</span><span class="sxs-lookup"><span data-stu-id="e799d-116">If you do have alerts on management events, the output of this PowerShell cmdlet will look like this:</span></span>

```
Alert Name: webhookEvent1
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/webhookEvent1
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : microsoft.web/sites/start/action
ResourceGroupName    : 
ResourceProviderName : 
Status               : succeeded
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Web/sites/samplealertapp

---------------------------------
Alert Name: someclilogalert
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/someclilogalert
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : Start
ResourceGroupName    : 
ResourceProviderName : 
Status               : 
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Compute/virtualMachines/Seaofclouds

---------------------------------
```

<span data-ttu-id="e799d-117">Each alert is separated by a dashed line and details include the resource ID of the alert and the specific rule being monitored.</span><span class="sxs-lookup"><span data-stu-id="e799d-117">Each alert is separated by a dashed line and details include the resource ID of the alert and the specific rule being monitored.</span></span>

<span data-ttu-id="e799d-118">This functionality has been transitioned to [Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e799d-118">This functionality has been transitioned to [Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="e799d-119">These new alerts enable you to set a condition on Activity Log events and receive a notification when a new event matches the condition.</span><span class="sxs-lookup"><span data-stu-id="e799d-119">These new alerts enable you to set a condition on Activity Log events and receive a notification when a new event matches the condition.</span></span> <span data-ttu-id="e799d-120">They also offer several improvements from alerts on management events:</span><span class="sxs-lookup"><span data-stu-id="e799d-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="e799d-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing the complexity of changing who should receive an alert.</span><span class="sxs-lookup"><span data-stu-id="e799d-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing the complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="e799d-122">You can receive a notification directly on your phone using SMS with Action Groups.</span><span class="sxs-lookup"><span data-stu-id="e799d-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="e799d-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="e799d-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="e799d-124">You can create conditions with greater flexibility and complexity to meet your specific needs.</span><span class="sxs-lookup"><span data-stu-id="e799d-124">You can create conditions with greater flexibility and complexity to meet your specific needs.</span></span>
* <span data-ttu-id="e799d-125">Notifications are delivered more quickly.</span><span class="sxs-lookup"><span data-stu-id="e799d-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-to-migrate"></a><span data-ttu-id="e799d-126">How to migrate</span><span class="sxs-lookup"><span data-stu-id="e799d-126">How to migrate</span></span>
 
<span data-ttu-id="e799d-127">To create a new Activity Log Alert, you can either:</span><span class="sxs-lookup"><span data-stu-id="e799d-127">To create a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="e799d-128">Follow [our guide on how to create an alert in the Azure portal](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="e799d-128">Follow [our guide on how to create an alert in the Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="e799d-129">Learn how to [create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="e799d-129">Learn how to [create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="e799d-130">Alerts on management events that you have previously created will not be automatically migrated to Activity Log Alerts.</span><span class="sxs-lookup"><span data-stu-id="e799d-130">Alerts on management events that you have previously created will not be automatically migrated to Activity Log Alerts.</span></span> <span data-ttu-id="e799d-131">You need to use the preceding PowerShell script to list the alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span><span class="sxs-lookup"><span data-stu-id="e799d-131">You need to use the preceding PowerShell script to list the alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="e799d-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e799d-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="e799d-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span><span class="sxs-lookup"><span data-stu-id="e799d-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="e799d-134">If you have any questions, post in the comments below.</span><span class="sxs-lookup"><span data-stu-id="e799d-134">If you have any questions, post in the comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e799d-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="e799d-135">Next steps</span></span>

* <span data-ttu-id="e799d-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="e799d-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="e799d-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="e799d-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="e799d-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="e799d-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="e799d-139">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="e799d-139">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="e799d-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="e799d-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="e799d-141">Learn more about [Action Groups](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="e799d-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
