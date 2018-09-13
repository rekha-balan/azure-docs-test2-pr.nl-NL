---
title: Validate an Azure Stack backup using the ASDK | Microsoft Docs
description: How to validate an Azure Stack integerated systems backup using the ASDK.
services: azure-stack
author: jeffgilb
manager: femila
cloud: azure-stack
ms.service: azure-stack
ms.topic: article
ms.date: 09/05/2018
ms.author: jeffgilb
ms.reviewer: hectorl
ms.openlocfilehash: 6fa3ba36dca45d5b99c6b5f2ba24367bcd077024
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969058"
---
# <a name="use-the-asdk-to-validate-an-azure-stack-backup"></a><span data-ttu-id="de032-103">Use the ASDK to validate an Azure Stack backup</span><span class="sxs-lookup"><span data-stu-id="de032-103">Use the ASDK to validate an Azure Stack backup</span></span>
<span data-ttu-id="de032-104">After deploying Azure Stack and provisioning user resources such as offers, plans, quotas, and subscriptions, you should [enable Azure Stack infrastructure backup](..\azure-stack-backup-enable-backup-console.md).</span><span class="sxs-lookup"><span data-stu-id="de032-104">After deploying Azure Stack and provisioning user resources such as offers, plans, quotas, and subscriptions, you should [enable Azure Stack infrastructure backup](..\azure-stack-backup-enable-backup-console.md).</span></span> <span data-ttu-id="de032-105">Scheduling and running regular infrastructure backups will ensure that infrastructure management data is not lost if there is a catastrophic hardware or service failure.</span><span class="sxs-lookup"><span data-stu-id="de032-105">Scheduling and running regular infrastructure backups will ensure that infrastructure management data is not lost if there is a catastrophic hardware or service failure.</span></span>

> [!TIP]
> <span data-ttu-id="de032-106">We recommended that you [run an on-demand backup](..\azure-stack-backup-back-up-azure-stack.md) before beginning this procedure to ensure you have a copy of the latest infrastrcuture data available.</span><span class="sxs-lookup"><span data-stu-id="de032-106">We recommended that you [run an on-demand backup](..\azure-stack-backup-back-up-azure-stack.md) before beginning this procedure to ensure you have a copy of the latest infrastrcuture data available.</span></span> <span data-ttu-id="de032-107">Make sure to capture the backup ID after the backup successfully completes.</span><span class="sxs-lookup"><span data-stu-id="de032-107">Make sure to capture the backup ID after the backup successfully completes.</span></span> <span data-ttu-id="de032-108">This ID will be required during cloud recovery.</span><span class="sxs-lookup"><span data-stu-id="de032-108">This ID will be required during cloud recovery.</span></span> 

<span data-ttu-id="de032-109">Azure Stack infrastructure backups contain important data about your cloud that can be restored during redeployment of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="de032-109">Azure Stack infrastructure backups contain important data about your cloud that can be restored during redeployment of Azure Stack.</span></span> <span data-ttu-id="de032-110">You can use the ASDK to validate these backups without impacting your production cloud.</span><span class="sxs-lookup"><span data-stu-id="de032-110">You can use the ASDK to validate these backups without impacting your production cloud.</span></span> 

<span data-ttu-id="de032-111">Validating backups on ASDK is supported for the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="de032-111">Validating backups on ASDK is supported for the following scenarios:</span></span>

|<span data-ttu-id="de032-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="de032-112">Scenario</span></span>|<span data-ttu-id="de032-113">Purpose</span><span class="sxs-lookup"><span data-stu-id="de032-113">Purpose</span></span>|
|-----|-----|
|<span data-ttu-id="de032-114">Validate infrastructure backups from an integrated solution.</span><span class="sxs-lookup"><span data-stu-id="de032-114">Validate infrastructure backups from an integrated solution.</span></span>|<span data-ttu-id="de032-115">Short lived validation that the data in the backup is valid.</span><span class="sxs-lookup"><span data-stu-id="de032-115">Short lived validation that the data in the backup is valid.</span></span>|
|<span data-ttu-id="de032-116">Learn the end-to-end recovery workflow.</span><span class="sxs-lookup"><span data-stu-id="de032-116">Learn the end-to-end recovery workflow.</span></span>|<span data-ttu-id="de032-117">Use ASDK to validate the entire backup and restore experience.</span><span class="sxs-lookup"><span data-stu-id="de032-117">Use ASDK to validate the entire backup and restore experience.</span></span>|
|     |     |

