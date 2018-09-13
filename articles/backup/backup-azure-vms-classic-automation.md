---
title: Deploy and manage backup for Azure VMs using PowerShell | Microsoft Docs
description: Learn how to deploy and manage Azure Backup using PowerShell.
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5ba0bd83fcb9d2e94cfccc9f5466d606cba2588f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556408"
---
# <a name="use-azurermbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="01d2e-103">Use AzureRM.Backup cmdlets to back up virtual machines</span><span class="sxs-lookup"><span data-stu-id="01d2e-103">Use AzureRM.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-vms-automation.md)
> * [Classic](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="01d2e-106">This article shows you how to use Azure PowerShell for backup and recovery of Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="01d2e-106">This article shows you how to use Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="01d2e-107">Azure has two different deployment models for creating and working with resources: Resouce Manager and Classic.</span><span class="sxs-lookup"><span data-stu-id="01d2e-107">Azure has two different deployment models for creating and working with resources: Resouce Manager and Classic.</span></span> <span data-ttu-id="01d2e-108">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="01d2e-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="01d2e-109">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="01d2e-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="concepts"></a><span data-ttu-id="01d2e-110">Concepts</span><span class="sxs-lookup"><span data-stu-id="01d2e-110">Concepts</span></span>
<span data-ttu-id="01d2e-111">This article provides information specific to the PowerShell cmdlets used to back up virtual machines.</span><span class="sxs-lookup"><span data-stu-id="01d2e-111">This article provides information specific to the PowerShell cmdlets used to back up virtual machines.</span></span> <span data-ttu-id="01d2e-112">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="01d2e-112">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> Before you start, read the [prerequisites](backup-azure-vms-prepare.md) required to work with Azure Backup, and the [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of the current VM backup solution.
>
>

<span data-ttu-id="01d2e-114">To use PowerShell effectively, take a moment to understand the hierarchy of objects and from where to start.</span><span class="sxs-lookup"><span data-stu-id="01d2e-114">To use PowerShell effectively, take a moment to understand the hierarchy of objects and from where to start.</span></span>

![Object hierarchy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="01d2e-116">The two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span><span class="sxs-lookup"><span data-stu-id="01d2e-116">The two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="01d2e-117">The focus of this article is to help you become adept at working with the PowerShell cmdlets to enable these two scenarios.</span><span class="sxs-lookup"><span data-stu-id="01d2e-117">The focus of this article is to help you become adept at working with the PowerShell cmdlets to enable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="01d2e-118">Setup and Registration</span><span class="sxs-lookup"><span data-stu-id="01d2e-118">Setup and Registration</span></span>
<span data-ttu-id="01d2e-119">To begin:</span><span class="sxs-lookup"><span data-stu-id="01d2e-119">To begin:</span></span>

1. <span data-ttu-id="01d2e-120">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="01d2e-120">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="01d2e-121">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span><span class="sxs-lookup"><span data-stu-id="01d2e-121">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

<span data-ttu-id="01d2e-122">The following setup and registration tasks can be automated with PowerShell:</span><span class="sxs-lookup"><span data-stu-id="01d2e-122">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="01d2e-123">Create a backup vault</span><span class="sxs-lookup"><span data-stu-id="01d2e-123">Create a backup vault</span></span>
* <span data-ttu-id="01d2e-124">Registering the VMs with the Azure Backup service</span><span class="sxs-lookup"><span data-stu-id="01d2e-124">Registering the VMs with the Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="01d2e-125">Create a backup vault</span><span class="sxs-lookup"><span data-stu-id="01d2e-125">Create a backup vault</span></span>
> [!WARNING]
> For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription. This can be done by running the following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"
>
>

<span data-ttu-id="01d2e-128">You can create a new backup vault using the **New-AzureRmBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01d2e-128">You can create a new backup vault using the **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="01d2e-129">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span><span class="sxs-lookup"><span data-stu-id="01d2e-129">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="01d2e-130">In an elevated Azure PowerShell console, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="01d2e-130">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="01d2e-131">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRmBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01d2e-131">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> It is convenient to store the backup vault object into a variable. The vault object is needed as an input for many Azure Backup cmdlets.
>
>

### <a name="registering-the-vms"></a><span data-ttu-id="01d2e-134">Registering the VMs</span><span class="sxs-lookup"><span data-stu-id="01d2e-134">Registering the VMs</span></span>
<span data-ttu-id="01d2e-135">The first step towards configuring backup with Azure Backup is to register your machine or VM with an Azure Backup vault.</span><span class="sxs-lookup"><span data-stu-id="01d2e-135">The first step towards configuring backup with Azure Backup is to register your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="01d2e-136">The **Register-AzureRmBackupContainer** cmdlet takes the input information of an Azure IaaS virtual machine and registers it with the specified vault.</span><span class="sxs-lookup"><span data-stu-id="01d2e-136">The **Register-AzureRmBackupContainer** cmdlet takes the input information of an Azure IaaS virtual machine and registers it with the specified vault.</span></span> <span data-ttu-id="01d2e-137">The register operation associates the Azure virtual machine with the backup vault and tracks the VM through the backup lifecycle.</span><span class="sxs-lookup"><span data-stu-id="01d2e-137">The register operation associates the Azure virtual machine with the backup vault and tracks the VM through the backup lifecycle.</span></span>

<span data-ttu-id="01d2e-138">Registering your VM with the Azure Backup service creates a top-level container object.</span><span class="sxs-lookup"><span data-stu-id="01d2e-138">Registering your VM with the Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="01d2e-139">A container typically contains multiple items that can be backed up, but in the case of VMs there will be only one backup item for the container.</span><span class="sxs-lookup"><span data-stu-id="01d2e-139">A container typically contains multiple items that can be backed up, but in the case of VMs there will be only one backup item for the container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="01d2e-140">Backup Azure VMs</span><span class="sxs-lookup"><span data-stu-id="01d2e-140">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="01d2e-141">Create a protection policy</span><span class="sxs-lookup"><span data-stu-id="01d2e-141">Create a protection policy</span></span>
<span data-ttu-id="01d2e-142">It is not mandatory to create a new protection policy to start backup of your VMs.</span><span class="sxs-lookup"><span data-stu-id="01d2e-142">It is not mandatory to create a new protection policy to start backup of your VMs.</span></span> <span data-ttu-id="01d2e-143">The vault comes with a 'Default Policy' that can be used to quickly enable protection, and then edited later with the right details.</span><span class="sxs-lookup"><span data-stu-id="01d2e-143">The vault comes with a 'Default Policy' that can be used to quickly enable protection, and then edited later with the right details.</span></span> <span data-ttu-id="01d2e-144">You can get a list of the policies available in the vault by using the **Get-AzureRmBackupProtectionPolicy** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="01d2e-144">You can get a list of the policies available in the vault by using the **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> The timezone of the BackupTime field in PowerShell is UTC. However, when the backup time is shown in the Azure portal, the timezone is aligned to your local system along with the UTC offset.
>
>

<span data-ttu-id="01d2e-147">A backup policy is associated with at least one retention policy.</span><span class="sxs-lookup"><span data-stu-id="01d2e-147">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="01d2e-148">The retention policy defines how long a recovery point is kept with Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="01d2e-148">The retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="01d2e-149">The **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span><span class="sxs-lookup"><span data-stu-id="01d2e-149">The **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="01d2e-150">These retention policy objects are used as inputs to the *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with the *Enable-AzureRmBackupProtection* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01d2e-150">These retention policy objects are used as inputs to the *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="01d2e-151">A backup policy defines when and how often the backup of an item is done.</span><span class="sxs-lookup"><span data-stu-id="01d2e-151">A backup policy defines when and how often the backup of an item is done.</span></span> <span data-ttu-id="01d2e-152">The **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span><span class="sxs-lookup"><span data-stu-id="01d2e-152">The **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="01d2e-153">The backup policy is used as an input to the *Enable-AzureRmBackupProtection* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01d2e-153">The backup policy is used as an input to the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="01d2e-154">Enable protection</span><span class="sxs-lookup"><span data-stu-id="01d2e-154">Enable protection</span></span>
<span data-ttu-id="01d2e-155">Enabling protection involves two objects - the Item and the Policy, and both need to belong to the same vault.</span><span class="sxs-lookup"><span data-stu-id="01d2e-155">Enabling protection involves two objects - the Item and the Policy, and both need to belong to the same vault.</span></span> <span data-ttu-id="01d2e-156">Once the policy has been associated with the item, the backup workflow will kick in at the defined schedule.</span><span class="sxs-lookup"><span data-stu-id="01d2e-156">Once the policy has been associated with the item, the backup workflow will kick in at the defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="01d2e-157">Initial backup</span><span class="sxs-lookup"><span data-stu-id="01d2e-157">Initial backup</span></span>
<span data-ttu-id="01d2e-158">The backup schedule will take care of doing the full initial copy for the item and the incremental copy for the subsequent backups.</span><span class="sxs-lookup"><span data-stu-id="01d2e-158">The backup schedule will take care of doing the full initial copy for the item and the incremental copy for the subsequent backups.</span></span> <span data-ttu-id="01d2e-159">However, if you want to force the initial backup to happen at a certain time or even immediately then use the **Backup-AzureRmBackupItem** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="01d2e-159">However, if you want to force the initial backup to happen at a certain time or even immediately then use the **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> The timezone of the StartTime and EndTime fields shown in PowerShell is UTC. However, when the similar information is shown in the Azure portal, the timezone is aligned to your local system clock.
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="01d2e-162">Monitoring a backup job</span><span class="sxs-lookup"><span data-stu-id="01d2e-162">Monitoring a backup job</span></span>
<span data-ttu-id="01d2e-163">Most long-running operations in Azure Backup are modelled as a job.</span><span class="sxs-lookup"><span data-stu-id="01d2e-163">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="01d2e-164">This makes it easy to track progress without having to keep the Azure portal open at all times.</span><span class="sxs-lookup"><span data-stu-id="01d2e-164">This makes it easy to track progress without having to keep the Azure portal open at all times.</span></span>

<span data-ttu-id="01d2e-165">To get the latest status of an in-progress job, use the **Get-AzureRmBackupJob** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01d2e-165">To get the latest status of an in-progress job, use the **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="01d2e-166">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler to use the **Wait-AzureRmBackupJob** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01d2e-166">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler to use the **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="01d2e-167">When used in a script, the cmdlet will pause the execution until either the job completes or the specified timeout value is reached.</span><span class="sxs-lookup"><span data-stu-id="01d2e-167">When used in a script, the cmdlet will pause the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="01d2e-168">Restore an Azure VM</span><span class="sxs-lookup"><span data-stu-id="01d2e-168">Restore an Azure VM</span></span>
<span data-ttu-id="01d2e-169">In order to restore backup data, you need to identify the backed-up Item and the Recovery Point that holds the point-in-time data.</span><span class="sxs-lookup"><span data-stu-id="01d2e-169">In order to restore backup data, you need to identify the backed-up Item and the Recovery Point that holds the point-in-time data.</span></span> <span data-ttu-id="01d2e-170">This information is supplied to the Restore-AzureRmBackupItem cmdlet to initiate a restore of data from the vault to the customer's account.</span><span class="sxs-lookup"><span data-stu-id="01d2e-170">This information is supplied to the Restore-AzureRmBackupItem cmdlet to initiate a restore of data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="01d2e-171">Select the VM</span><span class="sxs-lookup"><span data-stu-id="01d2e-171">Select the VM</span></span>
<span data-ttu-id="01d2e-172">To get the PowerShell object that identifies the right backup Item, you need to start from the Container in the vault, and work your way down object hierarchy.</span><span class="sxs-lookup"><span data-stu-id="01d2e-172">To get the PowerShell object that identifies the right backup Item, you need to start from the Container in the vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="01d2e-173">To select the container that represents the VM, use the **Get-AzureRmBackupContainer** cmdlet and pipe that to the **Get-AzureRmBackupItem** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01d2e-173">To select the container that represents the VM, use the **Get-AzureRmBackupContainer** cmdlet and pipe that to the **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="01d2e-174">Choose a recovery point</span><span class="sxs-lookup"><span data-stu-id="01d2e-174">Choose a recovery point</span></span>
<span data-ttu-id="01d2e-175">You can now list all the recovery points for the backup item using the **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose the recovery point to restore.</span><span class="sxs-lookup"><span data-stu-id="01d2e-175">You can now list all the recovery points for the backup item using the **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose the recovery point to restore.</span></span> <span data-ttu-id="01d2e-176">Typically users pick the most recent *AppConsistent* point in the list.</span><span class="sxs-lookup"><span data-stu-id="01d2e-176">Typically users pick the most recent *AppConsistent* point in the list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="01d2e-177">The variable ```$rp``` is an array of recovery points for the selected backup item, sorted in reverse order of time - the latest recovery point is at index 0.</span><span class="sxs-lookup"><span data-stu-id="01d2e-177">The variable ```$rp``` is an array of recovery points for the selected backup item, sorted in reverse order of time - the latest recovery point is at index 0.</span></span> <span data-ttu-id="01d2e-178">Use standard PowerShell array indexing to pick the recovery point.</span><span class="sxs-lookup"><span data-stu-id="01d2e-178">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="01d2e-179">For example: ```$rp[0]``` will select the latest recovery point.</span><span class="sxs-lookup"><span data-stu-id="01d2e-179">For example: ```$rp[0]``` will select the latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="01d2e-180">Restoring disks</span><span class="sxs-lookup"><span data-stu-id="01d2e-180">Restoring disks</span></span>
<span data-ttu-id="01d2e-181">There is a key difference between the restore operations done through the Azure portal and through Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01d2e-181">There is a key difference between the restore operations done through the Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="01d2e-182">With PowerShell, the restore operation stops at restoring the disks and config information from the recovery point.</span><span class="sxs-lookup"><span data-stu-id="01d2e-182">With PowerShell, the restore operation stops at restoring the disks and config information from the recovery point.</span></span> <span data-ttu-id="01d2e-183">It does not create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="01d2e-183">It does not create a virtual machine.</span></span>

> [!WARNING]
> The Restore-AzureRmBackupItem does not create a VM. It only restores the disks to the specified storage account. This is not the same behavior you will experience in the Azure portal.
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="01d2e-187">You can get the details of the restore operation using the **Get-AzureRmBackupJobDetails** cmdlet once the Restore job has completed.</span><span class="sxs-lookup"><span data-stu-id="01d2e-187">You can get the details of the restore operation using the **Get-AzureRmBackupJobDetails** cmdlet once the Restore job has completed.</span></span> <span data-ttu-id="01d2e-188">The *ErrorDetails* property will have the information needed to rebuild the VM.</span><span class="sxs-lookup"><span data-stu-id="01d2e-188">The *ErrorDetails* property will have the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-the-vm"></a><span data-ttu-id="01d2e-189">Build the VM</span><span class="sxs-lookup"><span data-stu-id="01d2e-189">Build the VM</span></span>
<span data-ttu-id="01d2e-190">Building the VM out of the restored disks can be done using the older Azure Service Management PowerShell cmdlets, the new Azure Resource Manager templates, or even using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="01d2e-190">Building the VM out of the restored disks can be done using the older Azure Service Management PowerShell cmdlets, the new Azure Resource Manager templates, or even using the Azure portal.</span></span> <span data-ttu-id="01d2e-191">In a quick example, we will show how to get there using the Azure Service Management cmdlets.</span><span class="sxs-lookup"><span data-stu-id="01d2e-191">In a quick example, we will show how to get there using the Azure Service Management cmdlets.</span></span>

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

<span data-ttu-id="01d2e-192">For more information on how to build a VM from the restored disks, read about the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="01d2e-192">For more information on how to build a VM from the restored disks, read about the following cmdlets:</span></span>

* [<span data-ttu-id="01d2e-193">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="01d2e-193">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="01d2e-194">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="01d2e-194">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="01d2e-195">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="01d2e-195">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="01d2e-196">Code samples</span><span class="sxs-lookup"><span data-stu-id="01d2e-196">Code samples</span></span>
### <a name="1-get-the-completion-status-of-job-sub-tasks"></a><span data-ttu-id="01d2e-197">1. Get the completion status of job sub-tasks</span><span class="sxs-lookup"><span data-stu-id="01d2e-197">1. Get the completion status of job sub-tasks</span></span>
<span data-ttu-id="01d2e-198">To track the completion status of individual sub-tasks, you can use the **Get-AzureRmBackupJobDetails** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="01d2e-198">To track the completion status of individual sub-tasks, you can use the **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data to Backup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="01d2e-199">2. Create a daily/weekly report of backup jobs</span><span class="sxs-lookup"><span data-stu-id="01d2e-199">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="01d2e-200">Administrators typically want to know what backup jobs ran in the last 24 hours, the status of those backup jobs.</span><span class="sxs-lookup"><span data-stu-id="01d2e-200">Administrators typically want to know what backup jobs ran in the last 24 hours, the status of those backup jobs.</span></span> <span data-ttu-id="01d2e-201">Additionally, the amount of data transferred gives administrators a way to estimate their monthly data usage.</span><span class="sxs-lookup"><span data-stu-id="01d2e-201">Additionally, the amount of data transferred gives administrators a way to estimate their monthly data usage.</span></span> <span data-ttu-id="01d2e-202">The script below pulls the raw data from the Azure Backup service and displays the information in the PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="01d2e-202">The script below pulls the raw data from the Azure Backup service and displays the information in the PowerShell console.</span></span>

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -To $enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for the last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract the information for the reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

<span data-ttu-id="01d2e-203">If you want to add charting capabilities to this report output, learn from the TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="01d2e-203">If you want to add charting capabilities to this report output, learn from the TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="01d2e-204">Next steps</span><span class="sxs-lookup"><span data-stu-id="01d2e-204">Next steps</span></span>
<span data-ttu-id="01d2e-205">If you prefer using PowerShell to engage with your Azure resources, check out the PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="01d2e-205">If you prefer using PowerShell to engage with your Azure resources, check out the PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="01d2e-206">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="01d2e-206">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="01d2e-207">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span><span class="sxs-lookup"><span data-stu-id="01d2e-207">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>

