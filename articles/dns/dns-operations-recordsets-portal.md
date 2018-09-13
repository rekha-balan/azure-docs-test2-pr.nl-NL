---
title: Manage DNS record sets and records with Azure DNS | Microsoft Docs
description: Azure DNS provides the capability to manage DNS record sets and records when hosting your domain.
services: dns
documentationcenter: na
author: vhorne
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: victorh
ms.openlocfilehash: b95ec9b4b5077b236c5f3a7183820552b7ccac49
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827060"
---
# <a name="manage-dns-records-and-record-sets-by-using-the-azure-portal"></a><span data-ttu-id="fc9d6-103">Manage DNS records and record sets by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="fc9d6-103">Manage DNS records and record sets by using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

<span data-ttu-id="fc9d6-108">This article shows you how to manage record sets and records for your DNS zone by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-108">This article shows you how to manage record sets and records for your DNS zone by using the Azure portal.</span></span>

<span data-ttu-id="fc9d6-109">It's important to understand the difference between DNS record sets and individual DNS records.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-109">It's important to understand the difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="fc9d6-110">A record set is a collection of records in a zone that have the same name and are the same type.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-110">A record set is a collection of records in a zone that have the same name and are the same type.</span></span> <span data-ttu-id="fc9d6-111">For more information, see [Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fc9d6-111">For more information, see [Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="fc9d6-112">Create a new record set and record</span><span class="sxs-lookup"><span data-stu-id="fc9d6-112">Create a new record set and record</span></span>

<span data-ttu-id="fc9d6-113">To create a record set in the Azure portal, see [Create DNS records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fc9d6-113">To create a record set in the Azure portal, see [Create DNS records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="fc9d6-114">View a record set</span><span class="sxs-lookup"><span data-stu-id="fc9d6-114">View a record set</span></span>

1. <span data-ttu-id="fc9d6-115">In the Azure portal, go to the **DNS zone** blade.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-115">In the Azure portal, go to the **DNS zone** blade.</span></span>
2. <span data-ttu-id="fc9d6-116">Search for the record set and select it.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-116">Search for the record set and select it.</span></span> <span data-ttu-id="fc9d6-117">This opens the record set properties.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-117">This opens the record set properties.</span></span>

    ![Search for a record set](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-to-a-record-set"></a><span data-ttu-id="fc9d6-119">Add a new record to a record set</span><span class="sxs-lookup"><span data-stu-id="fc9d6-119">Add a new record to a record set</span></span>

<span data-ttu-id="fc9d6-120">You can add up to 20 records to any record set.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-120">You can add up to 20 records to any record set.</span></span> <span data-ttu-id="fc9d6-121">A record set cannot contain two identical records.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="fc9d6-122">Empty record sets (with zero records) can be created, but do not appear on the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-122">Empty record sets (with zero records) can be created, but do not appear on the Azure DNS name servers.</span></span> <span data-ttu-id="fc9d6-123">Record sets of type CNAME can contain one record at most.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="fc9d6-124">On the **Record set properties** blade for your DNS zone, click the record set that you want to add a record to.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-124">On the **Record set properties** blade for your DNS zone, click the record set that you want to add a record to.</span></span>

    ![Select a record set](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="fc9d6-126">Specify the record set properties by filling in the fields.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-126">Specify the record set properties by filling in the fields.</span></span>

    ![Add a record](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="fc9d6-128">Click **Save** at the top of the blade to save your settings.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-128">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="fc9d6-129">Then close the blade.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-129">Then close the blade.</span></span>
4. <span data-ttu-id="fc9d6-130">In the corner, you will see that the record is saving.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-130">In the corner, you will see that the record is saving.</span></span>

    ![Saving record set](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="fc9d6-132">After the record has been saved, the values on the **DNS zone** blade will reflect the new record.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-132">After the record has been saved, the values on the **DNS zone** blade will reflect the new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="fc9d6-133">Update a record</span><span class="sxs-lookup"><span data-stu-id="fc9d6-133">Update a record</span></span>

<span data-ttu-id="fc9d6-134">When you update a record in an existing record set, the fields you can update depend on the type of record you're working with.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-134">When you update a record in an existing record set, the fields you can update depend on the type of record you're working with.</span></span>

1. <span data-ttu-id="fc9d6-135">On the **Record set properties** blade for your record set, search for the record.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-135">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="fc9d6-136">Modify the record.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-136">Modify the record.</span></span> <span data-ttu-id="fc9d6-137">When you modify a record, you can change the available settings for the record.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-137">When you modify a record, you can change the available settings for the record.</span></span> <span data-ttu-id="fc9d6-138">In the following example, the **IP address** field is selected, and the IP address is in the process of being modified.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-138">In the following example, the **IP address** field is selected, and the IP address is in the process of being modified.</span></span>

    ![Modify a record](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="fc9d6-140">Click **Save** at the top of the blade to save your settings.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-140">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="fc9d6-141">In the upper right corner, you'll see the notification that the record has been saved.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-141">In the upper right corner, you'll see the notification that the record has been saved.</span></span>

    ![Saved record set](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="fc9d6-143">After the record has been saved, the values for the record set on the **DNS zone** blade will reflect the updated record.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-143">After the record has been saved, the values for the record set on the **DNS zone** blade will reflect the updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="fc9d6-144">Remove a record from a record set</span><span class="sxs-lookup"><span data-stu-id="fc9d6-144">Remove a record from a record set</span></span>

<span data-ttu-id="fc9d6-145">You can use the Azure portal to remove records from a record set.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-145">You can use the Azure portal to remove records from a record set.</span></span> <span data-ttu-id="fc9d6-146">Note that removing the last record from a record set does not delete the record set.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-146">Note that removing the last record from a record set does not delete the record set.</span></span>

1. <span data-ttu-id="fc9d6-147">On the **Record set properties** blade for your record set, search for the record.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-147">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="fc9d6-148">Click the record that you want to remove.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-148">Click the record that you want to remove.</span></span> <span data-ttu-id="fc9d6-149">Then select **Remove**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-149">Then select **Remove**.</span></span>

    ![Remove a record](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="fc9d6-151">Click **Save** at the top of the blade to save your settings.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-151">Click **Save** at the top of the blade to save your settings.</span></span>
4. <span data-ttu-id="fc9d6-152">After the record has been removed, the values for the record on the **DNS zone** blade will reflect the removal.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-152">After the record has been removed, the values for the record on the **DNS zone** blade will reflect the removal.</span></span>

## <a name="delete"></a><span data-ttu-id="fc9d6-153">Delete a record set</span><span class="sxs-lookup"><span data-stu-id="fc9d6-153">Delete a record set</span></span>

1. <span data-ttu-id="fc9d6-154">On the **Record set properties** blade for your record set, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-154">On the **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Delete a record set](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="fc9d6-156">A message appears asking if you want to delete the record set.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-156">A message appears asking if you want to delete the record set.</span></span>
3. <span data-ttu-id="fc9d6-157">Verify that the name matches the record set that you want to delete, and then click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-157">Verify that the name matches the record set that you want to delete, and then click **Yes**.</span></span>
4. <span data-ttu-id="fc9d6-158">On the **DNS zone** blade, verify that the record set is no longer visible.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-158">On the **DNS zone** blade, verify that the record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="fc9d6-159">Work with NS and SOA records</span><span class="sxs-lookup"><span data-stu-id="fc9d6-159">Work with NS and SOA records</span></span>

<span data-ttu-id="fc9d6-160">NS and SOA records that are automatically created are managed differently from other record types.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="fc9d6-161">Modify SOA records</span><span class="sxs-lookup"><span data-stu-id="fc9d6-161">Modify SOA records</span></span>

<span data-ttu-id="fc9d6-162">You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "\@").</span><span class="sxs-lookup"><span data-stu-id="fc9d6-162">You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "\@").</span></span> <span data-ttu-id="fc9d6-163">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-163">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

### <a name="modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="fc9d6-164">Modify NS records at the zone apex</span><span class="sxs-lookup"><span data-stu-id="fc9d6-164">Modify NS records at the zone apex</span></span>

<span data-ttu-id="fc9d6-165">The NS record set at the zone apex is automatically created with each DNS zone.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-165">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="fc9d6-166">It contains the names of the Azure DNS name servers assigned to the zone.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-166">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="fc9d6-167">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-167">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="fc9d6-168">You can also modify the TTL and metadata for this record set.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-168">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="fc9d6-169">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-169">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="fc9d6-170">Note that this applies only to the NS record set at the zone apex.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-170">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="fc9d6-171">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-171">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="fc9d6-172">Delete SOA or NS record sets</span><span class="sxs-lookup"><span data-stu-id="fc9d6-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="fc9d6-173">You cannot delete the SOA and NS record sets at the zone apex (name = "\@") that are created automatically when the zone is created.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-173">You cannot delete the SOA and NS record sets at the zone apex (name = "\@") that are created automatically when the zone is created.</span></span> <span data-ttu-id="fc9d6-174">They are deleted automatically when you delete the zone.</span><span class="sxs-lookup"><span data-stu-id="fc9d6-174">They are deleted automatically when you delete the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc9d6-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc9d6-175">Next steps</span></span>

* <span data-ttu-id="fc9d6-176">For more information about Azure DNS, see the [Azure DNS overview](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc9d6-176">For more information about Azure DNS, see the [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="fc9d6-177">For more information about automating DNS, see [Creating DNS zones and record sets using the .NET SDK](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="fc9d6-177">For more information about automating DNS, see [Creating DNS zones and record sets using the .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="fc9d6-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc9d6-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
