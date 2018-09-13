---
title: Search explorer for querying indexes in Azure Search | Microsoft Docs
description: Learn how to use Search explorer for querying indexes in Azure Search.
manager: cgronlun
author: HeidiSteen
services: search
ms.service: search
ms.topic: conceptual
ms.date: 07/10/2018
ms.author: heidist
ms.openlocfilehash: 520d9e7b1899c54d922ff6fb77e0901f9609b029
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783386"
---
# <a name="how-to-use-search-explorer-to-query-indexes-in-azure-search"></a><span data-ttu-id="00327-103">How to use Search explorer to query indexes in Azure Search</span><span class="sxs-lookup"><span data-stu-id="00327-103">How to use Search explorer to query indexes in Azure Search</span></span> 

<span data-ttu-id="00327-104">This article shows you how to query an existing Azure Search index using **Search explorer** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="00327-104">This article shows you how to query an existing Azure Search index using **Search explorer** in the Azure portal.</span></span> <span data-ttu-id="00327-105">You can use Search explorer to submit simple or full Lucene query strings to any existing index in your service.</span><span class="sxs-lookup"><span data-stu-id="00327-105">You can use Search explorer to submit simple or full Lucene query strings to any existing index in your service.</span></span>

## <a name="open-the-service-dashboard"></a><span data-ttu-id="00327-106">Open the service dashboard</span><span class="sxs-lookup"><span data-stu-id="00327-106">Open the service dashboard</span></span>
1. <span data-ttu-id="00327-107">Click **All resources** in the jump bar on the left side of the [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="00327-107">Click **All resources** in the jump bar on the left side of the [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="00327-108">Select your Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="00327-108">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="00327-109">Select an index</span><span class="sxs-lookup"><span data-stu-id="00327-109">Select an index</span></span>

<span data-ttu-id="00327-110">Select the index you would like to search from the **Indexes** tile.</span><span class="sxs-lookup"><span data-stu-id="00327-110">Select the index you would like to search from the **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="00327-111">Open Search explorer</span><span class="sxs-lookup"><span data-stu-id="00327-111">Open Search explorer</span></span>

<span data-ttu-id="00327-112">Click on the Search explorer tile to slide open the search bar and results pane.</span><span class="sxs-lookup"><span data-stu-id="00327-112">Click on the Search explorer tile to slide open the search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="00327-113">Start searching</span><span class="sxs-lookup"><span data-stu-id="00327-113">Start searching</span></span>

<span data-ttu-id="00327-114">When using the Search explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) to formulate the query.</span><span class="sxs-lookup"><span data-stu-id="00327-114">When using the Search explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) to formulate the query.</span></span>

1. <span data-ttu-id="00327-115">In **Query string**, type a query and then press **Search**.</span><span class="sxs-lookup"><span data-stu-id="00327-115">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="00327-116">The query string is automatically parsed into the proper request URL to submit a HTTP request against the Azure Search REST API.</span><span class="sxs-lookup"><span data-stu-id="00327-116">The query string is automatically parsed into the proper request URL to submit a HTTP request against the Azure Search REST API.</span></span>   
   
   <span data-ttu-id="00327-117">You can use any valid simple or full Lucene query syntax to create the request.</span><span class="sxs-lookup"><span data-stu-id="00327-117">You can use any valid simple or full Lucene query syntax to create the request.</span></span> <span data-ttu-id="00327-118">The `*` character is equivalent to an empty or unspecified search that returns all documents in no particular order.</span><span class="sxs-lookup"><span data-stu-id="00327-118">The `*` character is equivalent to an empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="00327-119">In  **Results**, query results are presented in raw JSON, identical to the payload returned in an HTTP Response Body when issuing requests programmatically.</span><span class="sxs-lookup"><span data-stu-id="00327-119">In  **Results**, query results are presented in raw JSON, identical to the payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="00327-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="00327-120">Next steps</span></span>

<span data-ttu-id="00327-121">The following resources provide additional query syntax information and examples.</span><span class="sxs-lookup"><span data-stu-id="00327-121">The following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="00327-122">Simple query syntax</span><span class="sxs-lookup"><span data-stu-id="00327-122">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="00327-123">Lucene query syntax</span><span class="sxs-lookup"><span data-stu-id="00327-123">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="00327-124">Lucene query syntax examples</span><span class="sxs-lookup"><span data-stu-id="00327-124">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="00327-125">OData Filter expression syntax</span><span class="sxs-lookup"><span data-stu-id="00327-125">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 