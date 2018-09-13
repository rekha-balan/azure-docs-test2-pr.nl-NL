---
title: Azure Stack add scale nodes | Microsoft Docs
description: Add nodes to scale units in Azure Stack.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/20/2018
ms.author: brenduns
ms.reviewer: thoroet
ms.openlocfilehash: 02602243bcb4e426ebf4984e387da8e8c148232e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965800"
---
# <a name="add-additional-scale-unit-nodes-in-azure-stack"></a><span data-ttu-id="55f22-103">Add additional scale unit nodes in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="55f22-103">Add additional scale unit nodes in Azure Stack</span></span>

<span data-ttu-id="55f22-104">Azure Stack operators can increase the overall capacity of an existing scale unit by adding an additional physical computer.</span><span class="sxs-lookup"><span data-stu-id="55f22-104">Azure Stack operators can increase the overall capacity of an existing scale unit by adding an additional physical computer.</span></span> <span data-ttu-id="55f22-105">The physical computer is also referred to as a scale unit node.</span><span class="sxs-lookup"><span data-stu-id="55f22-105">The physical computer is also referred to as a scale unit node.</span></span> <span data-ttu-id="55f22-106">Each new scale unit node you add must be homogenous in CPU type, memory, and disk number & size to the nodes that are already present in the scale unit.</span><span class="sxs-lookup"><span data-stu-id="55f22-106">Each new scale unit node you add must be homogenous in CPU type, memory, and disk number & size to the nodes that are already present in the scale unit.</span></span>

> [!NOTE]  
<span data-ttu-id="55f22-107">You must run Azure Stack 1807 or later to add additional scale unit nodes.</span><span class="sxs-lookup"><span data-stu-id="55f22-107">You must run Azure Stack 1807 or later to add additional scale unit nodes.</span></span>

<span data-ttu-id="55f22-108">To add a scale unit node, you act in Azure Stack and run tooling from your hardware equipment manufacturer (OEM).</span><span class="sxs-lookup"><span data-stu-id="55f22-108">To add a scale unit node, you act in Azure Stack and run tooling from your hardware equipment manufacturer (OEM).</span></span> <span data-ttu-id="55f22-109">The OEM tooling runs on the hardware lifecycle host (HLH) to make sure the new physical computer matches the same firmware level as existing nodes.</span><span class="sxs-lookup"><span data-stu-id="55f22-109">The OEM tooling runs on the hardware lifecycle host (HLH) to make sure the new physical computer matches the same firmware level as existing nodes.</span></span>

<span data-ttu-id="55f22-110">The following flow diagram shows the general process to add a scale unit node.</span><span class="sxs-lookup"><span data-stu-id="55f22-110">The following flow diagram shows the general process to add a scale unit node.</span></span>

<span data-ttu-id="55f22-111">![Add scale unit flow](media/azure-stack-add-scale-node/add-node-flow.png) &#42; *Whether your OEM hardware vendor enacts the physical server rack placement and updates the firmware varies based on your support contract.*</span><span class="sxs-lookup"><span data-stu-id="55f22-111">![Add scale unit flow](media/azure-stack-add-scale-node/add-node-flow.png) &#42; *Whether your OEM hardware vendor enacts the physical server rack placement and updates the firmware varies based on your support contract.*</span></span>

<span data-ttu-id="55f22-112">The operation to add a new node can take several hours or days to complete.</span><span class="sxs-lookup"><span data-stu-id="55f22-112">The operation to add a new node can take several hours or days to complete.</span></span>

