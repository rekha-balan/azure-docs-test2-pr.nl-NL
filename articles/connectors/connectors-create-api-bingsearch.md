---
title: Add the Bing Search connector logic apps | Microsoft Docs
description: Overview of the Bing Search connector with REST API parameters
services: ''
suite: ''
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
tags: connectors
ms.assetid: a7f530e8-1573-4612-8899-c9c84aa2de6d
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: dbb920f212d46365233e83ba1e0a0ae99917e405
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554932"
---
# <a name="get-started-with-the-bing-search-connector"></a>Get started with the Bing Search connector
Connect to Bing Search to search news, search videos, and more. With Bing Search, you can: 

* Build your business flow based on the data you get from your search. 
* Use actions to search images, search the news, and more. These actions get a response, and then make the output available for other actions. For example, you can search for a video, and then use Twitter to post that video to a Twitter feed.

To add an operation in logic apps, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="triggers-and-actions"></a>Triggers and actions
Bing Search includes the following actions. There are no triggers. 

| Triggers | Actions |
| --- | --- |
| None |<ul><li>Search web</li><li>Search videos</li><li>Search images</li><li>Search news</li><li>Search related</li><li>Search spellings</li><li>Search all</li></ul> |

All connectors support data in JSON and XML formats.

## <a name="swagger-rest-api-reference"></a>Swagger REST API reference
Applies to version: 1.0.

