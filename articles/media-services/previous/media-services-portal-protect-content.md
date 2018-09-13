---
title: Configure content protection policies by using the Azure portal | Microsoft Docs
description: This article demonstrates how to use the Azure portal to configure content protection policies. The article also shows how to enable dynamic encryption for your assets.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: c46faf2298ebaac4f40fb1d18cbfca83076e0d4f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865243"
---
# <a name="configure-content-protection-policies-by-using-the-azure-portal"></a><span data-ttu-id="9350a-104">Configure content protection policies by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9350a-104">Configure content protection policies by using the Azure portal</span></span>
 <span data-ttu-id="9350a-105">With Azure Media Services, you can secure your media from the time it leaves your computer through storage, processing, and delivery.</span><span class="sxs-lookup"><span data-stu-id="9350a-105">With Azure Media Services, you can secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="9350a-106">You can use Media Services to deliver your content encrypted dynamically with the Advanced Encryption Standard (AES) by using 128-bit encryption keys.</span><span class="sxs-lookup"><span data-stu-id="9350a-106">You can use Media Services to deliver your content encrypted dynamically with the Advanced Encryption Standard (AES) by using 128-bit encryption keys.</span></span> <span data-ttu-id="9350a-107">You also can use it with common encryption (CENC) by using PlayReady and/or Widevine digital rights management (DRM) and Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="9350a-107">You also can use it with common encryption (CENC) by using PlayReady and/or Widevine digital rights management (DRM) and Apple FairPlay.</span></span> 

<span data-ttu-id="9350a-108">Media Services provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span><span class="sxs-lookup"><span data-stu-id="9350a-108">Media Services provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="9350a-109">You can use the Azure portal to create one key/license authorization policy for all types of encryptions.</span><span class="sxs-lookup"><span data-stu-id="9350a-109">You can use the Azure portal to create one key/license authorization policy for all types of encryptions.</span></span>

<span data-ttu-id="9350a-110">This article demonstrates how to configure a content protection policy by using the portal.</span><span class="sxs-lookup"><span data-stu-id="9350a-110">This article demonstrates how to configure a content protection policy by using the portal.</span></span> <span data-ttu-id="9350a-111">The article also shows how to apply dynamic encryption to your assets.</span><span class="sxs-lookup"><span data-stu-id="9350a-111">The article also shows how to apply dynamic encryption to your assets.</span></span>

## <a name="start-to-configure-content-protection"></a><span data-ttu-id="9350a-112">Start to configure content protection</span><span class="sxs-lookup"><span data-stu-id="9350a-112">Start to configure content protection</span></span>
<span data-ttu-id="9350a-113">To use the portal to configure global content protection by using your Media Services account, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="9350a-113">To use the portal to configure global content protection by using your Media Services account, take the following steps:</span></span>

