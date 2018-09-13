---
title: Retrieve Azure Load Balancer metrics with the REST API | Microsoft Docs
description: Use the Azure REST APIs to collect health and utilization metrics for Load Balancer for a given range of time and dates.
services: sql-database
author: KumudD
ms.reviewer: routlaw
manager: jeconnoc
ms.service: load-balancer
ms.custom: REST
ms.topic: article
ms.date: 06/06/2017
ms.author: KumudD
ms.openlocfilehash: 1fac461c3af4ea0a2e1f2257256969c47bc3d134
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857448"
---
# <a name="get-load-balancer-utilization-metrics-using-the-rest-api"></a><span data-ttu-id="5bf16-103">Get Load Balancer utilization metrics using the REST API</span><span class="sxs-lookup"><span data-stu-id="5bf16-103">Get Load Balancer utilization metrics using the REST API</span></span>

<span data-ttu-id="5bf16-104">This how-to shows how to collect the number of bytes processed by a [Standard Load Balancer](/azure/load-balancer/load-balancer-standard-overview) for an interval of time using the [Azure REST API](/rest/api/azure/).</span><span class="sxs-lookup"><span data-stu-id="5bf16-104">This how-to shows how to collect the number of bytes processed by a [Standard Load Balancer](/azure/load-balancer/load-balancer-standard-overview) for an interval of time using the [Azure REST API](/rest/api/azure/).</span></span>

<span data-ttu-id="5bf16-105">Complete reference documention and additional samples for the REST API are available in the [Azure Monitor REST reference](/rest/api/monitor).</span><span class="sxs-lookup"><span data-stu-id="5bf16-105">Complete reference documention and additional samples for the REST API are available in the [Azure Monitor REST reference](/rest/api/monitor).</span></span> 

## <a name="build-the-request"></a><span data-ttu-id="5bf16-106">Build the request</span><span class="sxs-lookup"><span data-stu-id="5bf16-106">Build the request</span></span>

