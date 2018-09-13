---
title: Manage Azure Reservations | Microsoft Docs
description: Learn how you can change subscription scope and manage access for Azure Reservations.
services: billing
documentationcenter: ''
author: yashesvi
manager: yashesvi
editor: ''
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2018
ms.author: yashesvi
ms.openlocfilehash: 3e5316ac0ca20c58a0960818d3151c238927df0d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866173"
---
# <a name="manage-reservations-for-azure-resources"></a><span data-ttu-id="3e4b4-103">Manage Reservations for Azure resources</span><span class="sxs-lookup"><span data-stu-id="3e4b4-103">Manage Reservations for Azure resources</span></span>

<span data-ttu-id="3e4b4-104">After you buy an Azure Reservation, you may need to apply the reservation to a different subscription, change who can manage the reservation, or change the scope of the reservation.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-104">After you buy an Azure Reservation, you may need to apply the reservation to a different subscription, change who can manage the reservation, or change the scope of the reservation.</span></span> <span data-ttu-id="3e4b4-105">You can also split a reservation into two reservations to apply some of the instances you bought to another subscription.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-105">You can also split a reservation into two reservations to apply some of the instances you bought to another subscription.</span></span>

<span data-ttu-id="3e4b4-106">If you bought Azure Reserved Virtual Machine Instances, you can change the optimize setting for the reservation.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-106">If you bought Azure Reserved Virtual Machine Instances, you can change the optimize setting for the reservation.</span></span> <span data-ttu-id="3e4b4-107">The reservation discount can apply to VMs in the same series or you can reserve data center capacity for a specific VM size.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-107">The reservation discount can apply to VMs in the same series or you can reserve data center capacity for a specific VM size.</span></span>

## <a name="change-the-scope-for-a-reservation"></a><span data-ttu-id="3e4b4-108">Change the scope for a reservation</span><span class="sxs-lookup"><span data-stu-id="3e4b4-108">Change the scope for a reservation</span></span>

 <span data-ttu-id="3e4b4-109">Your reservation discount applies to virtual machines, SQL databases, or other resources that match your reservation and run within the reservation scope.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-109">Your reservation discount applies to virtual machines, SQL databases, or other resources that match your reservation and run within the reservation scope.</span></span> <span data-ttu-id="3e4b4-110">The scope of a reservation can be single subscription or all subscriptions in your billing context.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-110">The scope of a reservation can be single subscription or all subscriptions in your billing context.</span></span> <span data-ttu-id="3e4b4-111">If you set the scope to single subscription, the reservation is matched to running resources in the selected subscription.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-111">If you set the scope to single subscription, the reservation is matched to running resources in the selected subscription.</span></span> <span data-ttu-id="3e4b4-112">If you set the scope to shared, Azure matches the reservation to resources that run in all the subscriptions within the billing context.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-112">If you set the scope to shared, Azure matches the reservation to resources that run in all the subscriptions within the billing context.</span></span> <span data-ttu-id="3e4b4-113">The billing context is dependent on the subscription used to buy the reservation.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-113">The billing context is dependent on the subscription used to buy the reservation.</span></span>

<span data-ttu-id="3e4b4-114">To update the scope of a reservation:</span><span class="sxs-lookup"><span data-stu-id="3e4b4-114">To update the scope of a reservation:</span></span>

1. <span data-ttu-id="3e4b4-115">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3e4b4-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3e4b4-116">Select **All services** > **Reservations**.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-116">Select **All services** > **Reservations**.</span></span>
3. <span data-ttu-id="3e4b4-117">Select the reservation.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-117">Select the reservation.</span></span>
4. <span data-ttu-id="3e4b4-118">Select **Settings** > **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-118">Select **Settings** > **Configuration**.</span></span>
5. <span data-ttu-id="3e4b4-119">Change the scope.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-119">Change the scope.</span></span> 

<span data-ttu-id="3e4b4-120">If you change from shared to single scope, you can only select subscriptions where you are the owner.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-120">If you change from shared to single scope, you can only select subscriptions where you are the owner.</span></span> <span data-ttu-id="3e4b4-121">Only subscriptions within the same billing context as the reservation, can be selected.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-121">Only subscriptions within the same billing context as the reservation, can be selected.</span></span>

<span data-ttu-id="3e4b4-122">The scope only applies to Pay-As-You-Go offer MS-AZR-0003P, Enterprise offer MS-AZR-0017P, or CSP subscription types.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-122">The scope only applies to Pay-As-You-Go offer MS-AZR-0003P, Enterprise offer MS-AZR-0017P, or CSP subscription types.</span></span> <span data-ttu-id="3e4b4-123">For enterprise agreements, dev/test subscriptions are not eligible to get the reservation discount.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-123">For enterprise agreements, dev/test subscriptions are not eligible to get the reservation discount.</span></span>

