---
title: Azure asynchronous operations | Microsoft Docs
description: Describes how to track asynchronous operations in Azure.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 9fe3d98cd345aae45722295b6c1b7fc3e9036e95
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551433"
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="110e8-103">Track asynchronous Azure operations</span><span class="sxs-lookup"><span data-stu-id="110e8-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="110e8-104">Some Azure REST operations run asynchronously because the operation cannot be completed quickly.</span><span class="sxs-lookup"><span data-stu-id="110e8-104">Some Azure REST operations run asynchronously because the operation cannot be completed quickly.</span></span> <span data-ttu-id="110e8-105">This topic describes how to track the status of asynchronous operations through values returned in the response.</span><span class="sxs-lookup"><span data-stu-id="110e8-105">This topic describes how to track the status of asynchronous operations through values returned in the response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="110e8-106">Status codes for asynchronous operations</span><span class="sxs-lookup"><span data-stu-id="110e8-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="110e8-107">An asynchronous operation initially returns an HTTP status code of either:</span><span class="sxs-lookup"><span data-stu-id="110e8-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="110e8-108">201 (Created)</span><span class="sxs-lookup"><span data-stu-id="110e8-108">201 (Created)</span></span>
* <span data-ttu-id="110e8-109">202 (Accepted)</span><span class="sxs-lookup"><span data-stu-id="110e8-109">202 (Accepted)</span></span> 

<span data-ttu-id="110e8-110">When the operation successfully completes, it returns either:</span><span class="sxs-lookup"><span data-stu-id="110e8-110">When the operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="110e8-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="110e8-111">200 (OK)</span></span>
* <span data-ttu-id="110e8-112">204 (No Content)</span><span class="sxs-lookup"><span data-stu-id="110e8-112">204 (No Content)</span></span> 

<span data-ttu-id="110e8-113">Refer to the [REST API documentation](/rest/api/) to see the responses for the operation you are executing.</span><span class="sxs-lookup"><span data-stu-id="110e8-113">Refer to the [REST API documentation](/rest/api/) to see the responses for the operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="110e8-114">Monitor status of operation</span><span class="sxs-lookup"><span data-stu-id="110e8-114">Monitor status of operation</span></span>
<span data-ttu-id="110e8-115">The asynchronous REST operations return header values, which you use to determine the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="110e8-115">The asynchronous REST operations return header values, which you use to determine the status of the operation.</span></span> <span data-ttu-id="110e8-116">There are potentially three header values to examine:</span><span class="sxs-lookup"><span data-stu-id="110e8-116">There are potentially three header values to examine:</span></span>

* <span data-ttu-id="110e8-117">`Azure-AsyncOperation` - URL for checking the ongoing status of the operation.</span><span class="sxs-lookup"><span data-stu-id="110e8-117">`Azure-AsyncOperation` - URL for checking the ongoing status of the operation.</span></span> <span data-ttu-id="110e8-118">If your operation returns this value, always use it (instead of Location) to track the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="110e8-118">If your operation returns this value, always use it (instead of Location) to track the status of the operation.</span></span>
* <span data-ttu-id="110e8-119">`Location` - URL for determining when an operation has completed.</span><span class="sxs-lookup"><span data-stu-id="110e8-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="110e8-120">Use this value only when Azure-AsyncOperation is not returned.</span><span class="sxs-lookup"><span data-stu-id="110e8-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="110e8-121">`Retry-After` - The number of seconds to wait before checking the status of the asynchronous operation.</span><span class="sxs-lookup"><span data-stu-id="110e8-121">`Retry-After` - The number of seconds to wait before checking the status of the asynchronous operation.</span></span>

<span data-ttu-id="110e8-122">However, not every asynchronous operation returns all these values.</span><span class="sxs-lookup"><span data-stu-id="110e8-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="110e8-123">For example, you may need to evaluate the Azure-AsyncOperation header value for one operation, and the Location header value for another operation.</span><span class="sxs-lookup"><span data-stu-id="110e8-123">For example, you may need to evaluate the Azure-AsyncOperation header value for one operation, and the Location header value for another operation.</span></span> 