> [!Note]  
> <span data-ttu-id="55f22-113">Do not attempt any of the following operations while an add scale unit node operation is already in progress:</span><span class="sxs-lookup"><span data-stu-id="55f22-113">Do not attempt any of the following operations while an add scale unit node operation is already in progress:</span></span>
>
>  - <span data-ttu-id="55f22-114">Update Azure Stack</span><span class="sxs-lookup"><span data-stu-id="55f22-114">Update Azure Stack</span></span>
>  - <span data-ttu-id="55f22-115">Rotate certificates</span><span class="sxs-lookup"><span data-stu-id="55f22-115">Rotate certificates</span></span>
>  - <span data-ttu-id="55f22-116">Stop Azure Stack</span><span class="sxs-lookup"><span data-stu-id="55f22-116">Stop Azure Stack</span></span>
>  - <span data-ttu-id="55f22-117">Repair scale unit node</span><span class="sxs-lookup"><span data-stu-id="55f22-117">Repair scale unit node</span></span>


## <a name="add-scale-unit-nodes"></a><span data-ttu-id="55f22-118">Add scale unit nodes</span><span class="sxs-lookup"><span data-stu-id="55f22-118">Add scale unit nodes</span></span>

<span data-ttu-id="55f22-119">The following steps are a high-level overview of how to add a node.</span><span class="sxs-lookup"><span data-stu-id="55f22-119">The following steps are a high-level overview of how to add a node.</span></span> <span data-ttu-id="55f22-120">Don't follow these steps without first referring to your OEM-provided capacity expansion documentation.</span><span class="sxs-lookup"><span data-stu-id="55f22-120">Don't follow these steps without first referring to your OEM-provided capacity expansion documentation.</span></span>

