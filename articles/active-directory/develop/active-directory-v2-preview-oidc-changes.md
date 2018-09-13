---
title: Changes to the Azure AD v2.0 endpoint | Microsoft Docs
description: A description of changes that are being made to the app model v2.0 public preview protocols.
services: active-directory
documentationcenter: ''
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: e6c5b891-0b5d-47dc-8184-5d0ef6a1a006
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.openlocfilehash: ce60eb0586b4756aabab0bad830e7fc3ca506097
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670071"
---
# <a name="important-updates-to-the-v20-authentication-protocols"></a><span data-ttu-id="f826b-103">Important Updates to the v2.0 Authentication Protocols</span><span class="sxs-lookup"><span data-stu-id="f826b-103">Important Updates to the v2.0 Authentication Protocols</span></span>
<span data-ttu-id="f826b-104">Attention developers!</span><span class="sxs-lookup"><span data-stu-id="f826b-104">Attention developers!</span></span> <span data-ttu-id="f826b-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span><span class="sxs-lookup"><span data-stu-id="f826b-105">Over the next two weeks, we will be making a few updates to our v2.0 authentication protocols that may mean breaking changes for any apps you have written during our preview period.</span></span>  

## <a name="who-does-this-affect"></a><span data-ttu-id="f826b-106">Who does this affect?</span><span class="sxs-lookup"><span data-stu-id="f826b-106">Who does this affect?</span></span>
<span data-ttu-id="f826b-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span><span class="sxs-lookup"><span data-stu-id="f826b-107">Any apps that have been written to use the v2.0 converged authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
```

<span data-ttu-id="f826b-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f826b-108">More information on the v2.0 endpoint can be found [here](active-directory-appmodel-v2-overview.md).</span></span>

<span data-ttu-id="f826b-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span><span class="sxs-lookup"><span data-stu-id="f826b-109">If you have built an app using the v2.0 endpoint by coding directly to the v2.0 protocol, using any of our OpenID Connect or OAuth web middlewares, or using other 3rd party libraries to perform authentication, you should be prepared to test your projects and make changes if necessary.</span></span>

## <a name="who-doesnt-this-affect"></a><span data-ttu-id="f826b-110">Who doesn\`t this affect?</span><span class="sxs-lookup"><span data-stu-id="f826b-110">Who doesn\`t this affect?</span></span>
<span data-ttu-id="f826b-111">Any apps that have been written against the production Azure AD authentication endpoint,</span><span class="sxs-lookup"><span data-stu-id="f826b-111">Any apps that have been written against the production Azure AD authentication endpoint,</span></span>

```
https://login.microsoftonline.com/common/oauth2/authorize
```

<span data-ttu-id="f826b-112">This protocol is set in stone and will not be experiencing any changes.</span><span class="sxs-lookup"><span data-stu-id="f826b-112">This protocol is set in stone and will not be experiencing any changes.</span></span>

<span data-ttu-id="f826b-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span><span class="sxs-lookup"><span data-stu-id="f826b-113">Furthermore, if your app **only** uses our ADAL library to perform authentication, you won\`t have to change anything.</span></span>  <span data-ttu-id="f826b-114">ADAL has shielded your app from the changes.</span><span class="sxs-lookup"><span data-stu-id="f826b-114">ADAL has shielded your app from the changes.</span></span>  

## <a name="what-are-the-changes"></a><span data-ttu-id="f826b-115">What are the changes?</span><span class="sxs-lookup"><span data-stu-id="f826b-115">What are the changes?</span></span>
### <a name="removing-the-x5t-value-from-jwt-headers"></a><span data-ttu-id="f826b-116">Removing the x5t value from JWT headers</span><span class="sxs-lookup"><span data-stu-id="f826b-116">Removing the x5t value from JWT headers</span></span>
<span data-ttu-id="f826b-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span><span class="sxs-lookup"><span data-stu-id="f826b-117">The v2.0 endpoint uses JWT tokens extensively, which contain a header parameters section with relevant metadata about the token.</span></span>  <span data-ttu-id="f826b-118">If you decode the header of one of our current JWTs, you would find something like:</span><span class="sxs-lookup"><span data-stu-id="f826b-118">If you decode the header of one of our current JWTs, you would find something like:</span></span>

```
{ 
    "type": "JWT",
    "alg": "RS256",
    "x5t": "MnC_VZcATfM5pOYiJHMba9goEKY",
    "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

<span data-ttu-id="f826b-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span><span class="sxs-lookup"><span data-stu-id="f826b-119">Where both the "x5t" and "kid" properties identify the public key that should be used to validate the token\`s signature, as retrieved from the OpenID Connect metadata endpoint.</span></span>

<span data-ttu-id="f826b-120">The change we are making here is to remove the "x5t" property.</span><span class="sxs-lookup"><span data-stu-id="f826b-120">The change we are making here is to remove the "x5t" property.</span></span>  <span data-ttu-id="f826b-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span><span class="sxs-lookup"><span data-stu-id="f826b-121">You may continue to use the same mechanisms to validate tokens, but should rely only on the "kid" property to retrieve the correct public key, as specified in the OpenID Connect protocol.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f826b-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span><span class="sxs-lookup"><span data-stu-id="f826b-122">**Your job: Make sure your app does not depend on the existence of the x5t value.**</span></span>
> 
> 

### <a name="removing-profileinfo"></a><span data-ttu-id="f826b-123">Removing profile_info</span><span class="sxs-lookup"><span data-stu-id="f826b-123">Removing profile_info</span></span>
<span data-ttu-id="f826b-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span><span class="sxs-lookup"><span data-stu-id="f826b-124">Previously, the v2.0 endpoint has been returning a base64 encoded JSON object in token responses called `profile_info`.</span></span>  <span data-ttu-id="f826b-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span><span class="sxs-lookup"><span data-stu-id="f826b-125">When requesting an access token from the v2.0 endpoint by sending a request to:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="f826b-126">The response would look like the following JSON object:</span><span class="sxs-lookup"><span data-stu-id="f826b-126">The response would look like the following JSON object:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="f826b-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span><span class="sxs-lookup"><span data-stu-id="f826b-127">The `profile_info` value contained information about the user who signed into the app - their display name, first name, surname, email address, identifier, and so on.</span></span>  <span data-ttu-id="f826b-128">Primarily, the `profile_info` was used for token caching and display purposes.</span><span class="sxs-lookup"><span data-stu-id="f826b-128">Primarily, the `profile_info` was used for token caching and display purposes.</span></span>

<span data-ttu-id="f826b-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span><span class="sxs-lookup"><span data-stu-id="f826b-129">We are now removing the `profile_info` value – but don't worry, we are still providing this information to developers in a slightly different place.</span></span>  <span data-ttu-id="f826b-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span><span class="sxs-lookup"><span data-stu-id="f826b-130">Instead of `profile_info`, the v2.0 endpoint will now return an `id_token` in each token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https://outlook.office.com/mail.read",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="f826b-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span><span class="sxs-lookup"><span data-stu-id="f826b-131">You may decode and parse the id_token to retrieve the same information that you received from profile_info.</span></span>  <span data-ttu-id="f826b-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f826b-132">The id_token is a JSON Web Token (JWT), with contents as specified by OpenID Connect.</span></span>  <span data-ttu-id="f826b-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span><span class="sxs-lookup"><span data-stu-id="f826b-133">The code for doing so should be very similar – you simply need to extract the middle segment (the body) of the id_token and base64 decode it to access the JSON object within.</span></span>

<span data-ttu-id="f826b-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span><span class="sxs-lookup"><span data-stu-id="f826b-134">Over the next two weeks, you should code your app to retrieve the user information from either the `id_token` or `profile_info`; whichever is present.</span></span>  <span data-ttu-id="f826b-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span><span class="sxs-lookup"><span data-stu-id="f826b-135">That way when the change is made, your app can seamlessly handle the transition from `profile_info` to `id_token` without interruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f826b-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span><span class="sxs-lookup"><span data-stu-id="f826b-136">**Your job: Make sure your app does not depend on the existence of the `profile_info` value.**</span></span>
> 
> 

### <a name="removing-idtokenexpiresin"></a><span data-ttu-id="f826b-137">Removing id_token_expires_in</span><span class="sxs-lookup"><span data-stu-id="f826b-137">Removing id_token_expires_in</span></span>
<span data-ttu-id="f826b-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span><span class="sxs-lookup"><span data-stu-id="f826b-138">Similar to `profile_info`, we are also removing the `id_token_expires_in` parameter from responses.</span></span>  <span data-ttu-id="f826b-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span><span class="sxs-lookup"><span data-stu-id="f826b-139">Previously, the v2.0 endpoint would return a value for `id_token_expires_in` along with each id_token response, for instance in an authorize response:</span></span>

```
https://myapp.com?id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...&id_token_expires_in=3599...
```

<span data-ttu-id="f826b-140">Or in a token response:</span><span class="sxs-lookup"><span data-stu-id="f826b-140">Or in a token response:</span></span>

```
{ 
    "token_type": "Bearer",
    "id_token_expires_in": 3599,
    "scope": "openid",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
    "refresh_token": "OAAABAAAAiL9Kn2Z27UubvWFPbm0gL...",
    "profile_info": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsI...",
}
```

<span data-ttu-id="f826b-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span><span class="sxs-lookup"><span data-stu-id="f826b-141">The `id_token_expires_in` value would indicate the number of seconds the id_token would remain valid for.</span></span>  <span data-ttu-id="f826b-142">Now, we are removing the `id_token_expires_in` value completely.</span><span class="sxs-lookup"><span data-stu-id="f826b-142">Now, we are removing the `id_token_expires_in` value completely.</span></span>  <span data-ttu-id="f826b-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span><span class="sxs-lookup"><span data-stu-id="f826b-143">Instead, you may use the OpenID Connect standard `nbf` and `exp` claims to examine the validity of an id_token.</span></span>  <span data-ttu-id="f826b-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span><span class="sxs-lookup"><span data-stu-id="f826b-144">See the [v2.0 token reference](active-directory-v2-tokens.md) for more information on these claims.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f826b-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span><span class="sxs-lookup"><span data-stu-id="f826b-145">**Your job: Make sure your app does not depend on the existence of the `id_token_expires_in` value.**</span></span>
> 
> 

### <a name="changing-the-claims-returned-by-scopeopenid"></a><span data-ttu-id="f826b-146">Changing the claims returned by scope=openid</span><span class="sxs-lookup"><span data-stu-id="f826b-146">Changing the claims returned by scope=openid</span></span>
<span data-ttu-id="f826b-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="f826b-147">This change will be the most significant – in fact, it will affect almost every app that uses the v2.0 endpoint.</span></span>  <span data-ttu-id="f826b-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span><span class="sxs-lookup"><span data-stu-id="f826b-148">Many applications send requests to the v2.0 endpoint using the `openid` scope, like:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="f826b-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span><span class="sxs-lookup"><span data-stu-id="f826b-149">Today, when the user grants consent for the `openid` scope, your app receives a wealth of information about the user in the resulting id_token.</span></span>  <span data-ttu-id="f826b-150">These claims can include their name, preferred username, email address, object ID, and more.</span><span class="sxs-lookup"><span data-stu-id="f826b-150">These claims can include their name, preferred username, email address, object ID, and more.</span></span>

<span data-ttu-id="f826b-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span><span class="sxs-lookup"><span data-stu-id="f826b-151">In this update, we are changing the information that the `openid` scope affords your app access to, to better comform with the OpenID Connect specification.</span></span>  <span data-ttu-id="f826b-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span><span class="sxs-lookup"><span data-stu-id="f826b-152">The `openid` scope will only allow your app to sign the user in, and receive an app-specific identifier for the user in the `sub` claim of the id_token.</span></span>  <span data-ttu-id="f826b-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span><span class="sxs-lookup"><span data-stu-id="f826b-153">The claims in an id_token with only the `openid` scope granted will be devoid of any personally identifiable information.</span></span>  <span data-ttu-id="f826b-154">Example id_token claims are:</span><span class="sxs-lookup"><span data-stu-id="f826b-154">Example id_token claims are:</span></span>

```
{ 
    "aud": "580e250c-8f26-49d0-bee8-1c078add1609",
    "iss": "https://login.microsoftonline.com/b9410318-09af-49c2-b0c3-653adc1f376e/v2.0 ",
    "iat": 1449520283,
    "nbf": 1449520283,
    "exp": 1449524183,
    "nonce": "12345",
    "sub": "MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q",
    "tid": "b9410318-09af-49c2-b0c3-653adc1f376e",
    "ver": "2.0",
}
```

<span data-ttu-id="f826b-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span><span class="sxs-lookup"><span data-stu-id="f826b-155">If you want to obtain personally identifiable information (PII) about the user in your app, your app will need to request additional permissions from the user.</span></span>  <span data-ttu-id="f826b-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span><span class="sxs-lookup"><span data-stu-id="f826b-156">We are introducing support for two new scopes from the OpenID Connect spec – the `email` and `profile` scopes – which allow you to do so.</span></span>

* <span data-ttu-id="f826b-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span><span class="sxs-lookup"><span data-stu-id="f826b-157">The `email` scope is very straightforward – it allows your app access to the user's primary email address via the `email` claim in the id_token.</span></span>  <span data-ttu-id="f826b-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span><span class="sxs-lookup"><span data-stu-id="f826b-158">Note that the `email` claim will not always be present in id_tokens – it will only be included if available in the user's profile.</span></span>
* <span data-ttu-id="f826b-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span><span class="sxs-lookup"><span data-stu-id="f826b-159">The `profile` scope affords your app access to all other basic information about the user – their name, preferred username, object ID, and so on.</span></span>

<span data-ttu-id="f826b-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span><span class="sxs-lookup"><span data-stu-id="f826b-160">This allows you to code your app in a minimal-disclosure fashion – you can ask the user for just the set of information that your app requires to do its job.</span></span>  <span data-ttu-id="f826b-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span><span class="sxs-lookup"><span data-stu-id="f826b-161">If you want to continue getting the full set of user information that your app is currently receiving, you should include all three scopes in your authorization requests:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=...
&redirect_uri=...
&response_mode=form_post
&response_type=id_token
&scope=openid profile email offline_access https://outlook.office.com/mail.read
```

<span data-ttu-id="f826b-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span><span class="sxs-lookup"><span data-stu-id="f826b-162">Your app can begin sending the `email` and `profile` scopes immediately, and the v2.0 endpoint will accept these two scopes and begin requesting permissions from users as necessary.</span></span>  <span data-ttu-id="f826b-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span><span class="sxs-lookup"><span data-stu-id="f826b-163">However, the change in the interpretation of the `openid` scope will not take effect for a few weeks.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f826b-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span><span class="sxs-lookup"><span data-stu-id="f826b-164">**Your job: Add the `profile` and `email` scopes if your app requires information about the user.**</span></span>  <span data-ttu-id="f826b-165">Note that ADAL will include both of these permissions in requests by default.</span><span class="sxs-lookup"><span data-stu-id="f826b-165">Note that ADAL will include both of these permissions in requests by default.</span></span> 
> 
> 

### <a name="removing-the-issuer-trailing-slash"></a><span data-ttu-id="f826b-166">Removing the issuer trailing slash.</span><span class="sxs-lookup"><span data-stu-id="f826b-166">Removing the issuer trailing slash.</span></span>
<span data-ttu-id="f826b-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span><span class="sxs-lookup"><span data-stu-id="f826b-167">Previously, the issuer value that appears in tokens from the v2.0 endpoint took the form</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0/
```

<span data-ttu-id="f826b-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span><span class="sxs-lookup"><span data-stu-id="f826b-168">Where the guid was the tenantId of the Azure AD tenant which issued the token.</span></span>  <span data-ttu-id="f826b-169">With these changes, the issuer value becomes</span><span class="sxs-lookup"><span data-stu-id="f826b-169">With these changes, the issuer value becomes</span></span>

```
https://login.microsoftonline.com/{some-guid}/v2.0 
```

<span data-ttu-id="f826b-170">in both tokens and in the OpenID Connect discovery document.</span><span class="sxs-lookup"><span data-stu-id="f826b-170">in both tokens and in the OpenID Connect discovery document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f826b-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span><span class="sxs-lookup"><span data-stu-id="f826b-171">**Your job: Make sure your app accepts the issuer value both with and without a trailing slash during issuer validation.**</span></span>
> 
> 

## <a name="why-change"></a><span data-ttu-id="f826b-172">Why change?</span><span class="sxs-lookup"><span data-stu-id="f826b-172">Why change?</span></span>
<span data-ttu-id="f826b-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span><span class="sxs-lookup"><span data-stu-id="f826b-173">The primary motivation for introducing these changes is to be compliant with the OpenID Connect standard specification.</span></span>  <span data-ttu-id="f826b-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span><span class="sxs-lookup"><span data-stu-id="f826b-174">By being OpenID Connect compliant, we hope to minimize differences between integrating with Microsoft identity services and with other identity services in the industry.</span></span>  <span data-ttu-id="f826b-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span><span class="sxs-lookup"><span data-stu-id="f826b-175">We want to enable developers to use their favorite open source authentication libraries without having to alter the libraries to accommodate Microsoft differences.</span></span>

## <a name="what-can-you-do"></a><span data-ttu-id="f826b-176">What can you do?</span><span class="sxs-lookup"><span data-stu-id="f826b-176">What can you do?</span></span>
<span data-ttu-id="f826b-177">As of today, you can begin making all of the changes described above.</span><span class="sxs-lookup"><span data-stu-id="f826b-177">As of today, you can begin making all of the changes described above.</span></span>  <span data-ttu-id="f826b-178">You should immediately:</span><span class="sxs-lookup"><span data-stu-id="f826b-178">You should immediately:</span></span>

1. <span data-ttu-id="f826b-179">**Remove any dependencies on the `x5t` header parameter.**</span><span class="sxs-lookup"><span data-stu-id="f826b-179">**Remove any dependencies on the `x5t` header parameter.**</span></span>
2. <span data-ttu-id="f826b-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span><span class="sxs-lookup"><span data-stu-id="f826b-180">**Gracefully handle the transition from `profile_info` to `id_token` in token responses.**</span></span>
3. <span data-ttu-id="f826b-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span><span class="sxs-lookup"><span data-stu-id="f826b-181">**Remove any dependencies on the `id_token_expires_in` response parameter.**</span></span>
4. <span data-ttu-id="f826b-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span><span class="sxs-lookup"><span data-stu-id="f826b-182">**Add the `profile` and `email` scopes to your app if your app needs basic user information.**</span></span>
5. <span data-ttu-id="f826b-183">**Accept issuer values in tokens both with and without a trailing slash.**</span><span class="sxs-lookup"><span data-stu-id="f826b-183">**Accept issuer values in tokens both with and without a trailing slash.**</span></span>

<span data-ttu-id="f826b-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span><span class="sxs-lookup"><span data-stu-id="f826b-184">Our [v2.0 protocol documentation](active-directory-v2-protocols.md) has already been updated to reflect these changes, so you may use it as reference in helping update your code.</span></span>

<span data-ttu-id="f826b-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="f826b-185">If you have any further questions on the scope of the changes, please feel free to reach out to us on Twitter at @AzureAD.</span></span>

## <a name="how-often-will-protocol-changes-occur"></a><span data-ttu-id="f826b-186">How often will protocol changes occur?</span><span class="sxs-lookup"><span data-stu-id="f826b-186">How often will protocol changes occur?</span></span>
<span data-ttu-id="f826b-187">We do not foresee any further breaking changes to the authentication protocols.</span><span class="sxs-lookup"><span data-stu-id="f826b-187">We do not foresee any further breaking changes to the authentication protocols.</span></span>  <span data-ttu-id="f826b-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span><span class="sxs-lookup"><span data-stu-id="f826b-188">We are intentionally bundling these changes into one release so that you won\`t have to go through this type of update process again any time soon.</span></span>  <span data-ttu-id="f826b-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span><span class="sxs-lookup"><span data-stu-id="f826b-189">Of course, we will continue to add features to the converged v2.0 authentication service that you can take advantage of, but those changes should be additive and not break existing code.</span></span>

<span data-ttu-id="f826b-190">Lastly, we would like to say thank you for trying things out during the preview period.</span><span class="sxs-lookup"><span data-stu-id="f826b-190">Lastly, we would like to say thank you for trying things out during the preview period.</span></span>  <span data-ttu-id="f826b-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span><span class="sxs-lookup"><span data-stu-id="f826b-191">The insights and experiences of our early adopters have been invaluable thus far, and we hope you\`ll continue to share your opinions and ideas.</span></span>

<span data-ttu-id="f826b-192">Happy coding!</span><span class="sxs-lookup"><span data-stu-id="f826b-192">Happy coding!</span></span>

<span data-ttu-id="f826b-193">The Microsoft Identity Division</span><span class="sxs-lookup"><span data-stu-id="f826b-193">The Microsoft Identity Division</span></span>

