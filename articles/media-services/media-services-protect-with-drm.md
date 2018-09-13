---
title: Using PlayReady and/or Widevine dynamic common encryption | Microsoft Docs
description: Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and Http-Live-Streaming (HLS) streams protected with Microsoft PlayReady DRM. It also enables you to delivery DASH encrypted with Widevine DRM. This topic shows how to dynamically encrypt with PlayReady and Widevine DRM.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/16/2017
ms.author: juliako
ms.openlocfilehash: 4c52710319d8fd7a79236aac0d06e8ebdaa7e7ad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554772"
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="17fed-105">Using PlayReady and/or Widevine dynamic common encryption</span><span class="sxs-lookup"><span data-stu-id="17fed-105">Using PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-drm.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

<span data-ttu-id="17fed-109">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="17fed-109">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="17fed-110">It also enables you to deliver encrypted DASH streams with Widevine DRM licenses.</span><span class="sxs-lookup"><span data-stu-id="17fed-110">It also enables you to deliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="17fed-111">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span><span class="sxs-lookup"><span data-stu-id="17fed-111">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="17fed-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with the version 3.5.1) or REST API to configure your AssetDeliveryConfiguration to use Widevine.</span><span class="sxs-lookup"><span data-stu-id="17fed-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with the version 3.5.1) or REST API to configure your AssetDeliveryConfiguration to use Widevine.</span></span>

<span data-ttu-id="17fed-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span><span class="sxs-lookup"><span data-stu-id="17fed-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="17fed-114">Media Services also provides APIs that let you configure the rights and restrictions that you want for the PlayReady or Widevine DRM runtime to enforce when a user plays back protected content.</span><span class="sxs-lookup"><span data-stu-id="17fed-114">Media Services also provides APIs that let you configure the rights and restrictions that you want for the PlayReady or Widevine DRM runtime to enforce when a user plays back protected content.</span></span> <span data-ttu-id="17fed-115">When a user requests a DRM protected content, the player application will request a license from the AMS license service.</span><span class="sxs-lookup"><span data-stu-id="17fed-115">When a user requests a DRM protected content, the player application will request a license from the AMS license service.</span></span> <span data-ttu-id="17fed-116">The AMS license service will issue a license to the player if it is authorized.</span><span class="sxs-lookup"><span data-stu-id="17fed-116">The AMS license service will issue a license to the player if it is authorized.</span></span> <span data-ttu-id="17fed-117">A PlayReady or Widevine license contains the decryption key that can be used by the client player to decrypt and stream the content.</span><span class="sxs-lookup"><span data-stu-id="17fed-117">A PlayReady or Widevine license contains the decryption key that can be used by the client player to decrypt and stream the content.</span></span>

<span data-ttu-id="17fed-118">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="17fed-118">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span> <span data-ttu-id="17fed-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="17fed-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="17fed-120">Media Services supports multiple ways of authorizing users who make key requests.</span><span class="sxs-lookup"><span data-stu-id="17fed-120">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="17fed-121">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span><span class="sxs-lookup"><span data-stu-id="17fed-121">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="17fed-122">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="17fed-122">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="17fed-123">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span><span class="sxs-lookup"><span data-stu-id="17fed-123">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="17fed-124">For more information, see Configure the content key’s authorization policy.</span><span class="sxs-lookup"><span data-stu-id="17fed-124">For more information, see Configure the content key’s authorization policy.</span></span>

<span data-ttu-id="17fed-125">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span><span class="sxs-lookup"><span data-stu-id="17fed-125">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="17fed-126">You also need to configure the delivery policies for the asset (described later in this topic).</span><span class="sxs-lookup"><span data-stu-id="17fed-126">You also need to configure the delivery policies for the asset (described later in this topic).</span></span> <span data-ttu-id="17fed-127">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span><span class="sxs-lookup"><span data-stu-id="17fed-127">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span></span> <span data-ttu-id="17fed-128">As a result, you only need to store and pay for the files in a single storage format and Media Services will build and serve the appropriate HTTP response based on each request from a client.</span><span class="sxs-lookup"><span data-stu-id="17fed-128">As a result, you only need to store and pay for the files in a single storage format and Media Services will build and serve the appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="17fed-129">This topic would be useful to developers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span><span class="sxs-lookup"><span data-stu-id="17fed-129">This topic would be useful to developers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="17fed-130">The topic shows you how to configure the PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="17fed-130">The topic shows you how to configure the PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="17fed-131">It also shows how to use dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span><span class="sxs-lookup"><span data-stu-id="17fed-131">It also shows how to use dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
>When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state. To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state. 

