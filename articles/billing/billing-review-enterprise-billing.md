---
title: Review Azure enterprise enrollment billing data with REST API | Microsoft Docs
description: Learn how to use Azure REST APIs to review enterprise enrollment billing information.
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
ms.openlocfilehash: 71143549916fc7440d5f21bcb03f1f795ddc73ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869715"
---
# <a name="review-enterprise-enrollment-billing-using-rest-apis"></a><span data-ttu-id="52302-103">Review enterprise enrollment billing using REST APIs</span><span class="sxs-lookup"><span data-stu-id="52302-103">Review enterprise enrollment billing using REST APIs</span></span>

<span data-ttu-id="52302-104">Azure Reporting APIs help you review and manage your Azure costs.</span><span class="sxs-lookup"><span data-stu-id="52302-104">Azure Reporting APIs help you review and manage your Azure costs.</span></span>

<span data-ttu-id="52302-105">In this article, you learn to retrieve the billing information associated with billing accounts, department, or enterprtise agreement (EA) enrollment accounts using the Azure REST APIs.</span><span class="sxs-lookup"><span data-stu-id="52302-105">In this article, you learn to retrieve the billing information associated with billing accounts, department, or enterprtise agreement (EA) enrollment accounts using the Azure REST APIs.</span></span> 

## <a name="individual-account-billing"></a><span data-ttu-id="52302-106">Individual account billing</span><span class="sxs-lookup"><span data-stu-id="52302-106">Individual account billing</span></span>

<span data-ttu-id="52302-107">To get usage details for accounts in a department:</span><span class="sxs-lookup"><span data-stu-id="52302-107">To get usage details for accounts in a department:</span></span>

```http
GET https://management.azure.com/providers/Microsoft.Billing/billingAccounts/{billingAccountId}/providers/Microsoft.Consumption/usageDetails?api-version=2018-06-30
Content-Type: application/json   
Authorization: Bearer
```

<span data-ttu-id="52302-108">The `{billingAccountId}` parameter is required and should contain the ID for the account.</span><span class="sxs-lookup"><span data-stu-id="52302-108">The `{billingAccountId}` parameter is required and should contain the ID for the account.</span></span>

<span data-ttu-id="52302-109">The following headers are required:</span><span class="sxs-lookup"><span data-stu-id="52302-109">The following headers are required:</span></span> 

|<span data-ttu-id="52302-110">Request header</span><span class="sxs-lookup"><span data-stu-id="52302-110">Request header</span></span>|<span data-ttu-id="52302-111">Description</span><span class="sxs-lookup"><span data-stu-id="52302-111">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="52302-112">*Content-Type:*</span><span class="sxs-lookup"><span data-stu-id="52302-112">*Content-Type:*</span></span>|<span data-ttu-id="52302-113">Required.</span><span class="sxs-lookup"><span data-stu-id="52302-113">Required.</span></span> <span data-ttu-id="52302-114">Set to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="52302-114">Set to `application/json`.</span></span>|  
|<span data-ttu-id="52302-115">*Authorization:*</span><span class="sxs-lookup"><span data-stu-id="52302-115">*Authorization:*</span></span>|<span data-ttu-id="52302-116">Required.</span><span class="sxs-lookup"><span data-stu-id="52302-116">Required.</span></span> <span data-ttu-id="52302-117">Set to a valid `Bearer` [API key](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based).</span><span class="sxs-lookup"><span data-stu-id="52302-117">Set to a valid `Bearer` [API key](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based).</span></span> |  

<span data-ttu-id="52302-118">This example shows a synchronous call that returns details for the current billing cycle.</span><span class="sxs-lookup"><span data-stu-id="52302-118">This example shows a synchronous call that returns details for the current billing cycle.</span></span> <span data-ttu-id="52302-119">For performance reasons, synchronous calls return information for the last month.</span><span class="sxs-lookup"><span data-stu-id="52302-119">For performance reasons, synchronous calls return information for the last month.</span></span>  <span data-ttu-id="52302-120">You can also call the [API asynchronously](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based) to return data for 36 months.</span><span class="sxs-lookup"><span data-stu-id="52302-120">You can also call the [API asynchronously](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based) to return data for 36 months.</span></span>


## <a name="response"></a><span data-ttu-id="52302-121">Response</span><span class="sxs-lookup"><span data-stu-id="52302-121">Response</span></span>  

