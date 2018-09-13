---
title: Restore Key Vault key and secret for encrypted VMs using Azure Backup | Microsoft Docs
description: Learn how to restore Key Vault key and secret in Azure Backup using PowerShell
services: backup
documentationcenter: ''
author: JPallavi
manager: vijayts
editor: ''
ms.assetid: 45214083-d5fc-4eb3-a367-0239dc59e0f6
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ddb9e7909eb4ab97204059d21690795ceb6ff9e8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662335"
---
# <a name="restore-an-encrypted-virtual-machine-from-an-azure-backup-recovery-point"></a><span data-ttu-id="1d673-103">Restore an encrypted virtual machine from an Azure Backup recovery point</span><span class="sxs-lookup"><span data-stu-id="1d673-103">Restore an encrypted virtual machine from an Azure Backup recovery point</span></span>
<span data-ttu-id="1d673-104">This article talks about using Azure VM Backup to perform restore of encrypted Azure VMs, if your key and secret do not exist in the key vault.</span><span class="sxs-lookup"><span data-stu-id="1d673-104">This article talks about using Azure VM Backup to perform restore of encrypted Azure VMs, if your key and secret do not exist in the key vault.</span></span> <span data-ttu-id="1d673-105">These steps can also be used if you want to maintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for the restored VM.</span><span class="sxs-lookup"><span data-stu-id="1d673-105">These steps can also be used if you want to maintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for the restored VM.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="1d673-106">Pre-requisites</span><span class="sxs-lookup"><span data-stu-id="1d673-106">Pre-requisites</span></span>
1. <span data-ttu-id="1d673-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="1d673-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="1d673-108">Refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how to backup encrypted Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="1d673-108">Refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how to backup encrypted Azure VMs.</span></span>
2. <span data-ttu-id="1d673-109">**Configure Azure Key Vault** – Ensure that key vault to which keys and secrets need to be restored is already present.</span><span class="sxs-lookup"><span data-stu-id="1d673-109">**Configure Azure Key Vault** – Ensure that key vault to which keys and secrets need to be restored is already present.</span></span> <span data-ttu-id="1d673-110">Refer the article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span><span class="sxs-lookup"><span data-stu-id="1d673-110">Refer the article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>

## <a name="setup-recovery-services-vault"></a><span data-ttu-id="1d673-111">Setup recovery services vault</span><span class="sxs-lookup"><span data-stu-id="1d673-111">Setup recovery services vault</span></span>
<span data-ttu-id="1d673-112">Use the following steps to log in to PowerShell and set recovery services vault context</span><span class="sxs-lookup"><span data-stu-id="1d673-112">Use the following steps to log in to PowerShell and set recovery services vault context</span></span>

### <a name="log-in-to-azure-powershell"></a><span data-ttu-id="1d673-113">Log in to Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d673-113">Log in to Azure PowerShell</span></span>
<span data-ttu-id="1d673-114">Log in to Azure account using the following cmdlet</span><span class="sxs-lookup"><span data-stu-id="1d673-114">Log in to Azure account using the following cmdlet</span></span>

```
PS C:\> Login-AzureRmAccount
```

### <a name="set-recovery-services-vault-context"></a><span data-ttu-id="1d673-115">Set recovery services vault context</span><span class="sxs-lookup"><span data-stu-id="1d673-115">Set recovery services vault context</span></span>
<span data-ttu-id="1d673-116">Once logged in, use the following cmdlet to get the list of your available subscriptions</span><span class="sxs-lookup"><span data-stu-id="1d673-116">Once logged in, use the following cmdlet to get the list of your available subscriptions</span></span>

```
PS C:\> Get-AzureRmSubscription
```

<span data-ttu-id="1d673-117">Select the subscription in which resources are available</span><span class="sxs-lookup"><span data-stu-id="1d673-117">Select the subscription in which resources are available</span></span>

```
PS C:\> Set-AzureRmContext -SubscriptionId "<subscription-id>"
```

<span data-ttu-id="1d673-118">Set the vault context using Recovery Services vault where backup was enabled for encrypted VMs</span><span class="sxs-lookup"><span data-stu-id="1d673-118">Set the vault context using Recovery Services vault where backup was enabled for encrypted VMs</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -ResourceGroupName "<rg-name>" -Name "<rs-vault-name>" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="get-recovery-point"></a><span data-ttu-id="1d673-119">Get recovery point</span><span class="sxs-lookup"><span data-stu-id="1d673-119">Get recovery point</span></span>
<span data-ttu-id="1d673-120">Select container in the vault that represents encrypted Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="1d673-120">Select container in the vault that represents encrypted Azure virtual machine</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -Name "<vm-name>"
```

<span data-ttu-id="1d673-121">Using this container, get back up item for the corresponding virtual machine</span><span class="sxs-lookup"><span data-stu-id="1d673-121">Using this container, get back up item for the corresponding virtual machine</span></span>

```
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
```

<span data-ttu-id="1d673-122">Get an array of recovery points for the selected backup item in the variable rp</span><span class="sxs-lookup"><span data-stu-id="1d673-122">Get an array of recovery points for the selected backup item in the variable rp</span></span>

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
```

## <a name="restore-encrypted-virtual-machine"></a><span data-ttu-id="1d673-123">Restore encrypted virtual machine</span><span class="sxs-lookup"><span data-stu-id="1d673-123">Restore encrypted virtual machine</span></span>
<span data-ttu-id="1d673-124">Use the following steps to restore encrypted VM, its key and secret.</span><span class="sxs-lookup"><span data-stu-id="1d673-124">Use the following steps to restore encrypted VM, its key and secret.</span></span>

