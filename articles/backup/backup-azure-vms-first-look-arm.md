---
title: 'First look: Protect Azure VMs with a recovery services vault | Microsoft Docs'
description: Protect Azure VMs with a recovery services vault. Use backups of Resource Manager-deployed VMs, Classic-deployed VMs and Premium Storage VMs, Encrypted VMs, VMs on Managed Disks to protect your data. Create and register a recovery services vault. Register VMs, create policy, and protect VMs in Azure.
services: backup
documentationcenter: ''
author: markgalioto
manager: cfreeman
editor: ''
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5b953a213e824d7fde028bd8406a282e1ead421
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553221"
---
# <a name="back-up-azure-virtual-machines-to-recovery-services-vaults"></a><span data-ttu-id="7c62a-106">Back up Azure virtual machines to Recovery Services vaults</span><span class="sxs-lookup"><span data-stu-id="7c62a-106">Back up Azure virtual machines to Recovery Services vaults</span></span>
> [!div class="op_single_selector"]
> * [Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md)
> * [Protect VMs with a backup vault](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="7c62a-109">This tutorial takes you through the steps for creating a recovery services vault and backing up an Azure virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="7c62a-109">This tutorial takes you through the steps for creating a recovery services vault and backing up an Azure virtual machine (VM).</span></span> <span data-ttu-id="7c62a-110">Recovery services vaults protect:</span><span class="sxs-lookup"><span data-stu-id="7c62a-110">Recovery services vaults protect:</span></span>

* <span data-ttu-id="7c62a-111">Azure Resource Manager-deployed VMs</span><span class="sxs-lookup"><span data-stu-id="7c62a-111">Azure Resource Manager-deployed VMs</span></span>
* <span data-ttu-id="7c62a-112">Classic VMs</span><span class="sxs-lookup"><span data-stu-id="7c62a-112">Classic VMs</span></span>
* <span data-ttu-id="7c62a-113">Standard storage VMs</span><span class="sxs-lookup"><span data-stu-id="7c62a-113">Standard storage VMs</span></span>
* <span data-ttu-id="7c62a-114">Premium storage VMs</span><span class="sxs-lookup"><span data-stu-id="7c62a-114">Premium storage VMs</span></span>
* <span data-ttu-id="7c62a-115">VMs running on Managed Disks</span><span class="sxs-lookup"><span data-stu-id="7c62a-115">VMs running on Managed Disks</span></span>
* <span data-ttu-id="7c62a-116">VMs encrypted using Azure Disk Encryption, with BEK and KEK</span><span class="sxs-lookup"><span data-stu-id="7c62a-116">VMs encrypted using Azure Disk Encryption, with BEK and KEK</span></span>
* <span data-ttu-id="7c62a-117">Application consistent backup of Windows VMs using VSS and Linux VMs using custom pre-snapshot and post-snapshot scripts</span><span class="sxs-lookup"><span data-stu-id="7c62a-117">Application consistent backup of Windows VMs using VSS and Linux VMs using custom pre-snapshot and post-snapshot scripts</span></span>

<span data-ttu-id="7c62a-118">For more information on protecting Premium storage VMs, see the article, [Back up and Restore Premium Storage VMs](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup).</span><span class="sxs-lookup"><span data-stu-id="7c62a-118">For more information on protecting Premium storage VMs, see the article, [Back up and Restore Premium Storage VMs](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup).</span></span> <span data-ttu-id="7c62a-119">For more information on support for managed disk VMs, see [Back up and restore VMs on managed disks](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).</span><span class="sxs-lookup"><span data-stu-id="7c62a-119">For more information on support for managed disk VMs, see [Back up and restore VMs on managed disks](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).</span></span> <span data-ttu-id="7c62a-120">For more information on pre and post-script framework for Linux VM backup see [Application consistent Linux VM backup using pre-script and post-script] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)</span><span class="sxs-lookup"><span data-stu-id="7c62a-120">For more information on pre and post-script framework for Linux VM backup see [Application consistent Linux VM backup using pre-script and post-script] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)</span></span>

> [!NOTE]
> This tutorial assumes you already have a VM in your Azure subscription and that you have taken measures to allow the backup service to access the VM.
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="7c62a-122">Depending on the number of virtual machines you want to protect, you can begin from different starting points.</span><span class="sxs-lookup"><span data-stu-id="7c62a-122">Depending on the number of virtual machines you want to protect, you can begin from different starting points.</span></span> <span data-ttu-id="7c62a-123">If you want to back up multiple virtual machines in one operation, go to the Recovery Services vault and [initiate the backup job from the vault dashboard](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault).</span><span class="sxs-lookup"><span data-stu-id="7c62a-123">If you want to back up multiple virtual machines in one operation, go to the Recovery Services vault and [initiate the backup job from the vault dashboard](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault).</span></span> <span data-ttu-id="7c62a-124">If you want to back up a single virtual machine, you can initiate the backup job from VM management blade.</span><span class="sxs-lookup"><span data-stu-id="7c62a-124">If you want to back up a single virtual machine, you can initiate the backup job from VM management blade.</span></span>

## <a name="configure-the-backup-job-from-the-vm-management-blade"></a><span data-ttu-id="7c62a-125">Configure the backup job from the VM management blade</span><span class="sxs-lookup"><span data-stu-id="7c62a-125">Configure the backup job from the VM management blade</span></span>

<span data-ttu-id="7c62a-126">Use the following steps to configure the backup job from the virtual machine management blade in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7c62a-126">Use the following steps to configure the backup job from the virtual machine management blade in the Azure portal.</span></span> <span data-ttu-id="7c62a-127">These steps do not apply to the virtual machines in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="7c62a-127">These steps do not apply to the virtual machines in the classic portal.</span></span>

