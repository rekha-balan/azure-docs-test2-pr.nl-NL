---
title: Network topology considerations when using Azure Active Directory Application Proxy | Microsoft Docs
description: Covers network topology considerations when using Azure AD Application Proxy.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: kgremban
ms.openlocfilehash: f66fea4205852a9dbe4122da4b9b53659530bd34
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549975"
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a><span data-ttu-id="d64e5-103">Network topology considerations when using Azure Active Directory Application Proxy</span><span class="sxs-lookup"><span data-stu-id="d64e5-103">Network topology considerations when using Azure Active Directory Application Proxy</span></span>

<span data-ttu-id="d64e5-104">This article explains network topology considerations when using Azure Active Directory (Azure AD) Application Proxy for publishing and accessing your applications remotely.</span><span class="sxs-lookup"><span data-stu-id="d64e5-104">This article explains network topology considerations when using Azure Active Directory (Azure AD) Application Proxy for publishing and accessing your applications remotely.</span></span>

## <a name="traffic-flow"></a><span data-ttu-id="d64e5-105">Traffic flow</span><span class="sxs-lookup"><span data-stu-id="d64e5-105">Traffic flow</span></span>

<span data-ttu-id="d64e5-106">When an application is published through Azure AD Application Proxy, all traffic from the users to the target back-end applications flows through the following hops:</span><span class="sxs-lookup"><span data-stu-id="d64e5-106">When an application is published through Azure AD Application Proxy, all traffic from the users to the target back-end applications flows through the following hops:</span></span>

