---
title: VM restarting or resizing issues in Azure | Microsoft Docs
description: Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure
services: virtual-machines-linux, azure-resource-manager
documentationcenter: ''
author: Deland-Han
manager: felixwu
editor: ''
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 173a6968f7a73fd3b675928aa501fbee99ccb8fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549064"
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="686a9-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="686a9-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="686a9-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="686a9-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="686a9-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span><span class="sxs-lookup"><span data-stu-id="686a9-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="686a9-106">Collect activity logs</span><span class="sxs-lookup"><span data-stu-id="686a9-106">Collect activity logs</span></span>
<span data-ttu-id="686a9-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span><span class="sxs-lookup"><span data-stu-id="686a9-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="686a9-108">The following links contain detailed information on the process:</span><span class="sxs-lookup"><span data-stu-id="686a9-108">The following links contain detailed information on the process:</span></span>

[<span data-ttu-id="686a9-109">View deployment operations</span><span class="sxs-lookup"><span data-stu-id="686a9-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="686a9-110">View activity logs to manage Azure resources</span><span class="sxs-lookup"><span data-stu-id="686a9-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="686a9-111">Issue: Error when starting a stopped VM</span><span class="sxs-lookup"><span data-stu-id="686a9-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="686a9-112">You try to start a stopped VM but get an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="686a9-112">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="686a9-113">Cause</span><span class="sxs-lookup"><span data-stu-id="686a9-113">Cause</span></span>
<span data-ttu-id="686a9-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span><span class="sxs-lookup"><span data-stu-id="686a9-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="686a9-115">However, the cluster does not have free space available to fulfill the request.</span><span class="sxs-lookup"><span data-stu-id="686a9-115">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="686a9-116">Resolution</span><span class="sxs-lookup"><span data-stu-id="686a9-116">Resolution</span></span>
* <span data-ttu-id="686a9-117">Stop all the VMs in the availability set, and then restart each VM.</span><span class="sxs-lookup"><span data-stu-id="686a9-117">Stop all the VMs in the availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="686a9-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span><span class="sxs-lookup"><span data-stu-id="686a9-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="686a9-119">After all the VMs stop, select each of the stopped VMs and click Start.</span><span class="sxs-lookup"><span data-stu-id="686a9-119">After all the VMs stop, select each of the stopped VMs and click Start.</span></span>
* <span data-ttu-id="686a9-120">Retry the restart request at a later time.</span><span class="sxs-lookup"><span data-stu-id="686a9-120">Retry the restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="686a9-121">Issue: Error when resizing an existing VM</span><span class="sxs-lookup"><span data-stu-id="686a9-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="686a9-122">You try to resize an existing VM but get an allocation failure.</span><span class="sxs-lookup"><span data-stu-id="686a9-122">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="686a9-123">Cause</span><span class="sxs-lookup"><span data-stu-id="686a9-123">Cause</span></span>
<span data-ttu-id="686a9-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span><span class="sxs-lookup"><span data-stu-id="686a9-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="686a9-125">However, the cluster does not support the requested VM size.</span><span class="sxs-lookup"><span data-stu-id="686a9-125">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="686a9-126">Resolution</span><span class="sxs-lookup"><span data-stu-id="686a9-126">Resolution</span></span>
* <span data-ttu-id="686a9-127">Retry the request using a smaller VM size.</span><span class="sxs-lookup"><span data-stu-id="686a9-127">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="686a9-128">If the size of the requested VM cannot be changed：</span><span class="sxs-lookup"><span data-stu-id="686a9-128">If the size of the requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="686a9-129">Stop all the VMs in the availability set.</span><span class="sxs-lookup"><span data-stu-id="686a9-129">Stop all the VMs in the availability set.</span></span>
     
     * <span data-ttu-id="686a9-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span><span class="sxs-lookup"><span data-stu-id="686a9-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="686a9-131">After all the VMs stop, resize the desired VM to a larger size.</span><span class="sxs-lookup"><span data-stu-id="686a9-131">After all the VMs stop, resize the desired VM to a larger size.</span></span>
  3. <span data-ttu-id="686a9-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span><span class="sxs-lookup"><span data-stu-id="686a9-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="686a9-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="686a9-133">Next steps</span></span>
<span data-ttu-id="686a9-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="686a9-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

