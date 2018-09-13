---
title: Understand Azure Reservations usage for Pay-As-You-Go subscription | Microsoft Docs
description: Learn how to read your usage to understand how the Azure reservation for your Pay-As-You-Go subscription is applied.
services: billing
documentationcenter: ''
author: manish-shukla01
manager: manshuk
editor: ''
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2018
ms.author: manshuk
ms.openlocfilehash: 1226b2f73d556da2ff7d73f6f322e0bd1590f915
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858056"
---
# <a name="understand-azure-reservation-usage-for-your-pay-as-you-go-subscription"></a><span data-ttu-id="a5ee3-103">Understand Azure reservation usage for your Pay-As-You-Go subscription</span><span class="sxs-lookup"><span data-stu-id="a5ee3-103">Understand Azure reservation usage for your Pay-As-You-Go subscription</span></span>

<span data-ttu-id="a5ee3-104">Use the ReservationId from [Reservation page](https://portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=Reservations&Microsoft_Azure_Reservations=true#blade/Microsoft_Azure_Reservations/ReservationsBrowseBlade) and the usage file from the [Azure Accounts portal](https://account.azure.com) to evaluate your reservation usage.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-104">Use the ReservationId from [Reservation page](https://portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=Reservations&Microsoft_Azure_Reservations=true#blade/Microsoft_Azure_Reservations/ReservationsBrowseBlade) and the usage file from the [Azure Accounts portal](https://account.azure.com) to evaluate your reservation usage.</span></span>

<span data-ttu-id="a5ee3-105">If you are a customer with an Enterprise Agreement, see [Understand reservation usage for your Enterprise enrollment.](billing-understand-reserved-instance-usage-ea.md).</span><span class="sxs-lookup"><span data-stu-id="a5ee3-105">If you are a customer with an Enterprise Agreement, see [Understand reservation usage for your Enterprise enrollment.](billing-understand-reserved-instance-usage-ea.md).</span></span>

<span data-ttu-id="a5ee3-106">This article assumes that the reservation is applied to a single subscription.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-106">This article assumes that the reservation is applied to a single subscription.</span></span> <span data-ttu-id="a5ee3-107">If the reservation is applied to more than one subscription, your reservation benefit may span multiple usage CSV files.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-107">If the reservation is applied to more than one subscription, your reservation benefit may span multiple usage CSV files.</span></span>

## <a name="usage-for-reserved-virtual-machine-instances"></a><span data-ttu-id="a5ee3-108">Usage for Reserved Virtual Machine Instances</span><span class="sxs-lookup"><span data-stu-id="a5ee3-108">Usage for Reserved Virtual Machine Instances</span></span>

<span data-ttu-id="a5ee3-109">For the following sections, assume that you are running a Standard_DS1_v2 Windows VM in the east US region and your reserved VM instance information looks like the following table:</span><span class="sxs-lookup"><span data-stu-id="a5ee3-109">For the following sections, assume that you are running a Standard_DS1_v2 Windows VM in the east US region and your reserved VM instance information looks like the following table:</span></span>

| <span data-ttu-id="a5ee3-110">Field</span><span class="sxs-lookup"><span data-stu-id="a5ee3-110">Field</span></span> | <span data-ttu-id="a5ee3-111">Value</span><span class="sxs-lookup"><span data-stu-id="a5ee3-111">Value</span></span> |
|---| :---: |
|<span data-ttu-id="a5ee3-112">ReservationId</span><span class="sxs-lookup"><span data-stu-id="a5ee3-112">ReservationId</span></span> |<span data-ttu-id="a5ee3-113">8117adfb-1d94-4675-be2b-f3c1bca808b6</span><span class="sxs-lookup"><span data-stu-id="a5ee3-113">8117adfb-1d94-4675-be2b-f3c1bca808b6</span></span>|
|<span data-ttu-id="a5ee3-114">Quantity</span><span class="sxs-lookup"><span data-stu-id="a5ee3-114">Quantity</span></span> |<span data-ttu-id="a5ee3-115">1</span><span class="sxs-lookup"><span data-stu-id="a5ee3-115">1</span></span>|
|<span data-ttu-id="a5ee3-116">SKU</span><span class="sxs-lookup"><span data-stu-id="a5ee3-116">SKU</span></span> | <span data-ttu-id="a5ee3-117">Standard_DS1_v2</span><span class="sxs-lookup"><span data-stu-id="a5ee3-117">Standard_DS1_v2</span></span>|
|<span data-ttu-id="a5ee3-118">Region</span><span class="sxs-lookup"><span data-stu-id="a5ee3-118">Region</span></span> | <span data-ttu-id="a5ee3-119">eastus</span><span class="sxs-lookup"><span data-stu-id="a5ee3-119">eastus</span></span> |

<span data-ttu-id="a5ee3-120">The hardware portion of the VM is covered because the deployed VM matches the reservation attributes.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-120">The hardware portion of the VM is covered because the deployed VM matches the reservation attributes.</span></span> <span data-ttu-id="a5ee3-121">To see what Windows software isn't covered by the reserved VM instance, see [Azure Reserve VM Instances Windows software costs](billing-reserved-instance-windows-software-costs.md)</span><span class="sxs-lookup"><span data-stu-id="a5ee3-121">To see what Windows software isn't covered by the reserved VM instance, see [Azure Reserve VM Instances Windows software costs](billing-reserved-instance-windows-software-costs.md)</span></span>

### <a name="statement-section-of-csv-file-for-vms"></a><span data-ttu-id="a5ee3-122">Statement section of CSV file for VMs</span><span class="sxs-lookup"><span data-stu-id="a5ee3-122">Statement section of CSV file for VMs</span></span>

<span data-ttu-id="a5ee3-123">This section of your CSV file shows the total usage for your reservation.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-123">This section of your CSV file shows the total usage for your reservation.</span></span> <span data-ttu-id="a5ee3-124">Apply the filter on the **Meter Subcategory** field that contains **"Reservation-"**.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-124">Apply the filter on the **Meter Subcategory** field that contains **"Reservation-"**.</span></span> <span data-ttu-id="a5ee3-125">You see something like the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="a5ee3-125">You see something like the following screenshot:</span></span>

![Screenshot of filtered reservation usage details and charges](./media/billing-understand-reserved-instance-usage/billing-payg-reserved-instance-csv-statements.png)

<span data-ttu-id="a5ee3-127">The **Reservation-Base VM** line has the total number of hours that are covered by the reservation.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-127">The **Reservation-Base VM** line has the total number of hours that are covered by the reservation.</span></span> <span data-ttu-id="a5ee3-128">This line is $0.00 because the reservation covers it.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-128">This line is $0.00 because the reservation covers it.</span></span> <span data-ttu-id="a5ee3-129">The **Reservation-Windows Svr (1 Core)** line covers the cost of Windows software.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-129">The **Reservation-Windows Svr (1 Core)** line covers the cost of Windows software.</span></span>

### <a name="daily-usage-section-of-csv-file"></a><span data-ttu-id="a5ee3-130">Daily usage section of CSV file</span><span class="sxs-lookup"><span data-stu-id="a5ee3-130">Daily usage section of CSV file</span></span>

<span data-ttu-id="a5ee3-131">Filter on **Additional Info** and type in your **Reservation ID**.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-131">Filter on **Additional Info** and type in your **Reservation ID**.</span></span> <span data-ttu-id="a5ee3-132">The following screenshot shows the fields related to the reservation.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-132">The following screenshot shows the fields related to the reservation.</span></span>

![Screenshot of daily usage details and charges](./media/billing-understand-reserved-instance-usage/billing-payg-reserved-instance-csv-details.png)

1. <span data-ttu-id="a5ee3-134">**ReservationId** in the **Additional Info** field is the reservation that's applied to the VM.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-134">**ReservationId** in the **Additional Info** field is the reservation that's applied to the VM.</span></span>
2. <span data-ttu-id="a5ee3-135">**ConsumptionMeter** is the meter ID for the VM.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-135">**ConsumptionMeter** is the meter ID for the VM.</span></span>
3. <span data-ttu-id="a5ee3-136">The **Reservation-Base VM** **Meter Subcategory** line represents the $0 cost in statement section.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-136">The **Reservation-Base VM** **Meter Subcategory** line represents the $0 cost in statement section.</span></span> <span data-ttu-id="a5ee3-137">The cost of running this VM is already paid by the reservation.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-137">The cost of running this VM is already paid by the reservation.</span></span>
4. <span data-ttu-id="a5ee3-138">**Meter ID** is the meter ID for the reservation.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-138">**Meter ID** is the meter ID for the reservation.</span></span> <span data-ttu-id="a5ee3-139">The cost of this meter is $0.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-139">The cost of this meter is $0.</span></span> <span data-ttu-id="a5ee3-140">This meter id appears for any VM that qualifies for the reservation discount.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-140">This meter id appears for any VM that qualifies for the reservation discount.</span></span>
5. <span data-ttu-id="a5ee3-141">Standard_DS1_v2 is one vCPU VM and the VM is deployed without Azure Hybrid Benefit.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-141">Standard_DS1_v2 is one vCPU VM and the VM is deployed without Azure Hybrid Benefit.</span></span> <span data-ttu-id="a5ee3-142">So, this meter covers the extra charge of the Windows software.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-142">So, this meter covers the extra charge of the Windows software.</span></span> <span data-ttu-id="a5ee3-143">To find the meter corresponding to D series 1 core VM, see [Azure Reserve VM Instances Windows software costs](billing-reserved-instance-windows-software-costs.md).</span><span class="sxs-lookup"><span data-stu-id="a5ee3-143">To find the meter corresponding to D series 1 core VM, see [Azure Reserve VM Instances Windows software costs](billing-reserved-instance-windows-software-costs.md).</span></span> <span data-ttu-id="a5ee3-144">If you have the Azure Hybrid Benefit, this extra charge is not applied.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-144">If you have the Azure Hybrid Benefit, this extra charge is not applied.</span></span>

## <a name="usage-for-sql-database-reserved-capacity-reservations"></a><span data-ttu-id="a5ee3-145">Usage for SQL Database reserved capacity reservations</span><span class="sxs-lookup"><span data-stu-id="a5ee3-145">Usage for SQL Database reserved capacity reservations</span></span>

<span data-ttu-id="a5ee3-146">For the following sections, assume that you are running a SQL Database Gen 4 in the east US region and your reservation information looks like the following table:</span><span class="sxs-lookup"><span data-stu-id="a5ee3-146">For the following sections, assume that you are running a SQL Database Gen 4 in the east US region and your reservation information looks like the following table:</span></span>

| <span data-ttu-id="a5ee3-147">Field</span><span class="sxs-lookup"><span data-stu-id="a5ee3-147">Field</span></span> | <span data-ttu-id="a5ee3-148">Value</span><span class="sxs-lookup"><span data-stu-id="a5ee3-148">Value</span></span> |
|---| --- |
|<span data-ttu-id="a5ee3-149">ReservationId</span><span class="sxs-lookup"><span data-stu-id="a5ee3-149">ReservationId</span></span> |<span data-ttu-id="a5ee3-150">446ec809-423d-467c-8c5c-bbd5d22906b1</span><span class="sxs-lookup"><span data-stu-id="a5ee3-150">446ec809-423d-467c-8c5c-bbd5d22906b1</span></span>|
|<span data-ttu-id="a5ee3-151">Quantity</span><span class="sxs-lookup"><span data-stu-id="a5ee3-151">Quantity</span></span> |<span data-ttu-id="a5ee3-152">2</span><span class="sxs-lookup"><span data-stu-id="a5ee3-152">2</span></span>|
|<span data-ttu-id="a5ee3-153">Product</span><span class="sxs-lookup"><span data-stu-id="a5ee3-153">Product</span></span>| <span data-ttu-id="a5ee3-154">SQL Database Gen 4 (2 Core)</span><span class="sxs-lookup"><span data-stu-id="a5ee3-154">SQL Database Gen 4 (2 Core)</span></span>|
|<span data-ttu-id="a5ee3-155">Region</span><span class="sxs-lookup"><span data-stu-id="a5ee3-155">Region</span></span> | <span data-ttu-id="a5ee3-156">eastus</span><span class="sxs-lookup"><span data-stu-id="a5ee3-156">eastus</span></span> |

### <a name="statement-section-of-csv-file"></a><span data-ttu-id="a5ee3-157">Statement section of CSV file</span><span class="sxs-lookup"><span data-stu-id="a5ee3-157">Statement section of CSV file</span></span>

<span data-ttu-id="a5ee3-158">Filter on **Reserved Instance Usage** meter name.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-158">Filter on **Reserved Instance Usage** meter name.</span></span> <span data-ttu-id="a5ee3-159">You see something like the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="a5ee3-159">You see something like the following screenshot:</span></span>

![CSV file for SQL Database reserved capacity](./media/billing-understand-reserved-instance-usage/billing-payg-sql-db-reserved-capacity-csv-statements.png)

<span data-ttu-id="a5ee3-161">The **Reserved Instance Usage** line has the total number of core hours covered by the reservation.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-161">The **Reserved Instance Usage** line has the total number of core hours covered by the reservation.</span></span> <span data-ttu-id="a5ee3-162">The rate is $0 for this line as the reservation covered the cost.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-162">The rate is $0 for this line as the reservation covered the cost.</span></span>

### <a name="detail-section-of-csv-file"></a><span data-ttu-id="a5ee3-163">Detail section of CSV file</span><span class="sxs-lookup"><span data-stu-id="a5ee3-163">Detail section of CSV file</span></span>

<span data-ttu-id="a5ee3-164">Filter on **Additional Info** and type in your **Reservation ID**.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-164">Filter on **Additional Info** and type in your **Reservation ID**.</span></span> <span data-ttu-id="a5ee3-165">The following screenshot shows the fields related to the SQL Database reserved capacity reservation.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-165">The following screenshot shows the fields related to the SQL Database reserved capacity reservation.</span></span>

![CSV file for SQL Database reserved capacity](./media/billing-understand-reserved-instance-usage/billing-payg-sql-db-reserved-capacity-csv-details.png)

1. <span data-ttu-id="a5ee3-167">**ReservationId** in the **Additional Info** field is the SQL Database reserved capacity reservation that's applied to the SQL database resource.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-167">**ReservationId** in the **Additional Info** field is the SQL Database reserved capacity reservation that's applied to the SQL database resource.</span></span>
2. <span data-ttu-id="a5ee3-168">**ConsumptionMeter** is the meter ID for the SQL Database resource.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-168">**ConsumptionMeter** is the meter ID for the SQL Database resource.</span></span>
3. <span data-ttu-id="a5ee3-169">The **Meter Id** is the reservation meter.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-169">The **Meter Id** is the reservation meter.</span></span> <span data-ttu-id="a5ee3-170">The cost of this meter is $0.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-170">The cost of this meter is $0.</span></span> <span data-ttu-id="a5ee3-171">Any SQL Database resources that qualify for the reservation discount shows this meter ID in the CSV file.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-171">Any SQL Database resources that qualify for the reservation discount shows this meter ID in the CSV file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5ee3-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="a5ee3-172">Next steps</span></span>

<span data-ttu-id="a5ee3-173">To learn more about Azure Reservations, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="a5ee3-173">To learn more about Azure Reservations, see the following articles:</span></span>

- [<span data-ttu-id="a5ee3-174">What are Azure Reservations?</span><span class="sxs-lookup"><span data-stu-id="a5ee3-174">What are Azure Reservations?</span></span>](billing-save-compute-costs-reservations.md)
- [<span data-ttu-id="a5ee3-175">Prepay for Virtual Machines with Azure Reserved VM Instances</span><span class="sxs-lookup"><span data-stu-id="a5ee3-175">Prepay for Virtual Machines with Azure Reserved VM Instances</span></span>](../virtual-machines/windows/prepay-reserved-vm-instances.md)
- [<span data-ttu-id="a5ee3-176">Prepay for SQL Database compute resources with Azure SQL Database reserved capacity</span><span class="sxs-lookup"><span data-stu-id="a5ee3-176">Prepay for SQL Database compute resources with Azure SQL Database reserved capacity</span></span>](../sql-database/sql-database-reserved-capacity.md)
- [<span data-ttu-id="a5ee3-177">Manage Azure Reservations</span><span class="sxs-lookup"><span data-stu-id="a5ee3-177">Manage Azure Reservations</span></span>](billing-manage-reserved-vm-instance.md)
- [<span data-ttu-id="a5ee3-178">Understand how the reservation discount is applied</span><span class="sxs-lookup"><span data-stu-id="a5ee3-178">Understand how the reservation discount is applied</span></span>](billing-understand-vm-reservation-charges.md)
- [<span data-ttu-id="a5ee3-179">Understand reservation usage for your Enterprise enrollment</span><span class="sxs-lookup"><span data-stu-id="a5ee3-179">Understand reservation usage for your Enterprise enrollment</span></span>](billing-understand-reserved-instance-usage-ea.md)
- [<span data-ttu-id="a5ee3-180">Windows software costs not included with Reservations</span><span class="sxs-lookup"><span data-stu-id="a5ee3-180">Windows software costs not included with Reservations</span></span>](billing-reserved-instance-windows-software-costs.md)

## <a name="need-help-contact-support"></a><span data-ttu-id="a5ee3-181">Need help?</span><span class="sxs-lookup"><span data-stu-id="a5ee3-181">Need help?</span></span> <span data-ttu-id="a5ee3-182">Contact support</span><span class="sxs-lookup"><span data-stu-id="a5ee3-182">Contact support</span></span>

<span data-ttu-id="a5ee3-183">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span><span class="sxs-lookup"><span data-stu-id="a5ee3-183">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
