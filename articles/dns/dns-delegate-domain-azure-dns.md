---
title: Delegate your domain to Azure DNS | Microsoft Docs
description: Understand how to change domain delegation and use Azure DNS name servers to provide domain hosting.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: d44806ec05248127fdeba094bdd5326a10ee515f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549919"
---
# <a name="delegate-a-domain-to-azure-dns"></a><span data-ttu-id="f7dd6-103">Delegate a domain to Azure DNS</span><span class="sxs-lookup"><span data-stu-id="f7dd6-103">Delegate a domain to Azure DNS</span></span>

<span data-ttu-id="f7dd6-104">Azure DNS allows you to host a DNS zone and manage the DNS records for a domain in Azure.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-104">Azure DNS allows you to host a DNS zone and manage the DNS records for a domain in Azure.</span></span> <span data-ttu-id="f7dd6-105">In order for DNS queries for a domain to reach Azure DNS, the domain has to be delegated to Azure DNS from the parent domain.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-105">In order for DNS queries for a domain to reach Azure DNS, the domain has to be delegated to Azure DNS from the parent domain.</span></span> <span data-ttu-id="f7dd6-106">Keep in mind Azure DNS is not the domain registrar.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-106">Keep in mind Azure DNS is not the domain registrar.</span></span> <span data-ttu-id="f7dd6-107">This article explains how to delegate your domain to Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-107">This article explains how to delegate your domain to Azure DNS.</span></span>

<span data-ttu-id="f7dd6-108">For domains purchased from a registrar, your registrar offers the option to set up these NS records.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-108">For domains purchased from a registrar, your registrar offers the option to set up these NS records.</span></span> <span data-ttu-id="f7dd6-109">You do not have to own a domain to create a DNS zone with that domain name in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-109">You do not have to own a domain to create a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="f7dd6-110">However, you do need to own the domain to set up the delegation to Azure DNS with the registrar.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-110">However, you do need to own the domain to set up the delegation to Azure DNS with the registrar.</span></span>

<span data-ttu-id="f7dd6-111">For example, suppose you purchase the domain 'contoso.net' and create a zone with the name 'contoso.net' in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-111">For example, suppose you purchase the domain 'contoso.net' and create a zone with the name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="f7dd6-112">As the owner of the domain, your registrar offers you the option to configure the name server addresses (that is, the NS records) for your domain.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-112">As the owner of the domain, your registrar offers you the option to configure the name server addresses (that is, the NS records) for your domain.</span></span> <span data-ttu-id="f7dd6-113">The registrar stores these NS records in the parent domain, in this case '.net'.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-113">The registrar stores these NS records in the parent domain, in this case '.net'.</span></span> <span data-ttu-id="f7dd6-114">Clients around the world can then be directed to your domain in Azure DNS zone when trying to resolve DNS records in 'contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-114">Clients around the world can then be directed to your domain in Azure DNS zone when trying to resolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="f7dd6-115">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="f7dd6-115">Create a DNS zone</span></span>

