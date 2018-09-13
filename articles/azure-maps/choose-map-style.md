---
title: Map style functionalities in Azure Maps| Microsoft Docs
description: Learn about Azure Maps style related functionalities.
author: walsehgal
ms.author: v-musehg
ms.date: 08/31/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: 160752cd0467ef307f7a45b1e0d703c7ddd5d773
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867593"
---
# <a name="choose-a-map-style-in-azure-maps"></a><span data-ttu-id="f50f6-103">Choose a map style in Azure Maps</span><span class="sxs-lookup"><span data-stu-id="f50f6-103">Choose a map style in Azure Maps</span></span>
<span data-ttu-id="f50f6-104">Azure Maps has four different maps styles to choose from.</span><span class="sxs-lookup"><span data-stu-id="f50f6-104">Azure Maps has four different maps styles to choose from.</span></span> <span data-ttu-id="f50f6-105">For more about map styles, see [supported map styles in Azure Maps](./supported-map-styles.md).</span><span class="sxs-lookup"><span data-stu-id="f50f6-105">For more about map styles, see [supported map styles in Azure Maps](./supported-map-styles.md).</span></span> <span data-ttu-id="f50f6-106">This article shows how to use the style-related functionalities to set a style on map load, set a new style and use the style picker control.</span><span class="sxs-lookup"><span data-stu-id="f50f6-106">This article shows how to use the style-related functionalities to set a style on map load, set a new style and use the style picker control.</span></span>

## <a name="setting-style-on-map-load"></a><span data-ttu-id="f50f6-107">Setting style on map load</span><span class="sxs-lookup"><span data-stu-id="f50f6-107">Setting style on map load</span></span>

<iframe height='500' scrolling='no' title='<span data-ttu-id="f50f6-108">Setting the style on map load</span><span class="sxs-lookup"><span data-stu-id="f50f6-108">Setting the style on map load</span></span>' src='//codepen.io/azuremaps/embed/WKOQRq/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="f50f6-109">See the Pen <a href='https://codepen.io/azuremaps/pen/WKOQRq/'>Setting the style on map load</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="f50f6-109">See the Pen <a href='https://codepen.io/azuremaps/pen/WKOQRq/'>Setting the style on map load</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="f50f6-110">The code above creates a map object with the style set to Grayscale.</span><span class="sxs-lookup"><span data-stu-id="f50f6-110">The code above creates a map object with the style set to Grayscale.</span></span> <span data-ttu-id="f50f6-111">See [create a map](./map-create.md) for instructions on how to create a map.</span><span class="sxs-lookup"><span data-stu-id="f50f6-111">See [create a map](./map-create.md) for instructions on how to create a map.</span></span>

## <a name="updating-the-style"></a><span data-ttu-id="f50f6-112">Updating the style</span><span class="sxs-lookup"><span data-stu-id="f50f6-112">Updating the style</span></span>

<iframe height='500' scrolling='no' title='<span data-ttu-id="f50f6-113">Updating the style</span><span class="sxs-lookup"><span data-stu-id="f50f6-113">Updating the style</span></span>' src='//codepen.io/azuremaps/embed/yqXYzY/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="f50f6-114">See the Pen <a href='https://codepen.io/azuremaps/pen/yqXYzY/'>Updating the style</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="f50f6-114">See the Pen <a href='https://codepen.io/azuremaps/pen/yqXYzY/'>Updating the style</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="f50f6-115">The first block of code in the above code creates a map object without pre-setting the style.</span><span class="sxs-lookup"><span data-stu-id="f50f6-115">The first block of code in the above code creates a map object without pre-setting the style.</span></span> <span data-ttu-id="f50f6-116">See [create a map](./map-create.md) for instructions on how to create a map.</span><span class="sxs-lookup"><span data-stu-id="f50f6-116">See [create a map](./map-create.md) for instructions on how to create a map.</span></span>

