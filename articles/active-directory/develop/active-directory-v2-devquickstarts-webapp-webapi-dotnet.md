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
# <a name="calling-a-web-api-from-a-net-web-app"></a>Calling a web API from a .NET web app
With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.  Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.  The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".

This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).  As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).

> [!NOTE]
> Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.  To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

## <a name="download-sample-code"></a>Download sample code
The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).  To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a>Register an app
Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).  Make sure to:

* Copy down the **Application Id** assigned to your app, you'll need it soon.
* Create an **App Secret** of the **Password** type, and copy down its value for later
* Add the **Web** platform for your app.
* Enter the correct **Redirect URI**. The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.

## <a name="install-owin"></a>Install OWIN
Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.  The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-the-user-in"></a>Sign the user in
Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).  

* Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.
  * The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.
  * The `ida:ClientSecret` is the **App Secret** you created in the registration portal.
  * The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.
* Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.
* Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.
* In the same file, implement the `ConfigureAuth(...)` method.  The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.

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

## <a name="use-msal-to-get-access-tokens"></a>Use MSAL to get access tokens
In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.  MSAL can make this process easy for you:

* First, install the preview version of MSAL:

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.
* Now add a new method, the `OnAuthorizationCodeReceived` event handler.  This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:

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

* In web apps, MSAL has an extensible token cache that can be used to store tokens.  This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.

<!-- TODO: Token Cache article -->


## <a name="call-the-web-api"></a>Call the Web API
Now it's time to actually use the access_token you acquired in step 3.  Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.

* You can use MSAL again here to fetch access_tokens from the MSAL cache.  First, add a `using` statement for MSAL to this file.
  
    `using Microsoft.Identity.Client;`
* In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:

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

* The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.
* If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.  In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.

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

* Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.  This is as simple as catching any `MSALException`:

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show the user an error indicating they might need to sign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading To Do List: " + ee.Message + " You might need to log out and log back in.");
}
// ...
```

* The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.  In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.  MSAL will take care of acquiring, caching, and refreshing tokens for you.

Finally, build and run your app!  Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.  Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.  You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.

For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).  

## <a name="next-steps"></a>Next Steps
For additional resources, check out:

* [The v2.0 developer guide >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow "azure-active-directory" tag >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Get security updates for our products
We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.

