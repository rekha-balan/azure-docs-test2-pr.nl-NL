---
title: Add custom html in Azure Maps | Microsoft Docs
description: How to add custom html to a Javascript map
author: jingjing-z
ms.author: jinzh
ms.date: 05/07/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.custom: codepen
ms.openlocfilehash: 5060839be244f55700b40735e598964a0b7b6709
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864564"
---
# <a name="add-custom-html-to-the-map"></a>Add custom HTML to the map

This article shows you how to add a custom HTML such as an image file to the map. 

## <a name="understand-the-code"></a>Understand the code

<iframe height='466' scrolling='no' title='Add custom html to a map - png' src='//codepen.io/azuremaps/embed/MVoeVw/?height=466&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/azuremaps/pen/MVoeVw/'>Add custom html to a map - png</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

In the code above, the first block of code constructs a map object. You can see [create a map](./map-create.md) for instructions.

The second block of code creates an HTML element from an image.

The last block of code uses [addHtml](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addhtml) function of the map class to add the image to the specified position of the map.

## <a name="next-steps"></a>Next steps

Learn more about the classes and methods used in this article: 
* [Map](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [addHtml](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addhtml)
    
For more code examples to add to your maps, see the following articles: 
* [Show search results](./map-search-location.md)
* [Get information from a coordinate](./map-get-information-from-coordinate.md)

