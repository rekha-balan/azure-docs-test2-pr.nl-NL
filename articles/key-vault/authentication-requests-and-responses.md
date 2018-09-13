---
title: Authentication, requests and responses
description: Authenticate to AD for using Key Vault
services: key-vault
documentationcenter: ''
author: bryanla
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 4c321939-8a5b-42ca-83c4-2f5f647ca13e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/09/2018
ms.author: bryanla
ms.openlocfilehash: c7cd9dfa019ca0d8560833b10a3e8a1a37a1e1ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856596"
---
# <a name="authentication-requests-and-responses"></a><span data-ttu-id="c7f91-103">Authentication, requests and responses</span><span class="sxs-lookup"><span data-stu-id="c7f91-103">Authentication, requests and responses</span></span>

<span data-ttu-id="c7f91-104">Azure Key Vault supports JSON formatted requests and responses.</span><span class="sxs-lookup"><span data-stu-id="c7f91-104">Azure Key Vault supports JSON formatted requests and responses.</span></span> <span data-ttu-id="c7f91-105">Requests to the Azure Key Vault are directed to a valid Azure Key Vault URL using HTTPS with some URL parameters and JSON encoded request and response bodies.</span><span class="sxs-lookup"><span data-stu-id="c7f91-105">Requests to the Azure Key Vault are directed to a valid Azure Key Vault URL using HTTPS with some URL parameters and JSON encoded request and response bodies.</span></span>

