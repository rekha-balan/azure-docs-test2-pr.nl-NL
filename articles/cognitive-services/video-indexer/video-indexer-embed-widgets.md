---
title: Embed Azure Video Indexer widgets into your applications | Microsoft Docs
description: ''
services: cognitive services
documentationcenter: ''
author: juliako
manager: erikre
ms.service: cognitive-services
ms.topic: article
ms.date: 08/25/2018
ms.author: juliako
ms.openlocfilehash: b8de9e8d73ba899fb7f3036d871c5d30daf101de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869947"
---
# <a name="embed-video-indexer-widgets-into-your-applications"></a><span data-ttu-id="870d3-102">Embed Video Indexer widgets into your applications</span><span class="sxs-lookup"><span data-stu-id="870d3-102">Embed Video Indexer widgets into your applications</span></span>

<span data-ttu-id="870d3-103">Video Indexer supports embedding two types of widgets into your application: **Cognitive Insights** and **Player**.</span><span class="sxs-lookup"><span data-stu-id="870d3-103">Video Indexer supports embedding two types of widgets into your application: **Cognitive Insights** and **Player**.</span></span> 

* <span data-ttu-id="870d3-104">A **Cognitive Insights** widget includes all visual insights that were extracted from your video indexing process.</span><span class="sxs-lookup"><span data-stu-id="870d3-104">A **Cognitive Insights** widget includes all visual insights that were extracted from your video indexing process.</span></span> 
    <span data-ttu-id="870d3-105">The insights widget supports the following optional URL params:</span><span class="sxs-lookup"><span data-stu-id="870d3-105">The insights widget supports the following optional URL params:</span></span>

    |<span data-ttu-id="870d3-106">Name</span><span class="sxs-lookup"><span data-stu-id="870d3-106">Name</span></span>|<span data-ttu-id="870d3-107">Definition</span><span class="sxs-lookup"><span data-stu-id="870d3-107">Definition</span></span>|<span data-ttu-id="870d3-108">Description</span><span class="sxs-lookup"><span data-stu-id="870d3-108">Description</span></span>|
    |---|---|---|
    |<span data-ttu-id="870d3-109">widgets</span><span class="sxs-lookup"><span data-stu-id="870d3-109">widgets</span></span>|<span data-ttu-id="870d3-110">Strings separated by comma</span><span class="sxs-lookup"><span data-stu-id="870d3-110">Strings separated by comma</span></span>|<span data-ttu-id="870d3-111">Allows you to control the insights you want to render.</span><span class="sxs-lookup"><span data-stu-id="870d3-111">Allows you to control the insights you want to render.</span></span> <br/><span data-ttu-id="870d3-112">Example: **widgets=people,brands** will render only people and brands ui insights</span><span class="sxs-lookup"><span data-stu-id="870d3-112">Example: **widgets=people,brands** will render only people and brands ui insights</span></span><br/><span data-ttu-id="870d3-113">Available options:  People, Keywords, Annotations, Brands, Sentiments, Transcript, Search</span><span class="sxs-lookup"><span data-stu-id="870d3-113">Available options:  People, Keywords, Annotations, Brands, Sentiments, Transcript, Search</span></span> | 