<span data-ttu-id="110e8-124">You retrieve the header values as you would retrieve any header value for a request.</span><span class="sxs-lookup"><span data-stu-id="110e8-124">You retrieve the header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="110e8-125">For example, in C#, you retrieve the header value from an `HttpWebResponse` object named `response` with the following code:</span><span class="sxs-lookup"><span data-stu-id="110e8-125">For example, in C#, you retrieve the header value from an `HttpWebResponse` object named `response` with the following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="110e8-126">Azure-AsyncOperation request and response</span><span class="sxs-lookup"><span data-stu-id="110e8-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="110e8-127">To get the status of the asynchronous operation, send a GET request to the URL in Azure-AsyncOperation header value.</span><span class="sxs-lookup"><span data-stu-id="110e8-127">To get the status of the asynchronous operation, send a GET request to the URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="110e8-128">The body of the response from this operation contains information about the operation.</span><span class="sxs-lookup"><span data-stu-id="110e8-128">The body of the response from this operation contains information about the operation.</span></span> <span data-ttu-id="110e8-129">The following example shows the possible values returned from the operation:</span><span class="sxs-lookup"><span data-stu-id="110e8-129">The following example shows the possible values returned from the operation:</span></span>

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

<span data-ttu-id="110e8-130">Only `status` is returned for all responses.</span><span class="sxs-lookup"><span data-stu-id="110e8-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="110e8-131">The error object is returned when the status is Failed or Canceled.</span><span class="sxs-lookup"><span data-stu-id="110e8-131">The error object is returned when the status is Failed or Canceled.</span></span> <span data-ttu-id="110e8-132">All other values are optional; therefore, the response you receive may look different than the example.</span><span class="sxs-lookup"><span data-stu-id="110e8-132">All other values are optional; therefore, the response you receive may look different than the example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="110e8-133">provisioningState values</span><span class="sxs-lookup"><span data-stu-id="110e8-133">provisioningState values</span></span>

<span data-ttu-id="110e8-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span><span class="sxs-lookup"><span data-stu-id="110e8-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="110e8-135">When an operation has completed, one of following three values is returned:</span><span class="sxs-lookup"><span data-stu-id="110e8-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="110e8-136">Succeeded</span><span class="sxs-lookup"><span data-stu-id="110e8-136">Succeeded</span></span>
* <span data-ttu-id="110e8-137">Failed</span><span class="sxs-lookup"><span data-stu-id="110e8-137">Failed</span></span>
* <span data-ttu-id="110e8-138">Canceled</span><span class="sxs-lookup"><span data-stu-id="110e8-138">Canceled</span></span>

