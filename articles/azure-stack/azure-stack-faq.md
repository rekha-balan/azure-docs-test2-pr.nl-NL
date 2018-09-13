---
title: Frequently asked questions for Azure Stack | Microsoft Docs
description: Azure Stack frequently asked questions.
services: azure-stack
documentationcenter: ''
author: HeathL17
manager: byronr
editor: ''
ms.assetid: 028479e4-a17e-43c7-885c-cb2130f850d2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/1/2017
ms.author: helaw
ms.openlocfilehash: 7e84323168705b8900521834c42b358eb34d8afa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551434"
---
# <a name="frequently-asked-questions-for-azure-stack"></a><span data-ttu-id="c6345-103">Frequently asked questions for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c6345-103">Frequently asked questions for Azure Stack</span></span>
## <a name="deployment"></a><span data-ttu-id="c6345-104">Deployment</span><span class="sxs-lookup"><span data-stu-id="c6345-104">Deployment</span></span>
### <a name="do-i-need-to-format-my-data-disks-before-starting-or-restarting-an-installation"></a><span data-ttu-id="c6345-105">Do I need to format my data disks before starting or restarting an installation?</span><span class="sxs-lookup"><span data-stu-id="c6345-105">Do I need to format my data disks before starting or restarting an installation?</span></span>
<span data-ttu-id="c6345-106">Disks should be in raw format.</span><span class="sxs-lookup"><span data-stu-id="c6345-106">Disks should be in raw format.</span></span> <span data-ttu-id="c6345-107">If you reinstall the operating system, you may need to check if the old storage pool is still present and delete using the following steps:</span><span class="sxs-lookup"><span data-stu-id="c6345-107">If you reinstall the operating system, you may need to check if the old storage pool is still present and delete using the following steps:</span></span>

1. <span data-ttu-id="c6345-108">Open Server Manager.</span><span class="sxs-lookup"><span data-stu-id="c6345-108">Open Server Manager.</span></span>
2. <span data-ttu-id="c6345-109">Select Storage Pools.</span><span class="sxs-lookup"><span data-stu-id="c6345-109">Select Storage Pools.</span></span>
3. <span data-ttu-id="c6345-110">See if a storage pool is listed.</span><span class="sxs-lookup"><span data-stu-id="c6345-110">See if a storage pool is listed.</span></span>
4. <span data-ttu-id="c6345-111">Right-click **storage pool** if listed and enable read / write.</span><span class="sxs-lookup"><span data-stu-id="c6345-111">Right-click **storage pool** if listed and enable read / write.</span></span>
5. <span data-ttu-id="c6345-112">Right-click **Virtual Hard Disk** (Lower left corner) and select delete.</span><span class="sxs-lookup"><span data-stu-id="c6345-112">Right-click **Virtual Hard Disk** (Lower left corner) and select delete.</span></span>
6. <span data-ttu-id="c6345-113">Right-click **Storage Pool** and click delete.</span><span class="sxs-lookup"><span data-stu-id="c6345-113">Right-click **Storage Pool** and click delete.</span></span>
7. <span data-ttu-id="c6345-114">Launch Azure Stack script again and verify that the disk verification passes.</span><span class="sxs-lookup"><span data-stu-id="c6345-114">Launch Azure Stack script again and verify that the disk verification passes.</span></span>

<span data-ttu-id="c6345-115">Optionally, the following script can be used:</span><span class="sxs-lookup"><span data-stu-id="c6345-115">Optionally, the following script can be used:</span></span>

```PowerShell
$pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
if ($pools -ne $null) {
  $pools| Set-StoragePool -IsReadOnly $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$False
  $pools | Remove-StoragePool -Confirm:$False
}
```

### <a name="can-i-use-all-ssd-disks-for-the-storage-pool-in-the-poc-installation"></a><span data-ttu-id="c6345-116">Can I use all SSD disks for the storage pool in the POC installation?</span><span class="sxs-lookup"><span data-stu-id="c6345-116">Can I use all SSD disks for the storage pool in the POC installation?</span></span>
<span data-ttu-id="c6345-117">For more information on storage configurations, see the [requirements guide](azure-stack-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c6345-117">For more information on storage configurations, see the [requirements guide](azure-stack-deploy.md).</span></span>

### <a name="can-i-use-nvme-data-disks-for-the-microsoft-azure-stack-poc"></a><span data-ttu-id="c6345-118">Can I use NVMe data disks for the Microsoft Azure Stack POC?</span><span class="sxs-lookup"><span data-stu-id="c6345-118">Can I use NVMe data disks for the Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="c6345-119">While Storage Spaces Direct supports NVMe disks, Azure Stack only supports a subset of the possible drive types and combinations possible for Storage Spaces Direct.</span><span class="sxs-lookup"><span data-stu-id="c6345-119">While Storage Spaces Direct supports NVMe disks, Azure Stack only supports a subset of the possible drive types and combinations possible for Storage Spaces Direct.</span></span>  <span data-ttu-id="c6345-120">See the [requirements guide](azure-stack-deploy.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="c6345-120">See the [requirements guide](azure-stack-deploy.md) for more information.</span></span> 

### <a name="how-can-i-reinstall-azure-stack"></a><span data-ttu-id="c6345-121">How can I reinstall Azure Stack?</span><span class="sxs-lookup"><span data-stu-id="c6345-121">How can I reinstall Azure Stack?</span></span>
<span data-ttu-id="c6345-122">You can follow the steps in the [redeployment guide](azure-stack-redeploy.md).</span><span class="sxs-lookup"><span data-stu-id="c6345-122">You can follow the steps in the [redeployment guide](azure-stack-redeploy.md).</span></span>  

## <a name="tenant"></a><span data-ttu-id="c6345-123">Tenant</span><span class="sxs-lookup"><span data-stu-id="c6345-123">Tenant</span></span>
### <a name="can-i-deploy-my-own-images-as-a-tenant"></a><span data-ttu-id="c6345-124">Can I deploy my own images as a tenant?</span><span class="sxs-lookup"><span data-stu-id="c6345-124">Can I deploy my own images as a tenant?</span></span>
<span data-ttu-id="c6345-125">Yes, just like in Azure, a tenant can upload images in Azure Stack, in addition to using the images from the service administrator.</span><span class="sxs-lookup"><span data-stu-id="c6345-125">Yes, just like in Azure, a tenant can upload images in Azure Stack, in addition to using the images from the service administrator.</span></span> <span data-ttu-id="c6345-126">For an overview, see the [Adding a VM Image](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="c6345-126">For an overview, see the [Adding a VM Image](azure-stack-add-vm-image.md).</span></span> 

## <a name="testing"></a><span data-ttu-id="c6345-127">Testing</span><span class="sxs-lookup"><span data-stu-id="c6345-127">Testing</span></span>
### <a name="can-i-use-nested-virtualization-to-test-the-microsoft-azure-stack-poc"></a><span data-ttu-id="c6345-128">Can I use Nested Virtualization to test the Microsoft Azure Stack POC?</span><span class="sxs-lookup"><span data-stu-id="c6345-128">Can I use Nested Virtualization to test the Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="c6345-129">Nested virtualization is not supported or tested with Azure Stack Technical Preview 3.</span><span class="sxs-lookup"><span data-stu-id="c6345-129">Nested virtualization is not supported or tested with Azure Stack Technical Preview 3.</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="c6345-130">Virtual machines</span><span class="sxs-lookup"><span data-stu-id="c6345-130">Virtual machines</span></span>
### <a name="does-azure-stack-support-dynamic-disks-for-virtual-machines"></a><span data-ttu-id="c6345-131">Does Azure Stack support dynamic disks for virtual machines?</span><span class="sxs-lookup"><span data-stu-id="c6345-131">Does Azure Stack support dynamic disks for virtual machines?</span></span>
<span data-ttu-id="c6345-132">Azure Stack does not support dynamic disks.</span><span class="sxs-lookup"><span data-stu-id="c6345-132">Azure Stack does not support dynamic disks.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c6345-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="c6345-133">Next steps</span></span>
[<span data-ttu-id="c6345-134">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="c6345-134">Troubleshooting</span></span>](azure-stack-troubleshooting.md)