* <span data-ttu-id="870d3-114">A **Player** widget enables you to stream the video using adaptive bit rate.</span><span class="sxs-lookup"><span data-stu-id="870d3-114">A **Player** widget enables you to stream the video using adaptive bit rate.</span></span>

    <span data-ttu-id="870d3-115">The player widget supports the following optional URL params:</span><span class="sxs-lookup"><span data-stu-id="870d3-115">The player widget supports the following optional URL params:</span></span>

    |<span data-ttu-id="870d3-116">Name</span><span class="sxs-lookup"><span data-stu-id="870d3-116">Name</span></span>|<span data-ttu-id="870d3-117">Definition</span><span class="sxs-lookup"><span data-stu-id="870d3-117">Definition</span></span>|<span data-ttu-id="870d3-118">Description</span><span class="sxs-lookup"><span data-stu-id="870d3-118">Description</span></span>|
    |---|---|---|
    |<span data-ttu-id="870d3-119">t</span><span class="sxs-lookup"><span data-stu-id="870d3-119">t</span></span>|<span data-ttu-id="870d3-120">Seconds from start</span><span class="sxs-lookup"><span data-stu-id="870d3-120">Seconds from start</span></span>|<span data-ttu-id="870d3-121">Makes the player start playing from the given time point.</span><span class="sxs-lookup"><span data-stu-id="870d3-121">Makes the player start playing from the given time point.</span></span><br/><span data-ttu-id="870d3-122">Example: t=60</span><span class="sxs-lookup"><span data-stu-id="870d3-122">Example: t=60</span></span>|
    |<span data-ttu-id="870d3-123">captions</span><span class="sxs-lookup"><span data-stu-id="870d3-123">captions</span></span>|<span data-ttu-id="870d3-124">Language code</span><span class="sxs-lookup"><span data-stu-id="870d3-124">Language code</span></span>|<span data-ttu-id="870d3-125">Fetches the caption in the given language during the widget loading to be available in the captions menu.</span><span class="sxs-lookup"><span data-stu-id="870d3-125">Fetches the caption in the given language during the widget loading to be available in the captions menu.</span></span><br/><span data-ttu-id="870d3-126">Example: captions=en-Us</span><span class="sxs-lookup"><span data-stu-id="870d3-126">Example: captions=en-Us</span></span>|
    |<span data-ttu-id="870d3-127">showCaptions</span><span class="sxs-lookup"><span data-stu-id="870d3-127">showCaptions</span></span>|<span data-ttu-id="870d3-128">A boolean value</span><span class="sxs-lookup"><span data-stu-id="870d3-128">A boolean value</span></span>|<span data-ttu-id="870d3-129">Makes the player load with the captions already enabled.</span><span class="sxs-lookup"><span data-stu-id="870d3-129">Makes the player load with the captions already enabled.</span></span><br/><span data-ttu-id="870d3-130">Example: showCaptions=true</span><span class="sxs-lookup"><span data-stu-id="870d3-130">Example: showCaptions=true</span></span>|
    |<span data-ttu-id="870d3-131">type</span><span class="sxs-lookup"><span data-stu-id="870d3-131">type</span></span>||<span data-ttu-id="870d3-132">Activates an audio player skin (video part is removed).</span><span class="sxs-lookup"><span data-stu-id="870d3-132">Activates an audio player skin (video part is removed).</span></span><br/><span data-ttu-id="870d3-133">Example: type=audio</span><span class="sxs-lookup"><span data-stu-id="870d3-133">Example: type=audio</span></span>|
    |<span data-ttu-id="870d3-134">autoplay</span><span class="sxs-lookup"><span data-stu-id="870d3-134">autoplay</span></span>|<span data-ttu-id="870d3-135">A boolean value</span><span class="sxs-lookup"><span data-stu-id="870d3-135">A boolean value</span></span>|<span data-ttu-id="870d3-136">Decide if the player should start playing the video when loaded (default is true).</span><span class="sxs-lookup"><span data-stu-id="870d3-136">Decide if the player should start playing the video when loaded (default is true).</span></span><br/><span data-ttu-id="870d3-137">Example: autoplay=false</span><span class="sxs-lookup"><span data-stu-id="870d3-137">Example: autoplay=false</span></span>|
    |<span data-ttu-id="870d3-138">language</span><span class="sxs-lookup"><span data-stu-id="870d3-138">language</span></span>|<span data-ttu-id="870d3-139">Language code</span><span class="sxs-lookup"><span data-stu-id="870d3-139">Language code</span></span>|<span data-ttu-id="870d3-140">Control the player controls localization (default is en-US)</span><span class="sxs-lookup"><span data-stu-id="870d3-140">Control the player controls localization (default is en-US)</span></span><br/><span data-ttu-id="870d3-141">Example: language=de-DE</span><span class="sxs-lookup"><span data-stu-id="870d3-141">Example: language=de-DE</span></span>|