<span data-ttu-id="de032-118">The following scenario **is not** supported when validating backups on the ASDK:</span><span class="sxs-lookup"><span data-stu-id="de032-118">The following scenario **is not** supported when validating backups on the ASDK:</span></span>

|<span data-ttu-id="de032-119">Scenario</span><span class="sxs-lookup"><span data-stu-id="de032-119">Scenario</span></span>|<span data-ttu-id="de032-120">Purpose</span><span class="sxs-lookup"><span data-stu-id="de032-120">Purpose</span></span>|
|-----|-----|
|<span data-ttu-id="de032-121">ASDK build to build backup and restore.</span><span class="sxs-lookup"><span data-stu-id="de032-121">ASDK build to build backup and restore.</span></span>|<span data-ttu-id="de032-122">Restore backup data from a previous version of the ASDK to a newer version.</span><span class="sxs-lookup"><span data-stu-id="de032-122">Restore backup data from a previous version of the ASDK to a newer version.</span></span>|
|     |     |


## <a name="cloud-recovery-deployment"></a><span data-ttu-id="de032-123">Cloud recovery deployment</span><span class="sxs-lookup"><span data-stu-id="de032-123">Cloud recovery deployment</span></span>
<span data-ttu-id="de032-124">Infrastructure backups from your integrated systems deployment can be validated by performing a cloud recovery deployment of the ASDK.</span><span class="sxs-lookup"><span data-stu-id="de032-124">Infrastructure backups from your integrated systems deployment can be validated by performing a cloud recovery deployment of the ASDK.</span></span> <span data-ttu-id="de032-125">In this type of deployment, specific service data is restored from backup after the ASDK is installed on the host computer.</span><span class="sxs-lookup"><span data-stu-id="de032-125">In this type of deployment, specific service data is restored from backup after the ASDK is installed on the host computer.</span></span>



### <a name="cloud-recovery-prerequisites"></a><span data-ttu-id="de032-126">Cloud recovery prerequisites</span><span class="sxs-lookup"><span data-stu-id="de032-126">Cloud recovery prerequisites</span></span>
<span data-ttu-id="de032-127">Before starting a cloud recovery deployment of the ASDK, ensure that you have the following information:</span><span class="sxs-lookup"><span data-stu-id="de032-127">Before starting a cloud recovery deployment of the ASDK, ensure that you have the following information:</span></span>

