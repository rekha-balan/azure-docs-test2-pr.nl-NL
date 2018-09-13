---
title: Stream the Azure Activity Log to Event Hubs
description: Learn how to stream the Azure Activity Log to Event Hubs.
author: johnkemnetz
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 07/25/2018
ms.author: johnkem
ms.component: activitylog
ms.openlocfilehash: 7a5372174fcc7cd9552c00c9d283772c9863b815
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805225"
---
# <a name="stream-the-azure-activity-log-to-event-hubs"></a><span data-ttu-id="21332-103">Stream the Azure Activity Log to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="21332-103">Stream the Azure Activity Log to Event Hubs</span></span>
<span data-ttu-id="21332-104">You can stream the [Azure Activity Log](monitoring-overview-activity-logs.md) in near real time to any application by either:</span><span class="sxs-lookup"><span data-stu-id="21332-104">You can stream the [Azure Activity Log](monitoring-overview-activity-logs.md) in near real time to any application by either:</span></span>

* <span data-ttu-id="21332-105">Using the built-in **Export** option in the portal</span><span class="sxs-lookup"><span data-stu-id="21332-105">Using the built-in **Export** option in the portal</span></span>
* <span data-ttu-id="21332-106">Enabling the Azure Service Bus rule ID in a log profile via the Azure PowerShell cmdlets or Azure CLI</span><span class="sxs-lookup"><span data-stu-id="21332-106">Enabling the Azure Service Bus rule ID in a log profile via the Azure PowerShell cmdlets or Azure CLI</span></span>

## <a name="what-you-can-do-with-the-activity-log-and-event-hubs"></a><span data-ttu-id="21332-107">What you can do with the Activity Log and Event Hubs</span><span class="sxs-lookup"><span data-stu-id="21332-107">What you can do with the Activity Log and Event Hubs</span></span>
<span data-ttu-id="21332-108">Here are two ways you might use the streaming capability for the Activity Log:</span><span class="sxs-lookup"><span data-stu-id="21332-108">Here are two ways you might use the streaming capability for the Activity Log:</span></span>

