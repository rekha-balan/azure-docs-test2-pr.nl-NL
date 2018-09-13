---
title: App types for the Azure Active Directory v2.0 endpoint | Microsoft Docs
description: The types of apps and scenarios supported by the Azure Active Directory v2.0 endpoint.
services: active-directory
documentationcenter: ''
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: d809f3d01cf6fade02962faf99efc16563672e75
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554017"
---
# <a name="app-types-for-the-azure-active-directory-v20-endpoint"></a><span data-ttu-id="7660b-103">App types for the Azure Active Directory v2.0 endpoint</span><span class="sxs-lookup"><span data-stu-id="7660b-103">App types for the Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="7660b-104">The Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-104">The Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="7660b-105">This article describes the types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span><span class="sxs-lookup"><span data-stu-id="7660b-105">This article describes the types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="7660b-106">The information in this article is designed to help you understand high-level scenarios before you [start working with the code](active-directory-appmodel-v2-overview.md#getting-started).</span><span class="sxs-lookup"><span data-stu-id="7660b-106">The information in this article is designed to help you understand high-level scenarios before you [start working with the code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="7660b-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span><span class="sxs-lookup"><span data-stu-id="7660b-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="7660b-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="the-basics"></a><span data-ttu-id="7660b-109">The basics</span><span class="sxs-lookup"><span data-stu-id="7660b-109">The basics</span></span>
<span data-ttu-id="7660b-110">You must register each app that uses the v2.0 endpoint in the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7660b-110">You must register each app that uses the v2.0 endpoint in the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="7660b-111">The app registration process collects and assigns these values for your app:</span><span class="sxs-lookup"><span data-stu-id="7660b-111">The app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="7660b-112">An **Application ID** that uniquely identifies your app</span><span class="sxs-lookup"><span data-stu-id="7660b-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="7660b-113">A **redirect URI** that you can use to direct responses back to your app</span><span class="sxs-lookup"><span data-stu-id="7660b-113">A **redirect URI** that you can use to direct responses back to your app</span></span>
* <span data-ttu-id="7660b-114">A few other scenario-specific values</span><span class="sxs-lookup"><span data-stu-id="7660b-114">A few other scenario-specific values</span></span>

