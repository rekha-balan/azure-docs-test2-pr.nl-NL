---
title: Azure Backup - Use PowerShell to back up DPM workloads
description: Learn how to deploy and manage Azure Backup for Data Protection Manager (DPM) using PowerShell
services: backup
author: NKolli1
manager: shreeshd
ms.service: backup
ms.topic: conceptual
ms.date: 1/23/2017
ms.author: adigan
ms.openlocfilehash: 4a74aa674bd80f3d1297e71873eb9d71e46fd4cb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814085"
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="97121-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span><span class="sxs-lookup"><span data-stu-id="97121-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
<span data-ttu-id="97121-104">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span><span class="sxs-lookup"><span data-stu-id="97121-104">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span></span>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="97121-105">Setting up the PowerShell environment</span><span class="sxs-lookup"><span data-stu-id="97121-105">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="97121-106">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97121-106">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span></span> <span data-ttu-id="97121-107">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span><span class="sxs-lookup"><span data-stu-id="97121-107">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="97121-108">Setup and Registration</span><span class="sxs-lookup"><span data-stu-id="97121-108">Setup and Registration</span></span>
<span data-ttu-id="97121-109">To begin:</span><span class="sxs-lookup"><span data-stu-id="97121-109">To begin:</span></span>

1. <span data-ttu-id="97121-110">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="97121-110">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="97121-111">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span><span class="sxs-lookup"><span data-stu-id="97121-111">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="97121-112">The following setup and registration tasks can be automated with PowerShell:</span><span class="sxs-lookup"><span data-stu-id="97121-112">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="97121-113">Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="97121-113">Create a Recovery Services vault</span></span>
* <span data-ttu-id="97121-114">Installing the Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="97121-114">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="97121-115">Registering with the Azure Backup service</span><span class="sxs-lookup"><span data-stu-id="97121-115">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="97121-116">Networking settings</span><span class="sxs-lookup"><span data-stu-id="97121-116">Networking settings</span></span>
* <span data-ttu-id="97121-117">Encryption settings</span><span class="sxs-lookup"><span data-stu-id="97121-117">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="97121-118">Create a recovery services vault</span><span class="sxs-lookup"><span data-stu-id="97121-118">Create a recovery services vault</span></span>
<span data-ttu-id="97121-119">The following steps lead you through creating a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="97121-119">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="97121-120">A Recovery Services vault is different than a Backup vault.</span><span class="sxs-lookup"><span data-stu-id="97121-120">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="97121-121">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span><span class="sxs-lookup"><span data-stu-id="97121-121">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="97121-122">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span><span class="sxs-lookup"><span data-stu-id="97121-122">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="97121-123">You can use an existing resource group, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="97121-123">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="97121-124">When creating a new resource group, specify the name and location for the resource group.</span><span class="sxs-lookup"><span data-stu-id="97121-124">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="97121-125">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span><span class="sxs-lookup"><span data-stu-id="97121-125">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span></span> <span data-ttu-id="97121-126">Be sure to specify the same location for the vault as was used for the resource group.</span><span class="sxs-lookup"><span data-stu-id="97121-126">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="97121-127">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy-lrs.md) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy-grs.md).</span><span class="sxs-lookup"><span data-stu-id="97121-127">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy-lrs.md) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy-grs.md).</span></span> <span data-ttu-id="97121-128">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="97121-128">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="97121-129">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span><span class="sxs-lookup"><span data-stu-id="97121-129">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="97121-130">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span><span class="sxs-lookup"><span data-stu-id="97121-130">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="97121-131">View the vaults in a subscription</span><span class="sxs-lookup"><span data-stu-id="97121-131">View the vaults in a subscription</span></span>
<span data-ttu-id="97121-132">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="97121-132">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="97121-133">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span><span class="sxs-lookup"><span data-stu-id="97121-133">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="97121-134">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span><span class="sxs-lookup"><span data-stu-id="97121-134">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="97121-135">Installing the Azure Backup agent on a DPM Server</span><span class="sxs-lookup"><span data-stu-id="97121-135">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="97121-136">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span><span class="sxs-lookup"><span data-stu-id="97121-136">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="97121-137">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span><span class="sxs-lookup"><span data-stu-id="97121-137">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="97121-138">Save the installer to an easily accessible location like \*C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="97121-138">Save the installer to an easily accessible location like \*C:\Downloads\*.</span></span>

