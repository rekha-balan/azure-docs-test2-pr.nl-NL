---
title: Deploy and manage backups for Resource Manager-deployed VMs using PowerShell | Microsoft Docs
description: Use PowerShell to deploy and manage backups in Azure for Resource Manager-deployed VMs
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3df130a2c8e903c30006d61c71b2e5a6e0919145
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669615"
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="76fb2-103">Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines</span><span class="sxs-lookup"><span data-stu-id="76fb2-103">Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-vms-automation.md)
> * [Classic](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="76fb2-106">This article shows you how to use Azure PowerShell cmdlets to back up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="76fb2-106">This article shows you how to use Azure PowerShell cmdlets to back up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="76fb2-107">A Recovery Services vault is an Azure Resource Manager resource and is used to protect data and assets in both Azure Backup and Azure Site Recovery services.</span><span class="sxs-lookup"><span data-stu-id="76fb2-107">A Recovery Services vault is an Azure Resource Manager resource and is used to protect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="76fb2-108">You can use a Recovery Services vault to protect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span><span class="sxs-lookup"><span data-stu-id="76fb2-108">You can use a Recovery Services vault to protect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). This article is for use with VMs created using the Resource Manager model.
>
>

<span data-ttu-id="76fb2-111">This article walks you through using PowerShell to protect a VM, and restore data from a recovery point.</span><span class="sxs-lookup"><span data-stu-id="76fb2-111">This article walks you through using PowerShell to protect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="76fb2-112">Concepts</span><span class="sxs-lookup"><span data-stu-id="76fb2-112">Concepts</span></span>
<span data-ttu-id="76fb2-113">If you are not familiar with the Azure Backup service, for an overview of the service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="76fb2-113">If you are not familiar with the Azure Backup service, for an overview of the service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="76fb2-114">Before you start, ensure that you cover the essentials about the prerequisites needed to work with Azure Backup, and the limitations of the current VM backup solution.</span><span class="sxs-lookup"><span data-stu-id="76fb2-114">Before you start, ensure that you cover the essentials about the prerequisites needed to work with Azure Backup, and the limitations of the current VM backup solution.</span></span>

<span data-ttu-id="76fb2-115">To use PowerShell effectively, it is necessary to understand the hierarchy of objects and from where to start.</span><span class="sxs-lookup"><span data-stu-id="76fb2-115">To use PowerShell effectively, it is necessary to understand the hierarchy of objects and from where to start.</span></span>

