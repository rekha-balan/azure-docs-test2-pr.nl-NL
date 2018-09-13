---
title: Frequently asked questions for Azure Application Gateway | Microsoft Docs
description: This page provides answers to frequently asked questions about Azure Application Gateway
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 037045c4e76d0fb8e96944fe8a3235223594a034
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550357"
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="6e263-103">Frequently asked questions for Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6e263-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="6e263-104">General</span><span class="sxs-lookup"><span data-stu-id="6e263-104">General</span></span>

<span data-ttu-id="6e263-105">**Q. What is Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6e263-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="6e263-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span><span class="sxs-lookup"><span data-stu-id="6e263-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="6e263-107">It offers highly available and scalable service, which is fully managed by Azure.</span><span class="sxs-lookup"><span data-stu-id="6e263-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="6e263-108">**Q. What features does Application Gateway support?**</span><span class="sxs-lookup"><span data-stu-id="6e263-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="6e263-109">Application Gateway supports SSL offloading and end to end SSL, Web Application Firewall (preview), cookie-based session affinity, url path-based routing, multi site hosting, and others.</span><span class="sxs-lookup"><span data-stu-id="6e263-109">Application Gateway supports SSL offloading and end to end SSL, Web Application Firewall (preview), cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="6e263-110">For a full list of supported features visit [Introduction to Application Gateway](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="6e263-110">For a full list of supported features visit [Introduction to Application Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="6e263-111">**Q. What is the difference between Application Gateway and Azure Load Balancer?**</span><span class="sxs-lookup"><span data-stu-id="6e263-111">**Q. What is the difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="6e263-112">Application Gateway is a layer 7 load balancer.</span><span class="sxs-lookup"><span data-stu-id="6e263-112">Application Gateway is a layer 7 load balancer.</span></span> <span data-ttu-id="6e263-113">This means that Application Gateway deals with web traffic only (HTTP/HTTPS/WebSocket).</span><span class="sxs-lookup"><span data-stu-id="6e263-113">This means that Application Gateway deals with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="6e263-114">It supports application load balancing capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span><span class="sxs-lookup"><span data-stu-id="6e263-114">It supports application load balancing capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="6e263-115">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span><span class="sxs-lookup"><span data-stu-id="6e263-115">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="6e263-116">**Q. What protocols does Application Gateway support?**</span><span class="sxs-lookup"><span data-stu-id="6e263-116">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="6e263-117">Application Gateway supports HTTP, HTTPS, and WebSocket.</span><span class="sxs-lookup"><span data-stu-id="6e263-117">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="6e263-118">**Q. What resources are supported today as part of backend pool?**</span><span class="sxs-lookup"><span data-stu-id="6e263-118">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="6e263-119">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, and fully qualified domain names (FQDN).</span><span class="sxs-lookup"><span data-stu-id="6e263-119">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, and fully qualified domain names (FQDN).</span></span> <span data-ttu-id="6e263-120">Support for Azure Web Apps is not available today.</span><span class="sxs-lookup"><span data-stu-id="6e263-120">Support for Azure Web Apps is not available today.</span></span> <span data-ttu-id="6e263-121">Application Gateway backend pool members are not tied to an availability set.</span><span class="sxs-lookup"><span data-stu-id="6e263-121">Application Gateway backend pool members are not tied to an availability set.</span></span> <span data-ttu-id="6e263-122">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span><span class="sxs-lookup"><span data-stu-id="6e263-122">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="6e263-123">**Q. What regions is the service available in?**</span><span class="sxs-lookup"><span data-stu-id="6e263-123">**Q. What regions is the service available in?**</span></span>

<span data-ttu-id="6e263-124">Application Gateway is available in all regions of public Azure.</span><span class="sxs-lookup"><span data-stu-id="6e263-124">Application Gateway is available in all regions of public Azure.</span></span> <span data-ttu-id="6e263-125">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span><span class="sxs-lookup"><span data-stu-id="6e263-125">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="6e263-126">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span><span class="sxs-lookup"><span data-stu-id="6e263-126">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="6e263-127">Application Gateway is a dedicated deployment in your virtual network.</span><span class="sxs-lookup"><span data-stu-id="6e263-127">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="6e263-128">**Q. Is HTTP->HTTPS redirection supported?**</span><span class="sxs-lookup"><span data-stu-id="6e263-128">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="6e263-129">This is currently not supported.</span><span class="sxs-lookup"><span data-stu-id="6e263-129">This is currently not supported.</span></span>

<span data-ttu-id="6e263-130">**Q. Where do I find Application Gateway’s IP and DNS?**</span><span class="sxs-lookup"><span data-stu-id="6e263-130">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="6e263-131">When using a public IP address as an endpoint, this information can be found on the public IP address resource or on the Overview page for the Application Gateway in the portal.</span><span class="sxs-lookup"><span data-stu-id="6e263-131">When using a public IP address as an endpoint, this information can be found on the public IP address resource or on the Overview page for the Application Gateway in the portal.</span></span> <span data-ttu-id="6e263-132">For internal IP addresses, this can be found on the Overview page.</span><span class="sxs-lookup"><span data-stu-id="6e263-132">For internal IP addresses, this can be found on the Overview page.</span></span>

<span data-ttu-id="6e263-133">**Q. Does the IP or DNS change over the lifetime of the Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6e263-133">**Q. Does the IP or DNS change over the lifetime of the Application Gateway?**</span></span>

<span data-ttu-id="6e263-134">The VIP can change if the gateway is stopped and started by the customer.</span><span class="sxs-lookup"><span data-stu-id="6e263-134">The VIP can change if the gateway is stopped and started by the customer.</span></span> <span data-ttu-id="6e263-135">The DNS associated with Application Gateway does not change over the lifecycle of the gateway.</span><span class="sxs-lookup"><span data-stu-id="6e263-135">The DNS associated with Application Gateway does not change over the lifecycle of the gateway.</span></span> <span data-ttu-id="6e263-136">For this reason, it is recommended to use a CNAME alias and point it to the DNS address of the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6e263-136">For this reason, it is recommended to use a CNAME alias and point it to the DNS address of the Application Gateway.</span></span>

<span data-ttu-id="6e263-137">**Q. Does Application Gateway support static IP?**</span><span class="sxs-lookup"><span data-stu-id="6e263-137">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="6e263-138">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span><span class="sxs-lookup"><span data-stu-id="6e263-138">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="6e263-139">**Q. Does Application Gateway support multiple public IPs on the gateway?**</span><span class="sxs-lookup"><span data-stu-id="6e263-139">**Q. Does Application Gateway support multiple public IPs on the gateway?**</span></span>

<span data-ttu-id="6e263-140">Only one public IP address is supported on an Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6e263-140">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="6e263-141">**Q. Does Application Gateway support x-forwarded-for headers?**</span><span class="sxs-lookup"><span data-stu-id="6e263-141">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="6e263-142">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into the request forwarded to the backend.</span><span class="sxs-lookup"><span data-stu-id="6e263-142">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into the request forwarded to the backend.</span></span> <span data-ttu-id="6e263-143">The format for x-forwarded-for header is a comma-separated list of IP:Port.</span><span class="sxs-lookup"><span data-stu-id="6e263-143">The format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="6e263-144">The valid values for x-forwarded-proto are http or https.</span><span class="sxs-lookup"><span data-stu-id="6e263-144">The valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="6e263-145">X-forwarded-port specifies the port at which the request reached at the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6e263-145">X-forwarded-port specifies the port at which the request reached at the Application Gateway.</span></span>

## <a name="configuration"></a><span data-ttu-id="6e263-146">Configuration</span><span class="sxs-lookup"><span data-stu-id="6e263-146">Configuration</span></span>

<span data-ttu-id="6e263-147">**Q. Is Application Gateway always deployed in a virtual network?**</span><span class="sxs-lookup"><span data-stu-id="6e263-147">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="6e263-148">Yes, Application Gateway is always deployed in a virtual network subnet.</span><span class="sxs-lookup"><span data-stu-id="6e263-148">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="6e263-149">This subnet can only contain Application Gateways.</span><span class="sxs-lookup"><span data-stu-id="6e263-149">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="6e263-150">**Q. Can Application Gateway talk to instances outside its virtual network?**</span><span class="sxs-lookup"><span data-stu-id="6e263-150">**Q. Can Application Gateway talk to instances outside its virtual network?**</span></span>

<span data-ttu-id="6e263-151">Application Gateway can talk to instances outside of the virtual network that it is in as long as there is IP connectivity.</span><span class="sxs-lookup"><span data-stu-id="6e263-151">Application Gateway can talk to instances outside of the virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="6e263-152">If you plan to use internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="6e263-152">If you plan to use internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="6e263-153">**Q. Can I deploy anything else in the Application Gateway subnet?**</span><span class="sxs-lookup"><span data-stu-id="6e263-153">**Q. Can I deploy anything else in the Application Gateway subnet?**</span></span>

<span data-ttu-id="6e263-154">No, but you can deploy other application gateways in the subnet</span><span class="sxs-lookup"><span data-stu-id="6e263-154">No, but you can deploy other application gateways in the subnet</span></span>

<span data-ttu-id="6e263-155">**Q. Are Network Security Groups supported on the Application Gateway subnet?**</span><span class="sxs-lookup"><span data-stu-id="6e263-155">**Q. Are Network Security Groups supported on the Application Gateway subnet?**</span></span>

<span data-ttu-id="6e263-156">Network Security Groups are supported on the Application Gateway subnet, but exceptions must be put in for ports 65503-65534 for backend health to work correctly.</span><span class="sxs-lookup"><span data-stu-id="6e263-156">Network Security Groups are supported on the Application Gateway subnet, but exceptions must be put in for ports 65503-65534 for backend health to work correctly.</span></span> <span data-ttu-id="6e263-157">Outbound internet connectivity should not be blocked.</span><span class="sxs-lookup"><span data-stu-id="6e263-157">Outbound internet connectivity should not be blocked.</span></span>

<span data-ttu-id="6e263-158">**Q. What are the limits on Application Gateway? Can I increase these limits?**</span><span class="sxs-lookup"><span data-stu-id="6e263-158">**Q. What are the limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="6e263-159">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) to view the limits.</span><span class="sxs-lookup"><span data-stu-id="6e263-159">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) to view the limits.</span></span>

