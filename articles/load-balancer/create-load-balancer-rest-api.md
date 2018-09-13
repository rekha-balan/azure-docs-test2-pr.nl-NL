---
title: Create an Azure Load Balancer using REST API | Microsoft Docs
description: Learn how to create an Azure Load Balancer using REST API.
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: load-balancer
ms.date: 06/06/2018
ms.author: kumud
ms.openlocfilehash: ca952fa4fbea742121e579b28be35d834f17eade
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869128"
---
# <a name="create-an-azure-basic-load-balancer-using-rest-api"></a><span data-ttu-id="5a5fa-103">Create an Azure Basic Load Balancer using REST API</span><span class="sxs-lookup"><span data-stu-id="5a5fa-103">Create an Azure Basic Load Balancer using REST API</span></span>

<span data-ttu-id="5a5fa-104">An Azure Load Balancer distributes new inbound flows that arrive on the load balancer's frontend to the backend pool instances, according to rules and health probes.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-104">An Azure Load Balancer distributes new inbound flows that arrive on the load balancer's frontend to the backend pool instances, according to rules and health probes.</span></span> <span data-ttu-id="5a5fa-105">The Load Balancer is available in two SKUs: Basic and Standard.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-105">The Load Balancer is available in two SKUs: Basic and Standard.</span></span> <span data-ttu-id="5a5fa-106">To understand the difference between the two SKU versions, [Load Balancer SKU comparisons](load-balancer-overview.md#skus).</span><span class="sxs-lookup"><span data-stu-id="5a5fa-106">To understand the difference between the two SKU versions, [Load Balancer SKU comparisons](load-balancer-overview.md#skus).</span></span>
 
<span data-ttu-id="5a5fa-107">This how-to shows how to create an Azure Basic Load Balancer using [Azure REST API](/rest/api/azure/) to help load balance incoming request across multiple VMs within an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-107">This how-to shows how to create an Azure Basic Load Balancer using [Azure REST API](/rest/api/azure/) to help load balance incoming request across multiple VMs within an Azure virtual network.</span></span> <span data-ttu-id="5a5fa-108">Complete reference documentation and additional samples are available in the [Azure Load Balancer REST reference](/rest/api/load-balancer/).</span><span class="sxs-lookup"><span data-stu-id="5a5fa-108">Complete reference documentation and additional samples are available in the [Azure Load Balancer REST reference](/rest/api/load-balancer/).</span></span>
 
## <a name="build-the-request"></a><span data-ttu-id="5a5fa-109">Build the request</span><span class="sxs-lookup"><span data-stu-id="5a5fa-109">Build the request</span></span>
<span data-ttu-id="5a5fa-110">Use the following HTTP PUT request to create a new Azure Basic Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-110">Use the following HTTP PUT request to create a new Azure Basic Load Balancer.</span></span>
 ```HTTP
  PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/loadBalancers/{loadBalancerName}?api-version=2018-02-01
  ```
### <a name="uri-parameters"></a><span data-ttu-id="5a5fa-111">URI parameters</span><span class="sxs-lookup"><span data-stu-id="5a5fa-111">URI parameters</span></span>

|<span data-ttu-id="5a5fa-112">Name</span><span class="sxs-lookup"><span data-stu-id="5a5fa-112">Name</span></span>  |<span data-ttu-id="5a5fa-113">In</span><span class="sxs-lookup"><span data-stu-id="5a5fa-113">In</span></span>  |<span data-ttu-id="5a5fa-114">Required</span><span class="sxs-lookup"><span data-stu-id="5a5fa-114">Required</span></span> |<span data-ttu-id="5a5fa-115">Type</span><span class="sxs-lookup"><span data-stu-id="5a5fa-115">Type</span></span> |<span data-ttu-id="5a5fa-116">Description</span><span class="sxs-lookup"><span data-stu-id="5a5fa-116">Description</span></span> |
|---------|---------|---------|---------|--------|
|<span data-ttu-id="5a5fa-117">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="5a5fa-117">subscriptionId</span></span>   |  <span data-ttu-id="5a5fa-118">path</span><span class="sxs-lookup"><span data-stu-id="5a5fa-118">path</span></span>       |  <span data-ttu-id="5a5fa-119">True</span><span class="sxs-lookup"><span data-stu-id="5a5fa-119">True</span></span>       |   <span data-ttu-id="5a5fa-120">string</span><span class="sxs-lookup"><span data-stu-id="5a5fa-120">string</span></span>      |  <span data-ttu-id="5a5fa-121">The subscription credentials that uniquely identify the Microsoft Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-121">The subscription credentials that uniquely identify the Microsoft Azure subscription.</span></span> <span data-ttu-id="5a5fa-122">The subscription ID forms part of the URI for every service call.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-122">The subscription ID forms part of the URI for every service call.</span></span>      |
|<span data-ttu-id="5a5fa-123">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="5a5fa-123">resourceGroupName</span></span>     |     <span data-ttu-id="5a5fa-124">path</span><span class="sxs-lookup"><span data-stu-id="5a5fa-124">path</span></span>    | <span data-ttu-id="5a5fa-125">True</span><span class="sxs-lookup"><span data-stu-id="5a5fa-125">True</span></span>        |  <span data-ttu-id="5a5fa-126">string</span><span class="sxs-lookup"><span data-stu-id="5a5fa-126">string</span></span>       |   <span data-ttu-id="5a5fa-127">The name of the resource group.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-127">The name of the resource group.</span></span>     |
|<span data-ttu-id="5a5fa-128">loadBalancerName</span><span class="sxs-lookup"><span data-stu-id="5a5fa-128">loadBalancerName</span></span>     |  <span data-ttu-id="5a5fa-129">path</span><span class="sxs-lookup"><span data-stu-id="5a5fa-129">path</span></span>       |      <span data-ttu-id="5a5fa-130">True</span><span class="sxs-lookup"><span data-stu-id="5a5fa-130">True</span></span>   |    <span data-ttu-id="5a5fa-131">string</span><span class="sxs-lookup"><span data-stu-id="5a5fa-131">string</span></span>     |    <span data-ttu-id="5a5fa-132">The name of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-132">The name of the load balancer.</span></span>    |
|<span data-ttu-id="5a5fa-133">api-version</span><span class="sxs-lookup"><span data-stu-id="5a5fa-133">api-version</span></span>    |   <span data-ttu-id="5a5fa-134">query</span><span class="sxs-lookup"><span data-stu-id="5a5fa-134">query</span></span>     |  <span data-ttu-id="5a5fa-135">True</span><span class="sxs-lookup"><span data-stu-id="5a5fa-135">True</span></span>       |     <span data-ttu-id="5a5fa-136">string</span><span class="sxs-lookup"><span data-stu-id="5a5fa-136">string</span></span>    |  <span data-ttu-id="5a5fa-137">Client API version.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-137">Client API version.</span></span>      |



