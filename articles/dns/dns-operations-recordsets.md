---
title: Manage DNS records in Azure DNS using Azure PowerShell | Microsoft Docs
description: Managing DNS record sets and records on Azure DNS when hosting your domain on Azure DNS. All PowerShell commands for operations on record sets and records.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 51ed9893aa0a49b2bde5069cfcad222b0bae4fdc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540706"
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="6b207-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b207-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

<span data-ttu-id="6b207-108">This article shows you how to manage DNS records for your DNS zone by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b207-108">This article shows you how to manage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="6b207-109">DNS records can also be managed by using the cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6b207-109">DNS records can also be managed by using the cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="6b207-110">The examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="6b207-110">The examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="6b207-111">Introduction</span><span class="sxs-lookup"><span data-stu-id="6b207-111">Introduction</span></span>

<span data-ttu-id="6b207-112">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span><span class="sxs-lookup"><span data-stu-id="6b207-112">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="6b207-113">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="6b207-113">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="6b207-114">Create a new DNS record</span><span class="sxs-lookup"><span data-stu-id="6b207-114">Create a new DNS record</span></span>

<span data-ttu-id="6b207-115">If your new record has the same name and type as an existing record, you need to [add it to the existing record set](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="6b207-115">If your new record has the same name and type as an existing record, you need to [add it to the existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="6b207-116">If your new record has a different name and type to all existing records, you need to create a new record set.</span><span class="sxs-lookup"><span data-stu-id="6b207-116">If your new record has a different name and type to all existing records, you need to create a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="6b207-117">Create A records in a new record set</span><span class="sxs-lookup"><span data-stu-id="6b207-117">Create A records in a new record set</span></span>

<span data-ttu-id="6b207-118">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6b207-118">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="6b207-119">When creating a record set, you need to specify the record set name, the zone, the time to live (TTL), the record type, and the records to be created.</span><span class="sxs-lookup"><span data-stu-id="6b207-119">When creating a record set, you need to specify the record set name, the zone, the time to live (TTL), the record type, and the records to be created.</span></span>

<span data-ttu-id="6b207-120">The parameters for adding records to a record set vary depending on the type of the record set.</span><span class="sxs-lookup"><span data-stu-id="6b207-120">The parameters for adding records to a record set vary depending on the type of the record set.</span></span> <span data-ttu-id="6b207-121">For example, when using a record set of type 'A', you need to specify the IP address using the parameter `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="6b207-121">For example, when using a record set of type 'A', you need to specify the IP address using the parameter `-IPv4Address`.</span></span> <span data-ttu-id="6b207-122">Other parameters are used for other record types.</span><span class="sxs-lookup"><span data-stu-id="6b207-122">Other parameters are used for other record types.</span></span> <span data-ttu-id="6b207-123">See [Additional record type examples](#additional-record-type-examples) for details.</span><span class="sxs-lookup"><span data-stu-id="6b207-123">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="6b207-124">The following example creates a record set with the relative name 'www' in the DNS Zone 'contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="6b207-124">The following example creates a record set with the relative name 'www' in the DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="6b207-125">The fully-qualified name of the record set is 'www.contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="6b207-125">The fully-qualified name of the record set is 'www.contoso.com'.</span></span> <span data-ttu-id="6b207-126">The record type is 'A, and the TTL is 3600 seconds.</span><span class="sxs-lookup"><span data-stu-id="6b207-126">The record type is 'A, and the TTL is 3600 seconds.</span></span> <span data-ttu-id="6b207-127">The record set contains a single record, with IP address '1.2.3.4'.</span><span class="sxs-lookup"><span data-stu-id="6b207-127">The record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="6b207-128">To create a record set at the 'apex' of a zone (in this case, 'contoso.com'), use the record set name '@' (excluding quotation marks):</span><span class="sxs-lookup"><span data-stu-id="6b207-128">To create a record set at the 'apex' of a zone (in this case, 'contoso.com'), use the record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="6b207-129">If you need to create a record set containing more than one record, first create a local array and add the records, then pass the array to `New-AzureRmDnsRecordSet` as follows:</span><span class="sxs-lookup"><span data-stu-id="6b207-129">If you need to create a record set containing more than one record, first create a local array and add the records, then pass the array to `New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="6b207-130">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="6b207-130">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="6b207-131">The following example shows how to create a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span><span class="sxs-lookup"><span data-stu-id="6b207-131">The following example shows how to create a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="6b207-132">Azure DNS also supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span><span class="sxs-lookup"><span data-stu-id="6b207-132">Azure DNS also supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="6b207-133">Empty record sets are visible in the Azure DNS control plane, but do appear on the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="6b207-133">Empty record sets are visible in the Azure DNS control plane, but do appear on the Azure DNS name servers.</span></span> <span data-ttu-id="6b207-134">The following example creates an empty record set:</span><span class="sxs-lookup"><span data-stu-id="6b207-134">The following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="6b207-135">Create records of other types</span><span class="sxs-lookup"><span data-stu-id="6b207-135">Create records of other types</span></span>

<span data-ttu-id="6b207-136">Having seen in detail how to create 'A' records, the following examples show how to create records of other record types supported by Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6b207-136">Having seen in detail how to create 'A' records, the following examples show how to create records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="6b207-137">In each case, we show how to create a record set containing a single record.</span><span class="sxs-lookup"><span data-stu-id="6b207-137">In each case, we show how to create a record set containing a single record.</span></span> <span data-ttu-id="6b207-138">The earlier examples for 'A' records can be adapted to create record sets of other types containing multiple records, with metadata, or to create empty record sets.</span><span class="sxs-lookup"><span data-stu-id="6b207-138">The earlier examples for 'A' records can be adapted to create record sets of other types containing multiple records, with metadata, or to create empty record sets.</span></span>

<span data-ttu-id="6b207-139">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span><span class="sxs-lookup"><span data-stu-id="6b207-139">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="6b207-140">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="6b207-140">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="6b207-141">Create an AAAA record set with a single record</span><span class="sxs-lookup"><span data-stu-id="6b207-141">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="6b207-142">Create a CNAME record set with a single record</span><span class="sxs-lookup"><span data-stu-id="6b207-142">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> The DNS standards do not permit CNAME records at the apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.
> 
> For more information, see [CNAME records](dns-zones-records.md#cname-records).


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="6b207-145">Create an MX record set with a single record</span><span class="sxs-lookup"><span data-stu-id="6b207-145">Create an MX record set with a single record</span></span>

<span data-ttu-id="6b207-146">In this example, we use the record set name '@' to create an MX record at the zone apex (in this case, 'contoso.com').</span><span class="sxs-lookup"><span data-stu-id="6b207-146">In this example, we use the record set name '@' to create an MX record at the zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="6b207-147">Create an NS record set with a single record</span><span class="sxs-lookup"><span data-stu-id="6b207-147">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="6b207-148">Create a PTR record set with a single record</span><span class="sxs-lookup"><span data-stu-id="6b207-148">Create a PTR record set with a single record</span></span>

<span data-ttu-id="6b207-149">In this case, 'my-arpa-zone.com' represents the ARPA reverse lookup zone representing your IP range.</span><span class="sxs-lookup"><span data-stu-id="6b207-149">In this case, 'my-arpa-zone.com' represents the ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="6b207-150">Each PTR record set in this zone corresponds to an IP address within this IP range.</span><span class="sxs-lookup"><span data-stu-id="6b207-150">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span> <span data-ttu-id="6b207-151">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span><span class="sxs-lookup"><span data-stu-id="6b207-151">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="6b207-152">Create an SRV record set with a single record</span><span class="sxs-lookup"><span data-stu-id="6b207-152">Create an SRV record set with a single record</span></span>

<span data-ttu-id="6b207-153">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span><span class="sxs-lookup"><span data-stu-id="6b207-153">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="6b207-154">There is no need to include '@' in the record set name when creating an SRV record set at the zone apex.</span><span class="sxs-lookup"><span data-stu-id="6b207-154">There is no need to include '@' in the record set name when creating an SRV record set at the zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="6b207-155">Create a TXT record set with a single record</span><span class="sxs-lookup"><span data-stu-id="6b207-155">Create a TXT record set with a single record</span></span>

<span data-ttu-id="6b207-156">The following example shows how to create a TXT record.</span><span class="sxs-lookup"><span data-stu-id="6b207-156">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="6b207-157">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="6b207-157">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="6b207-158">Get a record set</span><span class="sxs-lookup"><span data-stu-id="6b207-158">Get a record set</span></span>

<span data-ttu-id="6b207-159">To retrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="6b207-159">To retrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="6b207-160">This cmdlet returns a local object that represents the record set in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6b207-160">This cmdlet returns a local object that represents the record set in Azure DNS.</span></span>

<span data-ttu-id="6b207-161">As with `New-AzureRmDnsRecordSet`, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span><span class="sxs-lookup"><span data-stu-id="6b207-161">As with `New-AzureRmDnsRecordSet`, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="6b207-162">You also need to specify the record type, and the zone containing the record set.</span><span class="sxs-lookup"><span data-stu-id="6b207-162">You also need to specify the record type, and the zone containing the record set.</span></span>

<span data-ttu-id="6b207-163">The following example shows how to retrieve a record set.</span><span class="sxs-lookup"><span data-stu-id="6b207-163">The following example shows how to retrieve a record set.</span></span> <span data-ttu-id="6b207-164">In this example, the zone is specified using the `-ZoneName` and `-ResourceGroupName` parameters.</span><span class="sxs-lookup"><span data-stu-id="6b207-164">In this example, the zone is specified using the `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="6b207-165">Alternatively, you can also specify the zone using a zone object, passed using the \`-Zone' parameter.</span><span class="sxs-lookup"><span data-stu-id="6b207-165">Alternatively, you can also specify the zone using a zone object, passed using the \`-Zone' parameter.</span></span> 

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="6b207-166">List record sets</span><span class="sxs-lookup"><span data-stu-id="6b207-166">List record sets</span></span>

<span data-ttu-id="6b207-167">You can also use `Get-AzureRmDnsZone` to list record sets in a zone, by omitting the `-Name` and/or `-RecordType` parameters.</span><span class="sxs-lookup"><span data-stu-id="6b207-167">You can also use `Get-AzureRmDnsZone` to list record sets in a zone, by omitting the `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="6b207-168">The following example returns all record sets in the zone:</span><span class="sxs-lookup"><span data-stu-id="6b207-168">The following example returns all record sets in the zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="6b207-169">The following example shows how all record sets of a given type can be retrieved by specifying the record type while omitting the record set name:</span><span class="sxs-lookup"><span data-stu-id="6b207-169">The following example shows how all record sets of a given type can be retrieved by specifying the record type while omitting the record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="6b207-170">To retrieve all record sets with a given name, across record types, you need to retrieve all record sets and then filter the results:</span><span class="sxs-lookup"><span data-stu-id="6b207-170">To retrieve all record sets with a given name, across record types, you need to retrieve all record sets and then filter the results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="6b207-171">In all the above examples, the zone can be specified either by using the `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span><span class="sxs-lookup"><span data-stu-id="6b207-171">In all the above examples, the zone can be specified either by using the `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="6b207-172">Add a record to an existing record set</span><span class="sxs-lookup"><span data-stu-id="6b207-172">Add a record to an existing record set</span></span>

<span data-ttu-id="6b207-173">To add a record to an existing record set, follow the following three steps:</span><span class="sxs-lookup"><span data-stu-id="6b207-173">To add a record to an existing record set, follow the following three steps:</span></span>

1. <span data-ttu-id="6b207-174">Get the existing record set</span><span class="sxs-lookup"><span data-stu-id="6b207-174">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="6b207-175">Add the new record to the local record set.</span><span class="sxs-lookup"><span data-stu-id="6b207-175">Add the new record to the local record set.</span></span> <span data-ttu-id="6b207-176">This is an off-line operation.</span><span class="sxs-lookup"><span data-stu-id="6b207-176">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="6b207-177">Commit the change back to the Azure DNS service.</span><span class="sxs-lookup"><span data-stu-id="6b207-177">Commit the change back to the Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="6b207-178">Using `Set-AzureRmDnsRecordSet` *replaces* the existing record set in Azure DNS (and all records it contains) with the record set specified.</span><span class="sxs-lookup"><span data-stu-id="6b207-178">Using `Set-AzureRmDnsRecordSet` *replaces* the existing record set in Azure DNS (and all records it contains) with the record set specified.</span></span> <span data-ttu-id="6b207-179">[Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span><span class="sxs-lookup"><span data-stu-id="6b207-179">[Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="6b207-180">You can use the optional `-Overwrite` switch to suppress these checks.</span><span class="sxs-lookup"><span data-stu-id="6b207-180">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="6b207-181">This sequence of operations can also be *piped*, meaning you pass the record set object by using the pipe rather than passing it as a parameter:</span><span class="sxs-lookup"><span data-stu-id="6b207-181">This sequence of operations can also be *piped*, meaning you pass the record set object by using the pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="6b207-182">The examples above show how to add an 'A' record to an existing record set of type 'A'.</span><span class="sxs-lookup"><span data-stu-id="6b207-182">The examples above show how to add an 'A' record to an existing record set of type 'A'.</span></span> <span data-ttu-id="6b207-183">A similar sequence of operations is used to add records to record sets of other types, substituting the `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific to each record type.</span><span class="sxs-lookup"><span data-stu-id="6b207-183">A similar sequence of operations is used to add records to record sets of other types, substituting the `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific to each record type.</span></span> <span data-ttu-id="6b207-184">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span><span class="sxs-lookup"><span data-stu-id="6b207-184">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="6b207-185">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span><span class="sxs-lookup"><span data-stu-id="6b207-185">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="6b207-186">This constraint arises from the DNS standards.</span><span class="sxs-lookup"><span data-stu-id="6b207-186">This constraint arises from the DNS standards.</span></span> <span data-ttu-id="6b207-187">It is not a limitation of Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6b207-187">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="6b207-188">Remove a record from an existing record set</span><span class="sxs-lookup"><span data-stu-id="6b207-188">Remove a record from an existing record set</span></span>

<span data-ttu-id="6b207-189">The process to remove a record from a record set is similar to the process to add a record to an existing record set:</span><span class="sxs-lookup"><span data-stu-id="6b207-189">The process to remove a record from a record set is similar to the process to add a record to an existing record set:</span></span>

1. <span data-ttu-id="6b207-190">Get the existing record set</span><span class="sxs-lookup"><span data-stu-id="6b207-190">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="6b207-191">Remove the record from the local record set object.</span><span class="sxs-lookup"><span data-stu-id="6b207-191">Remove the record from the local record set object.</span></span> <span data-ttu-id="6b207-192">This is an off-line operation.</span><span class="sxs-lookup"><span data-stu-id="6b207-192">This is an off-line operation.</span></span> <span data-ttu-id="6b207-193">The record that's being removed must be an exact match with an existing record across all parameters.</span><span class="sxs-lookup"><span data-stu-id="6b207-193">The record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="6b207-194">Commit the change back to the Azure DNS service.</span><span class="sxs-lookup"><span data-stu-id="6b207-194">Commit the change back to the Azure DNS service.</span></span> <span data-ttu-id="6b207-195">Use the optional `-Overwrite` switch to suppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span><span class="sxs-lookup"><span data-stu-id="6b207-195">Use the optional `-Overwrite` switch to suppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="6b207-196">Using the above sequence to remove the last record from a record set does not delete the record set, rather it leaves an empty record set.</span><span class="sxs-lookup"><span data-stu-id="6b207-196">Using the above sequence to remove the last record from a record set does not delete the record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="6b207-197">To remove a record set entirely, see [Delete a record set](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="6b207-197">To remove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="6b207-198">Similarly to adding records to a record set, the sequence of operations to remove a record set can also be piped:</span><span class="sxs-lookup"><span data-stu-id="6b207-198">Similarly to adding records to a record set, the sequence of operations to remove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="6b207-199">Different record types are supported by passing the appropriate type-specific parameters to `Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="6b207-199">Different record types are supported by passing the appropriate type-specific parameters to `Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="6b207-200">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span><span class="sxs-lookup"><span data-stu-id="6b207-200">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="6b207-201">Modify an existing record set</span><span class="sxs-lookup"><span data-stu-id="6b207-201">Modify an existing record set</span></span>

<span data-ttu-id="6b207-202">The steps for modifying an existing record set are similar to the steps you take when adding or removing records from a record set:</span><span class="sxs-lookup"><span data-stu-id="6b207-202">The steps for modifying an existing record set are similar to the steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="6b207-203">Retrieve the existing record set by using `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="6b207-203">Retrieve the existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="6b207-204">Modify the local record set object by:</span><span class="sxs-lookup"><span data-stu-id="6b207-204">Modify the local record set object by:</span></span>
    * <span data-ttu-id="6b207-205">Adding or removing records</span><span class="sxs-lookup"><span data-stu-id="6b207-205">Adding or removing records</span></span>
    * <span data-ttu-id="6b207-206">Changing the parameters of existing records</span><span class="sxs-lookup"><span data-stu-id="6b207-206">Changing the parameters of existing records</span></span>
    * <span data-ttu-id="6b207-207">Changing the record set metadata and time to live (TTL)</span><span class="sxs-lookup"><span data-stu-id="6b207-207">Changing the record set metadata and time to live (TTL)</span></span>
3. <span data-ttu-id="6b207-208">Commit your changes by using the `Set-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6b207-208">Commit your changes by using the `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="6b207-209">This *replaces* the existing record set in Azure DNS with the record set specified.</span><span class="sxs-lookup"><span data-stu-id="6b207-209">This *replaces* the existing record set in Azure DNS with the record set specified.</span></span>

<span data-ttu-id="6b207-210">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span><span class="sxs-lookup"><span data-stu-id="6b207-210">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="6b207-211">You can use the optional `-Overwrite` switch to suppress these checks.</span><span class="sxs-lookup"><span data-stu-id="6b207-211">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

### <a name="to-update-a-record-in-an-existing-record-set"></a><span data-ttu-id="6b207-212">To update a record in an existing record set</span><span class="sxs-lookup"><span data-stu-id="6b207-212">To update a record in an existing record set</span></span>

<span data-ttu-id="6b207-213">In this example, we change the IP address of an existing 'A' record:</span><span class="sxs-lookup"><span data-stu-id="6b207-213">In this example, we change the IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="6b207-214">To modify an SOA record</span><span class="sxs-lookup"><span data-stu-id="6b207-214">To modify an SOA record</span></span>

<span data-ttu-id="6b207-215">You cannot add or remove records from the automatically created SOA record set at the zone apex (`-Name "@"`, including quote marks).</span><span class="sxs-lookup"><span data-stu-id="6b207-215">You cannot add or remove records from the automatically created SOA record set at the zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="6b207-216">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span><span class="sxs-lookup"><span data-stu-id="6b207-216">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

<span data-ttu-id="6b207-217">The following example shows how to change the *Email* property of the SOA record:</span><span class="sxs-lookup"><span data-stu-id="6b207-217">The following example shows how to change the *Email* property of the SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="6b207-218">To modify NS records at the zone apex</span><span class="sxs-lookup"><span data-stu-id="6b207-218">To modify NS records at the zone apex</span></span>

<span data-ttu-id="6b207-219">You cannot add to, remove, or modify the records in the automatically-created NS record set at the zone apex (`-Name "@"`, including quote marks).</span><span class="sxs-lookup"><span data-stu-id="6b207-219">You cannot add to, remove, or modify the records in the automatically-created NS record set at the zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="6b207-220">The only changes permitted are to modify the record set TTL and metadata.</span><span class="sxs-lookup"><span data-stu-id="6b207-220">The only changes permitted are to modify the record set TTL and metadata.</span></span>

<span data-ttu-id="6b207-221">The following example shows how to change the TTL property of the NS record set:</span><span class="sxs-lookup"><span data-stu-id="6b207-221">The following example shows how to change the TTL property of the NS record set:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Ttl = 300
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-record-set-metadata"></a><span data-ttu-id="6b207-222">To modify record set metadata</span><span class="sxs-lookup"><span data-stu-id="6b207-222">To modify record set metadata</span></span>

<span data-ttu-id="6b207-223">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="6b207-223">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="6b207-224">The following example shows how to modify the metadata of an existing record set:</span><span class="sxs-lookup"><span data-stu-id="6b207-224">The following example shows how to modify the metadata of an existing record set:</span></span>

```powershell
# Get the record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="6b207-225">Delete a record set</span><span class="sxs-lookup"><span data-stu-id="6b207-225">Delete a record set</span></span>

<span data-ttu-id="6b207-226">Record sets can be deleted by using the `Remove-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6b207-226">Record sets can be deleted by using the `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="6b207-227">Deleting a record set also deletes all records within the record set.</span><span class="sxs-lookup"><span data-stu-id="6b207-227">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> You cannot delete the SOA and NS record sets at the zone apex (`-Name '@'`).  Azure DNS created these automatically when the zone was created, and deletes them automatically when the zone is deleted.

<span data-ttu-id="6b207-230">The following example shows how to delete a record set.</span><span class="sxs-lookup"><span data-stu-id="6b207-230">The following example shows how to delete a record set.</span></span> <span data-ttu-id="6b207-231">In this example, the record set name, record set type, zone name, and resource group are each specified explicitly.</span><span class="sxs-lookup"><span data-stu-id="6b207-231">In this example, the record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="6b207-232">Alternatively, the record set can be specified by name and type, and the zone specified using an object:</span><span class="sxs-lookup"><span data-stu-id="6b207-232">Alternatively, the record set can be specified by name and type, and the zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="6b207-233">As a third option, the record set itself can be specified using a record set object:</span><span class="sxs-lookup"><span data-stu-id="6b207-233">As a third option, the record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="6b207-234">When you specify the record set to be deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not deleted.</span><span class="sxs-lookup"><span data-stu-id="6b207-234">When you specify the record set to be deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="6b207-235">You can use the optional `-Overwrite` switch to suppress these checks.</span><span class="sxs-lookup"><span data-stu-id="6b207-235">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="6b207-236">The record set object can also be piped instead of being passed as a parameter:</span><span class="sxs-lookup"><span data-stu-id="6b207-236">The record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="6b207-237">Confirmation prompts</span><span class="sxs-lookup"><span data-stu-id="6b207-237">Confirmation prompts</span></span>

<span data-ttu-id="6b207-238">The `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span><span class="sxs-lookup"><span data-stu-id="6b207-238">The `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="6b207-239">Each cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span><span class="sxs-lookup"><span data-stu-id="6b207-239">Each cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="6b207-240">Since the default value for `$ConfirmPreference` is `High`, these prompts are not given when using the default PowerShell settings.</span><span class="sxs-lookup"><span data-stu-id="6b207-240">Since the default value for `$ConfirmPreference` is `High`, these prompts are not given when using the default PowerShell settings.</span></span>

<span data-ttu-id="6b207-241">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span><span class="sxs-lookup"><span data-stu-id="6b207-241">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="6b207-242">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span><span class="sxs-lookup"><span data-stu-id="6b207-242">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="6b207-243">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span><span class="sxs-lookup"><span data-stu-id="6b207-243">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="6b207-244">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="6b207-244">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b207-245">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b207-245">Next steps</span></span>

<span data-ttu-id="6b207-246">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="6b207-246">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="6b207-247">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6b207-247">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="6b207-248">Review the [Azure DNS PowerShell reference documentation](/powershell/resourcemanager/azurerm.dns/v2.3.0/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="6b207-248">Review the [Azure DNS PowerShell reference documentation](/powershell/resourcemanager/azurerm.dns/v2.3.0/azurerm.dns).</span></span>