<span data-ttu-id="6e263-160">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span><span class="sxs-lookup"><span data-stu-id="6e263-160">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="6e263-161">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6e263-161">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="6e263-162">**Q. Is VNet peering supported?**</span><span class="sxs-lookup"><span data-stu-id="6e263-162">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="6e263-163">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span><span class="sxs-lookup"><span data-stu-id="6e263-163">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="6e263-164">**Q. Can I talk to on-premises servers if they are connected by ExpressRoute or VPN tunnels?**</span><span class="sxs-lookup"><span data-stu-id="6e263-164">**Q. Can I talk to on-premises servers if they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="6e263-165">Yes, as long as traffic is allowed.</span><span class="sxs-lookup"><span data-stu-id="6e263-165">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="6e263-166">**Q. Can I have one backend pool serving many applications on different ports?**</span><span class="sxs-lookup"><span data-stu-id="6e263-166">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="6e263-167">Micro service architecture is supported.</span><span class="sxs-lookup"><span data-stu-id="6e263-167">Micro service architecture is supported.</span></span> <span data-ttu-id="6e263-168">You would need multiple http settings configured to probe on different ports.</span><span class="sxs-lookup"><span data-stu-id="6e263-168">You would need multiple http settings configured to probe on different ports.</span></span>

<span data-ttu-id="6e263-169">**Q. Do custom probes support wildcards/regex on response data?**</span><span class="sxs-lookup"><span data-stu-id="6e263-169">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="6e263-170">Custom probes do not support wildcard or regex on response data.</span><span class="sxs-lookup"><span data-stu-id="6e263-170">Custom probes do not support wildcard or regex on response data.</span></span>

