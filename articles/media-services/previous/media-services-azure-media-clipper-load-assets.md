---
title: Load assets into Azure Media Clipper | Microsoft Docs
description: Steps for loading assets into Azure Media Clipper
services: media-services
keywords: clip;subclip;encoding;media
author: dbgeorge
manager: jasonsue
ms.author: dwgeo
ms.date: 11/10/2017
ms.topic: article
ms.service: media-services
ms.openlocfilehash: 6a479218ff8bd5addf4273b23c06380859e0ea08
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866165"
---
# <a name="loading-assets-into-azure-media-clipper"></a><span data-ttu-id="fb1f6-104">Loading assets into Azure Media Clipper</span><span class="sxs-lookup"><span data-stu-id="fb1f6-104">Loading assets into Azure Media Clipper</span></span>
<span data-ttu-id="fb1f6-105">Assets can be loaded into the Azure Media Clipper by two methods:</span><span class="sxs-lookup"><span data-stu-id="fb1f6-105">Assets can be loaded into the Azure Media Clipper by two methods:</span></span>
1. <span data-ttu-id="fb1f6-106">Statically passing in a library of assets</span><span class="sxs-lookup"><span data-stu-id="fb1f6-106">Statically passing in a library of assets</span></span>
2. <span data-ttu-id="fb1f6-107">Dynamically generating a list of assets via API</span><span class="sxs-lookup"><span data-stu-id="fb1f6-107">Dynamically generating a list of assets via API</span></span>

## <a name="statically-load-videos-into-clipper"></a><span data-ttu-id="fb1f6-108">Statically load videos into Clipper</span><span class="sxs-lookup"><span data-stu-id="fb1f6-108">Statically load videos into Clipper</span></span>
<span data-ttu-id="fb1f6-109">Statically load videos into the Clipper to enable end users to build clips without selecting videos from the asset selection panel.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-109">Statically load videos into the Clipper to enable end users to build clips without selecting videos from the asset selection panel.</span></span>

<span data-ttu-id="fb1f6-110">In this case, you pass in a static set of assets to the Clipper.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-110">In this case, you pass in a static set of assets to the Clipper.</span></span> <span data-ttu-id="fb1f6-111">Each asset includes an AMS asset/filter ID, name, published streaming URL.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-111">Each asset includes an AMS asset/filter ID, name, published streaming URL.</span></span> <span data-ttu-id="fb1f6-112">If applicable, a content protection authentication token or array of thumbnail URLs may be passed in.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-112">If applicable, a content protection authentication token or array of thumbnail URLs may be passed in.</span></span> <span data-ttu-id="fb1f6-113">If passed in, the thumbnails are populated into the interface.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-113">If passed in, the thumbnails are populated into the interface.</span></span> <span data-ttu-id="fb1f6-114">In scenarios where the asset library is static and small, you can pass in the asset contract for each asset in the library.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-114">In scenarios where the asset library is static and small, you can pass in the asset contract for each asset in the library.</span></span>

> [!NOTE]
> <span data-ttu-id="fb1f6-115">When statically loading assets into the Clipper, assets are added **directly to the timeline** and the **asset pane is not rendered**.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-115">When statically loading assets into the Clipper, assets are added **directly to the timeline** and the **asset pane is not rendered**.</span></span> <span data-ttu-id="fb1f6-116">The first asset is added to the timeline and the rest of the assets are stacked at the right side of the timeline).</span><span class="sxs-lookup"><span data-stu-id="fb1f6-116">The first asset is added to the timeline and the rest of the assets are stacked at the right side of the timeline).</span></span>

<span data-ttu-id="fb1f6-117">To load a static asset library, use the **load** method to pass in a JSON representation of each asset.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-117">To load a static asset library, use the **load** method to pass in a JSON representation of each asset.</span></span> <span data-ttu-id="fb1f6-118">The following code sample illustrates the JSON representation for one asset.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-118">The following code sample illustrates the JSON representation for one asset.</span></span>

```javascript
var assets = [
    {
      /* Required: represents the Azure Media Services asset Id when "type" === "asset"; otherwise, represents the dynamic manifest asset filter Id ("type" === "filter")  */
      "id": "my-asset-or-dynamic-manifest-asset-filter-id",
    
      /* Required: represents the asset name as shown in the Clipper interface */
      "name": "My Asset or Dynamic Manifest Asset Filter Name",
    
      /* Required: must be one of the following values: "asset" or "filter" */
      /* NOTE: "asset" type represents a rendered asset; "filter" type represents a dynamic manifest asset filter */
      "type": "asset",
    
      /* Required */
      "source": {
    
        /* Required: represents the asset streaming locator, the base Smooth Streaming URL */
        "src": "//amssamples.streaming.mediaservices.windows.net/91492735-c523-432b-ba01-faba6c2206a2/AzureMediaServicesPromo.ism/manifest",
    
        /* Optional: default value "application/vnd.ms-sstr+xml" */
        "type": "application/vnd.ms-sstr+xml",
    
        /* Required: If the asset has content protection applied, then you must include an array with the different protection types along with the token to request the license/key; otherwise, provide an empty array */
        "protectionInfo": [{
            "type": "AES",
            "authenticationToken": "Bearer aes-token-placeholder"
          },
          {
            "type": "PlayReady",
            "authenticationToken": "Bearer playready-token-placeholder"
          },
          {
            "type": "Widevine",
            "authenticationToken": "Bearer widevine-token-placeholder"
          },
          {
            "type": "FairPlay",
            "certificateUrl": "//example/path/to/myfairplay.der",
            "authenticationToken": "Bearer fairplay-token-placeholder"
          }
        ]
      },
    
      /* Optional: array containing thumbnail URLs for the video. */
      /* NOTE: For the thumbnail URLs to work as expected in the Clipper timeline they must be evenly distributed across the video (based on the duration) and in chronological order within the array. */
      "thumbnails": [
        "//example/path/thumbnail_001.jpg",
        "//example/path/thumbnail_002.jpg",
        "//example/path/thumbnail_003.jpg",
        "//example/path/thumbnail_004.jpg",
        "//example/path/thumbnail_005.jpg"
        ]
    }
];

var subclipper = new subclipper({
    selector: '#root',
    restVersion: '2.0',
    submitSubclipCallback: onSubmitSubclip,
});
subclipper.ready(function () {
    subclipper.load(assets);
});

```

