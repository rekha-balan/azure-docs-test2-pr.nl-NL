---
title: Azure DNS troubleshooting guide | Microsoft Docs
description: How to troubleshoot common issues with Azure DNS
services: dns
documentationcenter: na
author: genlin
manager: cshepard
editor: ''
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: genli
ms.openlocfilehash: 816ad6c0079e9272286cdc072ff71bf15313eb8e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784100"
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="e1082-103">Azure DNS troubleshooting guide</span><span class="sxs-lookup"><span data-stu-id="e1082-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="e1082-104">This page provides troubleshooting information for common Azure DNS questions.</span><span class="sxs-lookup"><span data-stu-id="e1082-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="e1082-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="e1082-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="e1082-106">Alternatively, open an Azure support request.</span><span class="sxs-lookup"><span data-stu-id="e1082-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="e1082-107">I can't create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="e1082-107">I can't create a DNS zone</span></span>

<span data-ttu-id="e1082-108">To resolve common issues, try one or more of the following steps:</span><span class="sxs-lookup"><span data-stu-id="e1082-108">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="e1082-109">Review the Azure DNS audit logs to determine the failure reason.</span><span class="sxs-lookup"><span data-stu-id="e1082-109">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="e1082-110">Each DNS zone name must be unique within its resource group.</span><span class="sxs-lookup"><span data-stu-id="e1082-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="e1082-111">That is, two DNS zones with the same name cannot share a resource group.</span><span class="sxs-lookup"><span data-stu-id="e1082-111">That is, two DNS zones with the same name cannot share a resource group.</span></span> <span data-ttu-id="e1082-112">Try using a different zone name, or a different resource group.</span><span class="sxs-lookup"><span data-stu-id="e1082-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="e1082-113">You may see an error "You have reached or exceeded the maximum number of zones in subscription {subscription id}."</span><span class="sxs-lookup"><span data-stu-id="e1082-113">You may see an error "You have reached or exceeded the maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="e1082-114">Either use a different Azure subscription, delete some zones, or contact Azure Support to raise your subscription limit.</span><span class="sxs-lookup"><span data-stu-id="e1082-114">Either use a different Azure subscription, delete some zones, or contact Azure Support to raise your subscription limit.</span></span>
4.  <span data-ttu-id="e1082-115">You may see an error "The zone '{zone name}' is not available."</span><span class="sxs-lookup"><span data-stu-id="e1082-115">You may see an error "The zone '{zone name}' is not available."</span></span> <span data-ttu-id="e1082-116">This error means that Azure DNS was unable to allocate name servers for this DNS zone.</span><span class="sxs-lookup"><span data-stu-id="e1082-116">This error means that Azure DNS was unable to allocate name servers for this DNS zone.</span></span> <span data-ttu-id="e1082-117">Try using a different zone name.</span><span class="sxs-lookup"><span data-stu-id="e1082-117">Try using a different zone name.</span></span> <span data-ttu-id="e1082-118">Alternatively, if you are the domain name owner, contact Azure support, who can allocate name servers for you.</span><span class="sxs-lookup"><span data-stu-id="e1082-118">Alternatively, if you are the domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="e1082-119">**Recommended documents**</span><span class="sxs-lookup"><span data-stu-id="e1082-119">**Recommended documents**</span></span>

[<span data-ttu-id="e1082-120">DNS zones and records</span><span class="sxs-lookup"><span data-stu-id="e1082-120">DNS zones and records</span></span>](dns-zones-records.md)
<br>
[<span data-ttu-id="e1082-121">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="e1082-121">Create a DNS zone</span></span>](dns-getstarted-create-dnszone-portal.md)

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="e1082-122">I can't create a DNS record</span><span class="sxs-lookup"><span data-stu-id="e1082-122">I can't create a DNS record</span></span>