## <a name="embedding-public-content"></a><span data-ttu-id="870d3-142">Embedding public content</span><span class="sxs-lookup"><span data-stu-id="870d3-142">Embedding public content</span></span>

1. <span data-ttu-id="870d3-143">Sign in to your [Video Indexer](https://api-portal.videoindexer.ai/) account.</span><span class="sxs-lookup"><span data-stu-id="870d3-143">Sign in to your [Video Indexer](https://api-portal.videoindexer.ai/) account.</span></span> 
2. <span data-ttu-id="870d3-144">Click the "embed" button that appears below the video.</span><span class="sxs-lookup"><span data-stu-id="870d3-144">Click the "embed" button that appears below the video.</span></span>

    ![Widget](./media/video-indexer-embed-widgets/video-indexer-widget01.png)

    <span data-ttu-id="870d3-146">After clicking the button, an embed modal will appear on the screen where you can choose what widget you want to embed in your application.</span><span class="sxs-lookup"><span data-stu-id="870d3-146">After clicking the button, an embed modal will appear on the screen where you can choose what widget you want to embed in your application.</span></span>
    <span data-ttu-id="870d3-147">Selecting a widget (**Player** or **Cognitive Insights**), generates the embedded code for you to paste in your application.</span><span class="sxs-lookup"><span data-stu-id="870d3-147">Selecting a widget (**Player** or **Cognitive Insights**), generates the embedded code for you to paste in your application.</span></span>
 
3. <span data-ttu-id="870d3-148">Choose the type of widget you want (**Cognitive Insights** or **Player**).</span><span class="sxs-lookup"><span data-stu-id="870d3-148">Choose the type of widget you want (**Cognitive Insights** or **Player**).</span></span>
4. <span data-ttu-id="870d3-149">Copy the embed code, and add to your application.</span><span class="sxs-lookup"><span data-stu-id="870d3-149">Copy the embed code, and add to your application.</span></span> 

    ![Widget](./media/video-indexer-embed-widgets/video-indexer-widget02.png)

## <a name="embedding-private-content"></a><span data-ttu-id="870d3-151">Embedding private content</span><span class="sxs-lookup"><span data-stu-id="870d3-151">Embedding private content</span></span>

<span data-ttu-id="870d3-152">You can get embed codes from embed popups (as shown in the previous section) for **Public** videos only.</span><span class="sxs-lookup"><span data-stu-id="870d3-152">You can get embed codes from embed popups (as shown in the previous section) for **Public** videos only.</span></span> 

<span data-ttu-id="870d3-153">If you want to embed a **Private** video, you have to pass an access token in the **iframe**'s **src** attribute:</span><span class="sxs-lookup"><span data-stu-id="870d3-153">If you want to embed a **Private** video, you have to pass an access token in the **iframe**'s **src** attribute:</span></span>

     https://www.videoindexer.ai/embed/[insights | player]/<accountId>/<VideoId>/?accessToken=<accessToken>
    
<span data-ttu-id="870d3-154">Use the [**Get Insights Widget**](https://api-portal.videoindexer.ai/docs/services/operations/operations/Get-insights-widget?) API to get the Cognitive Insights widget content, Or use [**Get Video Access Token**](https://api-portal.videoindexer.ai/docs/services/authorization/operations/Get-Video-Access-Token?) and add that as a query param to the url as shown above.</span><span class="sxs-lookup"><span data-stu-id="870d3-154">Use the [**Get Insights Widget**](https://api-portal.videoindexer.ai/docs/services/operations/operations/Get-insights-widget?) API to get the Cognitive Insights widget content, Or use [**Get Video Access Token**](https://api-portal.videoindexer.ai/docs/services/authorization/operations/Get-Video-Access-Token?) and add that as a query param to the url as shown above.</span></span> <span data-ttu-id="870d3-155">Specify this URL as the **iframe**'s **src** value.</span><span class="sxs-lookup"><span data-stu-id="870d3-155">Specify this URL as the **iframe**'s **src** value.</span></span>

<span data-ttu-id="870d3-156">If you want to provide editing insights capabilities (like we have in our web application) in your embedded widget, you will have to pass an access token with editing permissions.</span><span class="sxs-lookup"><span data-stu-id="870d3-156">If you want to provide editing insights capabilities (like we have in our web application) in your embedded widget, you will have to pass an access token with editing permissions.</span></span> <span data-ttu-id="870d3-157">Use [**Get Insights Widget**](https://api-portal.videoindexer.ai/docs/services/operations/operations/Get-insights-widget?)  or [**Get Video Access Token**](https://api-portal.videoindexer.ai/docs/services/authorization/operations/Get-Video-Access-Token?) with **&allowEdit=true**.</span><span class="sxs-lookup"><span data-stu-id="870d3-157">Use [**Get Insights Widget**](https://api-portal.videoindexer.ai/docs/services/operations/operations/Get-insights-widget?)  or [**Get Video Access Token**](https://api-portal.videoindexer.ai/docs/services/authorization/operations/Get-Video-Access-Token?) with **&allowEdit=true**.</span></span> 

## <a name="widgets-interaction"></a><span data-ttu-id="870d3-158">Widgets interaction</span><span class="sxs-lookup"><span data-stu-id="870d3-158">Widgets interaction</span></span>

<span data-ttu-id="870d3-159">The **Cognitive Insights** widget can interact with a video on your application.</span><span class="sxs-lookup"><span data-stu-id="870d3-159">The **Cognitive Insights** widget can interact with a video on your application.</span></span> <span data-ttu-id="870d3-160">This section shows how to achieve this interaction.</span><span class="sxs-lookup"><span data-stu-id="870d3-160">This section shows how to achieve this interaction.</span></span>

![Widget](./media/video-indexer-embed-widgets/video-indexer-widget03.png)

### <a name="cross-origin-communications"></a><span data-ttu-id="870d3-162">Cross-origin communications</span><span class="sxs-lookup"><span data-stu-id="870d3-162">Cross-origin communications</span></span>

<span data-ttu-id="870d3-163">To get Video Indexer widgets to communicate with other components, the Video Indexer service does the following:</span><span class="sxs-lookup"><span data-stu-id="870d3-163">To get Video Indexer widgets to communicate with other components, the Video Indexer service does the following:</span></span>

- <span data-ttu-id="870d3-164">Uses the cross-origin communication HTML5 method **postMessage** and</span><span class="sxs-lookup"><span data-stu-id="870d3-164">Uses the cross-origin communication HTML5 method **postMessage** and</span></span> 
- <span data-ttu-id="870d3-165">Validates the message across VideoIndexer.ai origin.</span><span class="sxs-lookup"><span data-stu-id="870d3-165">Validates the message across VideoIndexer.ai origin.</span></span> 

<span data-ttu-id="870d3-166">If you choose to implement your own player code and do the integration with **Cognitive Insights** widgets, it is your responsibility to validate the origin of the message that comes from VideoIndexer.ai.</span><span class="sxs-lookup"><span data-stu-id="870d3-166">If you choose to implement your own player code and do the integration with **Cognitive Insights** widgets, it is your responsibility to validate the origin of the message that comes from VideoIndexer.ai.</span></span>

### <a name="embed-both-types-of-widgets-in-your-application--blog-recommended"></a><span data-ttu-id="870d3-167">Embed both types of widgets in your application / blog (recommended)</span><span class="sxs-lookup"><span data-stu-id="870d3-167">Embed both types of widgets in your application / blog (recommended)</span></span> 

<span data-ttu-id="870d3-168">This section shows how to achieve interaction between two Video Indexer widgets so when a user clicks the insight control on your application, the player jumps to the relevant moment.</span><span class="sxs-lookup"><span data-stu-id="870d3-168">This section shows how to achieve interaction between two Video Indexer widgets so when a user clicks the insight control on your application, the player jumps to the relevant moment.</span></span>

    <script src="https://breakdown.blob.core.windows.net/public/vb.widgets.mediator.js"></script> 

1. <span data-ttu-id="870d3-169">Copy the **Player** widget embed code.</span><span class="sxs-lookup"><span data-stu-id="870d3-169">Copy the **Player** widget embed code.</span></span>
2. <span data-ttu-id="870d3-170">Copy the **Cognitive Insights** embed code.</span><span class="sxs-lookup"><span data-stu-id="870d3-170">Copy the **Cognitive Insights** embed code.</span></span>
3. <span data-ttu-id="870d3-171">Add the [**Mediator file**](https://breakdown.blob.core.windows.net/public/vb.widgets.mediator.js) to handle the communication between the two widgets:</span><span class="sxs-lookup"><span data-stu-id="870d3-171">Add the [**Mediator file**](https://breakdown.blob.core.windows.net/public/vb.widgets.mediator.js) to handle the communication between the two widgets:</span></span>

    <script src="https://breakdown.blob.core.windows.net/public/vb.widgets.mediator.js"></script>

<span data-ttu-id="870d3-172">Now when a user clicks the insight control on your application, the player jumps to the relevant moment.</span><span class="sxs-lookup"><span data-stu-id="870d3-172">Now when a user clicks the insight control on your application, the player jumps to the relevant moment.</span></span>

<span data-ttu-id="870d3-173">For more information, see [this demo](https://codepen.io/videoindexer/pen/NzJeOb).</span><span class="sxs-lookup"><span data-stu-id="870d3-173">For more information, see [this demo](https://codepen.io/videoindexer/pen/NzJeOb).</span></span>

### <a name="embed-the-cognitive-insights-widget-and-use-azure-media-player-to-play-the-content"></a><span data-ttu-id="870d3-174">Embed the Cognitive Insights widget and use Azure Media Player to play the content</span><span class="sxs-lookup"><span data-stu-id="870d3-174">Embed the Cognitive Insights widget and use Azure Media Player to play the content</span></span>

<span data-ttu-id="870d3-175">This section shows how to achieve interaction between a **Cognitive Insights** widget and an Azure Media Player instance using the [AMP plugin](https://breakdown.blob.core.windows.net/public/amp-vb.plugin.js).</span><span class="sxs-lookup"><span data-stu-id="870d3-175">This section shows how to achieve interaction between a **Cognitive Insights** widget and an Azure Media Player instance using the [AMP plugin](https://breakdown.blob.core.windows.net/public/amp-vb.plugin.js).</span></span>
 
1. <span data-ttu-id="870d3-176">Add a Video Indexer plugin for the AMP player.</span><span class="sxs-lookup"><span data-stu-id="870d3-176">Add a Video Indexer plugin for the AMP player.</span></span>

        <script src="https://breakdown.blob.core.windows.net/public/amp-vb.plugin.js"></script>


2. <span data-ttu-id="870d3-177">Instantiate Azure Media Player with the Video Indexer plugin.</span><span class="sxs-lookup"><span data-stu-id="870d3-177">Instantiate Azure Media Player with the Video Indexer plugin.</span></span>

        // Init Source
        function initSource() {
            var tracks = [{
            kind: 'captions',
            // Here is how to load vtt from VI, you can replace it with your vtt url.
            src: this.getSubtitlesUrl("c4c1ad4c9a", "English"),
            srclang: 'en',
            label: 'English'
            }];

            myPlayer.src([
            {
                "src": "//amssamples.streaming.mediaservices.windows.net/91492735-c523-432b-ba01-faba6c2206a2/AzureMediaServicesPromo.ism/manifest",
                "type": "application/vnd.ms-sstr+xml"
            }
            ], tracks);
        }

        // Init your AMP instance
        var myPlayer = amp('vid1', { /* Options */
            "nativeControlsForTouch": false,
            autoplay: true,
            controls: true,
            width: "640",
            height: "400",
            poster: "",
            plugins: {
            videobreakedown: {}
            }
        }, function () {
            // Activate the plugin
            this.videobreakdown({
            videoId: "c4c1ad4c9a",
            syncTranscript: true,
            syncLanguage: true
            });

            // Set the source dynamically
            initSource.call(this);
        });

3. <span data-ttu-id="870d3-178">Copy the **Cognitive Insights** embed code.</span><span class="sxs-lookup"><span data-stu-id="870d3-178">Copy the **Cognitive Insights** embed code.</span></span>

<span data-ttu-id="870d3-179">You should be able now to communicate with your Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="870d3-179">You should be able now to communicate with your Azure Media Player.</span></span>

<span data-ttu-id="870d3-180">For more information, see [this demo](https://codepen.io/videoindexer/pen/rYONrO).</span><span class="sxs-lookup"><span data-stu-id="870d3-180">For more information, see [this demo](https://codepen.io/videoindexer/pen/rYONrO).</span></span>

### <a name="embed-video-indexer-cognitive-insights-widget-and-use-your-own-player-could-be-any-player"></a><span data-ttu-id="870d3-181">Embed Video Indexer Cognitive Insights widget and use your own player (could be any player)</span><span class="sxs-lookup"><span data-stu-id="870d3-181">Embed Video Indexer Cognitive Insights widget and use your own player (could be any player)</span></span>

<span data-ttu-id="870d3-182">If you use your own player, you have to take care of manipulating your player yourself in order to achieve the communication.</span><span class="sxs-lookup"><span data-stu-id="870d3-182">If you use your own player, you have to take care of manipulating your player yourself in order to achieve the communication.</span></span> 

1. <span data-ttu-id="870d3-183">Insert your video player.</span><span class="sxs-lookup"><span data-stu-id="870d3-183">Insert your video player.</span></span>

    <span data-ttu-id="870d3-184">For example, a standard HTML5 player</span><span class="sxs-lookup"><span data-stu-id="870d3-184">For example, a standard HTML5 player</span></span>

        <video id="vid1" width="640" height="360" controls autoplay preload>
           <source src="//breakdown.blob.core.windows.net/public/Microsoft%20HoloLens-%20RoboRaid.mp4" type="video/mp4" /> 
           Your browser does not support the video tag.
        </video>    

2. <span data-ttu-id="870d3-185">Embed the Cognitive Insights widget.</span><span class="sxs-lookup"><span data-stu-id="870d3-185">Embed the Cognitive Insights widget.</span></span>
3. <span data-ttu-id="870d3-186">Implement communication for your player by listening to the "message" event.</span><span class="sxs-lookup"><span data-stu-id="870d3-186">Implement communication for your player by listening to the "message" event.</span></span> <span data-ttu-id="870d3-187">For example:</span><span class="sxs-lookup"><span data-stu-id="870d3-187">For example:</span></span>

        <script>
    
            (function(){
            // Reference your player instance
            var playerInstance = document.getElementById('vid1');
        
            function jumpTo(evt) {
              var origin = evt.origin || evt.originalEvent.origin;
        
              // Validate that event comes from the videobreakdown domain.
              if ((origin === "https://www.videobreakdown.com") && evt.data.time !== undefined){
                
                // Here you need to call your player "jumpTo" implementation
                playerInstance.currentTime = evt.data.time;
               
                // Confirm arrival to us
                if ('postMessage' in window) {
                  evt.source.postMessage({confirm: true, time: evt.data.time}, origin);
                }
              }
            }
        
            // Listen to message event
            window.addEventListener("message", jumpTo, false);
          
            }())    
        
        </script>


<span data-ttu-id="870d3-188">For more information, see [this demo](https://codepen.io/videoindexer/pen/YEyPLd).</span><span class="sxs-lookup"><span data-stu-id="870d3-188">For more information, see [this demo](https://codepen.io/videoindexer/pen/YEyPLd).</span></span>

## <a name="adding-subtitles"></a><span data-ttu-id="870d3-189">Adding subtitles</span><span class="sxs-lookup"><span data-stu-id="870d3-189">Adding subtitles</span></span>

<span data-ttu-id="870d3-190">If you embed Video Indexer insights with your own AMP player, you can use the **GetVttUrl** method to get closed captions (subtitles).</span><span class="sxs-lookup"><span data-stu-id="870d3-190">If you embed Video Indexer insights with your own AMP player, you can use the **GetVttUrl** method to get closed captions (subtitles).</span></span> <span data-ttu-id="870d3-191">You can also call a javascript method from the Video Indexer AMP plugin **getSubtitlesUrl** (as shown earlier).</span><span class="sxs-lookup"><span data-stu-id="870d3-191">You can also call a javascript method from the Video Indexer AMP plugin **getSubtitlesUrl** (as shown earlier).</span></span> 

## <a name="customizing-embeddable-widgets"></a><span data-ttu-id="870d3-192">Customizing embeddable widgets</span><span class="sxs-lookup"><span data-stu-id="870d3-192">Customizing embeddable widgets</span></span>

### <a name="cognitive-insights-widget"></a><span data-ttu-id="870d3-193">Cognitive insights widget</span><span class="sxs-lookup"><span data-stu-id="870d3-193">Cognitive insights widget</span></span>
<span data-ttu-id="870d3-194">You can choose the types of insights you want by specifying them as a value to the following URL parameter added to the embed code you get (from API or from the web application):</span><span class="sxs-lookup"><span data-stu-id="870d3-194">You can choose the types of insights you want by specifying them as a value to the following URL parameter added to the embed code you get (from API or from the web application):</span></span>

<span data-ttu-id="870d3-195">**&widgets=** \<list of wanted widgets></span><span class="sxs-lookup"><span data-stu-id="870d3-195">**&widgets=** \<list of wanted widgets></span></span>

<span data-ttu-id="870d3-196">The possible values are: people, keywords, sentiments, transcript, search.</span><span class="sxs-lookup"><span data-stu-id="870d3-196">The possible values are: people, keywords, sentiments, transcript, search.</span></span>

<span data-ttu-id="870d3-197">For example, if you want to embed a widget containing only people and search insights the iframe embed URL will look like this: https://www.videoindexer.ai/embed/insights/c4c1ad4c9a/?widgets=people,search</span><span class="sxs-lookup"><span data-stu-id="870d3-197">For example, if you want to embed a widget containing only people and search insights the iframe embed URL will look like this: https://www.videoindexer.ai/embed/insights/c4c1ad4c9a/?widgets=people,search</span></span>

<span data-ttu-id="870d3-198">The title of the iframe window can also be customized by providing **&title=**<YourTitle> to the iframe url.</span><span class="sxs-lookup"><span data-stu-id="870d3-198">The title of the iframe window can also be customized by providing **&title=**<YourTitle> to the iframe url.</span></span> <span data-ttu-id="870d3-199">(It will customize the html \<title> value ).</span><span class="sxs-lookup"><span data-stu-id="870d3-199">(It will customize the html \<title> value ).</span></span>
<span data-ttu-id="870d3-200">For example, if you want to give your iframe window the title "MyInsights", the url will look like this: https://www.videoindexer.ai/embed/insights/c4c1ad4c9a/?title=MyInsights.</span><span class="sxs-lookup"><span data-stu-id="870d3-200">For example, if you want to give your iframe window the title "MyInsights", the url will look like this: https://www.videoindexer.ai/embed/insights/c4c1ad4c9a/?title=MyInsights.</span></span> <span data-ttu-id="870d3-201">Notice that this option is relevant only in cases when you need to open the insights in a new window.</span><span class="sxs-lookup"><span data-stu-id="870d3-201">Notice that this option is relevant only in cases when you need to open the insights in a new window.</span></span>

### <a name="player-widget"></a><span data-ttu-id="870d3-202">Player widget</span><span class="sxs-lookup"><span data-stu-id="870d3-202">Player widget</span></span>
<span data-ttu-id="870d3-203">If you embed Video Indexer player you can choose the size of the player by specifying the size of the iframe.</span><span class="sxs-lookup"><span data-stu-id="870d3-203">If you embed Video Indexer player you can choose the size of the player by specifying the size of the iframe.</span></span>

<span data-ttu-id="870d3-204">For example :</span><span class="sxs-lookup"><span data-stu-id="870d3-204">For example :</span></span>

    <iframe width="640" height="360" src="https://www.videoindexer.ai/embed/player/{id}” frameborder="0" allowfullscreen />

<span data-ttu-id="870d3-205">By default Video Indexer player will have auto generated closed captions based on the transcript of the video that was extracted from the video with the source language that was selected when the video was uploaded.</span><span class="sxs-lookup"><span data-stu-id="870d3-205">By default Video Indexer player will have auto generated closed captions based on the transcript of the video that was extracted from the video with the source language that was selected when the video was uploaded.</span></span>

<span data-ttu-id="870d3-206">If you want to embed with a different language you can add **&captions=< Language | ”all” | “false” >** to the embed player URL or put “all” as the value if you want to have all available languages captions.</span><span class="sxs-lookup"><span data-stu-id="870d3-206">If you want to embed with a different language you can add **&captions=< Language | ”all” | “false” >** to the embed player URL or put “all” as the value if you want to have all available languages captions.</span></span>
<span data-ttu-id="870d3-207">If you want the captions to be displayed by default you can pass **&showCaptions=true**</span><span class="sxs-lookup"><span data-stu-id="870d3-207">If you want the captions to be displayed by default you can pass **&showCaptions=true**</span></span>

<span data-ttu-id="870d3-208">The embed URL then will look like this : https://www.videoindexer.ai/embed/player/9a296c6ec3/?captions=italian.</span><span class="sxs-lookup"><span data-stu-id="870d3-208">The embed URL then will look like this : https://www.videoindexer.ai/embed/player/9a296c6ec3/?captions=italian.</span></span> <span data-ttu-id="870d3-209">If you want to disable captions you can pass “false” as value for captions parameter.</span><span class="sxs-lookup"><span data-stu-id="870d3-209">If you want to disable captions you can pass “false” as value for captions parameter.</span></span>

<span data-ttu-id="870d3-210">Auto play – by default the player will start playing the video.</span><span class="sxs-lookup"><span data-stu-id="870d3-210">Auto play – by default the player will start playing the video.</span></span> <span data-ttu-id="870d3-211">you can choose not to by passing &autoplay=false to the embed URL above.</span><span class="sxs-lookup"><span data-stu-id="870d3-211">you can choose not to by passing &autoplay=false to the embed URL above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="870d3-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="870d3-212">Next steps</span></span>

<span data-ttu-id="870d3-213">For information about how to view and edit Video Indexer insights, see [this](video-indexer-view-edit.md) article.</span><span class="sxs-lookup"><span data-stu-id="870d3-213">For information about how to view and edit Video Indexer insights, see [this](video-indexer-view-edit.md) article.</span></span>

<span data-ttu-id="870d3-214">Also, check out [Video indexer codepen](https://codepen.io/videoindexer/pen/eGxebZ).</span><span class="sxs-lookup"><span data-stu-id="870d3-214">Also, check out [Video indexer codepen](https://codepen.io/videoindexer/pen/eGxebZ).</span></span>
