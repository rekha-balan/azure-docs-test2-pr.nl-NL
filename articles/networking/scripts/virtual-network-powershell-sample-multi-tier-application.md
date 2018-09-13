---
title: Azure PowerShell script sample - Create a network for multi-tier applications | Microsoft Docs
description: Azure PowerShell script sample - Create a virtual network for multi-tier applications.
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: cff445f7657d5661f8577d9f6be7072eed2c1c28
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866193"
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="f17c1-103">Create a network for multi-tier applications</span><span class="sxs-lookup"><span data-stu-id="f17c1-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="f17c1-104">This script sample creates a virtual network with front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="f17c1-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="f17c1-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="f17c1-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="f17c1-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span><span class="sxs-lookup"><span data-stu-id="f17c1-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="f17c1-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="f17c1-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f17c1-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="f17c1-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f17c1-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="f17c1-109">Clean up deployment</span></span> 

<span data-ttu-id="f17c1-110">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f17c1-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f17c1-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f17c1-111">Script explanation</span></span>

<span data-ttu-id="f17c1-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span><span class="sxs-lookup"><span data-stu-id="f17c1-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="f17c1-113">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="f17c1-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="f17c1-114">Command</span><span class="sxs-lookup"><span data-stu-id="f17c1-114">Command</span></span> | <span data-ttu-id="f17c1-115">Notes</span><span class="sxs-lookup"><span data-stu-id="f17c1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f17c1-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f17c1-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f17c1-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="f17c1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f17c1-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f17c1-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="f17c1-119">Creates an Azure virtual network and front-end subnet.</span><span class="sxs-lookup"><span data-stu-id="f17c1-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="f17c1-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="f17c1-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="f17c1-121">Creates a back-end subnet.</span><span class="sxs-lookup"><span data-stu-id="f17c1-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="f17c1-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="f17c1-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="f17c1-123">Creates a public IP address to access the VM from the Internet.</span><span class="sxs-lookup"><span data-stu-id="f17c1-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="f17c1-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="f17c1-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="f17c1-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="f17c1-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="f17c1-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="f17c1-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="f17c1-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="f17c1-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="f17c1-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="f17c1-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="f17c1-129">Creates NSG rules that allow or block specific ports to specific subnets.</span><span class="sxs-lookup"><span data-stu-id="f17c1-129">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="f17c1-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="f17c1-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="f17c1-131">Creates virtual machines and attaches a NIC to each VM.</span><span class="sxs-lookup"><span data-stu-id="f17c1-131">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="f17c1-132">This command also specifies the virtual machine image to use and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="f17c1-132">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="f17c1-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f17c1-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f17c1-134">Deletes a resource group and all resources it contains.</span><span class="sxs-lookup"><span data-stu-id="f17c1-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f17c1-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="f17c1-135">Next steps</span></span>

<span data-ttu-id="f17c1-136">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f17c1-136">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="f17c1-137">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f17c1-137">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
