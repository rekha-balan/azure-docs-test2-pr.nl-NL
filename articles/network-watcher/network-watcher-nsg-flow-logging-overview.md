---
title: Introduction to flow logging for network security groups with Azure Network Watcher | Microsoft Docs
description: This article explains how to use the NSG flow logs feature of Azure Network Watcher.
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: ae4edb82fa5e192a30d297dae82199bb7efca0c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809548"
---
# <a name="introduction-to-flow-logging-for-network-security-groups"></a><span data-ttu-id="529de-103">Introduction to flow logging for network security groups</span><span class="sxs-lookup"><span data-stu-id="529de-103">Introduction to flow logging for network security groups</span></span>

<span data-ttu-id="529de-104">Network security group (NSG) flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through an NSG.</span><span class="sxs-lookup"><span data-stu-id="529de-104">Network security group (NSG) flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through an NSG.</span></span> <span data-ttu-id="529de-105">Flow logs are written in json format, and show outbound and inbound flows on a per rule basis, the network interface (NIC) the flow applies to, 5-tuple information about the flow (Source/destination IP, source/destination port, and protocol), and if the traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="529de-105">Flow logs are written in json format, and show outbound and inbound flows on a per rule basis, the network interface (NIC) the flow applies to, 5-tuple information about the flow (Source/destination IP, source/destination port, and protocol), and if the traffic was allowed or denied.</span></span>

![flow logs overview](./media/network-watcher-nsg-flow-logging-overview/figure1.png)

