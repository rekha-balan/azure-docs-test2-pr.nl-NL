---
title: Use PowerShell to manage Windows Server backups in Azure| Microsoft Docs
description: Deploy and manage Windows Server backups using PowerShell.
services: backup
documentationcenter: ''
author: saurabhsensharma
manager: shivamg
editor: ''
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: 79c174092c5aeeb46a1e662f045abbb9d495036f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555053"
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="30a49-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span><span class="sxs-lookup"><span data-stu-id="30a49-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [ARM](backup-client-automation.md)
> * [Classic](backup-client-automation-classic.md)
>
>

<span data-ttu-id="30a49-106">This article shows you how to use PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span><span class="sxs-lookup"><span data-stu-id="30a49-106">This article shows you how to use PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="30a49-107">Install Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="30a49-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="30a49-108">In October 2015, Azure PowerShell 1.0 was released.</span><span class="sxs-lookup"><span data-stu-id="30a49-108">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="30a49-109">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span><span class="sxs-lookup"><span data-stu-id="30a49-109">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="30a49-110">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="30a49-110">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="30a49-111">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span><span class="sxs-lookup"><span data-stu-id="30a49-111">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="30a49-112">This command is not necessary in 1.0 or later.</span><span class="sxs-lookup"><span data-stu-id="30a49-112">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="30a49-113">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span><span class="sxs-lookup"><span data-stu-id="30a49-113">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="30a49-114">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="30a49-114">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="30a49-115">Create a backup vault</span><span class="sxs-lookup"><span data-stu-id="30a49-115">Create a backup vault</span></span>
> [!WARNING]
> For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription. This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"
>
>

<span data-ttu-id="30a49-118">You can create a new backup vault using the **New-AzureRMBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-118">You can create a new backup vault using the **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="30a49-119">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span><span class="sxs-lookup"><span data-stu-id="30a49-119">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="30a49-120">In an elevated Azure PowerShell console, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="30a49-120">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="30a49-121">Use the **Get-AzureRMBackupVault** cmdlet to list the backup vaults in a subscription.</span><span class="sxs-lookup"><span data-stu-id="30a49-121">Use the **Get-AzureRMBackupVault** cmdlet to list the backup vaults in a subscription.</span></span>

## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="30a49-122">Installing the Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="30a49-122">Installing the Azure Backup agent</span></span>
<span data-ttu-id="30a49-123">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span><span class="sxs-lookup"><span data-stu-id="30a49-123">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="30a49-124">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span><span class="sxs-lookup"><span data-stu-id="30a49-124">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="30a49-125">Save the installer to an easily accessible location like \*C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="30a49-125">Save the installer to an easily accessible location like \*C:\Downloads\*.</span></span>

<span data-ttu-id="30a49-126">To install the agent, run the following command in an elevated PowerShell console:</span><span class="sxs-lookup"><span data-stu-id="30a49-126">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="30a49-127">This installs the agent with all the default options.</span><span class="sxs-lookup"><span data-stu-id="30a49-127">This installs the agent with all the default options.</span></span> <span data-ttu-id="30a49-128">The installation takes a few minutes in the background.</span><span class="sxs-lookup"><span data-stu-id="30a49-128">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="30a49-129">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span><span class="sxs-lookup"><span data-stu-id="30a49-129">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="30a49-130">Once installed, the agent will show in the list of installed programs.</span><span class="sxs-lookup"><span data-stu-id="30a49-130">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="30a49-131">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span><span class="sxs-lookup"><span data-stu-id="30a49-131">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent installed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="30a49-133">Installation options</span><span class="sxs-lookup"><span data-stu-id="30a49-133">Installation options</span></span>
<span data-ttu-id="30a49-134">To see all the options available via the command-line, use the following command:</span><span class="sxs-lookup"><span data-stu-id="30a49-134">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="30a49-135">The available options include:</span><span class="sxs-lookup"><span data-stu-id="30a49-135">The available options include:</span></span>

