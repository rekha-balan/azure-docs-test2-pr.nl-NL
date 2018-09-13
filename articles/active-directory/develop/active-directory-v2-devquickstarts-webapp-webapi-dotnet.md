---
title: Azure AD v2.0 .NET web app calling API getting started | Microsoft Docs
description: How to build a .NET MVC Web App that calls web services using personal Microsoft accounts and work or school accounts for sign-in.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.openlocfilehash: c6cca8fda4ba6a26d5ee74b43e0bae37639865c5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554965"
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="d97e7-103">Calling a web API from a .NET web app</span><span class="sxs-lookup"><span data-stu-id="d97e7-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="d97e7-104">With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span><span class="sxs-lookup"><span data-stu-id="d97e7-104">With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="d97e7-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span><span class="sxs-lookup"><span data-stu-id="d97e7-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="d97e7-106">The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span><span class="sxs-lookup"><span data-stu-id="d97e7-106">The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="d97e7-107">This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="d97e7-107">This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="d97e7-108">As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="d97e7-108">As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d97e7-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="d97e7-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="d97e7-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d97e7-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="d97e7-111">Download sample code</span><span class="sxs-lookup"><span data-stu-id="d97e7-111">Download sample code</span></span>
<span data-ttu-id="d97e7-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="d97e7-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="d97e7-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span><span class="sxs-lookup"><span data-stu-id="d97e7-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="d97e7-114">Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:</span><span class="sxs-lookup"><span data-stu-id="d97e7-114">Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="d97e7-115">Register an app</span><span class="sxs-lookup"><span data-stu-id="d97e7-115">Register an app</span></span>
<span data-ttu-id="d97e7-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="d97e7-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="d97e7-117">Make sure to:</span><span class="sxs-lookup"><span data-stu-id="d97e7-117">Make sure to:</span></span>

* <span data-ttu-id="d97e7-118">Copy down the **Application Id** assigned to your app, you'll need it soon.</span><span class="sxs-lookup"><span data-stu-id="d97e7-118">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="d97e7-119">Create an **App Secret** of the **Password** type, and copy down its value for later</span><span class="sxs-lookup"><span data-stu-id="d97e7-119">Create an **App Secret** of the **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="d97e7-120">Add the **Web** platform for your app.</span><span class="sxs-lookup"><span data-stu-id="d97e7-120">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="d97e7-121">Enter the correct **Redirect URI**.</span><span class="sxs-lookup"><span data-stu-id="d97e7-121">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="d97e7-122">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="d97e7-122">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="d97e7-123">Install OWIN</span><span class="sxs-lookup"><span data-stu-id="d97e7-123">Install OWIN</span></span>
<span data-ttu-id="d97e7-124">Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="d97e7-124">Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.</span></span>  <span data-ttu-id="d97e7-125">The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span><span class="sxs-lookup"><span data-stu-id="d97e7-125">The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-the-user-in"></a><span data-ttu-id="d97e7-126">Sign the user in</span><span class="sxs-lookup"><span data-stu-id="d97e7-126">Sign the user in</span></span>
<span data-ttu-id="d97e7-127">Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="d97e7-127">Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="d97e7-128">Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="d97e7-128">Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="d97e7-129">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span><span class="sxs-lookup"><span data-stu-id="d97e7-129">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="d97e7-130">The `ida:ClientSecret` is the **App Secret** you created in the registration portal.</span><span class="sxs-lookup"><span data-stu-id="d97e7-130">The `ida:ClientSecret` is the **App Secret** you created in the registration portal.</span></span>
  * <span data-ttu-id="d97e7-131">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span><span class="sxs-lookup"><span data-stu-id="d97e7-131">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>