<span data-ttu-id="52302-122">Status code 200 (OK) is returned for a successful response, which contains a list of detailed costs for the account.</span><span class="sxs-lookup"><span data-stu-id="52302-122">Status code 200 (OK) is returned for a successful response, which contains a list of detailed costs for the account.</span></span>

```json
{
  "value": [
    {
      "id": "/providers/Microsoft.Billing/BillingAccounts/1234/providers/Microsoft.Billing/billingPeriods/201702/providers/Microsoft.Consumption/usageDetails/usageDetailsId1",
      "name": "usageDetailsId1",
      "type": "Microsoft.Consumption/usageDetails",
      "properties": {
        ...
        "usageStart": "2017-02-13T00:00:00Z",
        "usageEnd": "2017-02-13T23:59:59Z",
        "instanceName": "shared1",
        "instanceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-Web-eastasia/providers/Microsoft.Web/sites/shared1",
        "currency": "USD",
        "usageQuantity": 0.00328,
        "billableQuantity": 0.00328,
        "pretaxCost": 0.67,
        "isEstimated": false,
        ...
      }
    }
  ]
}
```  

<span data-ttu-id="52302-123">This example is abbreviated; see [Get usage detail for a billing account](/rest/api/consumption/usagedetails/listbybillingaccount) for a complete description of each response field and error handling.</span><span class="sxs-lookup"><span data-stu-id="52302-123">This example is abbreviated; see [Get usage detail for a billing account](/rest/api/consumption/usagedetails/listbybillingaccount) for a complete description of each response field and error handling.</span></span>

## <a name="department-billing"></a><span data-ttu-id="52302-124">Department billing</span><span class="sxs-lookup"><span data-stu-id="52302-124">Department billing</span></span> 

<span data-ttu-id="52302-125">Get usage details aggregated for all accounts in a department.</span><span class="sxs-lookup"><span data-stu-id="52302-125">Get usage details aggregated for all accounts in a department.</span></span> 

```http
GET https://management.azure.com/providers/Microsoft.Billing/departments/{departmentId}/providers/Microsoft.Consumption/usageDetails?api-version=2018-06-30
Content-Type: application/json   
Authorization: Bearer
```

<span data-ttu-id="52302-126">The `{departmentId}` parameter is required and should contain the ID for the department in the enrollment account.</span><span class="sxs-lookup"><span data-stu-id="52302-126">The `{departmentId}` parameter is required and should contain the ID for the department in the enrollment account.</span></span>

<span data-ttu-id="52302-127">The following headers are required:</span><span class="sxs-lookup"><span data-stu-id="52302-127">The following headers are required:</span></span> 

|<span data-ttu-id="52302-128">Request header</span><span class="sxs-lookup"><span data-stu-id="52302-128">Request header</span></span>|<span data-ttu-id="52302-129">Description</span><span class="sxs-lookup"><span data-stu-id="52302-129">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="52302-130">*Content-Type:*</span><span class="sxs-lookup"><span data-stu-id="52302-130">*Content-Type:*</span></span>|<span data-ttu-id="52302-131">Required.</span><span class="sxs-lookup"><span data-stu-id="52302-131">Required.</span></span> <span data-ttu-id="52302-132">Set to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="52302-132">Set to `application/json`.</span></span>|  
|<span data-ttu-id="52302-133">*Authorization:*</span><span class="sxs-lookup"><span data-stu-id="52302-133">*Authorization:*</span></span>|<span data-ttu-id="52302-134">Required.</span><span class="sxs-lookup"><span data-stu-id="52302-134">Required.</span></span> <span data-ttu-id="52302-135">Set to a valid `Bearer` [API key](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based).</span><span class="sxs-lookup"><span data-stu-id="52302-135">Set to a valid `Bearer` [API key](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based).</span></span> |  

<span data-ttu-id="52302-136">This example shows a synchronous call that returns details for the current billing cycle.</span><span class="sxs-lookup"><span data-stu-id="52302-136">This example shows a synchronous call that returns details for the current billing cycle.</span></span> <span data-ttu-id="52302-137">For performance reasons, synchronous calls return information for the last month.</span><span class="sxs-lookup"><span data-stu-id="52302-137">For performance reasons, synchronous calls return information for the last month.</span></span>  <span data-ttu-id="52302-138">You can also call the [API asynchronously](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based) to return data for 36 months.</span><span class="sxs-lookup"><span data-stu-id="52302-138">You can also call the [API asynchronously](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based) to return data for 36 months.</span></span>

