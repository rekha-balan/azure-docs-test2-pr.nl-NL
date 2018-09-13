---
title: Azure AD .NET web app Getting Started | Microsoft Docs
description: Build a .NET MVC web app that integrates with Azure AD for sign-in.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.openlocfilehash: 43ba592b6294a9a75a20dacd81953a77c241b89f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551470"
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="6c14e-103">ASP.NET web app sign-in and sign-out with Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c14e-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="6c14e-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span><span class="sxs-lookup"><span data-stu-id="6c14e-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="6c14e-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span><span class="sxs-lookup"><span data-stu-id="6c14e-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="6c14e-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="6c14e-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="6c14e-107">This article shows how to use OWIN to:</span><span class="sxs-lookup"><span data-stu-id="6c14e-107">This article shows how to use OWIN to:</span></span>

* <span data-ttu-id="6c14e-108">Sign users in to web apps by using Azure AD as the identity provider.</span><span class="sxs-lookup"><span data-stu-id="6c14e-108">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="6c14e-109">Display some user information.</span><span class="sxs-lookup"><span data-stu-id="6c14e-109">Display some user information.</span></span>
* <span data-ttu-id="6c14e-110">Sign users out of the apps.</span><span class="sxs-lookup"><span data-stu-id="6c14e-110">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="6c14e-111">Before you get started</span><span class="sxs-lookup"><span data-stu-id="6c14e-111">Before you get started</span></span>
* <span data-ttu-id="6c14e-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="6c14e-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="6c14e-113">You also need an Azure AD tenant in which to register the app.</span><span class="sxs-lookup"><span data-stu-id="6c14e-113">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="6c14e-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="6c14e-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="6c14e-115">When you are ready, follow the procedures in the next four sections.</span><span class="sxs-lookup"><span data-stu-id="6c14e-115">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="6c14e-116">Step 1: Register the new app with Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c14e-116">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="6c14e-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span><span class="sxs-lookup"><span data-stu-id="6c14e-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="6c14e-118">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6c14e-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6c14e-119">On the top bar, click your account name.</span><span class="sxs-lookup"><span data-stu-id="6c14e-119">On the top bar, click your account name.</span></span> <span data-ttu-id="6c14e-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span><span class="sxs-lookup"><span data-stu-id="6c14e-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="6c14e-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6c14e-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="6c14e-122">Click **App registrations**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="6c14e-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="6c14e-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="6c14e-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="6c14e-124">**Name** describes the app to users.</span><span class="sxs-lookup"><span data-stu-id="6c14e-124">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="6c14e-125">**Sign-On URL** is the base URL of the app.</span><span class="sxs-lookup"><span data-stu-id="6c14e-125">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="6c14e-126">The skeleton's default URL is https://localhost:44320/.</span><span class="sxs-lookup"><span data-stu-id="6c14e-126">The skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="6c14e-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span><span class="sxs-lookup"><span data-stu-id="6c14e-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="6c14e-128">Copy the value from the app page to use in the next sections.</span><span class="sxs-lookup"><span data-stu-id="6c14e-128">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="6c14e-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span><span class="sxs-lookup"><span data-stu-id="6c14e-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="6c14e-130">The **App ID URI** is a unique identifier for the app.</span><span class="sxs-lookup"><span data-stu-id="6c14e-130">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="6c14e-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="6c14e-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="6c14e-132">Step 2: Set up the app to use the OWIN authentication pipeline</span><span class="sxs-lookup"><span data-stu-id="6c14e-132">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="6c14e-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span><span class="sxs-lookup"><span data-stu-id="6c14e-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="6c14e-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span><span class="sxs-lookup"><span data-stu-id="6c14e-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="6c14e-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="6c14e-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="6c14e-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="6c14e-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="6c14e-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span><span class="sxs-lookup"><span data-stu-id="6c14e-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span></span>
3. <span data-ttu-id="6c14e-138">Change the class declaration to `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="6c14e-138">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="6c14e-139">We've already implemented part of this class for you in another file.</span><span class="sxs-lookup"><span data-stu-id="6c14e-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="6c14e-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span><span class="sxs-lookup"><span data-stu-id="6c14e-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="6c14e-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span><span class="sxs-lookup"><span data-stu-id="6c14e-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="6c14e-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c14e-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span></span> <span data-ttu-id="6c14e-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span><span class="sxs-lookup"><span data-stu-id="6c14e-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span></span>

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
             });
     }
     ```

