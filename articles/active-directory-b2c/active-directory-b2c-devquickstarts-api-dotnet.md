---
title: Azure AD B2C | Microsoft Docs
description: How to build a .NET Web API by using Azure Active Directory B2C, secured using OAuth 2.0 access tokens for authentication.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: ''
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d67043f2e0a062796f4d6167b28774ce494027c2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552308"
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="b71ce-103">Azure Active Directory B2C: Build a .NET web API</span><span class="sxs-lookup"><span data-stu-id="b71ce-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="b71ce-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span><span class="sxs-lookup"><span data-stu-id="b71ce-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="b71ce-105">These tokens allow your client apps to authenticate to the API.</span><span class="sxs-lookup"><span data-stu-id="b71ce-105">These tokens allow your client apps to authenticate to the API.</span></span> <span data-ttu-id="b71ce-106">This article shows you how to create a .NET MVC "to-do list" API that allows users of your client application to CRUD tasks.</span><span class="sxs-lookup"><span data-stu-id="b71ce-106">This article shows you how to create a .NET MVC "to-do list" API that allows users of your client application to CRUD tasks.</span></span> <span data-ttu-id="b71ce-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span><span class="sxs-lookup"><span data-stu-id="b71ce-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="b71ce-108">Create an Azure AD B2C directory</span><span class="sxs-lookup"><span data-stu-id="b71ce-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="b71ce-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span><span class="sxs-lookup"><span data-stu-id="b71ce-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="b71ce-110">A directory is a container for all of your users, apps, groups, and more.</span><span class="sxs-lookup"><span data-stu-id="b71ce-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="b71ce-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span><span class="sxs-lookup"><span data-stu-id="b71ce-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="b71ce-112">The client application and web API must use the same Azure AD B2C directory.</span><span class="sxs-lookup"><span data-stu-id="b71ce-112">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="b71ce-113">Create a web API</span><span class="sxs-lookup"><span data-stu-id="b71ce-113">Create a web API</span></span>

<span data-ttu-id="b71ce-114">Next, you need to create a web API app in your B2C directory.</span><span class="sxs-lookup"><span data-stu-id="b71ce-114">Next, you need to create a web API app in your B2C directory.</span></span> <span data-ttu-id="b71ce-115">This gives Azure AD information that it needs to securely communicate with your app.</span><span class="sxs-lookup"><span data-stu-id="b71ce-115">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="b71ce-116">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="b71ce-116">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="b71ce-117">Be sure to:</span><span class="sxs-lookup"><span data-stu-id="b71ce-117">Be sure to:</span></span>

* <span data-ttu-id="b71ce-118">Include a **web app** or **web API** in the application.</span><span class="sxs-lookup"><span data-stu-id="b71ce-118">Include a **web app** or **web API** in the application.</span></span>
* <span data-ttu-id="b71ce-119">Use the **Redirect URI** `https://localhost:44332/` for the web app.</span><span class="sxs-lookup"><span data-stu-id="b71ce-119">Use the **Redirect URI** `https://localhost:44332/` for the web app.</span></span> <span data-ttu-id="b71ce-120">This is the default location of the web app client for this code sample.</span><span class="sxs-lookup"><span data-stu-id="b71ce-120">This is the default location of the web app client for this code sample.</span></span>
* <span data-ttu-id="b71ce-121">Copy the **Application ID** that is assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="b71ce-121">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="b71ce-122">You'll need it later.</span><span class="sxs-lookup"><span data-stu-id="b71ce-122">You'll need it later.</span></span>
* <span data-ttu-id="b71ce-123">Enter an app identifier into **App ID URI**.</span><span class="sxs-lookup"><span data-stu-id="b71ce-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="b71ce-124">Add permissions through the **Published scopes** menu.</span><span class="sxs-lookup"><span data-stu-id="b71ce-124">Add permissions through the **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="b71ce-125">Create your policies</span><span class="sxs-lookup"><span data-stu-id="b71ce-125">Create your policies</span></span>

<span data-ttu-id="b71ce-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b71ce-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="b71ce-127">You will need to create a policy to communicate with Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b71ce-127">You will need to create a policy to communicate with Azure AD B2C.</span></span> <span data-ttu-id="b71ce-128">We recommend using the combined sign-up/sign-in policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b71ce-128">We recommend using the combined sign-up/sign-in policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="b71ce-129">When you create your policy, be sure to:</span><span class="sxs-lookup"><span data-stu-id="b71ce-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="b71ce-130">Choose **Display name** and other sign-up attributes in your policy.</span><span class="sxs-lookup"><span data-stu-id="b71ce-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="b71ce-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span><span class="sxs-lookup"><span data-stu-id="b71ce-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="b71ce-132">You can choose other claims as well.</span><span class="sxs-lookup"><span data-stu-id="b71ce-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="b71ce-133">Copy the **Name** of each policy after you create it.</span><span class="sxs-lookup"><span data-stu-id="b71ce-133">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="b71ce-134">You'll need the policy name later.</span><span class="sxs-lookup"><span data-stu-id="b71ce-134">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="b71ce-135">After you have successfully created the policy, you're ready to build your app.</span><span class="sxs-lookup"><span data-stu-id="b71ce-135">After you have successfully created the policy, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="b71ce-136">Download the code</span><span class="sxs-lookup"><span data-stu-id="b71ce-136">Download the code</span></span>