<span data-ttu-id="c7f91-106">This topic covers specifics for the Azure Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="c7f91-106">This topic covers specifics for the Azure Key Vault service.</span></span> <span data-ttu-id="c7f91-107">For general information on using Azure REST interfaces, including authentication/authorization and how to acquire an access token, see [Azure REST API Reference](https://docs.microsoft.com/rest/api/azure).</span><span class="sxs-lookup"><span data-stu-id="c7f91-107">For general information on using Azure REST interfaces, including authentication/authorization and how to acquire an access token, see [Azure REST API Reference](https://docs.microsoft.com/rest/api/azure).</span></span>

## <a name="request-url"></a><span data-ttu-id="c7f91-108">Request URL</span><span class="sxs-lookup"><span data-stu-id="c7f91-108">Request URL</span></span>  
 <span data-ttu-id="c7f91-109">Key management operations use HTTP DELETE, GET, PATCH, PUT and HTTP POST and cryptographic operations against existing key objects use HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="c7f91-109">Key management operations use HTTP DELETE, GET, PATCH, PUT and HTTP POST and cryptographic operations against existing key objects use HTTP POST.</span></span> <span data-ttu-id="c7f91-110">Clients that cannot support specific HTTP verbs may also use HTTP POST using the X-HTTP-REQUEST header to specify the intended verb; requests that do not normally require a body should include an empty body when using HTTP POST, for example when using POST instead of DELETE.</span><span class="sxs-lookup"><span data-stu-id="c7f91-110">Clients that cannot support specific HTTP verbs may also use HTTP POST using the X-HTTP-REQUEST header to specify the intended verb; requests that do not normally require a body should include an empty body when using HTTP POST, for example when using POST instead of DELETE.</span></span>  

 <span data-ttu-id="c7f91-111">To work with objects in the Azure Key Vault, the following are example URLs:</span><span class="sxs-lookup"><span data-stu-id="c7f91-111">To work with objects in the Azure Key Vault, the following are example URLs:</span></span>  

-   <span data-ttu-id="c7f91-112">To CREATE a key called TESTKEY in a Key Vault use - `PUT /keys/TESTKEY?api-version=<api_version> HTTP/1.1`</span><span class="sxs-lookup"><span data-stu-id="c7f91-112">To CREATE a key called TESTKEY in a Key Vault use - `PUT /keys/TESTKEY?api-version=<api_version> HTTP/1.1`</span></span>  

-   <span data-ttu-id="c7f91-113">To IMPORT a key called IMPORTEDKEY into a Key Vault use - `POST /keys/IMPORTEDKEY/import?api-version=<api_version> HTTP/1.1`</span><span class="sxs-lookup"><span data-stu-id="c7f91-113">To IMPORT a key called IMPORTEDKEY into a Key Vault use - `POST /keys/IMPORTEDKEY/import?api-version=<api_version> HTTP/1.1`</span></span>  

-   <span data-ttu-id="c7f91-114">To GET a secret called MYSECRET in a Key Vault use - `GET /secrets/MYSECRET?api-version=<api_version> HTTP/1.1`</span><span class="sxs-lookup"><span data-stu-id="c7f91-114">To GET a secret called MYSECRET in a Key Vault use - `GET /secrets/MYSECRET?api-version=<api_version> HTTP/1.1`</span></span>  

-   <span data-ttu-id="c7f91-115">To SIGN a digest using a key called TESTKEY in a Key Vault use - `POST /keys/TESTKEY/sign?api-version=<api_version> HTTP/1.1`</span><span class="sxs-lookup"><span data-stu-id="c7f91-115">To SIGN a digest using a key called TESTKEY in a Key Vault use - `POST /keys/TESTKEY/sign?api-version=<api_version> HTTP/1.1`</span></span>  

 <span data-ttu-id="c7f91-116">The authority for a request to a Key Vault is always as follows,  `https://{keyvault-name}.vault.azure.net/`</span><span class="sxs-lookup"><span data-stu-id="c7f91-116">The authority for a request to a Key Vault is always as follows,  `https://{keyvault-name}.vault.azure.net/`</span></span>  

 <span data-ttu-id="c7f91-117">Keys are always stored under the /keys path, Secrets are always stored under the /secrets path.</span><span class="sxs-lookup"><span data-stu-id="c7f91-117">Keys are always stored under the /keys path, Secrets are always stored under the /secrets path.</span></span>  

## <a name="api-version"></a><span data-ttu-id="c7f91-118">API Version</span><span class="sxs-lookup"><span data-stu-id="c7f91-118">API Version</span></span>  
 <span data-ttu-id="c7f91-119">The Azure Key Vault Service supports protocol versioning to provide compatibility with down-level clients, although not all capabilities will be available to those clients.</span><span class="sxs-lookup"><span data-stu-id="c7f91-119">The Azure Key Vault Service supports protocol versioning to provide compatibility with down-level clients, although not all capabilities will be available to those clients.</span></span> <span data-ttu-id="c7f91-120">Clients must use the `api-version` query string parameter to specify the version of the protocol that they support as there is no default.</span><span class="sxs-lookup"><span data-stu-id="c7f91-120">Clients must use the `api-version` query string parameter to specify the version of the protocol that they support as there is no default.</span></span>  

 <span data-ttu-id="c7f91-121">Azure Key Vault protocol versions follow a date numbering scheme using a {YYYY}.{MM}.{DD} format.</span><span class="sxs-lookup"><span data-stu-id="c7f91-121">Azure Key Vault protocol versions follow a date numbering scheme using a {YYYY}.{MM}.{DD} format.</span></span>  

## <a name="request-body"></a><span data-ttu-id="c7f91-122">Request Body</span><span class="sxs-lookup"><span data-stu-id="c7f91-122">Request Body</span></span>  
 <span data-ttu-id="c7f91-123">As per the HTTP specification, GET operations must NOT have a request body, and POST and PUT operations must have a request body.</span><span class="sxs-lookup"><span data-stu-id="c7f91-123">As per the HTTP specification, GET operations must NOT have a request body, and POST and PUT operations must have a request body.</span></span> <span data-ttu-id="c7f91-124">The body in DELETE operations is optional in HTTP.</span><span class="sxs-lookup"><span data-stu-id="c7f91-124">The body in DELETE operations is optional in HTTP.</span></span>  

 <span data-ttu-id="c7f91-125">Unless otherwise noted in operation description, the request body content type must be application/json and must contain a serialized JSON object conformant to content type.</span><span class="sxs-lookup"><span data-stu-id="c7f91-125">Unless otherwise noted in operation description, the request body content type must be application/json and must contain a serialized JSON object conformant to content type.</span></span>  

 <span data-ttu-id="c7f91-126">Unless otherwise noted in operation description, the Accept request header must contain the application/json media type.</span><span class="sxs-lookup"><span data-stu-id="c7f91-126">Unless otherwise noted in operation description, the Accept request header must contain the application/json media type.</span></span>  

## <a name="response-body"></a><span data-ttu-id="c7f91-127">Response Body</span><span class="sxs-lookup"><span data-stu-id="c7f91-127">Response Body</span></span>  
 <span data-ttu-id="c7f91-128">Unless otherwise noted in operation description, the response body content type of both successful and failed operations will be application/json and contains detailed error information.</span><span class="sxs-lookup"><span data-stu-id="c7f91-128">Unless otherwise noted in operation description, the response body content type of both successful and failed operations will be application/json and contains detailed error information.</span></span>  

## <a name="using-http-post"></a><span data-ttu-id="c7f91-129">Using HTTP POST</span><span class="sxs-lookup"><span data-stu-id="c7f91-129">Using HTTP POST</span></span>  
 <span data-ttu-id="c7f91-130">Some clients may not be able to use certain HTTP verbs, such as PATCH or DELETE.</span><span class="sxs-lookup"><span data-stu-id="c7f91-130">Some clients may not be able to use certain HTTP verbs, such as PATCH or DELETE.</span></span> <span data-ttu-id="c7f91-131">Azure Key Vault supports HTTP POST as an alternative for these clients provided that the client also includes the “X-HTTP-METHOD” header to specific the original HTTP verb.</span><span class="sxs-lookup"><span data-stu-id="c7f91-131">Azure Key Vault supports HTTP POST as an alternative for these clients provided that the client also includes the “X-HTTP-METHOD” header to specific the original HTTP verb.</span></span> <span data-ttu-id="c7f91-132">Support for HTTP POST is noted for each of the API defined in this document.</span><span class="sxs-lookup"><span data-stu-id="c7f91-132">Support for HTTP POST is noted for each of the API defined in this document.</span></span>  

## <a name="error-responses"></a><span data-ttu-id="c7f91-133">Error Responses</span><span class="sxs-lookup"><span data-stu-id="c7f91-133">Error Responses</span></span>  
 <span data-ttu-id="c7f91-134">Error handling will use HTTP status codes.</span><span class="sxs-lookup"><span data-stu-id="c7f91-134">Error handling will use HTTP status codes.</span></span> <span data-ttu-id="c7f91-135">Typical results are:</span><span class="sxs-lookup"><span data-stu-id="c7f91-135">Typical results are:</span></span>  

-   <span data-ttu-id="c7f91-136">2xx – Success: Used for normal operation.</span><span class="sxs-lookup"><span data-stu-id="c7f91-136">2xx – Success: Used for normal operation.</span></span> <span data-ttu-id="c7f91-137">The response body will contain the expected result</span><span class="sxs-lookup"><span data-stu-id="c7f91-137">The response body will contain the expected result</span></span>  

-   <span data-ttu-id="c7f91-138">3xx – Redirection: The 304 "Not Modified" may be returned to fulfill a conditional GET.</span><span class="sxs-lookup"><span data-stu-id="c7f91-138">3xx – Redirection: The 304 "Not Modified" may be returned to fulfill a conditional GET.</span></span> <span data-ttu-id="c7f91-139">Other 3xx codes may be used in the future to indicate DNS and path changes.</span><span class="sxs-lookup"><span data-stu-id="c7f91-139">Other 3xx codes may be used in the future to indicate DNS and path changes.</span></span>  

-   <span data-ttu-id="c7f91-140">4xx – Client Error: Used for bad requests, missing keys, syntax errors, invalid parameters, authentication errors, etc. The response body will contain detailed error explanation.</span><span class="sxs-lookup"><span data-stu-id="c7f91-140">4xx – Client Error: Used for bad requests, missing keys, syntax errors, invalid parameters, authentication errors, etc. The response body will contain detailed error explanation.</span></span>  

-   <span data-ttu-id="c7f91-141">5xx – Server Error: Used for internal server errors.</span><span class="sxs-lookup"><span data-stu-id="c7f91-141">5xx – Server Error: Used for internal server errors.</span></span> <span data-ttu-id="c7f91-142">The response body will contain summarized error information.</span><span class="sxs-lookup"><span data-stu-id="c7f91-142">The response body will contain summarized error information.</span></span>  

 <span data-ttu-id="c7f91-143">The system is designed to work behind a proxy or firewall.</span><span class="sxs-lookup"><span data-stu-id="c7f91-143">The system is designed to work behind a proxy or firewall.</span></span> <span data-ttu-id="c7f91-144">Therefore, a client might receive other error codes.</span><span class="sxs-lookup"><span data-stu-id="c7f91-144">Therefore, a client might receive other error codes.</span></span>  

 <span data-ttu-id="c7f91-145">Azure Key Vault also returns error information in the response body when a problem occurs.</span><span class="sxs-lookup"><span data-stu-id="c7f91-145">Azure Key Vault also returns error information in the response body when a problem occurs.</span></span> <span data-ttu-id="c7f91-146">The response body is JSON formatted and takes the form:</span><span class="sxs-lookup"><span data-stu-id="c7f91-146">The response body is JSON formatted and takes the form:</span></span>  

```  

{  
  "error":  
  {  
    "code": "BadArgument",  
    "message":  

      "’Foo’ is not a valid argument for ‘type’."  
    }  
  }  
}  

```  

## <a name="authentication"></a><span data-ttu-id="c7f91-147">Authentication</span><span class="sxs-lookup"><span data-stu-id="c7f91-147">Authentication</span></span>  
 <span data-ttu-id="c7f91-148">All requests to Azure Key Vault MUST be authenticated.</span><span class="sxs-lookup"><span data-stu-id="c7f91-148">All requests to Azure Key Vault MUST be authenticated.</span></span> <span data-ttu-id="c7f91-149">Azure Key Vault supports Azure Active Directory access tokens that may be obtained using OAuth2 [[RFC6749](http://tools.ietf.org/html/rfc6749)].</span><span class="sxs-lookup"><span data-stu-id="c7f91-149">Azure Key Vault supports Azure Active Directory access tokens that may be obtained using OAuth2 [[RFC6749](http://tools.ietf.org/html/rfc6749)].</span></span> 
 
 <span data-ttu-id="c7f91-150">For more information on registering your application and authenticating to use Azure Key Vault, see [Register your client application with Azure AD](https://docs.microsoft.com/rest/api/azure/index#register-your-client-application-with-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="c7f91-150">For more information on registering your application and authenticating to use Azure Key Vault, see [Register your client application with Azure AD](https://docs.microsoft.com/rest/api/azure/index#register-your-client-application-with-azure-ad).</span></span>
 
 <span data-ttu-id="c7f91-151">Access tokens must be sent to the service using the HTTP Authorization header:</span><span class="sxs-lookup"><span data-stu-id="c7f91-151">Access tokens must be sent to the service using the HTTP Authorization header:</span></span>  

```  
PUT /keys/MYKEY?api-version=<api_version>  HTTP/1.1  
Authorization: Bearer <access_token>  

```  

 <span data-ttu-id="c7f91-152">When an access token is not supplied, or when a token is not accepted by the service, an HTTP 401 error will be returned to the client and will include the WWW-Authenticate header, for example:</span><span class="sxs-lookup"><span data-stu-id="c7f91-152">When an access token is not supplied, or when a token is not accepted by the service, an HTTP 401 error will be returned to the client and will include the WWW-Authenticate header, for example:</span></span>  

```  
401 Not Authorized  
WWW-Authenticate: Bearer authorization="…", resource="…"  

```  

 <span data-ttu-id="c7f91-153">The parameters on the WWW-Authenticate header are:</span><span class="sxs-lookup"><span data-stu-id="c7f91-153">The parameters on the WWW-Authenticate header are:</span></span>  

-   <span data-ttu-id="c7f91-154">authorization: The address of the OAuth2 authorization service that may be used to obtain an access token for the request.</span><span class="sxs-lookup"><span data-stu-id="c7f91-154">authorization: The address of the OAuth2 authorization service that may be used to obtain an access token for the request.</span></span>  

-   <span data-ttu-id="c7f91-155">resource: The name of the resource to use in the authorization request.</span><span class="sxs-lookup"><span data-stu-id="c7f91-155">resource: The name of the resource to use in the authorization request.</span></span>  

## <a name="see-also"></a><span data-ttu-id="c7f91-156">See Also</span><span class="sxs-lookup"><span data-stu-id="c7f91-156">See Also</span></span>  
 [<span data-ttu-id="c7f91-157">About keys, secrets, and certificates</span><span class="sxs-lookup"><span data-stu-id="c7f91-157">About keys, secrets, and certificates</span></span>](about-keys-secrets-and-certificates.md)
