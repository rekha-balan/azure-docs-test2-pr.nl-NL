---
title: Introduction to flow logging for Network Security Groups with Azure Network Watcher | Microsoft Docs
description: This page explains how to use NSG flow logs a feature of Azure Network Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 3bf9a5b34c27f4943f28e47b8287397e4d90d866
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553083"
---
# <a name="introduction-to-flow-logging-for-network-security-groups"></a><span data-ttu-id="2cbde-103">Introduction to flow logging for Network Security Groups</span><span class="sxs-lookup"><span data-stu-id="2cbde-103">Introduction to flow logging for Network Security Groups</span></span>

<span data-ttu-id="2cbde-104">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="2cbde-104">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="2cbde-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="2cbde-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

![flow logs overview][1]

<span data-ttu-id="2cbde-107">While flow logs target Network Security Groups, they are not displayed the same as the other logs.</span><span class="sxs-lookup"><span data-stu-id="2cbde-107">While flow logs target Network Security Groups, they are not displayed the same as the other logs.</span></span> <span data-ttu-id="2cbde-108">Flow logs are stored only within a storage account and following the logging path as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="2cbde-108">Flow logs are stored only within a storage account and following the logging path as shown in the following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="2cbde-109">The same retention policies as seen on other logs apply to flow logs.</span><span class="sxs-lookup"><span data-stu-id="2cbde-109">The same retention policies as seen on other logs apply to flow logs.</span></span> <span data-ttu-id="2cbde-110">Logs have a retention policy that can be set from 1 day to 365 days.</span><span class="sxs-lookup"><span data-stu-id="2cbde-110">Logs have a retention policy that can be set from 1 day to 365 days.</span></span> <span data-ttu-id="2cbde-111">If a retention policy is not set, the logs are maintained forever.</span><span class="sxs-lookup"><span data-stu-id="2cbde-111">If a retention policy is not set, the logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="2cbde-112">Log file</span><span class="sxs-lookup"><span data-stu-id="2cbde-112">Log file</span></span>

<span data-ttu-id="2cbde-113">Flow logs have multiple properties.</span><span class="sxs-lookup"><span data-stu-id="2cbde-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="2cbde-114">The following list is a listing of the properties that are returned within the NSG flow log:</span><span class="sxs-lookup"><span data-stu-id="2cbde-114">The following list is a listing of the properties that are returned within the NSG flow log:</span></span>

* <span data-ttu-id="2cbde-115">**time** - Time when the event was logged</span><span class="sxs-lookup"><span data-stu-id="2cbde-115">**time** - Time when the event was logged</span></span>
* <span data-ttu-id="2cbde-116">**systemId** - Network Security Group resource Id.</span><span class="sxs-lookup"><span data-stu-id="2cbde-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="2cbde-117">**category** - The category of the event, this is always be NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="2cbde-117">**category** - The category of the event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="2cbde-118">**resourceid** - The resource Id of the NSG</span><span class="sxs-lookup"><span data-stu-id="2cbde-118">**resourceid** - The resource Id of the NSG</span></span>
* <span data-ttu-id="2cbde-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="2cbde-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="2cbde-120">**properties** - A collection of properties of the flow</span><span class="sxs-lookup"><span data-stu-id="2cbde-120">**properties** - A collection of properties of the flow</span></span>
    * <span data-ttu-id="2cbde-121">**Version** - Version number of the Flow Log event schema</span><span class="sxs-lookup"><span data-stu-id="2cbde-121">**Version** - Version number of the Flow Log event schema</span></span>
    * <span data-ttu-id="2cbde-122">**flows** - A collection of flows.</span><span class="sxs-lookup"><span data-stu-id="2cbde-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="2cbde-123">This property has multiple entries for different rules</span><span class="sxs-lookup"><span data-stu-id="2cbde-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="2cbde-124">**rule** - Rule for which the flows are listed</span><span class="sxs-lookup"><span data-stu-id="2cbde-124">**rule** - Rule for which the flows are listed</span></span>
            * <span data-ttu-id="2cbde-125">**flows** - a collection of flows</span><span class="sxs-lookup"><span data-stu-id="2cbde-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="2cbde-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span><span class="sxs-lookup"><span data-stu-id="2cbde-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span></span>
                * <span data-ttu-id="2cbde-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span><span class="sxs-lookup"><span data-stu-id="2cbde-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="2cbde-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span><span class="sxs-lookup"><span data-stu-id="2cbde-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="2cbde-129">**Source IP** - The source IP</span><span class="sxs-lookup"><span data-stu-id="2cbde-129">**Source IP** - The source IP</span></span>
                    * <span data-ttu-id="2cbde-130">**Destination IP** - The destination IP</span><span class="sxs-lookup"><span data-stu-id="2cbde-130">**Destination IP** - The destination IP</span></span>
                    * <span data-ttu-id="2cbde-131">**Source Port** - The source port</span><span class="sxs-lookup"><span data-stu-id="2cbde-131">**Source Port** - The source port</span></span>
                    * <span data-ttu-id="2cbde-132">**Destination Port** - The destination Port</span><span class="sxs-lookup"><span data-stu-id="2cbde-132">**Destination Port** - The destination Port</span></span>
                    * <span data-ttu-id="2cbde-133">**Protocol** - The protocol of the flow.</span><span class="sxs-lookup"><span data-stu-id="2cbde-133">**Protocol** - The protocol of the flow.</span></span> <span data-ttu-id="2cbde-134">Valid values are **T** for TCP and **U** for UDP</span><span class="sxs-lookup"><span data-stu-id="2cbde-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="2cbde-135">**Traffic Flow** - The direction of the traffic flow.</span><span class="sxs-lookup"><span data-stu-id="2cbde-135">**Traffic Flow** - The direction of the traffic flow.</span></span> <span data-ttu-id="2cbde-136">Valid values are **I** for inbound and **O** for outbound.</span><span class="sxs-lookup"><span data-stu-id="2cbde-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="2cbde-137">**Traffic** - Whether traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="2cbde-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="2cbde-138">Valid values are **A** for allowed and **D** for denied.</span><span class="sxs-lookup"><span data-stu-id="2cbde-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="2cbde-139">The following is an example of a Flow log.</span><span class="sxs-lookup"><span data-stu-id="2cbde-139">The following is an example of a Flow log.</span></span> <span data-ttu-id="2cbde-140">As you can see there are multiple records that follow the property list described in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="2cbde-140">As you can see there are multiple records that follow the property list described in the preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="2cbde-141">Values in the flowTuples property are a comma-separated list.</span><span class="sxs-lookup"><span data-stu-id="2cbde-141">Values in the flowTuples property are a comma-separated list.</span></span>
 
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

## <a name="next-steps"></a><span data-ttu-id="2cbde-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="2cbde-142">Next steps</span></span>

<span data-ttu-id="2cbde-143">Learn how to enable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2cbde-143">Learn how to enable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="2cbde-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="2cbde-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="2cbde-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2cbde-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-overview/figure1.png


