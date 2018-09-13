---
title: Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js | Microsoft Docs
description: This topic demonstrates how to embed an MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js.
author: Juliako
manager: cfowler
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 2b0e6bf643f55e1809b29def7766c58b59f4bb50
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868730"
---
# <a name="embedding-an-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="7a62a-103">Embedding an MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span><span class="sxs-lookup"><span data-stu-id="7a62a-103">Embedding an MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="7a62a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7a62a-104">Overview</span></span>
<span data-ttu-id="7a62a-105">MPEG-DASH is an ISO standard for the adaptive streaming of video content, which offers significant benefits for developers wanting to deliver high-quality, adaptive video streaming output.</span><span class="sxs-lookup"><span data-stu-id="7a62a-105">MPEG-DASH is an ISO standard for the adaptive streaming of video content, which offers significant benefits for developers wanting to deliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="7a62a-106">With MPEG-DASH, the video stream adjusts automatically to a lower definition when the network becomes congested.</span><span class="sxs-lookup"><span data-stu-id="7a62a-106">With MPEG-DASH, the video stream adjusts automatically to a lower definition when the network becomes congested.</span></span> <span data-ttu-id="7a62a-107">This reduces the likelihood of the viewer seeing a "paused" video while the player downloads the next few seconds to play (aka buffering).</span><span class="sxs-lookup"><span data-stu-id="7a62a-107">This reduces the likelihood of the viewer seeing a "paused" video while the player downloads the next few seconds to play (aka buffering).</span></span> <span data-ttu-id="7a62a-108">As network congestion reduces, the video player will in turn return to a higher-quality stream.</span><span class="sxs-lookup"><span data-stu-id="7a62a-108">As network congestion reduces, the video player will in turn return to a higher-quality stream.</span></span> <span data-ttu-id="7a62a-109">This ability to adapt the bandwidth required also results in a faster start time for video.</span><span class="sxs-lookup"><span data-stu-id="7a62a-109">This ability to adapt the bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="7a62a-110">That means that the first few seconds can be played in a fast-to-download lower quality segment and then step up to a higher quality once sufficient content has been buffered.</span><span class="sxs-lookup"><span data-stu-id="7a62a-110">That means that the first few seconds can be played in a fast-to-download lower quality segment and then step up to a higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="7a62a-111">Dash.js is an open-source MPEG-DASH video player written in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7a62a-111">Dash.js is an open-source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="7a62a-112">Its goal is to provide a robust, cross-platform player that can be freely reused in applications that require video playback.</span><span class="sxs-lookup"><span data-stu-id="7a62a-112">Its goal is to provide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="7a62a-113">It provides MPEG-DASH playback in any browser that supports the W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge, and IE11 (other browsers have indicated their intent to support MSE).</span><span class="sxs-lookup"><span data-stu-id="7a62a-113">It provides MPEG-DASH playback in any browser that supports the W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge, and IE11 (other browsers have indicated their intent to support MSE).</span></span> <span data-ttu-id="7a62a-114">For more information about DASH.js, js see the GitHub dash.js repository.</span><span class="sxs-lookup"><span data-stu-id="7a62a-114">For more information about DASH.js, js see the GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="7a62a-115">Creating a browser-based streaming video player</span><span class="sxs-lookup"><span data-stu-id="7a62a-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="7a62a-116">To create a simple web page that displays a video player with the expected controls such a play, pause, rewind etc., you need to:</span><span class="sxs-lookup"><span data-stu-id="7a62a-116">To create a simple web page that displays a video player with the expected controls such a play, pause, rewind etc., you need to:</span></span>

1. <span data-ttu-id="7a62a-117">Create an HTML page</span><span class="sxs-lookup"><span data-stu-id="7a62a-117">Create an HTML page</span></span>
2. <span data-ttu-id="7a62a-118">Add the video tag</span><span class="sxs-lookup"><span data-stu-id="7a62a-118">Add the video tag</span></span>
3. <span data-ttu-id="7a62a-119">Add the dash.js player</span><span class="sxs-lookup"><span data-stu-id="7a62a-119">Add the dash.js player</span></span>
4. <span data-ttu-id="7a62a-120">Initialize the player</span><span class="sxs-lookup"><span data-stu-id="7a62a-120">Initialize the player</span></span>
5. <span data-ttu-id="7a62a-121">Add some CSS style</span><span class="sxs-lookup"><span data-stu-id="7a62a-121">Add some CSS style</span></span>
6. <span data-ttu-id="7a62a-122">View the results in a browser that implements MSE</span><span class="sxs-lookup"><span data-stu-id="7a62a-122">View the results in a browser that implements MSE</span></span>

