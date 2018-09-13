---
title: include file
description: include file
services: virtual-machines
author: shants123
ms.service: virtual-machines
ms.topic: include
ms.date: 07/02/2018
ms.author: shants
ms.custom: include file
ms.openlocfilehash: efedb2f48748264fb936fe82a1dbb3cf4403cc5e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969450"
---
## <a name="view-vms-scheduled-for-maintenance-in-the-portal"></a><span data-ttu-id="130ea-103">View VMs scheduled for maintenance in the portal</span><span class="sxs-lookup"><span data-stu-id="130ea-103">View VMs scheduled for maintenance in the portal</span></span>

<span data-ttu-id="130ea-104">Once a planned maintenance wave is scheduled, you can observe the list of virtual machines that are impacted by the upcoming maintenance wave.</span><span class="sxs-lookup"><span data-stu-id="130ea-104">Once a planned maintenance wave is scheduled, you can observe the list of virtual machines that are impacted by the upcoming maintenance wave.</span></span> 

<span data-ttu-id="130ea-105">You can use the Azure portal and look for VMs scheduled for maintenance.</span><span class="sxs-lookup"><span data-stu-id="130ea-105">You can use the Azure portal and look for VMs scheduled for maintenance.</span></span>

1. <span data-ttu-id="130ea-106">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="130ea-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="130ea-107">In the left navigation, click **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="130ea-107">In the left navigation, click **Virtual Machines**.</span></span>

3. <span data-ttu-id="130ea-108">In the Virtual Machines pane, click the **Columns** button to open the list of available columns.</span><span class="sxs-lookup"><span data-stu-id="130ea-108">In the Virtual Machines pane, click the **Columns** button to open the list of available columns.</span></span>

4. <span data-ttu-id="130ea-109">Select and add the following columns:</span><span class="sxs-lookup"><span data-stu-id="130ea-109">Select and add the following columns:</span></span>

   <span data-ttu-id="130ea-110">**Maintenance**: Shows the maintenance status for the VM.</span><span class="sxs-lookup"><span data-stu-id="130ea-110">**Maintenance**: Shows the maintenance status for the VM.</span></span> <span data-ttu-id="130ea-111">The following are the potential values:</span><span class="sxs-lookup"><span data-stu-id="130ea-111">The following are the potential values:</span></span>
      
      | <span data-ttu-id="130ea-112">Value</span><span class="sxs-lookup"><span data-stu-id="130ea-112">Value</span></span> | <span data-ttu-id="130ea-113">Description</span><span class="sxs-lookup"><span data-stu-id="130ea-113">Description</span></span> |
      |-------|-------------|
      | <span data-ttu-id="130ea-114">Start now</span><span class="sxs-lookup"><span data-stu-id="130ea-114">Start now</span></span> | <span data-ttu-id="130ea-115">The VM is in the self-service maintenance window that lets you initiate the maintenance yourself.</span><span class="sxs-lookup"><span data-stu-id="130ea-115">The VM is in the self-service maintenance window that lets you initiate the maintenance yourself.</span></span> <span data-ttu-id="130ea-116">See below on how to start maintenance on your VM.</span><span class="sxs-lookup"><span data-stu-id="130ea-116">See below on how to start maintenance on your VM.</span></span> | 
      | <span data-ttu-id="130ea-117">Scheduled</span><span class="sxs-lookup"><span data-stu-id="130ea-117">Scheduled</span></span> | <span data-ttu-id="130ea-118">The VM is scheduled for maintenance with no option for you to initiate maintenance.</span><span class="sxs-lookup"><span data-stu-id="130ea-118">The VM is scheduled for maintenance with no option for you to initiate maintenance.</span></span> <span data-ttu-id="130ea-119">You can learn of the maintenance window by selecting the Maintenance - Scheduled window in this view or by clicking on the VM.</span><span class="sxs-lookup"><span data-stu-id="130ea-119">You can learn of the maintenance window by selecting the Maintenance - Scheduled window in this view or by clicking on the VM.</span></span> | 
      | <span data-ttu-id="130ea-120">Already updated</span><span class="sxs-lookup"><span data-stu-id="130ea-120">Already updated</span></span> | <span data-ttu-id="130ea-121">Your VM is already updated and no further action is required at this time.</span><span class="sxs-lookup"><span data-stu-id="130ea-121">Your VM is already updated and no further action is required at this time.</span></span> | 
      | <span data-ttu-id="130ea-122">Retry later</span><span class="sxs-lookup"><span data-stu-id="130ea-122">Retry later</span></span> | <span data-ttu-id="130ea-123">You have initiated maintenance with no success.</span><span class="sxs-lookup"><span data-stu-id="130ea-123">You have initiated maintenance with no success.</span></span> <span data-ttu-id="130ea-124">You will be able to use the self-service maintenance option at a later time.</span><span class="sxs-lookup"><span data-stu-id="130ea-124">You will be able to use the self-service maintenance option at a later time.</span></span> | 
      | <span data-ttu-id="130ea-125">Retry now</span><span class="sxs-lookup"><span data-stu-id="130ea-125">Retry now</span></span> | <span data-ttu-id="130ea-126">You can retry a previously unsuccessful self-initiated maintenance.</span><span class="sxs-lookup"><span data-stu-id="130ea-126">You can retry a previously unsuccessful self-initiated maintenance.</span></span> | 
      | - | <span data-ttu-id="130ea-127">Your virtual machine is not part of a planned maintenance wave.</span><span class="sxs-lookup"><span data-stu-id="130ea-127">Your virtual machine is not part of a planned maintenance wave.</span></span> |
      

   <span data-ttu-id="130ea-128">**Maintenance - Self-service window**: Shows the time window when you can self-start maintenance on your VMs.</span><span class="sxs-lookup"><span data-stu-id="130ea-128">**Maintenance - Self-service window**: Shows the time window when you can self-start maintenance on your VMs.</span></span>
   
   <span data-ttu-id="130ea-129">**Maintenance - Scheduled window**: Shows the time window when Azure will maintain your VM in order to complete maintenance.</span><span class="sxs-lookup"><span data-stu-id="130ea-129">**Maintenance - Scheduled window**: Shows the time window when Azure will maintain your VM in order to complete maintenance.</span></span> 



