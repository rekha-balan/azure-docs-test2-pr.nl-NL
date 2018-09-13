---
title: Publish content in the Azure portal | Microsoft Docs
description: This tutorial walks you through the steps of publishing your content in the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d93bfc548134f730f4fad49a37593c861d6b6cbb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871033"
---
# <a name="publish-content-in-the-azure-portal"></a><span data-ttu-id="75c54-103">Publish content in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="75c54-103">Publish content in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="75c54-107">Overview</span><span class="sxs-lookup"><span data-stu-id="75c54-107">Overview</span></span>
> [!NOTE]
> To complete this tutorial, you need an Azure account. For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

<span data-ttu-id="75c54-110">To provide your user with a URL that they can use to stream or download your content, first you must publish your asset by creating a locator.</span><span class="sxs-lookup"><span data-stu-id="75c54-110">To provide your user with a URL that they can use to stream or download your content, first you must publish your asset by creating a locator.</span></span> <span data-ttu-id="75c54-111">Locators provide access to asset files.</span><span class="sxs-lookup"><span data-stu-id="75c54-111">Locators provide access to asset files.</span></span> <span data-ttu-id="75c54-112">Azure Media Services supports two types of locators:</span><span class="sxs-lookup"><span data-stu-id="75c54-112">Azure Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="75c54-113">**Streaming (OnDemandOrigin) locators**.</span><span class="sxs-lookup"><span data-stu-id="75c54-113">**Streaming (OnDemandOrigin) locators**.</span></span> <span data-ttu-id="75c54-114">Streaming locators are used for adaptive streaming.</span><span class="sxs-lookup"><span data-stu-id="75c54-114">Streaming locators are used for adaptive streaming.</span></span> <span data-ttu-id="75c54-115">Examples of adaptive streaming include Apple HTTP Live Streaming (HLS), Microsoft Smooth Streaming, and Dynamic Adaptive Streaming over HTTP (DASH, also called MPEG-DASH).</span><span class="sxs-lookup"><span data-stu-id="75c54-115">Examples of adaptive streaming include Apple HTTP Live Streaming (HLS), Microsoft Smooth Streaming, and Dynamic Adaptive Streaming over HTTP (DASH, also called MPEG-DASH).</span></span> <span data-ttu-id="75c54-116">To create a streaming locator, your asset must include an .ism file.</span><span class="sxs-lookup"><span data-stu-id="75c54-116">To create a streaming locator, your asset must include an .ism file.</span></span> <span data-ttu-id="75c54-117">For example, http://amstest.streaming.mediaservices.windows.net/61b3da1d-96c7-489e-bd21-c5f8a7494b03/scott.ism/manifest.</span><span class="sxs-lookup"><span data-stu-id="75c54-117">For example, http://amstest.streaming.mediaservices.windows.net/61b3da1d-96c7-489e-bd21-c5f8a7494b03/scott.ism/manifest.</span></span>
* <span data-ttu-id="75c54-118">**Progressive (shared access signature) locators**.</span><span class="sxs-lookup"><span data-stu-id="75c54-118">**Progressive (shared access signature) locators**.</span></span> <span data-ttu-id="75c54-119">Progressive locators are used to deliver video via progressive download.</span><span class="sxs-lookup"><span data-stu-id="75c54-119">Progressive locators are used to deliver video via progressive download.</span></span>

<span data-ttu-id="75c54-120">To build an HLS streaming URL, append *(format=m3u8-aapl)* to the URL:</span><span class="sxs-lookup"><span data-stu-id="75c54-120">To build an HLS streaming URL, append *(format=m3u8-aapl)* to the URL:</span></span>

    {streaming endpoint name-media services account name}/{locator ID}/{file name}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="75c54-121">To build a streaming URL to play Smooth Streaming assets, use the following URL format:</span><span class="sxs-lookup"><span data-stu-id="75c54-121">To build a streaming URL to play Smooth Streaming assets, use the following URL format:</span></span>

    {streaming endpoint name-media services account name}/{locator ID}/{file name}.ism/Manifest

