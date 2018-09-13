---
title: Desired State Configuration for Azure Overview | Microsoft Docs
description: Overview for using the Microsoft Azure extension handler for PowerShell Desired State Configuration. Including prerequisites, architecture, cmdlets..
services: virtual-machines-windows
documentationcenter: ''
author: zjalexander
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
keywords: ''
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: 46de2a88df91ea7a0a318abd2e519a341e7284c5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551216"
---
# <a name="introduction-to-the-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="9dd6c-104">Introduction to the Azure Desired State Configuration extension handler</span><span class="sxs-lookup"><span data-stu-id="9dd6c-104">Introduction to the Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="9dd6c-105">The Azure VM Agent and associated Extensions are part of the Microsoft Azure Infrastructure Services.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-105">The Azure VM Agent and associated Extensions are part of the Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="9dd6c-106">VM Extensions are software components that extend the VM functionality and simplify various VM management operations.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-106">VM Extensions are software components that extend the VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="9dd6c-107">For example, the VMAccess extension can be used to reset an administrator's password, or the Custom Script extension can be used to execute a script on the VM.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-107">For example, the VMAccess extension can be used to reset an administrator's password, or the Custom Script extension can be used to execute a script on the VM.</span></span>

<span data-ttu-id="9dd6c-108">This article introduces the PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of the Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-108">This article introduces the PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of the Azure PowerShell SDK.</span></span> <span data-ttu-id="9dd6c-109">You can use new cmdlets to upload and apply a PowerShell DSC configuration on an Azure VM enabled with the PowerShell DSC extension.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-109">You can use new cmdlets to upload and apply a PowerShell DSC configuration on an Azure VM enabled with the PowerShell DSC extension.</span></span> <span data-ttu-id="9dd6c-110">The PowerShell DSC extension calls into PowerShell DSC to enact the received DSC configuration on the VM.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-110">The PowerShell DSC extension calls into PowerShell DSC to enact the received DSC configuration on the VM.</span></span> <span data-ttu-id="9dd6c-111">This functionality is also available through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-111">This functionality is also available through the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9dd6c-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9dd6c-112">Prerequisites</span></span>
<span data-ttu-id="9dd6c-113">**Local machine** To interact with the Azure VM extension, you need to use either the Azure portal or the Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-113">**Local machine** To interact with the Azure VM extension, you need to use either the Azure portal or the Azure PowerShell SDK.</span></span> 

<span data-ttu-id="9dd6c-114">**Guest Agent** The Azure VM that is configured by the DSC configuration needs to be an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-114">**Guest Agent** The Azure VM that is configured by the DSC configuration needs to be an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="9dd6c-115">The full list of supported OS versions can be found at the [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span><span class="sxs-lookup"><span data-stu-id="9dd6c-115">The full list of supported OS versions can be found at the [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="9dd6c-116">Terms and concepts</span><span class="sxs-lookup"><span data-stu-id="9dd6c-116">Terms and concepts</span></span>
<span data-ttu-id="9dd6c-117">This guide presumes familiarity with the following concepts:</span><span class="sxs-lookup"><span data-stu-id="9dd6c-117">This guide presumes familiarity with the following concepts:</span></span>

<span data-ttu-id="9dd6c-118">Configuration - A DSC configuration document.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="9dd6c-119">Node - A target for a DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="9dd6c-120">In this document, "node" always refers to an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-120">In this document, "node" always refers to an Azure VM.</span></span>

<span data-ttu-id="9dd6c-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span><span class="sxs-lookup"><span data-stu-id="9dd6c-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="9dd6c-122">Architectural overview</span><span class="sxs-lookup"><span data-stu-id="9dd6c-122">Architectural overview</span></span>
<span data-ttu-id="9dd6c-123">The Azure DSC extension uses the Azure VM Agent framework to deliver, enact, and report on DSC configurations running on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-123">The Azure DSC extension uses the Azure VM Agent framework to deliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="9dd6c-124">The DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through the Azure PowerShell SDK or through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-124">The DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through the Azure PowerShell SDK or through the Azure portal.</span></span>

<span data-ttu-id="9dd6c-125">When the extension is called for the first time, it runs an installation process.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-125">When the extension is called for the first time, it runs an installation process.</span></span> <span data-ttu-id="9dd6c-126">This process installs a version of the Windows Management Framework (WMF) using the following logic:</span><span class="sxs-lookup"><span data-stu-id="9dd6c-126">This process installs a version of the Windows Management Framework (WMF) using the following logic:</span></span>

1. <span data-ttu-id="9dd6c-127">If the Azure VM OS is Windows Server 2016, no action is taken.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-127">If the Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="9dd6c-128">Windows Server 2016 already has the latest version of PowerShell installed.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-128">Windows Server 2016 already has the latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="9dd6c-129">If the `wmfVersion` property is specified, that version of the WMF is installed unless it is incompatible with the VM's OS.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-129">If the `wmfVersion` property is specified, that version of the WMF is installed unless it is incompatible with the VM's OS.</span></span>
3. <span data-ttu-id="9dd6c-130">If no `wmfVersion` property is specified, the latest applicable version of the WMF is installed.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-130">If no `wmfVersion` property is specified, the latest applicable version of the WMF is installed.</span></span>

