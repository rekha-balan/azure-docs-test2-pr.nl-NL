---
title: 'Azure Backup: Use PowerShell to back up DPM workloads | Microsoft Docs'
description: Learn how to deploy and manage Azure Backup for Data Protection Manager (DPM) using PowerShell
services: backup
documentationcenter: ''
author: Nkolli1
manager: shreeshd
editor: ''
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 4cfa838ec000967a79b123a673290fdeb598dad0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564098"
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="3bc68-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bc68-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Classic](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="3bc68-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span><span class="sxs-lookup"><span data-stu-id="3bc68-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span></span>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="3bc68-107">Setting up the PowerShell environment</span><span class="sxs-lookup"><span data-stu-id="3bc68-107">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="3bc68-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you will need to have the right environment in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3bc68-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you will need to have the right environment in PowerShell.</span></span> <span data-ttu-id="3bc68-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span><span class="sxs-lookup"><span data-stu-id="3bc68-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="3bc68-110">Setup and Registration</span><span class="sxs-lookup"><span data-stu-id="3bc68-110">Setup and Registration</span></span>
<span data-ttu-id="3bc68-111">To begin:</span><span class="sxs-lookup"><span data-stu-id="3bc68-111">To begin:</span></span>

1. <span data-ttu-id="3bc68-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="3bc68-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="3bc68-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span><span class="sxs-lookup"><span data-stu-id="3bc68-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="3bc68-114">The following setup and registration tasks can be automated with PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3bc68-114">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="3bc68-115">Create a backup vault</span><span class="sxs-lookup"><span data-stu-id="3bc68-115">Create a backup vault</span></span>
* <span data-ttu-id="3bc68-116">Installing the Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="3bc68-116">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="3bc68-117">Registering with the Azure Backup service</span><span class="sxs-lookup"><span data-stu-id="3bc68-117">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="3bc68-118">Networking settings</span><span class="sxs-lookup"><span data-stu-id="3bc68-118">Networking settings</span></span>
* <span data-ttu-id="3bc68-119">Encryption settings</span><span class="sxs-lookup"><span data-stu-id="3bc68-119">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="3bc68-120">Create a backup vault</span><span class="sxs-lookup"><span data-stu-id="3bc68-120">Create a backup vault</span></span>
> [!WARNING]
> For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription. This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"
>
>

<span data-ttu-id="3bc68-123">You can create a new backup vault using the **New-AzureRMBackupVault** commandlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-123">You can create a new backup vault using the **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="3bc68-124">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span><span class="sxs-lookup"><span data-stu-id="3bc68-124">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="3bc68-125">In an elevated Azure PowerShell console, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="3bc68-125">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="3bc68-126">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRMBackupVault** commandlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-126">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="3bc68-127">Installing the Azure Backup agent on a DPM Server</span><span class="sxs-lookup"><span data-stu-id="3bc68-127">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="3bc68-128">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3bc68-128">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="3bc68-129">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span><span class="sxs-lookup"><span data-stu-id="3bc68-129">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="3bc68-130">Save the installer to an easily accessible location like \*C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="3bc68-130">Save the installer to an easily accessible location like \*C:\Downloads\*.</span></span>

<span data-ttu-id="3bc68-131">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span><span class="sxs-lookup"><span data-stu-id="3bc68-131">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="3bc68-132">This installs the agent with all the default options.</span><span class="sxs-lookup"><span data-stu-id="3bc68-132">This installs the agent with all the default options.</span></span> <span data-ttu-id="3bc68-133">The installation takes a few minutes in the background.</span><span class="sxs-lookup"><span data-stu-id="3bc68-133">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="3bc68-134">If you do not specify the */nu* option the **Windows Update** window will open at the end of the installation to check for any updates.</span><span class="sxs-lookup"><span data-stu-id="3bc68-134">If you do not specify the */nu* option the **Windows Update** window will open at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="3bc68-135">The agent will show in the list of installed programs.</span><span class="sxs-lookup"><span data-stu-id="3bc68-135">The agent will show in the list of installed programs.</span></span> <span data-ttu-id="3bc68-136">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span><span class="sxs-lookup"><span data-stu-id="3bc68-136">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent installed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="3bc68-138">Installation options</span><span class="sxs-lookup"><span data-stu-id="3bc68-138">Installation options</span></span>
<span data-ttu-id="3bc68-139">To see all the options available via the command-line, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3bc68-139">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="3bc68-140">The available options include:</span><span class="sxs-lookup"><span data-stu-id="3bc68-140">The available options include:</span></span>

