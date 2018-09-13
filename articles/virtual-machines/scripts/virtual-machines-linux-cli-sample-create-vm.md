---
title: Azure CLI Script Sample - Create a Linux VM | Microsoft Docs
description: Azure CLI Script Sample - Create a Linux VM
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
ms.openlocfilehash: 71ac2494c71802fd9554a004ac7607f423657a1e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554377"
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="14437-103">Create a fully configured virtual machine</span><span class="sxs-lookup"><span data-stu-id="14437-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="14437-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span><span class="sxs-lookup"><span data-stu-id="14437-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="14437-105">After running the script, you can access the virtual machine over SSH.</span><span class="sxs-lookup"><span data-stu-id="14437-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="14437-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="14437-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="14437-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="14437-107">Clean up deployment</span></span> 

<span data-ttu-id="14437-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="14437-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="14437-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="14437-109">Script explanation</span></span>

<span data-ttu-id="14437-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="14437-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="14437-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="14437-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="14437-112">Command</span><span class="sxs-lookup"><span data-stu-id="14437-112">Command</span></span> | <span data-ttu-id="14437-113">Notes</span><span class="sxs-lookup"><span data-stu-id="14437-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="14437-114">az group create</span><span class="sxs-lookup"><span data-stu-id="14437-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="14437-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="14437-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="14437-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="14437-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="14437-117">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="14437-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="14437-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="14437-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="14437-119">Creates a public IP address with a static IP address and an associated DNS name.</span><span class="sxs-lookup"><span data-stu-id="14437-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="14437-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="14437-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="14437-121">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="14437-121">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="14437-122">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="14437-122">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="14437-123">Creates an NSG rule to allow inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="14437-123">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="14437-124">In this sample, port 22 is opened for SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="14437-124">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="14437-125">az network nic create</span><span class="sxs-lookup"><span data-stu-id="14437-125">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="14437-126">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="14437-126">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="14437-127">az vm create</span><span class="sxs-lookup"><span data-stu-id="14437-127">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="14437-128">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="14437-128">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="14437-129">This command also specifies the virtual machine image to be used, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="14437-129">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="14437-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="14437-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="14437-131">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="14437-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="14437-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="14437-132">Next steps</span></span>

<span data-ttu-id="14437-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="14437-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="14437-134">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="14437-134">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