## <a name="add-or-change-users-who-can-manage-a-reservation"></a><span data-ttu-id="3e4b4-124">Add or change users who can manage a reservation</span><span class="sxs-lookup"><span data-stu-id="3e4b4-124">Add or change users who can manage a reservation</span></span>

<span data-ttu-id="3e4b4-125">You can delegate management of a reservation by adding people to roles on the reservation.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-125">You can delegate management of a reservation by adding people to roles on the reservation.</span></span> <span data-ttu-id="3e4b4-126">By default, the person that bought the reservation and the account administrator have the Owner role on the reservation.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-126">By default, the person that bought the reservation and the account administrator have the Owner role on the reservation.</span></span>

<span data-ttu-id="3e4b4-127">You can manage access to reservations independently from the subscriptions that get the reservation discount.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-127">You can manage access to reservations independently from the subscriptions that get the reservation discount.</span></span> <span data-ttu-id="3e4b4-128">When you give someone permissions to manage a reservation, that doesn't give them rights to manage the subscription.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-128">When you give someone permissions to manage a reservation, that doesn't give them rights to manage the subscription.</span></span> <span data-ttu-id="3e4b4-129">And if you give someone permissions to manage a subscription within the reservation's scope, that doesn't give them rights to manage the reservation.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-129">And if you give someone permissions to manage a subscription within the reservation's scope, that doesn't give them rights to manage the reservation.</span></span>

<span data-ttu-id="3e4b4-130">To delegate access management for a reservation:</span><span class="sxs-lookup"><span data-stu-id="3e4b4-130">To delegate access management for a reservation:</span></span>

1. <span data-ttu-id="3e4b4-131">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3e4b4-131">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3e4b4-132">Select **All Services** > **Reservation** to list reservations that you have access to.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-132">Select **All Services** > **Reservation** to list reservations that you have access to.</span></span>
3. <span data-ttu-id="3e4b4-133">Select the reservation that you want to delegate access to other users.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-133">Select the reservation that you want to delegate access to other users.</span></span>
4. <span data-ttu-id="3e4b4-134">Select **Access Control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-134">Select **Access Control (IAM)**.</span></span>
5. <span data-ttu-id="3e4b4-135">Select **Add** > **Role** > **Owner**.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-135">Select **Add** > **Role** > **Owner**.</span></span> <span data-ttu-id="3e4b4-136">Or, if you want to give limited access, select a different role.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-136">Or, if you want to give limited access, select a different role.</span></span>
6. <span data-ttu-id="3e4b4-137">Type the email address of the user you want to add as owner.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-137">Type the email address of the user you want to add as owner.</span></span>
7. <span data-ttu-id="3e4b4-138">Select the user, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-138">Select the user, and then select **Save**.</span></span>

## <a name="split-a-single-reservation-into-two-reservations"></a><span data-ttu-id="3e4b4-139">Split a single reservation into two reservations</span><span class="sxs-lookup"><span data-stu-id="3e4b4-139">Split a single reservation into two reservations</span></span>

 <span data-ttu-id="3e4b4-140">After you buy more than one resource instance within a reservation, you may want to assign instances within that reservation to different subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-140">After you buy more than one resource instance within a reservation, you may want to assign instances within that reservation to different subscriptions.</span></span> <span data-ttu-id="3e4b4-141">By default, all instances have one scope - either single subscription or shared.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-141">By default, all instances have one scope - either single subscription or shared.</span></span> <span data-ttu-id="3e4b4-142">For example, you bought 10 reservation instances and specified the scope to be subscription A. You may now want to change the scope for 7 reservations to subscription A and the remaining 3 to subscription B. Splitting a reservation allows you to distribute instances for granular scope management.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-142">For example, you bought 10 reservation instances and specified the scope to be subscription A. You may now want to change the scope for 7 reservations to subscription A and the remaining 3 to subscription B. Splitting a reservation allows you to distribute instances for granular scope management.</span></span> <span data-ttu-id="3e4b4-143">You can simplify the allocation to subscriptions by choosing shared scope.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-143">You can simplify the allocation to subscriptions by choosing shared scope.</span></span> <span data-ttu-id="3e4b4-144">But for cost management or budgeting purposes, you can allocate quantities to specific subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-144">But for cost management or budgeting purposes, you can allocate quantities to specific subscriptions.</span></span>

 <span data-ttu-id="3e4b4-145">You can split a reservation into two reservations though PowerShell, CLI, or through the API.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-145">You can split a reservation into two reservations though PowerShell, CLI, or through the API.</span></span>

### <a name="split-a-reservation-by-using-powershell"></a><span data-ttu-id="3e4b4-146">Split a reservation by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e4b4-146">Split a reservation by using PowerShell</span></span>

