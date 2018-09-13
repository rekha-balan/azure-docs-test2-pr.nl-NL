---
title: Manage DNS records in Azure DNS using the Azure CLI 2.0 | Microsoft Docs
description: Managing DNS record sets and records on Azure DNS when hosting your domain on Azure DNS. All CLI 2.0 commands for operations on record sets and records.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: jonatul
ms.openlocfilehash: 3f76d7377250d7014067ae36dad3ebd56b1291fe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549519"
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="344b6-104">Manage DNS records and recordsets in Azure DNS using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="344b6-104">Manage DNS records and recordsets in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

<span data-ttu-id="344b6-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="344b6-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="344b6-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="344b6-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="344b6-111">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="344b6-111">CLI versions to complete the task</span></span>

<span data-ttu-id="344b6-112">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="344b6-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="344b6-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span><span class="sxs-lookup"><span data-stu-id="344b6-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="344b6-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span><span class="sxs-lookup"><span data-stu-id="344b6-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="344b6-115">The examples in this article assume you have already [installed the Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="344b6-115">The examples in this article assume you have already [installed the Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="344b6-116">Introduction</span><span class="sxs-lookup"><span data-stu-id="344b6-116">Introduction</span></span>

<span data-ttu-id="344b6-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span><span class="sxs-lookup"><span data-stu-id="344b6-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="344b6-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="344b6-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="344b6-119">Create a DNS record</span><span class="sxs-lookup"><span data-stu-id="344b6-119">Create a DNS record</span></span>

<span data-ttu-id="344b6-120">To create a DNS record, use the `az network dns record-set <recordtype> add-record` command.</span><span class="sxs-lookup"><span data-stu-id="344b6-120">To create a DNS record, use the `az network dns record-set <recordtype> add-record` command.</span></span> <span data-ttu-id="344b6-121">(Where recordtype is the type of record, i.e</span><span class="sxs-lookup"><span data-stu-id="344b6-121">(Where recordtype is the type of record, i.e</span></span> <span data-ttu-id="344b6-122">A, SRV, TXT, etc) For help, see `az network dns record-set --help`.</span><span class="sxs-lookup"><span data-stu-id="344b6-122">A, SRV, TXT, etc) For help, see `az network dns record-set --help`.</span></span>

<span data-ttu-id="344b6-123">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span><span class="sxs-lookup"><span data-stu-id="344b6-123">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="344b6-124">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span><span class="sxs-lookup"><span data-stu-id="344b6-124">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="344b6-125">If the record set does not already exist, this command creates it for you.</span><span class="sxs-lookup"><span data-stu-id="344b6-125">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="344b6-126">If the record set already exists, this command adda the record you specify to the existing record set.</span><span class="sxs-lookup"><span data-stu-id="344b6-126">If the record set already exists, this command adda the record you specify to the existing record set.</span></span>

<span data-ttu-id="344b6-127">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span><span class="sxs-lookup"><span data-stu-id="344b6-127">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="344b6-128">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="344b6-128">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="344b6-129">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="344b6-129">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="344b6-130">The IP address of the A record is *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="344b6-130">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
az network dns record-set a add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="344b6-131">To create a record set in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span><span class="sxs-lookup"><span data-stu-id="344b6-131">To create a record set in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
az network dns record-set a add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="344b6-132">Create a DNS record set</span><span class="sxs-lookup"><span data-stu-id="344b6-132">Create a DNS record set</span></span>

<span data-ttu-id="344b6-133">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span><span class="sxs-lookup"><span data-stu-id="344b6-133">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="344b6-134">You can also create the record set *explicitly* before adding records to it.</span><span class="sxs-lookup"><span data-stu-id="344b6-134">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="344b6-135">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span><span class="sxs-lookup"><span data-stu-id="344b6-135">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="344b6-136">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="344b6-136">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="344b6-137">Record sets are created using the `az network dns record-set create` command.</span><span class="sxs-lookup"><span data-stu-id="344b6-137">Record sets are created using the `az network dns record-set create` command.</span></span> <span data-ttu-id="344b6-138">For help, see `az network dns record-set create --help`.</span><span class="sxs-lookup"><span data-stu-id="344b6-138">For help, see `az network dns record-set create --help`.</span></span>

