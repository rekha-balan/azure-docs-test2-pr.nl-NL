---
title: Create Activity Log Alerts | Microsoft Docs
description: Be notified via SMS, webhook, and email when certain events occur in the Activity log.
author: anirudhcavale
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ''
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 5381f628da167559dc649a0ac28eb6ba1a64922a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564390"
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="b1310-103">Create Activity Log Alerts</span><span class="sxs-lookup"><span data-stu-id="b1310-103">Create Activity Log Alerts</span></span>

## <a name="overview"></a><span data-ttu-id="b1310-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b1310-104">Overview</span></span>
<span data-ttu-id="b1310-105">Activity Log Alerts are Azure resources so they can be managed using the Azure portal or the Azure Resource Manager (ARM).</span><span class="sxs-lookup"><span data-stu-id="b1310-105">Activity Log Alerts are Azure resources so they can be managed using the Azure portal or the Azure Resource Manager (ARM).</span></span> <span data-ttu-id="b1310-106">This article shows you how to use the Azure portal to set up alerts on activity log events.</span><span class="sxs-lookup"><span data-stu-id="b1310-106">This article shows you how to use the Azure portal to set up alerts on activity log events.</span></span>

<span data-ttu-id="b1310-107">You can receive alerts about operations that were performed on resources in your subscription or about service health events that may impact the health of your resources.</span><span class="sxs-lookup"><span data-stu-id="b1310-107">You can receive alerts about operations that were performed on resources in your subscription or about service health events that may impact the health of your resources.</span></span> <span data-ttu-id="b1310-108">An Activity Log Alert monitors the activity log events for the specific subscription the alert is deployed to.</span><span class="sxs-lookup"><span data-stu-id="b1310-108">An Activity Log Alert monitors the activity log events for the specific subscription the alert is deployed to.</span></span>

<span data-ttu-id="b1310-109">You can configure the alert based on:</span><span class="sxs-lookup"><span data-stu-id="b1310-109">You can configure the alert based on:</span></span>
* <span data-ttu-id="b1310-110">Event Category (for [service health events click here](monitoring-activity-log-alerts-on-service-notifications.md))</span><span class="sxs-lookup"><span data-stu-id="b1310-110">Event Category (for [service health events click here](monitoring-activity-log-alerts-on-service-notifications.md))</span></span>
- <span data-ttu-id="b1310-111">Resource Group</span><span class="sxs-lookup"><span data-stu-id="b1310-111">Resource Group</span></span>
- <span data-ttu-id="b1310-112">Resource</span><span class="sxs-lookup"><span data-stu-id="b1310-112">Resource</span></span>
- <span data-ttu-id="b1310-113">Resource Type</span><span class="sxs-lookup"><span data-stu-id="b1310-113">Resource Type</span></span>
- <span data-ttu-id="b1310-114">Operation name</span><span class="sxs-lookup"><span data-stu-id="b1310-114">Operation name</span></span>
- <span data-ttu-id="b1310-115">The level of the notifications (Verbose, Informational, Warning, Error, Critical)</span><span class="sxs-lookup"><span data-stu-id="b1310-115">The level of the notifications (Verbose, Informational, Warning, Error, Critical)</span></span>
- <span data-ttu-id="b1310-116">Status</span><span class="sxs-lookup"><span data-stu-id="b1310-116">Status</span></span>
- <span data-ttu-id="b1310-117">Event initiated by</span><span class="sxs-lookup"><span data-stu-id="b1310-117">Event initiated by</span></span>

<span data-ttu-id="b1310-118">You can also the configure who the alert should be sent to:</span><span class="sxs-lookup"><span data-stu-id="b1310-118">You can also the configure who the alert should be sent to:</span></span>
* <span data-ttu-id="b1310-119">Select an existing Action Group</span><span class="sxs-lookup"><span data-stu-id="b1310-119">Select an existing Action Group</span></span>
- <span data-ttu-id="b1310-120">Create a new Action Group (that can be later used for future alerts)</span><span class="sxs-lookup"><span data-stu-id="b1310-120">Create a new Action Group (that can be later used for future alerts)</span></span>

