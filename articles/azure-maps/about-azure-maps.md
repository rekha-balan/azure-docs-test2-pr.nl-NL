---
title: Overview of Azure Maps | Microsoft Docs
description: An introduction to Azure Maps
author: dsk-2015
ms.author: dkshir
ms.date: 07/12/2018
ms.topic: overview
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: 803e82a294b64452ffd788880097b9d86ac1065b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867015"
---
# <a name="what-is-azure-maps"></a><span data-ttu-id="20297-103">What is Azure Maps?</span><span class="sxs-lookup"><span data-stu-id="20297-103">What is Azure Maps?</span></span>
<span data-ttu-id="20297-104">Azure Maps is a collection of geospatial services, backed by fresh mapping data so you can provide accurate geographic context to your web and mobile applications.</span><span class="sxs-lookup"><span data-stu-id="20297-104">Azure Maps is a collection of geospatial services, backed by fresh mapping data so you can provide accurate geographic context to your web and mobile applications.</span></span> <span data-ttu-id="20297-105">It contains REST APIs for rendering maps, searching points of interest, routes to points of interests, traffic conditions, time zones, and IP to location services.</span><span class="sxs-lookup"><span data-stu-id="20297-105">It contains REST APIs for rendering maps, searching points of interest, routes to points of interests, traffic conditions, time zones, and IP to location services.</span></span> <span data-ttu-id="20297-106">You can use these APIs with familiar tools to quickly develop and scale solutions that integrate location information into your Azure solutions.</span><span class="sxs-lookup"><span data-stu-id="20297-106">You can use these APIs with familiar tools to quickly develop and scale solutions that integrate location information into your Azure solutions.</span></span> <span data-ttu-id="20297-107">Along with the REST APIs, it provides a web-based JavaScript control to make development easy, flexible, and portable across multiple mediums.</span><span class="sxs-lookup"><span data-stu-id="20297-107">Along with the REST APIs, it provides a web-based JavaScript control to make development easy, flexible, and portable across multiple mediums.</span></span> 

<span data-ttu-id="20297-108">The following video explains Azure Maps in depth:</span><span class="sxs-lookup"><span data-stu-id="20297-108">The following video explains Azure Maps in depth:</span></span>

<iframe src="https://channel9.msdn.com/Shows/Azure-Friday/Azure-Location-Based-Services/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="services-in-azure-maps"></a><span data-ttu-id="20297-109">Services in Azure Maps</span><span class="sxs-lookup"><span data-stu-id="20297-109">Services in Azure Maps</span></span>

<span data-ttu-id="20297-110">Azure Maps consists of the following six services that can provide geographic context to your Azure applications.</span><span class="sxs-lookup"><span data-stu-id="20297-110">Azure Maps consists of the following six services that can provide geographic context to your Azure applications.</span></span> 

### <a name="render-service"></a><span data-ttu-id="20297-111">Render service</span><span class="sxs-lookup"><span data-stu-id="20297-111">Render service</span></span>

<span data-ttu-id="20297-112">The Render service is designed for developers to create web and mobile applications around mapping.</span><span class="sxs-lookup"><span data-stu-id="20297-112">The Render service is designed for developers to create web and mobile applications around mapping.</span></span> <span data-ttu-id="20297-113">The service uses either high-quality raster graphic images, available in 19 zoom levels, or fully customizable vector format map images.</span><span class="sxs-lookup"><span data-stu-id="20297-113">The service uses either high-quality raster graphic images, available in 19 zoom levels, or fully customizable vector format map images.</span></span>

![Azure Maps Map.png](media/about-azure-maps/Introduction_Map.png)