![Recovery Services object hierarchy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="76fb2-117">To view the AzureRmRecoveryServicesBackup PowerShell cmdlet reference, see the [Azure Backup - Recovery Services Cmdlets](https://msdn.microsoft.com/library/mt723320.aspx) in the Azure library.</span><span class="sxs-lookup"><span data-stu-id="76fb2-117">To view the AzureRmRecoveryServicesBackup PowerShell cmdlet reference, see the [Azure Backup - Recovery Services Cmdlets](https://msdn.microsoft.com/library/mt723320.aspx) in the Azure library.</span></span>
<span data-ttu-id="76fb2-118">To view the AzureRmRecoveryServicesVault PowerShell cmdlet reference, see the [Azure Recovery Service Cmdlets](https://msdn.microsoft.com/library/mt643905.aspx).</span><span class="sxs-lookup"><span data-stu-id="76fb2-118">To view the AzureRmRecoveryServicesVault PowerShell cmdlet reference, see the [Azure Recovery Service Cmdlets](https://msdn.microsoft.com/library/mt643905.aspx).</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="76fb2-119">Setup and Registration</span><span class="sxs-lookup"><span data-stu-id="76fb2-119">Setup and Registration</span></span>
<span data-ttu-id="76fb2-120">To begin:</span><span class="sxs-lookup"><span data-stu-id="76fb2-120">To begin:</span></span>

1. <span data-ttu-id="76fb2-121">[Download the latest version of PowerShell](https://github.com/Azure/azure-powershell/releases) (the minimum version required is: 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="76fb2-121">[Download the latest version of PowerShell](https://github.com/Azure/azure-powershell/releases) (the minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="76fb2-122">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span><span class="sxs-lookup"><span data-stu-id="76fb2-122">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


<span data-ttu-id="76fb2-123">The following tasks can be automated with PowerShell:</span><span class="sxs-lookup"><span data-stu-id="76fb2-123">The following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="76fb2-124">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="76fb2-124">Create a Recovery Services vault</span></span>
* <span data-ttu-id="76fb2-125">Backup or protect Azure VMs</span><span class="sxs-lookup"><span data-stu-id="76fb2-125">Backup or protect Azure VMs</span></span>
* <span data-ttu-id="76fb2-126">Trigger a backup job</span><span class="sxs-lookup"><span data-stu-id="76fb2-126">Trigger a backup job</span></span>
* <span data-ttu-id="76fb2-127">Monitor a backup job</span><span class="sxs-lookup"><span data-stu-id="76fb2-127">Monitor a backup job</span></span>
* <span data-ttu-id="76fb2-128">Restore an Azure VM</span><span class="sxs-lookup"><span data-stu-id="76fb2-128">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="76fb2-129">Create a recovery services vault</span><span class="sxs-lookup"><span data-stu-id="76fb2-129">Create a recovery services vault</span></span>
<span data-ttu-id="76fb2-130">The following steps lead you through creating a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="76fb2-130">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="76fb2-131">A Recovery Services vault is different than a Backup vault.</span><span class="sxs-lookup"><span data-stu-id="76fb2-131">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="76fb2-132">If you are using Azure Backup for the first time, you must use the **[Register-AzureRMResourceProvider](https://msdn.microsoft.com/library/mt679020.aspx)** cmdlet to register the Azure Recovery Service provider with your subscription.</span><span class="sxs-lookup"><span data-stu-id="76fb2-132">If you are using Azure Backup for the first time, you must use the **[Register-AzureRMResourceProvider](https://msdn.microsoft.com/library/mt679020.aspx)** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="76fb2-133">The Recovery Services vault is a Resource Manager resource, so you need to place it within a resource group.</span><span class="sxs-lookup"><span data-stu-id="76fb2-133">The Recovery Services vault is a Resource Manager resource, so you need to place it within a resource group.</span></span> <span data-ttu-id="76fb2-134">You can use an existing resource group, or create a resource group with the **[New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt678985.aspx)** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="76fb2-134">You can use an existing resource group, or create a resource group with the **[New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt678985.aspx)** cmdlet.</span></span> <span data-ttu-id="76fb2-135">When creating a resource group, specify the name and location for the resource group.</span><span class="sxs-lookup"><span data-stu-id="76fb2-135">When creating a resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="76fb2-136">Use the **[New-AzureRmRecoveryServicesVault](https://msdn.microsoft.com/library/mt643910.aspx)** cmdlet to create the vault.</span><span class="sxs-lookup"><span data-stu-id="76fb2-136">Use the **[New-AzureRmRecoveryServicesVault](https://msdn.microsoft.com/library/mt643910.aspx)** cmdlet to create the vault.</span></span> <span data-ttu-id="76fb2-137">Be sure to specify the same location for the vault as was used for the resource group.</span><span class="sxs-lookup"><span data-stu-id="76fb2-137">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="76fb2-138">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="76fb2-138">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="76fb2-139">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="76fb2-139">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > Many Azure Backup cmdlets require the Recovery Services vault object as an input. For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.
   >
   >

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="76fb2-142">View the vaults in a subscription</span><span class="sxs-lookup"><span data-stu-id="76fb2-142">View the vaults in a subscription</span></span>
<span data-ttu-id="76fb2-143">Use **[Get-AzureRmRecoveryServicesVault](https://msdn.microsoft.com/library/mt643907.aspx)** to view the list of all vaults in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="76fb2-143">Use **[Get-AzureRmRecoveryServicesVault](https://msdn.microsoft.com/library/mt643907.aspx)** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="76fb2-144">You can use this command to check that a new vault was created, or to see what vaults are available in the subscription.</span><span class="sxs-lookup"><span data-stu-id="76fb2-144">You can use this command to check that a new vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="76fb2-145">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span><span class="sxs-lookup"><span data-stu-id="76fb2-145">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="backup-azure-vms"></a><span data-ttu-id="76fb2-146">Backup Azure VMs</span><span class="sxs-lookup"><span data-stu-id="76fb2-146">Backup Azure VMs</span></span>
<span data-ttu-id="76fb2-147">Now that you have created a recovery services vault, you can use it to protect a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="76fb2-147">Now that you have created a recovery services vault, you can use it to protect a virtual machine.</span></span> <span data-ttu-id="76fb2-148">However before you apply the protection, you must set the vault context and you will want to verify the protection policy.</span><span class="sxs-lookup"><span data-stu-id="76fb2-148">However before you apply the protection, you must set the vault context and you will want to verify the protection policy.</span></span> <span data-ttu-id="76fb2-149">Vault context defines the type of data that is protected in the vault.</span><span class="sxs-lookup"><span data-stu-id="76fb2-149">Vault context defines the type of data that is protected in the vault.</span></span> <span data-ttu-id="76fb2-150">The protection policy is the schedule for when the backup job is run, and how long each backup snapshot is retained.</span><span class="sxs-lookup"><span data-stu-id="76fb2-150">The protection policy is the schedule for when the backup job is run, and how long each backup snapshot is retained.</span></span>

<span data-ttu-id="76fb2-151">Before enabling protection on a VM, you must set the vault context.</span><span class="sxs-lookup"><span data-stu-id="76fb2-151">Before enabling protection on a VM, you must set the vault context.</span></span> <span data-ttu-id="76fb2-152">The context is applied to all subsequent cmdlets.</span><span class="sxs-lookup"><span data-stu-id="76fb2-152">The context is applied to all subsequent cmdlets.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name testvault | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="76fb2-153">Create a protection policy</span><span class="sxs-lookup"><span data-stu-id="76fb2-153">Create a protection policy</span></span>
<span data-ttu-id="76fb2-154">When you create a vault, it comes with a default policy.</span><span class="sxs-lookup"><span data-stu-id="76fb2-154">When you create a vault, it comes with a default policy.</span></span> <span data-ttu-id="76fb2-155">This policy triggers a backup job each day at a specified time.</span><span class="sxs-lookup"><span data-stu-id="76fb2-155">This policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="76fb2-156">Per the default policy, the backup snapshot is retained for 30 days.</span><span class="sxs-lookup"><span data-stu-id="76fb2-156">Per the default policy, the backup snapshot is retained for 30 days.</span></span> <span data-ttu-id="76fb2-157">You can use the default policy to quickly protect your VM and edit the policy later with different details.</span><span class="sxs-lookup"><span data-stu-id="76fb2-157">You can use the default policy to quickly protect your VM and edit the policy later with different details.</span></span>

<span data-ttu-id="76fb2-158">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://msdn.microsoft.com/library/mt723300.aspx)** to view the available list of policies in the vault:</span><span class="sxs-lookup"><span data-stu-id="76fb2-158">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://msdn.microsoft.com/library/mt723300.aspx)** to view the available list of policies in the vault:</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType AzureVM
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> The timezone of the BackupTime field in PowerShell is UTC. However, when the backup time is shown in the Azure portal, the time is adjusted to your local timezone.
>
>

<span data-ttu-id="76fb2-161">A backup protection policy is associated with at least one retention policy.</span><span class="sxs-lookup"><span data-stu-id="76fb2-161">A backup protection policy is associated with at least one retention policy.</span></span>  <span data-ttu-id="76fb2-162">Retention policy defines how long a recovery point is kept with Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="76fb2-162">Retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="76fb2-163">Use **Get-AzureRmRecoveryServicesBackupRetentionPolicyObject** to view the default retention policy.</span><span class="sxs-lookup"><span data-stu-id="76fb2-163">Use **Get-AzureRmRecoveryServicesBackupRetentionPolicyObject** to view the default retention policy.</span></span>  <span data-ttu-id="76fb2-164">Similarly you can use **Get-AzureRmRecoveryServicesBackupSchedulePolicyObject** to obtain the default schedule policy.</span><span class="sxs-lookup"><span data-stu-id="76fb2-164">Similarly you can use **Get-AzureRmRecoveryServicesBackupSchedulePolicyObject** to obtain the default schedule policy.</span></span> <span data-ttu-id="76fb2-165">The schedule and retention policy objects are used as inputs to the **New-AzureRmRecoveryServicesBackupProtectionPolicy** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="76fb2-165">The schedule and retention policy objects are used as inputs to the **New-AzureRmRecoveryServicesBackupProtectionPolicy** cmdlet.</span></span>

<span data-ttu-id="76fb2-166">A backup protection policy defines when and how often the backup of an item is done.</span><span class="sxs-lookup"><span data-stu-id="76fb2-166">A backup protection policy defines when and how often the backup of an item is done.</span></span> <span data-ttu-id="76fb2-167">The New-AzureRmRecoveryServicesBackupProtectionPolicy cmdlet creates a PowerShell object that holds backup policy information.</span><span class="sxs-lookup"><span data-stu-id="76fb2-167">The New-AzureRmRecoveryServicesBackupProtectionPolicy cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="76fb2-168">The backup policy is used as an input to the Enable-AzureRmRecoveryServicesBackupProtection cmdlet.</span><span class="sxs-lookup"><span data-stu-id="76fb2-168">The backup policy is used as an input to the Enable-AzureRmRecoveryServicesBackupProtection cmdlet.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\>  $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\>  New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType AzureVM -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```

### <a name="enable-protection"></a><span data-ttu-id="76fb2-169">Enable protection</span><span class="sxs-lookup"><span data-stu-id="76fb2-169">Enable protection</span></span>
<span data-ttu-id="76fb2-170">Enabling protection involves two objects - the item and the policy.</span><span class="sxs-lookup"><span data-stu-id="76fb2-170">Enabling protection involves two objects - the item and the policy.</span></span> <span data-ttu-id="76fb2-171">Both objects are required to enable protection on the vault.</span><span class="sxs-lookup"><span data-stu-id="76fb2-171">Both objects are required to enable protection on the vault.</span></span> <span data-ttu-id="76fb2-172">Once the policy has been associated with the vault, the backup workflow is triggered at the time defined in the policy schedule.</span><span class="sxs-lookup"><span data-stu-id="76fb2-172">Once the policy has been associated with the vault, the backup workflow is triggered at the time defined in the policy schedule.</span></span>

<span data-ttu-id="76fb2-173">To enable the protection on non-encrypted Resource Manager VMs</span><span class="sxs-lookup"><span data-stu-id="76fb2-173">To enable the protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="76fb2-174">To enable the protection on encrypted VMs[encrypted using BEK and KEK], you need to give permissions for Azure Backup service to read keys and secrets from key vault.</span><span class="sxs-lookup"><span data-stu-id="76fb2-174">To enable the protection on encrypted VMs[encrypted using BEK and KEK], you need to give permissions for Azure Backup service to read keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName 'KeyVaultName' -ResourceGroupName 'RGNameOfKeyVault' -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> If you are on Azure Government cloud, then use the value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for the parameter **-ServicePrincipalName** in Set-AzureRmKeyVaultAccessPolicy cmdlet.
>
>

<span data-ttu-id="76fb2-176">For classic VMs</span><span class="sxs-lookup"><span data-stu-id="76fb2-176">For classic VMs</span></span>

```
PS C:\>  $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\>  Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="76fb2-177">Modify a protection policy</span><span class="sxs-lookup"><span data-stu-id="76fb2-177">Modify a protection policy</span></span>
<span data-ttu-id="76fb2-178">To modify the policy, modify the BackupSchedulePolicyObject or BackupRetentionPolicy object and modify the policy using Set-AzureRmRecoveryServicesBackupProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="76fb2-178">To modify the policy, modify the BackupSchedulePolicyObject or BackupRetentionPolicy object and modify the policy using Set-AzureRmRecoveryServicesBackupProtectionPolicy</span></span>

<span data-ttu-id="76fb2-179">The following example changes the retention count to 365.</span><span class="sxs-lookup"><span data-stu-id="76fb2-179">The following example changes the retention count to 365.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name NewPolicy
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy  $RetPol
```

## <a name="run-an-initial-backup"></a><span data-ttu-id="76fb2-180">Run an initial backup</span><span class="sxs-lookup"><span data-stu-id="76fb2-180">Run an initial backup</span></span>
<span data-ttu-id="76fb2-181">The backup schedule triggers a full backup on the initial backup for the item.</span><span class="sxs-lookup"><span data-stu-id="76fb2-181">The backup schedule triggers a full backup on the initial backup for the item.</span></span> <span data-ttu-id="76fb2-182">On subsequent backups, backup is an incremental copy.</span><span class="sxs-lookup"><span data-stu-id="76fb2-182">On subsequent backups, backup is an incremental copy.</span></span> <span data-ttu-id="76fb2-183">If you want to force the initial backup to happen at a certain time or even immediately, then use the **[Backup-AzureRmRecoveryServicesBackupItem](https://msdn.microsoft.com/library/mt723312.aspx)** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="76fb2-183">If you want to force the initial backup to happen at a certain time or even immediately, then use the **[Backup-AzureRmRecoveryServicesBackupItem](https://msdn.microsoft.com/library/mt723312.aspx)** cmdlet:</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName 'V2VM'
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> The timezone of the StartTime and EndTime fields in PowerShell is UTC. However, when the time is shown in the Azure portal, the time is adjusted to your local timezone.
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="76fb2-186">Monitoring a backup job</span><span class="sxs-lookup"><span data-stu-id="76fb2-186">Monitoring a backup job</span></span>
<span data-ttu-id="76fb2-187">Most long-running operations in Azure Backup are modeled as a job.</span><span class="sxs-lookup"><span data-stu-id="76fb2-187">Most long-running operations in Azure Backup are modeled as a job.</span></span> <span data-ttu-id="76fb2-188">This makes it easy to track progress without having to keep the Azure portal open always.</span><span class="sxs-lookup"><span data-stu-id="76fb2-188">This makes it easy to track progress without having to keep the Azure portal open always.</span></span>

<span data-ttu-id="76fb2-189">To get the latest status of an in-progress job, use the Get-AzureRmRecoveryservicesBackupJob cmdlet.</span><span class="sxs-lookup"><span data-stu-id="76fb2-189">To get the latest status of an in-progress job, use the Get-AzureRmRecoveryservicesBackupJob cmdlet.</span></span>

```
PS C:\ > $joblist = Get-AzureRmRecoveryservicesBackupJob –Status InProgress
PS C:\ > $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="76fb2-190">Instead of polling these jobs for completion - which is unnecessary additional code - use the **[Wait-AzureRmRecoveryServicesBackupJob](https://msdn.microsoft.com/library/mt723321.aspx)** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="76fb2-190">Instead of polling these jobs for completion - which is unnecessary additional code - use the **[Wait-AzureRmRecoveryServicesBackupJob](https://msdn.microsoft.com/library/mt723321.aspx)** cmdlet.</span></span> <span data-ttu-id="76fb2-191">This cmdlet pauses the execution until either the job completes or the specified timeout value is reached.</span><span class="sxs-lookup"><span data-stu-id="76fb2-191">This cmdlet pauses the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="76fb2-192">Restore an Azure VM</span><span class="sxs-lookup"><span data-stu-id="76fb2-192">Restore an Azure VM</span></span>
<span data-ttu-id="76fb2-193">There is a key difference between the restoring a VM using the Azure portal and restoring a VM using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76fb2-193">There is a key difference between the restoring a VM using the Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="76fb2-194">With PowerShell, the restore operation is complete once the disks and configuration information from the recovery point are created.</span><span class="sxs-lookup"><span data-stu-id="76fb2-194">With PowerShell, the restore operation is complete once the disks and configuration information from the recovery point are created.</span></span> <span data-ttu-id="76fb2-195">The restore operation does not create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="76fb2-195">The restore operation does not create a virtual machine.</span></span> <span data-ttu-id="76fb2-196">The instructions for creating the virtual machine from disks are provided.</span><span class="sxs-lookup"><span data-stu-id="76fb2-196">The instructions for creating the virtual machine from disks are provided.</span></span> <span data-ttu-id="76fb2-197">However, to fully restore a VM, you need to work through the following procedures:</span><span class="sxs-lookup"><span data-stu-id="76fb2-197">However, to fully restore a VM, you need to work through the following procedures:</span></span>

* <span data-ttu-id="76fb2-198">Select the VM</span><span class="sxs-lookup"><span data-stu-id="76fb2-198">Select the VM</span></span>
* <span data-ttu-id="76fb2-199">Choose a recovery point</span><span class="sxs-lookup"><span data-stu-id="76fb2-199">Choose a recovery point</span></span>
* <span data-ttu-id="76fb2-200">Restore the disks</span><span class="sxs-lookup"><span data-stu-id="76fb2-200">Restore the disks</span></span>
* <span data-ttu-id="76fb2-201">Create the VM from stored disks</span><span class="sxs-lookup"><span data-stu-id="76fb2-201">Create the VM from stored disks</span></span>

<span data-ttu-id="76fb2-202">The graphic below shows the object hierarchy from the RecoveryServicesVault down to the BackupRecoveryPoint.</span><span class="sxs-lookup"><span data-stu-id="76fb2-202">The graphic below shows the object hierarchy from the RecoveryServicesVault down to the BackupRecoveryPoint.</span></span>

![Recovery Services object hierarchy showing BackupContainer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="76fb2-204">To restore backup data, identify the backed-up item and the recovery point that holds the point-in-time data.</span><span class="sxs-lookup"><span data-stu-id="76fb2-204">To restore backup data, identify the backed-up item and the recovery point that holds the point-in-time data.</span></span> <span data-ttu-id="76fb2-205">Then use the **[Restore-AzureRmRecoveryServicesBackupItem](https://msdn.microsoft.com/library/mt723316.aspx)** cmdlet to restore data from the vault to the customer's account.</span><span class="sxs-lookup"><span data-stu-id="76fb2-205">Then use the **[Restore-AzureRmRecoveryServicesBackupItem](https://msdn.microsoft.com/library/mt723316.aspx)** cmdlet to restore data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="76fb2-206">Select the VM</span><span class="sxs-lookup"><span data-stu-id="76fb2-206">Select the VM</span></span>
<span data-ttu-id="76fb2-207">To get the PowerShell object that identifies the right backup item, start from the container in the vault, and work your way down the object hierarchy.</span><span class="sxs-lookup"><span data-stu-id="76fb2-207">To get the PowerShell object that identifies the right backup item, start from the container in the vault, and work your way down the object hierarchy.</span></span> <span data-ttu-id="76fb2-208">To select the container that represents the VM, use the **[Get-AzureRmRecoveryServicesBackupContainer](https://msdn.microsoft.com/library/mt723319.aspx)** cmdlet and pipe that to the **[Get-AzureRmRecoveryServicesBackupItem](https://msdn.microsoft.com/library/mt723305.aspx)** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="76fb2-208">To select the container that represents the VM, use the **[Get-AzureRmRecoveryServicesBackupContainer](https://msdn.microsoft.com/library/mt723319.aspx)** cmdlet and pipe that to the **[Get-AzureRmRecoveryServicesBackupItem](https://msdn.microsoft.com/library/mt723305.aspx)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType AzureVM –Status Registered -FriendlyName 'V2VM'
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="76fb2-209">Choose a recovery point</span><span class="sxs-lookup"><span data-stu-id="76fb2-209">Choose a recovery point</span></span>
<span data-ttu-id="76fb2-210">Use the **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://msdn.microsoft.com/library/mt723308.aspx)** cmdlet to list all the recovery points for the backup item.</span><span class="sxs-lookup"><span data-stu-id="76fb2-210">Use the **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://msdn.microsoft.com/library/mt723308.aspx)** cmdlet to list all the recovery points for the backup item.</span></span> <span data-ttu-id="76fb2-211">Then choose the recovery point to restore.</span><span class="sxs-lookup"><span data-stu-id="76fb2-211">Then choose the recovery point to restore.</span></span> <span data-ttu-id="76fb2-212">If you are unsure which recovery point to use, it is a good practice to choose the most recent RecoveryPointType = AppConsistent point in the list.</span><span class="sxs-lookup"><span data-stu-id="76fb2-212">If you are unsure which recovery point to use, it is a good practice to choose the most recent RecoveryPointType = AppConsistent point in the list.</span></span>

<span data-ttu-id="76fb2-213">In the following script, the variable, **$rp**, is an array of recovery points for the selected backup item.</span><span class="sxs-lookup"><span data-stu-id="76fb2-213">In the following script, the variable, **$rp**, is an array of recovery points for the selected backup item.</span></span> <span data-ttu-id="76fb2-214">The array is sorted in reverse order of time with the latest recovery point at index 0.</span><span class="sxs-lookup"><span data-stu-id="76fb2-214">The array is sorted in reverse order of time with the latest recovery point at index 0.</span></span> <span data-ttu-id="76fb2-215">Use standard PowerShell array indexing to pick the recovery point.</span><span class="sxs-lookup"><span data-stu-id="76fb2-215">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="76fb2-216">For example: $rp[0] will select the latest recovery point.</span><span class="sxs-lookup"><span data-stu-id="76fb2-216">For example: $rp[0] will select the latest recovery point.</span></span>

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM
                              /recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-the-disks"></a><span data-ttu-id="76fb2-217">Restore the disks</span><span class="sxs-lookup"><span data-stu-id="76fb2-217">Restore the disks</span></span>
<span data-ttu-id="76fb2-218">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://msdn.microsoft.com/library/mt723316.aspx)** cmdlet to restore data and configuration for a Backup item, to a recovery point.</span><span class="sxs-lookup"><span data-stu-id="76fb2-218">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://msdn.microsoft.com/library/mt723316.aspx)** cmdlet to restore data and configuration for a Backup item, to a recovery point.</span></span> <span data-ttu-id="76fb2-219">Once you have identified a recovery point use it as the value for the **-RecoveryPoint** parameter.</span><span class="sxs-lookup"><span data-stu-id="76fb2-219">Once you have identified a recovery point use it as the value for the **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="76fb2-220">In the previous example code, **$rp[0]** was chosen as the recovery point to use.</span><span class="sxs-lookup"><span data-stu-id="76fb2-220">In the previous example code, **$rp[0]** was chosen as the recovery point to use.</span></span> <span data-ttu-id="76fb2-221">In the sample code below, **$rp[0]** is specified as the recovery point to use for restoring to disk.</span><span class="sxs-lookup"><span data-stu-id="76fb2-221">In the sample code below, **$rp[0]** is specified as the recovery point to use for restoring to disk.</span></span>

<span data-ttu-id="76fb2-222">To restore the disks and configuration information</span><span class="sxs-lookup"><span data-stu-id="76fb2-222">To restore the disks and configuration information</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName DestAccount -StorageAccountResourceGroupName DestRG
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="76fb2-223">You can use the **[Wait-AzureRmRecoveryServicesBackupJob](https://msdn.microsoft.com/library/mt723321.aspx)** to wait for the Restore job to complete.</span><span class="sxs-lookup"><span data-stu-id="76fb2-223">You can use the **[Wait-AzureRmRecoveryServicesBackupJob](https://msdn.microsoft.com/library/mt723321.aspx)** to wait for the Restore job to complete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="76fb2-224">Once the Restore job has completed, use the **[Get-AzureRmRecoveryServicesBackupJobDetails](https://msdn.microsoft.com/library/mt723310.aspx)** cmdlet to get the details of the restore operation.</span><span class="sxs-lookup"><span data-stu-id="76fb2-224">Once the Restore job has completed, use the **[Get-AzureRmRecoveryServicesBackupJobDetails](https://msdn.microsoft.com/library/mt723310.aspx)** cmdlet to get the details of the restore operation.</span></span> <span data-ttu-id="76fb2-225">The JobDetails property has the information needed to rebuild the VM.</span><span class="sxs-lookup"><span data-stu-id="76fb2-225">The JobDetails property has the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="76fb2-226">Once you restore the disks, go to the next section for information on creating the VM.</span><span class="sxs-lookup"><span data-stu-id="76fb2-226">Once you restore the disks, go to the next section for information on creating the VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="76fb2-227">Create a VM from restored disks</span><span class="sxs-lookup"><span data-stu-id="76fb2-227">Create a VM from restored disks</span></span>
<span data-ttu-id="76fb2-228">After you have restored the disks, use these steps to create and configure the virtual machine from disk.</span><span class="sxs-lookup"><span data-stu-id="76fb2-228">After you have restored the disks, use these steps to create and configure the virtual machine from disk.</span></span>

> [!NOTE]
> If you are creating encrypted VMs using restored disks, your role should be allowed to perform **Microsoft.KeyVault/vaults/deploy/action**. If your role does not have this permission, create a custom role with this action. Refer [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md) to get more details.
>
>

1. <span data-ttu-id="76fb2-232">Query the restored disk properties for the job details.</span><span class="sxs-lookup"><span data-stu-id="76fb2-232">Query the restored disk properties for the job details.</span></span>

    ```
    PS C:\> $properties = $details.properties
    PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
    PS C:\> $containerName = $properties["Config Blob Container Name"]
    PS C:\> $blobName = $properties["Config Blob Name"]
    ```
2. <span data-ttu-id="76fb2-233">Set the Azure storage context and restore the JSON configuration file.</span><span class="sxs-lookup"><span data-stu-id="76fb2-233">Set the Azure storage context and restore the JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName testvault
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```
3. <span data-ttu-id="76fb2-234">Use the JSON configuration file to create the VM configuration.</span><span class="sxs-lookup"><span data-stu-id="76fb2-234">Use the JSON configuration file to create the VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.HardwareProfile.VirtualMachineSize -VMName "testrestore"
    ```
4. <span data-ttu-id="76fb2-235">Attach the OS disk and data disks.</span><span class="sxs-lookup"><span data-stu-id="76fb2-235">Attach the OS disk and data disks.</span></span>

      <span data-ttu-id="76fb2-236">For non-encrypted VMs,</span><span class="sxs-lookup"><span data-stu-id="76fb2-236">For non-encrypted VMs,</span></span>

      ```
      PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.StorageProfile.OSDisk.VirtualHardDisk.Uri -CreateOption “Attach”
      PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.StorageProfile.OSDisk.OperatingSystemType
      PS C:\> foreach($dd in $obj.StorageProfile.DataDisks)
       {
       $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.VirtualHardDisk.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption Attach
       }
       ```
       
      For encrypted VMs, you need to specify [Key vault information](https://msdn.microsoft.com/library/dn868052.aspx) before you can attach disks.

      ```
      <span data-ttu-id="76fb2-237">PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.StorageProfile.OSDisk.VirtualHardDisk.Uri -DiskEncryptionKeyUrl "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007" -DiskEncryptionKeyVaultId "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault" -KeyEncryptionKeyUrl "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007" -KeyEncryptionKeyVaultId "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault" -CreateOption "Attach" -Windows    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.StorageProfile.OSDisk.OperatingSystemType    PS C:\> foreach($dd in $obj.StorageProfile.DataDisks)     {     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.VirtualHardDisk.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption Attach     }</span><span class="sxs-lookup"><span data-stu-id="76fb2-237">PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.StorageProfile.OSDisk.VirtualHardDisk.Uri -DiskEncryptionKeyUrl "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007" -DiskEncryptionKeyVaultId "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault" -KeyEncryptionKeyUrl "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007" -KeyEncryptionKeyVaultId "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault" -CreateOption "Attach" -Windows    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.StorageProfile.OSDisk.OperatingSystemType    PS C:\> foreach($dd in $obj.StorageProfile.DataDisks)     {     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.VirtualHardDisk.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption Attach     }</span></span>
       ```
       
5. <span data-ttu-id="76fb2-238">Set the Network settings.</span><span class="sxs-lookup"><span data-stu-id="76fb2-238">Set the Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="76fb2-239">Create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="76fb2-239">Create the virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="76fb2-240">Next steps</span><span class="sxs-lookup"><span data-stu-id="76fb2-240">Next steps</span></span>
<span data-ttu-id="76fb2-241">If you prefer using PowerShell to engage with your Azure resources, check out the PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="76fb2-241">If you prefer using PowerShell to engage with your Azure resources, check out the PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="76fb2-242">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="76fb2-242">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="76fb2-243">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span><span class="sxs-lookup"><span data-stu-id="76fb2-243">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  


