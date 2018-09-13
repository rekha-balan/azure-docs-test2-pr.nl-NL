---
title: Enable Azure VM backup during creation
description: See the steps to enable Azure virtual machine backup during the creation process.
services: backup, virtual-machines
author: markgalioto
manager: carmonm
tags: azure-resource-manager, virtual-machine-backup
ms.service: backup, virtual-machines
ms.topic: conceptual
ms.date: 01/08/2018
ms.author: trinadhk
ms.openlocfilehash: 9fd4707a201163002cc15cc9cf97e544e76cf7c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866661"
---
# <a name="enable-backup-during-azure-virtual-machine-creation"></a><span data-ttu-id="b5b20-103">Enable backup during Azure virtual machine creation</span><span class="sxs-lookup"><span data-stu-id="b5b20-103">Enable backup during Azure virtual machine creation</span></span> 

<span data-ttu-id="b5b20-104">The Azure Backup service provides an interface to create and configure backups to the cloud.</span><span class="sxs-lookup"><span data-stu-id="b5b20-104">The Azure Backup service provides an interface to create and configure backups to the cloud.</span></span> <span data-ttu-id="b5b20-105">Protect your data by taking backups, called recovery points, at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="b5b20-105">Protect your data by taking backups, called recovery points, at regular intervals.</span></span> <span data-ttu-id="b5b20-106">Azure Backup creates recovery points that can be stored in geo-redundant recovery vaults.</span><span class="sxs-lookup"><span data-stu-id="b5b20-106">Azure Backup creates recovery points that can be stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="b5b20-107">This article details how to enable backup while creating a virtual machine (VM) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b5b20-107">This article details how to enable backup while creating a virtual machine (VM) in the Azure portal.</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="b5b20-108">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="b5b20-108">Log in to Azure</span></span> 

<span data-ttu-id="b5b20-109">If you are not already in signed in to your account, sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5b20-109">If you are not already in signed in to your account, sign in to the [Azure portal](http://portal.azure.com).</span></span>
 
## <a name="create-virtual-machine-with-backup-configured"></a><span data-ttu-id="b5b20-110">Create virtual machine with backup configured</span><span class="sxs-lookup"><span data-stu-id="b5b20-110">Create virtual machine with backup configured</span></span> 

1. <span data-ttu-id="b5b20-111">In the upper left-hand corner of the Azure portal, click **New**.</span><span class="sxs-lookup"><span data-stu-id="b5b20-111">In the upper left-hand corner of the Azure portal, click **New**.</span></span> 

2. <span data-ttu-id="b5b20-112">Select **Compute**, and then select an image of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b5b20-112">Select **Compute**, and then select an image of the virtual machine.</span></span>   

3. <span data-ttu-id="b5b20-113">Enter the virtual machine information.</span><span class="sxs-lookup"><span data-stu-id="b5b20-113">Enter the virtual machine information.</span></span> <span data-ttu-id="b5b20-114">The user name and password provided is used to sign in to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b5b20-114">The user name and password provided is used to sign in to the virtual machine.</span></span> <span data-ttu-id="b5b20-115">When complete, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5b20-115">When complete, click **OK**.</span></span> 

4. <span data-ttu-id="b5b20-116">Select a size for the VM.</span><span class="sxs-lookup"><span data-stu-id="b5b20-116">Select a size for the VM.</span></span>  

5. <span data-ttu-id="b5b20-117">Under **Settings > Backup**, click **Enabled** to bring up backup configuration settings.</span><span class="sxs-lookup"><span data-stu-id="b5b20-117">Under **Settings > Backup**, click **Enabled** to bring up backup configuration settings.</span></span> <span data-ttu-id="b5b20-118">You can accept default values and click **OK** on the settings page to proceed to Summary page to create the VM.</span><span class="sxs-lookup"><span data-stu-id="b5b20-118">You can accept default values and click **OK** on the settings page to proceed to Summary page to create the VM.</span></span> <span data-ttu-id="b5b20-119">If you want to change the values, follow next steps.</span><span class="sxs-lookup"><span data-stu-id="b5b20-119">If you want to change the values, follow next steps.</span></span>  

