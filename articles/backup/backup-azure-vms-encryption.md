---
title: Back up and restore encrypted VMs by using Azure Backup
description: This article talks about the backup and restore experience for VMs encrypted by using Azure Disk Encryption.
services: backup
author: sogup
manager: vijayts
ms.service: backup
ms.topic: conceptual
ms.date: 7/10/2018
ms.author: sogup
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b2f22500a4e557cb89bac7ed114d8c76ca8d9f9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44781045"
---
# <a name="back-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a><span data-ttu-id="2ca23-103">Back up and restore encrypted virtual machines with Azure Backup</span><span class="sxs-lookup"><span data-stu-id="2ca23-103">Back up and restore encrypted virtual machines with Azure Backup</span></span>
<span data-ttu-id="2ca23-104">This article talks about the steps to back up and restore virtual machines (VMs) by using Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="2ca23-104">This article talks about the steps to back up and restore virtual machines (VMs) by using Azure Backup.</span></span> <span data-ttu-id="2ca23-105">It also provides details about supported scenarios, prerequisites, and troubleshooting steps for error cases.</span><span class="sxs-lookup"><span data-stu-id="2ca23-105">It also provides details about supported scenarios, prerequisites, and troubleshooting steps for error cases.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="2ca23-106">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="2ca23-106">Supported scenarios</span></span>

 <span data-ttu-id="2ca23-107">Backup and restore of encrypted VMs is supported only for VMs that use the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="2ca23-107">Backup and restore of encrypted VMs is supported only for VMs that use the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="2ca23-108">It's not supported for VMs that use the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="2ca23-108">It's not supported for VMs that use the classic deployment model.</span></span> <span data-ttu-id="2ca23-109">Backup and restore of encrypted VMs is supported for Windows and Linux VMs that use Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="2ca23-109">Backup and restore of encrypted VMs is supported for Windows and Linux VMs that use Azure Disk Encryption.</span></span> <span data-ttu-id="2ca23-110">Disk Encryption uses the industry standard BitLocker feature of Windows and the dm-crypt feature of Linux to provide encryption of disks.</span><span class="sxs-lookup"><span data-stu-id="2ca23-110">Disk Encryption uses the industry standard BitLocker feature of Windows and the dm-crypt feature of Linux to provide encryption of disks.</span></span> <span data-ttu-id="2ca23-111">The following table shows encryption type and support for VMs.</span><span class="sxs-lookup"><span data-stu-id="2ca23-111">The following table shows encryption type and support for VMs.</span></span>

   |  | <span data-ttu-id="2ca23-112">BEK + KEK VMs</span><span class="sxs-lookup"><span data-stu-id="2ca23-112">BEK + KEK VMs</span></span> | <span data-ttu-id="2ca23-113">BEK-only VMs</span><span class="sxs-lookup"><span data-stu-id="2ca23-113">BEK-only VMs</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="2ca23-114">**Nonmanaged VMs**</span><span class="sxs-lookup"><span data-stu-id="2ca23-114">**Nonmanaged VMs**</span></span>  | <span data-ttu-id="2ca23-115">Yes</span><span class="sxs-lookup"><span data-stu-id="2ca23-115">Yes</span></span> | <span data-ttu-id="2ca23-116">Yes</span><span class="sxs-lookup"><span data-stu-id="2ca23-116">Yes</span></span>  |
   | <span data-ttu-id="2ca23-117">**Managed VMs**</span><span class="sxs-lookup"><span data-stu-id="2ca23-117">**Managed VMs**</span></span>  | <span data-ttu-id="2ca23-118">Yes</span><span class="sxs-lookup"><span data-stu-id="2ca23-118">Yes</span></span> | <span data-ttu-id="2ca23-119">Yes</span><span class="sxs-lookup"><span data-stu-id="2ca23-119">Yes</span></span>  |