<span data-ttu-id="344b6-139">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span><span class="sxs-lookup"><span data-stu-id="344b6-139">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="344b6-140">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="344b6-140">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="344b6-141">The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span><span class="sxs-lookup"><span data-stu-id="344b6-141">The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
az network dns record-set create --resource-group myresourcegroup --zone-name contoso.com --name www --type A --ttl 60
```

<span data-ttu-id="344b6-142">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter :</span><span class="sxs-lookup"><span data-stu-id="344b6-142">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter :</span></span>

```azurecli
az network dns record-set create --resource-group myresourcegroup --zone-name contoso.com --name www --type A --metadata "dept=finance" "environment=production"
```

<span data-ttu-id="344b6-143">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="344b6-143">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="344b6-144">Create records of other types</span><span class="sxs-lookup"><span data-stu-id="344b6-144">Create records of other types</span></span>

<span data-ttu-id="344b6-145">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="344b6-145">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="344b6-146">The parameters used to specify the record data vary depending on the type of the record.</span><span class="sxs-lookup"><span data-stu-id="344b6-146">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="344b6-147">For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="344b6-147">For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="344b6-148">The parameters for each record type can be listed using `az network dns record-set <type> add-record --help`.</span><span class="sxs-lookup"><span data-stu-id="344b6-148">The parameters for each record type can be listed using `az network dns record-set <type> add-record --help`.</span></span>

<span data-ttu-id="344b6-149">In each case, we show how to create a single record.</span><span class="sxs-lookup"><span data-stu-id="344b6-149">In each case, we show how to create a single record.</span></span> <span data-ttu-id="344b6-150">The record is added to the existing record set, or a record set created implicitly.</span><span class="sxs-lookup"><span data-stu-id="344b6-150">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="344b6-151">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="344b6-151">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="344b6-152">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span><span class="sxs-lookup"><span data-stu-id="344b6-152">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="344b6-153">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="344b6-153">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="344b6-154">Create an AAAA record</span><span class="sxs-lookup"><span data-stu-id="344b6-154">Create an AAAA record</span></span>

```azurecli
az network dns record-set aaaa add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="344b6-155">Create a CNAME record</span><span class="sxs-lookup"><span data-stu-id="344b6-155">Create a CNAME record</span></span>

