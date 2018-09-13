---
title: Azure Media Services and Apple FairPlay license support | Microsoft Docs
description: This topic gives an overview of a Apple FairPlay license requirements and configuration.
author: juliako
manager: cfowler
editor: ''
services: media-services
documentationcenter: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2018
ms.author: juliako
ms.openlocfilehash: a68896d061040843990318cbc39eaf1aaa3c8b27
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868813"
---
# <a name="apple-fairplay-license-requirements-and-configuration"></a><span data-ttu-id="e3fda-103">Apple FairPlay license requirements and configuration</span><span class="sxs-lookup"><span data-stu-id="e3fda-103">Apple FairPlay license requirements and configuration</span></span> 

<span data-ttu-id="e3fda-104">Azure Media Services enables you to encrypt your HLS content with **Apple FairPlay** (AES-128 CBC).</span><span class="sxs-lookup"><span data-stu-id="e3fda-104">Azure Media Services enables you to encrypt your HLS content with **Apple FairPlay** (AES-128 CBC).</span></span> <span data-ttu-id="e3fda-105">Media Services also provides a service for delivering FairPlay licenses.</span><span class="sxs-lookup"><span data-stu-id="e3fda-105">Media Services also provides a service for delivering FairPlay licenses.</span></span> <span data-ttu-id="e3fda-106">When a player tries to play your FairPlay-protected content, a request is sent to the license delivery service to obtain a license.</span><span class="sxs-lookup"><span data-stu-id="e3fda-106">When a player tries to play your FairPlay-protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="e3fda-107">If the license service approves the request, it issues the license that is sent to the client and is used to decrypt and play the specified content.</span><span class="sxs-lookup"><span data-stu-id="e3fda-107">If the license service approves the request, it issues the license that is sent to the client and is used to decrypt and play the specified content.</span></span>

<span data-ttu-id="e3fda-108">Media Services also provides APIs that you can use to configure your FairPlay licenses.</span><span class="sxs-lookup"><span data-stu-id="e3fda-108">Media Services also provides APIs that you can use to configure your FairPlay licenses.</span></span> <span data-ttu-id="e3fda-109">This topic discusses FairPlay license requirements and demonstrates how you can configure a **FairPlay** license using Media Sercies APIs.</span><span class="sxs-lookup"><span data-stu-id="e3fda-109">This topic discusses FairPlay license requirements and demonstrates how you can configure a **FairPlay** license using Media Sercies APIs.</span></span> 

## <a name="requirements"></a><span data-ttu-id="e3fda-110">Requirements</span><span class="sxs-lookup"><span data-stu-id="e3fda-110">Requirements</span></span>

<span data-ttu-id="e3fda-111">The following are required when using Media Services to encrypt your HLS content with **Apple FairPlay** and use Media Services to deliver FairPlay licenses:</span><span class="sxs-lookup"><span data-stu-id="e3fda-111">The following are required when using Media Services to encrypt your HLS content with **Apple FairPlay** and use Media Services to deliver FairPlay licenses:</span></span>

