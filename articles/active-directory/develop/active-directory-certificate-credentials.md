---
title: Certificate credentials in Azure AD | Microsoft Docs
description: This article discusses the registration and use of certificate credentials for application authentication
services: active-directory
documentationcenter: .net
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2018
ms.author: celested
ms.reviewer: nacanuma, jmprieur
ms.custom: aaddev
ms.openlocfilehash: 7d3796d8d4a5a2e292afaf9cd013ff04ffc082c5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871249"
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="c584a-103">Certificate credentials for application authentication</span><span class="sxs-lookup"><span data-stu-id="c584a-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="c584a-104">Azure Active Directory (Azure AD) allows an application to use its own credentials for authentication, for example, in the OAuth 2.0 Client Credentials Grant flow ([v1.0](v1-oauth2-client-creds-grant-flow.md), [v2.0](v2-oauth2-client-creds-grant-flow.md)) and the On-Behalf-Of flow ([v1.0](v1-oauth2-on-behalf-of-flow.md), [v2.0](v2-oauth2-on-behalf-of-flow.md)).</span><span class="sxs-lookup"><span data-stu-id="c584a-104">Azure Active Directory (Azure AD) allows an application to use its own credentials for authentication, for example, in the OAuth 2.0 Client Credentials Grant flow ([v1.0](v1-oauth2-client-creds-grant-flow.md), [v2.0](v2-oauth2-client-creds-grant-flow.md)) and the On-Behalf-Of flow ([v1.0](v1-oauth2-on-behalf-of-flow.md), [v2.0](v2-oauth2-on-behalf-of-flow.md)).</span></span>

<span data-ttu-id="c584a-105">One form of credential that an application can use for authentication is a JSON Web Token(JWT) assertion signed with a certificate that the application owns.</span><span class="sxs-lookup"><span data-stu-id="c584a-105">One form of credential that an application can use for authentication is a JSON Web Token(JWT) assertion signed with a certificate that the application owns.</span></span>

