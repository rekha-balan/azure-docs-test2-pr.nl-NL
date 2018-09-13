---
title: Configure a content key authorization policy with REST - Azure | Microsoft Docs
description: Learn how to configure an authorization policy for a content key by using the Media Services REST API.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 7af5f9e2-8ed8-43f2-843b-580ce8759fd4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2017
ms.author: juliako
ms.openlocfilehash: 87bd5120e23fe4ec7f4e2f842ddb96ba8b3dd3ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870595"
---
# <a name="dynamic-encryption-configure-a-content-key-authorization-policy"></a><span data-ttu-id="a2f08-103">Dynamic encryption: Configure a content key authorization policy</span><span class="sxs-lookup"><span data-stu-id="a2f08-103">Dynamic encryption: Configure a content key authorization policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="a2f08-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a2f08-104">Overview</span></span>
 <span data-ttu-id="a2f08-105">You can use Azure Media Services to deliver your content encrypted (dynamically) with the Advanced Encryption Standard (AES) by using 128-bit encryption keys and PlayReady or Widevine digital rights management (DRM).</span><span class="sxs-lookup"><span data-stu-id="a2f08-105">You can use Azure Media Services to deliver your content encrypted (dynamically) with the Advanced Encryption Standard (AES) by using 128-bit encryption keys and PlayReady or Widevine digital rights management (DRM).</span></span> <span data-ttu-id="a2f08-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses to authorized clients.</span><span class="sxs-lookup"><span data-stu-id="a2f08-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses to authorized clients.</span></span>

<span data-ttu-id="a2f08-107">If you want Media Services to encrypt an asset, you need to associate an encryption key (CommonEncryption or EnvelopeEncryption) with the asset.</span><span class="sxs-lookup"><span data-stu-id="a2f08-107">If you want Media Services to encrypt an asset, you need to associate an encryption key (CommonEncryption or EnvelopeEncryption) with the asset.</span></span> <span data-ttu-id="a2f08-108">For more information, see [Create content keys with REST](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="a2f08-108">For more information, see [Create content keys with REST](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="a2f08-109">You also need to configure authorization policies for the key (as described in this article).</span><span class="sxs-lookup"><span data-stu-id="a2f08-109">You also need to configure authorization policies for the key (as described in this article).</span></span>

<span data-ttu-id="a2f08-110">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content by using AES or PlayReady encryption.</span><span class="sxs-lookup"><span data-stu-id="a2f08-110">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content by using AES or PlayReady encryption.</span></span> <span data-ttu-id="a2f08-111">To decrypt the stream, the player requests the key from the key delivery service.</span><span class="sxs-lookup"><span data-stu-id="a2f08-111">To decrypt the stream, the player requests the key from the key delivery service.</span></span> <span data-ttu-id="a2f08-112">To determine whether the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span><span class="sxs-lookup"><span data-stu-id="a2f08-112">To determine whether the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="a2f08-113">Media Services supports multiple ways of authenticating users who make key requests.</span><span class="sxs-lookup"><span data-stu-id="a2f08-113">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="a2f08-114">The content key authorization policy can have one or more authorization restrictions by using either the open or token restriction.</span><span class="sxs-lookup"><span data-stu-id="a2f08-114">The content key authorization policy can have one or more authorization restrictions by using either the open or token restriction.</span></span> <span data-ttu-id="a2f08-115">The token-restricted policy must be accompanied by a token issued by a security token service (STS).</span><span class="sxs-lookup"><span data-stu-id="a2f08-115">The token-restricted policy must be accompanied by a token issued by a security token service (STS).</span></span> <span data-ttu-id="a2f08-116">Media Services supports tokens in the simple web token ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) and JSON Web Token (JWT) formats.</span><span class="sxs-lookup"><span data-stu-id="a2f08-116">Media Services supports tokens in the simple web token ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) and JSON Web Token (JWT) formats.</span></span>

