---
title: Azure Active Directory B2C | Microsoft Docs
description: How to build a web application that has sign-in, sign-up, and profile management by using Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: 0b1c6ede-de0a-4c32-92b3-5c813dc26804
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: ae8995f8a5eb16de11043aa40e3f66ea73291799
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551774"
---
# <a name="azure-ad-b2c-build-a-net-web-app"></a><span data-ttu-id="3b4c9-103">Azure AD B2C: Build a .NET web app</span><span class="sxs-lookup"><span data-stu-id="3b4c9-103">Azure AD B2C: Build a .NET web app</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="3b4c9-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your web app in a few short steps.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your web app in a few short steps.</span></span> <span data-ttu-id="3b4c9-105">This article will discuss how to create a .NET Model-View-Controller (MVC) web app that includes user sign-up, sign-in, and profile management.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-105">This article will discuss how to create a .NET Model-View-Controller (MVC) web app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="3b4c9-106">The app will include support for sign-up and sign-in by using a user name or email, and by using social accounts such as Facebook and Google.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-106">The app will include support for sign-up and sign-in by using a user name or email, and by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="3b4c9-107">Get an Azure AD B2C directory</span><span class="sxs-lookup"><span data-stu-id="3b4c9-107">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="3b4c9-108">Before you can use Azure AD B2C, you must create a directory, or tenant.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-108">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="3b4c9-109">A directory is a container for all of your users, apps, groups, and more.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-109">A directory is a container for all of your users, apps, groups, and more.</span></span>  <span data-ttu-id="3b4c9-110">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-110">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="3b4c9-111">Create an application</span><span class="sxs-lookup"><span data-stu-id="3b4c9-111">Create an application</span></span>
<span data-ttu-id="3b4c9-112">Next, you need to create an app in your B2C directory.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-112">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="3b4c9-113">This gives Azure AD information that it needs to securely communicate with your app.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-113">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="3b4c9-114">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="3b4c9-114">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="3b4c9-115">Be sure to:</span><span class="sxs-lookup"><span data-stu-id="3b4c9-115">Be sure to:</span></span>

* <span data-ttu-id="3b4c9-116">Include a **web app/web API** in the application.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-116">Include a **web app/web API** in the application.</span></span>
* <span data-ttu-id="3b4c9-117">Enter `https://localhost:44316/` as a **Redirect URI**.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-117">Enter `https://localhost:44316/` as a **Redirect URI**.</span></span> <span data-ttu-id="3b4c9-118">It is the default URL for this code sample.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-118">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="3b4c9-119">Copy down the **Application ID** that is assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-119">Copy down the **Application ID** that is assigned to your app.</span></span>  <span data-ttu-id="3b4c9-120">You will need it later.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-120">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="3b4c9-121">Create your policies</span><span class="sxs-lookup"><span data-stu-id="3b4c9-121">Create your policies</span></span>
<span data-ttu-id="3b4c9-122">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3b4c9-122">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="3b4c9-123">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-123">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="3b4c9-124">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="3b4c9-124">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>

> [!NOTE]
> <span data-ttu-id="3b4c9-125">Azure AD B2C also supports a combined sign up or sign in policy which is not featured in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-125">Azure AD B2C also supports a combined sign up or sign in policy which is not featured in this tutorial.</span></span>  <span data-ttu-id="3b4c9-126">The sign up or sign in policy is shown in [this equivalent tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="3b4c9-126">The sign up or sign in policy is shown in [this equivalent tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>
>
>

<span data-ttu-id="3b4c9-127">When you create the three policies, be sure to:</span><span class="sxs-lookup"><span data-stu-id="3b4c9-127">When you create the three policies, be sure to:</span></span>

* <span data-ttu-id="3b4c9-128">Choose **User ID sign-up** or **Email sign-up** in the identity providers blade.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-128">Choose **User ID sign-up** or **Email sign-up** in the identity providers blade.</span></span>
* <span data-ttu-id="3b4c9-129">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-129">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="3b4c9-130">Choose the **Display name** claim as an application claim in every policy.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-130">Choose the **Display name** claim as an application claim in every policy.</span></span> <span data-ttu-id="3b4c9-131">You can choose other claims as well.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-131">You can choose other claims as well.</span></span>
* <span data-ttu-id="3b4c9-132">Copy the **Name** of each policy after you create it.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-132">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="3b4c9-133">You'll need those policy names later.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-133">You'll need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="3b4c9-134">After you create your three policies, you're ready to build your app.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-134">After you create your three policies, you're ready to build your app.</span></span>  

