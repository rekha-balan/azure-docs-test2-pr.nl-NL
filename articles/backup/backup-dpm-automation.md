---
title: Azure Backup - Use PowerShell to back up DPM workloads | Microsoft Docs
description: Learn how to deploy and manage Azure Backup for Data Protection Manager (DPM) using PowerShell
services: backup
documentationcenter: ''
author: NKolli1
manager: shreeshd
editor: ''
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 42c2074ae80e9167d1ce7c54e59258bf93918f18
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552843"
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="f638a-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span><span class="sxs-lookup"><span data-stu-id="f638a-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Classic](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="f638a-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span><span class="sxs-lookup"><span data-stu-id="f638a-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span></span>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="f638a-107">Setting up the PowerShell environment</span><span class="sxs-lookup"><span data-stu-id="f638a-107">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="f638a-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f638a-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span></span> <span data-ttu-id="f638a-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span><span class="sxs-lookup"><span data-stu-id="f638a-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="f638a-110">Setup and Registration</span><span class="sxs-lookup"><span data-stu-id="f638a-110">Setup and Registration</span></span>
<span data-ttu-id="f638a-111">To begin:</span><span class="sxs-lookup"><span data-stu-id="f638a-111">To begin:</span></span>

1. <span data-ttu-id="f638a-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="f638a-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="f638a-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span><span class="sxs-lookup"><span data-stu-id="f638a-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="f638a-114">The following setup and registration tasks can be automated with PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f638a-114">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="f638a-115">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="f638a-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="f638a-116">Installing the Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="f638a-116">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="f638a-117">Registering with the Azure Backup service</span><span class="sxs-lookup"><span data-stu-id="f638a-117">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="f638a-118">Networking settings</span><span class="sxs-lookup"><span data-stu-id="f638a-118">Networking settings</span></span>
* <span data-ttu-id="f638a-119">Encryption settings</span><span class="sxs-lookup"><span data-stu-id="f638a-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="f638a-120">Create a recovery services vault</span><span class="sxs-lookup"><span data-stu-id="f638a-120">Create a recovery services vault</span></span>
<span data-ttu-id="f638a-121">The following steps lead you through creating a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="f638a-121">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="f638a-122">A Recovery Services vault is different than a Backup vault.</span><span class="sxs-lookup"><span data-stu-id="f638a-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="f638a-123">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span><span class="sxs-lookup"><span data-stu-id="f638a-123">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="f638a-124">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span><span class="sxs-lookup"><span data-stu-id="f638a-124">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="f638a-125">You can use an existing resource group, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="f638a-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="f638a-126">When creating a new resource group, specify the name and location for the resource group.</span><span class="sxs-lookup"><span data-stu-id="f638a-126">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="f638a-127">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span><span class="sxs-lookup"><span data-stu-id="f638a-127">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span></span> <span data-ttu-id="f638a-128">Be sure to specify the same location for the vault as was used for the resource group.</span><span class="sxs-lookup"><span data-stu-id="f638a-128">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="f638a-129">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="f638a-129">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="f638a-130">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="f638a-130">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > Many Azure Backup cmdlets require the Recovery Services vault object as an input. For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="f638a-133">View the vaults in a subscription</span><span class="sxs-lookup"><span data-stu-id="f638a-133">View the vaults in a subscription</span></span>
<span data-ttu-id="f638a-134">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="f638a-134">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="f638a-135">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span><span class="sxs-lookup"><span data-stu-id="f638a-135">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="f638a-136">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span><span class="sxs-lookup"><span data-stu-id="f638a-136">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="f638a-137">Installing the Azure Backup agent on a DPM Server</span><span class="sxs-lookup"><span data-stu-id="f638a-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="f638a-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span><span class="sxs-lookup"><span data-stu-id="f638a-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="f638a-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span><span class="sxs-lookup"><span data-stu-id="f638a-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="f638a-140">Save the installer to an easily accessible location like \*C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="f638a-140">Save the installer to an easily accessible location like \*C:\Downloads\*.</span></span>

<span data-ttu-id="f638a-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span><span class="sxs-lookup"><span data-stu-id="f638a-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="f638a-142">This installs the agent with all the default options.</span><span class="sxs-lookup"><span data-stu-id="f638a-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="f638a-143">The installation takes a few minutes in the background.</span><span class="sxs-lookup"><span data-stu-id="f638a-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="f638a-144">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span><span class="sxs-lookup"><span data-stu-id="f638a-144">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="f638a-145">The agent shows up in the list of installed programs.</span><span class="sxs-lookup"><span data-stu-id="f638a-145">The agent shows up in the list of installed programs.</span></span> <span data-ttu-id="f638a-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span><span class="sxs-lookup"><span data-stu-id="f638a-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent installed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/backup/media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="f638a-148">Installation options</span><span class="sxs-lookup"><span data-stu-id="f638a-148">Installation options</span></span>
<span data-ttu-id="f638a-149">To see all the options available via the commandline, use the following command:</span><span class="sxs-lookup"><span data-stu-id="f638a-149">To see all the options available via the commandline, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="f638a-150">The available options include:</span><span class="sxs-lookup"><span data-stu-id="f638a-150">The available options include:</span></span>

| <span data-ttu-id="f638a-151">Option</span><span class="sxs-lookup"><span data-stu-id="f638a-151">Option</span></span> | <span data-ttu-id="f638a-152">Details</span><span class="sxs-lookup"><span data-stu-id="f638a-152">Details</span></span> | <span data-ttu-id="f638a-153">Default</span><span class="sxs-lookup"><span data-stu-id="f638a-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f638a-154">/q</span><span class="sxs-lookup"><span data-stu-id="f638a-154">/q</span></span> |<span data-ttu-id="f638a-155">Quiet installation</span><span class="sxs-lookup"><span data-stu-id="f638a-155">Quiet installation</span></span> |- |
| <span data-ttu-id="f638a-156">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="f638a-156">/p:"location"</span></span> |<span data-ttu-id="f638a-157">Path to the installation folder for the Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="f638a-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="f638a-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="f638a-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="f638a-159">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="f638a-159">/s:"location"</span></span> |<span data-ttu-id="f638a-160">Path to the cache folder for the Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="f638a-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="f638a-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="f638a-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="f638a-162">/m</span><span class="sxs-lookup"><span data-stu-id="f638a-162">/m</span></span> |<span data-ttu-id="f638a-163">Opt-in to Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="f638a-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="f638a-164">/nu</span><span class="sxs-lookup"><span data-stu-id="f638a-164">/nu</span></span> |<span data-ttu-id="f638a-165">Do not Check for updates after installation is complete</span><span class="sxs-lookup"><span data-stu-id="f638a-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="f638a-166">/d</span><span class="sxs-lookup"><span data-stu-id="f638a-166">/d</span></span> |<span data-ttu-id="f638a-167">Uninstalls Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="f638a-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="f638a-168">/ph</span><span class="sxs-lookup"><span data-stu-id="f638a-168">/ph</span></span> |<span data-ttu-id="f638a-169">Proxy Host Address</span><span class="sxs-lookup"><span data-stu-id="f638a-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="f638a-170">/po</span><span class="sxs-lookup"><span data-stu-id="f638a-170">/po</span></span> |<span data-ttu-id="f638a-171">Proxy Host Port Number</span><span class="sxs-lookup"><span data-stu-id="f638a-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="f638a-172">/pu</span><span class="sxs-lookup"><span data-stu-id="f638a-172">/pu</span></span> |<span data-ttu-id="f638a-173">Proxy Host UserName</span><span class="sxs-lookup"><span data-stu-id="f638a-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="f638a-174">/pw</span><span class="sxs-lookup"><span data-stu-id="f638a-174">/pw</span></span> |<span data-ttu-id="f638a-175">Proxy Password</span><span class="sxs-lookup"><span data-stu-id="f638a-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-to-a-recovery-services-vault"></a><span data-ttu-id="f638a-176">Registering DPM to a Recovery Services Vault</span><span class="sxs-lookup"><span data-stu-id="f638a-176">Registering DPM to a Recovery Services Vault</span></span>
<span data-ttu-id="f638a-177">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="f638a-177">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="f638a-178">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span><span class="sxs-lookup"><span data-stu-id="f638a-178">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="f638a-179">Initial configuration settings</span><span class="sxs-lookup"><span data-stu-id="f638a-179">Initial configuration settings</span></span>
<span data-ttu-id="f638a-180">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span><span class="sxs-lookup"><span data-stu-id="f638a-180">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="f638a-181">These subscription settings include Networking, Encryption and the Staging area.</span><span class="sxs-lookup"><span data-stu-id="f638a-181">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="f638a-182">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f638a-182">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="f638a-183">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-183">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="f638a-184">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span><span class="sxs-lookup"><span data-stu-id="f638a-184">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="f638a-185">The settings will not be applied and used by Azure Backup unless committed.</span><span class="sxs-lookup"><span data-stu-id="f638a-185">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="f638a-186">Networking</span><span class="sxs-lookup"><span data-stu-id="f638a-186">Networking</span></span>
<span data-ttu-id="f638a-187">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span><span class="sxs-lookup"><span data-stu-id="f638a-187">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="f638a-188">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-188">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="f638a-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span><span class="sxs-lookup"><span data-stu-id="f638a-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="f638a-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span><span class="sxs-lookup"><span data-stu-id="f638a-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="f638a-191">In this example, we are not setting any throttling.</span><span class="sxs-lookup"><span data-stu-id="f638a-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-the-staging-area"></a><span data-ttu-id="f638a-192">Configuring the staging Area</span><span class="sxs-lookup"><span data-stu-id="f638a-192">Configuring the staging Area</span></span>
<span data-ttu-id="f638a-193">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span><span class="sxs-lookup"><span data-stu-id="f638a-193">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="f638a-194">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span><span class="sxs-lookup"><span data-stu-id="f638a-194">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="f638a-195">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="f638a-195">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="f638a-196">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span><span class="sxs-lookup"><span data-stu-id="f638a-196">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="f638a-197">Encryption settings</span><span class="sxs-lookup"><span data-stu-id="f638a-197">Encryption settings</span></span>
<span data-ttu-id="f638a-198">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span><span class="sxs-lookup"><span data-stu-id="f638a-198">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="f638a-199">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span><span class="sxs-lookup"><span data-stu-id="f638a-199">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="f638a-200">It is important to keep this information safe and secure once it is set.</span><span class="sxs-lookup"><span data-stu-id="f638a-200">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="f638a-201">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="f638a-201">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="f638a-202">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span><span class="sxs-lookup"><span data-stu-id="f638a-202">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Keep the passphrase information safe and secure once it is set. You will not be able to restore data from Azure without this passphrase.
>
>

<span data-ttu-id="f638a-205">At this point, you should have made all the required changes to the ```$setting``` object.</span><span class="sxs-lookup"><span data-stu-id="f638a-205">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="f638a-206">Remember to commit the changes.</span><span class="sxs-lookup"><span data-stu-id="f638a-206">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="f638a-207">Protect data to Azure Backup</span><span class="sxs-lookup"><span data-stu-id="f638a-207">Protect data to Azure Backup</span></span>
<span data-ttu-id="f638a-208">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="f638a-208">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="f638a-209">In the examples, we will demonstrate how to back up files and folders.</span><span class="sxs-lookup"><span data-stu-id="f638a-209">In the examples, we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="f638a-210">The logic can easily be extended to backup any DPM-supported data source.</span><span class="sxs-lookup"><span data-stu-id="f638a-210">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="f638a-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span><span class="sxs-lookup"><span data-stu-id="f638a-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="f638a-212">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span><span class="sxs-lookup"><span data-stu-id="f638a-212">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="f638a-213">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span><span class="sxs-lookup"><span data-stu-id="f638a-213">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="f638a-214">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span><span class="sxs-lookup"><span data-stu-id="f638a-214">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="f638a-215">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span><span class="sxs-lookup"><span data-stu-id="f638a-215">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="f638a-216">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span><span class="sxs-lookup"><span data-stu-id="f638a-216">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="f638a-217">In our example we will protect data to the local disk and to the cloud.</span><span class="sxs-lookup"><span data-stu-id="f638a-217">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="f638a-218">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span><span class="sxs-lookup"><span data-stu-id="f638a-218">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="f638a-219">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span><span class="sxs-lookup"><span data-stu-id="f638a-219">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="f638a-220">Creating a protection group</span><span class="sxs-lookup"><span data-stu-id="f638a-220">Creating a protection group</span></span>
<span data-ttu-id="f638a-221">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-221">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="f638a-222">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="f638a-222">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="f638a-223">An existing protection group can also be modified later to add backup to the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="f638a-223">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="f638a-224">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-224">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="f638a-225">Adding group members to the Protection Group</span><span class="sxs-lookup"><span data-stu-id="f638a-225">Adding group members to the Protection Group</span></span>
<span data-ttu-id="f638a-226">Each DPM Agent knows the list of datasources on the server that it is installed on.</span><span class="sxs-lookup"><span data-stu-id="f638a-226">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="f638a-227">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span><span class="sxs-lookup"><span data-stu-id="f638a-227">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="f638a-228">One or more datasources are then selected and added to the Protection Group.</span><span class="sxs-lookup"><span data-stu-id="f638a-228">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="f638a-229">The PowerShell steps needed to achieve this are:</span><span class="sxs-lookup"><span data-stu-id="f638a-229">The PowerShell steps needed to achieve this are:</span></span>

1. <span data-ttu-id="f638a-230">Fetch a list of all servers managed by DPM through the DPM Agent.</span><span class="sxs-lookup"><span data-stu-id="f638a-230">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="f638a-231">Choose a specific server.</span><span class="sxs-lookup"><span data-stu-id="f638a-231">Choose a specific server.</span></span>
3. <span data-ttu-id="f638a-232">Fetch a list of all datasources on the server.</span><span class="sxs-lookup"><span data-stu-id="f638a-232">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="f638a-233">Choose one or more datasources and add them to the Protection Group</span><span class="sxs-lookup"><span data-stu-id="f638a-233">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="f638a-234">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-234">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="f638a-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span><span class="sxs-lookup"><span data-stu-id="f638a-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="f638a-236">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-236">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="f638a-237">In this example we are filtering for the volume \*D:\* that we want to configure for backup.</span><span class="sxs-lookup"><span data-stu-id="f638a-237">In this example we are filtering for the volume \*D:\* that we want to configure for backup.</span></span> <span data-ttu-id="f638a-238">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-238">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="f638a-239">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span><span class="sxs-lookup"><span data-stu-id="f638a-239">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="f638a-240">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span><span class="sxs-lookup"><span data-stu-id="f638a-240">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="f638a-241">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span><span class="sxs-lookup"><span data-stu-id="f638a-241">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="f638a-242">Selecting the data protection method</span><span class="sxs-lookup"><span data-stu-id="f638a-242">Selecting the data protection method</span></span>
<span data-ttu-id="f638a-243">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-243">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="f638a-244">In this example, the Protection Group is setup for local disk and cloud backup.</span><span class="sxs-lookup"><span data-stu-id="f638a-244">In this example, the Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="f638a-245">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span><span class="sxs-lookup"><span data-stu-id="f638a-245">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="f638a-246">Setting the retention range</span><span class="sxs-lookup"><span data-stu-id="f638a-246">Setting the retention range</span></span>
<span data-ttu-id="f638a-247">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-247">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="f638a-248">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span><span class="sxs-lookup"><span data-stu-id="f638a-248">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="f638a-249">It is always possible to set the backup schedule first and the retention policy after.</span><span class="sxs-lookup"><span data-stu-id="f638a-249">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="f638a-250">In the example below, the cmdlet sets the retention parameters for disk backups.</span><span class="sxs-lookup"><span data-stu-id="f638a-250">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="f638a-251">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span><span class="sxs-lookup"><span data-stu-id="f638a-251">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="f638a-252">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span><span class="sxs-lookup"><span data-stu-id="f638a-252">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span></span>  <span data-ttu-id="f638a-253">This setting prevents backups from becoming too large.</span><span class="sxs-lookup"><span data-stu-id="f638a-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="f638a-254">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="f638a-254">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="f638a-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span><span class="sxs-lookup"><span data-stu-id="f638a-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="f638a-256">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-256">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="f638a-257">Set the backup schedule</span><span class="sxs-lookup"><span data-stu-id="f638a-257">Set the backup schedule</span></span>
<span data-ttu-id="f638a-258">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-258">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="f638a-259">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-259">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="f638a-260">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span><span class="sxs-lookup"><span data-stu-id="f638a-260">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="f638a-261">```$onlineSch[0]``` contains the daily schedule</span><span class="sxs-lookup"><span data-stu-id="f638a-261">```$onlineSch[0]``` contains the daily schedule</span></span>
2. <span data-ttu-id="f638a-262">```$onlineSch[1]``` contains the weekly schedule</span><span class="sxs-lookup"><span data-stu-id="f638a-262">```$onlineSch[1]``` contains the weekly schedule</span></span>
3. <span data-ttu-id="f638a-263">```$onlineSch[2]``` contains the monthly schedule</span><span class="sxs-lookup"><span data-stu-id="f638a-263">```$onlineSch[2]``` contains the monthly schedule</span></span>
4. <span data-ttu-id="f638a-264">```$onlineSch[3]``` contains the yearly schedule</span><span class="sxs-lookup"><span data-stu-id="f638a-264">```$onlineSch[3]``` contains the yearly schedule</span></span>

<span data-ttu-id="f638a-265">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="f638a-265">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="f638a-266">Initial backup</span><span class="sxs-lookup"><span data-stu-id="f638a-266">Initial backup</span></span>
<span data-ttu-id="f638a-267">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span><span class="sxs-lookup"><span data-stu-id="f638a-267">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="f638a-268">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="f638a-268">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="f638a-269">Changing the size of DPM Replica & recovery point volume</span><span class="sxs-lookup"><span data-stu-id="f638a-269">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="f638a-270">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="f638a-270">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="f638a-271">Committing the changes to the Protection Group</span><span class="sxs-lookup"><span data-stu-id="f638a-271">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="f638a-272">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span><span class="sxs-lookup"><span data-stu-id="f638a-272">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="f638a-273">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-273">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="f638a-274">View the backup points</span><span class="sxs-lookup"><span data-stu-id="f638a-274">View the backup points</span></span>
<span data-ttu-id="f638a-275">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span><span class="sxs-lookup"><span data-stu-id="f638a-275">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="f638a-276">In this example, we will:</span><span class="sxs-lookup"><span data-stu-id="f638a-276">In this example, we will:</span></span>

* <span data-ttu-id="f638a-277">fetch all the PGs on the DPM server and stored in an array ```$PG```</span><span class="sxs-lookup"><span data-stu-id="f638a-277">fetch all the PGs on the DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="f638a-278">get the datasources corresponding to the ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="f638a-278">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="f638a-279">get all the recovery points for a datasource.</span><span class="sxs-lookup"><span data-stu-id="f638a-279">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="f638a-280">Restore data protected on Azure</span><span class="sxs-lookup"><span data-stu-id="f638a-280">Restore data protected on Azure</span></span>
<span data-ttu-id="f638a-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span><span class="sxs-lookup"><span data-stu-id="f638a-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="f638a-282">In the previous section, we got a list of the backup points for a datasource.</span><span class="sxs-lookup"><span data-stu-id="f638a-282">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="f638a-283">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span><span class="sxs-lookup"><span data-stu-id="f638a-283">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="f638a-284">This example includes:</span><span class="sxs-lookup"><span data-stu-id="f638a-284">This example includes:</span></span>

* <span data-ttu-id="f638a-285">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-285">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="f638a-286">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f638a-286">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="f638a-287">Choosing a backup point to restore from.</span><span class="sxs-lookup"><span data-stu-id="f638a-287">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="f638a-288">The commands can easily be extended for any datasource type.</span><span class="sxs-lookup"><span data-stu-id="f638a-288">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f638a-289">Next steps</span><span class="sxs-lookup"><span data-stu-id="f638a-289">Next steps</span></span>
* <span data-ttu-id="f638a-290">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="f638a-290">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>

