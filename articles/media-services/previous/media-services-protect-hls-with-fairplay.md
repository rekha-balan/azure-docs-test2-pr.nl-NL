---
title: Protect HLS content with Microsoft PlayReady or Apple FairPlay - Azure | Microsoft Docs
description: This topic gives an overview and shows how to use Azure Media Services to dynamically encrypt your HTTP Live Streaming (HLS) content with Apple FairPlay. It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: 65188dacbb29fea5562ca5b83283861986719ce1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868802"
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="b9c3f-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="b9c3f-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="b9c3f-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span></span>  

* <span data-ttu-id="b9c3f-106">**AES-128 envelope clear key**</span><span class="sxs-lookup"><span data-stu-id="b9c3f-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="b9c3f-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="b9c3f-108">The decryption of the stream is supported by iOS and OS X player natively.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-108">The decryption of the stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="b9c3f-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="b9c3f-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="b9c3f-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="b9c3f-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="b9c3f-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="b9c3f-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="b9c3f-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="b9c3f-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="b9c3f-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagram of dynamic encryption workflow](./media/media-services-content-protection-overview/media-services-content-protection-with-FairPlay.png)

<span data-ttu-id="b9c3f-117">This article demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-117">This article demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="b9c3f-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="b9c3f-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span></span> <span data-ttu-id="b9c3f-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-playready-widevine.md).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-playready-widevine.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="b9c3f-121">Requirements and considerations</span><span class="sxs-lookup"><span data-stu-id="b9c3f-121">Requirements and considerations</span></span>

<span data-ttu-id="b9c3f-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span></span>

  * <span data-ttu-id="b9c3f-123">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-123">An Azure account.</span></span> <span data-ttu-id="b9c3f-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="b9c3f-125">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-125">A Media Services account.</span></span> <span data-ttu-id="b9c3f-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="b9c3f-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="b9c3f-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="b9c3f-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span></span> <span data-ttu-id="b9c3f-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span></span> <span data-ttu-id="b9c3f-131">You use ASK to configure FairPlay.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-131">You use ASK to configure FairPlay.</span></span>
  * <span data-ttu-id="b9c3f-132">Azure Media Services .NET SDK version **3.6.0** or later.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="b9c3f-133">The following things must be set on Media Services key delivery side:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-133">The following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="b9c3f-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span></span> <span data-ttu-id="b9c3f-135">You create this file and encrypt it with a password.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="b9c3f-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span></span>

      <span data-ttu-id="b9c3f-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="b9c3f-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="b9c3f-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="b9c3f-140">Run the following command from the command line.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-140">Run the following command from the command line.</span></span> <span data-ttu-id="b9c3f-141">This converts the .cer file to a .pem file.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-141">This converts the .cer file to a .pem file.</span></span>

        <span data-ttu-id="b9c3f-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in FairPlay.cer -out FairPlay-out.pem</span><span class="sxs-lookup"><span data-stu-id="b9c3f-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in FairPlay.cer -out FairPlay-out.pem</span></span>
    3. <span data-ttu-id="b9c3f-143">Run the following command from the command line.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-143">Run the following command from the command line.</span></span> <span data-ttu-id="b9c3f-144">This converts the .pem file to a .pfx file with the private key.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-144">This converts the .pem file to a .pfx file with the private key.</span></span> <span data-ttu-id="b9c3f-145">The password for the .pfx file is then asked by OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-145">The password for the .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="b9c3f-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out FairPlay-out.pfx -inkey privatekey.pem -in FairPlay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="b9c3f-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out FairPlay-out.pfx -inkey privatekey.pem -in FairPlay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="b9c3f-147">**App Cert password**: The password for creating the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-147">**App Cert password**: The password for creating the .pfx file.</span></span>
  * <span data-ttu-id="b9c3f-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span></span> <span data-ttu-id="b9c3f-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span></span> <span data-ttu-id="b9c3f-150">This is what they need to use inside the key delivery policy option.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-150">This is what they need to use inside the key delivery policy option.</span></span>
  * <span data-ttu-id="b9c3f-151">**iv**: This is a random value of 16 bytes.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="b9c3f-152">It must match the iv in the asset delivery policy.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-152">It must match the iv in the asset delivery policy.</span></span> <span data-ttu-id="b9c3f-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span></span>
  * <span data-ttu-id="b9c3f-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span></span> <span data-ttu-id="b9c3f-155">Each development team receives a unique ASK.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-155">Each development team receives a unique ASK.</span></span> <span data-ttu-id="b9c3f-156">Save a copy of the ASK, and store it in a safe place.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-156">Save a copy of the ASK, and store it in a safe place.</span></span> <span data-ttu-id="b9c3f-157">You need to configure ASK as FairPlayAsk to Media Services later.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-157">You need to configure ASK as FairPlayAsk to Media Services later.</span></span>
  * <span data-ttu-id="b9c3f-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="b9c3f-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="b9c3f-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span></span>

