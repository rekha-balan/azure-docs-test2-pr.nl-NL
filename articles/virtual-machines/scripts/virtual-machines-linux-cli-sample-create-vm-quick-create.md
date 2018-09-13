---
title: Azure CLI Script Sample - Quick Create a Linux VM | Microsoft Docs
description: Azure CLI Script Sample - Quick Create a Linux VM
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
ms.openlocfilehash: 64b4af72a53f0e9d540ee400a30e66457ad6d6f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553943"
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="1d156-103">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="1d156-103">Create a virtual machine</span></span>

<span data-ttu-id="1d156-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span><span class="sxs-lookup"><span data-stu-id="1d156-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="1d156-105">After running the script, you can access the virtual machine over SSH.</span><span class="sxs-lookup"><span data-stu-id="1d156-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1d156-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="1d156-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1d156-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="1d156-107">Clean up deployment</span></span> 

<span data-ttu-id="1d156-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="1d156-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1d156-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="1d156-109">Script explanation</span></span>

<span data-ttu-id="1d156-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="1d156-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="1d156-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="1d156-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1d156-112">Command</span><span class="sxs-lookup"><span data-stu-id="1d156-112">Command</span></span> | <span data-ttu-id="1d156-113">Notes</span><span class="sxs-lookup"><span data-stu-id="1d156-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1d156-114">az group create</span><span class="sxs-lookup"><span data-stu-id="1d156-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1d156-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="1d156-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1d156-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="1d156-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="1d156-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span><span class="sxs-lookup"><span data-stu-id="1d156-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="1d156-118">This command also specifies the virtual machine image to be used and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="1d156-118">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="1d156-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="1d156-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="1d156-120">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="1d156-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1d156-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d156-121">Next steps</span></span>

<span data-ttu-id="1d156-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1d156-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1d156-123">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d156-123">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