### <a name="search-web"></a>Search web
Retrieves web sites from a Bing search.  
```GET: /Web```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| query |string |yes |query |none |Text to search for (example: 'xbox') |
| maxResult |integer |no |query |none |Maximum number of results to return |
| startOffset |integer |no |query |none |Number of results to skip |
| adultContent |string |no |query |none |Adult content filter. Valid values: <ul><li>Off</li><li>Moderate</li><li>Strict</li></ul> |
| market |string |no |query |none |Market or region to narrow the search (example: en-US) |
| longitude |number |no |query |none |Longitude (east/west coordinate) to narrow the search (example: 47.603450) |
| latitude |number |no |query |none |Latitude (north/south coordinate) to narrow the search (example: -122.329696) |
| webFileType |string |no |query |none |File type to narrow the search (example: 'DOC') |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="search-videos"></a>Search videos
Retrieves videos from a Bing search.  
```GET: /Video```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| query |string |yes |query |none |Text to search for (example: 'xbox') |
| maxResult |integer |no |query |none |Maximum number of results to return |
| startOffset |integer |no |query |none |Number of results to skip |
| adultContent |string |no |query |none |Adult content filter. Valid values: <ul><li>Off</li><li>Moderate</li><li>Strict</li></ul> |
| market |string |no |query |none |Market or region to narrow the search (example: en-US) |
| longitude |number |no |query |none |Longitude (east/west coordinate) to narrow the search (example: 47.603450) |
| latitude |number |no |query |none |Latitude (north/south coordinate) to narrow the search (example: -122.329696) |
| videoFilters |string |no |query |none |Filter search based on size, aspect, color, style, face or any combination thereof.  Valid values: <ul><li>Duration:Short</li><li>Duration:Medium</li><li>Duration:Long</li><li>Aspect:Standard</li><li>Aspect:Widescreen</li><li>Resolution:Low</li><li>Resolution:Medium</li><li>Resolution:High</li></ul> <br/><br/>For example: 'Duration:Short+Resolution:High' |
| videoSortBy |string |no |query |none |Sort order for results. Valid values: <ul><li>Date</li><li>Relevance</li></ul> <p>Date sort order implies descending.</p> |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="search-images"></a>Search images
Retrieves images from a Bing search.  
```GET: /Image```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| query |string |yes |query |none |Text to search for (example: 'xbox') |
| maxResult |integer |no |query |none |Maximum number of results to return |
| startOffset |integer |no |query |none |Number of results to skip |
| adultContent |string |no |query |none |Adult content filter. Valid values: <ul><li>Off</li><li>Moderate</li><li>Strict</li></ul> |
| market |string |no |query |none |Market or region to narrow the search (example: en-US) |
| longitude |number |no |query |none |Longitude (east/west coordinate) to narrow the search (example: 47.603450) |
| latitude |number |no |query |none |Latitude (north/south coordinate) to narrow the search (example: -122.329696) |
| imageFilters |string |no |query |none |Filter search based on size, aspect, color, style, face or any combination thereof. Valid values: <ul><li>Size:Small</li><li>Size:Medium</li><li>Size:Large</li><li>Size:Width:[Width]</li><li>Size:Height:[Height]</li><li>Aspect:Square</li><li>Aspect:Wide</li><li>Aspect:Tall</li><li>Color:Color</li><li>Color:Monochrome</li><li>Style:Photo</li><li>Style:Graphics</li><li>Face:Face</li><li>Face:Portrait</li><li>Face:Other</li></ul><br/><br/>For example: 'Size:Small+Aspect:Square' |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="search-news"></a>Search news
Retrieves news results from a Bing search.  
```GET: /News```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| query |string |yes |query |none |Text to search for (example: 'xbox') |
| maxResult |integer |no |query |none |Maximum number of results to return |
| startOffset |integer |no |query |none |Number of results to skip |
| adultContent |string |no |query |none |Adult content filter. Valid values: <ul><li>Off</li><li>Moderate</li><li>Strict</li></ul> |
| market |string |no |query |none |Market or region to narrow the search (example: en-US) |
| longitude |number |no |query |none |Longitude (east/west coordinate) to narrow the search (example: 47.603450) |
| latitude |number |no |query |none |Latitude (north/south coordinate) to narrow the search (example: -122.329696) |
| newsSortBy |string |no |query |none |Sort order for results. Valid values: <ul><li>Date</li><li>Relevance</li></ul> <p>Date sort order implies descending.</p> |
| newsCategory |string |no |query | |Category of news to narrow the search (example: 'rt_Business') |
| newsLocationOverride |string |no |query |none |Override for Bing location detection. This parameter is only applicable in en-US market. The format for input is US./<state /> (example: 'US.WA') |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="search-spellings"></a>Search spellings
Retrieves spelling suggestions.  
```GET: /SpellingSuggestions```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| query |string |yes |query |none |Text to search for (example: 'xbox') |
| maxResult |integer |no |query |none |Maximum number of results to return |
| startOffset |integer |no |query |none |Number of results to skip |
| adultContent |string |no |query |none |Adult content filter. Valid values: <ul><li>Off</li><li>Moderate</li><li>Strict</li></ul> |
| market |string |no |query |none |Market or region to narrow the search (example: en-US) |
| longitude |number |no |query |none |Longitude (east/west coordinate) to narrow the search (example: 47.603450) |
| latitude |number |no |query |none |Latitude (north/south coordinate) to narrow the search (example: -122.329696) |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="search-related"></a>Search related
Retrieves related search results from a Bing search.  
```GET: /RelatedSearch```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| query |string |yes |query |none |Text to search for (example: 'xbox') |
| maxResult |integer |no |query |none |Maximum number of results to return |
| startOffset |integer |no |query |none |Number of results to skip |
| adultContent |string |no |query |none |Adult content filter. Valid values: <ul><li>Off</li><li>Moderate</li><li>Strict</li></ul> |
| market |string |no |query |none |Market or region to narrow the search (example: en-US) |
| longitude |number |no |query |none |Longitude (east/west coordinate) to narrow the search (example: 47.603450) |
| latitude |number |no |query |none |Latitude (north/south coordinate) to narrow the search (example: -122.329696) |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

