---
title: Protect HLS content with Microsoft PlayReady or Apple FairPlay - Azure | Microsoft Docs
description: This topic gives an overview and shows how to use Azure Media Services to dynamically encrypt your HTTP Live Streaming (HLS) content with Apple FairPlay. It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 77d75362352221a0bd08e878ec4f84897bc14a9f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661342"
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="cffaf-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="cffaf-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="cffaf-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span><span class="sxs-lookup"><span data-stu-id="cffaf-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span></span>  

* <span data-ttu-id="cffaf-106">**AES-128 envelope clear key**</span><span class="sxs-lookup"><span data-stu-id="cffaf-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="cffaf-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span><span class="sxs-lookup"><span data-stu-id="cffaf-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="cffaf-108">The decryption of the stream is supported by iOS and OS X player natively.</span><span class="sxs-lookup"><span data-stu-id="cffaf-108">The decryption of the stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="cffaf-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="cffaf-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="cffaf-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="cffaf-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="cffaf-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span><span class="sxs-lookup"><span data-stu-id="cffaf-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="cffaf-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span><span class="sxs-lookup"><span data-stu-id="cffaf-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="cffaf-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span><span class="sxs-lookup"><span data-stu-id="cffaf-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="cffaf-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="cffaf-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="cffaf-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span><span class="sxs-lookup"><span data-stu-id="cffaf-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagram of dynamic encryption workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="cffaf-117">This topic demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="cffaf-117">This topic demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="cffaf-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span><span class="sxs-lookup"><span data-stu-id="cffaf-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="cffaf-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span><span class="sxs-lookup"><span data-stu-id="cffaf-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span></span> <span data-ttu-id="cffaf-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="cffaf-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="cffaf-121">Requirements and considerations</span><span class="sxs-lookup"><span data-stu-id="cffaf-121">Requirements and considerations</span></span>