<span data-ttu-id="20297-115">The Render service now offers preview APIs to allow developers to work with satellite imagery.</span><span class="sxs-lookup"><span data-stu-id="20297-115">The Render service now offers preview APIs to allow developers to work with satellite imagery.</span></span> <span data-ttu-id="20297-116">For more details, read the [Azure Maps Render APIs](https://docs.microsoft.com/rest/api/maps/render).</span><span class="sxs-lookup"><span data-stu-id="20297-116">For more details, read the [Azure Maps Render APIs](https://docs.microsoft.com/rest/api/maps/render).</span></span>


### <a name="route-service"></a><span data-ttu-id="20297-117">Route service</span><span class="sxs-lookup"><span data-stu-id="20297-117">Route service</span></span> 

<span data-ttu-id="20297-118">The Route service contains robust geometry calculations for real-world infrastructure and directions for multiple transportation modes.</span><span class="sxs-lookup"><span data-stu-id="20297-118">The Route service contains robust geometry calculations for real-world infrastructure and directions for multiple transportation modes.</span></span> <span data-ttu-id="20297-119">The service allows for developers to calculate directions across a number of travel modes such as car, truck, bicycle, or walking.</span><span class="sxs-lookup"><span data-stu-id="20297-119">The service allows for developers to calculate directions across a number of travel modes such as car, truck, bicycle, or walking.</span></span> <span data-ttu-id="20297-120">The service can also consider inputs such as traffic conditions, weight restrictions, or hazardous material transport.</span><span class="sxs-lookup"><span data-stu-id="20297-120">The service can also consider inputs such as traffic conditions, weight restrictions, or hazardous material transport.</span></span>

![Azure Maps Route.png](media/about-azure-maps/Introduction_Route.png)

<span data-ttu-id="20297-122">The Route service now offers a preview of advanced features such as batch processing of multiple route requests, matrices of travel time and distance between a set of origins and destinations, and finding routes or distances you can travel based on your time or fuel requirements.</span><span class="sxs-lookup"><span data-stu-id="20297-122">The Route service now offers a preview of advanced features such as batch processing of multiple route requests, matrices of travel time and distance between a set of origins and destinations, and finding routes or distances you can travel based on your time or fuel requirements.</span></span> <span data-ttu-id="20297-123">For details on the routing capabilities, read the [Azure Maps Route APIs](https://docs.microsoft.com/rest/api/maps/route).</span><span class="sxs-lookup"><span data-stu-id="20297-123">For details on the routing capabilities, read the [Azure Maps Route APIs](https://docs.microsoft.com/rest/api/maps/route).</span></span>


### <a name="search-service"></a><span data-ttu-id="20297-124">Search service</span><span class="sxs-lookup"><span data-stu-id="20297-124">Search service</span></span>

<span data-ttu-id="20297-125">The Search service is designed for developers to search for addresses, places, business listings by name or category, and other geographic information.</span><span class="sxs-lookup"><span data-stu-id="20297-125">The Search service is designed for developers to search for addresses, places, business listings by name or category, and other geographic information.</span></span> <span data-ttu-id="20297-126">The Search Service can also [reverse geocode](https://en.wikipedia.org/wiki/Reverse_geocoding) addresses and cross streets based on latitudes and longitudes.</span><span class="sxs-lookup"><span data-stu-id="20297-126">The Search Service can also [reverse geocode](https://en.wikipedia.org/wiki/Reverse_geocoding) addresses and cross streets based on latitudes and longitudes.</span></span> 

![Azure Maps Search.png](media/about-azure-maps/Introduction_Search.png)

<span data-ttu-id="20297-128">The Search service also provides advanced features such as search along a route, search inside a wider area, batch a group of search requests, as well as search for larger area instead of a location point.</span><span class="sxs-lookup"><span data-stu-id="20297-128">The Search service also provides advanced features such as search along a route, search inside a wider area, batch a group of search requests, as well as search for larger area instead of a location point.</span></span> <span data-ttu-id="20297-129">APIs for batch and area search are currently in preview.</span><span class="sxs-lookup"><span data-stu-id="20297-129">APIs for batch and area search are currently in preview.</span></span> <span data-ttu-id="20297-130">For more details on the search capabilities, read the [Azure Maps Search APIs](https://docs.microsoft.com/rest/api/maps/search) page.</span><span class="sxs-lookup"><span data-stu-id="20297-130">For more details on the search capabilities, read the [Azure Maps Search APIs](https://docs.microsoft.com/rest/api/maps/search) page.</span></span>


### <a name="time-zone-service"></a><span data-ttu-id="20297-131">Time Zone service</span><span class="sxs-lookup"><span data-stu-id="20297-131">Time Zone service</span></span>

<span data-ttu-id="20297-132">The Time Zone service allows you to query current, historical, and future time zone information using either latitude-longitude pairs or an [IANA ID](http://www.iana.org/).</span><span class="sxs-lookup"><span data-stu-id="20297-132">The Time Zone service allows you to query current, historical, and future time zone information using either latitude-longitude pairs or an [IANA ID](http://www.iana.org/).</span></span> <span data-ttu-id="20297-133">The Time Zone service also allows for converting Microsoft Windows time zone IDs to IANA time zones, fetching a time zone offset to UTC and getting the current time in a respective time zone.</span><span class="sxs-lookup"><span data-stu-id="20297-133">The Time Zone service also allows for converting Microsoft Windows time zone IDs to IANA time zones, fetching a time zone offset to UTC and getting the current time in a respective time zone.</span></span> <span data-ttu-id="20297-134">A typical JSON response for a query to the Time Zone Service looks like the following sample:</span><span class="sxs-lookup"><span data-stu-id="20297-134">A typical JSON response for a query to the Time Zone Service looks like the following sample:</span></span>

```JSON
{
    "Version": "2017c",
    "ReferenceUtcTimestamp": "2017-11-20T23:09:48.686173Z",
    "TimeZones": [{
        "Id": "America/Los_Angeles",
        "ReferenceTime": {
            "Tag": "PST",
            "StandardOffset": "-08:00:00",
            "DaylightSavings": "00:00:00",
            "WallTime": "2017-11-20T15:09:48.686173-08:00",
            "PosixTzValidYear": 2017,
            "PosixTz": "PST+8PDT,M3.2.0,M11.1.0"
        }
    }]
}
```

<span data-ttu-id="20297-135">For details on this service, visit the [Azure Maps Timezone APIs](https://docs.microsoft.com/rest/api/maps/timezone) page.</span><span class="sxs-lookup"><span data-stu-id="20297-135">For details on this service, visit the [Azure Maps Timezone APIs](https://docs.microsoft.com/rest/api/maps/timezone) page.</span></span>

### <a name="traffic-service"></a><span data-ttu-id="20297-136">Traffic service</span><span class="sxs-lookup"><span data-stu-id="20297-136">Traffic service</span></span>

<span data-ttu-id="20297-137">The Traffic service is a suite of web services designed for developers to create web and mobile applications requiring traffic.</span><span class="sxs-lookup"><span data-stu-id="20297-137">The Traffic service is a suite of web services designed for developers to create web and mobile applications requiring traffic.</span></span> <span data-ttu-id="20297-138">The service provides two data types:</span><span class="sxs-lookup"><span data-stu-id="20297-138">The service provides two data types:</span></span>
    * <span data-ttu-id="20297-139">Traffic flow - real-time observed speeds and travel times for all key roads in the network.</span><span class="sxs-lookup"><span data-stu-id="20297-139">Traffic flow - real-time observed speeds and travel times for all key roads in the network.</span></span> 
    * <span data-ttu-id="20297-140">Traffic incidents - an accurate view about the traffic jams and incidents around the road network.</span><span class="sxs-lookup"><span data-stu-id="20297-140">Traffic incidents - an accurate view about the traffic jams and incidents around the road network.</span></span>

![Azure Maps Traffic](media/about-azure-maps/Introduction_Traffic.png)

<span data-ttu-id="20297-142">Visit the [Azure Maps Traffic APIs](https://docs.microsoft.com/rest/api/maps/traffic) page for more details.</span><span class="sxs-lookup"><span data-stu-id="20297-142">Visit the [Azure Maps Traffic APIs](https://docs.microsoft.com/rest/api/maps/traffic) page for more details.</span></span>

### <a name="ip-to-location"></a><span data-ttu-id="20297-143">IP to Location</span><span class="sxs-lookup"><span data-stu-id="20297-143">IP to Location</span></span>

<span data-ttu-id="20297-144">The IP to Location is a preview service that allows you to retrieve the two letter country code for a given IP address.</span><span class="sxs-lookup"><span data-stu-id="20297-144">The IP to Location is a preview service that allows you to retrieve the two letter country code for a given IP address.</span></span> <span data-ttu-id="20297-145">This service can help you tailor your application to meet special geopolitical constraints, as well as enhance user experience by changing the application's content based on the geographic location.</span><span class="sxs-lookup"><span data-stu-id="20297-145">This service can help you tailor your application to meet special geopolitical constraints, as well as enhance user experience by changing the application's content based on the geographic location.</span></span> 

<span data-ttu-id="20297-146">For information on the REST APIs for IP to Location service, visit the [Azure Maps Geolocation APIs](https://docs.microsoft.com/rest/api/maps/geolocation) page.</span><span class="sxs-lookup"><span data-stu-id="20297-146">For information on the REST APIs for IP to Location service, visit the [Azure Maps Geolocation APIs](https://docs.microsoft.com/rest/api/maps/geolocation) page.</span></span>

## <a name="programming-model"></a><span data-ttu-id="20297-147">Programming model</span><span class="sxs-lookup"><span data-stu-id="20297-147">Programming model</span></span>

<span data-ttu-id="20297-148">Azure Maps is built for mobility and can power cross-platform applications.</span><span class="sxs-lookup"><span data-stu-id="20297-148">Azure Maps is built for mobility and can power cross-platform applications.</span></span> <span data-ttu-id="20297-149">It uses a programming model that is language agnostic and supports JSON output through [REST APIs](https://docs.microsoft.com/rest/api/maps/).</span><span class="sxs-lookup"><span data-stu-id="20297-149">It uses a programming model that is language agnostic and supports JSON output through [REST APIs](https://docs.microsoft.com/rest/api/maps/).</span></span> 

<span data-ttu-id="20297-150">Additionally, Azure Maps offers a convenient [JavaScript map control](https://docs.microsoft.com/javascript/api/azure-maps-control/models?view=azure-iot-typescript-latest) with a simple programming model for quick and easy development of both web and mobile applications.</span><span class="sxs-lookup"><span data-stu-id="20297-150">Additionally, Azure Maps offers a convenient [JavaScript map control](https://docs.microsoft.com/javascript/api/azure-maps-control/models?view=azure-iot-typescript-latest) with a simple programming model for quick and easy development of both web and mobile applications.</span></span> 


## <a name="usage"></a><span data-ttu-id="20297-151">Usage</span><span class="sxs-lookup"><span data-stu-id="20297-151">Usage</span></span>

<span data-ttu-id="20297-152">Accessing the Maps services is a matter of navigating to the [Azure portal](http://portal.azure.com) and creating an Azure Maps account.</span><span class="sxs-lookup"><span data-stu-id="20297-152">Accessing the Maps services is a matter of navigating to the [Azure portal](http://portal.azure.com) and creating an Azure Maps account.</span></span> 

<span data-ttu-id="20297-153">Azure Maps uses a key-based authentication scheme.</span><span class="sxs-lookup"><span data-stu-id="20297-153">Azure Maps uses a key-based authentication scheme.</span></span> <span data-ttu-id="20297-154">Your account comes with two keys pre-generated for you.</span><span class="sxs-lookup"><span data-stu-id="20297-154">Your account comes with two keys pre-generated for you.</span></span> <span data-ttu-id="20297-155">Start integrating these location capabilities directly into your applications by using either of your keys in the requests to the Azure Maps service.</span><span class="sxs-lookup"><span data-stu-id="20297-155">Start integrating these location capabilities directly into your applications by using either of your keys in the requests to the Azure Maps service.</span></span>

## <a name="supported-regions"></a><span data-ttu-id="20297-156">Supported regions</span><span class="sxs-lookup"><span data-stu-id="20297-156">Supported regions</span></span>
<span data-ttu-id="20297-157">The Azure Maps API is currently available in all countries except for the following:</span><span class="sxs-lookup"><span data-stu-id="20297-157">The Azure Maps API is currently available in all countries except for the following:</span></span> 

* <span data-ttu-id="20297-158">Argentina</span><span class="sxs-lookup"><span data-stu-id="20297-158">Argentina</span></span>
* <span data-ttu-id="20297-159">China</span><span class="sxs-lookup"><span data-stu-id="20297-159">China</span></span>
* <span data-ttu-id="20297-160">India</span><span class="sxs-lookup"><span data-stu-id="20297-160">India</span></span>
* <span data-ttu-id="20297-161">Morocco</span><span class="sxs-lookup"><span data-stu-id="20297-161">Morocco</span></span>
* <span data-ttu-id="20297-162">Pakistan</span><span class="sxs-lookup"><span data-stu-id="20297-162">Pakistan</span></span>
* <span data-ttu-id="20297-163">South Korea</span><span class="sxs-lookup"><span data-stu-id="20297-163">South Korea</span></span>

<span data-ttu-id="20297-164">Check your current IP address and verify that the location of your IP address is not in one of the unsupported countries above.</span><span class="sxs-lookup"><span data-stu-id="20297-164">Check your current IP address and verify that the location of your IP address is not in one of the unsupported countries above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20297-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="20297-165">Next steps</span></span>

- <span data-ttu-id="20297-166">For more information on the new features of Azure Maps:</span><span class="sxs-lookup"><span data-stu-id="20297-166">For more information on the new features of Azure Maps:</span></span> 
    - <span data-ttu-id="20297-167">[Route Matrix, Isochrones, IP lookup, and more](https://azure.microsoft.com/blog/route-matrix-isochrones-ip-lookup-and-more-added-to-azure-maps/).</span><span class="sxs-lookup"><span data-stu-id="20297-167">[Route Matrix, Isochrones, IP lookup, and more](https://azure.microsoft.com/blog/route-matrix-isochrones-ip-lookup-and-more-added-to-azure-maps/).</span></span> 
- <span data-ttu-id="20297-168">Proceed to trying out a sample app showcasing the service</span><span class="sxs-lookup"><span data-stu-id="20297-168">Proceed to trying out a sample app showcasing the service</span></span>
    - [<span data-ttu-id="20297-169">Launch a demo interactive search map</span><span class="sxs-lookup"><span data-stu-id="20297-169">Launch a demo interactive search map</span></span>](quick-demo-map-app.md)