<span data-ttu-id="b71ce-137">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="b71ce-137">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="b71ce-138">You can clone the sample by running:</span><span class="sxs-lookup"><span data-stu-id="b71ce-138">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="b71ce-139">After you download the sample code, open the Visual Studio .sln file to get started.</span><span class="sxs-lookup"><span data-stu-id="b71ce-139">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="b71ce-140">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="b71ce-140">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="b71ce-141">`TaskWebApp` is an MVC web application that the user interacts with.</span><span class="sxs-lookup"><span data-stu-id="b71ce-141">`TaskWebApp` is an MVC web application that the user interacts with.</span></span> <span data-ttu-id="b71ce-142">`TaskService` is the app's back-end web API that stores each user's to-do list.</span><span class="sxs-lookup"><span data-stu-id="b71ce-142">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="b71ce-143">This article will only discuss the `TaskService` application.</span><span class="sxs-lookup"><span data-stu-id="b71ce-143">This article will only discuss the `TaskService` application.</span></span> <span data-ttu-id="b71ce-144">To learn how to build `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="b71ce-144">To learn how to build `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="b71ce-145">Update the Azure AD B2C configuration</span><span class="sxs-lookup"><span data-stu-id="b71ce-145">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="b71ce-146">Our sample is configured to use the policies and client ID of our demo tenant.</span><span class="sxs-lookup"><span data-stu-id="b71ce-146">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="b71ce-147">If you would like to use your own tenant, you will need to do the following:</span><span class="sxs-lookup"><span data-stu-id="b71ce-147">If you would like to use your own tenant, you will need to do the following:</span></span>

1. <span data-ttu-id="b71ce-148">Open `web.config` in the `TaskService` project and replace the values for</span><span class="sxs-lookup"><span data-stu-id="b71ce-148">Open `web.config` in the `TaskService` project and replace the values for</span></span>
    * <span data-ttu-id="b71ce-149">`ida:Tenant` with your tenant name</span><span class="sxs-lookup"><span data-stu-id="b71ce-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="b71ce-150">`ida:ClientId` with your web API application ID</span><span class="sxs-lookup"><span data-stu-id="b71ce-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="b71ce-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span><span class="sxs-lookup"><span data-stu-id="b71ce-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="b71ce-152">Open `web.config` in the `TaskWebApp` project and replace the values for</span><span class="sxs-lookup"><span data-stu-id="b71ce-152">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>
    * <span data-ttu-id="b71ce-153">`ida:Tenant` with your tenant name</span><span class="sxs-lookup"><span data-stu-id="b71ce-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="b71ce-154">`ida:ClientId` with your web app application ID</span><span class="sxs-lookup"><span data-stu-id="b71ce-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="b71ce-155">`ida:ClientSecret` with your web app secret key</span><span class="sxs-lookup"><span data-stu-id="b71ce-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="b71ce-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span><span class="sxs-lookup"><span data-stu-id="b71ce-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="b71ce-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span><span class="sxs-lookup"><span data-stu-id="b71ce-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="b71ce-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span><span class="sxs-lookup"><span data-stu-id="b71ce-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-the-api"></a><span data-ttu-id="b71ce-159">Secure the API</span><span class="sxs-lookup"><span data-stu-id="b71ce-159">Secure the API</span></span>

<span data-ttu-id="b71ce-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span><span class="sxs-lookup"><span data-stu-id="b71ce-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="b71ce-161">This ensures that each request to your API will only be valid if the request has a bearer token.</span><span class="sxs-lookup"><span data-stu-id="b71ce-161">This ensures that each request to your API will only be valid if the request has a bearer token.</span></span> <span data-ttu-id="b71ce-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span><span class="sxs-lookup"><span data-stu-id="b71ce-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="b71ce-163">Install OWIN</span><span class="sxs-lookup"><span data-stu-id="b71ce-163">Install OWIN</span></span>

<span data-ttu-id="b71ce-164">Begin by installing the OWIN OAuth authentication pipeline by using the Visual Studio Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="b71ce-164">Begin by installing the OWIN OAuth authentication pipeline by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="b71ce-165">This will install the OWIN middleware that will accept and validate bearer tokens.</span><span class="sxs-lookup"><span data-stu-id="b71ce-165">This will install the OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="b71ce-166">Add an OWIN startup class</span><span class="sxs-lookup"><span data-stu-id="b71ce-166">Add an OWIN startup class</span></span>

