---
title: Host reverse DNS lookup zones in Azure DNS | Microsoft Docs
description: Learn how to use Azure DNS to host the reverse DNS lookup zones for your IP ranges
services: dns
documentationcenter: na
author: vhorne
manager: jeconnoc
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: victorh
ms.openlocfilehash: b1c55e054d1113871e4f3753a11cd2bf62e42e67
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867381"
---
# <a name="host-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="8ddc6-103">Host reverse DNS lookup zones in Azure DNS</span><span class="sxs-lookup"><span data-stu-id="8ddc6-103">Host reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="8ddc6-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="8ddc6-105">The IP ranges represented by the reverse lookup zones must be assigned to your organization, typically by your ISP.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-105">The IP ranges represented by the reverse lookup zones must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="8ddc6-106">To configure reverse DNS for an Azure-owned IP address that's assigned to your Azure service, see [Configure reverse DNS for services hosted in Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-106">To configure reverse DNS for an Azure-owned IP address that's assigned to your Azure service, see [Configure reverse DNS for services hosted in Azure](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="8ddc6-107">Before you read this article, you should be familiar with the [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-107">Before you read this article, you should be familiar with the [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="8ddc6-108">This article walks you through the steps to create your first reverse lookup DNS zone and record by using the Azure portal, Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-108">This article walks you through the steps to create your first reverse lookup DNS zone and record by using the Azure portal, Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="8ddc6-109">Create a reverse lookup DNS zone</span><span class="sxs-lookup"><span data-stu-id="8ddc6-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="8ddc6-110">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-110">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="8ddc6-111">On the **Hub** menu, select **New** > **Networking**, and then select **DNS zone**.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-111">On the **Hub** menu, select **New** > **Networking**, and then select **DNS zone**.</span></span>

   !["DNS zone" selection](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="8ddc6-113">In the **Create DNS zone** pane, name your DNS zone.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-113">In the **Create DNS zone** pane, name your DNS zone.</span></span> <span data-ttu-id="8ddc6-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="8ddc6-115">Use the instructions for [IPv4](#ipv4) or [IPv6](#ipv6) to name your zone.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-115">Use the instructions for [IPv4](#ipv4) or [IPv6](#ipv6) to name your zone.</span></span> <span data-ttu-id="8ddc6-116">When you're finished, select **Create** to create the zone.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-116">When you're finished, select **Create** to create the zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="8ddc6-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="8ddc6-117">IPv4</span></span>

<span data-ttu-id="8ddc6-118">The name of an IPv4 reverse lookup zone is based on the IP range that it represents.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-118">The name of an IPv4 reverse lookup zone is based on the IP range that it represents.</span></span> <span data-ttu-id="8ddc6-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="8ddc6-120">For examples, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-120">For examples, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="8ddc6-121">When you're creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash (`/`) in the zone name.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-121">When you're creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash (`/`) in the zone name.</span></span>
>
> <span data-ttu-id="8ddc6-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="8ddc6-123">Although the DNS standards support both methods, Azure DNS doesn't support DNS zone names that contain for forward slash (`/`) character.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-123">Although the DNS standards support both methods, Azure DNS doesn't support DNS zone names that contain for forward slash (`/`) character.</span></span>

<span data-ttu-id="8ddc6-124">The following example shows how to create a Class C reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="8ddc6-124">The following example shows how to create a Class C reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span></span>

 !["Create DNS zone" pane, with boxes filled in](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="8ddc6-126">**Resource group location** defines the location for the resource group.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-126">**Resource group location** defines the location for the resource group.</span></span> <span data-ttu-id="8ddc6-127">It has no impact on the DNS zone.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-127">It has no impact on the DNS zone.</span></span> <span data-ttu-id="8ddc6-128">The DNS zone location is always "global," and is not shown.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-128">The DNS zone location is always "global," and is not shown.</span></span>

<span data-ttu-id="8ddc6-129">The following examples show how to complete this task by using Azure PowerShell and Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-129">The following examples show how to complete this task by using Azure PowerShell and Azure CLI.</span></span>

#### <a name="powershell"></a><span data-ttu-id="8ddc6-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ddc6-130">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="8ddc6-131">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-131">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="8ddc6-132">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-132">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="8ddc6-133">IPv6</span><span class="sxs-lookup"><span data-stu-id="8ddc6-133">IPv6</span></span>

<span data-ttu-id="8ddc6-134">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-134">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="8ddc6-135">For examples, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-135">For examples, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="8ddc6-136">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="8ddc6-136">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span></span>

 !["Create DNS zone" pane, with boxes filled in](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="8ddc6-138">**Resource group location** defines the location for the resource group.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-138">**Resource group location** defines the location for the resource group.</span></span> <span data-ttu-id="8ddc6-139">It has no impact on the DNS zone.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-139">It has no impact on the DNS zone.</span></span> <span data-ttu-id="8ddc6-140">The DNS zone location is always "global," and is not shown.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-140">The DNS zone location is always "global," and is not shown.</span></span>

<span data-ttu-id="8ddc6-141">The following examples show how to complete this task by using Azure PowerShell and Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-141">The following examples show how to complete this task by using Azure PowerShell and Azure CLI.</span></span>

#### <a name="powershell"></a><span data-ttu-id="8ddc6-142">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ddc6-142">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="8ddc6-143">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-143">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="8ddc6-144">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-144">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="8ddc6-145">Delegate a reverse DNS lookup zone</span><span class="sxs-lookup"><span data-stu-id="8ddc6-145">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="8ddc6-146">Now that you've created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-146">Now that you've created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span></span> <span data-ttu-id="8ddc6-147">DNS delegation enables the DNS name resolution process to find the name servers that host your reverse DNS lookup zone.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-147">DNS delegation enables the DNS name resolution process to find the name servers that host your reverse DNS lookup zone.</span></span> <span data-ttu-id="8ddc6-148">Those name servers can then answer DNS reverse queries for the IP addresses in your address range.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-148">Those name servers can then answer DNS reverse queries for the IP addresses in your address range.</span></span>

<span data-ttu-id="8ddc6-149">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-149">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="8ddc6-150">Delegation for reverse lookup zones works the same way.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-150">Delegation for reverse lookup zones works the same way.</span></span> <span data-ttu-id="8ddc6-151">The only difference is that you need to configure the name servers with the ISP that provided your IP range, rather than your domain name registrar.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-151">The only difference is that you need to configure the name servers with the ISP that provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="8ddc6-152">Create a DNS PTR record</span><span class="sxs-lookup"><span data-stu-id="8ddc6-152">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="8ddc6-153">IPv4</span><span class="sxs-lookup"><span data-stu-id="8ddc6-153">IPv4</span></span>

<span data-ttu-id="8ddc6-154">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-154">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="8ddc6-155">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-155">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="8ddc6-156">At the top of the **DNS zone** pane, select **+ Record set** to open the **Add record set** pane.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-156">At the top of the **DNS zone** pane, select **+ Record set** to open the **Add record set** pane.</span></span>

   ![Button for creating a record set](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="8ddc6-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span></span> 

   <span data-ttu-id="8ddc6-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span></span> <span data-ttu-id="8ddc6-160">Therefore, only the last octet is supplied in the **Name** box.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-160">Therefore, only the last octet is supplied in the **Name** box.</span></span> <span data-ttu-id="8ddc6-161">For example, you might name your record set **15** for a resource whose IP address is 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-161">For example, you might name your record set **15** for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="8ddc6-162">For **Type**, select **PTR**.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-162">For **Type**, select **PTR**.</span></span>  
1. <span data-ttu-id="8ddc6-163">For **DOMAIN NAME**, enter the fully qualified domain name (FQDN) of the resource that uses the IP.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-163">For **DOMAIN NAME**, enter the fully qualified domain name (FQDN) of the resource that uses the IP.</span></span>
1. <span data-ttu-id="8ddc6-164">Select **OK** at the bottom of the pane to create the DNS record.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-164">Select **OK** at the bottom of the pane to create the DNS record.</span></span>

 !["Add record set" pane, with boxes filled in](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="8ddc6-166">The following examples show how to complete this task by using PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-166">The following examples show how to complete this task by using PowerShell or Azure CLI.</span></span>

#### <a name="powershell"></a><span data-ttu-id="8ddc6-167">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ddc6-167">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azure-cli-10"></a><span data-ttu-id="8ddc6-168">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-168">Azure CLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azure-cli-20"></a><span data-ttu-id="8ddc6-169">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-169">Azure CLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="8ddc6-170">IPv6</span><span class="sxs-lookup"><span data-stu-id="8ddc6-170">IPv6</span></span>

<span data-ttu-id="8ddc6-171">The following example walks you through the process of creating new PTR record.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-171">The following example walks you through the process of creating new PTR record.</span></span> <span data-ttu-id="8ddc6-172">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-172">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="8ddc6-173">At the top of the **DNS zone** pane, select **+ Record set** to open the **Add record set** pane.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-173">At the top of the **DNS zone** pane, select **+ Record set** to open the **Add record set** pane.</span></span>

   ![Button for creating a record set](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="8ddc6-175">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-175">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span></span> <span data-ttu-id="8ddc6-176">It must not include any zero compression.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-176">It must not include any zero compression.</span></span> 

   <span data-ttu-id="8ddc6-177">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-177">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="8ddc6-178">Therefore, only the last 64 bits are supplied in the **Name** box.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-178">Therefore, only the last 64 bits are supplied in the **Name** box.</span></span> <span data-ttu-id="8ddc6-179">The last 64 bits of the IP address are entered in reverse order, with a period as the delimiter between each hexadecimal number.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-179">The last 64 bits of the IP address are entered in reverse order, with a period as the delimiter between each hexadecimal number.</span></span> <span data-ttu-id="8ddc6-180">For example, you might name your record set **e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f** for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-180">For example, you might name your record set **e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f** for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
3. <span data-ttu-id="8ddc6-181">For **Type**, select **PTR**.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-181">For **Type**, select **PTR**.</span></span>  
4. <span data-ttu-id="8ddc6-182">For **DOMAIN NAME**, enter the FQDN of the resource that uses the IP.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-182">For **DOMAIN NAME**, enter the FQDN of the resource that uses the IP.</span></span>
5. <span data-ttu-id="8ddc6-183">Select **OK** at the bottom of the pane to create the DNS record.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-183">Select **OK** at the bottom of the pane to create the DNS record.</span></span>

!["Add record set" pane, with boxes filled in](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="8ddc6-185">The following examples show how to complete this task by using PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-185">The following examples show how to complete this task by using PowerShell or Azure CLI.</span></span>

#### <a name="powershell"></a><span data-ttu-id="8ddc6-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ddc6-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azure-cli-10"></a><span data-ttu-id="8ddc6-187">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-187">Azure CLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azure-cli-20"></a><span data-ttu-id="8ddc6-188">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-188">Azure CLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="8ddc6-189">View records</span><span class="sxs-lookup"><span data-stu-id="8ddc6-189">View records</span></span>

<span data-ttu-id="8ddc6-190">To view the records that you created, browse to your DNS zone in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-190">To view the records that you created, browse to your DNS zone in the Azure portal.</span></span> <span data-ttu-id="8ddc6-191">In the lower part of the **DNS zone** pane, you can see the records for the DNS zone.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-191">In the lower part of the **DNS zone** pane, you can see the records for the DNS zone.</span></span> <span data-ttu-id="8ddc6-192">You should see the default NS and SOA records, plus any new records that you've created.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-192">You should see the default NS and SOA records, plus any new records that you've created.</span></span> <span data-ttu-id="8ddc6-193">The NS and SOA records are created in every zone.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-193">The NS and SOA records are created in every zone.</span></span> 

### <a name="ipv4"></a><span data-ttu-id="8ddc6-194">IPv4</span><span class="sxs-lookup"><span data-stu-id="8ddc6-194">IPv4</span></span>

<span data-ttu-id="8ddc6-195">The **DNS zone** pane shows the IPv4 PTR records:</span><span class="sxs-lookup"><span data-stu-id="8ddc6-195">The **DNS zone** pane shows the IPv4 PTR records:</span></span>

!["DNS zone" pane with IPv4 records](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="8ddc6-197">The following examples show how to view the PTR records by using PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-197">The following examples show how to view the PTR records by using PowerShell or Azure CLI.</span></span>

#### <a name="powershell"></a><span data-ttu-id="8ddc6-198">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ddc6-198">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="8ddc6-199">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-199">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="8ddc6-200">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-200">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="8ddc6-201">IPv6</span><span class="sxs-lookup"><span data-stu-id="8ddc6-201">IPv6</span></span>

<span data-ttu-id="8ddc6-202">The **DNS zone** pane shows the IPv6 PTR records:</span><span class="sxs-lookup"><span data-stu-id="8ddc6-202">The **DNS zone** pane shows the IPv6 PTR records:</span></span>

!["DNS zone" pane with IPv6 records](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="8ddc6-204">The following examples show how to view the records by using PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-204">The following examples show how to view the records by using PowerShell or Azure CLI.</span></span>

#### <a name="powershell"></a><span data-ttu-id="8ddc6-205">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ddc6-205">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="8ddc6-206">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-206">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="8ddc6-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ddc6-207">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="8ddc6-208">FAQ</span><span class="sxs-lookup"><span data-stu-id="8ddc6-208">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="8ddc6-209">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span><span class="sxs-lookup"><span data-stu-id="8ddc6-209">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="8ddc6-210">Yes.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-210">Yes.</span></span> <span data-ttu-id="8ddc6-211">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-211">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="8ddc6-212">Create the reverse lookup zone in Azure DNS as explained in this article, and then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-212">Create the reverse lookup zone in Azure DNS as explained in this article, and then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span></span> <span data-ttu-id="8ddc6-213">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-213">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="8ddc6-214">How much does hosting my reverse DNS lookup zone cost?</span><span class="sxs-lookup"><span data-stu-id="8ddc6-214">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="8ddc6-215">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-215">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="8ddc6-216">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span><span class="sxs-lookup"><span data-stu-id="8ddc6-216">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="8ddc6-217">Yes.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-217">Yes.</span></span> <span data-ttu-id="8ddc6-218">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-218">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="8ddc6-219">Can I import an existing reverse DNS lookup zone?</span><span class="sxs-lookup"><span data-stu-id="8ddc6-219">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="8ddc6-220">Yes.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-220">Yes.</span></span> <span data-ttu-id="8ddc6-221">You can use Azure CLI to import existing DNS zones into Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-221">You can use Azure CLI to import existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="8ddc6-222">This method works for both forward lookup zones and reverse lookup zones.</span><span class="sxs-lookup"><span data-stu-id="8ddc6-222">This method works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="8ddc6-223">For more information, see [Import and export a DNS zone file using Azure CLI](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-223">For more information, see [Import and export a DNS zone file using Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ddc6-224">Next steps</span><span class="sxs-lookup"><span data-stu-id="8ddc6-224">Next steps</span></span>

<span data-ttu-id="8ddc6-225">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-225">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="8ddc6-226">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="8ddc6-226">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
