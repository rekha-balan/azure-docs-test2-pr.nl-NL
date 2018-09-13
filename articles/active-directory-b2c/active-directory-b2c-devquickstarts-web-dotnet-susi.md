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
# <a name="azure-ad-b2c-sign-up--sign-in-in-a-aspnet-web-app"></a><span data-ttu-id="00bff-103">Azure AD B2C: Sign-Up & Sign-In in a ASP.NET Web App</span><span class="sxs-lookup"><span data-stu-id="00bff-103">Azure AD B2C: Sign-Up & Sign-In in a ASP.NET Web App</span></span>

<span data-ttu-id="00bff-104">By using Azure AD B2C, you can add powerful identity management features to your web app.</span><span class="sxs-lookup"><span data-stu-id="00bff-104">By using Azure AD B2C, you can add powerful identity management features to your web app.</span></span> <span data-ttu-id="00bff-105">This article will discuss how to create an ASP.NET web app that includes user sign-up/sign-in, profile edit, and password reset.</span><span class="sxs-lookup"><span data-stu-id="00bff-105">This article will discuss how to create an ASP.NET web app that includes user sign-up/sign-in, profile edit, and password reset.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="00bff-106">Create an Azure AD B2C directory</span><span class="sxs-lookup"><span data-stu-id="00bff-106">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="00bff-107">Before you can use Azure AD B2C, you must create a directory, or tenant.</span><span class="sxs-lookup"><span data-stu-id="00bff-107">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="00bff-108">A directory is a container for all of your users, apps, groups, and more.</span><span class="sxs-lookup"><span data-stu-id="00bff-108">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="00bff-109">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span><span class="sxs-lookup"><span data-stu-id="00bff-109">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="00bff-110">Create an application</span><span class="sxs-lookup"><span data-stu-id="00bff-110">Create an application</span></span>

<span data-ttu-id="00bff-111">Next, you need to create a web app in your B2C directory.</span><span class="sxs-lookup"><span data-stu-id="00bff-111">Next, you need to create a web app in your B2C directory.</span></span> <span data-ttu-id="00bff-112">This gives Azure AD information that it needs to securely communicate with your app.</span><span class="sxs-lookup"><span data-stu-id="00bff-112">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="00bff-113">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="00bff-113">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="00bff-114">Be sure to:</span><span class="sxs-lookup"><span data-stu-id="00bff-114">Be sure to:</span></span>

* <span data-ttu-id="00bff-115">Include a **web app/web API** in the application.</span><span class="sxs-lookup"><span data-stu-id="00bff-115">Include a **web app/web API** in the application.</span></span>
* <span data-ttu-id="00bff-116">Enter `https://localhost:44316/` as a **Redirect URI**.</span><span class="sxs-lookup"><span data-stu-id="00bff-116">Enter `https://localhost:44316/` as a **Redirect URI**.</span></span> <span data-ttu-id="00bff-117">It is the default URL for this code sample.</span><span class="sxs-lookup"><span data-stu-id="00bff-117">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="00bff-118">Copy down the **Application ID** that is assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="00bff-118">Copy down the **Application ID** that is assigned to your app.</span></span>  <span data-ttu-id="00bff-119">You will need it later.</span><span class="sxs-lookup"><span data-stu-id="00bff-119">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="00bff-120">Create your policies</span><span class="sxs-lookup"><span data-stu-id="00bff-120">Create your policies</span></span>

<span data-ttu-id="00bff-121">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="00bff-121">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="00bff-122">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit** and **password reset**.</span><span class="sxs-lookup"><span data-stu-id="00bff-122">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit** and **password reset**.</span></span>  <span data-ttu-id="00bff-123">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="00bff-123">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="00bff-124">When you create the policies, be sure to:</span><span class="sxs-lookup"><span data-stu-id="00bff-124">When you create the policies, be sure to:</span></span>

* <span data-ttu-id="00bff-125">Choose **User ID sign-up** or **Email sign-up** in the identity providers blade.</span><span class="sxs-lookup"><span data-stu-id="00bff-125">Choose **User ID sign-up** or **Email sign-up** in the identity providers blade.</span></span>
* <span data-ttu-id="00bff-126">Choose the **Display name** and other sign-up attributes in your sign-up & sign-in policy.</span><span class="sxs-lookup"><span data-stu-id="00bff-126">Choose the **Display name** and other sign-up attributes in your sign-up & sign-in policy.</span></span>
* <span data-ttu-id="00bff-127">Choose the **Display name** claim as an application claim in every policy.</span><span class="sxs-lookup"><span data-stu-id="00bff-127">Choose the **Display name** claim as an application claim in every policy.</span></span> <span data-ttu-id="00bff-128">You can choose other claims as well.</span><span class="sxs-lookup"><span data-stu-id="00bff-128">You can choose other claims as well.</span></span>
* <span data-ttu-id="00bff-129">Copy the **Name** of each policy after you create it.</span><span class="sxs-lookup"><span data-stu-id="00bff-129">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="00bff-130">You'll need those policy names later.</span><span class="sxs-lookup"><span data-stu-id="00bff-130">You'll need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="00bff-131">After you create your policies, you're ready to build your app.</span><span class="sxs-lookup"><span data-stu-id="00bff-131">After you create your policies, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="00bff-132">Download the code</span><span class="sxs-lookup"><span data-stu-id="00bff-132">Download the code</span></span>

