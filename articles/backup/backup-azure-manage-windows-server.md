---
title: Manage Azure Recovery Services vaults and servers
description: Manage jobs and alerts in an Azure Recovery Services vault.
services: backup
author: markgalioto
manager: carmonm
ms.service: backup
ms.topic: conceptual
ms.date: 8/21/2018
ms.author: markgal
ms.openlocfilehash: 9fad5876ce177129d6178052916843b94b33ccf1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773714"
---
# <a name="monitor-and-manage-recovery-services-vaults"></a><span data-ttu-id="8b7ae-103">Monitor and manage Recovery Services vaults</span><span class="sxs-lookup"><span data-stu-id="8b7ae-103">Monitor and manage Recovery Services vaults</span></span>

<span data-ttu-id="8b7ae-104">This article explains how to use the Recovery Services vault **Overview** dashboard to monitor and manage your Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-104">This article explains how to use the Recovery Services vault **Overview** dashboard to monitor and manage your Recovery Services vaults.</span></span> <span data-ttu-id="8b7ae-105">When you open a Recovery Services vault from the list, the **Overview** dashboard for the selected vault, opens.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-105">When you open a Recovery Services vault from the list, the **Overview** dashboard for the selected vault, opens.</span></span> <span data-ttu-id="8b7ae-106">The dashboard provides various details about the vault.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-106">The dashboard provides various details about the vault.</span></span> <span data-ttu-id="8b7ae-107">There are *tiles* that show: the status of critical and warning alerts, in-progress and failed backup jobs, and the amount of locally redundant storage (LRS) and geo redundant storage (GRS) used.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-107">There are *tiles* that show: the status of critical and warning alerts, in-progress and failed backup jobs, and the amount of locally redundant storage (LRS) and geo redundant storage (GRS) used.</span></span> <span data-ttu-id="8b7ae-108">If you back up Azure VMs to the vault, the [**Backup Pre-Check Status** tile displays any critical or warning items](https://azure.microsoft.com/blog/azure-vm-backup-pre-checks/).</span><span class="sxs-lookup"><span data-stu-id="8b7ae-108">If you back up Azure VMs to the vault, the [**Backup Pre-Check Status** tile displays any critical or warning items](https://azure.microsoft.com/blog/azure-vm-backup-pre-checks/).</span></span> <span data-ttu-id="8b7ae-109">The following image is the **Overview** dashboard for **Contoso-vault**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-109">The following image is the **Overview** dashboard for **Contoso-vault**.</span></span> <span data-ttu-id="8b7ae-110">The **Backup Items** tile shows there are nine items registered to the vault.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-110">The **Backup Items** tile shows there are nine items registered to the vault.</span></span>

![recovery services vault dashboard](./media/backup-azure-manage-windows-server/rs-vault-blade.png)

<span data-ttu-id="8b7ae-112">The prerequisites for this article are: an Azure subscription, a Recovery Services vault, and that there is at least one backup item configured for the vault.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-112">The prerequisites for this article are: an Azure subscription, a Recovery Services vault, and that there is at least one backup item configured for the vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="8b7ae-113">Open a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="8b7ae-113">Open a Recovery Services vault</span></span>

<span data-ttu-id="8b7ae-114">To monitor alerts, or view management data about a Recovery Services vault, open the vault.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-114">To monitor alerts, or view management data about a Recovery Services vault, open the vault.</span></span>

1. <span data-ttu-id="8b7ae-115">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-115">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>

2. <span data-ttu-id="8b7ae-116">In the portal, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-116">In the portal, click **All services**.</span></span>

   ![Open list of Recovery Services vaults step 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png)

3. <span data-ttu-id="8b7ae-118">In the **All services** dialog box, type **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-118">In the **All services** dialog box, type **Recovery Services**.</span></span> <span data-ttu-id="8b7ae-119">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-119">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="8b7ae-120">When the **Recovery Services vaults** option appears, click it to open the list of Recovery Services vaults in your subscription.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-120">When the **Recovery Services vaults** option appears, click it to open the list of Recovery Services vaults in your subscription.</span></span>

    ![Create Recovery Services Vault step 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="8b7ae-122">From the list of vaults, click a vault to open its **Overview** dashboard.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-122">From the list of vaults, click a vault to open its **Overview** dashboard.</span></span> 

    ![recovery services vault dashboard](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="8b7ae-124">The Overview dashboard uses tiles to provide alerts and backup job data.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-124">The Overview dashboard uses tiles to provide alerts and backup job data.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="8b7ae-125">Monitor backup jobs and alerts</span><span class="sxs-lookup"><span data-stu-id="8b7ae-125">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="8b7ae-126">The Recovery Services vault **Overview** dashboard provides tiles for Monitoring and Usage information.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-126">The Recovery Services vault **Overview** dashboard provides tiles for Monitoring and Usage information.</span></span> <span data-ttu-id="8b7ae-127">The tiles in the Monitoring section display Critical and Warning alerts, and In progress and Failed jobs.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-127">The tiles in the Monitoring section display Critical and Warning alerts, and In progress and Failed jobs.</span></span> <span data-ttu-id="8b7ae-128">Click a particular alert or job to open the Backup Alerts or Backup Jobs menu, filtered for that job or alert.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-128">Click a particular alert or job to open the Backup Alerts or Backup Jobs menu, filtered for that job or alert.</span></span>

![Backup dashboard tasks](./media/backup-azure-manage-windows-server/monitor-dashboard-tiles-warning.png)

<span data-ttu-id="8b7ae-130">The Monitoring section shows the results of predefined **Backup Alerts** and **Backup Jobs** queries.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-130">The Monitoring section shows the results of predefined **Backup Alerts** and **Backup Jobs** queries.</span></span> <span data-ttu-id="8b7ae-131">The Monitoring tiles provide up-to-date information about:</span><span class="sxs-lookup"><span data-stu-id="8b7ae-131">The Monitoring tiles provide up-to-date information about:</span></span>

* <span data-ttu-id="8b7ae-132">Critical and Warning alerts for Backup jobs (in the last 24 hours)</span><span class="sxs-lookup"><span data-stu-id="8b7ae-132">Critical and Warning alerts for Backup jobs (in the last 24 hours)</span></span>
* <span data-ttu-id="8b7ae-133">Pre-check status for Azure VMs - For complete information on the pre-check status, see the [Backup blog on Backup Pre-check status](https://azure.microsoft.com/blog/azure-vm-backup-pre-checks/).</span><span class="sxs-lookup"><span data-stu-id="8b7ae-133">Pre-check status for Azure VMs - For complete information on the pre-check status, see the [Backup blog on Backup Pre-check status](https://azure.microsoft.com/blog/azure-vm-backup-pre-checks/).</span></span>
* <span data-ttu-id="8b7ae-134">The Backup jobs in progress, and jobs that have failed (in the last 24 hours).</span><span class="sxs-lookup"><span data-stu-id="8b7ae-134">The Backup jobs in progress, and jobs that have failed (in the last 24 hours).</span></span>

<span data-ttu-id="8b7ae-135">The Usage tiles provide:</span><span class="sxs-lookup"><span data-stu-id="8b7ae-135">The Usage tiles provide:</span></span>

* <span data-ttu-id="8b7ae-136">The number of Backup items configured for the vault.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-136">The number of Backup items configured for the vault.</span></span>
* <span data-ttu-id="8b7ae-137">The Azure storage (separated by LRS and GRS) consumed by the vault.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-137">The Azure storage (separated by LRS and GRS) consumed by the vault.</span></span>

<span data-ttu-id="8b7ae-138">Click the tiles (except Backup Storage) to open the associated menu.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-138">Click the tiles (except Backup Storage) to open the associated menu.</span></span> <span data-ttu-id="8b7ae-139">In the image above, the Backup Alerts tile shows three Critical alerts.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-139">In the image above, the Backup Alerts tile shows three Critical alerts.</span></span> <span data-ttu-id="8b7ae-140">Clicking the Critical alerts row in the Backup Alerts tile, opens the Backup Alerts filtered for Critical alerts.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-140">Clicking the Critical alerts row in the Backup Alerts tile, opens the Backup Alerts filtered for Critical alerts.</span></span>

![Backup alerts menu filtered for critical alerts](./media/backup-azure-manage-windows-server/critical-backup-alerts.png)

<span data-ttu-id="8b7ae-142">The Backup Alerts menu, in the image above, is filtered by: Status is Active, Severity is Critical, and time is the previous 24 hours.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-142">The Backup Alerts menu, in the image above, is filtered by: Status is Active, Severity is Critical, and time is the previous 24 hours.</span></span>

## <a name="manage-backup-alerts"></a><span data-ttu-id="8b7ae-143">Manage Backup alerts</span><span class="sxs-lookup"><span data-stu-id="8b7ae-143">Manage Backup alerts</span></span>

<span data-ttu-id="8b7ae-144">To access the Backup Alerts menu, in the Recovery Services vault menu, click **Backup Alerts**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-144">To access the Backup Alerts menu, in the Recovery Services vault menu, click **Backup Alerts**.</span></span>

![Backup alerts](./media/backup-azure-manage-windows-server/backup-alerts-menu.png)

<span data-ttu-id="8b7ae-146">The Backup Alerts report lists the alerts for the vault.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-146">The Backup Alerts report lists the alerts for the vault.</span></span> 

![Backup alerts](./media/backup-azure-manage-windows-server/backup-alerts.png)

### <a name="alerts"></a><span data-ttu-id="8b7ae-148">Alerts</span><span class="sxs-lookup"><span data-stu-id="8b7ae-148">Alerts</span></span>

<span data-ttu-id="8b7ae-149">The Backup Alerts list displays the selected information for the filtered alerts.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-149">The Backup Alerts list displays the selected information for the filtered alerts.</span></span> <span data-ttu-id="8b7ae-150">In the Backup Alerts menu, you can filter for Critical or Warning alerts.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-150">In the Backup Alerts menu, you can filter for Critical or Warning alerts.</span></span>

| <span data-ttu-id="8b7ae-151">Alert Level</span><span class="sxs-lookup"><span data-stu-id="8b7ae-151">Alert Level</span></span> | <span data-ttu-id="8b7ae-152">Events that generate alerts</span><span class="sxs-lookup"><span data-stu-id="8b7ae-152">Events that generate alerts</span></span> |
| ----------- | ----------- |
| <span data-ttu-id="8b7ae-153">Critical</span><span class="sxs-lookup"><span data-stu-id="8b7ae-153">Critical</span></span> | <span data-ttu-id="8b7ae-154">You receive critical alerts when: Backup jobs fail, recovery jobs fail, and when you stop protection on a server, but retain the data.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-154">You receive critical alerts when: Backup jobs fail, recovery jobs fail, and when you stop protection on a server, but retain the data.</span></span>|
| <span data-ttu-id="8b7ae-155">Warning</span><span class="sxs-lookup"><span data-stu-id="8b7ae-155">Warning</span></span> | <span data-ttu-id="8b7ae-156">You receive warning alerts when: Backup jobs complete with warnings, for example when fewer than 100 files are not backed up due to corruption issues, or when greater than 1,000,000 files are successfully backed up).</span><span class="sxs-lookup"><span data-stu-id="8b7ae-156">You receive warning alerts when: Backup jobs complete with warnings, for example when fewer than 100 files are not backed up due to corruption issues, or when greater than 1,000,000 files are successfully backed up).</span></span> |
| <span data-ttu-id="8b7ae-157">Informational</span><span class="sxs-lookup"><span data-stu-id="8b7ae-157">Informational</span></span> | <span data-ttu-id="8b7ae-158">currently, no informational alerts are in use.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-158">currently, no informational alerts are in use.</span></span> |

### <a name="viewing-alert-details"></a><span data-ttu-id="8b7ae-159">Viewing alert details</span><span class="sxs-lookup"><span data-stu-id="8b7ae-159">Viewing alert details</span></span>

<span data-ttu-id="8b7ae-160">The Backup Alerts report tracks eight details about each alert.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-160">The Backup Alerts report tracks eight details about each alert.</span></span> <span data-ttu-id="8b7ae-161">Use the **Choose columns** button to edit the details in the report.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-161">Use the **Choose columns** button to edit the details in the report.</span></span>

![Backup alerts](./media/backup-azure-manage-windows-server/backup-alerts.png)

<span data-ttu-id="8b7ae-163">By default, all details, except **Latest Occurrence Time**, appear in the report.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-163">By default, all details, except **Latest Occurrence Time**, appear in the report.</span></span>

* <span data-ttu-id="8b7ae-164">Alert</span><span class="sxs-lookup"><span data-stu-id="8b7ae-164">Alert</span></span>
* <span data-ttu-id="8b7ae-165">Backup Item</span><span class="sxs-lookup"><span data-stu-id="8b7ae-165">Backup Item</span></span>
* <span data-ttu-id="8b7ae-166">Protected Server</span><span class="sxs-lookup"><span data-stu-id="8b7ae-166">Protected Server</span></span>
* <span data-ttu-id="8b7ae-167">Severity</span><span class="sxs-lookup"><span data-stu-id="8b7ae-167">Severity</span></span>
* <span data-ttu-id="8b7ae-168">Duration</span><span class="sxs-lookup"><span data-stu-id="8b7ae-168">Duration</span></span>
* <span data-ttu-id="8b7ae-169">Creation Time</span><span class="sxs-lookup"><span data-stu-id="8b7ae-169">Creation Time</span></span>
* <span data-ttu-id="8b7ae-170">Status</span><span class="sxs-lookup"><span data-stu-id="8b7ae-170">Status</span></span>
* <span data-ttu-id="8b7ae-171">Latest Occurrence Time</span><span class="sxs-lookup"><span data-stu-id="8b7ae-171">Latest Occurrence Time</span></span>

### <a name="change-the-details-in-alerts-report"></a><span data-ttu-id="8b7ae-172">Change the details in alerts report</span><span class="sxs-lookup"><span data-stu-id="8b7ae-172">Change the details in alerts report</span></span>

1. <span data-ttu-id="8b7ae-173">To change the report information, in the **Backup Alerts** menu, click **Choose columns**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-173">To change the report information, in the **Backup Alerts** menu, click **Choose columns**.</span></span>

   ![Backup alerts](./media/backup-azure-manage-windows-server/alerts-menu-choose-columns.png)

   <span data-ttu-id="8b7ae-175">The **Choose columns** menu opens.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-175">The **Choose columns** menu opens.</span></span>

2. <span data-ttu-id="8b7ae-176">In the **Choose columns** menu, choose the details you want to appear in the report.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-176">In the **Choose columns** menu, choose the details you want to appear in the report.</span></span>

    ![Choose columns menu](./media/backup-azure-manage-windows-server/choose-columns-menu.png)

3. <span data-ttu-id="8b7ae-178">Click **Done** to save your changes and close the Choose columns menu.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-178">Click **Done** to save your changes and close the Choose columns menu.</span></span>

   <span data-ttu-id="8b7ae-179">If you make changes, but don't want to keep the changes, click **Reset** to return the selected to the last saved configuration.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-179">If you make changes, but don't want to keep the changes, click **Reset** to return the selected to the last saved configuration.</span></span>

### <a name="change-the-filter-in-alerts-report"></a><span data-ttu-id="8b7ae-180">Change the filter in alerts report</span><span class="sxs-lookup"><span data-stu-id="8b7ae-180">Change the filter in alerts report</span></span>

<span data-ttu-id="8b7ae-181">Use the **Filter** menu to change the Severity, Status, Start time and End time for the alerts.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-181">Use the **Filter** menu to change the Severity, Status, Start time and End time for the alerts.</span></span> 

> [!NOTE]
> <span data-ttu-id="8b7ae-182">Editing the Backup Alerts filter doesn't change the Critical or Warning alerts in the vault Overview dashboard.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-182">Editing the Backup Alerts filter doesn't change the Critical or Warning alerts in the vault Overview dashboard.</span></span>
>  

1. <span data-ttu-id="8b7ae-183">To change the Backup Alerts filter, in the Backup Alerts menu, click **Filter**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-183">To change the Backup Alerts filter, in the Backup Alerts menu, click **Filter**.</span></span>

   ![Choose filter menu](./media/backup-azure-manage-windows-server/alerts-menu-choose-filter.png)

   <span data-ttu-id="8b7ae-185">The Filter menu appears.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-185">The Filter menu appears.</span></span>

   ![Choose filter menu](./media/backup-azure-manage-windows-server/filter-alert-menu.png)

2. <span data-ttu-id="8b7ae-187">Edit the Severity, Status, Start time, or End time, and click **Done** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-187">Edit the Severity, Status, Start time, or End time, and click **Done** to save your changes.</span></span>

## <a name="configuring-notifications-for-alerts"></a><span data-ttu-id="8b7ae-188">Configuring notifications for alerts</span><span class="sxs-lookup"><span data-stu-id="8b7ae-188">Configuring notifications for alerts</span></span>

<span data-ttu-id="8b7ae-189">Configure notifications to generate emails when a Warning or Critical alert occurs.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-189">Configure notifications to generate emails when a Warning or Critical alert occurs.</span></span> <span data-ttu-id="8b7ae-190">You can send email alerts each hour, or when a particular alert occurs.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-190">You can send email alerts each hour, or when a particular alert occurs.</span></span>

   ![Filter alerts](./media/backup-azure-manage-windows-server/configure-notification.png)

<span data-ttu-id="8b7ae-192">By default, Email notifications are **On**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-192">By default, Email notifications are **On**.</span></span> <span data-ttu-id="8b7ae-193">Click **Off** to stop the email notifications.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-193">Click **Off** to stop the email notifications.</span></span>

<span data-ttu-id="8b7ae-194">On the **Notify** control, choose **Per Alert** if don't want grouping or don't have many items that could generate alerts.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-194">On the **Notify** control, choose **Per Alert** if don't want grouping or don't have many items that could generate alerts.</span></span> <span data-ttu-id="8b7ae-195">Every alert results in one notification (the default setting), and a resolution email is sent immediately.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-195">Every alert results in one notification (the default setting), and a resolution email is sent immediately.</span></span>

<span data-ttu-id="8b7ae-196">If you select **Hourly Digest**, an email is sent to the recipients explaining the unresolved alerts generated in the last hour.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-196">If you select **Hourly Digest**, an email is sent to the recipients explaining the unresolved alerts generated in the last hour.</span></span> <span data-ttu-id="8b7ae-197">A resolution email is sent out at the end of the hour.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-197">A resolution email is sent out at the end of the hour.</span></span>

<span data-ttu-id="8b7ae-198">Choose the alert severity (Critical or Warning) used to generate email.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-198">Choose the alert severity (Critical or Warning) used to generate email.</span></span> <span data-ttu-id="8b7ae-199">Currently there are no Information alerts.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-199">Currently there are no Information alerts.</span></span>

## <a name="manage-backup-items"></a><span data-ttu-id="8b7ae-200">Manage Backup items</span><span class="sxs-lookup"><span data-stu-id="8b7ae-200">Manage Backup items</span></span>

<span data-ttu-id="8b7ae-201">A Recovery Services vault holds many types of backup data.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-201">A Recovery Services vault holds many types of backup data.</span></span> <span data-ttu-id="8b7ae-202">For a complete list of backup types, see [Which applications and workloads can be backed up](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="8b7ae-202">For a complete list of backup types, see [Which applications and workloads can be backed up](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use).</span></span> <span data-ttu-id="8b7ae-203">To manage the various servers, computers, databases, and workloads, click the **Backup Items** tile to view the contents of the vault.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-203">To manage the various servers, computers, databases, and workloads, click the **Backup Items** tile to view the contents of the vault.</span></span>

![Backup items tile](./media/backup-azure-manage-windows-server/backup-items.png)

<span data-ttu-id="8b7ae-205">The list of Backup Items, organized by Backup Management Type, opens.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-205">The list of Backup Items, organized by Backup Management Type, opens.</span></span>

![list of Backup items](./media/backup-azure-manage-windows-server/list-backup-items.png)

<span data-ttu-id="8b7ae-207">To explore a specific type of protected instance, click the item in the Backup Management Type column.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-207">To explore a specific type of protected instance, click the item in the Backup Management Type column.</span></span> <span data-ttu-id="8b7ae-208">For example, in the above image, there are two Azure virtual machines protected in this vault.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-208">For example, in the above image, there are two Azure virtual machines protected in this vault.</span></span> <span data-ttu-id="8b7ae-209">Clicking **Azure Virtual Machine**, opens the list of protected virtual machines in this vault.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-209">Clicking **Azure Virtual Machine**, opens the list of protected virtual machines in this vault.</span></span>

![list of Backup type](./media/backup-azure-manage-windows-server/list-of-protected-virtual-machines.png)

<span data-ttu-id="8b7ae-211">The list of virtual machines has helpful data: the associated Resource Group, previous [Backup Pre-Check](https://azure.microsoft.com/blog/azure-vm-backup-pre-checks/), Last Backup Status, and date of the most recent Restore Point.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-211">The list of virtual machines has helpful data: the associated Resource Group, previous [Backup Pre-Check](https://azure.microsoft.com/blog/azure-vm-backup-pre-checks/), Last Backup Status, and date of the most recent Restore Point.</span></span> <span data-ttu-id="8b7ae-212">The ellipsis, in the last column, opens the menu to trigger common tasks.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-212">The ellipsis, in the last column, opens the menu to trigger common tasks.</span></span> <span data-ttu-id="8b7ae-213">The helpful data provided in columns, is different for each backup type.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-213">The helpful data provided in columns, is different for each backup type.</span></span>

![list of Backup type](./media/backup-azure-manage-windows-server/ellipsis-menu.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="8b7ae-215">Manage Backup jobs</span><span class="sxs-lookup"><span data-stu-id="8b7ae-215">Manage Backup jobs</span></span>

<span data-ttu-id="8b7ae-216">The **Backup Jobs** tile in the vault dashboard shows the number of jobs that are In Progress, or Failed in the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-216">The **Backup Jobs** tile in the vault dashboard shows the number of jobs that are In Progress, or Failed in the last 24 hours.</span></span> <span data-ttu-id="8b7ae-217">The tile provides a glimpse into the Backup Jobs menu.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-217">The tile provides a glimpse into the Backup Jobs menu.</span></span>

![Backup items from settings](./media/backup-azure-manage-windows-server/backup-jobs-tile.png)

<span data-ttu-id="8b7ae-219">To see additional details about the jobs, click **In Progress** or **Failed** to open the Backup Jobs menu filtered for that state.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-219">To see additional details about the jobs, click **In Progress** or **Failed** to open the Backup Jobs menu filtered for that state.</span></span>

### <a name="backup-jobs-menu"></a><span data-ttu-id="8b7ae-220">Backup jobs menu</span><span class="sxs-lookup"><span data-stu-id="8b7ae-220">Backup jobs menu</span></span>

<span data-ttu-id="8b7ae-221">The **Backup Jobs** menu displays information about the Item type, Operation, Status, Start Time, and Duration.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-221">The **Backup Jobs** menu displays information about the Item type, Operation, Status, Start Time, and Duration.</span></span>  

<span data-ttu-id="8b7ae-222">To open the Backup Jobs menu, in the vault's main menu, click **Backup Jobs**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-222">To open the Backup Jobs menu, in the vault's main menu, click **Backup Jobs**.</span></span> 

![Backup items from settings](./media/backup-azure-manage-windows-server/backup-jobs-menu-item.png)

<span data-ttu-id="8b7ae-224">The list of Backup jobs opens.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-224">The list of Backup jobs opens.</span></span>

![Backup items from settings](./media/backup-azure-manage-windows-server/backup-jobs-list.png)

<span data-ttu-id="8b7ae-226">The Backup Jobs menu shows the status for all operations, on all backup types, for the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-226">The Backup Jobs menu shows the status for all operations, on all backup types, for the last 24 hours.</span></span> <span data-ttu-id="8b7ae-227">Use **Filter** to change the filters.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-227">Use **Filter** to change the filters.</span></span> <span data-ttu-id="8b7ae-228">The filters are explained in the following sections.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-228">The filters are explained in the following sections.</span></span>

<span data-ttu-id="8b7ae-229">To change the filters:</span><span class="sxs-lookup"><span data-stu-id="8b7ae-229">To change the filters:</span></span>

1. <span data-ttu-id="8b7ae-230">In the vault Backup Jobs menu, click **Filter**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-230">In the vault Backup Jobs menu, click **Filter**.</span></span>

   ![Backup items from settings](./media/backup-azure-manage-windows-server/vault-backup-job-menu-filter.png)

    <span data-ttu-id="8b7ae-232">The Filter menu opens.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-232">The Filter menu opens.</span></span>

   ![Backup items from settings](./media/backup-azure-manage-windows-server/filter-menu-backup-jobs.png)

2. <span data-ttu-id="8b7ae-234">Choose the filter settings and click **Done**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-234">Choose the filter settings and click **Done**.</span></span> <span data-ttu-id="8b7ae-235">The filtered list refreshes based on the new settings.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-235">The filtered list refreshes based on the new settings.</span></span>

#### <a name="item-type"></a><span data-ttu-id="8b7ae-236">Item type</span><span class="sxs-lookup"><span data-stu-id="8b7ae-236">Item type</span></span>

<span data-ttu-id="8b7ae-237">The Item type is the backup management type of the protected instance.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-237">The Item type is the backup management type of the protected instance.</span></span> <span data-ttu-id="8b7ae-238">There are four types; see the following list.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-238">There are four types; see the following list.</span></span> <span data-ttu-id="8b7ae-239">You can view all item types, or one item type.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-239">You can view all item types, or one item type.</span></span> <span data-ttu-id="8b7ae-240">You can't select two or three item types.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-240">You can't select two or three item types.</span></span> <span data-ttu-id="8b7ae-241">The available Item types are:</span><span class="sxs-lookup"><span data-stu-id="8b7ae-241">The available Item types are:</span></span>

* <span data-ttu-id="8b7ae-242">All item types</span><span class="sxs-lookup"><span data-stu-id="8b7ae-242">All item types</span></span>
* <span data-ttu-id="8b7ae-243">Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="8b7ae-243">Azure virtual machine</span></span>
* <span data-ttu-id="8b7ae-244">Files and folders</span><span class="sxs-lookup"><span data-stu-id="8b7ae-244">Files and folders</span></span>
* <span data-ttu-id="8b7ae-245">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8b7ae-245">Azure Storage</span></span>
* <span data-ttu-id="8b7ae-246">Azure workload</span><span class="sxs-lookup"><span data-stu-id="8b7ae-246">Azure workload</span></span>

#### <a name="operation"></a><span data-ttu-id="8b7ae-247">Operation</span><span class="sxs-lookup"><span data-stu-id="8b7ae-247">Operation</span></span>

<span data-ttu-id="8b7ae-248">You can view one operation, or all operations.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-248">You can view one operation, or all operations.</span></span> <span data-ttu-id="8b7ae-249">You can't select two or three operations.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-249">You can't select two or three operations.</span></span> <span data-ttu-id="8b7ae-250">The available Operations are:</span><span class="sxs-lookup"><span data-stu-id="8b7ae-250">The available Operations are:</span></span>

* <span data-ttu-id="8b7ae-251">All Operations</span><span class="sxs-lookup"><span data-stu-id="8b7ae-251">All Operations</span></span>
* <span data-ttu-id="8b7ae-252">Register</span><span class="sxs-lookup"><span data-stu-id="8b7ae-252">Register</span></span>
* <span data-ttu-id="8b7ae-253">Configure backup</span><span class="sxs-lookup"><span data-stu-id="8b7ae-253">Configure backup</span></span>
* <span data-ttu-id="8b7ae-254">Backup</span><span class="sxs-lookup"><span data-stu-id="8b7ae-254">Backup</span></span>
* <span data-ttu-id="8b7ae-255">Restore</span><span class="sxs-lookup"><span data-stu-id="8b7ae-255">Restore</span></span>
* <span data-ttu-id="8b7ae-256">Disable backup</span><span class="sxs-lookup"><span data-stu-id="8b7ae-256">Disable backup</span></span>
* <span data-ttu-id="8b7ae-257">Delete backup data</span><span class="sxs-lookup"><span data-stu-id="8b7ae-257">Delete backup data</span></span>

#### <a name="status"></a><span data-ttu-id="8b7ae-258">Status</span><span class="sxs-lookup"><span data-stu-id="8b7ae-258">Status</span></span>

<span data-ttu-id="8b7ae-259">You can view All Status or one.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-259">You can view All Status or one.</span></span> <span data-ttu-id="8b7ae-260">You can't select two or three statuses.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-260">You can't select two or three statuses.</span></span> <span data-ttu-id="8b7ae-261">The available statuses are:</span><span class="sxs-lookup"><span data-stu-id="8b7ae-261">The available statuses are:</span></span>

* <span data-ttu-id="8b7ae-262">All Status</span><span class="sxs-lookup"><span data-stu-id="8b7ae-262">All Status</span></span>
* <span data-ttu-id="8b7ae-263">Completed</span><span class="sxs-lookup"><span data-stu-id="8b7ae-263">Completed</span></span>
* <span data-ttu-id="8b7ae-264">In progress</span><span class="sxs-lookup"><span data-stu-id="8b7ae-264">In progress</span></span>
* <span data-ttu-id="8b7ae-265">Failed</span><span class="sxs-lookup"><span data-stu-id="8b7ae-265">Failed</span></span>
* <span data-ttu-id="8b7ae-266">Canceled</span><span class="sxs-lookup"><span data-stu-id="8b7ae-266">Canceled</span></span>
* <span data-ttu-id="8b7ae-267">Completed with warnings</span><span class="sxs-lookup"><span data-stu-id="8b7ae-267">Completed with warnings</span></span>

#### <a name="start-time"></a><span data-ttu-id="8b7ae-268">Start time</span><span class="sxs-lookup"><span data-stu-id="8b7ae-268">Start time</span></span>

<span data-ttu-id="8b7ae-269">The day and time that the query begins.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-269">The day and time that the query begins.</span></span> <span data-ttu-id="8b7ae-270">The default is a 24-hour period.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-270">The default is a 24-hour period.</span></span>

#### <a name="end-time"></a><span data-ttu-id="8b7ae-271">End time</span><span class="sxs-lookup"><span data-stu-id="8b7ae-271">End time</span></span>

<span data-ttu-id="8b7ae-272">The day and time when the query ends.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-272">The day and time when the query ends.</span></span>

### <a name="export-jobs"></a><span data-ttu-id="8b7ae-273">Export jobs</span><span class="sxs-lookup"><span data-stu-id="8b7ae-273">Export jobs</span></span>

<span data-ttu-id="8b7ae-274">Use **Export jobs** to create a spreadsheet containing all Jobs menu information.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-274">Use **Export jobs** to create a spreadsheet containing all Jobs menu information.</span></span> <span data-ttu-id="8b7ae-275">The spreadsheet has one sheet that holds a summary of all jobs, and individual sheets for each job.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-275">The spreadsheet has one sheet that holds a summary of all jobs, and individual sheets for each job.</span></span>

<span data-ttu-id="8b7ae-276">To export the jobs information to a spreadsheet, click **Export jobs**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-276">To export the jobs information to a spreadsheet, click **Export jobs**.</span></span> <span data-ttu-id="8b7ae-277">The service creates a speadsheet using the name of the vault and date, but you can change the name.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-277">The service creates a speadsheet using the name of the vault and date, but you can change the name.</span></span>

## <a name="monitor-backup-usage"></a><span data-ttu-id="8b7ae-278">Monitor Backup usage</span><span class="sxs-lookup"><span data-stu-id="8b7ae-278">Monitor Backup usage</span></span>

<span data-ttu-id="8b7ae-279">The Backup Storage tile in the dashboard shows the storage consumed in Azure.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-279">The Backup Storage tile in the dashboard shows the storage consumed in Azure.</span></span> <span data-ttu-id="8b7ae-280">Storage usage is provided for:</span><span class="sxs-lookup"><span data-stu-id="8b7ae-280">Storage usage is provided for:</span></span>

* <span data-ttu-id="8b7ae-281">Cloud LRS storage usage associated with the vault</span><span class="sxs-lookup"><span data-stu-id="8b7ae-281">Cloud LRS storage usage associated with the vault</span></span>
* <span data-ttu-id="8b7ae-282">Cloud GRS storage usage associated with the vault</span><span class="sxs-lookup"><span data-stu-id="8b7ae-282">Cloud GRS storage usage associated with the vault</span></span>


## <a name="frequently-asked-questions"></a><span data-ttu-id="8b7ae-283">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="8b7ae-283">Frequently asked questions</span></span>

<span data-ttu-id="8b7ae-284">**Q1. How long does it take for the Azure backup agent job status to reflect in the portal?**</span><span class="sxs-lookup"><span data-stu-id="8b7ae-284">**Q1. How long does it take for the Azure backup agent job status to reflect in the portal?**</span></span>

<span data-ttu-id="8b7ae-285">A1.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-285">A1.</span></span> <span data-ttu-id="8b7ae-286">The Azure portal can take up to 15 mins to reflect the Azure backup agent job status.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-286">The Azure portal can take up to 15 mins to reflect the Azure backup agent job status.</span></span>

<span data-ttu-id="8b7ae-287">**Q2. When a backup job fails, how long does it take to raise an alert?**</span><span class="sxs-lookup"><span data-stu-id="8b7ae-287">**Q2. When a backup job fails, how long does it take to raise an alert?**</span></span>

<span data-ttu-id="8b7ae-288">A2.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-288">A2.</span></span> <span data-ttu-id="8b7ae-289">An alert is raised within 20 mins of the Azure backup failure.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-289">An alert is raised within 20 mins of the Azure backup failure.</span></span>

<span data-ttu-id="8b7ae-290">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span><span class="sxs-lookup"><span data-stu-id="8b7ae-290">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="8b7ae-291">A3.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-291">A3.</span></span> <span data-ttu-id="8b7ae-292">Yes.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-292">Yes.</span></span> <span data-ttu-id="8b7ae-293">In the following situations, notifications are not sent.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-293">In the following situations, notifications are not sent.</span></span>

* <span data-ttu-id="8b7ae-294">If notifications are configured hourly, and an alert is raised and resolved within the hour</span><span class="sxs-lookup"><span data-stu-id="8b7ae-294">If notifications are configured hourly, and an alert is raised and resolved within the hour</span></span>
* <span data-ttu-id="8b7ae-295">When a job is canceled</span><span class="sxs-lookup"><span data-stu-id="8b7ae-295">When a job is canceled</span></span>
* <span data-ttu-id="8b7ae-296">If a second backup job fails because the original backup job is in progress</span><span class="sxs-lookup"><span data-stu-id="8b7ae-296">If a second backup job fails because the original backup job is in progress</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="8b7ae-297">Troubleshooting Monitoring Issues</span><span class="sxs-lookup"><span data-stu-id="8b7ae-297">Troubleshooting Monitoring Issues</span></span>

<span data-ttu-id="8b7ae-298">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-298">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span></span>

<span data-ttu-id="8b7ae-299">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-299">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span></span> <span data-ttu-id="8b7ae-300">Occasionally this process can become stuck or shutdown.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-300">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="8b7ae-301">To verify the process isn't running, open **Task Manager**, and check ```OBRecoveryServicesManagementAgent``` is running.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-301">To verify the process isn't running, open **Task Manager**, and check ```OBRecoveryServicesManagementAgent``` is running.</span></span>

2. <span data-ttu-id="8b7ae-302">If the process isn't running, open **Control Panel**, and browse the list of services.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-302">If the process isn't running, open **Control Panel**, and browse the list of services.</span></span> <span data-ttu-id="8b7ae-303">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span><span class="sxs-lookup"><span data-stu-id="8b7ae-303">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="8b7ae-304">For further information, browse the logs at:</span><span class="sxs-lookup"><span data-stu-id="8b7ae-304">For further information, browse the logs at:</span></span><br/>
   <span data-ttu-id="8b7ae-305">`<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span><span class="sxs-lookup"><span data-stu-id="8b7ae-305">`<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="8b7ae-306">Next steps</span><span class="sxs-lookup"><span data-stu-id="8b7ae-306">Next steps</span></span>
* [<span data-ttu-id="8b7ae-307">Restore Windows Server or Windows Client from Azure</span><span class="sxs-lookup"><span data-stu-id="8b7ae-307">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="8b7ae-308">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="8b7ae-308">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="8b7ae-309">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="8b7ae-309">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
