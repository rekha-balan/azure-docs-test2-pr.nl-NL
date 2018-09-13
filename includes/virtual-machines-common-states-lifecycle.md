---
title: include file
description: include file
services: virtual-machines
author: shandilvarun
ms.service: virtual-machines
ms.topic: include
ms.date: 08/09/2018
ms.author: vashan, cynthn, rajsqr
ms.custom: include file
ms.openlocfilehash: 603e7c3a0c30eb42cb75d6a6ff87a96d847b7c9f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870320"
---
<span data-ttu-id="daf7a-103">Azure Virtual Machines (VMs) go through different states that can be categorized into *provisioning* and *power* states.</span><span class="sxs-lookup"><span data-stu-id="daf7a-103">Azure Virtual Machines (VMs) go through different states that can be categorized into *provisioning* and *power* states.</span></span> <span data-ttu-id="daf7a-104">The purpose of this article is to describe these states and specifically highlight when customers are billed for instance usage.</span><span class="sxs-lookup"><span data-stu-id="daf7a-104">The purpose of this article is to describe these states and specifically highlight when customers are billed for instance usage.</span></span> 

## <a name="power-states"></a><span data-ttu-id="daf7a-105">Power states</span><span class="sxs-lookup"><span data-stu-id="daf7a-105">Power states</span></span>

<span data-ttu-id="daf7a-106">The power state represents the last known state of the VM.</span><span class="sxs-lookup"><span data-stu-id="daf7a-106">The power state represents the last known state of the VM.</span></span>

![VM power state diagram](./media/virtual-machines-common-states-lifecycle/vm-power-states.png)

<br>
<span data-ttu-id="daf7a-108">The following table provides a  description of each instance state and indicates whether it is billed for instance usage or not.</span><span class="sxs-lookup"><span data-stu-id="daf7a-108">The following table provides a  description of each instance state and indicates whether it is billed for instance usage or not.</span></span>

<table>
<tr>
<th>
<span data-ttu-id="daf7a-109">State</span><span class="sxs-lookup"><span data-stu-id="daf7a-109">State</span></span>
</th>
<th>
<span data-ttu-id="daf7a-110">Description</span><span class="sxs-lookup"><span data-stu-id="daf7a-110">Description</span></span>
</th>
<th>
<span data-ttu-id="daf7a-111">Instance usage billing</span><span class="sxs-lookup"><span data-stu-id="daf7a-111">Instance usage billing</span></span>
</th>
</tr>
<tr>
<td>
<p><span data-ttu-id="daf7a-112"><b>Starting</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-112"><b>Starting</b></span></span></p>
</td>
<td>
<p><span data-ttu-id="daf7a-113">VM is starting up.</span><span class="sxs-lookup"><span data-stu-id="daf7a-113">VM is starting up.</span></span></p>
<code>"statuses": [<br>
   {<br>
      "code": "PowerState/starting",<br>
       "level": "Info",<br>
        "displayStatus": "VM starting"<br>
    }<br>
    ]</code><br>
</td>
<td>
<p><span data-ttu-id="daf7a-114"><b>Not billed</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-114"><b>Not billed</b></span></span></p>
</td>
</tr>
<tr>
<td>
<p><span data-ttu-id="daf7a-115"><b>Running</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-115"><b>Running</b></span></span></p>
</td>
<td>
<p><span data-ttu-id="daf7a-116">Normal working state for a VM</span><span class="sxs-lookup"><span data-stu-id="daf7a-116">Normal working state for a VM</span></span></p>
<code>"statuses": [<br>
 {<br>
 "code": "PowerState/running",<br>
 "level": "Info",<br>
 "displayStatus": "VM running"<br>
 }<br>
 ]</code><br>
</td>
<td>
<p><span data-ttu-id="daf7a-117"><b>Billed</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-117"><b>Billed</b></span></span></p>
</td>
</tr>
<tr>
<td>
<p><span data-ttu-id="daf7a-118"><b>Stopping</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-118"><b>Stopping</b></span></span></p>
</td>
<td>
<p><span data-ttu-id="daf7a-119">This is a transitional state.</span><span class="sxs-lookup"><span data-stu-id="daf7a-119">This is a transitional state.</span></span> <span data-ttu-id="daf7a-120">When completed, it will show as **Stopped**.</span><span class="sxs-lookup"><span data-stu-id="daf7a-120">When completed, it will show as **Stopped**.</span></span></p>
<code>"statuses": [<br>
 {<br>
 "code": "PowerState/stopping",<br>
 "level": "Info",<br>
 "displayStatus": "VM stopping"<br>
 }<br>
 ]</code><br>
