---
title: Azure PowerShell Script Sample - Docker | Microsoft Docs
description: Azure PowerShell Script Sample - Docker
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
ms.date: 03/02/2017
ms.author: nepeters
ms.openlocfilehash: 9ac729c51ad8d9db64bb7cfb8339edfce3ce0f52
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662050"
---
# <a name="create-a-docker-host-with-powershell"></a><span data-ttu-id="a2fb3-103">Create a Docker host with PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2fb3-103">Create a Docker host with PowerShell</span></span>

<span data-ttu-id="a2fb3-104">This script creates a virtual machine with Docker enabled and starts a container running NGINX.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-104">This script creates a virtual machine with Docker enabled and starts a container running NGINX.</span></span> <span data-ttu-id="a2fb3-105">After running the script, you can access the NGINX web server through the FQDN of the Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-105">After running the script, you can access the NGINX web server through the FQDN of the Azure virtual machine.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a2fb3-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="a2fb3-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-docker-host/create-docker-host.ps1 "Create Docker host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a2fb3-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="a2fb3-107">Clean up deployment</span></span> 

<span data-ttu-id="a2fb3-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a2fb3-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="a2fb3-109">Script explanation</span></span>

<span data-ttu-id="a2fb3-110">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="a2fb3-111">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a2fb3-112">Command</span><span class="sxs-lookup"><span data-stu-id="a2fb3-112">Command</span></span> | <span data-ttu-id="a2fb3-113">Notes</span><span class="sxs-lookup"><span data-stu-id="a2fb3-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a2fb3-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a2fb3-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/new-azurermresourcegroup) | <span data-ttu-id="a2fb3-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a2fb3-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="a2fb3-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="a2fb3-117">Creates a subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-117">Creates a subnet configuration.</span></span> <span data-ttu-id="a2fb3-118">This configuration is used with the virtual network creation process.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-118">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="a2fb3-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="a2fb3-119">New-AzureRmVirtualNetwork</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v1.0.13/new-azurermvirtualnetwork) | <span data-ttu-id="a2fb3-120">Creates a virtual network.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="a2fb3-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="a2fb3-121">New-AzureRmPublicIpAddress</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermpublicipaddress) | <span data-ttu-id="a2fb3-122">Creates a public IP address.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="a2fb3-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="a2fb3-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v2.1.0/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="a2fb3-124">Creates a network security group rule configuration.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="a2fb3-125">This configuration is used to create an NSG rule when the NSG is created.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-125">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="a2fb3-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="a2fb3-126">New-AzureRmNetworkSecurityGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.1.0/new-azurermnetworksecuritygroup) | <span data-ttu-id="a2fb3-127">Creates a network security group.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="a2fb3-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="a2fb3-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v1.0.13/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="a2fb3-129">Gets subnet information.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-129">Gets subnet information.</span></span> <span data-ttu-id="a2fb3-130">This information is used when creating a network interface.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="a2fb3-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="a2fb3-131">New-AzureRmNetworkInterface</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.4.0/new-azurermnetworkinterface) | <span data-ttu-id="a2fb3-132">Creates a network interface.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="a2fb3-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="a2fb3-133">New-AzureRmVMConfig</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v1.3.4/new-azurermvmconfig) | <span data-ttu-id="a2fb3-134">Creates a VM configuration.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-134">Creates a VM configuration.</span></span> <span data-ttu-id="a2fb3-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="a2fb3-136">The configuration is used during VM creation.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-136">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="a2fb3-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="a2fb3-137">New-AzureRmVM</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v1.3.4/new-azurermvm) | <span data-ttu-id="a2fb3-138">Create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="a2fb3-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="a2fb3-139">Set-AzureRmVMExtension</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.2.0/set-azurermvmextension) | <span data-ttu-id="a2fb3-140">Add a VM extension to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-140">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="a2fb3-141">In this sample, the Docker extension is used to configure Docker and run an NGINX Docker container.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-141">In this sample, the Docker extension is used to configure Docker and run an NGINX Docker container.</span></span> |
|[<span data-ttu-id="a2fb3-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a2fb3-142">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="a2fb3-143">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="a2fb3-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a2fb3-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2fb3-144">Next steps</span></span>

<span data-ttu-id="a2fb3-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="a2fb3-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/).</span></span>

<span data-ttu-id="a2fb3-146">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a2fb3-146">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