### <a name="request-body"></a><span data-ttu-id="5a5fa-138">Request body</span><span class="sxs-lookup"><span data-stu-id="5a5fa-138">Request body</span></span>

<span data-ttu-id="5a5fa-139">The only required parameter is `location`.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-139">The only required parameter is `location`.</span></span> <span data-ttu-id="5a5fa-140">If you do not define the *SKU* version, a Basic Load Balancer is created by default.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-140">If you do not define the *SKU* version, a Basic Load Balancer is created by default.</span></span>  <span data-ttu-id="5a5fa-141">Use [optional parameters](https://docs.microsoft.com/rest/api/load-balancer/loadbalancers/createorupdate#request-body) to customize the load balancer.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-141">Use [optional parameters](https://docs.microsoft.com/rest/api/load-balancer/loadbalancers/createorupdate#request-body) to customize the load balancer.</span></span>

| <span data-ttu-id="5a5fa-142">Name</span><span class="sxs-lookup"><span data-stu-id="5a5fa-142">Name</span></span> | <span data-ttu-id="5a5fa-143">Type</span><span class="sxs-lookup"><span data-stu-id="5a5fa-143">Type</span></span> | <span data-ttu-id="5a5fa-144">Description</span><span class="sxs-lookup"><span data-stu-id="5a5fa-144">Description</span></span> |
| :--- | :--- | :---------- |
| <span data-ttu-id="5a5fa-145">location</span><span class="sxs-lookup"><span data-stu-id="5a5fa-145">location</span></span> | <span data-ttu-id="5a5fa-146">string</span><span class="sxs-lookup"><span data-stu-id="5a5fa-146">string</span></span> | <span data-ttu-id="5a5fa-147">Resource location.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-147">Resource location.</span></span> <span data-ttu-id="5a5fa-148">Get a current list of locations using the [List Locations](https://docs.microsoft.com/rest/api/resources/subscriptions/listlocations) operation.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-148">Get a current list of locations using the [List Locations](https://docs.microsoft.com/rest/api/resources/subscriptions/listlocations) operation.</span></span> |


## <a name="example-create-and-update-a-basic-load-balancer"></a><span data-ttu-id="5a5fa-149">Example: Create and update a Basic Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5a5fa-149">Example: Create and update a Basic Load Balancer</span></span>

<span data-ttu-id="5a5fa-150">In this example, you first create a Basic Load Balancer along with its resources.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-150">In this example, you first create a Basic Load Balancer along with its resources.</span></span> <span data-ttu-id="5a5fa-151">Next, you configure the load balancer resources that include a frontend IP configuration, a backend address pool, a load balancing rule, a health probe, and an inbound NAT rule.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-151">Next, you configure the load balancer resources that include a frontend IP configuration, a backend address pool, a load balancing rule, a health probe, and an inbound NAT rule.</span></span>

<span data-ttu-id="5a5fa-152">Before you create a load balancer using the example below, create a virtual network named *vnetlb* with a subnet named *subnetlb* in a resource group named *rg1* in the **East US** location.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-152">Before you create a load balancer using the example below, create a virtual network named *vnetlb* with a subnet named *subnetlb* in a resource group named *rg1* in the **East US** location.</span></span>

### <a name="step-1-create-a-basic-load-balancer"></a><span data-ttu-id="5a5fa-153">STEP 1.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-153">STEP 1.</span></span> <span data-ttu-id="5a5fa-154">Create a Basic Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5a5fa-154">Create a Basic Load Balancer</span></span>
<span data-ttu-id="5a5fa-155">In this step, you create a Basic Load Balancer, named *lb* at the **EAST US** location within the *rg1* resource group.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-155">In this step, you create a Basic Load Balancer, named *lb* at the **EAST US** location within the *rg1* resource group.</span></span>
#### <a name="sample-request"></a><span data-ttu-id="5a5fa-156">Sample request</span><span class="sxs-lookup"><span data-stu-id="5a5fa-156">Sample request</span></span>

  ```HTTP    
  PUT https://management.azure.com/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/loadBalancers/lb?api-version=2018-02-01
  ```
#### <a name="request-body"></a><span data-ttu-id="5a5fa-157">Request body</span><span class="sxs-lookup"><span data-stu-id="5a5fa-157">Request body</span></span>

  ```JSON
   {
    "location": "eastus",
   }
  ```
### <a name="step-2-configure-load-balancer-resources"></a><span data-ttu-id="5a5fa-158">STEP 2.</span><span class="sxs-lookup"><span data-stu-id="5a5fa-158">STEP 2.</span></span> <span data-ttu-id="5a5fa-159">Configure load balancer resources</span><span class="sxs-lookup"><span data-stu-id="5a5fa-159">Configure load balancer resources</span></span>
<span data-ttu-id="5a5fa-160">In this step, you configure the load balancer *lb* resources that include a frontend IP configuration (*fe-lb*), a backend address pool (*be-lb*), a load balancing rule (*rulelb*), a health probe (*probe-lb*), and an inbound NAT rule (*in-nat-rule*).</span><span class="sxs-lookup"><span data-stu-id="5a5fa-160">In this step, you configure the load balancer *lb* resources that include a frontend IP configuration (*fe-lb*), a backend address pool (*be-lb*), a load balancing rule (*rulelb*), a health probe (*probe-lb*), and an inbound NAT rule (*in-nat-rule*).</span></span>
#### <a name="sample-request"></a><span data-ttu-id="5a5fa-161">Sample request</span><span class="sxs-lookup"><span data-stu-id="5a5fa-161">Sample request</span></span>

  ```HTTP    
  PUT https://management.azure.com/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/loadBalancers/lb?api-version=2018-02-01
  ```
#### <a name="request-body"></a><span data-ttu-id="5a5fa-162">Request body</span><span class="sxs-lookup"><span data-stu-id="5a5fa-162">Request body</span></span>

  ```JSON
{
  "properties": {
    "frontendIPConfigurations": [
      {
        "name": "fe-lb",
        "properties": {
          "subnet": {
            "id": "/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/virtualNetworks/vnetlb/subnets/subnetlb"
          },
          "loadBalancingRules": [
            {
              "id": "/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/loadBalancers/lb/loadBalancingRules/rulelb"
            }  ],
          "inboundNatRules": [
            {
              "id": "/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/loadBalancers/lb/inboundNatRules/in-nat-rule"
            }  ]  }  }  ],
    "backendAddressPools": [
      {
        "name": "be-lb",
        "properties": {
          "loadBalancingRules": [
            {
              "id": "/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/loadBalancers/lb/loadBalancingRules/rulelb"
            }  ]   }   }   ],
    "loadBalancingRules": [
      {
        "name": "rulelb",
        "properties": {
          "frontendIPConfiguration": {
            "id": "/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/loadBalancers/lb/frontendIPConfigurations/fe-lb"
          },
          "frontendPort": 80,
          "backendPort": 80,
          "enableFloatingIP": true,
          "idleTimeoutInMinutes": 15,
          "protocol": "Tcp",
          "loadDistribution": "Default",
          "backendAddressPool": {
            "id": "/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/loadBalancers/lb/backendAddressPools/be-lb"
          },
          "probe": {
            "id": "/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/loadBalancers/lb/probes/probe-lb"
          }  }  }  ],
    "probes": [
      {
        "name": "probe-lb",
        "properties": {
          "protocol": "Http",
          "port": 80,
          "requestPath": "healthcheck.aspx",
          "intervalInSeconds": 15,
          "numberOfProbes": 2,
          "loadBalancingRules": [
            {
              "id": "/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/loadBalancers/lb/loadBalancingRules/rulelb"
            }  ]  }  } ],
    "inboundNatRules": [
      {
        "name": "in-nat-rule",
        "properties": {
          "frontendIPConfiguration": {
            "id": "/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/loadBalancers/lb/frontendIPConfigurations/fe-lb"
          },
          "frontendPort": 3389,
          "backendPort": 3389,
          "enableFloatingIP": true,
          "idleTimeoutInMinutes": 15,
          "protocol": "Tcp"
        } } ],
    "inboundNatPools": [],
    "outboundNatRules": []
  }  }
```