<span data-ttu-id="7a62a-123">Initializing the player can be completed in just a handful of lines of JavaScript code.</span><span class="sxs-lookup"><span data-stu-id="7a62a-123">Initializing the player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="7a62a-124">Using dash.js, it really is that simple to embed MPEG-DASH video in your browser-based applications.</span><span class="sxs-lookup"><span data-stu-id="7a62a-124">Using dash.js, it really is that simple to embed MPEG-DASH video in your browser-based applications.</span></span>

## <a name="creating-the-html-page"></a><span data-ttu-id="7a62a-125">Creating the HTML Page</span><span class="sxs-lookup"><span data-stu-id="7a62a-125">Creating the HTML Page</span></span>
<span data-ttu-id="7a62a-126">The first step is to create a standard HTML page containing the **video** element, save this file as basicPlayer.html, as the following example illustrates:</span><span class="sxs-lookup"><span data-stu-id="7a62a-126">The first step is to create a standard HTML page containing the **video** element, save this file as basicPlayer.html, as the following example illustrates:</span></span>

```html
    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>
```

## <a name="adding-the-dashjs-player"></a><span data-ttu-id="7a62a-127">Adding the DASH.js Player</span><span class="sxs-lookup"><span data-stu-id="7a62a-127">Adding the DASH.js Player</span></span>
<span data-ttu-id="7a62a-128">To add the dash.js reference implementation to the application, you need to grab the dash.all.js file from the 1.0 release of dash.js project.</span><span class="sxs-lookup"><span data-stu-id="7a62a-128">To add the dash.js reference implementation to the application, you need to grab the dash.all.js file from the 1.0 release of dash.js project.</span></span> <span data-ttu-id="7a62a-129">This should be saved in the JavaScript folder of your application.</span><span class="sxs-lookup"><span data-stu-id="7a62a-129">This should be saved in the JavaScript folder of your application.</span></span> <span data-ttu-id="7a62a-130">This file is a convenience file that pulls together all the necessary dash.js code into a single file.</span><span class="sxs-lookup"><span data-stu-id="7a62a-130">This file is a convenience file that pulls together all the necessary dash.js code into a single file.</span></span> <span data-ttu-id="7a62a-131">If you have a look around the dash.js repository, you find the individual files, test code and much more, but if all you want to do is use dash.js, then the dash.all.js file is what you need.</span><span class="sxs-lookup"><span data-stu-id="7a62a-131">If you have a look around the dash.js repository, you find the individual files, test code and much more, but if all you want to do is use dash.js, then the dash.all.js file is what you need.</span></span>

<span data-ttu-id="7a62a-132">To add the dash.js player to your applications, add a script tag to the head section of basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="7a62a-132">To add the dash.js player to your applications, add a script tag to the head section of basicPlayer.html:</span></span>

```html
    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>
```

<span data-ttu-id="7a62a-133">Next, create a function to initialize the player when the page loads.</span><span class="sxs-lookup"><span data-stu-id="7a62a-133">Next, create a function to initialize the player when the page loads.</span></span> <span data-ttu-id="7a62a-134">Add the following script after the line in which you load dash.all.js:</span><span class="sxs-lookup"><span data-stu-id="7a62a-134">Add the following script after the line in which you load dash.all.js:</span></span>

```html
    <script>
    // setup the video element and attach it to the Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>
```

<span data-ttu-id="7a62a-135">This function first creates a DashContext.</span><span class="sxs-lookup"><span data-stu-id="7a62a-135">This function first creates a DashContext.</span></span> <span data-ttu-id="7a62a-136">This is used to configure the application for a specific runtime environment.</span><span class="sxs-lookup"><span data-stu-id="7a62a-136">This is used to configure the application for a specific runtime environment.</span></span> <span data-ttu-id="7a62a-137">From a technical point of view, it defines the classes that the dependency injection framework should use when constructing the application.</span><span class="sxs-lookup"><span data-stu-id="7a62a-137">From a technical point of view, it defines the classes that the dependency injection framework should use when constructing the application.</span></span> <span data-ttu-id="7a62a-138">In most cases, you use Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="7a62a-138">In most cases, you use Dash.di.DashContext.</span></span>

