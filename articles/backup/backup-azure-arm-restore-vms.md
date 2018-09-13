---
title: 'Azure Backup: Restore virtual machines using the Azure portal | Microsoft Docs'
description: Restore an Azure virtual machine from a recovery point using Azure portal
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
keywords: restore backup; how to restore; recovery point;
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/12/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 0372d8a9a04a03b77aef829b22b406279268dc3a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552550"
---
# <a name="use-azure-portal-to-restore-virtual-machines"></a><span data-ttu-id="1ea3f-104">Use Azure portal to restore virtual machines</span><span class="sxs-lookup"><span data-stu-id="1ea3f-104">Use Azure portal to restore virtual machines</span></span>
> [!div class="op_single_selector"]
> * [Restore VMs in Classic portal](backup-azure-restore-vms.md)
> * [Restore VMs in Azure portal](backup-azure-arm-restore-vms.md)
>
>

<span data-ttu-id="1ea3f-107">Protect your data by taking snapshots of your data at defined intervals.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-107">Protect your data by taking snapshots of your data at defined intervals.</span></span> <span data-ttu-id="1ea3f-108">These snapshots are known as recovery points, and they are stored in recovery services vaults.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-108">These snapshots are known as recovery points, and they are stored in recovery services vaults.</span></span> <span data-ttu-id="1ea3f-109">If or when it is necessary to repair or rebuild a VM, you can restore the VM from any of the saved recovery points.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-109">If or when it is necessary to repair or rebuild a VM, you can restore the VM from any of the saved recovery points.</span></span> <span data-ttu-id="1ea3f-110">When you restore a recovery point, you can create a new VM which is a point-in-time representation of your backed-up VM, or restore disks and use the template that comes along with it to customize the restored VM or do an individual file recovery.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-110">When you restore a recovery point, you can create a new VM which is a point-in-time representation of your backed-up VM, or restore disks and use the template that comes along with it to customize the restored VM or do an individual file recovery.</span></span> <span data-ttu-id="1ea3f-111">This article explains how to restore a VM to a new VM or restore all backed-up disks.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-111">This article explains how to restore a VM to a new VM or restore all backed-up disks.</span></span> <span data-ttu-id="1ea3f-112">For individual file recovery, refer to [Recover files from Azure VM backup](backup-azure-restore-files-from-vm.md)</span><span class="sxs-lookup"><span data-stu-id="1ea3f-112">For individual file recovery, refer to [Recover files from Azure VM backup](backup-azure-restore-files-from-vm.md)</span></span>

