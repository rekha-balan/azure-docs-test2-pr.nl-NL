---
title: Azure AD Service to Service Auth using OAuth2.0 | Microsoft Docs
description: This article describes how to use HTTP messages to implement service to service authentication using the OAuth2.0 client credentials grant flow.
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: ''
ms.assetid: a7f939d9-532d-4b6d-b6d3-95520207965d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: priyamo
ms.openlocfilehash: 1d78d980412c7c26329bb606c029169f43e6bf22
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562886"
---
# <a name="service-to-service-calls-using-client-credentials"></a><span data-ttu-id="8f0b8-103">Service to service calls using client credentials</span><span class="sxs-lookup"><span data-stu-id="8f0b8-103">Service to service calls using client credentials</span></span>
<span data-ttu-id="8f0b8-104">The OAuth 2.0 Client Credentials Grant Flow permits a web service (a **confidential client**) to use its own credentials to authenticate when calling another web service, instead of impersonating a user.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-104">The OAuth 2.0 Client Credentials Grant Flow permits a web service (a **confidential client**) to use its own credentials to authenticate when calling another web service, instead of impersonating a user.</span></span> <span data-ttu-id="8f0b8-105">In this scenario, the client is typically a middle-tier web service, a daemon service, or web site.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-105">In this scenario, the client is typically a middle-tier web service, a daemon service, or web site.</span></span>

## <a name="client-credentials-grant-flow-diagram"></a><span data-ttu-id="8f0b8-106">Client credentials grant flow diagram</span><span class="sxs-lookup"><span data-stu-id="8f0b8-106">Client credentials grant flow diagram</span></span>
<span data-ttu-id="8f0b8-107">The following diagram explains how the client credentials grant flow works in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f0b8-107">The following diagram explains how the client credentials grant flow works in Azure Active Directory (Azure AD).</span></span>

![OAuth2.0 Client Credentials Grant Flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/develop/media/active-directory-protocols-oauth-service-to-service/active-directory-protocols-oauth-client-credentials-grant-flow.jpg)

1. <span data-ttu-id="8f0b8-109">The client application authenticates to the Azure AD token issuance endpoint and requests an access token.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-109">The client application authenticates to the Azure AD token issuance endpoint and requests an access token.</span></span>
2. <span data-ttu-id="8f0b8-110">The Azure AD token issuance endpoint issues the access token.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-110">The Azure AD token issuance endpoint issues the access token.</span></span>
3. <span data-ttu-id="8f0b8-111">The access token is used to authenticate to the secured resource.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-111">The access token is used to authenticate to the secured resource.</span></span>
4. <span data-ttu-id="8f0b8-112">Data from the secured resource is returned to the web application.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-112">Data from the secured resource is returned to the web application.</span></span>

