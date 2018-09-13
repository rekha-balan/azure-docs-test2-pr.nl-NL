---
title: Creating Filters with Azure Media Services .NET SDK
description: This topic describes how to create filters so your client can use them to stream specific sections of a stream. Media Services creates dynamic manifests to achieve this selective streaming.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 12/07/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 04e6a1ac9b1fc94388580f03c6767da3da226c3a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857160"
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="6b1f4-104">Creating Filters with Azure Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6b1f4-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="6b1f4-107">Starting with 2.17 release, Media Services enables you to define filters for your assets.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-107">Starting with 2.17 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="6b1f4-108">These filters are server-side rules that allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span><span class="sxs-lookup"><span data-stu-id="6b1f4-108">These filters are server-side rules that allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="6b1f4-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span><span class="sxs-lookup"><span data-stu-id="6b1f4-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="6b1f4-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b1f4-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="6b1f4-111">This article shows how to use Media Services .NET SDK to create, update, and delete filters.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-111">This article shows how to use Media Services .NET SDK to create, update, and delete filters.</span></span> 

<span data-ttu-id="6b1f4-112">Note if you update a filter, it can take up to two minutes for streaming endpoint to refresh the rules.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-112">Note if you update a filter, it can take up to two minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="6b1f4-113">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-113">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="6b1f4-114">Always clear the cache after updating the filter.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-114">Always clear the cache after updating the filter.</span></span> <span data-ttu-id="6b1f4-115">If this option is not possible, consider using a different filter.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="6b1f4-116">Types used to create filters</span><span class="sxs-lookup"><span data-stu-id="6b1f4-116">Types used to create filters</span></span>
<span data-ttu-id="6b1f4-117">The following types are used when creating filters:</span><span class="sxs-lookup"><span data-stu-id="6b1f4-117">The following types are used when creating filters:</span></span> 

* <span data-ttu-id="6b1f4-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="6b1f4-119">This type is based on the following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="6b1f4-119">This type is based on the following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="6b1f4-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="6b1f4-121">This type is based on the following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="6b1f4-121">This type is based on the following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="6b1f4-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="6b1f4-123">This type is based on the following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="6b1f4-123">This type is based on the following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="6b1f4-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="6b1f4-125">These types are based on the following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="6b1f4-125">These types are based on the following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="6b1f4-126">Create/Update/Read/Delete global filters</span><span class="sxs-lookup"><span data-stu-id="6b1f4-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="6b1f4-127">The following code shows how to use .NET to create, update, read, and delete asset filters.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-127">The following code shows how to use .NET to create, update, read, and delete asset filters.</span></span>

```csharp
    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();
```

## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="6b1f4-128">Create/Update/Read/Delete asset filters</span><span class="sxs-lookup"><span data-stu-id="6b1f4-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="6b1f4-129">The following code shows how to use .NET to create, update, read, and delete asset filters.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-129">The following code shows how to use .NET to create, update, read, and delete asset filters.</span></span>

```csharp
    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();

```


## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="6b1f4-130">Build streaming URLs that use filters</span><span class="sxs-lookup"><span data-stu-id="6b1f4-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="6b1f4-131">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b1f4-131">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="6b1f4-132">The following examples show how to add filters to your streaming URLs.</span><span class="sxs-lookup"><span data-stu-id="6b1f4-132">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="6b1f4-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="6b1f4-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="6b1f4-134">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="6b1f4-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="6b1f4-135">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="6b1f4-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="6b1f4-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="6b1f4-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="6b1f4-137">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="6b1f4-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6b1f4-138">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="6b1f4-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="6b1f4-139">See Also</span><span class="sxs-lookup"><span data-stu-id="6b1f4-139">See Also</span></span>
[<span data-ttu-id="6b1f4-140">Dynamic manifests overview</span><span class="sxs-lookup"><span data-stu-id="6b1f4-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

