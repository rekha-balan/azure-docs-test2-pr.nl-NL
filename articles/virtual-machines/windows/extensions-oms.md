---
title: OMS Azure virtual machine extension for Windows | Microsoft Docs
description: Deploy the OMS agent on Windows virtual machine using a virtual machine extension.
services: virtual-machines-windows
documentationcenter: ''
author: neilpeterson
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: d06463bb6502b7a47b7fd244abd998522ce8da92
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554164"
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="f5cd4-103">OMS virtual machine extension for Windows</span><span class="sxs-lookup"><span data-stu-id="f5cd4-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="f5cd4-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="f5cd4-105">The OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-105">The OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="f5cd4-106">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-106">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="f5cd4-107">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Windows.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-107">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5cd4-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f5cd4-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="f5cd4-109">Operating system</span><span class="sxs-lookup"><span data-stu-id="f5cd4-109">Operating system</span></span>
<span data-ttu-id="f5cd4-110">The OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-110">The OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="f5cd4-111">Internet connectivity</span><span class="sxs-lookup"><span data-stu-id="f5cd4-111">Internet connectivity</span></span>
<span data-ttu-id="f5cd4-112">The OMS Agent extension for Windows requires that the target virtual machine is connected to the internet.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-112">The OMS Agent extension for Windows requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="f5cd4-113">Extension schema</span><span class="sxs-lookup"><span data-stu-id="f5cd4-113">Extension schema</span></span>

<span data-ttu-id="f5cd4-114">The following JSON shows the schema for the OMS Agent extension.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-114">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="f5cd4-115">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-115">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span></span> <span data-ttu-id="f5cd4-116">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-116">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="f5cd4-117">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-117">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="f5cd4-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a><span data-ttu-id="f5cd4-119">Property values</span><span class="sxs-lookup"><span data-stu-id="f5cd4-119">Property values</span></span>

| <span data-ttu-id="f5cd4-120">Name</span><span class="sxs-lookup"><span data-stu-id="f5cd4-120">Name</span></span> | <span data-ttu-id="f5cd4-121">Value / Example</span><span class="sxs-lookup"><span data-stu-id="f5cd4-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="f5cd4-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f5cd4-122">apiVersion</span></span> | <span data-ttu-id="f5cd4-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="f5cd4-123">2015-06-15</span></span> |
| <span data-ttu-id="f5cd4-124">publisher</span><span class="sxs-lookup"><span data-stu-id="f5cd4-124">publisher</span></span> | <span data-ttu-id="f5cd4-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="f5cd4-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="f5cd4-126">type</span><span class="sxs-lookup"><span data-stu-id="f5cd4-126">type</span></span> | <span data-ttu-id="f5cd4-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="f5cd4-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="f5cd4-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="f5cd4-128">typeHandlerVersion</span></span> | <span data-ttu-id="f5cd4-129">1.0</span><span class="sxs-lookup"><span data-stu-id="f5cd4-129">1.0</span></span> |
| <span data-ttu-id="f5cd4-130">workspaceId (e.g)</span><span class="sxs-lookup"><span data-stu-id="f5cd4-130">workspaceId (e.g)</span></span> | <span data-ttu-id="f5cd4-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="f5cd4-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="f5cd4-132">workspaceKey (e.g)</span><span class="sxs-lookup"><span data-stu-id="f5cd4-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="f5cd4-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="f5cd4-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="f5cd4-134">Template deployment</span><span class="sxs-lookup"><span data-stu-id="f5cd4-134">Template deployment</span></span>

<span data-ttu-id="f5cd4-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="f5cd4-136">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the OMS Agent extension during an Azure Resource Manager template deployment.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-136">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="f5cd4-137">A sample template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="f5cd4-137">A sample template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="f5cd4-138">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-138">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="f5cd4-139">The placement of the JSON affects the value of the resource name and type.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-139">The placement of the JSON affects the value of the resource name and type.</span></span> <span data-ttu-id="f5cd4-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="f5cd4-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="f5cd4-141">The following example assumes the OMS extension is nested inside the virtual machine resource.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-141">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="f5cd4-142">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-142">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

<span data-ttu-id="f5cd4-143">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-143">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span> 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a><span data-ttu-id="f5cd4-144">PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="f5cd4-144">PowerShell deployment</span></span>

<span data-ttu-id="f5cd4-145">The `Set-AzureRmVMExtension` command can be used to deploy the OMS Agent virtual machine extension to an existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-145">The `Set-AzureRmVMExtension` command can be used to deploy the OMS Agent virtual machine extension to an existing virtual machine.</span></span> <span data-ttu-id="f5cd4-146">Before running the command, the public and private configurations need to be stored in a PowerShell hash table.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-146">Before running the command, the public and private configurations need to be stored in a PowerShell hash table.</span></span> 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="f5cd4-147">Troubleshoot and support</span><span class="sxs-lookup"><span data-stu-id="f5cd4-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="f5cd4-148">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="f5cd4-148">Troubleshoot</span></span>

<span data-ttu-id="f5cd4-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-149">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="f5cd4-150">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-150">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="f5cd4-151">Extension execution output is logged to files found in the following directory:</span><span class="sxs-lookup"><span data-stu-id="f5cd4-151">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="f5cd4-152">Support</span><span class="sxs-lookup"><span data-stu-id="f5cd4-152">Support</span></span>

<span data-ttu-id="f5cd4-153">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="f5cd4-153">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="f5cd4-154">Alternatively, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="f5cd4-155">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span><span class="sxs-lookup"><span data-stu-id="f5cd4-155">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="f5cd4-156">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="f5cd4-156">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
