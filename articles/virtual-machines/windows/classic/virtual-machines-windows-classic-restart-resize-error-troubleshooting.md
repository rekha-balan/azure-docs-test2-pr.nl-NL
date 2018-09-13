---
title: VM restarting or resizing issues | Microsoft Docs
description: Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure
services: virtual-machines-windows
documentationcenter: ''
author: Deland-Han
manager: felixwu
editor: ''
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 95b12674f3e7d3d63421be6098c72d87cab562b6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540784"
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="631c3-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span><span class="sxs-lookup"><span data-stu-id="631c3-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [Classic](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [Resource Manager](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="631c3-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="631c3-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="631c3-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span><span class="sxs-lookup"><span data-stu-id="631c3-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).  This article covers using the classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model.
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="631c3-111">Collect audit logs</span><span class="sxs-lookup"><span data-stu-id="631c3-111">Collect audit logs</span></span>
<span data-ttu-id="631c3-112">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span><span class="sxs-lookup"><span data-stu-id="631c3-112">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="631c3-113">In the Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span><span class="sxs-lookup"><span data-stu-id="631c3-113">In the Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="631c3-114">Issue: Error when starting a stopped VM</span><span class="sxs-lookup"><span data-stu-id="631c3-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="631c3-115">You try to start a stopped VM but get an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="631c3-115">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="631c3-116">Cause</span><span class="sxs-lookup"><span data-stu-id="631c3-116">Cause</span></span>
<span data-ttu-id="631c3-117">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span><span class="sxs-lookup"><span data-stu-id="631c3-117">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="631c3-118">However, the cluster does not have free space available to fulfill the request.</span><span class="sxs-lookup"><span data-stu-id="631c3-118">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="631c3-119">Resolution</span><span class="sxs-lookup"><span data-stu-id="631c3-119">Resolution</span></span>
* <span data-ttu-id="631c3-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span><span class="sxs-lookup"><span data-stu-id="631c3-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="631c3-121">Delete the stopped VM.</span><span class="sxs-lookup"><span data-stu-id="631c3-121">Delete the stopped VM.</span></span>
* <span data-ttu-id="631c3-122">Recreate the VM in the new cloud service by using the disks.</span><span class="sxs-lookup"><span data-stu-id="631c3-122">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="631c3-123">Start the re-created VM.</span><span class="sxs-lookup"><span data-stu-id="631c3-123">Start the re-created VM.</span></span>

<span data-ttu-id="631c3-124">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="631c3-124">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="631c3-126">Issue: Error when resizing an existing VM</span><span class="sxs-lookup"><span data-stu-id="631c3-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="631c3-127">You try to resize an existing VM but get an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="631c3-127">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="631c3-128">Cause</span><span class="sxs-lookup"><span data-stu-id="631c3-128">Cause</span></span>
<span data-ttu-id="631c3-129">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span><span class="sxs-lookup"><span data-stu-id="631c3-129">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="631c3-130">However, the cluster does not support the requested VM size.</span><span class="sxs-lookup"><span data-stu-id="631c3-130">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="631c3-131">Resolution</span><span class="sxs-lookup"><span data-stu-id="631c3-131">Resolution</span></span>
<span data-ttu-id="631c3-132">Reduce the requested VM size, and retry the resize request.</span><span class="sxs-lookup"><span data-stu-id="631c3-132">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="631c3-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span><span class="sxs-lookup"><span data-stu-id="631c3-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="631c3-134">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="631c3-134">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="631c3-135">If it is not possible to reduce the VM size, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="631c3-135">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="631c3-136">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span><span class="sxs-lookup"><span data-stu-id="631c3-136">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="631c3-137">Create a new, larger-sized VM in it.</span><span class="sxs-lookup"><span data-stu-id="631c3-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="631c3-138">You can consolidate all your VMs in the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="631c3-138">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="631c3-139">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span><span class="sxs-lookup"><span data-stu-id="631c3-139">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="631c3-140">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span><span class="sxs-lookup"><span data-stu-id="631c3-140">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="631c3-141">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span><span class="sxs-lookup"><span data-stu-id="631c3-141">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="631c3-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="631c3-142">Next steps</span></span>
<span data-ttu-id="631c3-143">If you encounter issues when you create a new Windows VM in Azure, see [Troubleshoot deployment issues with creating a new Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="631c3-143">If you encounter issues when you create a new Windows VM in Azure, see [Troubleshoot deployment issues with creating a new Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

