---
title: Back up Azure VMs in Azure at scale
description: This tutorial details backing up multiple Azure virtual machines to a Recovery Services vault.
services: backup
author: markgalioto
manager: carmonm
keywords: virtual machine backup; back up virtual machine; backup and disaster recovery
ms.service: backup
ms.topic: tutorial
ms.date: 09/06/2017
ms.author: trinadhk
ms.custom: mvc
ms.openlocfilehash: 863960e012a8e345434459ad16526c8971f00b6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856977"
---
# <a name="back-up-azure-virtual-machines-in-azure-at-scale"></a><span data-ttu-id="5ef2a-104">Back up Azure virtual machines in Azure at scale</span><span class="sxs-lookup"><span data-stu-id="5ef2a-104">Back up Azure virtual machines in Azure at scale</span></span>

<span data-ttu-id="5ef2a-105">This tutorial details how to back up Azure virtual machines to a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-105">This tutorial details how to back up Azure virtual machines to a Recovery Services vault.</span></span> <span data-ttu-id="5ef2a-106">Most of the work for backing up virtual machines is the preparation.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-106">Most of the work for backing up virtual machines is the preparation.</span></span> <span data-ttu-id="5ef2a-107">Before you can back up (or protect) a virtual machine, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-107">Before you can back up (or protect) a virtual machine, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="5ef2a-108">This tutorial assumes you have already created a resource group and an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-108">This tutorial assumes you have already created a resource group and an Azure virtual machine.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="5ef2a-109">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="5ef2a-109">Create a Recovery Services vault</span></span>

<span data-ttu-id="5ef2a-110">A [Recovery Services vault](backup-azure-recovery-services-vault-overview.md) is a container that holds the recovery points for the items being backed up.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-110">A [Recovery Services vault](backup-azure-recovery-services-vault-overview.md) is a container that holds the recovery points for the items being backed up.</span></span> <span data-ttu-id="5ef2a-111">A Recovery Services vault is an Azure resource that can be deployed and managed as part of an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-111">A Recovery Services vault is an Azure resource that can be deployed and managed as part of an Azure resource group.</span></span> <span data-ttu-id="5ef2a-112">In this tutorial, you create a Recovery Services vault in the same resource group as the virtual machine being protected.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-112">In this tutorial, you create a Recovery Services vault in the same resource group as the virtual machine being protected.</span></span>


