---
title: Configure a content key authorization policy by using the Media Services .NET SDK | Microsoft Docs
description: Learn how to configure an authorization policy for a content key by using the Media Services .NET SDK.
services: media-services
documentationcenter: ''
author: mingfeiy
manager: cfowler
editor: ''
ms.assetid: 1a0aedda-5b87-4436-8193-09fc2f14310c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: 531b90b905df8549846c6027fe547521d16cf082
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864693"
---
# <a name="dynamic-encryption-configure-a-content-key-authorization-policy"></a><span data-ttu-id="826ec-103">Dynamic encryption: Configure a content key authorization policy</span><span class="sxs-lookup"><span data-stu-id="826ec-103">Dynamic encryption: Configure a content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="826ec-104">Overview</span><span class="sxs-lookup"><span data-stu-id="826ec-104">Overview</span></span>
 <span data-ttu-id="826ec-105">You can use Azure Media Services to deliver MPEG-DASH, Smooth Streaming, and HTTP Live Streaming (HLS) streams protected with the Advanced Encryption Standard (AES) by using 128-bit encryption keys or [PlayReady digital rights management (DRM)](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="826ec-105">You can use Azure Media Services to deliver MPEG-DASH, Smooth Streaming, and HTTP Live Streaming (HLS) streams protected with the Advanced Encryption Standard (AES) by using 128-bit encryption keys or [PlayReady digital rights management (DRM)](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="826ec-106">With Media Services, you also can deliver DASH streams encrypted with Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="826ec-106">With Media Services, you also can deliver DASH streams encrypted with Widevine DRM.</span></span> <span data-ttu-id="826ec-107">Both PlayReady and Widevine are encrypted per the common encryption (ISO/IEC 23001-7 CENC) specification.</span><span class="sxs-lookup"><span data-stu-id="826ec-107">Both PlayReady and Widevine are encrypted per the common encryption (ISO/IEC 23001-7 CENC) specification.</span></span>

<span data-ttu-id="826ec-108">Media Services also provides a key/license delivery service from which clients can obtain AES keys or PlayReady/Widevine licenses to play the encrypted content.</span><span class="sxs-lookup"><span data-stu-id="826ec-108">Media Services also provides a key/license delivery service from which clients can obtain AES keys or PlayReady/Widevine licenses to play the encrypted content.</span></span>

<span data-ttu-id="826ec-109">If you want Media Services to encrypt an asset, you need to associate an encryption key (CommonEncryption or EnvelopeEncryption) with the asset.</span><span class="sxs-lookup"><span data-stu-id="826ec-109">If you want Media Services to encrypt an asset, you need to associate an encryption key (CommonEncryption or EnvelopeEncryption) with the asset.</span></span> <span data-ttu-id="826ec-110">For more information, see [Create ContentKeys with .NET](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="826ec-110">For more information, see [Create ContentKeys with .NET](media-services-dotnet-create-contentkey.md).</span></span> <span data-ttu-id="826ec-111">You also need to configure authorization policies for the key (as described in this article).</span><span class="sxs-lookup"><span data-stu-id="826ec-111">You also need to configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="826ec-112">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content by using AES or DRM encryption.</span><span class="sxs-lookup"><span data-stu-id="826ec-112">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content by using AES or DRM encryption.</span></span> <span data-ttu-id="826ec-113">To decrypt the stream, the player requests the key from the key delivery service.</span><span class="sxs-lookup"><span data-stu-id="826ec-113">To decrypt the stream, the player requests the key from the key delivery service.</span></span> <span data-ttu-id="826ec-114">To determine whether the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span><span class="sxs-lookup"><span data-stu-id="826ec-114">To determine whether the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="826ec-115">Media Services supports multiple ways of authenticating users who make key requests.</span><span class="sxs-lookup"><span data-stu-id="826ec-115">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="826ec-116">The content key authorization policy can have one or more authorization restrictions.</span><span class="sxs-lookup"><span data-stu-id="826ec-116">The content key authorization policy can have one or more authorization restrictions.</span></span> <span data-ttu-id="826ec-117">The options are open or token restriction.</span><span class="sxs-lookup"><span data-stu-id="826ec-117">The options are open or token restriction.</span></span> <span data-ttu-id="826ec-118">The token-restricted policy must be accompanied by a token issued by a security token service (STS).</span><span class="sxs-lookup"><span data-stu-id="826ec-118">The token-restricted policy must be accompanied by a token issued by a security token service (STS).</span></span> <span data-ttu-id="826ec-119">Media Services supports tokens in the simple web token ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and the JSON Web Token ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span><span class="sxs-lookup"><span data-stu-id="826ec-119">Media Services supports tokens in the simple web token ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and the JSON Web Token ([JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3)) format.</span></span>

<span data-ttu-id="826ec-120">Media Services doesn't provide STS.</span><span class="sxs-lookup"><span data-stu-id="826ec-120">Media Services doesn't provide STS.</span></span> <span data-ttu-id="826ec-121">You can create a custom STS or use Azure Access Control Service to issue tokens.</span><span class="sxs-lookup"><span data-stu-id="826ec-121">You can create a custom STS or use Azure Access Control Service to issue tokens.</span></span> <span data-ttu-id="826ec-122">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span><span class="sxs-lookup"><span data-stu-id="826ec-122">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="826ec-123">If the token is valid and the claims in the token match those configured for the content key, the Media Services key delivery service returns the encryption key to the client.</span><span class="sxs-lookup"><span data-stu-id="826ec-123">If the token is valid and the claims in the token match those configured for the content key, the Media Services key delivery service returns the encryption key to the client.</span></span>

<span data-ttu-id="826ec-124">For more information, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="826ec-124">For more information, see the following articles:</span></span>

- [<span data-ttu-id="826ec-125">JWT token authentication</span><span class="sxs-lookup"><span data-stu-id="826ec-125">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)
- [<span data-ttu-id="826ec-126">Integrate Azure Media Services OWIN MVC-based app with Azure Active Directory and restrict content key delivery based on JWT claims</span><span class="sxs-lookup"><span data-stu-id="826ec-126">Integrate Azure Media Services OWIN MVC-based app with Azure Active Directory and restrict content key delivery based on JWT claims</span></span>](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)

### <a name="some-considerations-apply"></a><span data-ttu-id="826ec-127">Some considerations apply</span><span class="sxs-lookup"><span data-stu-id="826ec-127">Some considerations apply</span></span>
* <span data-ttu-id="826ec-128">When your Media Services account is created, a default streaming endpoint is added to your account in the "Stopped" state.</span><span class="sxs-lookup"><span data-stu-id="826ec-128">When your Media Services account is created, a default streaming endpoint is added to your account in the "Stopped" state.</span></span> <span data-ttu-id="826ec-129">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint must be in the "Running" state.</span><span class="sxs-lookup"><span data-stu-id="826ec-129">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, your streaming endpoint must be in the "Running" state.</span></span> 
* <span data-ttu-id="826ec-130">Your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span><span class="sxs-lookup"><span data-stu-id="826ec-130">Your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="826ec-131">For more information, see [Encode an asset](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="826ec-131">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="826ec-132">Upload and encode your assets by using the AssetCreationOptions.StorageEncrypted option.</span><span class="sxs-lookup"><span data-stu-id="826ec-132">Upload and encode your assets by using the AssetCreationOptions.StorageEncrypted option.</span></span>
* <span data-ttu-id="826ec-133">If you plan to have multiple content keys that require the same policy configuration, we recommend that you create a single authorization policy and reuse it with multiple content keys.</span><span class="sxs-lookup"><span data-stu-id="826ec-133">If you plan to have multiple content keys that require the same policy configuration, we recommend that you create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="826ec-134">The key delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="826ec-134">The key delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span> <span data-ttu-id="826ec-135">You can create ContentKeyAuthorizationPolicy and specify to use a token restriction, test it, and then update the policy to the open restriction.</span><span class="sxs-lookup"><span data-stu-id="826ec-135">You can create ContentKeyAuthorizationPolicy and specify to use a token restriction, test it, and then update the policy to the open restriction.</span></span> <span data-ttu-id="826ec-136">This process takes roughly 15 minutes before the policy switches to the open version of the policy.</span><span class="sxs-lookup"><span data-stu-id="826ec-136">This process takes roughly 15 minutes before the policy switches to the open version of the policy.</span></span>
* <span data-ttu-id="826ec-137">If you add or update your asset's delivery policy, you must delete any existing locator and create a new locator.</span><span class="sxs-lookup"><span data-stu-id="826ec-137">If you add or update your asset's delivery policy, you must delete any existing locator and create a new locator.</span></span>
* <span data-ttu-id="826ec-138">Currently, you can't encrypt progressive downloads.</span><span class="sxs-lookup"><span data-stu-id="826ec-138">Currently, you can't encrypt progressive downloads.</span></span>
* <span data-ttu-id="826ec-139">A Media Services streaming endpoint sets the value of the CORS 'Access-Control-Allow-Origin' header in preflight response as the wildcard '\*'.</span><span class="sxs-lookup"><span data-stu-id="826ec-139">A Media Services streaming endpoint sets the value of the CORS 'Access-Control-Allow-Origin' header in preflight response as the wildcard '\*'.</span></span> <span data-ttu-id="826ec-140">This value works well with most players, including Azure Media Player, Roku and JWPlayer, and others.</span><span class="sxs-lookup"><span data-stu-id="826ec-140">This value works well with most players, including Azure Media Player, Roku and JWPlayer, and others.</span></span> <span data-ttu-id="826ec-141">However, some players that use dashjs don't work because, with the credentials mode set to "include", XMLHttpRequest in their dashjs doesn't allow the wildcard "\*" as the value of 'Access-Control-Allow-Origin'.</span><span class="sxs-lookup"><span data-stu-id="826ec-141">However, some players that use dashjs don't work because, with the credentials mode set to "include", XMLHttpRequest in their dashjs doesn't allow the wildcard "\*" as the value of 'Access-Control-Allow-Origin'.</span></span> <span data-ttu-id="826ec-142">As a workaround to this limitation in dashjs, if you host your client from a single domain, Media Services can specify that domain in the preflight response header.</span><span class="sxs-lookup"><span data-stu-id="826ec-142">As a workaround to this limitation in dashjs, if you host your client from a single domain, Media Services can specify that domain in the preflight response header.</span></span> <span data-ttu-id="826ec-143">For assistance, open a support ticket through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="826ec-143">For assistance, open a support ticket through the Azure portal.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="826ec-144">AES-128 dynamic encryption</span><span class="sxs-lookup"><span data-stu-id="826ec-144">AES-128 dynamic encryption</span></span>
### <a name="open-restriction"></a><span data-ttu-id="826ec-145">Open restriction</span><span class="sxs-lookup"><span data-stu-id="826ec-145">Open restriction</span></span>
<span data-ttu-id="826ec-146">Open restriction means the system delivers the key to anyone who makes a key request.</span><span class="sxs-lookup"><span data-stu-id="826ec-146">Open restriction means the system delivers the key to anyone who makes a key request.</span></span> <span data-ttu-id="826ec-147">This restriction might be useful for testing purposes.</span><span class="sxs-lookup"><span data-stu-id="826ec-147">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="826ec-148">The following example creates an open authorization policy and adds it to the content key:</span><span class="sxs-lookup"><span data-stu-id="826ec-148">The following example creates an open authorization policy and adds it to the content key:</span></span>
```csharp
    static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
    {
        // Create ContentKeyAuthorizationPolicy with Open restrictions
        // and create authorization policy
        IContentKeyAuthorizationPolicy policy = _context.
        ContentKeyAuthorizationPolicies.
        CreateAsync("Open Authorization Policy").Result;
        
        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "HLS Open Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                Requirements = null // no requirements needed for HLS
            };

        restrictions.Add(restriction);

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy", 
            ContentKeyDeliveryType.BaselineHttp, 
            restrictions, 
            "");

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
    }
```

### <a name="token-restriction"></a><span data-ttu-id="826ec-149">Token restriction</span><span class="sxs-lookup"><span data-stu-id="826ec-149">Token restriction</span></span>
<span data-ttu-id="826ec-150">This section describes how to create a content key authorization policy and associate it with the content key.</span><span class="sxs-lookup"><span data-stu-id="826ec-150">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="826ec-151">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key.</span><span class="sxs-lookup"><span data-stu-id="826ec-151">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key.</span></span> <span data-ttu-id="826ec-152">For example, does the verification key list contain the key that the token was signed with?</span><span class="sxs-lookup"><span data-stu-id="826ec-152">For example, does the verification key list contain the key that the token was signed with?</span></span>

<span data-ttu-id="826ec-153">To configure the token restriction option, you need to use an XML to describe the token's authorization requirements.</span><span class="sxs-lookup"><span data-stu-id="826ec-153">To configure the token restriction option, you need to use an XML to describe the token's authorization requirements.</span></span> <span data-ttu-id="826ec-154">The token restriction configuration XML must conform to the following XML schema:</span><span class="sxs-lookup"><span data-stu-id="826ec-154">The token restriction configuration XML must conform to the following XML schema:</span></span>
```csharp
#### Token restriction schema
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>
```
<span data-ttu-id="826ec-155">When you configure the token-restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span><span class="sxs-lookup"><span data-stu-id="826ec-155">When you configure the token-restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="826ec-156">The primary verification key contains the key that the token was signed with.</span><span class="sxs-lookup"><span data-stu-id="826ec-156">The primary verification key contains the key that the token was signed with.</span></span> <span data-ttu-id="826ec-157">The issuer is the STS that issues the token.</span><span class="sxs-lookup"><span data-stu-id="826ec-157">The issuer is the STS that issues the token.</span></span> <span data-ttu-id="826ec-158">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span><span class="sxs-lookup"><span data-stu-id="826ec-158">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="826ec-159">The Media Services key delivery service validates that these values in the token match the values in the template.</span><span class="sxs-lookup"><span data-stu-id="826ec-159">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

<span data-ttu-id="826ec-160">When you use the Media Services SDK for .NET, you can use the TokenRestrictionTemplate class to generate the restriction token.</span><span class="sxs-lookup"><span data-stu-id="826ec-160">When you use the Media Services SDK for .NET, you can use the TokenRestrictionTemplate class to generate the restriction token.</span></span>
<span data-ttu-id="826ec-161">The following example creates an authorization policy with a token restriction.</span><span class="sxs-lookup"><span data-stu-id="826ec-161">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="826ec-162">In this example, the client must present a token that contains a signing key (VerificationKey), a token issuer, and required claims.</span><span class="sxs-lookup"><span data-stu-id="826ec-162">In this example, the client must present a token that contains a signing key (VerificationKey), a token issuer, and required claims.</span></span>
```csharp
    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                new List<ContentKeyAuthorizationPolicyRestriction>();

        ContentKeyAuthorizationPolicyRestriction restriction =
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString
                };

        restrictions.Add(restriction);

        //You could have multiple options 
        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
                "Token option for HLS",
                ContentKeyDeliveryType.BaselineHttp,
                restrictions,
                null  // no key delivery data is needed for HLS
                );

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKey.AuthorizationPolicyId = policy.Id;
        IContentKey updatedKey = contentKey.UpdateAsync().Result;
        Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

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
```
#### <a name="test-token"></a><span data-ttu-id="826ec-163">Test token</span><span class="sxs-lookup"><span data-stu-id="826ec-163">Test token</span></span>
<span data-ttu-id="826ec-164">To get a test token based on the token restriction that was used for the key authorization policy, do the following:</span><span class="sxs-lookup"><span data-stu-id="826ec-164">To get a test token based on the token restriction that was used for the key authorization policy, do the following:</span></span>
```csharp
    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    // Note, you need to pass the key id Guid because we specified 
    // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
    Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
    Console.WriteLine();
```

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="826ec-165">PlayReady dynamic encryption</span><span class="sxs-lookup"><span data-stu-id="826ec-165">PlayReady dynamic encryption</span></span>
<span data-ttu-id="826ec-166">You can use Media Services to configure the rights and restrictions that you want the PlayReady DRM runtime to enforce when a user tries to play back protected content.</span><span class="sxs-lookup"><span data-stu-id="826ec-166">You can use Media Services to configure the rights and restrictions that you want the PlayReady DRM runtime to enforce when a user tries to play back protected content.</span></span> 

<span data-ttu-id="826ec-167">When you protect your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="826ec-167">When you protect your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> <span data-ttu-id="826ec-168">In the Media Services SDK for .NET, the PlayReadyLicenseResponseTemplate and PlayReadyLicenseTemplate classes help you define the PlayReady license template.</span><span class="sxs-lookup"><span data-stu-id="826ec-168">In the Media Services SDK for .NET, the PlayReadyLicenseResponseTemplate and PlayReadyLicenseTemplate classes help you define the PlayReady license template.</span></span>

<span data-ttu-id="826ec-169">To learn how to encrypt your content with PlayReady and Widevine, see [Use PlayReady and/or Widevine dynamic common encryption](media-services-protect-with-playready-widevine.md).</span><span class="sxs-lookup"><span data-stu-id="826ec-169">To learn how to encrypt your content with PlayReady and Widevine, see [Use PlayReady and/or Widevine dynamic common encryption](media-services-protect-with-playready-widevine.md).</span></span>

### <a name="open-restriction"></a><span data-ttu-id="826ec-170">Open restriction</span><span class="sxs-lookup"><span data-stu-id="826ec-170">Open restriction</span></span>
<span data-ttu-id="826ec-171">Open restriction means the system delivers the key to anyone who makes a key request.</span><span class="sxs-lookup"><span data-stu-id="826ec-171">Open restriction means the system delivers the key to anyone who makes a key request.</span></span> <span data-ttu-id="826ec-172">This restriction might be useful for testing purposes.</span><span class="sxs-lookup"><span data-stu-id="826ec-172">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="826ec-173">The following example creates an open authorization policy and adds it to the content key:</span><span class="sxs-lookup"><span data-stu-id="826ec-173">The following example creates an open authorization policy and adds it to the content key:</span></span>

```csharp
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

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;


        contentKeyAuthorizationPolicy.Options.Add(policyOption);

        // Associate the content key authorization policy with the content key.
        contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
        contentKey = contentKey.UpdateAsync().Result;
    }
```

### <a name="token-restriction"></a><span data-ttu-id="826ec-174">Token restriction</span><span class="sxs-lookup"><span data-stu-id="826ec-174">Token restriction</span></span>
<span data-ttu-id="826ec-175">To configure the token restriction option, you need to use an XML to describe the token's authorization requirements.</span><span class="sxs-lookup"><span data-stu-id="826ec-175">To configure the token restriction option, you need to use an XML to describe the token's authorization requirements.</span></span> <span data-ttu-id="826ec-176">The token restriction configuration XML must conform to the XML schema shown in the "[Token restriction schema](#token-restriction-schema)" section.</span><span class="sxs-lookup"><span data-stu-id="826ec-176">The token restriction configuration XML must conform to the XML schema shown in the "[Token restriction schema](#token-restriction-schema)" section.</span></span>

```csharp
    public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
    {
        string tokenTemplateString = GenerateTokenRequirements();

        IContentKeyAuthorizationPolicy policy = _context.
                                ContentKeyAuthorizationPolicies.
                                CreateAsync("HLS token restricted authorization policy").Result;

        List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
        {
            new ContentKeyAuthorizationPolicyRestriction 
            { 
                Name = "Token Authorization Policy", 
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString, 
            }
        };

        // Configure PlayReady license template.
        string newLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

        IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                    restrictions, newLicenseTemplate);

        IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                    ContentKeyAuthorizationPolicies.
                    CreateAsync("Deliver Common Content Key with no restrictions").
                    Result;

        policy.Options.Add(policyOption);

        // Add ContentKeyAutorizationPolicy to ContentKey
        contentKeyAuthorizationPolicy.Options.Add(policyOption);

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
        // It grants the user the ability to play back the content subject to the zero or more restrictions 
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
```

<span data-ttu-id="826ec-177">To get a test token based on the token restriction that was used for the key authorization policy, see the "[Test token](#test-token)" section.</span><span class="sxs-lookup"><span data-stu-id="826ec-177">To get a test token based on the token restriction that was used for the key authorization policy, see the "[Test token](#test-token)" section.</span></span> 

## <a id="types"></a><span data-ttu-id="826ec-178">Types used when you define ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="826ec-178">Types used when you define ContentKeyAuthorizationPolicy</span></span>
### <a id="ContentKeyRestrictionType"></a><span data-ttu-id="826ec-179">ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="826ec-179">ContentKeyRestrictionType</span></span>

```csharp
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }
```

### <a id="ContentKeyDeliveryType"></a><span data-ttu-id="826ec-180">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="826ec-180">ContentKeyDeliveryType</span></span>

```csharp 
    public enum ContentKeyDeliveryType
    {
      None = 0,
      PlayReadyLicense = 1,
      BaselineHttp = 2,
      Widevine = 3
    }
```

### <a id="TokenType"></a><span data-ttu-id="826ec-181">TokenType</span><span class="sxs-lookup"><span data-stu-id="826ec-181">TokenType</span></span>

```csharp
    public enum TokenType
    {
        Undefined = 0,
        SWT = 1,
        JWT = 2,
    }
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="826ec-182">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="826ec-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="826ec-183">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="826ec-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="826ec-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="826ec-184">Next steps</span></span>
<span data-ttu-id="826ec-185">Now that you have configured the content key's authorization policy, see [Configure an asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="826ec-185">Now that you have configured the content key's authorization policy, see [Configure an asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