</td>
<td>
<p><span data-ttu-id="daf7a-121"><b>Billed</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-121"><b>Billed</b></span></span></p>
</td>
</tr>
<tr>
<td>
<p><span data-ttu-id="daf7a-122"><b>Stopped</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-122"><b>Stopped</b></span></span></p>
</td>
<td>
<p><span data-ttu-id="daf7a-123">The VM has been shut down from within the guest OS or using the PowerOff APIs.</span><span class="sxs-lookup"><span data-stu-id="daf7a-123">The VM has been shut down from within the guest OS or using the PowerOff APIs.</span></span></p>
<p><span data-ttu-id="daf7a-124">Hardware is still allocated to the VM and it remains on the host.</span><span class="sxs-lookup"><span data-stu-id="daf7a-124">Hardware is still allocated to the VM and it remains on the host.</span></span> </p>
<code>"statuses": [<br>
 {<br>
 "code": "PowerState/stopped",<br>
 "level": "Info",<br>
 "displayStatus": "VM stopped"<br>
 }<br>
 ]</code><br>
</td>
<td>
<p><span data-ttu-id="daf7a-125"><b>Not billed&#42;</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-125"><b>Not billed&#42;</b></span></span></p>
</td>
</tr>
<tr>
<td>
<p><span data-ttu-id="daf7a-126"><b>Deallocating</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-126"><b>Deallocating</b></span></span></p>
</td>
<td>
<p><span data-ttu-id="daf7a-127">Transitional state.</span><span class="sxs-lookup"><span data-stu-id="daf7a-127">Transitional state.</span></span> <span data-ttu-id="daf7a-128">When completed, the VM will show as **Deallocated**.</span><span class="sxs-lookup"><span data-stu-id="daf7a-128">When completed, the VM will show as **Deallocated**.</span></span></p>
<code>"statuses": [<br>
 {<br>
 "code": "PowerState/deallocating",<br>
 "level": "Info",<br>
 "displayStatus": "VM deallocating"<br>
 }<br>
 ]</code><br>
</td>
<td>
<p><span data-ttu-id="daf7a-129"><b>Not billed&#42;</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-129"><b>Not billed&#42;</b></span></span></p>
</td>
</tr>
<tr>
<td>
<p><span data-ttu-id="daf7a-130"><b>Deallocated</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-130"><b>Deallocated</b></span></span></p>
</td>
<td>
<p><span data-ttu-id="daf7a-131">The VM has been stopped successfully and removed from the host.</span><span class="sxs-lookup"><span data-stu-id="daf7a-131">The VM has been stopped successfully and removed from the host.</span></span> </p>
<code>"statuses": [<br>
 {<br>
 "code": "PowerState/deallocated",<br>
 "level": "Info",<br>
 "displayStatus": "VM deallocated"<br>
 }<br>
 ]</code><br>
</td>
<td>
<p><span data-ttu-id="daf7a-132"><b>Not billed</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-132"><b>Not billed</b></span></span></p>
</td>
</tr>
</tbody>
</table>


<span data-ttu-id="daf7a-133">&#42;Some Azure resources, such as Disks and Networking, incur charges regardless of the instance's state.</span><span class="sxs-lookup"><span data-stu-id="daf7a-133">&#42;Some Azure resources, such as Disks and Networking, incur charges regardless of the instance's state.</span></span> 

## <a name="provisioning-states"></a><span data-ttu-id="daf7a-134">Provisioning states</span><span class="sxs-lookup"><span data-stu-id="daf7a-134">Provisioning states</span></span>

<span data-ttu-id="daf7a-135">A provisioning state is the status of a user-initiated, control-plane operation on the VM.</span><span class="sxs-lookup"><span data-stu-id="daf7a-135">A provisioning state is the status of a user-initiated, control-plane operation on the VM.</span></span> <span data-ttu-id="daf7a-136">These states are separate from the power state of a VM.</span><span class="sxs-lookup"><span data-stu-id="daf7a-136">These states are separate from the power state of a VM.</span></span>

- <span data-ttu-id="daf7a-137">**Create** – VM creation.</span><span class="sxs-lookup"><span data-stu-id="daf7a-137">**Create** – VM creation.</span></span>

