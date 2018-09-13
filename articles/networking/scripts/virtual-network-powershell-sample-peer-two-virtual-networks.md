---
title: Azure PowerShell Script Sample - Peer two virtual networks | Microsoft Docs
description: Azure PowerShell Script Sample - Peer two virtual networks
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
ms.openlocfilehash: 6c475311f8b0299908dfc26aa590c1990e00bc4a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867266"
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="8a365-103">Peer two virtual networks</span><span class="sxs-lookup"><span data-stu-id="8a365-103">Peer two virtual networks</span></span>

<span data-ttu-id="8a365-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span><span class="sxs-lookup"><span data-stu-id="8a365-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="8a365-105">After running the script, you will create a peering between two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="8a365-105">After running the script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="8a365-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="8a365-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8a365-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="8a365-107">Sample script</span></span>

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8a365-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="8a365-108">Clean up deployment</span></span> 

<span data-ttu-id="8a365-109">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="8a365-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8a365-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="8a365-110">Script explanation</span></span>

<span data-ttu-id="8a365-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="8a365-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="8a365-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="8a365-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8a365-113">Command</span><span class="sxs-lookup"><span data-stu-id="8a365-113">Command</span></span> | <span data-ttu-id="8a365-114">Notes</span><span class="sxs-lookup"><span data-stu-id="8a365-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8a365-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8a365-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8a365-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="8a365-116">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="8a365-117">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="8a365-117">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="8a365-118">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="8a365-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="8a365-119">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="8a365-119">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="8a365-120">Creates a peering between two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="8a365-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="8a365-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8a365-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8a365-122">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="8a365-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8a365-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a365-123">Next steps</span></span>

<span data-ttu-id="8a365-124">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8a365-124">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="8a365-125">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8a365-125">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
