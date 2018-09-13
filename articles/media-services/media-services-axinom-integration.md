---
title: Using Axinom to deliver Widevine licenses to Azure Media Services | Microsoft Docs
description: This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs. The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by Axinom license server.
services: media-services
documentationcenter: ''
author: willzhan
manager: erikre
editor: ''
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 63d037738d0d9c46ab84c4ef1eaecd9843ccbc6e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555247"
---
# <a name="using-axinom-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="59873-104">Using Axinom to deliver Widevine licenses to Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="59873-104">Using Axinom to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [castLabs](media-services-castlabs-integration.md)
> * [Axinom](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="59873-107">Overview</span><span class="sxs-lookup"><span data-stu-id="59873-107">Overview</span></span>
<span data-ttu-id="59873-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span><span class="sxs-lookup"><span data-stu-id="59873-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="59873-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span><span class="sxs-lookup"><span data-stu-id="59873-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="59873-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span><span class="sxs-lookup"><span data-stu-id="59873-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="59873-111">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span><span class="sxs-lookup"><span data-stu-id="59873-111">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="59873-112">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="59873-112">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="59873-113">This article describes how to integrate and test Widevine license server managed by Axinom.</span><span class="sxs-lookup"><span data-stu-id="59873-113">This article describes how to integrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="59873-114">Specifically, it covers:</span><span class="sxs-lookup"><span data-stu-id="59873-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="59873-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span><span class="sxs-lookup"><span data-stu-id="59873-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="59873-116">Generating a JWT token in order to meet the license server requirements;</span><span class="sxs-lookup"><span data-stu-id="59873-116">Generating a JWT token in order to meet the license server requirements;</span></span>
* <span data-ttu-id="59873-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span><span class="sxs-lookup"><span data-stu-id="59873-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="59873-118">The complete system and the flow of content key, key ID, key seed, JTW token and its claims can be best described by the following diagram.</span><span class="sxs-lookup"><span data-stu-id="59873-118">The complete system and the flow of content key, key ID, key seed, JTW token and its claims can be best described by the following diagram.</span></span>

![DASH and CENC](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="59873-120">Content Protection</span><span class="sxs-lookup"><span data-stu-id="59873-120">Content Protection</span></span>
<span data-ttu-id="59873-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How to configure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span><span class="sxs-lookup"><span data-stu-id="59873-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How to configure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="59873-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of the following:</span><span class="sxs-lookup"><span data-stu-id="59873-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of the following:</span></span>

1. <span data-ttu-id="59873-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span><span class="sxs-lookup"><span data-stu-id="59873-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="59873-124">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="59873-124">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="59873-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span><span class="sxs-lookup"><span data-stu-id="59873-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="59873-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span><span class="sxs-lookup"><span data-stu-id="59873-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="59873-127">Considerations</span><span class="sxs-lookup"><span data-stu-id="59873-127">Considerations</span></span>
1. <span data-ttu-id="59873-128">You must use the Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID to generate the content key for configuring key delivery service.</span><span class="sxs-lookup"><span data-stu-id="59873-128">You must use the Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID to generate the content key for configuring key delivery service.</span></span> <span data-ttu-id="59873-129">Axinom license server will issue all licenses containing content keys based on the same key seed, which is valid for both testing and production.</span><span class="sxs-lookup"><span data-stu-id="59873-129">Axinom license server will issue all licenses containing content keys based on the same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="59873-130">The Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="59873-130">The Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="59873-131">Both HTTP and HTTS are allowed.</span><span class="sxs-lookup"><span data-stu-id="59873-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="59873-132">Azure Media Player Preparation</span><span class="sxs-lookup"><span data-stu-id="59873-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="59873-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="59873-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="59873-134">If Widevine license server does not require token authentication, there is nothing additional you need to do to test a DASH content protected by Widevine.</span><span class="sxs-lookup"><span data-stu-id="59873-134">If Widevine license server does not require token authentication, there is nothing additional you need to do to test a DASH content protected by Widevine.</span></span> <span data-ttu-id="59873-135">For an example, the AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span><span class="sxs-lookup"><span data-stu-id="59873-135">For an example, the AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="59873-136">The Widevine license server provided by Axinom requires JWT token authentication.</span><span class="sxs-lookup"><span data-stu-id="59873-136">The Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="59873-137">The JWT token needs to be submitted with license request through an HTTP header “X-AxDRM-Message”.</span><span class="sxs-lookup"><span data-stu-id="59873-137">The JWT token needs to be submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="59873-138">For this purpose, you need to add the following javascript in the web page hosting AMP before setting the source:</span><span class="sxs-lookup"><span data-stu-id="59873-138">For this purpose, you need to add the following javascript in the web page hosting AMP before setting the source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="59873-139">The rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="59873-139">The rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="59873-140">Note that the above javascript for setting custom authorization header is still a short term approach before the official long term approach in AMP is released.</span><span class="sxs-lookup"><span data-stu-id="59873-140">Note that the above javascript for setting custom authorization header is still a short term approach before the official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="59873-141">JWT Token Generation</span><span class="sxs-lookup"><span data-stu-id="59873-141">JWT Token Generation</span></span>
<span data-ttu-id="59873-142">Axinom Widevine license server for testing requires JWT token authentication.</span><span class="sxs-lookup"><span data-stu-id="59873-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="59873-143">In addition, one of the claims in the JWT token is of a complex object type instead of primitive data type.</span><span class="sxs-lookup"><span data-stu-id="59873-143">In addition, one of the claims in the JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="59873-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span><span class="sxs-lookup"><span data-stu-id="59873-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="59873-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you to input complex object type as claims.</span><span class="sxs-lookup"><span data-stu-id="59873-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you to input complex object type as claims.</span></span> <span data-ttu-id="59873-146">However, the claims are still serialized as string.</span><span class="sxs-lookup"><span data-stu-id="59873-146">However, the claims are still serialized as string.</span></span> <span data-ttu-id="59873-147">Therefore we cannot use any of the two for generating the JWT token for Widevine license request.</span><span class="sxs-lookup"><span data-stu-id="59873-147">Therefore we cannot use any of the two for generating the JWT token for Widevine license request.</span></span>

<span data-ttu-id="59873-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets the needs so we are going to use this Nuget package.</span><span class="sxs-lookup"><span data-stu-id="59873-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets the needs so we are going to use this Nuget package.</span></span>

<span data-ttu-id="59873-149">Below is the code for generating JWT token with the needed claims as required by Axinom Widevine license server for testing:</span><span class="sxs-lookup"><span data-stu-id="59873-149">Below is the code for generating JWT token with the needed claims as required by Axinom Widevine license server for testing:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string to byte[] Note: Note that the key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string to byte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "The binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

<span data-ttu-id="59873-150">Axinom Widevine license server</span><span class="sxs-lookup"><span data-stu-id="59873-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="59873-151">Considerations</span><span class="sxs-lookup"><span data-stu-id="59873-151">Considerations</span></span>
1. <span data-ttu-id="59873-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span><span class="sxs-lookup"><span data-stu-id="59873-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="59873-153">The Axinom communication key is used as signing key.</span><span class="sxs-lookup"><span data-stu-id="59873-153">The Axinom communication key is used as signing key.</span></span> <span data-ttu-id="59873-154">Note that the key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span><span class="sxs-lookup"><span data-stu-id="59873-154">Note that the key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="59873-155">This is achieved by the method ConvertHexStringToByteArray.</span><span class="sxs-lookup"><span data-stu-id="59873-155">This is achieved by the method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="59873-156">Retrieving Key ID</span><span class="sxs-lookup"><span data-stu-id="59873-156">Retrieving Key ID</span></span>
<span data-ttu-id="59873-157">You may have noticed that in the code for generating a JWT token, key ID is required.</span><span class="sxs-lookup"><span data-stu-id="59873-157">You may have noticed that in the code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="59873-158">Since the JWT token needs to be ready before loading AMP player, key ID needs to be retrieved in order to generate JWT token.</span><span class="sxs-lookup"><span data-stu-id="59873-158">Since the JWT token needs to be ready before loading AMP player, key ID needs to be retrieved in order to generate JWT token.</span></span>

<span data-ttu-id="59873-159">Of course there are multiple ways to get hold of key ID.</span><span class="sxs-lookup"><span data-stu-id="59873-159">Of course there are multiple ways to get hold of key ID.</span></span> <span data-ttu-id="59873-160">For example, one may store key ID together with content metadata in a database.</span><span class="sxs-lookup"><span data-stu-id="59873-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="59873-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span><span class="sxs-lookup"><span data-stu-id="59873-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="59873-162">The code below is for the latter.</span><span class="sxs-lookup"><span data-stu-id="59873-162">The code below is for the latter.</span></span>

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a><span data-ttu-id="59873-163">Summary</span><span class="sxs-lookup"><span data-stu-id="59873-163">Summary</span></span>
<span data-ttu-id="59873-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able to implement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for the following modern browsers:</span><span class="sxs-lookup"><span data-stu-id="59873-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able to implement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for the following modern browsers:</span></span>

* <span data-ttu-id="59873-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="59873-165">Chrome</span></span>
* <span data-ttu-id="59873-166">Microsoft Edge on Windows 10</span><span class="sxs-lookup"><span data-stu-id="59873-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="59873-167">IE 11 on Windows 8.1 and Windows 10</span><span class="sxs-lookup"><span data-stu-id="59873-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="59873-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and the same URL with Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="59873-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and the same URL with Azure Media Player</span></span>

<span data-ttu-id="59873-169">The following parameters are required in the mini-solution leveraging Axinom Widevine license server.</span><span class="sxs-lookup"><span data-stu-id="59873-169">The following parameters are required in the mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="59873-170">Except for key ID, the rest of parameters are provided by Axinom based on their Widevine server setup.</span><span class="sxs-lookup"><span data-stu-id="59873-170">Except for key ID, the rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="59873-171">Parameter</span><span class="sxs-lookup"><span data-stu-id="59873-171">Parameter</span></span> | <span data-ttu-id="59873-172">How it is used</span><span class="sxs-lookup"><span data-stu-id="59873-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="59873-173">Communication key ID</span><span class="sxs-lookup"><span data-stu-id="59873-173">Communication key ID</span></span> |<span data-ttu-id="59873-174">Must be included as value of the claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span><span class="sxs-lookup"><span data-stu-id="59873-174">Must be included as value of the claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="59873-175">Communication key</span><span class="sxs-lookup"><span data-stu-id="59873-175">Communication key</span></span> |<span data-ttu-id="59873-176">Must be used as the signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span><span class="sxs-lookup"><span data-stu-id="59873-176">Must be used as the signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="59873-177">Key seed</span><span class="sxs-lookup"><span data-stu-id="59873-177">Key seed</span></span> |<span data-ttu-id="59873-178">Must be used to generate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span><span class="sxs-lookup"><span data-stu-id="59873-178">Must be used to generate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="59873-179">Widevine License acquisition URL</span><span class="sxs-lookup"><span data-stu-id="59873-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="59873-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span><span class="sxs-lookup"><span data-stu-id="59873-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="59873-181">Content Key ID</span><span class="sxs-lookup"><span data-stu-id="59873-181">Content Key ID</span></span> |<span data-ttu-id="59873-182">Must be included as part of the value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span><span class="sxs-lookup"><span data-stu-id="59873-182">Must be included as part of the value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="59873-183">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="59873-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="59873-184">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="59873-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="59873-185">Acknowledgments</span><span class="sxs-lookup"><span data-stu-id="59873-185">Acknowledgments</span></span>
<span data-ttu-id="59873-186">We would like to acknowledge the following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span><span class="sxs-lookup"><span data-stu-id="59873-186">We would like to acknowledge the following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>


