---
title: Working with geospatial data in Azure DocumentDB | Microsoft Docs
description: Understand how to create, index and query spatial objects with Azure DocumentDB.
services: documentdb
documentationcenter: ''
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: documentdb
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/20/2016
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 382eecf863f1e4798533034f915101c08dd4f448
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555162"
---
# <a name="working-with-geospatial-and-geojson-location-data-in-documentdb"></a><span data-ttu-id="d0f1b-103">Working with geospatial and GeoJSON location data in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d0f1b-103">Working with geospatial and GeoJSON location data in DocumentDB</span></span>
<span data-ttu-id="d0f1b-104">This article is an introduction to the geospatial functionality in [Azure DocumentDB](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="d0f1b-104">This article is an introduction to the geospatial functionality in [Azure DocumentDB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="d0f1b-105">After reading this, you will be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="d0f1b-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="d0f1b-106">How do I store spatial data in Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="d0f1b-106">How do I store spatial data in Azure DocumentDB?</span></span>
* <span data-ttu-id="d0f1b-107">How can I query geospatial data in Azure DocumentDB in SQL and LINQ?</span><span class="sxs-lookup"><span data-stu-id="d0f1b-107">How can I query geospatial data in Azure DocumentDB in SQL and LINQ?</span></span>
* <span data-ttu-id="d0f1b-108">How do I enable or disable spatial indexing in DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="d0f1b-108">How do I enable or disable spatial indexing in DocumentDB?</span></span>

<span data-ttu-id="d0f1b-109">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-109">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="d0f1b-110">Introduction to spatial data</span><span class="sxs-lookup"><span data-stu-id="d0f1b-110">Introduction to spatial data</span></span>
<span data-ttu-id="d0f1b-111">Spatial data describes the position and shape of objects in space.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-111">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="d0f1b-112">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-112">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span></span> <span data-ttu-id="d0f1b-113">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-113">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="d0f1b-114">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span><span class="sxs-lookup"><span data-stu-id="d0f1b-114">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="d0f1b-115">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="d0f1b-115">GeoJSON</span></span>
<span data-ttu-id="d0f1b-116">DocumentDB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="d0f1b-116">DocumentDB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="d0f1b-117">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using DocumentDB without any specialized tools or libraries.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-117">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using DocumentDB without any specialized tools or libraries.</span></span> <span data-ttu-id="d0f1b-118">The DocumentDB SDKs provide helper classes and methods that make it easy to work with spatial data.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-118">The DocumentDB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="d0f1b-119">Points, LineStrings and Polygons</span><span class="sxs-lookup"><span data-stu-id="d0f1b-119">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="d0f1b-120">A **Point** denotes a single position in space.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-120">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="d0f1b-121">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-121">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="d0f1b-122">A point is represented in GeoJSON (and DocumentDB) using its coordinate pair or longitude and latitude.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-122">A point is represented in GeoJSON (and DocumentDB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="d0f1b-123">Here's an example JSON for a point.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-123">Here's an example JSON for a point.</span></span>

<span data-ttu-id="d0f1b-124">**Points in DocumentDB**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-124">**Points in DocumentDB**</span></span>

    {
       "type":"Point",
       "coordinates":[ 31.9, -4.8 ]
    }

> [!NOTE]
> <span data-ttu-id="d0f1b-125">The GeoJSON specification specifies longitude first and latitude second.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-125">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="d0f1b-126">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-126">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="d0f1b-127">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-127">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="d0f1b-128">DocumentDB interprets coordinates as represented per the WGS-84 reference system.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-128">DocumentDB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="d0f1b-129">Please see below for more details about coordinate reference systems.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-129">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="d0f1b-130">This can be embedded in a DocumentDB document as shown in this example of a user profile containing location data:</span><span class="sxs-lookup"><span data-stu-id="d0f1b-130">This can be embedded in a DocumentDB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="d0f1b-131">**Use Profile with Location stored in DocumentDB**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-131">**Use Profile with Location stored in DocumentDB**</span></span>

    {
       "id":"documentdb-profile",
       "screen_name":"@DocumentDB",
       "city":"Redmond",
       "topics":[ "NoSQL", "Javascript" ],
       "location":{
          "type":"Point",
          "coordinates":[ 31.9, -4.8 ]
       }
    }

<span data-ttu-id="d0f1b-132">In addition to points, GeoJSON also supports LineStrings and Polygons.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-132">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="d0f1b-133">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-133">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="d0f1b-134">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-134">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="d0f1b-135">A **Polygon** is a boundary of connected points that forms a closed LineString.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-135">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="d0f1b-136">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-136">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="d0f1b-137">Here's an example of a Polygon in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-137">Here's an example of a Polygon in DocumentDB.</span></span> 

<span data-ttu-id="d0f1b-138">**Polygons in DocumentDB**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-138">**Polygons in DocumentDB**</span></span>

    {
       "type":"Polygon",
       "coordinates":[
           [ 31.8, -5 ],
           [ 31.8, -4.7 ],
           [ 32, -4.7 ],
           [ 32, -5 ],
           [ 31.8, -5 ]
       ]
    }

> [!NOTE]
> <span data-ttu-id="d0f1b-139">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-139">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="d0f1b-140">Points within a Polygon must be specified in counter-clockwise order.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-140">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="d0f1b-141">A Polygon specified in clockwise order represents the inverse of the region within it.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-141">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="d0f1b-142">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-142">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="d0f1b-143">Since these objects are valid JSON, they can all be stored and processed in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-143">Since these objects are valid JSON, they can all be stored and processed in DocumentDB.</span></span> <span data-ttu-id="d0f1b-144">However DocumentDB only supports automatic indexing of points.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-144">However DocumentDB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="d0f1b-145">Coordinate reference systems</span><span class="sxs-lookup"><span data-stu-id="d0f1b-145">Coordinate reference systems</span></span>
<span data-ttu-id="d0f1b-146">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-146">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="d0f1b-147">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-147">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="d0f1b-148">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="d0f1b-148">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="d0f1b-149">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-149">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="d0f1b-150">DocumentDB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-150">DocumentDB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="d0f1b-151">Creating documents with spatial data</span><span class="sxs-lookup"><span data-stu-id="d0f1b-151">Creating documents with spatial data</span></span>
<span data-ttu-id="d0f1b-152">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-152">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span></span> <span data-ttu-id="d0f1b-153">If you're working with a DocumentDB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-153">If you're working with a DocumentDB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="d0f1b-154">**Create Document with Geospatial data in Node.js**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-154">**Create Document with Geospatial data in Node.js**</span></span>

    var userProfileDocument = {
       "name":"documentdb",
       "location":{
          "type":"Point",
          "coordinates":[ -122.12, 47.66 ]
       }
    };

    client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
        // additional code within the callback
    });

