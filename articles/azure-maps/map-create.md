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
# <a name="create-a-map"></a>Create a map

This article shows you how to create a map.  

## <a name="understand-the-code"></a>Understand the code

There are two ways you can construct a map. You can set the camera of the map by specifying the center point and zoom level, or set the camera bounds of the map by specifying the southwest bounding point and northeast bounding point.

<a id="setCameraOptions"></a>

### <a name="setting-the-camera"></a>Setting the camera

<iframe height='310' scrolling='no' title='Create a map via CameraOptions' src='//codepen.io/azuremaps/embed/qxKBMN/?height=265&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/azuremaps/pen/qxKBMN/'>Create a map via CameraOptions</a> by Azure LBS (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

In the code above, a [map object](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest) is created via `new atlas.Map()`. Map properties such as center and zoom level are part of [CameraOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraoptions?view=azure-iot-typescript-latest). CameraOptions can be defined in map constructor or via [setCamera](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamera) function of the map class.

<a id="setCameraBoundsOptions"></a>

### <a name="setting-the-camera-bounds"></a>Setting the camera bounds

<iframe height='310' scrolling='no' title='Create a map via CameraBoundsOptions' src='//codepen.io/azuremaps/embed/ZrRbPg/?height=265&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/azuremaps/pen/ZrRbPg/'>Create a map via CameraBoundsOptions</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

In the code above, a [map object](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest) is constructed via `new atlas.Map()`. Map properties such as bounding box are part of [CameraBoundsOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/models.cameraboundsoptions?view=azure-iot-typescript-latest). CameraBoundsOptions can be defined via [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamerabounds) function of the map class.

## <a name="try-out-the-code"></a>Try out the code 

Take a look at the sample code above. You can edit the JavaScript code on the JS tab on the left, and see the map view changes on the Result tab on the right. You can also click on the “Edit on CodePen” button and edit the code in CodePen. 

<a id="relatedReference"></a>

## <a name="next-steps"></a>Next steps

Learn more about the classes and methods used in this article: 
* [Map](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [setCamera](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamera)
    * [setCameraBounds](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamerabounds)
    
For more code examples to add to your maps, see the following articles: 
* [Choose a map style](choose-map-style.md)
* [Add map controls](map-add-controls.md)
    

