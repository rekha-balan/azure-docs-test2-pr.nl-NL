---
title: Tutorial - Grant access to an ASP.NET Core web API from a single-page app using Azure Active Directory B2C | Microsoft Docs
description: Tutorial on how to use Active Directory B2C to protect an .NET Core web api and call it from a single page app.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.author: davidmu
ms.date: 3/02/2018
ms.custom: mvc
ms.topic: tutorial
ms.service: active-directory
ms.component: B2C
ms.openlocfilehash: 54ddafbf0e4fe02bfc1445aad23ac3e20b42acb0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869258"
---
# <a name="tutorial-grant-access-to-an-aspnet-core-web-api-from-a-single-page-app-using-azure-active-directory-b2c"></a><span data-ttu-id="7a10b-103">Tutorial: Grant access to an ASP.NET Core web API from a single-page app using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="7a10b-103">Tutorial: Grant access to an ASP.NET Core web API from a single-page app using Azure Active Directory B2C</span></span>

<span data-ttu-id="7a10b-104">This tutorial shows you how to call an Azure Active Directory (Azure AD) B2C protected ASP.NET Core web API resource from a single page app.</span><span class="sxs-lookup"><span data-stu-id="7a10b-104">This tutorial shows you how to call an Azure Active Directory (Azure AD) B2C protected ASP.NET Core web API resource from a single page app.</span></span>

<span data-ttu-id="7a10b-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="7a10b-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a10b-106">Register a web API in your Azure AD B2C tenant</span><span class="sxs-lookup"><span data-stu-id="7a10b-106">Register a web API in your Azure AD B2C tenant</span></span>
> * <span data-ttu-id="7a10b-107">Define and configure scopes for a web API</span><span class="sxs-lookup"><span data-stu-id="7a10b-107">Define and configure scopes for a web API</span></span>
> * <span data-ttu-id="7a10b-108">Grant app permissions to the web API</span><span class="sxs-lookup"><span data-stu-id="7a10b-108">Grant app permissions to the web API</span></span>
> * <span data-ttu-id="7a10b-109">Update sample code to use Azure AD B2C to protect a web API</span><span class="sxs-lookup"><span data-stu-id="7a10b-109">Update sample code to use Azure AD B2C to protect a web API</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="7a10b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a10b-110">Prerequisites</span></span>

