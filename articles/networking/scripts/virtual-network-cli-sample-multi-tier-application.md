---
title: Azure CLI script sample - Create a network for multi-tier applications | Microsoft Docs
description: Azure CLI script sample - Create a virtual network for multi-tier applications.
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: aa5fef6e8910a5b0b5fe89d5c8cfb141415d07a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855687"
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="9e569-103">Create a network for multi-tier applications</span><span class="sxs-lookup"><span data-stu-id="9e569-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="9e569-104">This script sample creates a virtual network with front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="9e569-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="9e569-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="9e569-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="9e569-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span><span class="sxs-lookup"><span data-stu-id="9e569-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="9e569-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="9e569-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9e569-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="9e569-108">Clean up deployment</span></span> 

<span data-ttu-id="9e569-109">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="9e569-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="9e569-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="9e569-110">Script explanation</span></span>

<span data-ttu-id="9e569-111">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span><span class="sxs-lookup"><span data-stu-id="9e569-111">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="9e569-112">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="9e569-112">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="9e569-113">Command</span><span class="sxs-lookup"><span data-stu-id="9e569-113">Command</span></span> | <span data-ttu-id="9e569-114">Notes</span><span class="sxs-lookup"><span data-stu-id="9e569-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9e569-115">az group create</span><span class="sxs-lookup"><span data-stu-id="9e569-115">az group create</span></span>](/cli/azure/group#az_group_create) | <span data-ttu-id="9e569-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="9e569-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9e569-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="9e569-117">az network vnet create</span></span>](/cli/azure/network/vnet#az_network_vnet_create) | <span data-ttu-id="9e569-118">Creates an Azure virtual network and front-end subnet.</span><span class="sxs-lookup"><span data-stu-id="9e569-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="9e569-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="9e569-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#az_network_vnet_subnet_create) | <span data-ttu-id="9e569-120">Creates a back-end subnet.</span><span class="sxs-lookup"><span data-stu-id="9e569-120">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="9e569-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="9e569-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#az_network_public_ip_create) | <span data-ttu-id="9e569-122">Creates a public IP address to access the VM from the Internet.</span><span class="sxs-lookup"><span data-stu-id="9e569-122">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="9e569-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="9e569-123">az network nic create</span></span>](/cli/azure/network/nic#az_network_nic_create) | <span data-ttu-id="9e569-124">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="9e569-124">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="9e569-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="9e569-125">az network nsg create</span></span>](/cli/azure/network/nsg#az_network_nsg_create) | <span data-ttu-id="9e569-126">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="9e569-126">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="9e569-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="9e569-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#az_network_nsg_rule_create) |<span data-ttu-id="9e569-128">Creates NSG rules that allow or block specific ports to specific subnets.</span><span class="sxs-lookup"><span data-stu-id="9e569-128">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="9e569-129">az vm create</span><span class="sxs-lookup"><span data-stu-id="9e569-129">az vm create</span></span>](/cli/azure/vm#az_vm_create) | <span data-ttu-id="9e569-130">Creates virtual machines and attaches a NIC to each VM.</span><span class="sxs-lookup"><span data-stu-id="9e569-130">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="9e569-131">This command also specifies the virtual machine image to use and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="9e569-131">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="9e569-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="9e569-132">az group delete</span></span>](/cli/azure/group#az_group_delete) | <span data-ttu-id="9e569-133">Deletes a resource group and all resources it contains.</span><span class="sxs-lookup"><span data-stu-id="9e569-133">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9e569-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e569-134">Next steps</span></span>

<span data-ttu-id="9e569-135">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="9e569-135">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span></span>

<span data-ttu-id="9e569-136">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="9e569-136">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>