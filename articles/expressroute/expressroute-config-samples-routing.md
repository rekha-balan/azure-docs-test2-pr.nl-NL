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
ms.openlocfilehash: 6fefb9cfa96b0a6b7acfe4d7fcb17cb13ec240a0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550389"
---
# <a name="router-configuration-samples-to-set-up-and-manage-routing"></a><span data-ttu-id="eda2d-103">Router configuration samples to set up and manage routing</span><span class="sxs-lookup"><span data-stu-id="eda2d-103">Router configuration samples to set up and manage routing</span></span>
<span data-ttu-id="eda2d-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span><span class="sxs-lookup"><span data-stu-id="eda2d-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="eda2d-105">These are intended to be samples for guidance only and must not be used as is.</span><span class="sxs-lookup"><span data-stu-id="eda2d-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="eda2d-106">You can work with your vendor to come up with appropriate configurations for your network.</span><span class="sxs-lookup"><span data-stu-id="eda2d-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="eda2d-107">Samples in this page are intended to be purely for guidance.</span><span class="sxs-lookup"><span data-stu-id="eda2d-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="eda2d-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="eda2d-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="eda2d-109">Microsoft will not support issues related to configurations listed in this page.</span><span class="sxs-lookup"><span data-stu-id="eda2d-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="eda2d-110">You must contact your device vendor for support issues.</span><span class="sxs-lookup"><span data-stu-id="eda2d-110">You must contact your device vendor for support issues.</span></span>
> 
> 

<span data-ttu-id="eda2d-111">Router configuration samples below apply to all peerings.</span><span class="sxs-lookup"><span data-stu-id="eda2d-111">Router configuration samples below apply to all peerings.</span></span> <span data-ttu-id="eda2d-112">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span><span class="sxs-lookup"><span data-stu-id="eda2d-112">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>

## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="eda2d-113">Cisco IOS-XE based routers</span><span class="sxs-lookup"><span data-stu-id="eda2d-113">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="eda2d-114">The samples in this section apply for any router running the IOS-XE OS family.</span><span class="sxs-lookup"><span data-stu-id="eda2d-114">The samples in this section apply for any router running the IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="eda2d-115">1. Configuring interfaces and sub-interfaces</span><span class="sxs-lookup"><span data-stu-id="eda2d-115">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="eda2d-116">You will require a sub interface per peering in every router you connect to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eda2d-116">You will require a sub interface per peering in every router you connect to Microsoft.</span></span> <span data-ttu-id="eda2d-117">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span><span class="sxs-lookup"><span data-stu-id="eda2d-117">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="eda2d-118">**Dot1Q interface definition**</span><span class="sxs-lookup"><span data-stu-id="eda2d-118">**Dot1Q interface definition**</span></span>

<span data-ttu-id="eda2d-119">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="eda2d-119">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="eda2d-120">The VLAN ID is unique per peering.</span><span class="sxs-lookup"><span data-stu-id="eda2d-120">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="eda2d-121">The last octet of your IPv4 address will always be an odd number.</span><span class="sxs-lookup"><span data-stu-id="eda2d-121">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="eda2d-122">**QinQ interface definition**</span><span class="sxs-lookup"><span data-stu-id="eda2d-122">**QinQ interface definition**</span></span>

