---
title: App types for the Azure Active Directory v2.0 endpoint | Microsoft Docs
description: The types of apps and scenarios supported by the Azure Active Directory v2.0 endpoint.
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: celested
ms.reviewer: hirsin
ms.custom: aaddev
ms.openlocfilehash: 7ec4d447c3ff3f36f9f995390a61d021e325322e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866485"
---
# <a name="app-types-for-the-azure-active-directory-v20-endpoint"></a><span data-ttu-id="0e7e8-103">App types for the Azure Active Directory v2.0 endpoint</span><span class="sxs-lookup"><span data-stu-id="0e7e8-103">App types for the Azure Active Directory v2.0 endpoint</span></span>

<span data-ttu-id="0e7e8-104">The Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-104">The Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="0e7e8-105">This article describes the types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-105">This article describes the types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="0e7e8-106">The information in this article is designed to help you understand high-level scenarios before you [start working with the code](active-directory-appmodel-v2-overview.md#getting-started).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-106">The information in this article is designed to help you understand high-level scenarios before you [start working with the code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="0e7e8-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="0e7e8-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>

## <a name="the-basics"></a><span data-ttu-id="0e7e8-109">The basics</span><span class="sxs-lookup"><span data-stu-id="0e7e8-109">The basics</span></span>

<span data-ttu-id="0e7e8-110">You must register each app that uses the v2.0 endpoint in the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-110">You must register each app that uses the v2.0 endpoint in the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="0e7e8-111">The app registration process collects and assigns these values for your app:</span><span class="sxs-lookup"><span data-stu-id="0e7e8-111">The app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="0e7e8-112">An **Application ID** that uniquely identifies your app</span><span class="sxs-lookup"><span data-stu-id="0e7e8-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="0e7e8-113">A **Redirect URI** that you can use to direct responses back to your app</span><span class="sxs-lookup"><span data-stu-id="0e7e8-113">A **Redirect URI** that you can use to direct responses back to your app</span></span>
* <span data-ttu-id="0e7e8-114">A few other scenario-specific values</span><span class="sxs-lookup"><span data-stu-id="0e7e8-114">A few other scenario-specific values</span></span>

<span data-ttu-id="0e7e8-115">For details, learn how to [register an app](quickstart-v2-register-an-app.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-115">For details, learn how to [register an app](quickstart-v2-register-an-app.md).</span></span>

<span data-ttu-id="0e7e8-116">After the app is registered, the app communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-116">After the app is registered, the app communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="0e7e8-117">We provide open-source frameworks and libraries that handle the details of these requests.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-117">We provide open-source frameworks and libraries that handle the details of these requests.</span></span> <span data-ttu-id="0e7e8-118">You also have the option to implement the authentication logic yourself by creating requests to these endpoints:</span><span class="sxs-lookup"><span data-stu-id="0e7e8-118">You also have the option to implement the authentication logic yourself by creating requests to these endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries to link to -->

## <a name="web-apps"></a><span data-ttu-id="0e7e8-119">Web apps</span><span class="sxs-lookup"><span data-stu-id="0e7e8-119">Web apps</span></span>

<span data-ttu-id="0e7e8-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that the user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that the user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="0e7e8-121">In OpenID Connect, the web app receives an ID token.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-121">In OpenID Connect, the web app receives an ID token.</span></span> <span data-ttu-id="0e7e8-122">An ID token is a security token that verifies the user's identity and provides information about the user in the form of claims:</span><span class="sxs-lookup"><span data-stu-id="0e7e8-122">An ID token is a security token that verifies the user's identity and provides information about the user in the form of claims:</span></span>

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

<span data-ttu-id="0e7e8-123">You can learn about all the types of tokens and claims that are available to an app in the [v2.0 tokens reference](v2-id-and-access-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-123">You can learn about all the types of tokens and claims that are available to an app in the [v2.0 tokens reference](v2-id-and-access-tokens.md).</span></span>

<span data-ttu-id="0e7e8-124">In web server apps, the sign-in authentication flow takes these high-level steps:</span><span class="sxs-lookup"><span data-stu-id="0e7e8-124">In web server apps, the sign-in authentication flow takes these high-level steps:</span></span>

![Web app authentication flow](./media/v2-app-types/convergence_scenarios_webapp.png)

<span data-ttu-id="0e7e8-126">You can ensure the user's identity by validating the ID token with a public signing key that is received from the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-126">You can ensure the user's identity by validating the ID token with a public signing key that is received from the v2.0 endpoint.</span></span> <span data-ttu-id="0e7e8-127">A session cookie is set, which can be used to identify the user on subsequent page requests.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-127">A session cookie is set, which can be used to identify the user on subsequent page requests.</span></span>

<span data-ttu-id="0e7e8-128">To see this scenario in action, try one of the web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-128">To see this scenario in action, try one of the web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="0e7e8-129">In addition to simple sign-in, a web server app might need to access another web service, such as a REST API.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-129">In addition to simple sign-in, a web server app might need to access another web service, such as a REST API.</span></span> <span data-ttu-id="0e7e8-130">In this case, the web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-130">In this case, the web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="0e7e8-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="0e7e8-132">Web APIs</span><span class="sxs-lookup"><span data-stu-id="0e7e8-132">Web APIs</span></span>
<span data-ttu-id="0e7e8-133">You can use the v2.0 endpoint to secure web services, such as your app's RESTful Web API.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-133">You can use the v2.0 endpoint to secure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="0e7e8-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token to secure its data and to authenticate incoming requests.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token to secure its data and to authenticate incoming requests.</span></span> <span data-ttu-id="0e7e8-135">The caller of a Web API appends an access token in the authorization header of an HTTP request, like this:</span><span class="sxs-lookup"><span data-stu-id="0e7e8-135">The caller of a Web API appends an access token in the authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="0e7e8-136">The Web API uses the access token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the access token.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-136">The Web API uses the access token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the access token.</span></span> <span data-ttu-id="0e7e8-137">To learn about all the types of tokens and claims that are available to an app, see the [v2.0 tokens reference](v2-id-and-access-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-137">To learn about all the types of tokens and claims that are available to an app, see the [v2.0 tokens reference](v2-id-and-access-tokens.md).</span></span>

<span data-ttu-id="0e7e8-138">A Web API can give users the power to opt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](v2-permissions-and-consent.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-138">A Web API can give users the power to opt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](v2-permissions-and-consent.md).</span></span> <span data-ttu-id="0e7e8-139">For a calling app to acquire permission to a scope, the user must consent to the scope during a flow.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-139">For a calling app to acquire permission to a scope, the user must consent to the scope during a flow.</span></span> <span data-ttu-id="0e7e8-140">The v2.0 endpoint asks the user for permission, and then records permissions in all access tokens that the Web API receives.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-140">The v2.0 endpoint asks the user for permission, and then records permissions in all access tokens that the Web API receives.</span></span> <span data-ttu-id="0e7e8-141">The Web API validates the access tokens it receives on each call and performs authorization checks.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-141">The Web API validates the access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="0e7e8-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="0e7e8-143">The high-level flow for a Web API looks like this:</span><span class="sxs-lookup"><span data-stu-id="0e7e8-143">The high-level flow for a Web API looks like this:</span></span>

![Web API authentication flow](./media/v2-app-types/convergence_scenarios_webapi.png)

<span data-ttu-id="0e7e8-145">To learn how to secure a Web API by using OAuth2 access tokens, check out the Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-145">To learn how to secure a Web API by using OAuth2 access tokens, check out the Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="0e7e8-146">In many cases, web APIs also need to make outbound requests to other downstream web APIs secured by Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-146">In many cases, web APIs also need to make outbound requests to other downstream web APIs secured by Azure Active Directory.</span></span> <span data-ttu-id="0e7e8-147">To do so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows the web API to exchange an incoming access token for another access token to be used in outbound requests.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-147">To do so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows the web API to exchange an incoming access token for another access token to be used in outbound requests.</span></span> <span data-ttu-id="0e7e8-148">The v2.0 endpoint's On Behalf Of flow is described in [detail here](v2-oauth2-on-behalf-of-flow.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-148">The v2.0 endpoint's On Behalf Of flow is described in [detail here](v2-oauth2-on-behalf-of-flow.md).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="0e7e8-149">Mobile and native apps</span><span class="sxs-lookup"><span data-stu-id="0e7e8-149">Mobile and native apps</span></span>
<span data-ttu-id="0e7e8-150">Device-installed apps, such as mobile and desktop apps, often need to access back-end services or Web APIs that store data and perform functions on behalf of a user.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-150">Device-installed apps, such as mobile and desktop apps, often need to access back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="0e7e8-151">These apps can add sign-in and authorization to back-end services by using the [OAuth 2.0 authorization code flow](v2-oauth2-auth-code-flow.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-151">These apps can add sign-in and authorization to back-end services by using the [OAuth 2.0 authorization code flow](v2-oauth2-auth-code-flow.md).</span></span>

<span data-ttu-id="0e7e8-152">In this flow, the app receives an authorization code from the v2.0 endpoint when the user signs in.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-152">In this flow, the app receives an authorization code from the v2.0 endpoint when the user signs in.</span></span> <span data-ttu-id="0e7e8-153">The authorization code represents the app's permission to call back-end services on behalf of the user who is signed in.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-153">The authorization code represents the app's permission to call back-end services on behalf of the user who is signed in.</span></span> <span data-ttu-id="0e7e8-154">The app can exchange the authorization code in the background for an OAuth 2.0 access token and a refresh token.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-154">The app can exchange the authorization code in the background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="0e7e8-155">The app can use the access token to authenticate to Web APIs in HTTP requests, and use the refresh token to get new access tokens when older access tokens expire.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-155">The app can use the access token to authenticate to Web APIs in HTTP requests, and use the refresh token to get new access tokens when older access tokens expire.</span></span>

![Native app authentication flow](./media/v2-app-types/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="0e7e8-157">Single-page apps (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="0e7e8-157">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="0e7e8-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="0e7e8-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="0e7e8-160">The Azure AD v2.0 endpoint supports these apps by using the [OAuth 2.0 implicit flow](v2-oauth2-implicit-grant-flow.md).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-160">The Azure AD v2.0 endpoint supports these apps by using the [OAuth 2.0 implicit flow](v2-oauth2-implicit-grant-flow.md).</span></span>

<span data-ttu-id="0e7e8-161">In this flow, the app receives tokens directly from the v2.0 authorize endpoint, without any server-to-server exchanges.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-161">In this flow, the app receives tokens directly from the v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="0e7e8-162">All authentication logic and session handling takes place entirely in the JavaScript client, without extra page redirects.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-162">All authentication logic and session handling takes place entirely in the JavaScript client, without extra page redirects.</span></span>

![Implicit authentication flow](./media/v2-app-types/convergence_scenarios_implicit.png)

<span data-ttu-id="0e7e8-164">To see this scenario in action, try one of the single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-164">To see this scenario in action, try one of the single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="daemons-and-server-side-apps"></a><span data-ttu-id="0e7e8-165">Daemons and server-side apps</span><span class="sxs-lookup"><span data-stu-id="0e7e8-165">Daemons and server-side apps</span></span>
<span data-ttu-id="0e7e8-166">Apps that have long-running processes or that operate without interaction with a user also need a way to access secured resources, such as Web APIs.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-166">Apps that have long-running processes or that operate without interaction with a user also need a way to access secured resources, such as Web APIs.</span></span> <span data-ttu-id="0e7e8-167">These apps can authenticate and get tokens by using the app's identity, rather than a user's delegated identity, with the OAuth 2.0 client credentials flow.</span><span class="sxs-lookup"><span data-stu-id="0e7e8-167">These apps can authenticate and get tokens by using the app's identity, rather than a user's delegated identity, with the OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="0e7e8-168">In this flow, the app interacts directly with the `/token` endpoint to obtain endpoints:</span><span class="sxs-lookup"><span data-stu-id="0e7e8-168">In this flow, the app interacts directly with the `/token` endpoint to obtain endpoints:</span></span>

![Daemon app authentication flow](./media/v2-app-types/convergence_scenarios_daemon.png)

<span data-ttu-id="0e7e8-170">To build a daemon app, see the [client credentials documentation](v2-oauth2-client-creds-grant-flow.md), or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span><span class="sxs-lookup"><span data-stu-id="0e7e8-170">To build a daemon app, see the [client credentials documentation](v2-oauth2-client-creds-grant-flow.md), or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>
