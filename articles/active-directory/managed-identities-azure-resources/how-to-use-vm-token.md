---
title: How to use managed identities for Azure resources on a virtual machine to acquire an access token
description: Step by step instructions and examples for using managed identities for Azure resources on a virtual machines to acquire an OAuth access token.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/01/2017
ms.author: daveba
ms.openlocfilehash: 86830d8a13e4d83ff48bcf7e2f2dfac41d764718
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857253"
---
# <a name="how-to-use-managed-identities-for-azure-resources-on-an-azure-vm-to-acquire-an-access-token"></a><span data-ttu-id="31300-103">How to use managed identities for Azure resources on an Azure VM to acquire an access token</span><span class="sxs-lookup"><span data-stu-id="31300-103">How to use managed identities for Azure resources on an Azure VM to acquire an access token</span></span> 

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]  

<span data-ttu-id="31300-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="31300-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span></span> <span data-ttu-id="31300-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="31300-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span></span> 

<span data-ttu-id="31300-106">This article provides various code and script examples for token acquisition, as well as guidance on important topics such as handling token expiration and HTTP errors.</span><span class="sxs-lookup"><span data-stu-id="31300-106">This article provides various code and script examples for token acquisition, as well as guidance on important topics such as handling token expiration and HTTP errors.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="31300-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="31300-107">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

<span data-ttu-id="31300-108">If you plan to use the Azure PowerShell examples in this article, be sure to install the latest version of [Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM).</span><span class="sxs-lookup"><span data-stu-id="31300-108">If you plan to use the Azure PowerShell examples in this article, be sure to install the latest version of [Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM).</span></span>


> [!IMPORTANT]
> - <span data-ttu-id="31300-109">All sample code/script in this article assumes the client is running on a virtual machine with managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="31300-109">All sample code/script in this article assumes the client is running on a virtual machine with managed identities for Azure resources.</span></span> <span data-ttu-id="31300-110">Use the virtual machine "Connect" feature in the Azure portal, to remotely connect to your VM.</span><span class="sxs-lookup"><span data-stu-id="31300-110">Use the virtual machine "Connect" feature in the Azure portal, to remotely connect to your VM.</span></span> <span data-ttu-id="31300-111">For details on enabling managed identities for Azure resources on a VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md), or one of the variant articles (using PowerShell, CLI, a template, or an Azure SDK).</span><span class="sxs-lookup"><span data-stu-id="31300-111">For details on enabling managed identities for Azure resources on a VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md), or one of the variant articles (using PowerShell, CLI, a template, or an Azure SDK).</span></span> 

> [!IMPORTANT]
> - <span data-ttu-id="31300-112">The security boundary of managed identities for Azure resources, is the resource it's being used on.</span><span class="sxs-lookup"><span data-stu-id="31300-112">The security boundary of managed identities for Azure resources, is the resource it's being used on.</span></span> <span data-ttu-id="31300-113">All code/scripts running on a virtual machine can request and retrieve tokens for any managed identities available on it.</span><span class="sxs-lookup"><span data-stu-id="31300-113">All code/scripts running on a virtual machine can request and retrieve tokens for any managed identities available on it.</span></span> 

## <a name="overview"></a><span data-ttu-id="31300-114">Overview</span><span class="sxs-lookup"><span data-stu-id="31300-114">Overview</span></span>

