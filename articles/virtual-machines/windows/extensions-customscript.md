---
title: Azure Custom Script Extension for Windows | Microsoft Docs
description: Automate Windows VM configuration tasks by using the Custom Script extension
services: virtual-machines-windows
documentationcenter: ''
author: neilpeterson
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: 81a08a3cbd14c4a61efe68d9dd9fcd032dd1e1cd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556338"
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="7c396-103">Custom Script Extension for Windows</span><span class="sxs-lookup"><span data-stu-id="7c396-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="7c396-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="7c396-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="7c396-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span><span class="sxs-lookup"><span data-stu-id="7c396-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="7c396-106">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span><span class="sxs-lookup"><span data-stu-id="7c396-106">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="7c396-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span><span class="sxs-lookup"><span data-stu-id="7c396-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="7c396-108">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span><span class="sxs-lookup"><span data-stu-id="7c396-108">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c396-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7c396-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="7c396-110">Operating System</span><span class="sxs-lookup"><span data-stu-id="7c396-110">Operating System</span></span>

<span data-ttu-id="7c396-111">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span><span class="sxs-lookup"><span data-stu-id="7c396-111">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="7c396-112">Script Location</span><span class="sxs-lookup"><span data-stu-id="7c396-112">Script Location</span></span>

<span data-ttu-id="7c396-113">The script needs to be stored in Azure storage, or any other location accessible through a valid URL.</span><span class="sxs-lookup"><span data-stu-id="7c396-113">The script needs to be stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="7c396-114">Internet Connectivity</span><span class="sxs-lookup"><span data-stu-id="7c396-114">Internet Connectivity</span></span>

<span data-ttu-id="7c396-115">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span><span class="sxs-lookup"><span data-stu-id="7c396-115">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="7c396-116">Extension schema</span><span class="sxs-lookup"><span data-stu-id="7c396-116">Extension schema</span></span>

<span data-ttu-id="7c396-117">The following JSON shows the schema for the Custom Script Extension.</span><span class="sxs-lookup"><span data-stu-id="7c396-117">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="7c396-118">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span><span class="sxs-lookup"><span data-stu-id="7c396-118">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="7c396-119">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span><span class="sxs-lookup"><span data-stu-id="7c396-119">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="7c396-120">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span><span class="sxs-lookup"><span data-stu-id="7c396-120">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="7c396-121">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7c396-121">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

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
        "typeHandlerVersion": "1.8",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="7c396-122">Property values</span><span class="sxs-lookup"><span data-stu-id="7c396-122">Property values</span></span>

| <span data-ttu-id="7c396-123">Name</span><span class="sxs-lookup"><span data-stu-id="7c396-123">Name</span></span> | <span data-ttu-id="7c396-124">Value / Example</span><span class="sxs-lookup"><span data-stu-id="7c396-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="7c396-125">apiVersion</span><span class="sxs-lookup"><span data-stu-id="7c396-125">apiVersion</span></span> | <span data-ttu-id="7c396-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="7c396-126">2015-06-15</span></span> |
| <span data-ttu-id="7c396-127">publisher</span><span class="sxs-lookup"><span data-stu-id="7c396-127">publisher</span></span> | <span data-ttu-id="7c396-128">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="7c396-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="7c396-129">type</span><span class="sxs-lookup"><span data-stu-id="7c396-129">type</span></span> | <span data-ttu-id="7c396-130">extensions</span><span class="sxs-lookup"><span data-stu-id="7c396-130">extensions</span></span> |
| <span data-ttu-id="7c396-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="7c396-131">typeHandlerVersion</span></span> | <span data-ttu-id="7c396-132">1.8</span><span class="sxs-lookup"><span data-stu-id="7c396-132">1.8</span></span> |
| <span data-ttu-id="7c396-133">fileUris (e.g)</span><span class="sxs-lookup"><span data-stu-id="7c396-133">fileUris (e.g)</span></span> | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| <span data-ttu-id="7c396-134">commandToExecute (e.g)</span><span class="sxs-lookup"><span data-stu-id="7c396-134">commandToExecute (e.g)</span></span> | <span data-ttu-id="7c396-135">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="7c396-135">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="7c396-136">storageAccountName (e.g)</span><span class="sxs-lookup"><span data-stu-id="7c396-136">storageAccountName (e.g)</span></span> | <span data-ttu-id="7c396-137">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="7c396-137">examplestorageacct</span></span> |
| <span data-ttu-id="7c396-138">storageAccountKey (e.g)</span><span class="sxs-lookup"><span data-stu-id="7c396-138">storageAccountKey (e.g)</span></span> | <span data-ttu-id="7c396-139">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span><span class="sxs-lookup"><span data-stu-id="7c396-139">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="7c396-140">Template deployment</span><span class="sxs-lookup"><span data-stu-id="7c396-140">Template deployment</span></span>