<span data-ttu-id="a2f08-117">Media Services doesn't provide STS.</span><span class="sxs-lookup"><span data-stu-id="a2f08-117">Media Services doesn't provide STS.</span></span> <span data-ttu-id="a2f08-118">You can create a custom STS or use Azure Active Directory (Azure AD) to issue tokens.</span><span class="sxs-lookup"><span data-stu-id="a2f08-118">You can create a custom STS or use Azure Active Directory (Azure AD) to issue tokens.</span></span> <span data-ttu-id="a2f08-119">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span><span class="sxs-lookup"><span data-stu-id="a2f08-119">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration (as described in this article).</span></span> <span data-ttu-id="a2f08-120">If the token is valid and the claims in the token match those configured for the content key, the Media Services key delivery service returns the encryption key to the client.</span><span class="sxs-lookup"><span data-stu-id="a2f08-120">If the token is valid and the claims in the token match those configured for the content key, the Media Services key delivery service returns the encryption key to the client.</span></span>

<span data-ttu-id="a2f08-121">For more information, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="a2f08-121">For more information, see the following articles:</span></span>
- [<span data-ttu-id="a2f08-122">JWT token authentication</span><span class="sxs-lookup"><span data-stu-id="a2f08-122">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)
- [<span data-ttu-id="a2f08-123">Integrate an Azure Media Services OWIN MVC-based app with Azure Active Directory, and restrict content key delivery based on JWT claims</span><span class="sxs-lookup"><span data-stu-id="a2f08-123">Integrate an Azure Media Services OWIN MVC-based app with Azure Active Directory, and restrict content key delivery based on JWT claims</span></span>](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)

