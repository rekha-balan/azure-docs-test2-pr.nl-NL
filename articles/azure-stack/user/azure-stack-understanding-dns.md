---
title: Understanding iDNS in Azure Stack | Microsoft Docs
description: Understanding iDNS features and capabilities in Azure Stack
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/21/2018
ms.author: mabrigg
ms.reviewer: scottnap
ms.openlocfilehash: 9123160f42adea57c28dff265bd5b5dbbcbb7918
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869245"
---
# <a name="introducing-idns-for-azure-stack"></a><span data-ttu-id="73604-103">Introducing iDNS for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="73604-103">Introducing iDNS for Azure Stack</span></span>

<span data-ttu-id="73604-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="73604-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="73604-105">iDNS is an Azure Stack networking feature that enables you to resolve external DNS names (for example, http://www.bing.com.) It also allows you to register internal virtual network names.</span><span class="sxs-lookup"><span data-stu-id="73604-105">iDNS is an Azure Stack networking feature that enables you to resolve external DNS names (for example, http://www.bing.com.) It also allows you to register internal virtual network names.</span></span> <span data-ttu-id="73604-106">By doing so, you can resolve VMs on the same virtual network by name rather than IP address.</span><span class="sxs-lookup"><span data-stu-id="73604-106">By doing so, you can resolve VMs on the same virtual network by name rather than IP address.</span></span> <span data-ttu-id="73604-107">This approach removes the need to provide custom DNS server entries.</span><span class="sxs-lookup"><span data-stu-id="73604-107">This approach removes the need to provide custom DNS server entries.</span></span> <span data-ttu-id="73604-108">for more information about DNS, see the [Azure DNS Overview](https://docs.microsoft.com/en-us/azure/dns/dns-overview).</span><span class="sxs-lookup"><span data-stu-id="73604-108">for more information about DNS, see the [Azure DNS Overview](https://docs.microsoft.com/en-us/azure/dns/dns-overview).</span></span>

## <a name="what-does-idns-do"></a><span data-ttu-id="73604-109">What does iDNS do?</span><span class="sxs-lookup"><span data-stu-id="73604-109">What does iDNS do?</span></span>

<span data-ttu-id="73604-110">With iDNS in Azure Stack, you get the following capabilities, without having to specify custom DNS server entries:</span><span class="sxs-lookup"><span data-stu-id="73604-110">With iDNS in Azure Stack, you get the following capabilities, without having to specify custom DNS server entries:</span></span>

- <span data-ttu-id="73604-111">Shared DNS name resolution services for tenant workloads.</span><span class="sxs-lookup"><span data-stu-id="73604-111">Shared DNS name resolution services for tenant workloads.</span></span>
- <span data-ttu-id="73604-112">Authoritative DNS service for name resolution and DNS registration within the tenant virtual network.</span><span class="sxs-lookup"><span data-stu-id="73604-112">Authoritative DNS service for name resolution and DNS registration within the tenant virtual network.</span></span>
- <span data-ttu-id="73604-113">Recursive DNS service for resolution of Internet names from tenant VMs.</span><span class="sxs-lookup"><span data-stu-id="73604-113">Recursive DNS service for resolution of Internet names from tenant VMs.</span></span> <span data-ttu-id="73604-114">Tenants no longer need to specify custom DNS entries to resolve Internet names (for example, www.bing.com.)</span><span class="sxs-lookup"><span data-stu-id="73604-114">Tenants no longer need to specify custom DNS entries to resolve Internet names (for example, www.bing.com.)</span></span>

<span data-ttu-id="73604-115">You can still bring your own DNS and use custom DNS servers.</span><span class="sxs-lookup"><span data-stu-id="73604-115">You can still bring your own DNS and use custom DNS servers.</span></span> <span data-ttu-id="73604-116">However, by using iDNS, you can resolve Internet DNS names and connect to other VMs in the same virtual network, you don’t need to create custom DNS entries.</span><span class="sxs-lookup"><span data-stu-id="73604-116">However, by using iDNS, you can resolve Internet DNS names and connect to other VMs in the same virtual network, you don’t need to create custom DNS entries.</span></span>

## <a name="what-doesnt-idns-do"></a><span data-ttu-id="73604-117">What doesn't iDNS do?</span><span class="sxs-lookup"><span data-stu-id="73604-117">What doesn't iDNS do?</span></span>

<span data-ttu-id="73604-118">What iDNS does not allow you to do, is create a DNS record for a name that can be resolved from outside the virtual network.</span><span class="sxs-lookup"><span data-stu-id="73604-118">What iDNS does not allow you to do, is create a DNS record for a name that can be resolved from outside the virtual network.</span></span>

<span data-ttu-id="73604-119">In Azure, you have the option of specifying a DNS name label that is associated with a public IP address.</span><span class="sxs-lookup"><span data-stu-id="73604-119">In Azure, you have the option of specifying a DNS name label that is associated with a public IP address.</span></span> <span data-ttu-id="73604-120">You can choose the label (prefix), but Azure chooses the suffix, which is based on the region in which you create the public IP address.</span><span class="sxs-lookup"><span data-stu-id="73604-120">You can choose the label (prefix), but Azure chooses the suffix, which is based on the region in which you create the public IP address.</span></span>

![Example of a DNS name label](media/azure-stack-understanding-dns-in-tp2/image3.png)

<span data-ttu-id="73604-122">As the previous image shows, Azure will create an “A” record in DNS for the DNS name label specified under the zone **westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="73604-122">As the previous image shows, Azure will create an “A” record in DNS for the DNS name label specified under the zone **westus.cloudapp.azure.com**.</span></span> <span data-ttu-id="73604-123">The prefix and the suffix are combined to compose a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) (FQDN) that can be resolved from anywhere on the public Internet.</span><span class="sxs-lookup"><span data-stu-id="73604-123">The prefix and the suffix are combined to compose a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) (FQDN) that can be resolved from anywhere on the public Internet.</span></span>

<span data-ttu-id="73604-124">Azure Stack only supports iDNS for internal name registration, so it cannot do the following:</span><span class="sxs-lookup"><span data-stu-id="73604-124">Azure Stack only supports iDNS for internal name registration, so it cannot do the following:</span></span>

- <span data-ttu-id="73604-125">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external.)</span><span class="sxs-lookup"><span data-stu-id="73604-125">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external.)</span></span>
- <span data-ttu-id="73604-126">Create a DNS zone (such as Contoso.com.)</span><span class="sxs-lookup"><span data-stu-id="73604-126">Create a DNS zone (such as Contoso.com.)</span></span>
- <span data-ttu-id="73604-127">Create a record under your own custom DNS zone.</span><span class="sxs-lookup"><span data-stu-id="73604-127">Create a record under your own custom DNS zone.</span></span>
- <span data-ttu-id="73604-128">Support the purchase of domain names.</span><span class="sxs-lookup"><span data-stu-id="73604-128">Support the purchase of domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73604-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="73604-129">Next steps</span></span>

[<span data-ttu-id="73604-130">Using DNS in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="73604-130">Using DNS in Azure Stack</span></span>](azure-stack-dns.md)