![3-ways-restore-from-vm-backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Azure has two deployment models for creating and working with resources: [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md). This article provides the information and procedures for restoring VMs deployed using the Resource Manager model.
>
>

<span data-ttu-id="1ea3f-116">Restoring a VM or all disks from VM backup involves two steps:</span><span class="sxs-lookup"><span data-stu-id="1ea3f-116">Restoring a VM or all disks from VM backup involves two steps:</span></span>

1. <span data-ttu-id="1ea3f-117">Select a restore point for restore</span><span class="sxs-lookup"><span data-stu-id="1ea3f-117">Select a restore point for restore</span></span>
2. <span data-ttu-id="1ea3f-118">Selecting the restore type - create a new VM or restore disks and specify required parameters.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-118">Selecting the restore type - create a new VM or restore disks and specify required parameters.</span></span> 

## <a name="select-restore-point-for-restore"></a><span data-ttu-id="1ea3f-119">Select restore point for restore</span><span class="sxs-lookup"><span data-stu-id="1ea3f-119">Select restore point for restore</span></span>
1. <span data-ttu-id="1ea3f-120">Sign in to the [Azure portal](http://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="1ea3f-120">Sign in to the [Azure portal](http://portal.azure.com/)</span></span>
2. <span data-ttu-id="1ea3f-121">On the Azure menu, click **Browse** and in the list of services, type **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-121">On the Azure menu, click **Browse** and in the list of services, type **Recovery Services**.</span></span> <span data-ttu-id="1ea3f-122">The list of services adjusts to what you type.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-122">The list of services adjusts to what you type.</span></span> <span data-ttu-id="1ea3f-123">When you see **Recovery Services vaults**, select it.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-123">When you see **Recovery Services vaults**, select it.</span></span>

    ![Open Recovery Services vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    <span data-ttu-id="1ea3f-125">The list of vaults in the subscription is displayed.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-125">The list of vaults in the subscription is displayed.</span></span>

    ![List of Recovery Services vaults](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. <span data-ttu-id="1ea3f-127">From the list, select the vault associated with the VM you want to restore.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-127">From the list, select the vault associated with the VM you want to restore.</span></span> <span data-ttu-id="1ea3f-128">When you click the vault, its dashboard opens.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-128">When you click the vault, its dashboard opens.</span></span>

    ![List of Recovery Services vaults](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. <span data-ttu-id="1ea3f-130">Now that you're in the vault dashboard.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-130">Now that you're in the vault dashboard.</span></span> <span data-ttu-id="1ea3f-131">On the **Backup Items** tile, click **Azure Virtual Machines** to display the VMs associated with the vault.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-131">On the **Backup Items** tile, click **Azure Virtual Machines** to display the VMs associated with the vault.</span></span>

    ![vault dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/vault-dashboard.png)

    <span data-ttu-id="1ea3f-133">The **Backup Items** blade opens and displays the list of Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-133">The **Backup Items** blade opens and displays the list of Azure virtual machines.</span></span>

    ![list of VMs in vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. <span data-ttu-id="1ea3f-135">From the list, select a VM to open the dashboard.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-135">From the list, select a VM to open the dashboard.</span></span> <span data-ttu-id="1ea3f-136">The VM dashboard opens to the Monitoring area, which contains the Restore points tile.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-136">The VM dashboard opens to the Monitoring area, which contains the Restore points tile.</span></span>

    ![list of VMs in vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/vm-blade.png)
6. <span data-ttu-id="1ea3f-138">On the VM dashboard menu, click **Restore**</span><span class="sxs-lookup"><span data-stu-id="1ea3f-138">On the VM dashboard menu, click **Restore**</span></span>

    ![list of VMs in vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    <span data-ttu-id="1ea3f-140">The Restore blade opens.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-140">The Restore blade opens.</span></span>

    ![restore blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/restore-blade.png)
7. <span data-ttu-id="1ea3f-142">On the **Restore** blade, click **Restore point** to open the **Select Restore point** blade.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-142">On the **Restore** blade, click **Restore point** to open the **Select Restore point** blade.</span></span>

    ![restore blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    <span data-ttu-id="1ea3f-144">By default, the dialog displays all restore points from the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-144">By default, the dialog displays all restore points from the last 30 days.</span></span> <span data-ttu-id="1ea3f-145">Use the **Filter** to alter the time range of the restore points displayed.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-145">Use the **Filter** to alter the time range of the restore points displayed.</span></span> <span data-ttu-id="1ea3f-146">By default, restore points of all consistency are displayed.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-146">By default, restore points of all consistency are displayed.</span></span> <span data-ttu-id="1ea3f-147">Modify **All Restore points** filter to select a specific consistency of restore points.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-147">Modify **All Restore points** filter to select a specific consistency of restore points.</span></span> <span data-ttu-id="1ea3f-148">For more information about each type of restoration point, see the explanation of [Data consistency](backup-azure-vms-introduction.md#data-consistency).</span><span class="sxs-lookup"><span data-stu-id="1ea3f-148">For more information about each type of restoration point, see the explanation of [Data consistency](backup-azure-vms-introduction.md#data-consistency).</span></span>  

   * <span data-ttu-id="1ea3f-149">**Restore point consistency** from this list choose:</span><span class="sxs-lookup"><span data-stu-id="1ea3f-149">**Restore point consistency** from this list choose:</span></span>
     * <span data-ttu-id="1ea3f-150">Crash consistent restore points,</span><span class="sxs-lookup"><span data-stu-id="1ea3f-150">Crash consistent restore points,</span></span>
     * <span data-ttu-id="1ea3f-151">Application consistent restore points,</span><span class="sxs-lookup"><span data-stu-id="1ea3f-151">Application consistent restore points,</span></span>
     * <span data-ttu-id="1ea3f-152">File system consistent restore points</span><span class="sxs-lookup"><span data-stu-id="1ea3f-152">File system consistent restore points</span></span>
     * <span data-ttu-id="1ea3f-153">All restore points.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-153">All restore points.</span></span>  
8. <span data-ttu-id="1ea3f-154">Choose a Restore point and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-154">Choose a Restore point and click **OK**.</span></span>

    ![choose restore point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/select-recovery-point.png)

    <span data-ttu-id="1ea3f-156">The **Restore** blade shows the Restore point is set.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-156">The **Restore** blade shows the Restore point is set.</span></span>

    ![restore point is set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. <span data-ttu-id="1ea3f-158">On the **Restore** blade, **Restore configuration** opens automatically after restore point is set.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-158">On the **Restore** blade, **Restore configuration** opens automatically after restore point is set.</span></span>

## <a name="choosing-a-vm-restore-configuration"></a><span data-ttu-id="1ea3f-159">Choosing a VM restore configuration</span><span class="sxs-lookup"><span data-stu-id="1ea3f-159">Choosing a VM restore configuration</span></span>
<span data-ttu-id="1ea3f-160">Now that you have selected the restore point, choose a configuration for your restore VM.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-160">Now that you have selected the restore point, choose a configuration for your restore VM.</span></span> <span data-ttu-id="1ea3f-161">Your choices for configuring the restored VM are to use: Azure portal or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-161">Your choices for configuring the restored VM are to use: Azure portal or PowerShell.</span></span>

1. <span data-ttu-id="1ea3f-162">If you are not already there, go to the **Restore** blade.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-162">If you are not already there, go to the **Restore** blade.</span></span> <span data-ttu-id="1ea3f-163">Ensure a [Restore point has been selected](#select-restore-point-for-restore), and click **Restore configuration** to open the **Recovery configuration** blade.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-163">Ensure a [Restore point has been selected](#select-restore-point-for-restore), and click **Restore configuration** to open the **Recovery configuration** blade.</span></span>

    ![recovery configuration wizard is set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. <span data-ttu-id="1ea3f-165">On the **Restore configuration** blade, you have two choices:</span><span class="sxs-lookup"><span data-stu-id="1ea3f-165">On the **Restore configuration** blade, you have two choices:</span></span>
   * <span data-ttu-id="1ea3f-166">Restore full virtual machine</span><span class="sxs-lookup"><span data-stu-id="1ea3f-166">Restore full virtual machine</span></span>
   * <span data-ttu-id="1ea3f-167">Restore backed up disks</span><span class="sxs-lookup"><span data-stu-id="1ea3f-167">Restore backed up disks</span></span>

<span data-ttu-id="1ea3f-168">Portal provides a Quick Create option for restored VM.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-168">Portal provides a Quick Create option for restored VM.</span></span> <span data-ttu-id="1ea3f-169">If you want to customize the VM configuration or names of the resources created as part of create a new VM choice, use PowerShell or portal to restore backed up disks and use PowerShell commands to attach them to choice of VM configuration or use template that comes with restore disks to customize the restored VM.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-169">If you want to customize the VM configuration or names of the resources created as part of create a new VM choice, use PowerShell or portal to restore backed up disks and use PowerShell commands to attach them to choice of VM configuration or use template that comes with restore disks to customize the restored VM.</span></span> <span data-ttu-id="1ea3f-170">See [Restoring a VM with special network configurations](#restoring-vms-with-special-network-configurations) for details on how to restore VM which has multiple NICs or under load balancer.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-170">See [Restoring a VM with special network configurations](#restoring-vms-with-special-network-configurations) for details on how to restore VM which has multiple NICs or under load balancer.</span></span> 
 
## <a name="create-a-new-vm-from-restore-point"></a><span data-ttu-id="1ea3f-171">Create a new VM from restore point</span><span class="sxs-lookup"><span data-stu-id="1ea3f-171">Create a new VM from restore point</span></span>
<span data-ttu-id="1ea3f-172">If you are not already there, [select a restore point](#restoring-vms-with-special-network-configurations) before proceeding to creating a new VM from restore point.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-172">If you are not already there, [select a restore point](#restoring-vms-with-special-network-configurations) before proceeding to creating a new VM from restore point.</span></span> <span data-ttu-id="1ea3f-173">Once restore point is selected, on the **Restore configuration** blade, enter or select values for each of the following fields:</span><span class="sxs-lookup"><span data-stu-id="1ea3f-173">Once restore point is selected, on the **Restore configuration** blade, enter or select values for each of the following fields:</span></span>

* <span data-ttu-id="1ea3f-174">**Restore Type** - Create virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-174">**Restore Type** - Create virtual machine.</span></span>
* <span data-ttu-id="1ea3f-175">**Virtual machine name** - Provide a name for the VM.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-175">**Virtual machine name** - Provide a name for the VM.</span></span> <span data-ttu-id="1ea3f-176">The name must be unique to the resource group (for a Resource Manager-deployed VM) or cloud service (for a Classic VM).</span><span class="sxs-lookup"><span data-stu-id="1ea3f-176">The name must be unique to the resource group (for a Resource Manager-deployed VM) or cloud service (for a Classic VM).</span></span> <span data-ttu-id="1ea3f-177">You cannot replace the virtual machine if it already exists in the subscription.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-177">You cannot replace the virtual machine if it already exists in the subscription.</span></span>
* <span data-ttu-id="1ea3f-178">**Resource group** - Use an existing resource group, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-178">**Resource group** - Use an existing resource group, or create a new one.</span></span> <span data-ttu-id="1ea3f-179">If you are restoring a Classic VM, use this field to specify the name of a new cloud service.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-179">If you are restoring a Classic VM, use this field to specify the name of a new cloud service.</span></span> <span data-ttu-id="1ea3f-180">If you are creating a new resource group/cloud service, the name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-180">If you are creating a new resource group/cloud service, the name must be globally unique.</span></span> <span data-ttu-id="1ea3f-181">Typically, the cloud service name is associated with a public-facing URL - for example: [cloudservice].cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-181">Typically, the cloud service name is associated with a public-facing URL - for example: [cloudservice].cloudapp.net.</span></span> <span data-ttu-id="1ea3f-182">If you attempt to use a name for the cloud resource group/cloud service that has already been used, Azure assigns the resource group/cloud service the same name as the VM.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-182">If you attempt to use a name for the cloud resource group/cloud service that has already been used, Azure assigns the resource group/cloud service the same name as the VM.</span></span> <span data-ttu-id="1ea3f-183">Azure displays resource groups/cloud services and VMs not associated with any affinity groups.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-183">Azure displays resource groups/cloud services and VMs not associated with any affinity groups.</span></span> <span data-ttu-id="1ea3f-184">For more information, see [How to migrate from Affinity Groups to a Regional Virtual Network (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="1ea3f-184">For more information, see [How to migrate from Affinity Groups to a Regional Virtual Network (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).</span></span>
* <span data-ttu-id="1ea3f-185">**Virtual Network** - Select the virtual network (VNET) when creating the VM.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-185">**Virtual Network** - Select the virtual network (VNET) when creating the VM.</span></span> <span data-ttu-id="1ea3f-186">The field provides all VNETs associated with the subscription.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-186">The field provides all VNETs associated with the subscription.</span></span> <span data-ttu-id="1ea3f-187">Resource group of the VM is displayed in parentheses.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-187">Resource group of the VM is displayed in parentheses.</span></span>
* <span data-ttu-id="1ea3f-188">**Subnet** - If the VNET has subnets, the first subnet is selected by default.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-188">**Subnet** - If the VNET has subnets, the first subnet is selected by default.</span></span> <span data-ttu-id="1ea3f-189">If there are additional subnets, select the desired subnet.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-189">If there are additional subnets, select the desired subnet.</span></span>
* <span data-ttu-id="1ea3f-190">**Storage account** - This menu lists the storage accounts in the same location as the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-190">**Storage account** - This menu lists the storage accounts in the same location as the Recovery Services vault.</span></span> <span data-ttu-id="1ea3f-191">Storage accounts that are Zone redundant are not supported.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-191">Storage accounts that are Zone redundant are not supported.</span></span> <span data-ttu-id="1ea3f-192">If there are no storage accounts with the same location as the Recovery Services vault, you must create one before starting the restore operation.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-192">If there are no storage accounts with the same location as the Recovery Services vault, you must create one before starting the restore operation.</span></span> <span data-ttu-id="1ea3f-193">The storage account's replication type is mentioned in parentheses.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-193">The storage account's replication type is mentioned in parentheses.</span></span>

![restore configuration wizard is set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> If you are restoring a Resource Manager-deployed VM, you must identify a virtual network (VNET). A virtual network (VNET) is optional for a Classic VM.
>
>

<span data-ttu-id="1ea3f-197">On the **Restore configuration** blade, click **OK** to finalize the restore configuration.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-197">On the **Restore configuration** blade, click **OK** to finalize the restore configuration.</span></span> <span data-ttu-id="1ea3f-198">On the **Restore** blade, click **Restore** to trigger the restore operation.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-198">On the **Restore** blade, click **Restore** to trigger the restore operation.</span></span>

## <a name="restore-backed-up-disks"></a><span data-ttu-id="1ea3f-199">Restore backed up disks</span><span class="sxs-lookup"><span data-stu-id="1ea3f-199">Restore backed up disks</span></span>
<span data-ttu-id="1ea3f-200">If you would like to customize the virtual machine you would like to create from backed up disks than what is present in restore configuration blade, select **Restore disks** as value for **Restore Type**.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-200">If you would like to customize the virtual machine you would like to create from backed up disks than what is present in restore configuration blade, select **Restore disks** as value for **Restore Type**.</span></span> <span data-ttu-id="1ea3f-201">This choice asks for a storage account where disks from backups are copied to.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-201">This choice asks for a storage account where disks from backups are copied to.</span></span> <span data-ttu-id="1ea3f-202">When choosing a storage account, select an account that shares the same location as the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-202">When choosing a storage account, select an account that shares the same location as the Recovery Services vault.</span></span> <span data-ttu-id="1ea3f-203">Storage accounts that are Zone redundant are not supported.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-203">Storage accounts that are Zone redundant are not supported.</span></span> <span data-ttu-id="1ea3f-204">If there are no storage accounts with the same location as the Recovery Services vault, you must create one before starting the restore operation.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-204">If there are no storage accounts with the same location as the Recovery Services vault, you must create one before starting the restore operation.</span></span> <span data-ttu-id="1ea3f-205">The storage account's replication type is mentioned in parentheses.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-205">The storage account's replication type is mentioned in parentheses.</span></span>

<span data-ttu-id="1ea3f-206">After restore operation is completed, you can:</span><span class="sxs-lookup"><span data-stu-id="1ea3f-206">After restore operation is completed, you can:</span></span>
* [<span data-ttu-id="1ea3f-207">Use template to customize the restored VM</span><span class="sxs-lookup"><span data-stu-id="1ea3f-207">Use template to customize the restored VM</span></span>](#use-templates-to-customize-restore-vm)
* [<span data-ttu-id="1ea3f-208">Use the restored disks to attach to an existing virtual machine</span><span class="sxs-lookup"><span data-stu-id="1ea3f-208">Use the restored disks to attach to an existing virtual machine</span></span>](../virtual-machines/windows/attach-disk-portal.md)
* [<span data-ttu-id="1ea3f-209">Create a new virtual machine using PowerShell from restored disks.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-209">Create a new virtual machine using PowerShell from restored disks.</span></span>](./backup-azure-vms-automation.md#restore-an-azure-vm)

<span data-ttu-id="1ea3f-210">On the **Restore configuration** blade, click **OK** to finalize the restore configuration.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-210">On the **Restore configuration** blade, click **OK** to finalize the restore configuration.</span></span> <span data-ttu-id="1ea3f-211">On the **Restore** blade, click **Restore** to trigger the restore operation.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-211">On the **Restore** blade, click **Restore** to trigger the restore operation.</span></span>

![Recovery configuration completed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-the-restore-operation"></a><span data-ttu-id="1ea3f-213">Track the restore operation</span><span class="sxs-lookup"><span data-stu-id="1ea3f-213">Track the restore operation</span></span>
<span data-ttu-id="1ea3f-214">Once you trigger the restore operation, the Backup service creates a job for tracking the restore operation.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-214">Once you trigger the restore operation, the Backup service creates a job for tracking the restore operation.</span></span> <span data-ttu-id="1ea3f-215">The Backup service also creates and temporarily displays the notification in Notifications area of portal.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-215">The Backup service also creates and temporarily displays the notification in Notifications area of portal.</span></span> <span data-ttu-id="1ea3f-216">If you do not see the notification, you can always click the Notifications icon to view your notifications.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-216">If you do not see the notification, you can always click the Notifications icon to view your notifications.</span></span>

![Restore triggered](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/restore-notification.png)

<span data-ttu-id="1ea3f-218">To view the operation while it is processing, or to view when it completed, open the Backup jobs list.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-218">To view the operation while it is processing, or to view when it completed, open the Backup jobs list.</span></span>

1. <span data-ttu-id="1ea3f-219">On the Azure menu, click **Browse** and in the list of services, type **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-219">On the Azure menu, click **Browse** and in the list of services, type **Recovery Services**.</span></span> <span data-ttu-id="1ea3f-220">The list of services adjusts to what you type.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-220">The list of services adjusts to what you type.</span></span> <span data-ttu-id="1ea3f-221">When you see **Recovery Services vaults**, select it.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-221">When you see **Recovery Services vaults**, select it.</span></span>

    ![Open Recovery Services vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    <span data-ttu-id="1ea3f-223">The list of vaults in the subscription is displayed.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-223">The list of vaults in the subscription is displayed.</span></span>

    ![List of Recovery Services vaults](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. <span data-ttu-id="1ea3f-225">From the list, select the vault associated with the VM you restored.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-225">From the list, select the vault associated with the VM you restored.</span></span> <span data-ttu-id="1ea3f-226">When you click the vault, its dashboard opens.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-226">When you click the vault, its dashboard opens.</span></span>
3. <span data-ttu-id="1ea3f-227">In the vault dashboard on the **Backup Jobs** tile, click **Azure Virtual Machines** to display the jobs associated with the vault.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-227">In the vault dashboard on the **Backup Jobs** tile, click **Azure Virtual Machines** to display the jobs associated with the vault.</span></span>

    ![vault dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    <span data-ttu-id="1ea3f-229">The **Backup Jobs** blade opens and displays the list of jobs.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-229">The **Backup Jobs** blade opens and displays the list of jobs.</span></span>

    ![list of VMs in vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-to-customize-restore-vm"></a><span data-ttu-id="1ea3f-231">Use templates to customize restore vm</span><span class="sxs-lookup"><span data-stu-id="1ea3f-231">Use templates to customize restore vm</span></span>
<span data-ttu-id="1ea3f-232">Once [restore disks operation is completed](#Track-the-restore-operation), you can use the template that is generated as part of restore operation to create a new VM with a configuration different from backup configuration or to customize names of resources created as create a new vm from restore point.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-232">Once [restore disks operation is completed](#Track-the-restore-operation), you can use the template that is generated as part of restore operation to create a new VM with a configuration different from backup configuration or to customize names of resources created as create a new vm from restore point.</span></span> 

> [!NOTE]
> Templates will be added as part of Restore Disks for recovery points taken after 1st March, 2017. They are applicable for non-encrypted and non-managed disk VMs. Support for encrypted VMs and Managed Disk VMs is coming in upcoming releases. 
>
>

<span data-ttu-id="1ea3f-236">To get the template generated as part of restore disks option,</span><span class="sxs-lookup"><span data-stu-id="1ea3f-236">To get the template generated as part of restore disks option,</span></span>

1. <span data-ttu-id="1ea3f-237">Go to restore job details corresponding to the job.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-237">Go to restore job details corresponding to the job.</span></span> 
2. <span data-ttu-id="1ea3f-238">This will list the template uri from which you can download the template.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-238">This will list the template uri from which you can download the template.</span></span> <span data-ttu-id="1ea3f-239">Please note the container name from values.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-239">Please note the container name from values.</span></span> 

     ![restore job drill-down](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
     
3. <span data-ttu-id="1ea3f-241">Note down the target storage account name, container name, template blob uri from values.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-241">Note down the target storage account name, container name, template blob uri from values.</span></span> <span data-ttu-id="1ea3f-242">Go to *target storage account > select Blobs > Containers* and go to file and download the file that starts with name *azuredeploy*.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-242">Go to *target storage account > select Blobs > Containers* and go to file and download the file that starts with name *azuredeploy*.</span></span>

    ![download-template-storage-account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/download-template.png)
    
   <span data-ttu-id="1ea3f-244">Alternatively, you can use [Azure Storage explorer](http://storageexplorer.com/) to go to corresponding subscription > target storage account > Blob Containers and select the container name noted in above step.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-244">Alternatively, you can use [Azure Storage explorer](http://storageexplorer.com/) to go to corresponding subscription > target storage account > Blob Containers and select the container name noted in above step.</span></span> <span data-ttu-id="1ea3f-245">On the right side pane that shows files inside the container, download the file that starts with name *azuredeploy*.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-245">On the right side pane that shows files inside the container, download the file that starts with name *azuredeploy*.</span></span> 
   
   ![download-template-storage-explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/template-storage-explorer-download.png)
     
<span data-ttu-id="1ea3f-247">Once template is downloaded, use template deployment to [edit and deploy the template](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) or append more customizations by [authoring a template](../azure-resource-manager/resource-group-authoring-templates.md) before you deploy.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-247">Once template is downloaded, use template deployment to [edit and deploy the template](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) or append more customizations by [authoring a template](../azure-resource-manager/resource-group-authoring-templates.md) before you deploy.</span></span> <span data-ttu-id="1ea3f-248">You can use Load file option to deploy the template downloaded above.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-248">You can use Load file option to deploy the template downloaded above.</span></span> 

   ![loading template deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/loading-template.png)
   
<span data-ttu-id="1ea3f-250">After entering the required values, accept the *Terms and Conditions* and click on **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-250">After entering the required values, accept the *Terms and Conditions* and click on **Purchase**.</span></span>

   ![submitting template deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a><span data-ttu-id="1ea3f-252">Post-Restore steps</span><span class="sxs-lookup"><span data-stu-id="1ea3f-252">Post-Restore steps</span></span>
* <span data-ttu-id="1ea3f-253">If you are using a cloud-init based Linux distribution such as Ubuntu, for security reasons, password is blocked post restore.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-253">If you are using a cloud-init based Linux distribution such as Ubuntu, for security reasons, password is blocked post restore.</span></span> <span data-ttu-id="1ea3f-254">Please use VMAccess extension on the restored VM to [reset the password](../virtual-machines/linux/classic/reset-access.md).</span><span class="sxs-lookup"><span data-stu-id="1ea3f-254">Please use VMAccess extension on the restored VM to [reset the password](../virtual-machines/linux/classic/reset-access.md).</span></span> <span data-ttu-id="1ea3f-255">We recommend using SSH keys on these distributions to avoid resetting password post restore.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-255">We recommend using SSH keys on these distributions to avoid resetting password post restore.</span></span>
* <span data-ttu-id="1ea3f-256">Extensions present during the backup config will be installed, however they won't be enabled.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-256">Extensions present during the backup config will be installed, however they won't be enabled.</span></span> <span data-ttu-id="1ea3f-257">Please reinstall extensions if you see any issue.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-257">Please reinstall extensions if you see any issue.</span></span> 
* <span data-ttu-id="1ea3f-258">If the backed-up VM has static IP, post restore, restored VM will have a dynamic IP to avoid conflict when creating restored VM.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-258">If the backed-up VM has static IP, post restore, restored VM will have a dynamic IP to avoid conflict when creating restored VM.</span></span> <span data-ttu-id="1ea3f-259">Learn more on how you can [add a static IP to restored VM](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)</span><span class="sxs-lookup"><span data-stu-id="1ea3f-259">Learn more on how you can [add a static IP to restored VM](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)</span></span>
* <span data-ttu-id="1ea3f-260">Restored VM will not have availability value set.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-260">Restored VM will not have availability value set.</span></span> <span data-ttu-id="1ea3f-261">We recommend using restore disks option and [adding availability set](../virtual-machines/windows/create-availability-set.md#use-powershell-to-create-an-availability-set) when creating a VM from PowerShell or templates using restored disks.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-261">We recommend using restore disks option and [adding availability set](../virtual-machines/windows/create-availability-set.md#use-powershell-to-create-an-availability-set) when creating a VM from PowerShell or templates using restored disks.</span></span> 

## <a name="backup-for-restored-vms"></a><span data-ttu-id="1ea3f-262">Backup for restored VMs</span><span class="sxs-lookup"><span data-stu-id="1ea3f-262">Backup for restored VMs</span></span>
<span data-ttu-id="1ea3f-263">If you have restored VM to same Resource Group with the same name as originally backed up VM, backup continues on the VM post restore.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-263">If you have restored VM to same Resource Group with the same name as originally backed up VM, backup continues on the VM post restore.</span></span> <span data-ttu-id="1ea3f-264">If you have either restored VM to a different Resource group or specified a different name for restored VM, this is treated as a new VM and you need to setup backup for restored VM.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-264">If you have either restored VM to a different Resource group or specified a different name for restored VM, this is treated as a new VM and you need to setup backup for restored VM.</span></span>

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a><span data-ttu-id="1ea3f-265">Restoring a VM during Azure dataCenter disaster</span><span class="sxs-lookup"><span data-stu-id="1ea3f-265">Restoring a VM during Azure dataCenter disaster</span></span>
<span data-ttu-id="1ea3f-266">Azure Backup allows restoring backed up VMs to the paired data center in case the primary data center where VMs are running experiences disaster and you configured Backup vault to be geo-redundant.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-266">Azure Backup allows restoring backed up VMs to the paired data center in case the primary data center where VMs are running experiences disaster and you configured Backup vault to be geo-redundant.</span></span> <span data-ttu-id="1ea3f-267">During such scenarios, you need to select a storage account, which is present in paired data center and rest of the restore process remains same.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-267">During such scenarios, you need to select a storage account, which is present in paired data center and rest of the restore process remains same.</span></span> <span data-ttu-id="1ea3f-268">Azure Backup uses Compute service from paired geo to create the restored virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-268">Azure Backup uses Compute service from paired geo to create the restored virtual machine.</span></span> <span data-ttu-id="1ea3f-269">Learn more about [Azure Data center resiliency](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)</span><span class="sxs-lookup"><span data-stu-id="1ea3f-269">Learn more about [Azure Data center resiliency](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)</span></span>

## <a name="restoring-vms-with-special-network-configurations"></a><span data-ttu-id="1ea3f-270">Restoring VMs with special network configurations</span><span class="sxs-lookup"><span data-stu-id="1ea3f-270">Restoring VMs with special network configurations</span></span>
<span data-ttu-id="1ea3f-271">It is possible to back up and restore VMs with the following special network configurations.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-271">It is possible to back up and restore VMs with the following special network configurations.</span></span> <span data-ttu-id="1ea3f-272">However, these configurations require some special consideration while going through the restore process.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-272">However, these configurations require some special consideration while going through the restore process.</span></span>

* <span data-ttu-id="1ea3f-273">VMs under load balancer (internal and external)</span><span class="sxs-lookup"><span data-stu-id="1ea3f-273">VMs under load balancer (internal and external)</span></span>
* <span data-ttu-id="1ea3f-274">VMs with multiple reserved IPs</span><span class="sxs-lookup"><span data-stu-id="1ea3f-274">VMs with multiple reserved IPs</span></span>
* <span data-ttu-id="1ea3f-275">VMs with multiple NICs</span><span class="sxs-lookup"><span data-stu-id="1ea3f-275">VMs with multiple NICs</span></span>

> [!IMPORTANT]
> When creating the special network configuration for VMs, you must use PowerShell to create VMs from the disks restored.
>
>

<span data-ttu-id="1ea3f-277">To fully recreate the virtual machines after restoring to disk, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="1ea3f-277">To fully recreate the virtual machines after restoring to disk, follow these steps:</span></span>

1. <span data-ttu-id="1ea3f-278">Restore the disks from a recovery services vault using [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="1ea3f-278">Restore the disks from a recovery services vault using [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
2. <span data-ttu-id="1ea3f-279">Create the VM configuration required for load balancer/multiple NIC/multiple reserved IP using the PowerShell cmdlets and use it to create the VM of desired configuration.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-279">Create the VM configuration required for load balancer/multiple NIC/multiple reserved IP using the PowerShell cmdlets and use it to create the VM of desired configuration.</span></span>

   * <span data-ttu-id="1ea3f-280">Create VM in cloud service with [Internal Load balancer ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span><span class="sxs-lookup"><span data-stu-id="1ea3f-280">Create VM in cloud service with [Internal Load balancer ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)</span></span>
   * <span data-ttu-id="1ea3f-281">Create VM to connect to [Internet facing load balancer](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)</span><span class="sxs-lookup"><span data-stu-id="1ea3f-281">Create VM to connect to [Internet facing load balancer](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)</span></span>
   * <span data-ttu-id="1ea3f-282">Create VM with [multiple NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span><span class="sxs-lookup"><span data-stu-id="1ea3f-282">Create VM with [multiple NICs](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)</span></span>
   * <span data-ttu-id="1ea3f-283">Create VM with [multiple reserved IPs](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span><span class="sxs-lookup"><span data-stu-id="1ea3f-283">Create VM with [multiple reserved IPs](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ea3f-284">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ea3f-284">Next steps</span></span>
<span data-ttu-id="1ea3f-285">Now that you can restore your VMs, see the troubleshooting article for information on common errors with VMs.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-285">Now that you can restore your VMs, see the troubleshooting article for information on common errors with VMs.</span></span> <span data-ttu-id="1ea3f-286">Also, check out the article on managing tasks with your VMs.</span><span class="sxs-lookup"><span data-stu-id="1ea3f-286">Also, check out the article on managing tasks with your VMs.</span></span>

* [<span data-ttu-id="1ea3f-287">Troubleshooting errors</span><span class="sxs-lookup"><span data-stu-id="1ea3f-287">Troubleshooting errors</span></span>](backup-azure-vms-troubleshoot.md#restore)
* [<span data-ttu-id="1ea3f-288">Manage virtual machines</span><span class="sxs-lookup"><span data-stu-id="1ea3f-288">Manage virtual machines</span></span>](backup-azure-manage-vms.md)

























