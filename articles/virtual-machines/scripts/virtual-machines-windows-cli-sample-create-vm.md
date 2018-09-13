---
title: Azure CLI Script Sample - Create a Windows Server VM | Microsoft Docs
description: Azure CLI Script Sample - Create a Windows Server VM
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: e200babc847e45fecd2c92596a5d492d25a0405c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549677"
---
# <a name="create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="17ce4-103">Create a virtual machine with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="17ce4-103">Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="17ce4-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="17ce4-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="17ce4-105">After running the script, you can access the virtual machine through a Remote Desktop connection.</span><span class="sxs-lookup"><span data-stu-id="17ce4-105">After running the script, you can access the virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="17ce4-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="17ce4-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="17ce4-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="17ce4-107">Clean up deployment</span></span> 

<span data-ttu-id="17ce4-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="17ce4-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="17ce4-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="17ce4-109">Script explanation</span></span>

<span data-ttu-id="17ce4-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="17ce4-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="17ce4-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="17ce4-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="17ce4-112">Command</span><span class="sxs-lookup"><span data-stu-id="17ce4-112">Command</span></span> | <span data-ttu-id="17ce4-113">Notes</span><span class="sxs-lookup"><span data-stu-id="17ce4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="17ce4-114">az group create</span><span class="sxs-lookup"><span data-stu-id="17ce4-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="17ce4-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="17ce4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="17ce4-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="17ce4-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="17ce4-117">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="17ce4-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="17ce4-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="17ce4-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="17ce4-119">Creates a public IP address with a static IP address and an associated DNS name.</span><span class="sxs-lookup"><span data-stu-id="17ce4-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="17ce4-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="17ce4-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="17ce4-121">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="17ce4-121">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="17ce4-122">az network nic create</span><span class="sxs-lookup"><span data-stu-id="17ce4-122">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="17ce4-123">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="17ce4-123">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="17ce4-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="17ce4-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="17ce4-125">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="17ce4-125">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="17ce4-126">This command also specifies the virtual machine image to be used, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="17ce4-126">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="17ce4-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="17ce4-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="17ce4-128">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="17ce4-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="17ce4-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="17ce4-129">Next steps</span></span>

<span data-ttu-id="17ce4-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="17ce4-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="17ce4-131">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="17ce4-131">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