## <a name="download-the-code-and-configure-authentication"></a><span data-ttu-id="3b4c9-135">Download the code and configure authentication</span><span class="sxs-lookup"><span data-stu-id="3b4c9-135">Download the code and configure authentication</span></span>
<span data-ttu-id="3b4c9-136">The code for this sample [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="3b4c9-136">The code for this sample [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIdConnect-DotNet).</span></span> <span data-ttu-id="3b4c9-137">To build the sample as you go, you can [download the skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="3b4c9-137">To build the sample as you go, you can [download the skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="3b4c9-138">You can also clone the skeleton:</span><span class="sxs-lookup"><span data-stu-id="3b4c9-138">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIdConnect-DotNet.git
```

<span data-ttu-id="3b4c9-139">The completed sample is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIdConnect-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-139">The completed sample is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIdConnect-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

<span data-ttu-id="3b4c9-140">After you download the sample code, open the Visual Studio .sln file to get started.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-140">After you download the sample code, open the Visual Studio .sln file to get started.</span></span>

<span data-ttu-id="3b4c9-141">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-141">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span></span> <span data-ttu-id="3b4c9-142">For .NET web applications, you can use Microsoft's OWIN middleware to send OpenID Connect authentication requests, execute policies, manage user sessions, and more.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-142">For .NET web applications, you can use Microsoft's OWIN middleware to send OpenID Connect authentication requests, execute policies, manage user sessions, and more.</span></span>

<span data-ttu-id="3b4c9-143">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-143">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

<span data-ttu-id="3b4c9-144">Next, open the `web.config` file in the root of the project and enter your app's configuration values in the `<appSettings>` section, replacing the existing values.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-144">Next, open the `web.config` file in the root of the project and enter your app's configuration values in the `<appSettings>` section, replacing the existing values.</span></span>

```
<configuration>
  <appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="ida:Tenant" value="fabrikamb2c.onmicrosoft.com" />
    <add key="ida:ClientId" value="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6" />
    <add key="ida:AadInstance" value="https://login.microsoftonline.com/{0}/v2.0/.well-known/openid-configuration?p={1}" />
    <add key="ida:RedirectUri" value="https://localhost:44316/" />
    <add key="ida:SignUpPolicyId" value="b2c_1_sign_up" />
    <add key="ida:SignInPolicyId" value="b2c_1_sign_in" />
    <add key="ida:UserProfilePolicyId" value="b2c_1_edit_profile" />
  </appSettings>
...
```

[!INCLUDE [active-directory-b2c-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="3b4c9-145">Next, add an OWIN startup class to the project called `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-145">Next, add an OWIN startup class to the project called `Startup.cs`.</span></span> <span data-ttu-id="3b4c9-146">Right-click on the project, select **Add** and **New Item**, and then Search for "OWIN."</span><span class="sxs-lookup"><span data-stu-id="3b4c9-146">Right-click on the project, select **Add** and **New Item**, and then Search for "OWIN."</span></span> <span data-ttu-id="3b4c9-147">**Make sure to change the class declaration to `public partial class Startup`**.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-147">**Make sure to change the class declaration to `public partial class Startup`**.</span></span> <span data-ttu-id="3b4c9-148">We implemented part of this class for you in another file.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-148">We implemented part of this class for you in another file.</span></span> <span data-ttu-id="3b4c9-149">The OWIN middleware will invoke the `Configuration(...)` method when your app starts.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-149">The OWIN middleware will invoke the `Configuration(...)` method when your app starts.</span></span> <span data-ttu-id="3b4c9-150">In this method, make a call to `ConfigureAuth(...)`, where you set up authentication for your app.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-150">In this method, make a call to `ConfigureAuth(...)`, where you set up authentication for your app.</span></span>

```C#
// Startup.cs

public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

<span data-ttu-id="3b4c9-151">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-151">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="3b4c9-152">The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-152">The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD.</span></span> <span data-ttu-id="3b4c9-153">You also need to set up cookie authentication.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-153">You also need to set up cookie authentication.</span></span> <span data-ttu-id="3b4c9-154">The OpenID Connect middleware uses cookies to maintain user sessions, among other things.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-154">The OpenID Connect middleware uses cookies to maintain user sessions, among other things.</span></span>

```C#
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // App config settings
    private static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
    private static string aadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
    private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];
    private static string redirectUri = ConfigurationManager.AppSettings["ida:RedirectUri"];

    // B2C policy identifiers
    public static string SignUpPolicyId = ConfigurationManager.AppSettings["ida:SignUpPolicyId"];
    public static string SignInPolicyId = ConfigurationManager.AppSettings["ida:SignInPolicyId"];
    public static string ProfilePolicyId = ConfigurationManager.AppSettings["ida:UserProfilePolicyId"];

    public void ConfigureAuth(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());

        // Configure OpenID Connect middleware for each policy
        app.UseOpenIdConnectAuthentication(CreateOptionsFromPolicy(SignUpPolicyId));
        app.UseOpenIdConnectAuthentication(CreateOptionsFromPolicy(ProfilePolicyId));
        app.UseOpenIdConnectAuthentication(CreateOptionsFromPolicy(SignInPolicyId));
    }

    // Used for avoiding yellow-screen-of-death
    private Task AuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
    {
        notification.HandleResponse();
        if (notification.Exception.Message == "access_denied")
        {
            notification.Response.Redirect("/");
        }
        else
        {
            notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
        }

        return Task.FromResult(0);
    }

    private OpenIdConnectAuthenticationOptions CreateOptionsFromPolicy(string policy)
    {
        return new OpenIdConnectAuthenticationOptions
        {
            // For each policy, give OWIN the policy-specific metadata address, and
            // set the authentication type to the id of the policy
            MetadataAddress = String.Format(aadInstance, tenant, policy),
            AuthenticationType = policy,

            // These are standard OpenID Connect parameters, with values pulled from web.config
            ClientId = clientId,
            RedirectUri = redirectUri,
            PostLogoutRedirectUri = redirectUri,
            Notifications = new OpenIdConnectAuthenticationNotifications
            {
                AuthenticationFailed = AuthenticationFailed,
            },
            Scope = "openid",
            ResponseType = "id_token",

            // This piece is optional - it is used for displaying the user's name in the navigation bar.
            TokenValidationParameters = new TokenValidationParameters
            {
                NameClaimType = "name",
            },
        };
    }
}
```

## <a name="send-authentication-requests-to-azure-ad"></a><span data-ttu-id="3b4c9-155">Send authentication requests to Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b4c9-155">Send authentication requests to Azure AD</span></span>
<span data-ttu-id="3b4c9-156">Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-156">Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="3b4c9-157">OWIN has taken care of all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-157">OWIN has taken care of all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="3b4c9-158">All that remains is to initiate each user's flow.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-158">All that remains is to initiate each user's flow.</span></span>

<span data-ttu-id="3b4c9-159">When a user selects **Sign up**, **Sign in**, or **Edit profile** in the web app, the associated action is invoked in `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-159">When a user selects **Sign up**, **Sign in**, or **Edit profile** in the web app, the associated action is invoked in `Controllers\AccountController.cs`.</span></span> <span data-ttu-id="3b4c9-160">In each case, you can use built-in OWIN methods to trigger the right policy:</span><span class="sxs-lookup"><span data-stu-id="3b4c9-160">In each case, you can use built-in OWIN methods to trigger the right policy:</span></span>

