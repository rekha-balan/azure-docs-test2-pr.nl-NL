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
# <a name="show-search-results-on-the-map"></a><span data-ttu-id="ef329-103">Show search results on the map</span><span class="sxs-lookup"><span data-stu-id="ef329-103">Show search results on the map</span></span>

<span data-ttu-id="ef329-104">This article shows you how to search for location of interest and show the search results on the map.</span><span class="sxs-lookup"><span data-stu-id="ef329-104">This article shows you how to search for location of interest and show the search results on the map.</span></span> 

<span data-ttu-id="ef329-105">There are two ways to search for a location of interest, one way is by using a service module to make a search request and the other is by making a search request through a [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Fuzzy search API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy).</span><span class="sxs-lookup"><span data-stu-id="ef329-105">There are two ways to search for a location of interest, one way is by using a service module to make a search request and the other is by making a search request through a [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Fuzzy search API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy).</span></span> <span data-ttu-id="ef329-106">We discuss both below.</span><span class="sxs-lookup"><span data-stu-id="ef329-106">We discuss both below.</span></span>

## <a name="making-a-search-request-via-service-module"></a><span data-ttu-id="ef329-107">Making a search request via service module</span><span class="sxs-lookup"><span data-stu-id="ef329-107">Making a search request via service module</span></span>

### <a name="understand-the-code"></a><span data-ttu-id="ef329-108">Understand the code</span><span class="sxs-lookup"><span data-stu-id="ef329-108">Understand the code</span></span>

<iframe height='500' scrolling='no' title='<span data-ttu-id="ef329-109">Show search results on a map (Service Module)</span><span class="sxs-lookup"><span data-stu-id="ef329-109">Show search results on a map (Service Module)</span></span>' src='//codepen.io/azuremaps/embed/zLdYEB/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="ef329-110">See the Pen <a href='https://codepen.io/azuremaps/pen/zLdYEB/'>Show search results on a map (Service Module)</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="ef329-110">See the Pen <a href='https://codepen.io/azuremaps/pen/zLdYEB/'>Show search results on a map (Service Module)</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="ef329-111">In the code above, the first block of code constructs a map object and instantiates a client service.</span><span class="sxs-lookup"><span data-stu-id="ef329-111">In the code above, the first block of code constructs a map object and instantiates a client service.</span></span> <span data-ttu-id="ef329-112">You can see [create a map](./map-create.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="ef329-112">You can see [create a map](./map-create.md) for instructions.</span></span>

