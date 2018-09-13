---
title: Azure Cosmos DB Table API .NET SDK & Resources | Microsoft Docs
description: Learn all about the Azure Cosmos DB Table API including release dates, retirement dates, and changes made between each version.
services: cosmos-db
author: rnagpal
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: dotnet
ms.topic: reference
ms.date: 08/17/2018
ms.author: rnagpal
ms.openlocfilehash: d0bd7dba5d50445cb681c16d9575b1bd69167e2f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871363"
---
# <a name="azure-cosmos-db-table-net-api-download-and-release-notes"></a><span data-ttu-id="c4075-103">Azure Cosmos DB Table .NET API: Download and release notes</span><span class="sxs-lookup"><span data-stu-id="c4075-103">Azure Cosmos DB Table .NET API: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [.NET](table-sdk-dotnet.md)
> * [Java](table-sdk-java.md)
> * [Node.js](table-sdk-nodejs.md)
> * [Python](table-sdk-python.md)

|   |   |
|---|---|
|<span data-ttu-id="c4075-108">**SDK download**</span><span class="sxs-lookup"><span data-stu-id="c4075-108">**SDK download**</span></span>|[<span data-ttu-id="c4075-109">NuGet</span><span class="sxs-lookup"><span data-stu-id="c4075-109">NuGet</span></span>](https://aka.ms/acdbtablenuget)|
|<span data-ttu-id="c4075-110">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="c4075-110">**API documentation**</span></span>|[<span data-ttu-id="c4075-111">.NET API reference documentation</span><span class="sxs-lookup"><span data-stu-id="c4075-111">.NET API reference documentation</span></span>](https://aka.ms/acdbtableapiref)|
|<span data-ttu-id="c4075-112">**Quickstart**</span><span class="sxs-lookup"><span data-stu-id="c4075-112">**Quickstart**</span></span>|[<span data-ttu-id="c4075-113">Azure Cosmos DB: Build an app with .NET and the Table API</span><span class="sxs-lookup"><span data-stu-id="c4075-113">Azure Cosmos DB: Build an app with .NET and the Table API</span></span>](create-table-dotnet.md)|
|<span data-ttu-id="c4075-114">**Tutorial**</span><span class="sxs-lookup"><span data-stu-id="c4075-114">**Tutorial**</span></span>|[<span data-ttu-id="c4075-115">Azure Cosmos DB: Develop with the Table API in .NET</span><span class="sxs-lookup"><span data-stu-id="c4075-115">Azure Cosmos DB: Develop with the Table API in .NET</span></span>](tutorial-develop-table-dotnet.md)|
|<span data-ttu-id="c4075-116">**Current supported framework**</span><span class="sxs-lookup"><span data-stu-id="c4075-116">**Current supported framework**</span></span>|[<span data-ttu-id="c4075-117">Microsoft .NET Framework 4.5.1</span><span class="sxs-lookup"><span data-stu-id="c4075-117">Microsoft .NET Framework 4.5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=40779)|

> [!IMPORTANT]
> If you created a Table API account during the preview, please create a [new Table API account](create-table-dotnet.md#create-a-database-account) to work with the generally available Table API SDKs.
>

## <a name="release-notes"></a><span data-ttu-id="c4075-119">Release notes</span><span class="sxs-lookup"><span data-stu-id="c4075-119">Release notes</span></span>

### <a name="a-name113113"></a><span data-ttu-id="c4075-120"><a name="1.1.3"/>1.1.3</span><span class="sxs-lookup"><span data-stu-id="c4075-120"><a name="1.1.3"/>1.1.3</span></span>
* <span data-ttu-id="c4075-121">Fixed NuGet package dependencies on Microsoft.Azure.Storage.Common and Microsoft.Azure.DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="c4075-121">Fixed NuGet package dependencies on Microsoft.Azure.Storage.Common and Microsoft.Azure.DocumentDB.</span></span>
* <span data-ttu-id="c4075-122">Bug fixes on table serialization when JsonConvert.DefaultSettings are configured.</span><span class="sxs-lookup"><span data-stu-id="c4075-122">Bug fixes on table serialization when JsonConvert.DefaultSettings are configured.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="c4075-123"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="c4075-123"><a name="1.1.1"/>1.1.1</span></span>
* <span data-ttu-id="c4075-124">Added validation for malformed ETAGs in Direct Mode.</span><span class="sxs-lookup"><span data-stu-id="c4075-124">Added validation for malformed ETAGs in Direct Mode.</span></span>
* <span data-ttu-id="c4075-125">Fixed LINQ query bug in Gateway Mode.</span><span class="sxs-lookup"><span data-stu-id="c4075-125">Fixed LINQ query bug in Gateway Mode.</span></span>
* <span data-ttu-id="c4075-126">Synchronous APIs now run on the thread pool with SynchronizationContext.</span><span class="sxs-lookup"><span data-stu-id="c4075-126">Synchronous APIs now run on the thread pool with SynchronizationContext.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="c4075-127"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="c4075-127"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="c4075-128">Add TableQueryMaxItemCount, TableQueryEnableScan, TableQueryMaxDegreeOfParallelism, and TableQueryContinuationTokenLimitInKb to TableRequestOptions</span><span class="sxs-lookup"><span data-stu-id="c4075-128">Add TableQueryMaxItemCount, TableQueryEnableScan, TableQueryMaxDegreeOfParallelism, and TableQueryContinuationTokenLimitInKb to TableRequestOptions</span></span>
* <span data-ttu-id="c4075-129">Bug Fixes</span><span class="sxs-lookup"><span data-stu-id="c4075-129">Bug Fixes</span></span>

### <a name="a-name100100"></a><span data-ttu-id="c4075-130"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="c4075-130"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="c4075-131">General availability release</span><span class="sxs-lookup"><span data-stu-id="c4075-131">General availability release</span></span>

### <a name="a-name010-preview090-preview"></a><span data-ttu-id="c4075-132"><a name="0.1.0-preview"/>0.9.0-preview</span><span class="sxs-lookup"><span data-stu-id="c4075-132"><a name="0.1.0-preview"/>0.9.0-preview</span></span>
* <span data-ttu-id="c4075-133">Initial preview release</span><span class="sxs-lookup"><span data-stu-id="c4075-133">Initial preview release</span></span>

## <a name="release-and-retirement-dates"></a><span data-ttu-id="c4075-134">Release and Retirement dates</span><span class="sxs-lookup"><span data-stu-id="c4075-134">Release and Retirement dates</span></span>
<span data-ttu-id="c4075-135">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="c4075-135">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="c4075-136">The [WindowsAzure.Storage-PremiumTable](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable/0.1.0-preview) preview package has been deprecated and replaced by the [Microsoft.Azure.CosmosDB.Table](https://www.nuget.org/packages/Microsoft.Azure.CosmosDB.Table) package.</span><span class="sxs-lookup"><span data-stu-id="c4075-136">The [WindowsAzure.Storage-PremiumTable](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable/0.1.0-preview) preview package has been deprecated and replaced by the [Microsoft.Azure.CosmosDB.Table](https://www.nuget.org/packages/Microsoft.Azure.CosmosDB.Table) package.</span></span> <span data-ttu-id="c4075-137">The WindowsAzure.Storage-PremiumTable SDK will be retired on November 15, 2018, at which time requests to the retired SDK will not be permitted.</span><span class="sxs-lookup"><span data-stu-id="c4075-137">The WindowsAzure.Storage-PremiumTable SDK will be retired on November 15, 2018, at which time requests to the retired SDK will not be permitted.</span></span> <span data-ttu-id="c4075-138">The `Microsoft.Azure.CosmosDB.Table` library is currently available for .NET Standard only, it's not yet available for .NET Core.</span><span class="sxs-lookup"><span data-stu-id="c4075-138">The `Microsoft.Azure.CosmosDB.Table` library is currently available for .NET Standard only, it's not yet available for .NET Core.</span></span>

<span data-ttu-id="c4075-139">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="c4075-139">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="c4075-140">Any requests to Azure Cosmos DB using a retired SDK are rejected by the service.</span><span class="sxs-lookup"><span data-stu-id="c4075-140">Any requests to Azure Cosmos DB using a retired SDK are rejected by the service.</span></span>
<br/>

| <span data-ttu-id="c4075-141">Version</span><span class="sxs-lookup"><span data-stu-id="c4075-141">Version</span></span> | <span data-ttu-id="c4075-142">Release Date</span><span class="sxs-lookup"><span data-stu-id="c4075-142">Release Date</span></span> | <span data-ttu-id="c4075-143">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="c4075-143">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="c4075-144">1.1.3</span><span class="sxs-lookup"><span data-stu-id="c4075-144">1.1.3</span></span>](#1.1.3) |<span data-ttu-id="c4075-145">July 17, 2018</span><span class="sxs-lookup"><span data-stu-id="c4075-145">July 17, 2018</span></span>|--- |
| [<span data-ttu-id="c4075-146">1.1.1</span><span class="sxs-lookup"><span data-stu-id="c4075-146">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="c4075-147">March 26, 2018</span><span class="sxs-lookup"><span data-stu-id="c4075-147">March 26, 2018</span></span>|--- |
| [<span data-ttu-id="c4075-148">1.1.0</span><span class="sxs-lookup"><span data-stu-id="c4075-148">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="c4075-149">February 21, 2018</span><span class="sxs-lookup"><span data-stu-id="c4075-149">February 21, 2018</span></span>|--- |
| [<span data-ttu-id="c4075-150">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c4075-150">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="c4075-151">November 15, 2017</span><span class="sxs-lookup"><span data-stu-id="c4075-151">November 15, 2017</span></span>|--- |
| [<span data-ttu-id="c4075-152">0.9.0-preview</span><span class="sxs-lookup"><span data-stu-id="c4075-152">0.9.0-preview</span></span>](#0.9.0-preview) |<span data-ttu-id="c4075-153">November 11, 2017</span><span class="sxs-lookup"><span data-stu-id="c4075-153">November 11, 2017</span></span> |--- |

## <a name="troubleshooting"></a><span data-ttu-id="c4075-154">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="c4075-154">Troubleshooting</span></span>

<span data-ttu-id="c4075-155">If you get the error</span><span class="sxs-lookup"><span data-stu-id="c4075-155">If you get the error</span></span> 

```
Unable to resolve dependency 'Microsoft.Azure.Storage.Common'. Source(s) used: 'nuget.org', 
'CliFallbackFolder', 'Microsoft Visual Studio Offline Packages', 'Microsoft Azure Service Fabric SDK'`
```

<span data-ttu-id="c4075-156">when attempting to use the Microsoft.Azure.CosmosDB.Table NuGet package, you have two options to fix the issue:</span><span class="sxs-lookup"><span data-stu-id="c4075-156">when attempting to use the Microsoft.Azure.CosmosDB.Table NuGet package, you have two options to fix the issue:</span></span>

* <span data-ttu-id="c4075-157">Use Package Manage Console to install the Microsoft.Azure.CosmosDB.Table package and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="c4075-157">Use Package Manage Console to install the Microsoft.Azure.CosmosDB.Table package and its dependencies.</span></span> <span data-ttu-id="c4075-158">To do this, type the following in the Package Manager Console for your solution.</span><span class="sxs-lookup"><span data-stu-id="c4075-158">To do this, type the following in the Package Manager Console for your solution.</span></span> 
    ```
    Install-Package Microsoft.Azure.CosmosDB.Table -IncludePrerelease
    ```
    
* <span data-ttu-id="c4075-159">Using your preferred NuGet package management tool, install the Microsoft.Azure.Storage.Common NuGet package before installing Microsoft.Azure.CosmosDB.Table.</span><span class="sxs-lookup"><span data-stu-id="c4075-159">Using your preferred NuGet package management tool, install the Microsoft.Azure.Storage.Common NuGet package before installing Microsoft.Azure.CosmosDB.Table.</span></span>

## <a name="faq"></a><span data-ttu-id="c4075-160">FAQ</span><span class="sxs-lookup"><span data-stu-id="c4075-160">FAQ</span></span>

[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="c4075-161">See also</span><span class="sxs-lookup"><span data-stu-id="c4075-161">See also</span></span>
<span data-ttu-id="c4075-162">To learn more about the Azure Cosmos DB Table API, see [Introduction to Azure Cosmos DB Table API](table-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4075-162">To learn more about the Azure Cosmos DB Table API, see [Introduction to Azure Cosmos DB Table API](table-introduction.md).</span></span> 
