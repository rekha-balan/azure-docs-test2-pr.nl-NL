---
title: Using castLabs to deliver Widevine licenses to Azure Media Services | Microsoft Docs
description: This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs. The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by castLabs license server.
services: media-services
documentationcenter: ''
author: Mingfeiy
manager: cfowler
editor: ''
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: aff5b94840e63176358d64a535c9cc0dd9ec617a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868292"
---
# <a name="using-castlabs-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="e3ce7-104">Using castLabs to deliver Widevine licenses to Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="e3ce7-104">Using castLabs to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e3ce7-107">Overview</span><span class="sxs-lookup"><span data-stu-id="e3ce7-107">Overview</span></span>
<span data-ttu-id="e3ce7-108">This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-108">This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="e3ce7-109">The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-109">The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="e3ce7-110">To playback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="e3ce7-110">To playback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="e3ce7-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="e3ce7-112">The following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-112">The following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![integration](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="e3ce7-114">Typical system set up</span><span class="sxs-lookup"><span data-stu-id="e3ce7-114">Typical system set up</span></span>
* <span data-ttu-id="e3ce7-115">Media content is stored in AMS.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="e3ce7-116">Key IDs of content keys are stored in both castLabs and AMS.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="e3ce7-117">castLabs and AMS both have token authentication built in.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="e3ce7-118">The following sections discuss authentication tokens.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-118">The following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="e3ce7-119">When a client requests to stream the video, the content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS to Smooth Streaming and DASH.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-119">When a client requests to stream the video, the content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS to Smooth Streaming and DASH.</span></span> <span data-ttu-id="e3ce7-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="e3ce7-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="e3ce7-122">Media Player automatically decides which license to fetch based on the client platform capability.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-122">Media Player automatically decides which license to fetch based on the client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="e3ce7-123">Authentication token generation for getting a license</span><span class="sxs-lookup"><span data-stu-id="e3ce7-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="e3ce7-124">Both castLabs and AMS support JWT (JSON Web Token) token format used to authorize a license.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-124">Both castLabs and AMS support JWT (JSON Web Token) token format used to authorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="e3ce7-125">JWT token in AMS</span><span class="sxs-lookup"><span data-stu-id="e3ce7-125">JWT token in AMS</span></span>
<span data-ttu-id="e3ce7-126">The following table describes JWT token in AMS.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-126">The following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="e3ce7-127">Issuer</span><span class="sxs-lookup"><span data-stu-id="e3ce7-127">Issuer</span></span> | <span data-ttu-id="e3ce7-128">Issuer string from the chosen Secure Token Service (STS)</span><span class="sxs-lookup"><span data-stu-id="e3ce7-128">Issuer string from the chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="e3ce7-129">Audience</span><span class="sxs-lookup"><span data-stu-id="e3ce7-129">Audience</span></span> |<span data-ttu-id="e3ce7-130">Audience string from the used STS</span><span class="sxs-lookup"><span data-stu-id="e3ce7-130">Audience string from the used STS</span></span> |
| <span data-ttu-id="e3ce7-131">Claims</span><span class="sxs-lookup"><span data-stu-id="e3ce7-131">Claims</span></span> |<span data-ttu-id="e3ce7-132">A set of claims</span><span class="sxs-lookup"><span data-stu-id="e3ce7-132">A set of claims</span></span> |
| <span data-ttu-id="e3ce7-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="e3ce7-133">NotBefore</span></span> |<span data-ttu-id="e3ce7-134">Start validity of the token</span><span class="sxs-lookup"><span data-stu-id="e3ce7-134">Start validity of the token</span></span> |
| <span data-ttu-id="e3ce7-135">Expires</span><span class="sxs-lookup"><span data-stu-id="e3ce7-135">Expires</span></span> |<span data-ttu-id="e3ce7-136">End validity of the token</span><span class="sxs-lookup"><span data-stu-id="e3ce7-136">End validity of the token</span></span> |
| <span data-ttu-id="e3ce7-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="e3ce7-137">SigningCredentials</span></span> |<span data-ttu-id="e3ce7-138">The key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-138">The key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="e3ce7-139">JWT token in castLabs</span><span class="sxs-lookup"><span data-stu-id="e3ce7-139">JWT token in castLabs</span></span>
<span data-ttu-id="e3ce7-140">The following table describes JWT token in castLabs.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-140">The following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="e3ce7-141">Name</span><span class="sxs-lookup"><span data-stu-id="e3ce7-141">Name</span></span> | <span data-ttu-id="e3ce7-142">Description</span><span class="sxs-lookup"><span data-stu-id="e3ce7-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3ce7-143">optData</span><span class="sxs-lookup"><span data-stu-id="e3ce7-143">optData</span></span> |<span data-ttu-id="e3ce7-144">A JSON string containing information about you.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="e3ce7-145">crt</span><span class="sxs-lookup"><span data-stu-id="e3ce7-145">crt</span></span> |<span data-ttu-id="e3ce7-146">A JSON string containing information about the asset, its license info and playback rights.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-146">A JSON string containing information about the asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="e3ce7-147">iat</span><span class="sxs-lookup"><span data-stu-id="e3ce7-147">iat</span></span> |<span data-ttu-id="e3ce7-148">The current datetime in epoch.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-148">The current datetime in epoch.</span></span> |
| <span data-ttu-id="e3ce7-149">jti</span><span class="sxs-lookup"><span data-stu-id="e3ce7-149">jti</span></span> |<span data-ttu-id="e3ce7-150">A unique identifier about this token (every token can only be used once in the castLabs system).</span><span class="sxs-lookup"><span data-stu-id="e3ce7-150">A unique identifier about this token (every token can only be used once in the castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="e3ce7-151">Sample solution set up</span><span class="sxs-lookup"><span data-stu-id="e3ce7-151">Sample solution set up</span></span>
<span data-ttu-id="e3ce7-152">The [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span><span class="sxs-lookup"><span data-stu-id="e3ce7-152">The [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="e3ce7-153">A console app that can be used to set DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-153">A console app that can be used to set DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="e3ce7-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="e3ce7-155">To use the console application:</span><span class="sxs-lookup"><span data-stu-id="e3ce7-155">To use the console application:</span></span>

1. <span data-ttu-id="e3ce7-156">Change the app.config to setup AMS credentials, castLabs credentials, STS configuration and shared key.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-156">Change the app.config to setup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="e3ce7-157">Upload an Asset into AMS.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="e3ce7-158">Get the UUID from the uploaded Asset, and change Line 32 in the Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="e3ce7-158">Get the UUID from the uploaded Asset, and change Line 32 in the Program.cs file:</span></span>
   
      <span data-ttu-id="e3ce7-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="e3ce7-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="e3ce7-160">Use an AssetId for naming the asset in the castLabs system (Line 44 in the Program.cs file).</span><span class="sxs-lookup"><span data-stu-id="e3ce7-160">Use an AssetId for naming the asset in the castLabs system (Line 44 in the Program.cs file).</span></span>
   
   <span data-ttu-id="e3ce7-161">You must set AssetId for **castLabs**; it needs to be a unique alphanumeric string.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-161">You must set AssetId for **castLabs**; it needs to be a unique alphanumeric string.</span></span>
5. <span data-ttu-id="e3ce7-162">Run the program.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-162">Run the program.</span></span>

<span data-ttu-id="e3ce7-163">To use the Web Application (STS):</span><span class="sxs-lookup"><span data-stu-id="e3ce7-163">To use the Web Application (STS):</span></span>

1. <span data-ttu-id="e3ce7-164">Change the web.config to setup castlabs merchant ID, the STS configuration and the shared key.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-164">Change the web.config to setup castlabs merchant ID, the STS configuration and the shared key.</span></span>
2. <span data-ttu-id="e3ce7-165">Deploy to Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-165">Deploy to Azure Websites.</span></span>
3. <span data-ttu-id="e3ce7-166">Navigate to the website.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-166">Navigate to the website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="e3ce7-167">Playing back a video</span><span class="sxs-lookup"><span data-stu-id="e3ce7-167">Playing back a video</span></span>
<span data-ttu-id="e3ce7-168">To playback a video encrypted with common encryption (PlayReady and/or Widevine), you can use the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="e3ce7-168">To playback a video encrypted with common encryption (PlayReady and/or Widevine), you can use the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="e3ce7-169">When running the console app, the Content Key ID and the Manifest URL are echoed.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-169">When running the console app, the Content Key ID and the Manifest URL are echoed.</span></span>

1. <span data-ttu-id="e3ce7-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span><span class="sxs-lookup"><span data-stu-id="e3ce7-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="e3ce7-171">Go to [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="e3ce7-171">Go to [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="e3ce7-172">Paste in the streaming URL.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-172">Paste in the streaming URL.</span></span>
4. <span data-ttu-id="e3ce7-173">Click the **Advanced Options** checkbox.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-173">Click the **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="e3ce7-174">In the **Protection** dropdown, select PlayReady and/or Widevine.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-174">In the **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="e3ce7-175">Paste the token that you got from your STS in the Token textbox.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-175">Paste the token that you got from your STS in the Token textbox.</span></span> 
   
   <span data-ttu-id="e3ce7-176">The castLab license server does not need the “Bearer=” prefix in front of the token.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-176">The castLab license server does not need the “Bearer=” prefix in front of the token.</span></span> <span data-ttu-id="e3ce7-177">So please remove that before submitting the token.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-177">So please remove that before submitting the token.</span></span>
7. <span data-ttu-id="e3ce7-178">Update the player.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-178">Update the player.</span></span>
8. <span data-ttu-id="e3ce7-179">The video should be playing.</span><span class="sxs-lookup"><span data-stu-id="e3ce7-179">The video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e3ce7-180">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="e3ce7-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e3ce7-181">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="e3ce7-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

