---
title: Create clips with Azure Media Clipper | Microsoft Docs
description: Overview of Azure Media Clipper, a tool for building media clips from assets
services: media-services
keywords: clip;subclip;encoding;media
author: dbgeorge
manager: jasonsue
ms.author: dwgeo
ms.date: 11/10/2017
ms.topic: article
ms.service: media-services
ms.openlocfilehash: f3822386d0d16b1feaf16853424329558a18f910
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867534"
---
# <a name="create-clips-with-azure-media-clipper"></a><span data-ttu-id="39935-104">Create clips with Azure Media Clipper</span><span class="sxs-lookup"><span data-stu-id="39935-104">Create clips with Azure Media Clipper</span></span>
<span data-ttu-id="39935-105">Azure Media Clipper is a free JavaScript library that enables web developers to provide their users with an interface for creating media clips.</span><span class="sxs-lookup"><span data-stu-id="39935-105">Azure Media Clipper is a free JavaScript library that enables web developers to provide their users with an interface for creating media clips.</span></span> <span data-ttu-id="39935-106">This tool can be integrated into any web page and provides APIs for loading assets and submitting clipping jobs.</span><span class="sxs-lookup"><span data-stu-id="39935-106">This tool can be integrated into any web page and provides APIs for loading assets and submitting clipping jobs.</span></span>

<span data-ttu-id="39935-107">Azure Media Clipper enables you to:</span><span class="sxs-lookup"><span data-stu-id="39935-107">Azure Media Clipper enables you to:</span></span>
- <span data-ttu-id="39935-108">Trim the pre-slate and post-slate from live archives</span><span class="sxs-lookup"><span data-stu-id="39935-108">Trim the pre-slate and post-slate from live archives</span></span> 
- <span data-ttu-id="39935-109">Compose video highlights from AMS live events, live archives, or fMP4 VOD files</span><span class="sxs-lookup"><span data-stu-id="39935-109">Compose video highlights from AMS live events, live archives, or fMP4 VOD files</span></span> 
- <span data-ttu-id="39935-110">Concatenate videos from multiple sources</span><span class="sxs-lookup"><span data-stu-id="39935-110">Concatenate videos from multiple sources</span></span> 
- <span data-ttu-id="39935-111">Produce summary clips from your AMS media assets</span><span class="sxs-lookup"><span data-stu-id="39935-111">Produce summary clips from your AMS media assets</span></span> 
- <span data-ttu-id="39935-112">Clip videos with frame accuracy</span><span class="sxs-lookup"><span data-stu-id="39935-112">Clip videos with frame accuracy</span></span> 
- <span data-ttu-id="39935-113">Generate dynamic manifest filters over existing live and VOD assets with group-of-pictures (GOP) accuracy</span><span class="sxs-lookup"><span data-stu-id="39935-113">Generate dynamic manifest filters over existing live and VOD assets with group-of-pictures (GOP) accuracy</span></span> 
- <span data-ttu-id="39935-114">Produce encoding jobs against the assets in your media services account</span><span class="sxs-lookup"><span data-stu-id="39935-114">Produce encoding jobs against the assets in your media services account</span></span>

