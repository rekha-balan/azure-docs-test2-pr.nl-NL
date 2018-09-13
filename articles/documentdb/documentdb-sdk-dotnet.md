---
title: Azure DocumentDB .NET SDK & Resources | Microsoft Docs
description: Learn all about the .NET API and SDK including release dates, retirement dates, and changes made between each version of the DocumentDB .NET SDK.
services: documentdb
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/29/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 410a5d04286ebc9984142303c3edd67ca60500e4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672259"
---
# <a name="documentdb-net-sdk-download-and-release-notes"></a>DocumentDB .NET SDK: Download and release notes
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

<tr><td>**SDK download**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td>**API documentation**</td><td>[.NET API reference documentation](https://msdn.microsoft.com/library/azure/dn948556.aspx)</td></tr>

<tr><td>**Samples**</td><td>[.NET code samples](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Get started**</td><td>[Get started with the DocumentDB .NET SDK](documentdb-get-started.md)</td></tr>

<tr><td>**Web app tutorial**</td><td>[Web application development with DocumentDB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Current supported framework**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>Release notes

### <a name="a-name11311131"></a><a name="1.13.1"/>1.13.1
* Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.

### <a name="a-name11301130"></a><a name="1.13.0"/>1.13.0
* Fixes to make SDK more resilient to automatic failover under certain conditions.

### <a name="a-name11221122"></a><a name="1.12.2"/>1.12.2
* Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.
* Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.

### <a name="a-name11211121"></a><a name="1.12.1"/>1.12.1
* Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).
* Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.
* Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.
* Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG). See [Aggregation support](documentdb-sql-query.md#Aggregates).
* Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.

### <a name="a-name11141114"></a><a name="1.11.4"/>1.11.4
* Fix for an issue wherein some of the cross-partition queries were failing in the 32-bit host process.
* Fix for an issue wherein the session container was not being updated with the token for failed requests in Gateway mode.
* Fix for an issue wherein a query with UDF calls in projection was failing in some cases.
* Client side performance fixes for increasing the read and write throughput of the requests.

### <a name="a-name11131113"></a><a name="1.11.3"/>1.11.3
* Fix for an issue wherein the session container was not being updated with the token for failed requests.
* Added support for the SDK to work in a 32-bit host process. Note that if you use cross partition queries, 64-bit host processing is recommended for improved performance.
* Improved performance for scenarios involving queries with a large number of partition key values in an IN expression.
* Populated various resource quota stats in the ResourceResponse for document collection read requests when PopulateQuotaInfo request option is set.

### <a name="a-name11111111"></a><a name="1.11.1"/>1.11.1
* Minor performance fix for the CreateDocumentCollectionIfNotExistsAsync API introduced in 1.11.0.
* Performance fix in the SDK for scenarios that involve high degree of concurrent requests.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Support for new classes and methods to process the [change feed](documentdb-change-feed.md) of documents within a collection.
* Support for cross-partition query continuation and some perf improvements for cross-partition queries.
* Addition of CreateDatabaseIfNotExistsAsync and CreateDocumentCollectionIfNotExistsAsync methods.
* LINQ support for system functions: IsDefined, IsNull and IsPrimitive.
* Fix for automatic binplacing of Microsoft.Azure.Documents.ServiceInterop.dll and DocumentDB.Spatial.Sql.dll assemblies to application’s bin folder when using the Nuget package with projects that have project.json tooling.
* Support for emitting client side ETW traces which could be helpful in debugging scenarios.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Added direct connectivity support for partitioned collections.
* Improved performance for the Bounded Staleness consistency level.
* Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.
* Added LINQ support for StringEnumConverter, IsoDateTimeConverter and UnixDateTimeConverter while translating predicates.
* Various SDK bug fixes.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Fixed an issue that caused the following NotFoundException: The read session is not available for the input session token. This exception occurred in some cases when querying for the read-region of a geo-distributed account.
* Exposed the ResponseStream property in the ResourceResponse class, which enables direct access to the underlying stream from a response.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Modified the ResourceResponse, FeedResponse, StoredProcedureResponse and MediaResponse classes to implement the corresponding public interface so that they can be mocked for test driven deployment (TDD).
* Fixed an issue that caused a malformed partition key header when using a custom JsonSerializerSettings object for serializing data.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Fixed an issue that caused long running queries to fail with error: Authorization token is not valid at the current time.
* Fixed an issue that removed the original SqlParameterCollection from cross partition top/order-by queries.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Added support for parallel queries for partitioned collections.
* Added support for cross partition ORDER BY and TOP queries for partitioned collections.
* Fixed the missing references to DocumentDB.Spatial.Sql.dll and Microsoft.Azure.Documents.ServiceInterop.dll that are required when referencing a DocumentDB project with a reference to the DocumentDB Nuget package.
* Fixed the ability to use parameters of different types when using user-defined functions in LINQ. 
* Fixed a bug for globally replicated accounts where Upsert calls were being directed to read locations instead of write locations.
* Added methods to the IDocumentClient interface that were missing: 
  * UpsertAttachmentAsync method that takes mediaStream and options as parameters
  * CreateAttachmentAsync method that takes options as a parameter
  * CreateOfferQuery method that takes querySpec as a parameter.
* Unsealed public classes that are exposed in the IDocumentClient interface.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Added the support for multi-region database accounts.
* Added support for retry on throttled requests.  User can customize the number of retries and the max wait time by configuring the ConnectionPolicy.RetryOptions property.
* Added a new IDocumentClient interface that defines the signatures of all DocumenClient properties and methods.  As part of this change, also changed extension methods that create IQueryable and IOrderedQueryable to methods on the DocumentClient class itself.
* Added configuration option to set the ServicePoint.ConnectionLimit for a given DocumentDB endpoint Uri.  Use ConnectionPolicy.MaxConnectionLimit to change the default value, which is set to 50.
* Deprecated IPartitionResolver and its implementation.  Support for IPartitionResolver is now obsolete. It's recommended that you use Partitioned Collections for higher storage and throughput.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Added an overload to Uri based ExecuteStoredProcedureAsync method that takes RequestOptions as a parameter.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Added time to live (TTL) support for documents.

### <a name="a-name163163"></a><a name="1.6.3"/>1.6.3
* Fixed a bug in Nuget packaging of .NET SDK for packaging it as part of an Azure Cloud Service solution.

### <a name="a-name162162"></a><a name="1.6.2"/>1.6.2
* Implemented [partitioned collections](documentdb-partition-data.md) and [user-defined performance levels](documentdb-performance-levels.md). 

### <a name="a-name153153"></a><a name="1.5.3"/>1.5.3
* **[Fixed]** Querying DocumentDB endpoint throws: 'System.Net.Http.HttpRequestException: Error while copying content to a stream'.

### <a name="a-name152152"></a><a name="1.5.2"/>1.5.2
* Expanded LINQ support including new operators for paging, conditional expressions and range comparison.
  * Take operator to enable SELECT TOP behavior in LINQ
  * CompareTo operator to enable string range comparisons
  * Conditional (?) and coalesce operators (??)
* **[Fixed]** ArgumentOutOfRangeException when combining Model projection with Where-In in linq query.  [#81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* **[Fixed]** If Select is not the last expression the LINQ Provider assumed no projection and produced SELECT * incorrectly.  [#58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Implemented Upsert, Added UpsertXXXAsync methods
* Performance improvements for all requests
* LINQ Provider support for conditional, coalesce and CompareTo methods for strings
* **[Fixed]** LINQ provider --> Implement Contains method on List to generate the same SQL as on IEnumerable and Array
* **[Fixed]** BackoffRetryUtility uses the same HttpRequestMessage again instead of creating a new one on retry
* **[Obsolete]** UriFactory.CreateCollection --> should now use UriFactory.CreateDocumentCollection

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1
* **[Fixed]** Localization issues when using non en culture info such as nl-NL etc. 

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* ID Based Routing
  * New UriFactory helper to assist with constructing ID based resource links
  * New overloads on DocumentClient to take in URI
* Added IsValid() and IsValidDetailed() in LINQ for geospatial
* LINQ Provider support enhanced
  * **Math** - Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate
  * **String** - Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper
  * **Array** - Concat, Contains, Count
  * **IN** operator

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Added support for modifying indexing policies
  * New ReplaceDocumentCollectionAsync method in DocumentClient
  * New IndexTransformationProgress property in ResourceResponse<T> for tracking percent progress of index policy changes
  * DocumentCollection.IndexingPolicy is now mutable
* Added support for spatial indexing and query
  * New Microsoft.Azure.Documents.Spatial namespace for serializing/deserializing spatial types like Point and Polygon
  * New SpatialIndex class for indexing GeoJSON data stored in DocumentDB
* **[Fixed]** : Incorrect SQL query generated from linq expression [#38](https://github.com/Azure/azure-documentdb-net/issues/38)

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Dependency on Newtonsoft.Json v5.0.7 
* Changes to support Order By
  
  * LINQ provider support for OrderBy() or OrderByDescending()
  * IndexingPolicy to support Order By 
    
    **NB: Possible breaking change** 
    
    If you have existing code that provisions collections with a custom indexing policy, then your existing code will need to be updated to support the new IndexingPolicy class. If you have no custom indexing policy, then this change does not affect you.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Support for partitioning data by using the new HashPartitionResolver and RangePartitionResolver classes and the IPartitionResolver
* DataContract serialization
* Guid support in LINQ provider
* UDF support in LINQ

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK

## <a name="release--retirement-dates"></a>Release & Retirement dates
Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.

New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible. 

Any request to DocumentDB using a retired SDK will be rejected by the service.

<br/>

| Version | Release Date | Retirement Date |
| --- | --- | --- |
| [1.13.1](#1.13.1) |March 29, 2017 |--- |
| [1.13.0](#1.13.0) |March 24, 2017 |--- |
| [1.12.2](#1.12.2) |March 20, 2017 |--- |
| [1.12.1](#1.12.1) |March 14, 2017 |--- |
| [1.12.0](#1.12.0) |February 15, 2017 |--- |
| [1.11.4](#1.11.4) |February 06, 2017 |--- |
| [1.11.3](#1.11.3) |January 26, 2017 |--- |
| [1.11.1](#1.11.1) |December 21, 2016 |--- |
| [1.11.0](#1.11.0) |December 08, 2016 |--- |
| [1.10.0](#1.10.0) |September 27, 2016 |--- |
| [1.9.5](#1.9.5) |September 01, 2016 |--- |
| [1.9.4](#1.9.4) |August 24, 2016 |--- |
| [1.9.3](#1.9.3) |August 15, 2016 |--- |
| [1.9.2](#1.9.2) |July 23, 2016 |--- |
| [1.8.0](#1.8.0) |June 14, 2016 |--- |
| [1.7.1](#1.7.1) |May 06, 2016 |--- |
| [1.7.0](#1.7.0) |April 26, 2016 |--- |
| [1.6.3](#1.6.3) |April 08, 2016 |--- |
| [1.6.2](#1.6.2) |March 29, 2016 |--- |
| [1.5.3](#1.5.3) |February 19, 2016 |--- |
| [1.5.2](#1.5.2) |December 14, 2015 |--- |
| [1.5.1](#1.5.1) |November 23, 2015 |--- |
| [1.5.0](#1.5.0) |October 05, 2015 |--- |
| [1.4.1](#1.4.1) |August 25, 2015 |--- |
| [1.4.0](#1.4.0) |August 13, 2015 |--- |
| [1.3.0](#1.3.0) |August 05, 2015 |--- |
| [1.2.0](#1.2.0) |July 06, 2015 |--- |
| [1.1.0](#1.1.0) |April 30, 2015 |--- |
| [1.0.0](#1.0.0) |April 08, 2015 |--- |


## <a name="faq"></a>FAQ
[!INCLUDE [documentdb-sdk-faq](../../includes/documentdb-sdk-faq.md)]

## <a name="see-also"></a>See also
To learn more about DocumentDB, see [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) service page. 

