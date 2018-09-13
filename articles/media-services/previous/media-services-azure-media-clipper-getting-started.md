---
title: Getting started with Azure Media Clipper | Microsoft Docs
description: Getting started with Azure Media Clipper, a tool for building video clips from AMS assets
services: media-services
keywords: clip;subclip;encoding;media
author: dbgeorge
manager: jasonsue
ms.author: dwgeo
ms.date: 11/10/2017
ms.topic: article
ms.service: media-services
ms.openlocfilehash: ac64d97aeeef6147aa62658c9ee440bf058f4db1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857863"
---
# <a name="create-clips-with-azure-media-clipper"></a><span data-ttu-id="08b5c-104">Create clips with Azure Media Clipper</span><span class="sxs-lookup"><span data-stu-id="08b5c-104">Create clips with Azure Media Clipper</span></span>
<span data-ttu-id="08b5c-105">This section shows you the basic steps of getting started with Azure Media Clipper.</span><span class="sxs-lookup"><span data-stu-id="08b5c-105">This section shows you the basic steps of getting started with Azure Media Clipper.</span></span> <span data-ttu-id="08b5c-106">Sections that follow provide the specifics on how to configure Azure Media Clipper.</span><span class="sxs-lookup"><span data-stu-id="08b5c-106">Sections that follow provide the specifics on how to configure Azure Media Clipper.</span></span>

- <span data-ttu-id="08b5c-107">First, add the following links for Azure Media Player and Azure Media Clipper to your document's head.</span><span class="sxs-lookup"><span data-stu-id="08b5c-107">First, add the following links for Azure Media Player and Azure Media Clipper to your document's head.</span></span> <span data-ttu-id="08b5c-108">We recommend explicitly specifying a version of the Clipper and Azure Media Player in the URLs.</span><span class="sxs-lookup"><span data-stu-id="08b5c-108">We recommend explicitly specifying a version of the Clipper and Azure Media Player in the URLs.</span></span> <span data-ttu-id="08b5c-109">Do not use the latest version of these resources in production as they are subject to change on demand.</span><span class="sxs-lookup"><span data-stu-id="08b5c-109">Do not use the latest version of these resources in production as they are subject to change on demand.</span></span>

```javascript
<!--Azure Media Player 2.1.4 or later is a prerequisite-->
<link href="//amp.azure.net/libs/amp/2.1.4/skins/amp-default/azuremediaplayer.min.css" rel="stylesheet">
<script src="//amp.azure.net/libs/amp/2.1.4/azuremediaplayer.min.js"></script>
<!--Azure Media Clipper script and stylesheet-->
<link href="//amp.azure.net/libs/amc/0.1.0/azuremediaclipper.css" rel="stylesheet">
<script src="//amp.azure.net/libs/amc/0.1.0/azuremediaclipper.min.js"></script>
```

- <span data-ttu-id="08b5c-110">Next, add the following classes to the div element where you would like to instantiate the Clipper.</span><span class="sxs-lookup"><span data-stu-id="08b5c-110">Next, add the following classes to the div element where you would like to instantiate the Clipper.</span></span>

```javascript
<div id="root" class="azure-subclipper" />
```

<span data-ttu-id="08b5c-111">Optionally, to enable the dark theme, add the dark-skin class:</span><span class="sxs-lookup"><span data-stu-id="08b5c-111">Optionally, to enable the dark theme, add the dark-skin class:</span></span>

```javascript
<div id="root" class="azure-subclipper dark-skin" />
```

- <span data-ttu-id="08b5c-112">Next, instantiate the Clipper with the following API call:</span><span class="sxs-lookup"><span data-stu-id="08b5c-112">Next, instantiate the Clipper with the following API call:</span></span>