<span data-ttu-id="e1082-123">To resolve common issues, try one or more of the following steps:</span><span class="sxs-lookup"><span data-stu-id="e1082-123">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="e1082-124">Review the Azure DNS audit logs to determine the failure reason.</span><span class="sxs-lookup"><span data-stu-id="e1082-124">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="e1082-125">Does the record set exist already?</span><span class="sxs-lookup"><span data-stu-id="e1082-125">Does the record set exist already?</span></span>  <span data-ttu-id="e1082-126">Azure DNS manages records using record *sets*, which are the collection of records of the same name and the same type.</span><span class="sxs-lookup"><span data-stu-id="e1082-126">Azure DNS manages records using record *sets*, which are the collection of records of the same name and the same type.</span></span> <span data-ttu-id="e1082-127">If a record with the same name and type already exists, then to add another such record you should edit the existing record set.</span><span class="sxs-lookup"><span data-stu-id="e1082-127">If a record with the same name and type already exists, then to add another such record you should edit the existing record set.</span></span>
3.  <span data-ttu-id="e1082-128">Are you trying to create a record at the DNS zone apex (the ‘root’ of the zone)?</span><span class="sxs-lookup"><span data-stu-id="e1082-128">Are you trying to create a record at the DNS zone apex (the ‘root’ of the zone)?</span></span> <span data-ttu-id="e1082-129">If so, the DNS convention is to use the ‘@’ character as the record name.</span><span class="sxs-lookup"><span data-stu-id="e1082-129">If so, the DNS convention is to use the ‘@’ character as the record name.</span></span> <span data-ttu-id="e1082-130">Also note that the DNS standards do not permit CNAME records at the zone apex.</span><span class="sxs-lookup"><span data-stu-id="e1082-130">Also note that the DNS standards do not permit CNAME records at the zone apex.</span></span>
4.  <span data-ttu-id="e1082-131">Do you have a CNAME conflict?</span><span class="sxs-lookup"><span data-stu-id="e1082-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="e1082-132">The DNS standards do not allow a CNAME record with the same name as a record of any other type.</span><span class="sxs-lookup"><span data-stu-id="e1082-132">The DNS standards do not allow a CNAME record with the same name as a record of any other type.</span></span> <span data-ttu-id="e1082-133">If you have an existing CNAME, creating a record with the same name of a different type fails.</span><span class="sxs-lookup"><span data-stu-id="e1082-133">If you have an existing CNAME, creating a record with the same name of a different type fails.</span></span>  <span data-ttu-id="e1082-134">Likewise, creating a CNAME fails if the name matches an existing record of a different type.</span><span class="sxs-lookup"><span data-stu-id="e1082-134">Likewise, creating a CNAME fails if the name matches an existing record of a different type.</span></span> <span data-ttu-id="e1082-135">Remove the conflict by removing the other record or choosing a different record name.</span><span class="sxs-lookup"><span data-stu-id="e1082-135">Remove the conflict by removing the other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="e1082-136">Have you reached the limit on the number of record sets permitted in a DNS zone?</span><span class="sxs-lookup"><span data-stu-id="e1082-136">Have you reached the limit on the number of record sets permitted in a DNS zone?</span></span> <span data-ttu-id="e1082-137">The current number of record sets and the maximum number of record sets are shown in the Azure portal, under the 'Properties' for the zone.</span><span class="sxs-lookup"><span data-stu-id="e1082-137">The current number of record sets and the maximum number of record sets are shown in the Azure portal, under the 'Properties' for the zone.</span></span> <span data-ttu-id="e1082-138">If you have reached this limit, then either delete some record sets or contact Azure Support to raise your record set limit for this zone, then try again.</span><span class="sxs-lookup"><span data-stu-id="e1082-138">If you have reached this limit, then either delete some record sets or contact Azure Support to raise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="e1082-139">**Recommended documents**</span><span class="sxs-lookup"><span data-stu-id="e1082-139">**Recommended documents**</span></span>

[<span data-ttu-id="e1082-140">DNS zones and records</span><span class="sxs-lookup"><span data-stu-id="e1082-140">DNS zones and records</span></span>](dns-zones-records.md)
<br>
[<span data-ttu-id="e1082-141">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="e1082-141">Create a DNS zone</span></span>](dns-getstarted-create-dnszone-portal.md)



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="e1082-142">I can't resolve my DNS record</span><span class="sxs-lookup"><span data-stu-id="e1082-142">I can't resolve my DNS record</span></span>

<span data-ttu-id="e1082-143">DNS name resolution is a multi-step process, which can fail for many reasons.</span><span class="sxs-lookup"><span data-stu-id="e1082-143">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="e1082-144">The following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="e1082-144">The following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="e1082-145">Confirm that the DNS records have been configured correctly in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="e1082-145">Confirm that the DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="e1082-146">Review the DNS records in the Azure portal, checking that the zone name, record name, and record type are correct.</span><span class="sxs-lookup"><span data-stu-id="e1082-146">Review the DNS records in the Azure portal, checking that the zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="e1082-147">Confirm that the DNS records resolve correctly on the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="e1082-147">Confirm that the DNS records resolve correctly on the Azure DNS name servers.</span></span>
    - <span data-ttu-id="e1082-148">If you make DNS queries from your local PC, you may see cached results that don’t reflect the current state of the name servers.</span><span class="sxs-lookup"><span data-stu-id="e1082-148">If you make DNS queries from your local PC, you may see cached results that don’t reflect the current state of the name servers.</span></span>  <span data-ttu-id="e1082-149">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed to specific name servers.</span><span class="sxs-lookup"><span data-stu-id="e1082-149">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed to specific name servers.</span></span>  <span data-ttu-id="e1082-150">To avoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="e1082-150">To avoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="e1082-151">Be sure to specify the correct name servers for your DNS zone, as shown in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1082-151">Be sure to specify the correct name servers for your DNS zone, as shown in the Azure portal.</span></span>
    - <span data-ttu-id="e1082-152">Check that the DNS name is correct (you have to specify the fully qualified name, including the zone name) and the record type is correct</span><span class="sxs-lookup"><span data-stu-id="e1082-152">Check that the DNS name is correct (you have to specify the fully qualified name, including the zone name) and the record type is correct</span></span>
