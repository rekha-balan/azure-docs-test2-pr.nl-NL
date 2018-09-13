---
title: Making an accessible application with Azure Maps | Microsoft Docs
description: How to build an accessible application using Azure Maps
services: azure-maps
keywords: ''
author: chgennar
ms.author: chgennar
ms.date: 05/18/2018
ms.topic: article
ms.service: azure-maps
documentationcenter: ''
manager: timlt
ms.devlang: na
ms.openlocfilehash: 3fe0ba47e2e3529352ca8386dc7531a96a2689af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865215"
---
# <a name="building-an-accessible-application"></a><span data-ttu-id="c9186-103">Building an accessible application</span><span class="sxs-lookup"><span data-stu-id="c9186-103">Building an accessible application</span></span>

<span data-ttu-id="c9186-104">This article shows you how to build a map application that can be used by a screen reader.</span><span class="sxs-lookup"><span data-stu-id="c9186-104">This article shows you how to build a map application that can be used by a screen reader.</span></span>

## <a name="understand-the-code"></a><span data-ttu-id="c9186-105">Understand the code</span><span class="sxs-lookup"><span data-stu-id="c9186-105">Understand the code</span></span>

<iframe height='500' scrolling='no' title='<span data-ttu-id="c9186-106">Make an accessible application</span><span class="sxs-lookup"><span data-stu-id="c9186-106">Make an accessible application</span></span>' src='//codepen.io/azuremaps/embed/ZoVyZQ/?height=504&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="c9186-107">See the Pen <a href='https://codepen.io/azuremaps/pen/ZoVyZQ/'>Make an accessible application</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span><span class="sxs-lookup"><span data-stu-id="c9186-107">See the Pen <a href='https://codepen.io/azuremaps/pen/ZoVyZQ/'>Make an accessible application</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

<span data-ttu-id="c9186-108">The map is prebuilt with some accessibility features.</span><span class="sxs-lookup"><span data-stu-id="c9186-108">The map is prebuilt with some accessibility features.</span></span> <span data-ttu-id="c9186-109">A user can navigate the map using the keyboard and if a screen reader is running, the map will notify the user of changes to its state.</span><span class="sxs-lookup"><span data-stu-id="c9186-109">A user can navigate the map using the keyboard and if a screen reader is running, the map will notify the user of changes to its state.</span></span> <span data-ttu-id="c9186-110">For example, the user will be notified of the map's new latitude, longitude, zoom and locality when the map is panned or zoomed.</span><span class="sxs-lookup"><span data-stu-id="c9186-110">For example, the user will be notified of the map's new latitude, longitude, zoom and locality when the map is panned or zoomed.</span></span> <span data-ttu-id="c9186-111">Any additional information that is placed on the base map should have corresponding textual information for screen reader users.</span><span class="sxs-lookup"><span data-stu-id="c9186-111">Any additional information that is placed on the base map should have corresponding textual information for screen reader users.</span></span> <span data-ttu-id="c9186-112">Using [Popup](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest) is one way to achieve this.</span><span class="sxs-lookup"><span data-stu-id="c9186-112">Using [Popup](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest) is one way to achieve this.</span></span> <span data-ttu-id="c9186-113">In the above search example, a popup with textual information is added to the map for every pin that is placed on the map.</span><span class="sxs-lookup"><span data-stu-id="c9186-113">In the above search example, a popup with textual information is added to the map for every pin that is placed on the map.</span></span> <span data-ttu-id="c9186-114">Using the [Popup's](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest) attach method allows the popup to be seen by a screen reader without visually displaying the popup on the map.</span><span class="sxs-lookup"><span data-stu-id="c9186-114">Using the [Popup's](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest) attach method allows the popup to be seen by a screen reader without visually displaying the popup on the map.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9186-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="c9186-115">Next steps</span></span>

<span data-ttu-id="c9186-116">Learn more about the Popup class and its methods used in this article:</span><span class="sxs-lookup"><span data-stu-id="c9186-116">Learn more about the Popup class and its methods used in this article:</span></span>

* [<span data-ttu-id="c9186-117">Popup</span><span class="sxs-lookup"><span data-stu-id="c9186-117">Popup</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest)
    * [<span data-ttu-id="c9186-118">attach</span><span class="sxs-lookup"><span data-stu-id="c9186-118">attach</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#attach)
    * [<span data-ttu-id="c9186-119">remove</span><span class="sxs-lookup"><span data-stu-id="c9186-119">remove</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#remove)
    * [<span data-ttu-id="c9186-120">open</span><span class="sxs-lookup"><span data-stu-id="c9186-120">open</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#open)
    * [<span data-ttu-id="c9186-121">close</span><span class="sxs-lookup"><span data-stu-id="c9186-121">close</span></span>](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.popup?view=azure-iot-typescript-latest#close)

<span data-ttu-id="c9186-122">Check out our [code sample page](http://aka.ms/AzureMapsSamples) for more mapping scenarios.</span><span class="sxs-lookup"><span data-stu-id="c9186-122">Check out our [code sample page](http://aka.ms/AzureMapsSamples) for more mapping scenarios.</span></span>