<span data-ttu-id="d0f1b-155">If you're working with the .NET (or Java) SDKs, you can use the new Point and Polygon classes within the Microsoft.Azure.Documents.Spatial namespace to embed location information within your application objects.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-155">If you're working with the .NET (or Java) SDKs, you can use the new Point and Polygon classes within the Microsoft.Azure.Documents.Spatial namespace to embed location information within your application objects.</span></span> <span data-ttu-id="d0f1b-156">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-156">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="d0f1b-157">**Create Document with Geospatial data in .NET**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-157">**Create Document with Geospatial data in .NET**</span></span>

    using Microsoft.Azure.Documents.Spatial;

    public class UserProfile
    {
        [JsonProperty("name")]
        public string Name { get; set; }

        [JsonProperty("location")]
        public Point Location { get; set; }

        // More properties
    }

    await client.CreateDocumentAsync(
        UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
        new UserProfile 
        { 
            Name = "documentdb", 
            Location = new Point (-122.12, 47.66) 
        });

<span data-ttu-id="d0f1b-158">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-158">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="d0f1b-159">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0f1b-159">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="d0f1b-160">Querying spatial types</span><span class="sxs-lookup"><span data-stu-id="d0f1b-160">Querying spatial types</span></span>
<span data-ttu-id="d0f1b-161">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using DocumentDB using SQL and LINQ.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-161">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using DocumentDB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="d0f1b-162">Spatial SQL built-in functions</span><span class="sxs-lookup"><span data-stu-id="d0f1b-162">Spatial SQL built-in functions</span></span>
<span data-ttu-id="d0f1b-163">DocumentDB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-163">DocumentDB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="d0f1b-164">For more details on the complete set of built-in functions in the SQL language, please refer to [Query DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="d0f1b-164">For more details on the complete set of built-in functions in the SQL language, please refer to [Query DocumentDB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="d0f1b-165"><strong>Usage</strong></span><span class="sxs-lookup"><span data-stu-id="d0f1b-165"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="d0f1b-166"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="d0f1b-166"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d0f1b-167">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="d0f1b-167">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="d0f1b-168">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-168">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d0f1b-169">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="d0f1b-169">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="d0f1b-170">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span><span class="sxs-lookup"><span data-stu-id="d0f1b-170">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d0f1b-171">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="d0f1b-171">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="d0f1b-172">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-172">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d0f1b-173">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="d0f1b-173">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="d0f1b-174">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-174">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d0f1b-175">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="d0f1b-175">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="d0f1b-176">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-176">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="d0f1b-177">Spatial functions can be used to perform proximity queries against spatial data.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-177">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="d0f1b-178">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-178">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="d0f1b-179">**Query**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-179">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="d0f1b-180">**Results**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-180">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="d0f1b-181">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-181">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="d0f1b-182">For more details on spatial indexing, please see the section below.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-182">For more details on spatial indexing, please see the section below.</span></span> <span data-ttu-id="d0f1b-183">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span><span class="sxs-lookup"><span data-stu-id="d0f1b-183">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="d0f1b-184">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-184">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="d0f1b-185">ST_WITHIN can be used to check if a point lies within a Polygon.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-185">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="d0f1b-186">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-186">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="d0f1b-187">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-187">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="d0f1b-188">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-188">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="d0f1b-189">**Query**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-189">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="d0f1b-190">**Results**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-190">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="d0f1b-191">Similar to how mismatched types works in DocumentDB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-191">Similar to how mismatched types works in DocumentDB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="d0f1b-192">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-192">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="d0f1b-193">DocumentDB also supports performing inverse queries, i.e. you can index Polygons or lines in DocumentDB, then query for the areas that contain a specified point.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-193">DocumentDB also supports performing inverse queries, i.e. you can index Polygons or lines in DocumentDB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="d0f1b-194">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-194">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="d0f1b-195">**Query**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-195">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="d0f1b-196">**Results**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-196">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="d0f1b-197">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-197">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="d0f1b-198">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span><span class="sxs-lookup"><span data-stu-id="d0f1b-198">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="d0f1b-199">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-199">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="d0f1b-200">\*\* Query \*\*</span><span class="sxs-lookup"><span data-stu-id="d0f1b-200">\*\* Query \*\*</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="d0f1b-201">**Results**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-201">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="d0f1b-202">These functions can also be used to validate Polygons.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-202">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="d0f1b-203">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-203">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="d0f1b-204">**Query**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-204">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="d0f1b-205">**Results**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-205">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="d0f1b-206">LINQ Querying in the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d0f1b-206">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="d0f1b-207">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-207">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="d0f1b-208">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span><span class="sxs-lookup"><span data-stu-id="d0f1b-208">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="d0f1b-209">Here's an example of a LINQ query that finds all documents in the DocumentDB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-209">Here's an example of a LINQ query that finds all documents in the DocumentDB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span></span>

