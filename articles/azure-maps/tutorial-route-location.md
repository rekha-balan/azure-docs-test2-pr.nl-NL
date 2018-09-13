---
title: Find route with Azure Maps | Microsoft Docs
description: Route to a point of interest using Azure Maps
author: dsk-2015
ms.author: dkshir
ms.date: 09/04/2018
ms.topic: tutorial
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: 1ef4467862f47a833e0592c94c662170ca2946d8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856006"
---
# <a name="route-to-a-point-of-interest-using-azure-maps"></a><span data-ttu-id="790ab-103">Route to a point of interest using Azure Maps</span><span class="sxs-lookup"><span data-stu-id="790ab-103">Route to a point of interest using Azure Maps</span></span>

<span data-ttu-id="790ab-104">This tutorial shows how to use your Azure Maps account and the Route Service SDK to find the route to your point of interest.</span><span class="sxs-lookup"><span data-stu-id="790ab-104">This tutorial shows how to use your Azure Maps account and the Route Service SDK to find the route to your point of interest.</span></span> <span data-ttu-id="790ab-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="790ab-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="790ab-106">Create a new web page using the map control API</span><span class="sxs-lookup"><span data-stu-id="790ab-106">Create a new web page using the map control API</span></span>
> * <span data-ttu-id="790ab-107">Set address coordinates</span><span class="sxs-lookup"><span data-stu-id="790ab-107">Set address coordinates</span></span>
> * <span data-ttu-id="790ab-108">Query Route Service for directions to point of interest</span><span class="sxs-lookup"><span data-stu-id="790ab-108">Query Route Service for directions to point of interest</span></span>

## <a name="prerequisites"></a><span data-ttu-id="790ab-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="790ab-109">Prerequisites</span></span>

