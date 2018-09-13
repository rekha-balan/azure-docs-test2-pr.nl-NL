---
title: Working with geospatial data in Azure Cosmos DB | Microsoft Docs
description: Understand how to create, index and query spatial objects with Azure Cosmos DB and the SQL API.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 10/20/2017
ms.author: sngun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 74824af6f17a6c1d2638c8604edd38ffa419d607
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855969"
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="b3d8b-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b3d8b-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="b3d8b-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="b3d8b-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="b3d8b-105">After reading this, you will be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="b3d8b-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="b3d8b-106">How do I store spatial data in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="b3d8b-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="b3d8b-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span><span class="sxs-lookup"><span data-stu-id="b3d8b-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="b3d8b-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="b3d8b-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="b3d8b-109">This article shows how to work with spatial data with the SQL API.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-109">This article shows how to work with spatial data with the SQL API.</span></span> <span data-ttu-id="b3d8b-110">See this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-110">See this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="b3d8b-111">Introduction to spatial data</span><span class="sxs-lookup"><span data-stu-id="b3d8b-111">Introduction to spatial data</span></span>
<span data-ttu-id="b3d8b-112">Spatial data describes the position and shape of objects in space.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-112">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="b3d8b-113">In most applications, these correspond to objects on the earth and geospatial data.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-113">In most applications, these correspond to objects on the earth and geospatial data.</span></span> <span data-ttu-id="b3d8b-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="b3d8b-115">Common use cases often involve proximity queries, for example, "find all coffee shops near my current location."</span><span class="sxs-lookup"><span data-stu-id="b3d8b-115">Common use cases often involve proximity queries, for example, "find all coffee shops near my current location."</span></span> 

### <a name="geojson"></a><span data-ttu-id="b3d8b-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="b3d8b-116">GeoJSON</span></span>
<span data-ttu-id="b3d8b-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="b3d8b-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="b3d8b-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="b3d8b-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="b3d8b-120">Points, LineStrings, and Polygons</span><span class="sxs-lookup"><span data-stu-id="b3d8b-120">Points, LineStrings, and Polygons</span></span>
<span data-ttu-id="b3d8b-121">A **Point** denotes a single position in space.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="b3d8b-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile, or a city.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile, or a city.</span></span>  <span data-ttu-id="b3d8b-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="b3d8b-124">Here's an example JSON for a point.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="b3d8b-125">**Points in Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="b3d8b-126">The GeoJSON specification specifies longitude first and latitude second.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-126">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="b3d8b-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="b3d8b-128">Longitude values are measured from the Prime Meridian and are between -180 degrees and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 degrees and 90.0 degrees.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-128">Longitude values are measured from the Prime Meridian and are between -180 degrees and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 degrees and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="b3d8b-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="b3d8b-130">See below for more details about coordinate reference systems.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-130">See below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="b3d8b-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span><span class="sxs-lookup"><span data-stu-id="b3d8b-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="b3d8b-132">**Use Profile with Location stored in Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

```json
{
    "id":"cosmosdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

<span data-ttu-id="b3d8b-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="b3d8b-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="b3d8b-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="b3d8b-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="b3d8b-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="b3d8b-138">Here's an example of a Polygon in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="b3d8b-139">**Polygons in GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-139">**Polygons in GeoJSON**</span></span>

```json
{
    "type":"Polygon",
    "coordinates":[ [
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ] ]
}
```

> [!NOTE]
> <span data-ttu-id="b3d8b-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="b3d8b-141">Points within a Polygon must be specified in counter-clockwise order.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="b3d8b-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="b3d8b-143">In addition to Point, LineString, and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-143">In addition to Point, LineString, and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="b3d8b-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="b3d8b-145">However Azure Cosmos DB only supports automatic indexing of points.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="b3d8b-146">Coordinate reference systems</span><span class="sxs-lookup"><span data-stu-id="b3d8b-146">Coordinate reference systems</span></span>
<span data-ttu-id="b3d8b-147">Since the shape of the earth is irregular, coordinates of geospatial data are represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-147">Since the shape of the earth is irregular, coordinates of geospatial data are represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="b3d8b-148">For example, the "National Grid of Britain" is a reference system is accurate for the United Kingdom, but not outside it.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-148">For example, the "National Grid of Britain" is a reference system is accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="b3d8b-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="b3d8b-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="b3d8b-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="b3d8b-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="b3d8b-152">Creating documents with spatial data</span><span class="sxs-lookup"><span data-stu-id="b3d8b-152">Creating documents with spatial data</span></span>
<span data-ttu-id="b3d8b-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the container.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the container.</span></span> <span data-ttu-id="b3d8b-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="b3d8b-155">**Create Document with Geospatial data in Node.js**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"cosmosdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within the callback
});
```

<span data-ttu-id="b3d8b-156">If you're working with the SQL APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-156">If you're working with the SQL APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span></span> <span data-ttu-id="b3d8b-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="b3d8b-158">**Create Document with Geospatial data in .NET**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-158">**Create Document with Geospatial data in .NET**</span></span>

