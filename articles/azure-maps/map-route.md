---
title: Show directions with Azure Maps | Microsoft Docs
description: How to display directions between two locations on a Javascript map
author: jingjing-z
ms.author: jinzh
ms.date: 09/07/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.custom: codepen
ms.openlocfilehash: cb0d5d7239095b67235cc68233d9492377178362
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969382"
---
# <a name="show-directions-from-a-to-b"></a><span data-ttu-id="7a105-103">Show directions from A to B</span><span class="sxs-lookup"><span data-stu-id="7a105-103">Show directions from A to B</span></span> 

<span data-ttu-id="7a105-104">This article shows you how to make a route request and show the route on the map.</span><span class="sxs-lookup"><span data-stu-id="7a105-104">This article shows you how to make a route request and show the route on the map.</span></span>

<span data-ttu-id="7a105-105">There are two ways to do so, one way is by querying the [Azure Maps Route API](https://docs.microsoft.com/rest/api/maps/route/getroutedirections) through a service module and the other is by making an [XMLHttpRequest](https://xhr.spec.whatwg.org/) to the API.</span><span class="sxs-lookup"><span data-stu-id="7a105-105">There are two ways to do so, one way is by querying the [Azure Maps Route API](https://docs.microsoft.com/rest/api/maps/route/getroutedirections) through a service module and the other is by making an [XMLHttpRequest](https://xhr.spec.whatwg.org/) to the API.</span></span> <span data-ttu-id="7a105-106">Both are discussed below.</span><span class="sxs-lookup"><span data-stu-id="7a105-106">Both are discussed below.</span></span>

## <a name="querying-the-route-via-service-module"></a><span data-ttu-id="7a105-107">Querying the route via service module</span><span class="sxs-lookup"><span data-stu-id="7a105-107">Querying the route via service module</span></span>

## <a name="understand-the-code"></a><span data-ttu-id="7a105-108">Understand the code</span><span class="sxs-lookup"><span data-stu-id="7a105-108">Understand the code</span></span>

<iframe height='500' scrolling='no' title='<span data-ttu-id="7a105-109">Show directions from A to B on a map (Service Module)</span><span class="sxs-lookup"><span data-stu-id="7a105-109">Show directions from A to B on a map (Service Module)</span></span>' src='//codepen.io/azuremaps/embed/RBZbep/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="7a105-110">See the Pen <a href='https://codepen.io/azuremaps/pen/RBZbep/'>Show directions from A to B on a map (Service Module)</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="7a105-110">See the Pen <a href='https://codepen.io/azuremaps/pen/RBZbep/'>Show directions from A to B on a map (Service Module)</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="7a105-111">In the code above, the first block of code constructs a map object.</span><span class="sxs-lookup"><span data-stu-id="7a105-111">In the code above, the first block of code constructs a map object.</span></span> <span data-ttu-id="7a105-112">You can see [create a map](./map-create.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="7a105-112">You can see [create a map](./map-create.md) for instructions.</span></span>

<span data-ttu-id="7a105-113">The line in the second block of code instantiates a service client.</span><span class="sxs-lookup"><span data-stu-id="7a105-113">The line in the second block of code instantiates a service client.</span></span>

<span data-ttu-id="7a105-114">The third code block initializes the [line String Layer](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addlinestrings) on the map.</span><span class="sxs-lookup"><span data-stu-id="7a105-114">The third code block initializes the [line String Layer](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addlinestrings) on the map.</span></span>

<span data-ttu-id="7a105-115">The fourth block of code creates and adds pins on the map to represent the start and end point of the route.</span><span class="sxs-lookup"><span data-stu-id="7a105-115">The fourth block of code creates and adds pins on the map to represent the start and end point of the route.</span></span> <span data-ttu-id="7a105-116">You can see [add a pin on the map](map-add-pin.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="7a105-116">You can see [add a pin on the map](map-add-pin.md) for instructions.</span></span>

<span data-ttu-id="7a105-117">The next block of code uses [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamerabounds) function of the map class to set the bounding box of the map based on the start and end point of the route.</span><span class="sxs-lookup"><span data-stu-id="7a105-117">The next block of code uses [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamerabounds) function of the map class to set the bounding box of the map based on the start and end point of the route.</span></span>

<span data-ttu-id="7a105-118">The sixth code block constructs a route query.</span><span class="sxs-lookup"><span data-stu-id="7a105-118">The sixth code block constructs a route query.</span></span>

<span data-ttu-id="7a105-119">The last block of code queries the Azure Maps routing service through the [getRouteDirections](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.route?view=azure-iot-typescript-latest#getroutedirections) method to get a route between the start and destination point.</span><span class="sxs-lookup"><span data-stu-id="7a105-119">The last block of code queries the Azure Maps routing service through the [getRouteDirections](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.route?view=azure-iot-typescript-latest#getroutedirections) method to get a route between the start and destination point.</span></span> <span data-ttu-id="7a105-120">The response is then parsed into GeoJSON format using the [getGeoJsonRoutes](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonroutedirectionsresponse?view=azure-iot-typescript-latest#getgeojsonroutes) method.</span><span class="sxs-lookup"><span data-stu-id="7a105-120">The response is then parsed into GeoJSON format using the [getGeoJsonRoutes](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonroutedirectionsresponse?view=azure-iot-typescript-latest#getgeojsonroutes) method.</span></span> <span data-ttu-id="7a105-121">It adds all those lines onto the map to render the route.</span><span class="sxs-lookup"><span data-stu-id="7a105-121">It adds all those lines onto the map to render the route.</span></span> <span data-ttu-id="7a105-122">You can see [add a line on the map](./map-add-shape.md#addALine) for more information.</span><span class="sxs-lookup"><span data-stu-id="7a105-122">You can see [add a line on the map](./map-add-shape.md#addALine) for more information.</span></span>

## <a name="querying-the-route-via-xmlhttprequest"></a><span data-ttu-id="7a105-123">Querying the route via XMLHttpRequest</span><span class="sxs-lookup"><span data-stu-id="7a105-123">Querying the route via XMLHttpRequest</span></span>

## <a name="understand-the-code"></a><span data-ttu-id="7a105-124">Understand the code</span><span class="sxs-lookup"><span data-stu-id="7a105-124">Understand the code</span></span>

<iframe height='500' scrolling='no' title='<span data-ttu-id="7a105-125">Show directions from A to B on a map</span><span class="sxs-lookup"><span data-stu-id="7a105-125">Show directions from A to B on a map</span></span>' src='//codepen.io/azuremaps/embed/zRyNmP/?height=469&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="7a105-126">See the Pen <a href='https://codepen.io/azuremaps/pen/zRyNmP/'>Show directions from A to B on a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="7a105-126">See the Pen <a href='https://codepen.io/azuremaps/pen/zRyNmP/'>Show directions from A to B on a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="7a105-127">In the code above, the first block of code constructs a map object.</span><span class="sxs-lookup"><span data-stu-id="7a105-127">In the code above, the first block of code constructs a map object.</span></span> <span data-ttu-id="7a105-128">You can see [create a map](./map-create.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="7a105-128">You can see [create a map](./map-create.md) for instructions.</span></span>

<span data-ttu-id="7a105-129">The second block of code creates and adds pins on the map to represent the start and end point of the route.</span><span class="sxs-lookup"><span data-stu-id="7a105-129">The second block of code creates and adds pins on the map to represent the start and end point of the route.</span></span> <span data-ttu-id="7a105-130">You can see [add a pin on the map](map-add-pin.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="7a105-130">You can see [add a pin on the map](map-add-pin.md) for instructions.</span></span>

<span data-ttu-id="7a105-131">The third block of code uses [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamerabounds) function of the map class to set the bounding box of the map based on the start and end point of the route.</span><span class="sxs-lookup"><span data-stu-id="7a105-131">The third block of code uses [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamerabounds) function of the map class to set the bounding box of the map based on the start and end point of the route.</span></span>

<span data-ttu-id="7a105-132">The fourth block of code sends an [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Route API](https://docs.microsoft.com/rest/api/maps/route/getroutedirections).</span><span class="sxs-lookup"><span data-stu-id="7a105-132">The fourth block of code sends an [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Route API](https://docs.microsoft.com/rest/api/maps/route/getroutedirections).</span></span>

<span data-ttu-id="7a105-133">The last block of code parses the incoming response.</span><span class="sxs-lookup"><span data-stu-id="7a105-133">The last block of code parses the incoming response.</span></span> <span data-ttu-id="7a105-134">For a successful response, it collects the latitude and longitude information for each waypoint.</span><span class="sxs-lookup"><span data-stu-id="7a105-134">For a successful response, it collects the latitude and longitude information for each waypoint.</span></span> <span data-ttu-id="7a105-135">It creates an array of lines by connecting each waypoint to its subsequent waypoint.</span><span class="sxs-lookup"><span data-stu-id="7a105-135">It creates an array of lines by connecting each waypoint to its subsequent waypoint.</span></span> <span data-ttu-id="7a105-136">It adds all those lines onto the map to render the route.</span><span class="sxs-lookup"><span data-stu-id="7a105-136">It adds all those lines onto the map to render the route.</span></span> <span data-ttu-id="7a105-137">You can see [add a line on the map](./map-add-shape.md#addALine) for instructions.</span><span class="sxs-lookup"><span data-stu-id="7a105-137">You can see [add a line on the map](./map-add-shape.md#addALine) for instructions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a105-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a105-138">Next steps</span></span>

<span data-ttu-id="7a105-139">Learn more about the classes and methods used in this article:</span><span class="sxs-lookup"><span data-stu-id="7a105-139">Learn more about the classes and methods used in this article:</span></span> 

* [<span data-ttu-id="7a105-140">getRouteDirections</span><span class="sxs-lookup"><span data-stu-id="7a105-140">getRouteDirections</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.route?view=azure-iot-typescript-latest#getroutedirections)
* [<span data-ttu-id="7a105-141">getGeoJsonRoutes</span><span class="sxs-lookup"><span data-stu-id="7a105-141">getGeoJsonRoutes</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonroutedirectionsresponse?view=azure-iot-typescript-latest#getgeojsonroutes)
* [<span data-ttu-id="7a105-142">Line String Layer</span><span class="sxs-lookup"><span data-stu-id="7a105-142">Line String Layer</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addlinestrings)
* [<span data-ttu-id="7a105-143">Map</span><span class="sxs-lookup"><span data-stu-id="7a105-143">Map</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="7a105-144">setCameraBounds</span><span class="sxs-lookup"><span data-stu-id="7a105-144">setCameraBounds</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamerabounds)
    * [<span data-ttu-id="7a105-145">addLinestrings</span><span class="sxs-lookup"><span data-stu-id="7a105-145">addLinestrings</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addlinestrings)
    * [<span data-ttu-id="7a105-146">addPins</span><span class="sxs-lookup"><span data-stu-id="7a105-146">addPins</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addpins)

<span data-ttu-id="7a105-147">For more code examples to add to your maps, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="7a105-147">For more code examples to add to your maps, see the following articles:</span></span> 
* [<span data-ttu-id="7a105-148">Show traffic on the map</span><span class="sxs-lookup"><span data-stu-id="7a105-148">Show traffic on the map</span></span>](./map-show-traffic.md)
* [<span data-ttu-id="7a105-149">Interacting with the map - mouse events</span><span class="sxs-lookup"><span data-stu-id="7a105-149">Interacting with the map - mouse events</span></span>](./map-events.md)