1. <span data-ttu-id="3e4b4-147">Get the reservation order ID by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3e4b4-147">Get the reservation order ID by running the following command:</span></span>

    ```powershell
    # Get the reservation orders you have access to
    Get-AzureRmReservationOrder
    ```

2. <span data-ttu-id="3e4b4-148">Get the details of a reservation:</span><span class="sxs-lookup"><span data-stu-id="3e4b4-148">Get the details of a reservation:</span></span>

    ```powershell
    Get-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId b8be062a-fb0a-46c1-808a-5a844714965a
    ```

3. <span data-ttu-id="3e4b4-149">Split the reservation into two and distribute the instances:</span><span class="sxs-lookup"><span data-stu-id="3e4b4-149">Split the reservation into two and distribute the instances:</span></span>

    ```powershell
    # Split the reservation. The sum of the reservations, the quantity, must equal the total number of instances in the reservation that you're splitting.
    Split-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId b8be062a-fb0a-46c1-808a-5a844714965a -Quantity 3,2
    ```
4. <span data-ttu-id="3e4b4-150">You can update the scope by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3e4b4-150">You can update the scope by running the following command:</span></span>

    ```powershell
    Update-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId 5257501b-d3e8-449d-a1ab-4879b1863aca -AppliedScopeType Single -AppliedScope /subscriptions/15bb3be0-76d5-491c-8078-61fe3468d414
    ```

## <a name="cancellations-and-exchanges"></a><span data-ttu-id="3e4b4-151">Cancellations and exchanges</span><span class="sxs-lookup"><span data-stu-id="3e4b4-151">Cancellations and exchanges</span></span>

<span data-ttu-id="3e4b4-152">Depending on the reservation type, you may be able to cancel or exchange a reservation.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-152">Depending on the reservation type, you may be able to cancel or exchange a reservation.</span></span> <span data-ttu-id="3e4b4-153">For more information, see the cancellation and exchanges sections in the following topics:</span><span class="sxs-lookup"><span data-stu-id="3e4b4-153">For more information, see the cancellation and exchanges sections in the following topics:</span></span>

