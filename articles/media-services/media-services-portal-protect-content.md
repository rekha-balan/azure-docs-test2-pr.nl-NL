---
title: Configuring content protection policies using the Azure portal | Microsoft Docs
description: This article demonstrates how to use the Azure portal to configure content protection policies. The article also shows how to enable dynamic encryption for your assets.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako
ms.openlocfilehash: c7cf46057bf1fa4cc0333c814433477e4c85ff2f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552061"
---
# <a name="configuring-content-protection-policies-using-the-azure-portal"></a><span data-ttu-id="3c66c-104">Configuring content protection policies using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3c66c-104">Configuring content protection policies using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="3c66c-105">To complete this tutorial, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="3c66c-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="3c66c-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c66c-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="3c66c-107">Overview</span><span class="sxs-lookup"><span data-stu-id="3c66c-107">Overview</span></span>
<span data-ttu-id="3c66c-108">Microsoft Azure Media Services (AMS) enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span><span class="sxs-lookup"><span data-stu-id="3c66c-108">Microsoft Azure Media Services (AMS) enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="3c66c-109">Media Services allows you to deliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="3c66c-109">Media Services allows you to deliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="3c66c-110">AMS provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span><span class="sxs-lookup"><span data-stu-id="3c66c-110">AMS provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="3c66c-111">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span><span class="sxs-lookup"><span data-stu-id="3c66c-111">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="3c66c-112">This article demonstrates how to configure content protection policies with the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3c66c-112">This article demonstrates how to configure content protection policies with the Azure portal.</span></span> <span data-ttu-id="3c66c-113">The article also shows how to apply dynamic encryption to your assets.</span><span class="sxs-lookup"><span data-stu-id="3c66c-113">The article also shows how to apply dynamic encryption to your assets.</span></span>


> [!NOTE]
> <span data-ttu-id="3c66c-114">If you used the Azure classic portal to create protection policies, the policies may not appear in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3c66c-114">If you used the Azure classic portal to create protection policies, the policies may not appear in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="3c66c-115">However, all the old polices still exist.</span><span class="sxs-lookup"><span data-stu-id="3c66c-115">However, all the old polices still exist.</span></span> <span data-ttu-id="3c66c-116">You can examine them using the Azure Media Services .NET SDK or the [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (to see the policies, right-click on the asset -> Display information (F4)->click on Content keys tab-> click on the key).</span><span class="sxs-lookup"><span data-stu-id="3c66c-116">You can examine them using the Azure Media Services .NET SDK or the [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (to see the policies, right-click on the asset -> Display information (F4)->click on Content keys tab-> click on the key).</span></span> 
> 
> <span data-ttu-id="3c66c-117">If you want to encrypt your asset using new policies, configure them with the Azure portal, click save, and reapply dynamic encryption.</span><span class="sxs-lookup"><span data-stu-id="3c66c-117">If you want to encrypt your asset using new policies, configure them with the Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="3c66c-118">Start configuring content protection</span><span class="sxs-lookup"><span data-stu-id="3c66c-118">Start configuring content protection</span></span>
<span data-ttu-id="3c66c-119">To use the portal to start configuring content protection, global to your AMS account, do the following:</span><span class="sxs-lookup"><span data-stu-id="3c66c-119">To use the portal to start configuring content protection, global to your AMS account, do the following:</span></span>

1. <span data-ttu-id="3c66c-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="3c66c-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="3c66c-121">Select **Settings** > **Content protection**.</span><span class="sxs-lookup"><span data-stu-id="3c66c-121">Select **Settings** > **Content protection**.</span></span>