```json
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
        Name = "cosmosdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

<span data-ttu-id="b3d8b-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="b3d8b-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="b3d8b-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="b3d8b-161">Querying spatial types</span><span class="sxs-lookup"><span data-stu-id="b3d8b-161">Querying spatial types</span></span>
<span data-ttu-id="b3d8b-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="b3d8b-163">Spatial SQL built-in functions</span><span class="sxs-lookup"><span data-stu-id="b3d8b-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="b3d8b-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="b3d8b-165">For more details on the complete set of built-in functions in the SQL language, see [Query Azure Cosmos DB](sql-api-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="b3d8b-165">For more details on the complete set of built-in functions in the SQL language, see [Query Azure Cosmos DB](sql-api-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="b3d8b-166"><strong>Usage</strong></span><span class="sxs-lookup"><span data-stu-id="b3d8b-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="b3d8b-167"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="b3d8b-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b3d8b-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="b3d8b-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="b3d8b-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b3d8b-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="b3d8b-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="b3d8b-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span><span class="sxs-lookup"><span data-stu-id="b3d8b-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b3d8b-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="b3d8b-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="b3d8b-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b3d8b-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="b3d8b-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="b3d8b-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="b3d8b-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="b3d8b-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="b3d8b-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="b3d8b-178">Spatial functions can be used to perform proximity queries against spatial data.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-178">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="b3d8b-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="b3d8b-180">**Query**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="b3d8b-181">**Results**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="b3d8b-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="b3d8b-183">For more details on spatial indexing, see the section below.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-183">For more details on spatial indexing, see the section below.</span></span> <span data-ttu-id="b3d8b-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span><span class="sxs-lookup"><span data-stu-id="b3d8b-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="b3d8b-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="b3d8b-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="b3d8b-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="b3d8b-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="b3d8b-189">Polygon arguments in ST_WITHIN can contain only a single ring, that is, the Polygons must not contain holes in them.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-189">Polygon arguments in ST_WITHIN can contain only a single ring, that is, the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="b3d8b-190">**Query**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="b3d8b-191">**Results**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="b3d8b-192">Similar to how mismatched types work in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it evaluates to **undefined** and the evaluated document to be skipped from the query results.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-192">Similar to how mismatched types work in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it evaluates to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="b3d8b-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatial type is invalid.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatial type is invalid.</span></span>     
> 
> 

<span data-ttu-id="b3d8b-194">Azure Cosmos DB also supports performing inverse queries, that is, you can index polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-194">Azure Cosmos DB also supports performing inverse queries, that is, you can index polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="b3d8b-195">This pattern is commonly used in logistics to identify, for example, when a truck enters or leaves a designated area.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-195">This pattern is commonly used in logistics to identify, for example, when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="b3d8b-196">**Query**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="b3d8b-197">**Results**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="b3d8b-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="b3d8b-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span><span class="sxs-lookup"><span data-stu-id="b3d8b-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="b3d8b-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="b3d8b-201">\*\* Query \*\*</span><span class="sxs-lookup"><span data-stu-id="b3d8b-201">\*\* Query \*\*</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="b3d8b-202">**Results**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="b3d8b-203">These functions can also be used to validate Polygons.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-203">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="b3d8b-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="b3d8b-205">**Query**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="b3d8b-206">**Results**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="b3d8b-207">LINQ Querying in the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b3d8b-207">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="b3d8b-208">The SQL .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-208">The SQL .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="b3d8b-209">The SQL LINQ provider translates this method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span><span class="sxs-lookup"><span data-stu-id="b3d8b-209">The SQL LINQ provider translates this method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="b3d8b-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30 km of the specified point using LINQ.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30 km of the specified point using LINQ.</span></span>

<span data-ttu-id="b3d8b-211">**LINQ query for Distance**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="b3d8b-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="b3d8b-213">**LINQ query for Within**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="b3d8b-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="b3d8b-215">Indexing</span><span class="sxs-lookup"><span data-stu-id="b3d8b-215">Indexing</span></span>
<span data-ttu-id="b3d8b-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="b3d8b-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons, and lines) represented in the GeoJSON standard.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons, and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="b3d8b-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="b3d8b-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="b3d8b-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, that is, all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, that is, all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span></span> <span data-ttu-id="b3d8b-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="b3d8b-222">If you specify an indexing policy that includes spatial index for /\* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="b3d8b-222">If you specify an indexing policy that includes spatial index for /\* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="b3d8b-223">Spatial indexes do not have a precision value, and always use a default precision value.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="b3d8b-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span><span class="sxs-lookup"><span data-stu-id="b3d8b-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="b3d8b-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, that is, index any GeoJSON point found within documents for spatial querying.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, that is, index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="b3d8b-226">If you are modifying the indexing policy using the Azure portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-226">If you are modifying the indexing policy using the Azure portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="b3d8b-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="b3d8b-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="b3d8b-229">**Create a collection with spatial indexing**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="b3d8b-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="b3d8b-231">**Modify an existing collection with spatial indexing**</span><span class="sxs-lookup"><span data-stu-id="b3d8b-231">**Modify an existing collection with spatial indexing**</span></span>

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
> <span data-ttu-id="b3d8b-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="b3d8b-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="b3d8b-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span><span class="sxs-lookup"><span data-stu-id="b3d8b-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b3d8b-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="b3d8b-235">Next steps</span></span>
<span data-ttu-id="b3d8b-236">Now that you have learned how to get started with geospatial support in Azure Cosmos DB, next you can:</span><span class="sxs-lookup"><span data-stu-id="b3d8b-236">Now that you have learned how to get started with geospatial support in Azure Cosmos DB, next you can:</span></span>

* <span data-ttu-id="b3d8b-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="b3d8b-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="b3d8b-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="b3d8b-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="b3d8b-239">Learn more about [Azure Cosmos DB Query](sql-api-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="b3d8b-239">Learn more about [Azure Cosmos DB Query](sql-api-sql-query.md)</span></span>
* <span data-ttu-id="b3d8b-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="b3d8b-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