## <a name="register-the-services-in-azure-ad"></a><span data-ttu-id="8f0b8-113">Register the Services in Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0b8-113">Register the Services in Azure AD</span></span>
<span data-ttu-id="8f0b8-114">Register both the calling service and the receiving service in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f0b8-114">Register both the calling service and the receiving service in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8f0b8-115">For detailed instructions, see [Integrating applications with Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="8f0b8-115">For detailed instructions, see [Integrating applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="request-an-access-token"></a><span data-ttu-id="8f0b8-116">Request an Access Token</span><span class="sxs-lookup"><span data-stu-id="8f0b8-116">Request an Access Token</span></span>
<span data-ttu-id="8f0b8-117">To request an access token, use an HTTP POST to the tenant-specific Azure AD endpoint.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-117">To request an access token, use an HTTP POST to the tenant-specific Azure AD endpoint.</span></span>

```
https://login.microsoftonline.com/<tenant id>/oauth2/token
```

## <a name="service-to-service-access-token-request"></a><span data-ttu-id="8f0b8-118">Service-to-service access token request</span><span class="sxs-lookup"><span data-stu-id="8f0b8-118">Service-to-service access token request</span></span>
<span data-ttu-id="8f0b8-119">A service-to-service access token request contains the following parameters.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-119">A service-to-service access token request contains the following parameters.</span></span>

| <span data-ttu-id="8f0b8-120">Parameter</span><span class="sxs-lookup"><span data-stu-id="8f0b8-120">Parameter</span></span> |  | <span data-ttu-id="8f0b8-121">Description</span><span class="sxs-lookup"><span data-stu-id="8f0b8-121">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8f0b8-122">response_type</span><span class="sxs-lookup"><span data-stu-id="8f0b8-122">response_type</span></span> |<span data-ttu-id="8f0b8-123">required</span><span class="sxs-lookup"><span data-stu-id="8f0b8-123">required</span></span> |<span data-ttu-id="8f0b8-124">Specifies the requested response type.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-124">Specifies the requested response type.</span></span> <span data-ttu-id="8f0b8-125">In a Client Credentials Grant flow, the value must be **client_credentials**.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-125">In a Client Credentials Grant flow, the value must be **client_credentials**.</span></span> |
| <span data-ttu-id="8f0b8-126">client_id</span><span class="sxs-lookup"><span data-stu-id="8f0b8-126">client_id</span></span> |<span data-ttu-id="8f0b8-127">required</span><span class="sxs-lookup"><span data-stu-id="8f0b8-127">required</span></span> |<span data-ttu-id="8f0b8-128">Specifies the Azure AD client id of the calling web service.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-128">Specifies the Azure AD client id of the calling web service.</span></span> <span data-ttu-id="8f0b8-129">To find the calling application's client ID, in the Azure Management Portal, click **Active Directory**, click the directory, click the application, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-129">To find the calling application's client ID, in the Azure Management Portal, click **Active Directory**, click the directory, click the application, and then click **Configure**.</span></span> |
| <span data-ttu-id="8f0b8-130">client_secret</span><span class="sxs-lookup"><span data-stu-id="8f0b8-130">client_secret</span></span> |<span data-ttu-id="8f0b8-131">required</span><span class="sxs-lookup"><span data-stu-id="8f0b8-131">required</span></span> |<span data-ttu-id="8f0b8-132">Enter a key registered for the calling web service in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-132">Enter a key registered for the calling web service in Azure AD.</span></span> <span data-ttu-id="8f0b8-133">To create a key, in the Azure Management Portal, click **Active Directory**, click the directory, click the application, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-133">To create a key, in the Azure Management Portal, click **Active Directory**, click the directory, click the application, and then click **Configure**.</span></span> |
| <span data-ttu-id="8f0b8-134">resource</span><span class="sxs-lookup"><span data-stu-id="8f0b8-134">resource</span></span> |<span data-ttu-id="8f0b8-135">required</span><span class="sxs-lookup"><span data-stu-id="8f0b8-135">required</span></span> |<span data-ttu-id="8f0b8-136">Enter the App ID URI of the receiving web service.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-136">Enter the App ID URI of the receiving web service.</span></span> <span data-ttu-id="8f0b8-137">To find the App ID URI, in the Azure Management Portal, click **Active Directory**, click the directory, click the application, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-137">To find the App ID URI, in the Azure Management Portal, click **Active Directory**, click the directory, click the application, and then click **Configure**.</span></span> |

## <a name="example"></a><span data-ttu-id="8f0b8-138">Example</span><span class="sxs-lookup"><span data-stu-id="8f0b8-138">Example</span></span>
<span data-ttu-id="8f0b8-139">The following HTTP POST requests an access token for the https://service.contoso.com/ web service.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-139">The following HTTP POST requests an access token for the https://service.contoso.com/ web service.</span></span> <span data-ttu-id="8f0b8-140">The `client_id` identifies the web service that requests the access token.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-140">The `client_id` identifies the web service that requests the access token.</span></span>

```
POST contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fservice.contoso.com%2F
```

## <a name="service-to-service-access-token-response"></a><span data-ttu-id="8f0b8-141">Service-to-Service Access Token Response</span><span class="sxs-lookup"><span data-stu-id="8f0b8-141">Service-to-Service Access Token Response</span></span>
<span data-ttu-id="8f0b8-142">A success response contains a JSON OAuth 2.0 response with the following parameters.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-142">A success response contains a JSON OAuth 2.0 response with the following parameters.</span></span>

| <span data-ttu-id="8f0b8-143">Parameter</span><span class="sxs-lookup"><span data-stu-id="8f0b8-143">Parameter</span></span> | <span data-ttu-id="8f0b8-144">Description</span><span class="sxs-lookup"><span data-stu-id="8f0b8-144">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8f0b8-145">access_token</span><span class="sxs-lookup"><span data-stu-id="8f0b8-145">access_token</span></span> |<span data-ttu-id="8f0b8-146">The requested access token.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-146">The requested access token.</span></span> <span data-ttu-id="8f0b8-147">The calling web service can use this token to authenticate to the receiving web service.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-147">The calling web service can use this token to authenticate to the receiving web service.</span></span> |
| <span data-ttu-id="8f0b8-148">access_type</span><span class="sxs-lookup"><span data-stu-id="8f0b8-148">access_type</span></span> |<span data-ttu-id="8f0b8-149">Indicates the token type value.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-149">Indicates the token type value.</span></span> <span data-ttu-id="8f0b8-150">The only type that Azure AD supports is **Bearer**.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-150">The only type that Azure AD supports is **Bearer**.</span></span> <span data-ttu-id="8f0b8-151">For more information about bearer tokens, see The [OAuth 2.0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt).</span><span class="sxs-lookup"><span data-stu-id="8f0b8-151">For more information about bearer tokens, see The [OAuth 2.0 Authorization Framework: Bearer Token Usage (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt).</span></span> |
| <span data-ttu-id="8f0b8-152">expires_in</span><span class="sxs-lookup"><span data-stu-id="8f0b8-152">expires_in</span></span> |<span data-ttu-id="8f0b8-153">How long the access token is valid (in seconds).</span><span class="sxs-lookup"><span data-stu-id="8f0b8-153">How long the access token is valid (in seconds).</span></span> |
| <span data-ttu-id="8f0b8-154">expires_on</span><span class="sxs-lookup"><span data-stu-id="8f0b8-154">expires_on</span></span> |<span data-ttu-id="8f0b8-155">The time when the access token expires.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-155">The time when the access token expires.</span></span> <span data-ttu-id="8f0b8-156">The date is represented as the number of seconds from 1970-01-01T0:0:0Z UTC until the expiration time.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-156">The date is represented as the number of seconds from 1970-01-01T0:0:0Z UTC until the expiration time.</span></span> <span data-ttu-id="8f0b8-157">This value is used to determine the lifetime of cached tokens.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-157">This value is used to determine the lifetime of cached tokens.</span></span> |
| <span data-ttu-id="8f0b8-158">resource</span><span class="sxs-lookup"><span data-stu-id="8f0b8-158">resource</span></span> |<span data-ttu-id="8f0b8-159">The App ID URI of the receiving web service.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-159">The App ID URI of the receiving web service.</span></span> |

## <a name="example"></a><span data-ttu-id="8f0b8-160">Example</span><span class="sxs-lookup"><span data-stu-id="8f0b8-160">Example</span></span>
<span data-ttu-id="8f0b8-161">The following example shows a success response to a request for an access token to a web service.</span><span class="sxs-lookup"><span data-stu-id="8f0b8-161">The following example shows a success response to a request for an access token to a web service.</span></span>

```
{
"access_token":"eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0ODI2NywibmJmIjoxMzg4NDQ4MjY3LCJleHAiOjEzODg0NTIxNjcsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsInN1YiI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZS8iLCJhcHBpZCI6ImQxN2QxNWJjLWM1NzYtNDFlNS05MjdmLWRiNWYzMGRkNThmMSIsImFwcGlkYWNyIjoiMSJ9.aqtfJ7G37CpKV901Vm9sGiQhde0WMg6luYJR4wuNR2ffaQsVPPpKirM5rbc6o5CmW1OtmaAIdwDcL6i9ZT9ooIIicSRrjCYMYWHX08ip-tj-uWUihGztI02xKdWiycItpWiHxapQm0a8Ti1CWRjJghORC1B1-fah_yWx6Cjuf4QE8xJcu-ZHX0pVZNPX22PHYV5Km-vPTq2HtIqdboKyZy3Y4y3geOrRIFElZYoqjqSv5q9Jgtj5ERsNQIjefpyxW3EwPtFqMcDm4ebiAEpoEWRN4QYOMxnC9OUBeG9oLA0lTfmhgHLAtvJogJcYFzwngTsVo6HznsvPWy7UP3MINA",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://service.contoso.com/"
}
```

## <a name="see-also"></a><span data-ttu-id="8f0b8-162">See also</span><span class="sxs-lookup"><span data-stu-id="8f0b8-162">See also</span></span>
* [<span data-ttu-id="8f0b8-163">OAuth 2.0 in Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f0b8-163">OAuth 2.0 in Azure AD</span></span>](active-directory-protocols-oauth-code.md)
