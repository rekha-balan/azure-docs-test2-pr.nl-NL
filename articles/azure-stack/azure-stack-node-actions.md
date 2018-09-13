---
title: Scale unit node actions in Azure Stack | Microsoft Docs
description: Learn how to view node status, and use the power on, power off, drain, and resume node actions on an Azure Stack integrated system.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2018
ms.author: mabrigg
ms.reviewer: ppacent
ms.openlocfilehash: 1f59f2ce6e3bf8d34ce225aa93da76ad523775e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969098"
---
# <a name="scale-unit-node-actions-in-azure-stack"></a><span data-ttu-id="fb5c1-103">Scale unit node actions in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fb5c1-103">Scale unit node actions in Azure Stack</span></span>

<span data-ttu-id="fb5c1-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="fb5c1-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="fb5c1-105">This article describes how to view the status of a scale unit and its associated nodes, and how to use the available node actions.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-105">This article describes how to view the status of a scale unit and its associated nodes, and how to use the available node actions.</span></span> <span data-ttu-id="fb5c1-106">Node actions include power on, power off, drain, resume, and repair.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-106">Node actions include power on, power off, drain, resume, and repair.</span></span> <span data-ttu-id="fb5c1-107">Typically, you use these node actions during field replacement of parts, or for node recovery scenarios.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-107">Typically, you use these node actions during field replacement of parts, or for node recovery scenarios.</span></span>

> [!Important]  
> <span data-ttu-id="fb5c1-108">All node actions described in this article should only target one node at a time.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-108">All node actions described in this article should only target one node at a time.</span></span>


## <a name="view-the-status-of-a-scale-unit-and-its-nodes"></a><span data-ttu-id="fb5c1-109">View the status of a scale unit and its nodes</span><span class="sxs-lookup"><span data-stu-id="fb5c1-109">View the status of a scale unit and its nodes</span></span>

<span data-ttu-id="fb5c1-110">In the administrator portal, you can easily view the status of a scale unit and its associated nodes.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-110">In the administrator portal, you can easily view the status of a scale unit and its associated nodes.</span></span>

<span data-ttu-id="fb5c1-111">To view the status of a scale unit:</span><span class="sxs-lookup"><span data-stu-id="fb5c1-111">To view the status of a scale unit:</span></span>

1. <span data-ttu-id="fb5c1-112">On the **Region management** tile, select the region.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-112">On the **Region management** tile, select the region.</span></span>
2. <span data-ttu-id="fb5c1-113">On the left, under **Infrastructure resources**, select **Scale units**.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-113">On the left, under **Infrastructure resources**, select **Scale units**.</span></span>
3. <span data-ttu-id="fb5c1-114">In the results, select the scale unit.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-114">In the results, select the scale unit.</span></span>
 
<span data-ttu-id="fb5c1-115">Here, you can view the following information:</span><span class="sxs-lookup"><span data-stu-id="fb5c1-115">Here, you can view the following information:</span></span>

- <span data-ttu-id="fb5c1-116">region name.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-116">region name.</span></span> <span data-ttu-id="fb5c1-117">The region name is referenced with **-Location** in the PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-117">The region name is referenced with **-Location** in the PowerShell module.</span></span>
- <span data-ttu-id="fb5c1-118">type of system</span><span class="sxs-lookup"><span data-stu-id="fb5c1-118">type of system</span></span>
- <span data-ttu-id="fb5c1-119">total logical cores</span><span class="sxs-lookup"><span data-stu-id="fb5c1-119">total logical cores</span></span>
- <span data-ttu-id="fb5c1-120">total memory</span><span class="sxs-lookup"><span data-stu-id="fb5c1-120">total memory</span></span>
- <span data-ttu-id="fb5c1-121">the list of individual nodes and their status; either **Running** or **Stopped**.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-121">the list of individual nodes and their status; either **Running** or **Stopped**.</span></span>

![Scale unit tile showing Running status for each node](media/azure-stack-node-actions/ScaleUnitStatus.PNG)

## <a name="view-information-about-a-scale-unit-node"></a><span data-ttu-id="fb5c1-123">View information about a scale unit node</span><span class="sxs-lookup"><span data-stu-id="fb5c1-123">View information about a scale unit node</span></span>

<span data-ttu-id="fb5c1-124">If you select an individual node, you can view the following information:</span><span class="sxs-lookup"><span data-stu-id="fb5c1-124">If you select an individual node, you can view the following information:</span></span>

- <span data-ttu-id="fb5c1-125">region name</span><span class="sxs-lookup"><span data-stu-id="fb5c1-125">region name</span></span>
- <span data-ttu-id="fb5c1-126">server model</span><span class="sxs-lookup"><span data-stu-id="fb5c1-126">server model</span></span>
- <span data-ttu-id="fb5c1-127">IP address of the baseboard management controller (BMC)</span><span class="sxs-lookup"><span data-stu-id="fb5c1-127">IP address of the baseboard management controller (BMC)</span></span>
- <span data-ttu-id="fb5c1-128">operational state</span><span class="sxs-lookup"><span data-stu-id="fb5c1-128">operational state</span></span>
- <span data-ttu-id="fb5c1-129">total number of cores</span><span class="sxs-lookup"><span data-stu-id="fb5c1-129">total number of cores</span></span>
- <span data-ttu-id="fb5c1-130">total amount of memory</span><span class="sxs-lookup"><span data-stu-id="fb5c1-130">total amount of memory</span></span>
 