## <a name="notification-and-alerts-in-the-portal"></a><span data-ttu-id="130ea-130">Notification and alerts in the portal</span><span class="sxs-lookup"><span data-stu-id="130ea-130">Notification and alerts in the portal</span></span>

<span data-ttu-id="130ea-131">Azure communicates a schedule for planned maintenance by sending an email to the subscription owner and co-owners group.</span><span class="sxs-lookup"><span data-stu-id="130ea-131">Azure communicates a schedule for planned maintenance by sending an email to the subscription owner and co-owners group.</span></span> <span data-ttu-id="130ea-132">You can add additional recipients and channels to this communication by creating Azure activity log alerts.</span><span class="sxs-lookup"><span data-stu-id="130ea-132">You can add additional recipients and channels to this communication by creating Azure activity log alerts.</span></span> <span data-ttu-id="130ea-133">For more information, see [Monitor subscription activity with the Azure Activity Log] (../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="130ea-133">For more information, see [Monitor subscription activity with the Azure Activity Log] (../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

1. <span data-ttu-id="130ea-134">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="130ea-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="130ea-135">In the menu on the left, select **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="130ea-135">In the menu on the left, select **Monitor**.</span></span> 
3. <span data-ttu-id="130ea-136">In the **Monitor - Alerts (classic)** pane, click **+ Add activity log alert**.</span><span class="sxs-lookup"><span data-stu-id="130ea-136">In the **Monitor - Alerts (classic)** pane, click **+ Add activity log alert**.</span></span>
5. <span data-ttu-id="130ea-137">Complete the information in the **Add activity log alert** page and make sure you set the following in **Criteria**:</span><span class="sxs-lookup"><span data-stu-id="130ea-137">Complete the information in the **Add activity log alert** page and make sure you set the following in **Criteria**:</span></span>
   - <span data-ttu-id="130ea-138">**Event category**: Service Health</span><span class="sxs-lookup"><span data-stu-id="130ea-138">**Event category**: Service Health</span></span>
   - <span data-ttu-id="130ea-139">**Services**: Virtual Machine Scale Sets and Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="130ea-139">**Services**: Virtual Machine Scale Sets and Virtual Machines</span></span>
   - <span data-ttu-id="130ea-140">**Type**: Planned maintenance</span><span class="sxs-lookup"><span data-stu-id="130ea-140">**Type**: Planned maintenance</span></span> 
    
<span data-ttu-id="130ea-141">To learn more on how to configure Activity Log Alerts, see [Create activity log alerts](../articles/monitoring-and-diagnostics/monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="130ea-141">To learn more on how to configure Activity Log Alerts, see [Create activity log alerts](../articles/monitoring-and-diagnostics/monitoring-activity-log-alerts.md).</span></span>
    
    
## <a name="start-maintenance-on-your-vm-from-the-portal"></a><span data-ttu-id="130ea-142">Start Maintenance on your VM from the portal</span><span class="sxs-lookup"><span data-stu-id="130ea-142">Start Maintenance on your VM from the portal</span></span>

<span data-ttu-id="130ea-143">While looking at the VM details, you will be able to see more maintenance-related details.</span><span class="sxs-lookup"><span data-stu-id="130ea-143">While looking at the VM details, you will be able to see more maintenance-related details.</span></span>  
<span data-ttu-id="130ea-144">At the top of the VM details view, a new notification ribbon will be added if your VM is included in a planned maintenance wave.</span><span class="sxs-lookup"><span data-stu-id="130ea-144">At the top of the VM details view, a new notification ribbon will be added if your VM is included in a planned maintenance wave.</span></span> <span data-ttu-id="130ea-145">In addition, a new option is added to start maintenance when possible.</span><span class="sxs-lookup"><span data-stu-id="130ea-145">In addition, a new option is added to start maintenance when possible.</span></span> 


<span data-ttu-id="130ea-146">Click on the maintenance notification to see the maintenance page with more details on the planned maintenance.</span><span class="sxs-lookup"><span data-stu-id="130ea-146">Click on the maintenance notification to see the maintenance page with more details on the planned maintenance.</span></span> <span data-ttu-id="130ea-147">From there, you will be able to **start maintenance** on your VM.</span><span class="sxs-lookup"><span data-stu-id="130ea-147">From there, you will be able to **start maintenance** on your VM.</span></span>

<span data-ttu-id="130ea-148">Once you start maintenance, your virtual machine will be maintained and the maintenance status will be updated to reflect the result within few minutes.</span><span class="sxs-lookup"><span data-stu-id="130ea-148">Once you start maintenance, your virtual machine will be maintained and the maintenance status will be updated to reflect the result within few minutes.</span></span>

<span data-ttu-id="130ea-149">If you missed the self-service window, you will still be able to see the window when your VM will be maintained by Azure.</span><span class="sxs-lookup"><span data-stu-id="130ea-149">If you missed the self-service window, you will still be able to see the window when your VM will be maintained by Azure.</span></span> 