<span data-ttu-id="6e263-171">**Q. What does the Host field for custom probes signify?**</span><span class="sxs-lookup"><span data-stu-id="6e263-171">**Q. What does the Host field for custom probes signify?**</span></span>

<span data-ttu-id="6e263-172">Host field specifies the name to send the probe to.</span><span class="sxs-lookup"><span data-stu-id="6e263-172">Host field specifies the name to send the probe to.</span></span> <span data-ttu-id="6e263-173">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span><span class="sxs-lookup"><span data-stu-id="6e263-173">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="6e263-174">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span><span class="sxs-lookup"><span data-stu-id="6e263-174">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span> 

## <a name="performance"></a><span data-ttu-id="6e263-175">Performance</span><span class="sxs-lookup"><span data-stu-id="6e263-175">Performance</span></span>

<span data-ttu-id="6e263-176">**Q. How does Application Gateway support high availability and scalability?**</span><span class="sxs-lookup"><span data-stu-id="6e263-176">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="6e263-177">Application Gateway supports high availability scenarios if you have more than 2 instances deployed.</span><span class="sxs-lookup"><span data-stu-id="6e263-177">Application Gateway supports high availability scenarios if you have more than 2 instances deployed.</span></span> <span data-ttu-id="6e263-178">Azure distributes these instances across update and fault domains to ensure that all instances do not fail at the same time.</span><span class="sxs-lookup"><span data-stu-id="6e263-178">Azure distributes these instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="6e263-179">Application Gateway supports scalability by adding multiple instances of the same gateway to share the load.</span><span class="sxs-lookup"><span data-stu-id="6e263-179">Application Gateway supports scalability by adding multiple instances of the same gateway to share the load.</span></span>

