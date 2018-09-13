---
title: Protect HLS content with offline Apple FairPlay - Azure | Microsoft Docs
description: This topic gives an overview and shows how to use Azure Media Services to dynamically encrypt your HTTP Live Streaming (HLS) content with Apple FairPlay in offline mode.
services: media-services
keywords: HLS, DRM, FairPlay Streaming (FPS), Offline, iOS 10
documentationcenter: ''
author: willzhan
manager: steveng
editor: ''
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2017
ms.author: willzhan, dwgeo
ms.openlocfilehash: dc38772097dddb7c7135d55598373d7ab544f9ea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864841"
---
# <a name="offline-fairplay-streaming-for-ios"></a><span data-ttu-id="2436b-104">Offline FairPlay Streaming for iOS</span><span class="sxs-lookup"><span data-stu-id="2436b-104">Offline FairPlay Streaming for iOS</span></span> 
 <span data-ttu-id="2436b-105">Azure Media Services provides a set of well-designed [content protection services](https://azure.microsoft.com/services/media-services/content-protection/) that cover:</span><span class="sxs-lookup"><span data-stu-id="2436b-105">Azure Media Services provides a set of well-designed [content protection services](https://azure.microsoft.com/services/media-services/content-protection/) that cover:</span></span>

- <span data-ttu-id="2436b-106">Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="2436b-106">Microsoft PlayReady</span></span>
- <span data-ttu-id="2436b-107">Google Widevine</span><span class="sxs-lookup"><span data-stu-id="2436b-107">Google Widevine</span></span>
- <span data-ttu-id="2436b-108">Apple FairPlay</span><span class="sxs-lookup"><span data-stu-id="2436b-108">Apple FairPlay</span></span>
- <span data-ttu-id="2436b-109">AES-128 encryption</span><span class="sxs-lookup"><span data-stu-id="2436b-109">AES-128 encryption</span></span>

<span data-ttu-id="2436b-110">Digital rights management (DRM)/Advanced Encryption Standard (AES) encryption of content is performed dynamically upon request for various streaming protocols.</span><span class="sxs-lookup"><span data-stu-id="2436b-110">Digital rights management (DRM)/Advanced Encryption Standard (AES) encryption of content is performed dynamically upon request for various streaming protocols.</span></span> <span data-ttu-id="2436b-111">DRM license/AES decryption key delivery services also are provided by Media Services.</span><span class="sxs-lookup"><span data-stu-id="2436b-111">DRM license/AES decryption key delivery services also are provided by Media Services.</span></span>

<span data-ttu-id="2436b-112">Besides protecting content for online streaming over various streaming protocols, offline mode for protected content is also an often-requested feature.</span><span class="sxs-lookup"><span data-stu-id="2436b-112">Besides protecting content for online streaming over various streaming protocols, offline mode for protected content is also an often-requested feature.</span></span> <span data-ttu-id="2436b-113">Offline-mode support is needed for the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="2436b-113">Offline-mode support is needed for the following scenarios:</span></span>

* <span data-ttu-id="2436b-114">Playback when internet connection isn't available, such as during travel.</span><span class="sxs-lookup"><span data-stu-id="2436b-114">Playback when internet connection isn't available, such as during travel.</span></span>
* <span data-ttu-id="2436b-115">Some content providers might disallow DRM license delivery beyond a country's border.</span><span class="sxs-lookup"><span data-stu-id="2436b-115">Some content providers might disallow DRM license delivery beyond a country's border.</span></span> <span data-ttu-id="2436b-116">If users want to watch content while traveling outside of the country, offline download is needed.</span><span class="sxs-lookup"><span data-stu-id="2436b-116">If users want to watch content while traveling outside of the country, offline download is needed.</span></span>
* <span data-ttu-id="2436b-117">In some countries, internet availability and/or bandwidth is still limited.</span><span class="sxs-lookup"><span data-stu-id="2436b-117">In some countries, internet availability and/or bandwidth is still limited.</span></span> <span data-ttu-id="2436b-118">Users might choose to download first to be able to watch content in a resolution that is high enough for a satisfactory viewing experience.</span><span class="sxs-lookup"><span data-stu-id="2436b-118">Users might choose to download first to be able to watch content in a resolution that is high enough for a satisfactory viewing experience.</span></span> <span data-ttu-id="2436b-119">In this case, the issue typically isn't network availability but limited network bandwidth.</span><span class="sxs-lookup"><span data-stu-id="2436b-119">In this case, the issue typically isn't network availability but limited network bandwidth.</span></span> <span data-ttu-id="2436b-120">Over-the-top (OTT)/online video platform (OVP) providers request offline-mode support.</span><span class="sxs-lookup"><span data-stu-id="2436b-120">Over-the-top (OTT)/online video platform (OVP) providers request offline-mode support.</span></span>

<span data-ttu-id="2436b-121">This article covers FairPlay Streaming (FPS) offline-mode support that targets devices running iOS 10 or later.</span><span class="sxs-lookup"><span data-stu-id="2436b-121">This article covers FairPlay Streaming (FPS) offline-mode support that targets devices running iOS 10 or later.</span></span> <span data-ttu-id="2436b-122">This feature isn't supported for other Apple platforms, such as watchOS, tvOS, or Safari on macOS.</span><span class="sxs-lookup"><span data-stu-id="2436b-122">This feature isn't supported for other Apple platforms, such as watchOS, tvOS, or Safari on macOS.</span></span>

## <a name="preliminary-steps"></a><span data-ttu-id="2436b-123">Preliminary steps</span><span class="sxs-lookup"><span data-stu-id="2436b-123">Preliminary steps</span></span>
<span data-ttu-id="2436b-124">Before you implement offline DRM for FairPlay on an iOS 10+ device:</span><span class="sxs-lookup"><span data-stu-id="2436b-124">Before you implement offline DRM for FairPlay on an iOS 10+ device:</span></span>

* <span data-ttu-id="2436b-125">Become familiar with online content protection for FairPlay.</span><span class="sxs-lookup"><span data-stu-id="2436b-125">Become familiar with online content protection for FairPlay.</span></span> <span data-ttu-id="2436b-126">For more information, see the following articles and samples:</span><span class="sxs-lookup"><span data-stu-id="2436b-126">For more information, see the following articles and samples:</span></span>

    - [<span data-ttu-id="2436b-127">Apple FairPlay Streaming for Azure Media Services is generally available</span><span class="sxs-lookup"><span data-stu-id="2436b-127">Apple FairPlay Streaming for Azure Media Services is generally available</span></span>](https://azure.microsoft.com/blog/apple-FairPlay-streaming-for-azure-media-services-generally-available/)
    - [<span data-ttu-id="2436b-128">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="2436b-128">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>](https://docs.microsoft.com/azure/media-services/media-services-protect-hls-with-FairPlay)
    - [<span data-ttu-id="2436b-129">A sample for online FPS streaming</span><span class="sxs-lookup"><span data-stu-id="2436b-129">A sample for online FPS streaming</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-dynamic-encryption-with-FairPlay/)

* <span data-ttu-id="2436b-130">Obtain the FPS SDK from the Apple Developer Network.</span><span class="sxs-lookup"><span data-stu-id="2436b-130">Obtain the FPS SDK from the Apple Developer Network.</span></span> <span data-ttu-id="2436b-131">The FPS SDK contains two components:</span><span class="sxs-lookup"><span data-stu-id="2436b-131">The FPS SDK contains two components:</span></span>

    - <span data-ttu-id="2436b-132">The FPS Server SDK, which contains the Key Security Module (KSM), client samples, a specification, and a set of test vectors.</span><span class="sxs-lookup"><span data-stu-id="2436b-132">The FPS Server SDK, which contains the Key Security Module (KSM), client samples, a specification, and a set of test vectors.</span></span>
    - <span data-ttu-id="2436b-133">The FPS Deployment Pack, which contains the D function specification, along with instructions about how to generate the FPS Certificate, customer-specific private key, and Application Secret Key.</span><span class="sxs-lookup"><span data-stu-id="2436b-133">The FPS Deployment Pack, which contains the D function specification, along with instructions about how to generate the FPS Certificate, customer-specific private key, and Application Secret Key.</span></span> <span data-ttu-id="2436b-134">Apple issues the FPS Deployment Pack only to licensed content providers.</span><span class="sxs-lookup"><span data-stu-id="2436b-134">Apple issues the FPS Deployment Pack only to licensed content providers.</span></span>

## <a name="configuration-in-media-services"></a><span data-ttu-id="2436b-135">Configuration in Media Services</span><span class="sxs-lookup"><span data-stu-id="2436b-135">Configuration in Media Services</span></span>
<span data-ttu-id="2436b-136">For FPS offline-mode configuration via the [Media Services .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices), use the Media Services .NET SDK version 4.0.0.4 or later, which provides the necessary API to configure FPS offline mode.</span><span class="sxs-lookup"><span data-stu-id="2436b-136">For FPS offline-mode configuration via the [Media Services .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices), use the Media Services .NET SDK version 4.0.0.4 or later, which provides the necessary API to configure FPS offline mode.</span></span>
<span data-ttu-id="2436b-137">You also need the working code to configure online-mode FPS content protection.</span><span class="sxs-lookup"><span data-stu-id="2436b-137">You also need the working code to configure online-mode FPS content protection.</span></span> <span data-ttu-id="2436b-138">After you obtain the code to configure online-mode content protection for FPS, you need only the following two changes.</span><span class="sxs-lookup"><span data-stu-id="2436b-138">After you obtain the code to configure online-mode content protection for FPS, you need only the following two changes.</span></span>

## <a name="code-change-in-the-fairplay-configuration"></a><span data-ttu-id="2436b-139">Code change in the FairPlay configuration</span><span class="sxs-lookup"><span data-stu-id="2436b-139">Code change in the FairPlay configuration</span></span>
<span data-ttu-id="2436b-140">The first change is to define an "enable offline mode" Boolean, called objDRMSettings.EnableOfflineMode, that is true when it enables the offline DRM scenario.</span><span class="sxs-lookup"><span data-stu-id="2436b-140">The first change is to define an "enable offline mode" Boolean, called objDRMSettings.EnableOfflineMode, that is true when it enables the offline DRM scenario.</span></span> <span data-ttu-id="2436b-141">Depending on this indicator, make the following change to the FairPlay configuration:</span><span class="sxs-lookup"><span data-stu-id="2436b-141">Depending on this indicator, make the following change to the FairPlay configuration:</span></span>

```csharp
if (objDRMSettings.EnableOfflineMode)
    {
        FairPlayConfiguration = Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
            objX509Certificate2,
            pfxPassword,
            pfxPasswordId,
            askId,
            iv, 
            RentalAndLeaseKeyType.PersistentUnlimited,
            0x9999);
    }
    else
    {
        FairPlayConfiguration = Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
            objX509Certificate2,
            pfxPassword,
            pfxPasswordId,
            askId,
            iv);
    }
```

## <a name="code-change-in-the-asset-delivery-policy-configuration"></a><span data-ttu-id="2436b-142">Code change in the asset delivery policy configuration</span><span class="sxs-lookup"><span data-stu-id="2436b-142">Code change in the asset delivery policy configuration</span></span>
<span data-ttu-id="2436b-143">The second change is to add the third key into Dictionary<AssetDeliveryPolicyConfigurationKey, string>.</span><span class="sxs-lookup"><span data-stu-id="2436b-143">The second change is to add the third key into Dictionary<AssetDeliveryPolicyConfigurationKey, string>.</span></span>
<span data-ttu-id="2436b-144">Add AssetDeliveryPolicyConfigurationKey as shown here:</span><span class="sxs-lookup"><span data-stu-id="2436b-144">Add AssetDeliveryPolicyConfigurationKey as shown here:</span></span>
 
```csharp
// FPS offline mode
    if (drmSettings.EnableOfflineMode)
    {
        objDictionary_AssetDeliveryPolicyConfigurationKey.Add(AssetDeliveryPolicyConfigurationKey.AllowPersistentLicense, "true");
        Console.WriteLine("FPS OFFLINE MODE: AssetDeliveryPolicyConfigurationKey.AllowPersistentLicense added into asset delivery policy configuration.");
    }

    // for IAssetDelivery for FPS
    IAssetDeliveryPolicy objIAssetDeliveryPolicy = objCloudMediaContext.AssetDeliveryPolicies.Create(
            drmSettings.AssetDeliveryPolicyName,
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
            objDictionary_AssetDeliveryPolicyConfigurationKey);
```

<span data-ttu-id="2436b-145">After this step, the <Dictionary_AssetDeliveryPolicyConfigurationKey> string in the FPS asset delivery policy contains the following three entries:</span><span class="sxs-lookup"><span data-stu-id="2436b-145">After this step, the <Dictionary_AssetDeliveryPolicyConfigurationKey> string in the FPS asset delivery policy contains the following three entries:</span></span>

* <span data-ttu-id="2436b-146">AssetDeliveryPolicyConfigurationKey.FairPlayBaseLicenseAcquisitionUrl or AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, depending on factors such as the FPS KSM/key server used and whether you reuse the same asset delivery policy across multiple assets</span><span class="sxs-lookup"><span data-stu-id="2436b-146">AssetDeliveryPolicyConfigurationKey.FairPlayBaseLicenseAcquisitionUrl or AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, depending on factors such as the FPS KSM/key server used and whether you reuse the same asset delivery policy across multiple assets</span></span>
* <span data-ttu-id="2436b-147">AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs</span><span class="sxs-lookup"><span data-stu-id="2436b-147">AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs</span></span>
* <span data-ttu-id="2436b-148">AssetDeliveryPolicyConfigurationKey.AllowPersistentLicense</span><span class="sxs-lookup"><span data-stu-id="2436b-148">AssetDeliveryPolicyConfigurationKey.AllowPersistentLicense</span></span>

<span data-ttu-id="2436b-149">Now your Media Services account is configured to deliver offline FairPlay licenses.</span><span class="sxs-lookup"><span data-stu-id="2436b-149">Now your Media Services account is configured to deliver offline FairPlay licenses.</span></span>

## <a name="sample-ios-player"></a><span data-ttu-id="2436b-150">Sample iOS Player</span><span class="sxs-lookup"><span data-stu-id="2436b-150">Sample iOS Player</span></span>
<span data-ttu-id="2436b-151">FPS offline-mode support is available only on iOS 10 and later.</span><span class="sxs-lookup"><span data-stu-id="2436b-151">FPS offline-mode support is available only on iOS 10 and later.</span></span> <span data-ttu-id="2436b-152">The FPS Server SDK (version 3.0 or later) contains the document and sample for FPS offline mode.</span><span class="sxs-lookup"><span data-stu-id="2436b-152">The FPS Server SDK (version 3.0 or later) contains the document and sample for FPS offline mode.</span></span> <span data-ttu-id="2436b-153">Specifically, FPS Server SDK (version 3.0 or later) contains the following two items related to offline mode:</span><span class="sxs-lookup"><span data-stu-id="2436b-153">Specifically, FPS Server SDK (version 3.0 or later) contains the following two items related to offline mode:</span></span>

* <span data-ttu-id="2436b-154">Document: "Offline Playback with FairPlay Streaming and HTTP Live Streaming."</span><span class="sxs-lookup"><span data-stu-id="2436b-154">Document: "Offline Playback with FairPlay Streaming and HTTP Live Streaming."</span></span> <span data-ttu-id="2436b-155">Apple, September 14, 2016.</span><span class="sxs-lookup"><span data-stu-id="2436b-155">Apple, September 14, 2016.</span></span> <span data-ttu-id="2436b-156">In FPS Server SDK version 4.0, this document is merged into the main FPS document.</span><span class="sxs-lookup"><span data-stu-id="2436b-156">In FPS Server SDK version 4.0, this document is merged into the main FPS document.</span></span>
* <span data-ttu-id="2436b-157">Sample code: HLSCatalog sample for FPS offline mode in the \FairPlay Streaming Server SDK version 3.1\Development\Client\HLSCatalog_With_FPS\HLSCatalog\.</span><span class="sxs-lookup"><span data-stu-id="2436b-157">Sample code: HLSCatalog sample for FPS offline mode in the \FairPlay Streaming Server SDK version 3.1\Development\Client\HLSCatalog_With_FPS\HLSCatalog\.</span></span> <span data-ttu-id="2436b-158">In the HLSCatalog sample app, the following code files are used to implement offline-mode features:</span><span class="sxs-lookup"><span data-stu-id="2436b-158">In the HLSCatalog sample app, the following code files are used to implement offline-mode features:</span></span>

    - <span data-ttu-id="2436b-159">AssetPersistenceManager.swift code file: AssetPersistenceManager is the main class in this sample that demonstrates how to:</span><span class="sxs-lookup"><span data-stu-id="2436b-159">AssetPersistenceManager.swift code file: AssetPersistenceManager is the main class in this sample that demonstrates how to:</span></span>

        - <span data-ttu-id="2436b-160">Manage downloading HLS streams, such as the APIs used to start and cancel downloads and to delete existing assets off devices.</span><span class="sxs-lookup"><span data-stu-id="2436b-160">Manage downloading HLS streams, such as the APIs used to start and cancel downloads and to delete existing assets off devices.</span></span>
        - <span data-ttu-id="2436b-161">Monitor the download progress.</span><span class="sxs-lookup"><span data-stu-id="2436b-161">Monitor the download progress.</span></span>
    - <span data-ttu-id="2436b-162">AssetListTableViewController.swift and AssetListTableViewCell.swift code files: AssetListTableViewController is the main interface of this sample.</span><span class="sxs-lookup"><span data-stu-id="2436b-162">AssetListTableViewController.swift and AssetListTableViewCell.swift code files: AssetListTableViewController is the main interface of this sample.</span></span> <span data-ttu-id="2436b-163">It provides a list of assets the sample can use to play, download, delete, or cancel a download.</span><span class="sxs-lookup"><span data-stu-id="2436b-163">It provides a list of assets the sample can use to play, download, delete, or cancel a download.</span></span> 

<span data-ttu-id="2436b-164">These steps show how to set up a running iOS player.</span><span class="sxs-lookup"><span data-stu-id="2436b-164">These steps show how to set up a running iOS player.</span></span> <span data-ttu-id="2436b-165">Assuming you start from the HLSCatalog sample in FPS Server SDK version 4.0.1, make the following code changes:</span><span class="sxs-lookup"><span data-stu-id="2436b-165">Assuming you start from the HLSCatalog sample in FPS Server SDK version 4.0.1, make the following code changes:</span></span>

<span data-ttu-id="2436b-166">In HLSCatalog\Shared\Managers\ContentKeyDelegate.swift, implement the method `requestContentKeyFromKeySecurityModule(spcData: Data, assetID: String)` by using the following code.</span><span class="sxs-lookup"><span data-stu-id="2436b-166">In HLSCatalog\Shared\Managers\ContentKeyDelegate.swift, implement the method `requestContentKeyFromKeySecurityModule(spcData: Data, assetID: String)` by using the following code.</span></span> <span data-ttu-id="2436b-167">Let "drmUr" be a variable assigned to the HLS URL.</span><span class="sxs-lookup"><span data-stu-id="2436b-167">Let "drmUr" be a variable assigned to the HLS URL.</span></span>

```swift
    var ckcData: Data? = nil
    
    let semaphore = DispatchSemaphore(value: 0)
    let postString = "spc=\(spcData.base64EncodedString())&assetId=\(assetIDString)"
    
    if let postData = postString.data(using: .ascii, allowLossyConversion: true), let drmServerUrl = URL(string: self.drmUrl) {
        var request = URLRequest(url: drmServerUrl)
        request.httpMethod = "POST"
        request.setValue(String(postData.count), forHTTPHeaderField: "Content-Length")
        request.setValue("application/x-www-form-urlencoded", forHTTPHeaderField: "Content-Type")
        request.httpBody = postData
        
        URLSession.shared.dataTask(with: request) { (data, _, error) in
            if let data = data, var responseString = String(data: data, encoding: .utf8) {
                responseString = responseString.replacingOccurrences(of: "<ckc>", with: "").replacingOccurrences(of: "</ckc>", with: "")
                ckcData = Data(base64Encoded: responseString)
            } else {
                print("Error encountered while fetching FairPlay license for URL: \(self.drmUrl), \(error?.localizedDescription ?? "Unknown error")")
            }
            
            semaphore.signal()
            }.resume()
    } else {
        fatalError("Invalid post data")
    }
    
    semaphore.wait()
    return ckcData
```

<span data-ttu-id="2436b-168">In HLSCatalog\Shared\Managers\ContentKeyDelegate.swift, implement the method `requestApplicationCertificate()`.</span><span class="sxs-lookup"><span data-stu-id="2436b-168">In HLSCatalog\Shared\Managers\ContentKeyDelegate.swift, implement the method `requestApplicationCertificate()`.</span></span> <span data-ttu-id="2436b-169">This implementation depends on whether you embed the certificate (public key only) with the device or host the certificate on the web.</span><span class="sxs-lookup"><span data-stu-id="2436b-169">This implementation depends on whether you embed the certificate (public key only) with the device or host the certificate on the web.</span></span> <span data-ttu-id="2436b-170">The following implementation uses the hosted application certificate used in the test samples.</span><span class="sxs-lookup"><span data-stu-id="2436b-170">The following implementation uses the hosted application certificate used in the test samples.</span></span> <span data-ttu-id="2436b-171">Let "certUrl" be a variable that contains the URL of the application certificate.</span><span class="sxs-lookup"><span data-stu-id="2436b-171">Let "certUrl" be a variable that contains the URL of the application certificate.</span></span>

```swift
func requestApplicationCertificate() throws -> Data {

        var applicationCertificate: Data? = nil
        do {
            applicationCertificate = try Data(contentsOf: URL(string: certUrl)!)
        } catch {
            print("Error loading FairPlay application certificate: \(error)")
        }
        
        return applicationCertificate
    }
```

<span data-ttu-id="2436b-172">For the final integrated test, both the video URL and the application certificate URL are provided in the section "Integrated Test."</span><span class="sxs-lookup"><span data-stu-id="2436b-172">For the final integrated test, both the video URL and the application certificate URL are provided in the section "Integrated Test."</span></span>

<span data-ttu-id="2436b-173">In HLSCatalog\Shared\Resources\Streams.plist, add your test video URL.</span><span class="sxs-lookup"><span data-stu-id="2436b-173">In HLSCatalog\Shared\Resources\Streams.plist, add your test video URL.</span></span> <span data-ttu-id="2436b-174">For the content key ID, use the FairPlay license acquisition URL with the skd protocol as the unique value.</span><span class="sxs-lookup"><span data-stu-id="2436b-174">For the content key ID, use the FairPlay license acquisition URL with the skd protocol as the unique value.</span></span>

![Offline FairPlay iOS App Streams](media/media-services-protect-hls-with-offline-FairPlay/media-services-offline-FairPlay-ios-app-streams.png)

<span data-ttu-id="2436b-176">Use your own test video URL, FairPlay license acquisition URL, and application certificate URL, if you have them set up.</span><span class="sxs-lookup"><span data-stu-id="2436b-176">Use your own test video URL, FairPlay license acquisition URL, and application certificate URL, if you have them set up.</span></span> <span data-ttu-id="2436b-177">Or you can continue to the next section, which contains test samples.</span><span class="sxs-lookup"><span data-stu-id="2436b-177">Or you can continue to the next section, which contains test samples.</span></span>

## <a name="integrated-test"></a><span data-ttu-id="2436b-178">Integrated test</span><span class="sxs-lookup"><span data-stu-id="2436b-178">Integrated test</span></span>
<span data-ttu-id="2436b-179">Three test samples in Media Services cover the following three scenarios:</span><span class="sxs-lookup"><span data-stu-id="2436b-179">Three test samples in Media Services cover the following three scenarios:</span></span>

* <span data-ttu-id="2436b-180">FPS protected, with video, audio, and alternate audio track</span><span class="sxs-lookup"><span data-stu-id="2436b-180">FPS protected, with video, audio, and alternate audio track</span></span>
* <span data-ttu-id="2436b-181">FPS protected, with video and audio, but no alternate audio track</span><span class="sxs-lookup"><span data-stu-id="2436b-181">FPS protected, with video and audio, but no alternate audio track</span></span>
* <span data-ttu-id="2436b-182">FPS protected, with video only and no audio</span><span class="sxs-lookup"><span data-stu-id="2436b-182">FPS protected, with video only and no audio</span></span>

<span data-ttu-id="2436b-183">You can find these samples at [this demo site](http://aka.ms/poc#22), with the corresponding application certificate hosted in an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="2436b-183">You can find these samples at [this demo site](http://aka.ms/poc#22), with the corresponding application certificate hosted in an Azure web app.</span></span>
<span data-ttu-id="2436b-184">With either the version 3 or version 4 sample of the FPS Server SDK, if a master playlist contains alternate audio, during offline mode it plays audio only.</span><span class="sxs-lookup"><span data-stu-id="2436b-184">With either the version 3 or version 4 sample of the FPS Server SDK, if a master playlist contains alternate audio, during offline mode it plays audio only.</span></span> <span data-ttu-id="2436b-185">Therefore, you need to strip the alternate audio.</span><span class="sxs-lookup"><span data-stu-id="2436b-185">Therefore, you need to strip the alternate audio.</span></span> <span data-ttu-id="2436b-186">In other words, the second and third samples listed previously work in online and offline mode.</span><span class="sxs-lookup"><span data-stu-id="2436b-186">In other words, the second and third samples listed previously work in online and offline mode.</span></span> <span data-ttu-id="2436b-187">The sample listed first plays audio only during offline mode, while online streaming works properly.</span><span class="sxs-lookup"><span data-stu-id="2436b-187">The sample listed first plays audio only during offline mode, while online streaming works properly.</span></span>

## <a name="faq"></a><span data-ttu-id="2436b-188">FAQ</span><span class="sxs-lookup"><span data-stu-id="2436b-188">FAQ</span></span>
<span data-ttu-id="2436b-189">The following frequently asked questions provide assistance with troubleshooting:</span><span class="sxs-lookup"><span data-stu-id="2436b-189">The following frequently asked questions provide assistance with troubleshooting:</span></span>

- <span data-ttu-id="2436b-190">**Why does only audio play but not video during offline mode?**</span><span class="sxs-lookup"><span data-stu-id="2436b-190">**Why does only audio play but not video during offline mode?**</span></span> <span data-ttu-id="2436b-191">This behavior seems to be by design of the sample app.</span><span class="sxs-lookup"><span data-stu-id="2436b-191">This behavior seems to be by design of the sample app.</span></span> <span data-ttu-id="2436b-192">When an alternate audio track is present (which is the case for HLS) during offline mode, both iOS 10 and iOS 11 default to the alternate audio track. To compensate this behavior for FPS offline mode, remove the alternate audio track from the stream.</span><span class="sxs-lookup"><span data-stu-id="2436b-192">When an alternate audio track is present (which is the case for HLS) during offline mode, both iOS 10 and iOS 11 default to the alternate audio track. To compensate this behavior for FPS offline mode, remove the alternate audio track from the stream.</span></span> <span data-ttu-id="2436b-193">To do this on Media Services, add the dynamic manifest filter "audio-only=false."</span><span class="sxs-lookup"><span data-stu-id="2436b-193">To do this on Media Services, add the dynamic manifest filter "audio-only=false."</span></span> <span data-ttu-id="2436b-194">In other words, an HLS URL ends with .ism/manifest(format=m3u8-aapl,audio-only=false).</span><span class="sxs-lookup"><span data-stu-id="2436b-194">In other words, an HLS URL ends with .ism/manifest(format=m3u8-aapl,audio-only=false).</span></span> 
- <span data-ttu-id="2436b-195">**Why does it still play audio only without video during offline mode after I add audio-only=false?**</span><span class="sxs-lookup"><span data-stu-id="2436b-195">**Why does it still play audio only without video during offline mode after I add audio-only=false?**</span></span> <span data-ttu-id="2436b-196">Depending on the content delivery network (CDN) cache key design, the content might be cached.</span><span class="sxs-lookup"><span data-stu-id="2436b-196">Depending on the content delivery network (CDN) cache key design, the content might be cached.</span></span> <span data-ttu-id="2436b-197">Purge the cache.</span><span class="sxs-lookup"><span data-stu-id="2436b-197">Purge the cache.</span></span>
- <span data-ttu-id="2436b-198">**Is FPS offline mode also supported on iOS 11 in addition to iOS 10?**</span><span class="sxs-lookup"><span data-stu-id="2436b-198">**Is FPS offline mode also supported on iOS 11 in addition to iOS 10?**</span></span> <span data-ttu-id="2436b-199">Yes.</span><span class="sxs-lookup"><span data-stu-id="2436b-199">Yes.</span></span> <span data-ttu-id="2436b-200">FPS offline mode is supported for iOS 10 and iOS 11.</span><span class="sxs-lookup"><span data-stu-id="2436b-200">FPS offline mode is supported for iOS 10 and iOS 11.</span></span>
- <span data-ttu-id="2436b-201">**Why can't I find the document "Offline Playback with FairPlay Streaming and HTTP Live Streaming" in the FPS Server SDK?**</span><span class="sxs-lookup"><span data-stu-id="2436b-201">**Why can't I find the document "Offline Playback with FairPlay Streaming and HTTP Live Streaming" in the FPS Server SDK?**</span></span> <span data-ttu-id="2436b-202">Since FPS Server SDK version 4, this document was merged into the "FairPlay Streaming Programming Guide."</span><span class="sxs-lookup"><span data-stu-id="2436b-202">Since FPS Server SDK version 4, this document was merged into the "FairPlay Streaming Programming Guide."</span></span>
- <span data-ttu-id="2436b-203">**What does the last parameter stand for in the following API for FPS offline mode?**
`Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(objX509Certificate2, pfxPassword, pfxPasswordId, askId, iv, RentalAndLeaseKeyType.PersistentUnlimited, 0x9999);`</span><span class="sxs-lookup"><span data-stu-id="2436b-203">**What does the last parameter stand for in the following API for FPS offline mode?**
`Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(objX509Certificate2, pfxPassword, pfxPasswordId, askId, iv, RentalAndLeaseKeyType.PersistentUnlimited, 0x9999);`</span></span>

    <span data-ttu-id="2436b-204">For the documentation for this API, see [FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration Method](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.mediaservices.client.FairPlay.FairPlayconfiguration.createserializedFairPlayoptionconfiguration?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="2436b-204">For the documentation for this API, see [FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration Method](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.mediaservices.client.FairPlay.FairPlayconfiguration.createserializedFairPlayoptionconfiguration?view=azure-dotnet).</span></span> <span data-ttu-id="2436b-205">The parameter represents the duration of the offline rental, with hour as the unit.</span><span class="sxs-lookup"><span data-stu-id="2436b-205">The parameter represents the duration of the offline rental, with hour as the unit.</span></span>
- <span data-ttu-id="2436b-206">**What is the downloaded/offline file structure on iOS devices?**</span><span class="sxs-lookup"><span data-stu-id="2436b-206">**What is the downloaded/offline file structure on iOS devices?**</span></span> <span data-ttu-id="2436b-207">The downloaded file structure on an iOS device looks like the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="2436b-207">The downloaded file structure on an iOS device looks like the following screenshot.</span></span> <span data-ttu-id="2436b-208">The `_keys` folder stores downloaded FPS licenses, with one store file for each license service host.</span><span class="sxs-lookup"><span data-stu-id="2436b-208">The `_keys` folder stores downloaded FPS licenses, with one store file for each license service host.</span></span> <span data-ttu-id="2436b-209">The `.movpkg` folder stores audio and video content.</span><span class="sxs-lookup"><span data-stu-id="2436b-209">The `.movpkg` folder stores audio and video content.</span></span> <span data-ttu-id="2436b-210">The first folder with a name that ends with a dash followed by a numeric contains video content.</span><span class="sxs-lookup"><span data-stu-id="2436b-210">The first folder with a name that ends with a dash followed by a numeric contains video content.</span></span> <span data-ttu-id="2436b-211">The numeric value is the PeakBandwidth of the video renditions.</span><span class="sxs-lookup"><span data-stu-id="2436b-211">The numeric value is the PeakBandwidth of the video renditions.</span></span> <span data-ttu-id="2436b-212">The second folder with a name that ends with a dash followed by 0 contains audio content.</span><span class="sxs-lookup"><span data-stu-id="2436b-212">The second folder with a name that ends with a dash followed by 0 contains audio content.</span></span> <span data-ttu-id="2436b-213">The third folder named "Data" contains the master playlist of the FPS content.</span><span class="sxs-lookup"><span data-stu-id="2436b-213">The third folder named "Data" contains the master playlist of the FPS content.</span></span> <span data-ttu-id="2436b-214">Finally, boot.xml provides a complete description of the `.movpkg` folder content.</span><span class="sxs-lookup"><span data-stu-id="2436b-214">Finally, boot.xml provides a complete description of the `.movpkg` folder content.</span></span> 

![Offline FairPlay iOS sample app file structure](media/media-services-protect-hls-with-offline-FairPlay/media-services-offline-FairPlay-file-structure.png)

<span data-ttu-id="2436b-216">A sample boot.xml file:</span><span class="sxs-lookup"><span data-stu-id="2436b-216">A sample boot.xml file:</span></span>
```xml
<?xml version="1.0" encoding="UTF-8"?>
<HLSMoviePackage xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://apple.com/IMG/Schemas/HLSMoviePackage" xsi:schemaLocation="http://apple.com/IMG/Schemas/HLSMoviePackage /System/Library/Schemas/HLSMoviePackage.xsd">
  <Version>1.0</Version>
  <HLSMoviePackageType>PersistedStore</HLSMoviePackageType>
  <Streams>
    <Stream ID="1-4DTFY3A3VDRCNZ53YZ3RJ2NPG2AJHNBD-0" Path="1-4DTFY3A3VDRCNZ53YZ3RJ2NPG2AJHNBD-0" NetworkURL="https://willzhanmswest.streaming.mediaservices.windows.net/e7c76dbb-8e38-44b3-be8c-5c78890c4bb4/MicrosoftElite01.ism/QualityLevels(127000)/Manifest(aac_eng_2_127,format=m3u8-aapl)">
      <Complete>YES</Complete>
    </Stream>
    <Stream ID="0-HC6H5GWC5IU62P4VHE7NWNGO2SZGPKUJ-310656" Path="0-HC6H5GWC5IU62P4VHE7NWNGO2SZGPKUJ-310656" NetworkURL="https://willzhanmswest.streaming.mediaservices.windows.net/e7c76dbb-8e38-44b3-be8c-5c78890c4bb4/MicrosoftElite01.ism/QualityLevels(161000)/Manifest(video,format=m3u8-aapl)">
      <Complete>YES</Complete>
    </Stream>
  </Streams>
  <MasterPlaylist>
    <NetworkURL>https://willzhanmswest.streaming.mediaservices.windows.net/e7c76dbb-8e38-44b3-be8c-5c78890c4bb4/MicrosoftElite01.ism/manifest(format=m3u8-aapl,audio-only=false)</NetworkURL>
  </MasterPlaylist>
  <DataItems Directory="Data">
    <DataItem>
      <ID>CB50F631-8227-477A-BCEC-365BBF12BCC0</ID>
      <Category>Playlist</Category>
      <Name>master.m3u8</Name>
      <DataPath>Playlist-master.m3u8-CB50F631-8227-477A-BCEC-365BBF12BCC0.data</DataPath>
      <Role>Master</Role>
    </DataItem>
  </DataItems>
</HLSMoviePackage>
```

## <a name="summary"></a><span data-ttu-id="2436b-217">Summary</span><span class="sxs-lookup"><span data-stu-id="2436b-217">Summary</span></span>
<span data-ttu-id="2436b-218">This document includes the following steps and information you can use to implement FPS offline mode:</span><span class="sxs-lookup"><span data-stu-id="2436b-218">This document includes the following steps and information you can use to implement FPS offline mode:</span></span>

* <span data-ttu-id="2436b-219">Media Services content protection configuration via the Media Services .NET API configures dynamic FairPlay encryption and FairPlay license delivery in Media Services.</span><span class="sxs-lookup"><span data-stu-id="2436b-219">Media Services content protection configuration via the Media Services .NET API configures dynamic FairPlay encryption and FairPlay license delivery in Media Services.</span></span>
* <span data-ttu-id="2436b-220">An iOS player based on the sample from the FPS Server SDK sets up an iOS player that can play FPS content either in online streaming mode or offline mode.</span><span class="sxs-lookup"><span data-stu-id="2436b-220">An iOS player based on the sample from the FPS Server SDK sets up an iOS player that can play FPS content either in online streaming mode or offline mode.</span></span>
* <span data-ttu-id="2436b-221">Sample FPS videos are used to test offline mode and online streaming.</span><span class="sxs-lookup"><span data-stu-id="2436b-221">Sample FPS videos are used to test offline mode and online streaming.</span></span>
* <span data-ttu-id="2436b-222">A FAQ answers questions about FPS offline mode.</span><span class="sxs-lookup"><span data-stu-id="2436b-222">A FAQ answers questions about FPS offline mode.</span></span>