> [!NOTE]
> The DNS standards do not permit CNAME records at the apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.
> 
> For more information, see [CNAME records](dns-zones-records.md#cname-records).

```azurecli
az network dns record-set cname add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="344b6-158">Create an MX record</span><span class="sxs-lookup"><span data-stu-id="344b6-158">Create an MX record</span></span>

<span data-ttu-id="344b6-159">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="344b6-159">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
az network dns record-set mx add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="344b6-160">Create an NS record</span><span class="sxs-lookup"><span data-stu-id="344b6-160">Create an NS record</span></span>

```azurecli
az network dns record-set ns add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "test-ns" --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="344b6-161">Create a PTR record</span><span class="sxs-lookup"><span data-stu-id="344b6-161">Create a PTR record</span></span>

<span data-ttu-id="344b6-162">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span><span class="sxs-lookup"><span data-stu-id="344b6-162">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="344b6-163">Each PTR record set in this zone corresponds to an IP address within this IP range.</span><span class="sxs-lookup"><span data-stu-id="344b6-163">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="344b6-164">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span><span class="sxs-lookup"><span data-stu-id="344b6-164">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
az network dns record-set ptr add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "my-arpa.zone.com" --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="344b6-165">Create an SRV record</span><span class="sxs-lookup"><span data-stu-id="344b6-165">Create an SRV record</span></span>

<span data-ttu-id="344b6-166">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span><span class="sxs-lookup"><span data-stu-id="344b6-166">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="344b6-167">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span><span class="sxs-lookup"><span data-stu-id="344b6-167">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
az network dns record srv add --resource-group myresourcegroup --zone-name contoso.com --record-set-name "_sip.tls" --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="344b6-168">Create a TXT record</span><span class="sxs-lookup"><span data-stu-id="344b6-168">Create a TXT record</span></span>

<span data-ttu-id="344b6-169">The following example shows how to create a TXT record.</span><span class="sxs-lookup"><span data-stu-id="344b6-169">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="344b6-170">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="344b6-170">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
az network dns record-set txt add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "test-txt" --value "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="344b6-171">Get a record set</span><span class="sxs-lookup"><span data-stu-id="344b6-171">Get a record set</span></span>

<span data-ttu-id="344b6-172">To retrieve an existing record set, use `az network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="344b6-172">To retrieve an existing record set, use `az network dns record-set show`.</span></span> <span data-ttu-id="344b6-173">For help, see `az network dns record-set show --help`.</span><span class="sxs-lookup"><span data-stu-id="344b6-173">For help, see `az network dns record-set show --help`.</span></span>

<span data-ttu-id="344b6-174">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span><span class="sxs-lookup"><span data-stu-id="344b6-174">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="344b6-175">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span><span class="sxs-lookup"><span data-stu-id="344b6-175">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="344b6-176">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="344b6-176">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set show --resource-group myresourcegroup --zone-name contoso.com --name www --type A
```

## <a name="list-record-sets"></a><span data-ttu-id="344b6-177">List record sets</span><span class="sxs-lookup"><span data-stu-id="344b6-177">List record sets</span></span>

<span data-ttu-id="344b6-178">You can list all records in a DNS zone by using the `az network dns record-set list` command.</span><span class="sxs-lookup"><span data-stu-id="344b6-178">You can list all records in a DNS zone by using the `az network dns record-set list` command.</span></span> <span data-ttu-id="344b6-179">For help, see `az network dns record-set list --help`.</span><span class="sxs-lookup"><span data-stu-id="344b6-179">For help, see `az network dns record-set list --help`.</span></span>

<span data-ttu-id="344b6-180">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span><span class="sxs-lookup"><span data-stu-id="344b6-180">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

<span data-ttu-id="344b6-181">This example returns all record sets that match the given record type (in this case, 'A' records):</span><span class="sxs-lookup"><span data-stu-id="344b6-181">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
az network dns record-setA a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="344b6-182">Add a record to an existing record set</span><span class="sxs-lookup"><span data-stu-id="344b6-182">Add a record to an existing record set</span></span>

<span data-ttu-id="344b6-183">You can use `az network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.</span><span class="sxs-lookup"><span data-stu-id="344b6-183">You can use `az network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="344b6-184">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span><span class="sxs-lookup"><span data-stu-id="344b6-184">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="344b6-185">Remove a record from an existing record set.</span><span class="sxs-lookup"><span data-stu-id="344b6-185">Remove a record from an existing record set.</span></span>

<span data-ttu-id="344b6-186">To remove a DNS record from an existing record set, use `az network dns record-set ? remove-record` (where ?</span><span class="sxs-lookup"><span data-stu-id="344b6-186">To remove a DNS record from an existing record set, use `az network dns record-set ? remove-record` (where ?</span></span> <span data-ttu-id="344b6-187">is the record type).</span><span class="sxs-lookup"><span data-stu-id="344b6-187">is the record type).</span></span> <span data-ttu-id="344b6-188">For help, see `az network dns record-set -h`.</span><span class="sxs-lookup"><span data-stu-id="344b6-188">For help, see `az network dns record-set -h`.</span></span>

<span data-ttu-id="344b6-189">This command deletes a DNS record from a record set.</span><span class="sxs-lookup"><span data-stu-id="344b6-189">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="344b6-190">If the last record in a record set is deleted, the record set itself is **not** deleted.</span><span class="sxs-lookup"><span data-stu-id="344b6-190">If the last record in a record set is deleted, the record set itself is **not** deleted.</span></span> <span data-ttu-id="344b6-191">Instead, an empty record set is left.</span><span class="sxs-lookup"><span data-stu-id="344b6-191">Instead, an empty record set is left.</span></span> <span data-ttu-id="344b6-192">To delete the record set instead, see [Delete a record set](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="344b6-192">To delete the record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="344b6-193">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="344b6-193">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="344b6-194">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span><span class="sxs-lookup"><span data-stu-id="344b6-194">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="344b6-195">This command prompts for confirmation.</span><span class="sxs-lookup"><span data-stu-id="344b6-195">This command prompts for confirmation.</span></span> <span data-ttu-id="344b6-196">This prompt can be suppressed using the `--yes` switch.</span><span class="sxs-lookup"><span data-stu-id="344b6-196">This prompt can be suppressed using the `--yes` switch.</span></span>

<span data-ttu-id="344b6-197">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="344b6-197">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="344b6-198">The confirmation prompt is suppressed.</span><span class="sxs-lookup"><span data-stu-id="344b6-198">The confirmation prompt is suppressed.</span></span>

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4 --yes
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="344b6-199">Modify an existing record set</span><span class="sxs-lookup"><span data-stu-id="344b6-199">Modify an existing record set</span></span>

<span data-ttu-id="344b6-200">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span><span class="sxs-lookup"><span data-stu-id="344b6-200">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="344b6-201">The following sections explain how to modify each of these properties.</span><span class="sxs-lookup"><span data-stu-id="344b6-201">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="344b6-202">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span><span class="sxs-lookup"><span data-stu-id="344b6-202">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="344b6-203">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span><span class="sxs-lookup"><span data-stu-id="344b6-203">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="344b6-204">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span><span class="sxs-lookup"><span data-stu-id="344b6-204">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="344b6-205">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="344b6-205">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
az network dns record-set a add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

<span data-ttu-id="344b6-206">You cannot add, remove, or modify the records in the automatically created NS record set at the zone apex (`--Name "@"`, including quote marks).</span><span class="sxs-lookup"><span data-stu-id="344b6-206">You cannot add, remove, or modify the records in the automatically created NS record set at the zone apex (`--Name "@"`, including quote marks).</span></span> <span data-ttu-id="344b6-207">For this record set, the only changes permitted are to modify the record set TTL and metadata.</span><span class="sxs-lookup"><span data-stu-id="344b6-207">For this record set, the only changes permitted are to modify the record set TTL and metadata.</span></span>

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="344b6-208">To modify a CNAME record</span><span class="sxs-lookup"><span data-stu-id="344b6-208">To modify a CNAME record</span></span>

<span data-ttu-id="344b6-209">To modify a CNAME record, use `az network dns record-set update` with the --set switch to add the new record value.</span><span class="sxs-lookup"><span data-stu-id="344b6-209">To modify a CNAME record, use `az network dns record-set update` with the --set switch to add the new record value.</span></span> <span data-ttu-id="344b6-210">Unlike other record types, a CNAME record set can only contain a single record.</span><span class="sxs-lookup"><span data-stu-id="344b6-210">Unlike other record types, a CNAME record set can only contain a single record.</span></span>

<span data-ttu-id="344b6-211">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span><span class="sxs-lookup"><span data-stu-id="344b6-211">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
az network dns record-set update --resource-group myresourcegroup --zone-name contoso.com --name test-cname --type cname --set cnameRecord.cname=www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="344b6-212">To modify an SOA record</span><span class="sxs-lookup"><span data-stu-id="344b6-212">To modify an SOA record</span></span>

<span data-ttu-id="344b6-213">Use `az network dns record-set soa update` to modify the SOA for a given DNS zone.</span><span class="sxs-lookup"><span data-stu-id="344b6-213">Use `az network dns record-set soa update` to modify the SOA for a given DNS zone.</span></span> <span data-ttu-id="344b6-214">For help, see `az network dns record soa update --help`.</span><span class="sxs-lookup"><span data-stu-id="344b6-214">For help, see `az network dns record soa update --help`.</span></span>

<span data-ttu-id="344b6-215">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="344b6-215">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="344b6-216">To modify the TTL of an existing record set</span><span class="sxs-lookup"><span data-stu-id="344b6-216">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="344b6-217">To modify the TTL of an existing record set, use `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="344b6-217">To modify the TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="344b6-218">For help, see `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="344b6-218">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="344b6-219">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span><span class="sxs-lookup"><span data-stu-id="344b6-219">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
az network dns record-set update --resource-group myresourcegroup --zone-name contoso.com --name "www" --type A --set ttl=60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="344b6-220">To modify the metadata of an existing record set</span><span class="sxs-lookup"><span data-stu-id="344b6-220">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="344b6-221">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="344b6-221">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="344b6-222">To modify the metadata of an existing record set, use `az network dns record-set update`.</span><span class="sxs-lookup"><span data-stu-id="344b6-222">To modify the metadata of an existing record set, use `az network dns record-set update`.</span></span> <span data-ttu-id="344b6-223">For help, see `az network dns record-set update --help`.</span><span class="sxs-lookup"><span data-stu-id="344b6-223">For help, see `az network dns record-set update --help`.</span></span>

<span data-ttu-id="344b6-224">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`).</span><span class="sxs-lookup"><span data-stu-id="344b6-224">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="344b6-225">Note that any existing metadata is *replaced* by the values given.</span><span class="sxs-lookup"><span data-stu-id="344b6-225">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
az network dns record-set update --resource-group myresourcegroup --zone-name contoso.com --name "www" --type A --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a><span data-ttu-id="344b6-226">Delete a record set</span><span class="sxs-lookup"><span data-stu-id="344b6-226">Delete a record set</span></span>

<span data-ttu-id="344b6-227">Record sets can be deleted by using the `azure network dns record-set delete` command.</span><span class="sxs-lookup"><span data-stu-id="344b6-227">Record sets can be deleted by using the `azure network dns record-set delete` command.</span></span> <span data-ttu-id="344b6-228">For help, see `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="344b6-228">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="344b6-229">Deleting a record set also deletes all records within the record set.</span><span class="sxs-lookup"><span data-stu-id="344b6-229">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> You cannot delete the SOA and NS record sets at the zone apex (`-Name "@"`).  These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.

<span data-ttu-id="344b6-232">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="344b6-232">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set delete --resource-group myresourcegroup --zone-name contoso.com --name www --type a
```

<span data-ttu-id="344b6-233">You are prompted to confirm the delete operation.</span><span class="sxs-lookup"><span data-stu-id="344b6-233">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="344b6-234">To suppress this prompt, use the `--yes` switch.</span><span class="sxs-lookup"><span data-stu-id="344b6-234">To suppress this prompt, use the `--yes` switch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="344b6-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="344b6-235">Next steps</span></span>

<span data-ttu-id="344b6-236">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="344b6-236">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="344b6-237">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="344b6-237">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
