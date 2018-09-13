---
title: Virtual machine extensions and features for Windows in Azure | Microsoft Docs
description: Learn what extensions are available for Azure virtual machines, grouped by what they provide or improve.
services: virtual-machines-windows
documentationcenter: ''
author: neilpeterson
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b164036d5efc4e561cebfcdb32ef33a9611b1c66
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563945"
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="26525-103">Virtual machine extensions and features for Windows</span><span class="sxs-lookup"><span data-stu-id="26525-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="26525-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="26525-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="26525-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span><span class="sxs-lookup"><span data-stu-id="26525-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="26525-106">Azure VM extensions can be run by using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="26525-106">Azure VM extensions can be run by using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="26525-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span><span class="sxs-lookup"><span data-stu-id="26525-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="26525-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how to detect, manage, and remove virtual machine extensions.</span><span class="sxs-lookup"><span data-stu-id="26525-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how to detect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="26525-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span><span class="sxs-lookup"><span data-stu-id="26525-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="26525-110">Extension-specific details can be found in each document specific to the individual extension.</span><span class="sxs-lookup"><span data-stu-id="26525-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="26525-111">Use cases and samples</span><span class="sxs-lookup"><span data-stu-id="26525-111">Use cases and samples</span></span>

<span data-ttu-id="26525-112">There are many different Azure VM extensions available, each with a specific use case.</span><span class="sxs-lookup"><span data-stu-id="26525-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="26525-113">Some example use cases are:</span><span class="sxs-lookup"><span data-stu-id="26525-113">Some example use cases are:</span></span>

- <span data-ttu-id="26525-114">Apply PowerShell Desired State configurations to a virtual machine by using the DSC extension for Windows.</span><span class="sxs-lookup"><span data-stu-id="26525-114">Apply PowerShell Desired State configurations to a virtual machine by using the DSC extension for Windows.</span></span> <span data-ttu-id="26525-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26525-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="26525-116">Configure virtual machine monitoring by using the Microsoft Monitoring Agent VM extension.</span><span class="sxs-lookup"><span data-stu-id="26525-116">Configure virtual machine monitoring by using the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="26525-117">For more information, see [Connect Azure virtual machines to Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="26525-117">For more information, see [Connect Azure virtual machines to Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="26525-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span><span class="sxs-lookup"><span data-stu-id="26525-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="26525-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="26525-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="26525-120">Configure an Azure virtual machine by using Chef.</span><span class="sxs-lookup"><span data-stu-id="26525-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="26525-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span><span class="sxs-lookup"><span data-stu-id="26525-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="26525-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span><span class="sxs-lookup"><span data-stu-id="26525-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="26525-123">The Custom Script extension for Windows allows any PowerShell script to be run on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="26525-123">The Custom Script extension for Windows allows any PowerShell script to be run on a virtual machine.</span></span> <span data-ttu-id="26525-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span><span class="sxs-lookup"><span data-stu-id="26525-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="26525-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="26525-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>