<span data-ttu-id="529de-107">While flow logs target NSGs, they are not displayed the same as the other logs.</span><span class="sxs-lookup"><span data-stu-id="529de-107">While flow logs target NSGs, they are not displayed the same as the other logs.</span></span> <span data-ttu-id="529de-108">Flow logs are stored only within a storage account and follow the logging path shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="529de-108">Flow logs are stored only within a storage account and follow the logging path shown in the following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId=/SUBSCRIPTIONS/{subscriptionID}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/{nsgName}/y={year}/m={month}/d={day}/h={hour}/m=00/macAddress={macAddress}/PT1H.json
```

<span data-ttu-id="529de-109">The same retention policies seen for other logs apply to flow logs.</span><span class="sxs-lookup"><span data-stu-id="529de-109">The same retention policies seen for other logs apply to flow logs.</span></span> <span data-ttu-id="529de-110">You can set log retention policy from 1 day to 2147483647 days.</span><span class="sxs-lookup"><span data-stu-id="529de-110">You can set log retention policy from 1 day to 2147483647 days.</span></span> <span data-ttu-id="529de-111">If a retention policy is not set, the logs are maintained forever.</span><span class="sxs-lookup"><span data-stu-id="529de-111">If a retention policy is not set, the logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="529de-112">Log file</span><span class="sxs-lookup"><span data-stu-id="529de-112">Log file</span></span>

<span data-ttu-id="529de-113">Flow logs include the following properties:</span><span class="sxs-lookup"><span data-stu-id="529de-113">Flow logs include the following properties:</span></span>

* <span data-ttu-id="529de-114">**time** - Time when the event was logged</span><span class="sxs-lookup"><span data-stu-id="529de-114">**time** - Time when the event was logged</span></span>
* <span data-ttu-id="529de-115">**systemId** - Network Security Group resource Id.</span><span class="sxs-lookup"><span data-stu-id="529de-115">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="529de-116">**category** - The category of the event.</span><span class="sxs-lookup"><span data-stu-id="529de-116">**category** - The category of the event.</span></span> <span data-ttu-id="529de-117">The category is always **NetworkSecurityGroupFlowEvent**</span><span class="sxs-lookup"><span data-stu-id="529de-117">The category is always **NetworkSecurityGroupFlowEvent**</span></span>
* <span data-ttu-id="529de-118">**resourceid** - The resource Id of the NSG</span><span class="sxs-lookup"><span data-stu-id="529de-118">**resourceid** - The resource Id of the NSG</span></span>
* <span data-ttu-id="529de-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="529de-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="529de-120">**properties** - A collection of properties of the flow</span><span class="sxs-lookup"><span data-stu-id="529de-120">**properties** - A collection of properties of the flow</span></span>
    * <span data-ttu-id="529de-121">**Version** - Version number of the Flow Log event schema</span><span class="sxs-lookup"><span data-stu-id="529de-121">**Version** - Version number of the Flow Log event schema</span></span>
    * <span data-ttu-id="529de-122">**flows** - A collection of flows.</span><span class="sxs-lookup"><span data-stu-id="529de-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="529de-123">This property has multiple entries for different rules</span><span class="sxs-lookup"><span data-stu-id="529de-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="529de-124">**rule** - Rule for which the flows are listed</span><span class="sxs-lookup"><span data-stu-id="529de-124">**rule** - Rule for which the flows are listed</span></span>
            * <span data-ttu-id="529de-125">**flows** - a collection of flows</span><span class="sxs-lookup"><span data-stu-id="529de-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="529de-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span><span class="sxs-lookup"><span data-stu-id="529de-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span></span>
                * <span data-ttu-id="529de-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span><span class="sxs-lookup"><span data-stu-id="529de-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="529de-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span><span class="sxs-lookup"><span data-stu-id="529de-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="529de-129">**Source IP** - The source IP</span><span class="sxs-lookup"><span data-stu-id="529de-129">**Source IP** - The source IP</span></span>
                    * <span data-ttu-id="529de-130">**Destination IP** - The destination IP</span><span class="sxs-lookup"><span data-stu-id="529de-130">**Destination IP** - The destination IP</span></span>
                    * <span data-ttu-id="529de-131">**Source Port** - The source port</span><span class="sxs-lookup"><span data-stu-id="529de-131">**Source Port** - The source port</span></span>
                    * <span data-ttu-id="529de-132">**Destination Port** - The destination Port</span><span class="sxs-lookup"><span data-stu-id="529de-132">**Destination Port** - The destination Port</span></span>
                    * <span data-ttu-id="529de-133">**Protocol** - The protocol of the flow.</span><span class="sxs-lookup"><span data-stu-id="529de-133">**Protocol** - The protocol of the flow.</span></span> <span data-ttu-id="529de-134">Valid values are **T** for TCP and **U** for UDP</span><span class="sxs-lookup"><span data-stu-id="529de-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="529de-135">**Traffic Flow** - The direction of the traffic flow.</span><span class="sxs-lookup"><span data-stu-id="529de-135">**Traffic Flow** - The direction of the traffic flow.</span></span> <span data-ttu-id="529de-136">Valid values are **I** for inbound and **O** for outbound.</span><span class="sxs-lookup"><span data-stu-id="529de-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="529de-137">**Traffic** - Whether traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="529de-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="529de-138">Valid values are **A** for allowed and **D** for denied.</span><span class="sxs-lookup"><span data-stu-id="529de-138">Valid values are **A** for allowed and **D** for denied.</span></span>

<span data-ttu-id="529de-139">The text that follows is an example of a flow log.</span><span class="sxs-lookup"><span data-stu-id="529de-139">The text that follows is an example of a flow log.</span></span> <span data-ttu-id="529de-140">As you can see, there are multiple records that follow the property list described in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="529de-140">As you can see, there are multiple records that follow the property list described in the preceding section.</span></span>

> [!NOTE]
> <span data-ttu-id="529de-141">Values in the \**flowTuples* property are a comma-separated list.</span><span class="sxs-lookup"><span data-stu-id="529de-141">Values in the \**flowTuples* property are a comma-separated list.</span></span>
 
```json
{
    "records":
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a><span data-ttu-id="529de-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="529de-142">Next steps</span></span>

- <span data-ttu-id="529de-143">To learn how to enable flow logs, see [Enabling NSG flow logging](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="529de-143">To learn how to enable flow logs, see [Enabling NSG flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>
- <span data-ttu-id="529de-144">To learn more about NSG logging, see [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="529de-144">To learn more about NSG logging, see [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json).</span></span>
- <span data-ttu-id="529de-145">To determine whether traffic is allowed or denied to or from a VM, see [Diagnose a VM network traffic filter problem](diagnose-vm-network-traffic-filtering-problem.md)</span><span class="sxs-lookup"><span data-stu-id="529de-145">To determine whether traffic is allowed or denied to or from a VM, see [Diagnose a VM network traffic filter problem](diagnose-vm-network-traffic-filtering-problem.md)</span></span>
