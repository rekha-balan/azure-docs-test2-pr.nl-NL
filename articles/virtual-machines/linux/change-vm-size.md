---
title: How to resize a Linux VM with the Azure CLI 2.0 | Microsoft Docs
description: How to scale up or scale down a Linux virtual machine, by changing the VM size.
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: ''
tags: ''
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 150f5be63423c1909a5b1608f390203f28b67be5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661142"
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="f8eb4-103">Resize a Linux virtual machine using CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f8eb4-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="f8eb4-104">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="f8eb4-104">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="f8eb4-105">In some cases, you must deallocate the VM first.</span><span class="sxs-lookup"><span data-stu-id="f8eb4-105">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="f8eb4-106">You need to deallocate the VM if the desired size is not available on the hardware cluster that is hosting the VM.</span><span class="sxs-lookup"><span data-stu-id="f8eb4-106">You need to deallocate the VM if the desired size is not available on the hardware cluster that is hosting the VM.</span></span> <span data-ttu-id="f8eb4-107">This article details how to resize a Linux VM with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f8eb4-107">This article details how to resize a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="f8eb4-108">You can also perform these steps with the [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f8eb4-108">You can also perform these steps with the [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f8eb4-109">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="f8eb4-109">CLI versions to complete the task</span></span>
<span data-ttu-id="f8eb4-110">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="f8eb4-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="f8eb4-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="f8eb4-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f8eb4-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="f8eb4-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>



<span data-ttu-id="f8eb4-113">To resize a VM, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f8eb4-113">To resize a VM, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="f8eb4-114">View the list of available VM sizes on the hardware cluster where the VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="f8eb4-114">View the list of available VM sizes on the hardware cluster where the VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="f8eb4-115">The following example lists VM sizes for the VM named `myVM` in the resource group `myResourceGroup` region:</span><span class="sxs-lookup"><span data-stu-id="f8eb4-115">The following example lists VM sizes for the VM named `myVM` in the resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="f8eb4-116">If the desired VM size is listed, resize the VM with [az vm resize](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="f8eb4-116">If the desired VM size is listed, resize the VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="f8eb4-117">The following example resizes the VM named `myVM` to the `Standard_DS3_v2` size:</span><span class="sxs-lookup"><span data-stu-id="f8eb4-117">The following example resizes the VM named `myVM` to the `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="f8eb4-118">The VM restarts during this process.</span><span class="sxs-lookup"><span data-stu-id="f8eb4-118">The VM restarts during this process.</span></span> <span data-ttu-id="f8eb4-119">After the restart, your existing OS and data disks are remapped.</span><span class="sxs-lookup"><span data-stu-id="f8eb4-119">After the restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="f8eb4-120">Anything on the temporary disk is lost.</span><span class="sxs-lookup"><span data-stu-id="f8eb4-120">Anything on the temporary disk is lost.</span></span>

3. <span data-ttu-id="f8eb4-121">If the desired VM size is not listed, you need to first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="f8eb4-121">If the desired VM size is not listed, you need to first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="f8eb4-122">This process allows the VM to then be resized to any size available that the region supports and then started.</span><span class="sxs-lookup"><span data-stu-id="f8eb4-122">This process allows the VM to then be resized to any size available that the region supports and then started.</span></span> <span data-ttu-id="f8eb4-123">The following steps deallocate, resize, and then start the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f8eb4-123">The following steps deallocate, resize, and then start the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="f8eb4-124">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span><span class="sxs-lookup"><span data-stu-id="f8eb4-124">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="f8eb4-125">The OS and data disks are not affected.</span><span class="sxs-lookup"><span data-stu-id="f8eb4-125">The OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8eb4-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="f8eb4-126">Next steps</span></span>
<span data-ttu-id="f8eb4-127">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span><span class="sxs-lookup"><span data-stu-id="f8eb4-127">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
