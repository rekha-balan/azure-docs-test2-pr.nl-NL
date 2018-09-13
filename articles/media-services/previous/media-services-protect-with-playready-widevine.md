---
title: Use PlayReady and/or Widevine dynamic common encryption | Microsoft Docs
description: You can use Azure Media Services to deliver MPEG-DASH, Smooth Streaming, and HTTP Live Streaming (HLS) streams protected with Microsoft PlayReady DRM. You also can use it to deliver DASH encrypted with Widevine DRM. This topic shows how to dynamically encrypt with PlayReady and Widevine DRM.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: b22cc44ad1a33f5898790ece7ae7cbaabd55d1e1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865377"
---
# <a name="use-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="25fb6-105">Use PlayReady and/or Widevine dynamic common encryption</span><span class="sxs-lookup"><span data-stu-id="25fb6-105">Use PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-playready-widevine.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>

> [!NOTE]
> To get the latest version of the Java SDK and get started developing with Java, see [Get started with the Java client SDK for Azure Media Services](https://docs.microsoft.com/azure/media-services/media-services-java-how-to-use). <br/>
> To download the latest PHP SDK for Media Services, look for version 0.5.7 of the Microsoft/WindowsAzure package in the [Packagist repository](https://packagist.org/packages/microsoft/windowsazure#v0.5.7). 

## <a name="overview"></a><span data-ttu-id="25fb6-111">Overview</span><span class="sxs-lookup"><span data-stu-id="25fb6-111">Overview</span></span>

 <span data-ttu-id="25fb6-112">You can use Media Services to deliver MPEG-DASH, Smooth Streaming, and HTTP Live Streaming (HLS) streams protected with [PlayReady digital rights management (DRM)](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="25fb6-112">You can use Media Services to deliver MPEG-DASH, Smooth Streaming, and HTTP Live Streaming (HLS) streams protected with [PlayReady digital rights management (DRM)](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="25fb6-113">You also can deliver encrypted DASH streams with Widevine DRM licenses.</span><span class="sxs-lookup"><span data-stu-id="25fb6-113">You also can deliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="25fb6-114">Both PlayReady and Widevine are encrypted per the common encryption (ISO/IEC 23001-7 CENC) specification.</span><span class="sxs-lookup"><span data-stu-id="25fb6-114">Both PlayReady and Widevine are encrypted per the common encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="25fb6-115">You can use the [Media Services .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with version 3.5.1) or the REST API to configure AssetDeliveryConfiguration to use Widevine.</span><span class="sxs-lookup"><span data-stu-id="25fb6-115">You can use the [Media Services .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with version 3.5.1) or the REST API to configure AssetDeliveryConfiguration to use Widevine.</span></span>

<span data-ttu-id="25fb6-116">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span><span class="sxs-lookup"><span data-stu-id="25fb6-116">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="25fb6-117">Media Services also provides APIs that you can use to configure the rights and restrictions that you want the PlayReady or Widevine DRM runtime to enforce when a user plays back protected content.</span><span class="sxs-lookup"><span data-stu-id="25fb6-117">Media Services also provides APIs that you can use to configure the rights and restrictions that you want the PlayReady or Widevine DRM runtime to enforce when a user plays back protected content.</span></span> <span data-ttu-id="25fb6-118">When a user requests DRM-protected content, the player application requests a license from the Media Services license service.</span><span class="sxs-lookup"><span data-stu-id="25fb6-118">When a user requests DRM-protected content, the player application requests a license from the Media Services license service.</span></span> <span data-ttu-id="25fb6-119">If the player application is authorized, the Media Services license service issues a license to the player.</span><span class="sxs-lookup"><span data-stu-id="25fb6-119">If the player application is authorized, the Media Services license service issues a license to the player.</span></span> <span data-ttu-id="25fb6-120">A PlayReady or Widevine license contains the decryption key that can be used by the client player to decrypt and stream the content.</span><span class="sxs-lookup"><span data-stu-id="25fb6-120">A PlayReady or Widevine license contains the decryption key that can be used by the client player to decrypt and stream the content.</span></span>

<span data-ttu-id="25fb6-121">You also can use the following Media Services partners to help you deliver Widevine licenses:</span><span class="sxs-lookup"><span data-stu-id="25fb6-121">You also can use the following Media Services partners to help you deliver Widevine licenses:</span></span> 

* [<span data-ttu-id="25fb6-122">Axinom</span><span class="sxs-lookup"><span data-stu-id="25fb6-122">Axinom</span></span>](http://www.axinom.com/press/ibc-axinom-drm-6/) 
* [<span data-ttu-id="25fb6-123">EZDRM</span><span class="sxs-lookup"><span data-stu-id="25fb6-123">EZDRM</span></span>](http://ezdrm.com/) 
* [<span data-ttu-id="25fb6-124">castLabs</span><span class="sxs-lookup"><span data-stu-id="25fb6-124">castLabs</span></span>](http://castlabs.com/company/partners/azure/) 

<span data-ttu-id="25fb6-125">For more information, see integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="25fb6-125">For more information, see integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="25fb6-126">Media Services supports multiple ways of authorizing users who make key requests.</span><span class="sxs-lookup"><span data-stu-id="25fb6-126">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="25fb6-127">The content key authorization policy can have one or more authorization restrictions, either open or token restrictions.</span><span class="sxs-lookup"><span data-stu-id="25fb6-127">The content key authorization policy can have one or more authorization restrictions, either open or token restrictions.</span></span> <span data-ttu-id="25fb6-128">The token-restricted policy must be accompanied by a token issued by a security token service (STS).</span><span class="sxs-lookup"><span data-stu-id="25fb6-128">The token-restricted policy must be accompanied by a token issued by a security token service (STS).</span></span> <span data-ttu-id="25fb6-129">Media Services supports tokens in the [simple web token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) formats.</span><span class="sxs-lookup"><span data-stu-id="25fb6-129">Media Services supports tokens in the [simple web token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) formats.</span></span> 

<span data-ttu-id="25fb6-130">For more information, see [Configure the content key's authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="25fb6-130">For more information, see [Configure the content key's authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="25fb6-131">To take advantage of dynamic encryption, you need an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span><span class="sxs-lookup"><span data-stu-id="25fb6-131">To take advantage of dynamic encryption, you need an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="25fb6-132">You also need to configure the delivery policies for the asset (described later in this topic).</span><span class="sxs-lookup"><span data-stu-id="25fb6-132">You also need to configure the delivery policies for the asset (described later in this topic).</span></span> <span data-ttu-id="25fb6-133">Then, based on the format specified in the streaming URL, the on-demand streaming server ensures that the stream is delivered in the protocol you selected.</span><span class="sxs-lookup"><span data-stu-id="25fb6-133">Then, based on the format specified in the streaming URL, the on-demand streaming server ensures that the stream is delivered in the protocol you selected.</span></span> <span data-ttu-id="25fb6-134">As a result, you store and pay for the files in only a single storage format.</span><span class="sxs-lookup"><span data-stu-id="25fb6-134">As a result, you store and pay for the files in only a single storage format.</span></span> <span data-ttu-id="25fb6-135">Media Services builds and serves the appropriate HTTP response based on each request from a client.</span><span class="sxs-lookup"><span data-stu-id="25fb6-135">Media Services builds and serves the appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="25fb6-136">This article is useful to developers who work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span><span class="sxs-lookup"><span data-stu-id="25fb6-136">This article is useful to developers who work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="25fb6-137">The article shows you how to configure the PlayReady license delivery service with authorization policies so that only authorized clients can receive PlayReady or Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="25fb6-137">The article shows you how to configure the PlayReady license delivery service with authorization policies so that only authorized clients can receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="25fb6-138">It also shows how to use dynamic encryption with PlayReady or Widevine DRM over DASH.</span><span class="sxs-lookup"><span data-stu-id="25fb6-138">It also shows how to use dynamic encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
>When your Media Services account is created, a default streaming endpoint is added to your account in the "Stopped" state. To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content must be in the "Running" state. 

## <a name="download-the-sample"></a><span data-ttu-id="25fb6-141">Download the sample</span><span class="sxs-lookup"><span data-stu-id="25fb6-141">Download the sample</span></span>
<span data-ttu-id="25fb6-142">You can download the sample described in this article from [Azure samples on GitHub](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="25fb6-142">You can download the sample described in this article from [Azure samples on GitHub](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configure-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="25fb6-143">Configure dynamic common encryption and DRM license delivery services</span><span class="sxs-lookup"><span data-stu-id="25fb6-143">Configure dynamic common encryption and DRM license delivery services</span></span>

<span data-ttu-id="25fb6-144">Perform the following general steps when you protect your assets with PlayReady by using the Media Services license delivery service and also by using dynamic encryption:</span><span class="sxs-lookup"><span data-stu-id="25fb6-144">Perform the following general steps when you protect your assets with PlayReady by using the Media Services license delivery service and also by using dynamic encryption:</span></span>

1. <span data-ttu-id="25fb6-145">Create an asset, and upload files into the asset.</span><span class="sxs-lookup"><span data-stu-id="25fb6-145">Create an asset, and upload files into the asset.</span></span>

2. <span data-ttu-id="25fb6-146">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span><span class="sxs-lookup"><span data-stu-id="25fb6-146">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span></span>

3. <span data-ttu-id="25fb6-147">Create a content key, and associate it with the encoded asset.</span><span class="sxs-lookup"><span data-stu-id="25fb6-147">Create a content key, and associate it with the encoded asset.</span></span> <span data-ttu-id="25fb6-148">In Media Services, the content key contains the asset's encryption key.</span><span class="sxs-lookup"><span data-stu-id="25fb6-148">In Media Services, the content key contains the asset's encryption key.</span></span>

4. <span data-ttu-id="25fb6-149">Configure the content key's authorization policy.</span><span class="sxs-lookup"><span data-stu-id="25fb6-149">Configure the content key's authorization policy.</span></span> <span data-ttu-id="25fb6-150">You must configure the content key authorization policy.</span><span class="sxs-lookup"><span data-stu-id="25fb6-150">You must configure the content key authorization policy.</span></span> <span data-ttu-id="25fb6-151">The client must meet the policy before the content key is delivered to the client.</span><span class="sxs-lookup"><span data-stu-id="25fb6-151">The client must meet the policy before the content key is delivered to the client.</span></span>

    <span data-ttu-id="25fb6-152">When you create the content key authorization policy, you must specify the delivery method (PlayReady or Widevine) and the restrictions (open or token).</span><span class="sxs-lookup"><span data-stu-id="25fb6-152">When you create the content key authorization policy, you must specify the delivery method (PlayReady or Widevine) and the restrictions (open or token).</span></span> <span data-ttu-id="25fb6-153">You also must specify information specific to the key delivery type that defines how the key is delivered to the client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span><span class="sxs-lookup"><span data-stu-id="25fb6-153">You also must specify information specific to the key delivery type that defines how the key is delivered to the client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="25fb6-154">Configure the delivery policy for an asset.</span><span class="sxs-lookup"><span data-stu-id="25fb6-154">Configure the delivery policy for an asset.</span></span> <span data-ttu-id="25fb6-155">The delivery policy configuration includes the delivery protocol (for example, MPEG-DASH, HLS, Smooth Streaming, or all).</span><span class="sxs-lookup"><span data-stu-id="25fb6-155">The delivery policy configuration includes the delivery protocol (for example, MPEG-DASH, HLS, Smooth Streaming, or all).</span></span> <span data-ttu-id="25fb6-156">The configuration also includes the type of dynamic encryption (for example, common encryption) and the PlayReady or Widevine license acquisition URL.</span><span class="sxs-lookup"><span data-stu-id="25fb6-156">The configuration also includes the type of dynamic encryption (for example, common encryption) and the PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="25fb6-157">You can apply a different policy to each protocol on the same asset.</span><span class="sxs-lookup"><span data-stu-id="25fb6-157">You can apply a different policy to each protocol on the same asset.</span></span> <span data-ttu-id="25fb6-158">For example, you can apply PlayReady encryption to Smooth/DASH and an AES envelope to HLS.</span><span class="sxs-lookup"><span data-stu-id="25fb6-158">For example, you can apply PlayReady encryption to Smooth/DASH and an AES envelope to HLS.</span></span> <span data-ttu-id="25fb6-159">Any protocols that aren't defined in a delivery policy (for example, if you add a single policy that specifies only HLS as the protocol) are blocked from streaming.</span><span class="sxs-lookup"><span data-stu-id="25fb6-159">Any protocols that aren't defined in a delivery policy (for example, if you add a single policy that specifies only HLS as the protocol) are blocked from streaming.</span></span> <span data-ttu-id="25fb6-160">The exception is if you have no asset delivery policy defined at all.</span><span class="sxs-lookup"><span data-stu-id="25fb6-160">The exception is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="25fb6-161">Then, all protocols are allowed in the clear.</span><span class="sxs-lookup"><span data-stu-id="25fb6-161">Then, all protocols are allowed in the clear.</span></span>

6. <span data-ttu-id="25fb6-162">Create an OnDemand locator to get a streaming URL.</span><span class="sxs-lookup"><span data-stu-id="25fb6-162">Create an OnDemand locator to get a streaming URL.</span></span>

<span data-ttu-id="25fb6-163">You can find a complete .NET example at the end of the article.</span><span class="sxs-lookup"><span data-stu-id="25fb6-163">You can find a complete .NET example at the end of the article.</span></span>

<span data-ttu-id="25fb6-164">The following image demonstrates the workflow previously described.</span><span class="sxs-lookup"><span data-stu-id="25fb6-164">The following image demonstrates the workflow previously described.</span></span> <span data-ttu-id="25fb6-165">Here, the token is used for authentication.</span><span class="sxs-lookup"><span data-stu-id="25fb6-165">Here, the token is used for authentication.</span></span>

![Protect with PlayReady](media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="25fb6-167">The remainder of this article provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks previously described.</span><span class="sxs-lookup"><span data-stu-id="25fb6-167">The remainder of this article provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks previously described.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="25fb6-168">Current limitations</span><span class="sxs-lookup"><span data-stu-id="25fb6-168">Current limitations</span></span>
<span data-ttu-id="25fb6-169">If you add or update an asset delivery policy, you must delete any associated locator and create a new locator.</span><span class="sxs-lookup"><span data-stu-id="25fb6-169">If you add or update an asset delivery policy, you must delete any associated locator and create a new locator.</span></span>

<span data-ttu-id="25fb6-170">Currently, multiple content keys aren't supported when you encrypt by using Widevine with Media Services.</span><span class="sxs-lookup"><span data-stu-id="25fb6-170">Currently, multiple content keys aren't supported when you encrypt by using Widevine with Media Services.</span></span> 

## <a name="create-an-asset-and-upload-files-into-the-asset"></a><span data-ttu-id="25fb6-171">Create an asset and upload files into the asset</span><span class="sxs-lookup"><span data-stu-id="25fb6-171">Create an asset and upload files into the asset</span></span>
<span data-ttu-id="25fb6-172">To manage, encode, and stream your videos, you must first upload your content into Media Services.</span><span class="sxs-lookup"><span data-stu-id="25fb6-172">To manage, encode, and stream your videos, you must first upload your content into Media Services.</span></span> <span data-ttu-id="25fb6-173">After it's uploaded, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="25fb6-173">After it's uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="25fb6-174">For more information, see [Upload files into a Media Services account](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="25fb6-174">For more information, see [Upload files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-the-asset-that-contains-the-file-to-the-adaptive-bitrate-mp4-set"></a><span data-ttu-id="25fb6-175">Encode the asset that contains the file to the adaptive bitrate MP4 set</span><span class="sxs-lookup"><span data-stu-id="25fb6-175">Encode the asset that contains the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="25fb6-176">With dynamic encryption, you create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span><span class="sxs-lookup"><span data-stu-id="25fb6-176">With dynamic encryption, you create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="25fb6-177">Then, based on the specified format in the manifest and fragment request, the on-demand streaming server ensures that you receive the stream in the protocol you selected.</span><span class="sxs-lookup"><span data-stu-id="25fb6-177">Then, based on the specified format in the manifest and fragment request, the on-demand streaming server ensures that you receive the stream in the protocol you selected.</span></span> <span data-ttu-id="25fb6-178">Then, you store and pay for the files in only a single storage format.</span><span class="sxs-lookup"><span data-stu-id="25fb6-178">Then, you store and pay for the files in only a single storage format.</span></span> <span data-ttu-id="25fb6-179">Media Services builds and serves the appropriate response based on requests from a client.</span><span class="sxs-lookup"><span data-stu-id="25fb6-179">Media Services builds and serves the appropriate response based on requests from a client.</span></span> <span data-ttu-id="25fb6-180">For more information, see [Dynamic packaging overview](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="25fb6-180">For more information, see [Dynamic packaging overview](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="25fb6-181">For instructions on how to encode, see [Encode an asset by using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="25fb6-181">For instructions on how to encode, see [Encode an asset by using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <a id="create_contentkey"></a><span data-ttu-id="25fb6-182">Create a content key and associate it with the encoded asset</span><span class="sxs-lookup"><span data-stu-id="25fb6-182">Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="25fb6-183">In Media Services, the content key contains the key that you want to encrypt an asset with.</span><span class="sxs-lookup"><span data-stu-id="25fb6-183">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="25fb6-184">For more information, see [Create a content key](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="25fb6-184">For more information, see [Create a content key](media-services-dotnet-create-contentkey.md).</span></span>

## <a id="configure_key_auth_policy"></a><span data-ttu-id="25fb6-185">Configure the content key's authorization policy</span><span class="sxs-lookup"><span data-stu-id="25fb6-185">Configure the content key's authorization policy</span></span>
<span data-ttu-id="25fb6-186">Media Services supports multiple ways of authenticating users who make key requests.</span><span class="sxs-lookup"><span data-stu-id="25fb6-186">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="25fb6-187">You must configure the content key authorization policy.</span><span class="sxs-lookup"><span data-stu-id="25fb6-187">You must configure the content key authorization policy.</span></span> <span data-ttu-id="25fb6-188">The client (player) must meet the policy before the key is delivered to the client.</span><span class="sxs-lookup"><span data-stu-id="25fb6-188">The client (player) must meet the policy before the key is delivered to the client.</span></span> <span data-ttu-id="25fb6-189">The content key authorization policy can have one or more authorization restrictions, either open or token restrictions.</span><span class="sxs-lookup"><span data-stu-id="25fb6-189">The content key authorization policy can have one or more authorization restrictions, either open or token restrictions.</span></span>

<span data-ttu-id="25fb6-190">For more information, see [Configure a content key authorization policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span><span class="sxs-lookup"><span data-stu-id="25fb6-190">For more information, see [Configure a content key authorization policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <a id="configure_asset_delivery_policy"></a><span data-ttu-id="25fb6-191">Configure an asset delivery policy</span><span class="sxs-lookup"><span data-stu-id="25fb6-191">Configure an asset delivery policy</span></span>
<span data-ttu-id="25fb6-192">Configure the delivery policy for your asset.</span><span class="sxs-lookup"><span data-stu-id="25fb6-192">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="25fb6-193">Some things that the asset delivery policy configuration includes are:</span><span class="sxs-lookup"><span data-stu-id="25fb6-193">Some things that the asset delivery policy configuration includes are:</span></span>

* <span data-ttu-id="25fb6-194">The DRM license acquisition URL.</span><span class="sxs-lookup"><span data-stu-id="25fb6-194">The DRM license acquisition URL.</span></span>
* <span data-ttu-id="25fb6-195">The asset delivery protocol (for example, MPEG-DASH, HLS, Smooth Streaming, or all).</span><span class="sxs-lookup"><span data-stu-id="25fb6-195">The asset delivery protocol (for example, MPEG-DASH, HLS, Smooth Streaming, or all).</span></span>
* <span data-ttu-id="25fb6-196">The type of dynamic encryption (in this case, common encryption).</span><span class="sxs-lookup"><span data-stu-id="25fb6-196">The type of dynamic encryption (in this case, common encryption).</span></span>

<span data-ttu-id="25fb6-197">For more information, see [Configure an asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="25fb6-197">For more information, see [Configure an asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

## <a id="create_locator"></a><span data-ttu-id="25fb6-198">Create an OnDemand streaming locator to get a streaming URL</span><span class="sxs-lookup"><span data-stu-id="25fb6-198">Create an OnDemand streaming locator to get a streaming URL</span></span>
<span data-ttu-id="25fb6-199">You need to provide your user with the streaming URL for Smooth Streaming, DASH, or HLS.</span><span class="sxs-lookup"><span data-stu-id="25fb6-199">You need to provide your user with the streaming URL for Smooth Streaming, DASH, or HLS.</span></span>

> [!NOTE]
> If you add or update your asset's delivery policy, you must delete any existing locator and create a new locator.
>
>

<span data-ttu-id="25fb6-201">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="25fb6-201">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="25fb6-202">Get a test token</span><span class="sxs-lookup"><span data-stu-id="25fb6-202">Get a test token</span></span>
<span data-ttu-id="25fb6-203">Get a test token based on the token restriction that was used for the key authorization policy.</span><span class="sxs-lookup"><span data-stu-id="25fb6-203">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

```csharp
    // Deserializes a string containing an XML representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word "Bearer" in front,
    //so you have to add it in front of the token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
```

<span data-ttu-id="25fb6-204">You can use the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span><span class="sxs-lookup"><span data-stu-id="25fb6-204">You can use the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="25fb6-205">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="25fb6-205">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="25fb6-206">Set up your development environment, and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="25fb6-206">Set up your development environment, and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

2. <span data-ttu-id="25fb6-207">Add the following elements to **appSettings** defined in your app.config file:</span><span class="sxs-lookup"><span data-stu-id="25fb6-207">Add the following elements to **appSettings** defined in your app.config file:</span></span>

```xml
        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>
```

## <a name="example"></a><span data-ttu-id="25fb6-208">Example</span><span class="sxs-lookup"><span data-stu-id="25fb6-208">Example</span></span>

<span data-ttu-id="25fb6-209">The following sample demonstrates functionality that was introduced in the Media Services SDK for .NET version 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="25fb6-209">The following sample demonstrates functionality that was introduced in the Media Services SDK for .NET version 3.5.2.</span></span> <span data-ttu-id="25fb6-210">(Specifically, it includes the ability to define a Widevine license template and request a Widevine license from Media Services.)</span><span class="sxs-lookup"><span data-stu-id="25fb6-210">(Specifically, it includes the ability to define a Widevine license template and request a Widevine license from Media Services.)</span></span>

<span data-ttu-id="25fb6-211">Overwrite the code in your Program.cs file with the code shown in this section.</span><span class="sxs-lookup"><span data-stu-id="25fb6-211">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
>There is a limit of 1 million policies for different Media Services policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). If you always use the same days/access permissions, use the same policy ID. An example is policies for locators that are intended to remain in place for a long time (non-upload policies). 

<span data-ttu-id="25fb6-215">For more information, see [Manage assets and related entities with the Media Services .NET SDK](media-services-dotnet-manage-entities.md#limit-access-policies).</span><span class="sxs-lookup"><span data-stu-id="25fb6-215">For more information, see [Manage assets and related entities with the Media Services .NET SDK](media-services-dotnet-manage-entities.md#limit-access-policies).</span></span>

<span data-ttu-id="25fb6-216">Make sure to update variables to point to folders where your input files are located.</span><span class="sxs-lookup"><span data-stu-id="25fb6-216">Make sure to update variables to point to folders where your input files are located.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Configuration;
using System.IO;
using System.Linq;
using System.Threading;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
using Newtonsoft.Json;

namespace DynamicEncryptionWithDRM
{
    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AMSAADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["AMSRESTAPIEndpoint"];
        private static readonly string _AMSClientId =
            ConfigurationManager.AppSettings["AMSClientId"];
        private static readonly string _AMSClientSecret =
            ConfigurationManager.AppSettings["AMSClientSecret"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            AzureAdTokenCredentials tokenCredentials =
                new AzureAdTokenCredentials(_AADTenantDomain,
                    new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                    AzureEnvironments.AzureCloudEnvironment);

            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
                tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
                AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
                // Deserializes a string containing an XML representation of a TokenRestrictionTemplate
                // back into a TokenRestrictionTemplate class instance.
                TokenRestrictionTemplate tokenTemplate =
                    TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

                // Generate a test token based on the data in the given TokenRestrictionTemplate.
                // Note that you need to pass the key ID GUID because 
                // TokenClaim.ContentKeyIdentifierClaim was specified during the creation of TokenRestrictionTemplate.
                Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
                string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                            DateTime.UtcNow.AddDays(365));
                Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
                Console.WriteLine();
            }

            // You can use the http://amsplayer.azurewebsites.net/azuremediaplayer.html player to test streams.
            // Note that DASH works on Internet Explorer 11 (via PlayReady), Edge (via PlayReady), and Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} to {1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate the key with the asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {

            // Create ContentKeyAuthorizationPolicy with open restrictions
            // and create an authorization policy.         

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Open",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                    Requirements = null
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate the content key authorization policy with the content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate the content key authorization policy with the content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // The following code configures the PlayReady license template by using .NET classes
            // and returns the XML string.

            //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user.
            //It contains a field for a custom data string between the license server and the application
            //(which might be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // The PlayReadyLicenseTemplate class represents a license template you can use to create PlayReady licenses
            // to be returned to end users.
            //It contains the data on the content key in the license and any rights or restrictions to be
            //enforced by the PlayReady DRM runtime when you use the content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether the license is persistent (saved in persistent storage on the client)
            //or nonpersistent (held in memory only while the player uses the license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use the license or not.  
            // If true, the MinimumSecurityLevel property of the license
            // is set to 150. If false (the default), the MinimumSecurityLevel property of the license is set to 2,000.
            licenseTemplate.AllowTestDevices = true;

            // You also can configure the PlayRight in the PlayReady license by using the PlayReadyPlayRight class.
            // It grants the user the ability to play back the content subject to the zero or more restrictions
            // configured in the license and on the PlayRight itself (for playback-specific policy).
            // Much of the policy on the PlayRight has to do with output restrictions,
            // which control the types of outputs that the content can be played over and
            // any restrictions that must be put in place when you use a given output.
            // For example, if DigitalVideoOnlyContentRestriction is enabled,
            // the DRM runtime allows the video to be displayed only over digital outputs
            //(analog video outputs aren't allowed to pass the content).

            //IMPORTANT: These types of restrictions can be very powerful but also can affect the consumer experience.
            // If output protections are too restrictive, 
            // content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
                allowed_track_types = AllowedTrackTypes.SD_HD,
                content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
                policy_overrides = new
                {
                    can_play = true,
                    can_persist = true,
                    can_renew = false
                }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get the PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches the KID to the URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // WidevineBaseLicenseAcquisitionUrl (used in the following) also tells dynamic encryption
            // to append /? KID =< keyId > to the end of the URL when you create the manifest.
            // As a result, the Widevine license acquisition URL has the KID appended twice,
            // so you need to remove the KID in the URL when you call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case, we specify only the DASH streaming protocol in the delivery policy.
            // All other protocols are blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy to the asset.
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the 
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day read-only access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
                rng.GetBytes(returnValue);
            }

            return returnValue;
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="25fb6-217">Next steps</span><span class="sxs-lookup"><span data-stu-id="25fb6-217">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="25fb6-218">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="25fb6-218">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="25fb6-219">See also</span><span class="sxs-lookup"><span data-stu-id="25fb6-219">See also</span></span>
* [<span data-ttu-id="25fb6-220">Use the CENC with multi-DRM and access control</span><span class="sxs-lookup"><span data-stu-id="25fb6-220">Use the CENC with multi-DRM and access control</span></span>](media-services-cenc-with-multidrm-access-control.md)
* [<span data-ttu-id="25fb6-221">Configure Widevine packaging with Media Services</span><span class="sxs-lookup"><span data-stu-id="25fb6-221">Configure Widevine packaging with Media Services</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)
* [<span data-ttu-id="25fb6-222">Announcing Google Widevine license delivery services in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="25fb6-222">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
