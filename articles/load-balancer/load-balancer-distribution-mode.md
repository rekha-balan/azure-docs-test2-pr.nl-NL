---
title: Configure Load Balancer distribution mode | Microsoft Docs
description: How to configure Azure load balancer distribution mode to support source IP affinity
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3a5a603a49111aafbdd134c088a2757d81dfce69
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552025"
---
# <a name="configure-the-distribution-mode-for-load-balancer"></a><span data-ttu-id="8e6c6-103">Configure the distribution mode for load balancer</span><span class="sxs-lookup"><span data-stu-id="8e6c6-103">Configure the distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="8e6c6-104">Hash-based distribution mode</span><span class="sxs-lookup"><span data-stu-id="8e6c6-104">Hash-based distribution mode</span></span>

<span data-ttu-id="8e6c6-105">The default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-105">The default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span></span> <span data-ttu-id="8e6c6-106">It provides stickiness only within a transport session.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="8e6c6-107">Packets in the same session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-107">Packets in the same session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span></span> <span data-ttu-id="8e6c6-108">When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-108">When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span></span>

![hash based load balancer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="8e6c6-110">Figure 1 - 5-tuple distribution</span><span class="sxs-lookup"><span data-stu-id="8e6c6-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="8e6c6-111">Source IP affinity mode</span><span class="sxs-lookup"><span data-stu-id="8e6c6-111">Source IP affinity mode</span></span>

<span data-ttu-id="8e6c6-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span><span class="sxs-lookup"><span data-stu-id="8e6c6-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="8e6c6-113">Azure Load Balancer can be configured to use a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) to map traffic to the available servers.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-113">Azure Load Balancer can be configured to use a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) to map traffic to the available servers.</span></span> <span data-ttu-id="8e6c6-114">By using Source IP affinity, connections initiated from the same client computer goes to the same DIP endpoint.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-114">By using Source IP affinity, connections initiated from the same client computer goes to the same DIP endpoint.</span></span>