```javascript
var subclipper = new subclipper({
    selector: '#root',
    logLevel: 'info',
    restVersion: '2.0',
    minimumMarkerGap: 6,
    submitSubclipCallback: onSubmitSubclip,
    singleBitrateMp4Profile: {
            Codecs: [{
                    // Video Codec with single H264Layers
                }, {
                    // Audio Codec
                }]
    },
    multiBitrateMp4Profile: {
            Codecs: [{
                    // Video Codec with multiple H264Layers
                }, {
                    // Audio Codec
                }]
    },
    keymap: {
      // See below for more info
    },
   // Enable the Video Assets panel in the widget to automatically load assets (input contract)
    assetsPanelLoaderCallback: onLoadAssets,
    height: 600,
    subclippingMode: 'all',
    filterAssetsTypes: true,
    speedLevels: [
        { name: '4x', value: 4.0 },
        { name: '3x', value: 3.0 },
        { name: '2x', value: 2.0 },
        { name: 'normal', value: 1.0 },
        { name: '0.75x', value: 0.75 },
        { name: '0.5x', value: 0.5 },
    ],
    resetOnJobDone: false,
    autoplayVideo: true,
    language: 'en'    
});
```

<span data-ttu-id="08b5c-113">The parameters for the initialization method call are:</span><span class="sxs-lookup"><span data-stu-id="08b5c-113">The parameters for the initialization method call are:</span></span>
- <span data-ttu-id="08b5c-114">`selector` {REQUIRED, string}: CSS selector of the matching HTML element where the widget should be rendered.</span><span class="sxs-lookup"><span data-stu-id="08b5c-114">`selector` {REQUIRED, string}: CSS selector of the matching HTML element where the widget should be rendered.</span></span>
- <span data-ttu-id="08b5c-115">`restVersion` {REQUIRED, string}: The Azure Media Services REST API version to target.</span><span class="sxs-lookup"><span data-stu-id="08b5c-115">`restVersion` {REQUIRED, string}: The Azure Media Services REST API version to target.</span></span> <span data-ttu-id="08b5c-116">The REST version defines the format of the output generated by the widget.</span><span class="sxs-lookup"><span data-stu-id="08b5c-116">The REST version defines the format of the output generated by the widget.</span></span> <span data-ttu-id="08b5c-117">Currently, only 2.0 is supported.</span><span class="sxs-lookup"><span data-stu-id="08b5c-117">Currently, only 2.0 is supported.</span></span>
- <span data-ttu-id="08b5c-118">`submitSubclipCallback` {REQUIRED, promise} The callback function invoked when the "submit" button of the widget is clicked.</span><span class="sxs-lookup"><span data-stu-id="08b5c-118">`submitSubclipCallback` {REQUIRED, promise} The callback function invoked when the "submit" button of the widget is clicked.</span></span> <span data-ttu-id="08b5c-119">The callback function should expect the output generated by the widget (a render job configuration or a filter definition).</span><span class="sxs-lookup"><span data-stu-id="08b5c-119">The callback function should expect the output generated by the widget (a render job configuration or a filter definition).</span></span> <span data-ttu-id="08b5c-120">For more information, see Submit subclip callback.</span><span class="sxs-lookup"><span data-stu-id="08b5c-120">For more information, see Submit subclip callback.</span></span>
- <span data-ttu-id="08b5c-121">`logLevel` {OPTIONAL, {'info', 'warn', 'error'}}: The logging level to be displayed in the browser’s console.</span><span class="sxs-lookup"><span data-stu-id="08b5c-121">`logLevel` {OPTIONAL, {'info', 'warn', 'error'}}: The logging level to be displayed in the browser’s console.</span></span> <span data-ttu-id="08b5c-122">Default value: error</span><span class="sxs-lookup"><span data-stu-id="08b5c-122">Default value: error</span></span>
- <span data-ttu-id="08b5c-123">`minimumMarkerGap` {OPTIONAL, int}: The minimum size of a subclip (in seconds).</span><span class="sxs-lookup"><span data-stu-id="08b5c-123">`minimumMarkerGap` {OPTIONAL, int}: The minimum size of a subclip (in seconds).</span></span> <span data-ttu-id="08b5c-124">Note: the value should be greater or equal to 6, which is also the default.</span><span class="sxs-lookup"><span data-stu-id="08b5c-124">Note: the value should be greater or equal to 6, which is also the default.</span></span>
- <span data-ttu-id="08b5c-125">`singleBitrateMp4Profile` {OPTIONAL, JSON object} The single bitrate mp4 profile to use for the render job configuration generated by the widget.</span><span class="sxs-lookup"><span data-stu-id="08b5c-125">`singleBitrateMp4Profile` {OPTIONAL, JSON object} The single bitrate mp4 profile to use for the render job configuration generated by the widget.</span></span> <span data-ttu-id="08b5c-126">If not provided, it uses the [default single-bitrate MP4 profile](https://docs.microsoft.com/azure/media-services/media-services-mes-preset-h264-single-bitrate-1080p).</span><span class="sxs-lookup"><span data-stu-id="08b5c-126">If not provided, it uses the [default single-bitrate MP4 profile](https://docs.microsoft.com/azure/media-services/media-services-mes-preset-h264-single-bitrate-1080p).</span></span>
- <span data-ttu-id="08b5c-127">`multiBitrateMp4Profile` {OPTIONAL, JSON object} The multi bitrate mp4 profile to use for render job configuration generated by the widget.</span><span class="sxs-lookup"><span data-stu-id="08b5c-127">`multiBitrateMp4Profile` {OPTIONAL, JSON object} The multi bitrate mp4 profile to use for render job configuration generated by the widget.</span></span> <span data-ttu-id="08b5c-128">If not provided, it uses the [default multi-bitrate MP4 profile](https://docs.microsoft.com/azure/media-services/media-services-mes-preset-h264-multiple-bitrate-1080p).</span><span class="sxs-lookup"><span data-stu-id="08b5c-128">If not provided, it uses the [default multi-bitrate MP4 profile](https://docs.microsoft.com/azure/media-services/media-services-mes-preset-h264-multiple-bitrate-1080p).</span></span>
- <span data-ttu-id="08b5c-129">`keymap` {OPTIONAL, json object} Allows customizing the keyboard shortcuts of the widget.</span><span class="sxs-lookup"><span data-stu-id="08b5c-129">`keymap` {OPTIONAL, json object} Allows customizing the keyboard shortcuts of the widget.</span></span> <span data-ttu-id="08b5c-130">For more information, see [customizable keyboard shortcuts](media-services-azure-media-clipper-keyboard-shortcuts.md).</span><span class="sxs-lookup"><span data-stu-id="08b5c-130">For more information, see [customizable keyboard shortcuts](media-services-azure-media-clipper-keyboard-shortcuts.md).</span></span>
- <span data-ttu-id="08b5c-131">`assetsPanelLoaderCallback` {OPTIONAL, promise} The callback function invoked to load (asynchronously) a new page of assets into the assets pane every time the user scrolls down to the bottom of the pane.</span><span class="sxs-lookup"><span data-stu-id="08b5c-131">`assetsPanelLoaderCallback` {OPTIONAL, promise} The callback function invoked to load (asynchronously) a new page of assets into the assets pane every time the user scrolls down to the bottom of the pane.</span></span> <span data-ttu-id="08b5c-132">For more information, see Asset pane loader callback.</span><span class="sxs-lookup"><span data-stu-id="08b5c-132">For more information, see Asset pane loader callback.</span></span>
- <span data-ttu-id="08b5c-133">`height` {OPTIONAL, number} The total height of the widget (minimum height is 600 px without assets pane and 850 px with the assets pane).</span><span class="sxs-lookup"><span data-stu-id="08b5c-133">`height` {OPTIONAL, number} The total height of the widget (minimum height is 600 px without assets pane and 850 px with the assets pane).</span></span>
- <span data-ttu-id="08b5c-134">`subclippingMode` (OPTIONAL, {'all', 'render', 'filter'}): The subclipping mode(s) allowed.</span><span class="sxs-lookup"><span data-stu-id="08b5c-134">`subclippingMode` (OPTIONAL, {'all', 'render', 'filter'}): The subclipping mode(s) allowed.</span></span> <span data-ttu-id="08b5c-135">The default value is all.</span><span class="sxs-lookup"><span data-stu-id="08b5c-135">The default value is all.</span></span>
- <span data-ttu-id="08b5c-136">`filterAssetsTypes` (OPTIONAL, bool): filterAssetsTypes allow you to show/hide the filters dropdown from the assets pane.</span><span class="sxs-lookup"><span data-stu-id="08b5c-136">`filterAssetsTypes` (OPTIONAL, bool): filterAssetsTypes allow you to show/hide the filters dropdown from the assets pane.</span></span> <span data-ttu-id="08b5c-137">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="08b5c-137">The default value is true.</span></span>
- <span data-ttu-id="08b5c-138">`speedLevels` (OPTIONAL, array): speedLevels allows setting different speed levels for the video player, see [Azure Media Player documentation](http://amp.azure.net/libs/amp/latest/docs/#amp.player.playbackspeedoptions) for more info.</span><span class="sxs-lookup"><span data-stu-id="08b5c-138">`speedLevels` (OPTIONAL, array): speedLevels allows setting different speed levels for the video player, see [Azure Media Player documentation](http://amp.azure.net/libs/amp/latest/docs/#amp.player.playbackspeedoptions) for more info.</span></span>
- <span data-ttu-id="08b5c-139">`resetOnJobDone` (OPTIONAL, bool): resetOnJobDone allows Clipper to reset the subclipper to an initial state when a job is submitted successfully.</span><span class="sxs-lookup"><span data-stu-id="08b5c-139">`resetOnJobDone` (OPTIONAL, bool): resetOnJobDone allows Clipper to reset the subclipper to an initial state when a job is submitted successfully.</span></span>
- <span data-ttu-id="08b5c-140">`autoplayVideo` (OPTIONAL, bool): autoplayVideo allows Clipper to autoplay the video on load.</span><span class="sxs-lookup"><span data-stu-id="08b5c-140">`autoplayVideo` (OPTIONAL, bool): autoplayVideo allows Clipper to autoplay the video on load.</span></span> <span data-ttu-id="08b5c-141">The default value is true.</span><span class="sxs-lookup"><span data-stu-id="08b5c-141">The default value is true.</span></span>
- <span data-ttu-id="08b5c-142">`language` {OPTIONAL, string}: language sets the language of the widget.</span><span class="sxs-lookup"><span data-stu-id="08b5c-142">`language` {OPTIONAL, string}: language sets the language of the widget.</span></span> <span data-ttu-id="08b5c-143">If not specified, the widget tries to localize the messages based on the browser language.</span><span class="sxs-lookup"><span data-stu-id="08b5c-143">If not specified, the widget tries to localize the messages based on the browser language.</span></span> <span data-ttu-id="08b5c-144">If no language is detected in the browser, the widget defaults to English.</span><span class="sxs-lookup"><span data-stu-id="08b5c-144">If no language is detected in the browser, the widget defaults to English.</span></span> <span data-ttu-id="08b5c-145">For more information, see the [configure localization](media-services-azure-media-clipper-localization.md) section.</span><span class="sxs-lookup"><span data-stu-id="08b5c-145">For more information, see the [configure localization](media-services-azure-media-clipper-localization.md) section.</span></span>
- <span data-ttu-id="08b5c-146">`languages` {OPTIONAL, JSON}: the languages parameter replaces the default dictionary of languages with a custom dictionary defined by the user.</span><span class="sxs-lookup"><span data-stu-id="08b5c-146">`languages` {OPTIONAL, JSON}: the languages parameter replaces the default dictionary of languages with a custom dictionary defined by the user.</span></span> <span data-ttu-id="08b5c-147">For more information, see the [configure localization](media-services-azure-media-clipper-localization.md) section.</span><span class="sxs-lookup"><span data-stu-id="08b5c-147">For more information, see the [configure localization](media-services-azure-media-clipper-localization.md) section.</span></span>
- <span data-ttu-id="08b5c-148">`extraLanguages` (OPTIONAL, JSON): the extraLanaguages parameter adds new languages to the default dictionary.</span><span class="sxs-lookup"><span data-stu-id="08b5c-148">`extraLanguages` (OPTIONAL, JSON): the extraLanaguages parameter adds new languages to the default dictionary.</span></span> <span data-ttu-id="08b5c-149">For more information, see the [configure localization](media-services-azure-media-clipper-localization.md) section.</span><span class="sxs-lookup"><span data-stu-id="08b5c-149">For more information, see the [configure localization](media-services-azure-media-clipper-localization.md) section.</span></span>

## <a name="typescript-definition"></a><span data-ttu-id="08b5c-150">TypeScript definition</span><span class="sxs-lookup"><span data-stu-id="08b5c-150">TypeScript definition</span></span>
<span data-ttu-id="08b5c-151">A [TypeScript](https://www.typescriptlang.org/) definition file for the Clipper can be found [here](http://amp.azure.net/libs/amc/latest/azuremediaclipper.d.ts).</span><span class="sxs-lookup"><span data-stu-id="08b5c-151">A [TypeScript](https://www.typescriptlang.org/) definition file for the Clipper can be found [here](http://amp.azure.net/libs/amc/latest/azuremediaclipper.d.ts).</span></span>

## <a name="azure-media-clipper-api"></a><span data-ttu-id="08b5c-152">Azure Media Clipper API</span><span class="sxs-lookup"><span data-stu-id="08b5c-152">Azure Media Clipper API</span></span>
<span data-ttu-id="08b5c-153">This section documents the API surface provided by the Clipper.</span><span class="sxs-lookup"><span data-stu-id="08b5c-153">This section documents the API surface provided by the Clipper.</span></span>

- <span data-ttu-id="08b5c-154">`ready(handler)`: offers a way to run JavaScript as soon as the Clipper is fully loaded and ready to be used.</span><span class="sxs-lookup"><span data-stu-id="08b5c-154">`ready(handler)`: offers a way to run JavaScript as soon as the Clipper is fully loaded and ready to be used.</span></span>
- <span data-ttu-id="08b5c-155">`load(assets)`: loads a list of assets into the widget timeline (should not be used together with assetsPanelLoaderCallback).</span><span class="sxs-lookup"><span data-stu-id="08b5c-155">`load(assets)`: loads a list of assets into the widget timeline (should not be used together with assetsPanelLoaderCallback).</span></span> <span data-ttu-id="08b5c-156">See this [article](media-services-azure-media-clipper-load-assets.md) for details on how to load assets into the Clipper.</span><span class="sxs-lookup"><span data-stu-id="08b5c-156">See this [article](media-services-azure-media-clipper-load-assets.md) for details on how to load assets into the Clipper.</span></span>
- <span data-ttu-id="08b5c-157">`setLogLevel(level)`: sets the logging level to be displayed in the browser’s console.</span><span class="sxs-lookup"><span data-stu-id="08b5c-157">`setLogLevel(level)`: sets the logging level to be displayed in the browser’s console.</span></span> <span data-ttu-id="08b5c-158">Possible values are: `info`, `warn`, `error`.</span><span class="sxs-lookup"><span data-stu-id="08b5c-158">Possible values are: `info`, `warn`, `error`.</span></span>
- <span data-ttu-id="08b5c-159">`setHeight(height)`: sets the total height of the widget in pixels (minimum height is 600 px without assets pane, and 850 px with the assets pane).</span><span class="sxs-lookup"><span data-stu-id="08b5c-159">`setHeight(height)`: sets the total height of the widget in pixels (minimum height is 600 px without assets pane, and 850 px with the assets pane).</span></span>
- <span data-ttu-id="08b5c-160">`version`: gets the widget version.</span><span class="sxs-lookup"><span data-stu-id="08b5c-160">`version`: gets the widget version.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08b5c-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="08b5c-161">Next steps</span></span>
<span data-ttu-id="08b5c-162">See the next steps for configuring Azure Media Clipper:</span><span class="sxs-lookup"><span data-stu-id="08b5c-162">See the next steps for configuring Azure Media Clipper:</span></span>
- [<span data-ttu-id="08b5c-163">Loading assets into Azure Media Clipper</span><span class="sxs-lookup"><span data-stu-id="08b5c-163">Loading assets into Azure Media Clipper</span></span>](media-services-azure-media-clipper-load-assets.md)
- [<span data-ttu-id="08b5c-164">Configuring custom keyboard shortcuts</span><span class="sxs-lookup"><span data-stu-id="08b5c-164">Configuring custom keyboard shortcuts</span></span>](media-services-azure-media-clipper-keyboard-shortcuts.md)
- [<span data-ttu-id="08b5c-165">Submitting clipping jobs from the Clipper</span><span class="sxs-lookup"><span data-stu-id="08b5c-165">Submitting clipping jobs from the Clipper</span></span>](media-services-azure-media-clipper-submit-job.md)
- [<span data-ttu-id="08b5c-166">Configuring localization</span><span class="sxs-lookup"><span data-stu-id="08b5c-166">Configuring localization</span></span>](media-services-azure-media-clipper-localization.md)