<span data-ttu-id="9dd6c-131">Installation of the WMF requires a reboot.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-131">Installation of the WMF requires a reboot.</span></span> <span data-ttu-id="9dd6c-132">After reboot, the extension downloads the .zip file specified in the `modulesUrl` property.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-132">After reboot, the extension downloads the .zip file specified in the `modulesUrl` property.</span></span> <span data-ttu-id="9dd6c-133">If this location is in Azure blob storage, a SAS token can be specified in the `sasToken` property to access the file.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-133">If this location is in Azure blob storage, a SAS token can be specified in the `sasToken` property to access the file.</span></span> <span data-ttu-id="9dd6c-134">After the .zip is downloaded and unpacked, the configuration function defined in `configurationFunction` is run to generate the MOF file.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-134">After the .zip is downloaded and unpacked, the configuration function defined in `configurationFunction` is run to generate the MOF file.</span></span> <span data-ttu-id="9dd6c-135">The extension then runs `Start-DscConfiguration -Force` on the generated MOF file.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-135">The extension then runs `Start-DscConfiguration -Force` on the generated MOF file.</span></span> <span data-ttu-id="9dd6c-136">The extension captures output and writes it back out to the Azure Status Channel.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-136">The extension captures output and writes it back out to the Azure Status Channel.</span></span> <span data-ttu-id="9dd6c-137">From this point on, the DSC LCM handles monitoring and correction as normal.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-137">From this point on, the DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="9dd6c-138">PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="9dd6c-138">PowerShell cmdlets</span></span>
<span data-ttu-id="9dd6c-139">PowerShell cmdlets can be used with Azure Resource Manager or the classic deployment model to package, publish, and monitor DSC extension deployments.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-139">PowerShell cmdlets can be used with Azure Resource Manager or the classic deployment model to package, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="9dd6c-140">The following cmdlets listed are the classic deployment modules, but "Azure" can be replaced with "AzureRm" to use the Azure Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-140">The following cmdlets listed are the classic deployment modules, but "Azure" can be replaced with "AzureRm" to use the Azure Resource Manager model.</span></span> <span data-ttu-id="9dd6c-141">For example,  `Publish-AzureVMDscConfiguration` uses the classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-141">For example,  `Publish-AzureVMDscConfiguration` uses the classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="9dd6c-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing the configuration and DSC resources needed to enact the configuration.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing the configuration and DSC resources needed to enact the configuration.</span></span> <span data-ttu-id="9dd6c-143">It can also create the package locally using the `-ConfigurationArchivePath` parameter.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-143">It can also create the package locally using the `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="9dd6c-144">Otherwise, it publishes the .zip file to Azure blob storage and secures it with a SAS token.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-144">Otherwise, it publishes the .zip file to Azure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="9dd6c-145">The .zip file created by this cmdlet has the .ps1 configuration script at the root of the archive folder.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-145">The .zip file created by this cmdlet has the .ps1 configuration script at the root of the archive folder.</span></span> <span data-ttu-id="9dd6c-146">Resources have the module folder placed in the archive folder.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-146">Resources have the module folder placed in the archive folder.</span></span> 

<span data-ttu-id="9dd6c-147">`Set-AzureVMDscExtension` injects the settings needed by the PowerShell DSC extension into a VM configuration object.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-147">`Set-AzureVMDscExtension` injects the settings needed by the PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="9dd6c-148">In the classic deployment model, the VM changes must be applied to an Azure VM with `Update-AzureVM`.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-148">In the classic deployment model, the VM changes must be applied to an Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="9dd6c-149">`Get-AzureVMDscExtension` retrieves the DSC extension status of a particular VM.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-149">`Get-AzureVMDscExtension` retrieves the DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="9dd6c-150">`Get-AzureVMDscExtensionStatus` retrieves the status of the DSC configuration enacted by the DSC extension handler.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-150">`Get-AzureVMDscExtensionStatus` retrieves the status of the DSC configuration enacted by the DSC extension handler.</span></span> <span data-ttu-id="9dd6c-151">This action can be performed on a single VM, or group of VMs.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="9dd6c-152">`Remove-AzureVMDscExtension` removes the extension handler from a given virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-152">`Remove-AzureVMDscExtension` removes the extension handler from a given virtual machine.</span></span> <span data-ttu-id="9dd6c-153">This cmdlet does **not** remove the configuration, uninstall the WMF, or change the applied settings on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-153">This cmdlet does **not** remove the configuration, uninstall the WMF, or change the applied settings on the virtual machine.</span></span> <span data-ttu-id="9dd6c-154">It only removes the extension handler.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-154">It only removes the extension handler.</span></span> 