<span data-ttu-id="eda2d-123">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span><span class="sxs-lookup"><span data-stu-id="eda2d-123">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="eda2d-124">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span><span class="sxs-lookup"><span data-stu-id="eda2d-124">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="eda2d-125">The inner VLAN ID (c-tag) is unique per peering.</span><span class="sxs-lookup"><span data-stu-id="eda2d-125">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="eda2d-126">The last octet of your IPv4 address will always be an odd number.</span><span class="sxs-lookup"><span data-stu-id="eda2d-126">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="eda2d-127">2. Setting up eBGP sessions</span><span class="sxs-lookup"><span data-stu-id="eda2d-127">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="eda2d-128">You must setup a BGP session with Microsoft for every peering.</span><span class="sxs-lookup"><span data-stu-id="eda2d-128">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="eda2d-129">The sample below enables you to setup a BGP session with Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eda2d-129">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="eda2d-130">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="eda2d-130">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="eda2d-131">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span><span class="sxs-lookup"><span data-stu-id="eda2d-131">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="eda2d-132">3. Setting up prefixes to be advertised over the BGP session</span><span class="sxs-lookup"><span data-stu-id="eda2d-132">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="eda2d-133">You can configure your router to advertise select prefixes to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eda2d-133">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="eda2d-134">You can do so using the sample below.</span><span class="sxs-lookup"><span data-stu-id="eda2d-134">You can do so using the sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="eda2d-135">4. Route maps</span><span class="sxs-lookup"><span data-stu-id="eda2d-135">4. Route maps</span></span>
<span data-ttu-id="eda2d-136">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span><span class="sxs-lookup"><span data-stu-id="eda2d-136">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="eda2d-137">You can use the sample below to accomplish the task.</span><span class="sxs-lookup"><span data-stu-id="eda2d-137">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="eda2d-138">Ensure that you have appropriate prefix lists setup.</span><span class="sxs-lookup"><span data-stu-id="eda2d-138">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="eda2d-139">Juniper MX series routers</span><span class="sxs-lookup"><span data-stu-id="eda2d-139">Juniper MX series routers</span></span>
<span data-ttu-id="eda2d-140">The samples in this section apply for any Juniper MX series routers.</span><span class="sxs-lookup"><span data-stu-id="eda2d-140">The samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="eda2d-141">1. Configuring interfaces and sub-interfaces</span><span class="sxs-lookup"><span data-stu-id="eda2d-141">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="eda2d-142">**Dot1Q interface definition**</span><span class="sxs-lookup"><span data-stu-id="eda2d-142">**Dot1Q interface definition**</span></span>

<span data-ttu-id="eda2d-143">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="eda2d-143">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="eda2d-144">The VLAN ID is unique per peering.</span><span class="sxs-lookup"><span data-stu-id="eda2d-144">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="eda2d-145">The last octet of your IPv4 address will always be an odd number.</span><span class="sxs-lookup"><span data-stu-id="eda2d-145">The last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="eda2d-146">**QinQ interface definition**</span><span class="sxs-lookup"><span data-stu-id="eda2d-146">**QinQ interface definition**</span></span>

<span data-ttu-id="eda2d-147">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span><span class="sxs-lookup"><span data-stu-id="eda2d-147">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="eda2d-148">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span><span class="sxs-lookup"><span data-stu-id="eda2d-148">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="eda2d-149">The inner VLAN ID (c-tag) is unique per peering.</span><span class="sxs-lookup"><span data-stu-id="eda2d-149">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="eda2d-150">The last octet of your IPv4 address will always be an odd number.</span><span class="sxs-lookup"><span data-stu-id="eda2d-150">The last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="eda2d-151">2. Setting up eBGP sessions</span><span class="sxs-lookup"><span data-stu-id="eda2d-151">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="eda2d-152">You must setup a BGP session with Microsoft for every peering.</span><span class="sxs-lookup"><span data-stu-id="eda2d-152">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="eda2d-153">The sample below enables you to setup a BGP session with Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eda2d-153">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="eda2d-154">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span><span class="sxs-lookup"><span data-stu-id="eda2d-154">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="eda2d-155">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span><span class="sxs-lookup"><span data-stu-id="eda2d-155">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="eda2d-156">3. Setting up prefixes to be advertised over the BGP session</span><span class="sxs-lookup"><span data-stu-id="eda2d-156">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="eda2d-157">You can configure your router to advertise select prefixes to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eda2d-157">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="eda2d-158">You can do so using the sample below.</span><span class="sxs-lookup"><span data-stu-id="eda2d-158">You can do so using the sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="eda2d-159">4. Route maps</span><span class="sxs-lookup"><span data-stu-id="eda2d-159">4. Route maps</span></span>
<span data-ttu-id="eda2d-160">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span><span class="sxs-lookup"><span data-stu-id="eda2d-160">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="eda2d-161">You can use the sample below to accomplish the task.</span><span class="sxs-lookup"><span data-stu-id="eda2d-161">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="eda2d-162">Ensure that you have appropriate prefix lists setup.</span><span class="sxs-lookup"><span data-stu-id="eda2d-162">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="eda2d-163">Next Steps</span><span class="sxs-lookup"><span data-stu-id="eda2d-163">Next Steps</span></span>
<span data-ttu-id="eda2d-164">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="eda2d-164">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