<span data-ttu-id="5ef2a-113">The first time you use Azure Backup, you must register the Azure Recovery Service provider with your subscription.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-113">The first time you use Azure Backup, you must register the Azure Recovery Service provider with your subscription.</span></span> <span data-ttu-id="5ef2a-114">If you have already registered the provider with your subscription, go to the next step.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-114">If you have already registered the provider with your subscription, go to the next step.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices
```

<span data-ttu-id="5ef2a-115">Create a Recovery Services vault with **New-AzureRmRecoveryServicesVault**.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-115">Create a Recovery Services vault with **New-AzureRmRecoveryServicesVault**.</span></span> <span data-ttu-id="5ef2a-116">Be sure to specify the resource group name and location used when configuring the virtual machine that you want to back up.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-116">Be sure to specify the resource group name and location used when configuring the virtual machine that you want to back up.</span></span> 

```powershell
New-AzureRmRecoveryServicesVault -Name myRSvault -ResourceGroupName "myResourceGroup" -Location "EastUS"
```

<span data-ttu-id="5ef2a-117">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-117">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="5ef2a-118">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-118">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span> <span data-ttu-id="5ef2a-119">Then use **Set-AzureRmRecoveryServicesBackupProperties** to set the **-BackupStorageRedundancy** option to [Geo-Redundant Storage (GRS)](../storage/common/storage-redundancy-grs.md).</span><span class="sxs-lookup"><span data-stu-id="5ef2a-119">Then use **Set-AzureRmRecoveryServicesBackupProperties** to set the **-BackupStorageRedundancy** option to [Geo-Redundant Storage (GRS)](../storage/common/storage-redundancy-grs.md).</span></span> 

```powershell
$vault1 = Get-AzureRmRecoveryServicesVault –Name myRSVault
Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
```

## <a name="back-up-azure-virtual-machines"></a><span data-ttu-id="5ef2a-120">Back up Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="5ef2a-120">Back up Azure virtual machines</span></span>

<span data-ttu-id="5ef2a-121">Before you can run the initial backup, you must set the vault context.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-121">Before you can run the initial backup, you must set the vault context.</span></span> <span data-ttu-id="5ef2a-122">The vault context is the type of data protected in the vault.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-122">The vault context is the type of data protected in the vault.</span></span> <span data-ttu-id="5ef2a-123">When you create a Recovery Services vault, it comes with default protection and retention policies.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-123">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="5ef2a-124">The default protection policy triggers a backup job each day at a specified time.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-124">The default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="5ef2a-125">The default retention policy retains the daily recovery point for 30 days.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-125">The default retention policy retains the daily recovery point for 30 days.</span></span> <span data-ttu-id="5ef2a-126">For this tutorial, accept the default policy.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-126">For this tutorial, accept the default policy.</span></span> 

<span data-ttu-id="5ef2a-127">Use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-127">Use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context.</span></span> <span data-ttu-id="5ef2a-128">Once the vault context is set, it applies to all subsequent cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-128">Once the vault context is set, it applies to all subsequent cmdlets.</span></span> 

```powershell
Get-AzureRmRecoveryServicesVault -Name myRSVault | Set-AzureRmRecoveryServicesVaultContext
```

<span data-ttu-id="5ef2a-129">Use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** to trigger the backup job.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-129">Use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** to trigger the backup job.</span></span> <span data-ttu-id="5ef2a-130">The backup job creates a recovery point.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-130">The backup job creates a recovery point.</span></span> <span data-ttu-id="5ef2a-131">If it is the initial backup, then the recovery point is a full backup.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-131">If it is the initial backup, then the recovery point is a full backup.</span></span> <span data-ttu-id="5ef2a-132">Subsequent backups create an incremental copy.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-132">Subsequent backups create an incremental copy.</span></span>

```powershell
$namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureVM -Status Registered -FriendlyName "V2VM"
$item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType AzureVM
$job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
```

## <a name="delete-the-recovery-services-vault"></a><span data-ttu-id="5ef2a-133">Delete the Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="5ef2a-133">Delete the Recovery Services vault</span></span>

<span data-ttu-id="5ef2a-134">To delete a Recovery Services vault, you must first delete any recovery points in the vault, and then unregister the vault.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-134">To delete a Recovery Services vault, you must first delete any recovery points in the vault, and then unregister the vault.</span></span> <span data-ttu-id="5ef2a-135">The following commands detail these steps.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-135">The following commands detail these steps.</span></span> 


```powershell
$Cont = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureVM -Status Registered
$PI = Get-AzureRmRecoveryServicesBackupItem -Container $Cont[0] -WorkloadType AzureVm
Disable-AzureRmRecoveryServicesBackupProtection -RemoveRecoveryPoints $PI[0]
Unregister-AzureRmRecoveryServicesBackupContainer -Container $namedContainer
Remove-AzureRmRecoveryServicesVault -Vault $vault1
```

## <a name="troubleshooting-errors"></a><span data-ttu-id="5ef2a-136">Troubleshooting errors</span><span class="sxs-lookup"><span data-stu-id="5ef2a-136">Troubleshooting errors</span></span>
<span data-ttu-id="5ef2a-137">If you run into issues while backing up your virtual machine, see the [Back up Azure virtual machines troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-137">If you run into issues while backing up your virtual machine, see the [Back up Azure virtual machines troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ef2a-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ef2a-138">Next steps</span></span>
<span data-ttu-id="5ef2a-139">Now that you have protected your virtual machines, see the following articles to learn about management tasks, and how to restore virtual machines from a recovery point.</span><span class="sxs-lookup"><span data-stu-id="5ef2a-139">Now that you have protected your virtual machines, see the following articles to learn about management tasks, and how to restore virtual machines from a recovery point.</span></span>

* <span data-ttu-id="5ef2a-140">To modify the backup policy, see [Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines](backup-azure-vms-automation.md#create-a-protection-policy).</span><span class="sxs-lookup"><span data-stu-id="5ef2a-140">To modify the backup policy, see [Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines](backup-azure-vms-automation.md#create-a-protection-policy).</span></span>
* [<span data-ttu-id="5ef2a-141">Manage and monitor your virtual machines</span><span class="sxs-lookup"><span data-stu-id="5ef2a-141">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="5ef2a-142">Restore virtual machines</span><span class="sxs-lookup"><span data-stu-id="5ef2a-142">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