| <span data-ttu-id="3bc68-141">Option</span><span class="sxs-lookup"><span data-stu-id="3bc68-141">Option</span></span> | <span data-ttu-id="3bc68-142">Details</span><span class="sxs-lookup"><span data-stu-id="3bc68-142">Details</span></span> | <span data-ttu-id="3bc68-143">Default</span><span class="sxs-lookup"><span data-stu-id="3bc68-143">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3bc68-144">/q</span><span class="sxs-lookup"><span data-stu-id="3bc68-144">/q</span></span> |<span data-ttu-id="3bc68-145">Quiet installation</span><span class="sxs-lookup"><span data-stu-id="3bc68-145">Quiet installation</span></span> |- |
| <span data-ttu-id="3bc68-146">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="3bc68-146">/p:"location"</span></span> |<span data-ttu-id="3bc68-147">Path to the installation folder for the Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="3bc68-147">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="3bc68-148">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="3bc68-148">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="3bc68-149">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="3bc68-149">/s:"location"</span></span> |<span data-ttu-id="3bc68-150">Path to the cache folder for the Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="3bc68-150">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="3bc68-151">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="3bc68-151">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="3bc68-152">/m</span><span class="sxs-lookup"><span data-stu-id="3bc68-152">/m</span></span> |<span data-ttu-id="3bc68-153">Opt-in to Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="3bc68-153">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="3bc68-154">/nu</span><span class="sxs-lookup"><span data-stu-id="3bc68-154">/nu</span></span> |<span data-ttu-id="3bc68-155">Do not Check for updates after installation is complete</span><span class="sxs-lookup"><span data-stu-id="3bc68-155">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="3bc68-156">/d</span><span class="sxs-lookup"><span data-stu-id="3bc68-156">/d</span></span> |<span data-ttu-id="3bc68-157">Uninstalls Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="3bc68-157">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="3bc68-158">/ph</span><span class="sxs-lookup"><span data-stu-id="3bc68-158">/ph</span></span> |<span data-ttu-id="3bc68-159">Proxy Host Address</span><span class="sxs-lookup"><span data-stu-id="3bc68-159">Proxy Host Address</span></span> |- |
| <span data-ttu-id="3bc68-160">/po</span><span class="sxs-lookup"><span data-stu-id="3bc68-160">/po</span></span> |<span data-ttu-id="3bc68-161">Proxy Host Port Number</span><span class="sxs-lookup"><span data-stu-id="3bc68-161">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="3bc68-162">/pu</span><span class="sxs-lookup"><span data-stu-id="3bc68-162">/pu</span></span> |<span data-ttu-id="3bc68-163">Proxy Host UserName</span><span class="sxs-lookup"><span data-stu-id="3bc68-163">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="3bc68-164">/pw</span><span class="sxs-lookup"><span data-stu-id="3bc68-164">/pw</span></span> |<span data-ttu-id="3bc68-165">Proxy Password</span><span class="sxs-lookup"><span data-stu-id="3bc68-165">Proxy Password</span></span> |- |

### <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="3bc68-166">Registering with the Azure Backup service</span><span class="sxs-lookup"><span data-stu-id="3bc68-166">Registering with the Azure Backup service</span></span>
<span data-ttu-id="3bc68-167">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-azure-dpm-introduction.md) are met.</span><span class="sxs-lookup"><span data-stu-id="3bc68-167">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="3bc68-168">You must:</span><span class="sxs-lookup"><span data-stu-id="3bc68-168">You must:</span></span>

* <span data-ttu-id="3bc68-169">Have a valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="3bc68-169">Have a valid Azure subscription</span></span>
* <span data-ttu-id="3bc68-170">Have a backup vault</span><span class="sxs-lookup"><span data-stu-id="3bc68-170">Have a backup vault</span></span>