<span data-ttu-id="790ab-110">Before you proceed, follow the steps in the previous tutorial to [create your Azure Maps account](./tutorial-search-location.md#createaccount), and [get the subscription key for your account](./tutorial-search-location.md#getkey).</span><span class="sxs-lookup"><span data-stu-id="790ab-110">Before you proceed, follow the steps in the previous tutorial to [create your Azure Maps account](./tutorial-search-location.md#createaccount), and [get the subscription key for your account](./tutorial-search-location.md#getkey).</span></span> 

<a id="getcoordinates"></a>

## <a name="create-a-new-map"></a><span data-ttu-id="790ab-111">Create a new map</span><span class="sxs-lookup"><span data-stu-id="790ab-111">Create a new map</span></span> 
<span data-ttu-id="790ab-112">The following steps show you how to create a static HTML page embedded with the Map Control API.</span><span class="sxs-lookup"><span data-stu-id="790ab-112">The following steps show you how to create a static HTML page embedded with the Map Control API.</span></span> 

1. <span data-ttu-id="790ab-113">On your local machine, create a new file and name it **MapRoute.html**.</span><span class="sxs-lookup"><span data-stu-id="790ab-113">On your local machine, create a new file and name it **MapRoute.html**.</span></span> 
2. <span data-ttu-id="790ab-114">Add the following HTML components to the file:</span><span class="sxs-lookup"><span data-stu-id="790ab-114">Add the following HTML components to the file:</span></span>

    ```HTML
    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, user-scalable=no" />
        <title>Map Route</title>
        <link rel="stylesheet" href="https://atlas.microsoft.com/sdk/css/atlas.min.css?api-version=1" type="text/css"/> 
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
    <span data-ttu-id="790ab-115">The HTML header embeds the resource locations for CSS and JavaScript files for the Azure Maps library.</span><span class="sxs-lookup"><span data-stu-id="790ab-115">The HTML header embeds the resource locations for CSS and JavaScript files for the Azure Maps library.</span></span> <span data-ttu-id="790ab-116">The *script* segment in the body of the HTML file will contain the inline JavaScript code to access the Azure Maps APIs.</span><span class="sxs-lookup"><span data-stu-id="790ab-116">The *script* segment in the body of the HTML file will contain the inline JavaScript code to access the Azure Maps APIs.</span></span>

3. <span data-ttu-id="790ab-117">Add the following JavaScript code to the *script* block of the HTML file.</span><span class="sxs-lookup"><span data-stu-id="790ab-117">Add the following JavaScript code to the *script* block of the HTML file.</span></span> <span data-ttu-id="790ab-118">Replace the string **\<your account key\>** with the primary key that you copied from your Maps account.</span><span class="sxs-lookup"><span data-stu-id="790ab-118">Replace the string **\<your account key\>** with the primary key that you copied from your Maps account.</span></span>

    ```JavaScript
    // Instantiate map to the div with id "map"
    var MapsAccountKey = "<your account key>";
    var map = new atlas.Map("map", {
        "subscription-key": MapsAccountKey
    });
    ```
    <span data-ttu-id="790ab-119">The **atlas.Map** provides the control for a visual and interactive web map, and is a component of the Azure Map Control API.</span><span class="sxs-lookup"><span data-stu-id="790ab-119">The **atlas.Map** provides the control for a visual and interactive web map, and is a component of the Azure Map Control API.</span></span>

4. <span data-ttu-id="790ab-120">Save the file and open it in your browser.</span><span class="sxs-lookup"><span data-stu-id="790ab-120">Save the file and open it in your browser.</span></span> <span data-ttu-id="790ab-121">At this point, you have a basic map that you can develop further.</span><span class="sxs-lookup"><span data-stu-id="790ab-121">At this point, you have a basic map that you can develop further.</span></span> 

   ![View basic map](./media/tutorial-route-location/basic-map.png)

## <a name="set-start-and-end-points"></a><span data-ttu-id="790ab-123">Set start and end points</span><span class="sxs-lookup"><span data-stu-id="790ab-123">Set start and end points</span></span>

<span data-ttu-id="790ab-124">For this tutorial, set the start point as Microsoft, and the destination point as a gas station in Seattle.</span><span class="sxs-lookup"><span data-stu-id="790ab-124">For this tutorial, set the start point as Microsoft, and the destination point as a gas station in Seattle.</span></span> 

1. <span data-ttu-id="790ab-125">In the same *script* block of the **MapRoute.html** file, add the following JavaScript code to create start and end points for the route:</span><span class="sxs-lookup"><span data-stu-id="790ab-125">In the same *script* block of the **MapRoute.html** file, add the following JavaScript code to create start and end points for the route:</span></span>

    ```JavaScript
    // Create the GeoJSON objects which represent the start and end point of the route
    var startPoint = new atlas.data.Point([-122.130137, 47.644702]);
    var startPin = new atlas.data.Feature(startPoint, {
        title: "Microsoft",
        icon: "pin-round-blue"
    });

    var destinationPoint = new atlas.data.Point([-122.3352, 47.61397]);
    var destinationPin = new atlas.data.Feature(destinationPoint, {
        title: "Contoso Oil & Gas",
        icon: "pin-blue"
    });
    ```
    <span data-ttu-id="790ab-126">This code creates two [GeoJSON objects](https://en.wikipedia.org/wiki/GeoJSON) to represent the start and end points of the route.</span><span class="sxs-lookup"><span data-stu-id="790ab-126">This code creates two [GeoJSON objects](https://en.wikipedia.org/wiki/GeoJSON) to represent the start and end points of the route.</span></span> 

2. <span data-ttu-id="790ab-127">Add the following JavaScript code to add the pins for the start and end points to the map:</span><span class="sxs-lookup"><span data-stu-id="790ab-127">Add the following JavaScript code to add the pins for the start and end points to the map:</span></span>

    ```JavaScript
    // Fit the map window to the bounding box defined by the start and destination points
    var swLon = Math.min(startPoint.coordinates[0], destinationPoint.coordinates[0]);
    var swLat = Math.min(startPoint.coordinates[1], destinationPoint.coordinates[1]);
    var neLon = Math.max(startPoint.coordinates[0], destinationPoint.coordinates[0]);
    var neLat = Math.max(startPoint.coordinates[1], destinationPoint.coordinates[1]);
    map.setCameraBounds({
        bounds: [swLon, swLat, neLon, neLat],
        padding: 50
    });

    // Add pins to the map for the start and end point of the route
    map.addPins([startPin, destinationPin], {
        name: "route-pins",
        textFont: "SegoeUi-Regular",
        textOffset: [0, -20]
    });
    ``` 
    <span data-ttu-id="790ab-128">The **map.setCameraBounds** adjusts the map window according to the coordinates of the start and end points.</span><span class="sxs-lookup"><span data-stu-id="790ab-128">The **map.setCameraBounds** adjusts the map window according to the coordinates of the start and end points.</span></span> <span data-ttu-id="790ab-129">The API **map.addPins** adds the points to the Map control as visual components.</span><span class="sxs-lookup"><span data-stu-id="790ab-129">The API **map.addPins** adds the points to the Map control as visual components.</span></span>

7. <span data-ttu-id="790ab-130">Save the **MapRoute.html** file and refresh your browser.</span><span class="sxs-lookup"><span data-stu-id="790ab-130">Save the **MapRoute.html** file and refresh your browser.</span></span> <span data-ttu-id="790ab-131">Now the map is centered over Seattle, and you can see the round blue pin marking the start point and the blue pin marking the finish point.</span><span class="sxs-lookup"><span data-stu-id="790ab-131">Now the map is centered over Seattle, and you can see the round blue pin marking the start point and the blue pin marking the finish point.</span></span>

   ![View map with start and end points marked](./media/tutorial-route-location/map-pins.png)

<a id="getroute"></a>

## <a name="get-directions"></a><span data-ttu-id="790ab-133">Get directions</span><span class="sxs-lookup"><span data-stu-id="790ab-133">Get directions</span></span>

<span data-ttu-id="790ab-134">This section shows how to use the Maps route service API to find the route from a given start point to a destination.</span><span class="sxs-lookup"><span data-stu-id="790ab-134">This section shows how to use the Maps route service API to find the route from a given start point to a destination.</span></span> <span data-ttu-id="790ab-135">The route service provides APIs to plan *fastest*, *shortest*, *eco*, or *thrilling* routes between two locations.</span><span class="sxs-lookup"><span data-stu-id="790ab-135">The route service provides APIs to plan *fastest*, *shortest*, *eco*, or *thrilling* routes between two locations.</span></span> <span data-ttu-id="790ab-136">It also allows users to plan routes in the future by using Azure's extensive historic traffic database and predicting route durations for any day and time.</span><span class="sxs-lookup"><span data-stu-id="790ab-136">It also allows users to plan routes in the future by using Azure's extensive historic traffic database and predicting route durations for any day and time.</span></span> <span data-ttu-id="790ab-137">For more information, see [Get route directions](https://docs.microsoft.com/rest/api/maps/route/getroutedirections).</span><span class="sxs-lookup"><span data-stu-id="790ab-137">For more information, see [Get route directions](https://docs.microsoft.com/rest/api/maps/route/getroutedirections).</span></span>


1. <span data-ttu-id="790ab-138">First, add a new layer on the map to display the route path, or *linestring*.</span><span class="sxs-lookup"><span data-stu-id="790ab-138">First, add a new layer on the map to display the route path, or *linestring*.</span></span> <span data-ttu-id="790ab-139">Add the following JavaScript code to the *script* block.</span><span class="sxs-lookup"><span data-stu-id="790ab-139">Add the following JavaScript code to the *script* block.</span></span>

    ```JavaScript
    // Initialize the linestring layer for routes on the map
    var routeLinesLayerName = "routes";
    map.addLinestrings([], {
        name: routeLinesLayerName,
        color: "#2272B9",
        width: 5,
        cap: "round",
        join: "round",
        before: "labels"
    });
    ```

2.  <span data-ttu-id="790ab-140">Instantiate the client service, by adding the following Javascript code to the script block.</span><span class="sxs-lookup"><span data-stu-id="790ab-140">Instantiate the client service, by adding the following Javascript code to the script block.</span></span>
    ```JavaScript
    var client = new atlas.service.Client(subscriptionKey);
    ```

3. <span data-ttu-id="790ab-141">Add the following block of code to construct a route query string.</span><span class="sxs-lookup"><span data-stu-id="790ab-141">Add the following block of code to construct a route query string.</span></span>
    ```JavaScript
    // Construct the route query string 
        var routeQuery = startPoint.coordinates[1] + 
            "," + 
            startPoint.coordinates[0] + 
            ":" + 
            destinationPoint.coordinates[1] + 
            "," + 
            destinationPoint.coordinates[0];     
    ```

4. <span data-ttu-id="790ab-142">To get the route, add the following block of code to the script.</span><span class="sxs-lookup"><span data-stu-id="790ab-142">To get the route, add the following block of code to the script.</span></span> <span data-ttu-id="790ab-143">It queries the Azure Maps routing service through the [getRouteDirections](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.route?view=azure-iot-typescript-latest#getroutedirections) method and then parses the response into GeoJSON format using the [getGeoJsonRoutes](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonroutedirectionsresponse?view=azure-iot-typescript-latest#getgeojsonroutes).</span><span class="sxs-lookup"><span data-stu-id="790ab-143">It queries the Azure Maps routing service through the [getRouteDirections](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.route?view=azure-iot-typescript-latest#getroutedirections) method and then parses the response into GeoJSON format using the [getGeoJsonRoutes](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.geojson.geojsonroutedirectionsresponse?view=azure-iot-typescript-latest#getgeojsonroutes).</span></span> <span data-ttu-id="790ab-144">It then adds all the response lines onto the map to render the route.</span><span class="sxs-lookup"><span data-stu-id="790ab-144">It then adds all the response lines onto the map to render the route.</span></span> <span data-ttu-id="790ab-145">You can see [add a line on the map](./map-add-shape.md#addALine) for more information.</span><span class="sxs-lookup"><span data-stu-id="790ab-145">You can see [add a line on the map](./map-add-shape.md#addALine) for more information.</span></span>

    ```JavaScript
    // Execute the query then add the route to the map once a response is received  
    client.route.getRouteDirections(routeQuery).then(response => { 
         // Parse the response into GeoJSON 
         var geoJsonResponse = new atlas.service.geojson.GeoJsonRouteDirectionsResponse(response); 
 
         // Get the first in the array of routes and add it to the map 
         map.addLinestrings([geoJsonResponse.getGeoJsonRoutes().features[0]], { 
             name: routeLinesLayerName 
         }); 
    }); 
    ```

5. <span data-ttu-id="790ab-146">Save the **MapRoute.html** file and refresh your web browser.</span><span class="sxs-lookup"><span data-stu-id="790ab-146">Save the **MapRoute.html** file and refresh your web browser.</span></span> <span data-ttu-id="790ab-147">For a successful connection with the Maps APIs, you should see a map similar to the following.</span><span class="sxs-lookup"><span data-stu-id="790ab-147">For a successful connection with the Maps APIs, you should see a map similar to the following.</span></span>

    ![Azure Map Control and Route Service](./media/tutorial-route-location/map-route.png)


## <a name="next-steps"></a><span data-ttu-id="790ab-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="790ab-149">Next steps</span></span>
<span data-ttu-id="790ab-150">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="790ab-150">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="790ab-151">Create a new web page using the map control API</span><span class="sxs-lookup"><span data-stu-id="790ab-151">Create a new web page using the map control API</span></span>
> * <span data-ttu-id="790ab-152">Set address coordinates</span><span class="sxs-lookup"><span data-stu-id="790ab-152">Set address coordinates</span></span>
> * <span data-ttu-id="790ab-153">Query the route service for directions to point of interest</span><span class="sxs-lookup"><span data-stu-id="790ab-153">Query the route service for directions to point of interest</span></span>

<span data-ttu-id="790ab-154">The next tutorial demonstrates how to create a route query with restrictions like mode of travel or type of cargo, then display multiple routes on the same map.</span><span class="sxs-lookup"><span data-stu-id="790ab-154">The next tutorial demonstrates how to create a route query with restrictions like mode of travel or type of cargo, then display multiple routes on the same map.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="790ab-155">Find routes for different modes of travel</span><span class="sxs-lookup"><span data-stu-id="790ab-155">Find routes for different modes of travel</span></span>](./tutorial-prioritized-routes.md)