* <span data-ttu-id="d97e7-132">Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.</span><span class="sxs-lookup"><span data-stu-id="d97e7-132">Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.</span></span>
* <span data-ttu-id="d97e7-133">Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.</span><span class="sxs-lookup"><span data-stu-id="d97e7-133">Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.</span></span>
* <span data-ttu-id="d97e7-134">In the same file, implement the `ConfigureAuth(...)` method.</span><span class="sxs-lookup"><span data-stu-id="d97e7-134">In the same file, implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="d97e7-135">The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d97e7-135">The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // The `Authority` represents the v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // The `Scope` describes the permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure the user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // The `AuthorizationCodeReceived` notification is used to capture and redeem the authorization_code that the v2.0 endpoint returns to your app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-to-get-access-tokens"></a><span data-ttu-id="d97e7-136">Use MSAL to get access tokens</span><span class="sxs-lookup"><span data-stu-id="d97e7-136">Use MSAL to get access tokens</span></span>
<span data-ttu-id="d97e7-137">In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.</span><span class="sxs-lookup"><span data-stu-id="d97e7-137">In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.</span></span>  <span data-ttu-id="d97e7-138">MSAL can make this process easy for you:</span><span class="sxs-lookup"><span data-stu-id="d97e7-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="d97e7-139">First, install the preview version of MSAL:</span><span class="sxs-lookup"><span data-stu-id="d97e7-139">First, install the preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="d97e7-140">And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.</span><span class="sxs-lookup"><span data-stu-id="d97e7-140">And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="d97e7-141">Now add a new method, the `OnAuthorizationCodeReceived` event handler.</span><span class="sxs-lookup"><span data-stu-id="d97e7-141">Now add a new method, the `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="d97e7-142">This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:</span><span class="sxs-lookup"><span data-stu-id="d97e7-142">This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="d97e7-143">In web apps, MSAL has an extensible token cache that can be used to store tokens.</span><span class="sxs-lookup"><span data-stu-id="d97e7-143">In web apps, MSAL has an extensible token cache that can be used to store tokens.</span></span>  <span data-ttu-id="d97e7-144">This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.</span><span class="sxs-lookup"><span data-stu-id="d97e7-144">This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-the-web-api"></a><span data-ttu-id="d97e7-145">Call the Web API</span><span class="sxs-lookup"><span data-stu-id="d97e7-145">Call the Web API</span></span>
<span data-ttu-id="d97e7-146">Now it's time to actually use the access_token you acquired in step 3.</span><span class="sxs-lookup"><span data-stu-id="d97e7-146">Now it's time to actually use the access_token you acquired in step 3.</span></span>  <span data-ttu-id="d97e7-147">Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.</span><span class="sxs-lookup"><span data-stu-id="d97e7-147">Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.</span></span>

* <span data-ttu-id="d97e7-148">You can use MSAL again here to fetch access_tokens from the MSAL cache.</span><span class="sxs-lookup"><span data-stu-id="d97e7-148">You can use MSAL again here to fetch access_tokens from the MSAL cache.</span></span>  <span data-ttu-id="d97e7-149">First, add a `using` statement for MSAL to this file.</span><span class="sxs-lookup"><span data-stu-id="d97e7-149">First, add a `using` statement for MSAL to this file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="d97e7-150">In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:</span><span class="sxs-lookup"><span data-stu-id="d97e7-150">In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="d97e7-151">The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.</span><span class="sxs-lookup"><span data-stu-id="d97e7-151">The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.</span></span>
* <span data-ttu-id="d97e7-152">If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.</span><span class="sxs-lookup"><span data-stu-id="d97e7-152">If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="d97e7-153">In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.</span><span class="sxs-lookup"><span data-stu-id="d97e7-153">In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.</span></span>

```C#
// ...
// If the call failed with access denied, then drop the current access token from the cache,
// and show the user an error indicating they might need to sign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need to sign in again.");
}
// ...
```

* <span data-ttu-id="d97e7-154">Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.</span><span class="sxs-lookup"><span data-stu-id="d97e7-154">Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.</span></span>  <span data-ttu-id="d97e7-155">This is as simple as catching any `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="d97e7-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show the user an error indicating they might need to sign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading To Do List: " + ee.Message + " You might need to log out and log back in.");
}
// ...
```

* <span data-ttu-id="d97e7-156">The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.</span><span class="sxs-lookup"><span data-stu-id="d97e7-156">The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.</span></span>  <span data-ttu-id="d97e7-157">In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.</span><span class="sxs-lookup"><span data-stu-id="d97e7-157">In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="d97e7-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span><span class="sxs-lookup"><span data-stu-id="d97e7-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="d97e7-159">Finally, build and run your app!</span><span class="sxs-lookup"><span data-stu-id="d97e7-159">Finally, build and run your app!</span></span>  <span data-ttu-id="d97e7-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="d97e7-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="d97e7-161">Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.</span><span class="sxs-lookup"><span data-stu-id="d97e7-161">Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="d97e7-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span><span class="sxs-lookup"><span data-stu-id="d97e7-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="d97e7-163">For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d97e7-163">For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d97e7-164">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d97e7-164">Next Steps</span></span>
<span data-ttu-id="d97e7-165">For additional resources, check out:</span><span class="sxs-lookup"><span data-stu-id="d97e7-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="d97e7-166">The v2.0 developer guide >></span><span class="sxs-lookup"><span data-stu-id="d97e7-166">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="d97e7-167">StackOverflow "azure-active-directory" tag >></span><span class="sxs-lookup"><span data-stu-id="d97e7-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="d97e7-168">Get security updates for our products</span><span class="sxs-lookup"><span data-stu-id="d97e7-168">Get security updates for our products</span></span>
<span data-ttu-id="d97e7-169">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="d97e7-169">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