<span data-ttu-id="00bff-133">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="00bff-133">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="00bff-134">You can clone the sample by running:</span><span class="sxs-lookup"><span data-stu-id="00bff-134">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="00bff-135">After you download the sample code, open the Visual Studio .sln file to get started.</span><span class="sxs-lookup"><span data-stu-id="00bff-135">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="00bff-136">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="00bff-136">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="00bff-137">`TaskWebApp` is the MVC web application that the user interacts with.</span><span class="sxs-lookup"><span data-stu-id="00bff-137">`TaskWebApp` is the MVC web application that the user interacts with.</span></span> <span data-ttu-id="00bff-138">`TaskService` is the app's back-end web API that stores each user's to-do list.</span><span class="sxs-lookup"><span data-stu-id="00bff-138">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="00bff-139">This article will only discuss the `TaskWebApp` application.</span><span class="sxs-lookup"><span data-stu-id="00bff-139">This article will only discuss the `TaskWebApp` application.</span></span> <span data-ttu-id="00bff-140">To learn how to build `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="00bff-140">To learn how to build `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="00bff-141">Update the Azure AD B2C configuration</span><span class="sxs-lookup"><span data-stu-id="00bff-141">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="00bff-142">Our sample is configured to use the policies and client ID of our demo tenant.</span><span class="sxs-lookup"><span data-stu-id="00bff-142">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="00bff-143">If you would like to use your own tenant, you will need to open `web.config` in the `TaskWebApp` project and replace the values for</span><span class="sxs-lookup"><span data-stu-id="00bff-143">If you would like to use your own tenant, you will need to open `web.config` in the `TaskWebApp` project and replace the values for</span></span>

* <span data-ttu-id="00bff-144">`ida:Tenant` with your tenant name</span><span class="sxs-lookup"><span data-stu-id="00bff-144">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="00bff-145">`ida:ClientId` with your web app application ID</span><span class="sxs-lookup"><span data-stu-id="00bff-145">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="00bff-146">`ida:ClientSecret` with your web app secret key</span><span class="sxs-lookup"><span data-stu-id="00bff-146">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="00bff-147">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span><span class="sxs-lookup"><span data-stu-id="00bff-147">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="00bff-148">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span><span class="sxs-lookup"><span data-stu-id="00bff-148">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="00bff-149">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span><span class="sxs-lookup"><span data-stu-id="00bff-149">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="add-authentication-support"></a><span data-ttu-id="00bff-150">Add authentication support</span><span class="sxs-lookup"><span data-stu-id="00bff-150">Add authentication support</span></span>

<span data-ttu-id="00bff-151">You can now configure your app to use Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="00bff-151">You can now configure your app to use Azure AD B2C.</span></span> <span data-ttu-id="00bff-152">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span><span class="sxs-lookup"><span data-stu-id="00bff-152">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="00bff-153">The requests dictate the user experience your app wants to execute by specifying the policy.</span><span class="sxs-lookup"><span data-stu-id="00bff-153">The requests dictate the user experience your app wants to execute by specifying the policy.</span></span> <span data-ttu-id="00bff-154">You can use Microsoft's OWIN library to send these requests, execute policies, manage user sessions, and more.</span><span class="sxs-lookup"><span data-stu-id="00bff-154">You can use Microsoft's OWIN library to send these requests, execute policies, manage user sessions, and more.</span></span>

### <a name="install-owin"></a><span data-ttu-id="00bff-155">Install OWIN</span><span class="sxs-lookup"><span data-stu-id="00bff-155">Install OWIN</span></span>

<span data-ttu-id="00bff-156">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="00bff-156">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="00bff-157">Add an OWIN startup class</span><span class="sxs-lookup"><span data-stu-id="00bff-157">Add an OWIN startup class</span></span>

