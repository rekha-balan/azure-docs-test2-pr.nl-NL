---
title: Azure CLI Script Sample - Create a Windows Server 2016 VM with IIS using DSC | Microsoft Docs
description: Azure CLI Script Sample - Create a Windows Server 2016 VM with IIS using DSC
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: 150e96244b48f1963b2511f9086364919fa133dd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551862"
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="de313-103">Create a VM with IIS using DSC</span><span class="sxs-lookup"><span data-stu-id="de313-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="de313-104">This script creates a virtual machine, and uses the Azure Virtual Machine DSC custom script extension to install and configure IIS.</span><span class="sxs-lookup"><span data-stu-id="de313-104">This script creates a virtual machine, and uses the Azure Virtual Machine DSC custom script extension to install and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="de313-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="de313-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="de313-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="de313-106">Clean up deployment</span></span> 

<span data-ttu-id="de313-107">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="de313-107">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="de313-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="de313-108">Script explanation</span></span>

<span data-ttu-id="de313-109">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="de313-109">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="de313-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="de313-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="de313-111">Command</span><span class="sxs-lookup"><span data-stu-id="de313-111">Command</span></span> | <span data-ttu-id="de313-112">Notes</span><span class="sxs-lookup"><span data-stu-id="de313-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="de313-113">az group create</span><span class="sxs-lookup"><span data-stu-id="de313-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="de313-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="de313-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="de313-115">az vm create</span><span class="sxs-lookup"><span data-stu-id="de313-115">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="de313-116">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="de313-116">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="de313-117">This command also specifies the virtual machine image to be used, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="de313-117">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="de313-118">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="de313-118">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="de313-119">Add the Custom Script Extension to the virtual machine which invokes a script to install IIS.</span><span class="sxs-lookup"><span data-stu-id="de313-119">Add the Custom Script Extension to the virtual machine which invokes a script to install IIS.</span></span> |
| [<span data-ttu-id="de313-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="de313-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="de313-121">Creates a network security group rule to allow inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="de313-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="de313-122">In this sample, port 80 is opened for HTTP traffic.</span><span class="sxs-lookup"><span data-stu-id="de313-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="de313-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="de313-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="de313-124">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="de313-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="de313-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="de313-125">Next steps</span></span>

<span data-ttu-id="de313-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="de313-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="de313-127">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de313-127">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>