* <span data-ttu-id="e3fda-112">Sign up with [Apple Development Program](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="e3fda-112">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
* <span data-ttu-id="e3fda-113">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="e3fda-113">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="e3fda-114">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span><span class="sxs-lookup"><span data-stu-id="e3fda-114">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span></span> <span data-ttu-id="e3fda-115">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span><span class="sxs-lookup"><span data-stu-id="e3fda-115">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span></span> <span data-ttu-id="e3fda-116">You use ASK to configure FairPlay.</span><span class="sxs-lookup"><span data-stu-id="e3fda-116">You use ASK to configure FairPlay.</span></span>
* <span data-ttu-id="e3fda-117">The following things must be set on Media Services key/license delivery side:</span><span class="sxs-lookup"><span data-stu-id="e3fda-117">The following things must be set on Media Services key/license delivery side:</span></span>

    * <span data-ttu-id="e3fda-118">**App Cert (AC)**: This is a .pfx file that contains the private key.</span><span class="sxs-lookup"><span data-stu-id="e3fda-118">**App Cert (AC)**: This is a .pfx file that contains the private key.</span></span> <span data-ttu-id="e3fda-119">You create this file and encrypt it with a password.</span><span class="sxs-lookup"><span data-stu-id="e3fda-119">You create this file and encrypt it with a password.</span></span> <span data-ttu-id="e3fda-120">The .pfx file shoul be in Base64 format.</span><span class="sxs-lookup"><span data-stu-id="e3fda-120">The .pfx file shoul be in Base64 format.</span></span>

        <span data-ttu-id="e3fda-121">The following steps describe how to generate a .pfx certificate file for FairPlay:</span><span class="sxs-lookup"><span data-stu-id="e3fda-121">The following steps describe how to generate a .pfx certificate file for FairPlay:</span></span>

        1. <span data-ttu-id="e3fda-122">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="e3fda-122">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

            <span data-ttu-id="e3fda-123">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span><span class="sxs-lookup"><span data-stu-id="e3fda-123">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span></span>
        2. <span data-ttu-id="e3fda-124">Run the following command from the command line.</span><span class="sxs-lookup"><span data-stu-id="e3fda-124">Run the following command from the command line.</span></span> <span data-ttu-id="e3fda-125">This converts the .cer file to a .pem file.</span><span class="sxs-lookup"><span data-stu-id="e3fda-125">This converts the .cer file to a .pem file.</span></span>

            <span data-ttu-id="e3fda-126">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in FairPlay.cer -out FairPlay-out.pem</span><span class="sxs-lookup"><span data-stu-id="e3fda-126">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in FairPlay.cer -out FairPlay-out.pem</span></span>
        3. <span data-ttu-id="e3fda-127">Run the following command from the command line.</span><span class="sxs-lookup"><span data-stu-id="e3fda-127">Run the following command from the command line.</span></span> <span data-ttu-id="e3fda-128">This converts the .pem file to a .pfx file with the private key.</span><span class="sxs-lookup"><span data-stu-id="e3fda-128">This converts the .pem file to a .pfx file with the private key.</span></span> <span data-ttu-id="e3fda-129">The password for the .pfx file is then asked by OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="e3fda-129">The password for the .pfx file is then asked by OpenSSL.</span></span>

            <span data-ttu-id="e3fda-130">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out FairPlay-out.pfx -inkey privatekey.pem -in FairPlay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="e3fda-130">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out FairPlay-out.pfx -inkey privatekey.pem -in FairPlay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
            
    * <span data-ttu-id="e3fda-131">**App Cert password**: The password for creating the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="e3fda-131">**App Cert password**: The password for creating the .pfx file.</span></span>
    * <span data-ttu-id="e3fda-132">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span><span class="sxs-lookup"><span data-stu-id="e3fda-132">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span></span> <span data-ttu-id="e3fda-133">Each development team receives a unique ASK.</span><span class="sxs-lookup"><span data-stu-id="e3fda-133">Each development team receives a unique ASK.</span></span> <span data-ttu-id="e3fda-134">Save a copy of the ASK, and store it in a safe place.</span><span class="sxs-lookup"><span data-stu-id="e3fda-134">Save a copy of the ASK, and store it in a safe place.</span></span> <span data-ttu-id="e3fda-135">You need to configure ASK as FairPlayAsk with Media Services.</span><span class="sxs-lookup"><span data-stu-id="e3fda-135">You need to configure ASK as FairPlayAsk with Media Services.</span></span>
    
* <span data-ttu-id="e3fda-136">The following things must be set by the FPS client side:</span><span class="sxs-lookup"><span data-stu-id="e3fda-136">The following things must be set by the FPS client side:</span></span>

  * <span data-ttu-id="e3fda-137">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span><span class="sxs-lookup"><span data-stu-id="e3fda-137">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span></span> <span data-ttu-id="e3fda-138">Media Services needs to know about it because it is required by the player.</span><span class="sxs-lookup"><span data-stu-id="e3fda-138">Media Services needs to know about it because it is required by the player.</span></span> <span data-ttu-id="e3fda-139">The key delivery service decrypts it using the corresponding private key.</span><span class="sxs-lookup"><span data-stu-id="e3fda-139">The key delivery service decrypts it using the corresponding private key.</span></span>

* <span data-ttu-id="e3fda-140">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span><span class="sxs-lookup"><span data-stu-id="e3fda-140">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="e3fda-141">That process creates all three parts:</span><span class="sxs-lookup"><span data-stu-id="e3fda-141">That process creates all three parts:</span></span>

  * <span data-ttu-id="e3fda-142">.der file</span><span class="sxs-lookup"><span data-stu-id="e3fda-142">.der file</span></span>
  * <span data-ttu-id="e3fda-143">.pfx file</span><span class="sxs-lookup"><span data-stu-id="e3fda-143">.pfx file</span></span>
  * <span data-ttu-id="e3fda-144">password for the .pfx</span><span class="sxs-lookup"><span data-stu-id="e3fda-144">password for the .pfx</span></span>

## <a name="fairplay-and-player-apps"></a><span data-ttu-id="e3fda-145">FairPlay and player apps</span><span class="sxs-lookup"><span data-stu-id="e3fda-145">FairPlay and player apps</span></span>

<span data-ttu-id="e3fda-146">When your content is encrypted with **Apple FairPlay**, the individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span><span class="sxs-lookup"><span data-stu-id="e3fda-146">When your content is encrypted with **Apple FairPlay**, the individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="e3fda-147">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span><span class="sxs-lookup"><span data-stu-id="e3fda-147">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="e3fda-148">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span><span class="sxs-lookup"><span data-stu-id="e3fda-148">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span></span>

<span data-ttu-id="e3fda-149">Azure Media Player also supports FairPlay playback.</span><span class="sxs-lookup"><span data-stu-id="e3fda-149">Azure Media Player also supports FairPlay playback.</span></span> <span data-ttu-id="e3fda-150">For more information, see [Azure Media Player documentation](https://amp.azure.net/libs/amp/latest/docs/index.html).</span><span class="sxs-lookup"><span data-stu-id="e3fda-150">For more information, see [Azure Media Player documentation](https://amp.azure.net/libs/amp/latest/docs/index.html).</span></span>

<span data-ttu-id="e3fda-151">You can develop your own player apps by using the iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="e3fda-151">You can develop your own player apps by using the iOS SDK.</span></span> <span data-ttu-id="e3fda-152">To be able to play FairPlay content, you have to implement the license exchange protocol.</span><span class="sxs-lookup"><span data-stu-id="e3fda-152">To be able to play FairPlay content, you have to implement the license exchange protocol.</span></span> <span data-ttu-id="e3fda-153">This protocol is not specified by Apple.</span><span class="sxs-lookup"><span data-stu-id="e3fda-153">This protocol is not specified by Apple.</span></span> <span data-ttu-id="e3fda-154">It is up to each app how to send key delivery requests.</span><span class="sxs-lookup"><span data-stu-id="e3fda-154">It is up to each app how to send key delivery requests.</span></span> <span data-ttu-id="e3fda-155">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span><span class="sxs-lookup"><span data-stu-id="e3fda-155">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span></span>

```
spc=<Base64 encoded SPC>
```

## <a name="fairplay-configuration-net-example"></a><span data-ttu-id="e3fda-156">FairPlay configuration .NET example</span><span class="sxs-lookup"><span data-stu-id="e3fda-156">FairPlay configuration .NET example</span></span>

<span data-ttu-id="e3fda-157">You can use Media Services API to configure FairPlay licenses.</span><span class="sxs-lookup"><span data-stu-id="e3fda-157">You can use Media Services API to configure FairPlay licenses.</span></span> <span data-ttu-id="e3fda-158">When the player tries to play your FairPlay-protected content, a request is sent to the license delivery service to obtain the license.</span><span class="sxs-lookup"><span data-stu-id="e3fda-158">When the player tries to play your FairPlay-protected content, a request is sent to the license delivery service to obtain the license.</span></span> <span data-ttu-id="e3fda-159">If the license service approves the request, the service issues the license.</span><span class="sxs-lookup"><span data-stu-id="e3fda-159">If the license service approves the request, the service issues the license.</span></span> <span data-ttu-id="e3fda-160">It's sent to the client and is used to decrypt and play the specified content.</span><span class="sxs-lookup"><span data-stu-id="e3fda-160">It's sent to the client and is used to decrypt and play the specified content.</span></span>

> [!NOTE]
> <span data-ttu-id="e3fda-161">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span><span class="sxs-lookup"><span data-stu-id="e3fda-161">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>

<span data-ttu-id="e3fda-162">The following example uses [Media Services .NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.media.models?view=azure-dotnet) to configure the license.</span><span class="sxs-lookup"><span data-stu-id="e3fda-162">The following example uses [Media Services .NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.media.models?view=azure-dotnet) to configure the license.</span></span>

```csharp
private static ContentKeyPolicyFairPlayConfiguration ConfigureFairPlayPolicyOptions()
{

    string askHex = "";
    string FairPlayPfxPassword = "";

    var appCert = new X509Certificate2("FairPlayPfxPath", FairPlayPfxPassword, X509KeyStorageFlags.Exportable);

    byte[] askBytes = Enumerable
        .Range(0, askHex.Length)
        .Where(x => x % 2 == 0)
        .Select(x => Convert.ToByte(askHex.Substring(x, 2), 16))
        .ToArray();

    ContentKeyPolicyFairPlayConfiguration fairPlayConfiguration =
    new ContentKeyPolicyFairPlayConfiguration
    {
        Ask = askBytes,
        FairPlayPfx =
                Convert.ToBase64String(appCert.Export(X509ContentType.Pfx, FairPlayPfxPassword)),
        FairPlayPfxPassword = FairPlayPfxPassword,
        RentalAndLeaseKeyType =
                ContentKeyPolicyFairPlayRentalAndLeaseKeyType
                .PersistentUnlimited,
        RentalDuration = 2249
    };

    return fairPlayConfiguration;
}
```

## <a name="next-steps"></a><span data-ttu-id="e3fda-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="e3fda-163">Next steps</span></span>

<span data-ttu-id="e3fda-164">Check out how to [protect with DRM](protect-with-drm.md)</span><span class="sxs-lookup"><span data-stu-id="e3fda-164">Check out how to [protect with DRM](protect-with-drm.md)</span></span>