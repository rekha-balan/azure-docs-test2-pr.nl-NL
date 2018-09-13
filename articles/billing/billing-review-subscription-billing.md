---
title: Review Azure subscription billing data with REST API | Microsoft Docs
description: Learn how to use Azure REST APIs to review subscription billing details.
services: billing
documentationcenter: na
author: lleonard-msft
manager: MBaldwin
editor: ''
ms.assetid: 82D50B98-40F2-44B1-A445-4391EA9EBBAA
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2018
ms.author: alleonar
ms.openlocfilehash: cc29d1f613af67604d50654be794cc90080098bb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968679"
---
# <a name="review-subscription-billing-using-rest-apis"></a><span data-ttu-id="718c7-103">Review subscription billing using REST APIs</span><span class="sxs-lookup"><span data-stu-id="718c7-103">Review subscription billing using REST APIs</span></span>

<span data-ttu-id="718c7-104">Azure Reporting APIs help you review and manage your Azure costs.</span><span class="sxs-lookup"><span data-stu-id="718c7-104">Azure Reporting APIs help you review and manage your Azure costs.</span></span>  

<span data-ttu-id="718c7-105">Filters help customize results to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="718c7-105">Filters help customize results to meet your needs.</span></span>

<span data-ttu-id="718c7-106">Here, you learn to use a REST API to return subscription billing details for a given date range.</span><span class="sxs-lookup"><span data-stu-id="718c7-106">Here, you learn to use a REST API to return subscription billing details for a given date range.</span></span>

``` http
GET https://management.azure.com/subscriptions/${subscriptionID}/providers/Microsoft.Billing/billingPeriods/${billingPeriod}/providers/Microsoft.Consumption/usageDetails?$filter=properties/usageEnd ge '${startDate}' AND properties/usageEnd le '${endDate}'
Content-Type: application/json   
Authorization: Bearer
```

## <a name="build-the-request"></a><span data-ttu-id="718c7-107">Build the request</span><span class="sxs-lookup"><span data-stu-id="718c7-107">Build the request</span></span>  

<span data-ttu-id="718c7-108">The `{subscriptionID}` parameter is required and identifies the target subscription.</span><span class="sxs-lookup"><span data-stu-id="718c7-108">The `{subscriptionID}` parameter is required and identifies the target subscription.</span></span>

