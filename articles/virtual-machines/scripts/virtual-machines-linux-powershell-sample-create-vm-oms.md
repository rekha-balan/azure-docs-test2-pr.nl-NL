---
title: Azure PowerShell Script Sample - OMS | Microsoft Docs
description: Azure PowerShell Script Sample - OMS
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
ms.openlocfilehash: 25e0fe62aee03a47b8cda0c362662312551d7fd1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548768"
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="ac56b-103">Create an Operations Management Suite monitored VM with PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac56b-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="ac56b-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="ac56b-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="ac56b-105">Once the script has run, the virtual machine will be visible in the OMS console.</span><span class="sxs-lookup"><span data-stu-id="ac56b-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ac56b-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="ac56b-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ac56b-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="ac56b-107">Clean up deployment</span></span> 

<span data-ttu-id="ac56b-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ac56b-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ac56b-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="ac56b-109">Script explanation</span></span>

<span data-ttu-id="ac56b-110">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="ac56b-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="ac56b-111">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="ac56b-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ac56b-112">Command</span><span class="sxs-lookup"><span data-stu-id="ac56b-112">Command</span></span> | <span data-ttu-id="ac56b-113">Notes</span><span class="sxs-lookup"><span data-stu-id="ac56b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ac56b-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ac56b-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/new-azurermresourcegroup) | <span data-ttu-id="ac56b-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="ac56b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ac56b-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ac56b-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ac56b-117">Creates a subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="ac56b-117">Creates a subnet configuration.</span></span> <span data-ttu-id="ac56b-118">This configuration is used with the virtual network creation process.</span><span class="sxs-lookup"><span data-stu-id="ac56b-118">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="ac56b-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ac56b-119">New-AzureRmVirtualNetwork</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v1.0.13/new-azurermvirtualnetwork) | <span data-ttu-id="ac56b-120">Creates a virtual network.</span><span class="sxs-lookup"><span data-stu-id="ac56b-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="ac56b-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ac56b-121">New-AzureRmPublicIpAddress</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermpublicipaddress) | <span data-ttu-id="ac56b-122">Creates a public IP address.</span><span class="sxs-lookup"><span data-stu-id="ac56b-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="ac56b-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ac56b-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="ac56b-124">Creates a network security group rule configuration.</span><span class="sxs-lookup"><span data-stu-id="ac56b-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="ac56b-125">This configuration is used to create an NSG rule when the NSG is created.</span><span class="sxs-lookup"><span data-stu-id="ac56b-125">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="ac56b-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ac56b-126">New-AzureRmNetworkSecurityGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.1.0/new-azurermnetworksecuritygroup) | <span data-ttu-id="ac56b-127">Creates a network security group.</span><span class="sxs-lookup"><span data-stu-id="ac56b-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="ac56b-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ac56b-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v1.0.13/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ac56b-129">Gets subnet information.</span><span class="sxs-lookup"><span data-stu-id="ac56b-129">Gets subnet information.</span></span> <span data-ttu-id="ac56b-130">This information is used when creating a network interface.</span><span class="sxs-lookup"><span data-stu-id="ac56b-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="ac56b-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ac56b-131">New-AzureRmNetworkInterface</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.4.0/new-azurermnetworkinterface) | <span data-ttu-id="ac56b-132">Creates a network interface.</span><span class="sxs-lookup"><span data-stu-id="ac56b-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="ac56b-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="ac56b-133">New-AzureRmVMConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v1.3.4/new-azurermvmconfig) | <span data-ttu-id="ac56b-134">Creates a VM configuration.</span><span class="sxs-lookup"><span data-stu-id="ac56b-134">Creates a VM configuration.</span></span> <span data-ttu-id="ac56b-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="ac56b-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="ac56b-136">The configuration is used during VM creation.</span><span class="sxs-lookup"><span data-stu-id="ac56b-136">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="ac56b-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ac56b-137">New-AzureRmVM</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v1.3.4/new-azurermvm) | <span data-ttu-id="ac56b-138">Create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ac56b-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="ac56b-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="ac56b-139">Set-AzureRmVMExtension</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.2.0/set-azurermvmextension) | <span data-ttu-id="ac56b-140">Add a VM extension to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ac56b-140">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="ac56b-141">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="ac56b-141">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="ac56b-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ac56b-142">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="ac56b-143">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="ac56b-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ac56b-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="ac56b-144">Next steps</span></span>

<span data-ttu-id="ac56b-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="ac56b-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="ac56b-146">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac56b-146">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