<span data-ttu-id="cffaf-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span><span class="sxs-lookup"><span data-stu-id="cffaf-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span></span>

  * <span data-ttu-id="cffaf-123">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="cffaf-123">An Azure account.</span></span> <span data-ttu-id="cffaf-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="cffaf-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="cffaf-125">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="cffaf-125">A Media Services account.</span></span> <span data-ttu-id="cffaf-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="cffaf-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="cffaf-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="cffaf-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="cffaf-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="cffaf-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="cffaf-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span><span class="sxs-lookup"><span data-stu-id="cffaf-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span></span> <span data-ttu-id="cffaf-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span><span class="sxs-lookup"><span data-stu-id="cffaf-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span></span> <span data-ttu-id="cffaf-131">You use ASK to configure FairPlay.</span><span class="sxs-lookup"><span data-stu-id="cffaf-131">You use ASK to configure FairPlay.</span></span>
  * <span data-ttu-id="cffaf-132">Azure Media Services .NET SDK version **3.6.0** or later.</span><span class="sxs-lookup"><span data-stu-id="cffaf-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="cffaf-133">The following things must be set on Media Services key delivery side:</span><span class="sxs-lookup"><span data-stu-id="cffaf-133">The following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="cffaf-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span><span class="sxs-lookup"><span data-stu-id="cffaf-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span></span> <span data-ttu-id="cffaf-135">You create this file and encrypt it with a password.</span><span class="sxs-lookup"><span data-stu-id="cffaf-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="cffaf-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span><span class="sxs-lookup"><span data-stu-id="cffaf-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span></span>

      <span data-ttu-id="cffaf-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span><span class="sxs-lookup"><span data-stu-id="cffaf-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="cffaf-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="cffaf-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="cffaf-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span><span class="sxs-lookup"><span data-stu-id="cffaf-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="cffaf-140">Run the following command from the command line.</span><span class="sxs-lookup"><span data-stu-id="cffaf-140">Run the following command from the command line.</span></span> <span data-ttu-id="cffaf-141">This converts the .cer file to a .pem file.</span><span class="sxs-lookup"><span data-stu-id="cffaf-141">This converts the .cer file to a .pem file.</span></span>

        <span data-ttu-id="cffaf-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="cffaf-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="cffaf-143">Run the following command from the command line.</span><span class="sxs-lookup"><span data-stu-id="cffaf-143">Run the following command from the command line.</span></span> <span data-ttu-id="cffaf-144">This converts the .pem file to a .pfx file with the private key.</span><span class="sxs-lookup"><span data-stu-id="cffaf-144">This converts the .pem file to a .pfx file with the private key.</span></span> <span data-ttu-id="cffaf-145">The password for the .pfx file is then asked by OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="cffaf-145">The password for the .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="cffaf-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="cffaf-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="cffaf-147">**App Cert password**: The password for creating the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="cffaf-147">**App Cert password**: The password for creating the .pfx file.</span></span>
  * <span data-ttu-id="cffaf-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span><span class="sxs-lookup"><span data-stu-id="cffaf-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span></span> <span data-ttu-id="cffaf-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span><span class="sxs-lookup"><span data-stu-id="cffaf-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span></span> <span data-ttu-id="cffaf-150">This is what they need to use inside the key delivery policy option.</span><span class="sxs-lookup"><span data-stu-id="cffaf-150">This is what they need to use inside the key delivery policy option.</span></span>
  * <span data-ttu-id="cffaf-151">**iv**: This is a random value of 16 bytes.</span><span class="sxs-lookup"><span data-stu-id="cffaf-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="cffaf-152">It must match the iv in the asset delivery policy.</span><span class="sxs-lookup"><span data-stu-id="cffaf-152">It must match the iv in the asset delivery policy.</span></span> <span data-ttu-id="cffaf-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span><span class="sxs-lookup"><span data-stu-id="cffaf-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span></span>
  * <span data-ttu-id="cffaf-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span><span class="sxs-lookup"><span data-stu-id="cffaf-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span></span> <span data-ttu-id="cffaf-155">Each development team will receive a unique ASK.</span><span class="sxs-lookup"><span data-stu-id="cffaf-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="cffaf-156">Save a copy of the ASK, and store it in a safe place.</span><span class="sxs-lookup"><span data-stu-id="cffaf-156">Save a copy of the ASK, and store it in a safe place.</span></span> <span data-ttu-id="cffaf-157">You will need to configure ASK as FairPlayAsk to Media Services later.</span><span class="sxs-lookup"><span data-stu-id="cffaf-157">You will need to configure ASK as FairPlayAsk to Media Services later.</span></span>
  * <span data-ttu-id="cffaf-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span><span class="sxs-lookup"><span data-stu-id="cffaf-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="cffaf-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span><span class="sxs-lookup"><span data-stu-id="cffaf-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="cffaf-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span><span class="sxs-lookup"><span data-stu-id="cffaf-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span></span>

<span data-ttu-id="cffaf-161">The following things must be set by the FPS client side:</span><span class="sxs-lookup"><span data-stu-id="cffaf-161">The following things must be set by the FPS client side:</span></span>

  * <span data-ttu-id="cffaf-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span><span class="sxs-lookup"><span data-stu-id="cffaf-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span></span> <span data-ttu-id="cffaf-163">Media Services needs to know about it because it is required by the player.</span><span class="sxs-lookup"><span data-stu-id="cffaf-163">Media Services needs to know about it because it is required by the player.</span></span> <span data-ttu-id="cffaf-164">The key delivery service decrypts it using the corresponding private key.</span><span class="sxs-lookup"><span data-stu-id="cffaf-164">The key delivery service decrypts it using the corresponding private key.</span></span>

<span data-ttu-id="cffaf-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span><span class="sxs-lookup"><span data-stu-id="cffaf-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="cffaf-166">That process creates all three parts:</span><span class="sxs-lookup"><span data-stu-id="cffaf-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="cffaf-167">.der file</span><span class="sxs-lookup"><span data-stu-id="cffaf-167">.der file</span></span>
  * <span data-ttu-id="cffaf-168">.pfx file</span><span class="sxs-lookup"><span data-stu-id="cffaf-168">.pfx file</span></span>
  * <span data-ttu-id="cffaf-169">password for the .pfx</span><span class="sxs-lookup"><span data-stu-id="cffaf-169">password for the .pfx</span></span>

