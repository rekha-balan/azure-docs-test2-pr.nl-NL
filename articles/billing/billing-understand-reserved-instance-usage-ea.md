---
title: Understand Azure Reservations usage for Enterprise | Microsoft Docs
description: Learn how to read your usage to understand how the Azure reservation for your Enterprise enrollment is applied.
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
ms.openlocfilehash: 334271139b791ab60f2bc89ae695ba9bf06b7d12
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867210"
---
# <a name="understand-azure-reservation-usage-for-your-enterprise-enrollment"></a><span data-ttu-id="9373c-103">Understand Azure reservation usage for your Enterprise enrollment</span><span class="sxs-lookup"><span data-stu-id="9373c-103">Understand Azure reservation usage for your Enterprise enrollment</span></span>

<span data-ttu-id="9373c-104">Use the **ReservationId** from [Reservations page](https://portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=Reservations&Microsoft_Azure_Reservations=true#blade/Microsoft_Azure_Reservations/ReservationsBrowseBlade) and the usage file from the [EA portal](https://ea.azure.com) to evaluate your reservation usage.</span><span class="sxs-lookup"><span data-stu-id="9373c-104">Use the **ReservationId** from [Reservations page](https://portal.azure.com/?microsoft_azure_marketplace_ItemHideKey=Reservations&Microsoft_Azure_Reservations=true#blade/Microsoft_Azure_Reservations/ReservationsBrowseBlade) and the usage file from the [EA portal](https://ea.azure.com) to evaluate your reservation usage.</span></span> <span data-ttu-id="9373c-105">You can also see the reservation usage in the usage summary section of [EA portal](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9373c-105">You can also see the reservation usage in the usage summary section of [EA portal](https://ea.azure.com).</span></span>

<span data-ttu-id="9373c-106">If you bought the reservation in a Pay-As-You-Go billing context, see [Understand reservation usage for your Pay-As-You-Go subscription.](billing-understand-reserved-instance-usage.md)</span><span class="sxs-lookup"><span data-stu-id="9373c-106">If you bought the reservation in a Pay-As-You-Go billing context, see [Understand reservation usage for your Pay-As-You-Go subscription.](billing-understand-reserved-instance-usage.md)</span></span>

## <a name="usage-for-reserved-virtual-machines-instances"></a><span data-ttu-id="9373c-107">Usage for Reserved Virtual Machines Instances</span><span class="sxs-lookup"><span data-stu-id="9373c-107">Usage for Reserved Virtual Machines Instances</span></span>

<span data-ttu-id="9373c-108">For the following sections, assume that you are running a Standard_D1_v2 Windows VM in the east US region and your reservation information looks like the following table:</span><span class="sxs-lookup"><span data-stu-id="9373c-108">For the following sections, assume that you are running a Standard_D1_v2 Windows VM in the east US region and your reservation information looks like the following table:</span></span>

| <span data-ttu-id="9373c-109">Field</span><span class="sxs-lookup"><span data-stu-id="9373c-109">Field</span></span> | <span data-ttu-id="9373c-110">Value</span><span class="sxs-lookup"><span data-stu-id="9373c-110">Value</span></span> |
|---| --- |
|<span data-ttu-id="9373c-111">ReservationId</span><span class="sxs-lookup"><span data-stu-id="9373c-111">ReservationId</span></span> |<span data-ttu-id="9373c-112">8f82d880-d33e-4e0d-bcb5-6bcb5de0c719</span><span class="sxs-lookup"><span data-stu-id="9373c-112">8f82d880-d33e-4e0d-bcb5-6bcb5de0c719</span></span>|
|<span data-ttu-id="9373c-113">Quantity</span><span class="sxs-lookup"><span data-stu-id="9373c-113">Quantity</span></span> |<span data-ttu-id="9373c-114">1</span><span class="sxs-lookup"><span data-stu-id="9373c-114">1</span></span>|
|<span data-ttu-id="9373c-115">SKU</span><span class="sxs-lookup"><span data-stu-id="9373c-115">SKU</span></span> | <span data-ttu-id="9373c-116">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="9373c-116">Standard_D1</span></span>|
|<span data-ttu-id="9373c-117">Region</span><span class="sxs-lookup"><span data-stu-id="9373c-117">Region</span></span> | <span data-ttu-id="9373c-118">eastus</span><span class="sxs-lookup"><span data-stu-id="9373c-118">eastus</span></span> |

<span data-ttu-id="9373c-119">The hardware portion of the VM is covered because the deployed VM matches the reservation attributes.</span><span class="sxs-lookup"><span data-stu-id="9373c-119">The hardware portion of the VM is covered because the deployed VM matches the reservation attributes.</span></span> <span data-ttu-id="9373c-120">To see what Windows software isn't covered by the reservation, see [Azure Reserve VM Instances Windows software costs](billing-reserved-instance-windows-software-costs.md).</span><span class="sxs-lookup"><span data-stu-id="9373c-120">To see what Windows software isn't covered by the reservation, see [Azure Reserve VM Instances Windows software costs](billing-reserved-instance-windows-software-costs.md).</span></span>

### <a name="usage-in-csv-file-for-reserved-vm-instances"></a><span data-ttu-id="9373c-121">Usage in CSV file for Reserved VM Instances</span><span class="sxs-lookup"><span data-stu-id="9373c-121">Usage in CSV file for Reserved VM Instances</span></span>

<span data-ttu-id="9373c-122">You can download the Enterprise usage CSV file from the Enterprise portal.</span><span class="sxs-lookup"><span data-stu-id="9373c-122">You can download the Enterprise usage CSV file from the Enterprise portal.</span></span> <span data-ttu-id="9373c-123">In the CSV file, filter on **Additional Info** and type in your **ReservationID**.</span><span class="sxs-lookup"><span data-stu-id="9373c-123">In the CSV file, filter on **Additional Info** and type in your **ReservationID**.</span></span> <span data-ttu-id="9373c-124">The following screenshot shows the fields related to the reservation:</span><span class="sxs-lookup"><span data-stu-id="9373c-124">The following screenshot shows the fields related to the reservation:</span></span>

![Enterprise Agreement (EA) csv for Azure reservation](./media/billing-understand-reserved-instance-usage-ea/billing-ea-reserved-instance-csv.png)

1. <span data-ttu-id="9373c-126">**ReservationId** in **Additional Info** field represents the reservation that's applied to the VM.</span><span class="sxs-lookup"><span data-stu-id="9373c-126">**ReservationId** in **Additional Info** field represents the reservation that's applied to the VM.</span></span>
2. <span data-ttu-id="9373c-127">**ConsumptionMeter** is the meter ID for the VM.</span><span class="sxs-lookup"><span data-stu-id="9373c-127">**ConsumptionMeter** is the meter ID for the VM.</span></span>
3. <span data-ttu-id="9373c-128">**Meter ID** is the reservation meter with $0 cost.</span><span class="sxs-lookup"><span data-stu-id="9373c-128">**Meter ID** is the reservation meter with $0 cost.</span></span> <span data-ttu-id="9373c-129">The cost of the running VM is paid by the reserved VM instance.</span><span class="sxs-lookup"><span data-stu-id="9373c-129">The cost of the running VM is paid by the reserved VM instance.</span></span>
4. <span data-ttu-id="9373c-130">Standard_D1 is one vCPU VM and the VM is deployed without the Azure Hybrid Benefit.</span><span class="sxs-lookup"><span data-stu-id="9373c-130">Standard_D1 is one vCPU VM and the VM is deployed without the Azure Hybrid Benefit.</span></span> <span data-ttu-id="9373c-131">So this meter covers the extra charge of Windows software.</span><span class="sxs-lookup"><span data-stu-id="9373c-131">So this meter covers the extra charge of Windows software.</span></span> <span data-ttu-id="9373c-132">To find the meter corresponding to the D series 1 core VM, see [Azure Reserve VM Instances Windows software costs](billing-reserved-instance-windows-software-costs.md).</span><span class="sxs-lookup"><span data-stu-id="9373c-132">To find the meter corresponding to the D series 1 core VM, see [Azure Reserve VM Instances Windows software costs](billing-reserved-instance-windows-software-costs.md).</span></span>  <span data-ttu-id="9373c-133">If you have the Azure Hybrid Benefit, this extra charge isn't applied.</span><span class="sxs-lookup"><span data-stu-id="9373c-133">If you have the Azure Hybrid Benefit, this extra charge isn't applied.</span></span>

## <a name="usage-for-sql-database-reserved-capacity-reservations"></a><span data-ttu-id="9373c-134">Usage for SQL Database reserved capacity reservations</span><span class="sxs-lookup"><span data-stu-id="9373c-134">Usage for SQL Database reserved capacity reservations</span></span>

<span data-ttu-id="9373c-135">For the following sections, assume that you are running a SQL Database Gen 4 in the east US region and your reservation information looks like the following table:</span><span class="sxs-lookup"><span data-stu-id="9373c-135">For the following sections, assume that you are running a SQL Database Gen 4 in the east US region and your reservation information looks like the following table:</span></span>

| <span data-ttu-id="9373c-136">Field</span><span class="sxs-lookup"><span data-stu-id="9373c-136">Field</span></span> | <span data-ttu-id="9373c-137">Value</span><span class="sxs-lookup"><span data-stu-id="9373c-137">Value</span></span> |
|---| --- |
|<span data-ttu-id="9373c-138">ReservationId</span><span class="sxs-lookup"><span data-stu-id="9373c-138">ReservationId</span></span> |<span data-ttu-id="9373c-139">8244e673-83e9-45ad-b54b-3f5295d37cae</span><span class="sxs-lookup"><span data-stu-id="9373c-139">8244e673-83e9-45ad-b54b-3f5295d37cae</span></span>|
|<span data-ttu-id="9373c-140">Quantity</span><span class="sxs-lookup"><span data-stu-id="9373c-140">Quantity</span></span> |<span data-ttu-id="9373c-141">2</span><span class="sxs-lookup"><span data-stu-id="9373c-141">2</span></span>|
|<span data-ttu-id="9373c-142">Product</span><span class="sxs-lookup"><span data-stu-id="9373c-142">Product</span></span>| <span data-ttu-id="9373c-143">SQL Database Gen 4 (2 Core)</span><span class="sxs-lookup"><span data-stu-id="9373c-143">SQL Database Gen 4 (2 Core)</span></span>|
|<span data-ttu-id="9373c-144">Region</span><span class="sxs-lookup"><span data-stu-id="9373c-144">Region</span></span> | <span data-ttu-id="9373c-145">eastus</span><span class="sxs-lookup"><span data-stu-id="9373c-145">eastus</span></span> |

### <a name="usage-in-csv-file-for-sql-database-reserved-capacity"></a><span data-ttu-id="9373c-146">Usage in CSV file for SQL Database reserved capacity</span><span class="sxs-lookup"><span data-stu-id="9373c-146">Usage in CSV file for SQL Database reserved capacity</span></span>

<span data-ttu-id="9373c-147">Filter on **Additional Info** and type in your **Reservation ID**.</span><span class="sxs-lookup"><span data-stu-id="9373c-147">Filter on **Additional Info** and type in your **Reservation ID**.</span></span> <span data-ttu-id="9373c-148">The following screenshot shows the fields related to the reservation.</span><span class="sxs-lookup"><span data-stu-id="9373c-148">The following screenshot shows the fields related to the reservation.</span></span>

![Enterprise Agreement (EA) csv for SQL Database reserved capacity](./media/billing-understand-reserved-instance-usage-ea/billing-ea-sql-db-reserved-capacity-csv.png)

1. <span data-ttu-id="9373c-150">**ReservationId** in the **Additional Info** field is the reservation that's applied to the SQL Database resource.</span><span class="sxs-lookup"><span data-stu-id="9373c-150">**ReservationId** in the **Additional Info** field is the reservation that's applied to the SQL Database resource.</span></span>
2. <span data-ttu-id="9373c-151">**ConsumptionMeter** is the meter ID for the SQL Database resource.</span><span class="sxs-lookup"><span data-stu-id="9373c-151">**ConsumptionMeter** is the meter ID for the SQL Database resource.</span></span>
3. <span data-ttu-id="9373c-152">**Meter ID** is the reservation meter with  $0 cost.</span><span class="sxs-lookup"><span data-stu-id="9373c-152">**Meter ID** is the reservation meter with  $0 cost.</span></span> <span data-ttu-id="9373c-153">Any SQL Database resource that qualifies for the reservation shows this meter ID in the CSV file.</span><span class="sxs-lookup"><span data-stu-id="9373c-153">Any SQL Database resource that qualifies for the reservation shows this meter ID in the CSV file.</span></span>

## <a name="usage-summary-page-in-enterprise-portal"></a><span data-ttu-id="9373c-154">Usage summary page in Enterprise portal</span><span class="sxs-lookup"><span data-stu-id="9373c-154">Usage summary page in Enterprise portal</span></span>

<span data-ttu-id="9373c-155">Your Azure reservation usage also shows up in usage summary section of Enterprise portal: ![Enterprise Agreement (EA) usage summary](./media/billing-understand-reserved-instance-usage-ea/billing-ea-reserved-instance-usagesummary.png)</span><span class="sxs-lookup"><span data-stu-id="9373c-155">Your Azure reservation usage also shows up in usage summary section of Enterprise portal: ![Enterprise Agreement (EA) usage summary](./media/billing-understand-reserved-instance-usage-ea/billing-ea-reserved-instance-usagesummary.png)</span></span>

1. <span data-ttu-id="9373c-156">You aren't charged for the hardware component of the VM as it is covered by reservation.</span><span class="sxs-lookup"><span data-stu-id="9373c-156">You aren't charged for the hardware component of the VM as it is covered by reservation.</span></span> <span data-ttu-id="9373c-157">For a SQL Database reservation, you see a line with **Service Name** as Azure SQL Database reserved capacity usage.</span><span class="sxs-lookup"><span data-stu-id="9373c-157">For a SQL Database reservation, you see a line with **Service Name** as Azure SQL Database reserved capacity usage.</span></span>
2. <span data-ttu-id="9373c-158">In this example, you don't have the Azure Hybrid Benefit so you're charged for the Windows software used with the VM.</span><span class="sxs-lookup"><span data-stu-id="9373c-158">In this example, you don't have the Azure Hybrid Benefit so you're charged for the Windows software used with the VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9373c-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="9373c-159">Next steps</span></span>

<span data-ttu-id="9373c-160">To learn more about Azure Reservations, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="9373c-160">To learn more about Azure Reservations, see the following articles:</span></span>

- [<span data-ttu-id="9373c-161">What are Azure Reservations?</span><span class="sxs-lookup"><span data-stu-id="9373c-161">What are Azure Reservations?</span></span>](billing-save-compute-costs-reservations.md)
- [<span data-ttu-id="9373c-162">Prepay for Virtual Machines with Azure Reserved VM Instances</span><span class="sxs-lookup"><span data-stu-id="9373c-162">Prepay for Virtual Machines with Azure Reserved VM Instances</span></span>](../virtual-machines/windows/prepay-reserved-vm-instances.md)
- [<span data-ttu-id="9373c-163">Prepay for SQL Database compute resources with Azure SQL Database reserved capacity</span><span class="sxs-lookup"><span data-stu-id="9373c-163">Prepay for SQL Database compute resources with Azure SQL Database reserved capacity</span></span>](../sql-database/sql-database-reserved-capacity.md) 
- [<span data-ttu-id="9373c-164">Manage Azure Reservations</span><span class="sxs-lookup"><span data-stu-id="9373c-164">Manage Azure Reservations</span></span>](billing-manage-reserved-vm-instance.md)
- [<span data-ttu-id="9373c-165">Understand how the reservation discount is applied</span><span class="sxs-lookup"><span data-stu-id="9373c-165">Understand how the reservation discount is applied</span></span>](billing-understand-vm-reservation-charges.md)
- [<span data-ttu-id="9373c-166">Understand reservation usage for your Pay-As-You-Go subscription</span><span class="sxs-lookup"><span data-stu-id="9373c-166">Understand reservation usage for your Pay-As-You-Go subscription</span></span>](billing-understand-reserved-instance-usage.md)
- [<span data-ttu-id="9373c-167">Windows software costs not included with Reservations</span><span class="sxs-lookup"><span data-stu-id="9373c-167">Windows software costs not included with Reservations</span></span>](billing-reserved-instance-windows-software-costs.md)

## <a name="need-help-contact-support"></a><span data-ttu-id="9373c-168">Need help?</span><span class="sxs-lookup"><span data-stu-id="9373c-168">Need help?</span></span> <span data-ttu-id="9373c-169">Contact support</span><span class="sxs-lookup"><span data-stu-id="9373c-169">Contact support</span></span>

<span data-ttu-id="9373c-170">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span><span class="sxs-lookup"><span data-stu-id="9373c-170">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>