<span data-ttu-id="6e263-180">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6e263-180">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="6e263-181">Customers can use Traffic Manager to distribute traffic across multiple Application Gateways in different datacenters.</span><span class="sxs-lookup"><span data-stu-id="6e263-181">Customers can use Traffic Manager to distribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="6e263-182">**Q. Is auto scaling supported?**</span><span class="sxs-lookup"><span data-stu-id="6e263-182">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="6e263-183">No, but Application Gateway has a throughput metric that can be used to alert you if a threshold is reached.</span><span class="sxs-lookup"><span data-stu-id="6e263-183">No, but Application Gateway has a throughput metric that can be used to alert you if a threshold is reached.</span></span> <span data-ttu-id="6e263-184">Manually adding instances or changing size does not restart the gateway and does not impact existing traffic.</span><span class="sxs-lookup"><span data-stu-id="6e263-184">Manually adding instances or changing size does not restart the gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="6e263-185">**Q. Does manual scale up/down cause downtime?**</span><span class="sxs-lookup"><span data-stu-id="6e263-185">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="6e263-186">There is no downtime, instances are distributed across upgrade domains and fault domains.</span><span class="sxs-lookup"><span data-stu-id="6e263-186">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="6e263-187">**Q. Can I change instance size from medium to large without disruption?**</span><span class="sxs-lookup"><span data-stu-id="6e263-187">**Q. Can I change instance size from medium to large without disruption?**</span></span>

<span data-ttu-id="6e263-188">Yes, Azure distributes instances across update and fault domains to ensure that all instances do not fail at the same time.</span><span class="sxs-lookup"><span data-stu-id="6e263-188">Yes, Azure distributes instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="6e263-189">Application Gateway supports scalability by adding multiple instances of the same gateway to share the load.</span><span class="sxs-lookup"><span data-stu-id="6e263-189">Application Gateway supports scalability by adding multiple instances of the same gateway to share the load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="6e263-190">SSL Configuration</span><span class="sxs-lookup"><span data-stu-id="6e263-190">SSL Configuration</span></span>