|<span data-ttu-id="de032-128">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="de032-128">Prerequisite</span></span>|<span data-ttu-id="de032-129">Description</span><span class="sxs-lookup"><span data-stu-id="de032-129">Description</span></span>|
|-----|-----|
|<span data-ttu-id="de032-130">Backup share path.</span><span class="sxs-lookup"><span data-stu-id="de032-130">Backup share path.</span></span>|<span data-ttu-id="de032-131">The UNC file share path of the latest Azure Stack backup that will be used to recover Azure Stack infrastructure information.</span><span class="sxs-lookup"><span data-stu-id="de032-131">The UNC file share path of the latest Azure Stack backup that will be used to recover Azure Stack infrastructure information.</span></span> <span data-ttu-id="de032-132">This local share will be created during the cloud recovery deployment process.</span><span class="sxs-lookup"><span data-stu-id="de032-132">This local share will be created during the cloud recovery deployment process.</span></span>|
|<span data-ttu-id="de032-133">Backup encryption key.</span><span class="sxs-lookup"><span data-stu-id="de032-133">Backup encryption key.</span></span>|<span data-ttu-id="de032-134">The encryption key that was used to schedule infrastructure backup to run using the Azure Stack administration portal.</span><span class="sxs-lookup"><span data-stu-id="de032-134">The encryption key that was used to schedule infrastructure backup to run using the Azure Stack administration portal.</span></span>|
|<span data-ttu-id="de032-135">Backup ID to restore.</span><span class="sxs-lookup"><span data-stu-id="de032-135">Backup ID to restore.</span></span>|<span data-ttu-id="de032-136">The backup ID, in the alphanumeric form of "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", that identifies the backup to be restored during cloud recovery.</span><span class="sxs-lookup"><span data-stu-id="de032-136">The backup ID, in the alphanumeric form of "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", that identifies the backup to be restored during cloud recovery.</span></span>|
|<span data-ttu-id="de032-137">Time server IP.</span><span class="sxs-lookup"><span data-stu-id="de032-137">Time server IP.</span></span>|<span data-ttu-id="de032-138">A valid time server IP, such as 132.163.97.2, is required for Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="de032-138">A valid time server IP, such as 132.163.97.2, is required for Azure Stack deployment.</span></span>|
|<span data-ttu-id="de032-139">External certificate password.</span><span class="sxs-lookup"><span data-stu-id="de032-139">External certificate password.</span></span>|<span data-ttu-id="de032-140">The password for the external certificate used by Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="de032-140">The password for the external certificate used by Azure Stack.</span></span> <span data-ttu-id="de032-141">The CA backup contains external certificates that need to be restored with this password.</span><span class="sxs-lookup"><span data-stu-id="de032-141">The CA backup contains external certificates that need to be restored with this password.</span></span>|
|     |     | 

## <a name="prepare-the-host-computer"></a><span data-ttu-id="de032-142">Prepare the host computer</span><span class="sxs-lookup"><span data-stu-id="de032-142">Prepare the host computer</span></span> 
<span data-ttu-id="de032-143">As in a normal ASDK deployment, the ASDK host system environment must be prepared for installation.</span><span class="sxs-lookup"><span data-stu-id="de032-143">As in a normal ASDK deployment, the ASDK host system environment must be prepared for installation.</span></span> <span data-ttu-id="de032-144">When the development kit host computer has been prepared, it will boot from the CloudBuilder.vhdx virtual machine hard drive to begin ASDK deployment.</span><span class="sxs-lookup"><span data-stu-id="de032-144">When the development kit host computer has been prepared, it will boot from the CloudBuilder.vhdx virtual machine hard drive to begin ASDK deployment.</span></span>

<span data-ttu-id="de032-145">On the ASDK host computer, download a new cloudbuilder.vhdx corresponding to the same version of Azure Stack that was backed up, and follow the instructions for [preparing the ASDK host computer](asdk-prepare-host.md).</span><span class="sxs-lookup"><span data-stu-id="de032-145">On the ASDK host computer, download a new cloudbuilder.vhdx corresponding to the same version of Azure Stack that was backed up, and follow the instructions for [preparing the ASDK host computer](asdk-prepare-host.md).</span></span>

<span data-ttu-id="de032-146">After the host server restarts from the cloudbuilder.vhdx, you must create a file share and copy your backup data into.</span><span class="sxs-lookup"><span data-stu-id="de032-146">After the host server restarts from the cloudbuilder.vhdx, you must create a file share and copy your backup data into.</span></span> <span data-ttu-id="de032-147">The file share should be accessible to the account running setup; Administrator in these example PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="de032-147">The file share should be accessible to the account running setup; Administrator in these example PowerShell commands:</span></span> 

```powershell
$shares = New-Item -Path "c:\" -Name "Shares" -ItemType "directory"
$azsbackupshare = New-Item -Path $shares.FullName -Name "AzSBackups" -ItemType "directory"
New-SmbShare -Path $azsbackupshare.FullName -FullAccess ($env:computername + "\Administrator")  -Name "AzSBackups"
```

