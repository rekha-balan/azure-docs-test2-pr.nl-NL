---
title: Custom Script extension on a Windows VM | Microsoft Docs
description: Automate Azure VM configuration tasks by using the Custom Script extension to run PowerShell scripts on a remote Windows VM
services: virtual-machines-windows
documentationcenter: ''
author: neilpeterson
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: c2b7ea84b6fb4333e8c8aaab4c3fe3ba0d4d8a8f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549906"
---
# <a name="custom-script-extension-for-windows-using-the-classic-deployment-model"></a><span data-ttu-id="677f0-103">Custom Script Extension for Windows using the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="677f0-103">Custom Script Extension for Windows using the classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="677f0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="677f0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="677f0-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="677f0-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="677f0-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="677f0-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="677f0-107">Learn how to [perform these steps using the Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="677f0-107">Learn how to [perform these steps using the Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="677f0-108">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="677f0-108">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="677f0-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span><span class="sxs-lookup"><span data-stu-id="677f0-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="677f0-110">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span><span class="sxs-lookup"><span data-stu-id="677f0-110">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span> <span data-ttu-id="677f0-111">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span><span class="sxs-lookup"><span data-stu-id="677f0-111">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="677f0-112">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span><span class="sxs-lookup"><span data-stu-id="677f0-112">This document details how to use the Custom Script Extension using the Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="677f0-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="677f0-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="677f0-114">Operating System</span><span class="sxs-lookup"><span data-stu-id="677f0-114">Operating System</span></span>

<span data-ttu-id="677f0-115">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span><span class="sxs-lookup"><span data-stu-id="677f0-115">The Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="677f0-116">Script Location</span><span class="sxs-lookup"><span data-stu-id="677f0-116">Script Location</span></span>

<span data-ttu-id="677f0-117">The script needs to be stored in Azure storage, or any other location accessible through a valid URL.</span><span class="sxs-lookup"><span data-stu-id="677f0-117">The script needs to be stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="677f0-118">Internet Connectivity</span><span class="sxs-lookup"><span data-stu-id="677f0-118">Internet Connectivity</span></span>

<span data-ttu-id="677f0-119">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span><span class="sxs-lookup"><span data-stu-id="677f0-119">The Custom Script Extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="677f0-120">Extension schema</span><span class="sxs-lookup"><span data-stu-id="677f0-120">Extension schema</span></span>

<span data-ttu-id="677f0-121">The following JSON shows the schema for the Custom Script Extension.</span><span class="sxs-lookup"><span data-stu-id="677f0-121">The following JSON shows the schema for the Custom Script Extension.</span></span> <span data-ttu-id="677f0-122">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span><span class="sxs-lookup"><span data-stu-id="677f0-122">The extension requires a script location (Azure Storage or other location with valid URL), and a command to execute.</span></span> <span data-ttu-id="677f0-123">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span><span class="sxs-lookup"><span data-stu-id="677f0-123">If using Azure Storage as the script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="677f0-124">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span><span class="sxs-lookup"><span data-stu-id="677f0-124">These items should be treated as sensitive data and specified in the extensions protected setting configuration.</span></span> <span data-ttu-id="677f0-125">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="677f0-125">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span>

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="677f0-126">Property values</span><span class="sxs-lookup"><span data-stu-id="677f0-126">Property values</span></span>

| <span data-ttu-id="677f0-127">Name</span><span class="sxs-lookup"><span data-stu-id="677f0-127">Name</span></span> | <span data-ttu-id="677f0-128">Value / Example</span><span class="sxs-lookup"><span data-stu-id="677f0-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="677f0-129">apiVersion</span><span class="sxs-lookup"><span data-stu-id="677f0-129">apiVersion</span></span> | <span data-ttu-id="677f0-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="677f0-130">2015-06-15</span></span> |
| <span data-ttu-id="677f0-131">publisher</span><span class="sxs-lookup"><span data-stu-id="677f0-131">publisher</span></span> | <span data-ttu-id="677f0-132">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="677f0-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="677f0-133">extension</span><span class="sxs-lookup"><span data-stu-id="677f0-133">extension</span></span> | <span data-ttu-id="677f0-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="677f0-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="677f0-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="677f0-135">typeHandlerVersion</span></span> | <span data-ttu-id="677f0-136">1.8</span><span class="sxs-lookup"><span data-stu-id="677f0-136">1.8</span></span> |
| <span data-ttu-id="677f0-137">fileUris (e.g)</span><span class="sxs-lookup"><span data-stu-id="677f0-137">fileUris (e.g)</span></span> | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| <span data-ttu-id="677f0-138">commandToExecute (e.g)</span><span class="sxs-lookup"><span data-stu-id="677f0-138">commandToExecute (e.g)</span></span> | <span data-ttu-id="677f0-139">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="677f0-139">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="677f0-140">Template deployment</span><span class="sxs-lookup"><span data-stu-id="677f0-140">Template deployment</span></span>

<span data-ttu-id="677f0-141">Azure VM extensions can be deployed with Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="677f0-141">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="677f0-142">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span><span class="sxs-lookup"><span data-stu-id="677f0-142">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="677f0-143">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="677f0-143">A sample template that includes the Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="677f0-144">PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="677f0-144">PowerShell deployment</span></span>

<span data-ttu-id="677f0-145">The `Set-AzureVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="677f0-145">The `Set-AzureVMCustomScriptExtension` command can be used to add the Custom Script extension to an existing virtual machine.</span></span> <span data-ttu-id="677f0-146">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="677f0-146">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="677f0-147">Troubleshoot and support</span><span class="sxs-lookup"><span data-stu-id="677f0-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="677f0-148">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="677f0-148">Troubleshoot</span></span>

<span data-ttu-id="677f0-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="677f0-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="677f0-150">To see the deployment state of extensions for a given VM, run the following command.</span><span class="sxs-lookup"><span data-stu-id="677f0-150">To see the deployment state of extensions for a given VM, run the following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="677f0-151">Extension execution output us logged to files found in the following directory on the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="677f0-151">Extension execution output us logged to files found in the following directory on the target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="677f0-152">The script itself is downloaded into the following directory on the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="677f0-152">The script itself is downloaded into the following directory on the target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="677f0-153">Support</span><span class="sxs-lookup"><span data-stu-id="677f0-153">Support</span></span>

<span data-ttu-id="677f0-154">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="677f0-154">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="677f0-155">Alternatively, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="677f0-155">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="677f0-156">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span><span class="sxs-lookup"><span data-stu-id="677f0-156">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="677f0-157">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="677f0-157">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>