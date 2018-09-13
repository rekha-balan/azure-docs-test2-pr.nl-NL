---
title: Azure PowerShell Script Sample - IIS with DSC | Microsoft Docs
description: Azure PowerShell Script Sample - IIS with DSC
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: a844e10599c6dc04f9d871b9a0fd065fb3c18f5d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551038"
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="6a14f-103">Create an IIS VM with PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a14f-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="6a14f-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses the Azure Virtual Machine DSC Extension to install IIS.</span><span class="sxs-lookup"><span data-stu-id="6a14f-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses the Azure Virtual Machine DSC Extension to install IIS.</span></span> <span data-ttu-id="6a14f-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6a14f-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6a14f-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="6a14f-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6a14f-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="6a14f-107">Clean up deployment</span></span> 

<span data-ttu-id="6a14f-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="6a14f-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6a14f-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="6a14f-109">Script explanation</span></span>

<span data-ttu-id="6a14f-110">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="6a14f-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="6a14f-111">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="6a14f-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6a14f-112">Command</span><span class="sxs-lookup"><span data-stu-id="6a14f-112">Command</span></span> | <span data-ttu-id="6a14f-113">Notes</span><span class="sxs-lookup"><span data-stu-id="6a14f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6a14f-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6a14f-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/new-azurermresourcegroup) | <span data-ttu-id="6a14f-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="6a14f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6a14f-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="6a14f-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="6a14f-117">Creates a subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="6a14f-117">Creates a subnet configuration.</span></span> <span data-ttu-id="6a14f-118">This configuration is used with the virtual network creation process.</span><span class="sxs-lookup"><span data-stu-id="6a14f-118">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="6a14f-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="6a14f-119">New-AzureRmVirtualNetwork</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v1.0.13/new-azurermvirtualnetwork) | <span data-ttu-id="6a14f-120">Creates a virtual network.</span><span class="sxs-lookup"><span data-stu-id="6a14f-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="6a14f-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="6a14f-121">New-AzureRmPublicIpAddress</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermpublicipaddress) | <span data-ttu-id="6a14f-122">Creates a public IP address.</span><span class="sxs-lookup"><span data-stu-id="6a14f-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="6a14f-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="6a14f-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="6a14f-124">Creates a network security group rule configuration.</span><span class="sxs-lookup"><span data-stu-id="6a14f-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="6a14f-125">This configuration is used to create an NSG rule when the NSG is created.</span><span class="sxs-lookup"><span data-stu-id="6a14f-125">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="6a14f-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="6a14f-126">New-AzureRmNetworkSecurityGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.1.0/new-azurermnetworksecuritygroup) | <span data-ttu-id="6a14f-127">Creates a network security group.</span><span class="sxs-lookup"><span data-stu-id="6a14f-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="6a14f-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="6a14f-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v1.0.13/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="6a14f-129">Gets subnet information.</span><span class="sxs-lookup"><span data-stu-id="6a14f-129">Gets subnet information.</span></span> <span data-ttu-id="6a14f-130">This information is used when creating a network interface.</span><span class="sxs-lookup"><span data-stu-id="6a14f-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="6a14f-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="6a14f-131">New-AzureRmNetworkInterface</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.4.0/new-azurermnetworkinterface) | <span data-ttu-id="6a14f-132">Creates a network interface.</span><span class="sxs-lookup"><span data-stu-id="6a14f-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="6a14f-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="6a14f-133">New-AzureRmVMConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v1.3.4/new-azurermvmconfig) | <span data-ttu-id="6a14f-134">Creates a VM configuration.</span><span class="sxs-lookup"><span data-stu-id="6a14f-134">Creates a VM configuration.</span></span> <span data-ttu-id="6a14f-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="6a14f-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="6a14f-136">The configuration is used during VM creation.</span><span class="sxs-lookup"><span data-stu-id="6a14f-136">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="6a14f-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="6a14f-137">New-AzureRmVM</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v1.3.4/new-azurermvm) | <span data-ttu-id="6a14f-138">Create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6a14f-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="6a14f-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="6a14f-139">Set-AzureRmVMExtension</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.2.0/set-azurermvmextension) | <span data-ttu-id="6a14f-140">Add a VM extension to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6a14f-140">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="6a14f-141">In this sample, the custom script extension is used to install IIS.</span><span class="sxs-lookup"><span data-stu-id="6a14f-141">In this sample, the custom script extension is used to install IIS.</span></span> |
|[<span data-ttu-id="6a14f-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6a14f-142">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="6a14f-143">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="6a14f-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6a14f-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a14f-144">Next steps</span></span>

<span data-ttu-id="6a14f-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="6a14f-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="6a14f-146">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6a14f-146">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>