![Protect content](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="3c66c-123">Key/license authorization policy</span><span class="sxs-lookup"><span data-stu-id="3c66c-123">Key/license authorization policy</span></span>
<span data-ttu-id="3c66c-124">AMS supports multiple ways of authenticating users who make key or license requests.</span><span class="sxs-lookup"><span data-stu-id="3c66c-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="3c66c-125">The content key authorization policy must be configured by you and met by your client in order for the key/license to be delived to the client.</span><span class="sxs-lookup"><span data-stu-id="3c66c-125">The content key authorization policy must be configured by you and met by your client in order for the key/license to be delived to the client.</span></span> <span data-ttu-id="3c66c-126">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span><span class="sxs-lookup"><span data-stu-id="3c66c-126">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="3c66c-127">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span><span class="sxs-lookup"><span data-stu-id="3c66c-127">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="3c66c-128">Open</span><span class="sxs-lookup"><span data-stu-id="3c66c-128">Open</span></span>
<span data-ttu-id="3c66c-129">Open restriction means that the system will deliver the key to anyone who makes a key request.</span><span class="sxs-lookup"><span data-stu-id="3c66c-129">Open restriction means that the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="3c66c-130">This restriction might be useful for test purposes.</span><span class="sxs-lookup"><span data-stu-id="3c66c-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="3c66c-131">Token</span><span class="sxs-lookup"><span data-stu-id="3c66c-131">Token</span></span>
<span data-ttu-id="3c66c-132">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="3c66c-132">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="3c66c-133">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span><span class="sxs-lookup"><span data-stu-id="3c66c-133">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="3c66c-134">Media Services does not provide Secure Token Services.</span><span class="sxs-lookup"><span data-stu-id="3c66c-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="3c66c-135">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span><span class="sxs-lookup"><span data-stu-id="3c66c-135">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="3c66c-136">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span><span class="sxs-lookup"><span data-stu-id="3c66c-136">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="3c66c-137">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span><span class="sxs-lookup"><span data-stu-id="3c66c-137">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span></span>

<span data-ttu-id="3c66c-138">When configuring the token restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span><span class="sxs-lookup"><span data-stu-id="3c66c-138">When configuring the token restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="3c66c-139">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span><span class="sxs-lookup"><span data-stu-id="3c66c-139">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="3c66c-140">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span><span class="sxs-lookup"><span data-stu-id="3c66c-140">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="3c66c-141">The Media Services key delivery service validates that these values in the token match the values in the template.</span><span class="sxs-lookup"><span data-stu-id="3c66c-141">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

![Protect content](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="3c66c-143">PlayReady rights template</span><span class="sxs-lookup"><span data-stu-id="3c66c-143">PlayReady rights template</span></span>
<span data-ttu-id="3c66c-144">For detailed information about the PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3c66c-144">For detailed information about the PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="3c66c-145">Non persistent</span><span class="sxs-lookup"><span data-stu-id="3c66c-145">Non persistent</span></span>
<span data-ttu-id="3c66c-146">If you configure license as non-persistent, it is only held in memory while the player is using the license.</span><span class="sxs-lookup"><span data-stu-id="3c66c-146">If you configure license as non-persistent, it is only held in memory while the player is using the license.</span></span>  

![Protect content](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="3c66c-148">Persistent</span><span class="sxs-lookup"><span data-stu-id="3c66c-148">Persistent</span></span>
<span data-ttu-id="3c66c-149">If you configure the license  as persistent, it is saved in persistent storage on the client.</span><span class="sxs-lookup"><span data-stu-id="3c66c-149">If you configure the license  as persistent, it is saved in persistent storage on the client.</span></span>

![Protect content](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="3c66c-151">Widevine rights template</span><span class="sxs-lookup"><span data-stu-id="3c66c-151">Widevine rights template</span></span>
<span data-ttu-id="3c66c-152">For detailed information about the Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3c66c-152">For detailed information about the Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="3c66c-153">Basic</span><span class="sxs-lookup"><span data-stu-id="3c66c-153">Basic</span></span>
<span data-ttu-id="3c66c-154">When you select **Basic**, the template will be created with all defaults values.</span><span class="sxs-lookup"><span data-stu-id="3c66c-154">When you select **Basic**, the template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="3c66c-155">Advanced</span><span class="sxs-lookup"><span data-stu-id="3c66c-155">Advanced</span></span>
<span data-ttu-id="3c66c-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span><span class="sxs-lookup"><span data-stu-id="3c66c-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Protect content](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="3c66c-158">FairPlay configuration</span><span class="sxs-lookup"><span data-stu-id="3c66c-158">FairPlay configuration</span></span>
<span data-ttu-id="3c66c-159">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option.</span><span class="sxs-lookup"><span data-stu-id="3c66c-159">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option.</span></span> <span data-ttu-id="3c66c-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span><span class="sxs-lookup"><span data-stu-id="3c66c-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Protect content](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-to-your-asset"></a><span data-ttu-id="3c66c-162">Apply dynamic encryption to your asset</span><span class="sxs-lookup"><span data-stu-id="3c66c-162">Apply dynamic encryption to your asset</span></span>
<span data-ttu-id="3c66c-163">To take advantage of dynamic encryption, you need to encode your source file into a set of adaptive-bitrate MP4 files.</span><span class="sxs-lookup"><span data-stu-id="3c66c-163">To take advantage of dynamic encryption, you need to encode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-to-encrypt"></a><span data-ttu-id="3c66c-164">Select an asset that you want to encrypt</span><span class="sxs-lookup"><span data-stu-id="3c66c-164">Select an asset that you want to encrypt</span></span>
<span data-ttu-id="3c66c-165">To see all your assets, select **Settings** > **Assets**.</span><span class="sxs-lookup"><span data-stu-id="3c66c-165">To see all your assets, select **Settings** > **Assets**.</span></span>

![Protect content](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="3c66c-167">Encrypt with AES or DRM</span><span class="sxs-lookup"><span data-stu-id="3c66c-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="3c66c-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span><span class="sxs-lookup"><span data-stu-id="3c66c-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="3c66c-169">AES</span><span class="sxs-lookup"><span data-stu-id="3c66c-169">AES</span></span>
<span data-ttu-id="3c66c-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="3c66c-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Protect content](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="3c66c-172">DRM</span><span class="sxs-lookup"><span data-stu-id="3c66c-172">DRM</span></span>
<span data-ttu-id="3c66c-173">When you select the DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span><span class="sxs-lookup"><span data-stu-id="3c66c-173">When you select the DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="3c66c-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="3c66c-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="3c66c-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="3c66c-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="3c66c-176">Will also encrypt your HLS streams with FairPlay.</span><span class="sxs-lookup"><span data-stu-id="3c66c-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="3c66c-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span><span class="sxs-lookup"><span data-stu-id="3c66c-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="3c66c-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="3c66c-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="3c66c-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span><span class="sxs-lookup"><span data-stu-id="3c66c-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="3c66c-180">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option of the Content Protection settings blade.</span><span class="sxs-lookup"><span data-stu-id="3c66c-180">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option of the Content Protection settings blade.</span></span>

![Protect content](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="3c66c-182">Once you make the encryption selection, press **Apply**.</span><span class="sxs-lookup"><span data-stu-id="3c66c-182">Once you make the encryption selection, press **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c66c-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c66c-183">Next steps</span></span>
<span data-ttu-id="3c66c-184">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="3c66c-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3c66c-185">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="3c66c-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]