<span data-ttu-id="39935-115">To request new features, provide ideas or feedback, submit to [UserVoice for Azure Media Services](http://aka.ms/amsvoice/).</span><span class="sxs-lookup"><span data-stu-id="39935-115">To request new features, provide ideas or feedback, submit to [UserVoice for Azure Media Services](http://aka.ms/amsvoice/).</span></span> <span data-ttu-id="39935-116">If you have and specific issues, questions or find any bugs, drop the Media Services team a line at amcinfo@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="39935-116">If you have and specific issues, questions or find any bugs, drop the Media Services team a line at amcinfo@microsoft.com.</span></span>

<span data-ttu-id="39935-117">The following image illustrates the Clipper interface: ![Azure Media Clipper](media/media-services-azure-media-clipper-overview/media-services-azure-media-clipper-interface.PNG)</span><span class="sxs-lookup"><span data-stu-id="39935-117">The following image illustrates the Clipper interface: ![Azure Media Clipper](media/media-services-azure-media-clipper-overview/media-services-azure-media-clipper-interface.PNG)</span></span>

## <a name="release-notes"></a><span data-ttu-id="39935-118">Release notes</span><span class="sxs-lookup"><span data-stu-id="39935-118">Release notes</span></span>
<span data-ttu-id="39935-119">See the following list for the Clipper blog post, various known issues, and changelog for the latest release of the Clipper:</span><span class="sxs-lookup"><span data-stu-id="39935-119">See the following list for the Clipper blog post, various known issues, and changelog for the latest release of the Clipper:</span></span>
- [<span data-ttu-id="39935-120">Blog post</span><span class="sxs-lookup"><span data-stu-id="39935-120">Blog post</span></span>](https://azure.microsoft.com/blog/azure-media-clipper/)
- [<span data-ttu-id="39935-121">Known issues list</span><span class="sxs-lookup"><span data-stu-id="39935-121">Known issues list</span></span>](https://amp.azure.net/libs/amc/latest/docs/known_issues.html)
- [<span data-ttu-id="39935-122">Changelog</span><span class="sxs-lookup"><span data-stu-id="39935-122">Changelog</span></span>](https://amp.azure.net/libs/amc/latest/docs/changelog.html)

## <a name="browser-support"></a><span data-ttu-id="39935-123">Browser support</span><span class="sxs-lookup"><span data-stu-id="39935-123">Browser support</span></span>
<span data-ttu-id="39935-124">Azure Media Clipper is built using modern HTML5 technologies and supports the following browsers:</span><span class="sxs-lookup"><span data-stu-id="39935-124">Azure Media Clipper is built using modern HTML5 technologies and supports the following browsers:</span></span>

- <span data-ttu-id="39935-125">Microsoft Edge 13+</span><span class="sxs-lookup"><span data-stu-id="39935-125">Microsoft Edge 13+</span></span>
- <span data-ttu-id="39935-126">Internet Explorer 11+</span><span class="sxs-lookup"><span data-stu-id="39935-126">Internet Explorer 11+</span></span>
- <span data-ttu-id="39935-127">Chrome 54+</span><span class="sxs-lookup"><span data-stu-id="39935-127">Chrome 54+</span></span>
- <span data-ttu-id="39935-128">Safari 10+</span><span class="sxs-lookup"><span data-stu-id="39935-128">Safari 10+</span></span>
- <span data-ttu-id="39935-129">Firefox 50+</span><span class="sxs-lookup"><span data-stu-id="39935-129">Firefox 50+</span></span>

> [!NOTE]
> <span data-ttu-id="39935-130">Only HTML5 playback of streams from Azure Media Services is currently supported.</span><span class="sxs-lookup"><span data-stu-id="39935-130">Only HTML5 playback of streams from Azure Media Services is currently supported.</span></span>

## <a name="language-support"></a><span data-ttu-id="39935-131">Language support</span><span class="sxs-lookup"><span data-stu-id="39935-131">Language support</span></span>
<span data-ttu-id="39935-132">The Clipper widget is available in the following 18 languages:</span><span class="sxs-lookup"><span data-stu-id="39935-132">The Clipper widget is available in the following 18 languages:</span></span>
- <span data-ttu-id="39935-133">Chinese (Simplified)</span><span class="sxs-lookup"><span data-stu-id="39935-133">Chinese (Simplified)</span></span>
- <span data-ttu-id="39935-134">Chinese (Traditional)</span><span class="sxs-lookup"><span data-stu-id="39935-134">Chinese (Traditional)</span></span>
- <span data-ttu-id="39935-135">Czech</span><span class="sxs-lookup"><span data-stu-id="39935-135">Czech</span></span>
- <span data-ttu-id="39935-136">Dutch, Flemish</span><span class="sxs-lookup"><span data-stu-id="39935-136">Dutch, Flemish</span></span>
- <span data-ttu-id="39935-137">English</span><span class="sxs-lookup"><span data-stu-id="39935-137">English</span></span>
- <span data-ttu-id="39935-138">French</span><span class="sxs-lookup"><span data-stu-id="39935-138">French</span></span>
- <span data-ttu-id="39935-139">German</span><span class="sxs-lookup"><span data-stu-id="39935-139">German</span></span>
- <span data-ttu-id="39935-140">Hungarian</span><span class="sxs-lookup"><span data-stu-id="39935-140">Hungarian</span></span>
- <span data-ttu-id="39935-141">Italian</span><span class="sxs-lookup"><span data-stu-id="39935-141">Italian</span></span>
- <span data-ttu-id="39935-142">Japanese</span><span class="sxs-lookup"><span data-stu-id="39935-142">Japanese</span></span>
- <span data-ttu-id="39935-143">Korean</span><span class="sxs-lookup"><span data-stu-id="39935-143">Korean</span></span>
- <span data-ttu-id="39935-144">Polish</span><span class="sxs-lookup"><span data-stu-id="39935-144">Polish</span></span>
- <span data-ttu-id="39935-145">Portuguese (Brazil)</span><span class="sxs-lookup"><span data-stu-id="39935-145">Portuguese (Brazil)</span></span>
- <span data-ttu-id="39935-146">Portuguese (Portugal)</span><span class="sxs-lookup"><span data-stu-id="39935-146">Portuguese (Portugal)</span></span>
- <span data-ttu-id="39935-147">Russian</span><span class="sxs-lookup"><span data-stu-id="39935-147">Russian</span></span>
- <span data-ttu-id="39935-148">Spanish</span><span class="sxs-lookup"><span data-stu-id="39935-148">Spanish</span></span>
- <span data-ttu-id="39935-149">Swedish</span><span class="sxs-lookup"><span data-stu-id="39935-149">Swedish</span></span>
- <span data-ttu-id="39935-150">Turkish</span><span class="sxs-lookup"><span data-stu-id="39935-150">Turkish</span></span>

## <a name="next-steps"></a><span data-ttu-id="39935-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="39935-151">Next steps</span></span>
<span data-ttu-id="39935-152">To get started using Azure Media Clipper, read the [getting started](media-services-azure-media-clipper-getting-started.md) article for details on how to deploy the widget.</span><span class="sxs-lookup"><span data-stu-id="39935-152">To get started using Azure Media Clipper, read the [getting started](media-services-azure-media-clipper-getting-started.md) article for details on how to deploy the widget.</span></span>