1. <span data-ttu-id="7c62a-128">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7c62a-128">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7c62a-129">On the Hub menu, click **More Services** and in the Filter dialog, type **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-129">On the Hub menu, click **More Services** and in the Filter dialog, type **Virtual machines**.</span></span> <span data-ttu-id="7c62a-130">As you type, the list of resources filters.</span><span class="sxs-lookup"><span data-stu-id="7c62a-130">As you type, the list of resources filters.</span></span> <span data-ttu-id="7c62a-131">When you see Virtual machines, select it.</span><span class="sxs-lookup"><span data-stu-id="7c62a-131">When you see Virtual machines, select it.</span></span>

  ![On Hub menu, click More Services to open text dialog, and type Virtual machines](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  <span data-ttu-id="7c62a-133">The list of virtual machines (VM) in the subscription, appears.</span><span class="sxs-lookup"><span data-stu-id="7c62a-133">The list of virtual machines (VM) in the subscription, appears.</span></span>

  ![The list of VMs in the subscription appears.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. <span data-ttu-id="7c62a-135">From the list, select a VM to back up.</span><span class="sxs-lookup"><span data-stu-id="7c62a-135">From the list, select a VM to back up.</span></span>

  ![The list of VMs in the subscription appears.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  <span data-ttu-id="7c62a-137">When you select the VM, the list of virtual machines shifts to the left, and the virtual machine management blade and the virtual machine dashboard, open.</span><span class="sxs-lookup"><span data-stu-id="7c62a-137">When you select the VM, the list of virtual machines shifts to the left, and the virtual machine management blade and the virtual machine dashboard, open.</span></span> </br>
 <span data-ttu-id="7c62a-138">![VM Management blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/vm-management-blade.png)</span><span class="sxs-lookup"><span data-stu-id="7c62a-138">![VM Management blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/vm-management-blade.png)</span></span>

4. <span data-ttu-id="7c62a-139">On the VM management blade, in the **Settings** section, click **Backup**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-139">On the VM management blade, in the **Settings** section, click **Backup**.</span></span> </br>

  ![Backup option in VM management blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  <span data-ttu-id="7c62a-141">The Enable backup blade opens.</span><span class="sxs-lookup"><span data-stu-id="7c62a-141">The Enable backup blade opens.</span></span>

  ![Backup option in VM management blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. <span data-ttu-id="7c62a-143">For the Recovery Services vault, click **Select existing** and choose the vault from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="7c62a-143">For the Recovery Services vault, click **Select existing** and choose the vault from the drop-down list.</span></span>

  ![Enable Backup Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  <span data-ttu-id="7c62a-145">If there are no Recovery Services vaults, or you want to use a new vault, click **Create new** and provide the name for the new vault.</span><span class="sxs-lookup"><span data-stu-id="7c62a-145">If there are no Recovery Services vaults, or you want to use a new vault, click **Create new** and provide the name for the new vault.</span></span> <span data-ttu-id="7c62a-146">A new vault is created in the same Resource Group and same location as the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7c62a-146">A new vault is created in the same Resource Group and same location as the virtual machine.</span></span> <span data-ttu-id="7c62a-147">If you want to create a Recovery Services vault with different values, see the section on how to [create a recovery services vault](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).</span><span class="sxs-lookup"><span data-stu-id="7c62a-147">If you want to create a Recovery Services vault with different values, see the section on how to [create a recovery services vault](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).</span></span>

6. <span data-ttu-id="7c62a-148">To view the details of the Backup policy, click **Backup policy**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-148">To view the details of the Backup policy, click **Backup policy**.</span></span>

  <span data-ttu-id="7c62a-149">The **Backup policy** blade opens and provides the details of the selected policy.</span><span class="sxs-lookup"><span data-stu-id="7c62a-149">The **Backup policy** blade opens and provides the details of the selected policy.</span></span> <span data-ttu-id="7c62a-150">If other policies exist, use the drop-down menu to choose a different backup policy.</span><span class="sxs-lookup"><span data-stu-id="7c62a-150">If other policies exist, use the drop-down menu to choose a different backup policy.</span></span> <span data-ttu-id="7c62a-151">If you want to create a policy, select **Create New** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="7c62a-151">If you want to create a policy, select **Create New** from the drop-down menu.</span></span> <span data-ttu-id="7c62a-152">For instructions on defining a backup policy, see [Defining a backup policy](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="7c62a-152">For instructions on defining a backup policy, see [Defining a backup policy](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).</span></span> <span data-ttu-id="7c62a-153">To save the changes to the backup policy and return to the Enable backup blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-153">To save the changes to the backup policy and return to the Enable backup blade, click **OK**.</span></span>

  ![Select backup policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. <span data-ttu-id="7c62a-155">On the Enable backup blade, click **Enable Backup** to deploy the policy.</span><span class="sxs-lookup"><span data-stu-id="7c62a-155">On the Enable backup blade, click **Enable Backup** to deploy the policy.</span></span> <span data-ttu-id="7c62a-156">Deploying the policy associates it with the vault and the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="7c62a-156">Deploying the policy associates it with the vault and the virtual machines.</span></span>

  ![Enable Backup button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. <span data-ttu-id="7c62a-158">You can track the configuration progress through the notifications that appear in the portal.</span><span class="sxs-lookup"><span data-stu-id="7c62a-158">You can track the configuration progress through the notifications that appear in the portal.</span></span> <span data-ttu-id="7c62a-159">The following example shows that Deployment started.</span><span class="sxs-lookup"><span data-stu-id="7c62a-159">The following example shows that Deployment started.</span></span>

  ![Enable Backup notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. <span data-ttu-id="7c62a-161">Once the configuration progress has completed, on the VM management blade, click **Backup** to open the Backup Item blade and view the details.</span><span class="sxs-lookup"><span data-stu-id="7c62a-161">Once the configuration progress has completed, on the VM management blade, click **Backup** to open the Backup Item blade and view the details.</span></span>

  ![VM Backup Item View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-item-view.png)

  <span data-ttu-id="7c62a-163">Until the initial backup has completed, **Last backup status** shows as **Warning(Initial backup pending)**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-163">Until the initial backup has completed, **Last backup status** shows as **Warning(Initial backup pending)**.</span></span> <span data-ttu-id="7c62a-164">To see when the next scheduled backup job occurs, under **Backup policy** click the name of the policy.</span><span class="sxs-lookup"><span data-stu-id="7c62a-164">To see when the next scheduled backup job occurs, under **Backup policy** click the name of the policy.</span></span> <span data-ttu-id="7c62a-165">The Backup Policy blade opens and shows the time of the scheduled backup.</span><span class="sxs-lookup"><span data-stu-id="7c62a-165">The Backup Policy blade opens and shows the time of the scheduled backup.</span></span>

10. <span data-ttu-id="7c62a-166">To run a Backup job and create the initial recovery point, on the Backup vault blade click **Backup now**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-166">To run a Backup job and create the initial recovery point, on the Backup vault blade click **Backup now**.</span></span>

  ![click Backup now to run the initial backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-now.png)

  <span data-ttu-id="7c62a-168">The Backup Now blade opens.</span><span class="sxs-lookup"><span data-stu-id="7c62a-168">The Backup Now blade opens.</span></span>

  ![shows the Backup Now blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. <span data-ttu-id="7c62a-170">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-170">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![set the last day the Backup Now recovery point is retained](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="7c62a-172">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span><span class="sxs-lookup"><span data-stu-id="7c62a-172">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span>

## <a name="configure-the-backup-job-from-the-recovery-services-vault"></a><span data-ttu-id="7c62a-173">Configure the backup job from the Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="7c62a-173">Configure the backup job from the Recovery Services vault</span></span>
<span data-ttu-id="7c62a-174">To configure the backup job, you complete the following steps.</span><span class="sxs-lookup"><span data-stu-id="7c62a-174">To configure the backup job, you complete the following steps.</span></span>  

1. <span data-ttu-id="7c62a-175">Create a Recovery Services vault for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7c62a-175">Create a Recovery Services vault for a virtual machine.</span></span>
2. <span data-ttu-id="7c62a-176">Use the Azure portal to select a Scenario, set a Backup policy, and identify items to protect.</span><span class="sxs-lookup"><span data-stu-id="7c62a-176">Use the Azure portal to select a Scenario, set a Backup policy, and identify items to protect.</span></span>
3. <span data-ttu-id="7c62a-177">Run the initial backup.</span><span class="sxs-lookup"><span data-stu-id="7c62a-177">Run the initial backup.</span></span>

## <a name="create-a-recovery-services-vault-for-a-vm"></a><span data-ttu-id="7c62a-178">Create a recovery services vault for a VM</span><span class="sxs-lookup"><span data-stu-id="7c62a-178">Create a recovery services vault for a VM</span></span>
<span data-ttu-id="7c62a-179">A Recovery Services vault is an entity that stores all the backups and recovery points that have been created over time.</span><span class="sxs-lookup"><span data-stu-id="7c62a-179">A Recovery Services vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="7c62a-180">The Recovery Services vault also contains the backup policy applied to the protected VMs.</span><span class="sxs-lookup"><span data-stu-id="7c62a-180">The Recovery Services vault also contains the backup policy applied to the protected VMs.</span></span>

> [!NOTE]
> Backing up VMs is a local process. You cannot back up VMs from one location to a Recovery Services vault in another location. So, for every Azure location that has VMs to be backed up, at least one Recovery Services vault must exist in that location.
>
>

<span data-ttu-id="7c62a-184">To create a Recovery Services vault:</span><span class="sxs-lookup"><span data-stu-id="7c62a-184">To create a Recovery Services vault:</span></span>

1. <span data-ttu-id="7c62a-185">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/) using your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7c62a-185">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="7c62a-186">On the Hub menu, click **More services** and in the Filter dialog type **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-186">On the Hub menu, click **More services** and in the Filter dialog type **Recovery Services**.</span></span> <span data-ttu-id="7c62a-187">As you type, the list of resources filters.</span><span class="sxs-lookup"><span data-stu-id="7c62a-187">As you type, the list of resources filters.</span></span> <span data-ttu-id="7c62a-188">When you see Recovery Services vaults in the list, click it.</span><span class="sxs-lookup"><span data-stu-id="7c62a-188">When you see Recovery Services vaults in the list, click it.</span></span>

    ![Create Recovery Services Vault step 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="7c62a-190">If there are Recovery Services vaults in the subscription, the vaults are listed.</span><span class="sxs-lookup"><span data-stu-id="7c62a-190">If there are Recovery Services vaults in the subscription, the vaults are listed.</span></span>

    ![Create Recovery Services Vault step 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. <span data-ttu-id="7c62a-192">On the **Recovery Services vaults** menu, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-192">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Create Recovery Services Vault step 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="7c62a-194">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-194">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Create Recovery Services Vault step 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="7c62a-196">For **Name**, enter a friendly name to identify the vault.</span><span class="sxs-lookup"><span data-stu-id="7c62a-196">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="7c62a-197">The name needs to be unique for the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7c62a-197">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="7c62a-198">Type a name that contains between 2 and 50 characters.</span><span class="sxs-lookup"><span data-stu-id="7c62a-198">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="7c62a-199">It must start with a letter, and can contain only letters, numbers, and hyphens.</span><span class="sxs-lookup"><span data-stu-id="7c62a-199">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="7c62a-200">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7c62a-200">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="7c62a-201">If you use only one subscription, that subscription appears and you can skip to the next step.</span><span class="sxs-lookup"><span data-stu-id="7c62a-201">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="7c62a-202">If you are not sure which subscription to use, use the default (or suggested) subscription.</span><span class="sxs-lookup"><span data-stu-id="7c62a-202">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="7c62a-203">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="7c62a-203">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="7c62a-204">In the **Resource group** section:</span><span class="sxs-lookup"><span data-stu-id="7c62a-204">In the **Resource group** section:</span></span>

    * <span data-ttu-id="7c62a-205">select **Create new** if you want to create a Resource group.</span><span class="sxs-lookup"><span data-stu-id="7c62a-205">select **Create new** if you want to create a Resource group.</span></span>
    <span data-ttu-id="7c62a-206">Or</span><span class="sxs-lookup"><span data-stu-id="7c62a-206">Or</span></span>
    * <span data-ttu-id="7c62a-207">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span><span class="sxs-lookup"><span data-stu-id="7c62a-207">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="7c62a-208">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c62a-208">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="7c62a-209">Click **Location** to select the geographic region for the vault.</span><span class="sxs-lookup"><span data-stu-id="7c62a-209">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="7c62a-210">This choice determines the geographic region where your backup data is sent.</span><span class="sxs-lookup"><span data-stu-id="7c62a-210">This choice determines the geographic region where your backup data is sent.</span></span>

  > [!IMPORTANT]
  > If you are unsure of the location in which your VM exists, close out of the vault creation dialog, and go to the list of Virtual Machines in the portal. If you have virtual machines in multiple regions, create a Recovery Services vault in each region. Create the vault in the first location before going to the next location. There is no need to specify the storage accounts used to store the backup data--the Recovery Services vault and the Azure Backup service automatically handle the storage.
  >

8. <span data-ttu-id="7c62a-215">At the bottom of the Recovery Services vault blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-215">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="7c62a-216">It can take several minutes for the Recovery Services vault to be created.</span><span class="sxs-lookup"><span data-stu-id="7c62a-216">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="7c62a-217">Monitor the status notifications in the upper right-hand area of the portal.</span><span class="sxs-lookup"><span data-stu-id="7c62a-217">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="7c62a-218">Once your vault is created, it appears in the list of Recovery Services vaults.</span><span class="sxs-lookup"><span data-stu-id="7c62a-218">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="7c62a-219">If after several minutes you don't see your vault, click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-219">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Click Refresh button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="7c62a-221">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span><span class="sxs-lookup"><span data-stu-id="7c62a-221">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

<span data-ttu-id="7c62a-222">Now that you've created your vault, learn how to set the storage replication.</span><span class="sxs-lookup"><span data-stu-id="7c62a-222">Now that you've created your vault, learn how to set the storage replication.</span></span>

### <a name="set-storage-replication"></a><span data-ttu-id="7c62a-223">Set Storage Replication</span><span class="sxs-lookup"><span data-stu-id="7c62a-223">Set Storage Replication</span></span>
<span data-ttu-id="7c62a-224">The storage replication option allows you to choose between geo-redundant storage and locally redundant storage.</span><span class="sxs-lookup"><span data-stu-id="7c62a-224">The storage replication option allows you to choose between geo-redundant storage and locally redundant storage.</span></span> <span data-ttu-id="7c62a-225">By default, your vault has geo-redundant storage.</span><span class="sxs-lookup"><span data-stu-id="7c62a-225">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="7c62a-226">If the Recovery Services vault is your primary backup, leave the storage replication option set to geo-redundant storage.</span><span class="sxs-lookup"><span data-stu-id="7c62a-226">If the Recovery Services vault is your primary backup, leave the storage replication option set to geo-redundant storage.</span></span> <span data-ttu-id="7c62a-227">Choose locally redundant storage if you want a cheaper option that isn't as durable.</span><span class="sxs-lookup"><span data-stu-id="7c62a-227">Choose locally redundant storage if you want a cheaper option that isn't as durable.</span></span> <span data-ttu-id="7c62a-228">Read more about [geo-redundant](../storage/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/storage-redundancy.md#locally-redundant-storage) storage options in the [Azure Storage replication overview](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="7c62a-228">Read more about [geo-redundant](../storage/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/storage-redundancy.md#locally-redundant-storage) storage options in the [Azure Storage replication overview](../storage/storage-redundancy.md).</span></span>

<span data-ttu-id="7c62a-229">To edit the storage replication setting:</span><span class="sxs-lookup"><span data-stu-id="7c62a-229">To edit the storage replication setting:</span></span>

1. <span data-ttu-id="7c62a-230">From the **Recovery Services vaults** blade, select the new vault.</span><span class="sxs-lookup"><span data-stu-id="7c62a-230">From the **Recovery Services vaults** blade, select the new vault.</span></span>

  ![Select the new vault from the list of Recovery Services vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  <span data-ttu-id="7c62a-232">When you select the vault, the Settings blade (*which has the vault's name at the top*) and the vault details blade open.</span><span class="sxs-lookup"><span data-stu-id="7c62a-232">When you select the vault, the Settings blade (*which has the vault's name at the top*) and the vault details blade open.</span></span>

  ![View the storage configuration for new vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="7c62a-234">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-234">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="7c62a-235">The Backup Infrastructure blade opens.</span><span class="sxs-lookup"><span data-stu-id="7c62a-235">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="7c62a-236">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span><span class="sxs-lookup"><span data-stu-id="7c62a-236">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Set the storage configuration for new vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="7c62a-238">Choose the appropriate storage replication option for your vault.</span><span class="sxs-lookup"><span data-stu-id="7c62a-238">Choose the appropriate storage replication option for your vault.</span></span>

    ![storage configuration choices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="7c62a-240">By default, your vault has geo-redundant storage.</span><span class="sxs-lookup"><span data-stu-id="7c62a-240">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="7c62a-241">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-241">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="7c62a-242">If you don't use Azure as a primary backup storage endpoint, then choose **Locally redundant**, which reduces the Azure storage costs.</span><span class="sxs-lookup"><span data-stu-id="7c62a-242">If you don't use Azure as a primary backup storage endpoint, then choose **Locally redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="7c62a-243">Read more about [geo-redundant](../storage/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="7c62a-243">Read more about [geo-redundant](../storage/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/storage-redundancy.md).</span></span>


## <a name="select-a-backup-goal-set-policy-and-define-items-to-protect"></a><span data-ttu-id="7c62a-244">Select a backup goal, set policy and define items to protect</span><span class="sxs-lookup"><span data-stu-id="7c62a-244">Select a backup goal, set policy and define items to protect</span></span>
<span data-ttu-id="7c62a-245">Before registering a VM with a vault, run the discovery process to ensure that any new virtual machines that have been added to the subscription are identified.</span><span class="sxs-lookup"><span data-stu-id="7c62a-245">Before registering a VM with a vault, run the discovery process to ensure that any new virtual machines that have been added to the subscription are identified.</span></span> <span data-ttu-id="7c62a-246">The process queries Azure for the list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span><span class="sxs-lookup"><span data-stu-id="7c62a-246">The process queries Azure for the list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span> <span data-ttu-id="7c62a-247">In the Azure portal, scenario refers to what you are going to put into the recovery services vault.</span><span class="sxs-lookup"><span data-stu-id="7c62a-247">In the Azure portal, scenario refers to what you are going to put into the recovery services vault.</span></span> <span data-ttu-id="7c62a-248">Policy is the schedule for how often and when recovery points are taken.</span><span class="sxs-lookup"><span data-stu-id="7c62a-248">Policy is the schedule for how often and when recovery points are taken.</span></span> <span data-ttu-id="7c62a-249">Policy also includes the retention range for the recovery points.</span><span class="sxs-lookup"><span data-stu-id="7c62a-249">Policy also includes the retention range for the recovery points.</span></span>

1. <span data-ttu-id="7c62a-250">If you already have a recovery services vault open, proceed to step 2.</span><span class="sxs-lookup"><span data-stu-id="7c62a-250">If you already have a recovery services vault open, proceed to step 2.</span></span> <span data-ttu-id="7c62a-251">Otherwise, on the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-251">Otherwise, on the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Create Recovery Services Vault step 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="7c62a-253">The list of recovery services vaults appears.</span><span class="sxs-lookup"><span data-stu-id="7c62a-253">The list of recovery services vaults appears.</span></span>

    ![View of the Recovery Services vaults list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    <span data-ttu-id="7c62a-255">From the list of recovery services vaults, select a vault to open its dashboard.</span><span class="sxs-lookup"><span data-stu-id="7c62a-255">From the list of recovery services vaults, select a vault to open its dashboard.</span></span>

     ![Open vault blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. <span data-ttu-id="7c62a-257">On the vault dashboard menu, click **Backup** to open the Backup blade.</span><span class="sxs-lookup"><span data-stu-id="7c62a-257">On the vault dashboard menu, click **Backup** to open the Backup blade.</span></span>

    ![Open Backup blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-vms-prepare/backup-button.png)

    <span data-ttu-id="7c62a-259">The Backup and Backup Goal blades open.</span><span class="sxs-lookup"><span data-stu-id="7c62a-259">The Backup and Backup Goal blades open.</span></span>

    ![Open Scenario blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. <span data-ttu-id="7c62a-261">On the Backup Goal blade, from the **Where is your workload running** drop-down menu, choose Azure.</span><span class="sxs-lookup"><span data-stu-id="7c62a-261">On the Backup Goal blade, from the **Where is your workload running** drop-down menu, choose Azure.</span></span> <span data-ttu-id="7c62a-262">From the **What do you want to backup** drop-down, choose Virtual machine, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-262">From the **What do you want to backup** drop-down, choose Virtual machine, then click **OK**.</span></span>

    <span data-ttu-id="7c62a-263">These actions register the VM extension with the vault.</span><span class="sxs-lookup"><span data-stu-id="7c62a-263">These actions register the VM extension with the vault.</span></span> <span data-ttu-id="7c62a-264">The Backup Goal blade closes and the **Backup policy** blade opens.</span><span class="sxs-lookup"><span data-stu-id="7c62a-264">The Backup Goal blade closes and the **Backup policy** blade opens.</span></span>

    ![Open Scenario blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. <span data-ttu-id="7c62a-266">On the Backup policy blade, select the backup policy you want to apply to the vault.</span><span class="sxs-lookup"><span data-stu-id="7c62a-266">On the Backup policy blade, select the backup policy you want to apply to the vault.</span></span>

    ![Select backup policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    <span data-ttu-id="7c62a-268">The details of the default policy are listed under the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="7c62a-268">The details of the default policy are listed under the drop-down menu.</span></span> <span data-ttu-id="7c62a-269">If you want to create a policy, select **Create New** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="7c62a-269">If you want to create a policy, select **Create New** from the drop-down menu.</span></span> <span data-ttu-id="7c62a-270">For instructions on defining a backup policy, see [Defining a backup policy](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="7c62a-270">For instructions on defining a backup policy, see [Defining a backup policy](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).</span></span>
    <span data-ttu-id="7c62a-271">Click **OK** to associate the backup policy with the vault.</span><span class="sxs-lookup"><span data-stu-id="7c62a-271">Click **OK** to associate the backup policy with the vault.</span></span>

    <span data-ttu-id="7c62a-272">The Backup policy blade closes and the **Select virtual machines** blade opens.</span><span class="sxs-lookup"><span data-stu-id="7c62a-272">The Backup policy blade closes and the **Select virtual machines** blade opens.</span></span>
5. <span data-ttu-id="7c62a-273">In the **Select virtual machines** blade, choose the virtual machines to associate with the specified policy and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-273">In the **Select virtual machines** blade, choose the virtual machines to associate with the specified policy and click **OK**.</span></span>

    ![Select workload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    <span data-ttu-id="7c62a-275">The selected virtual machine is validated.</span><span class="sxs-lookup"><span data-stu-id="7c62a-275">The selected virtual machine is validated.</span></span> <span data-ttu-id="7c62a-276">If you do not see the virtual machines that you expected to see, check that they exist in the same Azure location as the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="7c62a-276">If you do not see the virtual machines that you expected to see, check that they exist in the same Azure location as the Recovery Services vault.</span></span> <span data-ttu-id="7c62a-277">The location of the Recovery Services vault is shown on the vault dashboard.</span><span class="sxs-lookup"><span data-stu-id="7c62a-277">The location of the Recovery Services vault is shown on the vault dashboard.</span></span>

6. <span data-ttu-id="7c62a-278">Now that you have defined all settings for the vault, in the Backup blade, click **Enable Backup** to deploy the policy to the vault and the VMs.</span><span class="sxs-lookup"><span data-stu-id="7c62a-278">Now that you have defined all settings for the vault, in the Backup blade, click **Enable Backup** to deploy the policy to the vault and the VMs.</span></span> <span data-ttu-id="7c62a-279">Deploying the backup policy does not create the initial recovery point for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7c62a-279">Deploying the backup policy does not create the initial recovery point for the virtual machine.</span></span>

    ![Enable Backup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

<span data-ttu-id="7c62a-281">After successfully enabling the backup, your backup policy will execute on schedule.</span><span class="sxs-lookup"><span data-stu-id="7c62a-281">After successfully enabling the backup, your backup policy will execute on schedule.</span></span> <span data-ttu-id="7c62a-282">However, proceed to initiate the first backup job.</span><span class="sxs-lookup"><span data-stu-id="7c62a-282">However, proceed to initiate the first backup job.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="7c62a-283">Initial backup</span><span class="sxs-lookup"><span data-stu-id="7c62a-283">Initial backup</span></span>
<span data-ttu-id="7c62a-284">Once a backup policy has been deployed on the virtual machine, that does not mean the data has been backed up.</span><span class="sxs-lookup"><span data-stu-id="7c62a-284">Once a backup policy has been deployed on the virtual machine, that does not mean the data has been backed up.</span></span> <span data-ttu-id="7c62a-285">By default, the first scheduled backup (as defined in the backup policy) is the initial backup.</span><span class="sxs-lookup"><span data-stu-id="7c62a-285">By default, the first scheduled backup (as defined in the backup policy) is the initial backup.</span></span> <span data-ttu-id="7c62a-286">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-286">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Backup pending](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="7c62a-288">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-288">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span></span>

<span data-ttu-id="7c62a-289">To run the initial backup job:</span><span class="sxs-lookup"><span data-stu-id="7c62a-289">To run the initial backup job:</span></span>

1. <span data-ttu-id="7c62a-290">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span><span class="sxs-lookup"><span data-stu-id="7c62a-290">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span></span> <br/>
  <span data-ttu-id="7c62a-291">![Settings icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="7c62a-291">![Settings icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="7c62a-292">The **Backup Items** blade opens.</span><span class="sxs-lookup"><span data-stu-id="7c62a-292">The **Backup Items** blade opens.</span></span>

  ![Back up items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="7c62a-294">On the **Backup Items** blade, select the item.</span><span class="sxs-lookup"><span data-stu-id="7c62a-294">On the **Backup Items** blade, select the item.</span></span>

  ![Settings icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="7c62a-296">The **Backup Items** list opens.</span><span class="sxs-lookup"><span data-stu-id="7c62a-296">The **Backup Items** list opens.</span></span> <br/>

  ![Backup job triggered](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="7c62a-298">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span><span class="sxs-lookup"><span data-stu-id="7c62a-298">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

  ![Context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="7c62a-300">The Context menu appears.</span><span class="sxs-lookup"><span data-stu-id="7c62a-300">The Context menu appears.</span></span>

  ![Context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="7c62a-302">On the Context menu, click **Backup now**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-302">On the Context menu, click **Backup now**.</span></span>

  ![Context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="7c62a-304">The Backup Now blade opens.</span><span class="sxs-lookup"><span data-stu-id="7c62a-304">The Backup Now blade opens.</span></span>

  ![shows the Backup Now blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="7c62a-306">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-306">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![set the last day the Backup Now recovery point is retained](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="7c62a-308">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span><span class="sxs-lookup"><span data-stu-id="7c62a-308">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="7c62a-309">Depending on the size of your VM, creating the initial backup may take a while.</span><span class="sxs-lookup"><span data-stu-id="7c62a-309">Depending on the size of your VM, creating the initial backup may take a while.</span></span>

6. <span data-ttu-id="7c62a-310">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span><span class="sxs-lookup"><span data-stu-id="7c62a-310">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span></span>

  ![Backup Jobs tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="7c62a-312">The Backup Jobs blade opens.</span><span class="sxs-lookup"><span data-stu-id="7c62a-312">The Backup Jobs blade opens.</span></span>

  ![Backup Jobs tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="7c62a-314">In the **Backup jobs** blade, you can see the status of all jobs.</span><span class="sxs-lookup"><span data-stu-id="7c62a-314">In the **Backup jobs** blade, you can see the status of all jobs.</span></span> <span data-ttu-id="7c62a-315">Check if the backup job for your VM is still in progress, or if it has finished.</span><span class="sxs-lookup"><span data-stu-id="7c62a-315">Check if the backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="7c62a-316">When a backup job is finished, the status is *Completed*.</span><span class="sxs-lookup"><span data-stu-id="7c62a-316">When a backup job is finished, the status is *Completed*.</span></span>

  > [!NOTE]
  > As a part of the backup operation, the Azure Backup service issues a command to the backup extension in each VM to flush all writes and take a consistent snapshot.
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-the-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="7c62a-318">Install the VM Agent on the virtual machine</span><span class="sxs-lookup"><span data-stu-id="7c62a-318">Install the VM Agent on the virtual machine</span></span>
<span data-ttu-id="7c62a-319">This information is provided in case it is needed.</span><span class="sxs-lookup"><span data-stu-id="7c62a-319">This information is provided in case it is needed.</span></span> <span data-ttu-id="7c62a-320">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span><span class="sxs-lookup"><span data-stu-id="7c62a-320">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span></span> <span data-ttu-id="7c62a-321">However, if your VM was created from the Azure gallery, then the VM Agent is already present on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7c62a-321">However, if your VM was created from the Azure gallery, then the VM Agent is already present on the virtual machine.</span></span> <span data-ttu-id="7c62a-322">VMs that are migrated from on-premises datacenters would not have the VM Agent installed.</span><span class="sxs-lookup"><span data-stu-id="7c62a-322">VMs that are migrated from on-premises datacenters would not have the VM Agent installed.</span></span> <span data-ttu-id="7c62a-323">In such a case, the VM Agent needs to be installed.</span><span class="sxs-lookup"><span data-stu-id="7c62a-323">In such a case, the VM Agent needs to be installed.</span></span> <span data-ttu-id="7c62a-324">If you have problems backing up the Azure VM, check that the Azure VM Agent is correctly installed on the virtual machine (see the following table).</span><span class="sxs-lookup"><span data-stu-id="7c62a-324">If you have problems backing up the Azure VM, check that the Azure VM Agent is correctly installed on the virtual machine (see the following table).</span></span> <span data-ttu-id="7c62a-325">If you create a custom VM, [ensure the **Install the VM Agent** check box is selected](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) before the virtual machine is provisioned.</span><span class="sxs-lookup"><span data-stu-id="7c62a-325">If you create a custom VM, [ensure the **Install the VM Agent** check box is selected](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) before the virtual machine is provisioned.</span></span>

<span data-ttu-id="7c62a-326">Learn about the [VM Agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) and [how to install it](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7c62a-326">Learn about the [VM Agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) and [how to install it](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="7c62a-327">The following table provides additional information about the VM Agent for Windows and Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="7c62a-327">The following table provides additional information about the VM Agent for Windows and Linux VMs.</span></span>

| <span data-ttu-id="7c62a-328">**Operation**</span><span class="sxs-lookup"><span data-stu-id="7c62a-328">**Operation**</span></span> | <span data-ttu-id="7c62a-329">**Windows**</span><span class="sxs-lookup"><span data-stu-id="7c62a-329">**Windows**</span></span> | <span data-ttu-id="7c62a-330">**Linux**</span><span class="sxs-lookup"><span data-stu-id="7c62a-330">**Linux**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7c62a-331">Installing the VM Agent</span><span class="sxs-lookup"><span data-stu-id="7c62a-331">Installing the VM Agent</span></span> |<li><span data-ttu-id="7c62a-332">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="7c62a-332">Download and install the [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="7c62a-333">You need Administrator privileges to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="7c62a-333">You need Administrator privileges to complete the installation.</span></span> <li><span data-ttu-id="7c62a-334">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span><span class="sxs-lookup"><span data-stu-id="7c62a-334">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span></span> |<li> <span data-ttu-id="7c62a-335">Install the latest [Linux agent](https://github.com/Azure/WALinuxAgent) from GitHub.</span><span class="sxs-lookup"><span data-stu-id="7c62a-335">Install the latest [Linux agent](https://github.com/Azure/WALinuxAgent) from GitHub.</span></span> <span data-ttu-id="7c62a-336">You need Administrator privileges to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="7c62a-336">You need Administrator privileges to complete the installation.</span></span> <li> <span data-ttu-id="7c62a-337">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span><span class="sxs-lookup"><span data-stu-id="7c62a-337">[Update the VM property](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) to indicate that the agent is installed.</span></span> |
| <span data-ttu-id="7c62a-338">Updating the VM Agent</span><span class="sxs-lookup"><span data-stu-id="7c62a-338">Updating the VM Agent</span></span> |<span data-ttu-id="7c62a-339">Updating the VM Agent is as simple as reinstalling the [VM Agent binaries](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="7c62a-339">Updating the VM Agent is as simple as reinstalling the [VM Agent binaries](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <br><span data-ttu-id="7c62a-340">Ensure that no backup operation is running while the VM agent is being updated.</span><span class="sxs-lookup"><span data-stu-id="7c62a-340">Ensure that no backup operation is running while the VM agent is being updated.</span></span> |<span data-ttu-id="7c62a-341">Follow the instructions on [updating the Linux VM Agent](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7c62a-341">Follow the instructions on [updating the Linux VM Agent](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <br><span data-ttu-id="7c62a-342">Ensure that no backup operation is running while the VM Agent is being updated.</span><span class="sxs-lookup"><span data-stu-id="7c62a-342">Ensure that no backup operation is running while the VM Agent is being updated.</span></span> |
| <span data-ttu-id="7c62a-343">Validating the VM Agent installation</span><span class="sxs-lookup"><span data-stu-id="7c62a-343">Validating the VM Agent installation</span></span> |<li><span data-ttu-id="7c62a-344">Navigate to the *C:\WindowsAzure\Packages* folder in the Azure VM.</span><span class="sxs-lookup"><span data-stu-id="7c62a-344">Navigate to the *C:\WindowsAzure\Packages* folder in the Azure VM.</span></span> <li><span data-ttu-id="7c62a-345">You should find the WaAppAgent.exe file present.</span><span class="sxs-lookup"><span data-stu-id="7c62a-345">You should find the WaAppAgent.exe file present.</span></span><li> <span data-ttu-id="7c62a-346">Right-click the file, go to **Properties**, and then select the **Details** tab. The Product Version field should be 2.6.1198.718 or higher.</span><span class="sxs-lookup"><span data-stu-id="7c62a-346">Right-click the file, go to **Properties**, and then select the **Details** tab. The Product Version field should be 2.6.1198.718 or higher.</span></span> |<span data-ttu-id="7c62a-347">N/A</span><span class="sxs-lookup"><span data-stu-id="7c62a-347">N/A</span></span> |

### <a name="backup-extension"></a><span data-ttu-id="7c62a-348">Backup extension</span><span class="sxs-lookup"><span data-stu-id="7c62a-348">Backup extension</span></span>
<span data-ttu-id="7c62a-349">Once the VM Agent is installed on the virtual machine, the Azure Backup service installs the backup extension to the VM Agent.</span><span class="sxs-lookup"><span data-stu-id="7c62a-349">Once the VM Agent is installed on the virtual machine, the Azure Backup service installs the backup extension to the VM Agent.</span></span> <span data-ttu-id="7c62a-350">The Azure Backup service seamlessly upgrades and patches the backup extension without additional user intervention.</span><span class="sxs-lookup"><span data-stu-id="7c62a-350">The Azure Backup service seamlessly upgrades and patches the backup extension without additional user intervention.</span></span>

<span data-ttu-id="7c62a-351">The Backup service installs the backup extension, even if the VM is not running.</span><span class="sxs-lookup"><span data-stu-id="7c62a-351">The Backup service installs the backup extension, even if the VM is not running.</span></span> <span data-ttu-id="7c62a-352">A running VM provides the greatest chance of getting an application-consistent recovery point.</span><span class="sxs-lookup"><span data-stu-id="7c62a-352">A running VM provides the greatest chance of getting an application-consistent recovery point.</span></span> <span data-ttu-id="7c62a-353">However, the Azure Backup service continues to back up the VM even if it is turned off, and the extension could not be installed.</span><span class="sxs-lookup"><span data-stu-id="7c62a-353">However, the Azure Backup service continues to back up the VM even if it is turned off, and the extension could not be installed.</span></span> <span data-ttu-id="7c62a-354">This type of backup is known as Offline VM, and the recovery point is *crash consistent*.</span><span class="sxs-lookup"><span data-stu-id="7c62a-354">This type of backup is known as Offline VM, and the recovery point is *crash consistent*.</span></span>

## <a name="troubleshooting-information"></a><span data-ttu-id="7c62a-355">Troubleshooting information</span><span class="sxs-lookup"><span data-stu-id="7c62a-355">Troubleshooting information</span></span>
<span data-ttu-id="7c62a-356">If you have issues accomplishing some of the tasks in this article, consult the [Troubleshooting guidance](backup-azure-vms-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="7c62a-356">If you have issues accomplishing some of the tasks in this article, consult the [Troubleshooting guidance](backup-azure-vms-troubleshoot.md).</span></span>

## <a name="pricing"></a><span data-ttu-id="7c62a-357">Pricing</span><span class="sxs-lookup"><span data-stu-id="7c62a-357">Pricing</span></span>
<span data-ttu-id="7c62a-358">The cost of backing up Azure VMs is based on the number of protected instances.</span><span class="sxs-lookup"><span data-stu-id="7c62a-358">The cost of backing up Azure VMs is based on the number of protected instances.</span></span> <span data-ttu-id="7c62a-359">For a definition of a protected instance, see [What is a protected instance](backup-introduction-to-azure-backup.md#what-is-a-protected-instance).</span><span class="sxs-lookup"><span data-stu-id="7c62a-359">For a definition of a protected instance, see [What is a protected instance](backup-introduction-to-azure-backup.md#what-is-a-protected-instance).</span></span> <span data-ttu-id="7c62a-360">For an example of calculating the cost of backing up a virtual machine, see [How are protected instances calculated](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances).</span><span class="sxs-lookup"><span data-stu-id="7c62a-360">For an example of calculating the cost of backing up a virtual machine, see [How are protected instances calculated](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances).</span></span> <span data-ttu-id="7c62a-361">See the Azure Backup Pricing page for information about [Backup Pricing](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="7c62a-361">See the Azure Backup Pricing page for information about [Backup Pricing](https://azure.microsoft.com/pricing/details/backup/).</span></span>

## <a name="questions"></a><span data-ttu-id="7c62a-362">Questions?</span><span class="sxs-lookup"><span data-stu-id="7c62a-362">Questions?</span></span>
<span data-ttu-id="7c62a-363">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="7c62a-363">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>












