<span data-ttu-id="75c54-122">To build an MPEG-DASH streaming URL, append *(format=mpd-time-csf)* to the URL:</span><span class="sxs-lookup"><span data-stu-id="75c54-122">To build an MPEG-DASH streaming URL, append *(format=mpd-time-csf)* to the URL:</span></span>

    {streaming endpoint name-media services account name}/{locator ID}/{file name}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="75c54-123">A shared access signature URL has the following format:</span><span class="sxs-lookup"><span data-stu-id="75c54-123">A shared access signature URL has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{shared access signature}

<span data-ttu-id="75c54-124">For more information, see the [delivering content overview](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="75c54-124">For more information, see the [delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> Locators that were created in the Azure portal before March 2015 have a two-year expiration date.  
> 
> 

<span data-ttu-id="75c54-126">To update an expiration date on a locator, use can use a [REST API](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or a [.NET API](http://go.microsoft.com/fwlink/?LinkID=533259).</span><span class="sxs-lookup"><span data-stu-id="75c54-126">To update an expiration date on a locator, use can use a [REST API](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or a [.NET API](http://go.microsoft.com/fwlink/?LinkID=533259).</span></span> 

> [!NOTE]
> When you update the expiration date of a shared access signature locator, the URL changes.

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="75c54-128">To use the portal to publish an asset</span><span class="sxs-lookup"><span data-stu-id="75c54-128">To use the portal to publish an asset</span></span>
1. <span data-ttu-id="75c54-129">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="75c54-129">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="75c54-130">Select **Settings** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="75c54-130">Select **Settings** > **Assets**.</span></span> <span data-ttu-id="75c54-131">Select the asset that you want to publish.</span><span class="sxs-lookup"><span data-stu-id="75c54-131">Select the asset that you want to publish.</span></span>
3. <span data-ttu-id="75c54-132">Select the **Publish** button.</span><span class="sxs-lookup"><span data-stu-id="75c54-132">Select the **Publish** button.</span></span>
4. <span data-ttu-id="75c54-133">Select the locator type.</span><span class="sxs-lookup"><span data-stu-id="75c54-133">Select the locator type.</span></span>
5. <span data-ttu-id="75c54-134">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="75c54-134">Select **Add**.</span></span>
   
    ![Publish the video](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="75c54-136">The URL is added to the list of **Published URLs**.</span><span class="sxs-lookup"><span data-stu-id="75c54-136">The URL is added to the list of **Published URLs**.</span></span>

## <a name="play-content-in-the-portal"></a><span data-ttu-id="75c54-137">Play content in the portal</span><span class="sxs-lookup"><span data-stu-id="75c54-137">Play content in the portal</span></span>
<span data-ttu-id="75c54-138">You can test your video on a content player in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="75c54-138">You can test your video on a content player in the Azure portal.</span></span>

<span data-ttu-id="75c54-139">Select the video, and then select the **Play** button.</span><span class="sxs-lookup"><span data-stu-id="75c54-139">Select the video, and then select the **Play** button.</span></span>

![Play the video in the Azure portal](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="75c54-141">Some considerations apply:</span><span class="sxs-lookup"><span data-stu-id="75c54-141">Some considerations apply:</span></span>

* <span data-ttu-id="75c54-142">Make sure that the video has been published.</span><span class="sxs-lookup"><span data-stu-id="75c54-142">Make sure that the video has been published.</span></span>
* <span data-ttu-id="75c54-143">The Azure portal media player plays from the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="75c54-143">The Azure portal media player plays from the default streaming endpoint.</span></span> <span data-ttu-id="75c54-144">If you want to play from a non-default streaming endpoint, select and copy the URL, and then paste it into another player.</span><span class="sxs-lookup"><span data-stu-id="75c54-144">If you want to play from a non-default streaming endpoint, select and copy the URL, and then paste it into another player.</span></span> <span data-ttu-id="75c54-145">For example, you can test your video on the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="75c54-145">For example, you can test your video on the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="75c54-146">The streaming endpoint from which you are streaming must be running.</span><span class="sxs-lookup"><span data-stu-id="75c54-146">The streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="provide-feedback"></a><span data-ttu-id="75c54-147">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="75c54-147">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="75c54-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="75c54-148">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