<span data-ttu-id="d0f1b-210">**LINQ query for Distance**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-210">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="d0f1b-211">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-211">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="d0f1b-212">**LINQ query for Within**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-212">**LINQ query for Within**</span></span>

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


<span data-ttu-id="d0f1b-213">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure DocumentDB for spatial indexing.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-213">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure DocumentDB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="d0f1b-214">Indexing</span><span class="sxs-lookup"><span data-stu-id="d0f1b-214">Indexing</span></span>
<span data-ttu-id="d0f1b-215">As we described in the [Schema Agnostic Indexing with Azure DocumentDB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed DocumentDB’s database engine to be truly schema agnostic and provide first class support for JSON.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-215">As we described in the [Schema Agnostic Indexing with Azure DocumentDB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed DocumentDB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="d0f1b-216">The write optimized database engine of DocumentDB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-216">The write optimized database engine of DocumentDB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="d0f1b-217">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-217">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="d0f1b-218">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-218">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="d0f1b-219">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the DocumentDB index.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-219">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the DocumentDB index.</span></span> <span data-ttu-id="d0f1b-220">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-220">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="d0f1b-221">If you specify an indexing policy that includes spatial index for /\* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="d0f1b-221">If you specify an indexing policy that includes spatial index for /\* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="d0f1b-222">Spatial indexes do not have a precision value, and always use a default precision value.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-222">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="d0f1b-223">DocumentDB supports automatic indexing of Points, Polygons, and LineStrings</span><span class="sxs-lookup"><span data-stu-id="d0f1b-223">DocumentDB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="d0f1b-224">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-224">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="d0f1b-225">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-225">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="d0f1b-226">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-226">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

<span data-ttu-id="d0f1b-227">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-227">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="d0f1b-228">**Create a collection with spatial indexing**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-228">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="d0f1b-229">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-229">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="d0f1b-230">**Modify an existing collection with spatial indexing**</span><span class="sxs-lookup"><span data-stu-id="d0f1b-230">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing to complete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="d0f1b-231">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-231">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="d0f1b-232">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-232">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="d0f1b-233">If your collection definition includes a partition key, indexing transformation progress is not reported.</span><span class="sxs-lookup"><span data-stu-id="d0f1b-233">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d0f1b-234">Next steps</span><span class="sxs-lookup"><span data-stu-id="d0f1b-234">Next steps</span></span>
<span data-ttu-id="d0f1b-235">Now that you've learnt about how to get started with geospatial support in DocumentDB, you can:</span><span class="sxs-lookup"><span data-stu-id="d0f1b-235">Now that you've learnt about how to get started with geospatial support in DocumentDB, you can:</span></span>

* <span data-ttu-id="d0f1b-236">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="d0f1b-236">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="d0f1b-237">Get hands on with geospatial querying at the [DocumentDB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="d0f1b-237">Get hands on with geospatial querying at the [DocumentDB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="d0f1b-238">Learn more about [DocumentDB Query](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="d0f1b-238">Learn more about [DocumentDB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="d0f1b-239">Learn more about [DocumentDB Indexing Policies](documentdb-indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="d0f1b-239">Learn more about [DocumentDB Indexing Policies](documentdb-indexing-policies.md)</span></span>