* <span data-ttu-id="7a10b-111">Complete the [Authenticate users with Azure Active Directory B2C in a single page application tutorial](active-directory-b2c-tutorials-spa.md).</span><span class="sxs-lookup"><span data-stu-id="7a10b-111">Complete the [Authenticate users with Azure Active Directory B2C in a single page application tutorial](active-directory-b2c-tutorials-spa.md).</span></span>
* <span data-ttu-id="7a10b-112">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span><span class="sxs-lookup"><span data-stu-id="7a10b-112">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span></span>
* <span data-ttu-id="7a10b-113">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later</span><span class="sxs-lookup"><span data-stu-id="7a10b-113">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later</span></span>
* <span data-ttu-id="7a10b-114">Install [Node.js](https://nodejs.org/en/download/)</span><span class="sxs-lookup"><span data-stu-id="7a10b-114">Install [Node.js](https://nodejs.org/en/download/)</span></span>

## <a name="register-web-api"></a><span data-ttu-id="7a10b-115">Register web API</span><span class="sxs-lookup"><span data-stu-id="7a10b-115">Register web API</span></span>

<span data-ttu-id="7a10b-116">Web API resources need to be registered in your tenant before they can accept and respond to [protected resource requests](../active-directory/develop/developer-glossary.md#resource-server) by [client applications](../active-directory/develop/developer-glossary.md#client-application) that present an [access token](../active-directory/develop/developer-glossary.md#access-token) from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a10b-116">Web API resources need to be registered in your tenant before they can accept and respond to [protected resource requests](../active-directory/develop/developer-glossary.md#resource-server) by [client applications](../active-directory/develop/developer-glossary.md#client-application) that present an [access token](../active-directory/develop/developer-glossary.md#access-token) from Azure Active Directory.</span></span> <span data-ttu-id="7a10b-117">Registration establishes the [application and service principal object](../active-directory/develop/developer-glossary.md#application-object) in your tenant.</span><span class="sxs-lookup"><span data-stu-id="7a10b-117">Registration establishes the [application and service principal object](../active-directory/develop/developer-glossary.md#application-object) in your tenant.</span></span> 

<span data-ttu-id="7a10b-118">Log in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="7a10b-118">Log in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

1. <span data-ttu-id="7a10b-119">Select **Azure AD B2C** from the services list in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7a10b-119">Select **Azure AD B2C** from the services list in the Azure portal.</span></span>

2. <span data-ttu-id="7a10b-120">In the B2C settings, click **Applications** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="7a10b-120">In the B2C settings, click **Applications** and then click **Add**.</span></span>

    <span data-ttu-id="7a10b-121">To register the sample web API in your tenant, use the following settings.</span><span class="sxs-lookup"><span data-stu-id="7a10b-121">To register the sample web API in your tenant, use the following settings.</span></span>
    
    ![Add a new API](media/active-directory-b2c-tutorials-spa-webapi/web-api-registration.png)
    
    | <span data-ttu-id="7a10b-123">Setting</span><span class="sxs-lookup"><span data-stu-id="7a10b-123">Setting</span></span>      | <span data-ttu-id="7a10b-124">Suggested value</span><span class="sxs-lookup"><span data-stu-id="7a10b-124">Suggested value</span></span>  | <span data-ttu-id="7a10b-125">Description</span><span class="sxs-lookup"><span data-stu-id="7a10b-125">Description</span></span>                                        |
    | ------------ | ------- | -------------------------------------------------- |
    | <span data-ttu-id="7a10b-126">**Name**</span><span class="sxs-lookup"><span data-stu-id="7a10b-126">**Name**</span></span> | <span data-ttu-id="7a10b-127">Hello Core API</span><span class="sxs-lookup"><span data-stu-id="7a10b-127">Hello Core API</span></span> | <span data-ttu-id="7a10b-128">Enter a **Name** that describes your web API to developers.</span><span class="sxs-lookup"><span data-stu-id="7a10b-128">Enter a **Name** that describes your web API to developers.</span></span> |
    | <span data-ttu-id="7a10b-129">**Include web app / web API**</span><span class="sxs-lookup"><span data-stu-id="7a10b-129">**Include web app / web API**</span></span> | <span data-ttu-id="7a10b-130">Yes</span><span class="sxs-lookup"><span data-stu-id="7a10b-130">Yes</span></span> | <span data-ttu-id="7a10b-131">Select **Yes** for a web API.</span><span class="sxs-lookup"><span data-stu-id="7a10b-131">Select **Yes** for a web API.</span></span> |
    | <span data-ttu-id="7a10b-132">**Allow implicit flow**</span><span class="sxs-lookup"><span data-stu-id="7a10b-132">**Allow implicit flow**</span></span> | <span data-ttu-id="7a10b-133">Yes</span><span class="sxs-lookup"><span data-stu-id="7a10b-133">Yes</span></span> | <span data-ttu-id="7a10b-134">Select **Yes** since the API uses [OpenID Connect sign-in](active-directory-b2c-reference-oidc.md).</span><span class="sxs-lookup"><span data-stu-id="7a10b-134">Select **Yes** since the API uses [OpenID Connect sign-in](active-directory-b2c-reference-oidc.md).</span></span> |
    | <span data-ttu-id="7a10b-135">**Reply URL**</span><span class="sxs-lookup"><span data-stu-id="7a10b-135">**Reply URL**</span></span> | `http://localhost:44332` | <span data-ttu-id="7a10b-136">Reply URLs are endpoints where Azure AD B2C returns any tokens that your API requests.</span><span class="sxs-lookup"><span data-stu-id="7a10b-136">Reply URLs are endpoints where Azure AD B2C returns any tokens that your API requests.</span></span> <span data-ttu-id="7a10b-137">In this tutorial, the sample web API runs locally (localhost) and listens on port 5000.</span><span class="sxs-lookup"><span data-stu-id="7a10b-137">In this tutorial, the sample web API runs locally (localhost) and listens on port 5000.</span></span> |
    | <span data-ttu-id="7a10b-138">**App ID URI**</span><span class="sxs-lookup"><span data-stu-id="7a10b-138">**App ID URI**</span></span> | <span data-ttu-id="7a10b-139">HelloCoreAPI</span><span class="sxs-lookup"><span data-stu-id="7a10b-139">HelloCoreAPI</span></span> | <span data-ttu-id="7a10b-140">The URI uniquely identifies the API in the tenant.</span><span class="sxs-lookup"><span data-stu-id="7a10b-140">The URI uniquely identifies the API in the tenant.</span></span> <span data-ttu-id="7a10b-141">This allows you to register multiple APIs per tenant.</span><span class="sxs-lookup"><span data-stu-id="7a10b-141">This allows you to register multiple APIs per tenant.</span></span> <span data-ttu-id="7a10b-142">[Scopes](../active-directory/develop/developer-glossary.md#scopes) govern access to the protected API resource and are defined per App ID URI.</span><span class="sxs-lookup"><span data-stu-id="7a10b-142">[Scopes](../active-directory/develop/developer-glossary.md#scopes) govern access to the protected API resource and are defined per App ID URI.</span></span> |
    | <span data-ttu-id="7a10b-143">**Native client**</span><span class="sxs-lookup"><span data-stu-id="7a10b-143">**Native client**</span></span> | <span data-ttu-id="7a10b-144">No</span><span class="sxs-lookup"><span data-stu-id="7a10b-144">No</span></span> | <span data-ttu-id="7a10b-145">Since this is a web API and not a native client, select No.</span><span class="sxs-lookup"><span data-stu-id="7a10b-145">Since this is a web API and not a native client, select No.</span></span> |
    
3. <span data-ttu-id="7a10b-146">Click **Create** to register your API.</span><span class="sxs-lookup"><span data-stu-id="7a10b-146">Click **Create** to register your API.</span></span>

<span data-ttu-id="7a10b-147">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="7a10b-147">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span></span> <span data-ttu-id="7a10b-148">Select your web API from the list.</span><span class="sxs-lookup"><span data-stu-id="7a10b-148">Select your web API from the list.</span></span> <span data-ttu-id="7a10b-149">The web API's property pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="7a10b-149">The web API's property pane is displayed.</span></span>

![Web API properties](./media/active-directory-b2c-tutorials-spa-webapi/b2c-web-api-properties.png)

<span data-ttu-id="7a10b-151">Make note of the **Application Client ID**.</span><span class="sxs-lookup"><span data-stu-id="7a10b-151">Make note of the **Application Client ID**.</span></span> <span data-ttu-id="7a10b-152">The ID uniquely identifies the API and is needed when configuring the API later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="7a10b-152">The ID uniquely identifies the API and is needed when configuring the API later in the tutorial.</span></span>

<span data-ttu-id="7a10b-153">Registering your web API with Azure AD B2C defines a trust relationship.</span><span class="sxs-lookup"><span data-stu-id="7a10b-153">Registering your web API with Azure AD B2C defines a trust relationship.</span></span> <span data-ttu-id="7a10b-154">Since the API is registered with B2C, the API can now trust the B2C access tokens it receives from other applications.</span><span class="sxs-lookup"><span data-stu-id="7a10b-154">Since the API is registered with B2C, the API can now trust the B2C access tokens it receives from other applications.</span></span>

## <a name="define-and-configure-scopes"></a><span data-ttu-id="7a10b-155">Define and configure scopes</span><span class="sxs-lookup"><span data-stu-id="7a10b-155">Define and configure scopes</span></span>

<span data-ttu-id="7a10b-156">[Scopes](../active-directory/develop/developer-glossary.md#scopes) provide a way to govern access to protected resources.</span><span class="sxs-lookup"><span data-stu-id="7a10b-156">[Scopes](../active-directory/develop/developer-glossary.md#scopes) provide a way to govern access to protected resources.</span></span> <span data-ttu-id="7a10b-157">Scopes are used by the web API to implement scope-based access control.</span><span class="sxs-lookup"><span data-stu-id="7a10b-157">Scopes are used by the web API to implement scope-based access control.</span></span> <span data-ttu-id="7a10b-158">For example, some users could have both read and write access, whereas other users might have read-only permissions.</span><span class="sxs-lookup"><span data-stu-id="7a10b-158">For example, some users could have both read and write access, whereas other users might have read-only permissions.</span></span> <span data-ttu-id="7a10b-159">In this tutorial, you define read permissions for the web API.</span><span class="sxs-lookup"><span data-stu-id="7a10b-159">In this tutorial, you define read permissions for the web API.</span></span>

### <a name="define-scopes-for-the-web-api"></a><span data-ttu-id="7a10b-160">Define scopes for the web API</span><span class="sxs-lookup"><span data-stu-id="7a10b-160">Define scopes for the web API</span></span>

<span data-ttu-id="7a10b-161">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="7a10b-161">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span></span> <span data-ttu-id="7a10b-162">Select your web API from the list.</span><span class="sxs-lookup"><span data-stu-id="7a10b-162">Select your web API from the list.</span></span> <span data-ttu-id="7a10b-163">The web API's property pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="7a10b-163">The web API's property pane is displayed.</span></span>

<span data-ttu-id="7a10b-164">Click **Published scopes (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="7a10b-164">Click **Published scopes (Preview)**.</span></span>

<span data-ttu-id="7a10b-165">To configure scopes for the API, add the following entries.</span><span class="sxs-lookup"><span data-stu-id="7a10b-165">To configure scopes for the API, add the following entries.</span></span> 

![scopes defined in web api](media/active-directory-b2c-tutorials-spa-webapi/scopes-web-api.png)

| <span data-ttu-id="7a10b-167">Setting</span><span class="sxs-lookup"><span data-stu-id="7a10b-167">Setting</span></span>      | <span data-ttu-id="7a10b-168">Suggested value</span><span class="sxs-lookup"><span data-stu-id="7a10b-168">Suggested value</span></span>  | <span data-ttu-id="7a10b-169">Description</span><span class="sxs-lookup"><span data-stu-id="7a10b-169">Description</span></span>                                        |
| ------------ | ------- | -------------------------------------------------- |
| <span data-ttu-id="7a10b-170">**Scope**</span><span class="sxs-lookup"><span data-stu-id="7a10b-170">**Scope**</span></span> | <span data-ttu-id="7a10b-171">demo.read</span><span class="sxs-lookup"><span data-stu-id="7a10b-171">demo.read</span></span> | <span data-ttu-id="7a10b-172">Read access to demo API</span><span class="sxs-lookup"><span data-stu-id="7a10b-172">Read access to demo API</span></span> |

<span data-ttu-id="7a10b-173">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7a10b-173">Click **Save**.</span></span>

<span data-ttu-id="7a10b-174">The published scopes can be used to grant a client app permission to the web API.</span><span class="sxs-lookup"><span data-stu-id="7a10b-174">The published scopes can be used to grant a client app permission to the web API.</span></span>

### <a name="grant-app-permissions-to-web-api"></a><span data-ttu-id="7a10b-175">Grant app permissions to web API</span><span class="sxs-lookup"><span data-stu-id="7a10b-175">Grant app permissions to web API</span></span>

<span data-ttu-id="7a10b-176">To call a protected web API from an app, you need to grant your app permissions to the API.</span><span class="sxs-lookup"><span data-stu-id="7a10b-176">To call a protected web API from an app, you need to grant your app permissions to the API.</span></span> <span data-ttu-id="7a10b-177">In this tutorial, use the single page app created in [Authenticate users with Azure Active Directory B2C in a single page application (JavaScript)](active-directory-b2c-tutorials-spa.md).</span><span class="sxs-lookup"><span data-stu-id="7a10b-177">In this tutorial, use the single page app created in [Authenticate users with Azure Active Directory B2C in a single page application (JavaScript)](active-directory-b2c-tutorials-spa.md).</span></span>

1. <span data-ttu-id="7a10b-178">In the Azure portal, select **Azure AD B2C** from the services list and click **Applications** to view the registered app list.</span><span class="sxs-lookup"><span data-stu-id="7a10b-178">In the Azure portal, select **Azure AD B2C** from the services list and click **Applications** to view the registered app list.</span></span>

2. <span data-ttu-id="7a10b-179">Select **My sample single page app** from the app list and click **API access (Preview)** then **Add**.</span><span class="sxs-lookup"><span data-stu-id="7a10b-179">Select **My sample single page app** from the app list and click **API access (Preview)** then **Add**.</span></span>

3. <span data-ttu-id="7a10b-180">In the **Select API** dropdown, select your registered web API **Hello Core API**.</span><span class="sxs-lookup"><span data-stu-id="7a10b-180">In the **Select API** dropdown, select your registered web API **Hello Core API**.</span></span>

4. <span data-ttu-id="7a10b-181">In the **Select Scopes** dropdown, select the scopes you defined in the web API registration.</span><span class="sxs-lookup"><span data-stu-id="7a10b-181">In the **Select Scopes** dropdown, select the scopes you defined in the web API registration.</span></span>

    ![selecting scopes for app](media/active-directory-b2c-tutorials-spa-webapi/selecting-scopes-for-app.png)

5. <span data-ttu-id="7a10b-183">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a10b-183">Click **OK**.</span></span>

<span data-ttu-id="7a10b-184">Your **My sample single page app** is registered to call the protected **Hello Core API**.</span><span class="sxs-lookup"><span data-stu-id="7a10b-184">Your **My sample single page app** is registered to call the protected **Hello Core API**.</span></span> <span data-ttu-id="7a10b-185">A user [authenticates](../active-directory/develop/developer-glossary.md#authentication) with Azure AD B2C to use the WPF deskop app app.</span><span class="sxs-lookup"><span data-stu-id="7a10b-185">A user [authenticates](../active-directory/develop/developer-glossary.md#authentication) with Azure AD B2C to use the WPF deskop app app.</span></span> <span data-ttu-id="7a10b-186">The desktop app obtains an [authorization grant](../active-directory/develop/developer-glossary.md#authorization-grant) from Azure AD B2C to access the protected web API.</span><span class="sxs-lookup"><span data-stu-id="7a10b-186">The desktop app obtains an [authorization grant](../active-directory/develop/developer-glossary.md#authorization-grant) from Azure AD B2C to access the protected web API.</span></span>

## <a name="update-code"></a><span data-ttu-id="7a10b-187">Update code</span><span class="sxs-lookup"><span data-stu-id="7a10b-187">Update code</span></span>

<span data-ttu-id="7a10b-188">Now that the web API is registered and you have scopes defined, you need to configure the web API code to use your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="7a10b-188">Now that the web API is registered and you have scopes defined, you need to configure the web API code to use your Azure AD B2C tenant.</span></span> <span data-ttu-id="7a10b-189">In this tutorial, you configure a sample .NET Core web app you can download from GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a10b-189">In this tutorial, you configure a sample .NET Core web app you can download from GitHub.</span></span> 

<span data-ttu-id="7a10b-190">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi/archive/master.zip) or clone the sample web app from GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a10b-190">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi/archive/master.zip) or clone the sample web app from GitHub.</span></span>

```
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi.git
```

### <a name="configure-the-web-api"></a><span data-ttu-id="7a10b-191">Configure the web API</span><span class="sxs-lookup"><span data-stu-id="7a10b-191">Configure the web API</span></span>

1. <span data-ttu-id="7a10b-192">Open the **B2C-WebAPI.sln** solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a10b-192">Open the **B2C-WebAPI.sln** solution in Visual Studio.</span></span>

2. <span data-ttu-id="7a10b-193">Open the **appsettings.json** file.</span><span class="sxs-lookup"><span data-stu-id="7a10b-193">Open the **appsettings.json** file.</span></span> <span data-ttu-id="7a10b-194">Update the following values to configure the web api to use your tenant:</span><span class="sxs-lookup"><span data-stu-id="7a10b-194">Update the following values to configure the web api to use your tenant:</span></span>

    ```javascript
    "AzureAdB2C": 
      {
        "Tenant": "<your tenant name>.onmicrosoft.com", 
        "ClientId": "<The Application ID for your web API obtained from the Azure portal>",
        "Policy": "<Your sign up sign in policy e.g. B2C_1_SiUpIn>",
        "ScopeRead": "demo.read"  
      },
    ```

#### <a name="enable-cors"></a><span data-ttu-id="7a10b-195">Enable CORS</span><span class="sxs-lookup"><span data-stu-id="7a10b-195">Enable CORS</span></span>

<span data-ttu-id="7a10b-196">To allow your single page app to call the ASP.NET Core web API, you need to enable [CORS](https://docs.microsoft.com/aspnet/core/security/cors).</span><span class="sxs-lookup"><span data-stu-id="7a10b-196">To allow your single page app to call the ASP.NET Core web API, you need to enable [CORS](https://docs.microsoft.com/aspnet/core/security/cors).</span></span>

1. <span data-ttu-id="7a10b-197">In **Startup.cs**, add CORS to the `ConfigureServices()` method.</span><span class="sxs-lookup"><span data-stu-id="7a10b-197">In **Startup.cs**, add CORS to the `ConfigureServices()` method.</span></span>

    ```C#
    public void ConfigureServices(IServiceCollection services) {
      services.AddCors();
    ```

2. <span data-ttu-id="7a10b-198">In **Startup.cs**, configure CORS in the `Configure()` method.</span><span class="sxs-lookup"><span data-stu-id="7a10b-198">In **Startup.cs**, configure CORS in the `Configure()` method.</span></span>

    ```C#
    public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory) {
      app.UseCors(builder =>
        builder.WithOrigins("http://localhost:6420").AllowAnyHeader().AllowAnyMethod());
    ```

3. <span data-ttu-id="7a10b-199">Open the **launchSettings.json** file under **Properties**, locate the *applicationURL* setting, and record the value for use in the next section.</span><span class="sxs-lookup"><span data-stu-id="7a10b-199">Open the **launchSettings.json** file under **Properties**, locate the *applicationURL* setting, and record the value for use in the next section.</span></span>

### <a name="configure-the-single-page-app"></a><span data-ttu-id="7a10b-200">Configure the single page app</span><span class="sxs-lookup"><span data-stu-id="7a10b-200">Configure the single page app</span></span>

<span data-ttu-id="7a10b-201">The single page app uses Azure AD B2C for user sign-up, sign-in, and calls the protected ASP.NET Core web API.</span><span class="sxs-lookup"><span data-stu-id="7a10b-201">The single page app uses Azure AD B2C for user sign-up, sign-in, and calls the protected ASP.NET Core web API.</span></span> <span data-ttu-id="7a10b-202">You need to update the single page app call the .NET Core web api.</span><span class="sxs-lookup"><span data-stu-id="7a10b-202">You need to update the single page app call the .NET Core web api.</span></span>
<span data-ttu-id="7a10b-203">To change the app settings:</span><span class="sxs-lookup"><span data-stu-id="7a10b-203">To change the app settings:</span></span>

1. <span data-ttu-id="7a10b-204">Open the `index.html` file in the Node.js single page app sample.</span><span class="sxs-lookup"><span data-stu-id="7a10b-204">Open the `index.html` file in the Node.js single page app sample.</span></span>
2. <span data-ttu-id="7a10b-205">Configure the sample with the Azure AD B2C tenant registration information.</span><span class="sxs-lookup"><span data-stu-id="7a10b-205">Configure the sample with the Azure AD B2C tenant registration information.</span></span> <span data-ttu-id="7a10b-206">In the following code, add your tenant name to **b2cScopes** and change the **webApi** value to the *applicationURL* value that you previously recorded:</span><span class="sxs-lookup"><span data-stu-id="7a10b-206">In the following code, add your tenant name to **b2cScopes** and change the **webApi** value to the *applicationURL* value that you previously recorded:</span></span>

    ```javascript
    // The current application coordinates were pre-registered in a B2C tenant.
    var applicationConfig = {
        clientID: '<Application ID for your SPA obtained from portal app registration>',
        authority: "https://<your-tenant-name>.b2clogin.com/tfp/<your-tenant-name>.onmicrosoft.com/B2C_1_SiUpIn",
        b2cScopes: ["https://<Your tenant name>.onmicrosoft.com/HelloCoreAPI/demo.read"],
        webApi: 'http://localhost:64791/api/values',
    };
    ```

## <a name="run-the-spa-app-and-web-api"></a><span data-ttu-id="7a10b-207">Run the SPA app and web API</span><span class="sxs-lookup"><span data-stu-id="7a10b-207">Run the SPA app and web API</span></span>

<span data-ttu-id="7a10b-208">You need to run both the Node.js single page app and the .NET Core web API.</span><span class="sxs-lookup"><span data-stu-id="7a10b-208">You need to run both the Node.js single page app and the .NET Core web API.</span></span>

### <a name="run-the-aspnet-core-web-api"></a><span data-ttu-id="7a10b-209">Run the ASP.NET Core Web API</span><span class="sxs-lookup"><span data-stu-id="7a10b-209">Run the ASP.NET Core Web API</span></span> 

<span data-ttu-id="7a10b-210">Press **F5** to debug the **B2C-WebAPI.sln** solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a10b-210">Press **F5** to debug the **B2C-WebAPI.sln** solution in Visual Studio.</span></span>

<span data-ttu-id="7a10b-211">When the project launches, a web page is displayed in your default browser announcing the web api is available for requests.</span><span class="sxs-lookup"><span data-stu-id="7a10b-211">When the project launches, a web page is displayed in your default browser announcing the web api is available for requests.</span></span>

### <a name="run-the-single-page-app"></a><span data-ttu-id="7a10b-212">Run the single page app</span><span class="sxs-lookup"><span data-stu-id="7a10b-212">Run the single page app</span></span>

1. <span data-ttu-id="7a10b-213">Launch a Node.js command prompt.</span><span class="sxs-lookup"><span data-stu-id="7a10b-213">Launch a Node.js command prompt.</span></span>
2. <span data-ttu-id="7a10b-214">Change to the directory containing the Node.js sample.</span><span class="sxs-lookup"><span data-stu-id="7a10b-214">Change to the directory containing the Node.js sample.</span></span> <span data-ttu-id="7a10b-215">For example `cd c:\active-directory-b2c-javascript-msal-singlepageapp`</span><span class="sxs-lookup"><span data-stu-id="7a10b-215">For example `cd c:\active-directory-b2c-javascript-msal-singlepageapp`</span></span>
3. <span data-ttu-id="7a10b-216">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="7a10b-216">Run the following commands:</span></span>
    ```
    npm install && npm update
    node server.js
    ```

    <span data-ttu-id="7a10b-217">The console window displays the port number of where the app is hosted.</span><span class="sxs-lookup"><span data-stu-id="7a10b-217">The console window displays the port number of where the app is hosted.</span></span>
    
    ```
    Listening on port 6420...
    ```

4. <span data-ttu-id="7a10b-218">Use a browser to navigate to the address `http://localhost:6420` to view the app.</span><span class="sxs-lookup"><span data-stu-id="7a10b-218">Use a browser to navigate to the address `http://localhost:6420` to view the app.</span></span>
5. <span data-ttu-id="7a10b-219">Sign in using the email address and password used in [Authenticate users with Azure Active Directory B2C in a single page application (JavaScript)](active-directory-b2c-tutorials-spa.md).</span><span class="sxs-lookup"><span data-stu-id="7a10b-219">Sign in using the email address and password used in [Authenticate users with Azure Active Directory B2C in a single page application (JavaScript)](active-directory-b2c-tutorials-spa.md).</span></span>
6. <span data-ttu-id="7a10b-220">Click the **Call API** button.</span><span class="sxs-lookup"><span data-stu-id="7a10b-220">Click the **Call API** button.</span></span>

<span data-ttu-id="7a10b-221">After you sign up or sign in with a user account, the sample calls the protected web api and returns a result.</span><span class="sxs-lookup"><span data-stu-id="7a10b-221">After you sign up or sign in with a user account, the sample calls the protected web api and returns a result.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="7a10b-222">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="7a10b-222">Clean up resources</span></span>

<span data-ttu-id="7a10b-223">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C tutorials.</span><span class="sxs-lookup"><span data-stu-id="7a10b-223">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C tutorials.</span></span> <span data-ttu-id="7a10b-224">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span><span class="sxs-lookup"><span data-stu-id="7a10b-224">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a10b-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a10b-225">Next steps</span></span>

<span data-ttu-id="7a10b-226">This article walked you through protecting a web API by registering and defining scopes in Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7a10b-226">This article walked you through protecting a web API by registering and defining scopes in Azure AD B2C.</span></span> <span data-ttu-id="7a10b-227">Learn more by browsing the available Azure AD B2C code samples.</span><span class="sxs-lookup"><span data-stu-id="7a10b-227">Learn more by browsing the available Azure AD B2C code samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a10b-228">Azure AD B2C code samples</span><span class="sxs-lookup"><span data-stu-id="7a10b-228">Azure AD B2C code samples</span></span>](https://azure.microsoft.com/resources/samples/?service=active-directory-b2c&sort=0)