1. <span data-ttu-id="9350a-114">In the [portal](https://portal.azure.com/), select your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="9350a-114">In the [portal](https://portal.azure.com/), select your Media Services account.</span></span>

1. <span data-ttu-id="9350a-115">Select **Settings** > **Content protection**.</span><span class="sxs-lookup"><span data-stu-id="9350a-115">Select **Settings** > **Content protection**.</span></span>

    ![Content protection](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="9350a-117">Key/license authorization policy</span><span class="sxs-lookup"><span data-stu-id="9350a-117">Key/license authorization policy</span></span>
<span data-ttu-id="9350a-118">Media Services supports multiple ways of authenticating users who make key or license requests.</span><span class="sxs-lookup"><span data-stu-id="9350a-118">Media Services supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="9350a-119">You must configure the content key authorization policy.</span><span class="sxs-lookup"><span data-stu-id="9350a-119">You must configure the content key authorization policy.</span></span> <span data-ttu-id="9350a-120">Your client then must meet the policy before the key/license can be delivered to it.</span><span class="sxs-lookup"><span data-stu-id="9350a-120">Your client then must meet the policy before the key/license can be delivered to it.</span></span> <span data-ttu-id="9350a-121">The content key authorization policy can have one or more authorization restrictions, either open or token restrictions.</span><span class="sxs-lookup"><span data-stu-id="9350a-121">The content key authorization policy can have one or more authorization restrictions, either open or token restrictions.</span></span>

<span data-ttu-id="9350a-122">You can use the portal to create one key/license authorization policy for all types of encryptions.</span><span class="sxs-lookup"><span data-stu-id="9350a-122">You can use the portal to create one key/license authorization policy for all types of encryptions.</span></span>

### <a name="open-authorization"></a><span data-ttu-id="9350a-123">Open authorization</span><span class="sxs-lookup"><span data-stu-id="9350a-123">Open authorization</span></span>
<span data-ttu-id="9350a-124">Open restriction means that the system delivers the key to anyone who makes a key request.</span><span class="sxs-lookup"><span data-stu-id="9350a-124">Open restriction means that the system delivers the key to anyone who makes a key request.</span></span> <span data-ttu-id="9350a-125">This restriction might be useful for test purposes.</span><span class="sxs-lookup"><span data-stu-id="9350a-125">This restriction might be useful for test purposes.</span></span> 

### <a name="token-authorization"></a><span data-ttu-id="9350a-126">Token authorization</span><span class="sxs-lookup"><span data-stu-id="9350a-126">Token authorization</span></span>
<span data-ttu-id="9350a-127">The token-restricted policy must be accompanied by a token issued by a security token service (STS).</span><span class="sxs-lookup"><span data-stu-id="9350a-127">The token-restricted policy must be accompanied by a token issued by a security token service (STS).</span></span> <span data-ttu-id="9350a-128">Media Services supports tokens in the simple web token (SWT) and JSON Web Token (JWT) formats.</span><span class="sxs-lookup"><span data-stu-id="9350a-128">Media Services supports tokens in the simple web token (SWT) and JSON Web Token (JWT) formats.</span></span> <span data-ttu-id="9350a-129">Media Services doesn't provide an STS.</span><span class="sxs-lookup"><span data-stu-id="9350a-129">Media Services doesn't provide an STS.</span></span> <span data-ttu-id="9350a-130">You can create a custom STS or use Azure Access Control Service to issue tokens.</span><span class="sxs-lookup"><span data-stu-id="9350a-130">You can create a custom STS or use Azure Access Control Service to issue tokens.</span></span> <span data-ttu-id="9350a-131">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span><span class="sxs-lookup"><span data-stu-id="9350a-131">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="9350a-132">If the token is valid and the claims in the token match those configured for the key (or license), the Media Services key delivery service returns the requested key (or license) to the client.</span><span class="sxs-lookup"><span data-stu-id="9350a-132">If the token is valid and the claims in the token match those configured for the key (or license), the Media Services key delivery service returns the requested key (or license) to the client.</span></span>

<span data-ttu-id="9350a-133">When you configure the token-restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span><span class="sxs-lookup"><span data-stu-id="9350a-133">When you configure the token-restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="9350a-134">The primary verification key contains the key that the token was signed with.</span><span class="sxs-lookup"><span data-stu-id="9350a-134">The primary verification key contains the key that the token was signed with.</span></span> <span data-ttu-id="9350a-135">The issuer is the secure token service that issues the token.</span><span class="sxs-lookup"><span data-stu-id="9350a-135">The issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="9350a-136">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span><span class="sxs-lookup"><span data-stu-id="9350a-136">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="9350a-137">The Media Services key delivery service validates that these values in the token match the values in the template.</span><span class="sxs-lookup"><span data-stu-id="9350a-137">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

![Key/license authorization policy](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-license-template"></a><span data-ttu-id="9350a-139">PlayReady license template</span><span class="sxs-lookup"><span data-stu-id="9350a-139">PlayReady license template</span></span>
<span data-ttu-id="9350a-140">The PlayReady license template sets the functionality that is enabled on your PlayReady license.</span><span class="sxs-lookup"><span data-stu-id="9350a-140">The PlayReady license template sets the functionality that is enabled on your PlayReady license.</span></span> <span data-ttu-id="9350a-141">For more information about the PlayReady license template, see the [Media Services PlayReady license template overview](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9350a-141">For more information about the PlayReady license template, see the [Media Services PlayReady license template overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="nonpersistent"></a><span data-ttu-id="9350a-142">Nonpersistent</span><span class="sxs-lookup"><span data-stu-id="9350a-142">Nonpersistent</span></span>
<span data-ttu-id="9350a-143">If you configure a license as nonpersistent, it's held in memory only while the player uses the license.</span><span class="sxs-lookup"><span data-stu-id="9350a-143">If you configure a license as nonpersistent, it's held in memory only while the player uses the license.</span></span>  

![Nonpersistent content protection](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="9350a-145">Persistent</span><span class="sxs-lookup"><span data-stu-id="9350a-145">Persistent</span></span>
<span data-ttu-id="9350a-146">If you configure a license as persistent, it's saved in persistent storage on the client.</span><span class="sxs-lookup"><span data-stu-id="9350a-146">If you configure a license as persistent, it's saved in persistent storage on the client.</span></span>

![Persistent content protection](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-license-template"></a><span data-ttu-id="9350a-148">Widevine license template</span><span class="sxs-lookup"><span data-stu-id="9350a-148">Widevine license template</span></span>
<span data-ttu-id="9350a-149">The Widevine license template sets the functionality that is enabled on your Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="9350a-149">The Widevine license template sets the functionality that is enabled on your Widevine licenses.</span></span>

### <a name="basic"></a><span data-ttu-id="9350a-150">Basic</span><span class="sxs-lookup"><span data-stu-id="9350a-150">Basic</span></span>
<span data-ttu-id="9350a-151">When you select **Basic**, the template is created with all default values.</span><span class="sxs-lookup"><span data-stu-id="9350a-151">When you select **Basic**, the template is created with all default values.</span></span>

### <a name="advanced"></a><span data-ttu-id="9350a-152">Advanced</span><span class="sxs-lookup"><span data-stu-id="9350a-152">Advanced</span></span>
<span data-ttu-id="9350a-153">For more information about the Widevine rights template, see the [Widevine license template overview](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9350a-153">For more information about the Widevine rights template, see the [Widevine license template overview](media-services-widevine-license-template-overview.md).</span></span>

![Advanced content protection](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="9350a-155">FairPlay configuration</span><span class="sxs-lookup"><span data-stu-id="9350a-155">FairPlay configuration</span></span>
<span data-ttu-id="9350a-156">To enable FairPlay encryption, select **FairPlay configuration**.</span><span class="sxs-lookup"><span data-stu-id="9350a-156">To enable FairPlay encryption, select **FairPlay configuration**.</span></span> <span data-ttu-id="9350a-157">Then select the **App certificate** and enter the **Application Secret Key**.</span><span class="sxs-lookup"><span data-stu-id="9350a-157">Then select the **App certificate** and enter the **Application Secret Key**.</span></span> <span data-ttu-id="9350a-158">For more information about FairPlay configuration and requirements, see [Protect your HLS content with Apple FairPlay or Microsoft PlayReady](media-services-protect-hls-with-FairPlay.md).</span><span class="sxs-lookup"><span data-stu-id="9350a-158">For more information about FairPlay configuration and requirements, see [Protect your HLS content with Apple FairPlay or Microsoft PlayReady](media-services-protect-hls-with-FairPlay.md).</span></span>

![FairPlay configuration](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-to-your-asset"></a><span data-ttu-id="9350a-160">Apply dynamic encryption to your asset</span><span class="sxs-lookup"><span data-stu-id="9350a-160">Apply dynamic encryption to your asset</span></span>
<span data-ttu-id="9350a-161">To take advantage of dynamic encryption, encode your source file into a set of adaptive-bitrate MP4 files.</span><span class="sxs-lookup"><span data-stu-id="9350a-161">To take advantage of dynamic encryption, encode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-to-encrypt"></a><span data-ttu-id="9350a-162">Select an asset that you want to encrypt</span><span class="sxs-lookup"><span data-stu-id="9350a-162">Select an asset that you want to encrypt</span></span>
<span data-ttu-id="9350a-163">To see all your assets, select **Settings** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="9350a-163">To see all your assets, select **Settings** > **Assets**.</span></span>

![Assets option](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="9350a-165">Encrypt with AES or DRM</span><span class="sxs-lookup"><span data-stu-id="9350a-165">Encrypt with AES or DRM</span></span>
<span data-ttu-id="9350a-166">When you select **Encrypt** for an asset, you see two choices: **AES** or **DRM**.</span><span class="sxs-lookup"><span data-stu-id="9350a-166">When you select **Encrypt** for an asset, you see two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="9350a-167">AES</span><span class="sxs-lookup"><span data-stu-id="9350a-167">AES</span></span>
<span data-ttu-id="9350a-168">AES clear key encryption is enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="9350a-168">AES clear key encryption is enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Encryption configuration](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="9350a-170">DRM</span><span class="sxs-lookup"><span data-stu-id="9350a-170">DRM</span></span>
1. <span data-ttu-id="9350a-171">After you select **DRM**, you see different content protection policies (which must be configured by this point) and a set of streaming protocols:</span><span class="sxs-lookup"><span data-stu-id="9350a-171">After you select **DRM**, you see different content protection policies (which must be configured by this point) and a set of streaming protocols:</span></span>

    <span data-ttu-id="9350a-172">a.</span><span class="sxs-lookup"><span data-stu-id="9350a-172">a.</span></span> <span data-ttu-id="9350a-173">**PlayReady and Widevine with MPEG-DASH** dynamically encrypts your MPEG-DASH stream with PlayReady and Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="9350a-173">**PlayReady and Widevine with MPEG-DASH** dynamically encrypts your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>

    <span data-ttu-id="9350a-174">b.</span><span class="sxs-lookup"><span data-stu-id="9350a-174">b.</span></span> <span data-ttu-id="9350a-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="9350a-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="9350a-176">This option also encrypts your HLS streams with FairPlay.</span><span class="sxs-lookup"><span data-stu-id="9350a-176">This option also encrypts your HLS streams with FairPlay.</span></span>

    <span data-ttu-id="9350a-177">c.</span><span class="sxs-lookup"><span data-stu-id="9350a-177">c.</span></span> <span data-ttu-id="9350a-178">**PlayReady only with Smooth Streaming, HLS, and MPEG-DASH** dynamically encrypts Smooth Streaming, HLS, and MPEG-DASH streams with PlayReady DRM.</span><span class="sxs-lookup"><span data-stu-id="9350a-178">**PlayReady only with Smooth Streaming, HLS, and MPEG-DASH** dynamically encrypts Smooth Streaming, HLS, and MPEG-DASH streams with PlayReady DRM.</span></span>

    <span data-ttu-id="9350a-179">d.</span><span class="sxs-lookup"><span data-stu-id="9350a-179">d.</span></span> <span data-ttu-id="9350a-180">**Widevine only with MPEG-DASH** dynamically encrypts your MPEG-DASH with Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="9350a-180">**Widevine only with MPEG-DASH** dynamically encrypts your MPEG-DASH with Widevine DRM.</span></span>
    
    <span data-ttu-id="9350a-181">e.</span><span class="sxs-lookup"><span data-stu-id="9350a-181">e.</span></span> <span data-ttu-id="9350a-182">**FairPlay only with HLS** dynamically encrypts your HLS stream with FairPlay.</span><span class="sxs-lookup"><span data-stu-id="9350a-182">**FairPlay only with HLS** dynamically encrypts your HLS stream with FairPlay.</span></span>

1. <span data-ttu-id="9350a-183">To enable FairPlay encryption, on the **Content Protection Global Settings** blade, select **FairPlay configuration**.</span><span class="sxs-lookup"><span data-stu-id="9350a-183">To enable FairPlay encryption, on the **Content Protection Global Settings** blade, select **FairPlay configuration**.</span></span> <span data-ttu-id="9350a-184">Then select the **App certificate**, and enter the **Application Secret Key**.</span><span class="sxs-lookup"><span data-stu-id="9350a-184">Then select the **App certificate**, and enter the **Application Secret Key**.</span></span>

    ![Encryption type](./media/media-services-portal-content-protection/media-services-content-protection009.png)

1. <span data-ttu-id="9350a-186">After you make the encryption selection, select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="9350a-186">After you make the encryption selection, select **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="9350a-187">If you plan to play an AES-encrypted HLS in Safari, see the blog post [Encrypted HLS in Safari](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="9350a-187">If you plan to play an AES-encrypted HLS in Safari, see the blog post [Encrypted HLS in Safari](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9350a-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="9350a-188">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9350a-189">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="9350a-189">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

