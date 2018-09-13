---
title: Monitor Resource Manager-deployed virtual machine backups | Microsoft Docs
description: Monitor events and alerts from Resource Manager-deployed virtual machine backups. Send email based on alerts.
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: ''
ms.assetid: fed32015-2db2-44f8-b204-d89f6fd1bea2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: markgal;trinadhk;giridham;
ms.openlocfilehash: f3ee76f713d6b0d98a626e3acdabbf3d47dcbbdb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669016"
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a><span data-ttu-id="2a16c-104">Monitor alerts for Azure virtual machine backups</span><span class="sxs-lookup"><span data-stu-id="2a16c-104">Monitor alerts for Azure virtual machine backups</span></span>
<span data-ttu-id="2a16c-105">Alerts are responses from the service that an event threshold has been met or surpassed.</span><span class="sxs-lookup"><span data-stu-id="2a16c-105">Alerts are responses from the service that an event threshold has been met or surpassed.</span></span> <span data-ttu-id="2a16c-106">Knowing when problems start can be critical to keeping business costs down.</span><span class="sxs-lookup"><span data-stu-id="2a16c-106">Knowing when problems start can be critical to keeping business costs down.</span></span> <span data-ttu-id="2a16c-107">Alerts typically do not occur on a schedule, and so it is helpful to know as soon as possible after alerts occur.</span><span class="sxs-lookup"><span data-stu-id="2a16c-107">Alerts typically do not occur on a schedule, and so it is helpful to know as soon as possible after alerts occur.</span></span> <span data-ttu-id="2a16c-108">For example, when a backup or restore job fails, an alert occurs within five minutes of the failure.</span><span class="sxs-lookup"><span data-stu-id="2a16c-108">For example, when a backup or restore job fails, an alert occurs within five minutes of the failure.</span></span> <span data-ttu-id="2a16c-109">In the vault dashboard, the Backup Alerts tile displays Critical and Warning-level events.</span><span class="sxs-lookup"><span data-stu-id="2a16c-109">In the vault dashboard, the Backup Alerts tile displays Critical and Warning-level events.</span></span> <span data-ttu-id="2a16c-110">In the Backup Alerts settings, you can view all events.</span><span class="sxs-lookup"><span data-stu-id="2a16c-110">In the Backup Alerts settings, you can view all events.</span></span> <span data-ttu-id="2a16c-111">But what do you do if an alert occurs when you are working on a separate issue?</span><span class="sxs-lookup"><span data-stu-id="2a16c-111">But what do you do if an alert occurs when you are working on a separate issue?</span></span> <span data-ttu-id="2a16c-112">If you don't know when the alert happens, it could be a minor inconvenience, or it could compromise data.</span><span class="sxs-lookup"><span data-stu-id="2a16c-112">If you don't know when the alert happens, it could be a minor inconvenience, or it could compromise data.</span></span> <span data-ttu-id="2a16c-113">To make sure the correct people are aware of an alert - when it occurs, configure the service to send alert notifications via email.</span><span class="sxs-lookup"><span data-stu-id="2a16c-113">To make sure the correct people are aware of an alert - when it occurs, configure the service to send alert notifications via email.</span></span> <span data-ttu-id="2a16c-114">For details on setting up email notifications, see [Configure notifications](backup-azure-monitor-vms.md#configure-notifications).</span><span class="sxs-lookup"><span data-stu-id="2a16c-114">For details on setting up email notifications, see [Configure notifications](backup-azure-monitor-vms.md#configure-notifications).</span></span>

## <a name="how-do-i-find-information-about-the-alerts"></a><span data-ttu-id="2a16c-115">How do I find information about the alerts?</span><span class="sxs-lookup"><span data-stu-id="2a16c-115">How do I find information about the alerts?</span></span>
<span data-ttu-id="2a16c-116">To view information about the event that threw an alert, you must open the Backup Alerts blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-116">To view information about the event that threw an alert, you must open the Backup Alerts blade.</span></span> <span data-ttu-id="2a16c-117">There are two ways to open the Backup Alerts blade: either from the Backup Alerts tile in the vault dashboard, or from the Alerts and Events blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-117">There are two ways to open the Backup Alerts blade: either from the Backup Alerts tile in the vault dashboard, or from the Alerts and Events blade.</span></span>

<span data-ttu-id="2a16c-118">To open the Backup Alerts blade from Backup Alerts tile:</span><span class="sxs-lookup"><span data-stu-id="2a16c-118">To open the Backup Alerts blade from Backup Alerts tile:</span></span>

* <span data-ttu-id="2a16c-119">On the **Backup Alerts** tile on the vault dashboard, click **Critical** or **Warning** to view the operational events for that severity level.</span><span class="sxs-lookup"><span data-stu-id="2a16c-119">On the **Backup Alerts** tile on the vault dashboard, click **Critical** or **Warning** to view the operational events for that severity level.</span></span>

    ![Backup Alerts tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/backup-alerts-tile.png)

<span data-ttu-id="2a16c-121">To open the Backup Alerts blade from the Alerts and Events blade:</span><span class="sxs-lookup"><span data-stu-id="2a16c-121">To open the Backup Alerts blade from the Alerts and Events blade:</span></span>

1. <span data-ttu-id="2a16c-122">From the vault dashboard, click **All Settings**.</span><span class="sxs-lookup"><span data-stu-id="2a16c-122">From the vault dashboard, click **All Settings**.</span></span> <span data-ttu-id="2a16c-123">![All Settings button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/all-settings-button.png)</span><span class="sxs-lookup"><span data-stu-id="2a16c-123">![All Settings button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/all-settings-button.png)</span></span>
2. <span data-ttu-id="2a16c-124">On the **Settings** blade, click **Alerts and Events**.</span><span class="sxs-lookup"><span data-stu-id="2a16c-124">On the **Settings** blade, click **Alerts and Events**.</span></span> <span data-ttu-id="2a16c-125">![Alerts and Events button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/alerts-and-events-button.png)</span><span class="sxs-lookup"><span data-stu-id="2a16c-125">![Alerts and Events button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/alerts-and-events-button.png)</span></span>
3. <span data-ttu-id="2a16c-126">On the **Alerts and Events** blade, click **Backup Alerts**.</span><span class="sxs-lookup"><span data-stu-id="2a16c-126">On the **Alerts and Events** blade, click **Backup Alerts**.</span></span> <span data-ttu-id="2a16c-127">![Backup Alerts button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/backup-alerts.png)</span><span class="sxs-lookup"><span data-stu-id="2a16c-127">![Backup Alerts button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/backup-alerts.png)</span></span>

    <span data-ttu-id="2a16c-128">The **Backup Alerts** blade opens and displays the filtered alerts.</span><span class="sxs-lookup"><span data-stu-id="2a16c-128">The **Backup Alerts** blade opens and displays the filtered alerts.</span></span>

    ![Backup Alerts tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. <span data-ttu-id="2a16c-130">To view detailed information about a particular alert, from the list of events, click the alert to open its **Details** blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-130">To view detailed information about a particular alert, from the list of events, click the alert to open its **Details** blade.</span></span>

    ![Event Detail](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    <span data-ttu-id="2a16c-132">To customize the attributes displayed in the list, see [View additional event attributes](backup-azure-monitor-vms.md#view-additional-event-attributes)</span><span class="sxs-lookup"><span data-stu-id="2a16c-132">To customize the attributes displayed in the list, see [View additional event attributes](backup-azure-monitor-vms.md#view-additional-event-attributes)</span></span>

## <a name="configure-notifications"></a><span data-ttu-id="2a16c-133">Configure notifications</span><span class="sxs-lookup"><span data-stu-id="2a16c-133">Configure notifications</span></span>
 <span data-ttu-id="2a16c-134">You can configure the service to send email notifications for the alerts that occurred over the past hour, or when particular types of events occur.</span><span class="sxs-lookup"><span data-stu-id="2a16c-134">You can configure the service to send email notifications for the alerts that occurred over the past hour, or when particular types of events occur.</span></span>

<span data-ttu-id="2a16c-135">To set up email notifications for alerts</span><span class="sxs-lookup"><span data-stu-id="2a16c-135">To set up email notifications for alerts</span></span>

1. <span data-ttu-id="2a16c-136">On the Backup Alerts menu, click **Configure notifications**</span><span class="sxs-lookup"><span data-stu-id="2a16c-136">On the Backup Alerts menu, click **Configure notifications**</span></span>

    ![Backup Alerts menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/backup-alerts-menu.png)

    <span data-ttu-id="2a16c-138">The Configure notifications blade opens.</span><span class="sxs-lookup"><span data-stu-id="2a16c-138">The Configure notifications blade opens.</span></span>

    ![Configure notifications blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/configure-notifications.png)
2. <span data-ttu-id="2a16c-140">On the Configure notifications blade, for Email notifications, click **On**.</span><span class="sxs-lookup"><span data-stu-id="2a16c-140">On the Configure notifications blade, for Email notifications, click **On**.</span></span>

    <span data-ttu-id="2a16c-141">The Recipients and Severity dialogs have a star next to them because that information is required.</span><span class="sxs-lookup"><span data-stu-id="2a16c-141">The Recipients and Severity dialogs have a star next to them because that information is required.</span></span> <span data-ttu-id="2a16c-142">Provide at least one email address, and select at least one Severity.</span><span class="sxs-lookup"><span data-stu-id="2a16c-142">Provide at least one email address, and select at least one Severity.</span></span>
3. <span data-ttu-id="2a16c-143">In the **Recipients (Email)** dialog, type the email addresses for who receive the notifications.</span><span class="sxs-lookup"><span data-stu-id="2a16c-143">In the **Recipients (Email)** dialog, type the email addresses for who receive the notifications.</span></span> <span data-ttu-id="2a16c-144">Use the format: username@domainname.com.</span><span class="sxs-lookup"><span data-stu-id="2a16c-144">Use the format: username@domainname.com.</span></span> <span data-ttu-id="2a16c-145">Separate multiple email addresses with a semicolon (;).</span><span class="sxs-lookup"><span data-stu-id="2a16c-145">Separate multiple email addresses with a semicolon (;).</span></span>
4. <span data-ttu-id="2a16c-146">In the **Notify** area, choose **Per Alert** to send notification when the specified alert occurs, or **Hourly Digest** to send a summary for the past hour.</span><span class="sxs-lookup"><span data-stu-id="2a16c-146">In the **Notify** area, choose **Per Alert** to send notification when the specified alert occurs, or **Hourly Digest** to send a summary for the past hour.</span></span>
5. <span data-ttu-id="2a16c-147">In the **Severity** dialog, choose one or more levels that you want to trigger email notification.</span><span class="sxs-lookup"><span data-stu-id="2a16c-147">In the **Severity** dialog, choose one or more levels that you want to trigger email notification.</span></span>
6. <span data-ttu-id="2a16c-148">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2a16c-148">Click **Save**.</span></span>

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a><span data-ttu-id="2a16c-149">What alert types are available for Azure IaaS VM backup?</span><span class="sxs-lookup"><span data-stu-id="2a16c-149">What alert types are available for Azure IaaS VM backup?</span></span>
   | <span data-ttu-id="2a16c-150">Alert Level</span><span class="sxs-lookup"><span data-stu-id="2a16c-150">Alert Level</span></span> | <span data-ttu-id="2a16c-151">Alerts sent</span><span class="sxs-lookup"><span data-stu-id="2a16c-151">Alerts sent</span></span> |
   | --- | --- |
   | <span data-ttu-id="2a16c-152">Critical</span><span class="sxs-lookup"><span data-stu-id="2a16c-152">Critical</span></span> |<span data-ttu-id="2a16c-153">Backup failure, recovery failure</span><span class="sxs-lookup"><span data-stu-id="2a16c-153">Backup failure, recovery failure</span></span> |
   | <span data-ttu-id="2a16c-154">Warning</span><span class="sxs-lookup"><span data-stu-id="2a16c-154">Warning</span></span> |<span data-ttu-id="2a16c-155">None</span><span class="sxs-lookup"><span data-stu-id="2a16c-155">None</span></span> |
   | <span data-ttu-id="2a16c-156">Informational</span><span class="sxs-lookup"><span data-stu-id="2a16c-156">Informational</span></span> |<span data-ttu-id="2a16c-157">None</span><span class="sxs-lookup"><span data-stu-id="2a16c-157">None</span></span> |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a><span data-ttu-id="2a16c-158">Are there situations where email isn't sent even if notifications are configured?</span><span class="sxs-lookup"><span data-stu-id="2a16c-158">Are there situations where email isn't sent even if notifications are configured?</span></span>
<span data-ttu-id="2a16c-159">There are situations where an alert is not sent, even though the notifications have been properly configured.</span><span class="sxs-lookup"><span data-stu-id="2a16c-159">There are situations where an alert is not sent, even though the notifications have been properly configured.</span></span> <span data-ttu-id="2a16c-160">In the following situations email notifications are not sent to avoid alert noise:</span><span class="sxs-lookup"><span data-stu-id="2a16c-160">In the following situations email notifications are not sent to avoid alert noise:</span></span>

* <span data-ttu-id="2a16c-161">If notifications are configured to Hourly Digest, and an alert is raised and resolved within the hour.</span><span class="sxs-lookup"><span data-stu-id="2a16c-161">If notifications are configured to Hourly Digest, and an alert is raised and resolved within the hour.</span></span>
* <span data-ttu-id="2a16c-162">The job is canceled.</span><span class="sxs-lookup"><span data-stu-id="2a16c-162">The job is canceled.</span></span>
* <span data-ttu-id="2a16c-163">A backup job is triggered and then fails, and another backup job is in progress.</span><span class="sxs-lookup"><span data-stu-id="2a16c-163">A backup job is triggered and then fails, and another backup job is in progress.</span></span>
* <span data-ttu-id="2a16c-164">A scheduled backup job for a Resource Manager-enabled VM starts, but the VM no longer exists.</span><span class="sxs-lookup"><span data-stu-id="2a16c-164">A scheduled backup job for a Resource Manager-enabled VM starts, but the VM no longer exists.</span></span>

## <a name="customize-your-view-of-events"></a><span data-ttu-id="2a16c-165">Customize your view of events</span><span class="sxs-lookup"><span data-stu-id="2a16c-165">Customize your view of events</span></span>
<span data-ttu-id="2a16c-166">The **Audit logs** setting comes with a pre-defined set of filters and columns showing operational event information.</span><span class="sxs-lookup"><span data-stu-id="2a16c-166">The **Audit logs** setting comes with a pre-defined set of filters and columns showing operational event information.</span></span> <span data-ttu-id="2a16c-167">You can customize the view so that when the **Events** blade opens, it shows you the information you want.</span><span class="sxs-lookup"><span data-stu-id="2a16c-167">You can customize the view so that when the **Events** blade opens, it shows you the information you want.</span></span>

1. <span data-ttu-id="2a16c-168">In the [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse to and click **Audit Logs** to open the **Events** blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-168">In the [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse to and click **Audit Logs** to open the **Events** blade.</span></span>

    ![Audit Logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    <span data-ttu-id="2a16c-170">The **Events** blade opens to the operational events filtered just for the current vault.</span><span class="sxs-lookup"><span data-stu-id="2a16c-170">The **Events** blade opens to the operational events filtered just for the current vault.</span></span>

    ![Audit Logs Filter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/audit-logs-filter.png)

    <span data-ttu-id="2a16c-172">The blade shows the list of Critical, Error, Warning, and Informational events that occurred in the past week.</span><span class="sxs-lookup"><span data-stu-id="2a16c-172">The blade shows the list of Critical, Error, Warning, and Informational events that occurred in the past week.</span></span> <span data-ttu-id="2a16c-173">The time span is a default value set in the **Filter**.</span><span class="sxs-lookup"><span data-stu-id="2a16c-173">The time span is a default value set in the **Filter**.</span></span> <span data-ttu-id="2a16c-174">The **Events** blade also shows a bar chart tracking when the events occurred.</span><span class="sxs-lookup"><span data-stu-id="2a16c-174">The **Events** blade also shows a bar chart tracking when the events occurred.</span></span> <span data-ttu-id="2a16c-175">If you don't want to see the bar chart, in the **Events** menu, click **Hide chart** to toggle off the chart.</span><span class="sxs-lookup"><span data-stu-id="2a16c-175">If you don't want to see the bar chart, in the **Events** menu, click **Hide chart** to toggle off the chart.</span></span> <span data-ttu-id="2a16c-176">The default view of Events shows Operation, Level, Status, Resource, and Time information.</span><span class="sxs-lookup"><span data-stu-id="2a16c-176">The default view of Events shows Operation, Level, Status, Resource, and Time information.</span></span> <span data-ttu-id="2a16c-177">For information about exposing additional Event attributes, see the section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span><span class="sxs-lookup"><span data-stu-id="2a16c-177">For information about exposing additional Event attributes, see the section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span></span>
2. <span data-ttu-id="2a16c-178">For additional information on an operational event, in the **Operation** column, click an operational event to open its blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-178">For additional information on an operational event, in the **Operation** column, click an operational event to open its blade.</span></span> <span data-ttu-id="2a16c-179">The blade contains detailed information about the events.</span><span class="sxs-lookup"><span data-stu-id="2a16c-179">The blade contains detailed information about the events.</span></span> <span data-ttu-id="2a16c-180">Events are grouped by their correlation ID and a list of the events that occurred in the Time span.</span><span class="sxs-lookup"><span data-stu-id="2a16c-180">Events are grouped by their correlation ID and a list of the events that occurred in the Time span.</span></span>

    ![Operation Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. <span data-ttu-id="2a16c-182">To view detailed information about a particular event, from the list of events, click the event to open its **Details** blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-182">To view detailed information about a particular event, from the list of events, click the event to open its **Details** blade.</span></span>

    ![Event Detail](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    <span data-ttu-id="2a16c-184">The Event-level information is as detailed as the information gets.</span><span class="sxs-lookup"><span data-stu-id="2a16c-184">The Event-level information is as detailed as the information gets.</span></span> <span data-ttu-id="2a16c-185">If you prefer seeing this much information about each event, and would like to add this much detail to the **Events** blade, see the section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span><span class="sxs-lookup"><span data-stu-id="2a16c-185">If you prefer seeing this much information about each event, and would like to add this much detail to the **Events** blade, see the section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span></span>

## <a name="customize-the-event-filter"></a><span data-ttu-id="2a16c-186">Customize the event filter</span><span class="sxs-lookup"><span data-stu-id="2a16c-186">Customize the event filter</span></span>
<span data-ttu-id="2a16c-187">Use the **Filter** to adjust or choose the information that appears in a particular blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-187">Use the **Filter** to adjust or choose the information that appears in a particular blade.</span></span> <span data-ttu-id="2a16c-188">To filter the event information:</span><span class="sxs-lookup"><span data-stu-id="2a16c-188">To filter the event information:</span></span>

1. <span data-ttu-id="2a16c-189">In the [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse to and click **Audit Logs** to open the **Events** blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-189">In the [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse to and click **Audit Logs** to open the **Events** blade.</span></span>

    ![Audit Logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    <span data-ttu-id="2a16c-191">The **Events** blade opens to the operational events filtered just for the current vault.</span><span class="sxs-lookup"><span data-stu-id="2a16c-191">The **Events** blade opens to the operational events filtered just for the current vault.</span></span>

    ![Audit Logs Filter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/audit-logs-filter.png)
2. <span data-ttu-id="2a16c-193">On the **Events** menu, click **Filter** to open that blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-193">On the **Events** menu, click **Filter** to open that blade.</span></span>

    ![open filter blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. <span data-ttu-id="2a16c-195">On the **Filter** blade, adjust the **Level**, **Time span**, and **Caller** filters.</span><span class="sxs-lookup"><span data-stu-id="2a16c-195">On the **Filter** blade, adjust the **Level**, **Time span**, and **Caller** filters.</span></span> <span data-ttu-id="2a16c-196">The other filters are not available since they were set to provide the current information for the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2a16c-196">The other filters are not available since they were set to provide the current information for the Recovery Services vault.</span></span>

    ![Audit Logs-query details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/filter-blade.png)

    <span data-ttu-id="2a16c-198">You can specify the **Level** of event: Critical, Error, Warning, or Informational.</span><span class="sxs-lookup"><span data-stu-id="2a16c-198">You can specify the **Level** of event: Critical, Error, Warning, or Informational.</span></span> <span data-ttu-id="2a16c-199">You can choose any combination of event Levels, but you must have at least one Level selected.</span><span class="sxs-lookup"><span data-stu-id="2a16c-199">You can choose any combination of event Levels, but you must have at least one Level selected.</span></span> <span data-ttu-id="2a16c-200">Toggle the Level on or off.</span><span class="sxs-lookup"><span data-stu-id="2a16c-200">Toggle the Level on or off.</span></span> <span data-ttu-id="2a16c-201">The **Time span** filter allows you to specify the length of time for capturing events.</span><span class="sxs-lookup"><span data-stu-id="2a16c-201">The **Time span** filter allows you to specify the length of time for capturing events.</span></span> <span data-ttu-id="2a16c-202">If you use a custom Time span, you can set the start and end times.</span><span class="sxs-lookup"><span data-stu-id="2a16c-202">If you use a custom Time span, you can set the start and end times.</span></span>
4. <span data-ttu-id="2a16c-203">Once you are ready to query the operations logs using your filter, click **Update**.</span><span class="sxs-lookup"><span data-stu-id="2a16c-203">Once you are ready to query the operations logs using your filter, click **Update**.</span></span> <span data-ttu-id="2a16c-204">The results display in the **Events** blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-204">The results display in the **Events** blade.</span></span>

    ![Operation Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a><span data-ttu-id="2a16c-206">View additional event attributes</span><span class="sxs-lookup"><span data-stu-id="2a16c-206">View additional event attributes</span></span>
<span data-ttu-id="2a16c-207">Using the **Columns** button, you can enable additional event attributes to appear in the list on the **Events** blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-207">Using the **Columns** button, you can enable additional event attributes to appear in the list on the **Events** blade.</span></span> <span data-ttu-id="2a16c-208">The default list of events displays information for Operation, Level, Status, Resource, and Time.</span><span class="sxs-lookup"><span data-stu-id="2a16c-208">The default list of events displays information for Operation, Level, Status, Resource, and Time.</span></span> <span data-ttu-id="2a16c-209">To enable additional attributes:</span><span class="sxs-lookup"><span data-stu-id="2a16c-209">To enable additional attributes:</span></span>

1. <span data-ttu-id="2a16c-210">On the **Events** blade, click **Columns**.</span><span class="sxs-lookup"><span data-stu-id="2a16c-210">On the **Events** blade, click **Columns**.</span></span>

    ![Open Columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/audi-logs-column-button.png)

    <span data-ttu-id="2a16c-212">The **Choose columns** blade opens.</span><span class="sxs-lookup"><span data-stu-id="2a16c-212">The **Choose columns** blade opens.</span></span>

    ![Columns blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-monitor-vms/columns-blade.png)
2. <span data-ttu-id="2a16c-214">To select the attribute, click the checkbox.</span><span class="sxs-lookup"><span data-stu-id="2a16c-214">To select the attribute, click the checkbox.</span></span> <span data-ttu-id="2a16c-215">The attribute checkbox toggles on and off.</span><span class="sxs-lookup"><span data-stu-id="2a16c-215">The attribute checkbox toggles on and off.</span></span>
3. <span data-ttu-id="2a16c-216">Click **Reset** to reset the list of attributes in the **Events** blade.</span><span class="sxs-lookup"><span data-stu-id="2a16c-216">Click **Reset** to reset the list of attributes in the **Events** blade.</span></span> <span data-ttu-id="2a16c-217">After adding or removing attributes from the list, use **Reset** to view the new list of Event attributes.</span><span class="sxs-lookup"><span data-stu-id="2a16c-217">After adding or removing attributes from the list, use **Reset** to view the new list of Event attributes.</span></span>
4. <span data-ttu-id="2a16c-218">Click **Update** to update the data in the Event attributes.</span><span class="sxs-lookup"><span data-stu-id="2a16c-218">Click **Update** to update the data in the Event attributes.</span></span> <span data-ttu-id="2a16c-219">The following table provides information about each attribute.</span><span class="sxs-lookup"><span data-stu-id="2a16c-219">The following table provides information about each attribute.</span></span>

| <span data-ttu-id="2a16c-220">Column name</span><span class="sxs-lookup"><span data-stu-id="2a16c-220">Column name</span></span> | <span data-ttu-id="2a16c-221">Description</span><span class="sxs-lookup"><span data-stu-id="2a16c-221">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a16c-222">Operation</span><span class="sxs-lookup"><span data-stu-id="2a16c-222">Operation</span></span> |<span data-ttu-id="2a16c-223">The name of the operation</span><span class="sxs-lookup"><span data-stu-id="2a16c-223">The name of the operation</span></span> |
| <span data-ttu-id="2a16c-224">Level</span><span class="sxs-lookup"><span data-stu-id="2a16c-224">Level</span></span> |<span data-ttu-id="2a16c-225">The level of the operation, values can be: Informational, Warning, Error, or Critical</span><span class="sxs-lookup"><span data-stu-id="2a16c-225">The level of the operation, values can be: Informational, Warning, Error, or Critical</span></span> |
| <span data-ttu-id="2a16c-226">Status</span><span class="sxs-lookup"><span data-stu-id="2a16c-226">Status</span></span> |<span data-ttu-id="2a16c-227">Descriptive state of the operation</span><span class="sxs-lookup"><span data-stu-id="2a16c-227">Descriptive state of the operation</span></span> |
| <span data-ttu-id="2a16c-228">Resource</span><span class="sxs-lookup"><span data-stu-id="2a16c-228">Resource</span></span> |<span data-ttu-id="2a16c-229">URL that identifies the resource; also known as the resource ID</span><span class="sxs-lookup"><span data-stu-id="2a16c-229">URL that identifies the resource; also known as the resource ID</span></span> |
| <span data-ttu-id="2a16c-230">Time</span><span class="sxs-lookup"><span data-stu-id="2a16c-230">Time</span></span> |<span data-ttu-id="2a16c-231">Time, measured from the current time, when the event occurred</span><span class="sxs-lookup"><span data-stu-id="2a16c-231">Time, measured from the current time, when the event occurred</span></span> |
| <span data-ttu-id="2a16c-232">Caller</span><span class="sxs-lookup"><span data-stu-id="2a16c-232">Caller</span></span> |<span data-ttu-id="2a16c-233">Who or what called or triggered the event; can be the system, or a user</span><span class="sxs-lookup"><span data-stu-id="2a16c-233">Who or what called or triggered the event; can be the system, or a user</span></span> |
| <span data-ttu-id="2a16c-234">Timestamp</span><span class="sxs-lookup"><span data-stu-id="2a16c-234">Timestamp</span></span> |<span data-ttu-id="2a16c-235">The time when the event was triggered</span><span class="sxs-lookup"><span data-stu-id="2a16c-235">The time when the event was triggered</span></span> |
| <span data-ttu-id="2a16c-236">Resource Group</span><span class="sxs-lookup"><span data-stu-id="2a16c-236">Resource Group</span></span> |<span data-ttu-id="2a16c-237">The associated resource group</span><span class="sxs-lookup"><span data-stu-id="2a16c-237">The associated resource group</span></span> |
| <span data-ttu-id="2a16c-238">Resource Type</span><span class="sxs-lookup"><span data-stu-id="2a16c-238">Resource Type</span></span> |<span data-ttu-id="2a16c-239">The internal resource type used by Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2a16c-239">The internal resource type used by Resource Manager</span></span> |
| <span data-ttu-id="2a16c-240">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="2a16c-240">Subscription ID</span></span> |<span data-ttu-id="2a16c-241">The associated subscription ID</span><span class="sxs-lookup"><span data-stu-id="2a16c-241">The associated subscription ID</span></span> |
| <span data-ttu-id="2a16c-242">Category</span><span class="sxs-lookup"><span data-stu-id="2a16c-242">Category</span></span> |<span data-ttu-id="2a16c-243">Category of the event</span><span class="sxs-lookup"><span data-stu-id="2a16c-243">Category of the event</span></span> |
| <span data-ttu-id="2a16c-244">Correlation ID</span><span class="sxs-lookup"><span data-stu-id="2a16c-244">Correlation ID</span></span> |<span data-ttu-id="2a16c-245">Common ID for related events</span><span class="sxs-lookup"><span data-stu-id="2a16c-245">Common ID for related events</span></span> |

## <a name="use-powershell-to-customize-alerts"></a><span data-ttu-id="2a16c-246">Use PowerShell to customize alerts</span><span class="sxs-lookup"><span data-stu-id="2a16c-246">Use PowerShell to customize alerts</span></span>
<span data-ttu-id="2a16c-247">You can get custom alert notifications for the jobs in the portal.</span><span class="sxs-lookup"><span data-stu-id="2a16c-247">You can get custom alert notifications for the jobs in the portal.</span></span> <span data-ttu-id="2a16c-248">To get these jobs, define PowerShell-based alert rules on the operational logs events.</span><span class="sxs-lookup"><span data-stu-id="2a16c-248">To get these jobs, define PowerShell-based alert rules on the operational logs events.</span></span> <span data-ttu-id="2a16c-249">Use *PowerShell version 1.3.0 or later*.</span><span class="sxs-lookup"><span data-stu-id="2a16c-249">Use *PowerShell version 1.3.0 or later*.</span></span>

<span data-ttu-id="2a16c-250">To define a custom notification to alert for backup failures, use a command like the following script:</span><span class="sxs-lookup"><span data-stu-id="2a16c-250">To define a custom notification to alert for backup failures, use a command like the following script:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="2a16c-251">**ResourceId** : You can get ResourceId from the Audit logs.</span><span class="sxs-lookup"><span data-stu-id="2a16c-251">**ResourceId** : You can get ResourceId from the Audit logs.</span></span> <span data-ttu-id="2a16c-252">The ResourceId is a URL provided in the Resource column of the Operation logs.</span><span class="sxs-lookup"><span data-stu-id="2a16c-252">The ResourceId is a URL provided in the Resource column of the Operation logs.</span></span>

<span data-ttu-id="2a16c-253">**OperationName** : OperationName is in the format "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" where *EventName* can be:</span><span class="sxs-lookup"><span data-stu-id="2a16c-253">**OperationName** : OperationName is in the format "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" where *EventName* can be:</span></span><br/>

* <span data-ttu-id="2a16c-254">Register</span><span class="sxs-lookup"><span data-stu-id="2a16c-254">Register</span></span> <br/>
* <span data-ttu-id="2a16c-255">Unregister</span><span class="sxs-lookup"><span data-stu-id="2a16c-255">Unregister</span></span> <br/>
* <span data-ttu-id="2a16c-256">ConfigureProtection</span><span class="sxs-lookup"><span data-stu-id="2a16c-256">ConfigureProtection</span></span> <br/>
* <span data-ttu-id="2a16c-257">Backup</span><span class="sxs-lookup"><span data-stu-id="2a16c-257">Backup</span></span> <br/>
* <span data-ttu-id="2a16c-258">Restore</span><span class="sxs-lookup"><span data-stu-id="2a16c-258">Restore</span></span> <br/>
* <span data-ttu-id="2a16c-259">StopProtection</span><span class="sxs-lookup"><span data-stu-id="2a16c-259">StopProtection</span></span> <br/>
* <span data-ttu-id="2a16c-260">DeleteBackupData</span><span class="sxs-lookup"><span data-stu-id="2a16c-260">DeleteBackupData</span></span> <br/>
* <span data-ttu-id="2a16c-261">CreateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="2a16c-261">CreateProtectionPolicy</span></span> <br/>
* <span data-ttu-id="2a16c-262">DeleteProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="2a16c-262">DeleteProtectionPolicy</span></span> <br/>
* <span data-ttu-id="2a16c-263">UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="2a16c-263">UpdateProtectionPolicy</span></span> <br/>

<span data-ttu-id="2a16c-264">**Status** : Supported values are Started, Succeeded, or Failed.</span><span class="sxs-lookup"><span data-stu-id="2a16c-264">**Status** : Supported values are Started, Succeeded, or Failed.</span></span>

<span data-ttu-id="2a16c-265">**ResourceGroup** : This is the Resource Group to which the resource belongs.</span><span class="sxs-lookup"><span data-stu-id="2a16c-265">**ResourceGroup** : This is the Resource Group to which the resource belongs.</span></span> <span data-ttu-id="2a16c-266">You can add the Resource Group column to the generated logs.</span><span class="sxs-lookup"><span data-stu-id="2a16c-266">You can add the Resource Group column to the generated logs.</span></span> <span data-ttu-id="2a16c-267">Resource Group is one of the available types of event information.</span><span class="sxs-lookup"><span data-stu-id="2a16c-267">Resource Group is one of the available types of event information.</span></span>

<span data-ttu-id="2a16c-268">**Name** : Name of the Alert Rule.</span><span class="sxs-lookup"><span data-stu-id="2a16c-268">**Name** : Name of the Alert Rule.</span></span>

<span data-ttu-id="2a16c-269">**CustomEmail** : Specify the custom email address to which you want to send an alert notification</span><span class="sxs-lookup"><span data-stu-id="2a16c-269">**CustomEmail** : Specify the custom email address to which you want to send an alert notification</span></span>

<span data-ttu-id="2a16c-270">**SendToServiceOwners** : This option sends alert notifications to all administrators and co-administrators of the subscription.</span><span class="sxs-lookup"><span data-stu-id="2a16c-270">**SendToServiceOwners** : This option sends alert notifications to all administrators and co-administrators of the subscription.</span></span> <span data-ttu-id="2a16c-271">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span><span class="sxs-lookup"><span data-stu-id="2a16c-271">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="2a16c-272">Limitations on Alerts</span><span class="sxs-lookup"><span data-stu-id="2a16c-272">Limitations on Alerts</span></span>
<span data-ttu-id="2a16c-273">Event-based alerts are subject to the following limitations:</span><span class="sxs-lookup"><span data-stu-id="2a16c-273">Event-based alerts are subject to the following limitations:</span></span>

1. <span data-ttu-id="2a16c-274">Alerts are triggered on all virtual machines in the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2a16c-274">Alerts are triggered on all virtual machines in the Recovery Services vault.</span></span> <span data-ttu-id="2a16c-275">You cannot customize the alert for a subset of virtual machines in a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2a16c-275">You cannot customize the alert for a subset of virtual machines in a Recovery Services vault.</span></span>
2. <span data-ttu-id="2a16c-276">This feature is in Preview.</span><span class="sxs-lookup"><span data-stu-id="2a16c-276">This feature is in Preview.</span></span> [<span data-ttu-id="2a16c-277">Learn more</span><span class="sxs-lookup"><span data-stu-id="2a16c-277">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-alert-rules)
3. <span data-ttu-id="2a16c-278">Alerts are sent from "alerts-noreply@mail.windowsazure.com".</span><span class="sxs-lookup"><span data-stu-id="2a16c-278">Alerts are sent from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="2a16c-279">Currently you can't modify the email sender.</span><span class="sxs-lookup"><span data-stu-id="2a16c-279">Currently you can't modify the email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a16c-280">Next steps</span><span class="sxs-lookup"><span data-stu-id="2a16c-280">Next steps</span></span>
<span data-ttu-id="2a16c-281">Event logs enable great post-mortem and audit support for the backup operations.</span><span class="sxs-lookup"><span data-stu-id="2a16c-281">Event logs enable great post-mortem and audit support for the backup operations.</span></span> <span data-ttu-id="2a16c-282">The following operations are logged:</span><span class="sxs-lookup"><span data-stu-id="2a16c-282">The following operations are logged:</span></span>

* <span data-ttu-id="2a16c-283">Register</span><span class="sxs-lookup"><span data-stu-id="2a16c-283">Register</span></span>
* <span data-ttu-id="2a16c-284">Unregister</span><span class="sxs-lookup"><span data-stu-id="2a16c-284">Unregister</span></span>
* <span data-ttu-id="2a16c-285">Configure protection</span><span class="sxs-lookup"><span data-stu-id="2a16c-285">Configure protection</span></span>
* <span data-ttu-id="2a16c-286">Backup (Both scheduled as well as on-demand backup)</span><span class="sxs-lookup"><span data-stu-id="2a16c-286">Backup (Both scheduled as well as on-demand backup)</span></span>
* <span data-ttu-id="2a16c-287">Restore</span><span class="sxs-lookup"><span data-stu-id="2a16c-287">Restore</span></span>
* <span data-ttu-id="2a16c-288">Stop protection</span><span class="sxs-lookup"><span data-stu-id="2a16c-288">Stop protection</span></span>
* <span data-ttu-id="2a16c-289">Delete backup data</span><span class="sxs-lookup"><span data-stu-id="2a16c-289">Delete backup data</span></span>
* <span data-ttu-id="2a16c-290">Add policy</span><span class="sxs-lookup"><span data-stu-id="2a16c-290">Add policy</span></span>
* <span data-ttu-id="2a16c-291">Delete policy</span><span class="sxs-lookup"><span data-stu-id="2a16c-291">Delete policy</span></span>
* <span data-ttu-id="2a16c-292">Update policy</span><span class="sxs-lookup"><span data-stu-id="2a16c-292">Update policy</span></span>
* <span data-ttu-id="2a16c-293">Cancel job</span><span class="sxs-lookup"><span data-stu-id="2a16c-293">Cancel job</span></span>

<span data-ttu-id="2a16c-294">For a broad explanation of events, operations, and audit logs across the Azure services, see the article, [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md).</span><span class="sxs-lookup"><span data-stu-id="2a16c-294">For a broad explanation of events, operations, and audit logs across the Azure services, see the article, [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md).</span></span>

<span data-ttu-id="2a16c-295">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="2a16c-295">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="2a16c-296">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2a16c-296">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="2a16c-297">Learn about the management tasks for VM backups in the article, [Manage Azure virtual machine backups](backup-azure-manage-vms.md).</span><span class="sxs-lookup"><span data-stu-id="2a16c-297">Learn about the management tasks for VM backups in the article, [Manage Azure virtual machine backups](backup-azure-manage-vms.md).</span></span>



















