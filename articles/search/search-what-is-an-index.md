---
title: Create an Azure Search index | Microsoft Azure | Hosted cloud search service
description: What is an index in Azure Search and how is it used?
services: search
documentationcenter: ''
author: ashmaka
ms.assetid: a395e166-bf2e-4fca-8bfc-116a46c5f7b1
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 7fc45273c0f71c727b7087949cc63bbb4111f866
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662987"
---
# <a name="create-an-azure-search-index"></a>Create an Azure Search index
> [!div class="op_single_selector"]
> * [Overview](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

## <a name="what-is-an-index"></a>What is an index?
An *index* is a persistent store of *documents* and other constructs used by an Azure Search service. A document is a single unit of searchable data in your index. For example, an e-commerce retailer might have a document for each item they sell, a news organization might have a document for each article, etc. Mapping these concepts to more familiar database equivalents: an *index* is conceptually similar to a *table*, and *documents* are roughly equivalent to *rows* in a table.

When you add/upload documents and submit search queries to Azure Search, you submit your requests to a specific index in your search service.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Field types and attributes in an Azure Search index
As you define your schema, you must specify the name, type, and attributes of each field in your index. The field type classifies the data that is stored in that field. Attributes are set on individual fields to specify how the field is used. The following tables enumerate the types and attributes you can specify.

### <a name="field-types"></a>Field types
| Type | Description |
| --- | --- |
| *Edm.String* |Text that can optionally be tokenized for full-text search (word-breaking, stemming, etc). |
| *Collection(Edm.String)* |A list of strings that can optionally be tokenized for full-text search. There is no theoretical upper limit on the number of items in a collection, but the 16 MB upper limit on payload size applies to collections. |
| *Edm.Boolean* |Contains true/false values. |
| *Edm.Int32* |32-bit integer values. |
| *Edm.Int64* |64-bit integer values. |
| *Edm.Double* |Double-precision numeric data. |
| *Edm.DateTimeOffset* |Date time values represented in the OData V4 format (e.g. `yyyy-MM-ddTHH:mm:ss.fffZ` or `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`). |
| *Edm.GeographyPoint* |A point representing a geographic location on the globe. |

You can find more detailed information about Azure Search's [supported data types here](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types).

### <a name="field-attributes"></a>Field attributes
| Attribute | Description |
| --- | --- |
| *Key* |A string that provides the unique ID of each document, used for document look up. Every index must have one key. Only one field can be the key, and its type must be set to Edm.String. |
| *Retrievable* |Specifies whether a field can be returned in a search result. |
| *Filterable* |Allows the field to be used in filter queries. |
| *Sortable* |Allows a query to sort search results using this field. |
| *Facetable* |Allows a field to be used in a [faceted navigation](search-faceted-navigation.md) structure for user self-directed filtering. Typically fields containing repetitive values that you can use to group multiple documents together (for example, multiple documents that fall under a single brand or service category) work best as facets. |
| *Searchable* |Marks the field as full-text searchable. |

You can find more detailed information about Azure Search's [index attributes here](https://docs.microsoft.com/rest/api/searchservice/Create-Index).

## <a name="guidance-for-defining-an-index-schema"></a>Guidance for defining an index schema
As you design your index, take your time in the planning phase to think through each decision. It is important that you keep your search user experience and business needs in mind when designing your index as each field must be assigned the [proper attributes](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Changing an index after it is deployed involves rebuilding and reloading the data.

If data storage requirements change over time, you can increase or decrease capacity by adding or removing partitions. For details, see [Manage your Search service in Azure](search-manage.md) or [Service Limits](search-limits-quotas-capacity.md).