### <a name="search-all"></a>Search all
Retrieves all web sites, videos, images, etc. from a Bing search.  
```GET: /CompositeSearch```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| query |string |yes |query |none |Text to search for (example: 'xbox') |
| maxResult |integer |no |query |none |Maximum number of results to return |
| startOffset |integer |no |query |none |Number of results to skip |
| adultContent |string |no |query |none |Adult content filter. Valid values: <ul><li>Off</li><li>Moderate</li><li>Strict</li></ul> |
| market |string |no |query |none |Market or region to narrow the search (example: en-US) |
| longitude |number |no |query |none |Longitude (east/west coordinate) to narrow the search (example: 47.603450) |
| latitude |number |no |query |none |Latitude (north/south coordinate) to narrow the search (example: -122.329696) |
| webFileType |string |no |query |none |File type to narrow the search (example: 'DOC') |
| videoFilters |string |no |query |none |Filter search based on size, aspect, color, style, face or any combination thereof.  Valid values: <ul><li>Duration:Short</li><li>Duration:Medium</li><li>Duration:Long</li><li>Aspect:Standard</li><li>Aspect:Widescreen</li><li>Resolution:Low</li><li>Resolution:Medium</li><li>Resolution:High</li></ul> <br/><br/>For example: 'Duration:Short+Resolution:High' |
| videoSortBy |string |no |query |none |Sort order for results. Valid values: <ul><li>Date</li><li>Relevance</li></ul> <p>Date sort order implies descending.</p> |
| imageFilters |string |no |query |none |Filter search based on size, aspect, color, style, face or any combination thereof. Valid values: <ul><li>Size:Small</li><li>Size:Medium</li><li>Size:Large</li><li>Size:Width:[Width]</li><li>Size:Height:[Height]</li><li>Aspect:Square</li><li>Aspect:Wide</li><li>Aspect:Tall</li><li>Color:Color</li><li>Color:Monochrome</li><li>Style:Photo</li><li>Style:Graphics</li><li>Face:Face</li><li>Face:Portrait</li><li>Face:Other</li></ul><br/><br/>For example: 'Size:Small+Aspect:Square' |
| newsSortBy |string |no |query |none |Sort order for results. Valid values: <ul><li>Date</li><li>Relevance</li></ul> <p>Date sort order implies descending.</p> |
| newsCategory |string |no |query |none |Category of news to narrow the search (example: 'rt_Business') |
| newsLocationOverride |string |no |query |none |Override for Bing location detection. This parameter is only applicable in en-US market. The format for input is US./<state /> (example: 'US.WA') |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="object-definitions"></a>Object definitions
#### <a name="webresultmodel-bing-web-search-results"></a>WebResultModel: Bing web search results
| Property Name | Data Type | Required |
| --- | --- | --- |
| Title |string |no |
| Description |string |no |
| DisplayUrl |string |no |
| Id |string |no |
| FullUrl |string |no |

#### <a name="videoresultmodel-bing-video-search-results"></a>VideoResultModel: Bing video search results
| Property Name | Data Type | Required |
| --- | --- | --- |
| Title |string |no |
| DisplayUrl |string |no |
| Id |string |no |
| MediaUrl |string |no |
| Runtime |integer |no |
| Thumbnail |not defined |no |

#### <a name="thumbnailmodel-thumbnail-properties-of-the-multimedia-element"></a>ThumbnailModel: Thumbnail properties of the multimedia element
| Property Name | Data Type | Required |
| --- | --- | --- |
| MediaUrl |string |no |
| ContentType |string |no |
| Width |integer |no |
| Height |integer |no |
| FileSize |integer |no |

#### <a name="imageresultmodel-bing-image-search-results"></a>ImageResultModel: Bing image search results
| Property Name | Data Type | Required |
| --- | --- | --- |
| Title |string |no |
| DisplayUrl |string |no |
| Id |string |no |
| MediaUrl |string |no |
| SourceUrl |string |no |
| Thumbnail |not defined |no |

#### <a name="newsresultmodel-bing-news-search-results"></a>NewsResultModel: Bing news search results
| Property Name | Data Type | Required |
| --- | --- | --- |
| Title |string |no |
| Description |string |no |
| DisplayUrl |string |no |
| Id |string |no |
| Source |string |no |
| Date |string |no |

#### <a name="spellresultmodel-bing-spelling-suggestions-results"></a>SpellResultModel: Bing spelling suggestions results
| Property Name | Data Type | Required |
| --- | --- | --- |
| Id |string |no |
| Value |string |no |

#### <a name="relatedsearchresultmodel-bing-related-search-results"></a>RelatedSearchResultModel: Bing related search results
| Property Name | Data Type | Required |
| --- | --- | --- |
| Title |string |no |
| Id |string |no |
| BingUrl |string |no |

#### <a name="compositesearchresultmodel-bing-composite-search-results"></a>CompositeSearchResultModel: Bing composite search results
| Property Name | Data Type | Required |
| --- | --- | --- |
| WebResultsTotal |integer |no |
| ImageResultsTotal |integer |no |
| VideoResultsTotal |integer |no |
| NewsResultsTotal |integer |no |
| SpellSuggestionsTotal |integer |no |
| WebResults |array |no |
| ImageResults |array |no |
| VideoResults |array |no |
| NewsResults |array |no |
| SpellSuggestionResults |array |no |
| RelatedSearchResults |array |no |

## <a name="next-steps"></a>Next steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

Go back to the [APIs list](apis-list.md).

