---
title: Create a map with Azure Maps | Microsoft Docs
description: How to create a Javascript map
author: jingjing-z
ms.author: jinzh
ms.date: 05/07/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.custom: codepen
ms.openlocfilehash: c5d48e2e7316f33a565fc61a769a29c00834eed5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869012"
---
# <a name="create-a-map"></a><span data-ttu-id="c14db-103">Create a map</span><span class="sxs-lookup"><span data-stu-id="c14db-103">Create a map</span></span>

<span data-ttu-id="c14db-104">This article shows you how to create a map.</span><span class="sxs-lookup"><span data-stu-id="c14db-104">This article shows you how to create a map.</span></span>  

## <a name="understand-the-code"></a><span data-ttu-id="c14db-105">Understand the code</span><span class="sxs-lookup"><span data-stu-id="c14db-105">Understand the code</span></span>

<span data-ttu-id="c14db-106">There are two ways you can construct a map.</span><span class="sxs-lookup"><span data-stu-id="c14db-106">There are two ways you can construct a map.</span></span> <span data-ttu-id="c14db-107">You can set the camera of the map by specifying the center point and zoom level, or set the camera bounds of the map by specifying the southwest bounding point and northeast bounding point.</span><span class="sxs-lookup"><span data-stu-id="c14db-107">You can set the camera of the map by specifying the center point and zoom level, or set the camera bounds of the map by specifying the southwest bounding point and northeast bounding point.</span></span>

<a id="setCameraOptions"></a>

### <a name="setting-the-camera"></a><span data-ttu-id="c14db-108">Setting the camera</span><span class="sxs-lookup"><span data-stu-id="c14db-108">Setting the camera</span></span>

<iframe height='310' scrolling='no' title='<span data-ttu-id="c14db-109">Create a map via CameraOptions</span><span class="sxs-lookup"><span data-stu-id="c14db-109">Create a map via CameraOptions</span></span>' src='//codepen.io/azuremaps/embed/qxKBMN/?height=265&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="c14db-110">See the Pen <a href='https://codepen.io/azuremaps/pen/qxKBMN/'>Create a map via CameraOptions</a> by Azure LBS (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="c14db-110">See the Pen <a href='https://codepen.io/azuremaps/pen/qxKBMN/'>Create a map via CameraOptions</a> by Azure LBS (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="c14db-111">In the code above, a [map object](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest) is created via `new atlas.Map()`.</span><span class="sxs-lookup"><span data-stu-id="c14db-111">In the code above, a [map object](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest) is created via `new atlas.Map()`.</span></span> <span data-ttu-id="c14db-112">Map properties such as center and zoom level are part of [CameraOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraoptions?view=azure-iot-typescript-latest).</span><span class="sxs-lookup"><span data-stu-id="c14db-112">Map properties such as center and zoom level are part of [CameraOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraoptions?view=azure-iot-typescript-latest).</span></span> <span data-ttu-id="c14db-113">CameraOptions can be defined in map constructor or via [setCamera](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamera) function of the map class.</span><span class="sxs-lookup"><span data-stu-id="c14db-113">CameraOptions can be defined in map constructor or via [setCamera](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamera) function of the map class.</span></span>

<a id="setCameraBoundsOptions"></a>

### <a name="setting-the-camera-bounds"></a><span data-ttu-id="c14db-114">Setting the camera bounds</span><span class="sxs-lookup"><span data-stu-id="c14db-114">Setting the camera bounds</span></span>

<iframe height='310' scrolling='no' title='<span data-ttu-id="c14db-115">Create a map via CameraBoundsOptions</span><span class="sxs-lookup"><span data-stu-id="c14db-115">Create a map via CameraBoundsOptions</span></span>' src='//codepen.io/azuremaps/embed/ZrRbPg/?height=265&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="c14db-116">See the Pen <a href='https://codepen.io/azuremaps/pen/ZrRbPg/'>Create a map via CameraBoundsOptions</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="c14db-116">See the Pen <a href='https://codepen.io/azuremaps/pen/ZrRbPg/'>Create a map via CameraBoundsOptions</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="c14db-117">In the code above, a [map object](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest) is constructed via `new atlas.Map()`.</span><span class="sxs-lookup"><span data-stu-id="c14db-117">In the code above, a [map object](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest) is constructed via `new atlas.Map()`.</span></span> <span data-ttu-id="c14db-118">Map properties such as bounding box are part of [CameraBoundsOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraboundsoptions?view=azure-iot-typescript-latest).</span><span class="sxs-lookup"><span data-stu-id="c14db-118">Map properties such as bounding box are part of [CameraBoundsOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraboundsoptions?view=azure-iot-typescript-latest).</span></span> <span data-ttu-id="c14db-119">CameraBoundsOptions can be defined via [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamerabounds) function of the map class.</span><span class="sxs-lookup"><span data-stu-id="c14db-119">CameraBoundsOptions can be defined via [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamerabounds) function of the map class.</span></span>

## <a name="try-out-the-code"></a><span data-ttu-id="c14db-120">Try out the code</span><span class="sxs-lookup"><span data-stu-id="c14db-120">Try out the code</span></span> 

<span data-ttu-id="c14db-121">Take a look at the sample code above.</span><span class="sxs-lookup"><span data-stu-id="c14db-121">Take a look at the sample code above.</span></span> <span data-ttu-id="c14db-122">You can edit the JavaScript code on the JS tab on the left, and see the map view changes on the Result tab on the right.</span><span class="sxs-lookup"><span data-stu-id="c14db-122">You can edit the JavaScript code on the JS tab on the left, and see the map view changes on the Result tab on the right.</span></span> <span data-ttu-id="c14db-123">You can also click on the “Edit on CodePen” button and edit the code in CodePen.</span><span class="sxs-lookup"><span data-stu-id="c14db-123">You can also click on the “Edit on CodePen” button and edit the code in CodePen.</span></span> 

<a id="relatedReference"></a>

## <a name="next-steps"></a><span data-ttu-id="c14db-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="c14db-124">Next steps</span></span>

<span data-ttu-id="c14db-125">Learn more about the classes and methods used in this article:</span><span class="sxs-lookup"><span data-stu-id="c14db-125">Learn more about the classes and methods used in this article:</span></span> 
* [<span data-ttu-id="c14db-126">Map</span><span class="sxs-lookup"><span data-stu-id="c14db-126">Map</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="c14db-127">setCamera</span><span class="sxs-lookup"><span data-stu-id="c14db-127">setCamera</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamera)
    * [<span data-ttu-id="c14db-128">setCameraBounds</span><span class="sxs-lookup"><span data-stu-id="c14db-128">setCameraBounds</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamerabounds)
    
<span data-ttu-id="c14db-129">For more code examples to add to your maps, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="c14db-129">For more code examples to add to your maps, see the following articles:</span></span> 
* [<span data-ttu-id="c14db-130">Choose a map style</span><span class="sxs-lookup"><span data-stu-id="c14db-130">Choose a map style</span></span>](choose-map-style.md)
* [<span data-ttu-id="c14db-131">Add map controls</span><span class="sxs-lookup"><span data-stu-id="c14db-131">Add map controls</span></span>](map-add-controls.md)
    

