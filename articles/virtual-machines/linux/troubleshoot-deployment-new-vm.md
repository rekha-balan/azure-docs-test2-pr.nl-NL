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
ms.openlocfilehash: 3eda14a83fbc1edeec6d588968e46267b6abc1e5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554364"
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="15230-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="15230-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="15230-104">Collect activity logs</span><span class="sxs-lookup"><span data-stu-id="15230-104">Collect activity logs</span></span>
<span data-ttu-id="15230-105">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span><span class="sxs-lookup"><span data-stu-id="15230-105">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="15230-106">The following links contain detailed information on the process to follow.</span><span class="sxs-lookup"><span data-stu-id="15230-106">The following links contain detailed information on the process to follow.</span></span>

[<span data-ttu-id="15230-107">View deployment operations</span><span class="sxs-lookup"><span data-stu-id="15230-107">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="15230-108">View activity logs to manage Azure resources</span><span class="sxs-lookup"><span data-stu-id="15230-108">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="15230-109">**Y:** If the OS is Linux generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span><span class="sxs-lookup"><span data-stu-id="15230-109">**Y:** If the OS is Linux generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="15230-110">Similarly, if the OS is Linux specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span><span class="sxs-lookup"><span data-stu-id="15230-110">Similarly, if the OS is Linux specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="15230-111">**Upload Errors:**</span><span class="sxs-lookup"><span data-stu-id="15230-111">**Upload Errors:**</span></span>

<span data-ttu-id="15230-112">**N<sup>1</sup>:** If the OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because the VM is stuck at the provisioning stage.</span><span class="sxs-lookup"><span data-stu-id="15230-112">**N<sup>1</sup>:** If the OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because the VM is stuck at the provisioning stage.</span></span>

<span data-ttu-id="15230-113">**N<sup>2</sup>:** If the OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span><span class="sxs-lookup"><span data-stu-id="15230-113">**N<sup>2</sup>:** If the OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="15230-114">**Resolution:**</span><span class="sxs-lookup"><span data-stu-id="15230-114">**Resolution:**</span></span>

<span data-ttu-id="15230-115">To resolve both these errors, upload the original VHD, available on-prem, with the same setting as that for the OS (generalized/specialized).</span><span class="sxs-lookup"><span data-stu-id="15230-115">To resolve both these errors, upload the original VHD, available on-prem, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="15230-116">To upload as generalized, remember to run -deprovision first.</span><span class="sxs-lookup"><span data-stu-id="15230-116">To upload as generalized, remember to run -deprovision first.</span></span>

<span data-ttu-id="15230-117">**Capture Errors:**</span><span class="sxs-lookup"><span data-stu-id="15230-117">**Capture Errors:**</span></span>

<span data-ttu-id="15230-118">**N<sup>3</sup>:** If the OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span><span class="sxs-lookup"><span data-stu-id="15230-118">**N<sup>3</sup>:** If the OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="15230-119">**N<sup>4</sup>:** If the OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span><span class="sxs-lookup"><span data-stu-id="15230-119">**N<sup>4</sup>:** If the OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span> <span data-ttu-id="15230-120">Also, the original VM is not usable because it is marked as specialized.</span><span class="sxs-lookup"><span data-stu-id="15230-120">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="15230-121">**Resolution:**</span><span class="sxs-lookup"><span data-stu-id="15230-121">**Resolution:**</span></span>

<span data-ttu-id="15230-122">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span><span class="sxs-lookup"><span data-stu-id="15230-122">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="15230-123">Issue: Custom/ gallery/ marketplace image; allocation failure</span><span class="sxs-lookup"><span data-stu-id="15230-123">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="15230-124">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span><span class="sxs-lookup"><span data-stu-id="15230-124">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span></span>

<span data-ttu-id="15230-125">**Cause 1:** The cluster cannot support the requested VM size.</span><span class="sxs-lookup"><span data-stu-id="15230-125">**Cause 1:** The cluster cannot support the requested VM size.</span></span>

<span data-ttu-id="15230-126">**Resolution 1:**</span><span class="sxs-lookup"><span data-stu-id="15230-126">**Resolution 1:**</span></span>

* <span data-ttu-id="15230-127">Retry the request using a smaller VM size.</span><span class="sxs-lookup"><span data-stu-id="15230-127">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="15230-128">If the size of the requested VM cannot be changed:</span><span class="sxs-lookup"><span data-stu-id="15230-128">If the size of the requested VM cannot be changed:</span></span>
  * <span data-ttu-id="15230-129">Stop all the VMs in the availability set.</span><span class="sxs-lookup"><span data-stu-id="15230-129">Stop all the VMs in the availability set.</span></span>
    <span data-ttu-id="15230-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span><span class="sxs-lookup"><span data-stu-id="15230-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="15230-131">After all the VMs stop, create the new VM in the desired size.</span><span class="sxs-lookup"><span data-stu-id="15230-131">After all the VMs stop, create the new VM in the desired size.</span></span>
  * <span data-ttu-id="15230-132">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span><span class="sxs-lookup"><span data-stu-id="15230-132">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span></span>

<span data-ttu-id="15230-133">**Cause 2:** The cluster does not have free resources.</span><span class="sxs-lookup"><span data-stu-id="15230-133">**Cause 2:** The cluster does not have free resources.</span></span>

<span data-ttu-id="15230-134">**Resolution 2:**</span><span class="sxs-lookup"><span data-stu-id="15230-134">**Resolution 2:**</span></span>

* <span data-ttu-id="15230-135">Retry the request at a later time.</span><span class="sxs-lookup"><span data-stu-id="15230-135">Retry the request at a later time.</span></span>
* <span data-ttu-id="15230-136">If the new VM can be part of a different availability set</span><span class="sxs-lookup"><span data-stu-id="15230-136">If the new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="15230-137">Create a new VM in a different availability set (in the same region).</span><span class="sxs-lookup"><span data-stu-id="15230-137">Create a new VM in a different availability set (in the same region).</span></span>
  * <span data-ttu-id="15230-138">Add the new VM to the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="15230-138">Add the new VM to the same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15230-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="15230-139">Next steps</span></span>
<span data-ttu-id="15230-140">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="15230-140">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

