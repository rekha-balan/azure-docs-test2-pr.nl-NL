---
title: Extending GeoJSON geometries in Azure Maps | Microsoft Docs
description: Learn how to extend GeoJSON geometries in Azure Maps
author: sataneja
ms.author: sataneja
ms.date: 05/17/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.openlocfilehash: 319f9cba23d088553f361b6a0d648bbde94e0743
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966164"
---
# <a name="extending-geojson-geometries"></a><span data-ttu-id="632f3-103">Extending GeoJSON geometries</span><span class="sxs-lookup"><span data-stu-id="632f3-103">Extending GeoJSON geometries</span></span>

<span data-ttu-id="632f3-104">Azure Maps provides a list of powerful APIs to search inside/along geographical features.</span><span class="sxs-lookup"><span data-stu-id="632f3-104">Azure Maps provides a list of powerful APIs to search inside/along geographical features.</span></span>
<span data-ttu-id="632f3-105">These APIs standardize on [GeoJSON spec][1] for representing the geographical features (for example: state boundaries, routes).</span><span class="sxs-lookup"><span data-stu-id="632f3-105">These APIs standardize on [GeoJSON spec][1] for representing the geographical features (for example: state boundaries, routes).</span></span>  

<span data-ttu-id="632f3-106">The [GeoJSON spec][1] only supports the following geometries:</span><span class="sxs-lookup"><span data-stu-id="632f3-106">The [GeoJSON spec][1] only supports the following geometries:</span></span>

* <span data-ttu-id="632f3-107">GeometryCollection</span><span class="sxs-lookup"><span data-stu-id="632f3-107">GeometryCollection</span></span>
* <span data-ttu-id="632f3-108">LineString</span><span class="sxs-lookup"><span data-stu-id="632f3-108">LineString</span></span>
* <span data-ttu-id="632f3-109">MultiLineString</span><span class="sxs-lookup"><span data-stu-id="632f3-109">MultiLineString</span></span>
* <span data-ttu-id="632f3-110">MultiPoint</span><span class="sxs-lookup"><span data-stu-id="632f3-110">MultiPoint</span></span>
* <span data-ttu-id="632f3-111">MultiPolygon</span><span class="sxs-lookup"><span data-stu-id="632f3-111">MultiPolygon</span></span>
* <span data-ttu-id="632f3-112">Point</span><span class="sxs-lookup"><span data-stu-id="632f3-112">Point</span></span>
* <span data-ttu-id="632f3-113">Polygon</span><span class="sxs-lookup"><span data-stu-id="632f3-113">Polygon</span></span>

<span data-ttu-id="632f3-114">Some Azure Maps APIs (for example: [Search Inside Geometry](https://docs.microsoft.com/rest/api/maps/search/postsearchinsidegeometry)) accept geometries like "Circle", which are not part of the [GeoJSON spec][1].</span><span class="sxs-lookup"><span data-stu-id="632f3-114">Some Azure Maps APIs (for example: [Search Inside Geometry](https://docs.microsoft.com/rest/api/maps/search/postsearchinsidegeometry)) accept geometries like "Circle", which are not part of the [GeoJSON spec][1].</span></span>

<span data-ttu-id="632f3-115">This article provides a detailed explanation on how Azure Maps extends the [GeoJSON spec][1] to represent certain geometries.</span><span class="sxs-lookup"><span data-stu-id="632f3-115">This article provides a detailed explanation on how Azure Maps extends the [GeoJSON spec][1] to represent certain geometries.</span></span>

### <a name="circle"></a><span data-ttu-id="632f3-116">Circle</span><span class="sxs-lookup"><span data-stu-id="632f3-116">Circle</span></span>

<span data-ttu-id="632f3-117">The `Circle` geometry is not supported by the [GeoJSON spec][1]. We use the `GeoJSON Feature` object to represent a circle.</span><span class="sxs-lookup"><span data-stu-id="632f3-117">The `Circle` geometry is not supported by the [GeoJSON spec][1]. We use the `GeoJSON Feature` object to represent a circle.</span></span>

<span data-ttu-id="632f3-118">A `Circle` geometry represented using the `GeoJSON Feature` object __must__ contain the following:</span><span class="sxs-lookup"><span data-stu-id="632f3-118">A `Circle` geometry represented using the `GeoJSON Feature` object __must__ contain the following:</span></span>

1. <span data-ttu-id="632f3-119">Center</span><span class="sxs-lookup"><span data-stu-id="632f3-119">Center</span></span>
   ><span data-ttu-id="632f3-120">The circle's center is represented using a `GeoJSON Point` type.</span><span class="sxs-lookup"><span data-stu-id="632f3-120">The circle's center is represented using a `GeoJSON Point` type.</span></span>

2. <span data-ttu-id="632f3-121">Radius</span><span class="sxs-lookup"><span data-stu-id="632f3-121">Radius</span></span>
   ><span data-ttu-id="632f3-122">The circle's `radius` is represented using `GeoJSON Feature`'s properties.</span><span class="sxs-lookup"><span data-stu-id="632f3-122">The circle's `radius` is represented using `GeoJSON Feature`'s properties.</span></span> <span data-ttu-id="632f3-123">The radius value is in _meters_ and must be of the type `double`.</span><span class="sxs-lookup"><span data-stu-id="632f3-123">The radius value is in _meters_ and must be of the type `double`.</span></span>

3. <span data-ttu-id="632f3-124">SubType</span><span class="sxs-lookup"><span data-stu-id="632f3-124">SubType</span></span>
   ><span data-ttu-id="632f3-125">The circle geometry must also contain the `subType` property.</span><span class="sxs-lookup"><span data-stu-id="632f3-125">The circle geometry must also contain the `subType` property.</span></span> <span data-ttu-id="632f3-126">This property must be a part of the `GeoJSON Feature`'s properties and it's value should be _Circle_</span><span class="sxs-lookup"><span data-stu-id="632f3-126">This property must be a part of the `GeoJSON Feature`'s properties and it's value should be _Circle_</span></span>


#### <a name="example"></a><span data-ttu-id="632f3-127">Example</span><span class="sxs-lookup"><span data-stu-id="632f3-127">Example</span></span>

<span data-ttu-id="632f3-128">Here's how you'll represent a circle centered at (latitude: 47.639754, longitude: -122.126986) with a radius equal to 100 meters, using a `GeoJSON Feature` object:</span><span class="sxs-lookup"><span data-stu-id="632f3-128">Here's how you'll represent a circle centered at (latitude: 47.639754, longitude: -122.126986) with a radius equal to 100 meters, using a `GeoJSON Feature` object:</span></span>

```json            
{
    "type": "Feature",
    "geometry": {
        "type": "Point",
        "coordinates": [-122.126986, 47.639754]
    },
    "properties": {
        "subType": "Circle",
        "radius": 100
    }
}          
```

[1]: https://tools.ietf.org/html/rfc7946
