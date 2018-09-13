---
title: How to use the Azure Maps Map Control | Microsoft Docs
description: Learn how to use the Azure Maps Map Control client-side Javascript library.
author: dsk-2015
ms.author: dkshir
ms.date: 09/05/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: 5b8703c218790549a0cf5a319345132a0eca66ce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865134"
---
# <a name="how-to-use-the-azure-maps-map-control"></a><span data-ttu-id="c796e-103">How to use the Azure Maps Map Control</span><span class="sxs-lookup"><span data-stu-id="c796e-103">How to use the Azure Maps Map Control</span></span>
<span data-ttu-id="c796e-104">The Map Control client-side Javascript library allows you to render maps and embedded Azure Maps functionality into your web or mobile application.</span><span class="sxs-lookup"><span data-stu-id="c796e-104">The Map Control client-side Javascript library allows you to render maps and embedded Azure Maps functionality into your web or mobile application.</span></span> 

## <a name="create-a-new-map-in-a-web-page"></a><span data-ttu-id="c796e-105">Create a new map in a web page</span><span class="sxs-lookup"><span data-stu-id="c796e-105">Create a new map in a web page</span></span>

<span data-ttu-id="c796e-106">You can embed a map in a web page by using the Map Control client-side Javascript library.</span><span class="sxs-lookup"><span data-stu-id="c796e-106">You can embed a map in a web page by using the Map Control client-side Javascript library.</span></span>

1. <span data-ttu-id="c796e-107">Create a new file and name it MapSearch.html.</span><span class="sxs-lookup"><span data-stu-id="c796e-107">Create a new file and name it MapSearch.html.</span></span>

2. <span data-ttu-id="c796e-108">Add the Azure Maps stylesheet and script source references to the `<head>` element of the file:</span><span class="sxs-lookup"><span data-stu-id="c796e-108">Add the Azure Maps stylesheet and script source references to the `<head>` element of the file:</span></span>

    ```html
    <link rel="stylesheet" href="https://atlas.microsoft.com/sdk/css/atlas.min.css?api-version=1" type="text/css" />
    <script src="https://atlas.microsoft.com/sdk/js/atlas.min.js?api-version=1"></script>
    ```
    
3. <span data-ttu-id="c796e-109">In order to render a new map in your browser, add a **#map** reference in the `<style>` element.</span><span class="sxs-lookup"><span data-stu-id="c796e-109">In order to render a new map in your browser, add a **#map** reference in the `<style>` element.</span></span>

    ```html
    #map {
                width: 100%;
                height: 100%;
            }
    ``` 
    
4. <span data-ttu-id="c796e-110">In order to initialize the map control, define a new section in the html body and create a script.</span><span class="sxs-lookup"><span data-stu-id="c796e-110">In order to initialize the map control, define a new section in the html body and create a script.</span></span> <span data-ttu-id="c796e-111">Use your own Azure Maps account key in the script.</span><span class="sxs-lookup"><span data-stu-id="c796e-111">Use your own Azure Maps account key in the script.</span></span> <span data-ttu-id="c796e-112">If you need to create an account or find your key, see [How to manage your Azure Maps account and keys](how-to-manage-account-keys.md)</span><span class="sxs-lookup"><span data-stu-id="c796e-112">If you need to create an account or find your key, see [How to manage your Azure Maps account and keys](how-to-manage-account-keys.md)</span></span>

    ```html
    <div id="map">
        <script>
            var MapsAccountKey = "<_your account key_>";
            var map = new atlas.Map("map", {
                "subscription-key": MapsAccountKey,
                center: [-122.33263,47.59093],
                zoom: 12
            });
        </script>
    </div>
    ```
    
5. <span data-ttu-id="c796e-113">Open the file in your web browser and view the rendered map.</span><span class="sxs-lookup"><span data-stu-id="c796e-113">Open the file in your web browser and view the rendered map.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c796e-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="c796e-114">Next steps</span></span>

<span data-ttu-id="c796e-115">This article showed you how to create a basic map with your Azure Maps key.</span><span class="sxs-lookup"><span data-stu-id="c796e-115">This article showed you how to create a basic map with your Azure Maps key.</span></span> <span data-ttu-id="c796e-116">For more code examples to add to your maps, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="c796e-116">For more code examples to add to your maps, see the following articles:</span></span> 

* [<span data-ttu-id="c796e-117">Create a map</span><span class="sxs-lookup"><span data-stu-id="c796e-117">Create a map</span></span>](map-create.md)
* [<span data-ttu-id="c796e-118">Choose a map style</span><span class="sxs-lookup"><span data-stu-id="c796e-118">Choose a map style</span></span>](choose-map-style.md)
