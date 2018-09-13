---
title: Azure Active Directory B2C | Microsoft Docs
description: How to build a web application that has sign-up/sign-in, profile edit, and password reset using Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: ''
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 4d7476156b51ca82b1f119becb1576a97d2bd457
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564607"
---
# <a name="azure-ad-b2c-sign-up--sign-in-in-a-aspnet-web-app"></a>Azure AD B2C: Sign-Up & Sign-In in a ASP.NET Web App

By using Azure AD B2C, you can add powerful identity management features to your web app. This article will discuss how to create an ASP.NET web app that includes user sign-up/sign-in, profile edit, and password reset.

## <a name="create-an-azure-ad-b2c-directory"></a>Create an Azure AD B2C directory

Before you can use Azure AD B2C, you must create a directory, or tenant. A directory is a container for all of your users, apps, groups, and more. If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.

## <a name="create-an-application"></a>Create an application

Next, you need to create a web app in your B2C directory. This gives Azure AD information that it needs to securely communicate with your app. To create an app, follow [these instructions](active-directory-b2c-app-registration.md). Be sure to:

* Include a **web app/web API** in the application.
* Enter `https://localhost:44316/` as a **Redirect URI**. It is the default URL for this code sample.
* Copy down the **Application ID** that is assigned to your app.  You will need it later.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Create your policies

In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md). This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit** and **password reset**.  You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md). When you create the policies, be sure to:

* Choose **User ID sign-up** or **Email sign-up** in the identity providers blade.
* Choose the **Display name** and other sign-up attributes in your sign-up & sign-in policy.
* Choose the **Display name** claim as an application claim in every policy. You can choose other claims as well.
* Copy the **Name** of each policy after you create it. You'll need those policy names later.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

After you create your policies, you're ready to build your app.

## <a name="download-the-code"></a>Download the code

The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/b2c-dotnet-webapp-and-webapi). You can clone the sample by running:

```console
git clone https://github.com/Azure-Samples/b2c-dotnet-webapp-and-webapi.git
```

After you download the sample code, open the Visual Studio .sln file to get started. The solution file contains two projects: `TaskWebApp` and `TaskService`. `TaskWebApp` is the MVC web application that the user interacts with. `TaskService` is the app's back-end web API that stores each user's to-do list. This article will only discuss the `TaskWebApp` application. To learn how to build `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).

### <a name="update-the-azure-ad-b2c-configuration"></a>Update the Azure AD B2C configuration

Our sample is configured to use the policies and client ID of our demo tenant. If you would like to use your own tenant, you will need to open `web.config` in the `TaskWebApp` project and replace the values for

* `ida:Tenant` with your tenant name
* `ida:ClientId` with your web app application ID
* `ida:ClientSecret` with your web app secret key
* `ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name
* `ida:EditProfilePolicyId` with your "Edit Profile" policy name
* `ida:ResetPasswordPolicyId` with your "Reset Password" policy name

## <a name="add-authentication-support"></a>Add authentication support

You can now configure your app to use Azure AD B2C. Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests. The requests dictate the user experience your app wants to execute by specifying the policy. You can use Microsoft's OWIN library to send these requests, execute policies, manage user sessions, and more.

### <a name="install-owin"></a>Install OWIN

To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

### <a name="add-an-owin-startup-class"></a>Add an OWIN startup class

Add an OWIN startup class to the API called `Startup.cs`.  Right-click on the project, select **Add** and **New Item**, and then search for OWIN. The OWIN middleware will invoke the `Configuration(…)` method when your app starts.

In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`. Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`. After the modifications, `Startup.cs` looks like the following:

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-the-authentication-middleware"></a>Configure the authentication middleware

Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method. The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD B2C. If you do not specify certain parameters, it will use the default value. For example, we do not specify the `ResponseType` in the sample, so the default value `code id_token` will be used in each outgoing request to Azure AD B2C.

You also need to set up cookie authentication. The OpenID Connect middleware uses cookies to maintain user sessions, among other things.

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure the OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate the metadata address using the tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify the callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify the claims to validate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement the "Notification" methods...
}
```

In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by the OpenID Connect middleware. These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into the `Notifications` variable. In our sample, we define three different callbacks depending on the event.

#### <a name="using-different-policies"></a>Using different policies

The `RedirectToIdentityProvider` notification is triggered whenever a request is made to Azure AD B2C. In the callback function `OnRedirectToIdentityProvider`, we check in the outgoing call if we want to use a different policy. In order to do a password reset or edit a profile, you need to use the corresponding policy such as the password reset policy instead of the default "Sign-up or Sign-in" policy.

In our sample, when a user wants to reset the password or edit the profile, we add the policy we prefer to use into the OWIN context. That can be done by doing the following:

```CSharp
    // Let the middleware know you are trying to use the edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