## <a name="download-sample"></a><span data-ttu-id="17fed-134">Download sample</span><span class="sxs-lookup"><span data-stu-id="17fed-134">Download sample</span></span>
<span data-ttu-id="17fed-135">You can download the sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="17fed-135">You can download the sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="17fed-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span><span class="sxs-lookup"><span data-stu-id="17fed-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span></span>

<span data-ttu-id="17fed-137">The following are general steps that you would need to perform when protecting your assets with PlayReady, using the Media Services license delivery service, and also using dynamic encryption.</span><span class="sxs-lookup"><span data-stu-id="17fed-137">The following are general steps that you would need to perform when protecting your assets with PlayReady, using the Media Services license delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="17fed-138">Create an asset and upload files into the asset.</span><span class="sxs-lookup"><span data-stu-id="17fed-138">Create an asset and upload files into the asset.</span></span>
2. <span data-ttu-id="17fed-139">Encode the asset containing the file to the adaptive bitrate MP4 set.</span><span class="sxs-lookup"><span data-stu-id="17fed-139">Encode the asset containing the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="17fed-140">Create a content key and associate it with the encoded asset.</span><span class="sxs-lookup"><span data-stu-id="17fed-140">Create a content key and associate it with the encoded asset.</span></span> <span data-ttu-id="17fed-141">In Media Services, the content key contains the asset’s encryption key.</span><span class="sxs-lookup"><span data-stu-id="17fed-141">In Media Services, the content key contains the asset’s encryption key.</span></span>
4. <span data-ttu-id="17fed-142">Configure the content key’s authorization policy.</span><span class="sxs-lookup"><span data-stu-id="17fed-142">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="17fed-143">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span><span class="sxs-lookup"><span data-stu-id="17fed-143">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span></span>

    <span data-ttu-id="17fed-144">When creating the content key authorization policy, you need to specify the following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific to the key delivery type that defines how the key is delivered to the client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span><span class="sxs-lookup"><span data-stu-id="17fed-144">When creating the content key authorization policy, you need to specify the following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific to the key delivery type that defines how the key is delivered to the client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="17fed-145">Configure the delivery policy for an asset.</span><span class="sxs-lookup"><span data-stu-id="17fed-145">Configure the delivery policy for an asset.</span></span> <span data-ttu-id="17fed-146">The delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span><span class="sxs-lookup"><span data-stu-id="17fed-146">The delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="17fed-147">You could apply different policy to each protocol on the same asset.</span><span class="sxs-lookup"><span data-stu-id="17fed-147">You could apply different policy to each protocol on the same asset.</span></span> <span data-ttu-id="17fed-148">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span><span class="sxs-lookup"><span data-stu-id="17fed-148">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span></span> <span data-ttu-id="17fed-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span><span class="sxs-lookup"><span data-stu-id="17fed-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="17fed-150">The exception to this is if you have no asset delivery policy defined at all.</span><span class="sxs-lookup"><span data-stu-id="17fed-150">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="17fed-151">Then, all protocols will be allowed in the clear.</span><span class="sxs-lookup"><span data-stu-id="17fed-151">Then, all protocols will be allowed in the clear.</span></span>

6. <span data-ttu-id="17fed-152">Create an OnDemand locator in order to get a streaming URL.</span><span class="sxs-lookup"><span data-stu-id="17fed-152">Create an OnDemand locator in order to get a streaming URL.</span></span>

<span data-ttu-id="17fed-153">You will find a complete .NET example at the end of the topic.</span><span class="sxs-lookup"><span data-stu-id="17fed-153">You will find a complete .NET example at the end of the topic.</span></span>

