---
title: Troubleshoot Linux VM deployment-RM | Microsoft Docs
description: Troubleshoot Resource Manager deployment issues when you create a new Linux virtual machine in Azure
services: virtual-machines-linux, azure-resource-manager
documentationcenter: ''
author: JiangChen79
manager: felixwu
editor: ''
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 5dac84698c692dd26372a7fe44238a546bbe2e9c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805290"
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="b5ee7-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="b5ee7-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="b5ee7-104">Top issues</span><span class="sxs-lookup"><span data-stu-id="b5ee7-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="b5ee7-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b5ee7-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="b5ee7-106">Collect activity logs</span><span class="sxs-lookup"><span data-stu-id="b5ee7-106">Collect activity logs</span></span>
<span data-ttu-id="b5ee7-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="b5ee7-108">The following links contain detailed information on the process to follow.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-108">The following links contain detailed information on the process to follow.</span></span>

[<span data-ttu-id="b5ee7-109">View deployment operations</span><span class="sxs-lookup"><span data-stu-id="b5ee7-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="b5ee7-110">View activity logs to manage Azure resources</span><span class="sxs-lookup"><span data-stu-id="b5ee7-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="b5ee7-111">**Y:** If the OS is Linux generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-111">**Y:** If the OS is Linux generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="b5ee7-112">Similarly, if the OS is Linux specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-112">Similarly, if the OS is Linux specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="b5ee7-113">**Upload Errors:**</span><span class="sxs-lookup"><span data-stu-id="b5ee7-113">**Upload Errors:**</span></span>

<span data-ttu-id="b5ee7-114">**N<sup>1</sup>:** If the OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because the VM is stuck at the provisioning stage.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-114">**N<sup>1</sup>:** If the OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because the VM is stuck at the provisioning stage.</span></span>

<span data-ttu-id="b5ee7-115">**N<sup>2</sup>:** If the OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-115">**N<sup>2</sup>:** If the OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="b5ee7-116">**Resolution:**</span><span class="sxs-lookup"><span data-stu-id="b5ee7-116">**Resolution:**</span></span>

<span data-ttu-id="b5ee7-117">To resolve both these errors, upload the original VHD, available on-prem, with the same setting as that for the OS (generalized/specialized).</span><span class="sxs-lookup"><span data-stu-id="b5ee7-117">To resolve both these errors, upload the original VHD, available on-prem, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="b5ee7-118">To upload as generalized, remember to run -deprovision first.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-118">To upload as generalized, remember to run -deprovision first.</span></span>

<span data-ttu-id="b5ee7-119">**Capture Errors:**</span><span class="sxs-lookup"><span data-stu-id="b5ee7-119">**Capture Errors:**</span></span>

<span data-ttu-id="b5ee7-120">**N<sup>3</sup>:** If the OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-120">**N<sup>3</sup>:** If the OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="b5ee7-121">**N<sup>4</sup>:** If the OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-121">**N<sup>4</sup>:** If the OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span> <span data-ttu-id="b5ee7-122">Also, the original VM is not usable because it is marked as specialized.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-122">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="b5ee7-123">**Resolution:**</span><span class="sxs-lookup"><span data-stu-id="b5ee7-123">**Resolution:**</span></span>

<span data-ttu-id="b5ee7-124">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span><span class="sxs-lookup"><span data-stu-id="b5ee7-124">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="b5ee7-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span><span class="sxs-lookup"><span data-stu-id="b5ee7-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="b5ee7-126">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-126">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span></span>

<span data-ttu-id="b5ee7-127">**Cause 1:** The cluster cannot support the requested VM size.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-127">**Cause 1:** The cluster cannot support the requested VM size.</span></span>

<span data-ttu-id="b5ee7-128">**Resolution 1:**</span><span class="sxs-lookup"><span data-stu-id="b5ee7-128">**Resolution 1:**</span></span>

* <span data-ttu-id="b5ee7-129">Retry the request using a smaller VM size.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-129">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="b5ee7-130">If the size of the requested VM cannot be changed:</span><span class="sxs-lookup"><span data-stu-id="b5ee7-130">If the size of the requested VM cannot be changed:</span></span>
  * <span data-ttu-id="b5ee7-131">Stop all the VMs in the availability set.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-131">Stop all the VMs in the availability set.</span></span>
    <span data-ttu-id="b5ee7-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="b5ee7-133">After all the VMs stop, create the new VM in the desired size.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-133">After all the VMs stop, create the new VM in the desired size.</span></span>
  * <span data-ttu-id="b5ee7-134">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-134">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span></span>

<span data-ttu-id="b5ee7-135">**Cause 2:** The cluster does not have free resources.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-135">**Cause 2:** The cluster does not have free resources.</span></span>

<span data-ttu-id="b5ee7-136">**Resolution 2:**</span><span class="sxs-lookup"><span data-stu-id="b5ee7-136">**Resolution 2:**</span></span>

* <span data-ttu-id="b5ee7-137">Retry the request at a later time.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-137">Retry the request at a later time.</span></span>
* <span data-ttu-id="b5ee7-138">If the new VM can be part of a different availability set</span><span class="sxs-lookup"><span data-stu-id="b5ee7-138">If the new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="b5ee7-139">Create a new VM in a different availability set (in the same region).</span><span class="sxs-lookup"><span data-stu-id="b5ee7-139">Create a new VM in a different availability set (in the same region).</span></span>
  * <span data-ttu-id="b5ee7-140">Add the new VM to the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="b5ee7-140">Add the new VM to the same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5ee7-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5ee7-141">Next steps</span></span>
<span data-ttu-id="b5ee7-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5ee7-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

