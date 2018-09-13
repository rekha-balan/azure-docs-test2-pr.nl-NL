---
title: Azure CLI Script Sample - Create a Linux VM with WordPress | Microsoft Docs
description: Azure CLI Script Sample - Create a Linux VM with WordPress
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
ms.openlocfilehash: 8026aee6a52cb34abf7ddf925f6665630c893e20
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554865"
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="7a9f8-103">Create a VM with WordPress</span><span class="sxs-lookup"><span data-stu-id="7a9f8-103">Create a VM with WordPress</span></span>

<span data-ttu-id="7a9f8-104">This script creates a virtual machine, and then uses the Azure Virtual Machine custom script extension to install WordPress.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-104">This script creates a virtual machine, and then uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="7a9f8-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7a9f8-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="7a9f8-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7a9f8-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="7a9f8-107">Clean up deployment</span></span> 

<span data-ttu-id="7a9f8-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7a9f8-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="7a9f8-109">Script explanation</span></span>

<span data-ttu-id="7a9f8-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="7a9f8-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7a9f8-112">Command</span><span class="sxs-lookup"><span data-stu-id="7a9f8-112">Command</span></span> | <span data-ttu-id="7a9f8-113">Notes</span><span class="sxs-lookup"><span data-stu-id="7a9f8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7a9f8-114">az group create</span><span class="sxs-lookup"><span data-stu-id="7a9f8-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7a9f8-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7a9f8-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="7a9f8-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="7a9f8-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="7a9f8-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="7a9f8-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="7a9f8-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="7a9f8-120">Creates a network security group rule to allow inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-120">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="7a9f8-121">In this sample, port 80 is opened for HTTP traffic.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="7a9f8-122">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="7a9f8-122">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="7a9f8-123">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-123">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
| [<span data-ttu-id="7a9f8-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="7a9f8-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="7a9f8-125">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="7a9f8-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7a9f8-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a9f8-126">Next steps</span></span>

<span data-ttu-id="7a9f8-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7a9f8-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7a9f8-128">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a9f8-128">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