<span data-ttu-id="cffaf-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span><span class="sxs-lookup"><span data-stu-id="cffaf-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="cffaf-171">Configure FairPlay dynamic encryption and license delivery services</span><span class="sxs-lookup"><span data-stu-id="cffaf-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="cffaf-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span><span class="sxs-lookup"><span data-stu-id="cffaf-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="cffaf-173">Create an asset, and upload files into the asset.</span><span class="sxs-lookup"><span data-stu-id="cffaf-173">Create an asset, and upload files into the asset.</span></span>
2. <span data-ttu-id="cffaf-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span><span class="sxs-lookup"><span data-stu-id="cffaf-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="cffaf-175">Create a content key, and associate it with the encoded asset.</span><span class="sxs-lookup"><span data-stu-id="cffaf-175">Create a content key, and associate it with the encoded asset.</span></span>  
4. <span data-ttu-id="cffaf-176">Configure the content key’s authorization policy.</span><span class="sxs-lookup"><span data-stu-id="cffaf-176">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="cffaf-177">Specify the following:</span><span class="sxs-lookup"><span data-stu-id="cffaf-177">Specify the following:</span></span>

   * <span data-ttu-id="cffaf-178">The delivery method (in this case, FairPlay).</span><span class="sxs-lookup"><span data-stu-id="cffaf-178">The delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="cffaf-179">FairPlay policy options configuration.</span><span class="sxs-lookup"><span data-stu-id="cffaf-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="cffaf-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span><span class="sxs-lookup"><span data-stu-id="cffaf-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="cffaf-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span><span class="sxs-lookup"><span data-stu-id="cffaf-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="cffaf-182">Restrictions (open or token).</span><span class="sxs-lookup"><span data-stu-id="cffaf-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="cffaf-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span><span class="sxs-lookup"><span data-stu-id="cffaf-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span></span>
5. <span data-ttu-id="cffaf-184">Configure the asset delivery policy.</span><span class="sxs-lookup"><span data-stu-id="cffaf-184">Configure the asset delivery policy.</span></span> <span data-ttu-id="cffaf-185">The delivery policy configuration includes:</span><span class="sxs-lookup"><span data-stu-id="cffaf-185">The delivery policy configuration includes:</span></span>

   * <span data-ttu-id="cffaf-186">The delivery protocol (HLS).</span><span class="sxs-lookup"><span data-stu-id="cffaf-186">The delivery protocol (HLS).</span></span>
   * <span data-ttu-id="cffaf-187">The type of dynamic encryption (common CBC encryption).</span><span class="sxs-lookup"><span data-stu-id="cffaf-187">The type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="cffaf-188">The license acquisition URL.</span><span class="sxs-lookup"><span data-stu-id="cffaf-188">The license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="cffaf-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span><span class="sxs-lookup"><span data-stu-id="cffaf-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="cffaf-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span><span class="sxs-lookup"><span data-stu-id="cffaf-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="cffaf-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span><span class="sxs-lookup"><span data-stu-id="cffaf-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="cffaf-192">Create an OnDemand locator to get a streaming URL.</span><span class="sxs-lookup"><span data-stu-id="cffaf-192">Create an OnDemand locator to get a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="cffaf-193">Use FairPlay key delivery by player apps</span><span class="sxs-lookup"><span data-stu-id="cffaf-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="cffaf-194">You can develop player apps by using the iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="cffaf-194">You can develop player apps by using the iOS SDK.</span></span> <span data-ttu-id="cffaf-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span><span class="sxs-lookup"><span data-stu-id="cffaf-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span></span> <span data-ttu-id="cffaf-196">This protocol is not specified by Apple.</span><span class="sxs-lookup"><span data-stu-id="cffaf-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="cffaf-197">It is up to each app how to send key delivery requests.</span><span class="sxs-lookup"><span data-stu-id="cffaf-197">It is up to each app how to send key delivery requests.</span></span> <span data-ttu-id="cffaf-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span><span class="sxs-lookup"><span data-stu-id="cffaf-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="cffaf-199">Azure Media Player doesn’t support FairPlay playback out of the box.</span><span class="sxs-lookup"><span data-stu-id="cffaf-199">Azure Media Player doesn’t support FairPlay playback out of the box.</span></span> <span data-ttu-id="cffaf-200">To get FairPlay playback on MAC OS X, obtain the sample player from the Apple developer account.</span><span class="sxs-lookup"><span data-stu-id="cffaf-200">To get FairPlay playback on MAC OS X, obtain the sample player from the Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="cffaf-201">Streaming URLs</span><span class="sxs-lookup"><span data-stu-id="cffaf-201">Streaming URLs</span></span>
