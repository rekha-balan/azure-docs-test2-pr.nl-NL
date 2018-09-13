---
title: Tutorial - Grant access to an ASP.NET web API from a web app using Azure Active Directory B2C | Microsoft Docs
description: Tutorial on how to use Active Directory B2C to protect an ASP.NET web api and call it from an ASP.NET web app.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.author: davidmu
ms.date: 01/23/2018
ms.custom: mvc
ms.topic: tutorial
ms.service: active-directory
ms.component: B2C
ms.openlocfilehash: 469a3662b5bc4db467dde3285d557ac8bbae368e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866401"
---
# <a name="tutorial-grant-access-to-an-aspnet-web-api-from-a-web-app-using-azure-active-directory-b2c"></a><span data-ttu-id="2d899-103">Tutorial: Grant access to an ASP.NET web API from a web app using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="2d899-103">Tutorial: Grant access to an ASP.NET web API from a web app using Azure Active Directory B2C</span></span>

<span data-ttu-id="2d899-104">This tutorial shows you how to call an Azure Active Directory (Azure AD) B2C protected web API resource from an ASP.NET web app.</span><span class="sxs-lookup"><span data-stu-id="2d899-104">This tutorial shows you how to call an Azure Active Directory (Azure AD) B2C protected web API resource from an ASP.NET web app.</span></span>

<span data-ttu-id="2d899-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="2d899-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2d899-106">Register a web API in your Azure AD B2C tenant</span><span class="sxs-lookup"><span data-stu-id="2d899-106">Register a web API in your Azure AD B2C tenant</span></span>
> * <span data-ttu-id="2d899-107">Define and configure scopes for a web API</span><span class="sxs-lookup"><span data-stu-id="2d899-107">Define and configure scopes for a web API</span></span>
> * <span data-ttu-id="2d899-108">Grant app permissions to the web API</span><span class="sxs-lookup"><span data-stu-id="2d899-108">Grant app permissions to the web API</span></span>
> * <span data-ttu-id="2d899-109">Update sample code to use Azure AD B2C to protect a web API</span><span class="sxs-lookup"><span data-stu-id="2d899-109">Update sample code to use Azure AD B2C to protect a web API</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="2d899-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2d899-110">Prerequisites</span></span>