| <span data-ttu-id="30a49-136">Option</span><span class="sxs-lookup"><span data-stu-id="30a49-136">Option</span></span> | <span data-ttu-id="30a49-137">Details</span><span class="sxs-lookup"><span data-stu-id="30a49-137">Details</span></span> | <span data-ttu-id="30a49-138">Default</span><span class="sxs-lookup"><span data-stu-id="30a49-138">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="30a49-139">/q</span><span class="sxs-lookup"><span data-stu-id="30a49-139">/q</span></span> |<span data-ttu-id="30a49-140">Quiet installation</span><span class="sxs-lookup"><span data-stu-id="30a49-140">Quiet installation</span></span> |- |
| <span data-ttu-id="30a49-141">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="30a49-141">/p:"location"</span></span> |<span data-ttu-id="30a49-142">Path to the installation folder for the Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="30a49-142">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="30a49-143">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="30a49-143">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="30a49-144">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="30a49-144">/s:"location"</span></span> |<span data-ttu-id="30a49-145">Path to the cache folder for the Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="30a49-145">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="30a49-146">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="30a49-146">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="30a49-147">/m</span><span class="sxs-lookup"><span data-stu-id="30a49-147">/m</span></span> |<span data-ttu-id="30a49-148">Opt-in to Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="30a49-148">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="30a49-149">/nu</span><span class="sxs-lookup"><span data-stu-id="30a49-149">/nu</span></span> |<span data-ttu-id="30a49-150">Do not Check for updates after installation is complete</span><span class="sxs-lookup"><span data-stu-id="30a49-150">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="30a49-151">/d</span><span class="sxs-lookup"><span data-stu-id="30a49-151">/d</span></span> |<span data-ttu-id="30a49-152">Uninstalls Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="30a49-152">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="30a49-153">/ph</span><span class="sxs-lookup"><span data-stu-id="30a49-153">/ph</span></span> |<span data-ttu-id="30a49-154">Proxy Host Address</span><span class="sxs-lookup"><span data-stu-id="30a49-154">Proxy Host Address</span></span> |- |
| <span data-ttu-id="30a49-155">/po</span><span class="sxs-lookup"><span data-stu-id="30a49-155">/po</span></span> |<span data-ttu-id="30a49-156">Proxy Host Port Number</span><span class="sxs-lookup"><span data-stu-id="30a49-156">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="30a49-157">/pu</span><span class="sxs-lookup"><span data-stu-id="30a49-157">/pu</span></span> |<span data-ttu-id="30a49-158">Proxy Host UserName</span><span class="sxs-lookup"><span data-stu-id="30a49-158">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="30a49-159">/pw</span><span class="sxs-lookup"><span data-stu-id="30a49-159">/pw</span></span> |<span data-ttu-id="30a49-160">Proxy Password</span><span class="sxs-lookup"><span data-stu-id="30a49-160">Proxy Password</span></span> |- |

## <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="30a49-161">Registering with the Azure Backup service</span><span class="sxs-lookup"><span data-stu-id="30a49-161">Registering with the Azure Backup service</span></span>
<span data-ttu-id="30a49-162">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-configure-vault.md) are met.</span><span class="sxs-lookup"><span data-stu-id="30a49-162">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="30a49-163">You must:</span><span class="sxs-lookup"><span data-stu-id="30a49-163">You must:</span></span>

* <span data-ttu-id="30a49-164">Have a valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="30a49-164">Have a valid Azure subscription</span></span>
* <span data-ttu-id="30a49-165">Have a backup vault</span><span class="sxs-lookup"><span data-stu-id="30a49-165">Have a backup vault</span></span>

<span data-ttu-id="30a49-166">To download the vault credentials, run the **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like \*C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="30a49-166">To download the vault credentials, run the **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like \*C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="30a49-167">Registering the machine with the vault is done using the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="30a49-167">Registering the machine with the vault is done using the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> Do not use relative paths to specify the vault credentials file. You must provide an absolute path as an input to the cmdlet.
>
>

