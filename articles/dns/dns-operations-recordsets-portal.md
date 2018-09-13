---
title: Manage DNS record sets and records with Azure DNS | Microsoft Docs
description: Azure DNS provides the capability to manage DNS record sets and records when hosting your domain.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: b79fe466bd4d128e5f8151aaaba88d5b6b591138
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563184"
---
# <a name="manage-dns-records-and-record-sets-by-using-the-azure-portal"></a><span data-ttu-id="33c1c-103">Manage DNS records and record sets by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="33c1c-103">Manage DNS records and record sets by using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

<span data-ttu-id="33c1c-107">This article shows you how to manage record sets and records for your DNS zone by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33c1c-107">This article shows you how to manage record sets and records for your DNS zone by using the Azure portal.</span></span>

<span data-ttu-id="33c1c-108">It's important to understand the difference between DNS record sets and individual DNS records.</span><span class="sxs-lookup"><span data-stu-id="33c1c-108">It's important to understand the difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="33c1c-109">A record set is a collection of records in a zone that have the same name and are the same type.</span><span class="sxs-lookup"><span data-stu-id="33c1c-109">A record set is a collection of records in a zone that have the same name and are the same type.</span></span> <span data-ttu-id="33c1c-110">For more information, see [Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="33c1c-110">For more information, see [Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="33c1c-111">Create a new record set and record</span><span class="sxs-lookup"><span data-stu-id="33c1c-111">Create a new record set and record</span></span>

<span data-ttu-id="33c1c-112">To create a record set in the Azure portal, see [Create DNS records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="33c1c-112">To create a record set in the Azure portal, see [Create DNS records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="33c1c-113">View a record set</span><span class="sxs-lookup"><span data-stu-id="33c1c-113">View a record set</span></span>

1. <span data-ttu-id="33c1c-114">In the Azure portal, go to the **DNS zone** blade.</span><span class="sxs-lookup"><span data-stu-id="33c1c-114">In the Azure portal, go to the **DNS zone** blade.</span></span>
2. <span data-ttu-id="33c1c-115">Search for the record set and select it.</span><span class="sxs-lookup"><span data-stu-id="33c1c-115">Search for the record set and select it.</span></span> <span data-ttu-id="33c1c-116">This opens the record set properties.</span><span class="sxs-lookup"><span data-stu-id="33c1c-116">This opens the record set properties.</span></span>

    ![Search for a record set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-to-a-record-set"></a><span data-ttu-id="33c1c-118">Add a new record to a record set</span><span class="sxs-lookup"><span data-stu-id="33c1c-118">Add a new record to a record set</span></span>

<span data-ttu-id="33c1c-119">You can add up to 20 records to any record set.</span><span class="sxs-lookup"><span data-stu-id="33c1c-119">You can add up to 20 records to any record set.</span></span> <span data-ttu-id="33c1c-120">A record set cannot contain two identical records.</span><span class="sxs-lookup"><span data-stu-id="33c1c-120">A record set cannot contain two identical records.</span></span> <span data-ttu-id="33c1c-121">Empty record sets (with zero records) can be created, but do not appear on the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="33c1c-121">Empty record sets (with zero records) can be created, but do not appear on the Azure DNS name servers.</span></span> <span data-ttu-id="33c1c-122">Record sets of type CNAME can contain one record at most.</span><span class="sxs-lookup"><span data-stu-id="33c1c-122">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="33c1c-123">On the **Record set properties** blade for your DNS zone, click the record set that you want to add a record to.</span><span class="sxs-lookup"><span data-stu-id="33c1c-123">On the **Record set properties** blade for your DNS zone, click the record set that you want to add a record to.</span></span>

    ![Select a record set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="33c1c-125">Specify the record set properties by filling in the fields.</span><span class="sxs-lookup"><span data-stu-id="33c1c-125">Specify the record set properties by filling in the fields.</span></span>

    ![Add a record](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="33c1c-127">Click **Save** at the top of the blade to save your settings.</span><span class="sxs-lookup"><span data-stu-id="33c1c-127">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="33c1c-128">Then close the blade.</span><span class="sxs-lookup"><span data-stu-id="33c1c-128">Then close the blade.</span></span>
4. <span data-ttu-id="33c1c-129">In the corner, you will see that the record is saving.</span><span class="sxs-lookup"><span data-stu-id="33c1c-129">In the corner, you will see that the record is saving.</span></span>

    ![Saving record set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="33c1c-131">After the record has been saved, the values on the **DNS zone** blade will reflect the new record.</span><span class="sxs-lookup"><span data-stu-id="33c1c-131">After the record has been saved, the values on the **DNS zone** blade will reflect the new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="33c1c-132">Update a record</span><span class="sxs-lookup"><span data-stu-id="33c1c-132">Update a record</span></span>

<span data-ttu-id="33c1c-133">When you update a record in an existing record set, the fields you can update depend on the type of record you're working with.</span><span class="sxs-lookup"><span data-stu-id="33c1c-133">When you update a record in an existing record set, the fields you can update depend on the type of record you're working with.</span></span>

1. <span data-ttu-id="33c1c-134">On the **Record set properties** blade for your record set, search for the record.</span><span class="sxs-lookup"><span data-stu-id="33c1c-134">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="33c1c-135">Modify the record.</span><span class="sxs-lookup"><span data-stu-id="33c1c-135">Modify the record.</span></span> <span data-ttu-id="33c1c-136">When you modify a record, you can change the available settings for the record.</span><span class="sxs-lookup"><span data-stu-id="33c1c-136">When you modify a record, you can change the available settings for the record.</span></span> <span data-ttu-id="33c1c-137">In the following example, the **IP address** field is selected, and the IP address is in the process of being modified.</span><span class="sxs-lookup"><span data-stu-id="33c1c-137">In the following example, the **IP address** field is selected, and the IP address is in the process of being modified.</span></span>

    ![Modify a record](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="33c1c-139">Click **Save** at the top of the blade to save your settings.</span><span class="sxs-lookup"><span data-stu-id="33c1c-139">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="33c1c-140">In the upper right corner, you'll see the notification that the record has been saved.</span><span class="sxs-lookup"><span data-stu-id="33c1c-140">In the upper right corner, you'll see the notification that the record has been saved.</span></span>

    ![Saved record set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="33c1c-142">After the record has been saved, the values for the record set on the **DNS zone** blade will reflect the updated record.</span><span class="sxs-lookup"><span data-stu-id="33c1c-142">After the record has been saved, the values for the record set on the **DNS zone** blade will reflect the updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="33c1c-143">Remove a record from a record set</span><span class="sxs-lookup"><span data-stu-id="33c1c-143">Remove a record from a record set</span></span>

<span data-ttu-id="33c1c-144">You can use the Azure portal to remove records from a record set.</span><span class="sxs-lookup"><span data-stu-id="33c1c-144">You can use the Azure portal to remove records from a record set.</span></span> <span data-ttu-id="33c1c-145">Note that removing the last record from a record set does not delete the record set.</span><span class="sxs-lookup"><span data-stu-id="33c1c-145">Note that removing the last record from a record set does not delete the record set.</span></span>

1. <span data-ttu-id="33c1c-146">On the **Record set properties** blade for your record set, search for the record.</span><span class="sxs-lookup"><span data-stu-id="33c1c-146">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="33c1c-147">Click the record that you want to remove.</span><span class="sxs-lookup"><span data-stu-id="33c1c-147">Click the record that you want to remove.</span></span> <span data-ttu-id="33c1c-148">Then select **Remove**.</span><span class="sxs-lookup"><span data-stu-id="33c1c-148">Then select **Remove**.</span></span>

    ![Remove a record](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="33c1c-150">Click **Save** at the top of the blade to save your settings.</span><span class="sxs-lookup"><span data-stu-id="33c1c-150">Click **Save** at the top of the blade to save your settings.</span></span>
4. <span data-ttu-id="33c1c-151">After the record has been removed, the values for the record on the **DNS zone** blade will reflect the removal.</span><span class="sxs-lookup"><span data-stu-id="33c1c-151">After the record has been removed, the values for the record on the **DNS zone** blade will reflect the removal.</span></span>

## <a name="delete"></a><span data-ttu-id="33c1c-152">Delete a record set</span><span class="sxs-lookup"><span data-stu-id="33c1c-152">Delete a record set</span></span>

1. <span data-ttu-id="33c1c-153">On the **Record set properties** blade for your record set, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="33c1c-153">On the **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Delete a record set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="33c1c-155">A message appears asking if you want to delete the record set.</span><span class="sxs-lookup"><span data-stu-id="33c1c-155">A message appears asking if you want to delete the record set.</span></span>
3. <span data-ttu-id="33c1c-156">Verify that the name matches the record set that you want to delete, and then click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="33c1c-156">Verify that the name matches the record set that you want to delete, and then click **Yes**.</span></span>
4. <span data-ttu-id="33c1c-157">On the **DNS zone** blade, verify that the record set is no longer visible.</span><span class="sxs-lookup"><span data-stu-id="33c1c-157">On the **DNS zone** blade, verify that the record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="33c1c-158">Work with NS and SOA records</span><span class="sxs-lookup"><span data-stu-id="33c1c-158">Work with NS and SOA records</span></span>

<span data-ttu-id="33c1c-159">NS and SOA records that are automatically created are managed differently from other record types.</span><span class="sxs-lookup"><span data-stu-id="33c1c-159">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="33c1c-160">Modify SOA records</span><span class="sxs-lookup"><span data-stu-id="33c1c-160">Modify SOA records</span></span>

<span data-ttu-id="33c1c-161">You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "@").</span><span class="sxs-lookup"><span data-stu-id="33c1c-161">You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "@").</span></span> <span data-ttu-id="33c1c-162">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span><span class="sxs-lookup"><span data-stu-id="33c1c-162">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

### <a name="modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="33c1c-163">Modify NS records at the zone apex</span><span class="sxs-lookup"><span data-stu-id="33c1c-163">Modify NS records at the zone apex</span></span>

<span data-ttu-id="33c1c-164">You cannot add to, remove, or modify the records in the automatically created NS record set at the zone apex (name = "@").</span><span class="sxs-lookup"><span data-stu-id="33c1c-164">You cannot add to, remove, or modify the records in the automatically created NS record set at the zone apex (name = "@").</span></span> <span data-ttu-id="33c1c-165">The only change that's permitted is to modify the record set TTL.</span><span class="sxs-lookup"><span data-stu-id="33c1c-165">The only change that's permitted is to modify the record set TTL.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="33c1c-166">Delete SOA or NS record sets</span><span class="sxs-lookup"><span data-stu-id="33c1c-166">Delete SOA or NS record sets</span></span>

<span data-ttu-id="33c1c-167">You cannot delete the SOA and NS record sets at the zone apex (name = "@") that are created automatically when the zone is created.</span><span class="sxs-lookup"><span data-stu-id="33c1c-167">You cannot delete the SOA and NS record sets at the zone apex (name = "@") that are created automatically when the zone is created.</span></span> <span data-ttu-id="33c1c-168">They are deleted automatically when you delete the zone.</span><span class="sxs-lookup"><span data-stu-id="33c1c-168">They are deleted automatically when you delete the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33c1c-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="33c1c-169">Next steps</span></span>

* <span data-ttu-id="33c1c-170">For more information about Azure DNS, see the [Azure DNS overview](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="33c1c-170">For more information about Azure DNS, see the [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="33c1c-171">For more information about automating DNS, see [Creating DNS zones and record sets using the .NET SDK](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="33c1c-171">For more information about automating DNS, see [Creating DNS zones and record sets using the .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="33c1c-172">For more information about reverse DNS records, see [How to manage reverse DNS records for your services using PowerShell](dns-reverse-dns-record-operations-ps.md).</span><span class="sxs-lookup"><span data-stu-id="33c1c-172">For more information about reverse DNS records, see [How to manage reverse DNS records for your services using PowerShell](dns-reverse-dns-record-operations-ps.md).</span></span>