### <a name="restore-key"></a><span data-ttu-id="1d673-125">Restore key</span><span class="sxs-lookup"><span data-stu-id="1d673-125">Restore key</span></span>
<span data-ttu-id="1d673-126">The array $rp above, is sorted in reverse order of time with the latest recovery point at index 0.</span><span class="sxs-lookup"><span data-stu-id="1d673-126">The array $rp above, is sorted in reverse order of time with the latest recovery point at index 0.</span></span> <span data-ttu-id="1d673-127">For example: $rp[0] selects the latest recovery point.</span><span class="sxs-lookup"><span data-stu-id="1d673-127">For example: $rp[0] selects the latest recovery point.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation "C:\Users\downloads"
```

> [!NOTE]
> <span data-ttu-id="1d673-128">After this cmdlet runs successfully, a blob file gets generated in the specified folder on the machine where it is run.</span><span class="sxs-lookup"><span data-stu-id="1d673-128">After this cmdlet runs successfully, a blob file gets generated in the specified folder on the machine where it is run.</span></span> <span data-ttu-id="1d673-129">This blob file represents Key Encrypted Key in encrypted form.</span><span class="sxs-lookup"><span data-stu-id="1d673-129">This blob file represents Key Encrypted Key in encrypted form.</span></span>
>
>

<span data-ttu-id="1d673-130">Restore key back to the key vault using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1d673-130">Restore key back to the key vault using the following cmdlet.</span></span>

```
PS C:\> Restore-AzureKeyVaultKey -VaultName "contosokeyvault" -InputFile "C:\Users\downloads\key.blob"
```

### <a name="restore-secret"></a><span data-ttu-id="1d673-131">Restore secret</span><span class="sxs-lookup"><span data-stu-id="1d673-131">Restore secret</span></span>
<span data-ttu-id="1d673-132">Restore secret data from recovery point obtained above</span><span class="sxs-lookup"><span data-stu-id="1d673-132">Restore secret data from recovery point obtained above</span></span>

```
PS C:\> $rp1.KeyAndSecretDetails.SecretUrl

https://contosokeyvault.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/20aaae9eaa99996d89d99a29990d999a
```

> [!NOTE]
> <span data-ttu-id="1d673-133">The text before vault.azure.net represents original key vault name.</span><span class="sxs-lookup"><span data-stu-id="1d673-133">The text before vault.azure.net represents original key vault name.</span></span> <span data-ttu-id="1d673-134">The text after secrets/ represents secret name.</span><span class="sxs-lookup"><span data-stu-id="1d673-134">The text after secrets/ represents secret name.</span></span>
>
>

<span data-ttu-id="1d673-135">Get the secret name and value from the output of the cmdlet run above, in case you want to use the same secret name.</span><span class="sxs-lookup"><span data-stu-id="1d673-135">Get the secret name and value from the output of the cmdlet run above, in case you want to use the same secret name.</span></span> <span data-ttu-id="1d673-136">In other cases, $secretname below should be updated to use the new secret name.</span><span class="sxs-lookup"><span data-stu-id="1d673-136">In other cases, $secretname below should be updated to use the new secret name.</span></span>

```
PS C:\> $secretname = "B3284AAA-DAAA-4AAA-B393-60CAA848AAAA"
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
```

<span data-ttu-id="1d673-137">Set tags for the secret, in case VM needs to be restored as well.</span><span class="sxs-lookup"><span data-stu-id="1d673-137">Set tags for the secret, in case VM needs to be restored as well.</span></span> <span data-ttu-id="1d673-138">For the tag DiskEncryptionKeyFileName, value should contain name of the secret you plan to use.</span><span class="sxs-lookup"><span data-stu-id="1d673-138">For the tag DiskEncryptionKeyFileName, value should contain name of the secret you plan to use.</span></span>

```
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://contosokeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
```

> [!NOTE]
> <span data-ttu-id="1d673-139">Value for DiskEncryptionKeyFileName is same as secret name obtained above.</span><span class="sxs-lookup"><span data-stu-id="1d673-139">Value for DiskEncryptionKeyFileName is same as secret name obtained above.</span></span> <span data-ttu-id="1d673-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring the keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span><span class="sxs-lookup"><span data-stu-id="1d673-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring the keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>    
>
>

<span data-ttu-id="1d673-141">Set the secret back to the key vault</span><span class="sxs-lookup"><span data-stu-id="1d673-141">Set the secret back to the key vault</span></span>

```
PS C:\> Set-AzureKeyVaultSecret -VaultName "contosokeyvault" -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  "Wrapped BEK"
```

### <a name="restore-virtual-machine"></a><span data-ttu-id="1d673-142">Restore virtual machine</span><span class="sxs-lookup"><span data-stu-id="1d673-142">Restore virtual machine</span></span>
<span data-ttu-id="1d673-143">The above PowerShell cmdlets help you restore key and secret back to the key vault, if you have backed up encrypted VM using Azure VM Backup.</span><span class="sxs-lookup"><span data-stu-id="1d673-143">The above PowerShell cmdlets help you restore key and secret back to the key vault, if you have backed up encrypted VM using Azure VM Backup.</span></span> <span data-ttu-id="1d673-144">After restoring them, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) to restore encrypted VMs.</span><span class="sxs-lookup"><span data-stu-id="1d673-144">After restoring them, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) to restore encrypted VMs.</span></span>