<span data-ttu-id="cffaf-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span><span class="sxs-lookup"><span data-stu-id="cffaf-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="cffaf-203">The following considerations apply:</span><span class="sxs-lookup"><span data-stu-id="cffaf-203">The following considerations apply:</span></span>

* <span data-ttu-id="cffaf-204">Only zero or one encryption type can be specified.</span><span class="sxs-lookup"><span data-stu-id="cffaf-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="cffaf-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span><span class="sxs-lookup"><span data-stu-id="cffaf-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="cffaf-206">The encryption type is case insensitive.</span><span class="sxs-lookup"><span data-stu-id="cffaf-206">The encryption type is case insensitive.</span></span>
* <span data-ttu-id="cffaf-207">The following encryption types can be specified:</span><span class="sxs-lookup"><span data-stu-id="cffaf-207">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="cffaf-208">**cenc**:  Common encryption (PlayReady or Widevine)</span><span class="sxs-lookup"><span data-stu-id="cffaf-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="cffaf-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="cffaf-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="cffaf-210">**cbc**: AES envelope encryption</span><span class="sxs-lookup"><span data-stu-id="cffaf-210">**cbc**: AES envelope encryption</span></span>

## <a name="net-example-deliver-your-content-encrypted-with-fairplay"></a><span data-ttu-id="cffaf-211">.NET example: deliver your content encrypted with FairPlay</span><span class="sxs-lookup"><span data-stu-id="cffaf-211">.NET example: deliver your content encrypted with FairPlay</span></span>
<span data-ttu-id="cffaf-212">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span><span class="sxs-lookup"><span data-stu-id="cffaf-212">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="cffaf-213">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="cffaf-213">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span></span> <span data-ttu-id="cffaf-214">The following NuGet package command was used to install the package:</span><span class="sxs-lookup"><span data-stu-id="cffaf-214">The following NuGet package command was used to install the package:</span></span>

    PM> Install-Package windowsazure.mediaservices -Version 3.6.0


1. <span data-ttu-id="cffaf-215">Create a Console project.</span><span class="sxs-lookup"><span data-stu-id="cffaf-215">Create a Console project.</span></span>
2. <span data-ttu-id="cffaf-216">Use NuGet to install and add the Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="cffaf-216">Use NuGet to install and add the Azure Media Services .NET SDK.</span></span>
3. <span data-ttu-id="cffaf-217">Add additional references: System.Configuration.</span><span class="sxs-lookup"><span data-stu-id="cffaf-217">Add additional references: System.Configuration.</span></span>
4. <span data-ttu-id="cffaf-218">Add a config file that contains the account name and key information:</span><span class="sxs-lookup"><span data-stu-id="cffaf-218">Add a config file that contains the account name and key information:</span></span>

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
7. <span data-ttu-id="cffaf-219">Overwrite the code in your Program.cs file with the code shown in this section.</span><span class="sxs-lookup"><span data-stu-id="cffaf-219">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

    >[!NOTE]
    ><span data-ttu-id="cffaf-220">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="cffaf-220">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="cffaf-221">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span><span class="sxs-lookup"><span data-stu-id="cffaf-221">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="cffaf-222">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span><span class="sxs-lookup"><span data-stu-id="cffaf-222">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

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

                        // Generate a test token based on the the data in the given TokenRestrictionTemplate.
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
                    encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset),     AssetCreationOptions.StorageEncrypted);

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


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="cffaf-223">Next steps: Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="cffaf-223">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cffaf-224">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="cffaf-224">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

