---
title: Manage DNS records in Azure DNS using the Azure CLI 1.0 | Microsoft Docs
description: Managing DNS record sets and records on Azure DNS when hosting your domain on Azure DNS. All CLI 1.0 commands for operations on record sets and records.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 3074bf378f809a9857c7ea72521961368a14772c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548771"
---
# <a name="manage-dns-records-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="0b6b9-104">Manage DNS records in Azure DNS using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0b6b9-104">Manage DNS records in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

<span data-ttu-id="0b6b9-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="0b6b9-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="0b6b9-111">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="0b6b9-111">CLI versions to complete the task</span></span>

<span data-ttu-id="0b6b9-112">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="0b6b9-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="0b6b9-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="0b6b9-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="0b6b9-115">The examples in this article assume you have already [installed the Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-115">The examples in this article assume you have already [installed the Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="0b6b9-116">Introduction</span><span class="sxs-lookup"><span data-stu-id="0b6b9-116">Introduction</span></span>

<span data-ttu-id="0b6b9-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="0b6b9-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="0b6b9-119">Create a DNS record</span><span class="sxs-lookup"><span data-stu-id="0b6b9-119">Create a DNS record</span></span>

<span data-ttu-id="0b6b9-120">To create a DNS record, use the `azure network dns record-set add-record` command.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-120">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="0b6b9-121">For help, see `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="0b6b9-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="0b6b9-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="0b6b9-124">If the record set does not already exist, this command creates it for you.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-124">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="0b6b9-125">If the record set already exists, this command adda the record you specify to the existing record set.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-125">If the record set already exists, this command adda the record you specify to the existing record set.</span></span>

<span data-ttu-id="0b6b9-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="0b6b9-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="0b6b9-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="0b6b9-129">The IP address of the A record is *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-129">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="0b6b9-130">To create a record in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span><span class="sxs-lookup"><span data-stu-id="0b6b9-130">To create a record in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="0b6b9-131">Create a DNS record set</span><span class="sxs-lookup"><span data-stu-id="0b6b9-131">Create a DNS record set</span></span>

<span data-ttu-id="0b6b9-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="0b6b9-133">You can also create the record set *explicitly* before adding records to it.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-133">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="0b6b9-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="0b6b9-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="0b6b9-136">Record sets are created using the `azure network dns record-set create` command.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-136">Record sets are created using the `azure network dns record-set create` command.</span></span> <span data-ttu-id="0b6b9-137">For help, see `azure network dns record-set create -h`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="0b6b9-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="0b6b9-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="0b6b9-140">The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span><span class="sxs-lookup"><span data-stu-id="0b6b9-140">The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="0b6b9-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`):</span><span class="sxs-lookup"><span data-stu-id="0b6b9-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="0b6b9-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="0b6b9-143">Create records of other types</span><span class="sxs-lookup"><span data-stu-id="0b6b9-143">Create records of other types</span></span>

<span data-ttu-id="0b6b9-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="0b6b9-145">The parameters used to specify the record data vary depending on the type of the record.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-145">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="0b6b9-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="0b6b9-147">The parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-147">The parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="0b6b9-148">In each case, we show how to create a single record.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-148">In each case, we show how to create a single record.</span></span> <span data-ttu-id="0b6b9-149">The record is added to the existing record set, or a record set created implicitly.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-149">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="0b6b9-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="0b6b9-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="0b6b9-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="0b6b9-153">Create an AAAA record</span><span class="sxs-lookup"><span data-stu-id="0b6b9-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="0b6b9-154">Create a CNAME record</span><span class="sxs-lookup"><span data-stu-id="0b6b9-154">Create a CNAME record</span></span>

> [!NOTE]
> The DNS standards do not permit CNAME records at the apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.
> 
> For more information, see [CNAME records](dns-zones-records.md#cname-records).

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="0b6b9-157">Create an MX record</span><span class="sxs-lookup"><span data-stu-id="0b6b9-157">Create an MX record</span></span>

<span data-ttu-id="0b6b9-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="0b6b9-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="0b6b9-159">Create an NS record</span><span class="sxs-lookup"><span data-stu-id="0b6b9-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="0b6b9-160">Create a PTR record</span><span class="sxs-lookup"><span data-stu-id="0b6b9-160">Create a PTR record</span></span>

<span data-ttu-id="0b6b9-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="0b6b9-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="0b6b9-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="0b6b9-164">Create an SRV record</span><span class="sxs-lookup"><span data-stu-id="0b6b9-164">Create an SRV record</span></span>

<span data-ttu-id="0b6b9-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="0b6b9-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="0b6b9-167">Create a TXT record</span><span class="sxs-lookup"><span data-stu-id="0b6b9-167">Create a TXT record</span></span>

<span data-ttu-id="0b6b9-168">The following example shows how to create a TXT record.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-168">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="0b6b9-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="0b6b9-170">Get a record set</span><span class="sxs-lookup"><span data-stu-id="0b6b9-170">Get a record set</span></span>

<span data-ttu-id="0b6b9-171">To retrieve an existing record set, use `azure network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-171">To retrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="0b6b9-172">For help, see `azure network dns record-set show -h`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="0b6b9-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="0b6b9-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="0b6b9-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0b6b9-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="0b6b9-176">List record sets</span><span class="sxs-lookup"><span data-stu-id="0b6b9-176">List record sets</span></span>

<span data-ttu-id="0b6b9-177">You can list all records in a DNS zone by using the `azure network dns record-set list` command.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-177">You can list all records in a DNS zone by using the `azure network dns record-set list` command.</span></span> <span data-ttu-id="0b6b9-178">For help, see `azure network dns record-set list -h`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="0b6b9-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span><span class="sxs-lookup"><span data-stu-id="0b6b9-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="0b6b9-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span><span class="sxs-lookup"><span data-stu-id="0b6b9-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="0b6b9-181">Add a record to an existing record set</span><span class="sxs-lookup"><span data-stu-id="0b6b9-181">Add a record to an existing record set</span></span>

<span data-ttu-id="0b6b9-182">You can use `azure network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-182">You can use `azure network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="0b6b9-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="0b6b9-184">Remove a record from an existing record set.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="0b6b9-185">To remove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-185">To remove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="0b6b9-186">For help, see `azure network dns record-set delete-record -h`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="0b6b9-187">This command deletes a DNS record from a record set.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="0b6b9-188">If the last record in a record set is deleted, the record set itself is **not** deleted.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-188">If the last record in a record set is deleted, the record set itself is **not** deleted.</span></span> <span data-ttu-id="0b6b9-189">Instead, an empty record set is left.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="0b6b9-190">To delete the record set instead, see [Delete a record set](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-190">To delete the record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="0b6b9-191">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-191">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="0b6b9-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="0b6b9-193">This command prompts for confirmation.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-193">This command prompts for confirmation.</span></span> <span data-ttu-id="0b6b9-194">This prompt can be suppressed using the `--quiet` switch (short form `-q`).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-194">This prompt can be suppressed using the `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="0b6b9-195">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-195">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="0b6b9-196">The confirmation prompt is suppressed.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-196">The confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="0b6b9-197">Modify an existing record set</span><span class="sxs-lookup"><span data-stu-id="0b6b9-197">Modify an existing record set</span></span>

<span data-ttu-id="0b6b9-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="0b6b9-199">The following sections explain how to modify each of these properties.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-199">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="0b6b9-200">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span><span class="sxs-lookup"><span data-stu-id="0b6b9-200">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="0b6b9-201">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-201">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="0b6b9-202">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-202">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="0b6b9-203">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="0b6b9-203">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="0b6b9-204">You cannot add, remove, or modify the records in the automatically created NS record set at the zone apex (`-Name "@"`, including quote marks).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-204">You cannot add, remove, or modify the records in the automatically created NS record set at the zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="0b6b9-205">For this record set, the only changes permitted are to modify the record set TTL and metadata.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-205">For this record set, the only changes permitted are to modify the record set TTL and metadata.</span></span>

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="0b6b9-206">To modify a CNAME record</span><span class="sxs-lookup"><span data-stu-id="0b6b9-206">To modify a CNAME record</span></span>

<span data-ttu-id="0b6b9-207">To modify a CNAME record, use `azure network dns record-set add-record` to add the new record value.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-207">To modify a CNAME record, use `azure network dns record-set add-record` to add the new record value.</span></span> <span data-ttu-id="0b6b9-208">Unlike other record types, a CNAME record set can only contain a single record.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-208">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="0b6b9-209">Therefore, the existing record is *replaced* when the new record is added, and does not need to be deleted separately.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-209">Therefore, the existing record is *replaced* when the new record is added, and does not need to be deleted separately.</span></span>  <span data-ttu-id="0b6b9-210">You will be prompted to accept this replacement.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-210">You will be prompted to accept this replacement.</span></span>

<span data-ttu-id="0b6b9-211">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span><span class="sxs-lookup"><span data-stu-id="0b6b9-211">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="0b6b9-212">To modify an SOA record</span><span class="sxs-lookup"><span data-stu-id="0b6b9-212">To modify an SOA record</span></span>

<span data-ttu-id="0b6b9-213">Use `azure network dns record-set set-soa-record` to modify the SOA for a given DNS zone.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-213">Use `azure network dns record-set set-soa-record` to modify the SOA for a given DNS zone.</span></span> <span data-ttu-id="0b6b9-214">For help, see `azure network dns record-set set-soa-record -h`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-214">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="0b6b9-215">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0b6b9-215">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="0b6b9-216">To modify the TTL of an existing record set</span><span class="sxs-lookup"><span data-stu-id="0b6b9-216">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="0b6b9-217">To modify the TTL of an existing record set, use `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-217">To modify the TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="0b6b9-218">For help, see `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-218">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="0b6b9-219">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span><span class="sxs-lookup"><span data-stu-id="0b6b9-219">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="0b6b9-220">To modify the metadata of an existing record set</span><span class="sxs-lookup"><span data-stu-id="0b6b9-220">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="0b6b9-221">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-221">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="0b6b9-222">To modify the metadata of an existing record set, use `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-222">To modify the metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="0b6b9-223">For help, see `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-223">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="0b6b9-224">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-224">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="0b6b9-225">Note that any existing metadata is *replaced* by the values given.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-225">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="0b6b9-226">Delete a record set</span><span class="sxs-lookup"><span data-stu-id="0b6b9-226">Delete a record set</span></span>

<span data-ttu-id="0b6b9-227">Record sets can be deleted by using the `azure network dns record-set delete` command.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-227">Record sets can be deleted by using the `azure network dns record-set delete` command.</span></span> <span data-ttu-id="0b6b9-228">For help, see `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-228">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="0b6b9-229">Deleting a record set also deletes all records within the record set.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-229">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> You cannot delete the SOA and NS record sets at the zone apex (`-Name "@"`).  These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.

<span data-ttu-id="0b6b9-232">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0b6b9-232">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="0b6b9-233">You are prompted to confirm the delete operation.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-233">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="0b6b9-234">To suppress this prompt, use the `--quiet` switch (short form `-q`).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-234">To suppress this prompt, use the `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b6b9-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="0b6b9-235">Next steps</span></span>

<span data-ttu-id="0b6b9-236">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="0b6b9-236">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="0b6b9-237">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0b6b9-237">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