5. <span data-ttu-id="6c14e-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="6c14e-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="6c14e-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span><span class="sxs-lookup"><span data-stu-id="6c14e-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span></span>
  * <span data-ttu-id="6c14e-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="6c14e-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="6c14e-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span><span class="sxs-lookup"><span data-stu-id="6c14e-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="6c14e-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c14e-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="6c14e-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span><span class="sxs-lookup"><span data-stu-id="6c14e-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="6c14e-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span><span class="sxs-lookup"><span data-stu-id="6c14e-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="6c14e-151">All that remains is to give your users a way to sign in and sign out.</span><span class="sxs-lookup"><span data-stu-id="6c14e-151">All that remains is to give your users a way to sign in and sign out.</span></span>

1. <span data-ttu-id="6c14e-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span><span class="sxs-lookup"><span data-stu-id="6c14e-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span></span> <span data-ttu-id="6c14e-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span><span class="sxs-lookup"><span data-stu-id="6c14e-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="6c14e-154">You can also use OWIN to directly issue authentication requests from within your code.</span><span class="sxs-lookup"><span data-stu-id="6c14e-154">You can also use OWIN to directly issue authentication requests from within your code.</span></span> <span data-ttu-id="6c14e-155">To do so, open Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="6c14e-155">To do so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="6c14e-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span><span class="sxs-lookup"><span data-stu-id="6c14e-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. <span data-ttu-id="6c14e-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span><span class="sxs-lookup"><span data-stu-id="6c14e-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span></span>

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
             </li>
             <li>
                 @Html.ActionLink("Sign out", "SignOut", "Account")
             </li>
         </ul>
     </text>
    }
    else
    {
     <ul class="nav navbar-nav navbar-right">
         <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
     </ul>
    }
    ```

## <a name="step-4-display-user-information"></a><span data-ttu-id="6c14e-158">Step 4: Display user information</span><span class="sxs-lookup"><span data-stu-id="6c14e-158">Step 4: Display user information</span></span>
<span data-ttu-id="6c14e-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span><span class="sxs-lookup"><span data-stu-id="6c14e-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span></span> <span data-ttu-id="6c14e-160">You can use these claims to personalize the app by doing the following:</span><span class="sxs-lookup"><span data-stu-id="6c14e-160">You can use these claims to personalize the app by doing the following:</span></span>

1. <span data-ttu-id="6c14e-161">Open the Controllers\HomeController.cs file.</span><span class="sxs-lookup"><span data-stu-id="6c14e-161">Open the Controllers\HomeController.cs file.</span></span> <span data-ttu-id="6c14e-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span><span class="sxs-lookup"><span data-stu-id="6c14e-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. <span data-ttu-id="6c14e-163">Build and run the app.</span><span class="sxs-lookup"><span data-stu-id="6c14e-163">Build and run the app.</span></span> <span data-ttu-id="6c14e-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span><span class="sxs-lookup"><span data-stu-id="6c14e-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span></span> <span data-ttu-id="6c14e-165">Here's how:</span><span class="sxs-lookup"><span data-stu-id="6c14e-165">Here's how:</span></span>

  <span data-ttu-id="6c14e-166">a.</span><span class="sxs-lookup"><span data-stu-id="6c14e-166">a.</span></span> <span data-ttu-id="6c14e-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span><span class="sxs-lookup"><span data-stu-id="6c14e-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span></span>

  <span data-ttu-id="6c14e-168">b.</span><span class="sxs-lookup"><span data-stu-id="6c14e-168">b.</span></span> <span data-ttu-id="6c14e-169">Sign out, and then sign back in as another user in your tenant.</span><span class="sxs-lookup"><span data-stu-id="6c14e-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="6c14e-170">c.</span><span class="sxs-lookup"><span data-stu-id="6c14e-170">c.</span></span> <span data-ttu-id="6c14e-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span><span class="sxs-lookup"><span data-stu-id="6c14e-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c14e-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c14e-172">Next steps</span></span>
<span data-ttu-id="6c14e-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span><span class="sxs-lookup"><span data-stu-id="6c14e-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="6c14e-174">You can now move on to more advanced topics.</span><span class="sxs-lookup"><span data-stu-id="6c14e-174">You can now move on to more advanced topics.</span></span> <span data-ttu-id="6c14e-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6c14e-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
