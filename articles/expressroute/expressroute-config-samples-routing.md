---
title: ExpressRoute customer router configuration samples | Microsoft Docs
description: This page provides router config samples for Cisco and Juniper routers.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: ''
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 032e584dc5abf59e9e3e8d80673b402f1fbf721b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44812200"
---
# <a name="router-configuration-samples-to-set-up-and-manage-routing"></a><span data-ttu-id="189d0-103">Router configuration samples to set up and manage routing</span><span class="sxs-lookup"><span data-stu-id="189d0-103">Router configuration samples to set up and manage routing</span></span>
<span data-ttu-id="189d0-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span><span class="sxs-lookup"><span data-stu-id="189d0-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="189d0-105">These are intended to be samples for guidance only and must not be used as is.</span><span class="sxs-lookup"><span data-stu-id="189d0-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="189d0-106">You can work with your vendor to come up with appropriate configurations for your network.</span><span class="sxs-lookup"><span data-stu-id="189d0-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="189d0-107">Samples in this page are intended to be purely for guidance.</span><span class="sxs-lookup"><span data-stu-id="189d0-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="189d0-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="189d0-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="189d0-109">Microsoft will not support issues related to configurations listed in this page.</span><span class="sxs-lookup"><span data-stu-id="189d0-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="189d0-110">You must contact your device vendor for support issues.</span><span class="sxs-lookup"><span data-stu-id="189d0-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="189d0-111">MTU and TCP MSS settings on router interfaces</span><span class="sxs-lookup"><span data-stu-id="189d0-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="189d0-112">The MTU for the ExpressRoute interface is 1500, which is the typical default MTU for an Ethernet interface on a router.</span><span class="sxs-lookup"><span data-stu-id="189d0-112">The MTU for the ExpressRoute interface is 1500, which is the typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="189d0-113">Unless your router has a different MTU by default, there is no need to specify a value on the router interface.</span><span class="sxs-lookup"><span data-stu-id="189d0-113">Unless your router has a different MTU by default, there is no need to specify a value on the router interface.</span></span>
* <span data-ttu-id="189d0-114">Unlike an Azure VPN Gateway, the TCP MSS for an ExpressRoute circuit does not need to be specified.</span><span class="sxs-lookup"><span data-stu-id="189d0-114">Unlike an Azure VPN Gateway, the TCP MSS for an ExpressRoute circuit does not need to be specified.</span></span>

<span data-ttu-id="189d0-115">Router configuration samples below apply to all peerings.</span><span class="sxs-lookup"><span data-stu-id="189d0-115">Router configuration samples below apply to all peerings.</span></span> <span data-ttu-id="189d0-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span><span class="sxs-lookup"><span data-stu-id="189d0-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="189d0-117">Cisco IOS-XE based routers</span><span class="sxs-lookup"><span data-stu-id="189d0-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="189d0-118">The samples in this section apply for any router running the IOS-XE OS family.</span><span class="sxs-lookup"><span data-stu-id="189d0-118">The samples in this section apply for any router running the IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="189d0-119">1. Configuring interfaces and sub-interfaces</span><span class="sxs-lookup"><span data-stu-id="189d0-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="189d0-120">You will require a sub interface per peering in every router you connect to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="189d0-120">You will require a sub interface per peering in every router you connect to Microsoft.</span></span> <span data-ttu-id="189d0-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span><span class="sxs-lookup"><span data-stu-id="189d0-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="189d0-122">**Dot1Q interface definition**</span><span class="sxs-lookup"><span data-stu-id="189d0-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="189d0-123">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="189d0-123">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="189d0-124">The VLAN ID is unique per peering.</span><span class="sxs-lookup"><span data-stu-id="189d0-124">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="189d0-125">The last octet of your IPv4 address will always be an odd number.</span><span class="sxs-lookup"><span data-stu-id="189d0-125">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="189d0-126">**QinQ interface definition**</span><span class="sxs-lookup"><span data-stu-id="189d0-126">**QinQ interface definition**</span></span>

