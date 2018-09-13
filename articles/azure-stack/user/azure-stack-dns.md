---
title: DNS in Azure Stack | Microsoft Docs
description: Using DNS in Azure Stack
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.openlocfilehash: acb8b262256031ae8615180e0f55c98cb56b538d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969034"
---
# <a name="using-dns-in-azure-stack"></a><span data-ttu-id="89c7d-103">Using DNS in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="89c7d-103">Using DNS in Azure Stack</span></span>

<span data-ttu-id="89c7d-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="89c7d-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="89c7d-105">Azure Stack supports the following Domain Name System (DNS) features:</span><span class="sxs-lookup"><span data-stu-id="89c7d-105">Azure Stack supports the following Domain Name System (DNS) features:</span></span>

* <span data-ttu-id="89c7d-106">DNS hostname resolution</span><span class="sxs-lookup"><span data-stu-id="89c7d-106">DNS hostname resolution</span></span>
* <span data-ttu-id="89c7d-107">Creating and managing DNS zones and records using the API</span><span class="sxs-lookup"><span data-stu-id="89c7d-107">Creating and managing DNS zones and records using the API</span></span>

## <a name="support-for-dns-hostname-resolution"></a><span data-ttu-id="89c7d-108">Support for DNS hostname resolution</span><span class="sxs-lookup"><span data-stu-id="89c7d-108">Support for DNS hostname resolution</span></span>

<span data-ttu-id="89c7d-109">You can specify a DNS domain name label for public IP resources.</span><span class="sxs-lookup"><span data-stu-id="89c7d-109">You can specify a DNS domain name label for public IP resources.</span></span> <span data-ttu-id="89c7d-110">Azure Stack uses *domainnamelabel.location*.cloudapp.azurestack.external for the label name and maps it to the public IP address in Azure Stack managed DNS servers.</span><span class="sxs-lookup"><span data-stu-id="89c7d-110">Azure Stack uses *domainnamelabel.location*.cloudapp.azurestack.external for the label name and maps it to the public IP address in Azure Stack managed DNS servers.</span></span>

<span data-ttu-id="89c7d-111">For example, if you create a public IP resource with **contoso** as a domain name label in the Local Azure Stack location, the [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) (FQDN) **contoso.local.cloudapp.azurestack.external** resolves to the public IP address of the resource.</span><span class="sxs-lookup"><span data-stu-id="89c7d-111">For example, if you create a public IP resource with **contoso** as a domain name label in the Local Azure Stack location, the [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) (FQDN) **contoso.local.cloudapp.azurestack.external** resolves to the public IP address of the resource.</span></span> <span data-ttu-id="89c7d-112">You can use this FQDN to create a custom domain CNAME record that points to the public IP address in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="89c7d-112">You can use this FQDN to create a custom domain CNAME record that points to the public IP address in Azure Stack.</span></span>