### <a name="response"></a><span data-ttu-id="52302-139">Response</span><span class="sxs-lookup"><span data-stu-id="52302-139">Response</span></span>  

<span data-ttu-id="52302-140">Status code 200 (OK) is returned for a successful response, which contains a list of detailed usage information and costs for a given billing period and invoice ID for the department.</span><span class="sxs-lookup"><span data-stu-id="52302-140">Status code 200 (OK) is returned for a successful response, which contains a list of detailed usage information and costs for a given billing period and invoice ID for the department.</span></span>


<span data-ttu-id="52302-141">The following example shows the output of the REST API for department `1234`.</span><span class="sxs-lookup"><span data-stu-id="52302-141">The following example shows the output of the REST API for department `1234`.</span></span>

```json
{
  "value": [
    {
      "id": "/providers/Microsoft.Billing/Departments/1234/providers/Microsoft.Billing/billingPeriods/201702/providers/Microsoft.Consumption/usageDetails/usageDetailsId1",
      "name": "usageDetailsId1",
      "type": "Microsoft.Consumption/usageDetails",
      "properties": {
        "billingPeriodId": "/providers/Microsoft.Billing/Departments/1234/providers/Microsoft.Billing/billingPeriods/201702",
        "invoiceId": "/providers/Microsoft.Billing/Departments/1234/providers/Microsoft.Billing/invoices/201703-123456789",
        "usageStart": "2017-02-13T00:00:00Z",
        "usageEnd": "2017-02-13T23:59:59Z",
        "instanceName": "shared1",
        "instanceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-Web-eastasia/providers/Microsoft.Web/sites/shared1",
        "instanceLocation": "eastasia",
        "currency": "USD",
        "usageQuantity": 0.00328,
        "billableQuantity": 0.00328,
        "pretaxCost": 0.67,
        ...
      }
    }
  ]
}
```  

<span data-ttu-id="52302-142">This example is abbreviated; see [Get usage detail for a department](/rest/api/consumption/usagedetails/listbydepartment) for a complete description of each response field and error handling.</span><span class="sxs-lookup"><span data-stu-id="52302-142">This example is abbreviated; see [Get usage detail for a department](/rest/api/consumption/usagedetails/listbydepartment) for a complete description of each response field and error handling.</span></span>

## <a name="enrollment-account-billing"></a><span data-ttu-id="52302-143">Enrollment account billing</span><span class="sxs-lookup"><span data-stu-id="52302-143">Enrollment account billing</span></span>

<span data-ttu-id="52302-144">Get usage details aggregated for the enrollment account.</span><span class="sxs-lookup"><span data-stu-id="52302-144">Get usage details aggregated for the enrollment account.</span></span>

```http
GET GET https://management.azure.com/providers/Microsoft.Billing/enrollmentAccounts/{enrollmentAccountId}/providers/Microsoft.Consumption/usageDetails?api-version=2018-06-30
Content-Type: application/json   
Authorization: Bearer
```

<span data-ttu-id="52302-145">The `{enrollmentAccountId}` parameter is required and should contain the ID for the enrollment account.</span><span class="sxs-lookup"><span data-stu-id="52302-145">The `{enrollmentAccountId}` parameter is required and should contain the ID for the enrollment account.</span></span>

<span data-ttu-id="52302-146">The following headers are required:</span><span class="sxs-lookup"><span data-stu-id="52302-146">The following headers are required:</span></span> 

|<span data-ttu-id="52302-147">Request header</span><span class="sxs-lookup"><span data-stu-id="52302-147">Request header</span></span>|<span data-ttu-id="52302-148">Description</span><span class="sxs-lookup"><span data-stu-id="52302-148">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="52302-149">*Content-Type:*</span><span class="sxs-lookup"><span data-stu-id="52302-149">*Content-Type:*</span></span>|<span data-ttu-id="52302-150">Required.</span><span class="sxs-lookup"><span data-stu-id="52302-150">Required.</span></span> <span data-ttu-id="52302-151">Set to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="52302-151">Set to `application/json`.</span></span>|  
|<span data-ttu-id="52302-152">*Authorization:*</span><span class="sxs-lookup"><span data-stu-id="52302-152">*Authorization:*</span></span>|<span data-ttu-id="52302-153">Required.</span><span class="sxs-lookup"><span data-stu-id="52302-153">Required.</span></span> <span data-ttu-id="52302-154">Set to a valid `Bearer` [API key](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based).</span><span class="sxs-lookup"><span data-stu-id="52302-154">Set to a valid `Bearer` [API key](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based).</span></span> |  

