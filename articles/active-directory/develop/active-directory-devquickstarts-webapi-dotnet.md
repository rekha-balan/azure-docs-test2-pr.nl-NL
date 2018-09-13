---
title: Azure AD .NET web API Getting Started | Microsoft Docs
description: How to build a .NET MVC web API that integrates with Azure AD for authentication and authorization.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.openlocfilehash: b028a75836f7c762431bfb9e3fc30822b7dee885
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564571"
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="f4b7f-103">Help protect a web API by using bearer tokens from Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4b7f-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="f4b7f-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span></span>
<span data-ttu-id="f4b7f-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="f4b7f-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="f4b7f-107">Here we’ll use OWIN to build a "To Do List" web API that:</span><span class="sxs-lookup"><span data-stu-id="f4b7f-107">Here we’ll use OWIN to build a "To Do List" web API that:</span></span>

* <span data-ttu-id="f4b7f-108">Designates which APIs are protected.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="f4b7f-109">Validates that the web API calls contain a valid access token.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-109">Validates that the web API calls contain a valid access token.</span></span>

<span data-ttu-id="f4b7f-110">To build the To Do List API, you first need to:</span><span class="sxs-lookup"><span data-stu-id="f4b7f-110">To build the To Do List API, you first need to:</span></span>

1. <span data-ttu-id="f4b7f-111">Register an application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="f4b7f-112">Set up the app to use the OWIN authentication pipeline.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-112">Set up the app to use the OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="f4b7f-113">Configure a client application to call the web API.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-113">Configure a client application to call the web API.</span></span>

<span data-ttu-id="f4b7f-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f4b7f-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="f4b7f-115">Each is a Visual Studio 2013 solution.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="f4b7f-116">You also need an Azure AD tenant in which to register your application.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-116">You also need an Azure AD tenant in which to register your application.</span></span> <span data-ttu-id="f4b7f-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f4b7f-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="f4b7f-118">Step 1: Register an application with Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4b7f-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="f4b7f-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="f4b7f-120">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f4b7f-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f4b7f-121">On the top bar, click your account.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-121">On the top bar, click your account.</span></span> <span data-ttu-id="f4b7f-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>

3. <span data-ttu-id="f4b7f-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="f4b7f-124">Click **App registrations**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="f4b7f-125">Follow the prompts and create a new **Web Application and/or Web API**.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-125">Follow the prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="f4b7f-126">**Name** describes your application to users.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-126">**Name** describes your application to users.</span></span> <span data-ttu-id="f4b7f-127">Enter **To Do List Service**.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-127">Enter **To Do List Service**.</span></span>
  * <span data-ttu-id="f4b7f-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span></span> <span data-ttu-id="f4b7f-129">Enter `https://localhost:44321/` for this value.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="f4b7f-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="f4b7f-131">Enter a tenant-specific identifier.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="f4b7f-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="f4b7f-133">Save the configuration.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-133">Save the configuration.</span></span> <span data-ttu-id="f4b7f-134">Leave the portal open, because you'll also need to register your client application shortly.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-134">Leave the portal open, because you'll also need to register your client application shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="f4b7f-135">Step 2: Set up the app to use the OWIN authentication pipeline</span><span class="sxs-lookup"><span data-stu-id="f4b7f-135">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="f4b7f-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span></span>

1. <span data-ttu-id="f4b7f-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="f4b7f-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="f4b7f-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="f4b7f-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="f4b7f-141">Change the class declaration to `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-141">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="f4b7f-142">We’ve already implemented part of this class for you in another file.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="f4b7f-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="f4b7f-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="f4b7f-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. <span data-ttu-id="f4b7f-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="f4b7f-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="f4b7f-148">This will force the user to sign in before accessing that page.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-148">This will force the user to sign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="f4b7f-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span> <span data-ttu-id="f4b7f-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="f4b7f-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="f4b7f-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="f4b7f-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="f4b7f-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="f4b7f-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-the-service"></a><span data-ttu-id="f4b7f-156">Step 3: Configure a client application and run the service</span><span class="sxs-lookup"><span data-stu-id="f4b7f-156">Step 3: Configure a client application and run the service</span></span>
<span data-ttu-id="f4b7f-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span></span>

1. <span data-ttu-id="f4b7f-158">Go back to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f4b7f-158">Go back to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f4b7f-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span></span>
  * <span data-ttu-id="f4b7f-160">**Name** describes your application to users.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-160">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="f4b7f-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span></span>

3. <span data-ttu-id="f4b7f-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="f4b7f-163">You’ll need this value in the next steps, so copy it from the application page.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-163">You’ll need this value in the next steps, so copy it from the application page.</span></span>

4. <span data-ttu-id="f4b7f-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="f4b7f-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="f4b7f-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="f4b7f-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="f4b7f-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span></span>
  * <span data-ttu-id="f4b7f-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4b7f-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4b7f-170">Next steps</span></span>
<span data-ttu-id="f4b7f-171">Finally, clean, build, and run each project.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="f4b7f-172">If you haven’t already, now is the time to create a new user in your tenant with a \*.onmicrosoft.com domain.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-172">If you haven’t already, now is the time to create a new user in your tenant with a \*.onmicrosoft.com domain.</span></span> <span data-ttu-id="f4b7f-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span></span>

<span data-ttu-id="f4b7f-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f4b7f-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="f4b7f-175">You can now move on to more identity scenarios.</span><span class="sxs-lookup"><span data-stu-id="f4b7f-175">You can now move on to more identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
