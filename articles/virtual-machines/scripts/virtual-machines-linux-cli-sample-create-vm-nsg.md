---
title: Azure CLI Script Sample - Create two VMs with an internal and external NSG | Microsoft Docs
description: Azure CLI Script Sample - Create two VMs with internal and external NSG
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.openlocfilehash: efa4173bbc576753a335009bc6cbeceee4e0d20d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553926"
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="58722-103">Secure network traffic between virtual machines</span><span class="sxs-lookup"><span data-stu-id="58722-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="58722-104">This script creates two virtual machines and secures incoming traffic to both.</span><span class="sxs-lookup"><span data-stu-id="58722-104">This script creates two virtual machines and secures incoming traffic to both.</span></span> <span data-ttu-id="58722-105">One virtual machine is accessible on the internet and has a network security group (NSG) configured to allow traffic on port 22 and port 80.</span><span class="sxs-lookup"><span data-stu-id="58722-105">One virtual machine is accessible on the internet and has a network security group (NSG) configured to allow traffic on port 22 and port 80.</span></span> <span data-ttu-id="58722-106">The second virtual machine is not accessible on the internet, and has an NSG configured to only allow traffic from the first virtual machine.</span><span class="sxs-lookup"><span data-stu-id="58722-106">The second virtual machine is not accessible on the internet, and has an NSG configured to only allow traffic from the first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="58722-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="58722-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="58722-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="58722-108">Clean up deployment</span></span> 

<span data-ttu-id="58722-109">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="58722-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="58722-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="58722-110">Script explanation</span></span>

<span data-ttu-id="58722-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="58722-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="58722-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="58722-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="58722-113">Command</span><span class="sxs-lookup"><span data-stu-id="58722-113">Command</span></span> | <span data-ttu-id="58722-114">Notes</span><span class="sxs-lookup"><span data-stu-id="58722-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="58722-115">az group create</span><span class="sxs-lookup"><span data-stu-id="58722-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="58722-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="58722-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="58722-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="58722-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="58722-118">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="58722-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="58722-119">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="58722-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="58722-120">Creates a subnet.</span><span class="sxs-lookup"><span data-stu-id="58722-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="58722-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="58722-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="58722-122">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="58722-122">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="58722-123">This command also specifies the virtual machine image to be used, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="58722-123">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="58722-124">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="58722-124">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="58722-125">Returns information about a network security group rule.</span><span class="sxs-lookup"><span data-stu-id="58722-125">Returns information about a network security group rule.</span></span> <span data-ttu-id="58722-126">In this sample, the rule name is stored in a variable for use later in the script.</span><span class="sxs-lookup"><span data-stu-id="58722-126">In this sample, the rule name is stored in a variable for use later in the script.</span></span> |
| [<span data-ttu-id="58722-127">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="58722-127">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="58722-128">Updates an NSG rule.</span><span class="sxs-lookup"><span data-stu-id="58722-128">Updates an NSG rule.</span></span> <span data-ttu-id="58722-129">In this sample, the back-end rule is updated to pass through traffic only from the front-end subnet.</span><span class="sxs-lookup"><span data-stu-id="58722-129">In this sample, the back-end rule is updated to pass through traffic only from the front-end subnet.</span></span> |
| [<span data-ttu-id="58722-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="58722-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="58722-131">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="58722-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="58722-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="58722-132">Next steps</span></span>

<span data-ttu-id="58722-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="58722-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="58722-134">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58722-134">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