- <span data-ttu-id="daf7a-138">**Update** – updates the model for an existing VM.</span><span class="sxs-lookup"><span data-stu-id="daf7a-138">**Update** – updates the model for an existing VM.</span></span> <span data-ttu-id="daf7a-139">Some non-model changes to VM such as Start/Restart also fall under update.</span><span class="sxs-lookup"><span data-stu-id="daf7a-139">Some non-model changes to VM such as Start/Restart also fall under update.</span></span>

- <span data-ttu-id="daf7a-140">**Delete** – VM deletion.</span><span class="sxs-lookup"><span data-stu-id="daf7a-140">**Delete** – VM deletion.</span></span>

- <span data-ttu-id="daf7a-141">**Deallocate** – is where a VM is stopped and removed from the host.</span><span class="sxs-lookup"><span data-stu-id="daf7a-141">**Deallocate** – is where a VM is stopped and removed from the host.</span></span> <span data-ttu-id="daf7a-142">Deallocating a VM is considered an update, so it will display provisioning states related to updating.</span><span class="sxs-lookup"><span data-stu-id="daf7a-142">Deallocating a VM is considered an update, so it will display provisioning states related to updating.</span></span>



<span data-ttu-id="daf7a-143">Here are the transitional operation states after the platform has accepted a user-initiated action:</span><span class="sxs-lookup"><span data-stu-id="daf7a-143">Here are the transitional operation states after the platform has accepted a user-initiated action:</span></span>

<br>

