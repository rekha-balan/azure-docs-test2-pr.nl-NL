---
title: Restore a virtual machines from backup | Microsoft Docs
description: Learn how to restore an Azure virtual machine from a recovery point
services: backup
documentationcenter: ''
author: trinadhk
manager: shreeshd
editor: ''
keywords: restore backup; how to restore; recovery point;
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: trinadhk; jimpark;
ms.openlocfilehash: cdb5c42eb684bc5bf564638407c3ed1ba268046e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554049"
---
# <a name="restore-virtual-machines-in-azure"></a><span data-ttu-id="23ca7-104">Restore virtual machines in Azure</span><span class="sxs-lookup"><span data-stu-id="23ca7-104">Restore virtual machines in Azure</span></span>
> [!div class="op_single_selector"]
> * [Restore VMs in Azure portal](backup-azure-arm-restore-vms.md)
> * [Restore VMs in Classic portal](backup-azure-restore-vms.md)
> 
> 

<span data-ttu-id="23ca7-107">Restore a virtual machine to a new VM from the backups stored in an Azure backup vault with the following steps.</span><span class="sxs-lookup"><span data-stu-id="23ca7-107">Restore a virtual machine to a new VM from the backups stored in an Azure backup vault with the following steps.</span></span>

## <a name="restore-workflow"></a><span data-ttu-id="23ca7-108">Restore workflow</span><span class="sxs-lookup"><span data-stu-id="23ca7-108">Restore workflow</span></span>
### <a name="step-1-choose-an-item-to-restore"></a><span data-ttu-id="23ca7-109">Step 1: Choose an item to restore</span><span class="sxs-lookup"><span data-stu-id="23ca7-109">Step 1: Choose an item to restore</span></span>
1. <span data-ttu-id="23ca7-110">Navigate to the **Protected Items** tab and select the virtual machine you want to restore to a new VM.</span><span class="sxs-lookup"><span data-stu-id="23ca7-110">Navigate to the **Protected Items** tab and select the virtual machine you want to restore to a new VM.</span></span>
   
    ![Protected items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-vms/protected-items.png)
   
    <span data-ttu-id="23ca7-112">The **Recovery Point** column in the **Protected Items** page will tell you the number of recovery points for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="23ca7-112">The **Recovery Point** column in the **Protected Items** page will tell you the number of recovery points for a virtual machine.</span></span> <span data-ttu-id="23ca7-113">The **Newest Recovery Point** column tells you the time of the most recent backup from which a virtual machine can be restored.</span><span class="sxs-lookup"><span data-stu-id="23ca7-113">The **Newest Recovery Point** column tells you the time of the most recent backup from which a virtual machine can be restored.</span></span>
