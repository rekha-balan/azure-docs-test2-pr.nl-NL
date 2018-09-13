---
title: Quota types in Azure Stack | Microsoft Docs
description: Review the different quota types available for services and resources in Azure Stack.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2018
ms.author: brenduns
ms.reviewer: xiaofmao
ms.openlocfilehash: 2e884164347239838d08fbbc1616ed54ffc4ff24
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966112"
---
# <a name="quota-types-in-azure-stack"></a><span data-ttu-id="d4de3-103">Quota types in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d4de3-103">Quota types in Azure Stack</span></span>

<span data-ttu-id="d4de3-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="d4de3-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="d4de3-105">[Quotas](azure-stack-plan-offer-quota-overview.md#plans) define the limits of resources that a user subscription can provision or consume.</span><span class="sxs-lookup"><span data-stu-id="d4de3-105">[Quotas](azure-stack-plan-offer-quota-overview.md#plans) define the limits of resources that a user subscription can provision or consume.</span></span> <span data-ttu-id="d4de3-106">For example, a quota might allow a user to create up to five VMs.</span><span class="sxs-lookup"><span data-stu-id="d4de3-106">For example, a quota might allow a user to create up to five VMs.</span></span> <span data-ttu-id="d4de3-107">Each resource can have its own types of quotas.</span><span class="sxs-lookup"><span data-stu-id="d4de3-107">Each resource can have its own types of quotas.</span></span>

## <a name="compute-quota-types"></a><span data-ttu-id="d4de3-108">Compute quota types</span><span class="sxs-lookup"><span data-stu-id="d4de3-108">Compute quota types</span></span> 
| <span data-ttu-id="d4de3-109">**Type**</span><span class="sxs-lookup"><span data-stu-id="d4de3-109">**Type**</span></span> | <span data-ttu-id="d4de3-110">**Default value**</span><span class="sxs-lookup"><span data-stu-id="d4de3-110">**Default value**</span></span> | <span data-ttu-id="d4de3-111">**Description**</span><span class="sxs-lookup"><span data-stu-id="d4de3-111">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4de3-112">Max number of virtual machines</span><span class="sxs-lookup"><span data-stu-id="d4de3-112">Max number of virtual machines</span></span> | <span data-ttu-id="d4de3-113">20</span><span class="sxs-lookup"><span data-stu-id="d4de3-113">20</span></span> | <span data-ttu-id="d4de3-114">The maximum number of virtual machines that a subscription can create in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-114">The maximum number of virtual machines that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d4de3-115">Max number of virtual machine cores</span><span class="sxs-lookup"><span data-stu-id="d4de3-115">Max number of virtual machine cores</span></span> | <span data-ttu-id="d4de3-116">50</span><span class="sxs-lookup"><span data-stu-id="d4de3-116">50</span></span> | <span data-ttu-id="d4de3-117">The maximum number of cores that a subscription can create in this location (for example, an A3 VM has four cores).</span><span class="sxs-lookup"><span data-stu-id="d4de3-117">The maximum number of cores that a subscription can create in this location (for example, an A3 VM has four cores).</span></span> |
| <span data-ttu-id="d4de3-118">Max number of availability sets</span><span class="sxs-lookup"><span data-stu-id="d4de3-118">Max number of availability sets</span></span> | <span data-ttu-id="d4de3-119">10</span><span class="sxs-lookup"><span data-stu-id="d4de3-119">10</span></span> | <span data-ttu-id="d4de3-120">The maximum number of availability sets that can be created in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-120">The maximum number of availability sets that can be created in this location.</span></span> |
| <span data-ttu-id="d4de3-121">Max number of virtual machine scale sets</span><span class="sxs-lookup"><span data-stu-id="d4de3-121">Max number of virtual machine scale sets</span></span> | <span data-ttu-id="d4de3-122">20</span><span class="sxs-lookup"><span data-stu-id="d4de3-122">20</span></span> | <span data-ttu-id="d4de3-123">The maximum number of virtual machine scale sets that can be created in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-123">The maximum number of virtual machine scale sets that can be created in this location.</span></span> |

## <a name="storage-quota-types"></a><span data-ttu-id="d4de3-124">Storage quota types</span><span class="sxs-lookup"><span data-stu-id="d4de3-124">Storage quota types</span></span> 
| <span data-ttu-id="d4de3-125">**Item**</span><span class="sxs-lookup"><span data-stu-id="d4de3-125">**Item**</span></span> | <span data-ttu-id="d4de3-126">**Default value**</span><span class="sxs-lookup"><span data-stu-id="d4de3-126">**Default value**</span></span> | <span data-ttu-id="d4de3-127">**Description**</span><span class="sxs-lookup"><span data-stu-id="d4de3-127">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4de3-128">Maximum capacity (GB)</span><span class="sxs-lookup"><span data-stu-id="d4de3-128">Maximum capacity (GB)</span></span> |<span data-ttu-id="d4de3-129">500</span><span class="sxs-lookup"><span data-stu-id="d4de3-129">500</span></span> |<span data-ttu-id="d4de3-130">Total storage capacity that can be consumed by a subscription in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-130">Total storage capacity that can be consumed by a subscription in this location.</span></span> |
| <span data-ttu-id="d4de3-131">Total number of storage accounts</span><span class="sxs-lookup"><span data-stu-id="d4de3-131">Total number of storage accounts</span></span> |<span data-ttu-id="d4de3-132">20</span><span class="sxs-lookup"><span data-stu-id="d4de3-132">20</span></span> |<span data-ttu-id="d4de3-133">The maximum number of storage accounts that a subscription can create in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-133">The maximum number of storage accounts that a subscription can create in this location.</span></span> |

> [!NOTE]  
> <span data-ttu-id="d4de3-134">It can take up to two hours before a storage quota is enforced.</span><span class="sxs-lookup"><span data-stu-id="d4de3-134">It can take up to two hours before a storage quota is enforced.</span></span>


## <a name="network-quota-types"></a><span data-ttu-id="d4de3-135">Network quota types</span><span class="sxs-lookup"><span data-stu-id="d4de3-135">Network quota types</span></span>
| <span data-ttu-id="d4de3-136">**Item**</span><span class="sxs-lookup"><span data-stu-id="d4de3-136">**Item**</span></span> | <span data-ttu-id="d4de3-137">**Default value**</span><span class="sxs-lookup"><span data-stu-id="d4de3-137">**Default value**</span></span> | <span data-ttu-id="d4de3-138">**Description**</span><span class="sxs-lookup"><span data-stu-id="d4de3-138">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4de3-139">Max public IPs</span><span class="sxs-lookup"><span data-stu-id="d4de3-139">Max public IPs</span></span> |<span data-ttu-id="d4de3-140">50</span><span class="sxs-lookup"><span data-stu-id="d4de3-140">50</span></span> |<span data-ttu-id="d4de3-141">The maximum number of public IPs that a subscription can create in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-141">The maximum number of public IPs that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d4de3-142">Max virtual networks</span><span class="sxs-lookup"><span data-stu-id="d4de3-142">Max virtual networks</span></span> |<span data-ttu-id="d4de3-143">50</span><span class="sxs-lookup"><span data-stu-id="d4de3-143">50</span></span> |<span data-ttu-id="d4de3-144">The maximum number of virtual networks that a subscription can create in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-144">The maximum number of virtual networks that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d4de3-145">Max virtual network gateways</span><span class="sxs-lookup"><span data-stu-id="d4de3-145">Max virtual network gateways</span></span> |<span data-ttu-id="d4de3-146">1</span><span class="sxs-lookup"><span data-stu-id="d4de3-146">1</span></span> |<span data-ttu-id="d4de3-147">The maximum number of virtual network gateways (VPN Gateways) that a subscription can create in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-147">The maximum number of virtual network gateways (VPN Gateways) that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d4de3-148">Max network connections</span><span class="sxs-lookup"><span data-stu-id="d4de3-148">Max network connections</span></span> |<span data-ttu-id="d4de3-149">2</span><span class="sxs-lookup"><span data-stu-id="d4de3-149">2</span></span> |<span data-ttu-id="d4de3-150">The maximum number of network connections (point-to-point or site-to-site) that a subscription can create across all virtual network gateways in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-150">The maximum number of network connections (point-to-point or site-to-site) that a subscription can create across all virtual network gateways in this location.</span></span> |
| <span data-ttu-id="d4de3-151">Max load balancers</span><span class="sxs-lookup"><span data-stu-id="d4de3-151">Max load balancers</span></span> |<span data-ttu-id="d4de3-152">50</span><span class="sxs-lookup"><span data-stu-id="d4de3-152">50</span></span> |<span data-ttu-id="d4de3-153">The maximum number of load balancers that a subscription can create in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-153">The maximum number of load balancers that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d4de3-154">Max NICs</span><span class="sxs-lookup"><span data-stu-id="d4de3-154">Max NICs</span></span> |<span data-ttu-id="d4de3-155">100</span><span class="sxs-lookup"><span data-stu-id="d4de3-155">100</span></span> |<span data-ttu-id="d4de3-156">The maximum number of network interfaces that a subscription can create in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-156">The maximum number of network interfaces that a subscription can create in this location.</span></span> |
| <span data-ttu-id="d4de3-157">Max network security groups</span><span class="sxs-lookup"><span data-stu-id="d4de3-157">Max network security groups</span></span> |<span data-ttu-id="d4de3-158">50</span><span class="sxs-lookup"><span data-stu-id="d4de3-158">50</span></span> |<span data-ttu-id="d4de3-159">The maximum number of network security groups that a subscription can create in this location.</span><span class="sxs-lookup"><span data-stu-id="d4de3-159">The maximum number of network security groups that a subscription can create in this location.</span></span> |

## <a name="view-an-existing-quota"></a><span data-ttu-id="d4de3-160">View an existing quota</span><span class="sxs-lookup"><span data-stu-id="d4de3-160">View an existing quota</span></span>
1. <span data-ttu-id="d4de3-161">On the default dashboard of the Admin portal, find the **Resource providers** tile.</span><span class="sxs-lookup"><span data-stu-id="d4de3-161">On the default dashboard of the Admin portal, find the **Resource providers** tile.</span></span>
2. <span data-ttu-id="d4de3-162">Select the service with the quota that you want to view, like **Compute** or **Storage**.</span><span class="sxs-lookup"><span data-stu-id="d4de3-162">Select the service with the quota that you want to view, like **Compute** or **Storage**.</span></span>
3. <span data-ttu-id="d4de3-163">Select **Quotas**, and then select the quota you want to view.</span><span class="sxs-lookup"><span data-stu-id="d4de3-163">Select **Quotas**, and then select the quota you want to view.</span></span>


## <a name="edit-a-quota"></a><span data-ttu-id="d4de3-164">Edit a quota</span><span class="sxs-lookup"><span data-stu-id="d4de3-164">Edit a quota</span></span>  
<span data-ttu-id="d4de3-165">You can choose to edit the original configuration of a quota instead of [using an add-on plan](create-add-on-plan.md).</span><span class="sxs-lookup"><span data-stu-id="d4de3-165">You can choose to edit the original configuration of a quota instead of [using an add-on plan](create-add-on-plan.md).</span></span> <span data-ttu-id="d4de3-166">When you edit a quota, the new configuration automatically applies globally to all plans that use that quota and all existing subscriptions that use those plans.</span><span class="sxs-lookup"><span data-stu-id="d4de3-166">When you edit a quota, the new configuration automatically applies globally to all plans that use that quota and all existing subscriptions that use those plans.</span></span> <span data-ttu-id="d4de3-167">The editing of a quota is different than when you use an add-on plan to provide a modified quota, which a user chooses to subscribe to.</span><span class="sxs-lookup"><span data-stu-id="d4de3-167">The editing of a quota is different than when you use an add-on plan to provide a modified quota, which a user chooses to subscribe to.</span></span> 

### <a name="to-edit-a-quota"></a><span data-ttu-id="d4de3-168">To edit a quota</span><span class="sxs-lookup"><span data-stu-id="d4de3-168">To edit a quota</span></span>  
1. <span data-ttu-id="d4de3-169">On the default dashboard of the Admin portal, find the **Resource providers** tile.</span><span class="sxs-lookup"><span data-stu-id="d4de3-169">On the default dashboard of the Admin portal, find the **Resource providers** tile.</span></span>
2. <span data-ttu-id="d4de3-170">Select the service with the quota that you want to modify, like **Compute**, **Network**, or **Storage**.</span><span class="sxs-lookup"><span data-stu-id="d4de3-170">Select the service with the quota that you want to modify, like **Compute**, **Network**, or **Storage**.</span></span>
3. <span data-ttu-id="d4de3-171">Next, select **Quotas**, and then select the quota you want to change.</span><span class="sxs-lookup"><span data-stu-id="d4de3-171">Next, select **Quotas**, and then select the quota you want to change.</span></span>
4. <span data-ttu-id="d4de3-172">On the **Set quotas** pane, edit the values, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d4de3-172">On the **Set quotas** pane, edit the values, and then select **Save**.</span></span> 

<span data-ttu-id="d4de3-173">The new values for the quota apply globally to all plans that use the modified quota and to all existing subscriptions that use those plans.</span><span class="sxs-lookup"><span data-stu-id="d4de3-173">The new values for the quota apply globally to all plans that use the modified quota and to all existing subscriptions that use those plans.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="d4de3-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="d4de3-174">Next steps</span></span>

- [<span data-ttu-id="d4de3-175">Learn more about plans, offers, and quotas.</span><span class="sxs-lookup"><span data-stu-id="d4de3-175">Learn more about plans, offers, and quotas.</span></span>](azure-stack-plan-offer-quota-overview.md)
- [<span data-ttu-id="d4de3-176">Create quotas while creating a plan.</span><span class="sxs-lookup"><span data-stu-id="d4de3-176">Create quotas while creating a plan.</span></span>](azure-stack-create-plan.md)
