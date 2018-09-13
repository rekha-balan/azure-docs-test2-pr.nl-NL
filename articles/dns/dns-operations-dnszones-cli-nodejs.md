---
title: Manage DNS zones in Azure DNS - Azure CLI 1.0 | Microsoft Docs
description: You can manage DNS zones using Azure CLI 1.0. This article shows how to update, delete and create DNS zones on Azure DNS.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 9b545937f3e375dfcef815a66263a57bd5042f69
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662110"
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="8f302-104">How to manage DNS Zones in Azure DNS using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8f302-104">How to manage DNS Zones in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [Azure CLI](dns-operations-dnszones-cli.md)
> * [PowerShell](dns-operations-dnszones.md)

<span data-ttu-id="8f302-107">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="8f302-107">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="8f302-108">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8f302-108">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="8f302-109">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="8f302-109">CLI versions to complete the task</span></span>

<span data-ttu-id="8f302-110">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="8f302-110">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="8f302-111">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span><span class="sxs-lookup"><span data-stu-id="8f302-111">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="8f302-112">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span><span class="sxs-lookup"><span data-stu-id="8f302-112">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="8f302-113">Introduction</span><span class="sxs-lookup"><span data-stu-id="8f302-113">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="8f302-114">Getting help</span><span class="sxs-lookup"><span data-stu-id="8f302-114">Getting help</span></span>

<span data-ttu-id="8f302-115">All CLI 1.0 commands relating to Azure DNS start with `azure network dns`.</span><span class="sxs-lookup"><span data-stu-id="8f302-115">All CLI 1.0 commands relating to Azure DNS start with `azure network dns`.</span></span> <span data-ttu-id="8f302-116">Help is available for each command using the `--help` option (short form `-h`).</span><span class="sxs-lookup"><span data-stu-id="8f302-116">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="8f302-117">For example:</span><span class="sxs-lookup"><span data-stu-id="8f302-117">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="8f302-118">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="8f302-118">Create a DNS zone</span></span>

<span data-ttu-id="8f302-119">A DNS zone is created using the `azure network dns zone create` command.</span><span class="sxs-lookup"><span data-stu-id="8f302-119">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="8f302-120">For help, see `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="8f302-120">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="8f302-121">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="8f302-121">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="8f302-122">To create a DNS zone with tags.</span><span class="sxs-lookup"><span data-stu-id="8f302-122">To create a DNS zone with tags.</span></span>

<span data-ttu-id="8f302-123">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span><span class="sxs-lookup"><span data-stu-id="8f302-123">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="8f302-124">Get a DNS zone</span><span class="sxs-lookup"><span data-stu-id="8f302-124">Get a DNS zone</span></span>

<span data-ttu-id="8f302-125">To retrieve a DNS zone, use `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="8f302-125">To retrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="8f302-126">For help, see `azure network dns zone show -h`.</span><span class="sxs-lookup"><span data-stu-id="8f302-126">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="8f302-127">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="8f302-127">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="8f302-128">The following example is the response.</span><span class="sxs-lookup"><span data-stu-id="8f302-128">The following example is the response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

<span data-ttu-id="8f302-129">Note that DNS records are not returned by `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="8f302-129">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="8f302-130">To list DNS records, use `azure network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="8f302-130">To list DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="8f302-131">List DNS zones</span><span class="sxs-lookup"><span data-stu-id="8f302-131">List DNS zones</span></span>

<span data-ttu-id="8f302-132">To enumerate DNS zones, use `azure network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="8f302-132">To enumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="8f302-133">For help, see `azure network dns zone list -h`.</span><span class="sxs-lookup"><span data-stu-id="8f302-133">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="8f302-134">Specifying the resource group lists only those zones within the resource group:</span><span class="sxs-lookup"><span data-stu-id="8f302-134">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="8f302-135">Omitting the resource group lists all zones in the subscription:</span><span class="sxs-lookup"><span data-stu-id="8f302-135">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="8f302-136">Update a DNS zone</span><span class="sxs-lookup"><span data-stu-id="8f302-136">Update a DNS zone</span></span>

<span data-ttu-id="8f302-137">Changes to a DNS zone resource can be made using `azure network dns zone set`.</span><span class="sxs-lookup"><span data-stu-id="8f302-137">Changes to a DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="8f302-138">For help, see `azure network dns zone set -h`.</span><span class="sxs-lookup"><span data-stu-id="8f302-138">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="8f302-139">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="8f302-139">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="8f302-140">It is only used to update properties of the zone resource itself.</span><span class="sxs-lookup"><span data-stu-id="8f302-140">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="8f302-141">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span><span class="sxs-lookup"><span data-stu-id="8f302-141">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="8f302-142">The following example shows how to update the tags on a DNS zone.</span><span class="sxs-lookup"><span data-stu-id="8f302-142">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="8f302-143">The existing tags are replaced by the value specified.</span><span class="sxs-lookup"><span data-stu-id="8f302-143">The existing tags are replaced by the value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="8f302-144">Delete a DNS Zone</span><span class="sxs-lookup"><span data-stu-id="8f302-144">Delete a DNS Zone</span></span>

<span data-ttu-id="8f302-145">DNS zones can be deleted using `azure network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="8f302-145">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="8f302-146">For help, see `azure network dns zone delete -h`.</span><span class="sxs-lookup"><span data-stu-id="8f302-146">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> Deleting a DNS zone also deletes all DNS records within the zone. This operation cannot be undone. If the DNS zone is in use, services using the zone will fail when the zone is deleted.
>
>To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).

<span data-ttu-id="8f302-151">This command prompts for confirmation.</span><span class="sxs-lookup"><span data-stu-id="8f302-151">This command prompts for confirmation.</span></span> <span data-ttu-id="8f302-152">The optional `--quiet` switch (short form `-q`) suppresses this prompt.</span><span class="sxs-lookup"><span data-stu-id="8f302-152">The optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="8f302-153">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="8f302-153">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="8f302-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f302-154">Next steps</span></span>

<span data-ttu-id="8f302-155">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span><span class="sxs-lookup"><span data-stu-id="8f302-155">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="8f302-156">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="8f302-156">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