<span data-ttu-id="7660b-115">For details, learn how to [register an app](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-115">For details, learn how to [register an app](active-directory-v2-app-registration.md).</span></span>

<span data-ttu-id="7660b-116">After the app is registered, the app communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="7660b-116">After the app is registered, the app communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="7660b-117">We provide open-source frameworks and libraries that handle the details of these requests.</span><span class="sxs-lookup"><span data-stu-id="7660b-117">We provide open-source frameworks and libraries that handle the details of these requests.</span></span> <span data-ttu-id="7660b-118">You also have the option to implement the authentication logic yourself by creating requests to these endpoints:</span><span class="sxs-lookup"><span data-stu-id="7660b-118">You also have the option to implement the authentication logic yourself by creating requests to these endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries to link to -->

## <a name="web-apps"></a><span data-ttu-id="7660b-119">Web apps</span><span class="sxs-lookup"><span data-stu-id="7660b-119">Web apps</span></span>
<span data-ttu-id="7660b-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that the user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span><span class="sxs-lookup"><span data-stu-id="7660b-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that the user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="7660b-121">In OpenID Connect, the web app receives an ID token.</span><span class="sxs-lookup"><span data-stu-id="7660b-121">In OpenID Connect, the web app receives an ID token.</span></span> <span data-ttu-id="7660b-122">An ID token is a security token that verifies the user's identity and provides information about the user in the form of claims:</span><span class="sxs-lookup"><span data-stu-id="7660b-122">An ID token is a security token that verifies the user's identity and provides information about the user in the form of claims:</span></span>

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

<span data-ttu-id="7660b-123">You can learn about all the types of tokens and claims that are available to an app in the [v2.0 tokens reference](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-123">You can learn about all the types of tokens and claims that are available to an app in the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="7660b-124">In web server apps, the sign-in authentication flow takes these high-level steps:</span><span class="sxs-lookup"><span data-stu-id="7660b-124">In web server apps, the sign-in authentication flow takes these high-level steps:</span></span>

![Web app authentication flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/active-directory-v2-flows/convergence_scenarios_webapp.png)

<span data-ttu-id="7660b-126">You can ensure the user's identity by validating the ID token with a public signing key that is received from the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="7660b-126">You can ensure the user's identity by validating the ID token with a public signing key that is received from the v2.0 endpoint.</span></span> <span data-ttu-id="7660b-127">A session cookie is set, which can be used to identify the user on subsequent page requests.</span><span class="sxs-lookup"><span data-stu-id="7660b-127">A session cookie is set, which can be used to identify the user on subsequent page requests.</span></span>

<span data-ttu-id="7660b-128">To see this scenario in action, try one of the web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span><span class="sxs-lookup"><span data-stu-id="7660b-128">To see this scenario in action, try one of the web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="7660b-129">In addition to simple sign-in, a web server app might need to access another web service, such as a REST API.</span><span class="sxs-lookup"><span data-stu-id="7660b-129">In addition to simple sign-in, a web server app might need to access another web service, such as a REST API.</span></span> <span data-ttu-id="7660b-130">In this case, the web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-130">In this case, the web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="7660b-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="7660b-132">Web APIs</span><span class="sxs-lookup"><span data-stu-id="7660b-132">Web APIs</span></span>
<span data-ttu-id="7660b-133">You can use the v2.0 endpoint to secure web services, such as your app's RESTful Web API.</span><span class="sxs-lookup"><span data-stu-id="7660b-133">You can use the v2.0 endpoint to secure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="7660b-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token to secure its data and to authenticate incoming requests.</span><span class="sxs-lookup"><span data-stu-id="7660b-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token to secure its data and to authenticate incoming requests.</span></span> <span data-ttu-id="7660b-135">The caller of a Web API appends an access token in the authorization header of an HTTP request, like this:</span><span class="sxs-lookup"><span data-stu-id="7660b-135">The caller of a Web API appends an access token in the authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="7660b-136">The Web API uses the access token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the access token.</span><span class="sxs-lookup"><span data-stu-id="7660b-136">The Web API uses the access token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the access token.</span></span> <span data-ttu-id="7660b-137">To learn about all the types of tokens and claims that are available to an app, see the [v2.0 tokens reference](active-directory-v2-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-137">To learn about all the types of tokens and claims that are available to an app, see the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="7660b-138">A Web API can give users the power to opt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-138">A Web API can give users the power to opt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span></span> <span data-ttu-id="7660b-139">For a calling app to acquire permission to a scope, the user must consent to the scope during a flow.</span><span class="sxs-lookup"><span data-stu-id="7660b-139">For a calling app to acquire permission to a scope, the user must consent to the scope during a flow.</span></span> <span data-ttu-id="7660b-140">The v2.0 endpoint asks the user for permission, and then records permissions in all access tokens that the Web API receives.</span><span class="sxs-lookup"><span data-stu-id="7660b-140">The v2.0 endpoint asks the user for permission, and then records permissions in all access tokens that the Web API receives.</span></span> <span data-ttu-id="7660b-141">The Web API validates the access tokens it receives on each call and performs authorization checks.</span><span class="sxs-lookup"><span data-stu-id="7660b-141">The Web API validates the access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="7660b-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span><span class="sxs-lookup"><span data-stu-id="7660b-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="7660b-143">The high-level flow for a Web API looks like this:</span><span class="sxs-lookup"><span data-stu-id="7660b-143">The high-level flow for a Web API looks like this:</span></span>

![Web API authentication flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/active-directory-v2-flows/convergence_scenarios_webapi.png)

<span data-ttu-id="7660b-145">To learn more about authorization codes, refresh tokens, and the detailed steps of getting access tokens, read about the [OAuth 2.0 protocol](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-145">To learn more about authorization codes, refresh tokens, and the detailed steps of getting access tokens, read about the [OAuth 2.0 protocol](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="7660b-146">To learn how to secure a Web API by using OAuth2 access tokens, check out the Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span><span class="sxs-lookup"><span data-stu-id="7660b-146">To learn how to secure a Web API by using OAuth2 access tokens, check out the Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="7660b-147">Mobile and native apps</span><span class="sxs-lookup"><span data-stu-id="7660b-147">Mobile and native apps</span></span>
<span data-ttu-id="7660b-148">Device-installed apps, such as mobile and desktop apps, often need to access back-end services or Web APIs that store data and perform functions on behalf of a user.</span><span class="sxs-lookup"><span data-stu-id="7660b-148">Device-installed apps, such as mobile and desktop apps, often need to access back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="7660b-149">These apps can add sign-in and authorization to back-end services by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-149">These apps can add sign-in and authorization to back-end services by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="7660b-150">In this flow, the app receives an authorization code from the v2.0 endpoint when the user signs in.</span><span class="sxs-lookup"><span data-stu-id="7660b-150">In this flow, the app receives an authorization code from the v2.0 endpoint when the user signs in.</span></span> <span data-ttu-id="7660b-151">The authorization code represents the app's permission to call back-end services on behalf of the user who is signed in.</span><span class="sxs-lookup"><span data-stu-id="7660b-151">The authorization code represents the app's permission to call back-end services on behalf of the user who is signed in.</span></span> <span data-ttu-id="7660b-152">The app can exchange the authorization code in the background for an OAuth 2.0 access token and a refresh token.</span><span class="sxs-lookup"><span data-stu-id="7660b-152">The app can exchange the authorization code in the background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="7660b-153">The app can use the access token to authenticate to Web APIs in HTTP requests, and use the refresh token to get new access tokens when older access tokens expire.</span><span class="sxs-lookup"><span data-stu-id="7660b-153">The app can use the access token to authenticate to Web APIs in HTTP requests, and use the refresh token to get new access tokens when older access tokens expire.</span></span>

![Native app authentication flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="7660b-155">Single-page apps (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="7660b-155">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="7660b-156">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7660b-156">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="7660b-157">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span><span class="sxs-lookup"><span data-stu-id="7660b-157">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="7660b-158">The Azure AD v2.0 endpoint supports these apps by using the [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-158">The Azure AD v2.0 endpoint supports these apps by using the [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span></span>

<span data-ttu-id="7660b-159">In this flow, the app receives tokens directly from the v2.0 authorize endpoint, without any server-to-server exchanges.</span><span class="sxs-lookup"><span data-stu-id="7660b-159">In this flow, the app receives tokens directly from the v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="7660b-160">All authentication logic and session handling takes place entirely in the JavaScript client, without extra page redirects.</span><span class="sxs-lookup"><span data-stu-id="7660b-160">All authentication logic and session handling takes place entirely in the JavaScript client, without extra page redirects.</span></span>

![Implicit authentication flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/active-directory-v2-flows/convergence_scenarios_implicit.png)

<span data-ttu-id="7660b-162">To see this scenario in action, try one of the single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span><span class="sxs-lookup"><span data-stu-id="7660b-162">To see this scenario in action, try one of the single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

### <a name="daemons-and-server-side-apps"></a><span data-ttu-id="7660b-163">Daemons and server-side apps</span><span class="sxs-lookup"><span data-stu-id="7660b-163">Daemons and server-side apps</span></span>
<span data-ttu-id="7660b-164">Apps that have long-running processes or that operate without interaction with a user also need a way to access secured resources, such as Web APIs.</span><span class="sxs-lookup"><span data-stu-id="7660b-164">Apps that have long-running processes or that operate without interaction with a user also need a way to access secured resources, such as Web APIs.</span></span> <span data-ttu-id="7660b-165">These apps can authenticate and get tokens by using the app's identity, rather than a user's delegated identity, with the OAuth 2.0 client credentials flow.</span><span class="sxs-lookup"><span data-stu-id="7660b-165">These apps can authenticate and get tokens by using the app's identity, rather than a user's delegated identity, with the OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="7660b-166">In this flow, the app interacts directly with the `/token` endpoint to obtain endpoints:</span><span class="sxs-lookup"><span data-stu-id="7660b-166">In this flow, the app interacts directly with the `/token` endpoint to obtain endpoints:</span></span>

![Daemon app authentication flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/active-directory-v2-flows/convergence_scenarios_daemon.png)

<span data-ttu-id="7660b-168">To build a daemon app, see the client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span><span class="sxs-lookup"><span data-stu-id="7660b-168">To build a daemon app, see the client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>

## <a name="current-limitations"></a><span data-ttu-id="7660b-169">Current limitations</span><span class="sxs-lookup"><span data-stu-id="7660b-169">Current limitations</span></span>
<span data-ttu-id="7660b-170">Currently, the types of apps in this section are not supported by the v2.0 endpoint, but they are on the roadmap for future development.</span><span class="sxs-lookup"><span data-stu-id="7660b-170">Currently, the types of apps in this section are not supported by the v2.0 endpoint, but they are on the roadmap for future development.</span></span> <span data-ttu-id="7660b-171">For additional limitations and restrictions for the v2.0 endpoint, see [Should I use the v2.0 endpoint?](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-171">For additional limitations and restrictions for the v2.0 endpoint, see [Should I use the v2.0 endpoint?](active-directory-v2-limitations.md).</span></span>

### <a name="chained-web-apis-on-behalf-of"></a><span data-ttu-id="7660b-172">Chained Web APIs (on-behalf-of)</span><span class="sxs-lookup"><span data-stu-id="7660b-172">Chained Web APIs (on-behalf-of)</span></span>
<span data-ttu-id="7660b-173">Many architectures include a Web API that needs to call another downstream Web API, both secured by the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="7660b-173">Many architectures include a Web API that needs to call another downstream Web API, both secured by the v2.0 endpoint.</span></span> <span data-ttu-id="7660b-174">This scenario is common in native clients that have a Web API back end, which in turn calls an instance of Microsoft Online Services like Office 365, or the Graph API.</span><span class="sxs-lookup"><span data-stu-id="7660b-174">This scenario is common in native clients that have a Web API back end, which in turn calls an instance of Microsoft Online Services like Office 365, or the Graph API.</span></span>

<span data-ttu-id="7660b-175">This chained Web API scenario can be supported by using the OAuth 2.0 JSON Web Token (JWT) bearer credentials grant, also known as the [on-behalf-of flow](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="7660b-175">This chained Web API scenario can be supported by using the OAuth 2.0 JSON Web Token (JWT) bearer credentials grant, also known as the [on-behalf-of flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="7660b-176">Currently, the on-behalf-of flow is not implemented in the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="7660b-176">Currently, the on-behalf-of flow is not implemented in the v2.0 endpoint.</span></span> <span data-ttu-id="7660b-177">To see how this flow works in the generally available Azure AD service, check out the [on-behalf-of code sample on GitHub](https://github.com/AzureADSamples/WebAPI-OnBehalfOf-DotNet).</span><span class="sxs-lookup"><span data-stu-id="7660b-177">To see how this flow works in the generally available Azure AD service, check out the [on-behalf-of code sample on GitHub](https://github.com/AzureADSamples/WebAPI-OnBehalfOf-DotNet).</span></span>






