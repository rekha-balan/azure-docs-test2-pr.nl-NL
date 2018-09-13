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
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.openlocfilehash: 81d61eac30752b6d5870102c9a0c551a9159bba7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540917"
---
# <a name="deploy-the-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="f005e-103">Deploy the LAMP stack in a load-balanced virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f005e-103">Deploy the LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="f005e-104">This example creates a virtual machine scale set and applies an extension that runs a custom script to deploy the LAMP stack on each virtual machine in the scale set.</span><span class="sxs-lookup"><span data-stu-id="f005e-104">This example creates a virtual machine scale set and applies an extension that runs a custom script to deploy the LAMP stack on each virtual machine in the scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="f005e-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="f005e-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="f005e-106">Connect</span><span class="sxs-lookup"><span data-stu-id="f005e-106">Connect</span></span>

<span data-ttu-id="f005e-107">Use this code to see how to connect to your VMs and your scale set.</span><span class="sxs-lookup"><span data-stu-id="f005e-107">Use this code to see how to connect to your VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access the virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f005e-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="f005e-108">Clean up deployment</span></span> 

<span data-ttu-id="f005e-109">Run the following command to remove the resource group, the scale set and VMs, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f005e-109">Run the following command to remove the resource group, the scale set and VMs, and all related resources.</span></span>

```azurecli
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f005e-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f005e-110">Script explanation</span></span>

<span data-ttu-id="f005e-111">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f005e-111">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="f005e-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="f005e-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f005e-113">Command</span><span class="sxs-lookup"><span data-stu-id="f005e-113">Command</span></span> | <span data-ttu-id="f005e-114">Notes</span><span class="sxs-lookup"><span data-stu-id="f005e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f005e-115">az group create</span><span class="sxs-lookup"><span data-stu-id="f005e-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f005e-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="f005e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f005e-117">az vmss create</span><span class="sxs-lookup"><span data-stu-id="f005e-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="f005e-118">Creates a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f005e-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="f005e-119">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="f005e-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="f005e-120">Add a load-balanced endpoint</span><span class="sxs-lookup"><span data-stu-id="f005e-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="f005e-121">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="f005e-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="f005e-122">Create the extension that runs the custom script on deployment of a VM</span><span class="sxs-lookup"><span data-stu-id="f005e-122">Create the extension that runs the custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="f005e-123">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="f005e-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="f005e-124">Run the custom script on the VM instances that were deployed before the extension was applied to the scale set.</span><span class="sxs-lookup"><span data-stu-id="f005e-124">Run the custom script on the VM instances that were deployed before the extension was applied to the scale set.</span></span> |
| [<span data-ttu-id="f005e-125">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="f005e-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="f005e-126">Scale up the scale set by adding more VM instances.</span><span class="sxs-lookup"><span data-stu-id="f005e-126">Scale up the scale set by adding more VM instances.</span></span> <span data-ttu-id="f005e-127">The custom script is run on these when they are deployed.</span><span class="sxs-lookup"><span data-stu-id="f005e-127">The custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="f005e-128">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="f005e-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="f005e-129">Get the IP addresses of the VMs created by the sample.</span><span class="sxs-lookup"><span data-stu-id="f005e-129">Get the IP addresses of the VMs created by the sample.</span></span> |
| [<span data-ttu-id="f005e-130">az network lb show</span><span class="sxs-lookup"><span data-stu-id="f005e-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="f005e-131">Get the frontend and backend ports used by the load balancer.</span><span class="sxs-lookup"><span data-stu-id="f005e-131">Get the frontend and backend ports used by the load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f005e-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="f005e-132">Next steps</span></span>

<span data-ttu-id="f005e-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f005e-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f005e-134">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f005e-134">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
