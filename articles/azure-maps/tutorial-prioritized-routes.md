---
title: Multiple routes with Azure Maps | Microsoft Docs
description: Find routes for different modes of travel using Azure Maps
author: dsk-2015
ms.author: dkshir
ms.date: 09/05/2018
ms.topic: tutorial
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: 72bb0f238b77f00799129493df7443842e57b6fa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857910"
---
# <a name="find-routes-for-different-modes-of-travel-using-azure-maps"></a><span data-ttu-id="6153e-103">Find routes for different modes of travel using Azure Maps</span><span class="sxs-lookup"><span data-stu-id="6153e-103">Find routes for different modes of travel using Azure Maps</span></span>

<span data-ttu-id="6153e-104">This tutorial shows how to use your Azure Maps account and the route service to find the route to your point of interest, prioritized by your mode of travel.</span><span class="sxs-lookup"><span data-stu-id="6153e-104">This tutorial shows how to use your Azure Maps account and the route service to find the route to your point of interest, prioritized by your mode of travel.</span></span> <span data-ttu-id="6153e-105">You display two different routes on your map, one for cars and one for trucks that may have route restrictions because of height, weight, or hazardous cargo.</span><span class="sxs-lookup"><span data-stu-id="6153e-105">You display two different routes on your map, one for cars and one for trucks that may have route restrictions because of height, weight, or hazardous cargo.</span></span> <span data-ttu-id="6153e-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="6153e-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6153e-107">Create a new web page using the map control API</span><span class="sxs-lookup"><span data-stu-id="6153e-107">Create a new web page using the map control API</span></span>
> * <span data-ttu-id="6153e-108">Visualize traffic flow on your map</span><span class="sxs-lookup"><span data-stu-id="6153e-108">Visualize traffic flow on your map</span></span>
> * <span data-ttu-id="6153e-109">Create route queries that declare mode of travel</span><span class="sxs-lookup"><span data-stu-id="6153e-109">Create route queries that declare mode of travel</span></span>
> * <span data-ttu-id="6153e-110">Display multiple routes on your map</span><span class="sxs-lookup"><span data-stu-id="6153e-110">Display multiple routes on your map</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6153e-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6153e-111">Prerequisites</span></span>