1. <span data-ttu-id="f7dd6-116">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f7dd6-116">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="f7dd6-117">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-117">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS zone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="f7dd6-119">On the **Create DNS zone** blade enter the following values, then click **Create**:</span><span class="sxs-lookup"><span data-stu-id="f7dd6-119">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="f7dd6-120">**Setting**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-120">**Setting**</span></span> | <span data-ttu-id="f7dd6-121">**Value**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-121">**Value**</span></span> | <span data-ttu-id="f7dd6-122">**Details**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="f7dd6-123">**Name**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-123">**Name**</span></span>|<span data-ttu-id="f7dd6-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="f7dd6-124">contoso.net</span></span>|<span data-ttu-id="f7dd6-125">The name of the DNS zone</span><span class="sxs-lookup"><span data-stu-id="f7dd6-125">The name of the DNS zone</span></span>|
   |<span data-ttu-id="f7dd6-126">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-126">**Subscription**</span></span>|<span data-ttu-id="f7dd6-127">[Your subscription]</span><span class="sxs-lookup"><span data-stu-id="f7dd6-127">[Your subscription]</span></span>|<span data-ttu-id="f7dd6-128">Select a subscription to create the application gateway in.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-128">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="f7dd6-129">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-129">**Resource group**</span></span>|<span data-ttu-id="f7dd6-130">**Create new:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="f7dd6-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="f7dd6-131">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-131">Create a resource group.</span></span> <span data-ttu-id="f7dd6-132">The resource group name must be unique within the subscription you selected.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-132">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="f7dd6-133">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-133">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="f7dd6-134">**Location**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-134">**Location**</span></span>|<span data-ttu-id="f7dd6-135">West US</span><span class="sxs-lookup"><span data-stu-id="f7dd6-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="f7dd6-136">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-136">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="f7dd6-137">The DNS zone location is always "global", and is not shown.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-137">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="f7dd6-138">Retrieve name servers</span><span class="sxs-lookup"><span data-stu-id="f7dd6-138">Retrieve name servers</span></span>

<span data-ttu-id="f7dd6-139">Before you can delegate your DNS zone to Azure DNS, you first need to know the name server names for your zone.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-139">Before you can delegate your DNS zone to Azure DNS, you first need to know the name server names for your zone.</span></span> <span data-ttu-id="f7dd6-140">Azure DNS allocates name servers from a pool each time a zone is created.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="f7dd6-141">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-141">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="f7dd6-142">Click the **contoso.net** DNS zone in the **All resources** blade.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-142">Click the **contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="f7dd6-143">If the subscription you selected already has several resources in it, you can enter **contoso.net** in the Filter by name…</span><span class="sxs-lookup"><span data-stu-id="f7dd6-143">If the subscription you selected already has several resources in it, you can enter **contoso.net** in the Filter by name…</span></span> <span data-ttu-id="f7dd6-144">box to easily access the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-144">box to easily access the application gateway.</span></span> 

1. <span data-ttu-id="f7dd6-145">Retrieve the name servers from the DNS zone blade.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-145">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="f7dd6-146">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="f7dd6-146">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="f7dd6-148">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-148">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="f7dd6-149">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-149">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

<span data-ttu-id="f7dd6-150">The following examples also provide the steps to retrieve the name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-150">The following examples also provide the steps to retrieve the name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="f7dd6-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7dd6-151">PowerShell</span></span>