<span data-ttu-id="b9c3f-161">The following things must be set by the FPS client side:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-161">The following things must be set by the FPS client side:</span></span>

  * <span data-ttu-id="b9c3f-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span></span> <span data-ttu-id="b9c3f-163">Media Services needs to know about it because it is required by the player.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-163">Media Services needs to know about it because it is required by the player.</span></span> <span data-ttu-id="b9c3f-164">The key delivery service decrypts it using the corresponding private key.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-164">The key delivery service decrypts it using the corresponding private key.</span></span>

<span data-ttu-id="b9c3f-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="b9c3f-166">That process creates all three parts:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="b9c3f-167">.der file</span><span class="sxs-lookup"><span data-stu-id="b9c3f-167">.der file</span></span>
  * <span data-ttu-id="b9c3f-168">.pfx file</span><span class="sxs-lookup"><span data-stu-id="b9c3f-168">.pfx file</span></span>
  * <span data-ttu-id="b9c3f-169">password for the .pfx</span><span class="sxs-lookup"><span data-stu-id="b9c3f-169">password for the .pfx</span></span>

<span data-ttu-id="b9c3f-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="b9c3f-171">Configure FairPlay dynamic encryption and license delivery services</span><span class="sxs-lookup"><span data-stu-id="b9c3f-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="b9c3f-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="b9c3f-173">Create an asset, and upload files into the asset.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-173">Create an asset, and upload files into the asset.</span></span>
2. <span data-ttu-id="b9c3f-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="b9c3f-175">Create a content key, and associate it with the encoded asset.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-175">Create a content key, and associate it with the encoded asset.</span></span>  
4. <span data-ttu-id="b9c3f-176">Configure the content key’s authorization policy.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-176">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="b9c3f-177">Specify the following:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-177">Specify the following:</span></span>

   * <span data-ttu-id="b9c3f-178">The delivery method (in this case, FairPlay).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-178">The delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="b9c3f-179">FairPlay policy options configuration.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="b9c3f-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b9c3f-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="b9c3f-182">Restrictions (open or token).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="b9c3f-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span></span>