<span data-ttu-id="5bf16-107">Use the following GET request to collect the [ByteCount metric](/azure/load-balancer/load-balancer-standard-diagnostics#a-name--multidimensionalmetricsamulti-dimensional-metrics) from a Standard Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5bf16-107">Use the following GET request to collect the [ByteCount metric](/azure/load-balancer/load-balancer-standard-diagnostics#a-name--multidimensionalmetricsamulti-dimensional-metrics) from a Standard Load Balancer.</span></span> 

```http
GET https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/loadBalancers/{loadBalancerName}/providers/microsoft.insights/metrics?api-version=2018-01-01&metricnames=ByteCount&timespan=2018-06-05T03:00:00Z/2018-06-07T03:00:00Z
```

### <a name="request-headers"></a><span data-ttu-id="5bf16-108">Request headers</span><span class="sxs-lookup"><span data-stu-id="5bf16-108">Request headers</span></span>

<span data-ttu-id="5bf16-109">The following headers are required:</span><span class="sxs-lookup"><span data-stu-id="5bf16-109">The following headers are required:</span></span> 

|<span data-ttu-id="5bf16-110">Request header</span><span class="sxs-lookup"><span data-stu-id="5bf16-110">Request header</span></span>|<span data-ttu-id="5bf16-111">Description</span><span class="sxs-lookup"><span data-stu-id="5bf16-111">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="5bf16-112">*Content-Type:*</span><span class="sxs-lookup"><span data-stu-id="5bf16-112">*Content-Type:*</span></span>|<span data-ttu-id="5bf16-113">Required.</span><span class="sxs-lookup"><span data-stu-id="5bf16-113">Required.</span></span> <span data-ttu-id="5bf16-114">Set to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="5bf16-114">Set to `application/json`.</span></span>|  
|<span data-ttu-id="5bf16-115">*Authorization:*</span><span class="sxs-lookup"><span data-stu-id="5bf16-115">*Authorization:*</span></span>|<span data-ttu-id="5bf16-116">Required.</span><span class="sxs-lookup"><span data-stu-id="5bf16-116">Required.</span></span> <span data-ttu-id="5bf16-117">Set to a valid `Bearer` [access token](/rest/api/azure/#authorization-code-grant-interactive-clients).</span><span class="sxs-lookup"><span data-stu-id="5bf16-117">Set to a valid `Bearer` [access token](/rest/api/azure/#authorization-code-grant-interactive-clients).</span></span> |  

### <a name="uri-parameters"></a><span data-ttu-id="5bf16-118">URI parameters</span><span class="sxs-lookup"><span data-stu-id="5bf16-118">URI parameters</span></span>

| <span data-ttu-id="5bf16-119">Name</span><span class="sxs-lookup"><span data-stu-id="5bf16-119">Name</span></span> | <span data-ttu-id="5bf16-120">Description</span><span class="sxs-lookup"><span data-stu-id="5bf16-120">Description</span></span> |
| :--- | :---------- |
| <span data-ttu-id="5bf16-121">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="5bf16-121">subscriptionId</span></span> | <span data-ttu-id="5bf16-122">The subscription ID that identifies an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5bf16-122">The subscription ID that identifies an Azure subscription.</span></span> <span data-ttu-id="5bf16-123">If you have multiple subscriptions, see [Working with multiple subscriptions](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli?view=azure-cli-latest#working-with-multiple-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="5bf16-123">If you have multiple subscriptions, see [Working with multiple subscriptions](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli?view=azure-cli-latest#working-with-multiple-subscriptions).</span></span> |
| <span data-ttu-id="5bf16-124">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="5bf16-124">resourceGroupName</span></span> | <span data-ttu-id="5bf16-125">The name of the resource group that contains the resource.</span><span class="sxs-lookup"><span data-stu-id="5bf16-125">The name of the resource group that contains the resource.</span></span> <span data-ttu-id="5bf16-126">You can obtain this value from the Azure Resource Manager API, CLI, or the portal.</span><span class="sxs-lookup"><span data-stu-id="5bf16-126">You can obtain this value from the Azure Resource Manager API, CLI, or the portal.</span></span> |
| <span data-ttu-id="5bf16-127">loadBalancerName</span><span class="sxs-lookup"><span data-stu-id="5bf16-127">loadBalancerName</span></span> | <span data-ttu-id="5bf16-128">The name of the Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5bf16-128">The name of the Azure Load Balancer.</span></span> |
| <span data-ttu-id="5bf16-129">metricnames</span><span class="sxs-lookup"><span data-stu-id="5bf16-129">metricnames</span></span> | <span data-ttu-id="5bf16-130">Comma-separated list of valid  [Load Balancer metrics](/azure/load-balancer/load-balancer-standard-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="5bf16-130">Comma-separated list of valid  [Load Balancer metrics](/azure/load-balancer/load-balancer-standard-diagnostics).</span></span> |
| <span data-ttu-id="5bf16-131">api-version</span><span class="sxs-lookup"><span data-stu-id="5bf16-131">api-version</span></span> | <span data-ttu-id="5bf16-132">The API version to use for the request.</span><span class="sxs-lookup"><span data-stu-id="5bf16-132">The API version to use for the request.</span></span><br /><br /> <span data-ttu-id="5bf16-133">This document covers api-version `2018-01-01`, included in the above URL.</span><span class="sxs-lookup"><span data-stu-id="5bf16-133">This document covers api-version `2018-01-01`, included in the above URL.</span></span>  |
| <span data-ttu-id="5bf16-134">timespan</span><span class="sxs-lookup"><span data-stu-id="5bf16-134">timespan</span></span> | <span data-ttu-id="5bf16-135">The timespan of the query.</span><span class="sxs-lookup"><span data-stu-id="5bf16-135">The timespan of the query.</span></span> <span data-ttu-id="5bf16-136">It is a string with the following format `startDateTime_ISO/endDateTime_ISO`.</span><span class="sxs-lookup"><span data-stu-id="5bf16-136">It is a string with the following format `startDateTime_ISO/endDateTime_ISO`.</span></span> <span data-ttu-id="5bf16-137">This optional parameter is set to return a day's worth of data in the example.</span><span class="sxs-lookup"><span data-stu-id="5bf16-137">This optional parameter is set to return a day's worth of data in the example.</span></span> |
| &nbsp; | &nbsp; |

### <a name="request-body"></a><span data-ttu-id="5bf16-138">Request body</span><span class="sxs-lookup"><span data-stu-id="5bf16-138">Request body</span></span>

<span data-ttu-id="5bf16-139">No request body is needed for this operation.</span><span class="sxs-lookup"><span data-stu-id="5bf16-139">No request body is needed for this operation.</span></span>

## <a name="handle-the-response"></a><span data-ttu-id="5bf16-140">Handle the response</span><span class="sxs-lookup"><span data-stu-id="5bf16-140">Handle the response</span></span>

<span data-ttu-id="5bf16-141">Status code 200 is returned when the list of metric values is returned successfully.</span><span class="sxs-lookup"><span data-stu-id="5bf16-141">Status code 200 is returned when the list of metric values is returned successfully.</span></span> <span data-ttu-id="5bf16-142">A full list of error codes is available in the [reference documentation](/rest/api/monitor/metrics/list#errorresponse).</span><span class="sxs-lookup"><span data-stu-id="5bf16-142">A full list of error codes is available in the [reference documentation](/rest/api/monitor/metrics/list#errorresponse).</span></span>

## <a name="example-response"></a><span data-ttu-id="5bf16-143">Example response</span><span class="sxs-lookup"><span data-stu-id="5bf16-143">Example response</span></span> 

```json
{
    "cost": 0,
    "timespan": "2018-06-05T03:00:00Z/2018-06-07T03:00:00Z",
    "interval": "PT1M",
    "value": [
        {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/loadBalancers/{loadBalancerName}/providers/Microsoft.Insights/metrics/ByteCount",
            "type": "Microsoft.Insights/metrics",
            "name": {
                "value": "ByteCount",
                "localizedValue": "Byte Count"
            },
            "unit": "Count",
            "timeseries": [
                {
                    "metadatavalues": [],
                    "data": [
                        {
                            "timeStamp": "2018-06-06T17:24:00Z",
                            "total": 1067921034.0
                        },
                        {
                            "timeStamp": "2018-06-06T17:25:00Z",
                            "total": 0.0
                        },
                        {
                            "timeStamp": "2018-06-06T17:26:00Z",
                            "total": 3781344.0
                        },
                    ]
                }
            ]
        }
    ],
    "namespace": "Microsoft.Network/loadBalancers",
    "resourceregion": "eastus"
}
```