<table>
<tbody>
<tr>
<td width="162">
<p><span data-ttu-id="daf7a-144"><b>States</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-144"><b>States</b></span></span></p>
</td>
<td width="366">
<p><span data-ttu-id="daf7a-145">Description</span><span class="sxs-lookup"><span data-stu-id="daf7a-145">Description</span></span></p>
</td>
</tr>
<tr>
<td width="162">
<p><span data-ttu-id="daf7a-146"><b>Creating</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-146"><b>Creating</b></span></span></p>
</td>
<td width="366">
<code>"statuses": [<br>
 {<br>
 "code": "ProvisioningState/creating",<br>
 "level": "Info",<br>
 "displayStatus": "Creating"<br>
 }</code><br>
</td>
</tr>
<tr>
<td width="162">
<p><span data-ttu-id="daf7a-147"><b>Updating</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-147"><b>Updating</b></span></span></p>
</td>
<td width="366">
<code>"statuses": [<br>
 {<br>
 "code": "ProvisioningState/updating",<br>
 "level": "Info",<br>
 "displayStatus": "Updating"<br>
 }<br>
 ]</code><br>
</td>
</tr>
<tr>
<td width="162">
<p><span data-ttu-id="daf7a-148"><b>Deleting</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-148"><b>Deleting</b></span></span></p>
</td>
<td width="366">
<code>"statuses": [<br>
 {<br>
 "code": "ProvisioningState/deleting",<br>
 "level": "Info",<br>
 "displayStatus": "Deleting"<br>
 }<br>
 ]</code><br>
</td>
</tr>
<tr>
<td width="162">
<p><span data-ttu-id="daf7a-149"><b>OS provisioning states</b></span><span class="sxs-lookup"><span data-stu-id="daf7a-149"><b>OS provisioning states</b></span></span></p>
</td>
<td width="366">
<p><span data-ttu-id="daf7a-150">If a VM is created with an OS image and not with a specialized image, then following substates can be observed:</span><span class="sxs-lookup"><span data-stu-id="daf7a-150">If a VM is created with an OS image and not with a specialized image, then following substates can be observed:</span></span></p>
<p><span data-ttu-id="daf7a-151">1. <b>OSProvisioningInprogress</b> &ndash; The VM is running, and installation of guest OS is in progress.</span><span class="sxs-lookup"><span data-stu-id="daf7a-151">1. <b>OSProvisioningInprogress</b> &ndash; The VM is running, and installation of guest OS is in progress.</span></span> <p /> 
<code> "statuses": [<br>
 {<br>
 "code": "ProvisioningState/creating/OSProvisioningInprogress",<br>
 "level": "Info",<br>
 "displayStatus": "OS Provisioning In progress"<br>
 }<br>
]</code><br>
<p><span data-ttu-id="daf7a-152">2. <b>OSProvisioningComplete</b> &ndash; Short-lived state.</span><span class="sxs-lookup"><span data-stu-id="daf7a-152">2. <b>OSProvisioningComplete</b> &ndash; Short-lived state.</span></span> <span data-ttu-id="daf7a-153">The VM quickly transitions to **Success** unless any extensions need to be installed.</span><span class="sxs-lookup"><span data-stu-id="daf7a-153">The VM quickly transitions to **Success** unless any extensions need to be installed.</span></span> <span data-ttu-id="daf7a-154">Installing extensions can take time.</span><span class="sxs-lookup"><span data-stu-id="daf7a-154">Installing extensions can take time.</span></span> <br />
<code> "statuses": [<br>
 {<br>
 "code": "ProvisioningState/creating/OSProvisioningComplete",<br>
 "level": "Info",<br>
 "displayStatus": "OS Provisioning Complete"<br>
 }<br>
]</code><br>
<p><span data-ttu-id="daf7a-155"><b>Note</b>: OS Provisioning can transition to **Failed** if there is an OS failure or the OS doesn't install in time.</span><span class="sxs-lookup"><span data-stu-id="daf7a-155"><b>Note</b>: OS Provisioning can transition to **Failed** if there is an OS failure or the OS doesn't install in time.</span></span> <span data-ttu-id="daf7a-156">Customers will be billed for the deployed VM on the infrastructure.</span><span class="sxs-lookup"><span data-stu-id="daf7a-156">Customers will be billed for the deployed VM on the infrastructure.</span></span></p>
</td>
</tr>
</table>


<span data-ttu-id="daf7a-157">Once the operation is complete, the VM will transition into one of the following states:</span><span class="sxs-lookup"><span data-stu-id="daf7a-157">Once the operation is complete, the VM will transition into one of the following states:</span></span>

- <span data-ttu-id="daf7a-158">**Succeeded** – the user-initiated actions have completed.</span><span class="sxs-lookup"><span data-stu-id="daf7a-158">**Succeeded** – the user-initiated actions have completed.</span></span>

    ```
 "statuses": [ 
 {
     "code": "ProvisioningState/succeeded",
     "level": "Info",
     "displayStatus": "Provisioning succeeded",
     "time": "time"
 }
 ]
    ```

 

- <span data-ttu-id="daf7a-159">**Failed** – represents a failed operation.</span><span class="sxs-lookup"><span data-stu-id="daf7a-159">**Failed** – represents a failed operation.</span></span> <span data-ttu-id="daf7a-160">Refer to the error codes to get more information and possible solutions.</span><span class="sxs-lookup"><span data-stu-id="daf7a-160">Refer to the error codes to get more information and possible solutions.</span></span>

    ```
 "statuses": [
    {
      "code": "ProvisioningState/failed/InternalOperationError",
      "level": "Error",
      "displayStatus": "Provisioning failed",
      "message": "Operation abandoned due to internal error. Please try again later.",
      "time": "time"
    }
    ]
    ```



## <a name="vm-instance-view"></a><span data-ttu-id="daf7a-161">VM instance view</span><span class="sxs-lookup"><span data-stu-id="daf7a-161">VM instance view</span></span>

<span data-ttu-id="daf7a-162">The instance view API provides VM running-state information.</span><span class="sxs-lookup"><span data-stu-id="daf7a-162">The instance view API provides VM running-state information.</span></span> <span data-ttu-id="daf7a-163">For more information, see the [Virtual Machines - Instance View](https://docs.microsoft.com/rest/api/compute/virtualmachines/instanceview) API documentation.</span><span class="sxs-lookup"><span data-stu-id="daf7a-163">For more information, see the [Virtual Machines - Instance View](https://docs.microsoft.com/rest/api/compute/virtualmachines/instanceview) API documentation.</span></span>

<span data-ttu-id="daf7a-164">Azure Resources explorer provides a simple UI for viewing the VM running state: [Resource Explorer] (https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="daf7a-164">Azure Resources explorer provides a simple UI for viewing the VM running state: [Resource Explorer] (https://resources.azure.com/).</span></span>

<span data-ttu-id="daf7a-165">Provisioning states are visible on VM properties and instance view.</span><span class="sxs-lookup"><span data-stu-id="daf7a-165">Provisioning states are visible on VM properties and instance view.</span></span> <span data-ttu-id="daf7a-166">Power states are available in instance view of VM.</span><span class="sxs-lookup"><span data-stu-id="daf7a-166">Power states are available in instance view of VM.</span></span> 

