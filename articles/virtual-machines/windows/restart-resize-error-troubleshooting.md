---
title: VM restarting or resizing issues in Azure | Microsoft Docs
description: Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: ''
author: Deland-Han
manager: felixwu
editor: ''
tags: top-support-issue
ms.assetid: 0756b52d-4f5a-4503-ae45-c00a6a2edcdf
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b648b000e82b540c611658f369b15d6fe7f52121
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564059"
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-windows-vm-in-azure"></a><span data-ttu-id="53fde-103">Troubleshoot deployment issues with restarting or resizing an existing Windows VM in Azure</span><span class="sxs-lookup"><span data-stu-id="53fde-103">Troubleshoot deployment issues with restarting or resizing an existing Windows VM in Azure</span></span>
<span data-ttu-id="53fde-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="53fde-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="53fde-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span><span class="sxs-lookup"><span data-stu-id="53fde-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="53fde-106">Collect activity logs</span><span class="sxs-lookup"><span data-stu-id="53fde-106">Collect activity logs</span></span>
<span data-ttu-id="53fde-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span><span class="sxs-lookup"><span data-stu-id="53fde-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="53fde-108">The following links contain detailed information on the process:</span><span class="sxs-lookup"><span data-stu-id="53fde-108">The following links contain detailed information on the process:</span></span>

[<span data-ttu-id="53fde-109">View deployment operations</span><span class="sxs-lookup"><span data-stu-id="53fde-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="53fde-110">View activity logs to manage Azure resources</span><span class="sxs-lookup"><span data-stu-id="53fde-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="53fde-111">Issue: Error when starting a stopped VM</span><span class="sxs-lookup"><span data-stu-id="53fde-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="53fde-112">You try to start a stopped VM but get an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="53fde-112">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="53fde-113">Cause</span><span class="sxs-lookup"><span data-stu-id="53fde-113">Cause</span></span>
<span data-ttu-id="53fde-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span><span class="sxs-lookup"><span data-stu-id="53fde-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="53fde-115">However, the cluster does not have free space available to fulfill the request.</span><span class="sxs-lookup"><span data-stu-id="53fde-115">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="53fde-116">Resolution</span><span class="sxs-lookup"><span data-stu-id="53fde-116">Resolution</span></span>
* <span data-ttu-id="53fde-117">Stop all the VMs in the availability set, and then restart each VM.</span><span class="sxs-lookup"><span data-stu-id="53fde-117">Stop all the VMs in the availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="53fde-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span><span class="sxs-lookup"><span data-stu-id="53fde-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="53fde-119">After all the VMs stop, select each of the stopped VMs and click Start.</span><span class="sxs-lookup"><span data-stu-id="53fde-119">After all the VMs stop, select each of the stopped VMs and click Start.</span></span>
* <span data-ttu-id="53fde-120">Retry the restart request at a later time.</span><span class="sxs-lookup"><span data-stu-id="53fde-120">Retry the restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="53fde-121">Issue: Error when resizing an existing VM</span><span class="sxs-lookup"><span data-stu-id="53fde-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="53fde-122">You try to resize an existing VM but get an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="53fde-122">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="53fde-123">Cause</span><span class="sxs-lookup"><span data-stu-id="53fde-123">Cause</span></span>
<span data-ttu-id="53fde-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span><span class="sxs-lookup"><span data-stu-id="53fde-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="53fde-125">However, the cluster does not support the requested VM size.</span><span class="sxs-lookup"><span data-stu-id="53fde-125">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="53fde-126">Resolution</span><span class="sxs-lookup"><span data-stu-id="53fde-126">Resolution</span></span>
* <span data-ttu-id="53fde-127">Retry the request using a smaller VM size.</span><span class="sxs-lookup"><span data-stu-id="53fde-127">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="53fde-128">If the size of the requested VM cannot be changed：</span><span class="sxs-lookup"><span data-stu-id="53fde-128">If the size of the requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="53fde-129">Stop all the VMs in the availability set.</span><span class="sxs-lookup"><span data-stu-id="53fde-129">Stop all the VMs in the availability set.</span></span>
     
     * <span data-ttu-id="53fde-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span><span class="sxs-lookup"><span data-stu-id="53fde-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="53fde-131">After all the VMs stop, resize the desired VM to a larger size.</span><span class="sxs-lookup"><span data-stu-id="53fde-131">After all the VMs stop, resize the desired VM to a larger size.</span></span>
  3. <span data-ttu-id="53fde-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span><span class="sxs-lookup"><span data-stu-id="53fde-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53fde-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="53fde-133">Next steps</span></span>
<span data-ttu-id="53fde-134">If you encounter issues when you create a new Windows VM in Azure, see [Troubleshoot deployment issues with creating a new Windows virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="53fde-134">If you encounter issues when you create a new Windows VM in Azure, see [Troubleshoot deployment issues with creating a new Windows virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