<span data-ttu-id="00bff-158">Add an OWIN startup class to the API called `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="00bff-158">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="00bff-159">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span><span class="sxs-lookup"><span data-stu-id="00bff-159">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="00bff-160">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span><span class="sxs-lookup"><span data-stu-id="00bff-160">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="00bff-161">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="00bff-161">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="00bff-162">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="00bff-162">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="00bff-163">After the modifications, `Startup.cs` looks like the following:</span><span class="sxs-lookup"><span data-stu-id="00bff-163">After the modifications, `Startup.cs` looks like the following:</span></span>

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

### <a name="configure-the-authentication-middleware"></a><span data-ttu-id="00bff-164">Configure the authentication middleware</span><span class="sxs-lookup"><span data-stu-id="00bff-164">Configure the authentication middleware</span></span>

<span data-ttu-id="00bff-165">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span><span class="sxs-lookup"><span data-stu-id="00bff-165">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="00bff-166">The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="00bff-166">The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD B2C.</span></span> <span data-ttu-id="00bff-167">If you do not specify certain parameters, it will use the default value.</span><span class="sxs-lookup"><span data-stu-id="00bff-167">If you do not specify certain parameters, it will use the default value.</span></span> <span data-ttu-id="00bff-168">For example, we do not specify the `ResponseType` in the sample, so the default value `code id_token` will be used in each outgoing request to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="00bff-168">For example, we do not specify the `ResponseType` in the sample, so the default value `code id_token` will be used in each outgoing request to Azure AD B2C.</span></span>

<span data-ttu-id="00bff-169">You also need to set up cookie authentication.</span><span class="sxs-lookup"><span data-stu-id="00bff-169">You also need to set up cookie authentication.</span></span> <span data-ttu-id="00bff-170">The OpenID Connect middleware uses cookies to maintain user sessions, among other things.</span><span class="sxs-lookup"><span data-stu-id="00bff-170">The OpenID Connect middleware uses cookies to maintain user sessions, among other things.</span></span>

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

<span data-ttu-id="00bff-171">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by the OpenID Connect middleware.</span><span class="sxs-lookup"><span data-stu-id="00bff-171">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by the OpenID Connect middleware.</span></span> <span data-ttu-id="00bff-172">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into the `Notifications` variable.</span><span class="sxs-lookup"><span data-stu-id="00bff-172">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into the `Notifications` variable.</span></span> <span data-ttu-id="00bff-173">In our sample, we define three different callbacks depending on the event.</span><span class="sxs-lookup"><span data-stu-id="00bff-173">In our sample, we define three different callbacks depending on the event.</span></span>

#### <a name="using-different-policies"></a><span data-ttu-id="00bff-174">Using different policies</span><span class="sxs-lookup"><span data-stu-id="00bff-174">Using different policies</span></span>

<span data-ttu-id="00bff-175">The `RedirectToIdentityProvider` notification is triggered whenever a request is made to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="00bff-175">The `RedirectToIdentityProvider` notification is triggered whenever a request is made to Azure AD B2C.</span></span> <span data-ttu-id="00bff-176">In the callback function `OnRedirectToIdentityProvider`, we check in the outgoing call if we want to use a different policy.</span><span class="sxs-lookup"><span data-stu-id="00bff-176">In the callback function `OnRedirectToIdentityProvider`, we check in the outgoing call if we want to use a different policy.</span></span> <span data-ttu-id="00bff-177">In order to do a password reset or edit a profile, you need to use the corresponding policy such as the password reset policy instead of the default "Sign-up or Sign-in" policy.</span><span class="sxs-lookup"><span data-stu-id="00bff-177">In order to do a password reset or edit a profile, you need to use the corresponding policy such as the password reset policy instead of the default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="00bff-178">In our sample, when a user wants to reset the password or edit the profile, we add the policy we prefer to use into the OWIN context.</span><span class="sxs-lookup"><span data-stu-id="00bff-178">In our sample, when a user wants to reset the password or edit the profile, we add the policy we prefer to use into the OWIN context.</span></span> <span data-ttu-id="00bff-179">That can be done by doing the following:</span><span class="sxs-lookup"><span data-stu-id="00bff-179">That can be done by doing the following:</span></span>

```CSharp
    // Let the middleware know you are trying to use the edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="00bff-180">And you can implement the callback function `OnRedirectToIdentityProvider` by doing the following:</span><span class="sxs-lookup"><span data-stu-id="00bff-180">And you can implement the callback function `OnRedirectToIdentityProvider` by doing the following:</span></span>

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

#### <a name="handling-authorization-codes"></a><span data-ttu-id="00bff-181">Handling authorization codes</span><span class="sxs-lookup"><span data-stu-id="00bff-181">Handling authorization codes</span></span>