2. <span data-ttu-id="23ca7-114">Click **Restore** to open the **Restore an Item** wizard.</span><span class="sxs-lookup"><span data-stu-id="23ca7-114">Click **Restore** to open the **Restore an Item** wizard.</span></span>
   
    ![Restore an item](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a><span data-ttu-id="23ca7-116">Step 2: Pick a recovery point</span><span class="sxs-lookup"><span data-stu-id="23ca7-116">Step 2: Pick a recovery point</span></span>
1. <span data-ttu-id="23ca7-117">In the **select a recovery point** screen, you can restore from the newest recovery point, or from a previous point in time.</span><span class="sxs-lookup"><span data-stu-id="23ca7-117">In the **select a recovery point** screen, you can restore from the newest recovery point, or from a previous point in time.</span></span> <span data-ttu-id="23ca7-118">The default option selected when wizard opens is *Newest Recovery Point*.</span><span class="sxs-lookup"><span data-stu-id="23ca7-118">The default option selected when wizard opens is *Newest Recovery Point*.</span></span>
   
    ![Select a recovery point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-vms/select-recovery-point.png)
2. <span data-ttu-id="23ca7-120">To pick an earlier point in time, choose the **Select Date** option in the dropdown and select a date in the calendar control by clicking on the **calendar icon**.</span><span class="sxs-lookup"><span data-stu-id="23ca7-120">To pick an earlier point in time, choose the **Select Date** option in the dropdown and select a date in the calendar control by clicking on the **calendar icon**.</span></span> <span data-ttu-id="23ca7-121">In the control, all dates that have recovery points are filled with a light gray shade and are selectable by the user.</span><span class="sxs-lookup"><span data-stu-id="23ca7-121">In the control, all dates that have recovery points are filled with a light gray shade and are selectable by the user.</span></span>
   
    ![Select a date](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-vms/select-date.png)
   
    <span data-ttu-id="23ca7-123">Once you click a date in the calendar control, the recovery points available on that date will be shown in recovery points table below.</span><span class="sxs-lookup"><span data-stu-id="23ca7-123">Once you click a date in the calendar control, the recovery points available on that date will be shown in recovery points table below.</span></span> <span data-ttu-id="23ca7-124">The **Time** column indicates the time at which the snapshot was taken.</span><span class="sxs-lookup"><span data-stu-id="23ca7-124">The **Time** column indicates the time at which the snapshot was taken.</span></span> <span data-ttu-id="23ca7-125">The **Type** column displays the [consistency](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) of the recovery point.</span><span class="sxs-lookup"><span data-stu-id="23ca7-125">The **Type** column displays the [consistency](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) of the recovery point.</span></span> <span data-ttu-id="23ca7-126">The table header shows the number of recovery points available on that day in parentheses.</span><span class="sxs-lookup"><span data-stu-id="23ca7-126">The table header shows the number of recovery points available on that day in parentheses.</span></span>
   
    ![Recovery points](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-vms/recovery-points.png)
3. <span data-ttu-id="23ca7-128">Select the recovery point from the **Recovery Points** table and click the Next arrow to go to the next screen.</span><span class="sxs-lookup"><span data-stu-id="23ca7-128">Select the recovery point from the **Recovery Points** table and click the Next arrow to go to the next screen.</span></span>

### <a name="step-3-specify-a-destination-location"></a><span data-ttu-id="23ca7-129">Step 3: Specify a destination location</span><span class="sxs-lookup"><span data-stu-id="23ca7-129">Step 3: Specify a destination location</span></span>
1. <span data-ttu-id="23ca7-130">In the **Select restore instance** screen specify details of where to restore the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="23ca7-130">In the **Select restore instance** screen specify details of where to restore the virtual machine.</span></span>
   
   * <span data-ttu-id="23ca7-131">Specify the virtual machine name: In a given cloud service, the virtual machine name should be unique.</span><span class="sxs-lookup"><span data-stu-id="23ca7-131">Specify the virtual machine name: In a given cloud service, the virtual machine name should be unique.</span></span> <span data-ttu-id="23ca7-132">We don't support over-writing existing VM.</span><span class="sxs-lookup"><span data-stu-id="23ca7-132">We don't support over-writing existing VM.</span></span> 
   * <span data-ttu-id="23ca7-133">Select a cloud service for the VM: This is mandatory for creating a VM.</span><span class="sxs-lookup"><span data-stu-id="23ca7-133">Select a cloud service for the VM: This is mandatory for creating a VM.</span></span> <span data-ttu-id="23ca7-134">You can choose to either use an existing cloud service or create a new cloud service.</span><span class="sxs-lookup"><span data-stu-id="23ca7-134">You can choose to either use an existing cloud service or create a new cloud service.</span></span>
     
        <span data-ttu-id="23ca7-135">Whatever cloud service name is picked should be globally unique.</span><span class="sxs-lookup"><span data-stu-id="23ca7-135">Whatever cloud service name is picked should be globally unique.</span></span> <span data-ttu-id="23ca7-136">Typically, the cloud service name gets associated with a public-facing URL in the form of [cloudservice].cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="23ca7-136">Typically, the cloud service name gets associated with a public-facing URL in the form of [cloudservice].cloudapp.net.</span></span> <span data-ttu-id="23ca7-137">Azure will not allow you to create a new cloud service if the name has already been used.</span><span class="sxs-lookup"><span data-stu-id="23ca7-137">Azure will not allow you to create a new cloud service if the name has already been used.</span></span> <span data-ttu-id="23ca7-138">If you choose to create a new cloud service, it will be given the same name as the virtual machine – in which case the VM name picked should be unique enough to be applied to the associated cloud service.</span><span class="sxs-lookup"><span data-stu-id="23ca7-138">If you choose to create a new cloud service, it will be given the same name as the virtual machine – in which case the VM name picked should be unique enough to be applied to the associated cloud service.</span></span>
     
        <span data-ttu-id="23ca7-139">We only display cloud services and virtual networks that are not associated with any affinity groups in the restore instance details.</span><span class="sxs-lookup"><span data-stu-id="23ca7-139">We only display cloud services and virtual networks that are not associated with any affinity groups in the restore instance details.</span></span> <span data-ttu-id="23ca7-140">[Learn More](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="23ca7-140">[Learn More](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span></span>
2. <span data-ttu-id="23ca7-141">Select a storage account for the VM: This is mandatory for creating the VM.</span><span class="sxs-lookup"><span data-stu-id="23ca7-141">Select a storage account for the VM: This is mandatory for creating the VM.</span></span> <span data-ttu-id="23ca7-142">You can select from existing storage accounts in the same region as the Azure Backup vault.</span><span class="sxs-lookup"><span data-stu-id="23ca7-142">You can select from existing storage accounts in the same region as the Azure Backup vault.</span></span> <span data-ttu-id="23ca7-143">We don’t support storage accounts that are Zone redundant or of Premium storage type.</span><span class="sxs-lookup"><span data-stu-id="23ca7-143">We don’t support storage accounts that are Zone redundant or of Premium storage type.</span></span>
   
    <span data-ttu-id="23ca7-144">If there are no storage accounts with supported configuration, please create a storage account of supported configuration prior to starting restore operation.</span><span class="sxs-lookup"><span data-stu-id="23ca7-144">If there are no storage accounts with supported configuration, please create a storage account of supported configuration prior to starting restore operation.</span></span>
   
    ![Select a virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-vms/restore-sa.png)
3. <span data-ttu-id="23ca7-146">Select a Virtual Network: The virtual network (VNET) for the virtual machine should be selected at the time of creating the VM.</span><span class="sxs-lookup"><span data-stu-id="23ca7-146">Select a Virtual Network: The virtual network (VNET) for the virtual machine should be selected at the time of creating the VM.</span></span> <span data-ttu-id="23ca7-147">The restore UI shows all the VNETs within this subscription that can be used.</span><span class="sxs-lookup"><span data-stu-id="23ca7-147">The restore UI shows all the VNETs within this subscription that can be used.</span></span> <span data-ttu-id="23ca7-148">It is not mandatory to select a VNET for the restored VM – you will be able to connect to the restored virtual machine over the internet even if the VNET is not applied.</span><span class="sxs-lookup"><span data-stu-id="23ca7-148">It is not mandatory to select a VNET for the restored VM – you will be able to connect to the restored virtual machine over the internet even if the VNET is not applied.</span></span>
   
    <span data-ttu-id="23ca7-149">If the cloud service selected is associated with a virtual network, then you cannot change the virtual network.</span><span class="sxs-lookup"><span data-stu-id="23ca7-149">If the cloud service selected is associated with a virtual network, then you cannot change the virtual network.</span></span>
   
    ![Select a virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-vms/restore-cs-vnet.png)
4. <span data-ttu-id="23ca7-151">Select a subnet: In case the VNET has subnets, by default the first subnet will be selected.</span><span class="sxs-lookup"><span data-stu-id="23ca7-151">Select a subnet: In case the VNET has subnets, by default the first subnet will be selected.</span></span> <span data-ttu-id="23ca7-152">Choose the subnet of your choice from the dropdown options.</span><span class="sxs-lookup"><span data-stu-id="23ca7-152">Choose the subnet of your choice from the dropdown options.</span></span> <span data-ttu-id="23ca7-153">For subnet details, go to Networks extension in the [portal home page](https://manage.windowsazure.com/), go to **Virtual Networks** and select the virtual network and drill down into Configure to see subnet details.</span><span class="sxs-lookup"><span data-stu-id="23ca7-153">For subnet details, go to Networks extension in the [portal home page](https://manage.windowsazure.com/), go to **Virtual Networks** and select the virtual network and drill down into Configure to see subnet details.</span></span>
   
    ![Select a subnet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-vms/select-subnet.png)
5. <span data-ttu-id="23ca7-155">Click the **Submit** icon in the wizard to submit the details and create a restore job.</span><span class="sxs-lookup"><span data-stu-id="23ca7-155">Click the **Submit** icon in the wizard to submit the details and create a restore job.</span></span>

## <a name="track-the-restore-operation"></a><span data-ttu-id="23ca7-156">Track the Restore operation</span><span class="sxs-lookup"><span data-stu-id="23ca7-156">Track the Restore operation</span></span>
<span data-ttu-id="23ca7-157">Once you have input all the information into the restore wizard and submitted it Azure Backup will try to create a job to track the restore operation.</span><span class="sxs-lookup"><span data-stu-id="23ca7-157">Once you have input all the information into the restore wizard and submitted it Azure Backup will try to create a job to track the restore operation.</span></span>

![Creating a restore job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-vms/create-restore-job.png)

<span data-ttu-id="23ca7-159">If the job creation is successful, you will see a toast notification indicating that the job is created.</span><span class="sxs-lookup"><span data-stu-id="23ca7-159">If the job creation is successful, you will see a toast notification indicating that the job is created.</span></span> <span data-ttu-id="23ca7-160">You can get more details by clicking the **View Job** button that will take you to **Jobs** tab.</span><span class="sxs-lookup"><span data-stu-id="23ca7-160">You can get more details by clicking the **View Job** button that will take you to **Jobs** tab.</span></span>

![Restore job created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-vms/restore-job-created.png)

<span data-ttu-id="23ca7-162">Once the restore operation is finished, it will be marked as completed in **Jobs** tab.</span><span class="sxs-lookup"><span data-stu-id="23ca7-162">Once the restore operation is finished, it will be marked as completed in **Jobs** tab.</span></span>

![Restore job complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-restore-vms/restore-job-complete.png)

<span data-ttu-id="23ca7-164">After restoring the virtual machine you may need to re-install the extensions existing on the original VM and [modify the endpoints](../virtual-machines/windows/classic/setup-endpoints.md) for the virtual machine in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="23ca7-164">After restoring the virtual machine you may need to re-install the extensions existing on the original VM and [modify the endpoints](../virtual-machines/windows/classic/setup-endpoints.md) for the virtual machine in the Azure portal.</span></span>

## <a name="post-restore-steps"></a><span data-ttu-id="23ca7-165">Post-Restore steps</span><span class="sxs-lookup"><span data-stu-id="23ca7-165">Post-Restore steps</span></span>
<span data-ttu-id="23ca7-166">If you are using a cloud-init based Linux distribution such as Ubuntu, for security reasons, password will be blocked post restore.</span><span class="sxs-lookup"><span data-stu-id="23ca7-166">If you are using a cloud-init based Linux distribution such as Ubuntu, for security reasons, password will be blocked post restore.</span></span> <span data-ttu-id="23ca7-167">Please use VMAccess extension on the restored VM to [reset the password](../virtual-machines/linux/classic/reset-access.md).</span><span class="sxs-lookup"><span data-stu-id="23ca7-167">Please use VMAccess extension on the restored VM to [reset the password](../virtual-machines/linux/classic/reset-access.md).</span></span> <span data-ttu-id="23ca7-168">We recommend using SSH keys on these distributions to avoid resetting password post restore.</span><span class="sxs-lookup"><span data-stu-id="23ca7-168">We recommend using SSH keys on these distributions to avoid resetting password post restore.</span></span> 

## <a name="backup-for-restored-vms"></a><span data-ttu-id="23ca7-169">Backup for Restored VMs</span><span class="sxs-lookup"><span data-stu-id="23ca7-169">Backup for Restored VMs</span></span>
<span data-ttu-id="23ca7-170">If you have restored VM to same cloud service with the same name as originally backed up VM, backup will continue on the VM post restore.</span><span class="sxs-lookup"><span data-stu-id="23ca7-170">If you have restored VM to same cloud service with the same name as originally backed up VM, backup will continue on the VM post restore.</span></span> <span data-ttu-id="23ca7-171">If you have either restored VM to a different cloud service or specified a different name for restored VM, this will be treated as a new VM and you need to setup backup for restored VM.</span><span class="sxs-lookup"><span data-stu-id="23ca7-171">If you have either restored VM to a different cloud service or specified a different name for restored VM, this will be treated as a new VM and you need to setup backup for restored VM.</span></span>

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a><span data-ttu-id="23ca7-172">Restoring a VM during Azure DataCenter Disaster</span><span class="sxs-lookup"><span data-stu-id="23ca7-172">Restoring a VM during Azure DataCenter Disaster</span></span>
<span data-ttu-id="23ca7-173">Azure Backup allows restoring backed up VMs to the paired data center in case the primary data center where VMs are running experiences disaster and you configured Backup vault to be geo-redundant.</span><span class="sxs-lookup"><span data-stu-id="23ca7-173">Azure Backup allows restoring backed up VMs to the paired data center in case the primary data center where VMs are running experiences disaster and you configured Backup vault to be geo-redundant.</span></span> <span data-ttu-id="23ca7-174">During such scenarios, you need to select a storage account which is present in paired data center and rest of the restore process remains same.</span><span class="sxs-lookup"><span data-stu-id="23ca7-174">During such scenarios, you need to select a storage account which is present in paired data center and rest of the restore process remains same.</span></span> <span data-ttu-id="23ca7-175">Azure Backup uses Compute service from paired geo to create the restored virtual machine.</span><span class="sxs-lookup"><span data-stu-id="23ca7-175">Azure Backup uses Compute service from paired geo to create the restored virtual machine.</span></span> <span data-ttu-id="23ca7-176">Learn more about [Azure Data center resiliency](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)</span><span class="sxs-lookup"><span data-stu-id="23ca7-176">Learn more about [Azure Data center resiliency](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)</span></span>

## <a name="restoring-domain-controller-vms"></a><span data-ttu-id="23ca7-177">Restoring Domain Controller VMs</span><span class="sxs-lookup"><span data-stu-id="23ca7-177">Restoring Domain Controller VMs</span></span>
<span data-ttu-id="23ca7-178">Backup of Domain Controller (DC) virtual machines is a supported scenario with Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="23ca7-178">Backup of Domain Controller (DC) virtual machines is a supported scenario with Azure Backup.</span></span> <span data-ttu-id="23ca7-179">However some care must be taken during the restore process.</span><span class="sxs-lookup"><span data-stu-id="23ca7-179">However some care must be taken during the restore process.</span></span> <span data-ttu-id="23ca7-180">The restore experience is vastly different for Domain Controller VMs in a single-DC configuration vs. VMs in a multi-DC configuration.</span><span class="sxs-lookup"><span data-stu-id="23ca7-180">The restore experience is vastly different for Domain Controller VMs in a single-DC configuration vs. VMs in a multi-DC configuration.</span></span>

### <a name="single-dc"></a><span data-ttu-id="23ca7-181">Single DC</span><span class="sxs-lookup"><span data-stu-id="23ca7-181">Single DC</span></span>
<span data-ttu-id="23ca7-182">The VM can be restored (like any other VM) from the Azure portal or using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23ca7-182">The VM can be restored (like any other VM) from the Azure portal or using PowerShell.</span></span>

### <a name="multiple-dcs"></a><span data-ttu-id="23ca7-183">Multiple DCs</span><span class="sxs-lookup"><span data-stu-id="23ca7-183">Multiple DCs</span></span>
<span data-ttu-id="23ca7-184">When you have a multi-DC environment, the Domain Controllers have their own way of keeping data in sync. When an older backup point is restored *without the proper precautions*, The USN rollback process can wreak havoc in a multi-DC environment.</span><span class="sxs-lookup"><span data-stu-id="23ca7-184">When you have a multi-DC environment, the Domain Controllers have their own way of keeping data in sync. When an older backup point is restored *without the proper precautions*, The USN rollback process can wreak havoc in a multi-DC environment.</span></span> <span data-ttu-id="23ca7-185">The right way to recover such a VM is to boot it in DSRM mode.</span><span class="sxs-lookup"><span data-stu-id="23ca7-185">The right way to recover such a VM is to boot it in DSRM mode.</span></span>

<span data-ttu-id="23ca7-186">The challenge arises because DSRM mode is not present in Azure.</span><span class="sxs-lookup"><span data-stu-id="23ca7-186">The challenge arises because DSRM mode is not present in Azure.</span></span> <span data-ttu-id="23ca7-187">So to restore such a VM, you cannot use the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="23ca7-187">So to restore such a VM, you cannot use the Azure portal.</span></span> <span data-ttu-id="23ca7-188">The only supported restore mechanism is disk-based restore using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23ca7-188">The only supported restore mechanism is disk-based restore using PowerShell.</span></span>

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use the Azure portal for restore! Only PowerShell based restore is supported
> 
> 

<span data-ttu-id="23ca7-191">Read more about the [USN rollback problem](https://technet.microsoft.com/library/dd363553) and the strategies suggested to fix it.</span><span class="sxs-lookup"><span data-stu-id="23ca7-191">Read more about the [USN rollback problem](https://technet.microsoft.com/library/dd363553) and the strategies suggested to fix it.</span></span>

## <a name="restoring-vms-with-special-network-configurations"></a><span data-ttu-id="23ca7-192">Restoring VMs with special network configurations</span><span class="sxs-lookup"><span data-stu-id="23ca7-192">Restoring VMs with special network configurations</span></span>
<span data-ttu-id="23ca7-193">Azure Backup supports backup for following special network configurations of virtual machines.</span><span class="sxs-lookup"><span data-stu-id="23ca7-193">Azure Backup supports backup for following special network configurations of virtual machines.</span></span>

* <span data-ttu-id="23ca7-194">VMs under load balancer (internal and external)</span><span class="sxs-lookup"><span data-stu-id="23ca7-194">VMs under load balancer (internal and external)</span></span>
* <span data-ttu-id="23ca7-195">VMs with multiple reserved IPs</span><span class="sxs-lookup"><span data-stu-id="23ca7-195">VMs with multiple reserved IPs</span></span>
* <span data-ttu-id="23ca7-196">VMs with multiple NICs</span><span class="sxs-lookup"><span data-stu-id="23ca7-196">VMs with multiple NICs</span></span>

<span data-ttu-id="23ca7-197">These configurations mandate following considerations while restoring them.</span><span class="sxs-lookup"><span data-stu-id="23ca7-197">These configurations mandate following considerations while restoring them.</span></span>

> [!TIP]
> Please use PowerShell based restore flow to recreate the special network configuration of VMs post restore.
> 
> 

### <a name="restoring-from-the-ui"></a><span data-ttu-id="23ca7-199">Restoring from the UI:</span><span class="sxs-lookup"><span data-stu-id="23ca7-199">Restoring from the UI:</span></span>
<span data-ttu-id="23ca7-200">While restoring from UI, **always choose a new cloud service**.</span><span class="sxs-lookup"><span data-stu-id="23ca7-200">While restoring from UI, **always choose a new cloud service**.</span></span> <span data-ttu-id="23ca7-201">Please note that since portal only takes mandatory parameters during restore flow, VMs restored using UI will lose the special network configuration they possess.</span><span class="sxs-lookup"><span data-stu-id="23ca7-201">Please note that since portal only takes mandatory parameters during restore flow, VMs restored using UI will lose the special network configuration they possess.</span></span> <span data-ttu-id="23ca7-202">In other words, restore VMs will be normal VMs without configuration of load balancer or multi NIC or multiple reserved IP.</span><span class="sxs-lookup"><span data-stu-id="23ca7-202">In other words, restore VMs will be normal VMs without configuration of load balancer or multi NIC or multiple reserved IP.</span></span>

### <a name="restoring-from-powershell"></a><span data-ttu-id="23ca7-203">Restoring from PowerShell:</span><span class="sxs-lookup"><span data-stu-id="23ca7-203">Restoring from PowerShell:</span></span>
<span data-ttu-id="23ca7-204">PowerShell has the ability to just restore the VM disks from backup and not create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="23ca7-204">PowerShell has the ability to just restore the VM disks from backup and not create the virtual machine.</span></span> <span data-ttu-id="23ca7-205">This is helpful when restoring virtual machines which require special network configurations mentioned above.</span><span class="sxs-lookup"><span data-stu-id="23ca7-205">This is helpful when restoring virtual machines which require special network configurations mentioned above.</span></span>

<span data-ttu-id="23ca7-206">In order to fully recreate the virtual machine post restoring disks, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="23ca7-206">In order to fully recreate the virtual machine post restoring disks, follow these steps:</span></span>

1. <span data-ttu-id="23ca7-207">Restore the disks from backup vault using [Azure Backup PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="23ca7-207">Restore the disks from backup vault using [Azure Backup PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)</span></span>
2. <span data-ttu-id="23ca7-208">Create the VM config required for load balancer/multiple NIC/multiple reserved IP using the PowerShell cmdlets and use it to create the VM of desired configuration.</span><span class="sxs-lookup"><span data-stu-id="23ca7-208">Create the VM config required for load balancer/multiple NIC/multiple reserved IP using the PowerShell cmdlets and use it to create the VM of desired configuration.</span></span>
   
   * <span data-ttu-id="23ca7-209">Create VM in cloud service with [Internal Load balancer ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span><span class="sxs-lookup"><span data-stu-id="23ca7-209">Create VM in cloud service with [Internal Load balancer ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span></span>
   * <span data-ttu-id="23ca7-210">Create VM to connect to [Internet facing load balancer](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)</span><span class="sxs-lookup"><span data-stu-id="23ca7-210">Create VM to connect to [Internet facing load balancer](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)</span></span>
   * <span data-ttu-id="23ca7-211">Create VM with [multiple NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span><span class="sxs-lookup"><span data-stu-id="23ca7-211">Create VM with [multiple NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span></span>
   * <span data-ttu-id="23ca7-212">Create VM with [multiple reserved IPs](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span><span class="sxs-lookup"><span data-stu-id="23ca7-212">Create VM with [multiple reserved IPs](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="23ca7-213">Next steps</span><span class="sxs-lookup"><span data-stu-id="23ca7-213">Next steps</span></span>
* [<span data-ttu-id="23ca7-214">Troubleshooting errors</span><span class="sxs-lookup"><span data-stu-id="23ca7-214">Troubleshooting errors</span></span>](backup-azure-vms-troubleshoot.md#restore)
* [<span data-ttu-id="23ca7-215">Manage virtual machines</span><span class="sxs-lookup"><span data-stu-id="23ca7-215">Manage virtual machines</span></span>](backup-azure-manage-vms.md)