<span data-ttu-id="6e263-191">**Q. What certificates are supported on Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6e263-191">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="6e263-192">Self signed certs, CA certs, and wild-card certs are supported.</span><span class="sxs-lookup"><span data-stu-id="6e263-192">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="6e263-193">EV certs are not supported.</span><span class="sxs-lookup"><span data-stu-id="6e263-193">EV certs are not supported.</span></span>

<span data-ttu-id="6e263-194">**Q. What are the current cipher suites supported by Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6e263-194">**Q. What are the current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="6e263-195">The following are the current cipher suites supported in order of priority.</span><span class="sxs-lookup"><span data-stu-id="6e263-195">The following are the current cipher suites supported in order of priority.</span></span>

<span data-ttu-id="6e263-196">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P384</span><span class="sxs-lookup"><span data-stu-id="6e263-196">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P384</span></span>

<span data-ttu-id="6e263-197">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256</span><span class="sxs-lookup"><span data-stu-id="6e263-197">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256</span></span>

<span data-ttu-id="6e263-198">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256</span><span class="sxs-lookup"><span data-stu-id="6e263-198">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256</span></span>

<span data-ttu-id="6e263-199">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256</span><span class="sxs-lookup"><span data-stu-id="6e263-199">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256</span></span>

<span data-ttu-id="6e263-200">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256</span><span class="sxs-lookup"><span data-stu-id="6e263-200">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256</span></span>

<span data-ttu-id="6e263-201">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256</span><span class="sxs-lookup"><span data-stu-id="6e263-201">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256</span></span>

<span data-ttu-id="6e263-202">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="6e263-202">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>

<span data-ttu-id="6e263-203">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="6e263-203">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>

<span data-ttu-id="6e263-204">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="6e263-204">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>

<span data-ttu-id="6e263-205">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="6e263-205">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="6e263-206">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6e263-206">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>

<span data-ttu-id="6e263-207">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6e263-207">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>

<span data-ttu-id="6e263-208">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="6e263-208">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="6e263-209">**Q. Does Application Gateway also support re-encryption of traffic to the backend?**</span><span class="sxs-lookup"><span data-stu-id="6e263-209">**Q. Does Application Gateway also support re-encryption of traffic to the backend?**</span></span>

<span data-ttu-id="6e263-210">Yes, Applicated Gateway supports SSL offload, and end to end SSL, which re-encrypts the traffic to the backend.</span><span class="sxs-lookup"><span data-stu-id="6e263-210">Yes, Applicated Gateway supports SSL offload, and end to end SSL, which re-encrypts the traffic to the backend.</span></span>

<span data-ttu-id="6e263-211">**Q. Can I configure SSL policy to control SSL Protocol versions?**</span><span class="sxs-lookup"><span data-stu-id="6e263-211">**Q. Can I configure SSL policy to control SSL Protocol versions?**</span></span>

<span data-ttu-id="6e263-212">Yes, you can configure Application Gateway to deny TLS1.0, TLS1.1, and TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="6e263-212">Yes, you can configure Application Gateway to deny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="6e263-213">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span><span class="sxs-lookup"><span data-stu-id="6e263-213">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="6e263-214">**Q. Can I configure SSL policy to control cipher suites?**</span><span class="sxs-lookup"><span data-stu-id="6e263-214">**Q. Can I configure SSL policy to control cipher suites?**</span></span>

<span data-ttu-id="6e263-215">No, not currently.</span><span class="sxs-lookup"><span data-stu-id="6e263-215">No, not currently.</span></span>

<span data-ttu-id="6e263-216">**Q. How many SSL certificates are supported?**</span><span class="sxs-lookup"><span data-stu-id="6e263-216">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="6e263-217">Up to 20 SSL certificates are supported.</span><span class="sxs-lookup"><span data-stu-id="6e263-217">Up to 20 SSL certificates are supported.</span></span>

