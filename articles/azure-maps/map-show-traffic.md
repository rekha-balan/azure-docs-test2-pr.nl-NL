---
title: Show traffic with Azure Maps | Microsoft Docs
description: How to display traffic data on a Javascript map
author: jingjing-z
ms.author: jinzh
ms.date: 05/07/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.custom: codepen
ms.openlocfilehash: 2499822db587dbf47dccedf6039d0fb5823c58b5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866044"
---
# <a name="show-traffic-on-the-map"></a><span data-ttu-id="93499-103">Show traffic on the map</span><span class="sxs-lookup"><span data-stu-id="93499-103">Show traffic on the map</span></span>

<span data-ttu-id="93499-104">This article shows you how to show traffic and incidents information on the map.</span><span class="sxs-lookup"><span data-stu-id="93499-104">This article shows you how to show traffic and incidents information on the map.</span></span> 

## <a name="understand-the-code"></a><span data-ttu-id="93499-105">Understand the code</span><span class="sxs-lookup"><span data-stu-id="93499-105">Understand the code</span></span>

<iframe height='456' scrolling='no' title='<span data-ttu-id="93499-106">Show traffic on a map</span><span class="sxs-lookup"><span data-stu-id="93499-106">Show traffic on a map</span></span>' src='//codepen.io/azuremaps/embed/WMLRPw/?height=456&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="93499-107">See the Pen <a href='https://codepen.io/azuremaps/pen/WMLRPw/'>Show traffic on a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="93499-107">See the Pen <a href='https://codepen.io/azuremaps/pen/WMLRPw/'>Show traffic on a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="93499-108">In the code above, the first block of code constructs a map object.</span><span class="sxs-lookup"><span data-stu-id="93499-108">In the code above, the first block of code constructs a map object.</span></span> <span data-ttu-id="93499-109">You can see [create a map](map-create.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="93499-109">You can see [create a map](map-create.md) for instructions.</span></span>

<span data-ttu-id="93499-110">The second block of code uses [setTraffic](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#settraffic) function of the map class to render the traffic flows and incidents on the map.</span><span class="sxs-lookup"><span data-stu-id="93499-110">The second block of code uses [setTraffic](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#settraffic) function of the map class to render the traffic flows and incidents on the map.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93499-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="93499-111">Next steps</span></span>

<span data-ttu-id="93499-112">Learn more about the classes and methods used in this article:</span><span class="sxs-lookup"><span data-stu-id="93499-112">Learn more about the classes and methods used in this article:</span></span> 
* [<span data-ttu-id="93499-113">Map</span><span class="sxs-lookup"><span data-stu-id="93499-113">Map</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="93499-114">setTraffic</span><span class="sxs-lookup"><span data-stu-id="93499-114">setTraffic</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#settraffic)

<span data-ttu-id="93499-115">For more code examples to add to your maps, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="93499-115">For more code examples to add to your maps, see the following articles:</span></span> 
* [<span data-ttu-id="93499-116">Interacting with the map – mouse events</span><span class="sxs-lookup"><span data-stu-id="93499-116">Interacting with the map – mouse events</span></span>](./map-events.md)
* [<span data-ttu-id="93499-117">Building an accessible map</span><span class="sxs-lookup"><span data-stu-id="93499-117">Building an accessible map</span></span>](./map-accessibility.md)

<span data-ttu-id="93499-118">Check out our [code sample page](http://aka.ms/AzureMapsSamples) for more mapping scenarios.</span><span class="sxs-lookup"><span data-stu-id="93499-118">Check out our [code sample page](http://aka.ms/AzureMapsSamples) for more mapping scenarios.</span></span>
