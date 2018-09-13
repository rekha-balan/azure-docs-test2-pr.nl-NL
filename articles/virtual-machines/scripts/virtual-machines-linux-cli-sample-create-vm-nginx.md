---
title: Azure CLI Script Sample - Create a Linux VM with NGINX| Microsoft Docs
description: Azure CLI Script Sample - Create a Linux VM with NGINX
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.openlocfilehash: d8ec8a5a4099a2380549ea4713ef4d54c83b1378
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549910"
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="817c1-103">Create a VM with NGINX</span><span class="sxs-lookup"><span data-stu-id="817c1-103">Create a VM with NGINX</span></span>

<span data-ttu-id="817c1-104">This script creates an Azure Virtual Machine and uses the Azure Virtual Machine Custom Script Extension to install NGINX.</span><span class="sxs-lookup"><span data-stu-id="817c1-104">This script creates an Azure Virtual Machine and uses the Azure Virtual Machine Custom Script Extension to install NGINX.</span></span> <span data-ttu-id="817c1-105">After running the script, you can access a demo website on the public IP address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="817c1-105">After running the script, you can access a demo website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="817c1-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="817c1-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a><span data-ttu-id="817c1-107">Custom Script Extension</span><span class="sxs-lookup"><span data-stu-id="817c1-107">Custom Script Extension</span></span>

<span data-ttu-id="817c1-108">The custom script extension copies this script onto the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="817c1-108">The custom script extension copies this script onto the virtual machine.</span></span> <span data-ttu-id="817c1-109">The script is then run to install and configure an NGINX web server.</span><span class="sxs-lookup"><span data-stu-id="817c1-109">The script is then run to install and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="817c1-110">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="817c1-110">Clean up deployment</span></span> 

<span data-ttu-id="817c1-111">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="817c1-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="817c1-112">Script explanation</span><span class="sxs-lookup"><span data-stu-id="817c1-112">Script explanation</span></span>

<span data-ttu-id="817c1-113">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="817c1-113">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="817c1-114">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="817c1-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="817c1-115">Command</span><span class="sxs-lookup"><span data-stu-id="817c1-115">Command</span></span> | <span data-ttu-id="817c1-116">Notes</span><span class="sxs-lookup"><span data-stu-id="817c1-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="817c1-117">az group create</span><span class="sxs-lookup"><span data-stu-id="817c1-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="817c1-118">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="817c1-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="817c1-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="817c1-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="817c1-120">Creates the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="817c1-120">Creates the virtual machine.</span></span> <span data-ttu-id="817c1-121">This command also specifies the virtual machine image to be used, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="817c1-121">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="817c1-122">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="817c1-122">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="817c1-123">Creates a network security group rule to allow inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="817c1-123">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="817c1-124">In this sample, port 80 is opened for HTTP traffic.</span><span class="sxs-lookup"><span data-stu-id="817c1-124">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="817c1-125">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="817c1-125">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="817c1-126">Adds and runs a virtual machine extension to a VM.</span><span class="sxs-lookup"><span data-stu-id="817c1-126">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="817c1-127">In this sample, the custom script extension is used to install NGINX.</span><span class="sxs-lookup"><span data-stu-id="817c1-127">In this sample, the custom script extension is used to install NGINX.</span></span>|
| [<span data-ttu-id="817c1-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="817c1-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="817c1-129">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="817c1-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="817c1-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="817c1-130">Next steps</span></span>

<span data-ttu-id="817c1-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="817c1-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="817c1-132">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="817c1-132">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
