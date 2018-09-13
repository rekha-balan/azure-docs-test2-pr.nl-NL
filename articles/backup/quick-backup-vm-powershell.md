---
title: Azure Quickstart - Back up a VM with PowerShell
description: Learn how to back up your virtual machines with Azure PowerShell
services: backup
author: markgalioto
manager: carmonm
tags: azure-resource-manager, virtual-machine-backup
ms.service: backup
ms.devlang: azurecli
ms.topic: quickstart
ms.date: 2/14/2018
ms.author: markgal
ms.custom: mvc
ms.openlocfilehash: 4161b11e88d2b3201e18e095e13db864e25d7bfc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868656"
---
# <a name="back-up-a-virtual-machine-in-azure-with-powershell"></a><span data-ttu-id="c644a-103">Back up a virtual machine in Azure with PowerShell</span><span class="sxs-lookup"><span data-stu-id="c644a-103">Back up a virtual machine in Azure with PowerShell</span></span>
<span data-ttu-id="c644a-104">The Azure PowerShell module is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="c644a-104">The Azure PowerShell module is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="c644a-105">You can protect your data by taking backups at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="c644a-105">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="c644a-106">Azure Backup creates recovery points that can be stored in geo-redundant recovery vaults.</span><span class="sxs-lookup"><span data-stu-id="c644a-106">Azure Backup creates recovery points that can be stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="c644a-107">This article details how to back up a virtual machine (VM) with the Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="c644a-107">This article details how to back up a virtual machine (VM) with the Azure PowerShell module.</span></span> <span data-ttu-id="c644a-108">You can also perform these steps with the [Azure CLI](quick-backup-vm-cli.md) or [Azure portal](quick-backup-vm-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c644a-108">You can also perform these steps with the [Azure CLI](quick-backup-vm-cli.md) or [Azure portal](quick-backup-vm-portal.md).</span></span>

<span data-ttu-id="c644a-109">This quickstart enables backup on an existing Azure VM.</span><span class="sxs-lookup"><span data-stu-id="c644a-109">This quickstart enables backup on an existing Azure VM.</span></span> <span data-ttu-id="c644a-110">If you need to create a VM, you can [create a VM with Azure PowerShell](../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c644a-110">If you need to create a VM, you can [create a VM with Azure PowerShell](../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span>

<span data-ttu-id="c644a-111">This quickstart requires the Azure PowerShell module version 4.4 or later.</span><span class="sxs-lookup"><span data-stu-id="c644a-111">This quickstart requires the Azure PowerShell module version 4.4 or later.</span></span> <span data-ttu-id="c644a-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="c644a-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="c644a-113">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c644a-113">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="log-in-to-azure"></a><span data-ttu-id="c644a-114">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="c644a-114">Log in to Azure</span></span>
<span data-ttu-id="c644a-115">Log in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="c644a-115">Log in to your Azure subscription with the `Connect-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Connect-AzureRmAccount
```

<span data-ttu-id="c644a-116">The first time you use Azure Backup, you must register the Azure Recovery Service provider in your subscription with [Register-AzureRmResourceProvider](/powershell/module/AzureRM.Resources/Register-AzureRmResourceProvider).</span><span class="sxs-lookup"><span data-stu-id="c644a-116">The first time you use Azure Backup, you must register the Azure Recovery Service provider in your subscription with [Register-AzureRmResourceProvider](/powershell/module/AzureRM.Resources/Register-AzureRmResourceProvider).</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
```


## <a name="create-a-recovery-services-vaults"></a><span data-ttu-id="c644a-117">Create a recovery services vaults</span><span class="sxs-lookup"><span data-stu-id="c644a-117">Create a recovery services vaults</span></span>
<span data-ttu-id="c644a-118">A Recovery Services vault is a logical container that stores the backup data for each protected resource, such as Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="c644a-118">A Recovery Services vault is a logical container that stores the backup data for each protected resource, such as Azure VMs.</span></span> <span data-ttu-id="c644a-119">When the backup job for a protected resource runs, it creates a recovery point inside the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="c644a-119">When the backup job for a protected resource runs, it creates a recovery point inside the Recovery Services vault.</span></span> <span data-ttu-id="c644a-120">You can then use one of these recovery points to restore data to a given point in time.</span><span class="sxs-lookup"><span data-stu-id="c644a-120">You can then use one of these recovery points to restore data to a given point in time.</span></span>

<span data-ttu-id="c644a-121">Create a Recovery Services vault with [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault).</span><span class="sxs-lookup"><span data-stu-id="c644a-121">Create a Recovery Services vault with [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault).</span></span> <span data-ttu-id="c644a-122">Specify the same resource group and location as the VM you wish to protect.</span><span class="sxs-lookup"><span data-stu-id="c644a-122">Specify the same resource group and location as the VM you wish to protect.</span></span> <span data-ttu-id="c644a-123">If you used the [sample script](../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) to create your VM, the resource group is named *myResourceGroup*, the VM is named *myVM*, and the resources are in the *WestEurope* location.</span><span class="sxs-lookup"><span data-stu-id="c644a-123">If you used the [sample script](../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) to create your VM, the resource group is named *myResourceGroup*, the VM is named *myVM*, and the resources are in the *WestEurope* location.</span></span>

```powershell
New-AzureRmRecoveryServicesVault `
    -ResourceGroupName "myResourceGroup" `
    -Name "myRecoveryServicesVault" `
    -Location "WestEurope"
```

<span data-ttu-id="c644a-124">By default, the vault is set for Geo-Redundant storage.</span><span class="sxs-lookup"><span data-stu-id="c644a-124">By default, the vault is set for Geo-Redundant storage.</span></span> <span data-ttu-id="c644a-125">To further protect your data, this storage redundancy level ensures that your backup data is replicated to a secondary Azure region that is hundreds of miles away from the primary region.</span><span class="sxs-lookup"><span data-stu-id="c644a-125">To further protect your data, this storage redundancy level ensures that your backup data is replicated to a secondary Azure region that is hundreds of miles away from the primary region.</span></span>

<span data-ttu-id="c644a-126">To use this vault with the remaining steps, set the vault context with [Set-AzureRmRecoveryServicesVaultContext](/powershell/module/AzureRM.RecoveryServices/Set-AzureRmRecoveryServicesVaultContext)</span><span class="sxs-lookup"><span data-stu-id="c644a-126">To use this vault with the remaining steps, set the vault context with [Set-AzureRmRecoveryServicesVaultContext](/powershell/module/AzureRM.RecoveryServices/Set-AzureRmRecoveryServicesVaultContext)</span></span>

```powershell
Get-AzureRmRecoveryServicesVault `
    -Name "myRecoveryServicesVault" | Set-AzureRmRecoveryServicesVaultContext
```


## <a name="enable-backup-for-an-azure-vm"></a><span data-ttu-id="c644a-127">Enable backup for an Azure VM</span><span class="sxs-lookup"><span data-stu-id="c644a-127">Enable backup for an Azure VM</span></span>
<span data-ttu-id="c644a-128">You create and use policies to define when a backup job runs and how long the recovery points are stored.</span><span class="sxs-lookup"><span data-stu-id="c644a-128">You create and use policies to define when a backup job runs and how long the recovery points are stored.</span></span> <span data-ttu-id="c644a-129">The default protection policy runs a backup job each day, and retains recovery points for 30 days.</span><span class="sxs-lookup"><span data-stu-id="c644a-129">The default protection policy runs a backup job each day, and retains recovery points for 30 days.</span></span> <span data-ttu-id="c644a-130">You can use these default policy values to quickly protect your VM.</span><span class="sxs-lookup"><span data-stu-id="c644a-130">You can use these default policy values to quickly protect your VM.</span></span> <span data-ttu-id="c644a-131">First, set the default policy with [Get-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/AzureRM.RecoveryServices.Backup/Get-AzureRmRecoveryServicesBackupProtectionPolicy):</span><span class="sxs-lookup"><span data-stu-id="c644a-131">First, set the default policy with [Get-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/AzureRM.RecoveryServices.Backup/Get-AzureRmRecoveryServicesBackupProtectionPolicy):</span></span>

```powershell
$policy = Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "DefaultPolicy"
```

<span data-ttu-id="c644a-132">To enable backup protection for a VM, use [Enable-AzureRmRecoveryServicesBackupProtection](/powershell/module/AzureRM.RecoveryServices.Backup/Enable-AzureRmRecoveryServicesBackupProtection).</span><span class="sxs-lookup"><span data-stu-id="c644a-132">To enable backup protection for a VM, use [Enable-AzureRmRecoveryServicesBackupProtection](/powershell/module/AzureRM.RecoveryServices.Backup/Enable-AzureRmRecoveryServicesBackupProtection).</span></span> <span data-ttu-id="c644a-133">Specify the policy to use, then the resource group and VM to protect:</span><span class="sxs-lookup"><span data-stu-id="c644a-133">Specify the policy to use, then the resource group and VM to protect:</span></span>

```powershell
Enable-AzureRmRecoveryServicesBackupProtection `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVM" `
    -Policy $policy
```


## <a name="start-a-backup-job"></a><span data-ttu-id="c644a-134">Start a backup job</span><span class="sxs-lookup"><span data-stu-id="c644a-134">Start a backup job</span></span>
<span data-ttu-id="c644a-135">To start a backup now rather than wait for the default policy to run the job at the scheduled time, use [Backup-AzureRmRecoveryServicesBackupItem](/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem).</span><span class="sxs-lookup"><span data-stu-id="c644a-135">To start a backup now rather than wait for the default policy to run the job at the scheduled time, use [Backup-AzureRmRecoveryServicesBackupItem](/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem).</span></span> <span data-ttu-id="c644a-136">This first backup job creates a full recovery point.</span><span class="sxs-lookup"><span data-stu-id="c644a-136">This first backup job creates a full recovery point.</span></span> <span data-ttu-id="c644a-137">Each backup job after this initial backup creates incremental recovery points.</span><span class="sxs-lookup"><span data-stu-id="c644a-137">Each backup job after this initial backup creates incremental recovery points.</span></span> <span data-ttu-id="c644a-138">Incremental recovery points are storage and time-efficient, as they only transfer changes made since the last backup.</span><span class="sxs-lookup"><span data-stu-id="c644a-138">Incremental recovery points are storage and time-efficient, as they only transfer changes made since the last backup.</span></span>

<span data-ttu-id="c644a-139">In the following set of commands, you specify a container in the Recovery Services vault that holds your backup data with [Get-AzureRmRecoveryServicesBackupContainer](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer).</span><span class="sxs-lookup"><span data-stu-id="c644a-139">In the following set of commands, you specify a container in the Recovery Services vault that holds your backup data with [Get-AzureRmRecoveryServicesBackupContainer](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer).</span></span> <span data-ttu-id="c644a-140">Each VM to back up is treated as an item.</span><span class="sxs-lookup"><span data-stu-id="c644a-140">Each VM to back up is treated as an item.</span></span> <span data-ttu-id="c644a-141">To start a backup job, obtain information on your VM item with [Get-AzureRmRecoveryServicesBackupItem](/powershell/module/AzureRM.RecoveryServices.Backup/Get-AzureRmRecoveryServicesBackupItem).</span><span class="sxs-lookup"><span data-stu-id="c644a-141">To start a backup job, obtain information on your VM item with [Get-AzureRmRecoveryServicesBackupItem](/powershell/module/AzureRM.RecoveryServices.Backup/Get-AzureRmRecoveryServicesBackupItem).</span></span>

```powershell
$backupcontainer = Get-AzureRmRecoveryServicesBackupContainer `
    -ContainerType "AzureVM" `
    -FriendlyName "myVM"

$item = Get-AzureRmRecoveryServicesBackupItem `
    -Container $backupcontainer `
    -WorkloadType "AzureVM"

Backup-AzureRmRecoveryServicesBackupItem -Item $item
```

<span data-ttu-id="c644a-142">As this first backup job creates a full recovery point, the process can take up to 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="c644a-142">As this first backup job creates a full recovery point, the process can take up to 20 minutes.</span></span>


## <a name="monitor-the-backup-job"></a><span data-ttu-id="c644a-143">Monitor the backup job</span><span class="sxs-lookup"><span data-stu-id="c644a-143">Monitor the backup job</span></span>
<span data-ttu-id="c644a-144">To monitor the status of backup jobs, use [Get-AzureRmRecoveryservicesBackupJob](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob):</span><span class="sxs-lookup"><span data-stu-id="c644a-144">To monitor the status of backup jobs, use [Get-AzureRmRecoveryservicesBackupJob](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob):</span></span>

```powershell
Get-AzureRmRecoveryservicesBackupJob
```

<span data-ttu-id="c644a-145">The output is similar to the following example, which shows the backup job is **InProgress**:</span><span class="sxs-lookup"><span data-stu-id="c644a-145">The output is similar to the following example, which shows the backup job is **InProgress**:</span></span>

```
WorkloadName   Operation         Status       StartTime              EndTime                JobID
------------   ---------         ------       ---------              -------                -----
myvm           Backup            InProgress   9/18/2017 9:38:02 PM                          9f9e8f14
myvm           ConfigureBackup   Completed    9/18/2017 9:33:18 PM   9/18/2017 9:33:51 PM   fe79c739
```

<span data-ttu-id="c644a-146">When the *Status* of the backup job reports *Completed*, your VM is protected with Recovery Services and has a full recovery point stored.</span><span class="sxs-lookup"><span data-stu-id="c644a-146">When the *Status* of the backup job reports *Completed*, your VM is protected with Recovery Services and has a full recovery point stored.</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="c644a-147">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="c644a-147">Clean up deployment</span></span>
<span data-ttu-id="c644a-148">When no longer needed, you can disable protection on the VM, remove the restore points and Recovery Services vault, then delete the resource group and associated VM resources.</span><span class="sxs-lookup"><span data-stu-id="c644a-148">When no longer needed, you can disable protection on the VM, remove the restore points and Recovery Services vault, then delete the resource group and associated VM resources.</span></span> <span data-ttu-id="c644a-149">If you used an existing VM, you can skip the final [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) cmdlet to leave the resource group and VM in place.</span><span class="sxs-lookup"><span data-stu-id="c644a-149">If you used an existing VM, you can skip the final [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) cmdlet to leave the resource group and VM in place.</span></span>

<span data-ttu-id="c644a-150">If you are going to continue on to a Backup tutorial that explains how to restore data for your VM, skip the steps in this section and go to [Next steps](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="c644a-150">If you are going to continue on to a Backup tutorial that explains how to restore data for your VM, skip the steps in this section and go to [Next steps](#next-steps).</span></span> 

```powershell
Disable-AzureRmRecoveryServicesBackupProtection -Item $item -RemoveRecoveryPoints
$vault = Get-AzureRmRecoveryServicesVault -Name "myRecoveryServicesVault"
Remove-AzureRmRecoveryServicesVault -Vault $vault
Remove-AzureRmResourceGroup -Name "myResourceGroup"
```


## <a name="next-steps"></a><span data-ttu-id="c644a-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="c644a-151">Next steps</span></span>
<span data-ttu-id="c644a-152">In this quickstart, you created a Recovery Services vault, enabled protection on a VM, and created the initial recovery point.</span><span class="sxs-lookup"><span data-stu-id="c644a-152">In this quickstart, you created a Recovery Services vault, enabled protection on a VM, and created the initial recovery point.</span></span> <span data-ttu-id="c644a-153">To learn more about Azure Backup and Recovery Services, continue to the tutorials.</span><span class="sxs-lookup"><span data-stu-id="c644a-153">To learn more about Azure Backup and Recovery Services, continue to the tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c644a-154">Back up multiple Azure VMs</span><span class="sxs-lookup"><span data-stu-id="c644a-154">Back up multiple Azure VMs</span></span>](./tutorial-backup-vm-at-scale.md)