1. <span data-ttu-id="55f22-121">Place the new physical server in the rack and cable it appropriately.</span><span class="sxs-lookup"><span data-stu-id="55f22-121">Place the new physical server in the rack and cable it appropriately.</span></span> 
2. <span data-ttu-id="55f22-122">Enable physical switch ports and adjust access control lists (ACLs) if applicable.</span><span class="sxs-lookup"><span data-stu-id="55f22-122">Enable physical switch ports and adjust access control lists (ACLs) if applicable.</span></span>
3. <span data-ttu-id="55f22-123">Configure the correct IP Address in the baseboard management controller (BMC) and apply all BIOS settings per your OEM-provided documentation.</span><span class="sxs-lookup"><span data-stu-id="55f22-123">Configure the correct IP Address in the baseboard management controller (BMC) and apply all BIOS settings per your OEM-provided documentation.</span></span>
4. <span data-ttu-id="55f22-124">Apply the current firmware baseline to all components by using the tools that are provided by the hardware manufacturer that run on the HLH.</span><span class="sxs-lookup"><span data-stu-id="55f22-124">Apply the current firmware baseline to all components by using the tools that are provided by the hardware manufacturer that run on the HLH.</span></span>
5. <span data-ttu-id="55f22-125">Run the Add node operation in the Azure Stack admin portal.</span><span class="sxs-lookup"><span data-stu-id="55f22-125">Run the Add node operation in the Azure Stack admin portal.</span></span>
6. <span data-ttu-id="55f22-126">Validate that the add node operation succeeds.</span><span class="sxs-lookup"><span data-stu-id="55f22-126">Validate that the add node operation succeeds.</span></span> <span data-ttu-id="55f22-127">To do so, check the [**Status** of the Scale Unit](#monitor-add-node-operations).</span><span class="sxs-lookup"><span data-stu-id="55f22-127">To do so, check the [**Status** of the Scale Unit](#monitor-add-node-operations).</span></span> 

## <a name="add-the-node"></a><span data-ttu-id="55f22-128">Add the node</span><span class="sxs-lookup"><span data-stu-id="55f22-128">Add the node</span></span>

<span data-ttu-id="55f22-129">You can use the admin portal or PowerShell to add new nodes.</span><span class="sxs-lookup"><span data-stu-id="55f22-129">You can use the admin portal or PowerShell to add new nodes.</span></span> <span data-ttu-id="55f22-130">The add node operation first adds the new scale unit node as available compute capacity and then automatically extends the storage capacity.</span><span class="sxs-lookup"><span data-stu-id="55f22-130">The add node operation first adds the new scale unit node as available compute capacity and then automatically extends the storage capacity.</span></span> <span data-ttu-id="55f22-131">The capacity expands automatically because Azure Stack is a hyperconverged system where *compute* and *storage* scale together.</span><span class="sxs-lookup"><span data-stu-id="55f22-131">The capacity expands automatically because Azure Stack is a hyperconverged system where *compute* and *storage* scale together.</span></span>

### <a name="use-the-admin-portal"></a><span data-ttu-id="55f22-132">Use the admin portal</span><span class="sxs-lookup"><span data-stu-id="55f22-132">Use the admin portal</span></span>

1. <span data-ttu-id="55f22-133">Sign in to the Azure Stack admin portal as an Azure Stack operator.</span><span class="sxs-lookup"><span data-stu-id="55f22-133">Sign in to the Azure Stack admin portal as an Azure Stack operator.</span></span>
2. <span data-ttu-id="55f22-134">Navigate to **New** > **Capacity** > **Scale Unit Node**.</span><span class="sxs-lookup"><span data-stu-id="55f22-134">Navigate to **New** > **Capacity** > **Scale Unit Node**.</span></span>
   <span data-ttu-id="55f22-135">![Scale unit node](media/azure-stack-add-scale-node/select-node1.png)</span><span class="sxs-lookup"><span data-stu-id="55f22-135">![Scale unit node](media/azure-stack-add-scale-node/select-node1.png)</span></span>
3. <span data-ttu-id="55f22-136">On the **Add node** pane, select the *Region*, and then select the *Scale unit* that you want to add the node to.</span><span class="sxs-lookup"><span data-stu-id="55f22-136">On the **Add node** pane, select the *Region*, and then select the *Scale unit* that you want to add the node to.</span></span> <span data-ttu-id="55f22-137">Also specify the *BMC IP ADDRESS* for the scale unit node you are adding.</span><span class="sxs-lookup"><span data-stu-id="55f22-137">Also specify the *BMC IP ADDRESS* for the scale unit node you are adding.</span></span> <span data-ttu-id="55f22-138">You can only add one node at a time.</span><span class="sxs-lookup"><span data-stu-id="55f22-138">You can only add one node at a time.</span></span>
   <span data-ttu-id="55f22-139">![Add node details](media/azure-stack-add-scale-node/select-node2.png)</span><span class="sxs-lookup"><span data-stu-id="55f22-139">![Add node details](media/azure-stack-add-scale-node/select-node2.png)</span></span>
 

### <a name="use-powershell"></a><span data-ttu-id="55f22-140">Use PowerShell</span><span class="sxs-lookup"><span data-stu-id="55f22-140">Use PowerShell</span></span>

<span data-ttu-id="55f22-141">Use the **New-AzsScaleUnitNodeObject** cmdlet to add a node.</span><span class="sxs-lookup"><span data-stu-id="55f22-141">Use the **New-AzsScaleUnitNodeObject** cmdlet to add a node.</span></span>  

<span data-ttu-id="55f22-142">Before using either of the following sample PowerShell scripts, replace the values *node names* and *IP addresses* with values from your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="55f22-142">Before using either of the following sample PowerShell scripts, replace the values *node names* and *IP addresses* with values from your Azure Stack environment.</span></span>

  > [!Note]  
  > <span data-ttu-id="55f22-143">When naming a node you must keep the name to less than 15 characters in length.</span><span class="sxs-lookup"><span data-stu-id="55f22-143">When naming a node you must keep the name to less than 15 characters in length.</span></span> <span data-ttu-id="55f22-144">You also cannot use a name that contains a space or contains any of the following characters: `\`, `/`, `:`, `*`, `?`, `"`, `<`, `>`, `|`, `\`, `~`, `!`, `@`, `#`, `$`, `%`, `^`, `&`, `(`, `)`, `{`,` }`, `_`.</span><span class="sxs-lookup"><span data-stu-id="55f22-144">You also cannot use a name that contains a space or contains any of the following characters: `\`, `/`, `:`, `*`, `?`, `"`, `<`, `>`, `|`, `\`, `~`, `!`, `@`, `#`, `$`, `%`, `^`, `&`, `(`, `)`, `{`,` }`, `_`.</span></span>

<span data-ttu-id="55f22-145">**Add a node:**</span><span class="sxs-lookup"><span data-stu-id="55f22-145">**Add a node:**</span></span>
  ```powershell
  ## Add a single Node 
  $NewNode=New-AzsScaleUnitNodeObject -computername "<name_of_new_node>" -BMCIPv4Address "<BMCIP_address_of_new_node>" 
 
  Add-AzsScaleUnitNode -NodeList $NewNode -ScaleUnit "<name_of_scale_unit_cluster>" 
  ```  

## <a name="monitor-add-node-operations"></a><span data-ttu-id="55f22-146">Monitor add node operations</span><span class="sxs-lookup"><span data-stu-id="55f22-146">Monitor add node operations</span></span> 
<span data-ttu-id="55f22-147">You can use the admin portal or PowerShell to get the status of the add node operation.</span><span class="sxs-lookup"><span data-stu-id="55f22-147">You can use the admin portal or PowerShell to get the status of the add node operation.</span></span> <span data-ttu-id="55f22-148">Add node operations can take several hours to days to complete.</span><span class="sxs-lookup"><span data-stu-id="55f22-148">Add node operations can take several hours to days to complete.</span></span>

### <a name="use-the-admin-portal"></a><span data-ttu-id="55f22-149">Use the admin portal</span><span class="sxs-lookup"><span data-stu-id="55f22-149">Use the admin portal</span></span> 
<span data-ttu-id="55f22-150">To monitor the addition of a new node, in the admin portal review the scale unit or scale unit node objects.</span><span class="sxs-lookup"><span data-stu-id="55f22-150">To monitor the addition of a new node, in the admin portal review the scale unit or scale unit node objects.</span></span> <span data-ttu-id="55f22-151">To do so, go to **Region management** > **Scale units**.</span><span class="sxs-lookup"><span data-stu-id="55f22-151">To do so, go to **Region management** > **Scale units**.</span></span> <span data-ttu-id="55f22-152">Next, select the scale unit or scale unit node you want to review.</span><span class="sxs-lookup"><span data-stu-id="55f22-152">Next, select the scale unit or scale unit node you want to review.</span></span> 

### <a name="use-powershell"></a><span data-ttu-id="55f22-153">Use PowerShell</span><span class="sxs-lookup"><span data-stu-id="55f22-153">Use PowerShell</span></span>
<span data-ttu-id="55f22-154">The status for scale unit and scale unit nodes can be retrieved using PowerShell as follows:</span><span class="sxs-lookup"><span data-stu-id="55f22-154">The status for scale unit and scale unit nodes can be retrieved using PowerShell as follows:</span></span>
  ```powershell
  #Retrieve Status for the Scale Unit
  Get-AzsScaleUnit|select name,state
 
  #Retrieve Status for each Scale Unit Node
  Get-AzsScaleUnitNode |Select Name, ScaleUnitNodeStatus
```

### <a name="status-for-the-add-node-operation"></a><span data-ttu-id="55f22-155">Status for the add node operation</span><span class="sxs-lookup"><span data-stu-id="55f22-155">Status for the add node operation</span></span> 
<span data-ttu-id="55f22-156">**For a scale unit:**</span><span class="sxs-lookup"><span data-stu-id="55f22-156">**For a scale unit:**</span></span>
|<span data-ttu-id="55f22-157">Status</span><span class="sxs-lookup"><span data-stu-id="55f22-157">Status</span></span>               |<span data-ttu-id="55f22-158">Description</span><span class="sxs-lookup"><span data-stu-id="55f22-158">Description</span></span>  |
|---------------------|---------|
|<span data-ttu-id="55f22-159">Running</span><span class="sxs-lookup"><span data-stu-id="55f22-159">Running</span></span>              |<span data-ttu-id="55f22-160">All nodes are actively participating in the scale unit.</span><span class="sxs-lookup"><span data-stu-id="55f22-160">All nodes are actively participating in the scale unit.</span></span>|
|<span data-ttu-id="55f22-161">Stopped</span><span class="sxs-lookup"><span data-stu-id="55f22-161">Stopped</span></span>              |<span data-ttu-id="55f22-162">The scale unit node is either down or unreachable.</span><span class="sxs-lookup"><span data-stu-id="55f22-162">The scale unit node is either down or unreachable.</span></span>|
|<span data-ttu-id="55f22-163">Expanding</span><span class="sxs-lookup"><span data-stu-id="55f22-163">Expanding</span></span>            |<span data-ttu-id="55f22-164">One or more scale unit nodes are currently being added as compute capacity.</span><span class="sxs-lookup"><span data-stu-id="55f22-164">One or more scale unit nodes are currently being added as compute capacity.</span></span>|
|<span data-ttu-id="55f22-165">Configuring Storage</span><span class="sxs-lookup"><span data-stu-id="55f22-165">Configuring Storage</span></span>  |<span data-ttu-id="55f22-166">The compute capacity has been expanded and the storage configuration is running.</span><span class="sxs-lookup"><span data-stu-id="55f22-166">The compute capacity has been expanded and the storage configuration is running.</span></span>|
|<span data-ttu-id="55f22-167">Requires Remediation</span><span class="sxs-lookup"><span data-stu-id="55f22-167">Requires Remediation</span></span> |<span data-ttu-id="55f22-168">An error has been detected that requires one or more scale unit nodes to be repaired.</span><span class="sxs-lookup"><span data-stu-id="55f22-168">An error has been detected that requires one or more scale unit nodes to be repaired.</span></span>|


<span data-ttu-id="55f22-169">**For a scale unit node:**</span><span class="sxs-lookup"><span data-stu-id="55f22-169">**For a scale unit node:**</span></span>
|<span data-ttu-id="55f22-170">Status</span><span class="sxs-lookup"><span data-stu-id="55f22-170">Status</span></span>                |<span data-ttu-id="55f22-171">Description</span><span class="sxs-lookup"><span data-stu-id="55f22-171">Description</span></span>  |
|----------------------|---------|
|<span data-ttu-id="55f22-172">Running</span><span class="sxs-lookup"><span data-stu-id="55f22-172">Running</span></span>               |<span data-ttu-id="55f22-173">The node is actively participating in the scale unit.</span><span class="sxs-lookup"><span data-stu-id="55f22-173">The node is actively participating in the scale unit.</span></span>|
|<span data-ttu-id="55f22-174">Stopped</span><span class="sxs-lookup"><span data-stu-id="55f22-174">Stopped</span></span>               |<span data-ttu-id="55f22-175">The node is unavailable.</span><span class="sxs-lookup"><span data-stu-id="55f22-175">The node is unavailable.</span></span>|
|<span data-ttu-id="55f22-176">Adding</span><span class="sxs-lookup"><span data-stu-id="55f22-176">Adding</span></span>                |<span data-ttu-id="55f22-177">The node is actively being added to the scale unit.</span><span class="sxs-lookup"><span data-stu-id="55f22-177">The node is actively being added to the scale unit.</span></span>|
|<span data-ttu-id="55f22-178">Repairing</span><span class="sxs-lookup"><span data-stu-id="55f22-178">Repairing</span></span>             |<span data-ttu-id="55f22-179">The node is actively being repaired.</span><span class="sxs-lookup"><span data-stu-id="55f22-179">The node is actively being repaired.</span></span>|
|<span data-ttu-id="55f22-180">Maintenance</span><span class="sxs-lookup"><span data-stu-id="55f22-180">Maintenance</span></span>           |<span data-ttu-id="55f22-181">The node is paused, and no active user workload is running.</span><span class="sxs-lookup"><span data-stu-id="55f22-181">The node is paused, and no active user workload is running.</span></span> |
|<span data-ttu-id="55f22-182">Requires Remediation</span><span class="sxs-lookup"><span data-stu-id="55f22-182">Requires Remediation</span></span>  |<span data-ttu-id="55f22-183">An error has been detected that requires the node to be repaired.</span><span class="sxs-lookup"><span data-stu-id="55f22-183">An error has been detected that requires the node to be repaired.</span></span>|


## <a name="troubleshooting"></a><span data-ttu-id="55f22-184">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="55f22-184">Troubleshooting</span></span>
<span data-ttu-id="55f22-185">The following are common issues seen when adding a node.</span><span class="sxs-lookup"><span data-stu-id="55f22-185">The following are common issues seen when adding a node.</span></span> 

<span data-ttu-id="55f22-186">**Scenario 1:**  The add scale unit node operation fails but one or more nodes are listed with a status of Stopped.</span><span class="sxs-lookup"><span data-stu-id="55f22-186">**Scenario 1:**  The add scale unit node operation fails but one or more nodes are listed with a status of Stopped.</span></span>  
- <span data-ttu-id="55f22-187">Remediation: Use the repair operation to repair one or more nodes.</span><span class="sxs-lookup"><span data-stu-id="55f22-187">Remediation: Use the repair operation to repair one or more nodes.</span></span> <span data-ttu-id="55f22-188">Only a single repair operation can run at one time.</span><span class="sxs-lookup"><span data-stu-id="55f22-188">Only a single repair operation can run at one time.</span></span>

<span data-ttu-id="55f22-189">**Scenario 2:** One or more scale unit nodes have been added but the storage expansion failed.</span><span class="sxs-lookup"><span data-stu-id="55f22-189">**Scenario 2:** One or more scale unit nodes have been added but the storage expansion failed.</span></span> <span data-ttu-id="55f22-190">In this scenario, the scale unit node object reports a status of Running but the Configuring Storage task isn't started.</span><span class="sxs-lookup"><span data-stu-id="55f22-190">In this scenario, the scale unit node object reports a status of Running but the Configuring Storage task isn't started.</span></span>  
- <span data-ttu-id="55f22-191">Remediation: Use the privileged endpoint to review the storage health by running the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="55f22-191">Remediation: Use the privileged endpoint to review the storage health by running the following PowerShell cmdlet:</span></span>
  ```powershell
     Get-VirtualDisk -CimSession s-cluster | Get-StorageJob
  ```
 
<span data-ttu-id="55f22-192">**Scenario 3:** You received an alert that indicates the storage scale-out job failed.</span><span class="sxs-lookup"><span data-stu-id="55f22-192">**Scenario 3:** You received an alert that indicates the storage scale-out job failed.</span></span>  
- <span data-ttu-id="55f22-193">Remediation: In this case, the storage configuration task has failed.</span><span class="sxs-lookup"><span data-stu-id="55f22-193">Remediation: In this case, the storage configuration task has failed.</span></span> <span data-ttu-id="55f22-194">This problem requires you to contact support.</span><span class="sxs-lookup"><span data-stu-id="55f22-194">This problem requires you to contact support.</span></span>


## <a name="next-steps"></a><span data-ttu-id="55f22-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="55f22-195">Next steps</span></span> 
<span data-ttu-id="55f22-196">Review [Node actions](azure-stack-node-actions.md)</span><span class="sxs-lookup"><span data-stu-id="55f22-196">Review [Node actions](azure-stack-node-actions.md)</span></span> 
