---
title: Receive Activity Log Alerts on Service Notifications | Microsoft Docs
description: Get notified via SMS, email or webhook when Azure service occur.
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
ms.openlocfilehash: fd5566e20d5c98c37a2d05aa47592515df9f24cc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564271"
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="d5761-103">Create Activity Log Alerts on Service Notifications</span><span class="sxs-lookup"><span data-stu-id="d5761-103">Create Activity Log Alerts on Service Notifications</span></span>
## <a name="overview"></a><span data-ttu-id="d5761-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d5761-104">Overview</span></span>
<span data-ttu-id="d5761-105">This article shows you how to set up activity log alerts for service health notifications using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d5761-105">This article shows you how to set up activity log alerts for service health notifications using the Azure portal.</span></span>  

<span data-ttu-id="d5761-106">You can receive an alert based on service health notifications for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d5761-106">You can receive an alert based on service health notifications for your Azure subscription.</span></span>  
<span data-ttu-id="d5761-107">You can configure the alert based on:</span><span class="sxs-lookup"><span data-stu-id="d5761-107">You can configure the alert based on:</span></span>
- <span data-ttu-id="d5761-108">The class of service health notification (Incident, Maintenance, Information, etc.)</span><span class="sxs-lookup"><span data-stu-id="d5761-108">The class of service health notification (Incident, Maintenance, Information, etc.)</span></span>
- <span data-ttu-id="d5761-109">The status of the notification (Active vs. Resolved)</span><span class="sxs-lookup"><span data-stu-id="d5761-109">The status of the notification (Active vs. Resolved)</span></span>
- <span data-ttu-id="d5761-110">The level of the notifications (Informational, Warning, Error)</span><span class="sxs-lookup"><span data-stu-id="d5761-110">The level of the notifications (Informational, Warning, Error)</span></span>

<span data-ttu-id="d5761-111">You can also the configure who the alert should be sent to:</span><span class="sxs-lookup"><span data-stu-id="d5761-111">You can also the configure who the alert should be sent to:</span></span>
- <span data-ttu-id="d5761-112">Select an existing Action Group</span><span class="sxs-lookup"><span data-stu-id="d5761-112">Select an existing Action Group</span></span>
- <span data-ttu-id="d5761-113">Create a new Action Group (that can be later used for future alerts)</span><span class="sxs-lookup"><span data-stu-id="d5761-113">Create a new Action Group (that can be later used for future alerts)</span></span>

