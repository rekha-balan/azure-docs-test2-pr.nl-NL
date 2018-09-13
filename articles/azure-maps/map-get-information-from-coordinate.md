---
title: Show information about a coordinate with Azure Maps | Microsoft Docs
description: How to display information about an address on the map when a user selects a coordinate
author: jingjing-z
ms.author: jinzh
ms.date: 09/08/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.custom: codepen
ms.openlocfilehash: 993d1da4b2a99ec0f30a5a685835d9f6b6d35a9e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868113"
---
# <a name="get-information-from-a-coordinate"></a>Get information from a coordinate

This article shows you how to make a reverse address search, and upon a mouse click show the address of the clicked location in a popup.

There are two ways to make a reverse address search, one is by querying the [Azure Maps Reverse Address Search API](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse) through a service module and the other is by making a [XMLHttpRequest](https://xhr.spec.whatwg.org/) to the API to query the address. We discuss both below.

## <a name="making-a-reverse-search-request-via-service-module"></a>Making a reverse search request via service module

### <a name="understand-the-code"></a>Understand the code

<iframe height='500' scrolling='no' title='Get information from a coordinate (Service Module)' src='//codepen.io/azuremaps/embed/ejEYMZ/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/azuremaps/pen/ejEYMZ/'>Get information from a coordinate (Service Module)</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

In the code above, the first block of code constructs a map object. You can see [create a map](./map-create.md) for instructions.

The line in the second block of code instantiates a service client.

The third block of code updates the style of mouse cursor to a pointer.

The fourth code block creates a popup. You can see [add a popup on the map](./map-add-popup.md) for instructions.

The last block of code adds an event listener for mouse clicks. Upon a mouse click, it creates a search query with the co-ordinates of the clicked point. Then it uses the map's [getSearchAddressReverse](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.search?view=azure-iot-typescript-latest#getsearchaddressreverse) endpoint to query the address for the co-ordinates.

For a successful response, it collects the address for the clicked location, and defines the popup content and position via [setPopupOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#setpopupoptions) function of the popup class.

## <a name="making-a-reverse-search-request-via-xmlhttprequest"></a>Making a reverse search request via XMLHttpRequest

### <a name="understand-the-code"></a>Understand the code

<iframe height='500' scrolling='no' title='Get information from a coordinate' src='//codepen.io/azuremaps/embed/ddXzoB/?height=516&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/azuremaps/pen/ddXzoB/'>Get information from a coordinate</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

In the code above, the first block of code constructs a map object. You can see [create a map](./map-create.md) for instructions.

The second block of code updates the style of mouse cursor to a pointer.

The third block of code creates a popup. You can see [add a popup on the map](./map-add-popup.md) for instructions.

The last code block adds an event listener for mouse clicks. Upon a mouse click, it sends an [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Reverse Address Search API](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse). For a successful response, it collects the address for the clicked location, and defines the popup content and position via [setPopupOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#setpopupoptions) function of the popup class

## <a name="next-steps"></a>Next steps

Learn more about the classes and methods used in this article: 
* [Reverse address search](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse)
* [Map](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [addEventListener](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addeventlistener)
* [Popup](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest)
    * [setPopupOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#setpopupoptions)
    * [open](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#open)
    * [close](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#close)

For more code examples to add to your maps, see the following articles:
* [Show directions from A to B](./map-route.md)
* [Show traffic](./map-show-traffic.md)
