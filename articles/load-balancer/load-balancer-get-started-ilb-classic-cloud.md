---
title: Create an Internal load balancer for Azure Cloud Services | Microsoft Docs
description: Learn how to create an internal load balancer using PowerShell in the classic deployment model
services: load-balancer
documentationcenter: na
author: genlin
manager: cshepard
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: genli
ms.openlocfilehash: 96a7c5b21d78dcc84a32fbfc8835542d64a5d7af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44816158"
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="52970-103">Get started creating an internal load balancer (classic) for cloud services</span><span class="sxs-lookup"><span data-stu-id="52970-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Cloud services](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).  This article covers using the classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="52970-111">Configure internal load balancer for cloud services</span><span class="sxs-lookup"><span data-stu-id="52970-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="52970-112">Internal load balancer is supported for both virtual machines and cloud services.</span><span class="sxs-lookup"><span data-stu-id="52970-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="52970-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within the cloud service.</span><span class="sxs-lookup"><span data-stu-id="52970-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within the cloud service.</span></span>

<span data-ttu-id="52970-114">The internal load balancer configuration has to be set during the creation of the first deployment in the cloud service, as shown in the sample below.</span><span class="sxs-lookup"><span data-stu-id="52970-114">The internal load balancer configuration has to be set during the creation of the first deployment in the cloud service, as shown in the sample below.</span></span>

> [!IMPORTANT]
> A prerequisite to run the steps below is to have a virtual network already created for the cloud deployment. You will need the virtual network name and subnet name to create the Internal Load Balancing.

### <a name="step-1"></a><span data-ttu-id="52970-117">Step 1</span><span class="sxs-lookup"><span data-stu-id="52970-117">Step 1</span></span>

<span data-ttu-id="52970-118">Open the service configuration file (.cscfg) for your cloud deployment in Visual Studio and add the following section to create the Internal Load Balancing under the last "`</Role>`" item for the network configuration.</span><span class="sxs-lookup"><span data-stu-id="52970-118">Open the service configuration file (.cscfg) for your cloud deployment in Visual Studio and add the following section to create the Internal Load Balancing under the last "`</Role>`" item for the network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of the load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="52970-119">Let's add the values for the network configuration file to show how it will look.</span><span class="sxs-lookup"><span data-stu-id="52970-119">Let's add the values for the network configuration file to show how it will look.</span></span> <span data-ttu-id="52970-120">In the example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="52970-120">In the example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="52970-121">The load balancer will be named testLB.</span><span class="sxs-lookup"><span data-stu-id="52970-121">The load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="52970-122">For more information about the load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span><span class="sxs-lookup"><span data-stu-id="52970-122">For more information about the load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="52970-123">Step 2</span><span class="sxs-lookup"><span data-stu-id="52970-123">Step 2</span></span>

<span data-ttu-id="52970-124">Change the service definition (.csdef) file to add endpoints to the Internal Load Balancing.</span><span class="sxs-lookup"><span data-stu-id="52970-124">Change the service definition (.csdef) file to add endpoints to the Internal Load Balancing.</span></span> <span data-ttu-id="52970-125">The moment a role instance is created, the service definition file will add the role instances to the Internal Load Balancing.</span><span class="sxs-lookup"><span data-stu-id="52970-125">The moment a role instance is created, the service definition file will add the role instances to the Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="52970-126">Following the same values from the example above, let's add the values to the service definition file.</span><span class="sxs-lookup"><span data-stu-id="52970-126">Following the same values from the example above, let's add the values to the service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="52970-127">The network traffic will be load balanced using the testLB load balancer using port 80 for incoming requests, sending to worker role instances also on port 80.</span><span class="sxs-lookup"><span data-stu-id="52970-127">The network traffic will be load balanced using the testLB load balancer using port 80 for incoming requests, sending to worker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52970-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="52970-128">Next steps</span></span>

[<span data-ttu-id="52970-129">Configure a load balancer distribution mode using source IP affinity</span><span class="sxs-lookup"><span data-stu-id="52970-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="52970-130">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="52970-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

