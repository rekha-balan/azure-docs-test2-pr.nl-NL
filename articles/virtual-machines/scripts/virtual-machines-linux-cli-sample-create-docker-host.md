---
title: Azure CLI Script Sample - Create a Docker host| Microsoft Docs
description: Azure CLI Script Sample - Create a Docker host
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
ms.date: 03/15/2017
ms.author: nepeters
ms.openlocfilehash: c5ab1468015ca860f148291fa6a80910faa442bc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555007"
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="72dae-103">Create a VM with Docker</span><span class="sxs-lookup"><span data-stu-id="72dae-103">Create a VM with Docker</span></span>

<span data-ttu-id="72dae-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span><span class="sxs-lookup"><span data-stu-id="72dae-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="72dae-105">After running the script, you can access the NGINX web server through the FQDN of the Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="72dae-105">After running the script, you can access the NGINX web server through the FQDN of the Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="72dae-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="72dae-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="72dae-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="72dae-107">Clean up deployment</span></span> 

<span data-ttu-id="72dae-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="72dae-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="72dae-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="72dae-109">Script explanation</span></span>

<span data-ttu-id="72dae-110">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="72dae-110">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="72dae-111">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="72dae-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="72dae-112">Command</span><span class="sxs-lookup"><span data-stu-id="72dae-112">Command</span></span> | <span data-ttu-id="72dae-113">Notes</span><span class="sxs-lookup"><span data-stu-id="72dae-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="72dae-114">az group create</span><span class="sxs-lookup"><span data-stu-id="72dae-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="72dae-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="72dae-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="72dae-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="72dae-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="72dae-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span><span class="sxs-lookup"><span data-stu-id="72dae-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="72dae-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="72dae-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="72dae-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="72dae-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="72dae-120">Creates a network security group rule to allow inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="72dae-120">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="72dae-121">In this sample, port 80 is opened for HTTP traffic.</span><span class="sxs-lookup"><span data-stu-id="72dae-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="72dae-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="72dae-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="72dae-123">Adds and runs a virtual machine extension to a VM.</span><span class="sxs-lookup"><span data-stu-id="72dae-123">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="72dae-124">In this sample, the Docker VM extension is used to configure a Docker host.</span><span class="sxs-lookup"><span data-stu-id="72dae-124">In this sample, the Docker VM extension is used to configure a Docker host.</span></span>|
| [<span data-ttu-id="72dae-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="72dae-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="72dae-126">Deletes a resource group, including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="72dae-126">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="72dae-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="72dae-127">Next steps</span></span>

<span data-ttu-id="72dae-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="72dae-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="72dae-129">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72dae-129">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
