---
title: Show search results with Azure Maps | Microsoft Docs
description: How to perform a search request with Azure Maps then display the results on a Javascript map
author: jingjing-z
ms.author: jinzh
ms.date: 09/07/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.custom: codepen
ms.openlocfilehash: b324d0a68fde8f47072a087330f2e40a99378984
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864655"
---
# <a name="show-search-results-on-the-map"></a>Show search results on the map

This article shows you how to search for location of interest and show the search results on the map. 

There are two ways to search for a location of interest, one way is by using a service module to make a search request and the other is by making a search request through a [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Fuzzy search API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy). We discuss both below.

## <a name="making-a-search-request-via-service-module"></a>Making a search request via service module

### <a name="understand-the-code"></a>Understand the code

<iframe height='500' scrolling='no' title='Show search results on a map (Service Module)' src='//codepen.io/azuremaps/embed/zLdYEB/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/azuremaps/pen/zLdYEB/'>Show search results on a map (Service Module)</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

In the code above, the first block of code constructs a map object and instantiates a client service. You can see [create a map](./map-create.md) for instructions.

The second block of code uses Fuzzy search [Azure Maps Fuzzy Search API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy) to search for point of interest. Fuzzy search API can handle any combination of fuzzy inputs. The response from the fuzzy search service is then parsed into GeoJSON format using the [getGeoJsonSearchResponse](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonsearchresponse?view=azure-iot-typescript-latest#geojsonsearchresponse) method. The pins are then added to the map to show the points of interest on the map.

The last block of code adjusts the camera bounds for the map by using the Map's [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraboundsoptions?view=azure-iot-typescript-latest) property.


##  <a name="making-a-search-request-via-xmlhttprequest"></a>Making a search request via XMLHttpRequest

### <a name="understand-the-code"></a>Understand the code

<iframe height='500' scrolling='no' title='Show search results on a map' src='//codepen.io/azuremaps/embed/KQbaeM/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/azuremaps/pen/KQbaeM/'>Show search results on a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

In the code above, the first block of code constructs a map object. You can see [create a map](./map-create.md) for instructions.

The second code block adds search results layer to the map. The search results layer will display the search results as pins on the map.

The third block of code sends an [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Fuzzy search API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy) to search for the point of interest. Fuzzy search API can handle any combination of fuzzy inputs.

The last block of code parses the response and adjusts the adjusts the camera bounds for the map by using the Map's [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraboundsoptions?view=azure-iot-typescript-latest) to render the result pins.

## <a name="next-steps"></a>Next steps

Learn more about the classes and methods used in this article: 

* [Azure Maps Fuzzy Search API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy)
* [Map](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [addPins](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addpins)
    
For more code examples to add to your maps, see the following articles: 
* [Get information from a coordinate](./map-get-information-from-coordinate.md)
* [Show directions from A to B](./map-route.md)