5. <span data-ttu-id="b9c3f-184">Configure the asset delivery policy.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-184">Configure the asset delivery policy.</span></span> <span data-ttu-id="b9c3f-185">The delivery policy configuration includes:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-185">The delivery policy configuration includes:</span></span>

   * <span data-ttu-id="b9c3f-186">The delivery protocol (HLS).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-186">The delivery protocol (HLS).</span></span>
   * <span data-ttu-id="b9c3f-187">The type of dynamic encryption (common CBC encryption).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-187">The type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="b9c3f-188">The license acquisition URL.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-188">The license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b9c3f-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="b9c3f-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span><span class="sxs-lookup"><span data-stu-id="b9c3f-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="b9c3f-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span><span class="sxs-lookup"><span data-stu-id="b9c3f-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="b9c3f-192">Create an OnDemand locator to get a streaming URL.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-192">Create an OnDemand locator to get a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="b9c3f-193">Use FairPlay key delivery by player apps</span><span class="sxs-lookup"><span data-stu-id="b9c3f-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="b9c3f-194">You can develop player apps by using the iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-194">You can develop player apps by using the iOS SDK.</span></span> <span data-ttu-id="b9c3f-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span></span> <span data-ttu-id="b9c3f-196">This protocol is not specified by Apple.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="b9c3f-197">It is up to each app how to send key delivery requests.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-197">It is up to each app how to send key delivery requests.</span></span> <span data-ttu-id="b9c3f-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="b9c3f-199">Azure Media Player supports FairPlay playback.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-199">Azure Media Player supports FairPlay playback.</span></span> <span data-ttu-id="b9c3f-200">See [Azure Media Player documentation](https://amp.azure.net/libs/amp/latest/docs/index.html) for further information.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-200">See [Azure Media Player documentation](https://amp.azure.net/libs/amp/latest/docs/index.html) for further information.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="b9c3f-201">Streaming URLs</span><span class="sxs-lookup"><span data-stu-id="b9c3f-201">Streaming URLs</span></span>
<span data-ttu-id="b9c3f-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span><span class="sxs-lookup"><span data-stu-id="b9c3f-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="b9c3f-203">The following considerations apply:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-203">The following considerations apply:</span></span>

* <span data-ttu-id="b9c3f-204">Only zero or one encryption type can be specified.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="b9c3f-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="b9c3f-206">The encryption type is case insensitive.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-206">The encryption type is case insensitive.</span></span>
* <span data-ttu-id="b9c3f-207">The following encryption types can be specified:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-207">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="b9c3f-208">**cenc**:  Common encryption (PlayReady or Widevine)</span><span class="sxs-lookup"><span data-stu-id="b9c3f-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="b9c3f-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="b9c3f-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="b9c3f-210">**cbc**: AES envelope encryption</span><span class="sxs-lookup"><span data-stu-id="b9c3f-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="b9c3f-211">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="b9c3f-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="b9c3f-212">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-212">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="b9c3f-213">Add the following elements to **appSettings** defined in your app.config file:</span><span class="sxs-lookup"><span data-stu-id="b9c3f-213">Add the following elements to **appSettings** defined in your app.config file:</span></span>

    ```xml
            <add key="Issuer" value="http://testacs.com"/>
            <add key="Audience" value="urn:test"/>
    ```

## <a name="example"></a><span data-ttu-id="b9c3f-214">Example</span><span class="sxs-lookup"><span data-stu-id="b9c3f-214">Example</span></span>

<span data-ttu-id="b9c3f-215">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-215">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="b9c3f-216">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-216">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="b9c3f-217">Overwrite the code in your Program.cs file with the code shown in this section.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-217">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="b9c3f-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="b9c3f-219">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span><span class="sxs-lookup"><span data-stu-id="b9c3f-219">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="b9c3f-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) article.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) article.</span></span>

<span data-ttu-id="b9c3f-221">Make sure to update variables to point to folders where your input files are located.</span><span class="sxs-lookup"><span data-stu-id="b9c3f-221">Make sure to update variables to point to folders where your input files are located.</span></span>

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
using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
using Newtonsoft.Json;
using System.Security.Cryptography.X509Certificates;

namespace DynamicEncryptionWithFairPlay
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

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
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

                // Generate a test token based on the data in the given TokenRestrictionTemplate.
                // Note, you need to pass the key id Guid because we specified
                // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
                Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
                string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                            DateTime.UtcNow.AddDays(365));
                Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
                Console.WriteLine();
            }

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

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

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

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

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with the cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound to a real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key to generate the response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating the .pfx file.
            string pfxPassword = "<customer password for creating the .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key to generate the response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match the iv in the asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify the .pfx file created by the customer.
            var appCert = new X509Certificate2("path to the .pfx file created by the customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get the FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // The reason the below code replaces "https://" with "skd://" is because
            // in the IOS player sample code which you obtained in Apple developer account,
            // the player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
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
```

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="b9c3f-222">Next steps: Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="b9c3f-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b9c3f-223">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="b9c3f-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]
