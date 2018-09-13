---
title: Azure CLI Script Sample - Restart VMs | Microsoft Docs
description: Azure CLI Script Sample - Restart VMs by tag and by ID
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
ms.date: 03/01/2017
ms.author: allclark
ms.openlocfilehash: c60eab42b709a94f5caa4f64cd6de576012f30a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549149"
---
# <a name="restart-vms"></a><span data-ttu-id="14c93-103">Restart VMs</span><span class="sxs-lookup"><span data-stu-id="14c93-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="14c93-104">This sample shows a couple of ways to get some VMs and restart them.</span><span class="sxs-lookup"><span data-stu-id="14c93-104">This sample shows a couple of ways to get some VMs and restart them.</span></span>

<span data-ttu-id="14c93-105">The first restarts all the VMs in the resource group.</span><span class="sxs-lookup"><span data-stu-id="14c93-105">The first restarts all the VMs in the resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="14c93-106">The second gets the tagged VMs using `az resouce list` and filters to the resources that are VMs, and restarts those VMs.</span><span class="sxs-lookup"><span data-stu-id="14c93-106">The second gets the tagged VMs using `az resouce list` and filters to the resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="14c93-107">This sample works in a Bash shell.</span><span class="sxs-lookup"><span data-stu-id="14c93-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="14c93-108">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="14c93-108">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="14c93-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="14c93-109">Sample script</span></span>

<span data-ttu-id="14c93-110">The sample has three scripts.</span><span class="sxs-lookup"><span data-stu-id="14c93-110">The sample has three scripts.</span></span>
<span data-ttu-id="14c93-111">The first one provisions the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="14c93-111">The first one provisions the virtual machines.</span></span>
<span data-ttu-id="14c93-112">It uses the no-wait option so the command returns without waiting on each VM to be provisioned.</span><span class="sxs-lookup"><span data-stu-id="14c93-112">It uses the no-wait option so the command returns without waiting on each VM to be provisioned.</span></span>
<span data-ttu-id="14c93-113">The second waits for the VMs to be fully provisioned.</span><span class="sxs-lookup"><span data-stu-id="14c93-113">The second waits for the VMs to be fully provisioned.</span></span>
<span data-ttu-id="14c93-114">The third script restarts all the VMs that were provisioned, and then just the tagged VMs.</span><span class="sxs-lookup"><span data-stu-id="14c93-114">The third script restarts all the VMs that were provisioned, and then just the tagged VMs.</span></span>

### <a name="provision-the-vms"></a><span data-ttu-id="14c93-115">Provision the VMs</span><span class="sxs-lookup"><span data-stu-id="14c93-115">Provision the VMs</span></span>

<span data-ttu-id="14c93-116">This script creates a resource group and then it creates three VMs to restart.</span><span class="sxs-lookup"><span data-stu-id="14c93-116">This script creates a resource group and then it creates three VMs to restart.</span></span>
<span data-ttu-id="14c93-117">Two of them are tagged.</span><span class="sxs-lookup"><span data-stu-id="14c93-117">Two of them are tagged.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision the VMs")]

### <a name="wait"></a><span data-ttu-id="14c93-118">Wait</span><span class="sxs-lookup"><span data-stu-id="14c93-118">Wait</span></span>

<span data-ttu-id="14c93-119">This script checks on the provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails to provision.</span><span class="sxs-lookup"><span data-stu-id="14c93-119">This script checks on the provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails to provision.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for the VMs to be provisioned")]

### <a name="restart-the-vms"></a><span data-ttu-id="14c93-120">Restart the VMs</span><span class="sxs-lookup"><span data-stu-id="14c93-120">Restart the VMs</span></span>

<span data-ttu-id="14c93-121">This script restarts all the VMs in the resource group, and then it restarts just the tagged VMs.</span><span class="sxs-lookup"><span data-stu-id="14c93-121">This script restarts all the VMs in the resource group, and then it restarts just the tagged VMs.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="14c93-122">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="14c93-122">Clean up deployment</span></span> 

<span data-ttu-id="14c93-123">After the script sample has been run, the following command can be used to remove the resource groups, VMs, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="14c93-123">After the script sample has been run, the following command can be used to remove the resource groups, VMs, and all related resources.</span></span>

```azurecli
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="14c93-124">Script explanation</span><span class="sxs-lookup"><span data-stu-id="14c93-124">Script explanation</span></span>

<span data-ttu-id="14c93-125">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="14c93-125">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="14c93-126">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="14c93-126">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="14c93-127">Command</span><span class="sxs-lookup"><span data-stu-id="14c93-127">Command</span></span> | <span data-ttu-id="14c93-128">Notes</span><span class="sxs-lookup"><span data-stu-id="14c93-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="14c93-129">az group create</span><span class="sxs-lookup"><span data-stu-id="14c93-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="14c93-130">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="14c93-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="14c93-131">az vm create</span><span class="sxs-lookup"><span data-stu-id="14c93-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="14c93-132">Creates the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="14c93-132">Creates the virtual machines.</span></span>  |
| [<span data-ttu-id="14c93-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="14c93-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="14c93-134">Used with `--query` to ensure the VMs are provisioned before restarting them, and then to get the IDs of the VMs to restart them.</span><span class="sxs-lookup"><span data-stu-id="14c93-134">Used with `--query` to ensure the VMs are provisioned before restarting them, and then to get the IDs of the VMs to restart them.</span></span> |
| [<span data-ttu-id="14c93-135">az resource list</span><span class="sxs-lookup"><span data-stu-id="14c93-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="14c93-136">Used with `--query` to get the IDs of the VMs using the tag.</span><span class="sxs-lookup"><span data-stu-id="14c93-136">Used with `--query` to get the IDs of the VMs using the tag.</span></span> |
| [<span data-ttu-id="14c93-137">az vm restart</span><span class="sxs-lookup"><span data-stu-id="14c93-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="14c93-138">Restarts the VMs.</span><span class="sxs-lookup"><span data-stu-id="14c93-138">Restarts the VMs.</span></span> |
| [<span data-ttu-id="14c93-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="14c93-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="14c93-140">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="14c93-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="14c93-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="14c93-141">Next steps</span></span>

<span data-ttu-id="14c93-142">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="14c93-142">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="14c93-143">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="14c93-143">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