<span data-ttu-id="d5761-114">You can learn more about Action Groups [here](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="d5761-114">You can learn more about Action Groups [here](monitoring-action-groups.md)</span></span>

<span data-ttu-id="d5761-115">You can configure and get information about service health notification alerts using</span><span class="sxs-lookup"><span data-stu-id="d5761-115">You can configure and get information about service health notification alerts using</span></span>
- [<span data-ttu-id="d5761-116">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d5761-116">Azure Portal</span></span>](monitoring-activity-log-alerts-on-service-notifications.md)
- [<span data-ttu-id="d5761-117">Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="d5761-117">Resource Manager templates</span></span>](monitoring-create-activity-log-alerts-with-resource-manager-template.md)

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-with-the-azure-portal"></a><span data-ttu-id="d5761-118">Create an alert on a service health notification for a new action group with the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d5761-118">Create an alert on a service health notification for a new action group with the Azure Portal</span></span>
1.  <span data-ttu-id="d5761-119">In the [portal](https://portal.azure.com), navigate to the **Monitor** service</span><span class="sxs-lookup"><span data-stu-id="d5761-119">In the [portal](https://portal.azure.com), navigate to the **Monitor** service</span></span>

    ![Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.PNG)

2.  <span data-ttu-id="d5761-121">Click the **Monitor** option to open the Monitor blade.</span><span class="sxs-lookup"><span data-stu-id="d5761-121">Click the **Monitor** option to open the Monitor blade.</span></span> <span data-ttu-id="d5761-122">It first opens to the **Activity log** section.</span><span class="sxs-lookup"><span data-stu-id="d5761-122">It first opens to the **Activity log** section.</span></span>

3.  <span data-ttu-id="d5761-123">Now click on the **Alerts** section.</span><span class="sxs-lookup"><span data-stu-id="d5761-123">Now click on the **Alerts** section.</span></span>

    ![Alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.PNG)

4.  <span data-ttu-id="d5761-125">Select the **Add activity log alert** command and fill in the fields</span><span class="sxs-lookup"><span data-stu-id="d5761-125">Select the **Add activity log alert** command and fill in the fields</span></span>

    ![Add-Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.PNG)

5.  <span data-ttu-id="d5761-127">**Name** your activity log alert, and choose a **Description**.</span><span class="sxs-lookup"><span data-stu-id="d5761-127">**Name** your activity log alert, and choose a **Description**.</span></span> <span data-ttu-id="d5761-128">These will appear in the notifications sent when this alert fires.</span><span class="sxs-lookup"><span data-stu-id="d5761-128">These will appear in the notifications sent when this alert fires.</span></span>

    ![Add-Alert-New-Action-Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.PNG)

6.  <span data-ttu-id="d5761-130">The **Subscription** should be auto filled to the subscription you are currently operating under.</span><span class="sxs-lookup"><span data-stu-id="d5761-130">The **Subscription** should be auto filled to the subscription you are currently operating under.</span></span>

7.  <span data-ttu-id="d5761-131">Choose the **Resource Group** for this alert.</span><span class="sxs-lookup"><span data-stu-id="d5761-131">Choose the **Resource Group** for this alert.</span></span>

8.  <span data-ttu-id="d5761-132">Under **Event Category** select the ‘Service Health’ option.</span><span class="sxs-lookup"><span data-stu-id="d5761-132">Under **Event Category** select the ‘Service Health’ option.</span></span> <span data-ttu-id="d5761-133">Choose for what **Type, Status** and **Level** of Service Health Notifications you would like to be notified.</span><span class="sxs-lookup"><span data-stu-id="d5761-133">Choose for what **Type, Status** and **Level** of Service Health Notifications you would like to be notified.</span></span>

9.  <span data-ttu-id="d5761-134">Create a **New** Action Group by giving it **Name** and **Short Name**; the Short Name will be referenced in the notifications sent when this alert fires.</span><span class="sxs-lookup"><span data-stu-id="d5761-134">Create a **New** Action Group by giving it **Name** and **Short Name**; the Short Name will be referenced in the notifications sent when this alert fires.</span></span>

10. <span data-ttu-id="d5761-135">Then, define a list of receivers by providing the receiver’s</span><span class="sxs-lookup"><span data-stu-id="d5761-135">Then, define a list of receivers by providing the receiver’s</span></span>

    <span data-ttu-id="d5761-136">a.</span><span class="sxs-lookup"><span data-stu-id="d5761-136">a.</span></span> <span data-ttu-id="d5761-137">**Name:** Receiver’s name, alias or identifier.</span><span class="sxs-lookup"><span data-stu-id="d5761-137">**Name:** Receiver’s name, alias or identifier.</span></span>

    <span data-ttu-id="d5761-138">b.</span><span class="sxs-lookup"><span data-stu-id="d5761-138">b.</span></span> <span data-ttu-id="d5761-139">**Action Type:** Choose to contact the receiver via SMS, Email, or Webhook</span><span class="sxs-lookup"><span data-stu-id="d5761-139">**Action Type:** Choose to contact the receiver via SMS, Email, or Webhook</span></span>

    <span data-ttu-id="d5761-140">c.</span><span class="sxs-lookup"><span data-stu-id="d5761-140">c.</span></span> <span data-ttu-id="d5761-141">**Details:** Based on the action type chosen, provide a phone number, email address or webhook URI.</span><span class="sxs-lookup"><span data-stu-id="d5761-141">**Details:** Based on the action type chosen, provide a phone number, email address or webhook URI.</span></span>

11. <span data-ttu-id="d5761-142">Select **OK** when done to create the alert.</span><span class="sxs-lookup"><span data-stu-id="d5761-142">Select **OK** when done to create the alert.</span></span>

<span data-ttu-id="d5761-143">Within a few minutes, the alert is active and triggers as previously described.</span><span class="sxs-lookup"><span data-stu-id="d5761-143">Within a few minutes, the alert is active and triggers as previously described.</span></span>

<span data-ttu-id="d5761-144">For details on the webhook schema for activity log alerts [click here](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="d5761-144">For details on the webhook schema for activity log alerts [click here](monitoring-activity-log-alerts-webhook.md)</span></span>

>[!NOTE]
><span data-ttu-id="d5761-145">The action group defined in these steps will be reusable, as an existing action group, for all future alert definition.</span><span class="sxs-lookup"><span data-stu-id="d5761-145">The action group defined in these steps will be reusable, as an existing action group, for all future alert definition.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-with-the-azure-portal"></a><span data-ttu-id="d5761-146">Create an alert on a service health notification for an existing action group with the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d5761-146">Create an alert on a service health notification for an existing action group with the Azure Portal</span></span>
1.  <span data-ttu-id="d5761-147">In the [portal](https://portal.azure.com), navigate to the **Monitor** service</span><span class="sxs-lookup"><span data-stu-id="d5761-147">In the [portal](https://portal.azure.com), navigate to the **Monitor** service</span></span>

    ![Monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.PNG)
2.  <span data-ttu-id="d5761-149">Click the **Monitor** option to open the Monitor blade.</span><span class="sxs-lookup"><span data-stu-id="d5761-149">Click the **Monitor** option to open the Monitor blade.</span></span> <span data-ttu-id="d5761-150">It first opens to the **Activity log** section.</span><span class="sxs-lookup"><span data-stu-id="d5761-150">It first opens to the **Activity log** section.</span></span>

3.  <span data-ttu-id="d5761-151">Now click on the **Alerts** section.</span><span class="sxs-lookup"><span data-stu-id="d5761-151">Now click on the **Alerts** section.</span></span>

    ![Alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.PNG)
4.  <span data-ttu-id="d5761-153">Select the **Add activity log alert** command and fill in the fields</span><span class="sxs-lookup"><span data-stu-id="d5761-153">Select the **Add activity log alert** command and fill in the fields</span></span>

    ![Add-Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.PNG)
5.  <span data-ttu-id="d5761-155">**Name** your activity log alert, and choose a **Description**.</span><span class="sxs-lookup"><span data-stu-id="d5761-155">**Name** your activity log alert, and choose a **Description**.</span></span> <span data-ttu-id="d5761-156">These will appear in the notifications sent when this alert fires.</span><span class="sxs-lookup"><span data-stu-id="d5761-156">These will appear in the notifications sent when this alert fires.</span></span>

    ![Add-Alert-Existing-Action-Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-existing-action-group.PNG)
6.  <span data-ttu-id="d5761-158">The **Subscription** should be auto filled to the subscription you are currently operating under.</span><span class="sxs-lookup"><span data-stu-id="d5761-158">The **Subscription** should be auto filled to the subscription you are currently operating under.</span></span>

7.  <span data-ttu-id="d5761-159">Choose the **Resource Group** for this alert.</span><span class="sxs-lookup"><span data-stu-id="d5761-159">Choose the **Resource Group** for this alert.</span></span>

8.  <span data-ttu-id="d5761-160">Under **Event Category** select the ‘Service Health’ option.</span><span class="sxs-lookup"><span data-stu-id="d5761-160">Under **Event Category** select the ‘Service Health’ option.</span></span> <span data-ttu-id="d5761-161">Choose for what **Type, Status** and **Level** of Service Health Notifications you would like to be notified.</span><span class="sxs-lookup"><span data-stu-id="d5761-161">Choose for what **Type, Status** and **Level** of Service Health Notifications you would like to be notified.</span></span>

9.  <span data-ttu-id="d5761-162">Choose to **Notify Via** an **Existing action group**.</span><span class="sxs-lookup"><span data-stu-id="d5761-162">Choose to **Notify Via** an **Existing action group**.</span></span> <span data-ttu-id="d5761-163">Select the respective action group.</span><span class="sxs-lookup"><span data-stu-id="d5761-163">Select the respective action group.</span></span>

10. <span data-ttu-id="d5761-164">Select **OK** when done to create the alert.</span><span class="sxs-lookup"><span data-stu-id="d5761-164">Select **OK** when done to create the alert.</span></span>

<span data-ttu-id="d5761-165">Within a few minutes, the alert is active and triggers as previously described.</span><span class="sxs-lookup"><span data-stu-id="d5761-165">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="d5761-166">Managing your alerts</span><span class="sxs-lookup"><span data-stu-id="d5761-166">Managing your alerts</span></span>

<span data-ttu-id="d5761-167">Once you have created an alert, it will be visible in the Alerts section of the Monitor service.</span><span class="sxs-lookup"><span data-stu-id="d5761-167">Once you have created an alert, it will be visible in the Alerts section of the Monitor service.</span></span> <span data-ttu-id="d5761-168">Select the alert you wish to manage, you will be able to:</span><span class="sxs-lookup"><span data-stu-id="d5761-168">Select the alert you wish to manage, you will be able to:</span></span>
* <span data-ttu-id="d5761-169">**Edit** it.</span><span class="sxs-lookup"><span data-stu-id="d5761-169">**Edit** it.</span></span>
* <span data-ttu-id="d5761-170">**Delete** it.</span><span class="sxs-lookup"><span data-stu-id="d5761-170">**Delete** it.</span></span>
* <span data-ttu-id="d5761-171">**Disable** or **Enable** it if you want to temporarily stop of resume receiving notifications for the alert.</span><span class="sxs-lookup"><span data-stu-id="d5761-171">**Disable** or **Enable** it if you want to temporarily stop of resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5761-172">Next Steps:</span><span class="sxs-lookup"><span data-stu-id="d5761-172">Next Steps:</span></span>
<span data-ttu-id="d5761-173">Learn about [Service Health Notifications](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="d5761-173">Learn about [Service Health Notifications](monitoring-service-notifications.md)</span></span>  
<span data-ttu-id="d5761-174">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md) Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span><span class="sxs-lookup"><span data-stu-id="d5761-174">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md) Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span></span>  
<span data-ttu-id="d5761-175">Learn more about [action groups](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="d5761-175">Learn more about [action groups](monitoring-action-groups.md)</span></span>