<span data-ttu-id="31300-115">A client application can request managed identities for Azure resources [app-only access token](../develop/developer-glossary.md#access-token) for accessing a given resource.</span><span class="sxs-lookup"><span data-stu-id="31300-115">A client application can request managed identities for Azure resources [app-only access token](../develop/developer-glossary.md#access-token) for accessing a given resource.</span></span> <span data-ttu-id="31300-116">The token is [based on the managed identities for Azure resources service principal](overview.md#how-does-it-work).</span><span class="sxs-lookup"><span data-stu-id="31300-116">The token is [based on the managed identities for Azure resources service principal](overview.md#how-does-it-work).</span></span> <span data-ttu-id="31300-117">As such, there is no need for the client to register itself to obtain an access token under its own service principal.</span><span class="sxs-lookup"><span data-stu-id="31300-117">As such, there is no need for the client to register itself to obtain an access token under its own service principal.</span></span> <span data-ttu-id="31300-118">The token is suitable for use as a bearer token in [service-to-service calls requiring client credentials](../develop/v1-oauth2-client-creds-grant-flow.md).</span><span class="sxs-lookup"><span data-stu-id="31300-118">The token is suitable for use as a bearer token in [service-to-service calls requiring client credentials](../develop/v1-oauth2-client-creds-grant-flow.md).</span></span>

|  |  |
| -------------- | -------------------- |
| [<span data-ttu-id="31300-119">Get a token using HTTP</span><span class="sxs-lookup"><span data-stu-id="31300-119">Get a token using HTTP</span></span>](#get-a-token-using-http) | <span data-ttu-id="31300-120">Protocol details for managed identities for Azure resources token endpoint</span><span class="sxs-lookup"><span data-stu-id="31300-120">Protocol details for managed identities for Azure resources token endpoint</span></span> |
| [<span data-ttu-id="31300-121">Get a token using the Microsoft.Azure.Services.AppAuthentication library for .NET</span><span class="sxs-lookup"><span data-stu-id="31300-121">Get a token using the Microsoft.Azure.Services.AppAuthentication library for .NET</span></span>](#get-a-token-using-the-microsoftazureservicesappauthentication-library-for-net) | <span data-ttu-id="31300-122">Example of using the Microsoft.Azure.Services.AppAuthentication library from a .NET client</span><span class="sxs-lookup"><span data-stu-id="31300-122">Example of using the Microsoft.Azure.Services.AppAuthentication library from a .NET client</span></span>
| [<span data-ttu-id="31300-123">Get a token using C#</span><span class="sxs-lookup"><span data-stu-id="31300-123">Get a token using C#</span></span>](#get-a-token-using-c) | <span data-ttu-id="31300-124">Example of using managed identities for Azure resources REST endpoint from a C# client</span><span class="sxs-lookup"><span data-stu-id="31300-124">Example of using managed identities for Azure resources REST endpoint from a C# client</span></span> |
| [<span data-ttu-id="31300-125">Get a token using Go</span><span class="sxs-lookup"><span data-stu-id="31300-125">Get a token using Go</span></span>](#get-a-token-using-go) | <span data-ttu-id="31300-126">Example of using managed identities for Azure resources REST endpoint from a Go client</span><span class="sxs-lookup"><span data-stu-id="31300-126">Example of using managed identities for Azure resources REST endpoint from a Go client</span></span> |
| [<span data-ttu-id="31300-127">Get a token using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="31300-127">Get a token using Azure PowerShell</span></span>](#get-a-token-using-azure-powershell) | <span data-ttu-id="31300-128">Example of using managed identities for Azure resources REST endpoint from a PowerShell client</span><span class="sxs-lookup"><span data-stu-id="31300-128">Example of using managed identities for Azure resources REST endpoint from a PowerShell client</span></span> |
| [<span data-ttu-id="31300-129">Get a token using CURL</span><span class="sxs-lookup"><span data-stu-id="31300-129">Get a token using CURL</span></span>](#get-a-token-using-curl) | <span data-ttu-id="31300-130">Example of using managed identities for Azure resources REST endpoint from a Bash/CURL client</span><span class="sxs-lookup"><span data-stu-id="31300-130">Example of using managed identities for Azure resources REST endpoint from a Bash/CURL client</span></span> |
| [<span data-ttu-id="31300-131">Handling token caching</span><span class="sxs-lookup"><span data-stu-id="31300-131">Handling token caching</span></span>](#handling-token-caching) | <span data-ttu-id="31300-132">Guidance for handling expired access tokens</span><span class="sxs-lookup"><span data-stu-id="31300-132">Guidance for handling expired access tokens</span></span> |
| [<span data-ttu-id="31300-133">Error handling</span><span class="sxs-lookup"><span data-stu-id="31300-133">Error handling</span></span>](#error-handling) | <span data-ttu-id="31300-134">Guidance for handling HTTP errors returned from the managed identities for Azure resources token endpoint</span><span class="sxs-lookup"><span data-stu-id="31300-134">Guidance for handling HTTP errors returned from the managed identities for Azure resources token endpoint</span></span> |
| [<span data-ttu-id="31300-135">Resource IDs for Azure services</span><span class="sxs-lookup"><span data-stu-id="31300-135">Resource IDs for Azure services</span></span>](#resource-ids-for-azure-services) | <span data-ttu-id="31300-136">Where to get resource IDs for supported Azure services</span><span class="sxs-lookup"><span data-stu-id="31300-136">Where to get resource IDs for supported Azure services</span></span> |

## <a name="get-a-token-using-http"></a><span data-ttu-id="31300-137">Get a token using HTTP</span><span class="sxs-lookup"><span data-stu-id="31300-137">Get a token using HTTP</span></span> 

<span data-ttu-id="31300-138">The fundamental interface for acquiring an access token is based on REST, making it accessible to any client application running on the VM that can make HTTP REST calls.</span><span class="sxs-lookup"><span data-stu-id="31300-138">The fundamental interface for acquiring an access token is based on REST, making it accessible to any client application running on the VM that can make HTTP REST calls.</span></span> <span data-ttu-id="31300-139">This is similar to the Azure AD programming model, except the client uses an endpoint on the virtual machine (vs an Azure AD endpoint).</span><span class="sxs-lookup"><span data-stu-id="31300-139">This is similar to the Azure AD programming model, except the client uses an endpoint on the virtual machine (vs an Azure AD endpoint).</span></span>

<span data-ttu-id="31300-140">Sample request using the Azure Instance Metadata Service (IMDS) endpoint *(recommended)*:</span><span class="sxs-lookup"><span data-stu-id="31300-140">Sample request using the Azure Instance Metadata Service (IMDS) endpoint *(recommended)*:</span></span>

```
GET 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/' HTTP/1.1 Metadata: true
```

| <span data-ttu-id="31300-141">Element</span><span class="sxs-lookup"><span data-stu-id="31300-141">Element</span></span> | <span data-ttu-id="31300-142">Description</span><span class="sxs-lookup"><span data-stu-id="31300-142">Description</span></span> |
| ------- | ----------- |
| `GET` | <span data-ttu-id="31300-143">The HTTP verb, indicating you want to retrieve data from the endpoint.</span><span class="sxs-lookup"><span data-stu-id="31300-143">The HTTP verb, indicating you want to retrieve data from the endpoint.</span></span> <span data-ttu-id="31300-144">In this case, an OAuth access token.</span><span class="sxs-lookup"><span data-stu-id="31300-144">In this case, an OAuth access token.</span></span> | 
| `http://169.254.169.254/metadata/identity/oauth2/token` | <span data-ttu-id="31300-145">The managed identities for Azure resources endpoint for the Instance Metadata Service.</span><span class="sxs-lookup"><span data-stu-id="31300-145">The managed identities for Azure resources endpoint for the Instance Metadata Service.</span></span> |
| `api-version`  | <span data-ttu-id="31300-146">A query string parameter, indicating the API version for the IMDS endpoint.</span><span class="sxs-lookup"><span data-stu-id="31300-146">A query string parameter, indicating the API version for the IMDS endpoint.</span></span> <span data-ttu-id="31300-147">Please use API version `2018-02-01` or greater.</span><span class="sxs-lookup"><span data-stu-id="31300-147">Please use API version `2018-02-01` or greater.</span></span> |
| `resource` | <span data-ttu-id="31300-148">A query string parameter, indicating the App ID URI of the target resource.</span><span class="sxs-lookup"><span data-stu-id="31300-148">A query string parameter, indicating the App ID URI of the target resource.</span></span> <span data-ttu-id="31300-149">It also appears in the `aud` (audience) claim of the issued token.</span><span class="sxs-lookup"><span data-stu-id="31300-149">It also appears in the `aud` (audience) claim of the issued token.</span></span> <span data-ttu-id="31300-150">This example requests a token to access Azure Resource Manager, which has an App ID URI of https://management.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="31300-150">This example requests a token to access Azure Resource Manager, which has an App ID URI of https://management.azure.com/.</span></span> |
| `Metadata` | <span data-ttu-id="31300-151">An HTTP request header field, required by managed identities for Azure resources as a mitigation against Server Side Request Forgery (SSRF) attack.</span><span class="sxs-lookup"><span data-stu-id="31300-151">An HTTP request header field, required by managed identities for Azure resources as a mitigation against Server Side Request Forgery (SSRF) attack.</span></span> <span data-ttu-id="31300-152">This value must be set to "true", in all lower case.</span><span class="sxs-lookup"><span data-stu-id="31300-152">This value must be set to "true", in all lower case.</span></span> |
| `object_id` | <span data-ttu-id="31300-153">(Optional) A query string parameter, indicating the object_id of the managed identity you would like the token for.</span><span class="sxs-lookup"><span data-stu-id="31300-153">(Optional) A query string parameter, indicating the object_id of the managed identity you would like the token for.</span></span> <span data-ttu-id="31300-154">Required, if your VM has multiple user-assigned managed identities.</span><span class="sxs-lookup"><span data-stu-id="31300-154">Required, if your VM has multiple user-assigned managed identities.</span></span>|
| `client_id` | <span data-ttu-id="31300-155">(Optional) A query string parameter, indicating the client_id of the managed identity you would like the token for.</span><span class="sxs-lookup"><span data-stu-id="31300-155">(Optional) A query string parameter, indicating the client_id of the managed identity you would like the token for.</span></span> <span data-ttu-id="31300-156">Required, if your VM has multiple user-assigned managed identities.</span><span class="sxs-lookup"><span data-stu-id="31300-156">Required, if your VM has multiple user-assigned managed identities.</span></span>|

<span data-ttu-id="31300-157">Sample request using the managed identities for Azure resources VM Extension Endpoint *(planned for deprecation in January 2019)*:</span><span class="sxs-lookup"><span data-stu-id="31300-157">Sample request using the managed identities for Azure resources VM Extension Endpoint *(planned for deprecation in January 2019)*:</span></span>

```
GET http://localhost:50342/oauth2/token?resource=https%3A%2F%2Fmanagement.azure.com%2F HTTP/1.1
Metadata: true
```

| <span data-ttu-id="31300-158">Element</span><span class="sxs-lookup"><span data-stu-id="31300-158">Element</span></span> | <span data-ttu-id="31300-159">Description</span><span class="sxs-lookup"><span data-stu-id="31300-159">Description</span></span> |
| ------- | ----------- |
| `GET` | <span data-ttu-id="31300-160">The HTTP verb, indicating you want to retrieve data from the endpoint.</span><span class="sxs-lookup"><span data-stu-id="31300-160">The HTTP verb, indicating you want to retrieve data from the endpoint.</span></span> <span data-ttu-id="31300-161">In this case, an OAuth access token.</span><span class="sxs-lookup"><span data-stu-id="31300-161">In this case, an OAuth access token.</span></span> | 
| `http://localhost:50342/oauth2/token` | <span data-ttu-id="31300-162">The managed identities for Azure resources endpoint, where 50342 is the default port and is configurable.</span><span class="sxs-lookup"><span data-stu-id="31300-162">The managed identities for Azure resources endpoint, where 50342 is the default port and is configurable.</span></span> |
| `resource` | <span data-ttu-id="31300-163">A query string parameter, indicating the App ID URI of the target resource.</span><span class="sxs-lookup"><span data-stu-id="31300-163">A query string parameter, indicating the App ID URI of the target resource.</span></span> <span data-ttu-id="31300-164">It also appears in the `aud` (audience) claim of the issued token.</span><span class="sxs-lookup"><span data-stu-id="31300-164">It also appears in the `aud` (audience) claim of the issued token.</span></span> <span data-ttu-id="31300-165">This example requests a token to access Azure Resource Manager, which has an App ID URI of https://management.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="31300-165">This example requests a token to access Azure Resource Manager, which has an App ID URI of https://management.azure.com/.</span></span> |
| `Metadata` | <span data-ttu-id="31300-166">An HTTP request header field, required by managed identities for Azure resources as a mitigation against Server Side Request Forgery (SSRF) attack.</span><span class="sxs-lookup"><span data-stu-id="31300-166">An HTTP request header field, required by managed identities for Azure resources as a mitigation against Server Side Request Forgery (SSRF) attack.</span></span> <span data-ttu-id="31300-167">This value must be set to "true", in all lower case.</span><span class="sxs-lookup"><span data-stu-id="31300-167">This value must be set to "true", in all lower case.</span></span>|
| `object_id` | <span data-ttu-id="31300-168">(Optional) A query string parameter, indicating the object_id of the managed identity you would like the token for.</span><span class="sxs-lookup"><span data-stu-id="31300-168">(Optional) A query string parameter, indicating the object_id of the managed identity you would like the token for.</span></span> <span data-ttu-id="31300-169">Required, if your VM has multiple user-assigned managed identities.</span><span class="sxs-lookup"><span data-stu-id="31300-169">Required, if your VM has multiple user-assigned managed identities.</span></span>|
| `client_id` | <span data-ttu-id="31300-170">(Optional) A query string parameter, indicating the client_id of the managed identity you would like the token for.</span><span class="sxs-lookup"><span data-stu-id="31300-170">(Optional) A query string parameter, indicating the client_id of the managed identity you would like the token for.</span></span> <span data-ttu-id="31300-171">Required, if your VM has multiple user-assigned managed identities.</span><span class="sxs-lookup"><span data-stu-id="31300-171">Required, if your VM has multiple user-assigned managed identities.</span></span>|


<span data-ttu-id="31300-172">Sample response:</span><span class="sxs-lookup"><span data-stu-id="31300-172">Sample response:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "access_token": "eyJ0eXAi...",
  "refresh_token": "",
  "expires_in": "3599",
  "expires_on": "1506484173",
  "not_before": "1506480273",
  "resource": "https://management.azure.com/",
  "token_type": "Bearer"
}
```

| <span data-ttu-id="31300-173">Element</span><span class="sxs-lookup"><span data-stu-id="31300-173">Element</span></span> | <span data-ttu-id="31300-174">Description</span><span class="sxs-lookup"><span data-stu-id="31300-174">Description</span></span> |
| ------- | ----------- |
| `access_token` | <span data-ttu-id="31300-175">The requested access token.</span><span class="sxs-lookup"><span data-stu-id="31300-175">The requested access token.</span></span> <span data-ttu-id="31300-176">When calling a secured REST API, the token is embedded in the `Authorization` request header field as a "bearer" token, allowing the API to authenticate the caller.</span><span class="sxs-lookup"><span data-stu-id="31300-176">When calling a secured REST API, the token is embedded in the `Authorization` request header field as a "bearer" token, allowing the API to authenticate the caller.</span></span> | 
| `refresh_token` | <span data-ttu-id="31300-177">Not used by managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="31300-177">Not used by managed identities for Azure resources.</span></span> |
| `expires_in` | <span data-ttu-id="31300-178">The number of seconds the access token continues to be valid, before expiring, from time of issuance.</span><span class="sxs-lookup"><span data-stu-id="31300-178">The number of seconds the access token continues to be valid, before expiring, from time of issuance.</span></span> <span data-ttu-id="31300-179">Time of issuance can be found in the token's `iat` claim.</span><span class="sxs-lookup"><span data-stu-id="31300-179">Time of issuance can be found in the token's `iat` claim.</span></span> |
| `expires_on` | <span data-ttu-id="31300-180">The timespan when the access token expires.</span><span class="sxs-lookup"><span data-stu-id="31300-180">The timespan when the access token expires.</span></span> <span data-ttu-id="31300-181">The date is represented as the number of seconds from "1970-01-01T0:0:0Z UTC"  (corresponds to the token's `exp` claim).</span><span class="sxs-lookup"><span data-stu-id="31300-181">The date is represented as the number of seconds from "1970-01-01T0:0:0Z UTC"  (corresponds to the token's `exp` claim).</span></span> |
| `not_before` | <span data-ttu-id="31300-182">The timespan when the access token takes effect, and can be accepted.</span><span class="sxs-lookup"><span data-stu-id="31300-182">The timespan when the access token takes effect, and can be accepted.</span></span> <span data-ttu-id="31300-183">The date is represented as the number of seconds from "1970-01-01T0:0:0Z UTC" (corresponds to the token's `nbf` claim).</span><span class="sxs-lookup"><span data-stu-id="31300-183">The date is represented as the number of seconds from "1970-01-01T0:0:0Z UTC" (corresponds to the token's `nbf` claim).</span></span> |
| `resource` | <span data-ttu-id="31300-184">The resource the access token was requested for, which matches the `resource` query string parameter of the request.</span><span class="sxs-lookup"><span data-stu-id="31300-184">The resource the access token was requested for, which matches the `resource` query string parameter of the request.</span></span> |
| `token_type` | <span data-ttu-id="31300-185">The type of token, which is a "Bearer" access token, which means the resource can give access to the bearer of this token.</span><span class="sxs-lookup"><span data-stu-id="31300-185">The type of token, which is a "Bearer" access token, which means the resource can give access to the bearer of this token.</span></span> |

## <a name="get-a-token-using-the-microsoftazureservicesappauthentication-library-for-net"></a><span data-ttu-id="31300-186">Get a token using the Microsoft.Azure.Services.AppAuthentication library for .NET</span><span class="sxs-lookup"><span data-stu-id="31300-186">Get a token using the Microsoft.Azure.Services.AppAuthentication library for .NET</span></span>

<span data-ttu-id="31300-187">For .NET applications and functions, the simplest way to work with managed identities for Azure resources is through the Microsoft.Azure.Services.AppAuthentication package.</span><span class="sxs-lookup"><span data-stu-id="31300-187">For .NET applications and functions, the simplest way to work with managed identities for Azure resources is through the Microsoft.Azure.Services.AppAuthentication package.</span></span> <span data-ttu-id="31300-188">This library will also allow you to test your code locally on your development machine, using your user account from Visual Studio, the [Azure CLI](https://docs.microsoft.com/cli/azure?view=azure-cli-latest), or Active Directory Integrated Authentication.</span><span class="sxs-lookup"><span data-stu-id="31300-188">This library will also allow you to test your code locally on your development machine, using your user account from Visual Studio, the [Azure CLI](https://docs.microsoft.com/cli/azure?view=azure-cli-latest), or Active Directory Integrated Authentication.</span></span> <span data-ttu-id="31300-189">For more on local development options with this library, see the [Microsoft.Azure.Services.AppAuthentication reference].</span><span class="sxs-lookup"><span data-stu-id="31300-189">For more on local development options with this library, see the [Microsoft.Azure.Services.AppAuthentication reference].</span></span> <span data-ttu-id="31300-190">This section shows you how to get started with the library in your code.</span><span class="sxs-lookup"><span data-stu-id="31300-190">This section shows you how to get started with the library in your code.</span></span>

1. <span data-ttu-id="31300-191">Add references to the [Microsoft.Azure.Services.AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) and [Microsoft.Azure.KeyVault](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) NuGet packages to your application.</span><span class="sxs-lookup"><span data-stu-id="31300-191">Add references to the [Microsoft.Azure.Services.AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) and [Microsoft.Azure.KeyVault](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) NuGet packages to your application.</span></span>

2.  <span data-ttu-id="31300-192">Add the following code to your application:</span><span class="sxs-lookup"><span data-stu-id="31300-192">Add the following code to your application:</span></span>

    ```csharp
    using Microsoft.Azure.Services.AppAuthentication;
    using Microsoft.Azure.KeyVault;
    // ...
    var azureServiceTokenProvider = new AzureServiceTokenProvider();
    string accessToken = await azureServiceTokenProvider.GetAccessTokenAsync("https://management.azure.com/");
    // OR
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(azureServiceTokenProvider.KeyVaultTokenCallback));
    ```
    
<span data-ttu-id="31300-193">To learn more about Microsoft.Azure.Services.AppAuthentication and the operations it exposes, see the [Microsoft.Azure.Services.AppAuthentication reference](/azure/key-vault/service-to-service-authentication) and the [App Service and KeyVault with managed identities for Azure resources .NET sample](https://github.com/Azure-Samples/app-service-msi-keyvault-dotnet).</span><span class="sxs-lookup"><span data-stu-id="31300-193">To learn more about Microsoft.Azure.Services.AppAuthentication and the operations it exposes, see the [Microsoft.Azure.Services.AppAuthentication reference](/azure/key-vault/service-to-service-authentication) and the [App Service and KeyVault with managed identities for Azure resources .NET sample](https://github.com/Azure-Samples/app-service-msi-keyvault-dotnet).</span></span>

## <a name="get-a-token-using-c"></a><span data-ttu-id="31300-194">Get a token using C#</span><span class="sxs-lookup"><span data-stu-id="31300-194">Get a token using C#</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Net;
using System.Web.Script.Serialization; 

// Build request to acquire managed identities for Azure resources token
HttpWebRequest request = (HttpWebRequest)WebRequest.Create(http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/");
request.Headers["Metadata"] = "true";
request.Method = "GET";

try
{
    // Call /token endpoint
    HttpWebResponse response = (HttpWebResponse)request.GetResponse();

    // Pipe response Stream to a StreamReader, and extract access token
    StreamReader streamResponse = new StreamReader(response.GetResponseStream()); 
    string stringResponse = streamResponse.ReadToEnd();
    JavaScriptSerializer j = new JavaScriptSerializer();
    Dictionary<string, string> list = (Dictionary<string, string>) j.Deserialize(stringResponse, typeof(Dictionary<string, string>));
    string accessToken = list["access_token"];
}
catch (Exception e)
{
    string errorText = String.Format("{0} \n\n{1}", e.Message, e.InnerException != null ? e.InnerException.Message : "Acquire token failed");
}

```

## <a name="get-a-token-using-go"></a><span data-ttu-id="31300-195">Get a token using Go</span><span class="sxs-lookup"><span data-stu-id="31300-195">Get a token using Go</span></span>

```
package main

import (
  "fmt"
  "io/ioutil"
  "net/http"
  "net/url"
  "encoding/json"
)

type responseJson struct {
  AccessToken string `json:"access_token"`
  RefreshToken string `json:"refresh_token"`
  ExpiresIn string `json:"expires_in"`
  ExpiresOn string `json:"expires_on"`
  NotBefore string `json:"not_before"`
  Resource string `json:"resource"`
  TokenType string `json:"token_type"`
}

func main() {
    
    // Create HTTP request for a managed services for Azure resources token to access Azure Resource Manager
    var msi_endpoint *url.URL
    msi_endpoint, err := url.Parse("http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01")
    if err != nil {
      fmt.Println("Error creating URL: ", err)
      return 
    }
    msi_parameters := url.Values{}
    msi_parameters.Add("resource", "https://management.azure.com/")
    msi_endpoint.RawQuery = msi_parameters.Encode()
    req, err := http.NewRequest("GET", msi_endpoint.String(), nil)
    if err != nil {
      fmt.Println("Error creating HTTP request: ", err)
      return 
    }
    req.Header.Add("Metadata", "true")

    // Call managed services for Azure resources token endpoint
    client := &http.Client{}
    resp, err := client.Do(req) 
    if err != nil{
      fmt.Println("Error calling token endpoint: ", err)
      return
    }

    // Pull out response body
    responseBytes,err := ioutil.ReadAll(resp.Body)
    defer resp.Body.Close()
    if err != nil {
      fmt.Println("Error reading response body : ", err)
      return
    }

    // Unmarshall response body into struct
    var r responseJson
    err = json.Unmarshal(responseBytes, &r)
    if err != nil {
      fmt.Println("Error unmarshalling the response:", err)
      return
    }

    // Print HTTP response and marshalled response body elements to console
    fmt.Println("Response status:", resp.Status)
    fmt.Println("access_token: ", r.AccessToken)
    fmt.Println("refresh_token: ", r.RefreshToken)
    fmt.Println("expires_in: ", r.ExpiresIn)
    fmt.Println("expires_on: ", r.ExpiresOn)
    fmt.Println("not_before: ", r.NotBefore)
    fmt.Println("resource: ", r.Resource)
    fmt.Println("token_type: ", r.TokenType)
}
```

## <a name="get-a-token-using-azure-powershell"></a><span data-ttu-id="31300-196">Get a token using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="31300-196">Get a token using Azure PowerShell</span></span>

<span data-ttu-id="31300-197">The following example demonstrates how to use the managed identities for Azure resources REST endpoint from a PowerShell client to:</span><span class="sxs-lookup"><span data-stu-id="31300-197">The following example demonstrates how to use the managed identities for Azure resources REST endpoint from a PowerShell client to:</span></span>

1. <span data-ttu-id="31300-198">Acquire an access token.</span><span class="sxs-lookup"><span data-stu-id="31300-198">Acquire an access token.</span></span>
2. <span data-ttu-id="31300-199">Use the access token to call an Azure Resource Manager REST API and get information about the VM.</span><span class="sxs-lookup"><span data-stu-id="31300-199">Use the access token to call an Azure Resource Manager REST API and get information about the VM.</span></span> <span data-ttu-id="31300-200">Be sure to substitute your subscription ID, resource group name, and virtual machine name for `<SUBSCRIPTION-ID>`, `<RESOURCE-GROUP>`, and `<VM-NAME>`, respectively.</span><span class="sxs-lookup"><span data-stu-id="31300-200">Be sure to substitute your subscription ID, resource group name, and virtual machine name for `<SUBSCRIPTION-ID>`, `<RESOURCE-GROUP>`, and `<VM-NAME>`, respectively.</span></span>

```azurepowershell
Invoke-WebRequest -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -Headers @{Metadata="true"}
```

<span data-ttu-id="31300-201">Example on how to parse the access token from the response:</span><span class="sxs-lookup"><span data-stu-id="31300-201">Example on how to parse the access token from the response:</span></span>
```azurepowershell
# Get an access token for managed identities for Azure resources
$response = Invoke-WebRequest -Uri http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F `
                              -Headers @{Metadata="true"}
$content =$response.Content | ConvertFrom-Json
$access_token = $content.access_token
echo "The managed identities for Azure resources access token is $access_token"

# Use the access token to get resource information for the VM
$vmInfoRest = (Invoke-WebRequest -Uri https://management.azure.com/subscriptions/<SUBSCRIPTION-ID>/resourceGroups/<RESOURCE-GROUP>/providers/Microsoft.Compute/virtualMachines/<VM-NAME>?api-version=2017-12-01 -Method GET -ContentType "application/json" -Headers @{ Authorization ="Bearer $access_token"}).content
echo "JSON returned from call to get VM info:"
echo $vmInfoRest

```

## <a name="get-a-token-using-curl"></a><span data-ttu-id="31300-202">Get a token using CURL</span><span class="sxs-lookup"><span data-stu-id="31300-202">Get a token using CURL</span></span>

```bash
curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -H Metadata:true -s
```


<span data-ttu-id="31300-203">Example on how to parse the access token from the response:</span><span class="sxs-lookup"><span data-stu-id="31300-203">Example on how to parse the access token from the response:</span></span>

```bash
response=$(curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -H Metadata:true -s)
access_token=$(echo $response | python -c 'import sys, json; print (json.load(sys.stdin)["access_token"])')
echo The managed identities for Azure resources access token is $access_token
```

## <a name="token-caching"></a><span data-ttu-id="31300-204">Token caching</span><span class="sxs-lookup"><span data-stu-id="31300-204">Token caching</span></span>

<span data-ttu-id="31300-205">While the managed identities for Azure resources subsystem being used (IMDS/managed identities for Azure resources VM Extension) does cache tokens, we also recommend to implement token caching in your code.</span><span class="sxs-lookup"><span data-stu-id="31300-205">While the managed identities for Azure resources subsystem being used (IMDS/managed identities for Azure resources VM Extension) does cache tokens, we also recommend to implement token caching in your code.</span></span> <span data-ttu-id="31300-206">As a result, you should prepare for scenarios where the resource indicates that the token is expired.</span><span class="sxs-lookup"><span data-stu-id="31300-206">As a result, you should prepare for scenarios where the resource indicates that the token is expired.</span></span> 

<span data-ttu-id="31300-207">On-the-wire calls to Azure AD result only when:</span><span class="sxs-lookup"><span data-stu-id="31300-207">On-the-wire calls to Azure AD result only when:</span></span>
- <span data-ttu-id="31300-208">cache miss occurs due to no token in the managed identities for Azure resources subsystem cache</span><span class="sxs-lookup"><span data-stu-id="31300-208">cache miss occurs due to no token in the managed identities for Azure resources subsystem cache</span></span>
- <span data-ttu-id="31300-209">the cached token is expired</span><span class="sxs-lookup"><span data-stu-id="31300-209">the cached token is expired</span></span>

## <a name="error-handling"></a><span data-ttu-id="31300-210">Error handling</span><span class="sxs-lookup"><span data-stu-id="31300-210">Error handling</span></span>

<span data-ttu-id="31300-211">The managed identities for Azure resources endpoint signals errors via the status code field of the HTTP response message header, as either 4xx or 5xx errors:</span><span class="sxs-lookup"><span data-stu-id="31300-211">The managed identities for Azure resources endpoint signals errors via the status code field of the HTTP response message header, as either 4xx or 5xx errors:</span></span>

| <span data-ttu-id="31300-212">Status Code</span><span class="sxs-lookup"><span data-stu-id="31300-212">Status Code</span></span> | <span data-ttu-id="31300-213">Error Reason</span><span class="sxs-lookup"><span data-stu-id="31300-213">Error Reason</span></span> | <span data-ttu-id="31300-214">How To Handle</span><span class="sxs-lookup"><span data-stu-id="31300-214">How To Handle</span></span> |
| ----------- | ------------ | ------------- |
| <span data-ttu-id="31300-215">404 Not found.</span><span class="sxs-lookup"><span data-stu-id="31300-215">404 Not found.</span></span> | <span data-ttu-id="31300-216">IMDS endpoint is updating.</span><span class="sxs-lookup"><span data-stu-id="31300-216">IMDS endpoint is updating.</span></span> | <span data-ttu-id="31300-217">Retry with Expontential Backoff.</span><span class="sxs-lookup"><span data-stu-id="31300-217">Retry with Expontential Backoff.</span></span> <span data-ttu-id="31300-218">See guidance below.</span><span class="sxs-lookup"><span data-stu-id="31300-218">See guidance below.</span></span> |
| <span data-ttu-id="31300-219">429 Too many requests.</span><span class="sxs-lookup"><span data-stu-id="31300-219">429 Too many requests.</span></span> |  <span data-ttu-id="31300-220">IMDS Throttle limit reached.</span><span class="sxs-lookup"><span data-stu-id="31300-220">IMDS Throttle limit reached.</span></span> | <span data-ttu-id="31300-221">Retry with Exponential Backoff.</span><span class="sxs-lookup"><span data-stu-id="31300-221">Retry with Exponential Backoff.</span></span> <span data-ttu-id="31300-222">See guidance below.</span><span class="sxs-lookup"><span data-stu-id="31300-222">See guidance below.</span></span> |
| <span data-ttu-id="31300-223">4xx Error in request.</span><span class="sxs-lookup"><span data-stu-id="31300-223">4xx Error in request.</span></span> | <span data-ttu-id="31300-224">One or more of the request parameters was incorrect.</span><span class="sxs-lookup"><span data-stu-id="31300-224">One or more of the request parameters was incorrect.</span></span> | <span data-ttu-id="31300-225">Do not retry.</span><span class="sxs-lookup"><span data-stu-id="31300-225">Do not retry.</span></span>  <span data-ttu-id="31300-226">Examine the error details for more information.</span><span class="sxs-lookup"><span data-stu-id="31300-226">Examine the error details for more information.</span></span>  <span data-ttu-id="31300-227">4xx errors are design-time errors.</span><span class="sxs-lookup"><span data-stu-id="31300-227">4xx errors are design-time errors.</span></span>|
| <span data-ttu-id="31300-228">5xx Transient error from service.</span><span class="sxs-lookup"><span data-stu-id="31300-228">5xx Transient error from service.</span></span> | <span data-ttu-id="31300-229">The managed identities for Azure resources sub-system or Azure Active Directory returned a transient error.</span><span class="sxs-lookup"><span data-stu-id="31300-229">The managed identities for Azure resources sub-system or Azure Active Directory returned a transient error.</span></span> | <span data-ttu-id="31300-230">It is safe to retry after waiting for at least 1 second.</span><span class="sxs-lookup"><span data-stu-id="31300-230">It is safe to retry after waiting for at least 1 second.</span></span>  <span data-ttu-id="31300-231">If you retry too quickly or too often, IMDS and/or Azure AD may return a rate limit error (429).</span><span class="sxs-lookup"><span data-stu-id="31300-231">If you retry too quickly or too often, IMDS and/or Azure AD may return a rate limit error (429).</span></span>|
| <span data-ttu-id="31300-232">timeout</span><span class="sxs-lookup"><span data-stu-id="31300-232">timeout</span></span> | <span data-ttu-id="31300-233">IMDS endpoint is updating.</span><span class="sxs-lookup"><span data-stu-id="31300-233">IMDS endpoint is updating.</span></span> | <span data-ttu-id="31300-234">Retry with Expontential Backoff.</span><span class="sxs-lookup"><span data-stu-id="31300-234">Retry with Expontential Backoff.</span></span> <span data-ttu-id="31300-235">See guidance below.</span><span class="sxs-lookup"><span data-stu-id="31300-235">See guidance below.</span></span> |

<span data-ttu-id="31300-236">If an error occurs, the corresponding HTTP response body contains JSON with the error details:</span><span class="sxs-lookup"><span data-stu-id="31300-236">If an error occurs, the corresponding HTTP response body contains JSON with the error details:</span></span>

| <span data-ttu-id="31300-237">Element</span><span class="sxs-lookup"><span data-stu-id="31300-237">Element</span></span> | <span data-ttu-id="31300-238">Description</span><span class="sxs-lookup"><span data-stu-id="31300-238">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="31300-239">error</span><span class="sxs-lookup"><span data-stu-id="31300-239">error</span></span>   | <span data-ttu-id="31300-240">Error identifier.</span><span class="sxs-lookup"><span data-stu-id="31300-240">Error identifier.</span></span> |
| <span data-ttu-id="31300-241">error_description</span><span class="sxs-lookup"><span data-stu-id="31300-241">error_description</span></span> | <span data-ttu-id="31300-242">Verbose description of error.</span><span class="sxs-lookup"><span data-stu-id="31300-242">Verbose description of error.</span></span> <span data-ttu-id="31300-243">**Error descriptions can change at any time. Do not write code that branches based on values in the error description.**</span><span class="sxs-lookup"><span data-stu-id="31300-243">**Error descriptions can change at any time. Do not write code that branches based on values in the error description.**</span></span>|

### <a name="http-response-reference"></a><span data-ttu-id="31300-244">HTTP response reference</span><span class="sxs-lookup"><span data-stu-id="31300-244">HTTP response reference</span></span>

<span data-ttu-id="31300-245">This section documents the possible error responses.</span><span class="sxs-lookup"><span data-stu-id="31300-245">This section documents the possible error responses.</span></span> <span data-ttu-id="31300-246">A "200 OK" status is a successful response, and the access token is contained in the response body JSON, in the access_token element.</span><span class="sxs-lookup"><span data-stu-id="31300-246">A "200 OK" status is a successful response, and the access token is contained in the response body JSON, in the access_token element.</span></span>

| <span data-ttu-id="31300-247">Status code</span><span class="sxs-lookup"><span data-stu-id="31300-247">Status code</span></span> | <span data-ttu-id="31300-248">Error</span><span class="sxs-lookup"><span data-stu-id="31300-248">Error</span></span> | <span data-ttu-id="31300-249">Error Description</span><span class="sxs-lookup"><span data-stu-id="31300-249">Error Description</span></span> | <span data-ttu-id="31300-250">Solution</span><span class="sxs-lookup"><span data-stu-id="31300-250">Solution</span></span> |
| ----------- | ----- | ----------------- | -------- |
| <span data-ttu-id="31300-251">400 Bad Request</span><span class="sxs-lookup"><span data-stu-id="31300-251">400 Bad Request</span></span> | <span data-ttu-id="31300-252">invalid_resource</span><span class="sxs-lookup"><span data-stu-id="31300-252">invalid_resource</span></span> | <span data-ttu-id="31300-253">AADSTS50001: The application named *\<URI\>* was not found in the tenant named *\<TENANT-ID\>*.</span><span class="sxs-lookup"><span data-stu-id="31300-253">AADSTS50001: The application named *\<URI\>* was not found in the tenant named *\<TENANT-ID\>*.</span></span> <span data-ttu-id="31300-254">This can happen if the application has not been installed by the administrator of the tenant or consented to by any user in the tenant.</span><span class="sxs-lookup"><span data-stu-id="31300-254">This can happen if the application has not been installed by the administrator of the tenant or consented to by any user in the tenant.</span></span> <span data-ttu-id="31300-255">You might have sent your authentication request to the wrong tenant.\\</span><span class="sxs-lookup"><span data-stu-id="31300-255">You might have sent your authentication request to the wrong tenant.\\</span></span> | <span data-ttu-id="31300-256">(Linux only)</span><span class="sxs-lookup"><span data-stu-id="31300-256">(Linux only)</span></span> |
| <span data-ttu-id="31300-257">400 Bad Request</span><span class="sxs-lookup"><span data-stu-id="31300-257">400 Bad Request</span></span> | <span data-ttu-id="31300-258">bad_request_102</span><span class="sxs-lookup"><span data-stu-id="31300-258">bad_request_102</span></span> | <span data-ttu-id="31300-259">Required metadata header not specified</span><span class="sxs-lookup"><span data-stu-id="31300-259">Required metadata header not specified</span></span> | <span data-ttu-id="31300-260">Either the `Metadata` request header field is missing from your request, or is formatted incorrectly.</span><span class="sxs-lookup"><span data-stu-id="31300-260">Either the `Metadata` request header field is missing from your request, or is formatted incorrectly.</span></span> <span data-ttu-id="31300-261">The value must be specified as `true`, in all lower case.</span><span class="sxs-lookup"><span data-stu-id="31300-261">The value must be specified as `true`, in all lower case.</span></span> <span data-ttu-id="31300-262">See the "Sample request" in the [preceding REST section](#rest) for an example.</span><span class="sxs-lookup"><span data-stu-id="31300-262">See the "Sample request" in the [preceding REST section](#rest) for an example.</span></span>|
| <span data-ttu-id="31300-263">401 Unauthorized</span><span class="sxs-lookup"><span data-stu-id="31300-263">401 Unauthorized</span></span> | <span data-ttu-id="31300-264">unknown_source</span><span class="sxs-lookup"><span data-stu-id="31300-264">unknown_source</span></span> | <span data-ttu-id="31300-265">Unknown Source *\<URI\>*</span><span class="sxs-lookup"><span data-stu-id="31300-265">Unknown Source *\<URI\>*</span></span> | <span data-ttu-id="31300-266">Verify that your HTTP GET request URI is formatted correctly.</span><span class="sxs-lookup"><span data-stu-id="31300-266">Verify that your HTTP GET request URI is formatted correctly.</span></span> <span data-ttu-id="31300-267">The `scheme:host/resource-path` portion must be specified as `http://localhost:50342/oauth2/token`.</span><span class="sxs-lookup"><span data-stu-id="31300-267">The `scheme:host/resource-path` portion must be specified as `http://localhost:50342/oauth2/token`.</span></span> <span data-ttu-id="31300-268">See the "Sample request" in the [preceding REST section](#rest) for an example.</span><span class="sxs-lookup"><span data-stu-id="31300-268">See the "Sample request" in the [preceding REST section](#rest) for an example.</span></span>|
|           | <span data-ttu-id="31300-269">invalid_request</span><span class="sxs-lookup"><span data-stu-id="31300-269">invalid_request</span></span> | <span data-ttu-id="31300-270">The request is missing a required parameter, includes an invalid parameter value, includes a parameter more than once, or is otherwise malformed.</span><span class="sxs-lookup"><span data-stu-id="31300-270">The request is missing a required parameter, includes an invalid parameter value, includes a parameter more than once, or is otherwise malformed.</span></span> |  |
|           | <span data-ttu-id="31300-271">unauthorized_client</span><span class="sxs-lookup"><span data-stu-id="31300-271">unauthorized_client</span></span> | <span data-ttu-id="31300-272">The client is not authorized to request an access token using this method.</span><span class="sxs-lookup"><span data-stu-id="31300-272">The client is not authorized to request an access token using this method.</span></span> | <span data-ttu-id="31300-273">Caused by a request that didn’t use local loopback to call the extension, or on a VM that doesn’t have managed identities for Azure resources configured correctly.</span><span class="sxs-lookup"><span data-stu-id="31300-273">Caused by a request that didn’t use local loopback to call the extension, or on a VM that doesn’t have managed identities for Azure resources configured correctly.</span></span> <span data-ttu-id="31300-274">See [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md) if you need assistance with VM configuration.</span><span class="sxs-lookup"><span data-stu-id="31300-274">See [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md) if you need assistance with VM configuration.</span></span> |
|           | <span data-ttu-id="31300-275">access_denied</span><span class="sxs-lookup"><span data-stu-id="31300-275">access_denied</span></span> | <span data-ttu-id="31300-276">The resource owner or authorization server denied the request.</span><span class="sxs-lookup"><span data-stu-id="31300-276">The resource owner or authorization server denied the request.</span></span> |  |
|           | <span data-ttu-id="31300-277">unsupported_response_type</span><span class="sxs-lookup"><span data-stu-id="31300-277">unsupported_response_type</span></span> | <span data-ttu-id="31300-278">The authorization server does not support obtaining an access token using this method.</span><span class="sxs-lookup"><span data-stu-id="31300-278">The authorization server does not support obtaining an access token using this method.</span></span> |  |
|           | <span data-ttu-id="31300-279">invalid_scope</span><span class="sxs-lookup"><span data-stu-id="31300-279">invalid_scope</span></span> | <span data-ttu-id="31300-280">The requested scope is invalid, unknown, or malformed.</span><span class="sxs-lookup"><span data-stu-id="31300-280">The requested scope is invalid, unknown, or malformed.</span></span> |  |
| <span data-ttu-id="31300-281">500 Internal server error</span><span class="sxs-lookup"><span data-stu-id="31300-281">500 Internal server error</span></span> | <span data-ttu-id="31300-282">unknown</span><span class="sxs-lookup"><span data-stu-id="31300-282">unknown</span></span> | <span data-ttu-id="31300-283">Failed to retrieve token from the Active directory.</span><span class="sxs-lookup"><span data-stu-id="31300-283">Failed to retrieve token from the Active directory.</span></span> <span data-ttu-id="31300-284">For details see logs in *\<file path\>*</span><span class="sxs-lookup"><span data-stu-id="31300-284">For details see logs in *\<file path\>*</span></span> | <span data-ttu-id="31300-285">Verify that managed identities for Azure resources has been enabled on the VM.</span><span class="sxs-lookup"><span data-stu-id="31300-285">Verify that managed identities for Azure resources has been enabled on the VM.</span></span> <span data-ttu-id="31300-286">See [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md) if you need assistance with VM configuration.</span><span class="sxs-lookup"><span data-stu-id="31300-286">See [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md) if you need assistance with VM configuration.</span></span><br><br><span data-ttu-id="31300-287">Also verify that your HTTP GET request URI is formatted correctly, particularly the resource URI specified in the query string.</span><span class="sxs-lookup"><span data-stu-id="31300-287">Also verify that your HTTP GET request URI is formatted correctly, particularly the resource URI specified in the query string.</span></span> <span data-ttu-id="31300-288">See the "Sample request" in the [preceding REST section](#rest) for an example, or [Azure services that support Azure AD authentication](services-support-msi.md) for a list of services and their respective resource IDs.</span><span class="sxs-lookup"><span data-stu-id="31300-288">See the "Sample request" in the [preceding REST section](#rest) for an example, or [Azure services that support Azure AD authentication](services-support-msi.md) for a list of services and their respective resource IDs.</span></span>

## <a name="retry-guidance"></a><span data-ttu-id="31300-289">Retry guidance</span><span class="sxs-lookup"><span data-stu-id="31300-289">Retry guidance</span></span> 

<span data-ttu-id="31300-290">It is recommended to retry if you receive a 404, 429, or 5xx error code (see [Error handling](#error-handling) above).</span><span class="sxs-lookup"><span data-stu-id="31300-290">It is recommended to retry if you receive a 404, 429, or 5xx error code (see [Error handling](#error-handling) above).</span></span>

<span data-ttu-id="31300-291">Throttling limits apply to the number of calls made to the IMDS endpoint.</span><span class="sxs-lookup"><span data-stu-id="31300-291">Throttling limits apply to the number of calls made to the IMDS endpoint.</span></span> <span data-ttu-id="31300-292">When the throttling threshold is exceeded, IMDS endpoint limits any further requests while the throttle is in effect.</span><span class="sxs-lookup"><span data-stu-id="31300-292">When the throttling threshold is exceeded, IMDS endpoint limits any further requests while the throttle is in effect.</span></span> <span data-ttu-id="31300-293">During this period, the IMDS endpoint will return the HTTP status code 429 ("Too many requests"), and the requests fail.</span><span class="sxs-lookup"><span data-stu-id="31300-293">During this period, the IMDS endpoint will return the HTTP status code 429 ("Too many requests"), and the requests fail.</span></span> 

<span data-ttu-id="31300-294">For retry, we recommend the following strategy:</span><span class="sxs-lookup"><span data-stu-id="31300-294">For retry, we recommend the following strategy:</span></span> 

| <span data-ttu-id="31300-295">**Retry strategy**</span><span class="sxs-lookup"><span data-stu-id="31300-295">**Retry strategy**</span></span> | <span data-ttu-id="31300-296">**Settings**</span><span class="sxs-lookup"><span data-stu-id="31300-296">**Settings**</span></span> | <span data-ttu-id="31300-297">**Values**</span><span class="sxs-lookup"><span data-stu-id="31300-297">**Values**</span></span> | <span data-ttu-id="31300-298">**How it works**</span><span class="sxs-lookup"><span data-stu-id="31300-298">**How it works**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="31300-299">ExponentialBackoff</span><span class="sxs-lookup"><span data-stu-id="31300-299">ExponentialBackoff</span></span> |<span data-ttu-id="31300-300">Retry count</span><span class="sxs-lookup"><span data-stu-id="31300-300">Retry count</span></span><br /><span data-ttu-id="31300-301">Min back-off</span><span class="sxs-lookup"><span data-stu-id="31300-301">Min back-off</span></span><br /><span data-ttu-id="31300-302">Max back-off</span><span class="sxs-lookup"><span data-stu-id="31300-302">Max back-off</span></span><br /><span data-ttu-id="31300-303">Delta back-off</span><span class="sxs-lookup"><span data-stu-id="31300-303">Delta back-off</span></span><br /><span data-ttu-id="31300-304">First fast retry</span><span class="sxs-lookup"><span data-stu-id="31300-304">First fast retry</span></span> |<span data-ttu-id="31300-305">5</span><span class="sxs-lookup"><span data-stu-id="31300-305">5</span></span><br /><span data-ttu-id="31300-306">0 sec</span><span class="sxs-lookup"><span data-stu-id="31300-306">0 sec</span></span><br /><span data-ttu-id="31300-307">60 sec</span><span class="sxs-lookup"><span data-stu-id="31300-307">60 sec</span></span><br /><span data-ttu-id="31300-308">2 sec</span><span class="sxs-lookup"><span data-stu-id="31300-308">2 sec</span></span><br /><span data-ttu-id="31300-309">false</span><span class="sxs-lookup"><span data-stu-id="31300-309">false</span></span> |<span data-ttu-id="31300-310">Attempt 1 - delay 0 sec</span><span class="sxs-lookup"><span data-stu-id="31300-310">Attempt 1 - delay 0 sec</span></span><br /><span data-ttu-id="31300-311">Attempt 2 - delay ~2 sec</span><span class="sxs-lookup"><span data-stu-id="31300-311">Attempt 2 - delay ~2 sec</span></span><br /><span data-ttu-id="31300-312">Attempt 3 - delay ~6 sec</span><span class="sxs-lookup"><span data-stu-id="31300-312">Attempt 3 - delay ~6 sec</span></span><br /><span data-ttu-id="31300-313">Attempt 4 - delay ~14 sec</span><span class="sxs-lookup"><span data-stu-id="31300-313">Attempt 4 - delay ~14 sec</span></span><br /><span data-ttu-id="31300-314">Attempt 5 - delay ~30 sec</span><span class="sxs-lookup"><span data-stu-id="31300-314">Attempt 5 - delay ~30 sec</span></span> |

## <a name="resource-ids-for-azure-services"></a><span data-ttu-id="31300-315">Resource IDs for Azure services</span><span class="sxs-lookup"><span data-stu-id="31300-315">Resource IDs for Azure services</span></span>

<span data-ttu-id="31300-316">See [Azure services that support Azure AD authentication](services-support-msi.md) for a list of resources that support Azure AD and have been tested with managed identities for Azure resources, and their respective resource IDs.</span><span class="sxs-lookup"><span data-stu-id="31300-316">See [Azure services that support Azure AD authentication](services-support-msi.md) for a list of resources that support Azure AD and have been tested with managed identities for Azure resources, and their respective resource IDs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="31300-317">Next steps</span><span class="sxs-lookup"><span data-stu-id="31300-317">Next steps</span></span>

- <span data-ttu-id="31300-318">To enable managed identities for Azure resources on an Azure VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="31300-318">To enable managed identities for Azure resources on an Azure VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md).</span></span>








