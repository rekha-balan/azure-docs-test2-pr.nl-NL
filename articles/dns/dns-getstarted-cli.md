---
title: Get started with Azure DNS using Azure CLI 2.0 | Microsoft Docs
description: Learn how to create a DNS zone and record in Azure DNS. This is a step-by-step guide to create and manage your first DNS zone and record using the Azure CLI 2.0.
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 64e722d005ff76aa9d1b82c46a0d6eb079d18403
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555069"
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="bc733-104">Get started with Azure DNS using Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bc733-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

<span data-ttu-id="bc733-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="bc733-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="bc733-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc733-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="bc733-111">A DNS zone is used to host the DNS records for a particular domain.</span><span class="sxs-lookup"><span data-stu-id="bc733-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="bc733-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span><span class="sxs-lookup"><span data-stu-id="bc733-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="bc733-113">Each DNS record for your domain is then created inside this DNS zone.</span><span class="sxs-lookup"><span data-stu-id="bc733-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="bc733-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span><span class="sxs-lookup"><span data-stu-id="bc733-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="bc733-115">Each of these steps is described below.</span><span class="sxs-lookup"><span data-stu-id="bc733-115">Each of these steps is described below.</span></span>

<span data-ttu-id="bc733-116">These instructions assume you have already installed and signed in to Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="bc733-116">These instructions assume you have already installed and signed in to Azure CLI 1.0.</span></span> <span data-ttu-id="bc733-117">For help, see [How to manage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bc733-117">For help, see [How to manage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>


## <a name="create-a-dns-zone"></a><span data-ttu-id="bc733-118">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="bc733-118">Create a DNS zone</span></span>

<span data-ttu-id="bc733-119">A DNS zone is created using the `az network dns zone create` command.</span><span class="sxs-lookup"><span data-stu-id="bc733-119">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="bc733-120">To see help for this command, type `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="bc733-120">To see help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="bc733-121">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="bc733-121">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="bc733-122">Use the example to create a DNS zone, substituting the values for your own.</span><span class="sxs-lookup"><span data-stu-id="bc733-122">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="bc733-123">Create a DNS record</span><span class="sxs-lookup"><span data-stu-id="bc733-123">Create a DNS record</span></span>

<span data-ttu-id="bc733-124">To create a DNS record, use the `az network dns record-set [record type] add-record` command.</span><span class="sxs-lookup"><span data-stu-id="bc733-124">To create a DNS record, use the `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="bc733-125">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="bc733-125">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="bc733-126">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="bc733-126">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="bc733-127">The fully-qualified name of the record set is "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="bc733-127">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="bc733-128">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span><span class="sxs-lookup"><span data-stu-id="bc733-128">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set A add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="bc733-129">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bc733-129">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="bc733-130">View records</span><span class="sxs-lookup"><span data-stu-id="bc733-130">View records</span></span>

<span data-ttu-id="bc733-131">To list the DNS records in your zone, use:</span><span class="sxs-lookup"><span data-stu-id="bc733-131">To list the DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="bc733-132">Update name servers</span><span class="sxs-lookup"><span data-stu-id="bc733-132">Update name servers</span></span>

<span data-ttu-id="bc733-133">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="bc733-133">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="bc733-134">This enables other users on the Internet to find your DNS records.</span><span class="sxs-lookup"><span data-stu-id="bc733-134">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="bc733-135">The name servers for your zone are given by the `az network dns zone show` command.</span><span class="sxs-lookup"><span data-stu-id="bc733-135">The name servers for your zone are given by the `az network dns zone show` command.</span></span> <span data-ttu-id="bc733-136">To see the name server names, use JSON output, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="bc733-136">To see the name server names, use JSON output, as shown in the following example.</span></span>

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="bc733-137">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span><span class="sxs-lookup"><span data-stu-id="bc733-137">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="bc733-138">Your registrar will offer the option to set up the name servers for the domain.</span><span class="sxs-lookup"><span data-stu-id="bc733-138">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="bc733-139">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="bc733-139">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="bc733-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc733-140">Next steps</span></span>

<span data-ttu-id="bc733-141">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc733-141">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="bc733-142">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bc733-142">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="bc733-143">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bc733-143">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
