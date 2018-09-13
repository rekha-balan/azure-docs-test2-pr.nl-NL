---
title: Azure CLI Script Sample - Install IIS | Microsoft Docs
description: Azure CLI Script Sample - Install IIS
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 37a37b690ae14b35915e5e5b8f5a68b1f9d0b68c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555758"
---
# <a name="quick-create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="a011b-103">Quick Create a virtual machine with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a011b-103">Quick Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="a011b-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses the Azure Virtual Machine Custom Script Extension to install IIS.</span><span class="sxs-lookup"><span data-stu-id="a011b-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses the Azure Virtual Machine Custom Script Extension to install IIS.</span></span> <span data-ttu-id="a011b-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a011b-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a011b-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="a011b-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a011b-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="a011b-107">Clean up deployment</span></span> 

<span data-ttu-id="a011b-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="a011b-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="a011b-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="a011b-109">Script explanation</span></span>

<span data-ttu-id="a011b-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="a011b-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="a011b-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="a011b-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a011b-112">Command</span><span class="sxs-lookup"><span data-stu-id="a011b-112">Command</span></span> | <span data-ttu-id="a011b-113">Notes</span><span class="sxs-lookup"><span data-stu-id="a011b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a011b-114">az group create</span><span class="sxs-lookup"><span data-stu-id="a011b-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a011b-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="a011b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a011b-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="a011b-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="a011b-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span><span class="sxs-lookup"><span data-stu-id="a011b-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="a011b-118">This command also specifies the virtual machine image to be used and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="a011b-118">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="a011b-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="a011b-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="a011b-120">Creates a network security group rule to allow inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="a011b-120">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="a011b-121">In this sample, port 80 is opened for HTTP traffic.</span><span class="sxs-lookup"><span data-stu-id="a011b-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="a011b-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="a011b-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a011b-123">Adds and runs a virtual machine extension to a VM.</span><span class="sxs-lookup"><span data-stu-id="a011b-123">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="a011b-124">In this sample, the custom script extension is used to install IIS.</span><span class="sxs-lookup"><span data-stu-id="a011b-124">In this sample, the custom script extension is used to install IIS.</span></span>|
| [<span data-ttu-id="a011b-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="a011b-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a011b-126">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="a011b-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a011b-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="a011b-127">Next steps</span></span>

<span data-ttu-id="a011b-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a011b-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a011b-129">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a011b-129">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
