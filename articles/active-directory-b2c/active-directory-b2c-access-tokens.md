---
title: 'Azure Active Directory B2C: Requesting access tokens | Microsoft Docs'
description: This article will show you how to setup a client application and acquire an access token.
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: ''
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.translationtype: HT
ms.date: 03/16/2017
ms.author: parakhj
ms.openlocfilehash: dbe4c24a75eb2f58d22cefb64bb482caa3886542
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548824"
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a><span data-ttu-id="4c52d-103">Azure AD B2C: Requesting Access Tokens</span><span class="sxs-lookup"><span data-stu-id="4c52d-103">Azure AD B2C: Requesting Access Tokens</span></span>


<span data-ttu-id="4c52d-104">An access token (denoted as **access\_token**) is a form of security token that a client can use to access resources that are secured by an [authorization server](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), such as a web API.</span><span class="sxs-lookup"><span data-stu-id="4c52d-104">An access token (denoted as **access\_token**) is a form of security token that a client can use to access resources that are secured by an [authorization server](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), such as a web API.</span></span> <span data-ttu-id="4c52d-105">Access tokens are represented as [JWTs](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) and contain information about the intended resource server and the granted permissions to the server.</span><span class="sxs-lookup"><span data-stu-id="4c52d-105">Access tokens are represented as [JWTs](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) and contain information about the intended resource server and the granted permissions to the server.</span></span> <span data-ttu-id="4c52d-106">When calling the resource server, the access token must be present in the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="4c52d-106">When calling the resource server, the access token must be present in the HTTP request.</span></span>

<span data-ttu-id="4c52d-107">This article discusses how to configure a client application and have it make a request to acquire an **access\_token** from the `authorize` and `token` endpoints.</span><span class="sxs-lookup"><span data-stu-id="4c52d-107">This article discusses how to configure a client application and have it make a request to acquire an **access\_token** from the `authorize` and `token` endpoints.</span></span>

## <a name="prerequisite"></a><span data-ttu-id="4c52d-108">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="4c52d-108">Prerequisite</span></span>

<span data-ttu-id="4c52d-109">Before requesting an access token, you first need to register a web API and publish permissions that can be granted to the client application.</span><span class="sxs-lookup"><span data-stu-id="4c52d-109">Before requesting an access token, you first need to register a web API and publish permissions that can be granted to the client application.</span></span> <span data-ttu-id="4c52d-110">Get started by following the steps under the [Register a web API](active-directory-b2c-app-registration.md) section.</span><span class="sxs-lookup"><span data-stu-id="4c52d-110">Get started by following the steps under the [Register a web API](active-directory-b2c-app-registration.md) section.</span></span>

## <a name="granting-permissions-to-a-web-api"></a><span data-ttu-id="4c52d-111">Granting permissions to a web API</span><span class="sxs-lookup"><span data-stu-id="4c52d-111">Granting permissions to a web API</span></span>

<span data-ttu-id="4c52d-112">In order for a client application to get specific permissions to an API, the client application needs to be granted those permissions via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4c52d-112">In order for a client application to get specific permissions to an API, the client application needs to be granted those permissions via the Azure portal.</span></span> <span data-ttu-id="4c52d-113">To grant permissions to a client application:</span><span class="sxs-lookup"><span data-stu-id="4c52d-113">To grant permissions to a client application:</span></span>

1. <span data-ttu-id="4c52d-114">Navigate to the **Applications** menu in the B2C features blade.</span><span class="sxs-lookup"><span data-stu-id="4c52d-114">Navigate to the **Applications** menu in the B2C features blade.</span></span>
2. <span data-ttu-id="4c52d-115">Click on your client application ([Register an application](active-directory-b2c-app-registration.md) if you don’t have one).</span><span class="sxs-lookup"><span data-stu-id="4c52d-115">Click on your client application ([Register an application](active-directory-b2c-app-registration.md) if you don’t have one).</span></span>
3. <span data-ttu-id="4c52d-116">Select **Api access**.</span><span class="sxs-lookup"><span data-stu-id="4c52d-116">Select **Api access**.</span></span>
4. <span data-ttu-id="4c52d-117">Click on **Add**.</span><span class="sxs-lookup"><span data-stu-id="4c52d-117">Click on **Add**.</span></span>
5. <span data-ttu-id="4c52d-118">Select your web API and the scopes (permissions) you would like to grant.</span><span class="sxs-lookup"><span data-stu-id="4c52d-118">Select your web API and the scopes (permissions) you would like to grant.</span></span>
6. <span data-ttu-id="4c52d-119">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c52d-119">Click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="4c52d-120">Azure AD B2C does not ask your client application users for their consent.</span><span class="sxs-lookup"><span data-stu-id="4c52d-120">Azure AD B2C does not ask your client application users for their consent.</span></span> <span data-ttu-id="4c52d-121">Instead, all consent is provided by the admin, based on the permissions configured between the applications described above.</span><span class="sxs-lookup"><span data-stu-id="4c52d-121">Instead, all consent is provided by the admin, based on the permissions configured between the applications described above.</span></span> <span data-ttu-id="4c52d-122">If a permission grant for an application is revoked, all users who were previously able to acquire that permission will no longer be able to do so.</span><span class="sxs-lookup"><span data-stu-id="4c52d-122">If a permission grant for an application is revoked, all users who were previously able to acquire that permission will no longer be able to do so.</span></span>