And you can implement the callback function `OnRedirectToIdentityProvider` by doing the following:

```CSharp
/*
*  On each call to Azure AD B2C, check if a policy (e.g. the profile edit or password reset policy) has been specified in the OWIN context.
*  If so, use that policy when making the call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

#### <a name="handling-authorization-codes"></a>Handling authorization codes

The `AuthorizationCodeReceived` notification is triggered when an authorization code is received. The OpenID Connect middleware does not support exchanging codes for access tokens. You can manually exchange the code for the token in a callback function. For more information, please look at the [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.

#### <a name="handling-errors"></a>Handling errors

The `AuthenticationFailed` notification is triggered when authentication fails. In its callback method, you can handle the errors as you wish. You should however add a check for the error code `AADB2C90118`. During the execution of the "Sign-up or Sign-in" policy, the user has the opportunity to click on a **Forgot your password?** link. In this event, Azure AD B2C will send your app that error code indicating that your app should make a request using the password reset policy instead.

```CSharp
/*
* Catch any failures received by the authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle the error code that Azure AD B2C throws when trying to reset a password from the login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If the user clicked the reset password link, redirect to the reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

## <a name="send-authentication-requests-to-azure-ad"></a>Send authentication requests to Azure AD

Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol. OWIN has taken care of all of the details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session. All that remains is to initiate each user's flow.

When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in the web app, the associated action is invoked in `Controllers\AccountController.cs`:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign up or sign in
*/
public void SignUpSignIn()
{
    // Use the default policy to process the sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting to edit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let the middleware know you are trying to use the edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set the page to redirect to after editing the profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting to reset a password
*/
public void ResetPassword()
{
    // Let the middleware know you are trying to use the reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set the page to redirect to after changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

You can also use OWIN to sign out the user from the app. In `Controllers\AccountController.cs` we have:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign out
*/
public void SignOut()
{
    // To sign out the user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

In addition to explicitly invoking a policy, you can use an `[Authorize]` tag in your controllers that will execute a policy if the user is not signed in. Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.  OWIN will select the last policy configured when the `[Authorize]` tag is hit.

```CSharp
// Controllers\HomeController.cs

// You can use the Authorize decorator to execute a certain policy if the user is not already signed into the app.
[Authorize]
public ActionResult Claims()
{
  ...
```

## <a name="display-user-information"></a>Display user information

When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token to the app that contains **claims**. These are assertions about the user. You can use claims to personalize your app.

Open the `Controllers\HomeController.cs` file. You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

You can access any claim that your application receives in the same way.  A list of all the claims the app receives is available for you on the **Claims** page.

## <a name="run-the-sample-app"></a>Run the sample app

Finally, you can build and run your app. Sign up for the app by using an email address or user name. Sign out and sign back in as the same user. Edit the profile or reset the password. Sign out and sign up as a different user. Note that the information displayed on the **Claims** tab corresponds to the information that you configured on your policies.

## <a name="add-social-idps"></a>Add social IDPs

Currently, the app supports only user sign-up and sign-in by using **local accounts**. These are accounts stored in your B2C directory that use a user name and password. By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.

To add social IDPs to your app, begin by following the detailed instructions in these articles. For each IDP you want to support, you need to register an application in that system and obtain a client ID.

* [Set up Facebook as an IDP](active-directory-b2c-setup-fb-app.md)
* [Set up Google as an IDP](active-directory-b2c-setup-goog-app.md)
* [Set up Amazon as an IDP](active-directory-b2c-setup-amzn-app.md)
* [Set up LinkedIn as an IDP](active-directory-b2c-setup-li-app.md)

After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md). After you save your policies, run the app again.  You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.

You can experiment with your policies and observe the effect on your sample app. Add or remove IDPs, manipulate application claims, or change sign-up attributes. Experiment until you can see how policies, authentication requests, and OWIN tie together.
