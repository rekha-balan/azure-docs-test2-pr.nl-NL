---
title: Manage Azure Backup vaults and servers Azure using the classic deployment model | Microsoft Docs
description: Use this tutorial to learn how to manage Azure Backup vaults and servers.
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: markgal;
ms.openlocfilehash: 115e3ff86b6612d0f4e0b12e301622750f512efc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554566"
---
# <a name="manage-azure-backup-vaults-and-servers-using-the-classic-deployment-model"></a><span data-ttu-id="57c56-103">Manage Azure Backup vaults and servers using the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="57c56-103">Manage Azure Backup vaults and servers using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-manage-windows-server.md)
> * [Classic](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="57c56-106">In this article you'll find an overview of the backup management tasks available through the Azure classic portal and the Microsoft Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="57c56-106">In this article you'll find an overview of the backup management tasks available through the Azure classic portal and the Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model.

## <a name="management-portal-tasks"></a><span data-ttu-id="57c56-110">Management portal tasks</span><span class="sxs-lookup"><span data-stu-id="57c56-110">Management portal tasks</span></span>
1. <span data-ttu-id="57c56-111">Sign in to the [Management Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="57c56-111">Sign in to the [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="57c56-112">Click **Recovery Services**, then click the name of backup vault to view the Quick Start page.</span><span class="sxs-lookup"><span data-stu-id="57c56-112">Click **Recovery Services**, then click the name of backup vault to view the Quick Start page.</span></span>

    ![Recovery services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="57c56-114">By selecting the options at the top of the Quick Start page, you can see the available management tasks.</span><span class="sxs-lookup"><span data-stu-id="57c56-114">By selecting the options at the top of the Quick Start page, you can see the available management tasks.</span></span>

![Manage tabs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="57c56-116">Dashboard</span><span class="sxs-lookup"><span data-stu-id="57c56-116">Dashboard</span></span>
<span data-ttu-id="57c56-117">Select **Dashboard** to see the usage overview for the server.</span><span class="sxs-lookup"><span data-stu-id="57c56-117">Select **Dashboard** to see the usage overview for the server.</span></span> <span data-ttu-id="57c56-118">The **usage overview** includes:</span><span class="sxs-lookup"><span data-stu-id="57c56-118">The **usage overview** includes:</span></span>

* <span data-ttu-id="57c56-119">The number of Windows Servers registered to cloud</span><span class="sxs-lookup"><span data-stu-id="57c56-119">The number of Windows Servers registered to cloud</span></span>
* <span data-ttu-id="57c56-120">The number of Azure virtual machines protected in cloud</span><span class="sxs-lookup"><span data-stu-id="57c56-120">The number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="57c56-121">The total storage consumed in Azure</span><span class="sxs-lookup"><span data-stu-id="57c56-121">The total storage consumed in Azure</span></span>
* <span data-ttu-id="57c56-122">The status of recent jobs</span><span class="sxs-lookup"><span data-stu-id="57c56-122">The status of recent jobs</span></span>

<span data-ttu-id="57c56-123">At the bottom of the Dashboard you can perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="57c56-123">At the bottom of the Dashboard you can perform the following tasks:</span></span>

* <span data-ttu-id="57c56-124">**Manage certificate** - If a certificate was used to register the server, then use this to update the certificate.</span><span class="sxs-lookup"><span data-stu-id="57c56-124">**Manage certificate** - If a certificate was used to register the server, then use this to update the certificate.</span></span> <span data-ttu-id="57c56-125">If you are using vault credentials, do not use **Manage certificate**.</span><span class="sxs-lookup"><span data-stu-id="57c56-125">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="57c56-126">**Delete** - Deletes the current backup vault.</span><span class="sxs-lookup"><span data-stu-id="57c56-126">**Delete** - Deletes the current backup vault.</span></span> <span data-ttu-id="57c56-127">If a backup vault is no longer being used, you can delete it to free up storage space.</span><span class="sxs-lookup"><span data-stu-id="57c56-127">If a backup vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="57c56-128">**Delete** is only enabled after all registered servers have been deleted from the vault.</span><span class="sxs-lookup"><span data-stu-id="57c56-128">**Delete** is only enabled after all registered servers have been deleted from the vault.</span></span>

![Backup dashboard tasks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="57c56-130">Registered items</span><span class="sxs-lookup"><span data-stu-id="57c56-130">Registered items</span></span>
<span data-ttu-id="57c56-131">Select **Registered Items** to view the names of the servers that are registered to this vault.</span><span class="sxs-lookup"><span data-stu-id="57c56-131">Select **Registered Items** to view the names of the servers that are registered to this vault.</span></span>

![Registered items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="57c56-133">The **Type** filter defaults to Azure Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="57c56-133">The **Type** filter defaults to Azure Virtual Machine.</span></span> <span data-ttu-id="57c56-134">To view the names of the servers that are registered to this vault, select **Windows server** from the drop down menu.</span><span class="sxs-lookup"><span data-stu-id="57c56-134">To view the names of the servers that are registered to this vault, select **Windows server** from the drop down menu.</span></span>

<span data-ttu-id="57c56-135">From here you can perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="57c56-135">From here you can perform the following tasks:</span></span>

* <span data-ttu-id="57c56-136">**Allow Re-registration** - When this option is selected for a server you can use the **Registration Wizard** in the on-premises Microsoft Azure Backup agent to register the server with the backup vault a second time.</span><span class="sxs-lookup"><span data-stu-id="57c56-136">**Allow Re-registration** - When this option is selected for a server you can use the **Registration Wizard** in the on-premises Microsoft Azure Backup agent to register the server with the backup vault a second time.</span></span> <span data-ttu-id="57c56-137">You might need to re-register due to an error in the certificate or if a server had to be rebuilt.</span><span class="sxs-lookup"><span data-stu-id="57c56-137">You might need to re-register due to an error in the certificate or if a server had to be rebuilt.</span></span>
* <span data-ttu-id="57c56-138">**Delete** - Deletes a server from the backup vault.</span><span class="sxs-lookup"><span data-stu-id="57c56-138">**Delete** - Deletes a server from the backup vault.</span></span> <span data-ttu-id="57c56-139">All of the stored data associated with the server is deleted immediately.</span><span class="sxs-lookup"><span data-stu-id="57c56-139">All of the stored data associated with the server is deleted immediately.</span></span>

    ![Registered items tasks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="57c56-141">Protected items</span><span class="sxs-lookup"><span data-stu-id="57c56-141">Protected items</span></span>
<span data-ttu-id="57c56-142">Select **Protected Items** to view the items that have been backed up from the servers.</span><span class="sxs-lookup"><span data-stu-id="57c56-142">Select **Protected Items** to view the items that have been backed up from the servers.</span></span>

![Protected items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="57c56-144">Configure</span><span class="sxs-lookup"><span data-stu-id="57c56-144">Configure</span></span>
<span data-ttu-id="57c56-145">From the **Configure** tab you can select the appropriate storage redundancy option.</span><span class="sxs-lookup"><span data-stu-id="57c56-145">From the **Configure** tab you can select the appropriate storage redundancy option.</span></span> <span data-ttu-id="57c56-146">The best time to select the storage redundancy option is right after creating a vault and before any machines are registered to it.</span><span class="sxs-lookup"><span data-stu-id="57c56-146">The best time to select the storage redundancy option is right after creating a vault and before any machines are registered to it.</span></span>

> [!WARNING]
> Once an item has been registered to the vault, the storage redundancy option is locked and cannot be modified.
>
>

![Configure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="57c56-149">See this article for more information about [storage redundancy](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="57c56-149">See this article for more information about [storage redundancy](../storage/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="57c56-150">Microsoft Azure Backup agent tasks</span><span class="sxs-lookup"><span data-stu-id="57c56-150">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="57c56-151">Console</span><span class="sxs-lookup"><span data-stu-id="57c56-151">Console</span></span>
<span data-ttu-id="57c56-152">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="57c56-152">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Backup agent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="57c56-154">From the **Actions** available at the right of the backup agent console you can perform the following management tasks:</span><span class="sxs-lookup"><span data-stu-id="57c56-154">From the **Actions** available at the right of the backup agent console you can perform the following management tasks:</span></span>

* <span data-ttu-id="57c56-155">Register Server</span><span class="sxs-lookup"><span data-stu-id="57c56-155">Register Server</span></span>
* <span data-ttu-id="57c56-156">Schedule Backup</span><span class="sxs-lookup"><span data-stu-id="57c56-156">Schedule Backup</span></span>
* <span data-ttu-id="57c56-157">Back Up now</span><span class="sxs-lookup"><span data-stu-id="57c56-157">Back Up now</span></span>
* <span data-ttu-id="57c56-158">Change Properties</span><span class="sxs-lookup"><span data-stu-id="57c56-158">Change Properties</span></span>

![Agent console actions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="57c56-161">Modify an existing backup</span><span class="sxs-lookup"><span data-stu-id="57c56-161">Modify an existing backup</span></span>
1. <span data-ttu-id="57c56-162">In the Microsoft Azure Backup agent click **Schedule Backup**.</span><span class="sxs-lookup"><span data-stu-id="57c56-162">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="57c56-164">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="57c56-164">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Modify a scheduled backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="57c56-166">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span><span class="sxs-lookup"><span data-stu-id="57c56-166">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="57c56-167">You can also set **Exclusion Settings** from this page in the wizard.</span><span class="sxs-lookup"><span data-stu-id="57c56-167">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="57c56-168">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="57c56-168">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="57c56-169">Select the files and folders you want to back up and click **Okay**.</span><span class="sxs-lookup"><span data-stu-id="57c56-169">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Add items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="57c56-171">Specify the **backup schedule** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="57c56-171">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="57c56-172">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span><span class="sxs-lookup"><span data-stu-id="57c56-172">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Specify your Backup schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).
   >
   >
6. <span data-ttu-id="57c56-175">Select the **Retention Policy** for the backup copy and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="57c56-175">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Select your retention policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="57c56-177">On the **Confirmation** screen review the information and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="57c56-177">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="57c56-178">Once the wizard finishes creating the **backup schedule**, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="57c56-178">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="57c56-179">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span><span class="sxs-lookup"><span data-stu-id="57c56-179">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="57c56-180">Enable Network Throttling</span><span class="sxs-lookup"><span data-stu-id="57c56-180">Enable Network Throttling</span></span>
<span data-ttu-id="57c56-181">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span><span class="sxs-lookup"><span data-stu-id="57c56-181">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="57c56-182">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span><span class="sxs-lookup"><span data-stu-id="57c56-182">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="57c56-183">Throttling of data transfer applies to back up and restore activities.</span><span class="sxs-lookup"><span data-stu-id="57c56-183">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="57c56-184">To enable throttling:</span><span class="sxs-lookup"><span data-stu-id="57c56-184">To enable throttling:</span></span>

1. <span data-ttu-id="57c56-185">In the **Backup agent**, click **Change Properties**.</span><span class="sxs-lookup"><span data-stu-id="57c56-185">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="57c56-186">Select the **Enable internet bandwidth usage throttling for backup operations** checkbox.</span><span class="sxs-lookup"><span data-stu-id="57c56-186">Select the **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Network throttling](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="57c56-188">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span><span class="sxs-lookup"><span data-stu-id="57c56-188">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="57c56-189">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span><span class="sxs-lookup"><span data-stu-id="57c56-189">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="57c56-190">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span><span class="sxs-lookup"><span data-stu-id="57c56-190">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="57c56-191">The time outside of the designated Work hours is considered to be non-work hours.</span><span class="sxs-lookup"><span data-stu-id="57c56-191">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
4. <span data-ttu-id="57c56-192">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="57c56-192">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="57c56-193">Exclusion settings</span><span class="sxs-lookup"><span data-stu-id="57c56-193">Exclusion settings</span></span>
1. <span data-ttu-id="57c56-194">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span><span class="sxs-lookup"><span data-stu-id="57c56-194">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Open backup agent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="57c56-196">In the Microsoft Azure Backup agent click **Schedule Backup**.</span><span class="sxs-lookup"><span data-stu-id="57c56-196">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Schedule a Windows Server Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="57c56-198">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="57c56-198">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Modify a schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="57c56-200">Click **Exclusions Settings**.</span><span class="sxs-lookup"><span data-stu-id="57c56-200">Click **Exclusions Settings**.</span></span>

    ![Select items to exclude](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="57c56-202">Click **Add Exclusion**.</span><span class="sxs-lookup"><span data-stu-id="57c56-202">Click **Add Exclusion**.</span></span>

    ![Add exclusions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="57c56-204">Select the location and then, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="57c56-204">Select the location and then, click **OK**.</span></span>

    ![Select a location for exclusion](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="57c56-206">Add the file extension in the **File Type** field.</span><span class="sxs-lookup"><span data-stu-id="57c56-206">Add the file extension in the **File Type** field.</span></span>

    ![Exclude by file type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="57c56-208">Adding an .mp3 extension</span><span class="sxs-lookup"><span data-stu-id="57c56-208">Adding an .mp3 extension</span></span>

    ![File type example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="57c56-210">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span><span class="sxs-lookup"><span data-stu-id="57c56-210">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Another file type example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="57c56-212">When you've added all the extensions, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="57c56-212">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="57c56-213">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="57c56-213">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Exclusion confirmation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="57c56-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="57c56-215">Next steps</span></span>
* [<span data-ttu-id="57c56-216">Restore Windows Server or Windows Client from Azure</span><span class="sxs-lookup"><span data-stu-id="57c56-216">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="57c56-217">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="57c56-217">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="57c56-218">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="57c56-218">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>

