6. <span data-ttu-id="b5b20-120">Create or select a Recovery Services vault, which holds the backups of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b5b20-120">Create or select a Recovery Services vault, which holds the backups of the virtual machine.</span></span> <span data-ttu-id="b5b20-121">If you are creating a recovery services vault, you can choose a resource group for the vault.</span><span class="sxs-lookup"><span data-stu-id="b5b20-121">If you are creating a recovery services vault, you can choose a resource group for the vault.</span></span>  

    ![Backup configuration in vm create page](./media/backup-during-vm-creation/create-vm-backup-config.png) 

    > [!NOTE] 
    > <span data-ttu-id="b5b20-123">The resource group for the Recovery Services vault can be different than the resource group for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b5b20-123">The resource group for the Recovery Services vault can be different than the resource group for the virtual machine.</span></span>  
    > 
    > 

7. <span data-ttu-id="b5b20-124">By default, a backup policy is selected for you to quickly protect the VM.</span><span class="sxs-lookup"><span data-stu-id="b5b20-124">By default, a backup policy is selected for you to quickly protect the VM.</span></span> <span data-ttu-id="b5b20-125">A backup policy specifies how frequently to take backup snapshots, and how long to retain those backup copies.</span><span class="sxs-lookup"><span data-stu-id="b5b20-125">A backup policy specifies how frequently to take backup snapshots, and how long to retain those backup copies.</span></span> <span data-ttu-id="b5b20-126">You can accept the default policy, or you can create or select a different backup policy.</span><span class="sxs-lookup"><span data-stu-id="b5b20-126">You can accept the default policy, or you can create or select a different backup policy.</span></span> <span data-ttu-id="b5b20-127">To edit the backup policy, select **Backup Policy** and change the values of the policy.</span><span class="sxs-lookup"><span data-stu-id="b5b20-127">To edit the backup policy, select **Backup Policy** and change the values of the policy.</span></span>  

8. <span data-ttu-id="b5b20-128">When you are happy with the backup configuration values, in the Setting page, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5b20-128">When you are happy with the backup configuration values, in the Setting page, click **OK**.</span></span>  

9. <span data-ttu-id="b5b20-129">On the summary page, once validation has passed, click **Create** to create a virtual machine that uses the configured backup settings.</span><span class="sxs-lookup"><span data-stu-id="b5b20-129">On the summary page, once validation has passed, click **Create** to create a virtual machine that uses the configured backup settings.</span></span> 

## <a name="initiate-a-backup-after-creating-the-vm"></a><span data-ttu-id="b5b20-130">Initiate a backup after creating the VM</span><span class="sxs-lookup"><span data-stu-id="b5b20-130">Initiate a backup after creating the VM</span></span> 

<span data-ttu-id="b5b20-131">Though the Backup policy has been created, it is good practice to create an initial backup.</span><span class="sxs-lookup"><span data-stu-id="b5b20-131">Though the Backup policy has been created, it is good practice to create an initial backup.</span></span> <span data-ttu-id="b5b20-132">To view the backup details for the virtual machine once the VM creation template finishes, from the **Operations** setting on the left-hand menu, click **Backup**.</span><span class="sxs-lookup"><span data-stu-id="b5b20-132">To view the backup details for the virtual machine once the VM creation template finishes, from the **Operations** setting on the left-hand menu, click **Backup**.</span></span> <span data-ttu-id="b5b20-133">You can use this to trigger an on-demand backup, restore a full VM or all disks, restore files from VM backup, or change the backup policy associated with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b5b20-133">You can use this to trigger an on-demand backup, restore a full VM or all disks, restore files from VM backup, or change the backup policy associated with the virtual machine.</span></span>  

## <a name="using-a-resource-manager-template-to-deploy-a-protected-vm"></a><span data-ttu-id="b5b20-134">Using a Resource Manager template to deploy a protected VM</span><span class="sxs-lookup"><span data-stu-id="b5b20-134">Using a Resource Manager template to deploy a protected VM</span></span>