<span data-ttu-id="6e263-218">**Q. How many authentication certificates for backend re-encryption are supported?**</span><span class="sxs-lookup"><span data-stu-id="6e263-218">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="6e263-219">Up to 10 authentication certificates are supported with a default of 5.</span><span class="sxs-lookup"><span data-stu-id="6e263-219">Up to 10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="6e263-220">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span><span class="sxs-lookup"><span data-stu-id="6e263-220">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="6e263-221">No, it is not integrated with Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6e263-221">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="6e263-222">Web Application Firewall (WAF) Configuration</span><span class="sxs-lookup"><span data-stu-id="6e263-222">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="6e263-223">**Q. Does the WAF SKU offer all the features available with the Standard SKU?**</span><span class="sxs-lookup"><span data-stu-id="6e263-223">**Q. Does the WAF SKU offer all the features available with the Standard SKU?**</span></span>

<span data-ttu-id="6e263-224">Yes, WAF supports all the features in the Standard SKU.</span><span class="sxs-lookup"><span data-stu-id="6e263-224">Yes, WAF supports all the features in the Standard SKU.</span></span>

<span data-ttu-id="6e263-225">**Q. What is the CRS version Application Gateway supports?**</span><span class="sxs-lookup"><span data-stu-id="6e263-225">**Q. What is the CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="6e263-226">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="6e263-226">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="6e263-227">**Q. How do I monitor WAF?**</span><span class="sxs-lookup"><span data-stu-id="6e263-227">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="6e263-228">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="6e263-228">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="6e263-229">**Q. Does detection mode block traffic?**</span><span class="sxs-lookup"><span data-stu-id="6e263-229">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="6e263-230">No, detection mode only logs traffic, which triggered a WAF rule.</span><span class="sxs-lookup"><span data-stu-id="6e263-230">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="6e263-231">**Q. How do I customize WAF rules?**</span><span class="sxs-lookup"><span data-stu-id="6e263-231">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="6e263-232">Yes, WAF rules are customizable, for more information on how to customize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6e263-232">Yes, WAF rules are customizable, for more information on how to customize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="6e263-233">**Q. What rules are currently available?**</span><span class="sxs-lookup"><span data-stu-id="6e263-233">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="6e263-234">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of the top 10 vulnerabilities identified by the Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="6e263-234">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of the top 10 vulnerabilities identified by the Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="6e263-235">SQL injection protection</span><span class="sxs-lookup"><span data-stu-id="6e263-235">SQL injection protection</span></span>

* <span data-ttu-id="6e263-236">Cross site scripting protection</span><span class="sxs-lookup"><span data-stu-id="6e263-236">Cross site scripting protection</span></span>

* <span data-ttu-id="6e263-237">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span><span class="sxs-lookup"><span data-stu-id="6e263-237">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="6e263-238">Protection against HTTP protocol violations</span><span class="sxs-lookup"><span data-stu-id="6e263-238">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="6e263-239">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span><span class="sxs-lookup"><span data-stu-id="6e263-239">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="6e263-240">Prevention against bots, crawlers, and scanners</span><span class="sxs-lookup"><span data-stu-id="6e263-240">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="6e263-241">Detection of common application misconfigurations (i.e. Apache, IIS, etc.)</span><span class="sxs-lookup"><span data-stu-id="6e263-241">Detection of common application misconfigurations (i.e. Apache, IIS, etc.)</span></span>

<span data-ttu-id="6e263-242">**Q. Does WAF also support DDoS prevention?**</span><span class="sxs-lookup"><span data-stu-id="6e263-242">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="6e263-243">No, WAF does not provide DDoS prevention.</span><span class="sxs-lookup"><span data-stu-id="6e263-243">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="6e263-244">Diagnostics and Logging</span><span class="sxs-lookup"><span data-stu-id="6e263-244">Diagnostics and Logging</span></span>

