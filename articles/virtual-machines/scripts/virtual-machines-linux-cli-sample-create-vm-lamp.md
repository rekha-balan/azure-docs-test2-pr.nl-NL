---
title: Azure CLI Script Sample - Deploy the LAMP Stack in a Load-Balanced Virutal Machin Scale Set | Microsoft Docs
description: Use a custom script extension to deploy the LAMP Stack in a load=balanced virtual machine scale set on Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: 1764fc15a888fbe15cc14b990721240d1baf3c40
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791029"
---
# <a name="deploy-the-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="ba0b4-103">Deploy the LAMP stack in a load-balanced virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="ba0b4-103">Deploy the LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="ba0b4-104">This example creates a virtual machine scale set and applies an extension that runs a custom script to deploy the LAMP stack on each virtual machine in the scale set.</span><span class="sxs-lookup"><span data-stu-id="ba0b4-104">This example creates a virtual machine scale set and applies an extension that runs a custom script to deploy the LAMP stack on each virtual machine in the scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="ba0b4-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="ba0b4-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="ba0b4-106">Connect</span><span class="sxs-lookup"><span data-stu-id="ba0b4-106">Connect</span></span>

<span data-ttu-id="ba0b4-107">Use this code to see how to connect to your VMs and your scale set.</span><span class="sxs-lookup"><span data-stu-id="ba0b4-107">Use this code to see how to connect to your VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access the virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ba0b4-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="ba0b4-108">Clean up deployment</span></span> 

<span data-ttu-id="ba0b4-109">Run the following command to remove the resource group, the scale set and VMs, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ba0b4-109">Run the following command to remove the resource group, the scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ba0b4-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="ba0b4-110">Script explanation</span></span>

<span data-ttu-id="ba0b4-111">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ba0b4-111">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="ba0b4-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="ba0b4-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ba0b4-113">Command</span><span class="sxs-lookup"><span data-stu-id="ba0b4-113">Command</span></span> | <span data-ttu-id="ba0b4-114">Notes</span><span class="sxs-lookup"><span data-stu-id="ba0b4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ba0b4-115">az group create</span><span class="sxs-lookup"><span data-stu-id="ba0b4-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az_group_create) | <span data-ttu-id="ba0b4-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="ba0b4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ba0b4-117">az vmss create</span><span class="sxs-lookup"><span data-stu-id="ba0b4-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#az_vmss_create) | <span data-ttu-id="ba0b4-118">Creates a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="ba0b4-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="ba0b4-119">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="ba0b4-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#az_network_lb_rule_create) | <span data-ttu-id="ba0b4-120">Add a load-balanced endpoint</span><span class="sxs-lookup"><span data-stu-id="ba0b4-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="ba0b4-121">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="ba0b4-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#az_vmss_extension_set) | <span data-ttu-id="ba0b4-122">Create the extension that runs the custom script on deployment of a VM</span><span class="sxs-lookup"><span data-stu-id="ba0b4-122">Create the extension that runs the custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="ba0b4-123">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="ba0b4-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#az_vmss_update_instances) | <span data-ttu-id="ba0b4-124">Run the custom script on the VM instances that were deployed before the extension was applied to the scale set.</span><span class="sxs-lookup"><span data-stu-id="ba0b4-124">Run the custom script on the VM instances that were deployed before the extension was applied to the scale set.</span></span> |
| [<span data-ttu-id="ba0b4-125">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="ba0b4-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#az_vmss_scale) | <span data-ttu-id="ba0b4-126">Scale up the scale set by adding more VM instances.</span><span class="sxs-lookup"><span data-stu-id="ba0b4-126">Scale up the scale set by adding more VM instances.</span></span> <span data-ttu-id="ba0b4-127">The custom script is run on these when they are deployed.</span><span class="sxs-lookup"><span data-stu-id="ba0b4-127">The custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="ba0b4-128">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="ba0b4-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#az_network_public_ip_list) | <span data-ttu-id="ba0b4-129">Get the IP addresses of the VMs created by the sample.</span><span class="sxs-lookup"><span data-stu-id="ba0b4-129">Get the IP addresses of the VMs created by the sample.</span></span> |
| [<span data-ttu-id="ba0b4-130">az network lb show</span><span class="sxs-lookup"><span data-stu-id="ba0b4-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#az_network_lb_show) | <span data-ttu-id="ba0b4-131">Get the frontend and backend ports used by the load balancer.</span><span class="sxs-lookup"><span data-stu-id="ba0b4-131">Get the frontend and backend ports used by the load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ba0b4-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="ba0b4-132">Next steps</span></span>

<span data-ttu-id="ba0b4-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="ba0b4-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="ba0b4-134">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba0b4-134">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
