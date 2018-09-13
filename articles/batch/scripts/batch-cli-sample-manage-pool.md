---
title: Azure CLI Script Sample - Managing Pools in Batch | Microsoft Docs
description: Azure CLI Script Sample - Managing Pools in Batch
services: batch
documentationcenter: ''
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: ''
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/20/2017
ms.author: antisch
ms.openlocfilehash: 67c3c999cb5fe6ea59d7298843f0528082139a80
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550276"
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="7c834-103">Managing Azure Batch pools with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7c834-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="7c834-104">These script demonstrates some of the tools available in the Azure CLI to create and manage pools of compute nodes in the Azure Batch service.</span><span class="sxs-lookup"><span data-stu-id="7c834-104">These script demonstrates some of the tools available in the Azure CLI to create and manage pools of compute nodes in the Azure Batch service.</span></span>

<span data-ttu-id="7c834-105">Running these scripts assumes that a Batch account has already been set up and an application configured.</span><span class="sxs-lookup"><span data-stu-id="7c834-105">Running these scripts assumes that a Batch account has already been set up and an application configured.</span></span> <span data-ttu-id="7c834-106">For more information, please see the [sample scripts](../batch-cli-samples.md) covering each of these topics.</span><span class="sxs-lookup"><span data-stu-id="7c834-106">For more information, please see the [sample scripts](../batch-cli-samples.md) covering each of these topics.</span></span>

> [!NOTE]
> <span data-ttu-id="7c834-107">The commands in this sample create Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="7c834-107">The commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="7c834-108">Running VMs will accrue charges to your account.</span><span class="sxs-lookup"><span data-stu-id="7c834-108">Running VMs will accrue charges to your account.</span></span> <span data-ttu-id="7c834-109">To minimize these charges, delete the VMs once you're done running the sample.</span><span class="sxs-lookup"><span data-stu-id="7c834-109">To minimize these charges, delete the VMs once you're done running the sample.</span></span> <span data-ttu-id="7c834-110">See [Clean up pools](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="7c834-110">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="7c834-111">If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to log into Azure.</span><span class="sxs-lookup"><span data-stu-id="7c834-111">If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to log into Azure.</span></span>

<span data-ttu-id="7c834-112">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span><span class="sxs-lookup"><span data-stu-id="7c834-112">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="7c834-113">Pool with cloud service configuration sample script</span><span class="sxs-lookup"><span data-stu-id="7c834-113">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="7c834-114">Pool with virtual machine configuration sample script</span><span class="sxs-lookup"><span data-stu-id="7c834-114">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="7c834-115">Clean up pools</span><span class="sxs-lookup"><span data-stu-id="7c834-115">Clean up pools</span></span>

<span data-ttu-id="7c834-116">After you run the above sample script, run the following command to delete the pools.</span><span class="sxs-lookup"><span data-stu-id="7c834-116">After you run the above sample script, run the following command to delete the pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="7c834-117">Script explanation</span><span class="sxs-lookup"><span data-stu-id="7c834-117">Script explanation</span></span>

<span data-ttu-id="7c834-118">This script uses the following commands to create and manipulate Batch pools.</span><span class="sxs-lookup"><span data-stu-id="7c834-118">This script uses the following commands to create and manipulate Batch pools.</span></span>
<span data-ttu-id="7c834-119">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="7c834-119">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="7c834-120">Command</span><span class="sxs-lookup"><span data-stu-id="7c834-120">Command</span></span> | <span data-ttu-id="7c834-121">Notes</span><span class="sxs-lookup"><span data-stu-id="7c834-121">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7c834-122">az batch account login</span><span class="sxs-lookup"><span data-stu-id="7c834-122">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="7c834-123">Authenticate against a Batch account.</span><span class="sxs-lookup"><span data-stu-id="7c834-123">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="7c834-124">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="7c834-124">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="7c834-125">List the available applications in the Batch account.</span><span class="sxs-lookup"><span data-stu-id="7c834-125">List the available applications in the Batch account.</span></span>  |
| [<span data-ttu-id="7c834-126">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="7c834-126">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="7c834-127">Create a pool of VMs.</span><span class="sxs-lookup"><span data-stu-id="7c834-127">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="7c834-128">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="7c834-128">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="7c834-129">Update properties of a pool.</span><span class="sxs-lookup"><span data-stu-id="7c834-129">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="7c834-130">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="7c834-130">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="7c834-131">List available node agent SKUs and image information.</span><span class="sxs-lookup"><span data-stu-id="7c834-131">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="7c834-132">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="7c834-132">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="7c834-133">Resize the number of running VMs in the specified pool.</span><span class="sxs-lookup"><span data-stu-id="7c834-133">Resize the number of running VMs in the specified pool.</span></span>  |
| [<span data-ttu-id="7c834-134">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="7c834-134">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="7c834-135">Display the properties of a pool.</span><span class="sxs-lookup"><span data-stu-id="7c834-135">Display the properties of a pool.</span></span>  |
| [<span data-ttu-id="7c834-136">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="7c834-136">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="7c834-137">Delete the specified pool.</span><span class="sxs-lookup"><span data-stu-id="7c834-137">Delete the specified pool.</span></span>  |
| [<span data-ttu-id="7c834-138">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="7c834-138">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="7c834-139">Enable auto-scaling on a pool and apply a formula.</span><span class="sxs-lookup"><span data-stu-id="7c834-139">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="7c834-140">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="7c834-140">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="7c834-141">Disable auto-scaling on a pool.</span><span class="sxs-lookup"><span data-stu-id="7c834-141">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="7c834-142">az batch node list</span><span class="sxs-lookup"><span data-stu-id="7c834-142">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="7c834-143">List all the compute node in the specified pool.</span><span class="sxs-lookup"><span data-stu-id="7c834-143">List all the compute node in the specified pool.</span></span>  |
| [<span data-ttu-id="7c834-144">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="7c834-144">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="7c834-145">Reboot the specified compute node.</span><span class="sxs-lookup"><span data-stu-id="7c834-145">Reboot the specified compute node.</span></span>  |
| [<span data-ttu-id="7c834-146">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="7c834-146">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="7c834-147">Delete the listed nodes from the specified pool.</span><span class="sxs-lookup"><span data-stu-id="7c834-147">Delete the listed nodes from the specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="7c834-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c834-148">Next steps</span></span>

<span data-ttu-id="7c834-149">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c834-149">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7c834-150">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7c834-150">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