<span data-ttu-id="8e6c6-115">The following diagram illustrates a 2-tuple configuration.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-115">The following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="8e6c6-116">Notice how the 2-tuple runs through the load balancer to virtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-116">Notice how the 2-tuple runs through the load balancer to virtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![session affinity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="8e6c6-118">Figure 2 - 2-tuple distribution</span><span class="sxs-lookup"><span data-stu-id="8e6c6-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="8e6c6-119">Source IP affinity solves an incompatibility between the Azure Load Balancer and Remote Desktop (RD) Gateway.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-119">Source IP affinity solves an incompatibility between the Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="8e6c6-120">Now you can build an RD gateway farm in a single cloud service.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="8e6c6-121">Another use case scenario is media upload where the data upload happens through UDP but the control plane is achieved through TCP:</span><span class="sxs-lookup"><span data-stu-id="8e6c6-121">Another use case scenario is media upload where the data upload happens through UDP but the control plane is achieved through TCP:</span></span>

* <span data-ttu-id="8e6c6-122">A client first initiates a TCP session to the load balanced public address, gets directed to a specific DIP, this channel is left active to monitor the connection health</span><span class="sxs-lookup"><span data-stu-id="8e6c6-122">A client first initiates a TCP session to the load balanced public address, gets directed to a specific DIP, this channel is left active to monitor the connection health</span></span>
* <span data-ttu-id="8e6c6-123">A new UDP session from the same client computer is initiated to the same load balanced public endpoint, the expectation here is that this connection is also directed to the same DIP endpoint as the previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-123">A new UDP session from the same client computer is initiated to the same load balanced public endpoint, the expectation here is that this connection is also directed to the same DIP endpoint as the previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="8e6c6-124">When a load-balanced set changes (removing or adding a virtual machine), the distribution of client requests is recomputed.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-124">When a load-balanced set changes (removing or adding a virtual machine), the distribution of client requests is recomputed.</span></span> <span data-ttu-id="8e6c6-125">You cannot depend on new connections from existing clients ending up at the same server.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-125">You cannot depend on new connections from existing clients ending up at the same server.</span></span> <span data-ttu-id="8e6c6-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="8e6c6-127">Clients running behind proxies may be seen as one unique client application.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="8e6c6-128">Configuring Source IP affinity settings for load balancer</span><span class="sxs-lookup"><span data-stu-id="8e6c6-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="8e6c6-129">For virtual machines, you can use PowerShell to change timeout settings:</span><span class="sxs-lookup"><span data-stu-id="8e6c6-129">For virtual machines, you can use PowerShell to change timeout settings:</span></span>

<span data-ttu-id="8e6c6-130">Add an Azure endpoint to a Virtual Machine and set load balancer distribution mode</span><span class="sxs-lookup"><span data-stu-id="8e6c6-130">Add an Azure endpoint to a Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="8e6c6-131">LoadBalancerDistribution can be set to sourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want the default behavior of 5-tuple load balancing.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-131">LoadBalancerDistribution can be set to sourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want the default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="8e6c6-132">Use the following to retrieve an endpoint load balancer distribution mode configuration:</span><span class="sxs-lookup"><span data-stu-id="8e6c6-132">Use the following to retrieve an endpoint load balancer distribution mode configuration:</span></span>

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15
    LoadBalancerDistribution : sourceIP

<span data-ttu-id="8e6c6-133">If the LoadBalancerDistribution element is not present then the Azure Load balancer uses the default 5-tuple algorithm.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-133">If the LoadBalancerDistribution element is not present then the Azure Load balancer uses the default 5-tuple algorithm.</span></span>

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="8e6c6-134">Set the Distribution mode on a load balanced endpoint set</span><span class="sxs-lookup"><span data-stu-id="8e6c6-134">Set the Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="8e6c6-135">If endpoints are part of a load balanced endpoint set, the distribution mode must be set on the load balanced endpoint set:</span><span class="sxs-lookup"><span data-stu-id="8e6c6-135">If endpoints are part of a load balanced endpoint set, the distribution mode must be set on the load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a><span data-ttu-id="8e6c6-136">Cloud Service configuration to change distribution mode</span><span class="sxs-lookup"><span data-stu-id="8e6c6-136">Cloud Service configuration to change distribution mode</span></span>

<span data-ttu-id="8e6c6-137">You can leverage the Azure SDK for .NET 2.5 (to be released in November) to update your Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-137">You can leverage the Azure SDK for .NET 2.5 (to be released in November) to update your Cloud Service.</span></span> <span data-ttu-id="8e6c6-138">Endpoint settings for Cloud Services are made in the .csdef.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-138">Endpoint settings for Cloud Services are made in the .csdef.</span></span> <span data-ttu-id="8e6c6-139">In order to update the load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-139">In order to update the load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="8e6c6-140">Here is an example of .csdef changes for endpoint settings:</span><span class="sxs-lookup"><span data-stu-id="8e6c6-140">Here is an example of .csdef changes for endpoint settings:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
<InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
    <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
</InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="api-example"></a><span data-ttu-id="8e6c6-141">API example</span><span class="sxs-lookup"><span data-stu-id="8e6c6-141">API example</span></span>

<span data-ttu-id="8e6c6-142">You can configure the load balancer distribution using the service management API.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-142">You can configure the load balancer distribution using the service management API.</span></span> <span data-ttu-id="8e6c6-143">Make sure to add the `x-ms-version` header is set to version `2014-09-01` or higher.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-143">Make sure to add the `x-ms-version` header is set to version `2014-09-01` or higher.</span></span>

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="8e6c6-144">Update the configuration of the specified load-balanced set in a deployment</span><span class="sxs-lookup"><span data-stu-id="8e6c6-144">Update the configuration of the specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="8e6c6-145">Request example</span><span class="sxs-lookup"><span data-stu-id="8e6c6-145">Request example</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

<span data-ttu-id="8e6c6-146">The value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span><span class="sxs-lookup"><span data-stu-id="8e6c6-146">The value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="8e6c6-147">i.e. 5-tuple)</span><span class="sxs-lookup"><span data-stu-id="8e6c6-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="8e6c6-148">Response</span><span class="sxs-lookup"><span data-stu-id="8e6c6-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="8e6c6-149">Next Steps</span><span class="sxs-lookup"><span data-stu-id="8e6c6-149">Next Steps</span></span>

[<span data-ttu-id="8e6c6-150">Internal load balancer overview</span><span class="sxs-lookup"><span data-stu-id="8e6c6-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="8e6c6-151">Get started Configuring an Internet facing load balancer</span><span class="sxs-lookup"><span data-stu-id="8e6c6-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="8e6c6-152">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="8e6c6-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)