## <a name="assertion-format"></a><span data-ttu-id="c584a-106">Assertion format</span><span class="sxs-lookup"><span data-stu-id="c584a-106">Assertion format</span></span>
<span data-ttu-id="c584a-107">To compute the assertion, you can use one of the many [JSON Web Token](https://jwt.ms/) libraries in the language of your choice.</span><span class="sxs-lookup"><span data-stu-id="c584a-107">To compute the assertion, you can use one of the many [JSON Web Token](https://jwt.ms/) libraries in the language of your choice.</span></span> <span data-ttu-id="c584a-108">The information carried by the token are as follows:</span><span class="sxs-lookup"><span data-stu-id="c584a-108">The information carried by the token are as follows:</span></span>

### <a name="header"></a><span data-ttu-id="c584a-109">Header</span><span class="sxs-lookup"><span data-stu-id="c584a-109">Header</span></span>

| <span data-ttu-id="c584a-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="c584a-110">Parameter</span></span> |  <span data-ttu-id="c584a-111">Remark</span><span class="sxs-lookup"><span data-stu-id="c584a-111">Remark</span></span> |
| --- | --- |
| `alg` | <span data-ttu-id="c584a-112">Should be **RS256**</span><span class="sxs-lookup"><span data-stu-id="c584a-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="c584a-113">Should be **JWT**</span><span class="sxs-lookup"><span data-stu-id="c584a-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="c584a-114">Should be the X.509 Certificate SHA-1 thumbprint</span><span class="sxs-lookup"><span data-stu-id="c584a-114">Should be the X.509 Certificate SHA-1 thumbprint</span></span> |

### <a name="claims-payload"></a><span data-ttu-id="c584a-115">Claims (payload)</span><span class="sxs-lookup"><span data-stu-id="c584a-115">Claims (payload)</span></span>

| <span data-ttu-id="c584a-116">Parameter</span><span class="sxs-lookup"><span data-stu-id="c584a-116">Parameter</span></span> |  <span data-ttu-id="c584a-117">Remarks</span><span class="sxs-lookup"><span data-stu-id="c584a-117">Remarks</span></span> |
| --- | --- |
| `aud` | <span data-ttu-id="c584a-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="c584a-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="c584a-119">Expiration date: the date when the token expires.</span><span class="sxs-lookup"><span data-stu-id="c584a-119">Expiration date: the date when the token expires.</span></span> <span data-ttu-id="c584a-120">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.</span><span class="sxs-lookup"><span data-stu-id="c584a-120">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.</span></span>|
| `iss` | <span data-ttu-id="c584a-121">Issuer: should be the client_id (Application ID of the client service)</span><span class="sxs-lookup"><span data-stu-id="c584a-121">Issuer: should be the client_id (Application ID of the client service)</span></span> |
| `jti` | <span data-ttu-id="c584a-122">GUID: the JWT ID</span><span class="sxs-lookup"><span data-stu-id="c584a-122">GUID: the JWT ID</span></span> |
| `nbf` | <span data-ttu-id="c584a-123">Not Before: the date before which the token cannot be used.</span><span class="sxs-lookup"><span data-stu-id="c584a-123">Not Before: the date before which the token cannot be used.</span></span> <span data-ttu-id="c584a-124">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.</span><span class="sxs-lookup"><span data-stu-id="c584a-124">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.</span></span> |
| `sub` | <span data-ttu-id="c584a-125">Subject: As for `iss`, should be the client_id (Application ID of the client service)</span><span class="sxs-lookup"><span data-stu-id="c584a-125">Subject: As for `iss`, should be the client_id (Application ID of the client service)</span></span> |

### <a name="signature"></a><span data-ttu-id="c584a-126">Signature</span><span class="sxs-lookup"><span data-stu-id="c584a-126">Signature</span></span>

<span data-ttu-id="c584a-127">The signature is computed applying the certificate as described in the [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="c584a-127">The signature is computed applying the certificate as described in the [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

## <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="c584a-128">Example of a decoded JWT assertion</span><span class="sxs-lookup"><span data-stu-id="c584a-128">Example of a decoded JWT assertion</span></span>

```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

## <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="c584a-129">Example of an encoded JWT assertion</span><span class="sxs-lookup"><span data-stu-id="c584a-129">Example of an encoded JWT assertion</span></span>

<span data-ttu-id="c584a-130">The following string is an example of encoded assertion.</span><span class="sxs-lookup"><span data-stu-id="c584a-130">The following string is an example of encoded assertion.</span></span> <span data-ttu-id="c584a-131">If you look carefully, you notice three sections separated by dots (.):</span><span class="sxs-lookup"><span data-stu-id="c584a-131">If you look carefully, you notice three sections separated by dots (.):</span></span>
* <span data-ttu-id="c584a-132">The first section encodes the header</span><span class="sxs-lookup"><span data-stu-id="c584a-132">The first section encodes the header</span></span>
* <span data-ttu-id="c584a-133">The second section encodes the payload</span><span class="sxs-lookup"><span data-stu-id="c584a-133">The second section encodes the payload</span></span>
* <span data-ttu-id="c584a-134">The last section is the signature computed with the certificates from the content of the first two sections</span><span class="sxs-lookup"><span data-stu-id="c584a-134">The last section is the signature computed with the certificates from the content of the first two sections</span></span>

```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

## <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="c584a-135">Register your certificate with Azure AD</span><span class="sxs-lookup"><span data-stu-id="c584a-135">Register your certificate with Azure AD</span></span>

<span data-ttu-id="c584a-136">You can associate the certificate credential with the client application in Azure AD through the Azure portal using any of the following methods:</span><span class="sxs-lookup"><span data-stu-id="c584a-136">You can associate the certificate credential with the client application in Azure AD through the Azure portal using any of the following methods:</span></span>

### <a name="uploading-the-certificate-file"></a><span data-ttu-id="c584a-137">Uploading the certificate file</span><span class="sxs-lookup"><span data-stu-id="c584a-137">Uploading the certificate file</span></span>

<span data-ttu-id="c584a-138">In the Azure app registration for the client application:</span><span class="sxs-lookup"><span data-stu-id="c584a-138">In the Azure app registration for the client application:</span></span>
1. <span data-ttu-id="c584a-139">Select **Settings > Keys** and then select **Upload Public Key**.</span><span class="sxs-lookup"><span data-stu-id="c584a-139">Select **Settings > Keys** and then select **Upload Public Key**.</span></span> 
2. <span data-ttu-id="c584a-140">Select the certificate file you want to upload.</span><span class="sxs-lookup"><span data-stu-id="c584a-140">Select the certificate file you want to upload.</span></span>
3. <span data-ttu-id="c584a-141">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="c584a-141">Select **Save**.</span></span> 
   
   <span data-ttu-id="c584a-142">Once you save, the certificate is uploaded and the thumbprint, start date, and expiration values are displayed.</span><span class="sxs-lookup"><span data-stu-id="c584a-142">Once you save, the certificate is uploaded and the thumbprint, start date, and expiration values are displayed.</span></span> 

### <a name="updating-the-application-manifest"></a><span data-ttu-id="c584a-143">Updating the application manifest</span><span class="sxs-lookup"><span data-stu-id="c584a-143">Updating the application manifest</span></span>

<span data-ttu-id="c584a-144">Having hold of a certificate, you need to compute:</span><span class="sxs-lookup"><span data-stu-id="c584a-144">Having hold of a certificate, you need to compute:</span></span>

- <span data-ttu-id="c584a-145">`$base64Thumbprint`, which is the base64 encoding of the certificate hash</span><span class="sxs-lookup"><span data-stu-id="c584a-145">`$base64Thumbprint`, which is the base64 encoding of the certificate hash</span></span>
- <span data-ttu-id="c584a-146">`$base64Value`, which is the base64 encoding of the certificate raw data</span><span class="sxs-lookup"><span data-stu-id="c584a-146">`$base64Value`, which is the base64 encoding of the certificate raw data</span></span>

<span data-ttu-id="c584a-147">You also need to provide a GUID to identify the key in the application manifest (`$keyId`).</span><span class="sxs-lookup"><span data-stu-id="c584a-147">You also need to provide a GUID to identify the key in the application manifest (`$keyId`).</span></span>

<span data-ttu-id="c584a-148">In the Azure app registration for the client application:</span><span class="sxs-lookup"><span data-stu-id="c584a-148">In the Azure app registration for the client application:</span></span>
1. <span data-ttu-id="c584a-149">Open the application manifest.</span><span class="sxs-lookup"><span data-stu-id="c584a-149">Open the application manifest.</span></span>
2. <span data-ttu-id="c584a-150">Replace the *keyCredentials* property with your new certificate information using the following schema.</span><span class="sxs-lookup"><span data-stu-id="c584a-150">Replace the *keyCredentials* property with your new certificate information using the following schema.</span></span>

   ```
   "keyCredentials": [
       {
           "customKeyIdentifier": "$base64Thumbprint",
           "keyId": "$keyid",
           "type": "AsymmetricX509Cert",
           "usage": "Verify",
           "value":  "$base64Value"
       }
   ]
   ```
3. <span data-ttu-id="c584a-151">Save the edits to the application manifest and then upload the manifest to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c584a-151">Save the edits to the application manifest and then upload the manifest to Azure AD.</span></span> 

   <span data-ttu-id="c584a-152">The `keyCredentials` property is multi-valued, so you may upload multiple certificates for richer key management.</span><span class="sxs-lookup"><span data-stu-id="c584a-152">The `keyCredentials` property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
   
## <a name="code-sample"></a><span data-ttu-id="c584a-153">Code sample</span><span class="sxs-lookup"><span data-stu-id="c584a-153">Code sample</span></span>

<span data-ttu-id="c584a-154">The code sample on [Authenticating to Azure AD in daemon apps with certificates](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) shows how an application uses its own credentials for authentication.</span><span class="sxs-lookup"><span data-stu-id="c584a-154">The code sample on [Authenticating to Azure AD in daemon apps with certificates](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) shows how an application uses its own credentials for authentication.</span></span> <span data-ttu-id="c584a-155">It also shows how you can [create a self-signed certificate](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential#create-a-self-signed-certificate) using the `New-SelfSignedCertificate` Powershell command.</span><span class="sxs-lookup"><span data-stu-id="c584a-155">It also shows how you can [create a self-signed certificate](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential#create-a-self-signed-certificate) using the `New-SelfSignedCertificate` Powershell command.</span></span> <span data-ttu-id="c584a-156">You can also take advantage and use the [app creation scripts](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/AppCreationScripts/AppCreationScripts.md) to create the certificates, compute the thumbprint, and so on.</span><span class="sxs-lookup"><span data-stu-id="c584a-156">You can also take advantage and use the [app creation scripts](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/AppCreationScripts/AppCreationScripts.md) to create the certificates, compute the thumbprint, and so on.</span></span>