<span data-ttu-id="110e8-139">All other values indicate the operation is still running.</span><span class="sxs-lookup"><span data-stu-id="110e8-139">All other values indicate the operation is still running.</span></span> <span data-ttu-id="110e8-140">The resource provider can return a customized value that indicates its state.</span><span class="sxs-lookup"><span data-stu-id="110e8-140">The resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="110e8-141">For example, you may receive **Accepted** when the request is received and running.</span><span class="sxs-lookup"><span data-stu-id="110e8-141">For example, you may receive **Accepted** when the request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="110e8-142">Example requests and responses</span><span class="sxs-lookup"><span data-stu-id="110e8-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="110e8-143">Start virtual machine (202 with Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="110e8-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="110e8-144">This example shows how to determine the status of **start** operation for virtual machines.</span><span class="sxs-lookup"><span data-stu-id="110e8-144">This example shows how to determine the status of **start** operation for virtual machines.</span></span> <span data-ttu-id="110e8-145">The initial request is in the following format:</span><span class="sxs-lookup"><span data-stu-id="110e8-145">The initial request is in the following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="110e8-146">It returns status code 202.</span><span class="sxs-lookup"><span data-stu-id="110e8-146">It returns status code 202.</span></span> <span data-ttu-id="110e8-147">Among the header values, you see:</span><span class="sxs-lookup"><span data-stu-id="110e8-147">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="110e8-148">To check the status of the asynchronous operation, sending another request to that URL.</span><span class="sxs-lookup"><span data-stu-id="110e8-148">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="110e8-149">The response body contains the status of the operation:</span><span class="sxs-lookup"><span data-stu-id="110e8-149">The response body contains the status of the operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="110e8-150">Deploy resources (201 with Azure-AsyncOperation)</span><span class="sxs-lookup"><span data-stu-id="110e8-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="110e8-151">This example shows how to determine the status of **deployments** operation for deploying resources to Azure.</span><span class="sxs-lookup"><span data-stu-id="110e8-151">This example shows how to determine the status of **deployments** operation for deploying resources to Azure.</span></span> <span data-ttu-id="110e8-152">The initial request is in the following format:</span><span class="sxs-lookup"><span data-stu-id="110e8-152">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="110e8-153">It returns status code 201.</span><span class="sxs-lookup"><span data-stu-id="110e8-153">It returns status code 201.</span></span> <span data-ttu-id="110e8-154">The body of the response includes:</span><span class="sxs-lookup"><span data-stu-id="110e8-154">The body of the response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="110e8-155">Among the header values, you see:</span><span class="sxs-lookup"><span data-stu-id="110e8-155">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="110e8-156">To check the status of the asynchronous operation, sending another request to that URL.</span><span class="sxs-lookup"><span data-stu-id="110e8-156">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="110e8-157">The response body contains the status of the operation:</span><span class="sxs-lookup"><span data-stu-id="110e8-157">The response body contains the status of the operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="110e8-158">When the deployment is finished, the response contains:</span><span class="sxs-lookup"><span data-stu-id="110e8-158">When the deployment is finished, the response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="110e8-159">Create storage account (202 with Location and Retry-After)</span><span class="sxs-lookup"><span data-stu-id="110e8-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="110e8-160">This example shows how to determine the status of the **create** operation for storage accounts.</span><span class="sxs-lookup"><span data-stu-id="110e8-160">This example shows how to determine the status of the **create** operation for storage accounts.</span></span> <span data-ttu-id="110e8-161">The initial request is in the following format:</span><span class="sxs-lookup"><span data-stu-id="110e8-161">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="110e8-162">And the request body contains properties for the storage account:</span><span class="sxs-lookup"><span data-stu-id="110e8-162">And the request body contains properties for the storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="110e8-163">It returns status code 202.</span><span class="sxs-lookup"><span data-stu-id="110e8-163">It returns status code 202.</span></span> <span data-ttu-id="110e8-164">Among the header values, you see the following two values:</span><span class="sxs-lookup"><span data-stu-id="110e8-164">Among the header values, you see the following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="110e8-165">After waiting for number of seconds specified in Retry-After, check the status of the asynchronous operation by sending another request to that URL.</span><span class="sxs-lookup"><span data-stu-id="110e8-165">After waiting for number of seconds specified in Retry-After, check the status of the asynchronous operation by sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="110e8-166">If the request is still running, you receive a status code 202.</span><span class="sxs-lookup"><span data-stu-id="110e8-166">If the request is still running, you receive a status code 202.</span></span> <span data-ttu-id="110e8-167">If the request has completed, your receive a status code 200, and the body of the response contains the properties of the storage account that has been created.</span><span class="sxs-lookup"><span data-stu-id="110e8-167">If the request has completed, your receive a status code 200, and the body of the response contains the properties of the storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="110e8-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="110e8-168">Next steps</span></span>

* <span data-ttu-id="110e8-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="110e8-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="110e8-170">For information about managing resources through the Resource Manager REST API, see [Using the Resource Manager REST API](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="110e8-170">For information about managing resources through the Resource Manager REST API, see [Using the Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="110e8-171">for information about deploying templates through the Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="110e8-171">for information about deploying templates through the Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>