<span data-ttu-id="17fed-154">The following image demonstrates the workflow described above.</span><span class="sxs-lookup"><span data-stu-id="17fed-154">The following image demonstrates the workflow described above.</span></span> <span data-ttu-id="17fed-155">Here the token is used for authentication.</span><span class="sxs-lookup"><span data-stu-id="17fed-155">Here the token is used for authentication.</span></span>

![Protect with PlayReady](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="17fed-157">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span><span class="sxs-lookup"><span data-stu-id="17fed-157">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="17fed-158">Current limitations</span><span class="sxs-lookup"><span data-stu-id="17fed-158">Current limitations</span></span>
<span data-ttu-id="17fed-159">If you add or update an asset delivery policy, you must delete the associated locator (if any) and create a new locator.</span><span class="sxs-lookup"><span data-stu-id="17fed-159">If you add or update an asset delivery policy, you must delete the associated locator (if any) and create a new locator.</span></span>

<span data-ttu-id="17fed-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span><span class="sxs-lookup"><span data-stu-id="17fed-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span></span>

## <a name="create-an-asset-and-upload-files-into-the-asset"></a><span data-ttu-id="17fed-161">Create an asset and upload files into the asset</span><span class="sxs-lookup"><span data-stu-id="17fed-161">Create an asset and upload files into the asset</span></span>
<span data-ttu-id="17fed-162">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="17fed-162">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="17fed-163">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="17fed-163">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="17fed-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="17fed-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-the-asset-containing-the-file-to-the-adaptive-bitrate-mp4-set"></a><span data-ttu-id="17fed-165">Encode the asset containing the file to the adaptive bitrate MP4 set</span><span class="sxs-lookup"><span data-stu-id="17fed-165">Encode the asset containing the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="17fed-166">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span><span class="sxs-lookup"><span data-stu-id="17fed-166">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="17fed-167">Then, based on the specified format in the manifest and fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span><span class="sxs-lookup"><span data-stu-id="17fed-167">Then, based on the specified format in the manifest and fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="17fed-168">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span><span class="sxs-lookup"><span data-stu-id="17fed-168">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span> <span data-ttu-id="17fed-169">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span><span class="sxs-lookup"><span data-stu-id="17fed-169">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

<span data-ttu-id="17fed-170">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="17fed-170">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <a id="create_contentkey"></a><span data-ttu-id="17fed-171">Create a content key and associate it with the encoded asset</span><span class="sxs-lookup"><span data-stu-id="17fed-171">Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="17fed-172">In Media Services, the content key contains the key that you want to encrypt an asset with.</span><span class="sxs-lookup"><span data-stu-id="17fed-172">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="17fed-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="17fed-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <a id="configure_key_auth_policy"></a><span data-ttu-id="17fed-174">Configure the content key’s authorization policy</span><span class="sxs-lookup"><span data-stu-id="17fed-174">Configure the content key’s authorization policy</span></span>
<span data-ttu-id="17fed-175">Media Services supports multiple ways of authenticating users who make key requests.</span><span class="sxs-lookup"><span data-stu-id="17fed-175">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="17fed-176">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span><span class="sxs-lookup"><span data-stu-id="17fed-176">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span></span> <span data-ttu-id="17fed-177">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span><span class="sxs-lookup"><span data-stu-id="17fed-177">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span>

<span data-ttu-id="17fed-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span><span class="sxs-lookup"><span data-stu-id="17fed-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <a id="configure_asset_delivery_policy"></a><span data-ttu-id="17fed-179">Configure asset delivery policy</span><span class="sxs-lookup"><span data-stu-id="17fed-179">Configure asset delivery policy</span></span>
<span data-ttu-id="17fed-180">Configure the delivery policy for your asset.</span><span class="sxs-lookup"><span data-stu-id="17fed-180">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="17fed-181">Some things that the asset delivery policy configuration includes:</span><span class="sxs-lookup"><span data-stu-id="17fed-181">Some things that the asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="17fed-182">The DRM license acquisition URL.</span><span class="sxs-lookup"><span data-stu-id="17fed-182">The DRM license acquisition URL.</span></span>
* <span data-ttu-id="17fed-183">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span><span class="sxs-lookup"><span data-stu-id="17fed-183">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="17fed-184">The type of dynamic encryption (in this case, Common Encryption).</span><span class="sxs-lookup"><span data-stu-id="17fed-184">The type of dynamic encryption (in this case, Common Encryption).</span></span>

<span data-ttu-id="17fed-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="17fed-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a id="create_locator"></a><span data-ttu-id="17fed-186">Create an OnDemand streaming locator in order to get a streaming URL</span><span class="sxs-lookup"><span data-stu-id="17fed-186">Create an OnDemand streaming locator in order to get a streaming URL</span></span>
<span data-ttu-id="17fed-187">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span><span class="sxs-lookup"><span data-stu-id="17fed-187">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.
>
>

<span data-ttu-id="17fed-189">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="17fed-189">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="17fed-190">Get a test token</span><span class="sxs-lookup"><span data-stu-id="17fed-190">Get a test token</span></span>
<span data-ttu-id="17fed-191">Get a test token based on the token restriction that was used for the key authorization policy.</span><span class="sxs-lookup"><span data-stu-id="17fed-191">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);