```powershell
# The record name "@" is used to refer to records at the top of the zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="f7dd6-152">The following example is the response.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-152">The following example is the response.</span></span>

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a><span data-ttu-id="f7dd6-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f7dd6-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="f7dd6-154">The following example is the response.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-154">The following example is the response.</span></span>

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-the-domain"></a><span data-ttu-id="f7dd6-155">Delegate the domain</span><span class="sxs-lookup"><span data-stu-id="f7dd6-155">Delegate the domain</span></span>

<span data-ttu-id="f7dd6-156">Now that the DNS zone is created and you have the name servers, the parent domain needs to be updated with the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-156">Now that the DNS zone is created and you have the name servers, the parent domain needs to be updated with the Azure DNS name servers.</span></span> <span data-ttu-id="f7dd6-157">Each registrar has their own DNS management tools to change the name server records for a domain.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-157">Each registrar has their own DNS management tools to change the name server records for a domain.</span></span> <span data-ttu-id="f7dd6-158">In the registrar's DNS management page, edit the NS records and replace the NS records with the ones Azure DNS created.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-158">In the registrar's DNS management page, edit the NS records and replace the NS records with the ones Azure DNS created.</span></span>

<span data-ttu-id="f7dd6-159">When delegating a domain to Azure DNS, you must use the name server names provided by Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-159">When delegating a domain to Azure DNS, you must use the name server names provided by Azure DNS.</span></span> <span data-ttu-id="f7dd6-160">It is recommended to use all four name server names, regardless of the name of your domain.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-160">It is recommended to use all four name server names, regardless of the name of your domain.</span></span> <span data-ttu-id="f7dd6-161">Domain delegation does not require the name server name to use the same top-level domain as your domain.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-161">Domain delegation does not require the name server name to use the same top-level domain as your domain.</span></span>

<span data-ttu-id="f7dd6-162">You should not use 'glue records' to point to the Azure DNS name server IP addresses, since these IP addresses may change in future.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-162">You should not use 'glue records' to point to the Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="f7dd6-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="f7dd6-164">Verify name resolution is working</span><span class="sxs-lookup"><span data-stu-id="f7dd6-164">Verify name resolution is working</span></span>

<span data-ttu-id="f7dd6-165">After completing the delegation, you can verify that name resolution is working by using a tool such as 'nslookup' to query the SOA record for your zone (which is also automatically created when the zone is created).</span><span class="sxs-lookup"><span data-stu-id="f7dd6-165">After completing the delegation, you can verify that name resolution is working by using a tool such as 'nslookup' to query the SOA record for your zone (which is also automatically created when the zone is created).</span></span>

<span data-ttu-id="f7dd6-166">You do not have to specify the Azure DNS name servers, if the delegation has been set up correctly, the normal DNS resolution process finds the name servers automatically.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-166">You do not have to specify the Azure DNS name servers, if the delegation has been set up correctly, the normal DNS resolution process finds the name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="f7dd6-167">The following is an example response from the preceding command:</span><span class="sxs-lookup"><span data-stu-id="f7dd6-167">The following is an example response from the preceding command:</span></span>

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="f7dd6-168">Delegate sub-domains in Azure DNS</span><span class="sxs-lookup"><span data-stu-id="f7dd6-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="f7dd6-169">If you want to set up a separate child zone, you can delegate a sub-domain in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-169">If you want to set up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="f7dd6-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like to set up a separate child zone, 'partners.contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like to set up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="f7dd6-171">Create the child zone 'partners.contoso.net' in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-171">Create the child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="f7dd6-172">Look up the authoritative NS records in the child zone to obtain the name servers hosting the child zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-172">Look up the authoritative NS records in the child zone to obtain the name servers hosting the child zone in Azure DNS.</span></span>
3. <span data-ttu-id="f7dd6-173">Delegate the child zone by configuring NS records in the parent zone pointing to the child zone.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-173">Delegate the child zone by configuring NS records in the parent zone pointing to the child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="f7dd6-174">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="f7dd6-174">Create a DNS zone</span></span>

1. <span data-ttu-id="f7dd6-175">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f7dd6-175">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="f7dd6-176">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-176">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS zone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="f7dd6-178">On the **Create DNS zone** blade enter the following values, then click **Create**:</span><span class="sxs-lookup"><span data-stu-id="f7dd6-178">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="f7dd6-179">**Setting**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-179">**Setting**</span></span> | <span data-ttu-id="f7dd6-180">**Value**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-180">**Value**</span></span> | <span data-ttu-id="f7dd6-181">**Details**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="f7dd6-182">**Name**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-182">**Name**</span></span>|<span data-ttu-id="f7dd6-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="f7dd6-183">partners.contoso.net</span></span>|<span data-ttu-id="f7dd6-184">The name of the DNS zone</span><span class="sxs-lookup"><span data-stu-id="f7dd6-184">The name of the DNS zone</span></span>|
   |<span data-ttu-id="f7dd6-185">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-185">**Subscription**</span></span>|<span data-ttu-id="f7dd6-186">[Your subscription]</span><span class="sxs-lookup"><span data-stu-id="f7dd6-186">[Your subscription]</span></span>|<span data-ttu-id="f7dd6-187">Select a subscription to create the application gateway in.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-187">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="f7dd6-188">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-188">**Resource group**</span></span>|<span data-ttu-id="f7dd6-189">**Use Existing:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="f7dd6-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="f7dd6-190">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-190">Create a resource group.</span></span> <span data-ttu-id="f7dd6-191">The resource group name must be unique within the subscription you selected.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-191">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="f7dd6-192">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-192">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="f7dd6-193">**Location**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-193">**Location**</span></span>|<span data-ttu-id="f7dd6-194">West US</span><span class="sxs-lookup"><span data-stu-id="f7dd6-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="f7dd6-195">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-195">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="f7dd6-196">The DNS zone location is always "global", and is not shown.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-196">The DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="f7dd6-197">Retrieve name servers</span><span class="sxs-lookup"><span data-stu-id="f7dd6-197">Retrieve name servers</span></span>

1. <span data-ttu-id="f7dd6-198">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-198">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="f7dd6-199">Click the **partners.contoso.net** DNS zone in the **All resources** blade.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-199">Click the **partners.contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="f7dd6-200">If the subscription you selected already has several resources in it, you can enter **partners.contoso.net** in the Filter by name…</span><span class="sxs-lookup"><span data-stu-id="f7dd6-200">If the subscription you selected already has several resources in it, you can enter **partners.contoso.net** in the Filter by name…</span></span> <span data-ttu-id="f7dd6-201">box to easily access the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-201">box to easily access the application gateway.</span></span>

1. <span data-ttu-id="f7dd6-202">Retrieve the name servers from the DNS zone blade.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-202">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="f7dd6-203">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="f7dd6-203">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="f7dd6-205">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-205">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="f7dd6-206">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-206">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="f7dd6-207">Create name server record in parent zone</span><span class="sxs-lookup"><span data-stu-id="f7dd6-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="f7dd6-208">Navigate to the **contoso.net** DNS zone in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-208">Navigate to the **contoso.net** DNS zone in the Azure portal.</span></span>
1. <span data-ttu-id="f7dd6-209">Click **+ Record set**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="f7dd6-210">On the **Add record set** blade, enter the following values, then click **OK**:</span><span class="sxs-lookup"><span data-stu-id="f7dd6-210">On the **Add record set** blade, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="f7dd6-211">**Setting**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-211">**Setting**</span></span> | <span data-ttu-id="f7dd6-212">**Value**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-212">**Value**</span></span> | <span data-ttu-id="f7dd6-213">**Details**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="f7dd6-214">**Name**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-214">**Name**</span></span>|<span data-ttu-id="f7dd6-215">partners</span><span class="sxs-lookup"><span data-stu-id="f7dd6-215">partners</span></span>|<span data-ttu-id="f7dd6-216">The name of the child DNS zone</span><span class="sxs-lookup"><span data-stu-id="f7dd6-216">The name of the child DNS zone</span></span>|
   |<span data-ttu-id="f7dd6-217">**Type**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-217">**Type**</span></span>|<span data-ttu-id="f7dd6-218">NS</span><span class="sxs-lookup"><span data-stu-id="f7dd6-218">NS</span></span>|<span data-ttu-id="f7dd6-219">Use NS for name server records.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="f7dd6-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-220">**TTL**</span></span>|<span data-ttu-id="f7dd6-221">1</span><span class="sxs-lookup"><span data-stu-id="f7dd6-221">1</span></span>|<span data-ttu-id="f7dd6-222">Time to live.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-222">Time to live.</span></span>|
   |<span data-ttu-id="f7dd6-223">**TTL unit**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-223">**TTL unit**</span></span>|<span data-ttu-id="f7dd6-224">Hours</span><span class="sxs-lookup"><span data-stu-id="f7dd6-224">Hours</span></span>|<span data-ttu-id="f7dd6-225">sets time to live unit to hours</span><span class="sxs-lookup"><span data-stu-id="f7dd6-225">sets time to live unit to hours</span></span>|
   |<span data-ttu-id="f7dd6-226">**NAME SERVER**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-226">**NAME SERVER**</span></span>|<span data-ttu-id="f7dd6-227">{name servers from partners.contoso.net zone}</span><span class="sxs-lookup"><span data-stu-id="f7dd6-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="f7dd6-228">Enter all 4 of the name servers from partners.contoso.net zone.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-228">Enter all 4 of the name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="f7dd6-230">Delegating sub-domains in Azure DNS with other tools</span><span class="sxs-lookup"><span data-stu-id="f7dd6-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="f7dd6-231">The following examples provide the steps to delegate sub-domains in Azure DNS with PowerShell and CLI:</span><span class="sxs-lookup"><span data-stu-id="f7dd6-231">The following examples provide the steps to delegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="f7dd6-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7dd6-232">PowerShell</span></span>

<span data-ttu-id="f7dd6-233">The following PowerShell example demonstrates how this works.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-233">The following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="f7dd6-234">The same steps can be executed via the Azure portal, or via the cross-platform Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-234">The same steps can be executed via the Azure portal, or via the cross-platform Azure CLI.</span></span>

```powershell
# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve the authoritative NS records from the child zone as shown in the next example. This contains the name servers assigned to the child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create the corresponding NS record set in the parent zone to complete the delegation. The record set name in the parent zone matches the child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="f7dd6-235">Use `nslookup` to verify that everything is set up correctly by looking up the SOA record of the child zone.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-235">Use `nslookup` to verify that everything is set up correctly by looking up the SOA record of the child zone.</span></span>

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a><span data-ttu-id="f7dd6-236">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f7dd6-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="f7dd6-237">Retrieve the name servers for the `partners.contoso.net` zone from the output.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-237">Retrieve the name servers for the `partners.contoso.net` zone from the output.</span></span>

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="f7dd6-238">Create the record set and NS records for each name server.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-238">Create the record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create the record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="f7dd6-239">Delete all resources</span><span class="sxs-lookup"><span data-stu-id="f7dd6-239">Delete all resources</span></span>

