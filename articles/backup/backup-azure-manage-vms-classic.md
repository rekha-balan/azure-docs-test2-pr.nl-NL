---
title: Manage and monitor Azure virtual machine backups | Microsoft Docs
description: Learn how to manage and monitor an Azure virtual machine backups
services: backup
documentationcenter: ''
author: trinadhk
manager: shreeshd
editor: ''
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/31/2016
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a5a2d32132f1342befc29c6f49c4e44c1feb187
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554039"
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-the-classic-portal"></a><span data-ttu-id="1db59-103">Manage common Azure Backup jobs and trigger alerts in the classic portal</span><span class="sxs-lookup"><span data-stu-id="1db59-103">Manage common Azure Backup jobs and trigger alerts in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [Manage Azure VM backups](backup-azure-manage-vms.md)
> * [Manage Classic VM backups](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="1db59-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span><span class="sxs-lookup"><span data-stu-id="1db59-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). See [Prepare your environment to back up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.
>
>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="1db59-109">Manage protected virtual machines</span><span class="sxs-lookup"><span data-stu-id="1db59-109">Manage protected virtual machines</span></span>
<span data-ttu-id="1db59-110">To manage protected virtual machines:</span><span class="sxs-lookup"><span data-stu-id="1db59-110">To manage protected virtual machines:</span></span>

1. <span data-ttu-id="1db59-111">To view and manage backup settings for a virtual machine click the **Protected Items** tab.</span><span class="sxs-lookup"><span data-stu-id="1db59-111">To view and manage backup settings for a virtual machine click the **Protected Items** tab.</span></span>
2. <span data-ttu-id="1db59-112">Click on the name of a protected item to see the **Backup Details** tab, which shows you information about the last backup.</span><span class="sxs-lookup"><span data-stu-id="1db59-112">Click on the name of a protected item to see the **Backup Details** tab, which shows you information about the last backup.</span></span>

    ![Virtual machine backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="1db59-114">To view and manage backup policy settings for a virtual machine click the **Policies** tab.</span><span class="sxs-lookup"><span data-stu-id="1db59-114">To view and manage backup policy settings for a virtual machine click the **Policies** tab.</span></span>

    ![Virtual machine policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="1db59-116">The **Backup Policies** tab shows you the existing policy.</span><span class="sxs-lookup"><span data-stu-id="1db59-116">The **Backup Policies** tab shows you the existing policy.</span></span> <span data-ttu-id="1db59-117">You can modify as needed.</span><span class="sxs-lookup"><span data-stu-id="1db59-117">You can modify as needed.</span></span> <span data-ttu-id="1db59-118">If you need to create a new policy click **Create** on the **Policies** page.</span><span class="sxs-lookup"><span data-stu-id="1db59-118">If you need to create a new policy click **Create** on the **Policies** page.</span></span> <span data-ttu-id="1db59-119">Note that if you want to remove a policy it shouldn't have any virtual machines associated with it.</span><span class="sxs-lookup"><span data-stu-id="1db59-119">Note that if you want to remove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Virtual machine policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="1db59-121">You can get more information about actions or status for a virtual machine on the **Jobs** page.</span><span class="sxs-lookup"><span data-stu-id="1db59-121">You can get more information about actions or status for a virtual machine on the **Jobs** page.</span></span> <span data-ttu-id="1db59-122">Click a job in the list to get more details, or filter jobs for a specific virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1db59-122">Click a job in the list to get more details, or filter jobs for a specific virtual machine.</span></span>

    ![Jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="1db59-124">On-demand backup of a virtual machine</span><span class="sxs-lookup"><span data-stu-id="1db59-124">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="1db59-125">You can take an on-demand backup of a virtual machine once it is configured for protection.</span><span class="sxs-lookup"><span data-stu-id="1db59-125">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="1db59-126">If the initial backup is pending for the virtual machine, on-demand backup will create a full copy of the virtual machine in Azure backup vault.</span><span class="sxs-lookup"><span data-stu-id="1db59-126">If the initial backup is pending for the virtual machine, on-demand backup will create a full copy of the virtual machine in Azure backup vault.</span></span> <span data-ttu-id="1db59-127">If first backup is completed, on-demand backup will only send changes from previous backup to Azure backup vault i.e. it is always incremental.</span><span class="sxs-lookup"><span data-stu-id="1db59-127">If first backup is completed, on-demand backup will only send changes from previous backup to Azure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> Retention range of an on-demand backup is set to retention value specified for Daily retention in backup policy corresponding to the VM.  
>
>

<span data-ttu-id="1db59-129">To take an on-demand backup of a virtual machine:</span><span class="sxs-lookup"><span data-stu-id="1db59-129">To take an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="1db59-130">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span><span class="sxs-lookup"><span data-stu-id="1db59-130">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![VM Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="1db59-132">Select the virtual machine on which you want to take an on-demand backup and click on **Backup Now** button at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1db59-132">Select the virtual machine on which you want to take an on-demand backup and click on **Backup Now** button at the bottom of the page.</span></span>

    ![Back up now](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="1db59-134">This will create a backup job on the selected virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1db59-134">This will create a backup job on the selected virtual machine.</span></span> <span data-ttu-id="1db59-135">Retention range of recovery point created through this job will be same as that specified in the policy associated with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1db59-135">Retention range of recovery point created through this job will be same as that specified in the policy associated with the virtual machine.</span></span>

    ![Creating backup job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > To view the policy associated with a virtual machine, drill down into virtual machine in the **Protected Items** page and go to backup policy tab.
   >
   >
3. <span data-ttu-id="1db59-138">Once the job is created, you can click on **View job** button in the toast bar to see the corresponding job in the jobs page.</span><span class="sxs-lookup"><span data-stu-id="1db59-138">Once the job is created, you can click on **View job** button in the toast bar to see the corresponding job in the jobs page.</span></span>

    ![Backup job created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="1db59-140">After successful completion of the job, a recovery point will be created which you can use to restore the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1db59-140">After successful completion of the job, a recovery point will be created which you can use to restore the virtual machine.</span></span> <span data-ttu-id="1db59-141">This will also increment the recovery point column value by 1 in **Protected Items** page.</span><span class="sxs-lookup"><span data-stu-id="1db59-141">This will also increment the recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="1db59-142">Stop protecting virtual machines</span><span class="sxs-lookup"><span data-stu-id="1db59-142">Stop protecting virtual machines</span></span>
<span data-ttu-id="1db59-143">You can choose to stop the future backups of a virtual machine with the following options:</span><span class="sxs-lookup"><span data-stu-id="1db59-143">You can choose to stop the future backups of a virtual machine with the following options:</span></span>

* <span data-ttu-id="1db59-144">Retain backup data associated with virtual machine in Azure Backup vault</span><span class="sxs-lookup"><span data-stu-id="1db59-144">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="1db59-145">Delete backup data associated with virtual machine</span><span class="sxs-lookup"><span data-stu-id="1db59-145">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="1db59-146">If you have selected to retain backup data associated with virtual machine, you can use the backup data to restore the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1db59-146">If you have selected to retain backup data associated with virtual machine, you can use the backup data to restore the virtual machine.</span></span> <span data-ttu-id="1db59-147">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="1db59-147">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="1db59-148">To Stop protection for a virtual machine:</span><span class="sxs-lookup"><span data-stu-id="1db59-148">To Stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="1db59-149">Navigate to **Protected Items** page and select **Azure virtual machine** as the filter type (if not already selected) and click on **Select** button.</span><span class="sxs-lookup"><span data-stu-id="1db59-149">Navigate to **Protected Items** page and select **Azure virtual machine** as the filter type (if not already selected) and click on **Select** button.</span></span>

    ![VM Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="1db59-151">Select the virtual machine and click on **Stop Protection** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1db59-151">Select the virtual machine and click on **Stop Protection** at the bottom of the page.</span></span>

    ![Stop protection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="1db59-153">By default, Azure Backup doesn’t delete the backup data associated with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1db59-153">By default, Azure Backup doesn’t delete the backup data associated with the virtual machine.</span></span>

    ![Confirm stop protection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="1db59-155">If you want to delete backup data, select the check box.</span><span class="sxs-lookup"><span data-stu-id="1db59-155">If you want to delete backup data, select the check box.</span></span>

    ![Checkbox](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="1db59-157">Please select a reason for stopping the backup.</span><span class="sxs-lookup"><span data-stu-id="1db59-157">Please select a reason for stopping the backup.</span></span> <span data-ttu-id="1db59-158">While this is optional, providing a reason will help Azure Backup to work on the feedback and prioritize the customer scenarios.</span><span class="sxs-lookup"><span data-stu-id="1db59-158">While this is optional, providing a reason will help Azure Backup to work on the feedback and prioritize the customer scenarios.</span></span>
4. <span data-ttu-id="1db59-159">Click on **Submit** button to submit the **Stop protection** job.</span><span class="sxs-lookup"><span data-stu-id="1db59-159">Click on **Submit** button to submit the **Stop protection** job.</span></span> <span data-ttu-id="1db59-160">Click on **View Job** to see the corresponding the job in **Jobs** page.</span><span class="sxs-lookup"><span data-stu-id="1db59-160">Click on **View Job** to see the corresponding the job in **Jobs** page.</span></span>

    ![Stop protection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="1db59-162">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes to **Protection Stopped**.</span><span class="sxs-lookup"><span data-stu-id="1db59-162">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes to **Protection Stopped**.</span></span> <span data-ttu-id="1db59-163">The data remains with Azure Backup until it is explicitly deleted.</span><span class="sxs-lookup"><span data-stu-id="1db59-163">The data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="1db59-164">You can always delete the data by selecting the virtual machine in the **Protected Items** page and clicking **Delete**.</span><span class="sxs-lookup"><span data-stu-id="1db59-164">You can always delete the data by selecting the virtual machine in the **Protected Items** page and clicking **Delete**.</span></span>

    ![Stopped protection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="1db59-166">If you have selected the **Delete associated backup data** option, the virtual machine won’t be part of the **Protected Items** page.</span><span class="sxs-lookup"><span data-stu-id="1db59-166">If you have selected the **Delete associated backup data** option, the virtual machine won’t be part of the **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="1db59-167">Re-protect Virtual machine</span><span class="sxs-lookup"><span data-stu-id="1db59-167">Re-protect Virtual machine</span></span>
<span data-ttu-id="1db59-168">If you have not selected the **Delete associate backup data** option in **Stop Protection**, you can re-protect the virtual machine by following the steps similar to backing up registered virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1db59-168">If you have not selected the **Delete associate backup data** option in **Stop Protection**, you can re-protect the virtual machine by following the steps similar to backing up registered virtual machines.</span></span> <span data-ttu-id="1db59-169">Once protected, this virtual machine will have backup data retained prior to stop protection and recovery points created after re-protect.</span><span class="sxs-lookup"><span data-stu-id="1db59-169">Once protected, this virtual machine will have backup data retained prior to stop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="1db59-170">After re-protect, the virtual machine’s protection status will be changed to **Protected** if there are recovery points prior to **Stop Protection**.</span><span class="sxs-lookup"><span data-stu-id="1db59-170">After re-protect, the virtual machine’s protection status will be changed to **Protected** if there are recovery points prior to **Stop Protection**.</span></span>

  ![Reprotected VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="1db59-173">Unregister virtual machines</span><span class="sxs-lookup"><span data-stu-id="1db59-173">Unregister virtual machines</span></span>
<span data-ttu-id="1db59-174">If you want to remove the virtual machine from the backup vault:</span><span class="sxs-lookup"><span data-stu-id="1db59-174">If you want to remove the virtual machine from the backup vault:</span></span>

1. <span data-ttu-id="1db59-175">Click on the **UNREGISTER** button at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1db59-175">Click on the **UNREGISTER** button at the bottom of the page.</span></span>

    ![Disable protection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="1db59-177">A toast notification will appear at the bottom of the screen requesting confirmation.</span><span class="sxs-lookup"><span data-stu-id="1db59-177">A toast notification will appear at the bottom of the screen requesting confirmation.</span></span> <span data-ttu-id="1db59-178">Click **YES** to continue.</span><span class="sxs-lookup"><span data-stu-id="1db59-178">Click **YES** to continue.</span></span>

    ![Disable protection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="1db59-180">Delete Backup data</span><span class="sxs-lookup"><span data-stu-id="1db59-180">Delete Backup data</span></span>
<span data-ttu-id="1db59-181">You can delete the backup data associated with a virtual machine, either:</span><span class="sxs-lookup"><span data-stu-id="1db59-181">You can delete the backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="1db59-182">During Stop Protection Job</span><span class="sxs-lookup"><span data-stu-id="1db59-182">During Stop Protection Job</span></span>
* <span data-ttu-id="1db59-183">After a stop protection job is completed on a virtual machine</span><span class="sxs-lookup"><span data-stu-id="1db59-183">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="1db59-184">To delete backup data on a virtual machine, which is in the *Protection Stopped* state post successful completion of a **Stop Backup** job:</span><span class="sxs-lookup"><span data-stu-id="1db59-184">To delete backup data on a virtual machine, which is in the *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="1db59-185">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as *type* and click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="1db59-185">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as *type* and click the **Select** button.</span></span>

    ![VM Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="1db59-187">Select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1db59-187">Select the virtual machine.</span></span> <span data-ttu-id="1db59-188">The virtual machine will be in **Protection Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="1db59-188">The virtual machine will be in **Protection Stopped** state.</span></span>

    ![Protection stopped](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="1db59-190">Click the **DELETE** button at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1db59-190">Click the **DELETE** button at the bottom of the page.</span></span>

    ![Delete backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="1db59-192">In the **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="1db59-192">In the **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![Delete backup data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="1db59-194">This will create a job to delete backup data of selected virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1db59-194">This will create a job to delete backup data of selected virtual machine.</span></span> <span data-ttu-id="1db59-195">Click **View job** to see corresponding job in Jobs page.</span><span class="sxs-lookup"><span data-stu-id="1db59-195">Click **View job** to see corresponding job in Jobs page.</span></span>

    ![Data deletion successful](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="1db59-197">Once the job is completed, the entry corresponding to the virtual machine will be removed from **Protected items** page.</span><span class="sxs-lookup"><span data-stu-id="1db59-197">Once the job is completed, the entry corresponding to the virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="1db59-198">Dashboard</span><span class="sxs-lookup"><span data-stu-id="1db59-198">Dashboard</span></span>
<span data-ttu-id="1db59-199">On the **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="1db59-199">On the **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in the last 24 hours.</span></span> <span data-ttu-id="1db59-200">You can view backup status and any associated backup errors.</span><span class="sxs-lookup"><span data-stu-id="1db59-200">You can view backup status and any associated backup errors.</span></span>

![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> Values in the dashboard are refreshed once every 24 hours.
>
>

## <a name="auditing-operations"></a><span data-ttu-id="1db59-203">Auditing Operations</span><span class="sxs-lookup"><span data-stu-id="1db59-203">Auditing Operations</span></span>
<span data-ttu-id="1db59-204">Azure backup provides review of the "operation logs" of backup operations triggered by the customer making it easy to see exactly what management operations were performed on the backup vault.</span><span class="sxs-lookup"><span data-stu-id="1db59-204">Azure backup provides review of the "operation logs" of backup operations triggered by the customer making it easy to see exactly what management operations were performed on the backup vault.</span></span> <span data-ttu-id="1db59-205">Operations logs enable great post-mortem and audit support for the backup operations.</span><span class="sxs-lookup"><span data-stu-id="1db59-205">Operations logs enable great post-mortem and audit support for the backup operations.</span></span>

<span data-ttu-id="1db59-206">The following operations are logged in Operation logs:</span><span class="sxs-lookup"><span data-stu-id="1db59-206">The following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="1db59-207">Register</span><span class="sxs-lookup"><span data-stu-id="1db59-207">Register</span></span>
* <span data-ttu-id="1db59-208">Unregister</span><span class="sxs-lookup"><span data-stu-id="1db59-208">Unregister</span></span>
* <span data-ttu-id="1db59-209">Configure protection</span><span class="sxs-lookup"><span data-stu-id="1db59-209">Configure protection</span></span>
* <span data-ttu-id="1db59-210">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span><span class="sxs-lookup"><span data-stu-id="1db59-210">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="1db59-211">Restore</span><span class="sxs-lookup"><span data-stu-id="1db59-211">Restore</span></span>
* <span data-ttu-id="1db59-212">Stop protection</span><span class="sxs-lookup"><span data-stu-id="1db59-212">Stop protection</span></span>
* <span data-ttu-id="1db59-213">Delete backup data</span><span class="sxs-lookup"><span data-stu-id="1db59-213">Delete backup data</span></span>
* <span data-ttu-id="1db59-214">Add policy</span><span class="sxs-lookup"><span data-stu-id="1db59-214">Add policy</span></span>
* <span data-ttu-id="1db59-215">Delete policy</span><span class="sxs-lookup"><span data-stu-id="1db59-215">Delete policy</span></span>
* <span data-ttu-id="1db59-216">Update policy</span><span class="sxs-lookup"><span data-stu-id="1db59-216">Update policy</span></span>
* <span data-ttu-id="1db59-217">Cancel job</span><span class="sxs-lookup"><span data-stu-id="1db59-217">Cancel job</span></span>

<span data-ttu-id="1db59-218">To view operation logs corresponding to a backup vault:</span><span class="sxs-lookup"><span data-stu-id="1db59-218">To view operation logs corresponding to a backup vault:</span></span>

1. <span data-ttu-id="1db59-219">Navigate to **Management services** in Azure portal, and then click the **Operation Logs** tab.</span><span class="sxs-lookup"><span data-stu-id="1db59-219">Navigate to **Management services** in Azure portal, and then click the **Operation Logs** tab.</span></span>

    ![Operation Logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="1db59-221">In the filters, select **Backup** as *Type* and specify the backup vault name in *service name* and click on **Submit**.</span><span class="sxs-lookup"><span data-stu-id="1db59-221">In the filters, select **Backup** as *Type* and specify the backup vault name in *service name* and click on **Submit**.</span></span>

    ![Operation Logs Filter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="1db59-223">In the operations logs, select any operation and click  **Details** to see details corresponding to an operation.</span><span class="sxs-lookup"><span data-stu-id="1db59-223">In the operations logs, select any operation and click  **Details** to see details corresponding to an operation.</span></span>

    ![Operation Logs-Fetching details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="1db59-225">The **Details wizard** contains information about the operation triggered, job Id, resource on which this operation is triggered, and start time of the operation.</span><span class="sxs-lookup"><span data-stu-id="1db59-225">The **Details wizard** contains information about the operation triggered, job Id, resource on which this operation is triggered, and start time of the operation.</span></span>

    ![Operation Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="1db59-227">Alert notifications</span><span class="sxs-lookup"><span data-stu-id="1db59-227">Alert notifications</span></span>
<span data-ttu-id="1db59-228">You can get custom alert notifications for the jobs in portal.</span><span class="sxs-lookup"><span data-stu-id="1db59-228">You can get custom alert notifications for the jobs in portal.</span></span> <span data-ttu-id="1db59-229">This is achieved by defining PowerShell-based alert rules on operational logs events.</span><span class="sxs-lookup"><span data-stu-id="1db59-229">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="1db59-230">We recommend using *PowerShell version 1.3.0 or above*.</span><span class="sxs-lookup"><span data-stu-id="1db59-230">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="1db59-231">To define a custom notification to alert for backup failures, a sample command will look like:</span><span class="sxs-lookup"><span data-stu-id="1db59-231">To define a custom notification to alert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="1db59-232">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span><span class="sxs-lookup"><span data-stu-id="1db59-232">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="1db59-233">ResourceUri in details popup window of an operation is the ResourceId to be supplied for this cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1db59-233">ResourceUri in details popup window of an operation is the ResourceId to be supplied for this cmdlet.</span></span>

<span data-ttu-id="1db59-234">**OperationName**: This will be of the format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="1db59-234">**OperationName**: This will be of the format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="1db59-235">**Status**: Supported values are- Started, Succeeded and Failed.</span><span class="sxs-lookup"><span data-stu-id="1db59-235">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="1db59-236">**ResourceGroup**:ResourceGroup of the resource on which operation is triggered.</span><span class="sxs-lookup"><span data-stu-id="1db59-236">**ResourceGroup**:ResourceGroup of the resource on which operation is triggered.</span></span> <span data-ttu-id="1db59-237">You can obtain this from ResourceId value.</span><span class="sxs-lookup"><span data-stu-id="1db59-237">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="1db59-238">Value between fields */resourceGroups/* and */providers/* in ResourceId value is the value for ResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="1db59-238">Value between fields */resourceGroups/* and */providers/* in ResourceId value is the value for ResourceGroup.</span></span>

<span data-ttu-id="1db59-239">**Name**: Name of the Alert Rule.</span><span class="sxs-lookup"><span data-stu-id="1db59-239">**Name**: Name of the Alert Rule.</span></span>

<span data-ttu-id="1db59-240">**CustomEmail**: Specify the custom email address to which you want to send alert notification</span><span class="sxs-lookup"><span data-stu-id="1db59-240">**CustomEmail**: Specify the custom email address to which you want to send alert notification</span></span>

<span data-ttu-id="1db59-241">**SendToServiceOwners**: This option sends alert notification to all administrators and co-administrators of the subscription.</span><span class="sxs-lookup"><span data-stu-id="1db59-241">**SendToServiceOwners**: This option sends alert notification to all administrators and co-administrators of the subscription.</span></span> <span data-ttu-id="1db59-242">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span><span class="sxs-lookup"><span data-stu-id="1db59-242">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="1db59-243">Limitations on Alerts</span><span class="sxs-lookup"><span data-stu-id="1db59-243">Limitations on Alerts</span></span>
<span data-ttu-id="1db59-244">Event-based alerts are subjected to the following limitations:</span><span class="sxs-lookup"><span data-stu-id="1db59-244">Event-based alerts are subjected to the following limitations:</span></span>

1. <span data-ttu-id="1db59-245">Alerts are triggered on all virtual machines in the backup vault.</span><span class="sxs-lookup"><span data-stu-id="1db59-245">Alerts are triggered on all virtual machines in the backup vault.</span></span> <span data-ttu-id="1db59-246">You cannot customize it to get alerts for specific set of virtual machines in a backup vault.</span><span class="sxs-lookup"><span data-stu-id="1db59-246">You cannot customize it to get alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="1db59-247">This feature is in Preview.</span><span class="sxs-lookup"><span data-stu-id="1db59-247">This feature is in Preview.</span></span> [<span data-ttu-id="1db59-248">Learn more</span><span class="sxs-lookup"><span data-stu-id="1db59-248">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-alert-rules)
3. <span data-ttu-id="1db59-249">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span><span class="sxs-lookup"><span data-stu-id="1db59-249">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="1db59-250">Currently you can't modify the email sender.</span><span class="sxs-lookup"><span data-stu-id="1db59-250">Currently you can't modify the email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1db59-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="1db59-251">Next steps</span></span>
* [<span data-ttu-id="1db59-252">Restore Azure VMs</span><span class="sxs-lookup"><span data-stu-id="1db59-252">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)



