<span data-ttu-id="9dd6c-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span><span class="sxs-lookup"><span data-stu-id="9dd6c-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="9dd6c-156">Azure Resource Manager cmdlets are synchronous.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="9dd6c-157">ASM cmdlets are asynchronous.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="9dd6c-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="9dd6c-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="9dd6c-160">You can specify this parameter when your storage account belongs to a different resource group than the one where the virtual machine is created.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-160">You can specify this parameter when your storage account belongs to a different resource group than the one where the virtual machine is created.</span></span>
* <span data-ttu-id="9dd6c-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9dd6c-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="9dd6c-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9dd6c-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="9dd6c-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9dd6c-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="9dd6c-164">The AutoUpdate switch has been added to Azure Resource Manager to enable automatic updating of the extension handler to the latest version as and when it is available.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-164">The AutoUpdate switch has been added to Azure Resource Manager to enable automatic updating of the extension handler to the latest version as and when it is available.</span></span> <span data-ttu-id="9dd6c-165">Note this parameter has the potential to cause reboots on the VM when a new version of the WMF is released.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-165">Note this parameter has the potential to cause reboots on the VM when a new version of the WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="9dd6c-166">Azure portal functionality</span><span class="sxs-lookup"><span data-stu-id="9dd6c-166">Azure portal functionality</span></span>
<span data-ttu-id="9dd6c-167">Browse to a VM.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-167">Browse to a VM.</span></span> <span data-ttu-id="9dd6c-168">Under Settings -> General click "Extensions."</span><span class="sxs-lookup"><span data-stu-id="9dd6c-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="9dd6c-169">A new pane is created.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-169">A new pane is created.</span></span> <span data-ttu-id="9dd6c-170">Click "Add" and select PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="9dd6c-171">The portal needs input.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-171">The portal needs input.</span></span>
<span data-ttu-id="9dd6c-172">**Configuration Modules or Script**: This field is mandatory.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="9dd6c-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at the root, and all dependent resources in module folders within the .zip.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at the root, and all dependent resources in module folders within the .zip.</span></span> <span data-ttu-id="9dd6c-174">It can be created with the `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in the Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-174">It can be created with the `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in the Azure PowerShell SDK.</span></span> <span data-ttu-id="9dd6c-175">The .zip file is uploaded into your user blob storage secured by a SAS token.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-175">The .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="9dd6c-176">**Configuration Data PSD1 File**: This field is optional.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="9dd6c-177">If your configuration requires a configuration data file in .psd1, use this field to select it and upload it to your user blob storage, where it is secured by a SAS token.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-177">If your configuration requires a configuration data file in .psd1, use this field to select it and upload it to your user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="9dd6c-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="9dd6c-179">Enter the name of the configuration .ps1 script followed by a  '\' and the name of the configuration function.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-179">Enter the name of the configuration .ps1 script followed by a  '\' and the name of the configuration function.</span></span> <span data-ttu-id="9dd6c-180">For example, if your .ps1 script has the name "configuration.ps1", and the configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="9dd6c-180">For example, if your .ps1 script has the name "configuration.ps1", and the configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="9dd6c-181">**Configuration Arguments**: If the configuration function takes arguments, enter them in here in the format `argumentName1=value1,argumentName2=value2`.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-181">**Configuration Arguments**: If the configuration function takes arguments, enter them in here in the format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="9dd6c-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="9dd6c-183">Getting started</span><span class="sxs-lookup"><span data-stu-id="9dd6c-183">Getting started</span></span>
<span data-ttu-id="9dd6c-184">The Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-184">The Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="9dd6c-185">A simple example of a configuration follows.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="9dd6c-186">Save it locally as "IisInstall.ps1":</span><span class="sxs-lookup"><span data-stu-id="9dd6c-186">Save it locally as "IisInstall.ps1":</span></span>

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

<span data-ttu-id="9dd6c-187">The following steps place the IisInstall.ps1 script on the specified VM, execute the configuration, and report back on status.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-187">The following steps place the IisInstall.ps1 script on the specified VM, execute the configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="9dd6c-188">Classic model</span><span class="sxs-lookup"><span data-stu-id="9dd6c-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish the configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set the VM to run the DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update the configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="9dd6c-189">Azure Resource Manager model</span><span class="sxs-lookup"><span data-stu-id="9dd6c-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish the configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set the VM to run the DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="9dd6c-190">Logging</span><span class="sxs-lookup"><span data-stu-id="9dd6c-190">Logging</span></span>
<span data-ttu-id="9dd6c-191">Logs are placed in:</span><span class="sxs-lookup"><span data-stu-id="9dd6c-191">Logs are placed in:</span></span>

<span data-ttu-id="9dd6c-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span><span class="sxs-lookup"><span data-stu-id="9dd6c-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dd6c-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="9dd6c-193">Next steps</span></span>
<span data-ttu-id="9dd6c-194">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="9dd6c-194">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="9dd6c-195">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9dd6c-195">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="9dd6c-196">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span><span class="sxs-lookup"><span data-stu-id="9dd6c-196">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="9dd6c-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with the DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9dd6c-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with the DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