## <a name="networking-settings"></a><span data-ttu-id="30a49-170">Networking settings</span><span class="sxs-lookup"><span data-stu-id="30a49-170">Networking settings</span></span>
<span data-ttu-id="30a49-171">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span><span class="sxs-lookup"><span data-stu-id="30a49-171">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="30a49-172">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span><span class="sxs-lookup"><span data-stu-id="30a49-172">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="30a49-173">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span><span class="sxs-lookup"><span data-stu-id="30a49-173">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="30a49-174">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="30a49-174">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="30a49-175">Encryption settings</span><span class="sxs-lookup"><span data-stu-id="30a49-175">Encryption settings</span></span>
<span data-ttu-id="30a49-176">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span><span class="sxs-lookup"><span data-stu-id="30a49-176">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="30a49-177">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span><span class="sxs-lookup"><span data-stu-id="30a49-177">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> Keep the passphrase information safe and secure once it is set. You will not be able to restore data from Azure without this passphrase.
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="30a49-180">Back up files and folders</span><span class="sxs-lookup"><span data-stu-id="30a49-180">Back up files and folders</span></span>
<span data-ttu-id="30a49-181">All your backups from Windows Servers and clients to Azure Backup are governed by a policy.</span><span class="sxs-lookup"><span data-stu-id="30a49-181">All your backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="30a49-182">The policy comprises three parts:</span><span class="sxs-lookup"><span data-stu-id="30a49-182">The policy comprises three parts:</span></span>

