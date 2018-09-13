---
title: Azure DocumentDB .NET Core API, SDK & Resources | Microsoft Docs
description: Learn all about the .NET Core API and SDK including release dates, retirement dates, and changes made between each version of the DocumentDB .NET Core SDK.
services: documentdb
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/29/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82fd5a2f23fc6e7bc765d2ffea4b4b7b3c76896e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549506"
---
# <a name="documentdb-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="51045-103">DocumentDB .NET Core SDK: Release notes and resources</span><span class="sxs-lookup"><span data-stu-id="51045-103">DocumentDB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/en-us/rest/api/documentdb/)
> * [REST Resource Provider](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="51045-112">**SDK download**</span><span class="sxs-lookup"><span data-stu-id="51045-112">**SDK download**</span></span></td><td>[<span data-ttu-id="51045-113">NuGet</span><span class="sxs-lookup"><span data-stu-id="51045-113">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="51045-114">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="51045-114">**API documentation**</span></span></td><td>[<span data-ttu-id="51045-115">.NET API reference documentation</span><span class="sxs-lookup"><span data-stu-id="51045-115">.NET API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn948556.aspx)</td></tr>

<tr><td><span data-ttu-id="51045-116">**Samples**</span><span class="sxs-lookup"><span data-stu-id="51045-116">**Samples**</span></span></td><td>[<span data-ttu-id="51045-117">.NET code samples</span><span class="sxs-lookup"><span data-stu-id="51045-117">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="51045-118">**Get started**</span><span class="sxs-lookup"><span data-stu-id="51045-118">**Get started**</span></span></td><td>[<span data-ttu-id="51045-119">Get started with the DocumentDB .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="51045-119">Get started with the DocumentDB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="51045-120">**Web app tutorial**</span><span class="sxs-lookup"><span data-stu-id="51045-120">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="51045-121">Web application development with DocumentDB</span><span class="sxs-lookup"><span data-stu-id="51045-121">Web application development with DocumentDB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="51045-122">**Current supported framework**</span><span class="sxs-lookup"><span data-stu-id="51045-122">**Current supported framework**</span></span></td><td>[<span data-ttu-id="51045-123">.NET Standard 1.6</span><span class="sxs-lookup"><span data-stu-id="51045-123">.NET Standard 1.6</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="51045-124">Release Notes</span><span class="sxs-lookup"><span data-stu-id="51045-124">Release Notes</span></span>

<span data-ttu-id="51045-125">The DocumentDB .NET Core SDK has feature parity with the latest version of the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="51045-125">The DocumentDB .NET Core SDK has feature parity with the latest version of the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> The DocumentDB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps. If you are interested in the .NET Core SDK that does support UWP apps, send email to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com).

### <a name="a-name121121"></a><span data-ttu-id="51045-128"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="51045-128"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="51045-129">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span><span class="sxs-lookup"><span data-stu-id="51045-129">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="51045-130"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="51045-130"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="51045-131">Fixes to make SDK more resilient to automatic failover under certain conditions.</span><span class="sxs-lookup"><span data-stu-id="51045-131">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="51045-132"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="51045-132"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="51045-133">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span><span class="sxs-lookup"><span data-stu-id="51045-133">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="51045-134">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span><span class="sxs-lookup"><span data-stu-id="51045-134">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="51045-135"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="51045-135"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="51045-136">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="51045-136">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="51045-137">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span><span class="sxs-lookup"><span data-stu-id="51045-137">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="51045-138">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span><span class="sxs-lookup"><span data-stu-id="51045-138">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="51045-139">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span><span class="sxs-lookup"><span data-stu-id="51045-139">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="51045-140"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="51045-140"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="51045-141">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span><span class="sxs-lookup"><span data-stu-id="51045-141">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="51045-142">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="51045-142">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="51045-143">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="51045-143">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="51045-144"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="51045-144"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="51045-145">The DocumentDB .NET Core SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span><span class="sxs-lookup"><span data-stu-id="51045-145">The DocumentDB .NET Core SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span> <span data-ttu-id="51045-146">The latest release of the DocumentDB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used to build applications that target iOS, Android, and Mono (Linux).</span><span class="sxs-lookup"><span data-stu-id="51045-146">The latest release of the DocumentDB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used to build applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="51045-147"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="51045-147"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="51045-148">The DocumentDB .NET Core Preview SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span><span class="sxs-lookup"><span data-stu-id="51045-148">The DocumentDB .NET Core Preview SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="51045-149">The DocumentDB .NET Core Preview SDK has feature parity with the latest version of the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) and supports the following:</span><span class="sxs-lookup"><span data-stu-id="51045-149">The DocumentDB .NET Core Preview SDK has feature parity with the latest version of the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) and supports the following:</span></span>
* <span data-ttu-id="51045-150">All [connection modes](documentdb-performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span><span class="sxs-lookup"><span data-stu-id="51045-150">All [connection modes](documentdb-performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="51045-151">All [consistency levels](documentdb-consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span><span class="sxs-lookup"><span data-stu-id="51045-151">All [consistency levels](documentdb-consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="51045-152">[Partitioned collections](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="51045-152">[Partitioned collections](documentdb-partition-data.md).</span></span> 
* <span data-ttu-id="51045-153">[Multi-region database accounts and geo-replication](documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="51045-153">[Multi-region database accounts and geo-replication](documentdb-distribute-data-globally.md).</span></span>

<span data-ttu-id="51045-154">If you have questions related to this SDK, post to [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in the [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="51045-154">If you have questions related to this SDK, post to [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in the [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="51045-155">Release & Retirement Dates</span><span class="sxs-lookup"><span data-stu-id="51045-155">Release & Retirement Dates</span></span>

| <span data-ttu-id="51045-156">Version</span><span class="sxs-lookup"><span data-stu-id="51045-156">Version</span></span> | <span data-ttu-id="51045-157">Release Date</span><span class="sxs-lookup"><span data-stu-id="51045-157">Release Date</span></span> | <span data-ttu-id="51045-158">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="51045-158">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="51045-159">1.2.1</span><span class="sxs-lookup"><span data-stu-id="51045-159">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="51045-160">March 29, 2017</span><span class="sxs-lookup"><span data-stu-id="51045-160">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="51045-161">1.2.0</span><span class="sxs-lookup"><span data-stu-id="51045-161">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="51045-162">March 25, 2017</span><span class="sxs-lookup"><span data-stu-id="51045-162">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="51045-163">1.1.2</span><span class="sxs-lookup"><span data-stu-id="51045-163">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="51045-164">March 20, 2017</span><span class="sxs-lookup"><span data-stu-id="51045-164">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="51045-165">1.1.1</span><span class="sxs-lookup"><span data-stu-id="51045-165">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="51045-166">March 14, 2017</span><span class="sxs-lookup"><span data-stu-id="51045-166">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="51045-167">1.1.0</span><span class="sxs-lookup"><span data-stu-id="51045-167">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="51045-168">February 16, 2017</span><span class="sxs-lookup"><span data-stu-id="51045-168">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="51045-169">1.0.0</span><span class="sxs-lookup"><span data-stu-id="51045-169">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="51045-170">December 21, 2016</span><span class="sxs-lookup"><span data-stu-id="51045-170">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="51045-171">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="51045-171">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="51045-172">November 15, 2016</span><span class="sxs-lookup"><span data-stu-id="51045-172">November 15, 2016</span></span> |<span data-ttu-id="51045-173">December 31, 2016</span><span class="sxs-lookup"><span data-stu-id="51045-173">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="51045-174">See Also</span><span class="sxs-lookup"><span data-stu-id="51045-174">See Also</span></span>
<span data-ttu-id="51045-175">To learn more about DocumentDB, see [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) service page.</span><span class="sxs-lookup"><span data-stu-id="51045-175">To learn more about DocumentDB, see [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) service page.</span></span> 