<span data-ttu-id="00bff-182">The `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span><span class="sxs-lookup"><span data-stu-id="00bff-182">The `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="00bff-183">The OpenID Connect middleware does not support exchanging codes for access tokens.</span><span class="sxs-lookup"><span data-stu-id="00bff-183">The OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="00bff-184">You can manually exchange the code for the token in a callback function.</span><span class="sxs-lookup"><span data-stu-id="00bff-184">You can manually exchange the code for the token in a callback function.</span></span> <span data-ttu-id="00bff-185">For more information, please look at the [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span><span class="sxs-lookup"><span data-stu-id="00bff-185">For more information, please look at the [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

#### <a name="handling-errors"></a><span data-ttu-id="00bff-186">Handling errors</span><span class="sxs-lookup"><span data-stu-id="00bff-186">Handling errors</span></span>

<span data-ttu-id="00bff-187">The `AuthenticationFailed` notification is triggered when authentication fails.</span><span class="sxs-lookup"><span data-stu-id="00bff-187">The `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="00bff-188">In its callback method, you can handle the errors as you wish.</span><span class="sxs-lookup"><span data-stu-id="00bff-188">In its callback method, you can handle the errors as you wish.</span></span> <span data-ttu-id="00bff-189">You should however add a check for the error code `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="00bff-189">You should however add a check for the error code `AADB2C90118`.</span></span> <span data-ttu-id="00bff-190">During the execution of the "Sign-up or Sign-in" policy, the user has the opportunity to click on a **Forgot your password?** link.</span><span class="sxs-lookup"><span data-stu-id="00bff-190">During the execution of the "Sign-up or Sign-in" policy, the user has the opportunity to click on a **Forgot your password?** link.</span></span> <span data-ttu-id="00bff-191">In this event, Azure AD B2C will send your app that error code indicating that your app should make a request using the password reset policy instead.</span><span class="sxs-lookup"><span data-stu-id="00bff-191">In this event, Azure AD B2C will send your app that error code indicating that your app should make a request using the password reset policy instead.</span></span>

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

## <a name="send-authentication-requests-to-azure-ad"></a><span data-ttu-id="00bff-192">Send authentication requests to Azure AD</span><span class="sxs-lookup"><span data-stu-id="00bff-192">Send authentication requests to Azure AD</span></span>

<span data-ttu-id="00bff-193">Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol.</span><span class="sxs-lookup"><span data-stu-id="00bff-193">Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="00bff-194">OWIN has taken care of all of the details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span><span class="sxs-lookup"><span data-stu-id="00bff-194">OWIN has taken care of all of the details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="00bff-195">All that remains is to initiate each user's flow.</span><span class="sxs-lookup"><span data-stu-id="00bff-195">All that remains is to initiate each user's flow.</span></span>

<span data-ttu-id="00bff-196">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in the web app, the associated action is invoked in `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="00bff-196">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in the web app, the associated action is invoked in `Controllers\AccountController.cs`:</span></span>

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

<span data-ttu-id="00bff-197">You can also use OWIN to sign out the user from the app.</span><span class="sxs-lookup"><span data-stu-id="00bff-197">You can also use OWIN to sign out the user from the app.</span></span> <span data-ttu-id="00bff-198">In `Controllers\AccountController.cs` we have:</span><span class="sxs-lookup"><span data-stu-id="00bff-198">In `Controllers\AccountController.cs` we have:</span></span>

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

<span data-ttu-id="00bff-199">In addition to explicitly invoking a policy, you can use an `[Authorize]` tag in your controllers that will execute a policy if the user is not signed in.</span><span class="sxs-lookup"><span data-stu-id="00bff-199">In addition to explicitly invoking a policy, you can use an `[Authorize]` tag in your controllers that will execute a policy if the user is not signed in.</span></span> <span data-ttu-id="00bff-200">Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.</span><span class="sxs-lookup"><span data-stu-id="00bff-200">Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.</span></span>  <span data-ttu-id="00bff-201">OWIN will select the last policy configured when the `[Authorize]` tag is hit.</span><span class="sxs-lookup"><span data-stu-id="00bff-201">OWIN will select the last policy configured when the `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use the Authorize decorator to execute a certain policy if the user is not already signed into the app.
[Authorize]
public ActionResult Claims()
{
  ...
```

## <a name="display-user-information"></a><span data-ttu-id="00bff-202">Display user information</span><span class="sxs-lookup"><span data-stu-id="00bff-202">Display user information</span></span>

<span data-ttu-id="00bff-203">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token to the app that contains **claims**.</span><span class="sxs-lookup"><span data-stu-id="00bff-203">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token to the app that contains **claims**.</span></span> <span data-ttu-id="00bff-204">These are assertions about the user.</span><span class="sxs-lookup"><span data-stu-id="00bff-204">These are assertions about the user.</span></span> <span data-ttu-id="00bff-205">You can use claims to personalize your app.</span><span class="sxs-lookup"><span data-stu-id="00bff-205">You can use claims to personalize your app.</span></span>

<span data-ttu-id="00bff-206">Open the `Controllers\HomeController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="00bff-206">Open the `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="00bff-207">You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span><span class="sxs-lookup"><span data-stu-id="00bff-207">You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

<span data-ttu-id="00bff-208">You can access any claim that your application receives in the same way.</span><span class="sxs-lookup"><span data-stu-id="00bff-208">You can access any claim that your application receives in the same way.</span></span>  <span data-ttu-id="00bff-209">A list of all the claims the app receives is available for you on the **Claims** page.</span><span class="sxs-lookup"><span data-stu-id="00bff-209">A list of all the claims the app receives is available for you on the **Claims** page.</span></span>

## <a name="run-the-sample-app"></a><span data-ttu-id="00bff-210">Run the sample app</span><span class="sxs-lookup"><span data-stu-id="00bff-210">Run the sample app</span></span>

<span data-ttu-id="00bff-211">Finally, you can build and run your app.</span><span class="sxs-lookup"><span data-stu-id="00bff-211">Finally, you can build and run your app.</span></span> <span data-ttu-id="00bff-212">Sign up for the app by using an email address or user name.</span><span class="sxs-lookup"><span data-stu-id="00bff-212">Sign up for the app by using an email address or user name.</span></span> <span data-ttu-id="00bff-213">Sign out and sign back in as the same user.</span><span class="sxs-lookup"><span data-stu-id="00bff-213">Sign out and sign back in as the same user.</span></span> <span data-ttu-id="00bff-214">Edit the profile or reset the password.</span><span class="sxs-lookup"><span data-stu-id="00bff-214">Edit the profile or reset the password.</span></span> <span data-ttu-id="00bff-215">Sign out and sign up as a different user.</span><span class="sxs-lookup"><span data-stu-id="00bff-215">Sign out and sign up as a different user.</span></span> <span data-ttu-id="00bff-216">Note that the information displayed on the **Claims** tab corresponds to the information that you configured on your policies.</span><span class="sxs-lookup"><span data-stu-id="00bff-216">Note that the information displayed on the **Claims** tab corresponds to the information that you configured on your policies.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="00bff-217">Add social IDPs</span><span class="sxs-lookup"><span data-stu-id="00bff-217">Add social IDPs</span></span>

<span data-ttu-id="00bff-218">Currently, the app supports only user sign-up and sign-in by using **local accounts**.</span><span class="sxs-lookup"><span data-stu-id="00bff-218">Currently, the app supports only user sign-up and sign-in by using **local accounts**.</span></span> <span data-ttu-id="00bff-219">These are accounts stored in your B2C directory that use a user name and password.</span><span class="sxs-lookup"><span data-stu-id="00bff-219">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="00bff-220">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span><span class="sxs-lookup"><span data-stu-id="00bff-220">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="00bff-221">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span><span class="sxs-lookup"><span data-stu-id="00bff-221">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="00bff-222">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span><span class="sxs-lookup"><span data-stu-id="00bff-222">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="00bff-223">Set up Facebook as an IDP</span><span class="sxs-lookup"><span data-stu-id="00bff-223">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="00bff-224">Set up Google as an IDP</span><span class="sxs-lookup"><span data-stu-id="00bff-224">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="00bff-225">Set up Amazon as an IDP</span><span class="sxs-lookup"><span data-stu-id="00bff-225">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="00bff-226">Set up LinkedIn as an IDP</span><span class="sxs-lookup"><span data-stu-id="00bff-226">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="00bff-227">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="00bff-227">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="00bff-228">After you save your policies, run the app again.</span><span class="sxs-lookup"><span data-stu-id="00bff-228">After you save your policies, run the app again.</span></span>  <span data-ttu-id="00bff-229">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span><span class="sxs-lookup"><span data-stu-id="00bff-229">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="00bff-230">You can experiment with your policies and observe the effect on your sample app.</span><span class="sxs-lookup"><span data-stu-id="00bff-230">You can experiment with your policies and observe the effect on your sample app.</span></span> <span data-ttu-id="00bff-231">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span><span class="sxs-lookup"><span data-stu-id="00bff-231">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="00bff-232">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span><span class="sxs-lookup"><span data-stu-id="00bff-232">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>
