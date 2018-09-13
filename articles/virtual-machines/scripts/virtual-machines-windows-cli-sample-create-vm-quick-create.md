---
title: Azure CLI Script Sample - Quick Create a Windows Server 2016 VM | Microsoft Docs
description: Azure CLI Script Sample - Quick Create a Windows Server 2016 VM
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
ms.author: rickstercdn
ms.openlocfilehash: 639dd54140853a14fc5da38fbf03571c5dfd8afa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551840"
---
# <a name="quick-create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="2fbbf-103">Quick Create a virtual machine with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2fbbf-103">Quick Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="2fbbf-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2fbbf-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="2fbbf-105">After running the script, you can access the virtual machine through a Remote Desktop connection.</span><span class="sxs-lookup"><span data-stu-id="2fbbf-105">After running the script, you can access the virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2fbbf-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="2fbbf-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2fbbf-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="2fbbf-107">Clean up deployment</span></span> 

<span data-ttu-id="2fbbf-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="2fbbf-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="2fbbf-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="2fbbf-109">Script explanation</span></span>

<span data-ttu-id="2fbbf-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="2fbbf-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="2fbbf-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="2fbbf-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2fbbf-112">Command</span><span class="sxs-lookup"><span data-stu-id="2fbbf-112">Command</span></span> | <span data-ttu-id="2fbbf-113">Notes</span><span class="sxs-lookup"><span data-stu-id="2fbbf-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2fbbf-114">az group create</span><span class="sxs-lookup"><span data-stu-id="2fbbf-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2fbbf-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="2fbbf-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2fbbf-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="2fbbf-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2fbbf-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span><span class="sxs-lookup"><span data-stu-id="2fbbf-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="2fbbf-118">This command also specifies the virtual machine image to be used and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="2fbbf-118">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="2fbbf-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="2fbbf-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2fbbf-120">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="2fbbf-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2fbbf-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="2fbbf-121">Next steps</span></span>

<span data-ttu-id="2fbbf-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2fbbf-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2fbbf-123">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2fbbf-123">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
