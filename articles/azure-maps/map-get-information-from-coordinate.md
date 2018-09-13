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
# <a name="get-information-from-a-coordinate"></a><span data-ttu-id="b7dfc-103">Get information from a coordinate</span><span class="sxs-lookup"><span data-stu-id="b7dfc-103">Get information from a coordinate</span></span>

<span data-ttu-id="b7dfc-104">This article shows you how to make a reverse address search, and upon a mouse click show the address of the clicked location in a popup.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-104">This article shows you how to make a reverse address search, and upon a mouse click show the address of the clicked location in a popup.</span></span>

<span data-ttu-id="b7dfc-105">There are two ways to make a reverse address search, one is by querying the [Azure Maps Reverse Address Search API](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse) through a service module and the other is by making a [XMLHttpRequest](https://xhr.spec.whatwg.org/) to the API to query the address.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-105">There are two ways to make a reverse address search, one is by querying the [Azure Maps Reverse Address Search API](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse) through a service module and the other is by making a [XMLHttpRequest](https://xhr.spec.whatwg.org/) to the API to query the address.</span></span> <span data-ttu-id="b7dfc-106">We discuss both below.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-106">We discuss both below.</span></span>

## <a name="making-a-reverse-search-request-via-service-module"></a><span data-ttu-id="b7dfc-107">Making a reverse search request via service module</span><span class="sxs-lookup"><span data-stu-id="b7dfc-107">Making a reverse search request via service module</span></span>

### <a name="understand-the-code"></a><span data-ttu-id="b7dfc-108">Understand the code</span><span class="sxs-lookup"><span data-stu-id="b7dfc-108">Understand the code</span></span>

<iframe height='500' scrolling='no' title='<span data-ttu-id="b7dfc-109">Get information from a coordinate (Service Module)</span><span class="sxs-lookup"><span data-stu-id="b7dfc-109">Get information from a coordinate (Service Module)</span></span>' src='//codepen.io/azuremaps/embed/ejEYMZ/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="b7dfc-110">See the Pen <a href='https://codepen.io/azuremaps/pen/ejEYMZ/'>Get information from a coordinate (Service Module)</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-110">See the Pen <a href='https://codepen.io/azuremaps/pen/ejEYMZ/'>Get information from a coordinate (Service Module)</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="b7dfc-111">In the code above, the first block of code constructs a map object.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-111">In the code above, the first block of code constructs a map object.</span></span> <span data-ttu-id="b7dfc-112">You can see [create a map](./map-create.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-112">You can see [create a map](./map-create.md) for instructions.</span></span>

<span data-ttu-id="b7dfc-113">The line in the second block of code instantiates a service client.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-113">The line in the second block of code instantiates a service client.</span></span>

<span data-ttu-id="b7dfc-114">The third block of code updates the style of mouse cursor to a pointer.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-114">The third block of code updates the style of mouse cursor to a pointer.</span></span>

<span data-ttu-id="b7dfc-115">The fourth code block creates a popup.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-115">The fourth code block creates a popup.</span></span> <span data-ttu-id="b7dfc-116">You can see [add a popup on the map](./map-add-popup.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-116">You can see [add a popup on the map](./map-add-popup.md) for instructions.</span></span>

<span data-ttu-id="b7dfc-117">The last block of code adds an event listener for mouse clicks.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-117">The last block of code adds an event listener for mouse clicks.</span></span> <span data-ttu-id="b7dfc-118">Upon a mouse click, it creates a search query with the co-ordinates of the clicked point.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-118">Upon a mouse click, it creates a search query with the co-ordinates of the clicked point.</span></span> <span data-ttu-id="b7dfc-119">Then it uses the map's [getSearchAddressReverse](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.search?view=azure-iot-typescript-latest#getsearchaddressreverse) endpoint to query the address for the co-ordinates.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-119">Then it uses the map's [getSearchAddressReverse](https://docs.microsoft.com/javascript/api/azure-maps-rest/services.search?view=azure-iot-typescript-latest#getsearchaddressreverse) endpoint to query the address for the co-ordinates.</span></span>

<span data-ttu-id="b7dfc-120">For a successful response, it collects the address for the clicked location, and defines the popup content and position via [setPopupOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#setpopupoptions) function of the popup class.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-120">For a successful response, it collects the address for the clicked location, and defines the popup content and position via [setPopupOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#setpopupoptions) function of the popup class.</span></span>

## <a name="making-a-reverse-search-request-via-xmlhttprequest"></a><span data-ttu-id="b7dfc-121">Making a reverse search request via XMLHttpRequest</span><span class="sxs-lookup"><span data-stu-id="b7dfc-121">Making a reverse search request via XMLHttpRequest</span></span>

### <a name="understand-the-code"></a><span data-ttu-id="b7dfc-122">Understand the code</span><span class="sxs-lookup"><span data-stu-id="b7dfc-122">Understand the code</span></span>

<iframe height='500' scrolling='no' title='<span data-ttu-id="b7dfc-123">Get information from a coordinate</span><span class="sxs-lookup"><span data-stu-id="b7dfc-123">Get information from a coordinate</span></span>' src='//codepen.io/azuremaps/embed/ddXzoB/?height=516&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="b7dfc-124">See the Pen <a href='https://codepen.io/azuremaps/pen/ddXzoB/'>Get information from a coordinate</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-124">See the Pen <a href='https://codepen.io/azuremaps/pen/ddXzoB/'>Get information from a coordinate</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="b7dfc-125">In the code above, the first block of code constructs a map object.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-125">In the code above, the first block of code constructs a map object.</span></span> <span data-ttu-id="b7dfc-126">You can see [create a map](./map-create.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-126">You can see [create a map](./map-create.md) for instructions.</span></span>

<span data-ttu-id="b7dfc-127">The second block of code updates the style of mouse cursor to a pointer.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-127">The second block of code updates the style of mouse cursor to a pointer.</span></span>

<span data-ttu-id="b7dfc-128">The third block of code creates a popup.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-128">The third block of code creates a popup.</span></span> <span data-ttu-id="b7dfc-129">You can see [add a popup on the map](./map-add-popup.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-129">You can see [add a popup on the map](./map-add-popup.md) for instructions.</span></span>

<span data-ttu-id="b7dfc-130">The last code block adds an event listener for mouse clicks.</span><span class="sxs-lookup"><span data-stu-id="b7dfc-130">The last code block adds an event listener for mouse clicks.</span></span> <span data-ttu-id="b7dfc-131">Upon a mouse click, it sends an [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Reverse Address Search API](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse).</span><span class="sxs-lookup"><span data-stu-id="b7dfc-131">Upon a mouse click, it sends an [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Reverse Address Search API](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse).</span></span> <span data-ttu-id="b7dfc-132">For a successful response, it collects the address for the clicked location, and defines the popup content and position via [setPopupOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#setpopupoptions) function of the popup class</span><span class="sxs-lookup"><span data-stu-id="b7dfc-132">For a successful response, it collects the address for the clicked location, and defines the popup content and position via [setPopupOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#setpopupoptions) function of the popup class</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7dfc-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="b7dfc-133">Next steps</span></span>

<span data-ttu-id="b7dfc-134">Learn more about the classes and methods used in this article:</span><span class="sxs-lookup"><span data-stu-id="b7dfc-134">Learn more about the classes and methods used in this article:</span></span> 
* [<span data-ttu-id="b7dfc-135">Reverse address search</span><span class="sxs-lookup"><span data-stu-id="b7dfc-135">Reverse address search</span></span>](https://docs.microsoft.com/rest/api/maps/search/getsearchaddressreverse)
* [<span data-ttu-id="b7dfc-136">Map</span><span class="sxs-lookup"><span data-stu-id="b7dfc-136">Map</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="b7dfc-137">addEventListener</span><span class="sxs-lookup"><span data-stu-id="b7dfc-137">addEventListener</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addeventlistener)
* [<span data-ttu-id="b7dfc-138">Popup</span><span class="sxs-lookup"><span data-stu-id="b7dfc-138">Popup</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="b7dfc-139">setPopupOptions</span><span class="sxs-lookup"><span data-stu-id="b7dfc-139">setPopupOptions</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#setpopupoptions)
    * [<span data-ttu-id="b7dfc-140">open</span><span class="sxs-lookup"><span data-stu-id="b7dfc-140">open</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#open)
    * [<span data-ttu-id="b7dfc-141">close</span><span class="sxs-lookup"><span data-stu-id="b7dfc-141">close</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#close)

<span data-ttu-id="b7dfc-142">For more code examples to add to your maps, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="b7dfc-142">For more code examples to add to your maps, see the following articles:</span></span>
* [<span data-ttu-id="b7dfc-143">Show directions from A to B</span><span class="sxs-lookup"><span data-stu-id="b7dfc-143">Show directions from A to B</span></span>](./map-route.md)
* [<span data-ttu-id="b7dfc-144">Show traffic</span><span class="sxs-lookup"><span data-stu-id="b7dfc-144">Show traffic</span></span>](./map-show-traffic.md)