## <a name="prerequisites"></a><span data-ttu-id="2ca23-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2ca23-120">Prerequisites</span></span>
* <span data-ttu-id="2ca23-121">The VM was encrypted by using [Azure Disk Encryption](../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="2ca23-121">The VM was encrypted by using [Azure Disk Encryption](../security/azure-security-disk-encryption.md).</span></span>

* <span data-ttu-id="2ca23-122">A Recovery Services vault was created and storage replication was set by following the steps in [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span><span class="sxs-lookup"><span data-stu-id="2ca23-122">A Recovery Services vault was created and storage replication was set by following the steps in [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span></span>

* <span data-ttu-id="2ca23-123">Backup was given [permissions to access a key vault](#provide-permissions-to-backup) containing keys and secrets for encrypted VMs.</span><span class="sxs-lookup"><span data-stu-id="2ca23-123">Backup was given [permissions to access a key vault](#provide-permissions-to-backup) containing keys and secrets for encrypted VMs.</span></span>

## <a name="backup-encrypted-vm"></a><span data-ttu-id="2ca23-124">Backup-encrypted VM</span><span class="sxs-lookup"><span data-stu-id="2ca23-124">Backup-encrypted VM</span></span>
<span data-ttu-id="2ca23-125">Use the following steps to set a backup goal, define a policy, configure items, and trigger a backup.</span><span class="sxs-lookup"><span data-stu-id="2ca23-125">Use the following steps to set a backup goal, define a policy, configure items, and trigger a backup.</span></span>

### <a name="configure-backup"></a><span data-ttu-id="2ca23-126">Configure backup</span><span class="sxs-lookup"><span data-stu-id="2ca23-126">Configure backup</span></span>
1. <span data-ttu-id="2ca23-127">If you already have a Recovery Services vault open, proceed to the next step.</span><span class="sxs-lookup"><span data-stu-id="2ca23-127">If you already have a Recovery Services vault open, proceed to the next step.</span></span> <span data-ttu-id="2ca23-128">If you don't have a Recovery Services vault open but you're in the Azure portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-128">If you don't have a Recovery Services vault open but you're in the Azure portal, select **All services**.</span></span>

   <span data-ttu-id="2ca23-129">a.</span><span class="sxs-lookup"><span data-stu-id="2ca23-129">a.</span></span> <span data-ttu-id="2ca23-130">In the list of resources, type **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-130">In the list of resources, type **Recovery Services**.</span></span>

   <span data-ttu-id="2ca23-131">b.</span><span class="sxs-lookup"><span data-stu-id="2ca23-131">b.</span></span> <span data-ttu-id="2ca23-132">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="2ca23-132">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="2ca23-133">When you see **Recovery Services vaults**, select it.</span><span class="sxs-lookup"><span data-stu-id="2ca23-133">When you see **Recovery Services vaults**, select it.</span></span>

      ![Recovery Services vault](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="2ca23-135">c.</span><span class="sxs-lookup"><span data-stu-id="2ca23-135">c.</span></span> <span data-ttu-id="2ca23-136">The list of Recovery Services vaults appears.</span><span class="sxs-lookup"><span data-stu-id="2ca23-136">The list of Recovery Services vaults appears.</span></span> <span data-ttu-id="2ca23-137">Select a vault from the list.</span><span class="sxs-lookup"><span data-stu-id="2ca23-137">Select a vault from the list.</span></span>

     <span data-ttu-id="2ca23-138">The selected vault dashboard opens.</span><span class="sxs-lookup"><span data-stu-id="2ca23-138">The selected vault dashboard opens.</span></span>
1. <span data-ttu-id="2ca23-139">From the list of items that appears under the vault, select **Backup** to start backing up the encrypted VM.</span><span class="sxs-lookup"><span data-stu-id="2ca23-139">From the list of items that appears under the vault, select **Backup** to start backing up the encrypted VM.</span></span>

      ![Backup blade](./media/backup-azure-vms-encryption/select-backup.png)
1. <span data-ttu-id="2ca23-141">On the **Backup** tile, select **Backup goal**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-141">On the **Backup** tile, select **Backup goal**.</span></span>

      ![Scenario blade](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
1. <span data-ttu-id="2ca23-143">Under **Where is your workload running?**, select **Azure**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-143">Under **Where is your workload running?**, select **Azure**.</span></span> <span data-ttu-id="2ca23-144">Under **What do you want to backup?**, select **Virtual machine**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-144">Under **What do you want to backup?**, select **Virtual machine**.</span></span> <span data-ttu-id="2ca23-145">Then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-145">Then select **OK**.</span></span>

   ![Open Scenario blade](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
1. <span data-ttu-id="2ca23-147">Under **Choose backup policy**, select the backup policy you want to apply to the vault.</span><span class="sxs-lookup"><span data-stu-id="2ca23-147">Under **Choose backup policy**, select the backup policy you want to apply to the vault.</span></span> <span data-ttu-id="2ca23-148">Then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-148">Then select **OK**.</span></span>

      ![Select backup policy](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    <span data-ttu-id="2ca23-150">The details of the default policy are listed.</span><span class="sxs-lookup"><span data-stu-id="2ca23-150">The details of the default policy are listed.</span></span> <span data-ttu-id="2ca23-151">If you want to create a policy, select **Create New** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="2ca23-151">If you want to create a policy, select **Create New** from the drop-down list.</span></span> <span data-ttu-id="2ca23-152">After you select **OK**, the backup policy is associated with the vault.</span><span class="sxs-lookup"><span data-stu-id="2ca23-152">After you select **OK**, the backup policy is associated with the vault.</span></span>

1. <span data-ttu-id="2ca23-153">Choose the encrypted VMs to associate with the specified policy, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-153">Choose the encrypted VMs to associate with the specified policy, and select **OK**.</span></span>

      ![Select encrypted VMs](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
1. <span data-ttu-id="2ca23-155">This page shows a message about key vaults associated to the encrypted VMs you selected.</span><span class="sxs-lookup"><span data-stu-id="2ca23-155">This page shows a message about key vaults associated to the encrypted VMs you selected.</span></span> <span data-ttu-id="2ca23-156">Backup requires read-only access to the keys and secrets in the key vault.</span><span class="sxs-lookup"><span data-stu-id="2ca23-156">Backup requires read-only access to the keys and secrets in the key vault.</span></span> <span data-ttu-id="2ca23-157">It uses these permissions to back up the keys and secrets, along with the associated VMs.</span><span class="sxs-lookup"><span data-stu-id="2ca23-157">It uses these permissions to back up the keys and secrets, along with the associated VMs.</span></span><br>
<span data-ttu-id="2ca23-158">If you are a **Member user**, Enable Backup process will seamlessly acquire access to the key vault to backup encrypted VMs without requiring any user intervention.</span><span class="sxs-lookup"><span data-stu-id="2ca23-158">If you are a **Member user**, Enable Backup process will seamlessly acquire access to the key vault to backup encrypted VMs without requiring any user intervention.</span></span>

   ![Encrypted VMs message](./media/backup-azure-vms-encryption/member-user-encrypted-vm-warning-message.png)

   <span data-ttu-id="2ca23-160">For a **Guest user**, you must provide permissions to the backup service to access the key vault for backups to work.</span><span class="sxs-lookup"><span data-stu-id="2ca23-160">For a **Guest user**, you must provide permissions to the backup service to access the key vault for backups to work.</span></span> <span data-ttu-id="2ca23-161">You can      provide these permissions by following the [steps mentioned in the following section](#provide-permissions-to-backup)</span><span class="sxs-lookup"><span data-stu-id="2ca23-161">You can      provide these permissions by following the [steps mentioned in the following section](#provide-permissions-to-backup)</span></span>

   ![Encrypted VMs message](./media/backup-azure-vms-encryption/guest-user-encrypted-vm-warning-message.png)
 
    <span data-ttu-id="2ca23-163">Now that you have defined all settings for the vault, select **Enable Backup** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="2ca23-163">Now that you have defined all settings for the vault, select **Enable Backup** at the bottom of the page.</span></span> <span data-ttu-id="2ca23-164">**Enable Backup** deploys     the policy to the vault and the VMs.</span><span class="sxs-lookup"><span data-stu-id="2ca23-164">**Enable Backup** deploys     the policy to the vault and the VMs.</span></span>
  
1. <span data-ttu-id="2ca23-165">The next phase in preparation is installing the VM Agent or making sure the VM Agent is installed.</span><span class="sxs-lookup"><span data-stu-id="2ca23-165">The next phase in preparation is installing the VM Agent or making sure the VM Agent is installed.</span></span> <span data-ttu-id="2ca23-166">To do the same, follow the steps in [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span><span class="sxs-lookup"><span data-stu-id="2ca23-166">To do the same, follow the steps in [Prepare your environment for backup](backup-azure-arm-vms-prepare.md).</span></span>

### <a name="trigger-a-backup-job"></a><span data-ttu-id="2ca23-167">Trigger a backup job</span><span class="sxs-lookup"><span data-stu-id="2ca23-167">Trigger a backup job</span></span>
<span data-ttu-id="2ca23-168">Follow the steps in [Backup Azure VMs to a Recovery Services vault](backup-azure-arm-vms.md) to trigger a backup job.</span><span class="sxs-lookup"><span data-stu-id="2ca23-168">Follow the steps in [Backup Azure VMs to a Recovery Services vault](backup-azure-arm-vms.md) to trigger a backup job.</span></span>

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a><span data-ttu-id="2ca23-169">Continue backups of already backed-up VMs with encryption enabled</span><span class="sxs-lookup"><span data-stu-id="2ca23-169">Continue backups of already backed-up VMs with encryption enabled</span></span>  
<span data-ttu-id="2ca23-170">If you have VMs already being backed up in a Recovery Services vault that are enabled for encryption later, you must give permissions to Backup to access the key vault for backups to continue.</span><span class="sxs-lookup"><span data-stu-id="2ca23-170">If you have VMs already being backed up in a Recovery Services vault that are enabled for encryption later, you must give permissions to Backup to access the key vault for backups to continue.</span></span> <span data-ttu-id="2ca23-171">You can provide these permissions by following the [steps in the following section](#provide-permissions-to-azure-backup).</span><span class="sxs-lookup"><span data-stu-id="2ca23-171">You can provide these permissions by following the [steps in the following section](#provide-permissions-to-azure-backup).</span></span> <span data-ttu-id="2ca23-172">Or you can follow the PowerShell steps in the "Enable backup" section of the [PowerShell documentation](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="2ca23-172">Or you can follow the PowerShell steps in the "Enable backup" section of the [PowerShell documentation](backup-azure-vms-automation.md).</span></span> 

## <a name="provide-permissions-to-backup"></a><span data-ttu-id="2ca23-173">Provide permissions to Backup</span><span class="sxs-lookup"><span data-stu-id="2ca23-173">Provide permissions to Backup</span></span>
<span data-ttu-id="2ca23-174">Use the following steps to provide relevant permissions to Backup to access the key vault and perform backup of encrypted VMs.</span><span class="sxs-lookup"><span data-stu-id="2ca23-174">Use the following steps to provide relevant permissions to Backup to access the key vault and perform backup of encrypted VMs.</span></span>
1. <span data-ttu-id="2ca23-175">Select **All services**, and search for **Key vaults**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-175">Select **All services**, and search for **Key vaults**.</span></span>

    ![Key vaults](./media/backup-azure-vms-encryption/search-key-vault.png)
    
1. <span data-ttu-id="2ca23-177">From the list of key vaults, select the key vault associated with the encrypted VM that needs to be backed up.</span><span class="sxs-lookup"><span data-stu-id="2ca23-177">From the list of key vaults, select the key vault associated with the encrypted VM that needs to be backed up.</span></span>

     ![Key vault selection](./media/backup-azure-vms-encryption/select-key-vault.png)
     
1. <span data-ttu-id="2ca23-179">Select **Access policies**, and then select **Add new**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-179">Select **Access policies**, and then select **Add new**.</span></span>

    ![Add new](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
1. <span data-ttu-id="2ca23-181">Select **Select principal**, and then type **Backup Management Service** in the search box.</span><span class="sxs-lookup"><span data-stu-id="2ca23-181">Select **Select principal**, and then type **Backup Management Service** in the search box.</span></span> 

    ![Backup service search](./media/backup-azure-vms-encryption/search-backup-service.png)
    
1. <span data-ttu-id="2ca23-183">Select **Backup Management Service**, and then select **Select**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-183">Select **Backup Management Service**, and then select **Select**.</span></span>

    ![Backup service selection](./media/backup-azure-vms-encryption/select-backup-service.png)
    
1. <span data-ttu-id="2ca23-185">Under **Configure from template (optional)**, select **Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-185">Under **Configure from template (optional)**, select **Azure Backup**.</span></span> <span data-ttu-id="2ca23-186">The required permissions are prefilled for **Key permissions** and **Secret permissions**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-186">The required permissions are prefilled for **Key permissions** and **Secret permissions**.</span></span> <span data-ttu-id="2ca23-187">If your VM is encrypted by using **BEK only**, permissions only for secrets are required, so you must remove the selection for **Key permissions**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-187">If your VM is encrypted by using **BEK only**, permissions only for secrets are required, so you must remove the selection for **Key permissions**.</span></span>

    ![Azure backup selection](./media/backup-azure-vms-encryption/select-backup-template.png)
    
1. <span data-ttu-id="2ca23-189">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-189">Select **OK**.</span></span> <span data-ttu-id="2ca23-190">Notice that **Backup Management Service** gets added in **Access policies**.</span><span class="sxs-lookup"><span data-stu-id="2ca23-190">Notice that **Backup Management Service** gets added in **Access policies**.</span></span> 

    ![Access policies](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
1. <span data-ttu-id="2ca23-192">Select **Save** to give the required permissions to Backup.</span><span class="sxs-lookup"><span data-stu-id="2ca23-192">Select **Save** to give the required permissions to Backup.</span></span>

    ![Backup access policy](./media/backup-azure-vms-encryption/save-access-policy.png)

<span data-ttu-id="2ca23-194">After permissions are successfully provided, you can proceed with enabling backup for encrypted VMs.</span><span class="sxs-lookup"><span data-stu-id="2ca23-194">After permissions are successfully provided, you can proceed with enabling backup for encrypted VMs.</span></span>

## <a name="restore-an-encrypted-vm"></a><span data-ttu-id="2ca23-195">Restore an encrypted VM</span><span class="sxs-lookup"><span data-stu-id="2ca23-195">Restore an encrypted VM</span></span>
<span data-ttu-id="2ca23-196">To restore an encrypted VM, first restore disks by following the steps in the "Restore backed-up disks" section in [Choose a VM restore configuration](backup-azure-arm-restore-vms.md#choose-a-vm-restore-configuration).</span><span class="sxs-lookup"><span data-stu-id="2ca23-196">To restore an encrypted VM, first restore disks by following the steps in the "Restore backed-up disks" section in [Choose a VM restore configuration](backup-azure-arm-restore-vms.md#choose-a-vm-restore-configuration).</span></span> <span data-ttu-id="2ca23-197">After that, you can use one of the following options:</span><span class="sxs-lookup"><span data-stu-id="2ca23-197">After that, you can use one of the following options:</span></span>

* <span data-ttu-id="2ca23-198">Follow the PowerShell steps in [Create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create a full VM from restored disks.</span><span class="sxs-lookup"><span data-stu-id="2ca23-198">Follow the PowerShell steps in [Create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create a full VM from restored disks.</span></span>
* <span data-ttu-id="2ca23-199">Or, [use templates to customize a restored VM](backup-azure-arm-restore-vms.md#use-templates-to-customize-a-restored-vm) to create VMs from restored disks.</span><span class="sxs-lookup"><span data-stu-id="2ca23-199">Or, [use templates to customize a restored VM](backup-azure-arm-restore-vms.md#use-templates-to-customize-a-restored-vm) to create VMs from restored disks.</span></span> <span data-ttu-id="2ca23-200">Templates can be used only for recovery points created after April 26, 2017.</span><span class="sxs-lookup"><span data-stu-id="2ca23-200">Templates can be used only for recovery points created after April 26, 2017.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="2ca23-201">Troubleshooting errors</span><span class="sxs-lookup"><span data-stu-id="2ca23-201">Troubleshooting errors</span></span>
| <span data-ttu-id="2ca23-202">Operation</span><span class="sxs-lookup"><span data-stu-id="2ca23-202">Operation</span></span> | <span data-ttu-id="2ca23-203">Error details</span><span class="sxs-lookup"><span data-stu-id="2ca23-203">Error details</span></span> | <span data-ttu-id="2ca23-204">Resolution</span><span class="sxs-lookup"><span data-stu-id="2ca23-204">Resolution</span></span> |
| --- | --- | --- |
|<span data-ttu-id="2ca23-205">Backup</span><span class="sxs-lookup"><span data-stu-id="2ca23-205">Backup</span></span> | <span data-ttu-id="2ca23-206">Backup doesn't have sufficient permissions to the key vault for backup of encrypted VMs.</span><span class="sxs-lookup"><span data-stu-id="2ca23-206">Backup doesn't have sufficient permissions to the key vault for backup of encrypted VMs.</span></span> | <span data-ttu-id="2ca23-207">Backup should be provided these permissions by following the [steps in the previous section](#provide-permissions-to-azure-backup).</span><span class="sxs-lookup"><span data-stu-id="2ca23-207">Backup should be provided these permissions by following the [steps in the previous section](#provide-permissions-to-azure-backup).</span></span> <span data-ttu-id="2ca23-208">Or you can follow the PowerShell steps in the "Enable protection" section of the article, [Use PowerShell to back up and restore virtual machines](backup-azure-vms-automation.md#enable-protection).</span><span class="sxs-lookup"><span data-stu-id="2ca23-208">Or you can follow the PowerShell steps in the "Enable protection" section of the article, [Use PowerShell to back up and restore virtual machines](backup-azure-vms-automation.md#enable-protection).</span></span> |  
| <span data-ttu-id="2ca23-209">Restore</span><span class="sxs-lookup"><span data-stu-id="2ca23-209">Restore</span></span> |<span data-ttu-id="2ca23-210">You can't restore this encrypted VM because the key vault associated with this VM doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="2ca23-210">You can't restore this encrypted VM because the key vault associated with this VM doesn't exist.</span></span> |<span data-ttu-id="2ca23-211">Create a key vault by using [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ca23-211">Create a key vault by using [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span> <span data-ttu-id="2ca23-212">See [Restore a key vault key and a secret by using Azure Backup](backup-azure-restore-key-secret.md) to restore a key and a secret if they aren't present.</span><span class="sxs-lookup"><span data-stu-id="2ca23-212">See [Restore a key vault key and a secret by using Azure Backup](backup-azure-restore-key-secret.md) to restore a key and a secret if they aren't present.</span></span> |
| <span data-ttu-id="2ca23-213">Restore</span><span class="sxs-lookup"><span data-stu-id="2ca23-213">Restore</span></span> |<span data-ttu-id="2ca23-214">You can't restore this encrypted VM because the key and the secret associated with this VM don't exist.</span><span class="sxs-lookup"><span data-stu-id="2ca23-214">You can't restore this encrypted VM because the key and the secret associated with this VM don't exist.</span></span> |<span data-ttu-id="2ca23-215">See [Restore a key vault key and a secret by using Azure Backup](backup-azure-restore-key-secret.md) to restore a key and a secret if they aren't present.</span><span class="sxs-lookup"><span data-stu-id="2ca23-215">See [Restore a key vault key and a secret by using Azure Backup](backup-azure-restore-key-secret.md) to restore a key and a secret if they aren't present.</span></span> |
| <span data-ttu-id="2ca23-216">Restore</span><span class="sxs-lookup"><span data-stu-id="2ca23-216">Restore</span></span> |<span data-ttu-id="2ca23-217">Backup doesn't have the authorization to access resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="2ca23-217">Backup doesn't have the authorization to access resources in your subscription.</span></span> |<span data-ttu-id="2ca23-218">As mentioned previously, restore disks first by following the steps in the "Restore backed-up disks" section in [Choose a VM restore configuration](backup-azure-arm-restore-vms.md#choose-a-vm-restore-configuration).</span><span class="sxs-lookup"><span data-stu-id="2ca23-218">As mentioned previously, restore disks first by following the steps in the "Restore backed-up disks" section in [Choose a VM restore configuration](backup-azure-arm-restore-vms.md#choose-a-vm-restore-configuration).</span></span> <span data-ttu-id="2ca23-219">After that, use PowerShell to [create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks).</span><span class="sxs-lookup"><span data-stu-id="2ca23-219">After that, use PowerShell to [create a VM from restored disks](backup-azure-vms-automation.md#create-a-vm-from-restored-disks).</span></span> |