3.  <span data-ttu-id="e1082-153">Confirm that the DNS domain name has been correctly [delegated to the Azure DNS name servers](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="e1082-153">Confirm that the DNS domain name has been correctly [delegated to the Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="e1082-154">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="e1082-154">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="e1082-155">This test is a *zone* delegation test, so you should only enter the DNS zone name and not the fully qualified record name.</span><span class="sxs-lookup"><span data-stu-id="e1082-155">This test is a *zone* delegation test, so you should only enter the DNS zone name and not the fully qualified record name.</span></span>
4.  <span data-ttu-id="e1082-156">Having completed the above, your DNS record should now resolve correctly.</span><span class="sxs-lookup"><span data-stu-id="e1082-156">Having completed the above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="e1082-157">To verify, you can again use [digwebinterface](http://digwebinterface.com), this time using the default name server settings.</span><span class="sxs-lookup"><span data-stu-id="e1082-157">To verify, you can again use [digwebinterface](http://digwebinterface.com), this time using the default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="e1082-158">**Recommended documents**</span><span class="sxs-lookup"><span data-stu-id="e1082-158">**Recommended documents**</span></span>

[<span data-ttu-id="e1082-159">Delegate a domain to Azure DNS</span><span class="sxs-lookup"><span data-stu-id="e1082-159">Delegate a domain to Azure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-the-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="e1082-160">How do I specify the ‘service’ and ‘protocol’ for an SRV record?</span><span class="sxs-lookup"><span data-stu-id="e1082-160">How do I specify the ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="e1082-161">Azure DNS manages DNS records as record sets—the collection of records with the same name and the same type.</span><span class="sxs-lookup"><span data-stu-id="e1082-161">Azure DNS manages DNS records as record sets—the collection of records with the same name and the same type.</span></span> <span data-ttu-id="e1082-162">For an SRV record set, the 'service' and 'protocol' need to be specified as part of the record set name.</span><span class="sxs-lookup"><span data-stu-id="e1082-162">For an SRV record set, the 'service' and 'protocol' need to be specified as part of the record set name.</span></span> <span data-ttu-id="e1082-163">The other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in the record set.</span><span class="sxs-lookup"><span data-stu-id="e1082-163">The other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in the record set.</span></span>

<span data-ttu-id="e1082-164">Example SRV record names (service name 'sip', protocol 'tcp'):</span><span class="sxs-lookup"><span data-stu-id="e1082-164">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="e1082-165">\_sip.\_tcp (creates a record set at the zone apex)</span><span class="sxs-lookup"><span data-stu-id="e1082-165">\_sip.\_tcp (creates a record set at the zone apex)</span></span>
- <span data-ttu-id="e1082-166">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span><span class="sxs-lookup"><span data-stu-id="e1082-166">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="e1082-167">**Recommended documents**</span><span class="sxs-lookup"><span data-stu-id="e1082-167">**Recommended documents**</span></span>

[<span data-ttu-id="e1082-168">DNS zones and records</span><span class="sxs-lookup"><span data-stu-id="e1082-168">DNS zones and records</span></span>](dns-zones-records.md)
<br>
[<span data-ttu-id="e1082-169">Create DNS record sets and records by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e1082-169">Create DNS record sets and records by using the Azure portal</span></span>](dns-getstarted-create-recordset-portal.md)
<br>
[<span data-ttu-id="e1082-170">SRV record type (Wikipedia)</span><span class="sxs-lookup"><span data-stu-id="e1082-170">SRV record type (Wikipedia)</span></span>](https://en.wikipedia.org/wiki/SRV_record)


## <a name="next-steps"></a><span data-ttu-id="e1082-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1082-171">Next steps</span></span>

* <span data-ttu-id="e1082-172">Learn about [Azure DNS zones and records](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="e1082-172">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="e1082-173">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e1082-173">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="e1082-174">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="e1082-174">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span></span>