## <a name="requesting-a-token"></a><span data-ttu-id="4c52d-123">Requesting a token</span><span class="sxs-lookup"><span data-stu-id="4c52d-123">Requesting a token</span></span>

<span data-ttu-id="4c52d-124">To get an access token for a resource application, the client application needs to specify the permissions wanted in the **scope** parameter of the request.</span><span class="sxs-lookup"><span data-stu-id="4c52d-124">To get an access token for a resource application, the client application needs to specify the permissions wanted in the **scope** parameter of the request.</span></span> <span data-ttu-id="4c52d-125">For example, to acquire the “read” permission for the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/notes`, the scope would be `https://contoso.onmicrosoft.com/notes/read`.</span><span class="sxs-lookup"><span data-stu-id="4c52d-125">For example, to acquire the “read” permission for the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/notes`, the scope would be `https://contoso.onmicrosoft.com/notes/read`.</span></span> <span data-ttu-id="4c52d-126">Below is an example of an authorization code request to the `authorize` endpoint.</span><span class="sxs-lookup"><span data-stu-id="4c52d-126">Below is an example of an authorization code request to the `authorize` endpoint.</span></span>

```
https://login.microsoftonline.com/<yourTenantId>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

<span data-ttu-id="4c52d-127">To acquire multiple permissions in the same request, you can add multiple entries in the single **scope** parameter, separated by spaces.</span><span class="sxs-lookup"><span data-stu-id="4c52d-127">To acquire multiple permissions in the same request, you can add multiple entries in the single **scope** parameter, separated by spaces.</span></span> <span data-ttu-id="4c52d-128">For example:</span><span class="sxs-lookup"><span data-stu-id="4c52d-128">For example:</span></span>

<span data-ttu-id="4c52d-129">URL decoded:</span><span class="sxs-lookup"><span data-stu-id="4c52d-129">URL decoded:</span></span>

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

<span data-ttu-id="4c52d-130">URL encoded:</span><span class="sxs-lookup"><span data-stu-id="4c52d-130">URL encoded:</span></span>

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

<span data-ttu-id="4c52d-131">You may request more scopes/permissions for a resource than what is granted for your client application.</span><span class="sxs-lookup"><span data-stu-id="4c52d-131">You may request more scopes/permissions for a resource than what is granted for your client application.</span></span> <span data-ttu-id="4c52d-132">When this is the case, the call will succeed if at least one permission is granted.</span><span class="sxs-lookup"><span data-stu-id="4c52d-132">When this is the case, the call will succeed if at least one permission is granted.</span></span> <span data-ttu-id="4c52d-133">The resulting **access\_token** will have its “scp” claim populated with only the permissions that were successfully granted.</span><span class="sxs-lookup"><span data-stu-id="4c52d-133">The resulting **access\_token** will have its “scp” claim populated with only the permissions that were successfully granted.</span></span>

> [!NOTE] 
> <span data-ttu-id="4c52d-134">We do not support requesting permissions against two different web resources in the same request.</span><span class="sxs-lookup"><span data-stu-id="4c52d-134">We do not support requesting permissions against two different web resources in the same request.</span></span> <span data-ttu-id="4c52d-135">This kind of request will fail.</span><span class="sxs-lookup"><span data-stu-id="4c52d-135">This kind of request will fail.</span></span>

### <a name="special-cases"></a><span data-ttu-id="4c52d-136">Special cases</span><span class="sxs-lookup"><span data-stu-id="4c52d-136">Special cases</span></span>

<span data-ttu-id="4c52d-137">The OpenID Connect standard specifies several special “scope” values.</span><span class="sxs-lookup"><span data-stu-id="4c52d-137">The OpenID Connect standard specifies several special “scope” values.</span></span> <span data-ttu-id="4c52d-138">The following special scopes represent the permission to “access the user’s profile”:</span><span class="sxs-lookup"><span data-stu-id="4c52d-138">The following special scopes represent the permission to “access the user’s profile”:</span></span>

* <span data-ttu-id="4c52d-139">**openid**: This requests an ID token</span><span class="sxs-lookup"><span data-stu-id="4c52d-139">**openid**: This requests an ID token</span></span>
* <span data-ttu-id="4c52d-140">**offline\_access**: This requests a refresh token (using Auth Code flows).</span><span class="sxs-lookup"><span data-stu-id="4c52d-140">**offline\_access**: This requests a refresh token (using Auth Code flows).</span></span>

<span data-ttu-id="4c52d-141">If the “response\_type” parameter in a `authorize` request includes “token”, the “scope” parameter must include at least one resource permission (other than “openid” and “offline\_access”) that will be granted.</span><span class="sxs-lookup"><span data-stu-id="4c52d-141">If the “response\_type” parameter in a `authorize` request includes “token”, the “scope” parameter must include at least one resource permission (other than “openid” and “offline\_access”) that will be granted.</span></span> <span data-ttu-id="4c52d-142">Otherwise, the `authorize` request will terminate with a failure.</span><span class="sxs-lookup"><span data-stu-id="4c52d-142">Otherwise, the `authorize` request will terminate with a failure.</span></span>

## <a name="the-returned-token"></a><span data-ttu-id="4c52d-143">The returned token</span><span class="sxs-lookup"><span data-stu-id="4c52d-143">The returned token</span></span>

<span data-ttu-id="4c52d-144">In a successfully minted **access\_token** (from either the `authorize` or `token` endpoint), the following claims will be present:</span><span class="sxs-lookup"><span data-stu-id="4c52d-144">In a successfully minted **access\_token** (from either the `authorize` or `token` endpoint), the following claims will be present:</span></span>

| <span data-ttu-id="4c52d-145">Name</span><span class="sxs-lookup"><span data-stu-id="4c52d-145">Name</span></span> | <span data-ttu-id="4c52d-146">Claim</span><span class="sxs-lookup"><span data-stu-id="4c52d-146">Claim</span></span> | <span data-ttu-id="4c52d-147">Description</span><span class="sxs-lookup"><span data-stu-id="4c52d-147">Description</span></span> |
| --- | --- | --- |
|<span data-ttu-id="4c52d-148">Audience</span><span class="sxs-lookup"><span data-stu-id="4c52d-148">Audience</span></span> |`aud` |<span data-ttu-id="4c52d-149">The \*application ID\* of the single resource that the token grants access to.</span><span class="sxs-lookup"><span data-stu-id="4c52d-149">The \*application ID\* of the single resource that the token grants access to.</span></span> |
|<span data-ttu-id="4c52d-150">Scope</span><span class="sxs-lookup"><span data-stu-id="4c52d-150">Scope</span></span> |`scp` |<span data-ttu-id="4c52d-151">The permissions granted to the resource.</span><span class="sxs-lookup"><span data-stu-id="4c52d-151">The permissions granted to the resource.</span></span> <span data-ttu-id="4c52d-152">Multiple granted permissions will be separated by space.</span><span class="sxs-lookup"><span data-stu-id="4c52d-152">Multiple granted permissions will be separated by space.</span></span> |
|<span data-ttu-id="4c52d-153">Authorized Party</span><span class="sxs-lookup"><span data-stu-id="4c52d-153">Authorized Party</span></span> |`azp` |<span data-ttu-id="4c52d-154">The \*application ID\* of the client application that initiated the request.</span><span class="sxs-lookup"><span data-stu-id="4c52d-154">The \*application ID\* of the client application that initiated the request.</span></span> |

<span data-ttu-id="4c52d-155">When your API receives the **access\_token**, it must [validate the token](active-directory-b2c-reference-tokens.md) to prove that the token is authentic and has the correct claims.</span><span class="sxs-lookup"><span data-stu-id="4c52d-155">When your API receives the **access\_token**, it must [validate the token](active-directory-b2c-reference-tokens.md) to prove that the token is authentic and has the correct claims.</span></span>

<span data-ttu-id="4c52d-156">We are always open to feedback and suggestions!</span><span class="sxs-lookup"><span data-stu-id="4c52d-156">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="4c52d-157">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="4c52d-157">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="4c52d-158">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="4c52d-158">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
