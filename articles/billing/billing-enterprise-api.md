---
title: Azure Billing Enterprise APIs | Microsoft Docs
description: Learn about the Reporting APIs that enable Enterprise Azure customers to pull consumption data programmatically.
services: ''
documentationcenter: ''
author: anandedwin
manager: aedwin
editor: ''
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: b67e6202c470be46b3100c06e503c05415371c6e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867138"
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="e8cbf-103">Overview of Reporting APIs for Enterprise customers</span><span class="sxs-lookup"><span data-stu-id="e8cbf-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="e8cbf-104">The Reporting APIs enable Enterprise Azure customers to programmatically pull consumption and billing data into preferred data analysis tools.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-104">The Reporting APIs enable Enterprise Azure customers to programmatically pull consumption and billing data into preferred data analysis tools.</span></span> <span data-ttu-id="e8cbf-105">Enterprise customers have signed an [Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/) with Azure to make negotiated monetary commitments and gain access to custom pricing for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-105">Enterprise customers have signed an [Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/) with Azure to make negotiated monetary commitments and gain access to custom pricing for Azure resources.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e8cbf-106">Help improve Azure billing docs</span><span class="sxs-lookup"><span data-stu-id="e8cbf-106">Help improve Azure billing docs</span></span>](https://go.microsoft.com/fwlink/p/?linkid=2010091)

## <a name="enabling-data-access-to-the-api"></a><span data-ttu-id="e8cbf-107">Enabling data access to the API</span><span class="sxs-lookup"><span data-stu-id="e8cbf-107">Enabling data access to the API</span></span>
* <span data-ttu-id="e8cbf-108">**Generate or retrieve the API key** - Log in to the Enterprise portal, and navigate to Reports > Download Usage > API Access Key to generate or retrieve the API key.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-108">**Generate or retrieve the API key** - Log in to the Enterprise portal, and navigate to Reports > Download Usage > API Access Key to generate or retrieve the API key.</span></span>
* <span data-ttu-id="e8cbf-109">**Passing keys in the API** - The API key needs to be passed for each call for Authentication and Authorization.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-109">**Passing keys in the API** - The API key needs to be passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="e8cbf-110">The following property needs to be to the HTTP headers</span><span class="sxs-lookup"><span data-stu-id="e8cbf-110">The following property needs to be to the HTTP headers</span></span>

|<span data-ttu-id="e8cbf-111">Request Header Key</span><span class="sxs-lookup"><span data-stu-id="e8cbf-111">Request Header Key</span></span> | <span data-ttu-id="e8cbf-112">Value</span><span class="sxs-lookup"><span data-stu-id="e8cbf-112">Value</span></span>|
|-|-|
|<span data-ttu-id="e8cbf-113">Authorization</span><span class="sxs-lookup"><span data-stu-id="e8cbf-113">Authorization</span></span>| <span data-ttu-id="e8cbf-114">Specify the value in this format: **bearer {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="e8cbf-114">Specify the value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="e8cbf-115">Example: bearer eyr....09</span><span class="sxs-lookup"><span data-stu-id="e8cbf-115">Example: bearer eyr....09</span></span>| 

## <a name="consumption-apis"></a><span data-ttu-id="e8cbf-116">Consumption APIs</span><span class="sxs-lookup"><span data-stu-id="e8cbf-116">Consumption APIs</span></span>
<span data-ttu-id="e8cbf-117">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for the APIs described below which should enable easy introspection of the API and the ability to generate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="e8cbf-117">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for the APIs described below which should enable easy introspection of the API and the ability to generate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="e8cbf-118">Data beginning May 1, 2014 is available through this API.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-118">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="e8cbf-119">**Balance and Summary** - The [Balance and Summary API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-balance-summary) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-119">**Balance and Summary** - The [Balance and Summary API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-balance-summary) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="e8cbf-120">**Usage Details** - The [Usage Detail API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-120">**Usage Details** - The [Usage Detail API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-usage-detail) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="e8cbf-121">The result also includes information on instances, meters and departments.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-121">The result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="e8cbf-122">The API can be queried by Billing period or by a specified start and end date.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-122">The API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="e8cbf-123">**Marketplace Store Charge** - The [Marketplace Store Charge API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-marketplace-storecharge) returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span><span class="sxs-lookup"><span data-stu-id="e8cbf-123">**Marketplace Store Charge** - The [Marketplace Store Charge API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-marketplace-storecharge) returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="e8cbf-124">**Price Sheet** - The [Price Sheet API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-pricesheet) provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-124">**Price Sheet** - The [Price Sheet API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-pricesheet) provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span> 

## <a name="data-freshness"></a><span data-ttu-id="e8cbf-125">Data Freshness</span><span class="sxs-lookup"><span data-stu-id="e8cbf-125">Data Freshness</span></span>
<span data-ttu-id="e8cbf-126">Etags will be returned in the response of all the above API.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-126">Etags will be returned in the response of all the above API.</span></span> <span data-ttu-id="e8cbf-127">A change in Etag indicates the data has been refreshed.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-127">A change in Etag indicates the data has been refreshed.</span></span>  <span data-ttu-id="e8cbf-128">In subsequent calls to the same API using the same parameters, pass the captured Etag with the key “If-None-Match” in the header of http request.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-128">In subsequent calls to the same API using the same parameters, pass the captured Etag with the key “If-None-Match” in the header of http request.</span></span> <span data-ttu-id="e8cbf-129">The response status code would be "NotModified" if the data has not been refreshed any further and no data will be returned.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-129">The response status code would be "NotModified" if the data has not been refreshed any further and no data will be returned.</span></span> <span data-ttu-id="e8cbf-130">API will return the full dataset for the required period whenever there is an etag change.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-130">API will return the full dataset for the required period whenever there is an etag change.</span></span>

## <a name="helper-apis"></a><span data-ttu-id="e8cbf-131">Helper APIs</span><span class="sxs-lookup"><span data-stu-id="e8cbf-131">Helper APIs</span></span>
 <span data-ttu-id="e8cbf-132">**List Billing Periods** - The [Billing Periods API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-billing-periods) returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-132">**List Billing Periods** - The [Billing Periods API](https://docs.microsoft.com/rest/api/billing/enterprise/billing-enterprise-api-billing-periods) returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="e8cbf-133">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-133">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="e8cbf-134">API Response Codes</span><span class="sxs-lookup"><span data-stu-id="e8cbf-134">API Response Codes</span></span>   
|<span data-ttu-id="e8cbf-135">Response Status Code</span><span class="sxs-lookup"><span data-stu-id="e8cbf-135">Response Status Code</span></span>|<span data-ttu-id="e8cbf-136">Message</span><span class="sxs-lookup"><span data-stu-id="e8cbf-136">Message</span></span>|<span data-ttu-id="e8cbf-137">Description</span><span class="sxs-lookup"><span data-stu-id="e8cbf-137">Description</span></span>|
|-|-|-|
|<span data-ttu-id="e8cbf-138">200</span><span class="sxs-lookup"><span data-stu-id="e8cbf-138">200</span></span>| <span data-ttu-id="e8cbf-139">OK</span><span class="sxs-lookup"><span data-stu-id="e8cbf-139">OK</span></span>|<span data-ttu-id="e8cbf-140">No error</span><span class="sxs-lookup"><span data-stu-id="e8cbf-140">No error</span></span>|
|<span data-ttu-id="e8cbf-141">401</span><span class="sxs-lookup"><span data-stu-id="e8cbf-141">401</span></span>| <span data-ttu-id="e8cbf-142">Unauthorized</span><span class="sxs-lookup"><span data-stu-id="e8cbf-142">Unauthorized</span></span>| <span data-ttu-id="e8cbf-143">API Key not found, Invalid, Expired etc.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-143">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="e8cbf-144">404</span><span class="sxs-lookup"><span data-stu-id="e8cbf-144">404</span></span>| <span data-ttu-id="e8cbf-145">Unavailable</span><span class="sxs-lookup"><span data-stu-id="e8cbf-145">Unavailable</span></span>| <span data-ttu-id="e8cbf-146">Report endpoint not found</span><span class="sxs-lookup"><span data-stu-id="e8cbf-146">Report endpoint not found</span></span>|
|<span data-ttu-id="e8cbf-147">400</span><span class="sxs-lookup"><span data-stu-id="e8cbf-147">400</span></span>| <span data-ttu-id="e8cbf-148">Bad Request</span><span class="sxs-lookup"><span data-stu-id="e8cbf-148">Bad Request</span></span>| <span data-ttu-id="e8cbf-149">Invalid params – Date ranges, EA numbers etc.</span><span class="sxs-lookup"><span data-stu-id="e8cbf-149">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="e8cbf-150">500</span><span class="sxs-lookup"><span data-stu-id="e8cbf-150">500</span></span>| <span data-ttu-id="e8cbf-151">Server Error</span><span class="sxs-lookup"><span data-stu-id="e8cbf-151">Server Error</span></span>| <span data-ttu-id="e8cbf-152">Unexoected error processing request</span><span class="sxs-lookup"><span data-stu-id="e8cbf-152">Unexoected error processing request</span></span>| 









