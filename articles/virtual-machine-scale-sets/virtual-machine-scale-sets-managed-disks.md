---
title: Using Managed Disks With Azure Virtual Machine Scale Sets | Microsoft Docs
description: Learn why and how to use managed disks with virtual machine scale sets
services: virtual-machine-scale-sets
documentationcenter: ''
author: gatneil
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 2/21/2017
ms.author: negat
ms.openlocfilehash: 4ec20a30f423d4b30e953f873100be90167f987b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662423"
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="6a866-103">Azure VM scale sets and managed disks</span><span class="sxs-lookup"><span data-stu-id="6a866-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="6a866-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with managed disks.</span><span class="sxs-lookup"><span data-stu-id="6a866-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with managed disks.</span></span> <span data-ttu-id="6a866-105">Using managed disks with scale sets has several benefits, including:</span><span class="sxs-lookup"><span data-stu-id="6a866-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="6a866-106">You no longer need to pre-create and manage storage accounts to store the OS disks for the scale set VMs.</span><span class="sxs-lookup"><span data-stu-id="6a866-106">You no longer need to pre-create and manage storage accounts to store the OS disks for the scale set VMs.</span></span>

* <span data-ttu-id="6a866-107">You can attach managed data disks to the scale set.</span><span class="sxs-lookup"><span data-stu-id="6a866-107">You can attach managed data disks to the scale set.</span></span>

* <span data-ttu-id="6a866-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span><span class="sxs-lookup"><span data-stu-id="6a866-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="6a866-109">Get started</span><span class="sxs-lookup"><span data-stu-id="6a866-109">Get started</span></span>

<span data-ttu-id="6a866-110">A simple way to get started with managed disk scale sets is to deploy one from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6a866-110">A simple way to get started with managed disk scale sets is to deploy one from the Azure portal.</span></span> <span data-ttu-id="6a866-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="6a866-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="6a866-112">Another simple way to get started is to use [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) to deploy a scale set.</span><span class="sxs-lookup"><span data-stu-id="6a866-112">Another simple way to get started is to use [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) to deploy a scale set.</span></span> <span data-ttu-id="6a866-113">The following example shows how to create an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span><span class="sxs-lookup"><span data-stu-id="6a866-113">The following example shows how to create an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="6a866-114">Alternatively, you could look in the [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` to see pre-built examples of templates that deploy scale sets.</span><span class="sxs-lookup"><span data-stu-id="6a866-114">Alternatively, you could look in the [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` to see pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="6a866-115">To tell which templates are already using managed disks, you can refer to [this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span><span class="sxs-lookup"><span data-stu-id="6a866-115">To tell which templates are already using managed disks, you can refer to [this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="api-versions"></a><span data-ttu-id="6a866-116">API versions</span><span class="sxs-lookup"><span data-stu-id="6a866-116">API versions</span></span>

<span data-ttu-id="6a866-117">The current Generally Available API version for scale sets with managed disks is `2016-04-30-preview`.</span><span class="sxs-lookup"><span data-stu-id="6a866-117">The current Generally Available API version for scale sets with managed disks is `2016-04-30-preview`.</span></span> <span data-ttu-id="6a866-118">Scale sets with unmanaged disks will continue to work as they currently do, even in new API versions that have support for managed disk.</span><span class="sxs-lookup"><span data-stu-id="6a866-118">Scale sets with unmanaged disks will continue to work as they currently do, even in new API versions that have support for managed disk.</span></span> <span data-ttu-id="6a866-119">However, scale sets with unmanaged disks will not get the benefits of managed disks, even in these new api versions.</span><span class="sxs-lookup"><span data-stu-id="6a866-119">However, scale sets with unmanaged disks will not get the benefits of managed disks, even in these new api versions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a866-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a866-120">Next steps</span></span>

<span data-ttu-id="6a866-121">To find more information on managed disks in general, see [this article](../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6a866-121">To find more information on managed disks in general, see [this article](../storage/storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="6a866-122">To see how to convert a Resource Manager template to provision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span><span class="sxs-lookup"><span data-stu-id="6a866-122">To see how to convert a Resource Manager template to provision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="6a866-123">The same modifications to the Resource Manager templates apply to the Azure REST API as well.</span><span class="sxs-lookup"><span data-stu-id="6a866-123">The same modifications to the Resource Manager templates apply to the Azure REST API as well.</span></span>

<span data-ttu-id="6a866-124">To learn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="6a866-124">To learn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="6a866-125">To begin working with large scale sets, refer to [this article](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="6a866-125">To begin working with large scale sets, refer to [this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


