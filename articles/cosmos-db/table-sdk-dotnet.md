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
# <a name="azure-cosmos-db-table-net-api-download-and-release-notes"></a>Azure Cosmos DB Table .NET API: Download and release notes
> [!div class="op_single_selector"]
> * [.NET](table-sdk-dotnet.md)
> * [Java](table-sdk-java.md)
> * [Node.js](table-sdk-nodejs.md)
> * [Python](table-sdk-python.md)

|   |   |
|---|---|
|**SDK download**|[NuGet](https://aka.ms/acdbtablenuget)|
|**API documentation**|[.NET API reference documentation](https://aka.ms/acdbtableapiref)|
|**Quickstart**|[Azure Cosmos DB: Build an app with .NET and the Table API](create-table-dotnet.md)|
|**Tutorial**|[Azure Cosmos DB: Develop with the Table API in .NET](tutorial-develop-table-dotnet.md)|
|**Current supported framework**|[Microsoft .NET Framework 4.5.1](https://www.microsoft.com/en-us/download/details.aspx?id=40779)|

> [!IMPORTANT]
> If you created a Table API account during the preview, please create a [new Table API account](create-table-dotnet.md#create-a-database-account) to work with the generally available Table API SDKs.
>

## <a name="release-notes"></a>Release notes

### <a name="a-name113113"></a><a name="1.1.3"/>1.1.3
* Fixed NuGet package dependencies on Microsoft.Azure.Storage.Common and Microsoft.Azure.DocumentDB.
* Bug fixes on table serialization when JsonConvert.DefaultSettings are configured.

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1
* Added validation for malformed ETAGs in Direct Mode.
* Fixed LINQ query bug in Gateway Mode.
* Synchronous APIs now run on the thread pool with SynchronizationContext.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Add TableQueryMaxItemCount, TableQueryEnableScan, TableQueryMaxDegreeOfParallelism, and TableQueryContinuationTokenLimitInKb to TableRequestOptions
* Bug Fixes

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* General availability release

### <a name="a-name010-preview090-preview"></a><a name="0.1.0-preview"/>0.9.0-preview
* Initial preview release

## <a name="release-and-retirement-dates"></a>Release and Retirement dates
Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.

The [WindowsAzure.Storage-PremiumTable](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable/0.1.0-preview) preview package has been deprecated and replaced by the [Microsoft.Azure.CosmosDB.Table](https://www.nuget.org/packages/Microsoft.Azure.CosmosDB.Table) package. The WindowsAzure.Storage-PremiumTable SDK will be retired on November 15, 2018, at which time requests to the retired SDK will not be permitted. The `Microsoft.Azure.CosmosDB.Table` library is currently available for .NET Standard only, it's not yet available for .NET Core.

New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible. 

Any requests to Azure Cosmos DB using a retired SDK are rejected by the service.
<br/>

| Version | Release Date | Retirement Date |
| --- | --- | --- |
| [1.1.3](#1.1.3) |July 17, 2018|--- |
| [1.1.1](#1.1.1) |March 26, 2018|--- |
| [1.1.0](#1.1.0) |February 21, 2018|--- |
| [1.0.0](#1.0.0) |November 15, 2017|--- |
| [0.9.0-preview](#0.9.0-preview) |November 11, 2017 |--- |

## <a name="troubleshooting"></a>Troubleshooting

If you get the error 

```
Unable to resolve dependency 'Microsoft.Azure.Storage.Common'. Source(s) used: 'nuget.org', 
'CliFallbackFolder', 'Microsoft Visual Studio Offline Packages', 'Microsoft Azure Service Fabric SDK'`
```

when attempting to use the Microsoft.Azure.CosmosDB.Table NuGet package, you have two options to fix the issue:

* Use Package Manage Console to install the Microsoft.Azure.CosmosDB.Table package and its dependencies. To do this, type the following in the Package Manager Console for your solution. 
    ```
    Install-Package Microsoft.Azure.CosmosDB.Table -IncludePrerelease
    ```
    
* Using your preferred NuGet package management tool, install the Microsoft.Azure.Storage.Common NuGet package before installing Microsoft.Azure.CosmosDB.Table.

## <a name="faq"></a>FAQ

[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>See also
To learn more about the Azure Cosmos DB Table API, see [Introduction to Azure Cosmos DB Table API](table-introduction.md). 