<span data-ttu-id="26525-126">To work through an example where a VM extension is used in an end-to-end application deployment, see [Automating application deployments to Azure virtual machines](dotnet-core-1-landing.md).</span><span class="sxs-lookup"><span data-stu-id="26525-126">To work through an example where a VM extension is used in an end-to-end application deployment, see [Automating application deployments to Azure virtual machines](dotnet-core-1-landing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26525-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="26525-127">Prerequisites</span></span>

<span data-ttu-id="26525-128">Each virtual machine extension may have its own set of prerequisites.</span><span class="sxs-lookup"><span data-stu-id="26525-128">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="26525-129">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span><span class="sxs-lookup"><span data-stu-id="26525-129">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="26525-130">Requirements of individual extensions are detailed in the extension-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="26525-130">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="26525-131">Azure VM agent</span><span class="sxs-lookup"><span data-stu-id="26525-131">Azure VM agent</span></span>
<span data-ttu-id="26525-132">The Azure VM agent manages interaction between an Azure virtual machine and the Azure fabric controller.</span><span class="sxs-lookup"><span data-stu-id="26525-132">The Azure VM agent manages interaction between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="26525-133">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span><span class="sxs-lookup"><span data-stu-id="26525-133">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="26525-134">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span><span class="sxs-lookup"><span data-stu-id="26525-134">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="26525-135">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="26525-135">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="26525-136">Discover VM extensions</span><span class="sxs-lookup"><span data-stu-id="26525-136">Discover VM extensions</span></span>
<span data-ttu-id="26525-137">Many different VM extensions are available for use with Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="26525-137">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="26525-138">To see a complete list, run the following command with the Azure Resource Manager PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="26525-138">To see a complete list, run the following command with the Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="26525-139">Make sure to specify the desired location when you're running this command.</span><span class="sxs-lookup"><span data-stu-id="26525-139">Make sure to specify the desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="26525-140">Run VM extensions</span><span class="sxs-lookup"><span data-stu-id="26525-140">Run VM extensions</span></span>

<span data-ttu-id="26525-141">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span><span class="sxs-lookup"><span data-stu-id="26525-141">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="26525-142">VM extensions can also be bundled with Azure Resource Manager template deployments.</span><span class="sxs-lookup"><span data-stu-id="26525-142">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="26525-143">By using extensions with Resource Manager templates, you can enable Azure virtual machines to be deployed and configured without the need for post-deployment intervention.</span><span class="sxs-lookup"><span data-stu-id="26525-143">By using extensions with Resource Manager templates, you can enable Azure virtual machines to be deployed and configured without the need for post-deployment intervention.</span></span>

<span data-ttu-id="26525-144">The following methods can be used to run an extension against an existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="26525-144">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="26525-145">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26525-145">PowerShell</span></span>

<span data-ttu-id="26525-146">Several PowerShell commands exist for running individual extensions.</span><span class="sxs-lookup"><span data-stu-id="26525-146">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="26525-147">To see a list, run the following PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="26525-147">To see a list, run the following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="26525-148">This provides output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="26525-148">This provides output similar to the following:</span></span>

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

<span data-ttu-id="26525-149">The following example uses the Custom Script extension to download a script from a GitHub repository onto the target virtual machine and then run the script.</span><span class="sxs-lookup"><span data-stu-id="26525-149">The following example uses the Custom Script extension to download a script from a GitHub repository onto the target virtual machine and then run the script.</span></span> <span data-ttu-id="26525-150">For more information on the Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="26525-150">For more information on the Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="26525-151">In this example, the VM Access extension is used to reset the administrative password of a Windows virtual machine.</span><span class="sxs-lookup"><span data-stu-id="26525-151">In this example, the VM Access extension is used to reset the administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="26525-152">For more information on the VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="26525-152">For more information on the VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="26525-153">The `Set-AzureRmVMExtension` command can be used to start any VM extension.</span><span class="sxs-lookup"><span data-stu-id="26525-153">The `Set-AzureRmVMExtension` command can be used to start any VM extension.</span></span> <span data-ttu-id="26525-154">For more information, see the [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="26525-154">For more information, see the [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="26525-155">Azure portal</span><span class="sxs-lookup"><span data-stu-id="26525-155">Azure portal</span></span>

<span data-ttu-id="26525-156">A VM extension can be applied to an existing virtual machine through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="26525-156">A VM extension can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="26525-157">To do so, select the virtual machine you want to use, choose **Extensions**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="26525-157">To do so, select the virtual machine you want to use, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="26525-158">This provides a list of available extensions.</span><span class="sxs-lookup"><span data-stu-id="26525-158">This provides a list of available extensions.</span></span> <span data-ttu-id="26525-159">Select the one you want and follow the steps in the wizard.</span><span class="sxs-lookup"><span data-stu-id="26525-159">Select the one you want and follow the steps in the wizard.</span></span>

<span data-ttu-id="26525-160">The following image shows the installation of the Microsoft Antimalware extension from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="26525-160">The following image shows the installation of the Microsoft Antimalware extension from the Azure portal.</span></span>

![Install antimalware extension](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="26525-162">Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="26525-162">Azure Resource Manager templates</span></span>

<span data-ttu-id="26525-163">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span><span class="sxs-lookup"><span data-stu-id="26525-163">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="26525-164">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span><span class="sxs-lookup"><span data-stu-id="26525-164">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="26525-165">For example, the following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span><span class="sxs-lookup"><span data-stu-id="26525-165">For example, the following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="26525-166">The VM extension takes care of the software installation.</span><span class="sxs-lookup"><span data-stu-id="26525-166">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="26525-167">For more information, see the [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="26525-167">For more information, see the [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="26525-168">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](extensions-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="26525-168">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](extensions-authoring-templates.md).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="26525-169">Secure VM extension data</span><span class="sxs-lookup"><span data-stu-id="26525-169">Secure VM extension data</span></span>

<span data-ttu-id="26525-170">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span><span class="sxs-lookup"><span data-stu-id="26525-170">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="26525-171">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="26525-171">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="26525-172">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="26525-172">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="26525-173">The following example shows an instance of the Custom Script extension for Windows.</span><span class="sxs-lookup"><span data-stu-id="26525-173">The following example shows an instance of the Custom Script extension for Windows.</span></span> <span data-ttu-id="26525-174">Notice that the command to execute includes a set of credentials.</span><span class="sxs-lookup"><span data-stu-id="26525-174">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="26525-175">In this example, the command to execute will not be encrypted.</span><span class="sxs-lookup"><span data-stu-id="26525-175">In this example, the command to execute will not be encrypted.</span></span>


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="26525-176">Secure the execution string by moving the **command to execute** property to the **protected** configuration.</span><span class="sxs-lookup"><span data-stu-id="26525-176">Secure the execution string by moving the **command to execute** property to the **protected** configuration.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="26525-177">Troubleshoot VM extensions</span><span class="sxs-lookup"><span data-stu-id="26525-177">Troubleshoot VM extensions</span></span>

<span data-ttu-id="26525-178">Each VM extension may have specific troubleshooting steps.</span><span class="sxs-lookup"><span data-stu-id="26525-178">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="26525-179">For instance, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span><span class="sxs-lookup"><span data-stu-id="26525-179">For instance, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="26525-180">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="26525-180">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="26525-181">The following troubleshooting steps apply to all virtual machine extensions.</span><span class="sxs-lookup"><span data-stu-id="26525-181">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="26525-182">View extension status</span><span class="sxs-lookup"><span data-stu-id="26525-182">View extension status</span></span>

<span data-ttu-id="26525-183">After a virtual machine extension has been run against a virtual machine, use the following PowerShell command to return extension status.</span><span class="sxs-lookup"><span data-stu-id="26525-183">After a virtual machine extension has been run against a virtual machine, use the following PowerShell command to return extension status.</span></span> <span data-ttu-id="26525-184">Replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="26525-184">Replace example parameter names with your own values.</span></span> <span data-ttu-id="26525-185">The `Name` parameter takes the name given to the extension at execution time.</span><span class="sxs-lookup"><span data-stu-id="26525-185">The `Name` parameter takes the name given to the extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="26525-186">The output looks like the following:</span><span class="sxs-lookup"><span data-stu-id="26525-186">The output looks like the following:</span></span>

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

<span data-ttu-id="26525-187">Extension execution status can also be found in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="26525-187">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="26525-188">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span><span class="sxs-lookup"><span data-stu-id="26525-188">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="26525-189">Rerun VM extensions</span><span class="sxs-lookup"><span data-stu-id="26525-189">Rerun VM extensions</span></span>

<span data-ttu-id="26525-190">There may be cases in which a virtual machine extension needs to be rerun.</span><span class="sxs-lookup"><span data-stu-id="26525-190">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="26525-191">You can do this by removing the extension and then rerunning the extension with an execution method of your choice.</span><span class="sxs-lookup"><span data-stu-id="26525-191">You can do this by removing the extension and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="26525-192">To remove an extension, run the following command with the Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="26525-192">To remove an extension, run the following command with the Azure PowerShell module.</span></span> <span data-ttu-id="26525-193">Replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="26525-193">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="26525-194">An extension can also be removed using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="26525-194">An extension can also be removed using the Azure portal.</span></span> <span data-ttu-id="26525-195">To do so:</span><span class="sxs-lookup"><span data-stu-id="26525-195">To do so:</span></span>

1. <span data-ttu-id="26525-196">Select a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="26525-196">Select a virtual machine.</span></span>
2. <span data-ttu-id="26525-197">Select **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="26525-197">Select **Extensions**.</span></span>
3. <span data-ttu-id="26525-198">Choose the desired extension.</span><span class="sxs-lookup"><span data-stu-id="26525-198">Choose the desired extension.</span></span>
4. <span data-ttu-id="26525-199">Select **Uninstall**.</span><span class="sxs-lookup"><span data-stu-id="26525-199">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="26525-200">Common VM extensions reference</span><span class="sxs-lookup"><span data-stu-id="26525-200">Common VM extensions reference</span></span>
| <span data-ttu-id="26525-201">Extension name</span><span class="sxs-lookup"><span data-stu-id="26525-201">Extension name</span></span> | <span data-ttu-id="26525-202">Description</span><span class="sxs-lookup"><span data-stu-id="26525-202">Description</span></span> | <span data-ttu-id="26525-203">More information</span><span class="sxs-lookup"><span data-stu-id="26525-203">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26525-204">Custom Script Extension for Windows</span><span class="sxs-lookup"><span data-stu-id="26525-204">Custom Script Extension for Windows</span></span> |<span data-ttu-id="26525-205">Run scripts against an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="26525-205">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="26525-206">Custom Script Extension for Windows</span><span class="sxs-lookup"><span data-stu-id="26525-206">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="26525-207">DSC Extension for Windows</span><span class="sxs-lookup"><span data-stu-id="26525-207">DSC Extension for Windows</span></span> |<span data-ttu-id="26525-208">PowerShell DSC (Desired State Configuration) Extension</span><span class="sxs-lookup"><span data-stu-id="26525-208">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="26525-209">DSC Extension for Windows</span><span class="sxs-lookup"><span data-stu-id="26525-209">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="26525-210">Azure Diagnostics Extension</span><span class="sxs-lookup"><span data-stu-id="26525-210">Azure Diagnostics Extension</span></span> |<span data-ttu-id="26525-211">Manage Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="26525-211">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="26525-212">Azure Diagnostics Extension</span><span class="sxs-lookup"><span data-stu-id="26525-212">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="26525-213">Azure VM Access Extension</span><span class="sxs-lookup"><span data-stu-id="26525-213">Azure VM Access Extension</span></span> |<span data-ttu-id="26525-214">Manage users and credentials</span><span class="sxs-lookup"><span data-stu-id="26525-214">Manage users and credentials</span></span> |[<span data-ttu-id="26525-215">VM Access Extension for Linux</span><span class="sxs-lookup"><span data-stu-id="26525-215">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |

