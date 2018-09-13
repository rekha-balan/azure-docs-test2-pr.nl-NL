---
title: VM restarting or resizing issues | Microsoft Docs
description: Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure
services: virtual-machines-linux
documentationcenter: ''
author: Deland-Han
manager: felixwu
editor: ''
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: c6d4ed45133dc3f4b1f3d17fb5a87d3bf77aa3f7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550969"
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="ce7a3-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span><span class="sxs-lookup"><span data-stu-id="ce7a3-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [Classic](restart-resize-error-troubleshooting.md)
> * [Resource Manager](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="ce7a3-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="ce7a3-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. For the Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="ce7a3-112">Collect audit logs</span><span class="sxs-lookup"><span data-stu-id="ce7a3-112">Collect audit logs</span></span>
<span data-ttu-id="ce7a3-113">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-113">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="ce7a3-114">In the Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-114">In the Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="ce7a3-115">Issue: Error when starting a stopped VM</span><span class="sxs-lookup"><span data-stu-id="ce7a3-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="ce7a3-116">You try to start a stopped VM but get an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-116">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="ce7a3-117">Cause</span><span class="sxs-lookup"><span data-stu-id="ce7a3-117">Cause</span></span>
<span data-ttu-id="ce7a3-118">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-118">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="ce7a3-119">However, the cluster does not have free space available to fulfill the request.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-119">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="ce7a3-120">Resolution</span><span class="sxs-lookup"><span data-stu-id="ce7a3-120">Resolution</span></span>
* <span data-ttu-id="ce7a3-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="ce7a3-122">Delete the stopped VM.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-122">Delete the stopped VM.</span></span>
* <span data-ttu-id="ce7a3-123">Recreate the VM in the new cloud service by using the disks.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-123">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="ce7a3-124">Start the re-created VM.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-124">Start the re-created VM.</span></span>

<span data-ttu-id="ce7a3-125">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-125">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="ce7a3-127">Issue: Error when resizing an existing VM</span><span class="sxs-lookup"><span data-stu-id="ce7a3-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="ce7a3-128">You try to resize an existing VM but get an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-128">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="ce7a3-129">Cause</span><span class="sxs-lookup"><span data-stu-id="ce7a3-129">Cause</span></span>
<span data-ttu-id="ce7a3-130">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-130">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="ce7a3-131">However, the cluster does not support the requested VM size.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-131">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="ce7a3-132">Resolution</span><span class="sxs-lookup"><span data-stu-id="ce7a3-132">Resolution</span></span>
<span data-ttu-id="ce7a3-133">Reduce the requested VM size, and retry the resize request.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-133">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="ce7a3-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="ce7a3-135">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce7a3-135">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="ce7a3-136">If it is not possible to reduce the VM size, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ce7a3-136">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="ce7a3-137">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-137">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="ce7a3-138">Create a new, larger-sized VM in it.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="ce7a3-139">You can consolidate all your VMs in the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-139">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="ce7a3-140">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-140">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="ce7a3-141">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-141">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="ce7a3-142">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span><span class="sxs-lookup"><span data-stu-id="ce7a3-142">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce7a3-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="ce7a3-143">Next steps</span></span>
<span data-ttu-id="ce7a3-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ce7a3-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