<span data-ttu-id="17fed-192">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span><span class="sxs-lookup"><span data-stu-id="17fed-192">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <a id="example"></a><span data-ttu-id="17fed-193">Example</span><span class="sxs-lookup"><span data-stu-id="17fed-193">Example</span></span>
<span data-ttu-id="17fed-194">The following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, the ability to define a Widevine license template and request a Widevine license from Azure Media Services).</span><span class="sxs-lookup"><span data-stu-id="17fed-194">The following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, the ability to define a Widevine license template and request a Widevine license from Azure Media Services).</span></span> <span data-ttu-id="17fed-195">The following Nuget package command was used to install the package:</span><span class="sxs-lookup"><span data-stu-id="17fed-195">The following Nuget package command was used to install the package:</span></span>

    PM> Install-Package windowsazure.mediaservices -Version 3.5.2


1. <span data-ttu-id="17fed-196">Create a new Console project.</span><span class="sxs-lookup"><span data-stu-id="17fed-196">Create a new Console project.</span></span>
2. <span data-ttu-id="17fed-197">Use NuGet to install and add Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="17fed-197">Use NuGet to install and add Azure Media Services .NET SDK.</span></span>
3. <span data-ttu-id="17fed-198">Add additional references: System.Configuration.</span><span class="sxs-lookup"><span data-stu-id="17fed-198">Add additional references: System.Configuration.</span></span>
4. <span data-ttu-id="17fed-199">Add config file that contains the account name and key information:</span><span class="sxs-lookup"><span data-stu-id="17fed-199">Add config file that contains the account name and key information:</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
            <startup>
                <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
            </startup>
              <appSettings>

                <add key="MediaServicesAccountName" value="AccountName"/>
                <add key="MediaServicesAccountKey" value="AccountKey"/>

                <add key="Issuer" value="http://testacs.com"/>
                <add key="Audience" value="urn:test"/>
              </appSettings>
        </configuration>