> [!NOTE]
> <span data-ttu-id="fb1f6-119">It is recommended to chain the load() method call with the ready(handler) method as shown in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-119">It is recommended to chain the load() method call with the ready(handler) method as shown in the preceding example.</span></span> <span data-ttu-id="fb1f6-120">The preceding example guarantees that the widget is ready before loading the assets.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-120">The preceding example guarantees that the widget is ready before loading the assets.</span></span>

> [!NOTE]
> <span data-ttu-id="fb1f6-121">For the thumbnail URLs to work as expected in the Clipper timeline they must be evenly distributed across the video (based on the duration) and in chronological order within the array.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-121">For the thumbnail URLs to work as expected in the Clipper timeline they must be evenly distributed across the video (based on the duration) and in chronological order within the array.</span></span> <span data-ttu-id="fb1f6-122">You can use the following JSON preset snippet as a sample reference for generating images with the 'Media Encoder Standard' processor:</span><span class="sxs-lookup"><span data-stu-id="fb1f6-122">You can use the following JSON preset snippet as a sample reference for generating images with the 'Media Encoder Standard' processor:</span></span>

```json
{
  "Start": "0",
  "Step": "00:00:05",
  "Range": "100%",
  "Type": "PngImage",
  "PngLayers": [
    {
      "Type": "PngLayer",
      "Width": 48,
      "Height": 26
    }
  ]
}
```

## <a name="dynamically-load-videos-in-clipper"></a><span data-ttu-id="fb1f6-123">Dynamically load videos in Clipper</span><span class="sxs-lookup"><span data-stu-id="fb1f6-123">Dynamically load videos in Clipper</span></span>
<span data-ttu-id="fb1f6-124">Dynamically load videos into the Clipper to enable end users to select videos from the asset selection panel to clip against.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-124">Dynamically load videos into the Clipper to enable end users to select videos from the asset selection panel to clip against.</span></span>

<span data-ttu-id="fb1f6-125">Alternatively, you can load assets dynamically via a callback.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-125">Alternatively, you can load assets dynamically via a callback.</span></span> <span data-ttu-id="fb1f6-126">In scenarios where assets are dynamically generated or the library is large, you should load via the callback.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-126">In scenarios where assets are dynamically generated or the library is large, you should load via the callback.</span></span> <span data-ttu-id="fb1f6-127">To load asset dynamically, you must implement the optional onLoadAssets callback function.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-127">To load asset dynamically, you must implement the optional onLoadAssets callback function.</span></span> <span data-ttu-id="fb1f6-128">This function is passed into the Clipper at initialization.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-128">This function is passed into the Clipper at initialization.</span></span> <span data-ttu-id="fb1f6-129">The resolved assets should adhere to the same contract as statically loaded assets.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-129">The resolved assets should adhere to the same contract as statically loaded assets.</span></span> <span data-ttu-id="fb1f6-130">The following code sample illustrates the method signature, expected input, and expected output.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-130">The following code sample illustrates the method signature, expected input, and expected output.</span></span>

> [!NOTE]
> <span data-ttu-id="fb1f6-131">When dynamically loading assets into the Clipper, assets are rendered in the **asset selection panel**.</span><span class="sxs-lookup"><span data-stu-id="fb1f6-131">When dynamically loading assets into the Clipper, assets are rendered in the **asset selection panel**.</span></span>

```javascript
// Video Assets Pane Callback
    //
    // Filter Parameters:
    // - search: string value term that will be used in the back-end to filter assets by name.
    // - skip: int value used for pagination in the back-end that allows skipping a number of assets in the response.
    // - take: int value used for pagination in the back-end that allows defining the number of assets to include in the response.
    // - type: ('filter', 'asset') value that will be used in the back-end to filter assets by type.
    //
    // Returns: a Promise object that, when resolved, retuns an object containing an array of assets (input contract)
    //          that satisfies the filter parameters, plus optionally the total types of files available:
    // {
    //  total: 100,
    //  assets: [{...}],
    // }
    var onLoadAssets = function (search, skip, take, type) {
        var promise = new Promise(function (resolve, reject) {
            // TODO: implement the getAssetsFromBackend method to get the assets from the back-end using the filter parameters (search, skip, take, type).
            getAssetsFromBackend(search, skip, take, type)
                .then(function (assets) {
                    resolve({
                        total: assets.length,
                        assets: assets
                    });
                }).catch(function () {
                    reject(Error("error details"));
                });
        });
    
        return promise;
    };

    // Create widget instance:
    // - using a root element selector
    // - enabling the Video Assets panel by registering a callback in the 'assetsPanelLoaderCallback' option parameter.
    var widget = new subclipper({
        selector: '#root',

        // Enable the Video Assets panel in the widget to automatically load assets (input contract)
        assetsPanelLoaderCallback: onLoadAssets
    });

    // ...
    // The widget will automatically invoke the 'assetsPanelLoaderCallback' callback with the filter parameters specified by the user 
    // and load assets returned by the Promise into the Video Assets panel.
    // ...
```