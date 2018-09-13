---
title: Azure PowerShell Script Sample - Back up an Azure virtual machine | Microsoft Docs
description: Azure PowerShell Script Sample - Back up an Azure virtual machine
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
tags: ''
ms.assetid: ''
ms.service: backup
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 09/07/2017
ms.author: markgal
ms.custom: mvc
ms.openlocfilehash: 4376add4a2e51806bd5db228ad2fe2afcf2e4f57
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867286"
---
# <a name="back-up-an-encrypted-azure-virtual-machine-with-powershell"></a><span data-ttu-id="c9669-103">Back up an encrypted Azure virtual machine with PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9669-103">Back up an encrypted Azure virtual machine with PowerShell</span></span>

<span data-ttu-id="c9669-104">This script creates a Recovery Services vault with Geo-redundant storage (GRS) for an encrypted Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c9669-104">This script creates a Recovery Services vault with Geo-redundant storage (GRS) for an encrypted Azure virtual machine.</span></span> <span data-ttu-id="c9669-105">The default protection policy is applied to the vault.</span><span class="sxs-lookup"><span data-stu-id="c9669-105">The default protection policy is applied to the vault.</span></span> <span data-ttu-id="c9669-106">The policy generates a daily backup for the virtual machine, and retains each backup for 30 days.</span><span class="sxs-lookup"><span data-stu-id="c9669-106">The policy generates a daily backup for the virtual machine, and retains each backup for 30 days.</span></span> <span data-ttu-id="c9669-107">The script also triggers the initial recovery point for the virtual machine and retains that recovery point for 365 days.</span><span class="sxs-lookup"><span data-stu-id="c9669-107">The script also triggers the initial recovery point for the virtual machine and retains that recovery point for 365 days.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c9669-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="c9669-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/backup/backup-encrypted-vm/backup-encrypted-vm.ps1 "Back up encrypted virtual machine")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c9669-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="c9669-109">Clean up deployment</span></span> 

<span data-ttu-id="c9669-110">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="c9669-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c9669-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c9669-111">Script explanation</span></span>

<span data-ttu-id="c9669-112">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="c9669-112">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="c9669-113">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="c9669-113">Each item in the table links to command specific documentation.</span></span>


| <span data-ttu-id="c9669-114">Command</span><span class="sxs-lookup"><span data-stu-id="c9669-114">Command</span></span> | <span data-ttu-id="c9669-115">Notes</span><span class="sxs-lookup"><span data-stu-id="c9669-115">Notes</span></span> | 
|---|---| 
| [<span data-ttu-id="c9669-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c9669-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c9669-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="c9669-117">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="c9669-118">New-AzureRmRecoveryServicesVault</span><span class="sxs-lookup"><span data-stu-id="c9669-118">New-AzureRmRecoveryServicesVault</span></span>](/powershell/module/azurerm.recoveryservices/New-AzureRmRecoveryServicesVault) | <span data-ttu-id="c9669-119">Creates a recovery services vault to store backups.</span><span class="sxs-lookup"><span data-stu-id="c9669-119">Creates a recovery services vault to store backups.</span></span> | 
| [<span data-ttu-id="c9669-120">Set-AzureRmRecoveryServicesBackupProperties</span><span class="sxs-lookup"><span data-stu-id="c9669-120">Set-AzureRmRecoveryServicesBackupProperties</span></span>](/powershell/module/azurerm.recoveryservices/Set-AzureRmRecoveryServicesBackupProperties) | <span data-ttu-id="c9669-121">Sets backup storage properties on Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="c9669-121">Sets backup storage properties on Recovery Services vault.</span></span> | 
| [<span data-ttu-id="c9669-122">New-AzureRmRecoveryServicesBackupProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="c9669-122">New-AzureRmRecoveryServicesBackupProtectionPolicy</span></span>](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)| <span data-ttu-id="c9669-123">Creates protection policy using schedule policy and retention policy in Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="c9669-123">Creates protection policy using schedule policy and retention policy in Recovery Services vault.</span></span> | 
| [<span data-ttu-id="c9669-124">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="c9669-124">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="c9669-125">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span><span class="sxs-lookup"><span data-stu-id="c9669-125">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> | 
| [<span data-ttu-id="c9669-126">Enable-AzureRmRecoveryServicesBackupProtection</span><span class="sxs-lookup"><span data-stu-id="c9669-126">Enable-AzureRmRecoveryServicesBackupProtection</span></span>](/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection) | <span data-ttu-id="c9669-127">Enables backup for an item with a specified Backup protection policy.</span><span class="sxs-lookup"><span data-stu-id="c9669-127">Enables backup for an item with a specified Backup protection policy.</span></span> | 
| [<span data-ttu-id="c9669-128">Set-AzureRmRecoveryServicesBackupProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="c9669-128">Set-AzureRmRecoveryServicesBackupProtectionPolicy</span></span>](/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy)| <span data-ttu-id="c9669-129">Modifies an existing Backup protection policy.</span><span class="sxs-lookup"><span data-stu-id="c9669-129">Modifies an existing Backup protection policy.</span></span> | 
| [<span data-ttu-id="c9669-130">Backup-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="c9669-130">Backup-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem) | <span data-ttu-id="c9669-131">Starts a backup for a protected Azure Backup item that is not tied to the backup schedule.</span><span class="sxs-lookup"><span data-stu-id="c9669-131">Starts a backup for a protected Azure Backup item that is not tied to the backup schedule.</span></span> |
| [<span data-ttu-id="c9669-132">Wait-AzureRmRecoveryServicesBackupJob</span><span class="sxs-lookup"><span data-stu-id="c9669-132">Wait-AzureRmRecoveryServicesBackupJob</span></span>](/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob) | <span data-ttu-id="c9669-133">Waits for an Azure Backup job to finish.</span><span class="sxs-lookup"><span data-stu-id="c9669-133">Waits for an Azure Backup job to finish.</span></span> | 
| [<span data-ttu-id="c9669-134">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c9669-134">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c9669-135">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="c9669-135">Removes a resource group and all resources contained within.</span></span> | 

## <a name="next-steps"></a><span data-ttu-id="c9669-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="c9669-136">Next steps</span></span>

<span data-ttu-id="c9669-137">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9669-137">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

