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
# <a name="add-custom-html-to-the-map"></a><span data-ttu-id="c66b5-103">Add custom HTML to the map</span><span class="sxs-lookup"><span data-stu-id="c66b5-103">Add custom HTML to the map</span></span>

<span data-ttu-id="c66b5-104">This article shows you how to add a custom HTML such as an image file to the map.</span><span class="sxs-lookup"><span data-stu-id="c66b5-104">This article shows you how to add a custom HTML such as an image file to the map.</span></span> 

## <a name="understand-the-code"></a><span data-ttu-id="c66b5-105">Understand the code</span><span class="sxs-lookup"><span data-stu-id="c66b5-105">Understand the code</span></span>

<iframe height='466' scrolling='no' title='<span data-ttu-id="c66b5-106">Add custom html to a map - png</span><span class="sxs-lookup"><span data-stu-id="c66b5-106">Add custom html to a map - png</span></span>' src='//codepen.io/azuremaps/embed/MVoeVw/?height=466&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="c66b5-107">See the Pen <a href='https://codepen.io/azuremaps/pen/MVoeVw/'>Add custom html to a map - png</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="c66b5-107">See the Pen <a href='https://codepen.io/azuremaps/pen/MVoeVw/'>Add custom html to a map - png</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="c66b5-108">In the code above, the first block of code constructs a map object.</span><span class="sxs-lookup"><span data-stu-id="c66b5-108">In the code above, the first block of code constructs a map object.</span></span> <span data-ttu-id="c66b5-109">You can see [create a map](./map-create.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="c66b5-109">You can see [create a map](./map-create.md) for instructions.</span></span>

<span data-ttu-id="c66b5-110">The second block of code creates an HTML element from an image.</span><span class="sxs-lookup"><span data-stu-id="c66b5-110">The second block of code creates an HTML element from an image.</span></span>

<span data-ttu-id="c66b5-111">The last block of code uses [addHtml](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addhtml) function of the map class to add the image to the specified position of the map.</span><span class="sxs-lookup"><span data-stu-id="c66b5-111">The last block of code uses [addHtml](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addhtml) function of the map class to add the image to the specified position of the map.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c66b5-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="c66b5-112">Next steps</span></span>

<span data-ttu-id="c66b5-113">Learn more about the classes and methods used in this article:</span><span class="sxs-lookup"><span data-stu-id="c66b5-113">Learn more about the classes and methods used in this article:</span></span> 
* [<span data-ttu-id="c66b5-114">Map</span><span class="sxs-lookup"><span data-stu-id="c66b5-114">Map</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="c66b5-115">addHtml</span><span class="sxs-lookup"><span data-stu-id="c66b5-115">addHtml</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#addhtml)
    
<span data-ttu-id="c66b5-116">For more code examples to add to your maps, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="c66b5-116">For more code examples to add to your maps, see the following articles:</span></span> 
* [<span data-ttu-id="c66b5-117">Show search results</span><span class="sxs-lookup"><span data-stu-id="c66b5-117">Show search results</span></span>](./map-search-location.md)
* [<span data-ttu-id="c66b5-118">Get information from a coordinate</span><span class="sxs-lookup"><span data-stu-id="c66b5-118">Get information from a coordinate</span></span>](./map-get-information-from-coordinate.md)