<span data-ttu-id="6153e-112">Before you proceed, follow the steps in the first tutorial to [create your Azure Maps account](./tutorial-search-location.md#createaccount), and [get the subscription key for your account](./tutorial-search-location.md#getkey).</span><span class="sxs-lookup"><span data-stu-id="6153e-112">Before you proceed, follow the steps in the first tutorial to [create your Azure Maps account](./tutorial-search-location.md#createaccount), and [get the subscription key for your account](./tutorial-search-location.md#getkey).</span></span>


## <a name="create-a-new-map"></a><span data-ttu-id="6153e-113">Create a new map</span><span class="sxs-lookup"><span data-stu-id="6153e-113">Create a new map</span></span> 
<span data-ttu-id="6153e-114">The following steps show you how to create a static HTML page embedded with the Map Control API.</span><span class="sxs-lookup"><span data-stu-id="6153e-114">The following steps show you how to create a static HTML page embedded with the Map Control API.</span></span>

1. <span data-ttu-id="6153e-115">On your local machine, create a new file and name it **MapTruckRoute.html**.</span><span class="sxs-lookup"><span data-stu-id="6153e-115">On your local machine, create a new file and name it **MapTruckRoute.html**.</span></span>
2. <span data-ttu-id="6153e-116">Add the following HTML components to the file:</span><span class="sxs-lookup"><span data-stu-id="6153e-116">Add the following HTML components to the file:</span></span>

    ```HTML
    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, user-scalable=no" />
        <title>Map Truck Route</title>
        <link rel="stylesheet" href="https://atlas.microsoft.com/sdk/css/atlas.min.css?api-version=1" type="text/css" /> 
        <script src="https://atlas.microsoft.com/sdk/js/atlas.min.js?api-version=1"></script> 
        <script src="https://atlas.microsoft.com/sdk/js/atlas-service.min.js?api-version=1"></script> 
        <style>
            html,
            body {
                width: 100%;
                height: 100%;
                padding: 0;
                margin: 0;
            }

            #map {
                width: 100%;
                height: 100%;
            }
        </style>
    </head>
    
    <body>
        <div id="map"></div>
        <script>
            // Embed Map Control JavaScript code here
        </script>
    </body>

    </html>
    ```
    <span data-ttu-id="6153e-117">The HTML header embeds the resource locations for CSS and JavaScript files for the Azure Maps library.</span><span class="sxs-lookup"><span data-stu-id="6153e-117">The HTML header embeds the resource locations for CSS and JavaScript files for the Azure Maps library.</span></span> <span data-ttu-id="6153e-118">The *script* segment in the body of the HTML will contain the inline JavaScript code for the map.</span><span class="sxs-lookup"><span data-stu-id="6153e-118">The *script* segment in the body of the HTML will contain the inline JavaScript code for the map.</span></span>
3. <span data-ttu-id="6153e-119">Add the following JavaScript code to the *script* block of the HTML file.</span><span class="sxs-lookup"><span data-stu-id="6153e-119">Add the following JavaScript code to the *script* block of the HTML file.</span></span> <span data-ttu-id="6153e-120">Replace the string **\<your account key\>** with the primary key that you copied from your Maps account.</span><span class="sxs-lookup"><span data-stu-id="6153e-120">Replace the string **\<your account key\>** with the primary key that you copied from your Maps account.</span></span>

    ```JavaScript
    // Instantiate map to the div with id "map"
    var MapsAccountKey = "<your account key>";
    var map = new atlas.Map("map", {
        "subscription-key": MapsAccountKey
         center: [-118.2437, 34.0522], 
         zoom: 12 
    });
    ```
    <span data-ttu-id="6153e-121">The **atlas.Map** provides the control for a visual and interactive web map, and is a component of the Azure Map Control API.</span><span class="sxs-lookup"><span data-stu-id="6153e-121">The **atlas.Map** provides the control for a visual and interactive web map, and is a component of the Azure Map Control API.</span></span>

4. <span data-ttu-id="6153e-122">Save the file and open it in your browser.</span><span class="sxs-lookup"><span data-stu-id="6153e-122">Save the file and open it in your browser.</span></span> <span data-ttu-id="6153e-123">At this point, you have a basic map that you can develop further.</span><span class="sxs-lookup"><span data-stu-id="6153e-123">At this point, you have a basic map that you can develop further.</span></span> 

   ![View basic map](./media/tutorial-prioritized-routes/basic-map.png)

## <a name="visualize-traffic-flow"></a><span data-ttu-id="6153e-125">Visualize traffic flow</span><span class="sxs-lookup"><span data-stu-id="6153e-125">Visualize traffic flow</span></span>

1. <span data-ttu-id="6153e-126">If you don't tell the map where to focus, you see the whole world view.</span><span class="sxs-lookup"><span data-stu-id="6153e-126">If you don't tell the map where to focus, you see the whole world view.</span></span> <span data-ttu-id="6153e-127">To be able to view the traffic data, set a center point and a zoom level on your map.</span><span class="sxs-lookup"><span data-stu-id="6153e-127">To be able to view the traffic data, set a center point and a zoom level on your map.</span></span> <span data-ttu-id="6153e-128">Replace the code that declares a `new atlas.Map` with the following JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="6153e-128">Replace the code that declares a `new atlas.Map` with the following JavaScript code:</span></span> 
    
    ```JavaScript
    var map = new atlas.Map("map", {
        "subscription-key": MapsAccountKey,
        center: [-118.2437,34.0522],
        zoom: 12
    });
    ```

    <span data-ttu-id="6153e-129">This code sets the center point for the map, and declares a zoom level so that you can focus on a particular area by default.</span><span class="sxs-lookup"><span data-stu-id="6153e-129">This code sets the center point for the map, and declares a zoom level so that you can focus on a particular area by default.</span></span> 

1. <span data-ttu-id="6153e-130">Add the traffic flow display to the map:</span><span class="sxs-lookup"><span data-stu-id="6153e-130">Add the traffic flow display to the map:</span></span>

    ```JavaScript
    // Add Traffic Flow to the Map
    map.setTraffic({
        flow: "relative"
    });
    ```
    <span data-ttu-id="6153e-131">This code sets the traffic flow to `relative`, which is the speed of the road relative to free-flow.</span><span class="sxs-lookup"><span data-stu-id="6153e-131">This code sets the traffic flow to `relative`, which is the speed of the road relative to free-flow.</span></span> <span data-ttu-id="6153e-132">You could also set it to `absolute` speed of the road or `relative-delay`, which displays the relative speed where it differs from free-flow.</span><span class="sxs-lookup"><span data-stu-id="6153e-132">You could also set it to `absolute` speed of the road or `relative-delay`, which displays the relative speed where it differs from free-flow.</span></span> 

2. <span data-ttu-id="6153e-133">Save the **MapTruckRoute.html** file and refresh the page in your browser.</span><span class="sxs-lookup"><span data-stu-id="6153e-133">Save the **MapTruckRoute.html** file and refresh the page in your browser.</span></span> <span data-ttu-id="6153e-134">You should see the streets of Los Angeles with their current traffic data.</span><span class="sxs-lookup"><span data-stu-id="6153e-134">You should see the streets of Los Angeles with their current traffic data.</span></span>

   ![View traffic map](./media/tutorial-prioritized-routes/traffic-map.png)

<a id="queryroutes"></a>

## <a name="set-start-and-end-points"></a><span data-ttu-id="6153e-136">Set start and end points</span><span class="sxs-lookup"><span data-stu-id="6153e-136">Set start and end points</span></span>

<span data-ttu-id="6153e-137">For this tutorial, set the start point as a fictitious company in Seattle called Fabrikam, and the destination point as a Microsoft office.</span><span class="sxs-lookup"><span data-stu-id="6153e-137">For this tutorial, set the start point as a fictitious company in Seattle called Fabrikam, and the destination point as a Microsoft office.</span></span>

1. <span data-ttu-id="6153e-138">Add the following JavaScript code to create the pins for the start and end points of the route:</span><span class="sxs-lookup"><span data-stu-id="6153e-138">Add the following JavaScript code to create the pins for the start and end points of the route:</span></span>

    ```JavaScript
    // Create the GeoJSON objects which represent the start and end point of the route
    var startPoint = new atlas.data.Point([-122.356099, 47.580045]);
    var startPin = new atlas.data.Feature(startPoint, {
        title: "Fabrikam, Inc.",
        icon: "pin-round-blue"
    });

    var destinationPoint = new atlas.data.Point([-122.130137, 47.644702]);
    var destinationPin = new atlas.data.Feature(destinationPoint, {
        title: "Microsoft",
        icon: "pin-blue"
    });
    ```
    <span data-ttu-id="6153e-139">This code creates two [GeoJSON objects](https://en.wikipedia.org/wiki/GeoJSON) to represent the start and end points of the route.</span><span class="sxs-lookup"><span data-stu-id="6153e-139">This code creates two [GeoJSON objects](https://en.wikipedia.org/wiki/GeoJSON) to represent the start and end points of the route.</span></span>

2. <span data-ttu-id="6153e-140">Add the following JavaScript code to add the start and end points to the map:</span><span class="sxs-lookup"><span data-stu-id="6153e-140">Add the following JavaScript code to add the start and end points to the map:</span></span>

    ```JavaScript
    // Fit the map window to the bounding box defined by the start and destination points
    var swLon = Math.min(startPoint.coordinates[0], destinationPoint.coordinates[0]);
    var swLat = Math.min(startPoint.coordinates[1], destinationPoint.coordinates[1]);
    var neLon = Math.max(startPoint.coordinates[0], destinationPoint.coordinates[0]);
    var neLat = Math.max(startPoint.coordinates[1], destinationPoint.coordinates[1]);
    map.setCameraBounds({
        bounds: [swLon, swLat, neLon, neLat],
        padding: 100
    });

    // Add pins to the map for the start and end point of the route
    map.addPins([startPin, destinationPin], {
        name: "route-pins",
        textFont: "SegoeUi-Regular",
        textOffset: [0, -20]
    });
    ``` 
    <span data-ttu-id="6153e-141">The **map.setCameraBounds** call adjusts the map window according to the coordinates of the start and end points.</span><span class="sxs-lookup"><span data-stu-id="6153e-141">The **map.setCameraBounds** call adjusts the map window according to the coordinates of the start and end points.</span></span> <span data-ttu-id="6153e-142">The API **map.addPins** adds the points to the Map control as visual components.</span><span class="sxs-lookup"><span data-stu-id="6153e-142">The API **map.addPins** adds the points to the Map control as visual components.</span></span>

3. <span data-ttu-id="6153e-143">Save the file and refresh your browser to see the pins displayed on your map.</span><span class="sxs-lookup"><span data-stu-id="6153e-143">Save the file and refresh your browser to see the pins displayed on your map.</span></span> <span data-ttu-id="6153e-144">Even though you declared your map with a center point in Los Angeles, the **map.setCameraBounds** moved the view to display the start and end points.</span><span class="sxs-lookup"><span data-stu-id="6153e-144">Even though you declared your map with a center point in Los Angeles, the **map.setCameraBounds** moved the view to display the start and end points.</span></span> 

   ![View map with start and finish points](./media/tutorial-prioritized-routes/pins-map.png)


<a id="multipleroutes"></a>

## <a name="render-routes-prioritized-by-mode-of-travel"></a><span data-ttu-id="6153e-146">Render routes prioritized by mode of travel</span><span class="sxs-lookup"><span data-stu-id="6153e-146">Render routes prioritized by mode of travel</span></span>

<span data-ttu-id="6153e-147">This section shows how to use the Maps route service API to find multiple routes from a given start point to a destination based on your mode of transport.</span><span class="sxs-lookup"><span data-stu-id="6153e-147">This section shows how to use the Maps route service API to find multiple routes from a given start point to a destination based on your mode of transport.</span></span> <span data-ttu-id="6153e-148">The route service provides APIs to plan *fastest*, *shortest*, *eco*, or *thrilling* routes between two locations, considering the current traffic conditions.</span><span class="sxs-lookup"><span data-stu-id="6153e-148">The route service provides APIs to plan *fastest*, *shortest*, *eco*, or *thrilling* routes between two locations, considering the current traffic conditions.</span></span> <span data-ttu-id="6153e-149">It also allows users to plan routes in the future by using Azure's extensive historic traffic database and predicting route durations for any day and time.</span><span class="sxs-lookup"><span data-stu-id="6153e-149">It also allows users to plan routes in the future by using Azure's extensive historic traffic database and predicting route durations for any day and time.</span></span> <span data-ttu-id="6153e-150">For more information, see [Get route directions](https://docs.microsoft.com/rest/api/maps/route/getroutedirections).</span><span class="sxs-lookup"><span data-stu-id="6153e-150">For more information, see [Get route directions](https://docs.microsoft.com/rest/api/maps/route/getroutedirections).</span></span>


1. <span data-ttu-id="6153e-151">First, add a new layer on the map to display the route path, or *linestring*.</span><span class="sxs-lookup"><span data-stu-id="6153e-151">First, add a new layer on the map to display the route path, or *linestring*.</span></span> <span data-ttu-id="6153e-152">In this tutorial, there are two different routes, **car-route** and **truck-route**, each with their own styling.</span><span class="sxs-lookup"><span data-stu-id="6153e-152">In this tutorial, there are two different routes, **car-route** and **truck-route**, each with their own styling.</span></span> <span data-ttu-id="6153e-153">Add the following JavaScript code to the *script* block:</span><span class="sxs-lookup"><span data-stu-id="6153e-153">Add the following JavaScript code to the *script* block:</span></span>

    ```JavaScript
    // Place route layers on the map
    var carRouteLayerName = "car-route";
    map.addLinestrings([], {
        name: carRouteLayerName,
        color: "#B76DAB",
        width: 5,
        cap: "round",
        join: "round",
        before: "labels"
    });

    var truckRouteLayerName = "truck-route";
    map.addLinestrings([], {
        name: truckRouteLayerName,
        color: "#2272B9",
        width: 9,
        cap: "round",
        join: "round",
        before: carRouteLayerName
    });
    ```

2. <span data-ttu-id="6153e-154">Add the following JavaScript code to the *script* block, to request the route for a truck and display the results on the map:</span><span class="sxs-lookup"><span data-stu-id="6153e-154">Add the following JavaScript code to the *script* block, to request the route for a truck and display the results on the map:</span></span>

    ```JavaScript
    // Instantiate the service client  
        var client = new atlas.service.Client(MapsAccountKey); 
 
        // Construct the route query string 
        var routeQuery = startPoint.coordinates[1] + 
            "," + 
            startPoint.coordinates[0] + 
            ":" + 
            destinationPoint.coordinates[1] + 
            "," + 
            destinationPoint.coordinates[0]; 
 
        // Execute the truck route query then add the route to the map once a response is received  
        client.route.getRouteDirections(routeQuery, { 
            travelMode: "truck", 
            vehicleWidth: 2, 
            vehicleHeight: 2, 
            vehicleLength: 5, 
            vehicleLoadType: "USHazmatClass2" 
        }).then(response => { 
            // Parse the response into GeoJSON 
            var geoJsonResponse = new atlas.service.geojson.GeoJsonRouteDirectionsResponse(response); 
 
            // Get the first in the array of routes and add it to the map 
            map.addLinestrings([geoJsonResponse.getGeoJsonRoutes().features[0]], { 
                name: truckRouteLayerName 
            }); 
        }); 
    ```
    <span data-ttu-id="6153e-155">This code snippet above instantiates a service client, and constructs a route query string.</span><span class="sxs-lookup"><span data-stu-id="6153e-155">This code snippet above instantiates a service client, and constructs a route query string.</span></span> <span data-ttu-id="6153e-156">It then queries the Azure Maps routing service through the [getRouteDirections](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.route?view=azure-iot-typescript-latest#getroutedirections) method and then parses the response into GeoJSON format using the [getGeoJsonRouteDirectionsResponse](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonroutedirectionsresponse?view=azure-iot-typescript-latest).</span><span class="sxs-lookup"><span data-stu-id="6153e-156">It then queries the Azure Maps routing service through the [getRouteDirections](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.route?view=azure-iot-typescript-latest#getroutedirections) method and then parses the response into GeoJSON format using the [getGeoJsonRouteDirectionsResponse](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonroutedirectionsresponse?view=azure-iot-typescript-latest).</span></span> <span data-ttu-id="6153e-157">And then creates an array of coordinates for the route returned, and adds it to the map's `truckRouteLayerName` layer.</span><span class="sxs-lookup"><span data-stu-id="6153e-157">And then creates an array of coordinates for the route returned, and adds it to the map's `truckRouteLayerName` layer.</span></span>

3. <span data-ttu-id="6153e-158">Add the following JavaScript code to request the route for a car and display the results:</span><span class="sxs-lookup"><span data-stu-id="6153e-158">Add the following JavaScript code to request the route for a car and display the results:</span></span>

    ```JavaScript
    // Execute the car route query then add the route to the map once a response is received  
        client.route.getRouteDirections(routeQuery).then(response => { 
            // Parse the response into GeoJSON 
            var geoJsonResponse = new atlas.service.geojson.GeoJsonRouteDirectionsResponse(response); 
 
            // Get the first in the array of routes and add it to the map 
            map.addLinestrings([geoJsonResponse.getGeoJsonRoutes().features[0]], { 
                name: carRouteLayerName 
            }); 
    }); 
    ```
    <span data-ttu-id="6153e-159">This code snippet uses the same truck route query for a car.</span><span class="sxs-lookup"><span data-stu-id="6153e-159">This code snippet uses the same truck route query for a car.</span></span> <span data-ttu-id="6153e-160">It queries the Azure Maps routing service through the [getRouteDirections](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.route?view=azure-iot-typescript-latest#getroutedirections) method and then parses the response into GeoJSON format using the [getGeoJsonRouteDirectionsResponse](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonroutedirectionsresponse?view=azure-iot-typescript-latest).</span><span class="sxs-lookup"><span data-stu-id="6153e-160">It queries the Azure Maps routing service through the [getRouteDirections](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.route?view=azure-iot-typescript-latest#getroutedirections) method and then parses the response into GeoJSON format using the [getGeoJsonRouteDirectionsResponse](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonroutedirectionsresponse?view=azure-iot-typescript-latest).</span></span> <span data-ttu-id="6153e-161">And then creates an array of coordinates for the route returned, and adds it to the map's `carRouteLayerName` layer.</span><span class="sxs-lookup"><span data-stu-id="6153e-161">And then creates an array of coordinates for the route returned, and adds it to the map's `carRouteLayerName` layer.</span></span>

3. <span data-ttu-id="6153e-162">Save the **MapTruckRoute.html** file and refresh your browser to observe the result.</span><span class="sxs-lookup"><span data-stu-id="6153e-162">Save the **MapTruckRoute.html** file and refresh your browser to observe the result.</span></span> <span data-ttu-id="6153e-163">For a successful connection with the Maps' APIs, you should see a map similar to the following.</span><span class="sxs-lookup"><span data-stu-id="6153e-163">For a successful connection with the Maps' APIs, you should see a map similar to the following.</span></span>

    ![Prioritized routes with Azure Route Service](./media/tutorial-prioritized-routes/prioritized-routes.png)

    <span data-ttu-id="6153e-165">The truck route is blue and thicker, while the car route is purple and thinner.</span><span class="sxs-lookup"><span data-stu-id="6153e-165">The truck route is blue and thicker, while the car route is purple and thinner.</span></span> <span data-ttu-id="6153e-166">The car route goes across Lake Washington via I-90, which goes through tunnels under residential areas and so restricts hazardous waste cargo.</span><span class="sxs-lookup"><span data-stu-id="6153e-166">The car route goes across Lake Washington via I-90, which goes through tunnels under residential areas and so restricts hazardous waste cargo.</span></span> <span data-ttu-id="6153e-167">The truck route, which specifies a USHazmatClass2 cargo type, is correctly directed to use a different highway.</span><span class="sxs-lookup"><span data-stu-id="6153e-167">The truck route, which specifies a USHazmatClass2 cargo type, is correctly directed to use a different highway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6153e-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="6153e-168">Next steps</span></span>
<span data-ttu-id="6153e-169">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="6153e-169">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6153e-170">Create a new web page using the map control API</span><span class="sxs-lookup"><span data-stu-id="6153e-170">Create a new web page using the map control API</span></span>
> * <span data-ttu-id="6153e-171">Visualize traffic flow on your map</span><span class="sxs-lookup"><span data-stu-id="6153e-171">Visualize traffic flow on your map</span></span>
> * <span data-ttu-id="6153e-172">Create route queries that declare mode of travel</span><span class="sxs-lookup"><span data-stu-id="6153e-172">Create route queries that declare mode of travel</span></span>
> * <span data-ttu-id="6153e-173">Display multiple routes on your map</span><span class="sxs-lookup"><span data-stu-id="6153e-173">Display multiple routes on your map</span></span>

<span data-ttu-id="6153e-174">To learn more about the coverage and capabilities of Azure Maps, see [Zoom levels and tile grid](zoom-levels-and-tile-grid.md) and the other Concepts articles.</span><span class="sxs-lookup"><span data-stu-id="6153e-174">To learn more about the coverage and capabilities of Azure Maps, see [Zoom levels and tile grid](zoom-levels-and-tile-grid.md) and the other Concepts articles.</span></span>

<span data-ttu-id="6153e-175">For more code examples and an interactive coding experience, see [How to use the map control](how-to-use-map-control.md) and the other How-to guides.</span><span class="sxs-lookup"><span data-stu-id="6153e-175">For more code examples and an interactive coding experience, see [How to use the map control](how-to-use-map-control.md) and the other How-to guides.</span></span>