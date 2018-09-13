---
title: Use AES-128 dynamic encryption and the key delivery service | Microsoft Docs
description: Deliver your content encrypted with AES 128-bit encryption keys by using Microsoft Azure Media Services. Media Services also provides the key delivery service that delivers encryption keys to authorized users. This topic shows how to dynamically encrypt with AES-128 and use the key delivery service.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 335c080519df48709ebc5c1c3c44d9386d16b790
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965861"
---
# <a name="use-aes-128-dynamic-encryption-and-the-key-delivery-service"></a><span data-ttu-id="c69e6-105">Use AES-128 dynamic encryption and the key delivery service</span><span class="sxs-lookup"><span data-stu-id="c69e6-105">Use AES-128 dynamic encryption and the key delivery service</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-aes128.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 

> [!NOTE]
> To get the latest version of the Java SDK and get started developing with Java, see [Get started with the Java client SDK for Azure Media Services](https://docs.microsoft.com/azure/media-services/media-services-java-how-to-use). <br/>
> To download the latest PHP SDK for Media Services, look for version 0.5.7 of the Microsoft/WindowsAzure package in the [Packagist repository](https://packagist.org/packages/microsoft/windowsazure#v0.5.7).  

## <a name="overview"></a><span data-ttu-id="c69e6-111">Overview</span><span class="sxs-lookup"><span data-stu-id="c69e6-111">Overview</span></span>
> [!NOTE]
> For information on how to encrypt content with the Advanced Encryption Standard (AES) for delivery to Safari on macOS, see [this blog post](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).
> For an overview of how to protect your media content with AES encryption, see [this video](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption).
> 
> 

 <span data-ttu-id="c69e6-114">You can use Media Services to deliver HTTP Live Streaming (HLS) and Smooth Streaming encrypted with the AES by using 128-bit encryption keys.</span><span class="sxs-lookup"><span data-stu-id="c69e6-114">You can use Media Services to deliver HTTP Live Streaming (HLS) and Smooth Streaming encrypted with the AES by using 128-bit encryption keys.</span></span> <span data-ttu-id="c69e6-115">Media Services also provides the key delivery service that delivers encryption keys to authorized users.</span><span class="sxs-lookup"><span data-stu-id="c69e6-115">Media Services also provides the key delivery service that delivers encryption keys to authorized users.</span></span> <span data-ttu-id="c69e6-116">If you want Media Services to encrypt an asset, you associate an encryption key with the asset and also configure authorization policies for the key.</span><span class="sxs-lookup"><span data-stu-id="c69e6-116">If you want Media Services to encrypt an asset, you associate an encryption key with the asset and also configure authorization policies for the key.</span></span> <span data-ttu-id="c69e6-117">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content by using AES encryption.</span><span class="sxs-lookup"><span data-stu-id="c69e6-117">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content by using AES encryption.</span></span> <span data-ttu-id="c69e6-118">To decrypt the stream, the player requests the key from the key delivery service.</span><span class="sxs-lookup"><span data-stu-id="c69e6-118">To decrypt the stream, the player requests the key from the key delivery service.</span></span> <span data-ttu-id="c69e6-119">To determine whether the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span><span class="sxs-lookup"><span data-stu-id="c69e6-119">To determine whether the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="c69e6-120">Media Services supports multiple ways of authenticating users who make key requests.</span><span class="sxs-lookup"><span data-stu-id="c69e6-120">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="c69e6-121">The content key authorization policy can have one or more authorization restrictions, either open or token restrictions.</span><span class="sxs-lookup"><span data-stu-id="c69e6-121">The content key authorization policy can have one or more authorization restrictions, either open or token restrictions.</span></span> <span data-ttu-id="c69e6-122">The token-restricted policy must be accompanied by a token issued by a security token service (STS).</span><span class="sxs-lookup"><span data-stu-id="c69e6-122">The token-restricted policy must be accompanied by a token issued by a security token service (STS).</span></span> <span data-ttu-id="c69e6-123">Media Services supports tokens in the [simple web token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) formats.</span><span class="sxs-lookup"><span data-stu-id="c69e6-123">Media Services supports tokens in the [simple web token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) formats.</span></span> <span data-ttu-id="c69e6-124">For more information, see [Configure the content key's authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="c69e6-124">For more information, see [Configure the content key's authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="c69e6-125">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span><span class="sxs-lookup"><span data-stu-id="c69e6-125">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="c69e6-126">You also need to configure the delivery policy for the asset (described later in this article).</span><span class="sxs-lookup"><span data-stu-id="c69e6-126">You also need to configure the delivery policy for the asset (described later in this article).</span></span> <span data-ttu-id="c69e6-127">Then, based on the format specified in the streaming URL, the on-demand streaming server ensures that the stream is delivered in the protocol you selected.</span><span class="sxs-lookup"><span data-stu-id="c69e6-127">Then, based on the format specified in the streaming URL, the on-demand streaming server ensures that the stream is delivered in the protocol you selected.</span></span> <span data-ttu-id="c69e6-128">As a result, you need to store and pay only for the files in single storage format.</span><span class="sxs-lookup"><span data-stu-id="c69e6-128">As a result, you need to store and pay only for the files in single storage format.</span></span> <span data-ttu-id="c69e6-129">Media Services builds and serves the appropriate response based on requests from a client.</span><span class="sxs-lookup"><span data-stu-id="c69e6-129">Media Services builds and serves the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="c69e6-130">This article is useful to developers who work on applications that deliver protected media.</span><span class="sxs-lookup"><span data-stu-id="c69e6-130">This article is useful to developers who work on applications that deliver protected media.</span></span> <span data-ttu-id="c69e6-131">The article shows you how to configure the key delivery service with authorization policies so that only authorized clients can receive encryption keys.</span><span class="sxs-lookup"><span data-stu-id="c69e6-131">The article shows you how to configure the key delivery service with authorization policies so that only authorized clients can receive encryption keys.</span></span> <span data-ttu-id="c69e6-132">It also shows how to use dynamic encryption.</span><span class="sxs-lookup"><span data-stu-id="c69e6-132">It also shows how to use dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="c69e6-133">AES-128 dynamic encryption and key delivery service workflow</span><span class="sxs-lookup"><span data-stu-id="c69e6-133">AES-128 dynamic encryption and key delivery service workflow</span></span>

<span data-ttu-id="c69e6-134">Perform the following general steps when you encrypt your assets with AES by using the Media Services key delivery service and also by using dynamic encryption:</span><span class="sxs-lookup"><span data-stu-id="c69e6-134">Perform the following general steps when you encrypt your assets with AES by using the Media Services key delivery service and also by using dynamic encryption:</span></span>

1. <span data-ttu-id="c69e6-135">[Create an asset, and upload files into the asset](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="c69e6-135">[Create an asset, and upload files into the asset](media-services-protect-with-aes128.md#create_asset).</span></span>

2. <span data-ttu-id="c69e6-136">[Encode the asset that contains the file to the adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="c69e6-136">[Encode the asset that contains the file to the adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>

3. <span data-ttu-id="c69e6-137">[Create a content key, and associate it with the encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="c69e6-137">[Create a content key, and associate it with the encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="c69e6-138">In Media Services, the content key contains the asset's encryption key.</span><span class="sxs-lookup"><span data-stu-id="c69e6-138">In Media Services, the content key contains the asset's encryption key.</span></span>

4. <span data-ttu-id="c69e6-139">[Configure the content key's authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="c69e6-139">[Configure the content key's authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="c69e6-140">You must configure the content key authorization policy.</span><span class="sxs-lookup"><span data-stu-id="c69e6-140">You must configure the content key authorization policy.</span></span> <span data-ttu-id="c69e6-141">The client must meet the policy before the content key is delivered to the client.</span><span class="sxs-lookup"><span data-stu-id="c69e6-141">The client must meet the policy before the content key is delivered to the client.</span></span>

5. <span data-ttu-id="c69e6-142">[Configure the delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="c69e6-142">[Configure the delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="c69e6-143">The delivery policy configuration includes the key acquisition URL and an initialization vector (IV).</span><span class="sxs-lookup"><span data-stu-id="c69e6-143">The delivery policy configuration includes the key acquisition URL and an initialization vector (IV).</span></span> <span data-ttu-id="c69e6-144">(AES-128 requires the same IV for encryption and decryption.) The configuration also includes the delivery protocol (for example, MPEG-DASH, HLS, Smooth Streaming, or all) and the type of dynamic encryption (for example, envelope or no dynamic encryption).</span><span class="sxs-lookup"><span data-stu-id="c69e6-144">(AES-128 requires the same IV for encryption and decryption.) The configuration also includes the delivery protocol (for example, MPEG-DASH, HLS, Smooth Streaming, or all) and the type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="c69e6-145">You can apply a different policy to each protocol on the same asset.</span><span class="sxs-lookup"><span data-stu-id="c69e6-145">You can apply a different policy to each protocol on the same asset.</span></span> <span data-ttu-id="c69e6-146">For example, you can apply PlayReady encryption to Smooth/DASH and an AES envelope to HLS.</span><span class="sxs-lookup"><span data-stu-id="c69e6-146">For example, you can apply PlayReady encryption to Smooth/DASH and an AES envelope to HLS.</span></span> <span data-ttu-id="c69e6-147">Any protocols that aren't defined in a delivery policy are blocked from streaming.</span><span class="sxs-lookup"><span data-stu-id="c69e6-147">Any protocols that aren't defined in a delivery policy are blocked from streaming.</span></span> <span data-ttu-id="c69e6-148">(An example is if you add a single policy that specifies only HLS as the protocol.) The exception is if you have no asset delivery policy defined at all.</span><span class="sxs-lookup"><span data-stu-id="c69e6-148">(An example is if you add a single policy that specifies only HLS as the protocol.) The exception is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="c69e6-149">Then, all protocols are allowed in the clear.</span><span class="sxs-lookup"><span data-stu-id="c69e6-149">Then, all protocols are allowed in the clear.</span></span>

6. <span data-ttu-id="c69e6-150">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) to get a streaming URL.</span><span class="sxs-lookup"><span data-stu-id="c69e6-150">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) to get a streaming URL.</span></span>

<span data-ttu-id="c69e6-151">The article also shows [how a client application can request a key from the key delivery service](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="c69e6-151">The article also shows [how a client application can request a key from the key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="c69e6-152">You can find a complete [.NET example](media-services-protect-with-aes128.md#example) at the end of the article.</span><span class="sxs-lookup"><span data-stu-id="c69e6-152">You can find a complete [.NET example](media-services-protect-with-aes128.md#example) at the end of the article.</span></span>

<span data-ttu-id="c69e6-153">The following image demonstrates the workflow previously described.</span><span class="sxs-lookup"><span data-stu-id="c69e6-153">The following image demonstrates the workflow previously described.</span></span> <span data-ttu-id="c69e6-154">Here, the token is used for authentication.</span><span class="sxs-lookup"><span data-stu-id="c69e6-154">Here, the token is used for authentication.</span></span>

![Protect with AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="c69e6-156">The remainder of this article provides explanations, code examples, and links to topics that show you how to achieve the tasks previously described.</span><span class="sxs-lookup"><span data-stu-id="c69e6-156">The remainder of this article provides explanations, code examples, and links to topics that show you how to achieve the tasks previously described.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="c69e6-157">Current limitations</span><span class="sxs-lookup"><span data-stu-id="c69e6-157">Current limitations</span></span>
<span data-ttu-id="c69e6-158">If you add or update your asset's delivery policy, you must delete any existing locator and create a new locator.</span><span class="sxs-lookup"><span data-stu-id="c69e6-158">If you add or update your asset's delivery policy, you must delete any existing locator and create a new locator.</span></span>

## <a id="create_asset"></a><span data-ttu-id="c69e6-159">Create an asset and upload files into the asset</span><span class="sxs-lookup"><span data-stu-id="c69e6-159">Create an asset and upload files into the asset</span></span>
<span data-ttu-id="c69e6-160">To manage, encode, and stream your videos, you must first upload your content into Media Services.</span><span class="sxs-lookup"><span data-stu-id="c69e6-160">To manage, encode, and stream your videos, you must first upload your content into Media Services.</span></span> <span data-ttu-id="c69e6-161">After it's uploaded, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="c69e6-161">After it's uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> 

<span data-ttu-id="c69e6-162">For more information, see [Upload files into a Media Services account](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="c69e6-162">For more information, see [Upload files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a id="encode_asset"></a><span data-ttu-id="c69e6-163">Encode the asset that contains the file to the adaptive bitrate MP4 set</span><span class="sxs-lookup"><span data-stu-id="c69e6-163">Encode the asset that contains the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="c69e6-164">With dynamic encryption, you create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span><span class="sxs-lookup"><span data-stu-id="c69e6-164">With dynamic encryption, you create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="c69e6-165">Then, based on the specified format in the manifest or fragment request, the on-demand streaming server ensures that you receive the stream in the protocol you selected.</span><span class="sxs-lookup"><span data-stu-id="c69e6-165">Then, based on the specified format in the manifest or fragment request, the on-demand streaming server ensures that you receive the stream in the protocol you selected.</span></span> <span data-ttu-id="c69e6-166">Then, you only need to store and pay for the files in single storage format.</span><span class="sxs-lookup"><span data-stu-id="c69e6-166">Then, you only need to store and pay for the files in single storage format.</span></span> <span data-ttu-id="c69e6-167">Media Services builds and serves the appropriate response based on requests from a client.</span><span class="sxs-lookup"><span data-stu-id="c69e6-167">Media Services builds and serves the appropriate response based on requests from a client.</span></span> <span data-ttu-id="c69e6-168">For more information, see [Dynamic packaging overview](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c69e6-168">For more information, see [Dynamic packaging overview](media-services-dynamic-packaging-overview.md).</span></span>

>[!NOTE]
>When your Media Services account is created, a default streaming endpoint is added to your account in the "Stopped" state. To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content must be in the "Running" state. 
>
>Also, to use dynamic packaging and dynamic encryption, your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.

<span data-ttu-id="c69e6-172">For instructions on how to encode, see [Encode an asset by using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="c69e6-172">For instructions on how to encode, see [Encode an asset by using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <a id="create_contentkey"></a><span data-ttu-id="c69e6-173">Create a content key and associate it with the encoded asset</span><span class="sxs-lookup"><span data-stu-id="c69e6-173">Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="c69e6-174">In Media Services, the content key contains the key that you want to encrypt an asset with.</span><span class="sxs-lookup"><span data-stu-id="c69e6-174">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="c69e6-175">For more information, see [Create a content key](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="c69e6-175">For more information, see [Create a content key](media-services-dotnet-create-contentkey.md).</span></span>

## <a id="configure_key_auth_policy"></a><span data-ttu-id="c69e6-176">Configure the content key's authorization policy</span><span class="sxs-lookup"><span data-stu-id="c69e6-176">Configure the content key's authorization policy</span></span>
<span data-ttu-id="c69e6-177">Media Services supports multiple ways of authenticating users who make key requests.</span><span class="sxs-lookup"><span data-stu-id="c69e6-177">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="c69e6-178">You must configure the content key authorization policy.</span><span class="sxs-lookup"><span data-stu-id="c69e6-178">You must configure the content key authorization policy.</span></span> <span data-ttu-id="c69e6-179">The client (player) must meet the policy before the key can be delivered to the client.</span><span class="sxs-lookup"><span data-stu-id="c69e6-179">The client (player) must meet the policy before the key can be delivered to the client.</span></span> <span data-ttu-id="c69e6-180">The content key authorization policy can have one or more authorization restrictions, either open, token restriction, or IP restriction.</span><span class="sxs-lookup"><span data-stu-id="c69e6-180">The content key authorization policy can have one or more authorization restrictions, either open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="c69e6-181">For more information, see [Configure a content key authorization policy](media-services-dotnet-configure-content-key-auth-policy.md).</span><span class="sxs-lookup"><span data-stu-id="c69e6-181">For more information, see [Configure a content key authorization policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <a id="configure_asset_delivery_policy"></a><span data-ttu-id="c69e6-182">Configure an asset delivery policy</span><span class="sxs-lookup"><span data-stu-id="c69e6-182">Configure an asset delivery policy</span></span>
<span data-ttu-id="c69e6-183">Configure the delivery policy for your asset.</span><span class="sxs-lookup"><span data-stu-id="c69e6-183">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="c69e6-184">Some things that the asset delivery policy configuration includes are:</span><span class="sxs-lookup"><span data-stu-id="c69e6-184">Some things that the asset delivery policy configuration includes are:</span></span>

* <span data-ttu-id="c69e6-185">The key acquisition URL.</span><span class="sxs-lookup"><span data-stu-id="c69e6-185">The key acquisition URL.</span></span> 
* <span data-ttu-id="c69e6-186">The initialization vector (IV) to use for the envelope encryption.</span><span class="sxs-lookup"><span data-stu-id="c69e6-186">The initialization vector (IV) to use for the envelope encryption.</span></span> <span data-ttu-id="c69e6-187">AES-128 requires the same IV for encryption and decryption.</span><span class="sxs-lookup"><span data-stu-id="c69e6-187">AES-128 requires the same IV for encryption and decryption.</span></span> 
* <span data-ttu-id="c69e6-188">The asset delivery protocol (for example, MPEG-DASH, HLS, Smooth Streaming, or all).</span><span class="sxs-lookup"><span data-stu-id="c69e6-188">The asset delivery protocol (for example, MPEG-DASH, HLS, Smooth Streaming, or all).</span></span>
* <span data-ttu-id="c69e6-189">The type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span><span class="sxs-lookup"><span data-stu-id="c69e6-189">The type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="c69e6-190">For more information, see [Configure an asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="c69e6-190">For more information, see [Configure an asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

## <a id="create_locator"></a><span data-ttu-id="c69e6-191">Create an OnDemand streaming locator to get a streaming URL</span><span class="sxs-lookup"><span data-stu-id="c69e6-191">Create an OnDemand streaming locator to get a streaming URL</span></span>
<span data-ttu-id="c69e6-192">You need to provide your user with the streaming URL for Smooth Streaming, DASH, or HLS.</span><span class="sxs-lookup"><span data-stu-id="c69e6-192">You need to provide your user with the streaming URL for Smooth Streaming, DASH, or HLS.</span></span>

> [!NOTE]
> If you add or update your asset's delivery policy, you must delete any existing locator and create a new locator.
> 
> 

<span data-ttu-id="c69e6-194">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="c69e6-194">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="c69e6-195">Get a test token</span><span class="sxs-lookup"><span data-stu-id="c69e6-195">Get a test token</span></span>
<span data-ttu-id="c69e6-196">Get a test token based on the token restriction that was used for the key authorization policy.</span><span class="sxs-lookup"><span data-stu-id="c69e6-196">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

```csharp
    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word "Bearer" in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
```

<span data-ttu-id="c69e6-197">You can use the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span><span class="sxs-lookup"><span data-stu-id="c69e6-197">You can use the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <a id="client_request"></a><span data-ttu-id="c69e6-198">How can your client request a key from the key delivery service?</span><span class="sxs-lookup"><span data-stu-id="c69e6-198">How can your client request a key from the key delivery service?</span></span>
<span data-ttu-id="c69e6-199">In the previous step, you constructed the URL that points to a manifest file.</span><span class="sxs-lookup"><span data-stu-id="c69e6-199">In the previous step, you constructed the URL that points to a manifest file.</span></span> <span data-ttu-id="c69e6-200">Your client needs to extract the necessary information from the streaming manifest files to make a request to the key delivery service.</span><span class="sxs-lookup"><span data-stu-id="c69e6-200">Your client needs to extract the necessary information from the streaming manifest files to make a request to the key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="c69e6-201">Manifest files</span><span class="sxs-lookup"><span data-stu-id="c69e6-201">Manifest files</span></span>
<span data-ttu-id="c69e6-202">The client needs to extract the URL (that also contains content key ID [kid]) value from the manifest file.</span><span class="sxs-lookup"><span data-stu-id="c69e6-202">The client needs to extract the URL (that also contains content key ID [kid]) value from the manifest file.</span></span> <span data-ttu-id="c69e6-203">The client then tries to get the encryption key from the key delivery service.</span><span class="sxs-lookup"><span data-stu-id="c69e6-203">The client then tries to get the encryption key from the key delivery service.</span></span> <span data-ttu-id="c69e6-204">The client also needs to extract the IV value and use it to decrypt the stream.</span><span class="sxs-lookup"><span data-stu-id="c69e6-204">The client also needs to extract the IV value and use it to decrypt the stream.</span></span> <span data-ttu-id="c69e6-205">The following snippet shows the <Protection> element of the Smooth Streaming manifest:</span><span class="sxs-lookup"><span data-stu-id="c69e6-205">The following snippet shows the <Protection> element of the Smooth Streaming manifest:</span></span>

```xml
    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>
```

<span data-ttu-id="c69e6-206">In the case of HLS, the root manifest is broken into segment files.</span><span class="sxs-lookup"><span data-stu-id="c69e6-206">In the case of HLS, the root manifest is broken into segment files.</span></span> 

<span data-ttu-id="c69e6-207">For example, the root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl).</span><span class="sxs-lookup"><span data-stu-id="c69e6-207">For example, the root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl).</span></span> <span data-ttu-id="c69e6-208">It contains a list of segment file names.</span><span class="sxs-lookup"><span data-stu-id="c69e6-208">It contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="c69e6-209">If you open one of the segment files in a text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it contains #EXT-X-KEY, which indicates that the file is encrypted.</span><span class="sxs-lookup"><span data-stu-id="c69e6-209">If you open one of the segment files in a text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it contains #EXT-X-KEY, which indicates that the file is encrypted.</span></span>

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
>If you plan to play an AES-encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

### <a name="request-the-key-from-the-key-delivery-service"></a><span data-ttu-id="c69e6-211">Request the key from the key delivery service</span><span class="sxs-lookup"><span data-stu-id="c69e6-211">Request the key from the key delivery service</span></span>

<span data-ttu-id="c69e6-212">The following code shows how to send a request to the Media Services key delivery service by using a key delivery Uri (that was extracted from the manifest) and a token.</span><span class="sxs-lookup"><span data-stu-id="c69e6-212">The following code shows how to send a request to the Media Services key delivery service by using a key delivery Uri (that was extracted from the manifest) and a token.</span></span> <span data-ttu-id="c69e6-213">(This article doesn't explain how to get SWTs from an STS.)</span><span class="sxs-lookup"><span data-stu-id="c69e6-213">(This article doesn't explain how to get SWTs from an STS.)</span></span>

```csharp
    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }
```

## <a name="protect-your-content-with-aes-128-by-using-net"></a><span data-ttu-id="c69e6-214">Protect your content with AES-128 by using .NET</span><span class="sxs-lookup"><span data-stu-id="c69e6-214">Protect your content with AES-128 by using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c69e6-215">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="c69e6-215">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="c69e6-216">Set up your development environment, and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c69e6-216">Set up your development environment, and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

2. <span data-ttu-id="c69e6-217">Add the following elements to appSettings, as defined in your app.config file:</span><span class="sxs-lookup"><span data-stu-id="c69e6-217">Add the following elements to appSettings, as defined in your app.config file:</span></span>

    ```xml
            <add key="Issuer" value="http://testacs.com"/>
            <add key="Audience" value="urn:test"/>
    ```

### <a id="example"></a><span data-ttu-id="c69e6-218">Example</span><span class="sxs-lookup"><span data-stu-id="c69e6-218">Example</span></span>

<span data-ttu-id="c69e6-219">Overwrite the code in your Program.cs file with the code shown in this section.</span><span class="sxs-lookup"><span data-stu-id="c69e6-219">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>
 
>[!NOTE]
>There is a limit of 1,000,000 policies for different Media Services policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). Use the same policy ID if you always use the same days/access permissions. An example is policies for locators that are intended to remain in place for a long time (non-upload policies). For more information, see the "Limit access policies" section in [Manage assets and related entities with the Media Services .NET SDK](media-services-dotnet-manage-entities.md#limit-access-policies).

<span data-ttu-id="c69e6-224">Make sure to update variables to point to folders where your input files are located.</span><span class="sxs-lookup"><span data-stu-id="c69e6-224">Make sure to update variables to point to folders where your input files are located.</span></span>

```csharp
    [!code-csharp[Main](../../../samples-mediaservices-encryptionaes/DynamicEncryptionWithAES/DynamicEncryptionWithAES/Program.cs)]
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="c69e6-225">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="c69e6-225">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c69e6-226">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="c69e6-226">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