<span data-ttu-id="7a62a-139">Next, instantiate the primary class of the dash.js framework, MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="7a62a-139">Next, instantiate the primary class of the dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="7a62a-140">This class contains the core methods needed such as play and pause, manages the relationship with the video element and also manages the interpretation of the Media Presentation Description (MPD) file, which describes the video to be played.</span><span class="sxs-lookup"><span data-stu-id="7a62a-140">This class contains the core methods needed such as play and pause, manages the relationship with the video element and also manages the interpretation of the Media Presentation Description (MPD) file, which describes the video to be played.</span></span>

<span data-ttu-id="7a62a-141">The startup() function of the MediaPlayer class is called to ensure that the player is ready to play video.</span><span class="sxs-lookup"><span data-stu-id="7a62a-141">The startup() function of the MediaPlayer class is called to ensure that the player is ready to play video.</span></span> <span data-ttu-id="7a62a-142">Among other things, the function ensures that all the necessary classes (as defined by the context) have been loaded.</span><span class="sxs-lookup"><span data-stu-id="7a62a-142">Among other things, the function ensures that all the necessary classes (as defined by the context) have been loaded.</span></span> <span data-ttu-id="7a62a-143">Once the player is ready, you can attach the video element to it using the attachView() function.</span><span class="sxs-lookup"><span data-stu-id="7a62a-143">Once the player is ready, you can attach the video element to it using the attachView() function.</span></span> <span data-ttu-id="7a62a-144">The startup function enables the MediaPlayer to inject the video stream into the element and also control playback as necessary.</span><span class="sxs-lookup"><span data-stu-id="7a62a-144">The startup function enables the MediaPlayer to inject the video stream into the element and also control playback as necessary.</span></span>

<span data-ttu-id="7a62a-145">Pass the URL of the MPD file to the MediaPlayer so that it knows about the video it is expected to play.</span><span class="sxs-lookup"><span data-stu-id="7a62a-145">Pass the URL of the MPD file to the MediaPlayer so that it knows about the video it is expected to play.</span></span> <span data-ttu-id="7a62a-146">The setupVideo() function just created will need to be executed once the page has fully loaded.</span><span class="sxs-lookup"><span data-stu-id="7a62a-146">The setupVideo() function just created will need to be executed once the page has fully loaded.</span></span> <span data-ttu-id="7a62a-147">Do this by using the onload event of the body element.</span><span class="sxs-lookup"><span data-stu-id="7a62a-147">Do this by using the onload event of the body element.</span></span> <span data-ttu-id="7a62a-148">Change your <body> element to:</span><span class="sxs-lookup"><span data-stu-id="7a62a-148">Change your <body> element to:</span></span>

```html
    <body onload="setupVideo()">
```

<span data-ttu-id="7a62a-149">Finally, set the size of the video element using CSS.</span><span class="sxs-lookup"><span data-stu-id="7a62a-149">Finally, set the size of the video element using CSS.</span></span> <span data-ttu-id="7a62a-150">In an adaptive streaming environment, this is especially important because the size of the video being played may change as playback adapts to changing network conditions.</span><span class="sxs-lookup"><span data-stu-id="7a62a-150">In an adaptive streaming environment, this is especially important because the size of the video being played may change as playback adapts to changing network conditions.</span></span> <span data-ttu-id="7a62a-151">In this simple demo simply force the video element to be 80% of the available browser window by adding the following CSS to the head section of the page:</span><span class="sxs-lookup"><span data-stu-id="7a62a-151">In this simple demo simply force the video element to be 80% of the available browser window by adding the following CSS to the head section of the page:</span></span>

```html
    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>
```

## <a name="playing-a-video"></a><span data-ttu-id="7a62a-152">Playing a Video</span><span class="sxs-lookup"><span data-stu-id="7a62a-152">Playing a Video</span></span>
<span data-ttu-id="7a62a-153">To play a video, point your browser at the basicPlayback.html file and click play on the video player displayed.</span><span class="sxs-lookup"><span data-stu-id="7a62a-153">To play a video, point your browser at the basicPlayback.html file and click play on the video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="7a62a-154">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="7a62a-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7a62a-155">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="7a62a-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="7a62a-156">See Also</span><span class="sxs-lookup"><span data-stu-id="7a62a-156">See Also</span></span>
[<span data-ttu-id="7a62a-157">Develop video player applications</span><span class="sxs-lookup"><span data-stu-id="7a62a-157">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="7a62a-158">GitHub dash.js repository</span><span class="sxs-lookup"><span data-stu-id="7a62a-158">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

