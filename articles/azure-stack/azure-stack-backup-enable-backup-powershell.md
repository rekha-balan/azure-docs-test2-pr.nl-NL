---
title: Enable Backup for Azure Stack with PowerShell | Microsoft Docs
description: Enable the Infrastructure Backup Service with Windows PowerShell so that Azure Stack can be restored if there is a failure.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2018
ms.author: jeffgilb
ms.reviewer: hectorl
ms.openlocfilehash: 8fe7f0ddd630cfca0242af6cc1d728bdef163352
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857735"
---
# <a name="enable-backup-for-azure-stack-with-powershell"></a><span data-ttu-id="48ff5-103">Enable Backup for Azure Stack with PowerShell</span><span class="sxs-lookup"><span data-stu-id="48ff5-103">Enable Backup for Azure Stack with PowerShell</span></span>

<span data-ttu-id="48ff5-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="48ff5-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="48ff5-105">Enable the Infrastructure Backup Service with Windows PowerShell so take periodic backups of:</span><span class="sxs-lookup"><span data-stu-id="48ff5-105">Enable the Infrastructure Backup Service with Windows PowerShell so take periodic backups of:</span></span>
 - <span data-ttu-id="48ff5-106">Internal identity service and root certificate</span><span class="sxs-lookup"><span data-stu-id="48ff5-106">Internal identity service and root certificate</span></span>
 - <span data-ttu-id="48ff5-107">User plans, offers, subscriptions</span><span class="sxs-lookup"><span data-stu-id="48ff5-107">User plans, offers, subscriptions</span></span>
 - <span data-ttu-id="48ff5-108">Keyvault secrets</span><span class="sxs-lookup"><span data-stu-id="48ff5-108">Keyvault secrets</span></span>
 - <span data-ttu-id="48ff5-109">User RBAC roles and policies</span><span class="sxs-lookup"><span data-stu-id="48ff5-109">User RBAC roles and policies</span></span>

<span data-ttu-id="48ff5-110">You can access the PowerShell cmdlets to enable backup, start backup, and get backup information via the operator management endpoint.</span><span class="sxs-lookup"><span data-stu-id="48ff5-110">You can access the PowerShell cmdlets to enable backup, start backup, and get backup information via the operator management endpoint.</span></span>

## <a name="prepare-powershell-environment"></a><span data-ttu-id="48ff5-111">Prepare PowerShell environment</span><span class="sxs-lookup"><span data-stu-id="48ff5-111">Prepare PowerShell environment</span></span>

