---
title: Create a VM in the Azure portal | Microsoft Docs
description: Create a Windows virtual machine in the Azure portal.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: 6259c2d163cc2036964d119eb0b54ba108c5cd0a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540640"
---
# <a name="create-a-virtual-machine-running-windows-in-the-azure-portal"></a><span data-ttu-id="e5bfd-103">Create a virtual machine running Windows in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e5bfd-103">Create a virtual machine running Windows in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Azure classic portal](tutorial.md)
> * [PowerShell: Classic deployment](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. Learn how to [perform these steps using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using the **Azure portal**.

<span data-ttu-id="e5bfd-110">This tutorial shows you how to create an Azure virtual machine (VM) running Windows in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e5bfd-110">This tutorial shows you how to create an Azure virtual machine (VM) running Windows in the Azure portal.</span></span> <span data-ttu-id="e5bfd-111">We'll use a Windows Server image as an example, but that's just one of the many images Azure offers.</span><span class="sxs-lookup"><span data-stu-id="e5bfd-111">We'll use a Windows Server image as an example, but that's just one of the many images Azure offers.</span></span> <span data-ttu-id="e5bfd-112">Note that your image choices depend on your subscription.</span><span class="sxs-lookup"><span data-stu-id="e5bfd-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="e5bfd-113">For example, Windows desktop images may be available to MSDN subscribers.</span><span class="sxs-lookup"><span data-stu-id="e5bfd-113">For example, Windows desktop images may be available to MSDN subscribers.</span></span>

<span data-ttu-id="e5bfd-114">This section shows you how to use the **Dashboard** in the Azure portal to select and then create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e5bfd-114">This section shows you how to use the **Dashboard** in the Azure portal to select and then create the virtual machine.</span></span>

<span data-ttu-id="e5bfd-115">You can also create VMs using [your own images](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="e5bfd-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="e5bfd-116">To learn about this and other methods, see [Different ways to create a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5bfd-116">To learn about this and other methods, see [Different ways to create a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on the classic portal. -->

## <span data-ttu-id="e5bfd-117"><a id="createvirtualmachine"> </a>Create the virtual machine</span><span class="sxs-lookup"><span data-stu-id="e5bfd-117"><a id="createvirtualmachine"> </a>Create the virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="e5bfd-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5bfd-118">Next steps</span></span>
* <span data-ttu-id="e5bfd-119">Learn how to [create a VM using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e5bfd-119">Learn how to [create a VM using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in the Azure portal.</span></span>
* <span data-ttu-id="e5bfd-120">Log on to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e5bfd-120">Log on to the virtual machine.</span></span> <span data-ttu-id="e5bfd-121">For instructions, see [Log on to a virtual machine running Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="e5bfd-121">For instructions, see [Log on to a virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="e5bfd-122">Attach a disk to store data.</span><span class="sxs-lookup"><span data-stu-id="e5bfd-122">Attach a disk to store data.</span></span> <span data-ttu-id="e5bfd-123">You can attach both empty disks and disks that contain data.</span><span class="sxs-lookup"><span data-stu-id="e5bfd-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="e5bfd-124">For instructions, see the [Attach a data disk to a Windows virtual machine created with the classic deployment model](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="e5bfd-124">For instructions, see the [Attach a data disk to a Windows virtual machine created with the classic deployment model](attach-disk.md).</span></span>