![Scale unit tile showing Running status for each node](media/azure-stack-node-actions/NodeActions.PNG)

<span data-ttu-id="fb5c1-132">You can also perform scale unit node actions from here.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-132">You can also perform scale unit node actions from here.</span></span>

## <a name="scale-unit-node-actions"></a><span data-ttu-id="fb5c1-133">Scale unit node actions</span><span class="sxs-lookup"><span data-stu-id="fb5c1-133">Scale unit node actions</span></span>

<span data-ttu-id="fb5c1-134">When you view information about a scale unit node, you can also perform node actions such as:</span><span class="sxs-lookup"><span data-stu-id="fb5c1-134">When you view information about a scale unit node, you can also perform node actions such as:</span></span>

- <span data-ttu-id="fb5c1-135">Drain and resume</span><span class="sxs-lookup"><span data-stu-id="fb5c1-135">Drain and resume</span></span>
- <span data-ttu-id="fb5c1-136">Repair</span><span class="sxs-lookup"><span data-stu-id="fb5c1-136">Repair</span></span>

<span data-ttu-id="fb5c1-137">The operational state of the node determines which options are available.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-137">The operational state of the node determines which options are available.</span></span>

### <a name="power-off"></a><span data-ttu-id="fb5c1-138">Power off</span><span class="sxs-lookup"><span data-stu-id="fb5c1-138">Power off</span></span>

<span data-ttu-id="fb5c1-139">The **Power off** action turns off the node.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-139">The **Power off** action turns off the node.</span></span> <span data-ttu-id="fb5c1-140">It’s the same as if you press the power button.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-140">It’s the same as if you press the power button.</span></span> <span data-ttu-id="fb5c1-141">It does **not** send a shutdown signal to the operating system.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-141">It does **not** send a shutdown signal to the operating system.</span></span> <span data-ttu-id="fb5c1-142">For planned power off operations, make sure you drain a scale unit node first.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-142">For planned power off operations, make sure you drain a scale unit node first.</span></span>

<span data-ttu-id="fb5c1-143">This action is typically used when a node is in a hung state and no longer responds to requests.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-143">This action is typically used when a node is in a hung state and no longer responds to requests.</span></span>

> [!Important] 
> <span data-ttu-id="fb5c1-144">This functionality is only available via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-144">This functionality is only available via PowerShell.</span></span> <span data-ttu-id="fb5c1-145">It will be available in the Azure Stack administrator portal again at a later time.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-145">It will be available in the Azure Stack administrator portal again at a later time.</span></span>


<span data-ttu-id="fb5c1-146">To run the power off action through PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fb5c1-146">To run the power off action through PowerShell:</span></span>

````PowerShell
  Stop-AzsScaleUnitNode -Location <RegionName> -Name <NodeName>
```` 

<span data-ttu-id="fb5c1-147">In the unlikely case that the power off action doesn't work, use the BMC web interface instead.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-147">In the unlikely case that the power off action doesn't work, use the BMC web interface instead.</span></span>

### <a name="power-on"></a><span data-ttu-id="fb5c1-148">Power on</span><span class="sxs-lookup"><span data-stu-id="fb5c1-148">Power on</span></span>

<span data-ttu-id="fb5c1-149">The **Power on** action turns on the node.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-149">The **Power on** action turns on the node.</span></span> <span data-ttu-id="fb5c1-150">It’s the same as if you press the power button.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-150">It’s the same as if you press the power button.</span></span> 

> [!Important] 
> <span data-ttu-id="fb5c1-151">This functionality is only available via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-151">This functionality is only available via PowerShell.</span></span> <span data-ttu-id="fb5c1-152">It will be available in the Azure Stack administrator portal again at a later time.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-152">It will be available in the Azure Stack administrator portal again at a later time.</span></span>

<span data-ttu-id="fb5c1-153">To run the power on action through PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fb5c1-153">To run the power on action through PowerShell:</span></span>

````PowerShell
  Start-AzsScaleUnitNode -Location <RegionName> -Name <NodeName>
````

<span data-ttu-id="fb5c1-154">In the unlikely case that the power on action doesn't work, use the BMC web interface instead.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-154">In the unlikely case that the power on action doesn't work, use the BMC web interface instead.</span></span>

### <a name="drain"></a><span data-ttu-id="fb5c1-155">Drain</span><span class="sxs-lookup"><span data-stu-id="fb5c1-155">Drain</span></span>