7. <span data-ttu-id="17fed-200">Overwrite the code in your Program.cs file with the code shown in this section.</span><span class="sxs-lookup"><span data-stu-id="17fed-200">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

    >[!NOTE]
    >There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies). For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.

    <span data-ttu-id="17fed-204">Make sure to update variables to point to folders where your input files are located.</span><span class="sxs-lookup"><span data-stu-id="17fed-204">Make sure to update variables to point to folders where your input files are located.</span></span>

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
                private static readonly string _mediaServicesAccountName =
                    ConfigurationManager.AppSettings["MediaServicesAccountName"];
                private static readonly string _mediaServicesAccountKey =
                    ConfigurationManager.AppSettings["MediaServicesAccountKey"];

                private static readonly Uri _sampleIssuer =
                    new Uri(ConfigurationManager.AppSettings["Issuer"]);
                private static readonly Uri _sampleAudience =
                    new Uri(ConfigurationManager.AppSettings["Audience"]);

                // Field for service context.
                private static CloudMediaContext _context = null;
                private static MediaServicesCredentials _cachedCredentials = null;

                private static readonly string _mediaFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _singleMP4File =
                    Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    // Create and cache the Media Services credentials in a static class variable.
                    _cachedCredentials = new MediaServicesCredentials(
                                    _mediaServicesAccountName,
                                    _mediaServicesAccountKey);
                    // Used the cached credentials to create CloudMediaContext.
                    _context = new CloudMediaContext(_cachedCredentials);

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
                        // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
                        // back into a TokenRestrictionTemplate class instance.
                        TokenRestrictionTemplate tokenTemplate =
                            TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

                        // Generate a test token based on the the data in the given TokenRestrictionTemplate.
                        // Note, you need to pass the key id Guid because we specified
                        // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
                        Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
                        string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                                                                DateTime.UtcNow.AddDays(365));
                        Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
                        Console.WriteLine();
                    }

                    // You can use the http://amsplayer.azurewebsites.net/azuremediaplayer.html player to test streams.
                    // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

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
                    encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset),     AssetCreationOptions.StorageEncrypted);

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

                    // Create ContentKeyAuthorizationPolicy with Open restrictions
                    // and create authorization policy          

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

                    // Associate the content key authorization policy with the content key
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
                    // The following code configures PlayReady License Template using .NET classes
                    // and returns the XML string.

                    //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user.
                    //It contains a field for a custom data string between the license server and the application
                    //(may be useful for custom app logic) as well as a list of one or more license templates.
                    PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

                    // The PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
                    // to be returned to the end users.
                    //It contains the data on the content key in the license and any rights or restrictions to be
                    //enforced by the PlayReady DRM runtime when using the content key.
                    PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
                    //Configure whether the license is persistent (saved in persistent storage on the client)
                    //or non-persistent (only held in memory while the player is using the license).  
                    licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

                    // AllowTestDevices controls whether test devices can use the license or not.  
                    // If true, the MinimumSecurityLevel property of the license
                    // is set to 150.  If false (the default), the MinimumSecurityLevel property of the license is set to 2000.
                    licenseTemplate.AllowTestDevices = true;

                    // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class.
                    // It grants the user the ability to playback the content subject to the zero or more restrictions
                    // configured in the license and on the PlayRight itself (for playback specific policy).
                    // Much of the policy on the PlayRight has to do with output restrictions
                    // which control the types of outputs that the content can be played over and
                    // any restrictions that must be put in place when using a given output.
                    // For example, if the DigitalVideoOnlyContentRestriction is enabled,
                    //then the DRM runtime will only allow the video to be displayed over digital outputs
                    //(analog video outputs won’t be allowed to pass the content).

                    //IMPORTANT: These types of restrictions can be very powerful but can also affect the consumer experience.
                    // If the output protections are configured too restrictive,
                    // the content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

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
                    // The WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
                    // to append /? KID =< keyId > to the end of the url when creating the manifest.
                    // As a result Widevine license acquisition URL will have KID appended twice,
                    // so we need to remove the KID that in the URL when we call GetKeyDeliveryUrl.

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

                    // In this case we only specify Dash streaming protocol in the delivery policy,
                    // All other protocols will be blocked from streaming.
                    var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                            "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicCommonEncryption,
                        AssetDeliveryProtocol.Dash,
                        assetDeliveryPolicyConfiguration);


                    // Add AssetDelivery Policy to the asset
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

                    // Create a 30-day readonly access policy.
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


## <a name="next-step"></a><span data-ttu-id="17fed-205">Next step</span><span class="sxs-lookup"><span data-stu-id="17fed-205">Next step</span></span>
<span data-ttu-id="17fed-206">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="17fed-206">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="17fed-207">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="17fed-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="17fed-208">See also</span><span class="sxs-lookup"><span data-stu-id="17fed-208">See also</span></span>
[<span data-ttu-id="17fed-209">CENC with Multi-DRM and Access Control</span><span class="sxs-lookup"><span data-stu-id="17fed-209">CENC with Multi-DRM and Access Control</span></span>](media-services-cenc-with-multidrm-access-control.md)

[<span data-ttu-id="17fed-210">Configure Widevine packaging with AMS</span><span class="sxs-lookup"><span data-stu-id="17fed-210">Configure Widevine packaging with AMS</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[<span data-ttu-id="17fed-211">Announcing Google Widevine license delivery services in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="17fed-211">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)