<span data-ttu-id="b1310-121">You can learn more about [Action Groups here](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="b1310-121">You can learn more about [Action Groups here](monitoring-action-groups.md)</span></span>

<span data-ttu-id="b1310-122">You can configure and get information about service health notification alerts using</span><span class="sxs-lookup"><span data-stu-id="b1310-122">You can configure and get information about service health notification alerts using</span></span>
* [<span data-ttu-id="b1310-123">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b1310-123">Azure Portal</span></span>](monitoring-activity-log-alerts.md)
- [<span data-ttu-id="b1310-124">Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="b1310-124">Resource Manager templates</span></span>](monitoring-create-activity-log-alerts-with-resource-manager-template.md)

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-with-the-azure-portal"></a><span data-ttu-id="b1310-125">Create an alert on an activity log event with a new action group with the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b1310-125">Create an alert on an activity log event with a new action group with the Azure Portal</span></span>
1.  <span data-ttu-id="b1310-126">In the [portal](https://portal.azure.com), navigate to the **Monitor** service</span><span class="sxs-lookup"><span data-stu-id="b1310-126">In the [portal](https://portal.azure.com), navigate to the **Monitor** service</span></span>

    ![Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts/home-monitor.PNG)
2.  <span data-ttu-id="b1310-128">Click the **Monitor** option to open the Monitor blade.</span><span class="sxs-lookup"><span data-stu-id="b1310-128">Click the **Monitor** option to open the Monitor blade.</span></span> <span data-ttu-id="b1310-129">It first opens to the **Activity log** section.</span><span class="sxs-lookup"><span data-stu-id="b1310-129">It first opens to the **Activity log** section.</span></span>

3.  <span data-ttu-id="b1310-130">Now click on the **Alerts** section.</span><span class="sxs-lookup"><span data-stu-id="b1310-130">Now click on the **Alerts** section.</span></span>

    ![Alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts/alerts-blades.PNG)
4.  <span data-ttu-id="b1310-132">Select the **Add activity log alert** command and fill in the fields</span><span class="sxs-lookup"><span data-stu-id="b1310-132">Select the **Add activity log alert** command and fill in the fields</span></span>

5.  <span data-ttu-id="b1310-133">**Name** your activity log alert, and choose a **Description**.</span><span class="sxs-lookup"><span data-stu-id="b1310-133">**Name** your activity log alert, and choose a **Description**.</span></span> <span data-ttu-id="b1310-134">These will appear in the notifications sent when this alert fires.</span><span class="sxs-lookup"><span data-stu-id="b1310-134">These will appear in the notifications sent when this alert fires.</span></span>

    ![Add-Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts/add-activity-log-alert.PNG)

6.  <span data-ttu-id="b1310-136">The **Subscription** should be auto filled to the subscription you are currently operating under.</span><span class="sxs-lookup"><span data-stu-id="b1310-136">The **Subscription** should be auto filled to the subscription you are currently operating under.</span></span> <span data-ttu-id="b1310-137">This is the subscription the alert resource will be deployed to and monitor.</span><span class="sxs-lookup"><span data-stu-id="b1310-137">This is the subscription the alert resource will be deployed to and monitor.</span></span>

    ![Add-Alert-New-Action-Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.PNG)

7.  <span data-ttu-id="b1310-139">Choose the **Resource Group** this alert will be associated with in the **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="b1310-139">Choose the **Resource Group** this alert will be associated with in the **Subscription**.</span></span>

8.  <span data-ttu-id="b1310-140">Provide the **Event Category**, **Resource Group**, **Resource**, **Resource Type**, **Operation Name**, **Level**, **Status** and **Event intiated by** values to identify which events this alert should monitor.</span><span class="sxs-lookup"><span data-stu-id="b1310-140">Provide the **Event Category**, **Resource Group**, **Resource**, **Resource Type**, **Operation Name**, **Level**, **Status** and **Event intiated by** values to identify which events this alert should monitor.</span></span>

9.  <span data-ttu-id="b1310-141">Create a **New** Action Group by giving it **Name** and **Short Name**; the Short Name will be referenced in the notifications sent when this alert is activated.</span><span class="sxs-lookup"><span data-stu-id="b1310-141">Create a **New** Action Group by giving it **Name** and **Short Name**; the Short Name will be referenced in the notifications sent when this alert is activated.</span></span>

10. <span data-ttu-id="b1310-142">Then, define a list of receivers by providing the receiver’s</span><span class="sxs-lookup"><span data-stu-id="b1310-142">Then, define a list of receivers by providing the receiver’s</span></span>

    <span data-ttu-id="b1310-143">a.</span><span class="sxs-lookup"><span data-stu-id="b1310-143">a.</span></span> <span data-ttu-id="b1310-144">**Name:** Receiver’s name, alias or identifier.</span><span class="sxs-lookup"><span data-stu-id="b1310-144">**Name:** Receiver’s name, alias or identifier.</span></span>

    <span data-ttu-id="b1310-145">b.</span><span class="sxs-lookup"><span data-stu-id="b1310-145">b.</span></span> <span data-ttu-id="b1310-146">**Action Type:** Choose to contact the receiver via SMS, Email, or Webhook</span><span class="sxs-lookup"><span data-stu-id="b1310-146">**Action Type:** Choose to contact the receiver via SMS, Email, or Webhook</span></span>

    <span data-ttu-id="b1310-147">c.</span><span class="sxs-lookup"><span data-stu-id="b1310-147">c.</span></span> <span data-ttu-id="b1310-148">**Details:** Based on the action type chosen, provide a phone number, email address or webhook URI.</span><span class="sxs-lookup"><span data-stu-id="b1310-148">**Details:** Based on the action type chosen, provide a phone number, email address or webhook URI.</span></span>

11. <span data-ttu-id="b1310-149">Select **OK** when done to create the alert.</span><span class="sxs-lookup"><span data-stu-id="b1310-149">Select **OK** when done to create the alert.</span></span>

<span data-ttu-id="b1310-150">Within a few minutes, the alert is active and triggers as previously described.</span><span class="sxs-lookup"><span data-stu-id="b1310-150">Within a few minutes, the alert is active and triggers as previously described.</span></span>

<span data-ttu-id="b1310-151">For details on the webhook schema for activity log alerts [click here](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="b1310-151">For details on the webhook schema for activity log alerts [click here](monitoring-activity-log-alerts-webhook.md)</span></span>

>[!NOTE]
><span data-ttu-id="b1310-152">The action group defined in these steps will be reusable, as an existing action group, for all future alert definition.</span><span class="sxs-lookup"><span data-stu-id="b1310-152">The action group defined in these steps will be reusable, as an existing action group, for all future alert definition.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-with-the-azure-portal"></a><span data-ttu-id="b1310-153">Create an alert on an activity log event for an existing action group with the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b1310-153">Create an alert on an activity log event for an existing action group with the Azure Portal</span></span>
1.  <span data-ttu-id="b1310-154">In the [portal](https://portal.azure.com), navigate to the **Monitor** service</span><span class="sxs-lookup"><span data-stu-id="b1310-154">In the [portal](https://portal.azure.com), navigate to the **Monitor** service</span></span>

    ![Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts/home-monitor.PNG)
2.  <span data-ttu-id="b1310-156">Click the **Monitor** option to open the Monitor blade.</span><span class="sxs-lookup"><span data-stu-id="b1310-156">Click the **Monitor** option to open the Monitor blade.</span></span> <span data-ttu-id="b1310-157">It first opens to the **Activity log** section.</span><span class="sxs-lookup"><span data-stu-id="b1310-157">It first opens to the **Activity log** section.</span></span>

3.  <span data-ttu-id="b1310-158">Now click on the **Alerts** section.</span><span class="sxs-lookup"><span data-stu-id="b1310-158">Now click on the **Alerts** section.</span></span>

    ![Alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts/alerts-blades.PNG)
4.  <span data-ttu-id="b1310-160">Select the **Add activity log alert** command and fill in the fields</span><span class="sxs-lookup"><span data-stu-id="b1310-160">Select the **Add activity log alert** command and fill in the fields</span></span>

5.  <span data-ttu-id="b1310-161">**Name** your activity log alert, and choose a **Description**.</span><span class="sxs-lookup"><span data-stu-id="b1310-161">**Name** your activity log alert, and choose a **Description**.</span></span> <span data-ttu-id="b1310-162">These will appear in the notifications sent when this alert fires.</span><span class="sxs-lookup"><span data-stu-id="b1310-162">These will appear in the notifications sent when this alert fires.</span></span>

    ![Add-Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts/add-activity-log-alert.PNG)
6.  <span data-ttu-id="b1310-164">The **Subscription** should be auto filled to the subscription you are currently operating under.</span><span class="sxs-lookup"><span data-stu-id="b1310-164">The **Subscription** should be auto filled to the subscription you are currently operating under.</span></span>

    ![Add-Alert-Existing-Action-Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts/activity-log-alert-existing-action-group.PNG)
7.  <span data-ttu-id="b1310-166">Choose the **Resource Group** for this alert.</span><span class="sxs-lookup"><span data-stu-id="b1310-166">Choose the **Resource Group** for this alert.</span></span>

8.  <span data-ttu-id="b1310-167">Provide the **Event Category**, **Resource Group**, **Resource**, **Resource Type**, **Operation Name**, **Level**, **Status** and **Event intiated by** values to scope for what events this alert should apply.</span><span class="sxs-lookup"><span data-stu-id="b1310-167">Provide the **Event Category**, **Resource Group**, **Resource**, **Resource Type**, **Operation Name**, **Level**, **Status** and **Event intiated by** values to scope for what events this alert should apply.</span></span>

9.  <span data-ttu-id="b1310-168">Choose to **Notify Via** an **Existing action group**.</span><span class="sxs-lookup"><span data-stu-id="b1310-168">Choose to **Notify Via** an **Existing action group**.</span></span> <span data-ttu-id="b1310-169">Select the respective action group.</span><span class="sxs-lookup"><span data-stu-id="b1310-169">Select the respective action group.</span></span>

10. <span data-ttu-id="b1310-170">Select **OK** when done to create the alert.</span><span class="sxs-lookup"><span data-stu-id="b1310-170">Select **OK** when done to create the alert.</span></span>

<span data-ttu-id="b1310-171">Within a few minutes, the alert is active and triggers as previously described.</span><span class="sxs-lookup"><span data-stu-id="b1310-171">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="b1310-172">Managing your alerts</span><span class="sxs-lookup"><span data-stu-id="b1310-172">Managing your alerts</span></span>

<span data-ttu-id="b1310-173">Once you have created an alert, it will be visible in the Alerts section of the Monitor service.</span><span class="sxs-lookup"><span data-stu-id="b1310-173">Once you have created an alert, it will be visible in the Alerts section of the Monitor service.</span></span> <span data-ttu-id="b1310-174">Select the alert you wish to manage, you will be able to:</span><span class="sxs-lookup"><span data-stu-id="b1310-174">Select the alert you wish to manage, you will be able to:</span></span>
* <span data-ttu-id="b1310-175">**Edit** it.</span><span class="sxs-lookup"><span data-stu-id="b1310-175">**Edit** it.</span></span>
* <span data-ttu-id="b1310-176">**Delete** it.</span><span class="sxs-lookup"><span data-stu-id="b1310-176">**Delete** it.</span></span>
* <span data-ttu-id="b1310-177">**Disable** or **Enable** it if you want to temporarily stop of resume receiving notifications for the alert.</span><span class="sxs-lookup"><span data-stu-id="b1310-177">**Disable** or **Enable** it if you want to temporarily stop of resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1310-178">Next Steps:</span><span class="sxs-lookup"><span data-stu-id="b1310-178">Next Steps:</span></span>
<span data-ttu-id="b1310-179">Get an [overview of alerts](monitoring-overview-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="b1310-179">Get an [overview of alerts](monitoring-overview-alerts.md)</span></span>  
<span data-ttu-id="b1310-180">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md) Learn more about [action groups](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="b1310-180">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md) Learn more about [action groups](monitoring-action-groups.md)</span></span>  
<span data-ttu-id="b1310-181">Learn about [Service Health Notifications](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="b1310-181">Learn about [Service Health Notifications](monitoring-service-notifications.md)</span></span>