1. <span data-ttu-id="30a49-183">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span><span class="sxs-lookup"><span data-stu-id="30a49-183">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="30a49-184">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span><span class="sxs-lookup"><span data-stu-id="30a49-184">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="30a49-185">A **file inclusion/exclusion specification** that dictates what should be backed up.</span><span class="sxs-lookup"><span data-stu-id="30a49-185">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="30a49-186">In this document, since we're automating backup, we'll assume nothing has been configured.</span><span class="sxs-lookup"><span data-stu-id="30a49-186">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="30a49-187">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span><span class="sxs-lookup"><span data-stu-id="30a49-187">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="30a49-188">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span><span class="sxs-lookup"><span data-stu-id="30a49-188">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="30a49-189">Configuring the backup schedule</span><span class="sxs-lookup"><span data-stu-id="30a49-189">Configuring the backup schedule</span></span>
<span data-ttu-id="30a49-190">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-190">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="30a49-191">The backup schedule defines when backups need to be taken.</span><span class="sxs-lookup"><span data-stu-id="30a49-191">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="30a49-192">When creating a schedule you need to specify 2 input parameters:</span><span class="sxs-lookup"><span data-stu-id="30a49-192">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="30a49-193">**Days of the week** that the backup should run.</span><span class="sxs-lookup"><span data-stu-id="30a49-193">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="30a49-194">You can run the backup job on just one day, or every day of the week, or any combination in between.</span><span class="sxs-lookup"><span data-stu-id="30a49-194">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="30a49-195">**Times of the day** when the backup should run.</span><span class="sxs-lookup"><span data-stu-id="30a49-195">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="30a49-196">You can define up to 3 different times of the day when the backup will be triggered.</span><span class="sxs-lookup"><span data-stu-id="30a49-196">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="30a49-197">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span><span class="sxs-lookup"><span data-stu-id="30a49-197">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="30a49-198">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-198">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="30a49-199">Configuring a retention policy</span><span class="sxs-lookup"><span data-stu-id="30a49-199">Configuring a retention policy</span></span>
<span data-ttu-id="30a49-200">The retention policy defines how long recovery points created from backup jobs are retained.</span><span class="sxs-lookup"><span data-stu-id="30a49-200">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="30a49-201">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="30a49-201">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="30a49-202">The example below sets a retention policy of 7 days.</span><span class="sxs-lookup"><span data-stu-id="30a49-202">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="30a49-203">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="30a49-203">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="30a49-204">Including and excluding files to be backed up</span><span class="sxs-lookup"><span data-stu-id="30a49-204">Including and excluding files to be backed up</span></span>
<span data-ttu-id="30a49-205">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span><span class="sxs-lookup"><span data-stu-id="30a49-205">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="30a49-206">This is a set of rules that scope out the protected files and folders on a machine.</span><span class="sxs-lookup"><span data-stu-id="30a49-206">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="30a49-207">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span><span class="sxs-lookup"><span data-stu-id="30a49-207">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="30a49-208">When creating a new OBFileSpec object, you can:</span><span class="sxs-lookup"><span data-stu-id="30a49-208">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="30a49-209">Specify the files and folders to be included</span><span class="sxs-lookup"><span data-stu-id="30a49-209">Specify the files and folders to be included</span></span>
* <span data-ttu-id="30a49-210">Specify the files and folders to be excluded</span><span class="sxs-lookup"><span data-stu-id="30a49-210">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="30a49-211">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span><span class="sxs-lookup"><span data-stu-id="30a49-211">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="30a49-212">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span><span class="sxs-lookup"><span data-stu-id="30a49-212">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="30a49-213">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span><span class="sxs-lookup"><span data-stu-id="30a49-213">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="30a49-214">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span><span class="sxs-lookup"><span data-stu-id="30a49-214">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="30a49-215">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-215">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-the-policy"></a><span data-ttu-id="30a49-216">Applying the policy</span><span class="sxs-lookup"><span data-stu-id="30a49-216">Applying the policy</span></span>
<span data-ttu-id="30a49-217">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span><span class="sxs-lookup"><span data-stu-id="30a49-217">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="30a49-218">This policy can now be committed for Azure Backup to use.</span><span class="sxs-lookup"><span data-stu-id="30a49-218">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="30a49-219">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-219">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="30a49-220">Removing the policy will prompt for confirmation.</span><span class="sxs-lookup"><span data-stu-id="30a49-220">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="30a49-221">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-221">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="30a49-222">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-222">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="30a49-223">This will also ask for confirmation.</span><span class="sxs-lookup"><span data-stu-id="30a49-223">This will also ask for confirmation.</span></span> <span data-ttu-id="30a49-224">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-224">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want to save this backup policy ? [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

<span data-ttu-id="30a49-225">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-225">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="30a49-226">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span><span class="sxs-lookup"><span data-stu-id="30a49-226">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="30a49-227">Performing an ad-hoc backup</span><span class="sxs-lookup"><span data-stu-id="30a49-227">Performing an ad-hoc backup</span></span>
<span data-ttu-id="30a49-228">Once a backup policy has been set the backups will occur per the schedule.</span><span class="sxs-lookup"><span data-stu-id="30a49-228">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="30a49-229">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="30a49-229">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="30a49-230">Restore data from Azure Backup</span><span class="sxs-lookup"><span data-stu-id="30a49-230">Restore data from Azure Backup</span></span>
<span data-ttu-id="30a49-231">This section will guide you through the steps for automating recovery of data from Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="30a49-231">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="30a49-232">Doing so involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="30a49-232">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="30a49-233">Pick the source volume</span><span class="sxs-lookup"><span data-stu-id="30a49-233">Pick the source volume</span></span>
2. <span data-ttu-id="30a49-234">Choose a backup point to restore</span><span class="sxs-lookup"><span data-stu-id="30a49-234">Choose a backup point to restore</span></span>
3. <span data-ttu-id="30a49-235">Choose an item to restore</span><span class="sxs-lookup"><span data-stu-id="30a49-235">Choose an item to restore</span></span>
4. <span data-ttu-id="30a49-236">Trigger the restore process</span><span class="sxs-lookup"><span data-stu-id="30a49-236">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="30a49-237">Picking the source volume</span><span class="sxs-lookup"><span data-stu-id="30a49-237">Picking the source volume</span></span>
<span data-ttu-id="30a49-238">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span><span class="sxs-lookup"><span data-stu-id="30a49-238">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="30a49-239">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span><span class="sxs-lookup"><span data-stu-id="30a49-239">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="30a49-240">The next step in identifying the source is to identify the volume containing it.</span><span class="sxs-lookup"><span data-stu-id="30a49-240">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="30a49-241">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-241">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="30a49-242">This command returns an array of all the sources backed up from this server/client.</span><span class="sxs-lookup"><span data-stu-id="30a49-242">This command returns an array of all the sources backed up from this server/client.</span></span>

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-to-restore"></a><span data-ttu-id="30a49-243">Choosing a backup point to restore</span><span class="sxs-lookup"><span data-stu-id="30a49-243">Choosing a backup point to restore</span></span>
<span data-ttu-id="30a49-244">The list of backup points can be retrieved by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span><span class="sxs-lookup"><span data-stu-id="30a49-244">The list of backup points can be retrieved by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="30a49-245">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span><span class="sxs-lookup"><span data-stu-id="30a49-245">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
<span data-ttu-id="30a49-246">The object ```$rps``` is an array of backup points.</span><span class="sxs-lookup"><span data-stu-id="30a49-246">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="30a49-247">The first element is the latest point and the Nth element is the oldest point.</span><span class="sxs-lookup"><span data-stu-id="30a49-247">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="30a49-248">To choose the latest point, we will use ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="30a49-248">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="30a49-249">Choosing an item to restore</span><span class="sxs-lookup"><span data-stu-id="30a49-249">Choosing an item to restore</span></span>
<span data-ttu-id="30a49-250">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-250">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="30a49-251">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="30a49-251">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="30a49-252">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="30a49-252">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

<span data-ttu-id="30a49-253">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-253">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="30a49-254">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span><span class="sxs-lookup"><span data-stu-id="30a49-254">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="30a49-255">Triggering the restore process</span><span class="sxs-lookup"><span data-stu-id="30a49-255">Triggering the restore process</span></span>
<span data-ttu-id="30a49-256">To trigger the restore process, we first need to specify the recovery options.</span><span class="sxs-lookup"><span data-stu-id="30a49-256">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="30a49-257">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30a49-257">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="30a49-258">For this example, let's assume that we want to restore the files to *C:\temp*. Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*. To create such a recovery option, use the following command:</span><span class="sxs-lookup"><span data-stu-id="30a49-258">For this example, let's assume that we want to restore the files to *C:\temp*. Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*. To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="30a49-259">Now trigger restore by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="30a49-259">Now trigger restore by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="30a49-260">Uninstalling the Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="30a49-260">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="30a49-261">Uninstalling the Azure Backup agent can be done by using the following command:</span><span class="sxs-lookup"><span data-stu-id="30a49-261">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="30a49-262">Uninstalling the agent binaries from the machine has some consequences to consider:</span><span class="sxs-lookup"><span data-stu-id="30a49-262">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="30a49-263">It removes the file-filter from the machine, and tracking of changes is stopped.</span><span class="sxs-lookup"><span data-stu-id="30a49-263">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="30a49-264">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span><span class="sxs-lookup"><span data-stu-id="30a49-264">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="30a49-265">All backup schedules are removed, and no further backups are taken.</span><span class="sxs-lookup"><span data-stu-id="30a49-265">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="30a49-266">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span><span class="sxs-lookup"><span data-stu-id="30a49-266">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="30a49-267">Older points are automatically aged out.</span><span class="sxs-lookup"><span data-stu-id="30a49-267">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="30a49-268">Remote management</span><span class="sxs-lookup"><span data-stu-id="30a49-268">Remote management</span></span>
<span data-ttu-id="30a49-269">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30a49-269">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="30a49-270">The machine that will be managed remotely needs to be prepared correctly.</span><span class="sxs-lookup"><span data-stu-id="30a49-270">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="30a49-271">By default, the WinRM service is configured for manual startup.</span><span class="sxs-lookup"><span data-stu-id="30a49-271">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="30a49-272">The startup type must be set to *Automatic* and the service should be started.</span><span class="sxs-lookup"><span data-stu-id="30a49-272">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="30a49-273">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span><span class="sxs-lookup"><span data-stu-id="30a49-273">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="30a49-274">PowerShell should be configured for remoting.</span><span class="sxs-lookup"><span data-stu-id="30a49-274">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="30a49-275">The machine can now be managed remotely - starting from the installation of the agent.</span><span class="sxs-lookup"><span data-stu-id="30a49-275">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="30a49-276">For example, the following script copies the agent to the remote machine and installs it.</span><span class="sxs-lookup"><span data-stu-id="30a49-276">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="30a49-277">Next steps</span><span class="sxs-lookup"><span data-stu-id="30a49-277">Next steps</span></span>
<span data-ttu-id="30a49-278">For more information about Azure Backup for Windows Server/Client see</span><span class="sxs-lookup"><span data-stu-id="30a49-278">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="30a49-279">Introduction to Azure Backup</span><span class="sxs-lookup"><span data-stu-id="30a49-279">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="30a49-280">Back up Windows Servers</span><span class="sxs-lookup"><span data-stu-id="30a49-280">Back up Windows Servers</span></span>](backup-configure-vault.md)