<span data-ttu-id="7c396-141">Azure VM extensions can be deployed with Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="7c396-141">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="7c396-142">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span><span class="sxs-lookup"><span data-stu-id="7c396-142">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="7c396-143">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="7c396-143">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="7c396-144">PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="7c396-144">PowerShell deployment</span></span>

<span data-ttu-id="7c396-145">The `Set-AzureRmVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7c396-145">The `Set-AzureRmVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="7c396-146">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="7c396-146">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="7c396-147">Troubleshoot and support</span><span class="sxs-lookup"><span data-stu-id="7c396-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="7c396-148">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="7c396-148">Troubleshoot</span></span>

<span data-ttu-id="7c396-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="7c396-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="7c396-150">To see the deployment state of extensions for a given VM, run the following command.</span><span class="sxs-lookup"><span data-stu-id="7c396-150">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="7c396-151">Extension execution output is logged to files found under the following directory on the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7c396-151">Extension execution output is logged to files found under the following directory on the target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="7c396-152">The specified files are downloaded into the following directory on the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="7c396-152">The specified files are downloaded into the following directory on the target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="7c396-153">where `<n>` is a decimal integer which may change between executions of the extension.</span><span class="sxs-lookup"><span data-stu-id="7c396-153">where `<n>` is a decimal integer which may change between executions of the extension.</span></span>  <span data-ttu-id="7c396-154">The `1.*` value matches the actual, current `typeHandlerVersion` value of the extension.</span><span class="sxs-lookup"><span data-stu-id="7c396-154">The `1.*` value matches the actual, current `typeHandlerVersion` value of the extension.</span></span>  <span data-ttu-id="7c396-155">For example, the actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="7c396-155">For example, the actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="7c396-156">When executing the `commandToExecute` command, the extension will have set this directory (e.g., `...\Downloads\2`) as the current working directory.</span><span class="sxs-lookup"><span data-stu-id="7c396-156">When executing the `commandToExecute` command, the extension will have set this directory (e.g., `...\Downloads\2`) as the current working directory.</span></span> <span data-ttu-id="7c396-157">This enables the use of relative paths to locate the files downloaded via the `fileURIs` property.</span><span class="sxs-lookup"><span data-stu-id="7c396-157">This enables the use of relative paths to locate the files downloaded via the `fileURIs` property.</span></span> <span data-ttu-id="7c396-158">See the table below for examples.</span><span class="sxs-lookup"><span data-stu-id="7c396-158">See the table below for examples.</span></span>

<span data-ttu-id="7c396-159">Since the absolute download path may vary over time, it is better to opt for relative script/file paths in the `commandToExecute` string, whenever possible.</span><span class="sxs-lookup"><span data-stu-id="7c396-159">Since the absolute download path may vary over time, it is better to opt for relative script/file paths in the `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="7c396-160">For example:</span><span class="sxs-lookup"><span data-stu-id="7c396-160">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="7c396-161">Path information after the first URI segment is retained for files downloaded via the `fileUris` property list.</span><span class="sxs-lookup"><span data-stu-id="7c396-161">Path information after the first URI segment is retained for files downloaded via the `fileUris` property list.</span></span>  <span data-ttu-id="7c396-162">As shown in the table below, downloaded files are mapped into download subdirectories to reflect the structure of the `fileUris` values.</span><span class="sxs-lookup"><span data-stu-id="7c396-162">As shown in the table below, downloaded files are mapped into download subdirectories to reflect the structure of the `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="7c396-163">Examples of Downloaded Files</span><span class="sxs-lookup"><span data-stu-id="7c396-163">Examples of Downloaded Files</span></span>

| <span data-ttu-id="7c396-164">URI in fileUris</span><span class="sxs-lookup"><span data-stu-id="7c396-164">URI in fileUris</span></span> | <span data-ttu-id="7c396-165">Relative downloaded location</span><span class="sxs-lookup"><span data-stu-id="7c396-165">Relative downloaded location</span></span> | <span data-ttu-id="7c396-166">Absolute downloaded location \*</span><span class="sxs-lookup"><span data-stu-id="7c396-166">Absolute downloaded location \*</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="7c396-167">\* As above, the absolute directory paths will change over the lifetime of the VM, but not within a single execution of the CustomScript extension.</span><span class="sxs-lookup"><span data-stu-id="7c396-167">\* As above, the absolute directory paths will change over the lifetime of the VM, but not within a single execution of the CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="7c396-168">Support</span><span class="sxs-lookup"><span data-stu-id="7c396-168">Support</span></span>

<span data-ttu-id="7c396-169">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="7c396-169">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="7c396-170">Alternatively, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="7c396-170">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="7c396-171">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span><span class="sxs-lookup"><span data-stu-id="7c396-171">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="7c396-172">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="7c396-172">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
