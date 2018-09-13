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
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-the-azure-cli-20"></a>Manage DNS records and recordsets in Azure DNS using the Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux. You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).

## <a name="cli-versions-to-complete-the-task"></a>CLI versions to complete the task

You can complete the task using one of the following CLI versions:

* [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.
* [Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.

The examples in this article assume you have already [installed the Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).

## <a name="introduction"></a>Introduction

Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).

## <a name="create-a-dns-record"></a>Create a DNS record

To create a DNS record, use the `az network dns record-set <recordtype> add-record` command. (Where recordtype is the type of record, i.e A, SRV, TXT, etc) For help, see `az network dns record-set --help`.

When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created. The record set name given must be a *relative* name, meaning it must exclude the zone name.

If the record set does not already exist, this command creates it for you. If the record set already exists, this command adda the record you specify to the existing record set.

If a new record set is created, a default time-to-live (TTL) of 3600 is used. For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).

The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*. The IP address of the A record is *1.2.3.4*.

```azurecli
az network dns record-set a add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

To create a record set in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:

```azurecli
az network dns record-set a add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a>Create a DNS record set

In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*. You can also create the record set *explicitly* before adding records to it. Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records. Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.

Record sets are created using the `az network dns record-set create` command. For help, see `az network dns record-set create --help`.

Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata. [Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.

The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):

```azurecli
az network dns record-set create --resource-group myresourcegroup --zone-name contoso.com --name www --type A --ttl 60
```

The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter :

```azurecli
az network dns record-set create --resource-group myresourcegroup --zone-name contoso.com --name www --type A --metadata "dept=finance" "environment=production"
```

Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).

## <a name="create-records-of-other-types"></a>Create records of other types

Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.

The parameters used to specify the record data vary depending on the type of the record. For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`. The parameters for each record type can be listed using `az network dns record-set <type> add-record --help`.

In each case, we show how to create a single record. The record is added to the existing record set, or a record set created implicitly. For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).

We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately. However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record"></a>Create an AAAA record

```azurecli
az network dns record-set aaaa add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a>Create a CNAME record

> [!NOTE]
> The DNS standards do not permit CNAME records at the apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.
> 
> For more information, see [CNAME records](dns-zones-records.md#cname-records).

```azurecli
az network dns record-set cname add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a>Create an MX record

In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").

```azurecli
az network dns record-set mx add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a>Create an NS record

```azurecli
az network dns record-set ns add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "test-ns" --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a>Create a PTR record

In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range. Each PTR record set in this zone corresponds to an IP address within this IP range.  The record name '10' is the last octet of the IP address within this IP range represented by this record.

```azurecli
az network dns record-set ptr add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "my-arpa.zone.com" --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a>Create an SRV record

When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name. There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.

```azurecli
az network dns record srv add --resource-group myresourcegroup --zone-name contoso.com --record-set-name "_sip.tls" --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a>Create a TXT record

The following example shows how to create a TXT record. For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).

```azurecli
az network dns record-set txt add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "test-txt" --value "This is a TXT record"
```

## <a name="get-a-record-set"></a>Get a record set

To retrieve an existing record set, use `az network dns record-set show`. For help, see `az network dns record-set show --help`.

As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name. You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.

The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:

```azurecli
az network dns record-set show --resource-group myresourcegroup --zone-name contoso.com --name www --type A
```

## <a name="list-record-sets"></a>List record sets

You can list all records in a DNS zone by using the `az network dns record-set list` command. For help, see `az network dns record-set list --help`.

This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

This example returns all record sets that match the given record type (in this case, 'A' records):

```azurecli
az network dns record-setA a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-to-an-existing-record-set"></a>Add a record to an existing record set

You can use `az network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.

For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.

## <a name="remove-a-record-from-an-existing-record-set"></a>Remove a record from an existing record set.

To remove a DNS record from an existing record set, use `az network dns record-set ? remove-record` (where ? is the record type). For help, see `az network dns record-set -h`.

This command deletes a DNS record from a record set. If the last record in a record set is deleted, the record set itself is **not** deleted. Instead, an empty record set is left. To delete the record set instead, see [Delete a record set](#delete-a-record-set).

You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`. These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.

This command prompts for confirmation. This prompt can be suppressed using the `--yes` switch.

The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*. The confirmation prompt is suppressed.

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4 --yes
```

## <a name="modify-an-existing-record-set"></a>Modify an existing record set

Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records. The following sections explain how to modify each of these properties.

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a>To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record

To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record. For detailed instructions on how to delete and add records, see the earlier sections of this article.

The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:

```azurecli
az network dns record-set a add-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

You cannot add, remove, or modify the records in the automatically created NS record set at the zone apex (`--Name "@"`, including quote marks). For this record set, the only changes permitted are to modify the record set TTL and metadata.

### <a name="to-modify-a-cname-record"></a>To modify a CNAME record

To modify a CNAME record, use `az network dns record-set update` with the --set switch to add the new record value. Unlike other record types, a CNAME record set can only contain a single record.

The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:

```azurecli
az network dns record-set update --resource-group myresourcegroup --zone-name contoso.com --name test-cname --type cname --set cnameRecord.cname=www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a>To modify an SOA record

Use `az network dns record-set soa update` to modify the SOA for a given DNS zone. For help, see `az network dns record soa update --help`.

The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a>To modify the TTL of an existing record set

To modify the TTL of an existing record set, use `azure network dns record-set set`. For help, see `azure network dns record-set set -h`.

The following example shows how to modify a record set TTL, in this case to 60 seconds:

```azurecli
az network dns record-set update --resource-group myresourcegroup --zone-name contoso.com --name "www" --type A --set ttl=60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a>To modify the metadata of an existing record set

[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs. To modify the metadata of an existing record set, use `az network dns record-set update`. For help, see `az network dns record-set update --help`.

The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`). Note that any existing metadata is *replaced* by the values given.

```azurecli
az network dns record-set update --resource-group myresourcegroup --zone-name contoso.com --name "www" --type A --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a>Delete a record set

Record sets can be deleted by using the `azure network dns record-set delete` command. For help, see `azure network dns record-set delete -h`. Deleting a record set also deletes all records within the record set.

> [!NOTE]
> You cannot delete the SOA and NS record sets at the zone apex (`-Name "@"`).  These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.

The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:

```azurecli
az network dns record-set delete --resource-group myresourcegroup --zone-name contoso.com --name www --type a
```

You are prompted to confirm the delete operation. To suppress this prompt, use the `--yes` switch.

## <a name="next-steps"></a>Next steps

Learn more about [zones and records in Azure DNS](dns-zones-records.md).
<br>
Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.
