---
title: Service limits in Azure Search | Microsoft Docs
description: Service limits used for capacity planning and maximum limits on requests and responses for Azure Search.
services: search
documentationcenter: ''
author: HeidiSteen
manager: jhubbard
editor: ''
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/23/2017
ms.author: heidist
ms.openlocfilehash: c7094a92355a199e9b94bc695c8499271b9adc39
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550222"
---
# <a name="service-limits-in-azure-search"></a>Service limits in Azure Search
Maximum limits on storage, workloads, and quantities of indexes, documents, and other objects depend on whether you [provision Azure Search](search-create-service-portal.md) at a **Free**, **Basic**, or **Standard** pricing tier.

* **Free** is a multi-tenant shared service that comes with your Azure subscription. It's a no-additional-cost option for existing subscribers that allows you to experiment with the service before signing up for dedicated resources.
* **Basic** provides dedicated computing resources for production workloads at a smaller scale.
* **Standard** runs on dedicated machines, with more storage and processing capacity at every level. Standard comes in four levels: S1, S2, S3, and S3 High Density (S3 HD).

> [!NOTE]
> A service is provisioned at a specific tier. If you need to jump tiers to get more capacity, you must provision a new service (there is no in-place upgrade). For more information, see [Choose a SKU or tier](search-sku-tier.md). To learn more about adjusting capacity within a service you've already provisioned, see [Scale resource levels for query and indexing workloads](search-capacity-planning.md).
>

## <a name="per-subscription-limits"></a>Per subscription limits
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>Per service limits
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>Per index limits
There is a one-to-one correspondence between limits on indexes and limits on indexers. Given a limit of 200 indexes, the maximum limit for indexers is also 200 for the same service.

| Resource | Free | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Index: maximum fields per index |1000 |100 <sup>1</sup> |1000 |1000 |1000 |1000 |
| Index: maximum scoring profiles per index |16 |16 |16 |16 |16 |16 |
| Index: maximum functions per profile |8 |8 |8 |8 |8 |8 |
| Indexers: maximum indexing load per invocation |10,000 documents |Limited only by maximum documents |Limited only by maximum documents |Limited only by maximum documents |Limited only by maximum documents |N/A <sup>2</sup> |
| Indexers: maximum running time |3 minutes |24 hours |24 hours |24 hours |24 hours |N/A <sup>2</sup> |
| Blob indexer: maximum blob size, MB |16 |16 |128 |256 |256 |N/A <sup>2</sup> |
| Blob indexer: maximum characters of content extracted from a blob |32,000 |64,000 |4 million |4 million |4 million |N/A <sup>2</sup> |

<sup>1</sup> Basic tier is the only SKU with a lower limit of 100 fields per index.

<sup>2</sup> S3 HD doesn't currently support indexers. Contact Azure Support if you have an urgent need for this capability.

## <a name="document-size-limits"></a>Document size limits
| Resource | Free | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Individual document size per Index API |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |

Refers to the maximum document size when calling an Index API. Document size is actually a limit on the size of the Index API request body. Since you can pass a batch of multiple documents to the Index API at once, the size limit actually depends on how many documents are in the batch. For a batch with a single document, the maximum document size is 16 MB of JSON.

To keep document size down, remember to exclude non-queryable data from the request. Images and other binary data are not directly queryable and shouldn't be stored in the index. To integrate non-queryable data into search results, define a non-searchable field that stores a URL reference to the resource.

## <a name="workload-limits-queries-per-second"></a>Workload limits (Queries per second)
| Resource | Free | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| QPS |N/A |~3 per replica |~15 per replica |~60 per replica |>60 per replica |>60 per replica |

Queries per second (QPS) is an approximation based on heuristics, using simulated and actual customer workloads to derive estimated values. Exact QPS throughput varies depending on your data and the nature of the query.

Although rough estimates are provided above, an actual rate is difficult to determine, especially in the Free shared service where throughput is based on available bandwidth and competition for system resources. In the Free tier, compute and storage resources are shared by multiple subscribers, so QPS for your solution will always vary depending on how many other workloads are running at the same time.

At the standard level, you can estimate QPS more closely because you have control over more of the parameters. See the best practices section in [Manage your search solution](search-manage.md) for guidance on how to calculate QPS for your workloads.

## <a name="api-request-limits"></a>API Request limits
* Maximum of 16 MB per request <sup>1</sup>
* Maximum 8 KB URL length
* Maximum 1000 documents per batch of index uploads, merges, or deletes
* Maximum 32 fields in $orderby clause
* Maximum search term size is 32,766 bytes (32 KB minus 2 bytes) of UTF-8 encoded text

<sup>1</sup> In Azure Search, the body of a request is subject to an upper limit of 16 MB, imposing a practical limit on the contents of individual fields or collections that are not otherwise constrained by theoretical limits (see [Supported data types](https://msdn.microsoft.com/library/azure/dn798938.aspx) for more information about field composition and restrictions).

## <a name="api-response-limits"></a>API Response limits
* Maximum 1000 documents returned per page of search results
* Maximum 100 suggestions returned per Suggest API request

## <a name="api-key-limits"></a>API Key limits
Api-keys are used for service authentication. There are two types. Admin keys are specified in the request header and grant full read-write access to the service. Query keys are read-only, specified on the URL, and typically distributed to client applications.

* Maximum of 2 admin keys per service
* Maximum of 50 query keys per service