```C#
// Controllers\AccountController.cs

public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        // To execute a policy, you simply need to trigger an OWIN challenge.
        // You can indicate which policy to use by specifying the policy id as the AuthenticationType
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties () { RedirectUri = "/" }, Startup.SignInPolicyId);
    }
}

public void SignUp()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties() { RedirectUri = "/" }, Startup.SignUpPolicyId);
    }
}


public void Profile()
{
    if (Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties() { RedirectUri = "/" }, Startup.ProfilePolicyId);
    }
}
```

<span data-ttu-id="3b4c9-161">You can also use an `[Authorize]` tag in your controllers that requires the execution of a certain policy if the user is not signed in.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-161">You can also use an `[Authorize]` tag in your controllers that requires the execution of a certain policy if the user is not signed in.</span></span> <span data-ttu-id="3b4c9-162">Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-162">Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.</span></span>  <span data-ttu-id="3b4c9-163">OWIN will select the last policy configured to execute when the Authorize tag is invoked.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-163">OWIN will select the last policy configured to execute when the Authorize tag is invoked.</span></span>

```C#
// Controllers\HomeController.cs

// You can use the Authorize decorator to execute a policy if the user is not already signed in the app.
[Authorize]
public ActionResult Claims()
{
  ...
```

<span data-ttu-id="3b4c9-164">You can also use OWIN to sign out the user from the app.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-164">You can also use OWIN to sign out the user from the app.</span></span> <span data-ttu-id="3b4c9-165">In `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="3b4c9-165">In `Controllers\AccountController.cs`:</span></span>  