* <span data-ttu-id="d64e5-107">Hop 1: User to Azure AD Application Proxy service’s public endpoint on Azure</span><span class="sxs-lookup"><span data-stu-id="d64e5-107">Hop 1: User to Azure AD Application Proxy service’s public endpoint on Azure</span></span>
* <span data-ttu-id="d64e5-108">Hop 2: Application Proxy service to the connector</span><span class="sxs-lookup"><span data-stu-id="d64e5-108">Hop 2: Application Proxy service to the connector</span></span>
* <span data-ttu-id="d64e5-109">Hop 3: Connector to target application</span><span class="sxs-lookup"><span data-stu-id="d64e5-109">Hop 3: Connector to target application</span></span>

 ![Diagram showing traffic flow from user to target application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a><span data-ttu-id="d64e5-111">Tenant location and Application Proxy service</span><span class="sxs-lookup"><span data-stu-id="d64e5-111">Tenant location and Application Proxy service</span></span>

<span data-ttu-id="d64e5-112">When you sign up for an Azure AD tenant, the region of your tenant is determined by the country you specify.</span><span class="sxs-lookup"><span data-stu-id="d64e5-112">When you sign up for an Azure AD tenant, the region of your tenant is determined by the country you specify.</span></span> <span data-ttu-id="d64e5-113">When you enable Application Proxy, the Application Proxy service instances for your tenant are displayed in the same region as your Azure AD tenant, or the closest region to it.</span><span class="sxs-lookup"><span data-stu-id="d64e5-113">When you enable Application Proxy, the Application Proxy service instances for your tenant are displayed in the same region as your Azure AD tenant, or the closest region to it.</span></span>

<span data-ttu-id="d64e5-114">For example, if your Azure AD tenant’s region is the European Union (EU), all your Application Proxy connectors are using service instances in Azure datacenters in the EU.</span><span class="sxs-lookup"><span data-stu-id="d64e5-114">For example, if your Azure AD tenant’s region is the European Union (EU), all your Application Proxy connectors are using service instances in Azure datacenters in the EU.</span></span> <span data-ttu-id="d64e5-115">This also means that all your users go through the Application Proxy service instances in this location, when trying to access published applications.</span><span class="sxs-lookup"><span data-stu-id="d64e5-115">This also means that all your users go through the Application Proxy service instances in this location, when trying to access published applications.</span></span>

## <a name="considerations-for-reducing-latency"></a><span data-ttu-id="d64e5-116">Considerations for reducing latency</span><span class="sxs-lookup"><span data-stu-id="d64e5-116">Considerations for reducing latency</span></span>

<span data-ttu-id="d64e5-117">All proxy solutions introduce latency into your network connection.</span><span class="sxs-lookup"><span data-stu-id="d64e5-117">All proxy solutions introduce latency into your network connection.</span></span> <span data-ttu-id="d64e5-118">No matter which proxy or VPN solution you choose as your remote access solution, it always includes a set of servers enabling the connection to inside your corporate network.</span><span class="sxs-lookup"><span data-stu-id="d64e5-118">No matter which proxy or VPN solution you choose as your remote access solution, it always includes a set of servers enabling the connection to inside your corporate network.</span></span>

<span data-ttu-id="d64e5-119">Organizations have typically included server endpoints in their perimeter network.</span><span class="sxs-lookup"><span data-stu-id="d64e5-119">Organizations have typically included server endpoints in their perimeter network.</span></span> <span data-ttu-id="d64e5-120">But with Azure AD Application Proxy, no perimeter network is required.</span><span class="sxs-lookup"><span data-stu-id="d64e5-120">But with Azure AD Application Proxy, no perimeter network is required.</span></span> <span data-ttu-id="d64e5-121">This is because traffic flows through the proxy service in the cloud, while the connectors reside on your corporate network.</span><span class="sxs-lookup"><span data-stu-id="d64e5-121">This is because traffic flows through the proxy service in the cloud, while the connectors reside on your corporate network.</span></span>

### <a name="connector-placement"></a><span data-ttu-id="d64e5-122">Connector placement</span><span class="sxs-lookup"><span data-stu-id="d64e5-122">Connector placement</span></span>

<span data-ttu-id="d64e5-123">Application Proxy chooses the location of instances for you, based on your tenant location.</span><span class="sxs-lookup"><span data-stu-id="d64e5-123">Application Proxy chooses the location of instances for you, based on your tenant location.</span></span> <span data-ttu-id="d64e5-124">Therefore, you get to decide where to install the connector, giving you the power to define the latency characteristics of your network traffic.</span><span class="sxs-lookup"><span data-stu-id="d64e5-124">Therefore, you get to decide where to install the connector, giving you the power to define the latency characteristics of your network traffic.</span></span>

<span data-ttu-id="d64e5-125">When setting up the Application Proxy service, you should ask the following questions:</span><span class="sxs-lookup"><span data-stu-id="d64e5-125">When setting up the Application Proxy service, you should ask the following questions:</span></span>

* <span data-ttu-id="d64e5-126">Where is the app located?</span><span class="sxs-lookup"><span data-stu-id="d64e5-126">Where is the app located?</span></span>
* <span data-ttu-id="d64e5-127">Where are most users accessing the app located?</span><span class="sxs-lookup"><span data-stu-id="d64e5-127">Where are most users accessing the app located?</span></span>
* <span data-ttu-id="d64e5-128">Where is the Application Proxy instance located (this is based on your tenant)?</span><span class="sxs-lookup"><span data-stu-id="d64e5-128">Where is the Application Proxy instance located (this is based on your tenant)?</span></span>
* <span data-ttu-id="d64e5-129">Do you already have a dedicated network connection to Azure datacenters set up (such as Azure ExpressRoute or a similar VPN)?</span><span class="sxs-lookup"><span data-stu-id="d64e5-129">Do you already have a dedicated network connection to Azure datacenters set up (such as Azure ExpressRoute or a similar VPN)?</span></span>

<span data-ttu-id="d64e5-130">The placement of the connector determines the latency of hops 2 and 3 (described in the preceding section).</span><span class="sxs-lookup"><span data-stu-id="d64e5-130">The placement of the connector determines the latency of hops 2 and 3 (described in the preceding section).</span></span> <span data-ttu-id="d64e5-131">When evaluating the placement of the connector, you should consider the following:</span><span class="sxs-lookup"><span data-stu-id="d64e5-131">When evaluating the placement of the connector, you should consider the following:</span></span>

* <span data-ttu-id="d64e5-132">The connector needs a line of sight to a datacenter.</span><span class="sxs-lookup"><span data-stu-id="d64e5-132">The connector needs a line of sight to a datacenter.</span></span> <span data-ttu-id="d64e5-133">This allows the connector to perform Kerberos constrained delegation (KCD) operations, when you want single sign-on (SSO) to back-end applications.</span><span class="sxs-lookup"><span data-stu-id="d64e5-133">This allows the connector to perform Kerberos constrained delegation (KCD) operations, when you want single sign-on (SSO) to back-end applications.</span></span>
* <span data-ttu-id="d64e5-134">The connector is typically installed closer to the application, to reduce time from the connector to the application.</span><span class="sxs-lookup"><span data-stu-id="d64e5-134">The connector is typically installed closer to the application, to reduce time from the connector to the application.</span></span>

### <a name="general-approach-to-minimize-latency"></a><span data-ttu-id="d64e5-135">General approach to minimize latency</span><span class="sxs-lookup"><span data-stu-id="d64e5-135">General approach to minimize latency</span></span>

<span data-ttu-id="d64e5-136">You can try to minimize the latency of the end-to-end traffic by optimizing each of the network hops.</span><span class="sxs-lookup"><span data-stu-id="d64e5-136">You can try to minimize the latency of the end-to-end traffic by optimizing each of the network hops.</span></span> <span data-ttu-id="d64e5-137">Each hop can be optimized by:</span><span class="sxs-lookup"><span data-stu-id="d64e5-137">Each hop can be optimized by:</span></span>

* <span data-ttu-id="d64e5-138">Reducing the distance between the two ends of the hop.</span><span class="sxs-lookup"><span data-stu-id="d64e5-138">Reducing the distance between the two ends of the hop.</span></span>
* <span data-ttu-id="d64e5-139">Choosing the right network to traverse.</span><span class="sxs-lookup"><span data-stu-id="d64e5-139">Choosing the right network to traverse.</span></span> <span data-ttu-id="d64e5-140">For example, traversing a private network rather than the public Internet may be faster, due to dedicated links.</span><span class="sxs-lookup"><span data-stu-id="d64e5-140">For example, traversing a private network rather than the public Internet may be faster, due to dedicated links.</span></span>

<span data-ttu-id="d64e5-141">If you have a dedicated VPN or ExpressRoute link between Azure and your corporate network, you may want to use that.</span><span class="sxs-lookup"><span data-stu-id="d64e5-141">If you have a dedicated VPN or ExpressRoute link between Azure and your corporate network, you may want to use that.</span></span>

## <a name="focus-your-optimizing-strategy"></a><span data-ttu-id="d64e5-142">Focus your optimizing strategy</span><span class="sxs-lookup"><span data-stu-id="d64e5-142">Focus your optimizing strategy</span></span>

<span data-ttu-id="d64e5-143">Because your users may access apps remotely over the Internet, you should always focus on optimizing hops 2 and 3.</span><span class="sxs-lookup"><span data-stu-id="d64e5-143">Because your users may access apps remotely over the Internet, you should always focus on optimizing hops 2 and 3.</span></span> <span data-ttu-id="d64e5-144">The following are some of the common patterns you can incorporate.</span><span class="sxs-lookup"><span data-stu-id="d64e5-144">The following are some of the common patterns you can incorporate.</span></span>

### <a name="pattern-1-optimize-hop-3"></a><span data-ttu-id="d64e5-145">Pattern 1: Optimize hop 3</span><span class="sxs-lookup"><span data-stu-id="d64e5-145">Pattern 1: Optimize hop 3</span></span>

<span data-ttu-id="d64e5-146">To optimize hop 3, the connector is placed close to the target application in the customer network.</span><span class="sxs-lookup"><span data-stu-id="d64e5-146">To optimize hop 3, the connector is placed close to the target application in the customer network.</span></span> <span data-ttu-id="d64e5-147">The advantage of doing this is that the connector is likely to need a line of sight to the domain controller.</span><span class="sxs-lookup"><span data-stu-id="d64e5-147">The advantage of doing this is that the connector is likely to need a line of sight to the domain controller.</span></span> <span data-ttu-id="d64e5-148">This approach is sufficient for most scenarios.</span><span class="sxs-lookup"><span data-stu-id="d64e5-148">This approach is sufficient for most scenarios.</span></span> <span data-ttu-id="d64e5-149">(In fact, most of our customers follow this pattern.)</span><span class="sxs-lookup"><span data-stu-id="d64e5-149">(In fact, most of our customers follow this pattern.)</span></span>

 ![Diagram showing hop 3 optimization, with the connector placed close to the target application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-network-topologies/application-proxy-hop3.png)


> [!NOTE]
<span data-ttu-id="d64e5-151">There are some scenarios where you need to optimize both hop 2 and hop 3 to get the latency characteristics you want.</span><span class="sxs-lookup"><span data-stu-id="d64e5-151">There are some scenarios where you need to optimize both hop 2 and hop 3 to get the latency characteristics you want.</span></span> <span data-ttu-id="d64e5-152">For example, if you have a VPN or ExpressRoute set up between your network and the Azure datacenter, you can optimize both of these hops.</span><span class="sxs-lookup"><span data-stu-id="d64e5-152">For example, if you have a VPN or ExpressRoute set up between your network and the Azure datacenter, you can optimize both of these hops.</span></span>

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a><span data-ttu-id="d64e5-153">Pattern 2: Take advantage of ExpressRoute with public peering</span><span class="sxs-lookup"><span data-stu-id="d64e5-153">Pattern 2: Take advantage of ExpressRoute with public peering</span></span>

<span data-ttu-id="d64e5-154">If you have ExpressRoute set up with public peering, you can make use of the faster ExpressRoute connection for hop 2.</span><span class="sxs-lookup"><span data-stu-id="d64e5-154">If you have ExpressRoute set up with public peering, you can make use of the faster ExpressRoute connection for hop 2.</span></span> <span data-ttu-id="d64e5-155">(Hop 3 is already optimized, by placing the connector close to the app in your network.)</span><span class="sxs-lookup"><span data-stu-id="d64e5-155">(Hop 3 is already optimized, by placing the connector close to the app in your network.)</span></span>

![Diagram showing hop 2 optimization, by using an ExpressRoute connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-network-topologies/application-proxy-expressroute-public.png)

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a><span data-ttu-id="d64e5-157">Pattern 3: Take advantage of ExpressRoute with private peering</span><span class="sxs-lookup"><span data-stu-id="d64e5-157">Pattern 3: Take advantage of ExpressRoute with private peering</span></span>

<span data-ttu-id="d64e5-158">If you have a dedicated VPN or ExpressRoute set up with private peering between Azure and your corporate network, you have another option.</span><span class="sxs-lookup"><span data-stu-id="d64e5-158">If you have a dedicated VPN or ExpressRoute set up with private peering between Azure and your corporate network, you have another option.</span></span> <span data-ttu-id="d64e5-159">In this configuration, the virtual network in Azure is typically considered as an extension of the corporate network.</span><span class="sxs-lookup"><span data-stu-id="d64e5-159">In this configuration, the virtual network in Azure is typically considered as an extension of the corporate network.</span></span> <span data-ttu-id="d64e5-160">So you can install the connector in the Azure datacenter, and still satisfy the low latency requirements of the connector-to-app connection for hop 3.</span><span class="sxs-lookup"><span data-stu-id="d64e5-160">So you can install the connector in the Azure datacenter, and still satisfy the low latency requirements of the connector-to-app connection for hop 3.</span></span>

<span data-ttu-id="d64e5-161">Latency is not compromised, because traffic is flowing over a dedicated connection.</span><span class="sxs-lookup"><span data-stu-id="d64e5-161">Latency is not compromised, because traffic is flowing over a dedicated connection.</span></span> <span data-ttu-id="d64e5-162">You also get the added benefit of improving the latency characteristics of hop 2.</span><span class="sxs-lookup"><span data-stu-id="d64e5-162">You also get the added benefit of improving the latency characteristics of hop 2.</span></span> <span data-ttu-id="d64e5-163">This is because the Application Proxy service-to-connector connection is now a shorter hop.</span><span class="sxs-lookup"><span data-stu-id="d64e5-163">This is because the Application Proxy service-to-connector connection is now a shorter hop.</span></span> <span data-ttu-id="d64e5-164">The connector is installed in an Azure datacenter close to your Azure AD tenant (and therefore Application Proxy) location.</span><span class="sxs-lookup"><span data-stu-id="d64e5-164">The connector is installed in an Azure datacenter close to your Azure AD tenant (and therefore Application Proxy) location.</span></span>

![Diagram showing connector installed within an Azure datacenter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a><span data-ttu-id="d64e5-166">Other approaches</span><span class="sxs-lookup"><span data-stu-id="d64e5-166">Other approaches</span></span>

<span data-ttu-id="d64e5-167">Although the focus of this article is connector placement, you can also change the placement of the application to get better latency characteristics.</span><span class="sxs-lookup"><span data-stu-id="d64e5-167">Although the focus of this article is connector placement, you can also change the placement of the application to get better latency characteristics.</span></span>

<span data-ttu-id="d64e5-168">Increasingly, organizations are moving their networks into hosted environments.</span><span class="sxs-lookup"><span data-stu-id="d64e5-168">Increasingly, organizations are moving their networks into hosted environments.</span></span> <span data-ttu-id="d64e5-169">This enables them to place their apps in a hosted environment that is also part of their corporate network, and still be within the domain.</span><span class="sxs-lookup"><span data-stu-id="d64e5-169">This enables them to place their apps in a hosted environment that is also part of their corporate network, and still be within the domain.</span></span> <span data-ttu-id="d64e5-170">In this case, the patterns discussed in the preceding sections can be applied to the new application location.</span><span class="sxs-lookup"><span data-stu-id="d64e5-170">In this case, the patterns discussed in the preceding sections can be applied to the new application location.</span></span>

<span data-ttu-id="d64e5-171">Consider using connector groups to target apps that are in different locations and networks.</span><span class="sxs-lookup"><span data-stu-id="d64e5-171">Consider using connector groups to target apps that are in different locations and networks.</span></span> <span data-ttu-id="d64e5-172">If you're considering this option, see [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d64e5-172">If you're considering this option, see [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md).</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="d64e5-173">Common scenarios</span><span class="sxs-lookup"><span data-stu-id="d64e5-173">Common scenarios</span></span>

<span data-ttu-id="d64e5-174">In this section, we walk through a few use cases.</span><span class="sxs-lookup"><span data-stu-id="d64e5-174">In this section, we walk through a few use cases.</span></span> <span data-ttu-id="d64e5-175">Assume that the Azure AD tenant (and therefore proxy service endpoint) is located in the United States (US).</span><span class="sxs-lookup"><span data-stu-id="d64e5-175">Assume that the Azure AD tenant (and therefore proxy service endpoint) is located in the United States (US).</span></span> <span data-ttu-id="d64e5-176">The considerations discussed in these use cases usually also apply to other regions around the globe.</span><span class="sxs-lookup"><span data-stu-id="d64e5-176">The considerations discussed in these use cases usually also apply to other regions around the globe.</span></span>

### <a name="use-case-1"></a><span data-ttu-id="d64e5-177">Use case 1</span><span class="sxs-lookup"><span data-stu-id="d64e5-177">Use case 1</span></span>

<span data-ttu-id="d64e5-178">The app is in an organization's network in the US, with users in the same region.</span><span class="sxs-lookup"><span data-stu-id="d64e5-178">The app is in an organization's network in the US, with users in the same region.</span></span> <span data-ttu-id="d64e5-179">No ExpressRoute or VPN exists between the Azure datacenter and the corporate network.</span><span class="sxs-lookup"><span data-stu-id="d64e5-179">No ExpressRoute or VPN exists between the Azure datacenter and the corporate network.</span></span>

<span data-ttu-id="d64e5-180">**Recommendation:** Follow pattern 1, explained in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d64e5-180">**Recommendation:** Follow pattern 1, explained in the previous section.</span></span> <span data-ttu-id="d64e5-181">For improved latency, consider using ExpressRoute, if needed.</span><span class="sxs-lookup"><span data-stu-id="d64e5-181">For improved latency, consider using ExpressRoute, if needed.</span></span>

<span data-ttu-id="d64e5-182">This is a simple pattern.</span><span class="sxs-lookup"><span data-stu-id="d64e5-182">This is a simple pattern.</span></span> <span data-ttu-id="d64e5-183">You optimize hop 3, by placing the connector near the app.</span><span class="sxs-lookup"><span data-stu-id="d64e5-183">You optimize hop 3, by placing the connector near the app.</span></span> <span data-ttu-id="d64e5-184">This is also a natural choice, because the connector typically is installed with line of sight to the app and to the datacenter to perform KCD operations.</span><span class="sxs-lookup"><span data-stu-id="d64e5-184">This is also a natural choice, because the connector typically is installed with line of sight to the app and to the datacenter to perform KCD operations.</span></span>

![Diagram showing outline of the US, and how the hops are arranged in this use case](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a><span data-ttu-id="d64e5-186">Use case 2</span><span class="sxs-lookup"><span data-stu-id="d64e5-186">Use case 2</span></span>

<span data-ttu-id="d64e5-187">The app is in an organization's network in the US, with users spread out globally.</span><span class="sxs-lookup"><span data-stu-id="d64e5-187">The app is in an organization's network in the US, with users spread out globally.</span></span> <span data-ttu-id="d64e5-188">No ExpressRoute or VPN exists between the Azure datacenter and the corporate network.</span><span class="sxs-lookup"><span data-stu-id="d64e5-188">No ExpressRoute or VPN exists between the Azure datacenter and the corporate network.</span></span>

<span data-ttu-id="d64e5-189">**Recommendation:** Follow pattern 2, explained in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d64e5-189">**Recommendation:** Follow pattern 2, explained in the previous section.</span></span> <span data-ttu-id="d64e5-190">For improved latency, consider using ExpressRoute, if needed.</span><span class="sxs-lookup"><span data-stu-id="d64e5-190">For improved latency, consider using ExpressRoute, if needed.</span></span>

<span data-ttu-id="d64e5-191">Again, the common pattern is to optimize hop 3, where you place the connector near the app.</span><span class="sxs-lookup"><span data-stu-id="d64e5-191">Again, the common pattern is to optimize hop 3, where you place the connector near the app.</span></span> <span data-ttu-id="d64e5-192">Hop 3 is not typically expensive, if it is all within the same region.</span><span class="sxs-lookup"><span data-stu-id="d64e5-192">Hop 3 is not typically expensive, if it is all within the same region.</span></span> <span data-ttu-id="d64e5-193">However, hop 1 can be more expensive depending on where the user is, because all users access the Application Proxy instance in the US.</span><span class="sxs-lookup"><span data-stu-id="d64e5-193">However, hop 1 can be more expensive depending on where the user is, because all users access the Application Proxy instance in the US.</span></span> <span data-ttu-id="d64e5-194">It's worth noting that any proxy solution has similar characteristics regarding users being spread out globally.</span><span class="sxs-lookup"><span data-stu-id="d64e5-194">It's worth noting that any proxy solution has similar characteristics regarding users being spread out globally.</span></span>

![Diagram showing outline of global continents, and how the hops are arranged in this use case](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a><span data-ttu-id="d64e5-196">Use case 3</span><span class="sxs-lookup"><span data-stu-id="d64e5-196">Use case 3</span></span>

<span data-ttu-id="d64e5-197">The app is in an organization's network in the US.</span><span class="sxs-lookup"><span data-stu-id="d64e5-197">The app is in an organization's network in the US.</span></span> <span data-ttu-id="d64e5-198">ExpressRoute with public peering exists between Azure and the corporate network.</span><span class="sxs-lookup"><span data-stu-id="d64e5-198">ExpressRoute with public peering exists between Azure and the corporate network.</span></span>

<span data-ttu-id="d64e5-199">**Recommendation:** Place the connector as close as possible to the app.</span><span class="sxs-lookup"><span data-stu-id="d64e5-199">**Recommendation:** Place the connector as close as possible to the app.</span></span> <span data-ttu-id="d64e5-200">The system automatically uses ExpressRoute for hop 2.</span><span class="sxs-lookup"><span data-stu-id="d64e5-200">The system automatically uses ExpressRoute for hop 2.</span></span> <span data-ttu-id="d64e5-201">This follows pattern 2, explained in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d64e5-201">This follows pattern 2, explained in the previous section.</span></span>

<span data-ttu-id="d64e5-202">If the ExpressRoute link is using public peering, the traffic between the proxy and the connector flows over that link.</span><span class="sxs-lookup"><span data-stu-id="d64e5-202">If the ExpressRoute link is using public peering, the traffic between the proxy and the connector flows over that link.</span></span> <span data-ttu-id="d64e5-203">Hop 2 has optimized latency.</span><span class="sxs-lookup"><span data-stu-id="d64e5-203">Hop 2 has optimized latency.</span></span>

![Diagram showing outline of the US, and how the hops are arranged in this use case](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a><span data-ttu-id="d64e5-205">Use case 4</span><span class="sxs-lookup"><span data-stu-id="d64e5-205">Use case 4</span></span>

<span data-ttu-id="d64e5-206">The app is in an organization's network in the US.</span><span class="sxs-lookup"><span data-stu-id="d64e5-206">The app is in an organization's network in the US.</span></span> <span data-ttu-id="d64e5-207">ExpressRoute with private peering exists between Azure and the corporate network.</span><span class="sxs-lookup"><span data-stu-id="d64e5-207">ExpressRoute with private peering exists between Azure and the corporate network.</span></span>

<span data-ttu-id="d64e5-208">**Recommendation:** Place the connector in the Azure datacenter that is connected to the corporate network through ExpressRoute private peering.</span><span class="sxs-lookup"><span data-stu-id="d64e5-208">**Recommendation:** Place the connector in the Azure datacenter that is connected to the corporate network through ExpressRoute private peering.</span></span> <span data-ttu-id="d64e5-209">This follows pattern 3, explained in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d64e5-209">This follows pattern 3, explained in the previous section.</span></span>

<span data-ttu-id="d64e5-210">The connector can be placed in the Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="d64e5-210">The connector can be placed in the Azure datacenter.</span></span> <span data-ttu-id="d64e5-211">Since the connector still has a line of sight to the application and the datacenter through the private network, hop 3 remains optimized.</span><span class="sxs-lookup"><span data-stu-id="d64e5-211">Since the connector still has a line of sight to the application and the datacenter through the private network, hop 3 remains optimized.</span></span> <span data-ttu-id="d64e5-212">In addition, hop 2 is optimized further.</span><span class="sxs-lookup"><span data-stu-id="d64e5-212">In addition, hop 2 is optimized further.</span></span>

![Diagram showing outline of the US, and how the hops are arranged in this use case](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a><span data-ttu-id="d64e5-214">Use case 5</span><span class="sxs-lookup"><span data-stu-id="d64e5-214">Use case 5</span></span>

<span data-ttu-id="d64e5-215">The app is in an organization's network in the EU, with most users in the US.</span><span class="sxs-lookup"><span data-stu-id="d64e5-215">The app is in an organization's network in the EU, with most users in the US.</span></span>

<span data-ttu-id="d64e5-216">**Recommendation:** Place the connector near the app.</span><span class="sxs-lookup"><span data-stu-id="d64e5-216">**Recommendation:** Place the connector near the app.</span></span> <span data-ttu-id="d64e5-217">Because US users are accessing an Application Proxy instance that happens to be in the same region, hop 1 is not too expensive.</span><span class="sxs-lookup"><span data-stu-id="d64e5-217">Because US users are accessing an Application Proxy instance that happens to be in the same region, hop 1 is not too expensive.</span></span> <span data-ttu-id="d64e5-218">Hop 3 is optimized.</span><span class="sxs-lookup"><span data-stu-id="d64e5-218">Hop 3 is optimized.</span></span> <span data-ttu-id="d64e5-219">However, hop 2 is typically expensive in this use case.</span><span class="sxs-lookup"><span data-stu-id="d64e5-219">However, hop 2 is typically expensive in this use case.</span></span>

![Diagram showing outline of global continents, and how the hops are arranged in this use case](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-network-topologies/application-proxy-pattern5a.png)

<span data-ttu-id="d64e5-221">Consider using ExpressRoute, as described in preceding sections about patterns 2 and 3.</span><span class="sxs-lookup"><span data-stu-id="d64e5-221">Consider using ExpressRoute, as described in preceding sections about patterns 2 and 3.</span></span>

![Diagram showing outline of global continents, and how the hops are arranged in this use case](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-network-topologies/application-proxy-pattern5b.png)

<span data-ttu-id="d64e5-223">You can also consider using one other variant in this situation.</span><span class="sxs-lookup"><span data-stu-id="d64e5-223">You can also consider using one other variant in this situation.</span></span> <span data-ttu-id="d64e5-224">If most users in the organization are in the US, then chances are that your network extends to the US as well.</span><span class="sxs-lookup"><span data-stu-id="d64e5-224">If most users in the organization are in the US, then chances are that your network extends to the US as well.</span></span> <span data-ttu-id="d64e5-225">If that is the case, the connector can be placed in the US, and can use the dedicated internal corporate network line to the application in the EU.</span><span class="sxs-lookup"><span data-stu-id="d64e5-225">If that is the case, the connector can be placed in the US, and can use the dedicated internal corporate network line to the application in the EU.</span></span> <span data-ttu-id="d64e5-226">This way hops 2 and 3 are optimized.</span><span class="sxs-lookup"><span data-stu-id="d64e5-226">This way hops 2 and 3 are optimized.</span></span>

![Diagram showing outline of global continents, and how the hops are arranged in this use case](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a><span data-ttu-id="d64e5-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="d64e5-228">Next steps</span></span>

- [<span data-ttu-id="d64e5-229">Enable Application Proxy</span><span class="sxs-lookup"><span data-stu-id="d64e5-229">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
- [<span data-ttu-id="d64e5-230">Enable single-sign on</span><span class="sxs-lookup"><span data-stu-id="d64e5-230">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="d64e5-231">Enable conditional access</span><span class="sxs-lookup"><span data-stu-id="d64e5-231">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
- [<span data-ttu-id="d64e5-232">Troubleshoot issues you're having with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="d64e5-232">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)











