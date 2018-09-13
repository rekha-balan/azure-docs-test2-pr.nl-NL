---
title: Azure CLI Script Sample - Mount operating system disk | Microsoft Docs
description: Azure CLI Script Sample - Mount operating system disk
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
ms.openlocfilehash: 08b561f0c6928945c41473e19dcc08e292d5d41e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550845"
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="ff1bb-103">Troubleshoot a VMs operating system disk</span><span class="sxs-lookup"><span data-stu-id="ff1bb-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="ff1bb-104">This script mounts the operating system disk of a failed or problematic virtual machine as a data disk to a second virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-104">This script mounts the operating system disk of a failed or problematic virtual machine as a data disk to a second virtual machine.</span></span> <span data-ttu-id="ff1bb-105">This can be useful when troubleshooting disk issues or recovering data.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ff1bb-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="ff1bb-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a><span data-ttu-id="ff1bb-107">Script explanation</span><span class="sxs-lookup"><span data-stu-id="ff1bb-107">Script explanation</span></span>

<span data-ttu-id="ff1bb-108">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-108">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="ff1bb-109">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ff1bb-110">Command</span><span class="sxs-lookup"><span data-stu-id="ff1bb-110">Command</span></span> | <span data-ttu-id="ff1bb-111">Notes</span><span class="sxs-lookup"><span data-stu-id="ff1bb-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ff1bb-112">az vm show</span><span class="sxs-lookup"><span data-stu-id="ff1bb-112">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="ff1bb-113">Return a list of virtual machines.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-113">Return a list of virtual machines.</span></span> <span data-ttu-id="ff1bb-114">In this case, the query option is used to return the virtual machine operating system disk.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-114">In this case, the query option is used to return the virtual machine operating system disk.</span></span> <span data-ttu-id="ff1bb-115">This value is then added to a variable name ‘uri’.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-115">This value is then added to a variable name ‘uri’.</span></span> |
| [<span data-ttu-id="ff1bb-116">az vm delete</span><span class="sxs-lookup"><span data-stu-id="ff1bb-116">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="ff1bb-117">Deletes a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-117">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="ff1bb-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="ff1bb-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ff1bb-119">Creates a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-119">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="ff1bb-120">az vm disk attach</span><span class="sxs-lookup"><span data-stu-id="ff1bb-120">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="ff1bb-121">Attaches a disk to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-121">Attaches a disk to a virtual machine.</span></span> |
| [<span data-ttu-id="ff1bb-122">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="ff1bb-122">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="ff1bb-123">Returns the IP addresses of a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ff1bb-123">Returns the IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ff1bb-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff1bb-124">Next steps</span></span>

<span data-ttu-id="ff1bb-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ff1bb-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ff1bb-126">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff1bb-126">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