* <span data-ttu-id="2d899-111">Complete the [Use Azure Active Directory B2C for User Authentication in an ASP.NET Web App tutorial](active-directory-b2c-tutorials-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="2d899-111">Complete the [Use Azure Active Directory B2C for User Authentication in an ASP.NET Web App tutorial](active-directory-b2c-tutorials-web-app.md).</span></span>
* <span data-ttu-id="2d899-112">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span><span class="sxs-lookup"><span data-stu-id="2d899-112">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="register-web-api"></a><span data-ttu-id="2d899-113">Register web API</span><span class="sxs-lookup"><span data-stu-id="2d899-113">Register web API</span></span>

<span data-ttu-id="2d899-114">Web API resources need to be registered in your tenant before they can accept and respond to [protected resource requests](../active-directory/develop/developer-glossary.md#resource-server) by [client applications](../active-directory/develop/developer-glossary.md#client-application) that present an [access token](../active-directory/develop/developer-glossary.md#access-token) from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2d899-114">Web API resources need to be registered in your tenant before they can accept and respond to [protected resource requests](../active-directory/develop/developer-glossary.md#resource-server) by [client applications](../active-directory/develop/developer-glossary.md#client-application) that present an [access token](../active-directory/develop/developer-glossary.md#access-token) from Azure Active Directory.</span></span> <span data-ttu-id="2d899-115">Registration establishes the [application and service principal object](../active-directory/develop/developer-glossary.md#application-object) in your tenant.</span><span class="sxs-lookup"><span data-stu-id="2d899-115">Registration establishes the [application and service principal object](../active-directory/develop/developer-glossary.md#application-object) in your tenant.</span></span> 

1. <span data-ttu-id="2d899-116">Log in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="2d899-116">Log in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span></span>

2. <span data-ttu-id="2d899-117">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2d899-117">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span></span> <span data-ttu-id="2d899-118">Select your subscription information, and then select **Switch Directory**.</span><span class="sxs-lookup"><span data-stu-id="2d899-118">Select your subscription information, and then select **Switch Directory**.</span></span>

    ![Switch directories](./media/active-directory-b2c-tutorials-web-api/switch-directories.png)

3. <span data-ttu-id="2d899-120">Choose the directory that contains your tenant.</span><span class="sxs-lookup"><span data-stu-id="2d899-120">Choose the directory that contains your tenant.</span></span>

    ![Select directory](./media/active-directory-b2c-tutorials-web-api/select-directory.png)

4. <span data-ttu-id="2d899-122">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="2d899-122">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span></span> <span data-ttu-id="2d899-123">You should now be using the tenant that you created in the previous tutorial.</span><span class="sxs-lookup"><span data-stu-id="2d899-123">You should now be using the tenant that you created in the previous tutorial.</span></span>

5. <span data-ttu-id="2d899-124">Select **Applications** and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="2d899-124">Select **Applications** and then select **Add**.</span></span>

    <span data-ttu-id="2d899-125">To register the sample web API in your tenant, use the following settings.</span><span class="sxs-lookup"><span data-stu-id="2d899-125">To register the sample web API in your tenant, use the following settings.</span></span>
    
    ![Add a new API](./media/active-directory-b2c-tutorials-web-api/web-api-registration.png)
    
    | <span data-ttu-id="2d899-127">Setting</span><span class="sxs-lookup"><span data-stu-id="2d899-127">Setting</span></span>      | <span data-ttu-id="2d899-128">Suggested value</span><span class="sxs-lookup"><span data-stu-id="2d899-128">Suggested value</span></span>  | <span data-ttu-id="2d899-129">Description</span><span class="sxs-lookup"><span data-stu-id="2d899-129">Description</span></span>                                        |
    | ------------ | ------- | -------------------------------------------------- |
    | <span data-ttu-id="2d899-130">**Name**</span><span class="sxs-lookup"><span data-stu-id="2d899-130">**Name**</span></span> | <span data-ttu-id="2d899-131">My Sample Web API</span><span class="sxs-lookup"><span data-stu-id="2d899-131">My Sample Web API</span></span> | <span data-ttu-id="2d899-132">Enter a **Name** that describes your web API to developers.</span><span class="sxs-lookup"><span data-stu-id="2d899-132">Enter a **Name** that describes your web API to developers.</span></span> |
    | <span data-ttu-id="2d899-133">**Include web app / web API**</span><span class="sxs-lookup"><span data-stu-id="2d899-133">**Include web app / web API**</span></span> | <span data-ttu-id="2d899-134">Yes</span><span class="sxs-lookup"><span data-stu-id="2d899-134">Yes</span></span> | <span data-ttu-id="2d899-135">Select **Yes** for a web API.</span><span class="sxs-lookup"><span data-stu-id="2d899-135">Select **Yes** for a web API.</span></span> |
    | <span data-ttu-id="2d899-136">**Allow implicit flow**</span><span class="sxs-lookup"><span data-stu-id="2d899-136">**Allow implicit flow**</span></span> | <span data-ttu-id="2d899-137">Yes</span><span class="sxs-lookup"><span data-stu-id="2d899-137">Yes</span></span> | <span data-ttu-id="2d899-138">Select **Yes** since the API uses [OpenID Connect sign-in](active-directory-b2c-reference-oidc.md).</span><span class="sxs-lookup"><span data-stu-id="2d899-138">Select **Yes** since the API uses [OpenID Connect sign-in](active-directory-b2c-reference-oidc.md).</span></span> |
    | <span data-ttu-id="2d899-139">**Reply URL**</span><span class="sxs-lookup"><span data-stu-id="2d899-139">**Reply URL**</span></span> | `https://localhost:44332` | <span data-ttu-id="2d899-140">Reply URLs are endpoints where Azure AD B2C returns any tokens that your API requests.</span><span class="sxs-lookup"><span data-stu-id="2d899-140">Reply URLs are endpoints where Azure AD B2C returns any tokens that your API requests.</span></span> <span data-ttu-id="2d899-141">In this tutorial, the sample web API runs locally (localhost) and listens on port 44332.</span><span class="sxs-lookup"><span data-stu-id="2d899-141">In this tutorial, the sample web API runs locally (localhost) and listens on port 44332.</span></span> |
    | <span data-ttu-id="2d899-142">**App ID URI**</span><span class="sxs-lookup"><span data-stu-id="2d899-142">**App ID URI**</span></span> | <span data-ttu-id="2d899-143">myAPISample</span><span class="sxs-lookup"><span data-stu-id="2d899-143">myAPISample</span></span> | <span data-ttu-id="2d899-144">The URI uniquely identifies the API in the tenant.</span><span class="sxs-lookup"><span data-stu-id="2d899-144">The URI uniquely identifies the API in the tenant.</span></span> <span data-ttu-id="2d899-145">This allows you to register multiple APIs per tenant.</span><span class="sxs-lookup"><span data-stu-id="2d899-145">This allows you to register multiple APIs per tenant.</span></span> <span data-ttu-id="2d899-146">[Scopes](../active-directory/develop/developer-glossary.md#scopes) govern access to the protected API resource and are defined per App ID URI.</span><span class="sxs-lookup"><span data-stu-id="2d899-146">[Scopes](../active-directory/develop/developer-glossary.md#scopes) govern access to the protected API resource and are defined per App ID URI.</span></span> |
    | <span data-ttu-id="2d899-147">**Native client**</span><span class="sxs-lookup"><span data-stu-id="2d899-147">**Native client**</span></span> | <span data-ttu-id="2d899-148">No</span><span class="sxs-lookup"><span data-stu-id="2d899-148">No</span></span> | <span data-ttu-id="2d899-149">Since this is a web API and not a native client, select No.</span><span class="sxs-lookup"><span data-stu-id="2d899-149">Since this is a web API and not a native client, select No.</span></span> |
    
6. <span data-ttu-id="2d899-150">Click **Create** to register your API.</span><span class="sxs-lookup"><span data-stu-id="2d899-150">Click **Create** to register your API.</span></span>

<span data-ttu-id="2d899-151">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="2d899-151">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span></span> <span data-ttu-id="2d899-152">Select your web API from the list.</span><span class="sxs-lookup"><span data-stu-id="2d899-152">Select your web API from the list.</span></span> <span data-ttu-id="2d899-153">The web API's property pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="2d899-153">The web API's property pane is displayed.</span></span>

![Web API properties](./media/active-directory-b2c-tutorials-web-api/b2c-web-api-properties.png)

<span data-ttu-id="2d899-155">Make note of the **Application Client ID**.</span><span class="sxs-lookup"><span data-stu-id="2d899-155">Make note of the **Application Client ID**.</span></span> <span data-ttu-id="2d899-156">The ID uniquely identifies the API and is needed when configuring the API later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="2d899-156">The ID uniquely identifies the API and is needed when configuring the API later in the tutorial.</span></span>

<span data-ttu-id="2d899-157">Registering your web API with Azure AD B2C defines a trust relationship.</span><span class="sxs-lookup"><span data-stu-id="2d899-157">Registering your web API with Azure AD B2C defines a trust relationship.</span></span> <span data-ttu-id="2d899-158">Since the API is registered with B2C, the API can now trust the B2C access tokens it receives from other applications.</span><span class="sxs-lookup"><span data-stu-id="2d899-158">Since the API is registered with B2C, the API can now trust the B2C access tokens it receives from other applications.</span></span>

## <a name="define-and-configure-scopes"></a><span data-ttu-id="2d899-159">Define and configure scopes</span><span class="sxs-lookup"><span data-stu-id="2d899-159">Define and configure scopes</span></span>

<span data-ttu-id="2d899-160">[Scopes](../active-directory/develop/developer-glossary.md#scopes) provide a way to govern access to protected resources.</span><span class="sxs-lookup"><span data-stu-id="2d899-160">[Scopes](../active-directory/develop/developer-glossary.md#scopes) provide a way to govern access to protected resources.</span></span> <span data-ttu-id="2d899-161">Scopes are used by the web API to implement scope-based access control.</span><span class="sxs-lookup"><span data-stu-id="2d899-161">Scopes are used by the web API to implement scope-based access control.</span></span> <span data-ttu-id="2d899-162">For example, users of the web API could have both read and write access, or users of the web API might have only read access.</span><span class="sxs-lookup"><span data-stu-id="2d899-162">For example, users of the web API could have both read and write access, or users of the web API might have only read access.</span></span> <span data-ttu-id="2d899-163">In this tutorial, you use scopes to define read and write permissions for the web API.</span><span class="sxs-lookup"><span data-stu-id="2d899-163">In this tutorial, you use scopes to define read and write permissions for the web API.</span></span>

### <a name="define-scopes-for-the-web-api"></a><span data-ttu-id="2d899-164">Define scopes for the web API</span><span class="sxs-lookup"><span data-stu-id="2d899-164">Define scopes for the web API</span></span>

<span data-ttu-id="2d899-165">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="2d899-165">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span></span> <span data-ttu-id="2d899-166">Select your web API from the list.</span><span class="sxs-lookup"><span data-stu-id="2d899-166">Select your web API from the list.</span></span> <span data-ttu-id="2d899-167">The web API's property pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="2d899-167">The web API's property pane is displayed.</span></span>

<span data-ttu-id="2d899-168">Click **Published scopes (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="2d899-168">Click **Published scopes (Preview)**.</span></span>

<span data-ttu-id="2d899-169">To configure scopes for the API, add the following entries.</span><span class="sxs-lookup"><span data-stu-id="2d899-169">To configure scopes for the API, add the following entries.</span></span> 

![scopes defined in web api](media/active-directory-b2c-tutorials-web-api/scopes-defined-in-web-api.png)

| <span data-ttu-id="2d899-171">Setting</span><span class="sxs-lookup"><span data-stu-id="2d899-171">Setting</span></span>      | <span data-ttu-id="2d899-172">Suggested value</span><span class="sxs-lookup"><span data-stu-id="2d899-172">Suggested value</span></span>  | <span data-ttu-id="2d899-173">Description</span><span class="sxs-lookup"><span data-stu-id="2d899-173">Description</span></span>                                        |
| ------------ | ------- | -------------------------------------------------- |
| <span data-ttu-id="2d899-174">**Scope**</span><span class="sxs-lookup"><span data-stu-id="2d899-174">**Scope**</span></span> | <span data-ttu-id="2d899-175">Hello.Read</span><span class="sxs-lookup"><span data-stu-id="2d899-175">Hello.Read</span></span> | <span data-ttu-id="2d899-176">Read access to hello</span><span class="sxs-lookup"><span data-stu-id="2d899-176">Read access to hello</span></span> |
| <span data-ttu-id="2d899-177">**Scope**</span><span class="sxs-lookup"><span data-stu-id="2d899-177">**Scope**</span></span> | <span data-ttu-id="2d899-178">Hello.Write</span><span class="sxs-lookup"><span data-stu-id="2d899-178">Hello.Write</span></span> | <span data-ttu-id="2d899-179">Write access to hello</span><span class="sxs-lookup"><span data-stu-id="2d899-179">Write access to hello</span></span> |

<span data-ttu-id="2d899-180">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2d899-180">Click **Save**.</span></span>

<span data-ttu-id="2d899-181">The published scopes can be used to grant a client app permission to the web API.</span><span class="sxs-lookup"><span data-stu-id="2d899-181">The published scopes can be used to grant a client app permission to the web API.</span></span>

### <a name="grant-app-permissions-to-web-api"></a><span data-ttu-id="2d899-182">Grant app permissions to web API</span><span class="sxs-lookup"><span data-stu-id="2d899-182">Grant app permissions to web API</span></span>

<span data-ttu-id="2d899-183">To call a protected web API from an app, you need to grant your app permissions to the API.</span><span class="sxs-lookup"><span data-stu-id="2d899-183">To call a protected web API from an app, you need to grant your app permissions to the API.</span></span> <span data-ttu-id="2d899-184">In this tutorial, use the web app created in [Use Azure Active Directory B2C for User Authentication in an ASP.NET Web App tutorial](active-directory-b2c-tutorials-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="2d899-184">In this tutorial, use the web app created in [Use Azure Active Directory B2C for User Authentication in an ASP.NET Web App tutorial](active-directory-b2c-tutorials-web-app.md).</span></span> 

1. <span data-ttu-id="2d899-185">In the Azure portal, select **Azure AD B2C** from the services list and click **Applications** to view the registered app list.</span><span class="sxs-lookup"><span data-stu-id="2d899-185">In the Azure portal, select **Azure AD B2C** from the services list and click **Applications** to view the registered app list.</span></span>

2. <span data-ttu-id="2d899-186">Select **My Sample Web App** from the app list and click **API access (Preview)** then **Add**.</span><span class="sxs-lookup"><span data-stu-id="2d899-186">Select **My Sample Web App** from the app list and click **API access (Preview)** then **Add**.</span></span>

3. <span data-ttu-id="2d899-187">In the **Select API** dropdown, select your registered web API **My Sample Web API**.</span><span class="sxs-lookup"><span data-stu-id="2d899-187">In the **Select API** dropdown, select your registered web API **My Sample Web API**.</span></span>

4. <span data-ttu-id="2d899-188">In the **Select Scopes** dropdown, select the scopes you defined in the web API registration.</span><span class="sxs-lookup"><span data-stu-id="2d899-188">In the **Select Scopes** dropdown, select the scopes you defined in the web API registration.</span></span>

    ![selecting scopes for app](media/active-directory-b2c-tutorials-web-api/selecting-scopes-for-app.png)

5. <span data-ttu-id="2d899-190">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2d899-190">Click **OK**.</span></span>

<span data-ttu-id="2d899-191">Your **My Sample Web App** is registered to call the protected **My Sample Web API**.</span><span class="sxs-lookup"><span data-stu-id="2d899-191">Your **My Sample Web App** is registered to call the protected **My Sample Web API**.</span></span> <span data-ttu-id="2d899-192">A user [authenticates](../active-directory/develop/developer-glossary.md#authentication) with Azure AD B2C to use the web app.</span><span class="sxs-lookup"><span data-stu-id="2d899-192">A user [authenticates](../active-directory/develop/developer-glossary.md#authentication) with Azure AD B2C to use the web app.</span></span> <span data-ttu-id="2d899-193">The web app obtains an [authorization grant](../active-directory/develop/developer-glossary.md#authorization-grant) from Azure AD B2C to access the protected web API.</span><span class="sxs-lookup"><span data-stu-id="2d899-193">The web app obtains an [authorization grant](../active-directory/develop/developer-glossary.md#authorization-grant) from Azure AD B2C to access the protected web API.</span></span>

## <a name="update-code"></a><span data-ttu-id="2d899-194">Update code</span><span class="sxs-lookup"><span data-stu-id="2d899-194">Update code</span></span>

<span data-ttu-id="2d899-195">Now that the web API is registered and you have scopes defined, you need to configure the web API code to use your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="2d899-195">Now that the web API is registered and you have scopes defined, you need to configure the web API code to use your Azure AD B2C tenant.</span></span> <span data-ttu-id="2d899-196">In this tutorial, you configure a sample web API.</span><span class="sxs-lookup"><span data-stu-id="2d899-196">In this tutorial, you configure a sample web API.</span></span> 

<span data-ttu-id="2d899-197">The sample web API is included in the project you downloaded in the prerequisite tutorial: [Use Azure Active Directory B2C for User Authentication in an ASP.NET Web App tutorial](active-directory-b2c-tutorials-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="2d899-197">The sample web API is included in the project you downloaded in the prerequisite tutorial: [Use Azure Active Directory B2C for User Authentication in an ASP.NET Web App tutorial](active-directory-b2c-tutorials-web-app.md).</span></span> <span data-ttu-id="2d899-198">If you haven't completed the prerequisite tutorial, complete it before continuing.</span><span class="sxs-lookup"><span data-stu-id="2d899-198">If you haven't completed the prerequisite tutorial, complete it before continuing.</span></span>

<span data-ttu-id="2d899-199">There are two projects in the sample solution:</span><span class="sxs-lookup"><span data-stu-id="2d899-199">There are two projects in the sample solution:</span></span>

<span data-ttu-id="2d899-200">**Web app sample app (TaskWebApp):** Web app to create and edit a task list.</span><span class="sxs-lookup"><span data-stu-id="2d899-200">**Web app sample app (TaskWebApp):** Web app to create and edit a task list.</span></span> <span data-ttu-id="2d899-201">The web app uses the **sign-up or sign-in** policy to sign up or sign in users with an email address.</span><span class="sxs-lookup"><span data-stu-id="2d899-201">The web app uses the **sign-up or sign-in** policy to sign up or sign in users with an email address.</span></span>

<span data-ttu-id="2d899-202">**Web API sample app (TaskService):** Web API that supports the create, read,  update, and delete task list functionality.</span><span class="sxs-lookup"><span data-stu-id="2d899-202">**Web API sample app (TaskService):** Web API that supports the create, read,  update, and delete task list functionality.</span></span> <span data-ttu-id="2d899-203">The web API is secured by Azure AD B2C and called by the web app.</span><span class="sxs-lookup"><span data-stu-id="2d899-203">The web API is secured by Azure AD B2C and called by the web app.</span></span>

<span data-ttu-id="2d899-204">The sample web app and web API define the configuration values as app settings in each project's Web.config file.</span><span class="sxs-lookup"><span data-stu-id="2d899-204">The sample web app and web API define the configuration values as app settings in each project's Web.config file.</span></span>

<span data-ttu-id="2d899-205">Open the **B2C-WebAPI-DotNet** solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2d899-205">Open the **B2C-WebAPI-DotNet** solution in Visual Studio.</span></span>

### <a name="configure-the-web-app"></a><span data-ttu-id="2d899-206">Configure the web app</span><span class="sxs-lookup"><span data-stu-id="2d899-206">Configure the web app</span></span>

1. <span data-ttu-id="2d899-207">Open **Web.config** in the **TaskWebApp** project.</span><span class="sxs-lookup"><span data-stu-id="2d899-207">Open **Web.config** in the **TaskWebApp** project.</span></span>

2. <span data-ttu-id="2d899-208">To run the API locally, use the localhost setting for **api:TaskServiceUrl**.</span><span class="sxs-lookup"><span data-stu-id="2d899-208">To run the API locally, use the localhost setting for **api:TaskServiceUrl**.</span></span> <span data-ttu-id="2d899-209">Change the Web.config as follows:</span><span class="sxs-lookup"><span data-stu-id="2d899-209">Change the Web.config as follows:</span></span> 

    ```C#
    <add key="api:TaskServiceUrl" value="https://localhost:44332/"/>
    ```

3. <span data-ttu-id="2d899-210">Configure the URI of the API.</span><span class="sxs-lookup"><span data-stu-id="2d899-210">Configure the URI of the API.</span></span> <span data-ttu-id="2d899-211">This is the URI the web app uses to make the API request.</span><span class="sxs-lookup"><span data-stu-id="2d899-211">This is the URI the web app uses to make the API request.</span></span> <span data-ttu-id="2d899-212">Also, configure the requested permissions.</span><span class="sxs-lookup"><span data-stu-id="2d899-212">Also, configure the requested permissions.</span></span>

    ```C#
    <add key="api:ApiIdentifier" value="https://<Your tenant name>.onmicrosoft.com/myAPISample/" />
    <add key="api:ReadScope" value="Hello.Read" />
    <add key="api:WriteScope" value="Hello.Write" />
    ```

### <a name="configure-the-web-api"></a><span data-ttu-id="2d899-213">Configure the web API</span><span class="sxs-lookup"><span data-stu-id="2d899-213">Configure the web API</span></span>

1. <span data-ttu-id="2d899-214">Open **Web.config** in the **TaskService** project.</span><span class="sxs-lookup"><span data-stu-id="2d899-214">Open **Web.config** in the **TaskService** project.</span></span>

2. <span data-ttu-id="2d899-215">Configure the API to use your tenant.</span><span class="sxs-lookup"><span data-stu-id="2d899-215">Configure the API to use your tenant.</span></span>

    ```C#
    <add key="ida:Tenant" value="<Your tenant name>.onmicrosoft.com" />
    ```

3. <span data-ttu-id="2d899-216">Set the client ID to the registered Application ID for your API.</span><span class="sxs-lookup"><span data-stu-id="2d899-216">Set the client ID to the registered Application ID for your API.</span></span>

    ```C#
    <add key="ida:ClientId" value="<The Application ID for your web API obtained from the Azure portal>"/>
    ```

4. <span data-ttu-id="2d899-217">Update the policy setting with the name generated when you created your sign up and sign in policy.</span><span class="sxs-lookup"><span data-stu-id="2d899-217">Update the policy setting with the name generated when you created your sign up and sign in policy.</span></span>

    ```C#
    <add key="ida:SignUpSignInPolicyId" value="B2C_1_SiUpIn" />
    ```

5. <span data-ttu-id="2d899-218">Configure the scopes setting to match what you created in the portal.</span><span class="sxs-lookup"><span data-stu-id="2d899-218">Configure the scopes setting to match what you created in the portal.</span></span>

    ```C#
    <add key="api:ReadScope" value="Hello.Read" />
    <add key="api:WriteScope" value="Hello.Write" />
    ```

## <a name="run-the-sample"></a><span data-ttu-id="2d899-219">Run the sample</span><span class="sxs-lookup"><span data-stu-id="2d899-219">Run the sample</span></span>

<span data-ttu-id="2d899-220">You need to run both the **TaskWebApp** and **TaskService** projects.</span><span class="sxs-lookup"><span data-stu-id="2d899-220">You need to run both the **TaskWebApp** and **TaskService** projects.</span></span> 

1. <span data-ttu-id="2d899-221">In Solution Explorer, right-click on the solution and select **Set StartUp Projects...**.</span><span class="sxs-lookup"><span data-stu-id="2d899-221">In Solution Explorer, right-click on the solution and select **Set StartUp Projects...**.</span></span> 
2. <span data-ttu-id="2d899-222">Select **Multiple startup projects** radio button.</span><span class="sxs-lookup"><span data-stu-id="2d899-222">Select **Multiple startup projects** radio button.</span></span>
3. <span data-ttu-id="2d899-223">Change the **Action** for both projects to **Start**.</span><span class="sxs-lookup"><span data-stu-id="2d899-223">Change the **Action** for both projects to **Start**.</span></span>
4. <span data-ttu-id="2d899-224">Click OK to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="2d899-224">Click OK to save the configuration.</span></span>
5. <span data-ttu-id="2d899-225">Press **F5** to run both applications.</span><span class="sxs-lookup"><span data-stu-id="2d899-225">Press **F5** to run both applications.</span></span> <span data-ttu-id="2d899-226">Each application opens in its own browser tab. `https://localhost:44316/` is the web app.</span><span class="sxs-lookup"><span data-stu-id="2d899-226">Each application opens in its own browser tab. `https://localhost:44316/` is the web app.</span></span>
    <span data-ttu-id="2d899-227">`https://localhost:44332/` is the web API.</span><span class="sxs-lookup"><span data-stu-id="2d899-227">`https://localhost:44332/` is the web API.</span></span>

6. <span data-ttu-id="2d899-228">In the web app, click the sign up / sign in link in the menu banner to sign up for the web application.</span><span class="sxs-lookup"><span data-stu-id="2d899-228">In the web app, click the sign up / sign in link in the menu banner to sign up for the web application.</span></span> <span data-ttu-id="2d899-229">Use the account you created in the [web app tutorial](active-directory-b2c-tutorials-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="2d899-229">Use the account you created in the [web app tutorial](active-directory-b2c-tutorials-web-app.md).</span></span> 
7. <span data-ttu-id="2d899-230">Once signed in, click the **To-do list** link and create a to-do list item.</span><span class="sxs-lookup"><span data-stu-id="2d899-230">Once signed in, click the **To-do list** link and create a to-do list item.</span></span>

<span data-ttu-id="2d899-231">When you create a to-do list item, the web app makes a request to the web API to generate the to-do list item.</span><span class="sxs-lookup"><span data-stu-id="2d899-231">When you create a to-do list item, the web app makes a request to the web API to generate the to-do list item.</span></span> <span data-ttu-id="2d899-232">You're protected web app is calling the protected web API in your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="2d899-232">You're protected web app is calling the protected web API in your Azure AD B2C tenant.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="2d899-233">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="2d899-233">Clean up resources</span></span>

<span data-ttu-id="2d899-234">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C tutorials.</span><span class="sxs-lookup"><span data-stu-id="2d899-234">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C tutorials.</span></span> <span data-ttu-id="2d899-235">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span><span class="sxs-lookup"><span data-stu-id="2d899-235">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d899-236">Next steps</span><span class="sxs-lookup"><span data-stu-id="2d899-236">Next steps</span></span>

<span data-ttu-id="2d899-237">This article walked you through protecting a ASP.NET web API by registering and defining scopes in Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2d899-237">This article walked you through protecting a ASP.NET web API by registering and defining scopes in Azure AD B2C.</span></span> <span data-ttu-id="2d899-238">To learn more details about developing this scenario including code walkthroughs, continue to the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="2d899-238">To learn more details about developing this scenario including code walkthroughs, continue to the next tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d899-239">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span><span class="sxs-lookup"><span data-stu-id="2d899-239">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)