<span data-ttu-id="89c7d-113">To learn more about name resolution, refer to the [DNS resolution](https://docs.microsoft.com/azure/dns/dns-for-azure-services?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) article.</span><span class="sxs-lookup"><span data-stu-id="89c7d-113">To learn more about name resolution, refer to the [DNS resolution](https://docs.microsoft.com/azure/dns/dns-for-azure-services?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) article.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89c7d-114">Each domain name label you create must be unique within its Azure Stack location.</span><span class="sxs-lookup"><span data-stu-id="89c7d-114">Each domain name label you create must be unique within its Azure Stack location.</span></span>

<span data-ttu-id="89c7d-115">The next screen capture shows the **Create public IP address** dialog for creating a public IP address using the portal.</span><span class="sxs-lookup"><span data-stu-id="89c7d-115">The next screen capture shows the **Create public IP address** dialog for creating a public IP address using the portal.</span></span>

![Create public IP address](media/azure-stack-whats-new-dns/image01.png)

<span data-ttu-id="89c7d-117">**Example scenario**</span><span class="sxs-lookup"><span data-stu-id="89c7d-117">**Example scenario**</span></span>

<span data-ttu-id="89c7d-118">You have a load balancer processing requests from a web application.</span><span class="sxs-lookup"><span data-stu-id="89c7d-118">You have a load balancer processing requests from a web application.</span></span> <span data-ttu-id="89c7d-119">Behind the load balancer is a web site running on one or more virtual machines.</span><span class="sxs-lookup"><span data-stu-id="89c7d-119">Behind the load balancer is a web site running on one or more virtual machines.</span></span> <span data-ttu-id="89c7d-120">You can access the load-balanced web site using a DNS name, instead of an IP address.</span><span class="sxs-lookup"><span data-stu-id="89c7d-120">You can access the load-balanced web site using a DNS name, instead of an IP address.</span></span>

## <a name="create-and-manage-dns-zones-and-records-using-the-api"></a><span data-ttu-id="89c7d-121">Create and manage DNS zones and records using the API</span><span class="sxs-lookup"><span data-stu-id="89c7d-121">Create and manage DNS zones and records using the API</span></span>

<span data-ttu-id="89c7d-122">You can create and manage DNS zones and records in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="89c7d-122">You can create and manage DNS zones and records in Azure Stack.</span></span>

<span data-ttu-id="89c7d-123">Azure Stack provides a DNS service like Azure’s, using APIs that are consistent with Azure’s DNS APIs.</span><span class="sxs-lookup"><span data-stu-id="89c7d-123">Azure Stack provides a DNS service like Azure’s, using APIs that are consistent with Azure’s DNS APIs.</span></span>  <span data-ttu-id="89c7d-124">By hosting your domains in Azure Stack DNS, you can manage your DNS records using the same credentials, APIs, and tools.</span><span class="sxs-lookup"><span data-stu-id="89c7d-124">By hosting your domains in Azure Stack DNS, you can manage your DNS records using the same credentials, APIs, and tools.</span></span> <span data-ttu-id="89c7d-125">You can also use the same billing and support as your other Azure services.</span><span class="sxs-lookup"><span data-stu-id="89c7d-125">You can also use the same billing and support as your other Azure services.</span></span>

<span data-ttu-id="89c7d-126">The Azure Stack DNS infrastructure is more compact than Azure's.</span><span class="sxs-lookup"><span data-stu-id="89c7d-126">The Azure Stack DNS infrastructure is more compact than Azure's.</span></span> <span data-ttu-id="89c7d-127">The size and location of an Azure Stack deployment will affect DNS scope, scale, and performance.</span><span class="sxs-lookup"><span data-stu-id="89c7d-127">The size and location of an Azure Stack deployment will affect DNS scope, scale, and performance.</span></span> <span data-ttu-id="89c7d-128">This also means that performance, availability, global distribution, and high-availability can vary from deployment to deployment.</span><span class="sxs-lookup"><span data-stu-id="89c7d-128">This also means that performance, availability, global distribution, and high-availability can vary from deployment to deployment.</span></span>

## <a name="comparison-with-azure-dns"></a><span data-ttu-id="89c7d-129">Comparison with Azure DNS</span><span class="sxs-lookup"><span data-stu-id="89c7d-129">Comparison with Azure DNS</span></span>

<span data-ttu-id="89c7d-130">DNS in Azure Stack is similar to DNS in Azure, but there are major exceptions you need to understand.</span><span class="sxs-lookup"><span data-stu-id="89c7d-130">DNS in Azure Stack is similar to DNS in Azure, but there are major exceptions you need to understand.</span></span>

* <span data-ttu-id="89c7d-131">**It does not support AAAA records**</span><span class="sxs-lookup"><span data-stu-id="89c7d-131">**It does not support AAAA records**</span></span>

    <span data-ttu-id="89c7d-132">Azure Stack does NOT support AAAA records because Azure Stack does not support IPv6 addresses.</span><span class="sxs-lookup"><span data-stu-id="89c7d-132">Azure Stack does NOT support AAAA records because Azure Stack does not support IPv6 addresses.</span></span>  <span data-ttu-id="89c7d-133">This is a key difference between DNS in Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="89c7d-133">This is a key difference between DNS in Azure and Azure Stack.</span></span>
* <span data-ttu-id="89c7d-134">**It is not multi-tenant**</span><span class="sxs-lookup"><span data-stu-id="89c7d-134">**It is not multi-tenant**</span></span>

    <span data-ttu-id="89c7d-135">The DNS Service in Azure Stack is not multi-tenant.</span><span class="sxs-lookup"><span data-stu-id="89c7d-135">The DNS Service in Azure Stack is not multi-tenant.</span></span> <span data-ttu-id="89c7d-136">Each tenant cannot create the same DNS zone.</span><span class="sxs-lookup"><span data-stu-id="89c7d-136">Each tenant cannot create the same DNS zone.</span></span> <span data-ttu-id="89c7d-137">Only the first subscription that attempts to create the zone succeeds, and subsequent requests fail.</span><span class="sxs-lookup"><span data-stu-id="89c7d-137">Only the first subscription that attempts to create the zone succeeds, and subsequent requests fail.</span></span>  <span data-ttu-id="89c7d-138">It is a known issue, and a key difference between Azure and Azure Stack DNS.</span><span class="sxs-lookup"><span data-stu-id="89c7d-138">It is a known issue, and a key difference between Azure and Azure Stack DNS.</span></span> <span data-ttu-id="89c7d-139">This issue will be resolved in a future release.</span><span class="sxs-lookup"><span data-stu-id="89c7d-139">This issue will be resolved in a future release.</span></span>
* <span data-ttu-id="89c7d-140">**Tags, metadata, and Etags**</span><span class="sxs-lookup"><span data-stu-id="89c7d-140">**Tags, metadata, and Etags**</span></span>

    <span data-ttu-id="89c7d-141">There are minor differences in how Azure Stack handles tags, metadata, Etags, and limits.</span><span class="sxs-lookup"><span data-stu-id="89c7d-141">There are minor differences in how Azure Stack handles tags, metadata, Etags, and limits.</span></span>

<span data-ttu-id="89c7d-142">To learn more about Azure DNS, see [DNS zones and records](../../dns/dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="89c7d-142">To learn more about Azure DNS, see [DNS zones and records](../../dns/dns-zones-records.md).</span></span>

### <a name="tags-metadata-and-etags"></a><span data-ttu-id="89c7d-143">Tags, metadata, and Etags</span><span class="sxs-lookup"><span data-stu-id="89c7d-143">Tags, metadata, and Etags</span></span>

<span data-ttu-id="89c7d-144">**Tags**</span><span class="sxs-lookup"><span data-stu-id="89c7d-144">**Tags**</span></span>

<span data-ttu-id="89c7d-145">Azure Stack DNS supports using Azure Resource Manager tags on DNS zone resources.</span><span class="sxs-lookup"><span data-stu-id="89c7d-145">Azure Stack DNS supports using Azure Resource Manager tags on DNS zone resources.</span></span> <span data-ttu-id="89c7d-146">It does not support tags on DNS record sets, although as an alternative 'metadata' is supported on DNS record sets as explained next.</span><span class="sxs-lookup"><span data-stu-id="89c7d-146">It does not support tags on DNS record sets, although as an alternative 'metadata' is supported on DNS record sets as explained next.</span></span>

<span data-ttu-id="89c7d-147">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="89c7d-147">**Metadata**</span></span>

<span data-ttu-id="89c7d-148">As an alternative to record set tags, Azure Stack DNS supports annotating record sets using 'metadata'.</span><span class="sxs-lookup"><span data-stu-id="89c7d-148">As an alternative to record set tags, Azure Stack DNS supports annotating record sets using 'metadata'.</span></span> <span data-ttu-id="89c7d-149">Similar to tags, metadata enables you to associate name-value pairs with each record set.</span><span class="sxs-lookup"><span data-stu-id="89c7d-149">Similar to tags, metadata enables you to associate name-value pairs with each record set.</span></span> <span data-ttu-id="89c7d-150">For example, this can be useful to record the purpose of each record set.</span><span class="sxs-lookup"><span data-stu-id="89c7d-150">For example, this can be useful to record the purpose of each record set.</span></span> <span data-ttu-id="89c7d-151">Unlike tags, metadata cannot be used to provide a filtered view of your Azure bill and cannot be specified in an Azure Resource Manager policy.</span><span class="sxs-lookup"><span data-stu-id="89c7d-151">Unlike tags, metadata cannot be used to provide a filtered view of your Azure bill and cannot be specified in an Azure Resource Manager policy.</span></span>

<span data-ttu-id="89c7d-152">**Etags**</span><span class="sxs-lookup"><span data-stu-id="89c7d-152">**Etags**</span></span>

<span data-ttu-id="89c7d-153">Suppose two people or two processes try to modify a DNS record at the same time.</span><span class="sxs-lookup"><span data-stu-id="89c7d-153">Suppose two people or two processes try to modify a DNS record at the same time.</span></span> <span data-ttu-id="89c7d-154">Which one wins?</span><span class="sxs-lookup"><span data-stu-id="89c7d-154">Which one wins?</span></span> <span data-ttu-id="89c7d-155">And does the winner know that they've overwritten changes created by someone else?</span><span class="sxs-lookup"><span data-stu-id="89c7d-155">And does the winner know that they've overwritten changes created by someone else?</span></span>

<span data-ttu-id="89c7d-156">Azure Stack DNS uses Etags to handle concurrent changes to the same resource safely.</span><span class="sxs-lookup"><span data-stu-id="89c7d-156">Azure Stack DNS uses Etags to handle concurrent changes to the same resource safely.</span></span> <span data-ttu-id="89c7d-157">Etags are separate from Azure Resource Manager 'Tags'.</span><span class="sxs-lookup"><span data-stu-id="89c7d-157">Etags are separate from Azure Resource Manager 'Tags'.</span></span> <span data-ttu-id="89c7d-158">Each DNS resource (zone or record set) has an Etag associated with it.</span><span class="sxs-lookup"><span data-stu-id="89c7d-158">Each DNS resource (zone or record set) has an Etag associated with it.</span></span> <span data-ttu-id="89c7d-159">Whenever a resource is retrieved, its Etag is also retrieved.</span><span class="sxs-lookup"><span data-stu-id="89c7d-159">Whenever a resource is retrieved, its Etag is also retrieved.</span></span> <span data-ttu-id="89c7d-160">When updating a resource, you can choose to pass back the Etag so Azure Stack DNS can verify that the Etag on the server matches.</span><span class="sxs-lookup"><span data-stu-id="89c7d-160">When updating a resource, you can choose to pass back the Etag so Azure Stack DNS can verify that the Etag on the server matches.</span></span> <span data-ttu-id="89c7d-161">Since each update to a resource results in the Etag being regenerated, an Etag mismatch indicates a concurrent change has occurred.</span><span class="sxs-lookup"><span data-stu-id="89c7d-161">Since each update to a resource results in the Etag being regenerated, an Etag mismatch indicates a concurrent change has occurred.</span></span> <span data-ttu-id="89c7d-162">Etags can also be used when creating a new resource to ensure that the resource does not already exist.</span><span class="sxs-lookup"><span data-stu-id="89c7d-162">Etags can also be used when creating a new resource to ensure that the resource does not already exist.</span></span>

<span data-ttu-id="89c7d-163">By default, Azure Stack DNS PowerShell uses Etags to block concurrent changes to zones and record sets.</span><span class="sxs-lookup"><span data-stu-id="89c7d-163">By default, Azure Stack DNS PowerShell uses Etags to block concurrent changes to zones and record sets.</span></span> <span data-ttu-id="89c7d-164">The optional *-Overwrite* switch can be used to suppress Etag checks, in which case any concurrent changes that have occurred are overwritten.</span><span class="sxs-lookup"><span data-stu-id="89c7d-164">The optional *-Overwrite* switch can be used to suppress Etag checks, in which case any concurrent changes that have occurred are overwritten.</span></span>

<span data-ttu-id="89c7d-165">At the level of the Azure Stack DNS REST API, Etags are specified using HTTP headers.</span><span class="sxs-lookup"><span data-stu-id="89c7d-165">At the level of the Azure Stack DNS REST API, Etags are specified using HTTP headers.</span></span> <span data-ttu-id="89c7d-166">Their behavior is given in the following table:</span><span class="sxs-lookup"><span data-stu-id="89c7d-166">Their behavior is given in the following table:</span></span>

| <span data-ttu-id="89c7d-167">Header</span><span class="sxs-lookup"><span data-stu-id="89c7d-167">Header</span></span> | <span data-ttu-id="89c7d-168">Behavior</span><span class="sxs-lookup"><span data-stu-id="89c7d-168">Behavior</span></span>|
|--------|---------|
| <span data-ttu-id="89c7d-169">None</span><span class="sxs-lookup"><span data-stu-id="89c7d-169">None</span></span>   | <span data-ttu-id="89c7d-170">PUT always succeeds (no Etag checks)</span><span class="sxs-lookup"><span data-stu-id="89c7d-170">PUT always succeeds (no Etag checks)</span></span>|
| <span data-ttu-id="89c7d-171">If-match</span><span class="sxs-lookup"><span data-stu-id="89c7d-171">If-match</span></span>| <span data-ttu-id="89c7d-172">PUT only succeeds if resource exists and Etag matches</span><span class="sxs-lookup"><span data-stu-id="89c7d-172">PUT only succeeds if resource exists and Etag matches</span></span>|
| <span data-ttu-id="89c7d-173">If-match \*</span><span class="sxs-lookup"><span data-stu-id="89c7d-173">If-match \*</span></span>| <span data-ttu-id="89c7d-174">PUT only succeeds if resource exists</span><span class="sxs-lookup"><span data-stu-id="89c7d-174">PUT only succeeds if resource exists</span></span>|
| <span data-ttu-id="89c7d-175">If-none-match \*</span><span class="sxs-lookup"><span data-stu-id="89c7d-175">If-none-match \*</span></span>| <span data-ttu-id="89c7d-176">PUT only succeeds if resource does not exist</span><span class="sxs-lookup"><span data-stu-id="89c7d-176">PUT only succeeds if resource does not exist</span></span>|

### <a name="limits"></a><span data-ttu-id="89c7d-177">Limits</span><span class="sxs-lookup"><span data-stu-id="89c7d-177">Limits</span></span>

<span data-ttu-id="89c7d-178">The following default limits apply when using Azure Stack DNS:</span><span class="sxs-lookup"><span data-stu-id="89c7d-178">The following default limits apply when using Azure Stack DNS:</span></span>

| <span data-ttu-id="89c7d-179">Resource</span><span class="sxs-lookup"><span data-stu-id="89c7d-179">Resource</span></span>| <span data-ttu-id="89c7d-180">Default limit</span><span class="sxs-lookup"><span data-stu-id="89c7d-180">Default limit</span></span>|
|---------|--------------|
| <span data-ttu-id="89c7d-181">Zones per subscription</span><span class="sxs-lookup"><span data-stu-id="89c7d-181">Zones per subscription</span></span>| <span data-ttu-id="89c7d-182">100</span><span class="sxs-lookup"><span data-stu-id="89c7d-182">100</span></span>|
| <span data-ttu-id="89c7d-183">Record sets per zone</span><span class="sxs-lookup"><span data-stu-id="89c7d-183">Record sets per zone</span></span>| <span data-ttu-id="89c7d-184">5000</span><span class="sxs-lookup"><span data-stu-id="89c7d-184">5000</span></span>|
| <span data-ttu-id="89c7d-185">Records per record set</span><span class="sxs-lookup"><span data-stu-id="89c7d-185">Records per record set</span></span>| <span data-ttu-id="89c7d-186">20</span><span class="sxs-lookup"><span data-stu-id="89c7d-186">20</span></span>|

## <a name="next-steps"></a><span data-ttu-id="89c7d-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="89c7d-187">Next steps</span></span>

[<span data-ttu-id="89c7d-188">Introducing iDNS for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="89c7d-188">Introducing iDNS for Azure Stack</span></span>](azure-stack-understanding-dns.md)
