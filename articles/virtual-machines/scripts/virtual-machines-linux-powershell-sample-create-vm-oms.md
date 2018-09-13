---
title: Azure PowerShell Script Sample - OMS | Microsoft Docs
description: Azure PowerShell Script Sample - OMS
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: bde05b4e50d270a685b986ddf52e7707d545b2d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44779433"
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="237b5-103">Create an Operations Management Suite monitored VM with PowerShell</span><span class="sxs-lookup"><span data-stu-id="237b5-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="237b5-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="237b5-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="237b5-105">Once the script has run, the virtual machine will be visible in the OMS console.</span><span class="sxs-lookup"><span data-stu-id="237b5-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="237b5-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="237b5-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="237b5-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="237b5-107">Clean up deployment</span></span>

<span data-ttu-id="237b5-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="237b5-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="237b5-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="237b5-109">Script explanation</span></span>

<span data-ttu-id="237b5-110">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="237b5-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="237b5-111">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="237b5-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="237b5-112">Command</span><span class="sxs-lookup"><span data-stu-id="237b5-112">Command</span></span> | <span data-ttu-id="237b5-113">Notes</span><span class="sxs-lookup"><span data-stu-id="237b5-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="237b5-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="237b5-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="237b5-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="237b5-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="237b5-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="237b5-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="237b5-117">Creates a subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="237b5-117">Creates a subnet configuration.</span></span> <span data-ttu-id="237b5-118">This configuration is used with the virtual network creation process.</span><span class="sxs-lookup"><span data-stu-id="237b5-118">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="237b5-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="237b5-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="237b5-120">Creates a virtual network.</span><span class="sxs-lookup"><span data-stu-id="237b5-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="237b5-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="237b5-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="237b5-122">Creates a public IP address.</span><span class="sxs-lookup"><span data-stu-id="237b5-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="237b5-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="237b5-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="237b5-124">Creates a network security group rule configuration.</span><span class="sxs-lookup"><span data-stu-id="237b5-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="237b5-125">This configuration is used to create an NSG rule when the NSG is created.</span><span class="sxs-lookup"><span data-stu-id="237b5-125">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="237b5-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="237b5-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="237b5-127">Creates a network security group.</span><span class="sxs-lookup"><span data-stu-id="237b5-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="237b5-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="237b5-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="237b5-129">Gets subnet information.</span><span class="sxs-lookup"><span data-stu-id="237b5-129">Gets subnet information.</span></span> <span data-ttu-id="237b5-130">This information is used when creating a network interface.</span><span class="sxs-lookup"><span data-stu-id="237b5-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="237b5-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="237b5-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="237b5-132">Creates a network interface.</span><span class="sxs-lookup"><span data-stu-id="237b5-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="237b5-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="237b5-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="237b5-134">Creates a VM configuration.</span><span class="sxs-lookup"><span data-stu-id="237b5-134">Creates a VM configuration.</span></span> <span data-ttu-id="237b5-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="237b5-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="237b5-136">The configuration is used during VM creation.</span><span class="sxs-lookup"><span data-stu-id="237b5-136">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="237b5-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="237b5-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="237b5-138">Create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="237b5-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="237b5-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="237b5-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="237b5-140">Add a VM extension to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="237b5-140">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="237b5-141">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="237b5-141">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="237b5-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="237b5-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="237b5-143">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="237b5-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="237b5-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="237b5-144">Next steps</span></span>

<span data-ttu-id="237b5-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="237b5-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="237b5-146">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="237b5-146">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