<span data-ttu-id="f7dd6-240">To delete all resources created in thsi article, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="f7dd6-240">To delete all resources created in thsi article, complete the following steps:</span></span>

1. <span data-ttu-id="f7dd6-241">In the Azure portal **Favorites** pane, click **All resources**.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-241">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="f7dd6-242">Click the **contosorg** resource group in the All resources blade.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-242">Click the **contosorg** resource group in the All resources blade.</span></span> <span data-ttu-id="f7dd6-243">If the subscription you selected already has several resources in it, you can enter **contosorg** in the **Filter by name…**</span><span class="sxs-lookup"><span data-stu-id="f7dd6-243">If the subscription you selected already has several resources in it, you can enter **contosorg** in the **Filter by name…**</span></span> <span data-ttu-id="f7dd6-244">box to easily access the resource group.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-244">box to easily access the resource group.</span></span>
1. <span data-ttu-id="f7dd6-245">In the **contosorg** blade, click the **Delete** button.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-245">In the **contosorg** blade, click the **Delete** button.</span></span>
1. <span data-ttu-id="f7dd6-246">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-246">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span></span> <span data-ttu-id="f7dd6-247">Click **Delete**, Type *contosorg* for the resource group name, then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-247">Click **Delete**, Type *contosorg* for the resource group name, then click **Delete**.</span></span> <span data-ttu-id="f7dd6-248">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-248">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span></span> <span data-ttu-id="f7dd6-249">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-249">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span></span> <span data-ttu-id="f7dd6-250">This process takes several minutes.</span><span class="sxs-lookup"><span data-stu-id="f7dd6-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7dd6-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7dd6-251">Next steps</span></span>

[<span data-ttu-id="f7dd6-252">Manage DNS zones</span><span class="sxs-lookup"><span data-stu-id="f7dd6-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="f7dd6-253">Manage DNS records</span><span class="sxs-lookup"><span data-stu-id="f7dd6-253">Manage DNS records</span></span>](dns-operations-recordsets.md)




