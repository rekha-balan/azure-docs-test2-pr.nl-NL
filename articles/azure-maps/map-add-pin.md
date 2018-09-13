---
title: Add a pin with Azure Maps | Microsoft Docs
description: How to add a pin to a Javascript map
author: jingjing-z
ms.author: jinzh
ms.date: 05/07/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.custom: codepen
ms.openlocfilehash: 0dafb09e1704e8e446b034975f0c25a740050599
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855914"
---
# <a name="add-pins-to-the-map"></a><span data-ttu-id="a5a61-103">Add pins to the map</span><span class="sxs-lookup"><span data-stu-id="a5a61-103">Add pins to the map</span></span>

<span data-ttu-id="a5a61-104">This article shows you how to add a pin to a map.</span><span class="sxs-lookup"><span data-stu-id="a5a61-104">This article shows you how to add a pin to a map.</span></span>  

## <a name="understand-the-code"></a><span data-ttu-id="a5a61-105">Understand the code</span><span class="sxs-lookup"><span data-stu-id="a5a61-105">Understand the code</span></span>

<iframe height='500' scrolling='no' title='<span data-ttu-id="a5a61-106">Add a pin to a map</span><span class="sxs-lookup"><span data-stu-id="a5a61-106">Add a pin to a map</span></span>' src='//codepen.io/azuremaps/embed/ZrVpEa/?height=504&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="a5a61-107">See the Pen <a href='https://codepen.io/azuremaps/pen/ZrVpEa/'>Add a pin to a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="a5a61-107">See the Pen <a href='https://codepen.io/azuremaps/pen/ZrVpEa/'>Add a pin to a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="a5a61-108">In the code above, the first block of code constructs a map object.</span><span class="sxs-lookup"><span data-stu-id="a5a61-108">In the code above, the first block of code constructs a map object.</span></span> <span data-ttu-id="a5a61-109">You can see [create a map](./map-create.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="a5a61-109">You can see [create a map](./map-create.md) for instructions.</span></span>

<span data-ttu-id="a5a61-110">In the second block of code, a pin is created and added to the map.</span><span class="sxs-lookup"><span data-stu-id="a5a61-110">In the second block of code, a pin is created and added to the map.</span></span> <span data-ttu-id="a5a61-111">A pin is a [Feature](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.data.feature?view=azure-iot-typescript-latest) of [Point](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.data.point?view=azure-iot-typescript-latest) with [PinProperties](https://docs.microsoft.com/javascript/api/azure-maps-control/models.pinproperties?view=azure-iot-typescript-latest) as its Feature property.</span><span class="sxs-lookup"><span data-stu-id="a5a61-111">A pin is a [Feature](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.data.feature?view=azure-iot-typescript-latest) of [Point](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.data.point?view=azure-iot-typescript-latest) with [PinProperties](https://docs.microsoft.com/javascript/api/azure-maps-control/models.pinproperties?view=azure-iot-typescript-latest) as its Feature property.</span></span> <span data-ttu-id="a5a61-112">Use `new atlas.data.Feature(new atlas.data.Point())` to create a pin and define its properties.</span><span class="sxs-lookup"><span data-stu-id="a5a61-112">Use `new atlas.data.Feature(new atlas.data.Point())` to create a pin and define its properties.</span></span> <span data-ttu-id="a5a61-113">A pin layer is an array of pins.</span><span class="sxs-lookup"><span data-stu-id="a5a61-113">A pin layer is an array of pins.</span></span> <span data-ttu-id="a5a61-114">Use [addPins](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addpins) function of the map class to add a pin layer to the map and define the properties of the pin layer.</span><span class="sxs-lookup"><span data-stu-id="a5a61-114">Use [addPins](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addpins) function of the map class to add a pin layer to the map and define the properties of the pin layer.</span></span> <span data-ttu-id="a5a61-115">See properties of a pin layer at [PinLayerOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/models.pinlayeroptions?view=azure-iot-typescript-latest).</span><span class="sxs-lookup"><span data-stu-id="a5a61-115">See properties of a pin layer at [PinLayerOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/models.pinlayeroptions?view=azure-iot-typescript-latest).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a5a61-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="a5a61-116">Next steps</span></span>

<span data-ttu-id="a5a61-117">Learn more about the classes and methods used in this article:</span><span class="sxs-lookup"><span data-stu-id="a5a61-117">Learn more about the classes and methods used in this article:</span></span> 
* [<span data-ttu-id="a5a61-118">Map</span><span class="sxs-lookup"><span data-stu-id="a5a61-118">Map</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="a5a61-119">addPins</span><span class="sxs-lookup"><span data-stu-id="a5a61-119">addPins</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addpins)
    
<span data-ttu-id="a5a61-120">For more code examples to add to your maps, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="a5a61-120">For more code examples to add to your maps, see the following articles:</span></span> 
* [<span data-ttu-id="a5a61-121">Add a popup</span><span class="sxs-lookup"><span data-stu-id="a5a61-121">Add a popup</span></span>](./map-add-popup.md)
* [<span data-ttu-id="a5a61-122">Add a shape</span><span class="sxs-lookup"><span data-stu-id="a5a61-122">Add a shape</span></span>](./map-add-shape.md)

