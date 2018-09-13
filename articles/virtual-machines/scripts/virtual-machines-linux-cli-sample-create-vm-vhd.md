---
title: Azure CLI Script Sample - Create a VM with a VHD  | Microsoft Docs
description: Azure CLI Script Sample - Create a VM using a virtual hard disk.
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
ms.date: 03/09/2017
ms.author: allclark
ms.openlocfilehash: 913812180635b282ab19f99430fcd51112046aa2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555635"
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="fc380-103">Create a VM with a virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="fc380-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="fc380-104">This example creates a virtual machine using a VHD.</span><span class="sxs-lookup"><span data-stu-id="fc380-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="fc380-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading the VHD to the container.</span><span class="sxs-lookup"><span data-stu-id="fc380-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading the VHD to the container.</span></span>
<span data-ttu-id="fc380-106">It replaces the ssh public key with your public key so that you have access to the VM.</span><span class="sxs-lookup"><span data-stu-id="fc380-106">It replaces the ssh public key with your public key so that you have access to the VM.</span></span>

<span data-ttu-id="fc380-107">You'll need a bootable VHD.</span><span class="sxs-lookup"><span data-stu-id="fc380-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="fc380-108">You can download the VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span><span class="sxs-lookup"><span data-stu-id="fc380-108">You can download the VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="fc380-109">The script looks for `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="fc380-109">The script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fc380-110">Sample script</span><span class="sxs-lookup"><span data-stu-id="fc380-110">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fc380-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="fc380-111">Clean up deployment</span></span> 

<span data-ttu-id="fc380-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="fc380-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="fc380-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="fc380-113">Script explanation</span></span>

<span data-ttu-id="fc380-114">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="fc380-114">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="fc380-115">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="fc380-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fc380-116">Command</span><span class="sxs-lookup"><span data-stu-id="fc380-116">Command</span></span> | <span data-ttu-id="fc380-117">Notes</span><span class="sxs-lookup"><span data-stu-id="fc380-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fc380-118">az group create</span><span class="sxs-lookup"><span data-stu-id="fc380-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fc380-119">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="fc380-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fc380-120">az storage account list</span><span class="sxs-lookup"><span data-stu-id="fc380-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="fc380-121">Lists storage accounts</span><span class="sxs-lookup"><span data-stu-id="fc380-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="fc380-122">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="fc380-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="fc380-123">Checks that a storage account name is valid and that it doesn't already exist</span><span class="sxs-lookup"><span data-stu-id="fc380-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="fc380-124">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="fc380-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="fc380-125">Lists keys for the storage accounts</span><span class="sxs-lookup"><span data-stu-id="fc380-125">Lists keys for the storage accounts</span></span> |
| [<span data-ttu-id="fc380-126">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="fc380-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="fc380-127">Checks whether the blob exists</span><span class="sxs-lookup"><span data-stu-id="fc380-127">Checks whether the blob exists</span></span> |
| [<span data-ttu-id="fc380-128">az storage container create</span><span class="sxs-lookup"><span data-stu-id="fc380-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="fc380-129">Creates a container in a storage account.</span><span class="sxs-lookup"><span data-stu-id="fc380-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="fc380-130">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="fc380-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="fc380-131">Creates a blob in the container by uploading the VHD.</span><span class="sxs-lookup"><span data-stu-id="fc380-131">Creates a blob in the container by uploading the VHD.</span></span> |
| [<span data-ttu-id="fc380-132">az vm list</span><span class="sxs-lookup"><span data-stu-id="fc380-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="fc380-133">Used with `--query` check whether the VM name is in use.</span><span class="sxs-lookup"><span data-stu-id="fc380-133">Used with `--query` check whether the VM name is in use.</span></span> | 
| [<span data-ttu-id="fc380-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="fc380-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="fc380-135">Creates the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="fc380-135">Creates the virtual machines.</span></span> |
| [<span data-ttu-id="fc380-136">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="fc380-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="fc380-137">Resets the SSH key to give the current user access to the VM.</span><span class="sxs-lookup"><span data-stu-id="fc380-137">Resets the SSH key to give the current user access to the VM.</span></span> |
| [<span data-ttu-id="fc380-138">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="fc380-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="fc380-139">Gets the IP address of the VM that was created.</span><span class="sxs-lookup"><span data-stu-id="fc380-139">Gets the IP address of the VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fc380-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc380-140">Next steps</span></span>

<span data-ttu-id="fc380-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fc380-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fc380-142">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc380-142">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
