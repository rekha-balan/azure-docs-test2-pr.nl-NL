---
title: Add sign-in to a .NET MVC web API using the Azure AD v2.0 endpoint | Microsoft Docs
description: How to build a .NET MVC Web Api that accepts tokens from both personal Microsoft Account and work or school accounts.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: d063ea881c82b158a196cb5f63e7514777732846
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556673"
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="a5fab-103">Secure an MVC web API</span><span class="sxs-lookup"><span data-stu-id="a5fab-103">Secure an MVC web API</span></span>
<span data-ttu-id="a5fab-104">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span><span class="sxs-lookup"><span data-stu-id="a5fab-104">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="a5fab-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="a5fab-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="a5fab-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a5fab-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="a5fab-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="a5fab-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="a5fab-108">Here we’ll use OWIN to build a "To Do List" MVC Web API that allows clients to create and read tasks from a user's To-Do list.</span><span class="sxs-lookup"><span data-stu-id="a5fab-108">Here we’ll use OWIN to build a "To Do List" MVC Web API that allows clients to create and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="a5fab-109">The web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span><span class="sxs-lookup"><span data-stu-id="a5fab-109">The web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="a5fab-110">This sample was built using Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="a5fab-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="a5fab-111">Download</span><span class="sxs-lookup"><span data-stu-id="a5fab-111">Download</span></span>
<span data-ttu-id="a5fab-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="a5fab-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="a5fab-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span><span class="sxs-lookup"><span data-stu-id="a5fab-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="a5fab-114">The skeleton app includes all the boilerplate code for a simple API, but is missing all of the identity-related pieces.</span><span class="sxs-lookup"><span data-stu-id="a5fab-114">The skeleton app includes all the boilerplate code for a simple API, but is missing all of the identity-related pieces.</span></span> <span data-ttu-id="a5fab-115">If you don't want to follow along, you can instead clone or [download the completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a5fab-115">If you don't want to follow along, you can instead clone or [download the completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="a5fab-116">Register an app</span><span class="sxs-lookup"><span data-stu-id="a5fab-116">Register an app</span></span>
<span data-ttu-id="a5fab-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a5fab-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="a5fab-118">Make sure to:</span><span class="sxs-lookup"><span data-stu-id="a5fab-118">Make sure to:</span></span>

* <span data-ttu-id="a5fab-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span><span class="sxs-lookup"><span data-stu-id="a5fab-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>

<span data-ttu-id="a5fab-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span><span class="sxs-lookup"><span data-stu-id="a5fab-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="a5fab-121">The TodoListClient is used to demonstrate how a user signs-in and how a client can issue requests to your Web API.</span><span class="sxs-lookup"><span data-stu-id="a5fab-121">The TodoListClient is used to demonstrate how a user signs-in and how a client can issue requests to your Web API.</span></span>  <span data-ttu-id="a5fab-122">In this case, both the TodoListClient and the TodoListService are represented by the same app.</span><span class="sxs-lookup"><span data-stu-id="a5fab-122">In this case, both the TodoListClient and the TodoListService are represented by the same app.</span></span>  <span data-ttu-id="a5fab-123">To configure the TodoListClient, you should also:</span><span class="sxs-lookup"><span data-stu-id="a5fab-123">To configure the TodoListClient, you should also:</span></span>

* <span data-ttu-id="a5fab-124">Add the **Mobile** platform for your app.</span><span class="sxs-lookup"><span data-stu-id="a5fab-124">Add the **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="a5fab-125">Install OWIN</span><span class="sxs-lookup"><span data-stu-id="a5fab-125">Install OWIN</span></span>
<span data-ttu-id="a5fab-126">Now that you’ve registered an app, you need to set up your app to communicate with the v2.0 endpoint in order to validate incoming requests & tokens.</span><span class="sxs-lookup"><span data-stu-id="a5fab-126">Now that you’ve registered an app, you need to set up your app to communicate with the v2.0 endpoint in order to validate incoming requests & tokens.</span></span>

* <span data-ttu-id="a5fab-127">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project using the Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="a5fab-127">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="a5fab-128">Configure OAuth authentication</span><span class="sxs-lookup"><span data-stu-id="a5fab-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="a5fab-129">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="a5fab-129">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="a5fab-130">Right click on the project --> **Add** --> **New Item** --> Search for “OWIN”.</span><span class="sxs-lookup"><span data-stu-id="a5fab-130">Right click on the project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="a5fab-131">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span><span class="sxs-lookup"><span data-stu-id="a5fab-131">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="a5fab-132">Change the class declaration to `public partial class Startup` - we’ve already implemented part of this class for you in another file.</span><span class="sxs-lookup"><span data-stu-id="a5fab-132">Change the class declaration to `public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="a5fab-133">In the `Configuration(…)` method, make a call to ConfgureAuth(…) to set up authentication for your web app.</span><span class="sxs-lookup"><span data-stu-id="a5fab-133">In the `Configuration(…)` method, make a call to ConfgureAuth(…) to set up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="a5fab-134">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method, which will set up the Web API to accept tokens from the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="a5fab-134">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method, which will set up the Web API to accept tokens from the v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, the TodoListClient and TodoListService
                // are represented using the same Application Id - we use
                // the Application Id to represent the audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that the user's organization (if applicable) has
                // signed up for the app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up the OWIN pipeline to use OAuth 2.0 Bearer authentication.
        // The options provided here tell the middleware about the type of tokens
        // that will be recieved, which are JWTs for the v2.0 endpoint.

        // NOTE: The usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by the v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used to fetch & use the OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="a5fab-135">Now you can use `[Authorize]` attributes to protect your controllers and actions with OAuth 2.0 bearer authentication.</span><span class="sxs-lookup"><span data-stu-id="a5fab-135">Now you can use `[Authorize]` attributes to protect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="a5fab-136">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span><span class="sxs-lookup"><span data-stu-id="a5fab-136">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="a5fab-137">This will force the user to sign in before accessing that page.</span><span class="sxs-lookup"><span data-stu-id="a5fab-137">This will force the user to sign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="a5fab-138">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span><span class="sxs-lookup"><span data-stu-id="a5fab-138">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span>  <span data-ttu-id="a5fab-139">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span><span class="sxs-lookup"><span data-stu-id="a5fab-139">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use the ClaimsPrincipal to access information about the
    // user making the call.  In this case, we use the 'sub' or
    // NameIdentifier claim to serve as a key for the tasks in the data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="a5fab-140">Finally, open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="a5fab-140">Finally, open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="a5fab-141">Your `ida:Audience` is the **Application Id** of the app that you entered in the portal.</span><span class="sxs-lookup"><span data-stu-id="a5fab-141">Your `ida:Audience` is the **Application Id** of the app that you entered in the portal.</span></span>

## <a name="configure-the-client-app"></a><span data-ttu-id="a5fab-142">Configure the client app</span><span class="sxs-lookup"><span data-stu-id="a5fab-142">Configure the client app</span></span>
<span data-ttu-id="a5fab-143">Before you can see the Todo List Service in action, you need to configure the Todo List Client so it can get tokens from the v2.0 endpoint and make calls to the service.</span><span class="sxs-lookup"><span data-stu-id="a5fab-143">Before you can see the Todo List Service in action, you need to configure the Todo List Client so it can get tokens from the v2.0 endpoint and make calls to the service.</span></span>

* <span data-ttu-id="a5fab-144">In the TodoListClient project, open `App.config` and enter your configuration values in the `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="a5fab-144">In the TodoListClient project, open `App.config` and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="a5fab-145">Your `ida:ClientId` Application Id you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="a5fab-145">Your `ida:ClientId` Application Id you copied from the portal.</span></span>

<span data-ttu-id="a5fab-146">Finally, clean, build and run each project!</span><span class="sxs-lookup"><span data-stu-id="a5fab-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="a5fab-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span><span class="sxs-lookup"><span data-stu-id="a5fab-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="a5fab-148">Sign into the TodoListClient, and call your web api to add tasks to the user's To-Do list.</span><span class="sxs-lookup"><span data-stu-id="a5fab-148">Sign into the TodoListClient, and call your web api to add tasks to the user's To-Do list.</span></span>

<span data-ttu-id="a5fab-149">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span><span class="sxs-lookup"><span data-stu-id="a5fab-149">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="a5fab-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="a5fab-150">Next steps</span></span>
<span data-ttu-id="a5fab-151">You can now move onto additional topics.</span><span class="sxs-lookup"><span data-stu-id="a5fab-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="a5fab-152">You may want to try:</span><span class="sxs-lookup"><span data-stu-id="a5fab-152">You may want to try:</span></span>

[<span data-ttu-id="a5fab-153">Calling a Web API from a Web App >></span><span class="sxs-lookup"><span data-stu-id="a5fab-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="a5fab-154">For additional resources, check out:</span><span class="sxs-lookup"><span data-stu-id="a5fab-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="a5fab-155">The v2.0 developer guide >></span><span class="sxs-lookup"><span data-stu-id="a5fab-155">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="a5fab-156">StackOverflow "azure-active-directory" tag >></span><span class="sxs-lookup"><span data-stu-id="a5fab-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="a5fab-157">Get security updates for our products</span><span class="sxs-lookup"><span data-stu-id="a5fab-157">Get security updates for our products</span></span>
<span data-ttu-id="a5fab-158">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="a5fab-158">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