<span data-ttu-id="189d0-127">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span><span class="sxs-lookup"><span data-stu-id="189d0-127">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="189d0-128">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span><span class="sxs-lookup"><span data-stu-id="189d0-128">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="189d0-129">The inner VLAN ID (c-tag) is unique per peering.</span><span class="sxs-lookup"><span data-stu-id="189d0-129">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="189d0-130">The last octet of your IPv4 address will always be an odd number.</span><span class="sxs-lookup"><span data-stu-id="189d0-130">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="189d0-131">2. Setting up eBGP sessions</span><span class="sxs-lookup"><span data-stu-id="189d0-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="189d0-132">You must setup a BGP session with Microsoft for every peering.</span><span class="sxs-lookup"><span data-stu-id="189d0-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="189d0-133">The sample below enables you to setup a BGP session with Microsoft.</span><span class="sxs-lookup"><span data-stu-id="189d0-133">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="189d0-134">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="189d0-134">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="189d0-135">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span><span class="sxs-lookup"><span data-stu-id="189d0-135">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="189d0-136">3. Setting up prefixes to be advertised over the BGP session</span><span class="sxs-lookup"><span data-stu-id="189d0-136">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="189d0-137">You can configure your router to advertise select prefixes to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="189d0-137">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="189d0-138">You can do so using the sample below.</span><span class="sxs-lookup"><span data-stu-id="189d0-138">You can do so using the sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="189d0-139">4. Route maps</span><span class="sxs-lookup"><span data-stu-id="189d0-139">4. Route maps</span></span>
<span data-ttu-id="189d0-140">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span><span class="sxs-lookup"><span data-stu-id="189d0-140">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="189d0-141">You can use the sample below to accomplish the task.</span><span class="sxs-lookup"><span data-stu-id="189d0-141">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="189d0-142">Ensure that you have appropriate prefix lists setup.</span><span class="sxs-lookup"><span data-stu-id="189d0-142">Ensure that you have appropriate prefix lists setup.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="189d0-143">Juniper MX series routers</span><span class="sxs-lookup"><span data-stu-id="189d0-143">Juniper MX series routers</span></span>
<span data-ttu-id="189d0-144">The samples in this section apply for any Juniper MX series routers.</span><span class="sxs-lookup"><span data-stu-id="189d0-144">The samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="189d0-145">1. Configuring interfaces and sub-interfaces</span><span class="sxs-lookup"><span data-stu-id="189d0-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="189d0-146">**Dot1Q interface definition**</span><span class="sxs-lookup"><span data-stu-id="189d0-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="189d0-147">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="189d0-147">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="189d0-148">The VLAN ID is unique per peering.</span><span class="sxs-lookup"><span data-stu-id="189d0-148">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="189d0-149">The last octet of your IPv4 address will always be an odd number.</span><span class="sxs-lookup"><span data-stu-id="189d0-149">The last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


<span data-ttu-id="189d0-150">**QinQ interface definition**</span><span class="sxs-lookup"><span data-stu-id="189d0-150">**QinQ interface definition**</span></span>

<span data-ttu-id="189d0-151">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span><span class="sxs-lookup"><span data-stu-id="189d0-151">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="189d0-152">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span><span class="sxs-lookup"><span data-stu-id="189d0-152">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="189d0-153">The inner VLAN ID (c-tag) is unique per peering.</span><span class="sxs-lookup"><span data-stu-id="189d0-153">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="189d0-154">The last octet of your IPv4 address will always be an odd number.</span><span class="sxs-lookup"><span data-stu-id="189d0-154">The last octet of your IPv4 address will always be an odd number.</span></span>

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="189d0-155">2. Setting up eBGP sessions</span><span class="sxs-lookup"><span data-stu-id="189d0-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="189d0-156">You must setup a BGP session with Microsoft for every peering.</span><span class="sxs-lookup"><span data-stu-id="189d0-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="189d0-157">The sample below enables you to setup a BGP session with Microsoft.</span><span class="sxs-lookup"><span data-stu-id="189d0-157">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="189d0-158">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="189d0-158">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="189d0-159">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span><span class="sxs-lookup"><span data-stu-id="189d0-159">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="189d0-160">3. Setting up prefixes to be advertised over the BGP session</span><span class="sxs-lookup"><span data-stu-id="189d0-160">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="189d0-161">You can configure your router to advertise select prefixes to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="189d0-161">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="189d0-162">You can do so using the sample below.</span><span class="sxs-lookup"><span data-stu-id="189d0-162">You can do so using the sample below.</span></span>

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a><span data-ttu-id="189d0-163">4. Route maps</span><span class="sxs-lookup"><span data-stu-id="189d0-163">4. Route maps</span></span>
<span data-ttu-id="189d0-164">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span><span class="sxs-lookup"><span data-stu-id="189d0-164">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="189d0-165">You can use the sample below to accomplish the task.</span><span class="sxs-lookup"><span data-stu-id="189d0-165">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="189d0-166">Ensure that you have appropriate prefix lists setup.</span><span class="sxs-lookup"><span data-stu-id="189d0-166">Ensure that you have appropriate prefix lists setup.</span></span>

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a><span data-ttu-id="189d0-167">Next Steps</span><span class="sxs-lookup"><span data-stu-id="189d0-167">Next Steps</span></span>
<span data-ttu-id="189d0-168">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="189d0-168">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

