---
title: Add a popup with Azure Maps | Microsoft Docs
description: How to add a popup to Javascript map
author: jingjing-z
ms.author: jinzh
ms.date: 05/07/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.custom: codepen
ms.openlocfilehash: 0f86578e33e5c6a2d6528e2deb1c8068a0c94d01
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856068"
---
# <a name="add-a-popup-to-the-map"></a><span data-ttu-id="f6f89-103">Add a popup to the map</span><span class="sxs-lookup"><span data-stu-id="f6f89-103">Add a popup to the map</span></span>

<span data-ttu-id="f6f89-104">This article shows you how to add a popup to a map.</span><span class="sxs-lookup"><span data-stu-id="f6f89-104">This article shows you how to add a popup to a map.</span></span>  

## <a name="understand-the-code"></a><span data-ttu-id="f6f89-105">Understand the code</span><span class="sxs-lookup"><span data-stu-id="f6f89-105">Understand the code</span></span>

<a id="addAPopup"></a>

<iframe height='500' scrolling='no' title='<span data-ttu-id="f6f89-106">Add a popup to a map</span><span class="sxs-lookup"><span data-stu-id="f6f89-106">Add a popup to a map</span></span>' src='//codepen.io/azuremaps/embed/zRyKxj/?height=545&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="f6f89-107">See the Pen <a href='https://codepen.io/azuremaps/pen/zRyKxj/'>Add a popup to a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="f6f89-107">See the Pen <a href='https://codepen.io/azuremaps/pen/zRyKxj/'>Add a popup to a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="f6f89-108">In the code above, the first block of code constructs a map object.</span><span class="sxs-lookup"><span data-stu-id="f6f89-108">In the code above, the first block of code constructs a map object.</span></span> <span data-ttu-id="f6f89-109">You can see [create a map](./map-create.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="f6f89-109">You can see [create a map](./map-create.md) for instructions.</span></span>

<span data-ttu-id="f6f89-110">The second block of code creates a pin and add it to the map.</span><span class="sxs-lookup"><span data-stu-id="f6f89-110">The second block of code creates a pin and add it to the map.</span></span> <span data-ttu-id="f6f89-111">You can see [add a pin to the map](./map-add-pin.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="f6f89-111">You can see [add a pin to the map](./map-add-pin.md) for instructions.</span></span>

<span data-ttu-id="f6f89-112">The third block of code creates content to be displayed within a popup.</span><span class="sxs-lookup"><span data-stu-id="f6f89-112">The third block of code creates content to be displayed within a popup.</span></span> <span data-ttu-id="f6f89-113">Popup content is HTML element.</span><span class="sxs-lookup"><span data-stu-id="f6f89-113">Popup content is HTML element.</span></span> 

<span data-ttu-id="f6f89-114">The fourth block of code creates a [popup object](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest) via `new atlas.Popup()`.</span><span class="sxs-lookup"><span data-stu-id="f6f89-114">The fourth block of code creates a [popup object](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest) via `new atlas.Popup()`.</span></span> <span data-ttu-id="f6f89-115">Popup properties such as content and position are part of [PopupOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/models.popupoptions?view=azure-iot-typescript-latest).</span><span class="sxs-lookup"><span data-stu-id="f6f89-115">Popup properties such as content and position are part of [PopupOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/models.popupoptions?view=azure-iot-typescript-latest).</span></span> <span data-ttu-id="f6f89-116">PopupOptions can be defined in popup constructor or via [setPopupOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#setpopupoptions) function of the popup class.</span><span class="sxs-lookup"><span data-stu-id="f6f89-116">PopupOptions can be defined in popup constructor or via [setPopupOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#setpopupoptions) function of the popup class.</span></span>

<span data-ttu-id="f6f89-117">The last block of code uses [addEventListener](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addeventlistener) function of the map class to listen for mouseover event on the pins, and uses [open](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#open) function of the popup class to open the popup if the event occurs.</span><span class="sxs-lookup"><span data-stu-id="f6f89-117">The last block of code uses [addEventListener](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addeventlistener) function of the map class to listen for mouseover event on the pins, and uses [open](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#open) function of the popup class to open the popup if the event occurs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f6f89-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6f89-118">Next steps</span></span>

<span data-ttu-id="f6f89-119">Learn more about the classes and methods used in this article:</span><span class="sxs-lookup"><span data-stu-id="f6f89-119">Learn more about the classes and methods used in this article:</span></span> 

* [<span data-ttu-id="f6f89-120">Map</span><span class="sxs-lookup"><span data-stu-id="f6f89-120">Map</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="f6f89-121">addPins</span><span class="sxs-lookup"><span data-stu-id="f6f89-121">addPins</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addpins)
    * [<span data-ttu-id="f6f89-122">addEventListener</span><span class="sxs-lookup"><span data-stu-id="f6f89-122">addEventListener</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addeventlistener)
* [<span data-ttu-id="f6f89-123">Popup</span><span class="sxs-lookup"><span data-stu-id="f6f89-123">Popup</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="f6f89-124">setPopupOptions</span><span class="sxs-lookup"><span data-stu-id="f6f89-124">setPopupOptions</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#setpopupoptions)
    * [<span data-ttu-id="f6f89-125">open</span><span class="sxs-lookup"><span data-stu-id="f6f89-125">open</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#open)
    * [<span data-ttu-id="f6f89-126">close</span><span class="sxs-lookup"><span data-stu-id="f6f89-126">close</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#close)
    
<span data-ttu-id="f6f89-127">For more code examples to add to your maps, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="f6f89-127">For more code examples to add to your maps, see the following articles:</span></span> 
* [<span data-ttu-id="f6f89-128">Add a shape</span><span class="sxs-lookup"><span data-stu-id="f6f89-128">Add a shape</span></span>](./map-add-shape.md)
* [<span data-ttu-id="f6f89-129">Add custom HTML</span><span class="sxs-lookup"><span data-stu-id="f6f89-129">Add custom HTML</span></span>](./map-add-custom-html.md)
