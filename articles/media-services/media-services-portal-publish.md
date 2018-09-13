---
title: "  Publish content with the Azure portal | Microsoft Docs"
description: This tutorial walks you through the steps of publishing your content with the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: juliako
ms.openlocfilehash: 59def4242b9ae61eab1b52474fbd4648e9179bde
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553340"
---
# <a name="publish-content-with-the-azure-portal"></a><span data-ttu-id="10d9b-103">Publish content with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="10d9b-103">Publish content with the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="10d9b-107">Overview</span><span class="sxs-lookup"><span data-stu-id="10d9b-107">Overview</span></span>
> [!NOTE]
> To complete this tutorial, you need an Azure account. For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

<span data-ttu-id="10d9b-110">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span><span class="sxs-lookup"><span data-stu-id="10d9b-110">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="10d9b-111">Locators provide access to files contained in the asset.</span><span class="sxs-lookup"><span data-stu-id="10d9b-111">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="10d9b-112">Media Services supports two types of locators:</span><span class="sxs-lookup"><span data-stu-id="10d9b-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="10d9b-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="10d9b-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="10d9b-114">To create a streaming locator your asset must contain an .ism file.</span><span class="sxs-lookup"><span data-stu-id="10d9b-114">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="10d9b-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span><span class="sxs-lookup"><span data-stu-id="10d9b-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="10d9b-116">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span><span class="sxs-lookup"><span data-stu-id="10d9b-116">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="10d9b-117">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span><span class="sxs-lookup"><span data-stu-id="10d9b-117">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="10d9b-118">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span><span class="sxs-lookup"><span data-stu-id="10d9b-118">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="10d9b-119">A SAS URL has the following format.</span><span class="sxs-lookup"><span data-stu-id="10d9b-119">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="10d9b-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10d9b-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> If you used the portal to create locators before March 2015, locators with a two year expiration date were created.  
> 
> 

<span data-ttu-id="10d9b-122">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span><span class="sxs-lookup"><span data-stu-id="10d9b-122">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="10d9b-123">Note that when you update the expiration date of a SAS locator, the URL changes.</span><span class="sxs-lookup"><span data-stu-id="10d9b-123">Note that when you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="10d9b-124">To use the portal to publish an asset</span><span class="sxs-lookup"><span data-stu-id="10d9b-124">To use the portal to publish an asset</span></span>
<span data-ttu-id="10d9b-125">To use the portal to publish an asset, do the following:</span><span class="sxs-lookup"><span data-stu-id="10d9b-125">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="10d9b-126">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="10d9b-126">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="10d9b-127">Select **Settings** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="10d9b-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="10d9b-128">Select the asset that you want to publish.</span><span class="sxs-lookup"><span data-stu-id="10d9b-128">Select the asset that you want to publish.</span></span>
4. <span data-ttu-id="10d9b-129">Click the **Publish** button.</span><span class="sxs-lookup"><span data-stu-id="10d9b-129">Click the **Publish** button.</span></span>
5. <span data-ttu-id="10d9b-130">Select the locator type.</span><span class="sxs-lookup"><span data-stu-id="10d9b-130">Select the locator type.</span></span>
6. <span data-ttu-id="10d9b-131">Press **Add**.</span><span class="sxs-lookup"><span data-stu-id="10d9b-131">Press **Add**.</span></span>
   
    ![Publish](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="10d9b-133">The URL will be added to the list of **Published URLs**.</span><span class="sxs-lookup"><span data-stu-id="10d9b-133">The URL will be added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="10d9b-134">Play content from the portal</span><span class="sxs-lookup"><span data-stu-id="10d9b-134">Play content from the portal</span></span>
<span data-ttu-id="10d9b-135">The Azure portal provides a content player that you can use to test your video.</span><span class="sxs-lookup"><span data-stu-id="10d9b-135">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="10d9b-136">Click the desired video and then click the **Play** button.</span><span class="sxs-lookup"><span data-stu-id="10d9b-136">Click the desired video and then click the **Play** button.</span></span>

![Publish](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="10d9b-138">Some considerations apply:</span><span class="sxs-lookup"><span data-stu-id="10d9b-138">Some considerations apply:</span></span>

* <span data-ttu-id="10d9b-139">Make sure the video has been published.</span><span class="sxs-lookup"><span data-stu-id="10d9b-139">Make sure the video has been published.</span></span>
* <span data-ttu-id="10d9b-140">This **Media player** plays from the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="10d9b-140">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="10d9b-141">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span><span class="sxs-lookup"><span data-stu-id="10d9b-141">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="10d9b-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="10d9b-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="10d9b-143">The streaming endpoint from which you are streaming must be running.</span><span class="sxs-lookup"><span data-stu-id="10d9b-143">The streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="10d9b-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="10d9b-144">Next steps</span></span>
<span data-ttu-id="10d9b-145">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="10d9b-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="10d9b-146">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="10d9b-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



