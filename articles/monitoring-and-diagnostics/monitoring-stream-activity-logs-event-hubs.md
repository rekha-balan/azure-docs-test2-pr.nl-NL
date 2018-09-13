---
title: Stream the Azure Activity Log to Event Hubs | Microsoft Docs
description: Learn how to stream the Azure Activity Log to Event Hubs.
author: johnkemnetz
manager: rboucher
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: johnkem
ms.openlocfilehash: e49761aed75be4a3c0a71e2dd399996ace95524e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564534"
---
# <a name="stream-the-azure-activity-log-to-event-hubs"></a><span data-ttu-id="cd072-103">Stream the Azure Activity Log to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cd072-103">Stream the Azure Activity Log to Event Hubs</span></span>
<span data-ttu-id="cd072-104">The [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time to any application using the built-in “Export” option in the portal, or by enabling the Service Bus Rule Id in a Log Profile via the Azure PowerShell Cmdlets or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="cd072-104">The [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time to any application using the built-in “Export” option in the portal, or by enabling the Service Bus Rule Id in a Log Profile via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-the-activity-log-and-event-hubs"></a><span data-ttu-id="cd072-105">What you can do with the Activity Log and Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cd072-105">What you can do with the Activity Log and Event Hubs</span></span>
<span data-ttu-id="cd072-106">Here are just a few ways you might use the streaming capability for the Activity Log:</span><span class="sxs-lookup"><span data-stu-id="cd072-106">Here are just a few ways you might use the streaming capability for the Activity Log:</span></span>

* <span data-ttu-id="cd072-107">**Stream to third-party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your Activity Log into third-party SIEMs and log analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="cd072-107">**Stream to third-party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="cd072-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest the activity log.</span><span class="sxs-lookup"><span data-stu-id="cd072-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest the activity log.</span></span> [<span data-ttu-id="cd072-109">See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here.</span><span class="sxs-lookup"><span data-stu-id="cd072-109">See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-the-activity-log"></a><span data-ttu-id="cd072-110">Enable streaming of the Activity Log</span><span class="sxs-lookup"><span data-stu-id="cd072-110">Enable streaming of the Activity Log</span></span>
<span data-ttu-id="cd072-111">You can enable streaming of the Activity Log either programmatically or via the portal.</span><span class="sxs-lookup"><span data-stu-id="cd072-111">You can enable streaming of the Activity Log either programmatically or via the portal.</span></span> <span data-ttu-id="cd072-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when the first new Activity Log event occurs.</span><span class="sxs-lookup"><span data-stu-id="cd072-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when the first new Activity Log event occurs.</span></span> <span data-ttu-id="cd072-113">If you do not have a Service Bus Namespace, you first need to create one.</span><span class="sxs-lookup"><span data-stu-id="cd072-113">If you do not have a Service Bus Namespace, you first need to create one.</span></span> <span data-ttu-id="cd072-114">If you have previously streamed Activity Log events to this Service Bus Namespace, the Event Hub that was previously created will be reused.</span><span class="sxs-lookup"><span data-stu-id="cd072-114">If you have previously streamed Activity Log events to this Service Bus Namespace, the Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="cd072-115">The shared access policy defines the permissions that the streaming mechanism has.</span><span class="sxs-lookup"><span data-stu-id="cd072-115">The shared access policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="cd072-116">Today, streaming to an Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span><span class="sxs-lookup"><span data-stu-id="cd072-116">Today, streaming to an Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="cd072-117">You can create or modify Service Bus Namespace shared access policies in the classic portal under the “Configure” tab for your Service Bus Namespace.</span><span class="sxs-lookup"><span data-stu-id="cd072-117">You can create or modify Service Bus Namespace shared access policies in the classic portal under the “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="cd072-118">To update the Activity Log log profile to include streaming, the user making the change must have the ListKey permission on that Service Bus Authorization Rule.</span><span class="sxs-lookup"><span data-stu-id="cd072-118">To update the Activity Log log profile to include streaming, the user making the change must have the ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="cd072-119">The service bus or event hub namespace does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span><span class="sxs-lookup"><span data-stu-id="cd072-119">The service bus or event hub namespace does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="cd072-120">Via Azure portal</span><span class="sxs-lookup"><span data-stu-id="cd072-120">Via Azure portal</span></span>
1. <span data-ttu-id="cd072-121">Navigate to the **Activity Log** blade using the menu on the left side of the portal.</span><span class="sxs-lookup"><span data-stu-id="cd072-121">Navigate to the **Activity Log** blade using the menu on the left side of the portal.</span></span>
   
    ![Navigate to Activity Log in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="cd072-123">Click the **Export** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="cd072-123">Click the **Export** button at the top of the blade.</span></span>
   
    ![Export button in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="cd072-125">In the blade that appears, you can select the regions for which you would like to stream events and the Service Bus Namespace in which you would like an Event Hub to be created for streaming these events.</span><span class="sxs-lookup"><span data-stu-id="cd072-125">In the blade that appears, you can select the regions for which you would like to stream events and the Service Bus Namespace in which you would like an Event Hub to be created for streaming these events.</span></span>
   
    ![Export Activity Log blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="cd072-127">Click **Save** to save these settings.</span><span class="sxs-lookup"><span data-stu-id="cd072-127">Click **Save** to save these settings.</span></span> <span data-ttu-id="cd072-128">The settings are immediately be applied to your subscription.</span><span class="sxs-lookup"><span data-stu-id="cd072-128">The settings are immediately be applied to your subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="cd072-129">Via PowerShell Cmdlets</span><span class="sxs-lookup"><span data-stu-id="cd072-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="cd072-130">If a log profile already exists, you first need to remove that profile.</span><span class="sxs-lookup"><span data-stu-id="cd072-130">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="cd072-131">Use `Get-AzureRmLogProfile` to identify if a log profile exists</span><span class="sxs-lookup"><span data-stu-id="cd072-131">Use `Get-AzureRmLogProfile` to identify if a log profile exists</span></span>
2. <span data-ttu-id="cd072-132">If so, use `Remove-AzureRmLogProfile` to remove it.</span><span class="sxs-lookup"><span data-stu-id="cd072-132">If so, use `Remove-AzureRmLogProfile` to remove it.</span></span>
3. <span data-ttu-id="cd072-133">Use `Set-AzureRmLogProfile` to create a profile:</span><span class="sxs-lookup"><span data-stu-id="cd072-133">Use `Set-AzureRmLogProfile` to create a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="cd072-134">The Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span><span class="sxs-lookup"><span data-stu-id="cd072-134">The Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="cd072-135">Via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cd072-135">Via Azure CLI</span></span>
<span data-ttu-id="cd072-136">If a log profile already exists, you first need to remove that profile.</span><span class="sxs-lookup"><span data-stu-id="cd072-136">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="cd072-137">Use `azure insights logprofile list` to identify if a log profile exists</span><span class="sxs-lookup"><span data-stu-id="cd072-137">Use `azure insights logprofile list` to identify if a log profile exists</span></span>
2. <span data-ttu-id="cd072-138">If so, use `azure insights logprofile delete` to remove it.</span><span class="sxs-lookup"><span data-stu-id="cd072-138">If so, use `azure insights logprofile delete` to remove it.</span></span>
3. <span data-ttu-id="cd072-139">Use `azure insights logprofile add` to create a profile:</span><span class="sxs-lookup"><span data-stu-id="cd072-139">Use `azure insights logprofile add` to create a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="cd072-140">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="cd072-140">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="cd072-141">How do I consume the log data from Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="cd072-141">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="cd072-142">[The schema for the Activity Log is available here](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="cd072-142">[The schema for the Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="cd072-143">Each event is in an array of JSON blobs called “records.”</span><span class="sxs-lookup"><span data-stu-id="cd072-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd072-144">Next Steps</span><span class="sxs-lookup"><span data-stu-id="cd072-144">Next Steps</span></span>
* [<span data-ttu-id="cd072-145">Archive the Activity Log to a storage account</span><span class="sxs-lookup"><span data-stu-id="cd072-145">Archive the Activity Log to a storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="cd072-146">Read the overview of the Azure Activity Log</span><span class="sxs-lookup"><span data-stu-id="cd072-146">Read the overview of the Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="cd072-147">Set up an alert based on an Activity Log event</span><span class="sxs-lookup"><span data-stu-id="cd072-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)




