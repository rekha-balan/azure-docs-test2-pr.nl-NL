---
title: Query your Azure Search Index using the Azure Portal | Microsoft Docs
description: Issue a search query in the Azure Portal's Search Explorer.
services: search
manager: jhubbard
documentationcenter: ''
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: ashmaka
ms.openlocfilehash: 5366b8fa35e2187698fc433f4b53374e47846084
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672347"
---
# <a name="query-your-azure-search-index-using-the-azure-portal"></a>Query your Azure Search index using the Azure Portal
> [!div class="op_single_selector"]
> * [Overview](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

This guide will show you how to query your Azure Search index in the Azure Portal.

Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).

## <a name="i-go-to-your-azure-search-blade"></a>I. Go to your Azure Search blade
1. Click on "All resources" in the menu on the left side of the [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)
2. Select your Azure Search service

## <a name="ii-select-the-index-you-would-like-to-search"></a>II. Select the index you would like to search
1. Select the index you would like to search from the "Indexes" tile.

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-explorer/pick-index.png)

## <a name="iii-click-on-the-search-explorer-tile"></a>III. Click on the "Search Explorer" tile
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-explorer/search-explorer-tile.png)

## <a name="iii-start-searching"></a>III. Start searching
1. To search your Azure Search index, start typing into the "*Query string*" field and then press "**Search**".
   
   * When using the Search Explorer, you can specify any of the [query parameters](https://msdn.microsoft.com/library/dn798927.aspx)
2. In the "*Results*" section, the query's results will be presented in the raw JSON that you would receiving in an HTTP Response Body when issuing search requests against the Azure Search REST API.
3. The query string is automatically parsed into the proper request URL to submit a HTTP request against the Azure Search REST API

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-explorer/search-bar.png)