<span data-ttu-id="718c7-109">The `{billingPeriod}` parameter is required and specifies a current [billing period](https://docs.microsoft.com/rest/api/billing/billingperiods/get#billingperiod).</span><span class="sxs-lookup"><span data-stu-id="718c7-109">The `{billingPeriod}` parameter is required and specifies a current [billing period](https://docs.microsoft.com/rest/api/billing/billingperiods/get#billingperiod).</span></span>

<span data-ttu-id="718c7-110">The `${startDate}` and `${endDate}` parameters are required for this example, but optional for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="718c7-110">The `${startDate}` and `${endDate}` parameters are required for this example, but optional for the endpoint.</span></span>  <span data-ttu-id="718c7-111">They specify the date range as strings in the form of YYYY-MM-DD (examples: `'20180501'` and `'20180615'`).</span><span class="sxs-lookup"><span data-stu-id="718c7-111">They specify the date range as strings in the form of YYYY-MM-DD (examples: `'20180501'` and `'20180615'`).</span></span> 

<span data-ttu-id="718c7-112">The following headers are required:</span><span class="sxs-lookup"><span data-stu-id="718c7-112">The following headers are required:</span></span> 

|<span data-ttu-id="718c7-113">Request header</span><span class="sxs-lookup"><span data-stu-id="718c7-113">Request header</span></span>|<span data-ttu-id="718c7-114">Description</span><span class="sxs-lookup"><span data-stu-id="718c7-114">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="718c7-115">*Content-Type:*</span><span class="sxs-lookup"><span data-stu-id="718c7-115">*Content-Type:*</span></span>|<span data-ttu-id="718c7-116">Required.</span><span class="sxs-lookup"><span data-stu-id="718c7-116">Required.</span></span> <span data-ttu-id="718c7-117">Set to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="718c7-117">Set to `application/json`.</span></span>|  
|<span data-ttu-id="718c7-118">*Authorization:*</span><span class="sxs-lookup"><span data-stu-id="718c7-118">*Authorization:*</span></span>|<span data-ttu-id="718c7-119">Required.</span><span class="sxs-lookup"><span data-stu-id="718c7-119">Required.</span></span> <span data-ttu-id="718c7-120">Set to a valid `Bearer` [access token](https://docs.microsoft.com/rest/api/azure/#authorization-code-grant-interactive-clients).</span><span class="sxs-lookup"><span data-stu-id="718c7-120">Set to a valid `Bearer` [access token](https://docs.microsoft.com/rest/api/azure/#authorization-code-grant-interactive-clients).</span></span> |  

## <a name="response"></a><span data-ttu-id="718c7-121">Response</span><span class="sxs-lookup"><span data-stu-id="718c7-121">Response</span></span>  

<span data-ttu-id="718c7-122">Status code 200 (OK) is returned for a successful response, which contains a list of detailed costs for your account.</span><span class="sxs-lookup"><span data-stu-id="718c7-122">Status code 200 (OK) is returned for a successful response, which contains a list of detailed costs for your account.</span></span>

``` json
{
  "value": [
    {
      "id": "/subscriptions/{$subscriptionID}/providers/Microsoft.Billing/billingPeriods/201702/providers/Microsoft.Consumption/usageDetails/{$detailsID}",
      "name": "{$detailsID}",
      "type": "Microsoft.Consumption/usageDetails",
      "properties": {
        "billingPeriodId": "/subscriptions/${subscriptionID}/providers/Microsoft.Billing/billingPeriods/${billingPeriod}",
        "invoiceId": "/subscriptions/${subscriptionID}/providers/Microsoft.Billing/invoices/${invoiceID}",
        "usageStart": "${startDate}}",
        "usageEnd": "${endDate}",
        "currency": "USD",
        "usageQuantity": ${usageQuantity},
        "billableQuantity": ${billableQuantity},
        "pretaxCost": ${cost},
        "meterId": "${meterID}",
        "meterDetails": ${meterDetails}
      }
    }
    ],
    "nextLink": "${nextLinkURL}"
} 
```  

<span data-ttu-id="718c7-123">Each item in **value** represents a details regarding the use of a service:</span><span class="sxs-lookup"><span data-stu-id="718c7-123">Each item in **value** represents a details regarding the use of a service:</span></span>

|<span data-ttu-id="718c7-124">Response property</span><span class="sxs-lookup"><span data-stu-id="718c7-124">Response property</span></span>|<span data-ttu-id="718c7-125">Description</span><span class="sxs-lookup"><span data-stu-id="718c7-125">Description</span></span>|
|----------------|----------|
|<span data-ttu-id="718c7-126">**subscriptionGuid**</span><span class="sxs-lookup"><span data-stu-id="718c7-126">**subscriptionGuid**</span></span> | <span data-ttu-id="718c7-127">Globally unique ID for the subscription.</span><span class="sxs-lookup"><span data-stu-id="718c7-127">Globally unique ID for the subscription.</span></span> | 
|<span data-ttu-id="718c7-128">**startDate**</span><span class="sxs-lookup"><span data-stu-id="718c7-128">**startDate**</span></span> | <span data-ttu-id="718c7-129">Date the use started.</span><span class="sxs-lookup"><span data-stu-id="718c7-129">Date the use started.</span></span> |
|<span data-ttu-id="718c7-130">**endDate**</span><span class="sxs-lookup"><span data-stu-id="718c7-130">**endDate**</span></span> | <span data-ttu-id="718c7-131">Date the use ended.</span><span class="sxs-lookup"><span data-stu-id="718c7-131">Date the use ended.</span></span> |
|<span data-ttu-id="718c7-132">**useageQuantity**</span><span class="sxs-lookup"><span data-stu-id="718c7-132">**useageQuantity**</span></span> | <span data-ttu-id="718c7-133">Quantity used.</span><span class="sxs-lookup"><span data-stu-id="718c7-133">Quantity used.</span></span> | 
|<span data-ttu-id="718c7-134">**billableQuantity**</span><span class="sxs-lookup"><span data-stu-id="718c7-134">**billableQuantity**</span></span> | <span data-ttu-id="718c7-135">Quantity actually billed.</span><span class="sxs-lookup"><span data-stu-id="718c7-135">Quantity actually billed.</span></span> |
|<span data-ttu-id="718c7-136">**pretaxCost**</span><span class="sxs-lookup"><span data-stu-id="718c7-136">**pretaxCost**</span></span> | <span data-ttu-id="718c7-137">Cost invoiced, before applicable taxes.</span><span class="sxs-lookup"><span data-stu-id="718c7-137">Cost invoiced, before applicable taxes.</span></span> | 
|<span data-ttu-id="718c7-138">**meterDetails**</span><span class="sxs-lookup"><span data-stu-id="718c7-138">**meterDetails**</span></span> | <span data-ttu-id="718c7-139">Detailed information about the use.</span><span class="sxs-lookup"><span data-stu-id="718c7-139">Detailed information about the use.</span></span> |
|<span data-ttu-id="718c7-140">**nextLink**</span><span class="sxs-lookup"><span data-stu-id="718c7-140">**nextLink**</span></span>| <span data-ttu-id="718c7-141">When set, specifies a URL for the next "page" of details.</span><span class="sxs-lookup"><span data-stu-id="718c7-141">When set, specifies a URL for the next "page" of details.</span></span> <span data-ttu-id="718c7-142">Blank when the page is the last one.</span><span class="sxs-lookup"><span data-stu-id="718c7-142">Blank when the page is the last one.</span></span> |  
||
  
<span data-ttu-id="718c7-143">This example is abbreviated; see [List usage details](https://docs.microsoft.com/rest/api/consumption/usagedetails/listbybillingperiod#usagedetailslistresult) for a complete description of each response field.</span><span class="sxs-lookup"><span data-stu-id="718c7-143">This example is abbreviated; see [List usage details](https://docs.microsoft.com/rest/api/consumption/usagedetails/listbybillingperiod#usagedetailslistresult) for a complete description of each response field.</span></span> 

<span data-ttu-id="718c7-144">Other status codes indicate error conditions.</span><span class="sxs-lookup"><span data-stu-id="718c7-144">Other status codes indicate error conditions.</span></span> <span data-ttu-id="718c7-145">In these cases, the response object explains why the request failed.</span><span class="sxs-lookup"><span data-stu-id="718c7-145">In these cases, the response object explains why the request failed.</span></span>

``` json
{  
  "error": [  
    { "code": "Error type." 
      "message": "Error response describing why the operation failed."  
    }  
  ]  
}  
```  

## <a name="next-steps"></a><span data-ttu-id="718c7-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="718c7-146">Next steps</span></span> 
- <span data-ttu-id="718c7-147">Review [Enterprise reporting overview](https://docs.microsoft.com/azure/billing/billing-enterprise-api)</span><span class="sxs-lookup"><span data-stu-id="718c7-147">Review [Enterprise reporting overview](https://docs.microsoft.com/azure/billing/billing-enterprise-api)</span></span>
- <span data-ttu-id="718c7-148">Investigate [Enterprise Billing REST API](https://docs.microsoft.com/rest/api/billing/)</span><span class="sxs-lookup"><span data-stu-id="718c7-148">Investigate [Enterprise Billing REST API](https://docs.microsoft.com/rest/api/billing/)</span></span>   
- [<span data-ttu-id="718c7-149">Get started with Azure REST API</span><span class="sxs-lookup"><span data-stu-id="718c7-149">Get started with Azure REST API</span></span>](https://docs.microsoft.com/rest/api/azure/)   