<span data-ttu-id="3bc68-171">To download the vault credentials, run the **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like \*C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="3bc68-171">To download the vault credentials, run the **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like \*C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="3bc68-172">Registering the machine with the vault is done using the [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3bc68-172">Registering the machine with the vault is done using the [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="3bc68-173">This will register the DPM Server named “TestingServer” with Microsoft Azure Vault using the specified vault credentials.</span><span class="sxs-lookup"><span data-stu-id="3bc68-173">This will register the DPM Server named “TestingServer” with Microsoft Azure Vault using the specified vault credentials.</span></span>

> [!IMPORTANT]
> Do not use relative paths to specify the vault credentials file. You must provide an absolute path as an input to the cmdlet.
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="3bc68-176">Initial configuration settings</span><span class="sxs-lookup"><span data-stu-id="3bc68-176">Initial configuration settings</span></span>
<span data-ttu-id="3bc68-177">Once the DPM Server is registered with the Azure Backup vault, it will start with default subscription settings.</span><span class="sxs-lookup"><span data-stu-id="3bc68-177">Once the DPM Server is registered with the Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="3bc68-178">These subscription settings include Networking, Encryption and the Staging area.</span><span class="sxs-lookup"><span data-stu-id="3bc68-178">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="3bc68-179">To begin changing the subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3bc68-179">To begin changing the subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="3bc68-180">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-180">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="3bc68-181">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span><span class="sxs-lookup"><span data-stu-id="3bc68-181">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="3bc68-182">The settings will not be applied and used by Azure Backup unless committed.</span><span class="sxs-lookup"><span data-stu-id="3bc68-182">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="3bc68-183">Networking</span><span class="sxs-lookup"><span data-stu-id="3bc68-183">Networking</span></span>
<span data-ttu-id="3bc68-184">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for backups to succeed.</span><span class="sxs-lookup"><span data-stu-id="3bc68-184">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for backups to succeed.</span></span> <span data-ttu-id="3bc68-185">This is done by using the ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-185">This is done by using the ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="3bc68-186">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span><span class="sxs-lookup"><span data-stu-id="3bc68-186">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="3bc68-187">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span><span class="sxs-lookup"><span data-stu-id="3bc68-187">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="3bc68-188">In this example we are not setting any throttling.</span><span class="sxs-lookup"><span data-stu-id="3bc68-188">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-the-staging-area"></a><span data-ttu-id="3bc68-189">Configuring the staging Area</span><span class="sxs-lookup"><span data-stu-id="3bc68-189">Configuring the staging Area</span></span>
<span data-ttu-id="3bc68-190">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span><span class="sxs-lookup"><span data-stu-id="3bc68-190">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="3bc68-191">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span><span class="sxs-lookup"><span data-stu-id="3bc68-191">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="3bc68-192">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="3bc68-192">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="3bc68-193">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span><span class="sxs-lookup"><span data-stu-id="3bc68-193">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="3bc68-194">Encryption settings</span><span class="sxs-lookup"><span data-stu-id="3bc68-194">Encryption settings</span></span>
<span data-ttu-id="3bc68-195">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span><span class="sxs-lookup"><span data-stu-id="3bc68-195">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="3bc68-196">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span><span class="sxs-lookup"><span data-stu-id="3bc68-196">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="3bc68-197">It is important to keep this information safe and secure once it is set.</span><span class="sxs-lookup"><span data-stu-id="3bc68-197">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="3bc68-198">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="3bc68-198">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="3bc68-199">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span><span class="sxs-lookup"><span data-stu-id="3bc68-199">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Keep the passphrase information safe and secure once it is set. You will not be able to restore data from Azure without this passphrase.
>
>

<span data-ttu-id="3bc68-202">At this point, you should have made all the required changes to the ```$setting``` object.</span><span class="sxs-lookup"><span data-stu-id="3bc68-202">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="3bc68-203">Remember to commit the changes.</span><span class="sxs-lookup"><span data-stu-id="3bc68-203">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="3bc68-204">Protect data to Azure Backup</span><span class="sxs-lookup"><span data-stu-id="3bc68-204">Protect data to Azure Backup</span></span>
<span data-ttu-id="3bc68-205">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="3bc68-205">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="3bc68-206">In the examples we will demonstrate how to back up files and folders.</span><span class="sxs-lookup"><span data-stu-id="3bc68-206">In the examples we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="3bc68-207">The logic can easily be extended to backup any DPM-supported data source.</span><span class="sxs-lookup"><span data-stu-id="3bc68-207">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="3bc68-208">All your DPM backups are governed by a Protection Group (PG) with four parts:</span><span class="sxs-lookup"><span data-stu-id="3bc68-208">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="3bc68-209">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span><span class="sxs-lookup"><span data-stu-id="3bc68-209">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="3bc68-210">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span><span class="sxs-lookup"><span data-stu-id="3bc68-210">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="3bc68-211">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span><span class="sxs-lookup"><span data-stu-id="3bc68-211">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="3bc68-212">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span><span class="sxs-lookup"><span data-stu-id="3bc68-212">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="3bc68-213">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span><span class="sxs-lookup"><span data-stu-id="3bc68-213">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="3bc68-214">In our example we will protect data to the local disk and to the cloud.</span><span class="sxs-lookup"><span data-stu-id="3bc68-214">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="3bc68-215">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span><span class="sxs-lookup"><span data-stu-id="3bc68-215">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="3bc68-216">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc68-216">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="3bc68-217">Creating a protection group</span><span class="sxs-lookup"><span data-stu-id="3bc68-217">Creating a protection group</span></span>
<span data-ttu-id="3bc68-218">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-218">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="3bc68-219">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="3bc68-219">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="3bc68-220">An existing protection group can also be modified later to add backup to the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="3bc68-220">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="3bc68-221">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-221">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="3bc68-222">Adding group members to the Protection Group</span><span class="sxs-lookup"><span data-stu-id="3bc68-222">Adding group members to the Protection Group</span></span>
<span data-ttu-id="3bc68-223">Each DPM Agent knows the list of datasources on the server that it is installed on.</span><span class="sxs-lookup"><span data-stu-id="3bc68-223">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="3bc68-224">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span><span class="sxs-lookup"><span data-stu-id="3bc68-224">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="3bc68-225">One or more datasources are then selected and added to the Protection Group.</span><span class="sxs-lookup"><span data-stu-id="3bc68-225">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="3bc68-226">The PowerShell steps needed to get achieve this are:</span><span class="sxs-lookup"><span data-stu-id="3bc68-226">The PowerShell steps needed to get achieve this are:</span></span>

1. <span data-ttu-id="3bc68-227">Fetch a list of all servers managed by DPM through the DPM Agent.</span><span class="sxs-lookup"><span data-stu-id="3bc68-227">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="3bc68-228">Choose a specific server.</span><span class="sxs-lookup"><span data-stu-id="3bc68-228">Choose a specific server.</span></span>
3. <span data-ttu-id="3bc68-229">Fetch a list of all datasources on the server.</span><span class="sxs-lookup"><span data-stu-id="3bc68-229">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="3bc68-230">Choose one or more datasources and add them to the Protection Group</span><span class="sxs-lookup"><span data-stu-id="3bc68-230">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="3bc68-231">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-231">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="3bc68-232">In this example we will filter and only configure PS with name *productionserver01* for backup.</span><span class="sxs-lookup"><span data-stu-id="3bc68-232">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="3bc68-233">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-233">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="3bc68-234">In this example we are filtering for the volume \*D:\* which we want to configure for backup.</span><span class="sxs-lookup"><span data-stu-id="3bc68-234">In this example we are filtering for the volume \*D:\* which we want to configure for backup.</span></span> <span data-ttu-id="3bc68-235">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-235">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="3bc68-236">Remember to use the *modifable* protection group object ```$MPG``` to make the additions.</span><span class="sxs-lookup"><span data-stu-id="3bc68-236">Remember to use the *modifable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="3bc68-237">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span><span class="sxs-lookup"><span data-stu-id="3bc68-237">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="3bc68-238">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span><span class="sxs-lookup"><span data-stu-id="3bc68-238">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="3bc68-239">Selecting the data protection method</span><span class="sxs-lookup"><span data-stu-id="3bc68-239">Selecting the data protection method</span></span>
<span data-ttu-id="3bc68-240">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-240">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="3bc68-241">In this example, the Protection Group will be setup for local disk and cloud backup.</span><span class="sxs-lookup"><span data-stu-id="3bc68-241">In this example, the Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="3bc68-242">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span><span class="sxs-lookup"><span data-stu-id="3bc68-242">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="3bc68-243">Setting the retention range</span><span class="sxs-lookup"><span data-stu-id="3bc68-243">Setting the retention range</span></span>
<span data-ttu-id="3bc68-244">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-244">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="3bc68-245">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span><span class="sxs-lookup"><span data-stu-id="3bc68-245">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="3bc68-246">It is always possible to set the backup schedule first and the retention policy after.</span><span class="sxs-lookup"><span data-stu-id="3bc68-246">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="3bc68-247">In the example below, the cmdlet sets the retention parameters for disk backups.</span><span class="sxs-lookup"><span data-stu-id="3bc68-247">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="3bc68-248">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span><span class="sxs-lookup"><span data-stu-id="3bc68-248">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="3bc68-249">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server; this prevents backups from becoming too large.</span><span class="sxs-lookup"><span data-stu-id="3bc68-249">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="3bc68-250">For backups going to Azure (DPM refers to these as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="3bc68-250">For backups going to Azure (DPM refers to these as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="3bc68-251">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span><span class="sxs-lookup"><span data-stu-id="3bc68-251">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="3bc68-252">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-252">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="3bc68-253">Set the backup schedule</span><span class="sxs-lookup"><span data-stu-id="3bc68-253">Set the backup schedule</span></span>
<span data-ttu-id="3bc68-254">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-254">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="3bc68-255">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-255">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="3bc68-256">In the example above, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span><span class="sxs-lookup"><span data-stu-id="3bc68-256">In the example above, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="3bc68-257">```$onlineSch[0]``` will contain the daily schedule</span><span class="sxs-lookup"><span data-stu-id="3bc68-257">```$onlineSch[0]``` will contain the daily schedule</span></span>
2. <span data-ttu-id="3bc68-258">```$onlineSch[1]``` will contain the weekly schedule</span><span class="sxs-lookup"><span data-stu-id="3bc68-258">```$onlineSch[1]``` will contain the weekly schedule</span></span>
3. <span data-ttu-id="3bc68-259">```$onlineSch[2]``` will contain the monthly schedule</span><span class="sxs-lookup"><span data-stu-id="3bc68-259">```$onlineSch[2]``` will contain the monthly schedule</span></span>
4. <span data-ttu-id="3bc68-260">```$onlineSch[3]``` will contain the yearly schedule</span><span class="sxs-lookup"><span data-stu-id="3bc68-260">```$onlineSch[3]``` will contain the yearly schedule</span></span>

<span data-ttu-id="3bc68-261">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="3bc68-261">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="3bc68-262">Initial backup</span><span class="sxs-lookup"><span data-stu-id="3bc68-262">Initial backup</span></span>
<span data-ttu-id="3bc68-263">When backing up a datasource for the first time, DPM needs to create an initial replica which will create a copy of the datasource to be protected on DPM replica volume.</span><span class="sxs-lookup"><span data-stu-id="3bc68-263">When backing up a datasource for the first time, DPM needs to create an initial replica which will create a copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="3bc68-264">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="3bc68-264">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="3bc68-265">Changing the size of DPM Replica & recovery point volume</span><span class="sxs-lookup"><span data-stu-id="3bc68-265">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="3bc68-266">You can also change the size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="3bc68-266">You can also change the size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="3bc68-267">Committing the changes to the Protection Group</span><span class="sxs-lookup"><span data-stu-id="3bc68-267">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="3bc68-268">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span><span class="sxs-lookup"><span data-stu-id="3bc68-268">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="3bc68-269">This is done using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-269">This is done using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="3bc68-270">View the backup points</span><span class="sxs-lookup"><span data-stu-id="3bc68-270">View the backup points</span></span>
<span data-ttu-id="3bc68-271">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span><span class="sxs-lookup"><span data-stu-id="3bc68-271">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="3bc68-272">In this example, we will:</span><span class="sxs-lookup"><span data-stu-id="3bc68-272">In this example, we will:</span></span>

* <span data-ttu-id="3bc68-273">fetch all the PGs on the DPM server which will be stored in an array ```$PG```</span><span class="sxs-lookup"><span data-stu-id="3bc68-273">fetch all the PGs on the DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="3bc68-274">get the datasources corresponding to the ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="3bc68-274">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="3bc68-275">get all the recovery points for a datasource.</span><span class="sxs-lookup"><span data-stu-id="3bc68-275">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="3bc68-276">Restore data protected on Azure</span><span class="sxs-lookup"><span data-stu-id="3bc68-276">Restore data protected on Azure</span></span>
<span data-ttu-id="3bc68-277">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span><span class="sxs-lookup"><span data-stu-id="3bc68-277">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="3bc68-278">In the previous section, we got a list of the backup points for a datasource.</span><span class="sxs-lookup"><span data-stu-id="3bc68-278">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="3bc68-279">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span><span class="sxs-lookup"><span data-stu-id="3bc68-279">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="3bc68-280">This includes:</span><span class="sxs-lookup"><span data-stu-id="3bc68-280">This includes:</span></span>

* <span data-ttu-id="3bc68-281">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-281">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="3bc68-282">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bc68-282">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="3bc68-283">Choosing a backup point to restore from.</span><span class="sxs-lookup"><span data-stu-id="3bc68-283">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="3bc68-284">The commands can easily be extended for any datasource type.</span><span class="sxs-lookup"><span data-stu-id="3bc68-284">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bc68-285">Next steps</span><span class="sxs-lookup"><span data-stu-id="3bc68-285">Next steps</span></span>
* <span data-ttu-id="3bc68-286">For more information about Azure Backup for DPM see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="3bc68-286">For more information about Azure Backup for DPM see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>

