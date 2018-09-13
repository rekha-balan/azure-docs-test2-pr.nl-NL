---
title: Azure PowerShell Script Sample - OMS | Microsoft Docs
description: Azure PowerShell Script Sample - OMS
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
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: e02754627c4247e41e7a88c07ac58d2f93c3d927
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551850"
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="dfb22-103">Create an Operations Management Suite monitored VM with PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfb22-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="dfb22-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="dfb22-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="dfb22-105">Once the script has run, the virtual machine will be visible in the OMS console.</span><span class="sxs-lookup"><span data-stu-id="dfb22-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span> <span data-ttu-id="dfb22-106">Also, you need to update the OMS workspace ID and workspace key.</span><span class="sxs-lookup"><span data-stu-id="dfb22-106">Also, you need to update the OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dfb22-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="dfb22-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dfb22-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="dfb22-108">Clean up deployment</span></span> 

<span data-ttu-id="dfb22-109">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="dfb22-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="dfb22-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="dfb22-110">Script explanation</span></span>

<span data-ttu-id="dfb22-111">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="dfb22-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="dfb22-112">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="dfb22-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dfb22-113">Command</span><span class="sxs-lookup"><span data-stu-id="dfb22-113">Command</span></span> | <span data-ttu-id="dfb22-114">Notes</span><span class="sxs-lookup"><span data-stu-id="dfb22-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dfb22-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dfb22-115">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/new-azurermresourcegroup) | <span data-ttu-id="dfb22-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="dfb22-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dfb22-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="dfb22-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="dfb22-118">Creates a subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="dfb22-118">Creates a subnet configuration.</span></span> <span data-ttu-id="dfb22-119">This configuration is used with the virtual network creation process.</span><span class="sxs-lookup"><span data-stu-id="dfb22-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="dfb22-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="dfb22-120">New-AzureRmVirtualNetwork</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v1.0.13/new-azurermvirtualnetwork) | <span data-ttu-id="dfb22-121">Creates a virtual network.</span><span class="sxs-lookup"><span data-stu-id="dfb22-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="dfb22-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="dfb22-122">New-AzureRmPublicIpAddress</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermpublicipaddress) | <span data-ttu-id="dfb22-123">Creates a public IP address.</span><span class="sxs-lookup"><span data-stu-id="dfb22-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="dfb22-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="dfb22-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="dfb22-125">Creates a network security group rule configuration.</span><span class="sxs-lookup"><span data-stu-id="dfb22-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="dfb22-126">This configuration is used to create an NSG rule when the NSG is created.</span><span class="sxs-lookup"><span data-stu-id="dfb22-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="dfb22-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="dfb22-127">New-AzureRmNetworkSecurityGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.1.0/new-azurermnetworksecuritygroup) | <span data-ttu-id="dfb22-128">Creates a network security group.</span><span class="sxs-lookup"><span data-stu-id="dfb22-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="dfb22-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="dfb22-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v1.0.13/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="dfb22-130">Gets subnet information.</span><span class="sxs-lookup"><span data-stu-id="dfb22-130">Gets subnet information.</span></span> <span data-ttu-id="dfb22-131">This information is used when creating a network interface.</span><span class="sxs-lookup"><span data-stu-id="dfb22-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="dfb22-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="dfb22-132">New-AzureRmNetworkInterface</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.4.0/new-azurermnetworkinterface) | <span data-ttu-id="dfb22-133">Creates a network interface.</span><span class="sxs-lookup"><span data-stu-id="dfb22-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="dfb22-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="dfb22-134">New-AzureRmVMConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v1.3.4/new-azurermvmconfig) | <span data-ttu-id="dfb22-135">Creates a VM configuration.</span><span class="sxs-lookup"><span data-stu-id="dfb22-135">Creates a VM configuration.</span></span> <span data-ttu-id="dfb22-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="dfb22-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="dfb22-137">The configuration is used during VM creation.</span><span class="sxs-lookup"><span data-stu-id="dfb22-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="dfb22-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="dfb22-138">New-AzureRmVM</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v1.3.4/new-azurermvm) | <span data-ttu-id="dfb22-139">Create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dfb22-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="dfb22-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="dfb22-140">Set-AzureRmVMExtension</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.2.0/set-azurermvmextension) | <span data-ttu-id="dfb22-141">Add a VM extension to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dfb22-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="dfb22-142">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="dfb22-142">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="dfb22-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dfb22-143">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="dfb22-144">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="dfb22-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dfb22-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="dfb22-145">Next steps</span></span>

<span data-ttu-id="dfb22-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="dfb22-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="dfb22-147">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dfb22-147">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