- [<span data-ttu-id="3e4b4-154">Prepay for Virtual Machines with Azure Reserved VM Instances</span><span class="sxs-lookup"><span data-stu-id="3e4b4-154">Prepay for Virtual Machines with Azure Reserved VM Instances</span></span>](..//virtual-machines/windows/prepay-reserved-vm-instances.md#cancellations-and-exchanges)
- [<span data-ttu-id="3e4b4-155">Prepay for SUSE software plans from Azure Reservations</span><span class="sxs-lookup"><span data-stu-id="3e4b4-155">Prepay for SUSE software plans from Azure Reservations</span></span>](../virtual-machines/linux/prepay-suse-software-charges.md#cancellation-and-exchanges-not-allowed)
- [<span data-ttu-id="3e4b4-156">Prepay for SQL Database compute resources with Azure SQL Database reserved capacity</span><span class="sxs-lookup"><span data-stu-id="3e4b4-156">Prepay for SQL Database compute resources with Azure SQL Database reserved capacity</span></span>](../sql-database/sql-database-reserved-capacity.md#cancellations-and-exchanges)

## <a name="change-optimize-setting-for-reserved-vm-instances"></a><span data-ttu-id="3e4b4-157">Change optimize setting for Reserved VM Instances</span><span class="sxs-lookup"><span data-stu-id="3e4b4-157">Change optimize setting for Reserved VM Instances</span></span>

 <span data-ttu-id="3e4b4-158">When you buy a Reserved VM Instance, you choose instance size flexibility or capacity priority.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-158">When you buy a Reserved VM Instance, you choose instance size flexibility or capacity priority.</span></span> <span data-ttu-id="3e4b4-159">Instance size flexibility applies the reservation discount to other VMs in the same [VM size group](https://aka.ms/RIVMGroups).</span><span class="sxs-lookup"><span data-stu-id="3e4b4-159">Instance size flexibility applies the reservation discount to other VMs in the same [VM size group](https://aka.ms/RIVMGroups).</span></span> <span data-ttu-id="3e4b4-160">Capacity priority prioritizes data center capacity for your deployments.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-160">Capacity priority prioritizes data center capacity for your deployments.</span></span> <span data-ttu-id="3e4b4-161">This option offers additional confidence in your ability to launch the VM instances when you need them.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-161">This option offers additional confidence in your ability to launch the VM instances when you need them.</span></span>

<span data-ttu-id="3e4b4-162">By default, when the scope of the reservation is shared, the instance size flexibility is on.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-162">By default, when the scope of the reservation is shared, the instance size flexibility is on.</span></span> <span data-ttu-id="3e4b4-163">The data center capacity isn't prioritized for VM deployments.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-163">The data center capacity isn't prioritized for VM deployments.</span></span>

<span data-ttu-id="3e4b4-164">For reservations where the scope is single, you can optimize the reservation for capacity priority instead of VM instance size flexibility.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-164">For reservations where the scope is single, you can optimize the reservation for capacity priority instead of VM instance size flexibility.</span></span>

<span data-ttu-id="3e4b4-165">To update the optimize setting for the reservation:</span><span class="sxs-lookup"><span data-stu-id="3e4b4-165">To update the optimize setting for the reservation:</span></span>

1. <span data-ttu-id="3e4b4-166">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3e4b4-166">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3e4b4-167">Select **All Services** > **Reservations**.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-167">Select **All Services** > **Reservations**.</span></span>
3. <span data-ttu-id="3e4b4-168">Select the reservation.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-168">Select the reservation.</span></span>
4. <span data-ttu-id="3e4b4-169">Select **Settings** > **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-169">Select **Settings** > **Configuration**.</span></span>
5. <span data-ttu-id="3e4b4-170">Change the **Optimize for** setting.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-170">Change the **Optimize for** setting.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e4b4-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="3e4b4-171">Next steps</span></span>

<span data-ttu-id="3e4b4-172">To learn more about Azure Reservations, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="3e4b4-172">To learn more about Azure Reservations, see the following articles:</span></span>

- [<span data-ttu-id="3e4b4-173">What are Azure Reservations?</span><span class="sxs-lookup"><span data-stu-id="3e4b4-173">What are Azure Reservations?</span></span>](billing-save-compute-costs-reservations.md)
- [<span data-ttu-id="3e4b4-174">Prepay for Virtual Machines with Azure Reserved VM Instances</span><span class="sxs-lookup"><span data-stu-id="3e4b4-174">Prepay for Virtual Machines with Azure Reserved VM Instances</span></span>](../virtual-machines/windows/prepay-reserved-vm-instances.md)
- [<span data-ttu-id="3e4b4-175">Prepay for SQL Database compute resources with Azure SQL Database reserved capacity</span><span class="sxs-lookup"><span data-stu-id="3e4b4-175">Prepay for SQL Database compute resources with Azure SQL Database reserved capacity</span></span>](../sql-database/sql-database-reserved-capacity.md)
- [<span data-ttu-id="3e4b4-176">Prepay for SUSE software plans from Azure Reservations</span><span class="sxs-lookup"><span data-stu-id="3e4b4-176">Prepay for SUSE software plans from Azure Reservations</span></span>](../virtual-machines/linux/prepay-suse-software-charges.md)
- [<span data-ttu-id="3e4b4-177">Understand how the VM reservation discount is applied</span><span class="sxs-lookup"><span data-stu-id="3e4b4-177">Understand how the VM reservation discount is applied</span></span>](billing-understand-vm-reservation-charges.md)
- [<span data-ttu-id="3e4b4-178">Understand how the SUSE Linux Enterprise software plan discount is applied</span><span class="sxs-lookup"><span data-stu-id="3e4b4-178">Understand how the SUSE Linux Enterprise software plan discount is applied</span></span>](../billing/billing-understand-suse-reservation-charges.md)
- [<span data-ttu-id="3e4b4-179">Understand how other reservation discounts are applied</span><span class="sxs-lookup"><span data-stu-id="3e4b4-179">Understand how other reservation discounts are applied</span></span>](billing-understand-reservation-charges.md)
- [<span data-ttu-id="3e4b4-180">Understand reservation usage for your Pay-As-You-Go subscription</span><span class="sxs-lookup"><span data-stu-id="3e4b4-180">Understand reservation usage for your Pay-As-You-Go subscription</span></span>](billing-understand-reserved-instance-usage.md)
- [<span data-ttu-id="3e4b4-181">Understand reservation usage for your Enterprise enrollment</span><span class="sxs-lookup"><span data-stu-id="3e4b4-181">Understand reservation usage for your Enterprise enrollment</span></span>](billing-understand-reserved-instance-usage-ea.md)
- [<span data-ttu-id="3e4b4-182">Windows software costs not included with Reservations</span><span class="sxs-lookup"><span data-stu-id="3e4b4-182">Windows software costs not included with Reservations</span></span>](billing-reserved-instance-windows-software-costs.md)

## <a name="need-help-contact-support"></a><span data-ttu-id="3e4b4-183">Need help?</span><span class="sxs-lookup"><span data-stu-id="3e4b4-183">Need help?</span></span> <span data-ttu-id="3e4b4-184">Contact support</span><span class="sxs-lookup"><span data-stu-id="3e4b4-184">Contact support</span></span>

<span data-ttu-id="3e4b4-185">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span><span class="sxs-lookup"><span data-stu-id="3e4b4-185">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