<span data-ttu-id="52302-155">This example shows a synchronous call that returns details for the current billing cycle.</span><span class="sxs-lookup"><span data-stu-id="52302-155">This example shows a synchronous call that returns details for the current billing cycle.</span></span> <span data-ttu-id="52302-156">For performance reasons, synchronous calls return information for the last month.</span><span class="sxs-lookup"><span data-stu-id="52302-156">For performance reasons, synchronous calls return information for the last month.</span></span>  <span data-ttu-id="52302-157">You can also call the [API asynchronously](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based) to return data for 36 months.</span><span class="sxs-lookup"><span data-stu-id="52302-157">You can also call the [API asynchronously](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail#asynchronous-call-polling-based) to return data for 36 months.</span></span>

### <a name="response"></a><span data-ttu-id="52302-158">Response</span><span class="sxs-lookup"><span data-stu-id="52302-158">Response</span></span>  

<span data-ttu-id="52302-159">Status code 200 (OK) is returned for a successful response, which contains a list of detailed usage information and costs for a given billing period and invoice ID for the department.</span><span class="sxs-lookup"><span data-stu-id="52302-159">Status code 200 (OK) is returned for a successful response, which contains a list of detailed usage information and costs for a given billing period and invoice ID for the department.</span></span>

<span data-ttu-id="52302-160">The following example shows the output of the REST API for enterprise enrollment `1234`.</span><span class="sxs-lookup"><span data-stu-id="52302-160">The following example shows the output of the REST API for enterprise enrollment `1234`.</span></span>

```json
{
  "value": [
    {
      "id": "/providers/Microsoft.Billing/EnrollmentAccounts/1234/providers/Microsoft.Billing/billingPeriods/201702/providers/Microsoft.Consumption/usageDetails/usageDetailsId1",
      "name": "usageDetailsId1",
      "type": "Microsoft.Consumption/usageDetails",
      "properties": {
        "billingPeriodId": "/providers/Microsoft.Billing/EnrollmentAccounts/1234/providers/Microsoft.Billing/billingPeriods/201702",
        "invoiceId": "/providers/Microsoft.Billing/EnrollmentAccounts/1234/providers/Microsoft.Billing/invoices/201703-123456789",
        "usageStart": "2017-02-13T00:00:00Z",
        "usageEnd": "2017-02-13T23:59:59Z",
        ....
        "currency": "USD",
        "usageQuantity": 0.00328,
        "billableQuantity": 0.00328,
        "pretaxCost": 0.67,
        ...
      }
    }
  ]
}
``` 

<span data-ttu-id="52302-161">This example is abbreviated; see [Get usage detail for an enrollment account](/rest/api/consumption/usagedetails/listbyenrollmentaccount) for a complete description of each response field and error handling.</span><span class="sxs-lookup"><span data-stu-id="52302-161">This example is abbreviated; see [Get usage detail for an enrollment account](/rest/api/consumption/usagedetails/listbyenrollmentaccount) for a complete description of each response field and error handling.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52302-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="52302-162">Next steps</span></span> 
- <span data-ttu-id="52302-163">Review [Enterprise reporting overview](https://docs.microsoft.com/azure/billing/billing-enterprise-api)</span><span class="sxs-lookup"><span data-stu-id="52302-163">Review [Enterprise reporting overview](https://docs.microsoft.com/azure/billing/billing-enterprise-api)</span></span>
- <span data-ttu-id="52302-164">Investigate [Enterprise Billing REST API](https://docs.microsoft.com/rest/api/billing/)</span><span class="sxs-lookup"><span data-stu-id="52302-164">Investigate [Enterprise Billing REST API](https://docs.microsoft.com/rest/api/billing/)</span></span>   
- [<span data-ttu-id="52302-165">Get started with Azure REST API</span><span class="sxs-lookup"><span data-stu-id="52302-165">Get started with Azure REST API</span></span>](https://docs.microsoft.com/rest/api/azure/)   