```C#
// Controllers\AccountController.cs

public void SignOut()
{
    // To sign out the user, you should issue an OpenIDConnect sign out request
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

## <a name="display-user-information"></a><span data-ttu-id="3b4c9-166">Display user information</span><span class="sxs-lookup"><span data-stu-id="3b4c9-166">Display user information</span></span>
<span data-ttu-id="3b4c9-167">When you authenticate users by using OpenID Connect, Azure AD returns an ID token to the app that contains **claims**.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-167">When you authenticate users by using OpenID Connect, Azure AD returns an ID token to the app that contains **claims**.</span></span> <span data-ttu-id="3b4c9-168">These are assertions about the user.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-168">These are assertions about the user.</span></span> <span data-ttu-id="3b4c9-169">You can use claims to personalize your app.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-169">You can use claims to personalize your app.</span></span>  

<span data-ttu-id="3b4c9-170">Open the `Controllers\HomeController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-170">Open the `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="3b4c9-171">You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-171">You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

```C#
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

<span data-ttu-id="3b4c9-172">You can access any claim that your application receives in the same way.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-172">You can access any claim that your application receives in the same way.</span></span>  <span data-ttu-id="3b4c9-173">A list of all the claims the app receives is available for you on the **Claims** page.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-173">A list of all the claims the app receives is available for you on the **Claims** page.</span></span>

## <a name="run-the-sample-app"></a><span data-ttu-id="3b4c9-174">Run the sample app</span><span class="sxs-lookup"><span data-stu-id="3b4c9-174">Run the sample app</span></span>
<span data-ttu-id="3b4c9-175">Finally, you can build and run your app.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-175">Finally, you can build and run your app.</span></span> <span data-ttu-id="3b4c9-176">Sign up for the app by using an email address or user name.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-176">Sign up for the app by using an email address or user name.</span></span> <span data-ttu-id="3b4c9-177">Sign out and sign back in as the same user.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-177">Sign out and sign back in as the same user.</span></span> <span data-ttu-id="3b4c9-178">Edit that user's profile.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-178">Edit that user's profile.</span></span> <span data-ttu-id="3b4c9-179">Sign out and sign up as a different user.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-179">Sign out and sign up as a different user.</span></span> <span data-ttu-id="3b4c9-180">Note that the information displayed on the **Claims** tab corresponds to the information that you configured on your policies.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-180">Note that the information displayed on the **Claims** tab corresponds to the information that you configured on your policies.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="3b4c9-181">Add social IDPs</span><span class="sxs-lookup"><span data-stu-id="3b4c9-181">Add social IDPs</span></span>
<span data-ttu-id="3b4c9-182">Currently, the app supports only user sign-up and sign-in by using **local accounts**.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-182">Currently, the app supports only user sign-up and sign-in by using **local accounts**.</span></span> <span data-ttu-id="3b4c9-183">These are accounts stored in your B2C directory that use a user name and password.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-183">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="3b4c9-184">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-184">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="3b4c9-185">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-185">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="3b4c9-186">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-186">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="3b4c9-187">Set up Facebook as an IDP</span><span class="sxs-lookup"><span data-stu-id="3b4c9-187">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="3b4c9-188">Set up Google as an IDP</span><span class="sxs-lookup"><span data-stu-id="3b4c9-188">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="3b4c9-189">Set up Amazon as an IDP</span><span class="sxs-lookup"><span data-stu-id="3b4c9-189">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="3b4c9-190">Set up LinkedIn as an IDP</span><span class="sxs-lookup"><span data-stu-id="3b4c9-190">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="3b4c9-191">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3b4c9-191">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="3b4c9-192">After you save your policies, run the app again.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-192">After you save your policies, run the app again.</span></span>  <span data-ttu-id="3b4c9-193">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-193">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="3b4c9-194">You can experiment with your policies and observe the effect on your sample app.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-194">You can experiment with your policies and observe the effect on your sample app.</span></span> <span data-ttu-id="3b4c9-195">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-195">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="3b4c9-196">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span><span class="sxs-lookup"><span data-stu-id="3b4c9-196">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

<span data-ttu-id="3b4c9-197">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="3b4c9-197">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="3b4c9-198">You can also clone it from GitHub:</span><span class="sxs-lookup"><span data-stu-id="3b4c9-198">You can also clone it from GitHub:</span></span>

```
git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIdConnect-DotNet.git
```

<!--

## Next steps

You can now move on to more advanced B2C topics. You might try:

[Call a web API from a web app]()

[Customize the UX for a B2C app]()

-->