* <span data-ttu-id="21332-109">**Stream to third-party logging and telemetry systems**: Over time, Azure Event Hubs streaming will become the mechanism to pipe your Activity Log into third-party SIEMs and log analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="21332-109">**Stream to third-party logging and telemetry systems**: Over time, Azure Event Hubs streaming will become the mechanism to pipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="21332-110">**Build a custom telemetry and logging platform**: If you already have a custom-built telemetry platform or are thinking about building one, the highly scalable publish-subscribe nature of Event Hubs enables you to flexibly ingest the activity log.</span><span class="sxs-lookup"><span data-stu-id="21332-110">**Build a custom telemetry and logging platform**: If you already have a custom-built telemetry platform or are thinking about building one, the highly scalable publish-subscribe nature of Event Hubs enables you to flexibly ingest the activity log.</span></span> <span data-ttu-id="21332-111">For more information, see [Dan Rosanova’s video about using Event Hubs in a global-scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="21332-111">For more information, see [Dan Rosanova’s video about using Event Hubs in a global-scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-the-activity-log"></a><span data-ttu-id="21332-112">Enable streaming of the Activity Log</span><span class="sxs-lookup"><span data-stu-id="21332-112">Enable streaming of the Activity Log</span></span>
<span data-ttu-id="21332-113">You can enable streaming of the Activity Log either programmatically or via the portal.</span><span class="sxs-lookup"><span data-stu-id="21332-113">You can enable streaming of the Activity Log either programmatically or via the portal.</span></span> <span data-ttu-id="21332-114">Either way, you pick an Event Hubs namespace and a shared access policy for that namespace.</span><span class="sxs-lookup"><span data-stu-id="21332-114">Either way, you pick an Event Hubs namespace and a shared access policy for that namespace.</span></span> <span data-ttu-id="21332-115">An event hub with the name insights-logs-operationallogs is created in that namespace when the first new Activity Log event occurs.</span><span class="sxs-lookup"><span data-stu-id="21332-115">An event hub with the name insights-logs-operationallogs is created in that namespace when the first new Activity Log event occurs.</span></span> 

<span data-ttu-id="21332-116">If you don't have an Event Hubs namespace, you first need to create one.</span><span class="sxs-lookup"><span data-stu-id="21332-116">If you don't have an Event Hubs namespace, you first need to create one.</span></span> <span data-ttu-id="21332-117">If you previously streamed Activity Log events to this Event Hubs namespace, the event hub that was previously created will be reused.</span><span class="sxs-lookup"><span data-stu-id="21332-117">If you previously streamed Activity Log events to this Event Hubs namespace, the event hub that was previously created will be reused.</span></span> 

<span data-ttu-id="21332-118">The shared access policy defines the permissions that the streaming mechanism has.</span><span class="sxs-lookup"><span data-stu-id="21332-118">The shared access policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="21332-119">Today, streaming to Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span><span class="sxs-lookup"><span data-stu-id="21332-119">Today, streaming to Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="21332-120">You can create or modify shared access policies for the Event Hubs namespace in the Azure portal under the **Configure** tab for your Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="21332-120">You can create or modify shared access policies for the Event Hubs namespace in the Azure portal under the **Configure** tab for your Event Hubs namespace.</span></span> 

<span data-ttu-id="21332-121">To update the Activity Log log profile to include streaming, the user who's making the change must have the ListKey permission on that Event Hubs authorization rule.</span><span class="sxs-lookup"><span data-stu-id="21332-121">To update the Activity Log log profile to include streaming, the user who's making the change must have the ListKey permission on that Event Hubs authorization rule.</span></span> <span data-ttu-id="21332-122">The Event Hubs namespace does not have to be in the same subscription as the subscription that's emitting logs, as long as the user who configures the setting has appropriate RBAC access to both subscriptions and both subscriptions are in the same AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="21332-122">The Event Hubs namespace does not have to be in the same subscription as the subscription that's emitting logs, as long as the user who configures the setting has appropriate RBAC access to both subscriptions and both subscriptions are in the same AAD tenant.</span></span>

### <a name="via-the-azure-portal"></a><span data-ttu-id="21332-123">Via the Azure portal</span><span class="sxs-lookup"><span data-stu-id="21332-123">Via the Azure portal</span></span>
1. <span data-ttu-id="21332-124">Browse to the **Activity Log** section by using the **All services** search on the left side of the portal.</span><span class="sxs-lookup"><span data-stu-id="21332-124">Browse to the **Activity Log** section by using the **All services** search on the left side of the portal.</span></span>
   
   ![Selecting Activity Log from the list of services in the portal](./media/monitoring-stream-activity-logs-event-hubs/activity.png)
2. <span data-ttu-id="21332-126">Select the **Export** button at the top of the log.</span><span class="sxs-lookup"><span data-stu-id="21332-126">Select the **Export** button at the top of the log.</span></span>
   
   ![Export button in the portal](./media/monitoring-stream-activity-logs-event-hubs/export.png)

   <span data-ttu-id="21332-128">Note that the filter settings you had applied while viewing the Activity Log in the previous view have no impact on your export settings.</span><span class="sxs-lookup"><span data-stu-id="21332-128">Note that the filter settings you had applied while viewing the Activity Log in the previous view have no impact on your export settings.</span></span> <span data-ttu-id="21332-129">Those are only for filtering what you see while browsing through your Activity Log in the portal.</span><span class="sxs-lookup"><span data-stu-id="21332-129">Those are only for filtering what you see while browsing through your Activity Log in the portal.</span></span>
3. <span data-ttu-id="21332-130">In the section that appears, select **All regions**.</span><span class="sxs-lookup"><span data-stu-id="21332-130">In the section that appears, select **All regions**.</span></span> <span data-ttu-id="21332-131">Do not select particular regions.</span><span class="sxs-lookup"><span data-stu-id="21332-131">Do not select particular regions.</span></span>
   
   ![Export section](./media/monitoring-stream-activity-logs-event-hubs/export-audit.png)

   > [!WARNING]  
   > <span data-ttu-id="21332-133">If you select anything other than **All regions**, you'll miss key events that you expect to receive.</span><span class="sxs-lookup"><span data-stu-id="21332-133">If you select anything other than **All regions**, you'll miss key events that you expect to receive.</span></span> <span data-ttu-id="21332-134">The Activity Log is a global (non-regional) log, so most events do not have a region associated with them.</span><span class="sxs-lookup"><span data-stu-id="21332-134">The Activity Log is a global (non-regional) log, so most events do not have a region associated with them.</span></span> 
   >

4. <span data-ttu-id="21332-135">Click the **Azure Event Hubs** option, and select an event hubs namespace to which logs should be sent, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="21332-135">Click the **Azure Event Hubs** option, and select an event hubs namespace to which logs should be sent, then click **OK**.</span></span>
5. <span data-ttu-id="21332-136">Select **Save** to save these settings.</span><span class="sxs-lookup"><span data-stu-id="21332-136">Select **Save** to save these settings.</span></span> <span data-ttu-id="21332-137">The settings are immediately applied to your subscription.</span><span class="sxs-lookup"><span data-stu-id="21332-137">The settings are immediately applied to your subscription.</span></span>
6. <span data-ttu-id="21332-138">If you have several subscriptions, repeat this action and send all the data to the same event hub.</span><span class="sxs-lookup"><span data-stu-id="21332-138">If you have several subscriptions, repeat this action and send all the data to the same event hub.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="21332-139">Via PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="21332-139">Via PowerShell cmdlets</span></span>
<span data-ttu-id="21332-140">If a log profile already exists, you first need to remove the existing log profile and then create a new log profile.</span><span class="sxs-lookup"><span data-stu-id="21332-140">If a log profile already exists, you first need to remove the existing log profile and then create a new log profile.</span></span>

1. <span data-ttu-id="21332-141">Use `Get-AzureRmLogProfile` to identify if a log profile exists.</span><span class="sxs-lookup"><span data-stu-id="21332-141">Use `Get-AzureRmLogProfile` to identify if a log profile exists.</span></span>  <span data-ttu-id="21332-142">If a log profile does exist, locate the *name* property.</span><span class="sxs-lookup"><span data-stu-id="21332-142">If a log profile does exist, locate the *name* property.</span></span>
2. <span data-ttu-id="21332-143">Use `Remove-AzureRmLogProfile` to remove the log profile using the value from the *name* property.</span><span class="sxs-lookup"><span data-stu-id="21332-143">Use `Remove-AzureRmLogProfile` to remove the log profile using the value from the *name* property.</span></span>

    ```powershell
    # For example, if the log profile name is 'default'
    Remove-AzureRmLogProfile -Name "default"
    ```
3. <span data-ttu-id="21332-144">Use `Add-AzureRmLogProfile` to create a new log profile:</span><span class="sxs-lookup"><span data-stu-id="21332-144">Use `Add-AzureRmLogProfile` to create a new log profile:</span></span>

   ```powershell
   # Settings needed for the new log profile
   $logProfileName = "default"
   $locations = (Get-AzureRmLocation).Location
   $locations += "global"
   $subscriptionId = "<your Azure subscription Id>"
   $resourceGroupName = "<resource group name your event hub belongs to>"
   $eventHubNamespace = "<event hub namespace>"

   # Build the service bus rule Id from the settings above
   $serviceBusRuleId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.EventHub/namespaces/$eventHubNamespace/authorizationrules/RootManageSharedAccessKey"

   Add-AzureRmLogProfile -Name $logProfileName -Location $locations -ServiceBusRuleId $serviceBusRuleId
   ```

### <a name="via-azure-cli"></a><span data-ttu-id="21332-145">Via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="21332-145">Via Azure CLI</span></span>
<span data-ttu-id="21332-146">If a log profile already exists, you first need to remove the existing log profile and then create a new log profile.</span><span class="sxs-lookup"><span data-stu-id="21332-146">If a log profile already exists, you first need to remove the existing log profile and then create a new log profile.</span></span>

1. <span data-ttu-id="21332-147">Use `az monitor log-profiles list` to identify if a log profile exists.</span><span class="sxs-lookup"><span data-stu-id="21332-147">Use `az monitor log-profiles list` to identify if a log profile exists.</span></span>
2. <span data-ttu-id="21332-148">Use `az monitor log-profiles delete --name "<log profile name>` to remove the log profile using the value from the *name* property.</span><span class="sxs-lookup"><span data-stu-id="21332-148">Use `az monitor log-profiles delete --name "<log profile name>` to remove the log profile using the value from the *name* property.</span></span>
3. <span data-ttu-id="21332-149">Use `az monitor log-profiles create` to create a new log profile:</span><span class="sxs-lookup"><span data-stu-id="21332-149">Use `az monitor log-profiles create` to create a new log profile:</span></span>

   ```azurecli-interactive
   az monitor log-profiles create --name "default" --location null --locations "global" "eastus" "westus" --categories "Delete" "Write" "Action"  --enabled false --days 0 --service-bus-rule-id "/subscriptions/<YOUR SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP NAME>/providers/Microsoft.EventHub/namespaces/<EVENT HUB NAME SPACE>/authorizationrules/RootManageSharedAccessKey"
   ```

## <a name="consume-the-log-data-from-event-hubs"></a><span data-ttu-id="21332-150">Consume the log data from Event Hubs</span><span class="sxs-lookup"><span data-stu-id="21332-150">Consume the log data from Event Hubs</span></span>
<span data-ttu-id="21332-151">The schema for the Activity Log is available in [Monitor subscription activity with the Azure Activity Log](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="21332-151">The schema for the Activity Log is available in [Monitor subscription activity with the Azure Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="21332-152">Each event is in an array of JSON blobs called *records*.</span><span class="sxs-lookup"><span data-stu-id="21332-152">Each event is in an array of JSON blobs called *records*.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21332-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="21332-153">Next steps</span></span>
* [<span data-ttu-id="21332-154">Archive the Activity Log to a storage account</span><span class="sxs-lookup"><span data-stu-id="21332-154">Archive the Activity Log to a storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="21332-155">Read the overview of the Azure Activity Log</span><span class="sxs-lookup"><span data-stu-id="21332-155">Read the overview of the Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="21332-156">Set up an alert based on an Activity Log event</span><span class="sxs-lookup"><span data-stu-id="21332-156">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

