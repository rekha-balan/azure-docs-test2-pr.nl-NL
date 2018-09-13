---
title: Azure CLI Script Sample - Create two VMs with an internal and external NSG | Microsoft Docs
description: Azure CLI Script Sample - Create two VMs with internal and external NSG
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: 34e53f1d5b89b0b36292d95dbe533b7ec2c915b9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661722"
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="dfa2e-103">Secure network traffic between virtual machines</span><span class="sxs-lookup"><span data-stu-id="dfa2e-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="dfa2e-104">This script creates two virtual machines and secures incoming traffic to both.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-104">This script creates two virtual machines and secures incoming traffic to both.</span></span> <span data-ttu-id="dfa2e-105">One virtual machine is accessible on the internet and has a network security group (NSG) configured to allow traffic on port 3389 and port 80.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-105">One virtual machine is accessible on the internet and has a network security group (NSG) configured to allow traffic on port 3389 and port 80.</span></span> <span data-ttu-id="dfa2e-106">The second virtual machine is not accessible on the internet, and has an NSG configured to only allow traffic from the first virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-106">The second virtual machine is not accessible on the internet, and has an NSG configured to only allow traffic from the first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dfa2e-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="dfa2e-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dfa2e-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="dfa2e-108">Clean up deployment</span></span> 

<span data-ttu-id="dfa2e-109">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="dfa2e-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="dfa2e-110">Script explanation</span></span>

<span data-ttu-id="dfa2e-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="dfa2e-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dfa2e-113">Command</span><span class="sxs-lookup"><span data-stu-id="dfa2e-113">Command</span></span> | <span data-ttu-id="dfa2e-114">Notes</span><span class="sxs-lookup"><span data-stu-id="dfa2e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dfa2e-115">az group create</span><span class="sxs-lookup"><span data-stu-id="dfa2e-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dfa2e-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dfa2e-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="dfa2e-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="dfa2e-118">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="dfa2e-119">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="dfa2e-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="dfa2e-120">Creates a subnet.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="dfa2e-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="dfa2e-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="dfa2e-122">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-122">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="dfa2e-123">This command also specifies the virtual machine image to be used, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-123">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="dfa2e-124">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="dfa2e-124">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="dfa2e-125">Updates an NSG rule.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-125">Updates an NSG rule.</span></span> <span data-ttu-id="dfa2e-126">In this sample, the back-end rule is updated to pass through traffic only from the front-end subnet.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-126">In this sample, the back-end rule is updated to pass through traffic only from the front-end subnet.</span></span> |
| [<span data-ttu-id="dfa2e-127">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="dfa2e-127">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="dfa2e-128">Returns information about a network security group rule.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-128">Returns information about a network security group rule.</span></span> <span data-ttu-id="dfa2e-129">In this sample, the rule name is stored in a variable for use later in the script.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-129">In this sample, the rule name is stored in a variable for use later in the script.</span></span> |
| [<span data-ttu-id="dfa2e-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="dfa2e-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="dfa2e-131">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="dfa2e-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dfa2e-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="dfa2e-132">Next steps</span></span>

<span data-ttu-id="dfa2e-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dfa2e-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dfa2e-134">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dfa2e-134">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