<span data-ttu-id="b5b20-135">The previous steps explain how to use the Azure portal to create a virtual machine, and protect it to a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="b5b20-135">The previous steps explain how to use the Azure portal to create a virtual machine, and protect it to a Recovery Services vault.</span></span> <span data-ttu-id="b5b20-136">If you want to quickly deploy one or more virtual machines, and protect them to a Recovery Services vault, see the template, [Deploy a Windows VM and enable backup](https://azure.microsoft.com/resources/templates/101-recovery-services-create-vm-and-configure-backup/).</span><span class="sxs-lookup"><span data-stu-id="b5b20-136">If you want to quickly deploy one or more virtual machines, and protect them to a Recovery Services vault, see the template, [Deploy a Windows VM and enable backup](https://azure.microsoft.com/resources/templates/101-recovery-services-create-vm-and-configure-backup/).</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="b5b20-137">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="b5b20-137">Frequently asked questions</span></span> 

### <a name="which-vm-images-enable-backup-at-the-time-of-vm-creation"></a><span data-ttu-id="b5b20-138">Which VM images enable backup at the time of VM creation?</span><span class="sxs-lookup"><span data-stu-id="b5b20-138">Which VM images enable backup at the time of VM creation?</span></span> 

<span data-ttu-id="b5b20-139">The following list of core images published by Microsoft are supported for enabling backup during VM creation.</span><span class="sxs-lookup"><span data-stu-id="b5b20-139">The following list of core images published by Microsoft are supported for enabling backup during VM creation.</span></span> <span data-ttu-id="b5b20-140">For other VMs, you can enable backup once the VM is created.</span><span class="sxs-lookup"><span data-stu-id="b5b20-140">For other VMs, you can enable backup once the VM is created.</span></span> <span data-ttu-id="b5b20-141">Learn more [Enable backup after VM is created](quick-backup-vm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b5b20-141">Learn more [Enable backup after VM is created](quick-backup-vm-portal.md)</span></span> 

- <span data-ttu-id="b5b20-142">**Windows** - Windows Server 2016 Data center, Windows Server 2016 Data Center core, Windows Server 2012 DataCenter, Windows Server 2012 R2 DataCenter, Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="b5b20-142">**Windows** - Windows Server 2016 Data center, Windows Server 2016 Data Center core, Windows Server 2012 DataCenter, Windows Server 2012 R2 DataCenter, Windows Server 2008 R2 SP1</span></span> 
- <span data-ttu-id="b5b20-143">**Ubuntu** - Ubuntu Server 1710, Ubuntu Server 1704, UUbuntu Server 1604(LTS), Ubuntu Server 1404(LTS)</span><span class="sxs-lookup"><span data-stu-id="b5b20-143">**Ubuntu** - Ubuntu Server 1710, Ubuntu Server 1704, UUbuntu Server 1604(LTS), Ubuntu Server 1404(LTS)</span></span> 
- <span data-ttu-id="b5b20-144">**Red Hat** - RHEL 6.7, 6.8, 6.9, 7.2, 7.3, 7.4</span><span class="sxs-lookup"><span data-stu-id="b5b20-144">**Red Hat** - RHEL 6.7, 6.8, 6.9, 7.2, 7.3, 7.4</span></span> 
- <span data-ttu-id="b5b20-145">**SUSE** - SUSE Linux Enterprise Server 11 SP4, 12 SP2, 12 SP3</span><span class="sxs-lookup"><span data-stu-id="b5b20-145">**SUSE** - SUSE Linux Enterprise Server 11 SP4, 12 SP2, 12 SP3</span></span> 
- <span data-ttu-id="b5b20-146">**Debian** - Debian 8, Debian 9</span><span class="sxs-lookup"><span data-stu-id="b5b20-146">**Debian** - Debian 8, Debian 9</span></span> 
- <span data-ttu-id="b5b20-147">**CentOS** - CentOS 6.9, CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="b5b20-147">**CentOS** - CentOS 6.9, CentOS 7.3</span></span> 
- <span data-ttu-id="b5b20-148">**Oracle Linux** - Oracle Linux 6.7, 6.8, 6.9, 7.2, 7.3</span><span class="sxs-lookup"><span data-stu-id="b5b20-148">**Oracle Linux** - Oracle Linux 6.7, 6.8, 6.9, 7.2, 7.3</span></span> 
 
### <a name="is-backup-cost-included-in-the-vm-cost"></a><span data-ttu-id="b5b20-149">Is backup cost included in the VM cost?</span><span class="sxs-lookup"><span data-stu-id="b5b20-149">Is backup cost included in the VM cost?</span></span> 

<span data-ttu-id="b5b20-150">No, backup costs are separate, or distinct, from virtual machines costs.</span><span class="sxs-lookup"><span data-stu-id="b5b20-150">No, backup costs are separate, or distinct, from virtual machines costs.</span></span> <span data-ttu-id="b5b20-151">For more information on backup pricing, see the [Backup Pricing site](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="b5b20-151">For more information on backup pricing, see the [Backup Pricing site](https://azure.microsoft.com/pricing/details/backup/).</span></span>
 
### <a name="which-permissions-are-required-to-enable-backup-on-a-vm"></a><span data-ttu-id="b5b20-152">Which permissions are required to enable backup on a VM?</span><span class="sxs-lookup"><span data-stu-id="b5b20-152">Which permissions are required to enable backup on a VM?</span></span> 

<span data-ttu-id="b5b20-153">If you are a virtual machine contributor, you can enable backup on the VM.</span><span class="sxs-lookup"><span data-stu-id="b5b20-153">If you are a virtual machine contributor, you can enable backup on the VM.</span></span> <span data-ttu-id="b5b20-154">If you are using a custom role, you need the following permissions to successfully enable backup on the VM.</span><span class="sxs-lookup"><span data-stu-id="b5b20-154">If you are using a custom role, you need the following permissions to successfully enable backup on the VM.</span></span> 

- <span data-ttu-id="b5b20-155">Microsoft.RecoveryServices/Vaults/write</span><span class="sxs-lookup"><span data-stu-id="b5b20-155">Microsoft.RecoveryServices/Vaults/write</span></span> 
- <span data-ttu-id="b5b20-156">Microsoft.RecoveryServices/Vaults/read</span><span class="sxs-lookup"><span data-stu-id="b5b20-156">Microsoft.RecoveryServices/Vaults/read</span></span> 
- <span data-ttu-id="b5b20-157">Microsoft.RecoveryServices/locations/\*</span><span class="sxs-lookup"><span data-stu-id="b5b20-157">Microsoft.RecoveryServices/locations/\*</span></span> 
- <span data-ttu-id="b5b20-158">Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/\*/read</span><span class="sxs-lookup"><span data-stu-id="b5b20-158">Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/\*/read</span></span> 
- <span data-ttu-id="b5b20-159">Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read</span><span class="sxs-lookup"><span data-stu-id="b5b20-159">Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read</span></span> 
- <span data-ttu-id="b5b20-160">Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/write</span><span class="sxs-lookup"><span data-stu-id="b5b20-160">Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/write</span></span> 
- <span data-ttu-id="b5b20-161">Microsoft.RecoveryServices/Vaults/backupFabrics/backupProtectionIntent/write</span><span class="sxs-lookup"><span data-stu-id="b5b20-161">Microsoft.RecoveryServices/Vaults/backupFabrics/backupProtectionIntent/write</span></span> 
- <span data-ttu-id="b5b20-162">Microsoft.RecoveryServices/Vaults/backupPolicies/read</span><span class="sxs-lookup"><span data-stu-id="b5b20-162">Microsoft.RecoveryServices/Vaults/backupPolicies/read</span></span> 
- <span data-ttu-id="b5b20-163">Microsoft.RecoveryServices/Vaults/backupPolicies/write</span><span class="sxs-lookup"><span data-stu-id="b5b20-163">Microsoft.RecoveryServices/Vaults/backupPolicies/write</span></span> 
 
<span data-ttu-id="b5b20-164">If your recovery services vault and virtual machine have different resource groups, be sure you have write permissions in the recovery services vault resource group.</span><span class="sxs-lookup"><span data-stu-id="b5b20-164">If your recovery services vault and virtual machine have different resource groups, be sure you have write permissions in the recovery services vault resource group.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b5b20-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5b20-165">Next steps</span></span> 

<span data-ttu-id="b5b20-166">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span><span class="sxs-lookup"><span data-stu-id="b5b20-166">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span></span> 

- [<span data-ttu-id="b5b20-167">Manage and monitor your virtual machines</span><span class="sxs-lookup"><span data-stu-id="b5b20-167">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md) 
- [<span data-ttu-id="b5b20-168">Restore virtual machines</span><span class="sxs-lookup"><span data-stu-id="b5b20-168">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md) 