<span data-ttu-id="6e263-245">**Q. What types of logs are available with Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6e263-245">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="6e263-246">There are three logs available for Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6e263-246">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="6e263-247">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logging and metrics for Application Gateway](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6e263-247">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logging and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="6e263-248">**ApplicationGatewayAccessLog** - This log contains each request submitted to the Application Gateway frontend.</span><span class="sxs-lookup"><span data-stu-id="6e263-248">**ApplicationGatewayAccessLog** - This log contains each request submitted to the Application Gateway frontend.</span></span> <span data-ttu-id="6e263-249">The data includes the caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span><span class="sxs-lookup"><span data-stu-id="6e263-249">The data includes the caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="6e263-250">This log contains one record per instance of Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6e263-250">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="6e263-251">**ApplicationGatewayPerformanceLog** - This log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span><span class="sxs-lookup"><span data-stu-id="6e263-251">**ApplicationGatewayPerformanceLog** - This log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="6e263-252">**ApplicationGatewayFirewallLog** - This log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span><span class="sxs-lookup"><span data-stu-id="6e263-252">**ApplicationGatewayFirewallLog** - This log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="6e263-253">**Q. How do I know if my backend pool members are healthy?**</span><span class="sxs-lookup"><span data-stu-id="6e263-253">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="6e263-254">You can use the PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through the portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="6e263-254">You can use the PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through the portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="6e263-255">**Q. What is the retention policy on the diagnostics logs?**</span><span class="sxs-lookup"><span data-stu-id="6e263-255">**Q. What is the retention policy on the diagnostics logs?**</span></span>

<span data-ttu-id="6e263-256">Diagnostic logs flow to the customers storage account and customers can set the retention policy based on their preference.</span><span class="sxs-lookup"><span data-stu-id="6e263-256">Diagnostic logs flow to the customers storage account and customers can set the retention policy based on their preference.</span></span> <span data-ttu-id="6e263-257">Diagnostic logs can also be sent to an Event Hub or Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6e263-257">Diagnostic logs can also be sent to an Event Hub or Log Analytics.</span></span> <span data-ttu-id="6e263-258">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="6e263-258">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="6e263-259">**Q. How do I get audit logs for Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6e263-259">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="6e263-260">Audit logs are available for Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6e263-260">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="6e263-261">In the portal, click **Activity Log** in the menu blade of an Application Gateway to access the audit log.</span><span class="sxs-lookup"><span data-stu-id="6e263-261">In the portal, click **Activity Log** in the menu blade of an Application Gateway to access the audit log.</span></span> 

<span data-ttu-id="6e263-262">**Q. Can I set alerts with Application Gateway?**</span><span class="sxs-lookup"><span data-stu-id="6e263-262">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="6e263-263">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span><span class="sxs-lookup"><span data-stu-id="6e263-263">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="6e263-264">Application Gateway currently has a metric of "throughput", which can be configured to alert.</span><span class="sxs-lookup"><span data-stu-id="6e263-264">Application Gateway currently has a metric of "throughput", which can be configured to alert.</span></span> <span data-ttu-id="6e263-265">To learn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="6e263-265">To learn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="6e263-266">**Q. Backend health returns unknown status, what could be causing this?**</span><span class="sxs-lookup"><span data-stu-id="6e263-266">**Q. Backend health returns unknown status, what could be causing this?**</span></span>

<span data-ttu-id="6e263-267">The most common reason is access to the backend is being blocked by an NSG or custom DNS.</span><span class="sxs-lookup"><span data-stu-id="6e263-267">The most common reason is access to the backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="6e263-268">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) to learn more.</span><span class="sxs-lookup"><span data-stu-id="6e263-268">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e263-269">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6e263-269">Next Steps</span></span>

<span data-ttu-id="6e263-270">To learn more about Application Gateway visit [Introduction to Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e263-270">To learn more about Application Gateway visit [Introduction to Application Gateway](application-gateway-introduction.md).</span></span>