<span data-ttu-id="f50f6-117">The second code clock uses the map's [setStyle](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setstyle) method to set the map style to satellite.</span><span class="sxs-lookup"><span data-stu-id="f50f6-117">The second code clock uses the map's [setStyle](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setstyle) method to set the map style to satellite.</span></span>

## <a name="adding-the-style-picker"></a><span data-ttu-id="f50f6-118">Adding the style picker</span><span class="sxs-lookup"><span data-stu-id="f50f6-118">Adding the style picker</span></span>

<iframe height='500' scrolling='no' title='<span data-ttu-id="f50f6-119">Adding the style picker</span><span class="sxs-lookup"><span data-stu-id="f50f6-119">Adding the style picker</span></span>' src='//codepen.io/azuremaps/embed/OwgyvG/?height=265&theme-id=0&default-tab=js,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="f50f6-120">See the Pen <a href='https://codepen.io/azuremaps/pen/OwgyvG/'>Adding the style picker</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="f50f6-120">See the Pen <a href='https://codepen.io/azuremaps/pen/OwgyvG/'>Adding the style picker</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="f50f6-121">The first code block in the above code creates a map object without pre-setting the style.</span><span class="sxs-lookup"><span data-stu-id="f50f6-121">The first code block in the above code creates a map object without pre-setting the style.</span></span> <span data-ttu-id="f50f6-122">See [create a map](./map-create.md) for instructions on how to create a map.</span><span class="sxs-lookup"><span data-stu-id="f50f6-122">See [create a map](./map-create.md) for instructions on how to create a map.</span></span>

<span data-ttu-id="f50f6-123">The second code block constructs a style selector using the atlas [StyleControl](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.control.stylecontrol?view=azure-iot-typescript-latest#stylecontrol) constructor.</span><span class="sxs-lookup"><span data-stu-id="f50f6-123">The second code block constructs a style selector using the atlas [StyleControl](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.control.stylecontrol?view=azure-iot-typescript-latest#stylecontrol) constructor.</span></span>

<span data-ttu-id="f50f6-124">A style picker enables style selection for the map.</span><span class="sxs-lookup"><span data-stu-id="f50f6-124">A style picker enables style selection for the map.</span></span> <span data-ttu-id="f50f6-125">The third code block adds the style picker to the map using the map's [addControl](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addcontrol) method.</span><span class="sxs-lookup"><span data-stu-id="f50f6-125">The third code block adds the style picker to the map using the map's [addControl](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addcontrol) method.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f50f6-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="f50f6-126">Next steps</span></span>

<span data-ttu-id="f50f6-127">Learn more about the classes and methods used in this article:</span><span class="sxs-lookup"><span data-stu-id="f50f6-127">Learn more about the classes and methods used in this article:</span></span> 
* [<span data-ttu-id="f50f6-128">Map</span><span class="sxs-lookup"><span data-stu-id="f50f6-128">Map</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="f50f6-129">setStyle</span><span class="sxs-lookup"><span data-stu-id="f50f6-129">setStyle</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setstyle)
    * [<span data-ttu-id="f50f6-130">addControl</span><span class="sxs-lookup"><span data-stu-id="f50f6-130">addControl</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addcontrol)

* [<span data-ttu-id="f50f6-131">Atlas</span><span class="sxs-lookup"><span data-stu-id="f50f6-131">Atlas</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="f50f6-132">StyleControl</span><span class="sxs-lookup"><span data-stu-id="f50f6-132">StyleControl</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.control.stylecontrol?view=azure-iot-typescript-latest#stylecontrol)
    
<span data-ttu-id="f50f6-133">For more code examples to add to your maps, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="f50f6-133">For more code examples to add to your maps, see the following articles:</span></span>
* [<span data-ttu-id="f50f6-134">Add map controls</span><span class="sxs-lookup"><span data-stu-id="f50f6-134">Add map controls</span></span>](./map-add-controls.md)
* [<span data-ttu-id="f50f6-135">Add a pin</span><span class="sxs-lookup"><span data-stu-id="f50f6-135">Add a pin</span></span>](./map-add-pin.md)