<span data-ttu-id="fb5c1-156">The **Drain** action evacuates all active workloads by distributing them among the remaining nodes in that particular scale unit.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-156">The **Drain** action evacuates all active workloads by distributing them among the remaining nodes in that particular scale unit.</span></span>

<span data-ttu-id="fb5c1-157">This action is typically used during field replacement of parts, such as the replacement of an entire node.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-157">This action is typically used during field replacement of parts, such as the replacement of an entire node.</span></span>

> [!IMPORTANT]  
> <span data-ttu-id="fb5c1-158">Make sure that you drain a node only during a planned maintenance window, where users have been notified.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-158">Make sure that you drain a node only during a planned maintenance window, where users have been notified.</span></span> <span data-ttu-id="fb5c1-159">Under some conditions, active workloads can experience interruptions.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-159">Under some conditions, active workloads can experience interruptions.</span></span>

<span data-ttu-id="fb5c1-160">To run the drain action through PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fb5c1-160">To run the drain action through PowerShell:</span></span>

  ````PowerShell
  Disable-AzsScaleUnitNode -Location <RegionName> -Name <NodeName>
  ````

### <a name="resume"></a><span data-ttu-id="fb5c1-161">Resume</span><span class="sxs-lookup"><span data-stu-id="fb5c1-161">Resume</span></span>

<span data-ttu-id="fb5c1-162">The **Resume** action resumes a drained node and marks it active for workload placement.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-162">The **Resume** action resumes a drained node and marks it active for workload placement.</span></span> <span data-ttu-id="fb5c1-163">Earlier workloads that were running on the node do not fail back.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-163">Earlier workloads that were running on the node do not fail back.</span></span> <span data-ttu-id="fb5c1-164">(If you drain a node and then power off, when you power the node back on, it's not marked as active for workload placement.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-164">(If you drain a node and then power off, when you power the node back on, it's not marked as active for workload placement.</span></span> <span data-ttu-id="fb5c1-165">When ready, you must use the resume action to mark the node as active.)</span><span class="sxs-lookup"><span data-stu-id="fb5c1-165">When ready, you must use the resume action to mark the node as active.)</span></span>

<span data-ttu-id="fb5c1-166">To run the resume action through PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fb5c1-166">To run the resume action through PowerShell:</span></span>

  ````PowerShell
  Enable-AzsScaleUnitNode -Location <RegionName> -Name <NodeName>
  ````

### <a name="repair"></a><span data-ttu-id="fb5c1-167">Repair</span><span class="sxs-lookup"><span data-stu-id="fb5c1-167">Repair</span></span>

<span data-ttu-id="fb5c1-168">The **Repair** action repairs a node.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-168">The **Repair** action repairs a node.</span></span> <span data-ttu-id="fb5c1-169">Use it only for either of the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="fb5c1-169">Use it only for either of the following scenarios:</span></span>

- <span data-ttu-id="fb5c1-170">Full node replacement (with or without new data disks)</span><span class="sxs-lookup"><span data-stu-id="fb5c1-170">Full node replacement (with or without new data disks)</span></span>
- <span data-ttu-id="fb5c1-171">After hardware component failure and replacement (if advised in the field replaceable unit (FRU) documentation).</span><span class="sxs-lookup"><span data-stu-id="fb5c1-171">After hardware component failure and replacement (if advised in the field replaceable unit (FRU) documentation).</span></span>

> [!IMPORTANT]  
> <span data-ttu-id="fb5c1-172">See your OEM hardware vendor’s FRU documentation for exact steps when you need to replace a node or individual hardware components.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-172">See your OEM hardware vendor’s FRU documentation for exact steps when you need to replace a node or individual hardware components.</span></span> <span data-ttu-id="fb5c1-173">The FRU documentation will specify whether you need to run the repair action after replacing a hardware component.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-173">The FRU documentation will specify whether you need to run the repair action after replacing a hardware component.</span></span>  

<span data-ttu-id="fb5c1-174">When you run the repair action, you need to specify the BMC IP address.</span><span class="sxs-lookup"><span data-stu-id="fb5c1-174">When you run the repair action, you need to specify the BMC IP address.</span></span> 

<span data-ttu-id="fb5c1-175">To run the repair action through PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fb5c1-175">To run the repair action through PowerShell:</span></span>

  ````PowerShell
  Repair-AzsScaleUnitNode -Location <RegionName> -Name <NodeName> -BMCIPAddress <BMCIPAddress>
  ````

## <a name="next-steps"></a><span data-ttu-id="fb5c1-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="fb5c1-176">Next steps</span></span>

<span data-ttu-id="fb5c1-177">To learn more about the Azure Stack Fabric administrator module, see [Azs.Fabric.Admin](https://docs.microsoft.com/powershell/module/azs.fabric.admin/?view=azurestackps-1.4.0).</span><span class="sxs-lookup"><span data-stu-id="fb5c1-177">To learn more about the Azure Stack Fabric administrator module, see [Azs.Fabric.Admin](https://docs.microsoft.com/powershell/module/azs.fabric.admin/?view=azurestackps-1.4.0).</span></span>