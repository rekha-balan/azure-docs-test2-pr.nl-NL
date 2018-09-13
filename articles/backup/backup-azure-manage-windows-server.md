---
title: Manage Azure recovery services vaults and servers | Microsoft Docs
description: Use this tutorial to learn how to manage Azure recovery services vaults and servers.
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/9/2017
ms.author: markgal
ms.openlocfilehash: 5e6d32b2742beb00f7bf5758803bf0faf11418d1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563684"
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="5d5e6-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span><span class="sxs-lookup"><span data-stu-id="5d5e6-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-manage-windows-server.md)
> * [Classic](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="5d5e6-106">In this article you'll find an overview of the backup monitor and management tasks available through the Azure portal and the Microsoft Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-106">In this article you'll find an overview of the backup monitor and management tasks available through the Azure portal and the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="5d5e6-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="5d5e6-108">Open a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="5d5e6-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="5d5e6-109">The Recovery Services vault dashboard shows you the details or attributes of a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-109">The Recovery Services vault dashboard shows you the details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="5d5e6-110">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-110">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="5d5e6-111">On the Hub menu, click **More Services**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-111">On the Hub menu, click **More Services**.</span></span>

    ![Open list of Recovery Services vaults step 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="5d5e6-113">You want to open a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-113">You want to open a Recovery Services vault.</span></span> <span data-ttu-id="5d5e6-114">In the dialog box, start typing **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-114">In the dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="5d5e6-115">As you begin typing, the list will filter based on your input.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-115">As you begin typing, the list will filter based on your input.</span></span> <span data-ttu-id="5d5e6-116">Click **Recovery Services vaults** to display the list of Recovery Services vaults in your subscription.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-116">Click **Recovery Services vaults** to display the list of Recovery Services vaults in your subscription.</span></span>

    ![Create Recovery Services Vault step 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="5d5e6-118">The list of Recovery Services vaults opens.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-118">The list of Recovery Services vaults opens.</span></span>

    ![Create Recovery Services Vault step 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="5d5e6-120">From the list of vaults, select the name of the Recovery Services vault you want to open.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-120">From the list of vaults, select the name of the Recovery Services vault you want to open.</span></span> <span data-ttu-id="5d5e6-121">The Recovery Services vault dashboard blade opens.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-121">The Recovery Services vault dashboard blade opens.</span></span>

    ![recovery services vault dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="5d5e6-123">Now that you have opened the Recovery Services vault, try any of the monitoring or management tasks.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-123">Now that you have opened the Recovery Services vault, try any of the monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="5d5e6-124">Monitor backup jobs and alerts</span><span class="sxs-lookup"><span data-stu-id="5d5e6-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="5d5e6-125">You monitor jobs and alerts from the Recovery Services vault dashboard, where you see:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-125">You monitor jobs and alerts from the Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="5d5e6-126">Backup alerts details</span><span class="sxs-lookup"><span data-stu-id="5d5e6-126">Backup alerts details</span></span>
* <span data-ttu-id="5d5e6-127">Files and folders, as well as Azure virtual machines protected in the cloud</span><span class="sxs-lookup"><span data-stu-id="5d5e6-127">Files and folders, as well as Azure virtual machines protected in the cloud</span></span>
* <span data-ttu-id="5d5e6-128">Total storage consumed in Azure</span><span class="sxs-lookup"><span data-stu-id="5d5e6-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="5d5e6-129">Backup job status</span><span class="sxs-lookup"><span data-stu-id="5d5e6-129">Backup job status</span></span>

![Backup dashboard tasks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="5d5e6-131">Clicking the information in each of these tiles will open the associated blade where you manage related tasks.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-131">Clicking the information in each of these tiles will open the associated blade where you manage related tasks.</span></span>

<span data-ttu-id="5d5e6-132">From the top of the Dashboard:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-132">From the top of the Dashboard:</span></span>

* <span data-ttu-id="5d5e6-133">Settings provides access available backup tasks.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="5d5e6-134">Backup - helps you back up new files and folders (or Azure VMs) to the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-134">Backup - helps you back up new files and folders (or Azure VMs) to the Recovery Services vault.</span></span>
* <span data-ttu-id="5d5e6-135">Delete - If a recovery services vault is no longer being used, you can delete it to free up storage space.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-135">Delete - If a recovery services vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="5d5e6-136">Delete is only enabled after all protected servers have been deleted from the vault.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-136">Delete is only enabled after all protected servers have been deleted from the vault.</span></span>

![Backup dashboard tasks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="5d5e6-138">Alerts for backups using Azure backup agent:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="5d5e6-139">Alert Level</span><span class="sxs-lookup"><span data-stu-id="5d5e6-139">Alert Level</span></span> | <span data-ttu-id="5d5e6-140">Alerts sent</span><span class="sxs-lookup"><span data-stu-id="5d5e6-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="5d5e6-141">Critical</span><span class="sxs-lookup"><span data-stu-id="5d5e6-141">Critical</span></span> |<span data-ttu-id="5d5e6-142">Backup failure, recovery failure</span><span class="sxs-lookup"><span data-stu-id="5d5e6-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="5d5e6-143">Warning</span><span class="sxs-lookup"><span data-stu-id="5d5e6-143">Warning</span></span> |<span data-ttu-id="5d5e6-144">Backup completed with warnings (when fewer than one hundred files are not backed up due to corruption issues, and more than one million files are successfully backed up)</span><span class="sxs-lookup"><span data-stu-id="5d5e6-144">Backup completed with warnings (when fewer than one hundred files are not backed up due to corruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="5d5e6-145">Informational</span><span class="sxs-lookup"><span data-stu-id="5d5e6-145">Informational</span></span> |<span data-ttu-id="5d5e6-146">None</span><span class="sxs-lookup"><span data-stu-id="5d5e6-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="5d5e6-147">Manage Backup alerts</span><span class="sxs-lookup"><span data-stu-id="5d5e6-147">Manage Backup alerts</span></span>
<span data-ttu-id="5d5e6-148">Click the **Backup Alerts** tile to open the **Backup Alerts** blade and manage alerts.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-148">Click the **Backup Alerts** tile to open the **Backup Alerts** blade and manage alerts.</span></span>

![Backup alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="5d5e6-150">The Backup Alerts tile shows you the number of:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-150">The Backup Alerts tile shows you the number of:</span></span>

* <span data-ttu-id="5d5e6-151">critical alerts unresolved in last 24 hours</span><span class="sxs-lookup"><span data-stu-id="5d5e6-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="5d5e6-152">warning alerts unresolved in last 24 hours</span><span class="sxs-lookup"><span data-stu-id="5d5e6-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="5d5e6-153">Clicking on each of these links takes you to the **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span><span class="sxs-lookup"><span data-stu-id="5d5e6-153">Clicking on each of these links takes you to the **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="5d5e6-154">From the Backup Alerts blade, you:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-154">From the Backup Alerts blade, you:</span></span>

* <span data-ttu-id="5d5e6-155">Choose the appropriate information to include with your alerts.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-155">Choose the appropriate information to include with your alerts.</span></span>

    ![Choose columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="5d5e6-157">Filter alerts for severity, status and start/end times.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Filter alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="5d5e6-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Filter alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="5d5e6-161">If **Per Alert** is selected as the **Notify** frequency no grouping or reduction in emails occurs.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-161">If **Per Alert** is selected as the **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="5d5e6-162">Every alert results in 1 notification.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="5d5e6-163">This is the default setting and the resolution email is also sent out immediately.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-163">This is the default setting and the resolution email is also sent out immediately.</span></span>

<span data-ttu-id="5d5e6-164">If **Hourly Digest** is selected as the **Notify** frequency one email is sent to the user telling them that there are unresolved new alerts generated in the last hour.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-164">If **Hourly Digest** is selected as the **Notify** frequency one email is sent to the user telling them that there are unresolved new alerts generated in the last hour.</span></span> <span data-ttu-id="5d5e6-165">A resolution email is sent out at the end of the hour.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-165">A resolution email is sent out at the end of the hour.</span></span>

<span data-ttu-id="5d5e6-166">Alerts can be sent for the following severity levels:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-166">Alerts can be sent for the following severity levels:</span></span>

* <span data-ttu-id="5d5e6-167">critical</span><span class="sxs-lookup"><span data-stu-id="5d5e6-167">critical</span></span>
* <span data-ttu-id="5d5e6-168">warning</span><span class="sxs-lookup"><span data-stu-id="5d5e6-168">warning</span></span>
* <span data-ttu-id="5d5e6-169">information</span><span class="sxs-lookup"><span data-stu-id="5d5e6-169">information</span></span>

<span data-ttu-id="5d5e6-170">You inactivate the alert with the **inactivate** button in the job details blade.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-170">You inactivate the alert with the **inactivate** button in the job details blade.</span></span> <span data-ttu-id="5d5e6-171">When you click inactivate, you can provide resolution notes.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="5d5e6-172">You choose the columns you want to appear as part of the alert with the **Choose columns** button.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-172">You choose the columns you want to appear as part of the alert with the **Choose columns** button.</span></span>

> [!NOTE]
> From the **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="5d5e6-174">Manage Backup items</span><span class="sxs-lookup"><span data-stu-id="5d5e6-174">Manage Backup items</span></span>
<span data-ttu-id="5d5e6-175">Managing on-premises backups is now available in the management portal.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-175">Managing on-premises backups is now available in the management portal.</span></span> <span data-ttu-id="5d5e6-176">In the Backup section of the dashboard, the **Backup Items** tile shows the number of backup items protected to the vault.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-176">In the Backup section of the dashboard, the **Backup Items** tile shows the number of backup items protected to the vault.</span></span>

<span data-ttu-id="5d5e6-177">Click **File-Folders** in the Backup Items tile.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-177">Click **File-Folders** in the Backup Items tile.</span></span>

![Backup items tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="5d5e6-179">The Backup Items blade opens with the filter set to File-Folder where you see each specific backup item listed.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-179">The Backup Items blade opens with the filter set to File-Folder where you see each specific backup item listed.</span></span>

![Backup items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="5d5e6-181">If you select a specific backup item from the list, you see the essential details for that item.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-181">If you select a specific backup item from the list, you see the essential details for that item.</span></span>

> [!NOTE]
> From the **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from the drop down menu.
>
>

![Backup items from settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="5d5e6-184">Manage Backup jobs</span><span class="sxs-lookup"><span data-stu-id="5d5e6-184">Manage Backup jobs</span></span>
<span data-ttu-id="5d5e6-185">Backup jobs for both on-premises (when the on-premises server is backing up to Azure) and Azure backups are visible in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-185">Backup jobs for both on-premises (when the on-premises server is backing up to Azure) and Azure backups are visible in the dashboard.</span></span>

<span data-ttu-id="5d5e6-186">In the Backup section of the dashboard, the Backup job tile shows the number of jobs:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-186">In the Backup section of the dashboard, the Backup job tile shows the number of jobs:</span></span>

* <span data-ttu-id="5d5e6-187">in progress</span><span class="sxs-lookup"><span data-stu-id="5d5e6-187">in progress</span></span>
* <span data-ttu-id="5d5e6-188">failed in the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-188">failed in the last 24 hours.</span></span>

<span data-ttu-id="5d5e6-189">To manage your backup jobs, click the **Backup Jobs** tile, which opens the Backup Jobs blade.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-189">To manage your backup jobs, click the **Backup Jobs** tile, which opens the Backup Jobs blade.</span></span>

![Backup items from settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="5d5e6-191">You modify the information available in the Backup Jobs blade with the **Choose columns** button at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-191">You modify the information available in the Backup Jobs blade with the **Choose columns** button at the top of the page.</span></span>

<span data-ttu-id="5d5e6-192">Use the **Filter** button to select between Files and folders and Azure virtual machine backup.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-192">Use the **Filter** button to select between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="5d5e6-193">If you don't see your backed up files and folders, click **Filter** button at the top of the page and select **Files and folders** from the Item Type menu.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-193">If you don't see your backed up files and folders, click **Filter** button at the top of the page and select **Files and folders** from the Item Type menu.</span></span>

> [!NOTE]
> From the **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from the drop down menu.
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="5d5e6-195">Monitor Backup usage</span><span class="sxs-lookup"><span data-stu-id="5d5e6-195">Monitor Backup usage</span></span>
<span data-ttu-id="5d5e6-196">In the Backup section of the dashboard, the Backup Usage tile shows the storage consumed in Azure.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-196">In the Backup section of the dashboard, the Backup Usage tile shows the storage consumed in Azure.</span></span> <span data-ttu-id="5d5e6-197">Storage usage is provided for:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="5d5e6-198">Cloud LRS storage usage associated with the vault</span><span class="sxs-lookup"><span data-stu-id="5d5e6-198">Cloud LRS storage usage associated with the vault</span></span>
* <span data-ttu-id="5d5e6-199">Cloud GRS storage usage associated with the vault</span><span class="sxs-lookup"><span data-stu-id="5d5e6-199">Cloud GRS storage usage associated with the vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="5d5e6-200">Manage your production servers</span><span class="sxs-lookup"><span data-stu-id="5d5e6-200">Manage your production servers</span></span>
<span data-ttu-id="5d5e6-201">To manage your production servers, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-201">To manage your production servers, click **Settings**.</span></span>

<span data-ttu-id="5d5e6-202">Under Manage click **Backup infrastructure > Production Servers**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="5d5e6-203">The Production Servers blade lists of all your available production servers.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-203">The Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="5d5e6-204">Click on a server in the list to open the server details.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-204">Click on a server in the list to open the server details.</span></span>

![Protected items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-the-azure-backup-agent"></a><span data-ttu-id="5d5e6-206">Open the Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="5d5e6-206">Open the Azure Backup agent</span></span>
<span data-ttu-id="5d5e6-207">Open the **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="5d5e6-207">Open the **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="5d5e6-209">From the **Actions** available at the right of the backup agent console you perform the following management tasks:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-209">From the **Actions** available at the right of the backup agent console you perform the following management tasks:</span></span>

* <span data-ttu-id="5d5e6-210">Register Server</span><span class="sxs-lookup"><span data-stu-id="5d5e6-210">Register Server</span></span>
* <span data-ttu-id="5d5e6-211">Schedule Backup</span><span class="sxs-lookup"><span data-stu-id="5d5e6-211">Schedule Backup</span></span>
* <span data-ttu-id="5d5e6-212">Back Up now</span><span class="sxs-lookup"><span data-stu-id="5d5e6-212">Back Up now</span></span>
* <span data-ttu-id="5d5e6-213">Change Properties</span><span class="sxs-lookup"><span data-stu-id="5d5e6-213">Change Properties</span></span>

![Microsoft Azure Backup agent console actions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).
>
>

## <a name="modify-the-backup-schedule"></a><span data-ttu-id="5d5e6-216">Modify the backup schedule</span><span class="sxs-lookup"><span data-stu-id="5d5e6-216">Modify the backup schedule</span></span>
1. <span data-ttu-id="5d5e6-217">In the Microsoft Azure Backup agent click **Schedule Backup**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-217">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="5d5e6-219">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-219">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="5d5e6-221">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-221">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="5d5e6-222">You can also set **Exclusion Settings** from this page in the wizard.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-222">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="5d5e6-223">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="5d5e6-223">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="5d5e6-224">Select the files and folders you want to back up and click **Okay**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-224">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="5d5e6-226">Specify the **backup schedule** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-226">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="5d5e6-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Items for Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).
   >

6. <span data-ttu-id="5d5e6-230">Select the **Retention Policy** for the backup copy and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-230">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Items for Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="5d5e6-232">On the **Confirmation** screen review the information and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-232">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="5d5e6-233">Once the wizard finishes creating the **backup schedule**, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-233">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="5d5e6-234">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-234">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="5d5e6-235">Enable Network Throttling</span><span class="sxs-lookup"><span data-stu-id="5d5e6-235">Enable Network Throttling</span></span>

<span data-ttu-id="5d5e6-236">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-236">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="5d5e6-237">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-237">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="5d5e6-238">Throttling of data transfer applies to back up and restore activities.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-238">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="5d5e6-239">To enable throttling:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-239">To enable throttling:</span></span>

1. <span data-ttu-id="5d5e6-240">In the **Backup agent**, click **Change Properties**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-240">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="5d5e6-241">On the \*\*Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-241">On the \*\*Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Network throttling](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="5d5e6-243">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-243">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="5d5e6-244">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span><span class="sxs-lookup"><span data-stu-id="5d5e6-244">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="5d5e6-245">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-245">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="5d5e6-246">The time outside of the designated Work hours is considered to be non-work hours.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-246">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
3. <span data-ttu-id="5d5e6-247">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="5d5e6-248">Manage exclusion settings</span><span class="sxs-lookup"><span data-stu-id="5d5e6-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="5d5e6-249">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="5d5e6-249">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="5d5e6-251">In the Microsoft Azure Backup agent click **Schedule Backup**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-251">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="5d5e6-253">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-253">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="5d5e6-255">Click **Exclusions Settings**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-255">Click **Exclusions Settings**.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="5d5e6-257">Click **Add Exclusion**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-257">Click **Add Exclusion**.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="5d5e6-259">Select the location and then, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-259">Select the location and then, click **OK**.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="5d5e6-261">Add the file extension in the **File Type** field.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-261">Add the file extension in the **File Type** field.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="5d5e6-263">Adding an .mp3 extension</span><span class="sxs-lookup"><span data-stu-id="5d5e6-263">Adding an .mp3 extension</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="5d5e6-265">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span><span class="sxs-lookup"><span data-stu-id="5d5e6-265">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="5d5e6-267">When you've added all the extensions, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-267">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="5d5e6-268">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-268">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="5d5e6-270">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="5d5e6-270">Frequently asked questions</span></span>
<span data-ttu-id="5d5e6-271">**Q1. The backup job status shows as completed in the Azure backup agent, why doesn't it get reflected immediately in portal?**</span><span class="sxs-lookup"><span data-stu-id="5d5e6-271">**Q1. The backup job status shows as completed in the Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="5d5e6-272">A1.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-272">A1.</span></span> <span data-ttu-id="5d5e6-273">There is at maximum delay of 15 mins between the backup job status reflected in the Azure backup agent and the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-273">There is at maximum delay of 15 mins between the backup job status reflected in the Azure backup agent and the Azure portal.</span></span>

<span data-ttu-id="5d5e6-274">**Q.2 When a backup job fails, how long does it take to raise an alert?**</span><span class="sxs-lookup"><span data-stu-id="5d5e6-274">**Q.2 When a backup job fails, how long does it take to raise an alert?**</span></span>

<span data-ttu-id="5d5e6-275">A.2 An alert is raised within 20 mins of the Azure backup failure.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-275">A.2 An alert is raised within 20 mins of the Azure backup failure.</span></span>

<span data-ttu-id="5d5e6-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span><span class="sxs-lookup"><span data-stu-id="5d5e6-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="5d5e6-277">A3.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-277">A3.</span></span> <span data-ttu-id="5d5e6-278">Below are the cases when the notification will not be sent in order to reduce the alert noise:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-278">Below are the cases when the notification will not be sent in order to reduce the alert noise:</span></span>

* <span data-ttu-id="5d5e6-279">If notifications are configured hourly and an alert is raised and resolved within the hour</span><span class="sxs-lookup"><span data-stu-id="5d5e6-279">If notifications are configured hourly and an alert is raised and resolved within the hour</span></span>
* <span data-ttu-id="5d5e6-280">Job is canceled.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-280">Job is canceled.</span></span>
* <span data-ttu-id="5d5e6-281">Second backup job failed because original backup job is in progress.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="5d5e6-282">Troubleshooting Monitoring Issues</span><span class="sxs-lookup"><span data-stu-id="5d5e6-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="5d5e6-283">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-283">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span></span>

<span data-ttu-id="5d5e6-284">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-284">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span></span> <span data-ttu-id="5d5e6-285">Occasionally this process can become stuck or shutdown.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="5d5e6-286">To verify the process is not running, open **Task Manager** and check if the ```OBRecoveryServicesManagementAgent``` process is running.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-286">To verify the process is not running, open **Task Manager** and check if the ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="5d5e6-287">Assuming that the process is not running, open **Control Panel** and browse the list of services.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-287">Assuming that the process is not running, open **Control Panel** and browse the list of services.</span></span> <span data-ttu-id="5d5e6-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span><span class="sxs-lookup"><span data-stu-id="5d5e6-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="5d5e6-289">For further information, browse the logs at:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-289">For further information, browse the logs at:</span></span><br/>
   <span data-ttu-id="5d5e6-290">`<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span><span class="sxs-lookup"><span data-stu-id="5d5e6-290">`<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="5d5e6-291">Next steps</span><span class="sxs-lookup"><span data-stu-id="5d5e6-291">Next steps</span></span>
* [<span data-ttu-id="5d5e6-292">Restore Windows Server or Windows Client from Azure</span><span class="sxs-lookup"><span data-stu-id="5d5e6-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="5d5e6-293">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="5d5e6-293">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="5d5e6-294">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="5d5e6-294">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>

































