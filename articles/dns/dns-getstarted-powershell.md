---
title: Get started with Azure DNS using PowerShell | Microsoft Docs
description: Learn how to create a DNS zone and record in Azure DNS. This is a step-by-step guide to create and manage your first DNS zone and record using PowerShell.
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 9f9c2ad56483919bf676fc84af49a7c90ba042f9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550079"
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="c4f1a-104">Get Started with Azure DNS using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4f1a-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

<span data-ttu-id="c4f1a-109">This article walks you through the steps to create your first DNS zone and record using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-109">This article walks you through the steps to create your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="c4f1a-110">You can also perform these steps using the Azure portal or the cross-platform Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-110">You can also perform these steps using the Azure portal or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="c4f1a-111">A DNS zone is used to host the DNS records for a particular domain.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="c4f1a-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="c4f1a-113">Each DNS record for your domain is then created inside this DNS zone.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="c4f1a-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="c4f1a-115">Each of these steps is described below.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-115">Each of these steps is described below.</span></span>

<span data-ttu-id="c4f1a-116">These instructions assume you have already installed and signed in to Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-116">These instructions assume you have already installed and signed in to Azure PowerShell.</span></span> <span data-ttu-id="c4f1a-117">For help, see [How to manage DNS zones using PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="c4f1a-117">For help, see [How to manage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="c4f1a-118">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="c4f1a-118">Create a DNS zone</span></span>

<span data-ttu-id="c4f1a-119">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-119">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="c4f1a-120">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-120">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="c4f1a-121">Use the example to create a DNS zone, substituting the values for your own.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-121">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="c4f1a-122">Create a DNS record</span><span class="sxs-lookup"><span data-stu-id="c4f1a-122">Create a DNS record</span></span>

<span data-ttu-id="c4f1a-123">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-123">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="c4f1a-124">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="c4f1a-124">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="c4f1a-125">The fully-qualified name of the record set is "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="c4f1a-125">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="c4f1a-126">The record type is "A", with IP address "1.2.3.4", and the TTL is 3600 seconds.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-126">The record type is "A", with IP address "1.2.3.4", and the TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="c4f1a-127">For other record types, for record sets with more than one record, and to modify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="c4f1a-127">For other record types, for record sets with more than one record, and to modify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="c4f1a-128">View records</span><span class="sxs-lookup"><span data-stu-id="c4f1a-128">View records</span></span>

<span data-ttu-id="c4f1a-129">To list the DNS records in your zone, use:</span><span class="sxs-lookup"><span data-stu-id="c4f1a-129">To list the DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="c4f1a-130">Update name servers</span><span class="sxs-lookup"><span data-stu-id="c4f1a-130">Update name servers</span></span>

<span data-ttu-id="c4f1a-131">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-131">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="c4f1a-132">This enables other users on the Internet to find your DNS records.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-132">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="c4f1a-133">The name servers for your zone are given by the `Get-AzureRmDnsZone` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c4f1a-133">The name servers for your zone are given by the `Get-AzureRmDnsZone` cmdlet:</span></span>

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

<span data-ttu-id="c4f1a-134">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span><span class="sxs-lookup"><span data-stu-id="c4f1a-134">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="c4f1a-135">Your registrar will offer the option to set up the name servers for the domain.</span><span class="sxs-lookup"><span data-stu-id="c4f1a-135">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="c4f1a-136">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="c4f1a-136">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="c4f1a-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4f1a-137">Next steps</span></span>

<span data-ttu-id="c4f1a-138">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4f1a-138">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="c4f1a-139">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="c4f1a-139">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="c4f1a-140">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="c4f1a-140">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