<span data-ttu-id="97121-139">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span><span class="sxs-lookup"><span data-stu-id="97121-139">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="97121-140">This installs the agent with all the default options.</span><span class="sxs-lookup"><span data-stu-id="97121-140">This installs the agent with all the default options.</span></span> <span data-ttu-id="97121-141">The installation takes a few minutes in the background.</span><span class="sxs-lookup"><span data-stu-id="97121-141">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="97121-142">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span><span class="sxs-lookup"><span data-stu-id="97121-142">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="97121-143">The agent shows up in the list of installed programs.</span><span class="sxs-lookup"><span data-stu-id="97121-143">The agent shows up in the list of installed programs.</span></span> <span data-ttu-id="97121-144">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span><span class="sxs-lookup"><span data-stu-id="97121-144">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent installed](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="97121-146">Installation options</span><span class="sxs-lookup"><span data-stu-id="97121-146">Installation options</span></span>
<span data-ttu-id="97121-147">To see all the options available via the commandline, use the following command:</span><span class="sxs-lookup"><span data-stu-id="97121-147">To see all the options available via the commandline, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="97121-148">The available options include:</span><span class="sxs-lookup"><span data-stu-id="97121-148">The available options include:</span></span>

| <span data-ttu-id="97121-149">Option</span><span class="sxs-lookup"><span data-stu-id="97121-149">Option</span></span> | <span data-ttu-id="97121-150">Details</span><span class="sxs-lookup"><span data-stu-id="97121-150">Details</span></span> | <span data-ttu-id="97121-151">Default</span><span class="sxs-lookup"><span data-stu-id="97121-151">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97121-152">/q</span><span class="sxs-lookup"><span data-stu-id="97121-152">/q</span></span> |<span data-ttu-id="97121-153">Quiet installation</span><span class="sxs-lookup"><span data-stu-id="97121-153">Quiet installation</span></span> |- |
| <span data-ttu-id="97121-154">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="97121-154">/p:"location"</span></span> |<span data-ttu-id="97121-155">Path to the installation folder for the Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="97121-155">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="97121-156">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="97121-156">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="97121-157">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="97121-157">/s:"location"</span></span> |<span data-ttu-id="97121-158">Path to the cache folder for the Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="97121-158">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="97121-159">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="97121-159">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="97121-160">/m</span><span class="sxs-lookup"><span data-stu-id="97121-160">/m</span></span> |<span data-ttu-id="97121-161">Opt-in to Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="97121-161">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="97121-162">/nu</span><span class="sxs-lookup"><span data-stu-id="97121-162">/nu</span></span> |<span data-ttu-id="97121-163">Do not Check for updates after installation is complete</span><span class="sxs-lookup"><span data-stu-id="97121-163">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="97121-164">/d</span><span class="sxs-lookup"><span data-stu-id="97121-164">/d</span></span> |<span data-ttu-id="97121-165">Uninstalls Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="97121-165">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="97121-166">/ph</span><span class="sxs-lookup"><span data-stu-id="97121-166">/ph</span></span> |<span data-ttu-id="97121-167">Proxy Host Address</span><span class="sxs-lookup"><span data-stu-id="97121-167">Proxy Host Address</span></span> |- |
| <span data-ttu-id="97121-168">/po</span><span class="sxs-lookup"><span data-stu-id="97121-168">/po</span></span> |<span data-ttu-id="97121-169">Proxy Host Port Number</span><span class="sxs-lookup"><span data-stu-id="97121-169">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="97121-170">/pu</span><span class="sxs-lookup"><span data-stu-id="97121-170">/pu</span></span> |<span data-ttu-id="97121-171">Proxy Host UserName</span><span class="sxs-lookup"><span data-stu-id="97121-171">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="97121-172">/pw</span><span class="sxs-lookup"><span data-stu-id="97121-172">/pw</span></span> |<span data-ttu-id="97121-173">Proxy Password</span><span class="sxs-lookup"><span data-stu-id="97121-173">Proxy Password</span></span> |- |

## <a name="registering-dpm-to-a-recovery-services-vault"></a><span data-ttu-id="97121-174">Registering DPM to a Recovery Services Vault</span><span class="sxs-lookup"><span data-stu-id="97121-174">Registering DPM to a Recovery Services Vault</span></span>
<span data-ttu-id="97121-175">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="97121-175">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="97121-176">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span><span class="sxs-lookup"><span data-stu-id="97121-176">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="97121-177">Initial configuration settings</span><span class="sxs-lookup"><span data-stu-id="97121-177">Initial configuration settings</span></span>
<span data-ttu-id="97121-178">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span><span class="sxs-lookup"><span data-stu-id="97121-178">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="97121-179">These subscription settings include Networking, Encryption and the Staging area.</span><span class="sxs-lookup"><span data-stu-id="97121-179">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="97121-180">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="97121-180">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="97121-181">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-181">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="97121-182">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span><span class="sxs-lookup"><span data-stu-id="97121-182">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="97121-183">The settings will not be applied and used by Azure Backup unless committed.</span><span class="sxs-lookup"><span data-stu-id="97121-183">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="97121-184">Networking</span><span class="sxs-lookup"><span data-stu-id="97121-184">Networking</span></span>
<span data-ttu-id="97121-185">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span><span class="sxs-lookup"><span data-stu-id="97121-185">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="97121-186">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-186">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="97121-187">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span><span class="sxs-lookup"><span data-stu-id="97121-187">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="97121-188">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span><span class="sxs-lookup"><span data-stu-id="97121-188">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="97121-189">In this example, we are not setting any throttling.</span><span class="sxs-lookup"><span data-stu-id="97121-189">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-the-staging-area"></a><span data-ttu-id="97121-190">Configuring the staging Area</span><span class="sxs-lookup"><span data-stu-id="97121-190">Configuring the staging Area</span></span>
<span data-ttu-id="97121-191">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span><span class="sxs-lookup"><span data-stu-id="97121-191">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="97121-192">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span><span class="sxs-lookup"><span data-stu-id="97121-192">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="97121-193">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="97121-193">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="97121-194">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span><span class="sxs-lookup"><span data-stu-id="97121-194">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="97121-195">Encryption settings</span><span class="sxs-lookup"><span data-stu-id="97121-195">Encryption settings</span></span>
<span data-ttu-id="97121-196">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span><span class="sxs-lookup"><span data-stu-id="97121-196">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="97121-197">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span><span class="sxs-lookup"><span data-stu-id="97121-197">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="97121-198">It is important to keep this information safe and secure once it is set.</span><span class="sxs-lookup"><span data-stu-id="97121-198">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="97121-199">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="97121-199">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="97121-200">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span><span class="sxs-lookup"><span data-stu-id="97121-200">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="97121-201">Keep the passphrase information safe and secure once it is set.</span><span class="sxs-lookup"><span data-stu-id="97121-201">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="97121-202">You will not be able to restore data from Azure without this passphrase.</span><span class="sxs-lookup"><span data-stu-id="97121-202">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="97121-203">At this point, you should have made all the required changes to the ```$setting``` object.</span><span class="sxs-lookup"><span data-stu-id="97121-203">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="97121-204">Remember to commit the changes.</span><span class="sxs-lookup"><span data-stu-id="97121-204">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="97121-205">Protect data to Azure Backup</span><span class="sxs-lookup"><span data-stu-id="97121-205">Protect data to Azure Backup</span></span>
<span data-ttu-id="97121-206">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="97121-206">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="97121-207">In the examples, we will demonstrate how to back up files and folders.</span><span class="sxs-lookup"><span data-stu-id="97121-207">In the examples, we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="97121-208">The logic can easily be extended to backup any DPM-supported data source.</span><span class="sxs-lookup"><span data-stu-id="97121-208">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="97121-209">All your DPM backups are governed by a Protection Group (PG) with four parts:</span><span class="sxs-lookup"><span data-stu-id="97121-209">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="97121-210">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span><span class="sxs-lookup"><span data-stu-id="97121-210">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="97121-211">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span><span class="sxs-lookup"><span data-stu-id="97121-211">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="97121-212">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span><span class="sxs-lookup"><span data-stu-id="97121-212">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="97121-213">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span><span class="sxs-lookup"><span data-stu-id="97121-213">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="97121-214">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span><span class="sxs-lookup"><span data-stu-id="97121-214">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="97121-215">In our example we will protect data to the local disk and to the cloud.</span><span class="sxs-lookup"><span data-stu-id="97121-215">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="97121-216">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span><span class="sxs-lookup"><span data-stu-id="97121-216">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="97121-217">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span><span class="sxs-lookup"><span data-stu-id="97121-217">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="97121-218">Creating a protection group</span><span class="sxs-lookup"><span data-stu-id="97121-218">Creating a protection group</span></span>
<span data-ttu-id="97121-219">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-219">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="97121-220">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="97121-220">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="97121-221">An existing protection group can also be modified later to add backup to the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="97121-221">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="97121-222">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-222">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="97121-223">Adding group members to the Protection Group</span><span class="sxs-lookup"><span data-stu-id="97121-223">Adding group members to the Protection Group</span></span>
<span data-ttu-id="97121-224">Each DPM Agent knows the list of datasources on the server that it is installed on.</span><span class="sxs-lookup"><span data-stu-id="97121-224">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="97121-225">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span><span class="sxs-lookup"><span data-stu-id="97121-225">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="97121-226">One or more datasources are then selected and added to the Protection Group.</span><span class="sxs-lookup"><span data-stu-id="97121-226">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="97121-227">The PowerShell steps needed to achieve this are:</span><span class="sxs-lookup"><span data-stu-id="97121-227">The PowerShell steps needed to achieve this are:</span></span>

1. <span data-ttu-id="97121-228">Fetch a list of all servers managed by DPM through the DPM Agent.</span><span class="sxs-lookup"><span data-stu-id="97121-228">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="97121-229">Choose a specific server.</span><span class="sxs-lookup"><span data-stu-id="97121-229">Choose a specific server.</span></span>
3. <span data-ttu-id="97121-230">Fetch a list of all datasources on the server.</span><span class="sxs-lookup"><span data-stu-id="97121-230">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="97121-231">Choose one or more datasources and add them to the Protection Group</span><span class="sxs-lookup"><span data-stu-id="97121-231">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="97121-232">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-232">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="97121-233">In this example we will filter and only configure PS with name *productionserver01* for backup.</span><span class="sxs-lookup"><span data-stu-id="97121-233">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”}
```

<span data-ttu-id="97121-234">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-234">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="97121-235">In this example we are filtering for the volume \*D:\* that we want to configure for backup.</span><span class="sxs-lookup"><span data-stu-id="97121-235">In this example we are filtering for the volume \*D:\* that we want to configure for backup.</span></span> <span data-ttu-id="97121-236">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-236">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="97121-237">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span><span class="sxs-lookup"><span data-stu-id="97121-237">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="97121-238">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span><span class="sxs-lookup"><span data-stu-id="97121-238">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="97121-239">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span><span class="sxs-lookup"><span data-stu-id="97121-239">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="97121-240">Selecting the data protection method</span><span class="sxs-lookup"><span data-stu-id="97121-240">Selecting the data protection method</span></span>
<span data-ttu-id="97121-241">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-241">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="97121-242">In this example, the Protection Group is setup for local disk and cloud backup.</span><span class="sxs-lookup"><span data-stu-id="97121-242">In this example, the Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="97121-243">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span><span class="sxs-lookup"><span data-stu-id="97121-243">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="97121-244">Setting the retention range</span><span class="sxs-lookup"><span data-stu-id="97121-244">Setting the retention range</span></span>
<span data-ttu-id="97121-245">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-245">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="97121-246">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span><span class="sxs-lookup"><span data-stu-id="97121-246">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="97121-247">It is always possible to set the backup schedule first and the retention policy after.</span><span class="sxs-lookup"><span data-stu-id="97121-247">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="97121-248">In the example below, the cmdlet sets the retention parameters for disk backups.</span><span class="sxs-lookup"><span data-stu-id="97121-248">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="97121-249">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span><span class="sxs-lookup"><span data-stu-id="97121-249">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="97121-250">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span><span class="sxs-lookup"><span data-stu-id="97121-250">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span></span>  <span data-ttu-id="97121-251">This setting prevents backups from becoming too large.</span><span class="sxs-lookup"><span data-stu-id="97121-251">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="97121-252">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="97121-252">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="97121-253">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span><span class="sxs-lookup"><span data-stu-id="97121-253">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="97121-254">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-254">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="97121-255">Set the backup schedule</span><span class="sxs-lookup"><span data-stu-id="97121-255">Set the backup schedule</span></span>
<span data-ttu-id="97121-256">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-256">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="97121-257">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-257">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="97121-258">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span><span class="sxs-lookup"><span data-stu-id="97121-258">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="97121-259">```$onlineSch[0]``` contains the daily schedule</span><span class="sxs-lookup"><span data-stu-id="97121-259">```$onlineSch[0]``` contains the daily schedule</span></span>
2. <span data-ttu-id="97121-260">```$onlineSch[1]``` contains the weekly schedule</span><span class="sxs-lookup"><span data-stu-id="97121-260">```$onlineSch[1]``` contains the weekly schedule</span></span>
3. <span data-ttu-id="97121-261">```$onlineSch[2]``` contains the monthly schedule</span><span class="sxs-lookup"><span data-stu-id="97121-261">```$onlineSch[2]``` contains the monthly schedule</span></span>
4. <span data-ttu-id="97121-262">```$onlineSch[3]``` contains the yearly schedule</span><span class="sxs-lookup"><span data-stu-id="97121-262">```$onlineSch[3]``` contains the yearly schedule</span></span>

<span data-ttu-id="97121-263">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="97121-263">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="97121-264">Initial backup</span><span class="sxs-lookup"><span data-stu-id="97121-264">Initial backup</span></span>
<span data-ttu-id="97121-265">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span><span class="sxs-lookup"><span data-stu-id="97121-265">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="97121-266">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="97121-266">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="97121-267">Changing the size of DPM Replica & recovery point volume</span><span class="sxs-lookup"><span data-stu-id="97121-267">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="97121-268">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="97121-268">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="97121-269">Committing the changes to the Protection Group</span><span class="sxs-lookup"><span data-stu-id="97121-269">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="97121-270">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span><span class="sxs-lookup"><span data-stu-id="97121-270">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="97121-271">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-271">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="97121-272">View the backup points</span><span class="sxs-lookup"><span data-stu-id="97121-272">View the backup points</span></span>
<span data-ttu-id="97121-273">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span><span class="sxs-lookup"><span data-stu-id="97121-273">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="97121-274">In this example, we will:</span><span class="sxs-lookup"><span data-stu-id="97121-274">In this example, we will:</span></span>

* <span data-ttu-id="97121-275">fetch all the PGs on the DPM server and stored in an array ```$PG```</span><span class="sxs-lookup"><span data-stu-id="97121-275">fetch all the PGs on the DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="97121-276">get the datasources corresponding to the ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="97121-276">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="97121-277">get all the recovery points for a datasource.</span><span class="sxs-lookup"><span data-stu-id="97121-277">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="97121-278">Restore data protected on Azure</span><span class="sxs-lookup"><span data-stu-id="97121-278">Restore data protected on Azure</span></span>
<span data-ttu-id="97121-279">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span><span class="sxs-lookup"><span data-stu-id="97121-279">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="97121-280">In the previous section, we got a list of the backup points for a datasource.</span><span class="sxs-lookup"><span data-stu-id="97121-280">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="97121-281">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span><span class="sxs-lookup"><span data-stu-id="97121-281">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="97121-282">This example includes:</span><span class="sxs-lookup"><span data-stu-id="97121-282">This example includes:</span></span>

* <span data-ttu-id="97121-283">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-283">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="97121-284">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97121-284">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="97121-285">Choosing a backup point to restore from.</span><span class="sxs-lookup"><span data-stu-id="97121-285">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="97121-286">The commands can easily be extended for any datasource type.</span><span class="sxs-lookup"><span data-stu-id="97121-286">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97121-287">Next steps</span><span class="sxs-lookup"><span data-stu-id="97121-287">Next steps</span></span>
* <span data-ttu-id="97121-288">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="97121-288">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