<span data-ttu-id="b71ce-167">Add an OWIN startup class to the API called `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="b71ce-167">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="b71ce-168">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span><span class="sxs-lookup"><span data-stu-id="b71ce-168">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="b71ce-169">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span><span class="sxs-lookup"><span data-stu-id="b71ce-169">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="b71ce-170">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="b71ce-170">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="b71ce-171">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="b71ce-171">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="b71ce-172">After the modifications, `Startup.cs` looks like the following:</span><span class="sxs-lookup"><span data-stu-id="b71ce-172">After the modifications, `Startup.cs` looks like the following:</span></span>

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

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="b71ce-173">Configure OAuth 2.0 authentication</span><span class="sxs-lookup"><span data-stu-id="b71ce-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="b71ce-174">Open the file `App_Start\Startup.Auth.cs`, and implement the `ConfigureAuth(...)` method.</span><span class="sxs-lookup"><span data-stu-id="b71ce-174">Open the file `App_Start\Startup.Auth.cs`, and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="b71ce-175">For example, it could look like the following:</span><span class="sxs-lookup"><span data-stu-id="b71ce-175">For example, it could look like the following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure the authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where the audience of the token is equal to the client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches the Azure AD B2C metadata & signing keys from the OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-the-task-controller"></a><span data-ttu-id="b71ce-176">Secure the task controller</span><span class="sxs-lookup"><span data-stu-id="b71ce-176">Secure the task controller</span></span>

<span data-ttu-id="b71ce-177">After the app is configured to use OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag to the task controller.</span><span class="sxs-lookup"><span data-stu-id="b71ce-177">After the app is configured to use OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag to the task controller.</span></span> <span data-ttu-id="b71ce-178">This is the controller where all to-do list manipulation takes place, so you should secure the entire controller at the class level.</span><span class="sxs-lookup"><span data-stu-id="b71ce-178">This is the controller where all to-do list manipulation takes place, so you should secure the entire controller at the class level.</span></span> <span data-ttu-id="b71ce-179">You can also add the `[Authorize]` tag to individual actions for more fine-grained control.</span><span class="sxs-lookup"><span data-stu-id="b71ce-179">You can also add the `[Authorize]` tag to individual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-the-token"></a><span data-ttu-id="b71ce-180">Get user information from the token</span><span class="sxs-lookup"><span data-stu-id="b71ce-180">Get user information from the token</span></span>

<span data-ttu-id="b71ce-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" the task.</span><span class="sxs-lookup"><span data-stu-id="b71ce-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" the task.</span></span> <span data-ttu-id="b71ce-182">The owner is identified by the user's **object ID**.</span><span class="sxs-lookup"><span data-stu-id="b71ce-182">The owner is identified by the user's **object ID**.</span></span> <span data-ttu-id="b71ce-183">(This is why you needed to add the object ID as an application claim in all of your policies.)</span><span class="sxs-lookup"><span data-stu-id="b71ce-183">(This is why you needed to add the object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-the-permissions-in-the-token"></a><span data-ttu-id="b71ce-184">Validate the permissions in the token</span><span class="sxs-lookup"><span data-stu-id="b71ce-184">Validate the permissions in the token</span></span>

<span data-ttu-id="b71ce-185">A common requirement for web APIs is to validate the "scopes" present in the token.</span><span class="sxs-lookup"><span data-stu-id="b71ce-185">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="b71ce-186">This ensures that the user has consented to the permissions required to access the to-do list service.</span><span class="sxs-lookup"><span data-stu-id="b71ce-186">This ensures that the user has consented to the permissions required to access the to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "The Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="b71ce-187">Run the sample app</span><span class="sxs-lookup"><span data-stu-id="b71ce-187">Run the sample app</span></span>

<span data-ttu-id="b71ce-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="b71ce-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="b71ce-189">Create some tasks on the user's to-do list and notice how they are persisted in the API even after you stop and restart the client.</span><span class="sxs-lookup"><span data-stu-id="b71ce-189">Create some tasks on the user's to-do list and notice how they are persisted in the API even after you stop and restart the client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="b71ce-190">Edit your policies</span><span class="sxs-lookup"><span data-stu-id="b71ce-190">Edit your policies</span></span>

<span data-ttu-id="b71ce-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view the effects (or lack thereof) on the API.</span><span class="sxs-lookup"><span data-stu-id="b71ce-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view the effects (or lack thereof) on the API.</span></span> <span data-ttu-id="b71ce-192">You can manipulate the application claims in the policies and change the user information that is available in the web API.</span><span class="sxs-lookup"><span data-stu-id="b71ce-192">You can manipulate the application claims in the policies and change the user information that is available in the web API.</span></span> <span data-ttu-id="b71ce-193">Any claims that you add will be available to your .NET MVC web API in the `ClaimsPrincipal` object, as described earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="b71ce-193">Any claims that you add will be available to your .NET MVC web API in the `ClaimsPrincipal` object, as described earlier in this article.</span></span>