### <a name="some-considerations-apply"></a><span data-ttu-id="a2f08-124">Some considerations apply</span><span class="sxs-lookup"><span data-stu-id="a2f08-124">Some considerations apply</span></span>
* <span data-ttu-id="a2f08-125">To use dynamic packaging and dynamic encryption, make sure the streaming endpoint from which you want to stream your content is in the "Running" state.</span><span class="sxs-lookup"><span data-stu-id="a2f08-125">To use dynamic packaging and dynamic encryption, make sure the streaming endpoint from which you want to stream your content is in the "Running" state.</span></span>
* <span data-ttu-id="a2f08-126">Your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span><span class="sxs-lookup"><span data-stu-id="a2f08-126">Your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="a2f08-127">For more information, see [Encode an asset](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="a2f08-127">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="a2f08-128">Upload and encode your assets by using the AssetCreationOptions.StorageEncrypted option.</span><span class="sxs-lookup"><span data-stu-id="a2f08-128">Upload and encode your assets by using the AssetCreationOptions.StorageEncrypted option.</span></span>
* <span data-ttu-id="a2f08-129">If you plan to have multiple content keys that require the same policy configuration, we recommend that you create a single authorization policy and reuse it with multiple content keys.</span><span class="sxs-lookup"><span data-stu-id="a2f08-129">If you plan to have multiple content keys that require the same policy configuration, we recommend that you create a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="a2f08-130">The key delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="a2f08-130">The key delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span> <span data-ttu-id="a2f08-131">You can create ContentKeyAuthorizationPolicy and specify to use a token restriction, test it, and then update the policy to the open restriction.</span><span class="sxs-lookup"><span data-stu-id="a2f08-131">You can create ContentKeyAuthorizationPolicy and specify to use a token restriction, test it, and then update the policy to the open restriction.</span></span> <span data-ttu-id="a2f08-132">This process takes roughly 15 minutes before the policy switches to the open version of the policy.</span><span class="sxs-lookup"><span data-stu-id="a2f08-132">This process takes roughly 15 minutes before the policy switches to the open version of the policy.</span></span>
* <span data-ttu-id="a2f08-133">If you add or update your asset's delivery policy, you must delete any existing locator and create a new locator.</span><span class="sxs-lookup"><span data-stu-id="a2f08-133">If you add or update your asset's delivery policy, you must delete any existing locator and create a new locator.</span></span>
* <span data-ttu-id="a2f08-134">Currently, you can't encrypt progressive downloads.</span><span class="sxs-lookup"><span data-stu-id="a2f08-134">Currently, you can't encrypt progressive downloads.</span></span>
* <span data-ttu-id="a2f08-135">Media Services streaming endpoint sets the value of the CORS Access-Control-Allow-Origin header in preflight response as the wildcard "\*."</span><span class="sxs-lookup"><span data-stu-id="a2f08-135">Media Services streaming endpoint sets the value of the CORS Access-Control-Allow-Origin header in preflight response as the wildcard "\*."</span></span> <span data-ttu-id="a2f08-136">This value works well with most players, including Azure Media Player, Roku and JWPlayer, and others.</span><span class="sxs-lookup"><span data-stu-id="a2f08-136">This value works well with most players, including Azure Media Player, Roku and JWPlayer, and others.</span></span> <span data-ttu-id="a2f08-137">However, some players that use dash.js don't work because, with the credentials mode set to "include," XMLHttpRequest in their dash.js doesn't allow the wildcard "\*" as the value of Access-Control-Allow-Origin.</span><span class="sxs-lookup"><span data-stu-id="a2f08-137">However, some players that use dash.js don't work because, with the credentials mode set to "include," XMLHttpRequest in their dash.js doesn't allow the wildcard "\*" as the value of Access-Control-Allow-Origin.</span></span> <span data-ttu-id="a2f08-138">As a workaround to this limitation in dash.js, if you host your client from a single domain, Media Services can specify that domain in the preflight response header.</span><span class="sxs-lookup"><span data-stu-id="a2f08-138">As a workaround to this limitation in dash.js, if you host your client from a single domain, Media Services can specify that domain in the preflight response header.</span></span> <span data-ttu-id="a2f08-139">For assistance, open a support ticket through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a2f08-139">For assistance, open a support ticket through the Azure portal.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="a2f08-140">AES-128 dynamic encryption</span><span class="sxs-lookup"><span data-stu-id="a2f08-140">AES-128 dynamic encryption</span></span>
> [!NOTE]
> <span data-ttu-id="a2f08-141">When you work with the Media Services REST API, the following considerations apply.</span><span class="sxs-lookup"><span data-stu-id="a2f08-141">When you work with the Media Services REST API, the following considerations apply.</span></span>
> 
> <span data-ttu-id="a2f08-142">When you access entities in Media Services, you must set specific header fields and values in your HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="a2f08-142">When you access entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a2f08-143">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a2f08-143">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
> 
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="a2f08-144">Open restriction</span><span class="sxs-lookup"><span data-stu-id="a2f08-144">Open restriction</span></span>
<span data-ttu-id="a2f08-145">Open restriction means the system delivers the key to anyone who makes a key request.</span><span class="sxs-lookup"><span data-stu-id="a2f08-145">Open restriction means the system delivers the key to anyone who makes a key request.</span></span> <span data-ttu-id="a2f08-146">This restriction might be useful for testing purposes.</span><span class="sxs-lookup"><span data-stu-id="a2f08-146">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="a2f08-147">The following example creates an open authorization policy and adds it to the content key.</span><span class="sxs-lookup"><span data-stu-id="a2f08-147">The following example creates an open authorization policy and adds it to the content key.</span></span>

#### <a id="ContentKeyAuthorizationPolicies"></a><span data-ttu-id="a2f08-148">Create ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="a2f08-148">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="a2f08-149">Request:</span><span class="sxs-lookup"><span data-stu-id="a2f08-149">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 36

    {"Name":"Open Authorization Policy"}

<span data-ttu-id="a2f08-150">Response:</span><span class="sxs-lookup"><span data-stu-id="a2f08-150">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 211
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Adb4593da-f4d1-4cc5-a92a-d20eacbabee4')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    x-ms-request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:25:56 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:db4593da-f4d1-4cc5-a92a-d20eacbabee4","Name":"Open Authorization Policy"}

#### <a id="ContentKeyAuthorizationPolicyOptions"></a><span data-ttu-id="a2f08-151">Create ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="a2f08-151">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="a2f08-152">Request:</span><span class="sxs-lookup"><span data-stu-id="a2f08-152">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 168

    {"Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="a2f08-153">Response:</span><span class="sxs-lookup"><span data-stu-id="a2f08-153">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 349
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    x-ms-request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:56:40 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:57829b17-1101-4797-919b-f816f4a007b7","Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

#### <a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a><span data-ttu-id="a2f08-154">Link ContentKeyAuthorizationPolicies with Options</span><span class="sxs-lookup"><span data-stu-id="a2f08-154">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="a2f08-155">Request:</span><span class="sxs-lookup"><span data-stu-id="a2f08-155">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3A0baa438b-8ac2-4c40-a53c-4d4722b78715')/$links/Options HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: 9847f705-f2ca-4e95-a478-8f823dbbaa29
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 154

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')"}

<span data-ttu-id="a2f08-156">Response:</span><span class="sxs-lookup"><span data-stu-id="a2f08-156">Response:</span></span>

    HTTP/1.1 204 No Content

#### <a id="AddAuthorizationPolicyToKey"></a><span data-ttu-id="a2f08-157">Add an authorization policy to the content key</span><span class="sxs-lookup"><span data-stu-id="a2f08-157">Add an authorization policy to the content key</span></span>
<span data-ttu-id="a2f08-158">Request:</span><span class="sxs-lookup"><span data-stu-id="a2f08-158">Request:</span></span>

    PUT https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A2e6d36a7-a17c-4e9a-830d-eca23ad1a6f9') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: e613efff-cb6a-41b4-984a-f4f8fb6e76a4
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 78

    {"AuthorizationPolicyId":"nb:ckpid:UUID:c06cebb8-c4f0-4d1a-ba00-3273fb2bc3ad"}

<span data-ttu-id="a2f08-159">Response:</span><span class="sxs-lookup"><span data-stu-id="a2f08-159">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="a2f08-160">Token restriction</span><span class="sxs-lookup"><span data-stu-id="a2f08-160">Token restriction</span></span>
<span data-ttu-id="a2f08-161">This section describes how to create a content key authorization policy and associate it with the content key.</span><span class="sxs-lookup"><span data-stu-id="a2f08-161">This section describes how to create a content key authorization policy and associate it with the content key.</span></span> <span data-ttu-id="a2f08-162">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key.</span><span class="sxs-lookup"><span data-stu-id="a2f08-162">The authorization policy describes what authorization requirements must be met to determine if the user is authorized to receive the key.</span></span> <span data-ttu-id="a2f08-163">For example, does the verification key list contain the key that the token was signed with?</span><span class="sxs-lookup"><span data-stu-id="a2f08-163">For example, does the verification key list contain the key that the token was signed with?</span></span>

<span data-ttu-id="a2f08-164">To configure the token restriction option, you need to use an XML to describe the token's authorization requirements.</span><span class="sxs-lookup"><span data-stu-id="a2f08-164">To configure the token restriction option, you need to use an XML to describe the token's authorization requirements.</span></span> <span data-ttu-id="a2f08-165">The token restriction configuration XML must conform to the following XML schema:</span><span class="sxs-lookup"><span data-stu-id="a2f08-165">The token restriction configuration XML must conform to the following XML schema:</span></span>


#### <a id="schema"></a><span data-ttu-id="a2f08-166">Token restriction schema</span><span class="sxs-lookup"><span data-stu-id="a2f08-166">Token restriction schema</span></span>
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

<span data-ttu-id="a2f08-167">When you configure the token-restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span><span class="sxs-lookup"><span data-stu-id="a2f08-167">When you configure the token-restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="a2f08-168">The primary verification key contains the key that the token was signed with.</span><span class="sxs-lookup"><span data-stu-id="a2f08-168">The primary verification key contains the key that the token was signed with.</span></span> <span data-ttu-id="a2f08-169">The issuer is the STS that issues the token.</span><span class="sxs-lookup"><span data-stu-id="a2f08-169">The issuer is the STS that issues the token.</span></span> <span data-ttu-id="a2f08-170">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span><span class="sxs-lookup"><span data-stu-id="a2f08-170">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="a2f08-171">The Media Services key delivery service validates that these values in the token match the values in the template.</span><span class="sxs-lookup"><span data-stu-id="a2f08-171">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

<span data-ttu-id="a2f08-172">The following example creates an authorization policy with a token restriction.</span><span class="sxs-lookup"><span data-stu-id="a2f08-172">The following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="a2f08-173">In this example, the client must present a token that contains the signing key (VerificationKey), a token issuer, and required claims.</span><span class="sxs-lookup"><span data-stu-id="a2f08-173">In this example, the client must present a token that contains the signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="a2f08-174">Create ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="a2f08-174">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="a2f08-175">Create a token restriction policy, as shown in the section "[Create ContentKeyAuthorizationPolicies](#ContentKeyAuthorizationPolicies)."</span><span class="sxs-lookup"><span data-stu-id="a2f08-175">Create a token restriction policy, as shown in the section "[Create ContentKeyAuthorizationPolicies](#ContentKeyAuthorizationPolicies)."</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="a2f08-176">Create ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="a2f08-176">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="a2f08-177">Request:</span><span class="sxs-lookup"><span data-stu-id="a2f08-177">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580720&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5LsNu%2b0D4eD3UOP3BviTLDkUjaErdUx0ekJ8402xidQ%3d
    x-ms-version: 2.17
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1079

    {"Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="a2f08-178">Response:</span><span class="sxs-lookup"><span data-stu-id="a2f08-178">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1260
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae1ef6145-46e8-4ee6-9756-b1cf96328c23')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    x-ms-request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:10:37 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e1ef6145-46e8-4ee6-9756-b1cf96328c23","Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="a2f08-179">Link ContentKeyAuthorizationPolicies with options</span><span class="sxs-lookup"><span data-stu-id="a2f08-179">Link ContentKeyAuthorizationPolicies with options</span></span>
<span data-ttu-id="a2f08-180">Link ContentKeyAuthorizationPolicies with options, as shown in the section "[Create ContentKeyAuthorizationPolicies](#ContentKeyAuthorizationPolicies)."</span><span class="sxs-lookup"><span data-stu-id="a2f08-180">Link ContentKeyAuthorizationPolicies with options, as shown in the section "[Create ContentKeyAuthorizationPolicies](#ContentKeyAuthorizationPolicies)."</span></span>

#### <a name="add-an-authorization-policy-to-the-content-key"></a><span data-ttu-id="a2f08-181">Add an authorization policy to the content key</span><span class="sxs-lookup"><span data-stu-id="a2f08-181">Add an authorization policy to the content key</span></span>
<span data-ttu-id="a2f08-182">Add AuthorizationPolicy to ContentKey, as shown in the section "[Add an authorization policy to the content key](#AddAuthorizationPolicyToKey)."</span><span class="sxs-lookup"><span data-stu-id="a2f08-182">Add AuthorizationPolicy to ContentKey, as shown in the section "[Add an authorization policy to the content key](#AddAuthorizationPolicyToKey)."</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="a2f08-183">PlayReady dynamic encryption</span><span class="sxs-lookup"><span data-stu-id="a2f08-183">PlayReady dynamic encryption</span></span>
<span data-ttu-id="a2f08-184">You can use Media Services to configure the rights and restrictions that you want the PlayReady DRM runtime to enforce when a user tries to play back protected content.</span><span class="sxs-lookup"><span data-stu-id="a2f08-184">You can use Media Services to configure the rights and restrictions that you want the PlayReady DRM runtime to enforce when a user tries to play back protected content.</span></span> 

<span data-ttu-id="a2f08-185">When you protect your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2f08-185">When you protect your content with PlayReady, one of the things you need to specify in your authorization policy is an XML string that defines the [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="a2f08-186">Open restriction</span><span class="sxs-lookup"><span data-stu-id="a2f08-186">Open restriction</span></span>
<span data-ttu-id="a2f08-187">Open restriction means the system delivers the key to anyone who makes a key request.</span><span class="sxs-lookup"><span data-stu-id="a2f08-187">Open restriction means the system delivers the key to anyone who makes a key request.</span></span> <span data-ttu-id="a2f08-188">This restriction might be useful for testing purposes.</span><span class="sxs-lookup"><span data-stu-id="a2f08-188">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="a2f08-189">The following example creates an open authorization policy and adds it to the content key.</span><span class="sxs-lookup"><span data-stu-id="a2f08-189">The following example creates an open authorization policy and adds it to the content key.</span></span>

#### <a id="ContentKeyAuthorizationPolicies2"></a><span data-ttu-id="a2f08-190">Create ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="a2f08-190">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="a2f08-191">Request:</span><span class="sxs-lookup"><span data-stu-id="a2f08-191">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 58

    {"Name":"Deliver Common Content Key"}

<span data-ttu-id="a2f08-192">Response:</span><span class="sxs-lookup"><span data-stu-id="a2f08-192">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 233
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Acc3c64a8-e2fc-4e09-bf60-ac954251a387')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    x-ms-request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:26:00 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:cc3c64a8-e2fc-4e09-bf60-ac954251a387","Name":"Deliver Common Content Key"}


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="a2f08-193">Create ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="a2f08-193">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="a2f08-194">Request:</span><span class="sxs-lookup"><span data-stu-id="a2f08-194">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 593

    {"Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="a2f08-195">Response:</span><span class="sxs-lookup"><span data-stu-id="a2f08-195">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 774
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A1052308c-4df7-4fdb-8d21-4d2141fc2be0')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    x-ms-request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:23:24 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:1052308c-4df7-4fdb-8d21-4d2141fc2be0","Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="a2f08-196">Link ContentKeyAuthorizationPolicies with options</span><span class="sxs-lookup"><span data-stu-id="a2f08-196">Link ContentKeyAuthorizationPolicies with options</span></span>
<span data-ttu-id="a2f08-197">Link ContentKeyAuthorizationPolicies with options, as shown in the section "[Create ContentKeyAuthorizationPolicies](#ContentKeyAuthorizationPolicies)."</span><span class="sxs-lookup"><span data-stu-id="a2f08-197">Link ContentKeyAuthorizationPolicies with options, as shown in the section "[Create ContentKeyAuthorizationPolicies](#ContentKeyAuthorizationPolicies)."</span></span>

#### <a name="add-an-authorization-policy-to-the-content-key"></a><span data-ttu-id="a2f08-198">Add an authorization policy to the content key</span><span class="sxs-lookup"><span data-stu-id="a2f08-198">Add an authorization policy to the content key</span></span>
<span data-ttu-id="a2f08-199">Add AuthorizationPolicy to ContentKey, as shown in the section "[Add an authorization policy to the content key](#AddAuthorizationPolicyToKey)."</span><span class="sxs-lookup"><span data-stu-id="a2f08-199">Add AuthorizationPolicy to ContentKey, as shown in the section "[Add an authorization policy to the content key](#AddAuthorizationPolicyToKey)."</span></span>

### <a name="token-restriction"></a><span data-ttu-id="a2f08-200">Token restriction</span><span class="sxs-lookup"><span data-stu-id="a2f08-200">Token restriction</span></span>
<span data-ttu-id="a2f08-201">To configure the token restriction option, you need to use an XML to describe the token's authorization requirements.</span><span class="sxs-lookup"><span data-stu-id="a2f08-201">To configure the token restriction option, you need to use an XML to describe the token's authorization requirements.</span></span> <span data-ttu-id="a2f08-202">The token restriction configuration XML must conform to the XML schema shown in the section "[Token restriction schema](#schema)."</span><span class="sxs-lookup"><span data-stu-id="a2f08-202">The token restriction configuration XML must conform to the XML schema shown in the section "[Token restriction schema](#schema)."</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="a2f08-203">Create ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="a2f08-203">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="a2f08-204">Create ContentKeyAuthorizationPolicies, as shown in the section "[Create ContentKeyAuthorizationPolicies](#ContentKeyAuthorizationPolicies2)."</span><span class="sxs-lookup"><span data-stu-id="a2f08-204">Create ContentKeyAuthorizationPolicies, as shown in the section "[Create ContentKeyAuthorizationPolicies](#ContentKeyAuthorizationPolicies2)."</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="a2f08-205">Create ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="a2f08-205">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="a2f08-206">Request:</span><span class="sxs-lookup"><span data-stu-id="a2f08-206">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN> 
    x-ms-version: 2.17
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1525

    {"Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="a2f08-207">Response:</span><span class="sxs-lookup"><span data-stu-id="a2f08-207">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1706
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae42bbeae-de42-4077-90e9-a844f297ef70')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    x-ms-request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:58:47 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e42bbeae-de42-4077-90e9-a844f297ef70","Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="a2f08-208">Link ContentKeyAuthorizationPolicies with options</span><span class="sxs-lookup"><span data-stu-id="a2f08-208">Link ContentKeyAuthorizationPolicies with options</span></span>
<span data-ttu-id="a2f08-209">Link ContentKeyAuthorizationPolicies with options, as shown in the section "[Create ContentKeyAuthorizationPolicies](#ContentKeyAuthorizationPolicies)."</span><span class="sxs-lookup"><span data-stu-id="a2f08-209">Link ContentKeyAuthorizationPolicies with options, as shown in the section "[Create ContentKeyAuthorizationPolicies](#ContentKeyAuthorizationPolicies)."</span></span>

#### <a name="add-an-authorization-policy-to-the-content-key"></a><span data-ttu-id="a2f08-210">Add an authorization policy to the content key</span><span class="sxs-lookup"><span data-stu-id="a2f08-210">Add an authorization policy to the content key</span></span>
<span data-ttu-id="a2f08-211">Add AuthorizationPolicy to ContentKey, as shown in the section "[Add an authorization policy to the content key](#AddAuthorizationPolicyToKey)."</span><span class="sxs-lookup"><span data-stu-id="a2f08-211">Add AuthorizationPolicy to ContentKey, as shown in the section "[Add an authorization policy to the content key](#AddAuthorizationPolicyToKey)."</span></span>

## <a id="types"></a><span data-ttu-id="a2f08-212">Types used when you define ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="a2f08-212">Types used when you define ContentKeyAuthorizationPolicy</span></span>
### <a id="ContentKeyRestrictionType"></a><span data-ttu-id="a2f08-213">ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="a2f08-213">ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1, 
        IPRestricted = 2, // IP restriction on content key is not currently supported, reserved for future.
    }


> [!NOTE]
> <span data-ttu-id="a2f08-214">IP restriction on content key authorization policies is not yet available in the service.</span><span class="sxs-lookup"><span data-stu-id="a2f08-214">IP restriction on content key authorization policies is not yet available in the service.</span></span>


### <a id="ContentKeyDeliveryType"></a><span data-ttu-id="a2f08-215">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="a2f08-215">ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="a2f08-216">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="a2f08-216">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a2f08-217">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="a2f08-217">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a2f08-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2f08-218">Next steps</span></span>
<span data-ttu-id="a2f08-219">Now that you have configured a content key's authorization policy, see [Configure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a2f08-219">Now that you have configured a content key's authorization policy, see [Configure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

