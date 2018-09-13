---
title: Customize authentication and authorization in Azure App Service | Microsoft Docs
description: Shows how to customize authentication and authorization in App Service, and get user claims and different tokens.
services: app-service
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2018
ms.author: cephalin
ms.openlocfilehash: 629a76ab5610625e14780d7b5c57d3979c2224c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855681"
---
# <a name="customize-authentication-and-authorization-in-azure-app-service"></a><span data-ttu-id="b422d-103">Customize authentication and authorization in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b422d-103">Customize authentication and authorization in Azure App Service</span></span>

<span data-ttu-id="b422d-104">This article shows you how to customize [authentication and authorization in App Service](app-service-authentication-overview.md), and to manage identity from your application.</span><span class="sxs-lookup"><span data-stu-id="b422d-104">This article shows you how to customize [authentication and authorization in App Service](app-service-authentication-overview.md), and to manage identity from your application.</span></span> 

<span data-ttu-id="b422d-105">To get started quickly, see one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="b422d-105">To get started quickly, see one of the following tutorials:</span></span>

* [<span data-ttu-id="b422d-106">Tutorial: Authenticate and authorize users end-to-end in Azure App Service (Windows)</span><span class="sxs-lookup"><span data-stu-id="b422d-106">Tutorial: Authenticate and authorize users end-to-end in Azure App Service (Windows)</span></span>](app-service-web-tutorial-auth-aad.md)
* [<span data-ttu-id="b422d-107">Tutorial: Authenticate and authorize users end-to-end in Azure App Service for Linux</span><span class="sxs-lookup"><span data-stu-id="b422d-107">Tutorial: Authenticate and authorize users end-to-end in Azure App Service for Linux</span></span>](containers/tutorial-auth-aad.md)
* [<span data-ttu-id="b422d-108">How to configure your app to use Azure Active Directory login</span><span class="sxs-lookup"><span data-stu-id="b422d-108">How to configure your app to use Azure Active Directory login</span></span>](app-service-mobile-how-to-configure-active-directory-authentication.md)
* [<span data-ttu-id="b422d-109">How to configure your app to use Facebook login</span><span class="sxs-lookup"><span data-stu-id="b422d-109">How to configure your app to use Facebook login</span></span>](app-service-mobile-how-to-configure-facebook-authentication.md)
* [<span data-ttu-id="b422d-110">How to configure your app to use Google login</span><span class="sxs-lookup"><span data-stu-id="b422d-110">How to configure your app to use Google login</span></span>](app-service-mobile-how-to-configure-google-authentication.md)
* [<span data-ttu-id="b422d-111">How to configure your app to use Microsoft Account login</span><span class="sxs-lookup"><span data-stu-id="b422d-111">How to configure your app to use Microsoft Account login</span></span>](app-service-mobile-how-to-configure-microsoft-authentication.md)
* [<span data-ttu-id="b422d-112">How to configure your app to use Twitter login</span><span class="sxs-lookup"><span data-stu-id="b422d-112">How to configure your app to use Twitter login</span></span>](app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="use-multiple-sign-in-providers"></a><span data-ttu-id="b422d-113">Use multiple sign-in providers</span><span class="sxs-lookup"><span data-stu-id="b422d-113">Use multiple sign-in providers</span></span>

<span data-ttu-id="b422d-114">The portal configuration doesn't offer a turn-key way to present multiple sign-in providers to your users (such as both Facebook and Twitter).</span><span class="sxs-lookup"><span data-stu-id="b422d-114">The portal configuration doesn't offer a turn-key way to present multiple sign-in providers to your users (such as both Facebook and Twitter).</span></span> <span data-ttu-id="b422d-115">However, it isn't difficult to add the functionality to your web app.</span><span class="sxs-lookup"><span data-stu-id="b422d-115">However, it isn't difficult to add the functionality to your web app.</span></span> <span data-ttu-id="b422d-116">The steps are outlined as follows:</span><span class="sxs-lookup"><span data-stu-id="b422d-116">The steps are outlined as follows:</span></span>

<span data-ttu-id="b422d-117">First, in the **Authentication / Authorization** page in the Azure portal, configure each of the identity provider you want to enable.</span><span class="sxs-lookup"><span data-stu-id="b422d-117">First, in the **Authentication / Authorization** page in the Azure portal, configure each of the identity provider you want to enable.</span></span>

<span data-ttu-id="b422d-118">In **Action to take when request is not authenticated**, select **Allow Anonymous requests (no action)**.</span><span class="sxs-lookup"><span data-stu-id="b422d-118">In **Action to take when request is not authenticated**, select **Allow Anonymous requests (no action)**.</span></span>

<span data-ttu-id="b422d-119">In the sign-in page, or the navigation bar, or any other location of your web app, add a sign-in link to each of the providers you enabled (`/.auth/login/<provider>`).</span><span class="sxs-lookup"><span data-stu-id="b422d-119">In the sign-in page, or the navigation bar, or any other location of your web app, add a sign-in link to each of the providers you enabled (`/.auth/login/<provider>`).</span></span> <span data-ttu-id="b422d-120">For example:</span><span class="sxs-lookup"><span data-stu-id="b422d-120">For example:</span></span>

```HTML
<a href="/.auth/login/aad">Log in with Azure AD</a>
<a href="/.auth/login/microsoftaccount">Log in with Microsoft Account</a>
<a href="/.auth/login/facebook">Log in with Facebook</a>
<a href="/.auth/login/google">Log in with Google</a>
<a href="/.auth/login/twitter">Log in with Twitter</a>
```

<span data-ttu-id="b422d-121">When the user clicks on one of the links, the respective sign-in page opens to sign in the user.</span><span class="sxs-lookup"><span data-stu-id="b422d-121">When the user clicks on one of the links, the respective sign-in page opens to sign in the user.</span></span>

<span data-ttu-id="b422d-122">To redirect the user post-sign-in to a custom URL, use the `post_login_redirect_url` query string parameter (not to be confused with the Redirect URI in your identity provider configuration).</span><span class="sxs-lookup"><span data-stu-id="b422d-122">To redirect the user post-sign-in to a custom URL, use the `post_login_redirect_url` query string parameter (not to be confused with the Redirect URI in your identity provider configuration).</span></span> <span data-ttu-id="b422d-123">For example, to navigate the user to `/Home/Index` after sign-in, use the following HTML code:</span><span class="sxs-lookup"><span data-stu-id="b422d-123">For example, to navigate the user to `/Home/Index` after sign-in, use the following HTML code:</span></span>

```HTML
<a href="/.auth/login/<provider>?post_login_redirect_url=/Home/Index">Log in</a>
```

## <a name="sign-out-of-a-session"></a><span data-ttu-id="b422d-124">Sign out of a session</span><span class="sxs-lookup"><span data-stu-id="b422d-124">Sign out of a session</span></span>

<span data-ttu-id="b422d-125">Users can initiate a sign-out by sending a `GET` request to the app's `/.auth/logout` endpoint.</span><span class="sxs-lookup"><span data-stu-id="b422d-125">Users can initiate a sign-out by sending a `GET` request to the app's `/.auth/logout` endpoint.</span></span> <span data-ttu-id="b422d-126">The `GET` request does the following:</span><span class="sxs-lookup"><span data-stu-id="b422d-126">The `GET` request does the following:</span></span>

- <span data-ttu-id="b422d-127">Clears authentication cookies from the current session.</span><span class="sxs-lookup"><span data-stu-id="b422d-127">Clears authentication cookies from the current session.</span></span>
- <span data-ttu-id="b422d-128">Deletes the current user's tokens from the token store.</span><span class="sxs-lookup"><span data-stu-id="b422d-128">Deletes the current user's tokens from the token store.</span></span>
- <span data-ttu-id="b422d-129">For Azure Active Directory and Google, performs a server-side sign-out on the identity provider.</span><span class="sxs-lookup"><span data-stu-id="b422d-129">For Azure Active Directory and Google, performs a server-side sign-out on the identity provider.</span></span>

<span data-ttu-id="b422d-130">Here's a simple sign-out link in a webpage:</span><span class="sxs-lookup"><span data-stu-id="b422d-130">Here's a simple sign-out link in a webpage:</span></span>

```HTML
<a href="/.auth/logout">Sign out</a>
```

<span data-ttu-id="b422d-131">By default, a successful sign-out redirects the client to the URL `/.auth/logout/done`.</span><span class="sxs-lookup"><span data-stu-id="b422d-131">By default, a successful sign-out redirects the client to the URL `/.auth/logout/done`.</span></span> <span data-ttu-id="b422d-132">You can change the post-sign-out redirect page by adding the `post_logout_redirect_uri` query parameter.</span><span class="sxs-lookup"><span data-stu-id="b422d-132">You can change the post-sign-out redirect page by adding the `post_logout_redirect_uri` query parameter.</span></span> <span data-ttu-id="b422d-133">For example:</span><span class="sxs-lookup"><span data-stu-id="b422d-133">For example:</span></span>

```
GET /.auth/logout?post_logout_redirect_uri=/index.html
```

<span data-ttu-id="b422d-134">It's recommended that you [encode](https://wikipedia.org/wiki/Percent-encoding) the value of `post_logout_redirect_uri`.</span><span class="sxs-lookup"><span data-stu-id="b422d-134">It's recommended that you [encode](https://wikipedia.org/wiki/Percent-encoding) the value of `post_logout_redirect_uri`.</span></span>

<span data-ttu-id="b422d-135">When using fully qualified URLs, the URL must be either hosted in the same domain or configured as an allowed external redirect URL for your app.</span><span class="sxs-lookup"><span data-stu-id="b422d-135">When using fully qualified URLs, the URL must be either hosted in the same domain or configured as an allowed external redirect URL for your app.</span></span> <span data-ttu-id="b422d-136">In the following example, to redirect to `https://myexternalurl.com` that's not hosted in the same domain:</span><span class="sxs-lookup"><span data-stu-id="b422d-136">In the following example, to redirect to `https://myexternalurl.com` that's not hosted in the same domain:</span></span>

```
GET /.auth/logout?post_logout_redirect_uri=https%3A%2F%2Fmyexternalurl.com
```

<span data-ttu-id="b422d-137">You must run the following command in the [Azure Cloud Shell](../cloud-shell/quickstart.md):</span><span class="sxs-lookup"><span data-stu-id="b422d-137">You must run the following command in the [Azure Cloud Shell](../cloud-shell/quickstart.md):</span></span>

```azurecli-interactive
az webapp auth update --name <app_name> --resource-group <group_name> --allowed-external-redirect-urls "https://myexternalurl.com"
```

## <a name="preserve-url-fragments"></a><span data-ttu-id="b422d-138">Preserve URL fragments</span><span class="sxs-lookup"><span data-stu-id="b422d-138">Preserve URL fragments</span></span>

<span data-ttu-id="b422d-139">After users sign in to your app, they usually want to be redirected to the same section of the same page, such as `/wiki/Main_Page#SectionZ`.</span><span class="sxs-lookup"><span data-stu-id="b422d-139">After users sign in to your app, they usually want to be redirected to the same section of the same page, such as `/wiki/Main_Page#SectionZ`.</span></span> <span data-ttu-id="b422d-140">However, because [URL fragments](https://wikipedia.org/wiki/Fragment_identifier) (for example, `#SectionZ`) are never sent to the server, they are not preserved by default after the OAuth sign-in completes and redirects back to your app.</span><span class="sxs-lookup"><span data-stu-id="b422d-140">However, because [URL fragments](https://wikipedia.org/wiki/Fragment_identifier) (for example, `#SectionZ`) are never sent to the server, they are not preserved by default after the OAuth sign-in completes and redirects back to your app.</span></span> <span data-ttu-id="b422d-141">Users then get a suboptimal experience when they need to navigate to the desired anchor again.</span><span class="sxs-lookup"><span data-stu-id="b422d-141">Users then get a suboptimal experience when they need to navigate to the desired anchor again.</span></span> <span data-ttu-id="b422d-142">This limitation applies to all server-side authentication solutions.</span><span class="sxs-lookup"><span data-stu-id="b422d-142">This limitation applies to all server-side authentication solutions.</span></span>

<span data-ttu-id="b422d-143">In App Service authentication, you can preserve URL fragments across the OAuth sign-in.</span><span class="sxs-lookup"><span data-stu-id="b422d-143">In App Service authentication, you can preserve URL fragments across the OAuth sign-in.</span></span> <span data-ttu-id="b422d-144">To do this, set an app setting called `WEBSITE_AUTH_PRESERVE_URL_FRAGMENT` to `true`.</span><span class="sxs-lookup"><span data-stu-id="b422d-144">To do this, set an app setting called `WEBSITE_AUTH_PRESERVE_URL_FRAGMENT` to `true`.</span></span> <span data-ttu-id="b422d-145">You can do it in the [Azure portal](https://portal.azure.com), or simply run the following command in the [Azure Cloud Shell](../cloud-shell/quickstart.md):</span><span class="sxs-lookup"><span data-stu-id="b422d-145">You can do it in the [Azure portal](https://portal.azure.com), or simply run the following command in the [Azure Cloud Shell](../cloud-shell/quickstart.md):</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group <group_name> --settings WEBSITE_AUTH_PRESERVE_URL_FRAGMENT="true"
```

## <a name="access-user-claims"></a><span data-ttu-id="b422d-146">Access user claims</span><span class="sxs-lookup"><span data-stu-id="b422d-146">Access user claims</span></span>

<span data-ttu-id="b422d-147">App Service passes user claims to your application by using special headers.</span><span class="sxs-lookup"><span data-stu-id="b422d-147">App Service passes user claims to your application by using special headers.</span></span> <span data-ttu-id="b422d-148">External requests aren't allowed to set these headers, so they are present only if set by App Service.</span><span class="sxs-lookup"><span data-stu-id="b422d-148">External requests aren't allowed to set these headers, so they are present only if set by App Service.</span></span> <span data-ttu-id="b422d-149">Some example headers include:</span><span class="sxs-lookup"><span data-stu-id="b422d-149">Some example headers include:</span></span>

* <span data-ttu-id="b422d-150">X-MS-CLIENT-PRINCIPAL-NAME</span><span class="sxs-lookup"><span data-stu-id="b422d-150">X-MS-CLIENT-PRINCIPAL-NAME</span></span>
* <span data-ttu-id="b422d-151">X-MS-CLIENT-PRINCIPAL-ID</span><span class="sxs-lookup"><span data-stu-id="b422d-151">X-MS-CLIENT-PRINCIPAL-ID</span></span>

<span data-ttu-id="b422d-152">Code that is written in any language or framework can get the information that it needs from these headers.</span><span class="sxs-lookup"><span data-stu-id="b422d-152">Code that is written in any language or framework can get the information that it needs from these headers.</span></span> <span data-ttu-id="b422d-153">For ASP.NET 4.6 apps, the **ClaimsPrincipal** is automatically set with the appropriate values.</span><span class="sxs-lookup"><span data-stu-id="b422d-153">For ASP.NET 4.6 apps, the **ClaimsPrincipal** is automatically set with the appropriate values.</span></span>

<span data-ttu-id="b422d-154">Your application can also obtain additional details on the authenticated user by calling `/.auth/me`.</span><span class="sxs-lookup"><span data-stu-id="b422d-154">Your application can also obtain additional details on the authenticated user by calling `/.auth/me`.</span></span> <span data-ttu-id="b422d-155">The Mobile Apps server SDKs provide helper methods to work with this data.</span><span class="sxs-lookup"><span data-stu-id="b422d-155">The Mobile Apps server SDKs provide helper methods to work with this data.</span></span> <span data-ttu-id="b422d-156">For more information, see [How to use the Azure Mobile Apps Node.js SDK](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity), and [Work with the .NET backend server SDK for Azure Mobile Apps](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info).</span><span class="sxs-lookup"><span data-stu-id="b422d-156">For more information, see [How to use the Azure Mobile Apps Node.js SDK](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity), and [Work with the .NET backend server SDK for Azure Mobile Apps](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info).</span></span>

## <a name="retrieve-tokens-in-app-code"></a><span data-ttu-id="b422d-157">Retrieve tokens in app code</span><span class="sxs-lookup"><span data-stu-id="b422d-157">Retrieve tokens in app code</span></span>

<span data-ttu-id="b422d-158">From your server code, the provider-specific tokens are injected into the request header, so you can easily access them.</span><span class="sxs-lookup"><span data-stu-id="b422d-158">From your server code, the provider-specific tokens are injected into the request header, so you can easily access them.</span></span> <span data-ttu-id="b422d-159">The following table shows possible token header names:</span><span class="sxs-lookup"><span data-stu-id="b422d-159">The following table shows possible token header names:</span></span>

| | |
|-|-|
| <span data-ttu-id="b422d-160">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b422d-160">Azure Active Directory</span></span> | `X-MS-TOKEN-AAD-ID-TOKEN` <br/> `X-MS-TOKEN-AAD-ACCESS-TOKEN` <br/> `X-MS-TOKEN-AAD-EXPIRES-ON`  <br/> `X-MS-TOKEN-AAD-REFRESH-TOKEN` |
| <span data-ttu-id="b422d-161">Facebook Token</span><span class="sxs-lookup"><span data-stu-id="b422d-161">Facebook Token</span></span> | `X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN` <br/> `X-MS-TOKEN-FACEBOOK-EXPIRES-ON` |
| <span data-ttu-id="b422d-162">Google</span><span class="sxs-lookup"><span data-stu-id="b422d-162">Google</span></span> | `X-MS-TOKEN-GOOGLE-ID-TOKEN` <br/> `X-MS-TOKEN-GOOGLE-ACCESS-TOKEN` <br/> `X-MS-TOKEN-GOOGLE-EXPIRES-ON` <br/> `X-MS-TOKEN-GOOGLE-REFRESH-TOKEN` |
| <span data-ttu-id="b422d-163">Microsoft Account</span><span class="sxs-lookup"><span data-stu-id="b422d-163">Microsoft Account</span></span> | `X-MS-TOKEN-MICROSOFTACCOUNT-ACCESS-TOKEN` <br/> `X-MS-TOKEN-MICROSOFTACCOUNT-EXPIRES-ON` <br/> `X-MS-TOKEN-MICROSOFTACCOUNT-AUTHENTICATION-TOKEN` <br/> `X-MS-TOKEN-MICROSOFTACCOUNT-REFRESH-TOKEN` |
| <span data-ttu-id="b422d-164">Twitter</span><span class="sxs-lookup"><span data-stu-id="b422d-164">Twitter</span></span> | `X-MS-TOKEN-TWITTER-ACCESS-TOKEN` <br/> `X-MS-TOKEN-TWITTER-ACCESS-TOKEN-SECRET` |
|||

<span data-ttu-id="b422d-165">From your client code (such as a mobile app or in-browser JavaScript), send an HTTP `GET` request to `/.auth/me`.</span><span class="sxs-lookup"><span data-stu-id="b422d-165">From your client code (such as a mobile app or in-browser JavaScript), send an HTTP `GET` request to `/.auth/me`.</span></span> <span data-ttu-id="b422d-166">The returned JSON has the provider-specific tokens.</span><span class="sxs-lookup"><span data-stu-id="b422d-166">The returned JSON has the provider-specific tokens.</span></span>

> [!NOTE]
> <span data-ttu-id="b422d-167">Access tokens are for accessing provider resources, so they are present only if you configure your provider with a client secret.</span><span class="sxs-lookup"><span data-stu-id="b422d-167">Access tokens are for accessing provider resources, so they are present only if you configure your provider with a client secret.</span></span> <span data-ttu-id="b422d-168">To see how to get refresh tokens, see [Refresh access tokens](#refresh-access-tokens).</span><span class="sxs-lookup"><span data-stu-id="b422d-168">To see how to get refresh tokens, see [Refresh access tokens](#refresh-access-tokens).</span></span>

## <a name="refresh-access-tokens"></a><span data-ttu-id="b422d-169">Refresh access tokens</span><span class="sxs-lookup"><span data-stu-id="b422d-169">Refresh access tokens</span></span>

<span data-ttu-id="b422d-170">When your provider's access token expires, you need to reauthenticate the user.</span><span class="sxs-lookup"><span data-stu-id="b422d-170">When your provider's access token expires, you need to reauthenticate the user.</span></span> <span data-ttu-id="b422d-171">You can avoid token expiration by making a `GET` call to the `/.auth/refresh` endpoint of your application.</span><span class="sxs-lookup"><span data-stu-id="b422d-171">You can avoid token expiration by making a `GET` call to the `/.auth/refresh` endpoint of your application.</span></span> <span data-ttu-id="b422d-172">When called, App Service automatically refreshes the access tokens in the token store for the authenticated user.</span><span class="sxs-lookup"><span data-stu-id="b422d-172">When called, App Service automatically refreshes the access tokens in the token store for the authenticated user.</span></span> <span data-ttu-id="b422d-173">Subsequent requests for tokens by your app code get the refreshed tokens.</span><span class="sxs-lookup"><span data-stu-id="b422d-173">Subsequent requests for tokens by your app code get the refreshed tokens.</span></span> <span data-ttu-id="b422d-174">However, for token refresh to work, the token store must contain [refresh tokens](https://auth0.com/learn/refresh-tokens/) for your provider.</span><span class="sxs-lookup"><span data-stu-id="b422d-174">However, for token refresh to work, the token store must contain [refresh tokens](https://auth0.com/learn/refresh-tokens/) for your provider.</span></span> <span data-ttu-id="b422d-175">The way to get refresh tokens are documented by each provider, but the following list is a brief summary:</span><span class="sxs-lookup"><span data-stu-id="b422d-175">The way to get refresh tokens are documented by each provider, but the following list is a brief summary:</span></span>

- <span data-ttu-id="b422d-176">**Google**: Append an `access_type=offline` query string parameter to your `/.auth/login/google` API call.</span><span class="sxs-lookup"><span data-stu-id="b422d-176">**Google**: Append an `access_type=offline` query string parameter to your `/.auth/login/google` API call.</span></span> <span data-ttu-id="b422d-177">If using the Mobile Apps SDK, you can add the parameter to one of the `LogicAsync` overloads (see [Google Refresh Tokens](https://developers.google.com/identity/protocols/OpenIDConnect#refresh-tokens)).</span><span class="sxs-lookup"><span data-stu-id="b422d-177">If using the Mobile Apps SDK, you can add the parameter to one of the `LogicAsync` overloads (see [Google Refresh Tokens](https://developers.google.com/identity/protocols/OpenIDConnect#refresh-tokens)).</span></span>
- <span data-ttu-id="b422d-178">**Facebook**: Doesn't provide refresh tokens.</span><span class="sxs-lookup"><span data-stu-id="b422d-178">**Facebook**: Doesn't provide refresh tokens.</span></span> <span data-ttu-id="b422d-179">Long-lived tokens expire in 60 days (see [Facebook Expiration and Extension of Access Tokens](https://developers.facebook.com/docs/facebook-login/access-tokens/expiration-and-extension)).</span><span class="sxs-lookup"><span data-stu-id="b422d-179">Long-lived tokens expire in 60 days (see [Facebook Expiration and Extension of Access Tokens](https://developers.facebook.com/docs/facebook-login/access-tokens/expiration-and-extension)).</span></span>
- <span data-ttu-id="b422d-180">**Twitter**: Access tokens don't expire (see [Twitter OAuth FAQ](https://developer.twitter.com/en/docs/basics/authentication/guides/oauth-faq)).</span><span class="sxs-lookup"><span data-stu-id="b422d-180">**Twitter**: Access tokens don't expire (see [Twitter OAuth FAQ](https://developer.twitter.com/en/docs/basics/authentication/guides/oauth-faq)).</span></span>
- <span data-ttu-id="b422d-181">**Microsoft Account**: When [configuring Microsoft Account Authentication Settings](app-service-mobile-how-to-configure-microsoft-authentication.md), select the `wl.offline_access` scope.</span><span class="sxs-lookup"><span data-stu-id="b422d-181">**Microsoft Account**: When [configuring Microsoft Account Authentication Settings](app-service-mobile-how-to-configure-microsoft-authentication.md), select the `wl.offline_access` scope.</span></span>
- <span data-ttu-id="b422d-182">**Azure Active Directory**: In [https://resources.azure.com](https://resources.azure.com), do the following steps:</span><span class="sxs-lookup"><span data-stu-id="b422d-182">**Azure Active Directory**: In [https://resources.azure.com](https://resources.azure.com), do the following steps:</span></span>
    1. <span data-ttu-id="b422d-183">At the top of the page, select **Read/Write**.</span><span class="sxs-lookup"><span data-stu-id="b422d-183">At the top of the page, select **Read/Write**.</span></span>
    1. <span data-ttu-id="b422d-184">In the left browser, navigate to **subscriptions** > **_\<subscription\_name_** > **resourceGroups** > _**\<resource\_group\_name>**_ > **providers** > **Microsoft.Web** > **sites** > _**\<app\_name>**_ > **config** > **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="b422d-184">In the left browser, navigate to **subscriptions** > **_\<subscription\_name_** > **resourceGroups** > _**\<resource\_group\_name>**_ > **providers** > **Microsoft.Web** > **sites** > _**\<app\_name>**_ > **config** > **authsettings**.</span></span> 
    1. <span data-ttu-id="b422d-185">Click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="b422d-185">Click **Edit**.</span></span>
    1. <span data-ttu-id="b422d-186">Modify the following property.</span><span class="sxs-lookup"><span data-stu-id="b422d-186">Modify the following property.</span></span> <span data-ttu-id="b422d-187">Replace _\<app\_id>_ with the Azure Active Directory application ID of the service you want to access.</span><span class="sxs-lookup"><span data-stu-id="b422d-187">Replace _\<app\_id>_ with the Azure Active Directory application ID of the service you want to access.</span></span>

        ```json
        "additionalLoginParams": ["response_type=code id_token", "resource=<app_id>"]
        ```

    1. <span data-ttu-id="b422d-188">Click **Put**.</span><span class="sxs-lookup"><span data-stu-id="b422d-188">Click **Put**.</span></span> 

<span data-ttu-id="b422d-189">Once your provider is configured, you can [find the refresh token and the expiration time for the access token](#retrieve-tokens-in-app-code) in the token store.</span><span class="sxs-lookup"><span data-stu-id="b422d-189">Once your provider is configured, you can [find the refresh token and the expiration time for the access token](#retrieve-tokens-in-app-code) in the token store.</span></span> 

<span data-ttu-id="b422d-190">To refresh your access token at anytime, just call `/.auth/refresh` in any language.</span><span class="sxs-lookup"><span data-stu-id="b422d-190">To refresh your access token at anytime, just call `/.auth/refresh` in any language.</span></span> <span data-ttu-id="b422d-191">The following snippet uses jQuery to refresh your access tokens from a JavaScript client.</span><span class="sxs-lookup"><span data-stu-id="b422d-191">The following snippet uses jQuery to refresh your access tokens from a JavaScript client.</span></span>

```JavaScript
function refreshTokens() {
  var refreshUrl = "/.auth/refresh";
  $.ajax(refreshUrl) .done(function() {
    console.log("Token refresh completed successfully.");
  }) .fail(function() {
    console.log("Token refresh failed. See application logs for details.");
  });
}
```

<span data-ttu-id="b422d-192">If a user revokes the permissions granted to your app, your call to `/.auth/me` may fail with a `403 Forbidden` response.</span><span class="sxs-lookup"><span data-stu-id="b422d-192">If a user revokes the permissions granted to your app, your call to `/.auth/me` may fail with a `403 Forbidden` response.</span></span> <span data-ttu-id="b422d-193">To diagnose errors, check your application logs for details.</span><span class="sxs-lookup"><span data-stu-id="b422d-193">To diagnose errors, check your application logs for details.</span></span>

## <a name="extend-session-expiration-grace-period"></a><span data-ttu-id="b422d-194">Extend session expiration grace period</span><span class="sxs-lookup"><span data-stu-id="b422d-194">Extend session expiration grace period</span></span>

<span data-ttu-id="b422d-195">After an authenticated session expires, there is a 72-hour grace period by default.</span><span class="sxs-lookup"><span data-stu-id="b422d-195">After an authenticated session expires, there is a 72-hour grace period by default.</span></span> <span data-ttu-id="b422d-196">Within this grace period, you're allowed to refresh the session cookie or session token with App Service without reauthenticating the user.</span><span class="sxs-lookup"><span data-stu-id="b422d-196">Within this grace period, you're allowed to refresh the session cookie or session token with App Service without reauthenticating the user.</span></span> <span data-ttu-id="b422d-197">You can just call `/.auth/refresh` when your session cookie or session token becomes invalid, and you don't need to track token expiration yourself.</span><span class="sxs-lookup"><span data-stu-id="b422d-197">You can just call `/.auth/refresh` when your session cookie or session token becomes invalid, and you don't need to track token expiration yourself.</span></span> <span data-ttu-id="b422d-198">Once the 72-hour grace period is lapses, the user must sign in again to get a valid session cookie or session token.</span><span class="sxs-lookup"><span data-stu-id="b422d-198">Once the 72-hour grace period is lapses, the user must sign in again to get a valid session cookie or session token.</span></span>

<span data-ttu-id="b422d-199">If 72 hours isn't enough time for you, you can extend this expiration window.</span><span class="sxs-lookup"><span data-stu-id="b422d-199">If 72 hours isn't enough time for you, you can extend this expiration window.</span></span> <span data-ttu-id="b422d-200">Extending the expiration over a long period could have significant security implications (such as when an authentication token is leaked or stolen).</span><span class="sxs-lookup"><span data-stu-id="b422d-200">Extending the expiration over a long period could have significant security implications (such as when an authentication token is leaked or stolen).</span></span> <span data-ttu-id="b422d-201">So you should leave it at the default 72 hours or set the extension period to the smallest value.</span><span class="sxs-lookup"><span data-stu-id="b422d-201">So you should leave it at the default 72 hours or set the extension period to the smallest value.</span></span>

<span data-ttu-id="b422d-202">To extend the default expiration window, run the following command in the [Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="b422d-202">To extend the default expiration window, run the following command in the [Cloud Shell](../cloud-shell/overview.md).</span></span>

```azurecli-interactive
az webapp auth update --resource-group <group_name> --name <app_name> --token-refresh-extension-hours <hours>
```

> [!NOTE]
> <span data-ttu-id="b422d-203">The grace period only applies to the App Service authenticated session, not the tokens from the identity providers.</span><span class="sxs-lookup"><span data-stu-id="b422d-203">The grace period only applies to the App Service authenticated session, not the tokens from the identity providers.</span></span> <span data-ttu-id="b422d-204">There is no grace period for the expired provider tokens.</span><span class="sxs-lookup"><span data-stu-id="b422d-204">There is no grace period for the expired provider tokens.</span></span> 
>

## <a name="limit-the-domain-of-sign-in-accounts"></a><span data-ttu-id="b422d-205">Limit the domain of sign-in accounts</span><span class="sxs-lookup"><span data-stu-id="b422d-205">Limit the domain of sign-in accounts</span></span>

<span data-ttu-id="b422d-206">Both Microsoft Account and Azure Active Directory lets you sign in from multiple domains.</span><span class="sxs-lookup"><span data-stu-id="b422d-206">Both Microsoft Account and Azure Active Directory lets you sign in from multiple domains.</span></span> <span data-ttu-id="b422d-207">For example, Microsoft Account allows _outlook.com_, _live.com_, and _hotmail.com_ accounts.</span><span class="sxs-lookup"><span data-stu-id="b422d-207">For example, Microsoft Account allows _outlook.com_, _live.com_, and _hotmail.com_ accounts.</span></span> <span data-ttu-id="b422d-208">Azure Active Directory allows any number of custom domains for the sign-in accounts.</span><span class="sxs-lookup"><span data-stu-id="b422d-208">Azure Active Directory allows any number of custom domains for the sign-in accounts.</span></span> <span data-ttu-id="b422d-209">This behavior may be undesirable for an internal app, which you don't want anyone with an _outlook.com_ account to access.</span><span class="sxs-lookup"><span data-stu-id="b422d-209">This behavior may be undesirable for an internal app, which you don't want anyone with an _outlook.com_ account to access.</span></span> <span data-ttu-id="b422d-210">To limit the domain name of the sign-in accounts, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="b422d-210">To limit the domain name of the sign-in accounts, follow these steps.</span></span>

<span data-ttu-id="b422d-211">In [https://resources.azure.com](https://resources.azure.com), navigate to **subscriptions** > **_\<subscription\_name_** > **resourceGroups** > _**\<resource\_group\_name>**_ > **providers** > **Microsoft.Web** > **sites** > _**\<app\_name>**_ > **config** > **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="b422d-211">In [https://resources.azure.com](https://resources.azure.com), navigate to **subscriptions** > **_\<subscription\_name_** > **resourceGroups** > _**\<resource\_group\_name>**_ > **providers** > **Microsoft.Web** > **sites** > _**\<app\_name>**_ > **config** > **authsettings**.</span></span> 

<span data-ttu-id="b422d-212">Click **Edit**, modify the following property, and then click **Put**.</span><span class="sxs-lookup"><span data-stu-id="b422d-212">Click **Edit**, modify the following property, and then click **Put**.</span></span> <span data-ttu-id="b422d-213">Be sure to replace _\<domain\_name>_ with the domain you want.</span><span class="sxs-lookup"><span data-stu-id="b422d-213">Be sure to replace _\<domain\_name>_ with the domain you want.</span></span>

```json
"additionalLoginParams": ["domain_hint=<domain_name>"]
```
## <a name="next-steps"></a><span data-ttu-id="b422d-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="b422d-214">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="b422d-215">[Tutorial: Authenticate and authorize users end-to-end (Windows)](app-service-web-tutorial-auth-aad.md)
> [Tutorial: Authenticate and authorize users end-to-end (Linux)](containers/tutorial-auth-aad.md)</span><span class="sxs-lookup"><span data-stu-id="b422d-215">[Tutorial: Authenticate and authorize users end-to-end (Windows)](app-service-web-tutorial-auth-aad.md)
[Tutorial: Authenticate and authorize users end-to-end (Linux)](containers/tutorial-auth-aad.md)</span></span>