<span data-ttu-id="48ff5-112">For instructions on configuring the PowerShell environment, see [Install PowerShell for Azure Stack ](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="48ff5-112">For instructions on configuring the PowerShell environment, see [Install PowerShell for Azure Stack ](azure-stack-powershell-install.md).</span></span> <span data-ttu-id="48ff5-113">To sign in to Azure Stack, see [Configure the operator environment and sign in to Azure Stack](azure-stack-powershell-configure-admin.md).</span><span class="sxs-lookup"><span data-stu-id="48ff5-113">To sign in to Azure Stack, see [Configure the operator environment and sign in to Azure Stack](azure-stack-powershell-configure-admin.md).</span></span>

## <a name="provide-the-backup-share-credentials-and-encryption-key-to-enable-backup"></a><span data-ttu-id="48ff5-114">Provide the backup share, credentials, and encryption key to enable backup</span><span class="sxs-lookup"><span data-stu-id="48ff5-114">Provide the backup share, credentials, and encryption key to enable backup</span></span>

<span data-ttu-id="48ff5-115">In the same PowerShell session, edit the following PowerShell script by adding the variables for your environment.</span><span class="sxs-lookup"><span data-stu-id="48ff5-115">In the same PowerShell session, edit the following PowerShell script by adding the variables for your environment.</span></span> <span data-ttu-id="48ff5-116">Run the updated script to provide the backup share, credentials, and encryption key to the Infrastructure Backup Service.</span><span class="sxs-lookup"><span data-stu-id="48ff5-116">Run the updated script to provide the backup share, credentials, and encryption key to the Infrastructure Backup Service.</span></span>

| <span data-ttu-id="48ff5-117">Variable</span><span class="sxs-lookup"><span data-stu-id="48ff5-117">Variable</span></span>        | <span data-ttu-id="48ff5-118">Description</span><span class="sxs-lookup"><span data-stu-id="48ff5-118">Description</span></span>   |
|---              |---                                        |
| <span data-ttu-id="48ff5-119">$username</span><span class="sxs-lookup"><span data-stu-id="48ff5-119">$username</span></span>       | <span data-ttu-id="48ff5-120">Type the **Username** using the domain and username for the shared drive location with sufficient access to read and write files.</span><span class="sxs-lookup"><span data-stu-id="48ff5-120">Type the **Username** using the domain and username for the shared drive location with sufficient access to read and write files.</span></span> <span data-ttu-id="48ff5-121">For example, `Contoso\backupshareuser`.</span><span class="sxs-lookup"><span data-stu-id="48ff5-121">For example, `Contoso\backupshareuser`.</span></span> |
| <span data-ttu-id="48ff5-122">$password</span><span class="sxs-lookup"><span data-stu-id="48ff5-122">$password</span></span>       | <span data-ttu-id="48ff5-123">Type the **Password** for the user.</span><span class="sxs-lookup"><span data-stu-id="48ff5-123">Type the **Password** for the user.</span></span> |
| <span data-ttu-id="48ff5-124">$sharepath</span><span class="sxs-lookup"><span data-stu-id="48ff5-124">$sharepath</span></span>      | <span data-ttu-id="48ff5-125">Type the path to the **Backup storage location**.</span><span class="sxs-lookup"><span data-stu-id="48ff5-125">Type the path to the **Backup storage location**.</span></span> <span data-ttu-id="48ff5-126">You must use a Universal Naming Convention (UNC) string for the path to a file share hosted on a separate device.</span><span class="sxs-lookup"><span data-stu-id="48ff5-126">You must use a Universal Naming Convention (UNC) string for the path to a file share hosted on a separate device.</span></span> <span data-ttu-id="48ff5-127">A UNC string specifies the location of resources such as shared files or devices.</span><span class="sxs-lookup"><span data-stu-id="48ff5-127">A UNC string specifies the location of resources such as shared files or devices.</span></span> <span data-ttu-id="48ff5-128">To ensure availability of the backup data, the  device should be in a separate location.</span><span class="sxs-lookup"><span data-stu-id="48ff5-128">To ensure availability of the backup data, the  device should be in a separate location.</span></span> |
| <span data-ttu-id="48ff5-129">$frequencyInHours</span><span class="sxs-lookup"><span data-stu-id="48ff5-129">$frequencyInHours</span></span> | <span data-ttu-id="48ff5-130">The frequency in hours determines how often backups are created.</span><span class="sxs-lookup"><span data-stu-id="48ff5-130">The frequency in hours determines how often backups are created.</span></span> <span data-ttu-id="48ff5-131">The default value is 12.</span><span class="sxs-lookup"><span data-stu-id="48ff5-131">The default value is 12.</span></span> <span data-ttu-id="48ff5-132">Scheduler supports a maximum of 12 and a minimum of 4.</span><span class="sxs-lookup"><span data-stu-id="48ff5-132">Scheduler supports a maximum of 12 and a minimum of 4.</span></span>|
| <span data-ttu-id="48ff5-133">$retentionPeriodInDays</span><span class="sxs-lookup"><span data-stu-id="48ff5-133">$retentionPeriodInDays</span></span> | <span data-ttu-id="48ff5-134">The retention period in days determines how many days of backups are preserved on the external location.</span><span class="sxs-lookup"><span data-stu-id="48ff5-134">The retention period in days determines how many days of backups are preserved on the external location.</span></span> <span data-ttu-id="48ff5-135">The default value is 7.</span><span class="sxs-lookup"><span data-stu-id="48ff5-135">The default value is 7.</span></span> <span data-ttu-id="48ff5-136">Scheduler supports a maximum of 14 and a minimum of 2.</span><span class="sxs-lookup"><span data-stu-id="48ff5-136">Scheduler supports a maximum of 14 and a minimum of 2.</span></span> <span data-ttu-id="48ff5-137">Backups older than the retention period get automatically deleted from the external location.</span><span class="sxs-lookup"><span data-stu-id="48ff5-137">Backups older than the retention period get automatically deleted from the external location.</span></span>|
|     |     |

   ```powershell
    # Example username:
    $username = "domain\backupadmin"
    # Example share path:
    $sharepath = "\\serverIP\AzSBackupStore\contoso.com\seattle"
   
    $password = Read-Host -Prompt ("Password for: " + $username) -AsSecureString
    
    # The encryption key is generated using the New-AzsEncryptionKeyBase64 cmdlet provided in Azure Stack PowerShell.
    # Make sure to store your encryption key in a secure location after it is generated.
    $Encryptionkey = New-AzsEncryptionKeyBase64
    $key = ConvertTo-SecureString -String ($Encryptionkey) -AsPlainText -Force

    Set-AzsBackupShare -BackupShare $sharepath -Username $username -Password $password -EncryptionKey $key
   ```
   
##  <a name="confirm-backup-settings"></a><span data-ttu-id="48ff5-138">Confirm backup settings</span><span class="sxs-lookup"><span data-stu-id="48ff5-138">Confirm backup settings</span></span>

<span data-ttu-id="48ff5-139">In the same PowerShell session, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="48ff5-139">In the same PowerShell session, run the following commands:</span></span>

   ```powershell
    Get-AzsBackupLocation | Select-Object -Property Path, UserName
   ```

<span data-ttu-id="48ff5-140">The result should look like the following example output:</span><span class="sxs-lookup"><span data-stu-id="48ff5-140">The result should look like the following example output:</span></span>

   ```powershell
    Path                        : \\serverIP\AzsBackupStore\contoso.com\seattle
    UserName                    : domain\backupadmin
   ```

## <a name="update-backup-settings"></a><span data-ttu-id="48ff5-141">Update backup settings</span><span class="sxs-lookup"><span data-stu-id="48ff5-141">Update backup settings</span></span>
<span data-ttu-id="48ff5-142">In the same PowerShell session, you can update the default values for retention period and frequency for backups.</span><span class="sxs-lookup"><span data-stu-id="48ff5-142">In the same PowerShell session, you can update the default values for retention period and frequency for backups.</span></span> 

   ```powershell
    #Set the backup frequency and retention period values.
    $frequencyInHours = 10
    $retentionPeriodInDays = 5

    Set-AzsBackupShare -BackupFrequencyInHours $frequencyInHours -BackupRetentionPeriodInDays $retentionPeriodInDays
    Get-AzsBackupLocation | Select-Object -Property Path, UserName, AvailableCapacity, BackupFrequencyInHours, BackupRetentionPeriodInDays
   ```

<span data-ttu-id="48ff5-143">The result should look like the following example output:</span><span class="sxs-lookup"><span data-stu-id="48ff5-143">The result should look like the following example output:</span></span>

   ```powershell
    Path                        : \\serverIP\AzsBackupStore\contoso.com\seattle
    UserName                    : domain\backupadmin
    AvailableCapacity           : 60 GB
    BackupFrequencyInHours      : 10
    BackupRetentionPeriodInDays : 5
   ```

## <a name="next-steps"></a><span data-ttu-id="48ff5-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="48ff5-144">Next steps</span></span>

 - <span data-ttu-id="48ff5-145">Learn to run a backup, see [Back up Azure Stack](azure-stack-backup-back-up-azure-stack.md ).</span><span class="sxs-lookup"><span data-stu-id="48ff5-145">Learn to run a backup, see [Back up Azure Stack](azure-stack-backup-back-up-azure-stack.md ).</span></span>  
 - <span data-ttu-id="48ff5-146">Learn to verify that your backup ran, see [Confirm backup completed in administration portal](azure-stack-backup-back-up-azure-stack.md ).</span><span class="sxs-lookup"><span data-stu-id="48ff5-146">Learn to verify that your backup ran, see [Confirm backup completed in administration portal](azure-stack-backup-back-up-azure-stack.md ).</span></span>