<span data-ttu-id="de032-148">Next, copy your latest Azure Stack backup files to the newly created share.</span><span class="sxs-lookup"><span data-stu-id="de032-148">Next, copy your latest Azure Stack backup files to the newly created share.</span></span> <span data-ttu-id="de032-149">The folder structure within the share should be: `\\<ComputerName>\AzSBackups\MASBackup\<BackupID>\`.</span><span class="sxs-lookup"><span data-stu-id="de032-149">The folder structure within the share should be: `\\<ComputerName>\AzSBackups\MASBackup\<BackupID>\`.</span></span>

## <a name="deploy-the-asdk-in-cloud-recovery-mode"></a><span data-ttu-id="de032-150">Deploy the ASDK in cloud recovery mode</span><span class="sxs-lookup"><span data-stu-id="de032-150">Deploy the ASDK in cloud recovery mode</span></span>
<span data-ttu-id="de032-151">The **InstallAzureStackPOC.ps1** script is used to initiate cloud recovery.</span><span class="sxs-lookup"><span data-stu-id="de032-151">The **InstallAzureStackPOC.ps1** script is used to initiate cloud recovery.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="de032-152">ASDK installation supports exactly one network interface card (NIC) for networking.</span><span class="sxs-lookup"><span data-stu-id="de032-152">ASDK installation supports exactly one network interface card (NIC) for networking.</span></span> <span data-ttu-id="de032-153">If you have multiple NICs, make sure that only one is enabled (and all others are disabled) before running the deployment script.</span><span class="sxs-lookup"><span data-stu-id="de032-153">If you have multiple NICs, make sure that only one is enabled (and all others are disabled) before running the deployment script.</span></span>

<span data-ttu-id="de032-154">Modify the following PowerShell commands for your environment and run them to deploy the ASDK in cloud recovery mode:</span><span class="sxs-lookup"><span data-stu-id="de032-154">Modify the following PowerShell commands for your environment and run them to deploy the ASDK in cloud recovery mode:</span></span>

```powershell
cd C:\CloudDeployment\Setup     
$adminPass = Get-Credential Administrator
$key = ConvertTo-SecureString "<Your backup encryption key>" -AsPlainText -Force ` 
$certPass = Read-Host -AsSecureString  

.\InstallAzureStackPOC.ps1 -AdminPassword $adminpass.Password -BackupStorePath ("\\" + $env:COMPUTERNAME + "\AzSBackups") `
-BackupEncryptionKeyBase64 $key -BackupStoreCredential $adminPass -BackupId "<Backup ID to restore>" `
-TimeServer "<Valid time server IP>" -ExternalCertPassword $certPass
```

## <a name="restore-infrastructure-data-from-backup"></a><span data-ttu-id="de032-155">Restore infrastructure data from backup</span><span class="sxs-lookup"><span data-stu-id="de032-155">Restore infrastructure data from backup</span></span>
<span data-ttu-id="de032-156">After a successful cloud recovery deployment, you need to complete the restore using the **Restore-AzureStack** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="de032-156">After a successful cloud recovery deployment, you need to complete the restore using the **Restore-AzureStack** cmdlet.</span></span> 

<span data-ttu-id="de032-157">After logging in as the Azure Stack operator, [install Azure Stack PowerShell](asdk-post-deploy.md#install-azure-stack-powershell) and then, substituting your Backup ID for the `Name` parameter, run the following command:</span><span class="sxs-lookup"><span data-stu-id="de032-157">After logging in as the Azure Stack operator, [install Azure Stack PowerShell](asdk-post-deploy.md#install-azure-stack-powershell) and then, substituting your Backup ID for the `Name` parameter, run the following command:</span></span>

```powershell
Restore-AzsBackup -Name "<BackupID>"
```
<span data-ttu-id="de032-158">Wait 60 minutes after calling this cmdlet to start verification of backup data on the cloud recovered ASDK.</span><span class="sxs-lookup"><span data-stu-id="de032-158">Wait 60 minutes after calling this cmdlet to start verification of backup data on the cloud recovered ASDK.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de032-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="de032-159">Next steps</span></span>
[<span data-ttu-id="de032-160">Register Azure Stack</span><span class="sxs-lookup"><span data-stu-id="de032-160">Register Azure Stack</span></span>](asdk-register.md)