<span data-ttu-id="ef329-113">The second block of code uses Fuzzy search [Azure Maps Fuzzy Search API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy) to search for point of interest.</span><span class="sxs-lookup"><span data-stu-id="ef329-113">The second block of code uses Fuzzy search [Azure Maps Fuzzy Search API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy) to search for point of interest.</span></span> <span data-ttu-id="ef329-114">Fuzzy search API can handle any combination of fuzzy inputs.</span><span class="sxs-lookup"><span data-stu-id="ef329-114">Fuzzy search API can handle any combination of fuzzy inputs.</span></span> <span data-ttu-id="ef329-115">The response from the fuzzy search service is then parsed into GeoJSON format using the [getGeoJsonSearchResponse](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonsearchresponse?view=azure-iot-typescript-latest#geojsonsearchresponse) method.</span><span class="sxs-lookup"><span data-stu-id="ef329-115">The response from the fuzzy search service is then parsed into GeoJSON format using the [getGeoJsonSearchResponse](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonsearchresponse?view=azure-iot-typescript-latest#geojsonsearchresponse) method.</span></span> <span data-ttu-id="ef329-116">The pins are then added to the map to show the points of interest on the map.</span><span class="sxs-lookup"><span data-stu-id="ef329-116">The pins are then added to the map to show the points of interest on the map.</span></span>

<span data-ttu-id="ef329-117">The last block of code adjusts the camera bounds for the map by using the Map's [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraboundsoptions?view=azure-iot-typescript-latest) property.</span><span class="sxs-lookup"><span data-stu-id="ef329-117">The last block of code adjusts the camera bounds for the map by using the Map's [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraboundsoptions?view=azure-iot-typescript-latest) property.</span></span>


##  <a name="making-a-search-request-via-xmlhttprequest"></a><span data-ttu-id="ef329-118">Making a search request via XMLHttpRequest</span><span class="sxs-lookup"><span data-stu-id="ef329-118">Making a search request via XMLHttpRequest</span></span>

### <a name="understand-the-code"></a><span data-ttu-id="ef329-119">Understand the code</span><span class="sxs-lookup"><span data-stu-id="ef329-119">Understand the code</span></span>

<iframe height='500' scrolling='no' title='<span data-ttu-id="ef329-120">Show search results on a map</span><span class="sxs-lookup"><span data-stu-id="ef329-120">Show search results on a map</span></span>' src='//codepen.io/azuremaps/embed/KQbaeM/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="ef329-121">See the Pen <a href='https://codepen.io/azuremaps/pen/KQbaeM/'>Show search results on a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="ef329-121">See the Pen <a href='https://codepen.io/azuremaps/pen/KQbaeM/'>Show search results on a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="ef329-122">In the code above, the first block of code constructs a map object.</span><span class="sxs-lookup"><span data-stu-id="ef329-122">In the code above, the first block of code constructs a map object.</span></span> <span data-ttu-id="ef329-123">You can see [create a map](./map-create.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="ef329-123">You can see [create a map](./map-create.md) for instructions.</span></span>

<span data-ttu-id="ef329-124">The second code block adds search results layer to the map.</span><span class="sxs-lookup"><span data-stu-id="ef329-124">The second code block adds search results layer to the map.</span></span> <span data-ttu-id="ef329-125">The search results layer will display the search results as pins on the map.</span><span class="sxs-lookup"><span data-stu-id="ef329-125">The search results layer will display the search results as pins on the map.</span></span>

<span data-ttu-id="ef329-126">The third block of code sends an [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Fuzzy search API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy) to search for the point of interest.</span><span class="sxs-lookup"><span data-stu-id="ef329-126">The third block of code sends an [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Fuzzy search API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy) to search for the point of interest.</span></span> <span data-ttu-id="ef329-127">Fuzzy search API can handle any combination of fuzzy inputs.</span><span class="sxs-lookup"><span data-stu-id="ef329-127">Fuzzy search API can handle any combination of fuzzy inputs.</span></span>

<span data-ttu-id="ef329-128">The last block of code parses the response and adjusts the adjusts the camera bounds for the map by using the Map's [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraboundsoptions?view=azure-iot-typescript-latest) to render the result pins.</span><span class="sxs-lookup"><span data-stu-id="ef329-128">The last block of code parses the response and adjusts the adjusts the camera bounds for the map by using the Map's [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraboundsoptions?view=azure-iot-typescript-latest) to render the result pins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef329-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef329-129">Next steps</span></span>

<span data-ttu-id="ef329-130">Learn more about the classes and methods used in this article:</span><span class="sxs-lookup"><span data-stu-id="ef329-130">Learn more about the classes and methods used in this article:</span></span> 

* [<span data-ttu-id="ef329-131">Azure Maps Fuzzy Search API</span><span class="sxs-lookup"><span data-stu-id="ef329-131">Azure Maps Fuzzy Search API</span></span>](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy)
* [<span data-ttu-id="ef329-132">Map</span><span class="sxs-lookup"><span data-stu-id="ef329-132">Map</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="ef329-133">addPins</span><span class="sxs-lookup"><span data-stu-id="ef329-133">addPins</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addpins)
    
<span data-ttu-id="ef329-134">For more code examples to add to your maps, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="ef329-134">For more code examples to add to your maps, see the following articles:</span></span> 
* [<span data-ttu-id="ef329-135">Get information from a coordinate</span><span class="sxs-lookup"><span data-stu-id="ef329-135">Get information from a coordinate</span></span>](./map-get-information-from-coordinate.md)
* [<span data-ttu-id="ef329-136">Show directions from A to B</span><span class="sxs-lookup"><span data-stu-id="ef329-136">Show directions from A to B</span></span>](./map-route.md)
