---
title: Azure PowerShell Script Sample - WordPress | Microsoft Docs
description: Azure PowerShell Script Sample - WordPress
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: ee1da7d7eb275e55ec7c7f46425670468e5fa3c8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555932"
---
# <a name="create-a-wordpress-vm-with-powershell"></a><span data-ttu-id="ff617-103">Create a WordPress VM with PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff617-103">Create a WordPress VM with PowerShell</span></span>

<span data-ttu-id="ff617-104">This script creates a virtual machine and uses the Azure Virtual Machine custom script extension to install WordPress.</span><span class="sxs-lookup"><span data-stu-id="ff617-104">This script creates a virtual machine and uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="ff617-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="ff617-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ff617-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="ff617-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Create VM WordPress")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ff617-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="ff617-107">Clean up deployment</span></span> 

<span data-ttu-id="ff617-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ff617-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ff617-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="ff617-109">Script explanation</span></span>

<span data-ttu-id="ff617-110">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="ff617-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="ff617-111">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="ff617-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ff617-112">Command</span><span class="sxs-lookup"><span data-stu-id="ff617-112">Command</span></span> | <span data-ttu-id="ff617-113">Notes</span><span class="sxs-lookup"><span data-stu-id="ff617-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ff617-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ff617-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/new-azurermresourcegroup) | <span data-ttu-id="ff617-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="ff617-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ff617-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ff617-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ff617-117">Creates a subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="ff617-117">Creates a subnet configuration.</span></span> <span data-ttu-id="ff617-118">This configuration is used with the virtual network creation process.</span><span class="sxs-lookup"><span data-stu-id="ff617-118">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="ff617-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ff617-119">New-AzureRmVirtualNetwork</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v1.0.13/new-azurermvirtualnetwork) | <span data-ttu-id="ff617-120">Creates a virtual network.</span><span class="sxs-lookup"><span data-stu-id="ff617-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="ff617-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ff617-121">New-AzureRmPublicIpAddress</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermpublicipaddress) | <span data-ttu-id="ff617-122">Creates a public IP address.</span><span class="sxs-lookup"><span data-stu-id="ff617-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="ff617-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ff617-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="ff617-124">Creates a network security group rule configuration.</span><span class="sxs-lookup"><span data-stu-id="ff617-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="ff617-125">This configuration is used to create an NSG rule when the NSG is created.</span><span class="sxs-lookup"><span data-stu-id="ff617-125">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="ff617-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ff617-126">New-AzureRmNetworkSecurityGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.1.0/new-azurermnetworksecuritygroup) | <span data-ttu-id="ff617-127">Creates a network security group.</span><span class="sxs-lookup"><span data-stu-id="ff617-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="ff617-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ff617-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v1.0.13/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ff617-129">Gets subnet information.</span><span class="sxs-lookup"><span data-stu-id="ff617-129">Gets subnet information.</span></span> <span data-ttu-id="ff617-130">This information is used when creating a network interface.</span><span class="sxs-lookup"><span data-stu-id="ff617-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="ff617-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ff617-131">New-AzureRmNetworkInterface</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.4.0/new-azurermnetworkinterface) | <span data-ttu-id="ff617-132">Creates a network interface.</span><span class="sxs-lookup"><span data-stu-id="ff617-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="ff617-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="ff617-133">New-AzureRmVMConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v1.3.4/new-azurermvmconfig) | <span data-ttu-id="ff617-134">Creates a VM configuration.</span><span class="sxs-lookup"><span data-stu-id="ff617-134">Creates a VM configuration.</span></span> <span data-ttu-id="ff617-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="ff617-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="ff617-136">The configuration is used during VM creation.</span><span class="sxs-lookup"><span data-stu-id="ff617-136">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="ff617-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ff617-137">New-AzureRmVM</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v1.3.4/new-azurermvm) | <span data-ttu-id="ff617-138">Create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ff617-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="ff617-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="ff617-139">Set-AzureRmVMExtension</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.2.0/set-azurermvmextension) | <span data-ttu-id="ff617-140">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span><span class="sxs-lookup"><span data-stu-id="ff617-140">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
|[<span data-ttu-id="ff617-141">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ff617-141">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="ff617-142">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="ff617-142">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ff617-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff617-143">Next steps</span></span>

<span data-ttu-id="ff617-144">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="ff617-144">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="ff617-145">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff617-145">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>