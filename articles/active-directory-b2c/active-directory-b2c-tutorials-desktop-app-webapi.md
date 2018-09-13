---
title: Tutorial - Grant access to a Node.js web API from a desktop app using Azure Active Directory B2C | Microsoft Docs
description: Tutorial on how to use Active Directory B2C to protect a Node.js web api and call it from a .NET desktop app.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.author: davidmu
ms.date: 3/01/2018
ms.custom: mvc
ms.topic: tutorial
ms.service: active-directory
ms.component: B2C
ms.openlocfilehash: 98c86f5613116dce5423aa9ca6a2ff43e5414592
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871305"
---
# <a name="tutorial-grant-access-to-a-nodejs-web-api-from-a-desktop-app-using-azure-active-directory-b2c"></a><span data-ttu-id="212eb-103">Tutorial: Grant access to a Node.js web API from a desktop app using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="212eb-103">Tutorial: Grant access to a Node.js web API from a desktop app using Azure Active Directory B2C</span></span>

<span data-ttu-id="212eb-104">This tutorial shows you how to call an Azure Active Directory (Azure AD) B2C protected Node.js web API resource from a Windows Presentation Foundation (WPF) desktop app.</span><span class="sxs-lookup"><span data-stu-id="212eb-104">This tutorial shows you how to call an Azure Active Directory (Azure AD) B2C protected Node.js web API resource from a Windows Presentation Foundation (WPF) desktop app.</span></span>

<span data-ttu-id="212eb-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="212eb-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="212eb-106">Register a web API in your Azure AD B2C tenant</span><span class="sxs-lookup"><span data-stu-id="212eb-106">Register a web API in your Azure AD B2C tenant</span></span>
> * <span data-ttu-id="212eb-107">Define and configure scopes for a web API</span><span class="sxs-lookup"><span data-stu-id="212eb-107">Define and configure scopes for a web API</span></span>
> * <span data-ttu-id="212eb-108">Grant app permissions to the web API</span><span class="sxs-lookup"><span data-stu-id="212eb-108">Grant app permissions to the web API</span></span>
> * <span data-ttu-id="212eb-109">Update sample code to use Azure AD B2C to protect a web API</span><span class="sxs-lookup"><span data-stu-id="212eb-109">Update sample code to use Azure AD B2C to protect a web API</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="212eb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="212eb-110">Prerequisites</span></span>

* <span data-ttu-id="212eb-111">Complete the [Authenticate users with Azure Active Directory B2C in a desktop app tutorial](active-directory-b2c-tutorials-desktop-app.md).</span><span class="sxs-lookup"><span data-stu-id="212eb-111">Complete the [Authenticate users with Azure Active Directory B2C in a desktop app tutorial](active-directory-b2c-tutorials-desktop-app.md).</span></span>
* <span data-ttu-id="212eb-112">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with **.NET desktop development** and **ASP.NET and web development** workloads.</span><span class="sxs-lookup"><span data-stu-id="212eb-112">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with **.NET desktop development** and **ASP.NET and web development** workloads.</span></span>
* <span data-ttu-id="212eb-113">Install [Node.js](https://nodejs.org/en/download/)</span><span class="sxs-lookup"><span data-stu-id="212eb-113">Install [Node.js](https://nodejs.org/en/download/)</span></span>

## <a name="register-web-api"></a><span data-ttu-id="212eb-114">Register web API</span><span class="sxs-lookup"><span data-stu-id="212eb-114">Register web API</span></span>

<span data-ttu-id="212eb-115">Web API resources need to be registered in your tenant before they can accept and respond to [protected resource requests](../active-directory/develop/developer-glossary.md#resource-server) by [client applications](../active-directory/develop/developer-glossary.md#client-application) that present an [access token](../active-directory/develop/developer-glossary.md#access-token) from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="212eb-115">Web API resources need to be registered in your tenant before they can accept and respond to [protected resource requests](../active-directory/develop/developer-glossary.md#resource-server) by [client applications](../active-directory/develop/developer-glossary.md#client-application) that present an [access token](../active-directory/develop/developer-glossary.md#access-token) from Azure Active Directory.</span></span> <span data-ttu-id="212eb-116">Registration establishes the [application and service principal object](../active-directory/develop/developer-glossary.md#application-object) in your tenant.</span><span class="sxs-lookup"><span data-stu-id="212eb-116">Registration establishes the [application and service principal object](../active-directory/develop/developer-glossary.md#application-object) in your tenant.</span></span> 

<span data-ttu-id="212eb-117">Log in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="212eb-117">Log in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

1. <span data-ttu-id="212eb-118">Select **Azure AD B2C** from the services list in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="212eb-118">Select **Azure AD B2C** from the services list in the Azure portal.</span></span>

2. <span data-ttu-id="212eb-119">In the B2C settings, click **Applications** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="212eb-119">In the B2C settings, click **Applications** and then click **Add**.</span></span>

    <span data-ttu-id="212eb-120">To register the sample web API in your tenant, use the following settings.</span><span class="sxs-lookup"><span data-stu-id="212eb-120">To register the sample web API in your tenant, use the following settings.</span></span>
    
    ![Add a new API](media/active-directory-b2c-tutorials-desktop-app-webapi/web-api-registration.png)
    
    | <span data-ttu-id="212eb-122">Setting</span><span class="sxs-lookup"><span data-stu-id="212eb-122">Setting</span></span>      | <span data-ttu-id="212eb-123">Suggested value</span><span class="sxs-lookup"><span data-stu-id="212eb-123">Suggested value</span></span>  | <span data-ttu-id="212eb-124">Description</span><span class="sxs-lookup"><span data-stu-id="212eb-124">Description</span></span>                                        |
    | ------------ | ------- | -------------------------------------------------- |
    | <span data-ttu-id="212eb-125">**Name**</span><span class="sxs-lookup"><span data-stu-id="212eb-125">**Name**</span></span> | <span data-ttu-id="212eb-126">My sample Node.js web API</span><span class="sxs-lookup"><span data-stu-id="212eb-126">My sample Node.js web API</span></span> | <span data-ttu-id="212eb-127">Enter a **Name** that describes your web API to developers.</span><span class="sxs-lookup"><span data-stu-id="212eb-127">Enter a **Name** that describes your web API to developers.</span></span> |
    | <span data-ttu-id="212eb-128">**Include web app / web API**</span><span class="sxs-lookup"><span data-stu-id="212eb-128">**Include web app / web API**</span></span> | <span data-ttu-id="212eb-129">Yes</span><span class="sxs-lookup"><span data-stu-id="212eb-129">Yes</span></span> | <span data-ttu-id="212eb-130">Select **Yes** for a web API.</span><span class="sxs-lookup"><span data-stu-id="212eb-130">Select **Yes** for a web API.</span></span> |
    | <span data-ttu-id="212eb-131">**Allow implicit flow**</span><span class="sxs-lookup"><span data-stu-id="212eb-131">**Allow implicit flow**</span></span> | <span data-ttu-id="212eb-132">Yes</span><span class="sxs-lookup"><span data-stu-id="212eb-132">Yes</span></span> | <span data-ttu-id="212eb-133">Select **Yes** since the API uses [OpenID Connect sign-in](active-directory-b2c-reference-oidc.md).</span><span class="sxs-lookup"><span data-stu-id="212eb-133">Select **Yes** since the API uses [OpenID Connect sign-in](active-directory-b2c-reference-oidc.md).</span></span> |
    | <span data-ttu-id="212eb-134">**Reply URL**</span><span class="sxs-lookup"><span data-stu-id="212eb-134">**Reply URL**</span></span> | `http://localhost:5000` | <span data-ttu-id="212eb-135">Reply URLs are endpoints where Azure AD B2C returns any tokens that your API requests.</span><span class="sxs-lookup"><span data-stu-id="212eb-135">Reply URLs are endpoints where Azure AD B2C returns any tokens that your API requests.</span></span> <span data-ttu-id="212eb-136">In this tutorial, the sample web API runs locally (localhost) and listens on port 5000.</span><span class="sxs-lookup"><span data-stu-id="212eb-136">In this tutorial, the sample web API runs locally (localhost) and listens on port 5000.</span></span> |
    | <span data-ttu-id="212eb-137">**App ID URI**</span><span class="sxs-lookup"><span data-stu-id="212eb-137">**App ID URI**</span></span> | <span data-ttu-id="212eb-138">demoapi</span><span class="sxs-lookup"><span data-stu-id="212eb-138">demoapi</span></span> | <span data-ttu-id="212eb-139">The URI uniquely identifies the API in the tenant.</span><span class="sxs-lookup"><span data-stu-id="212eb-139">The URI uniquely identifies the API in the tenant.</span></span> <span data-ttu-id="212eb-140">This allows you to register multiple APIs per tenant.</span><span class="sxs-lookup"><span data-stu-id="212eb-140">This allows you to register multiple APIs per tenant.</span></span> <span data-ttu-id="212eb-141">[Scopes](../active-directory/develop/developer-glossary.md#scopes) govern access to the protected API resource and are defined per App ID URI.</span><span class="sxs-lookup"><span data-stu-id="212eb-141">[Scopes](../active-directory/develop/developer-glossary.md#scopes) govern access to the protected API resource and are defined per App ID URI.</span></span> |
    | <span data-ttu-id="212eb-142">**Native client**</span><span class="sxs-lookup"><span data-stu-id="212eb-142">**Native client**</span></span> | <span data-ttu-id="212eb-143">No</span><span class="sxs-lookup"><span data-stu-id="212eb-143">No</span></span> | <span data-ttu-id="212eb-144">Since this is a web API and not a native client, select No.</span><span class="sxs-lookup"><span data-stu-id="212eb-144">Since this is a web API and not a native client, select No.</span></span> |
    
3. <span data-ttu-id="212eb-145">Click **Create** to register your API.</span><span class="sxs-lookup"><span data-stu-id="212eb-145">Click **Create** to register your API.</span></span>

<span data-ttu-id="212eb-146">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="212eb-146">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span></span> <span data-ttu-id="212eb-147">Select your web API from the list.</span><span class="sxs-lookup"><span data-stu-id="212eb-147">Select your web API from the list.</span></span> <span data-ttu-id="212eb-148">The web API's property pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="212eb-148">The web API's property pane is displayed.</span></span>

![Web API properties](./media/active-directory-b2c-tutorials-web-api/b2c-web-api-properties.png)

<span data-ttu-id="212eb-150">Make note of the **Application Client ID**.</span><span class="sxs-lookup"><span data-stu-id="212eb-150">Make note of the **Application Client ID**.</span></span> <span data-ttu-id="212eb-151">The ID uniquely identifies the API and is needed when configuring the API later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="212eb-151">The ID uniquely identifies the API and is needed when configuring the API later in the tutorial.</span></span>

<span data-ttu-id="212eb-152">Registering your web API with Azure AD B2C defines a trust relationship.</span><span class="sxs-lookup"><span data-stu-id="212eb-152">Registering your web API with Azure AD B2C defines a trust relationship.</span></span> <span data-ttu-id="212eb-153">Since the API is registered with B2C, the API can now trust the B2C access tokens it receives from other applications.</span><span class="sxs-lookup"><span data-stu-id="212eb-153">Since the API is registered with B2C, the API can now trust the B2C access tokens it receives from other applications.</span></span>

## <a name="define-and-configure-scopes"></a><span data-ttu-id="212eb-154">Define and configure scopes</span><span class="sxs-lookup"><span data-stu-id="212eb-154">Define and configure scopes</span></span>

<span data-ttu-id="212eb-155">[Scopes](../active-directory/develop/developer-glossary.md#scopes) provide a way to govern access to protected resources.</span><span class="sxs-lookup"><span data-stu-id="212eb-155">[Scopes](../active-directory/develop/developer-glossary.md#scopes) provide a way to govern access to protected resources.</span></span> <span data-ttu-id="212eb-156">Scopes are used by the web API to implement scope-based access control.</span><span class="sxs-lookup"><span data-stu-id="212eb-156">Scopes are used by the web API to implement scope-based access control.</span></span> <span data-ttu-id="212eb-157">For example, some users could have both read and write access, whereas other users might have read-only permissions.</span><span class="sxs-lookup"><span data-stu-id="212eb-157">For example, some users could have both read and write access, whereas other users might have read-only permissions.</span></span> <span data-ttu-id="212eb-158">In this tutorial, you define read and write permissions for the web API.</span><span class="sxs-lookup"><span data-stu-id="212eb-158">In this tutorial, you define read and write permissions for the web API.</span></span>

### <a name="define-scopes-for-the-web-api"></a><span data-ttu-id="212eb-159">Define scopes for the web API</span><span class="sxs-lookup"><span data-stu-id="212eb-159">Define scopes for the web API</span></span>

<span data-ttu-id="212eb-160">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="212eb-160">Registered APIs are displayed in the applications list for the Azure AD B2C tenant.</span></span> <span data-ttu-id="212eb-161">Select your web API from the list.</span><span class="sxs-lookup"><span data-stu-id="212eb-161">Select your web API from the list.</span></span> <span data-ttu-id="212eb-162">The web API's property pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="212eb-162">The web API's property pane is displayed.</span></span>

<span data-ttu-id="212eb-163">Click **Published scopes (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="212eb-163">Click **Published scopes (Preview)**.</span></span>

<span data-ttu-id="212eb-164">To configure scopes for the API, add the following entries.</span><span class="sxs-lookup"><span data-stu-id="212eb-164">To configure scopes for the API, add the following entries.</span></span> 

![scopes defined in web api](media/active-directory-b2c-tutorials-web-api/scopes-defined-in-web-api.png)

| <span data-ttu-id="212eb-166">Setting</span><span class="sxs-lookup"><span data-stu-id="212eb-166">Setting</span></span>      | <span data-ttu-id="212eb-167">Suggested value</span><span class="sxs-lookup"><span data-stu-id="212eb-167">Suggested value</span></span>  | <span data-ttu-id="212eb-168">Description</span><span class="sxs-lookup"><span data-stu-id="212eb-168">Description</span></span>                                        |
| ------------ | ------- | -------------------------------------------------- |
| <span data-ttu-id="212eb-169">**Scope**</span><span class="sxs-lookup"><span data-stu-id="212eb-169">**Scope**</span></span> | <span data-ttu-id="212eb-170">demo.read</span><span class="sxs-lookup"><span data-stu-id="212eb-170">demo.read</span></span> | <span data-ttu-id="212eb-171">Read access to demo API</span><span class="sxs-lookup"><span data-stu-id="212eb-171">Read access to demo API</span></span>|

<span data-ttu-id="212eb-172">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="212eb-172">Click **Save**.</span></span>

<span data-ttu-id="212eb-173">The published scopes can be used to grant a client app permission to the web API.</span><span class="sxs-lookup"><span data-stu-id="212eb-173">The published scopes can be used to grant a client app permission to the web API.</span></span>

### <a name="grant-app-permissions-to-web-api"></a><span data-ttu-id="212eb-174">Grant app permissions to web API</span><span class="sxs-lookup"><span data-stu-id="212eb-174">Grant app permissions to web API</span></span>

<span data-ttu-id="212eb-175">To call a protected web API from an app, you need to grant your app permissions to the API.</span><span class="sxs-lookup"><span data-stu-id="212eb-175">To call a protected web API from an app, you need to grant your app permissions to the API.</span></span> <span data-ttu-id="212eb-176">In this tutorial, use the desktop app created in [Authenticate users with Azure Active Directory B2C in a desktop app tutorial](active-directory-b2c-tutorials-desktop-app.md).</span><span class="sxs-lookup"><span data-stu-id="212eb-176">In this tutorial, use the desktop app created in [Authenticate users with Azure Active Directory B2C in a desktop app tutorial](active-directory-b2c-tutorials-desktop-app.md).</span></span>

1. <span data-ttu-id="212eb-177">In the Azure portal, select **Azure AD B2C** from the services list and click **Applications** to view the registered app list.</span><span class="sxs-lookup"><span data-stu-id="212eb-177">In the Azure portal, select **Azure AD B2C** from the services list and click **Applications** to view the registered app list.</span></span>

2. <span data-ttu-id="212eb-178">Select **My Sample WPF App** from the app list and click **API access (Preview)** then **Add**.</span><span class="sxs-lookup"><span data-stu-id="212eb-178">Select **My Sample WPF App** from the app list and click **API access (Preview)** then **Add**.</span></span>

3. <span data-ttu-id="212eb-179">In the **Select API** dropdown, select your registered web API **My sample Node.js web API**.</span><span class="sxs-lookup"><span data-stu-id="212eb-179">In the **Select API** dropdown, select your registered web API **My sample Node.js web API**.</span></span>

4. <span data-ttu-id="212eb-180">In the **Select Scopes** dropdown, select the scopes you defined in the web API registration.</span><span class="sxs-lookup"><span data-stu-id="212eb-180">In the **Select Scopes** dropdown, select the scopes you defined in the web API registration.</span></span>

    ![selecting scopes for app](media/active-directory-b2c-tutorials-web-api/selecting-scopes-for-app.png)

5. <span data-ttu-id="212eb-182">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="212eb-182">Click **OK**.</span></span>

<span data-ttu-id="212eb-183">Your **My Sample WPF App** is registered to call the protected **My sample Node.js web API**.</span><span class="sxs-lookup"><span data-stu-id="212eb-183">Your **My Sample WPF App** is registered to call the protected **My sample Node.js web API**.</span></span> <span data-ttu-id="212eb-184">A user [authenticates](../active-directory/develop/developer-glossary.md#authentication) with Azure AD B2C to use the WPF deskop app app.</span><span class="sxs-lookup"><span data-stu-id="212eb-184">A user [authenticates](../active-directory/develop/developer-glossary.md#authentication) with Azure AD B2C to use the WPF deskop app app.</span></span> <span data-ttu-id="212eb-185">The desktop app obtains an [authorization grant](../active-directory/develop/developer-glossary.md#authorization-grant) from Azure AD B2C to access the protected web API.</span><span class="sxs-lookup"><span data-stu-id="212eb-185">The desktop app obtains an [authorization grant](../active-directory/develop/developer-glossary.md#authorization-grant) from Azure AD B2C to access the protected web API.</span></span>

## <a name="update-web-api-code"></a><span data-ttu-id="212eb-186">Update web API code</span><span class="sxs-lookup"><span data-stu-id="212eb-186">Update web API code</span></span>

<span data-ttu-id="212eb-187">Now that the web API is registered and you have scopes defined, you need to configure the web API code to use your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="212eb-187">Now that the web API is registered and you have scopes defined, you need to configure the web API code to use your Azure AD B2C tenant.</span></span> <span data-ttu-id="212eb-188">In this tutorial, you configure a sample Node.js web app you can download from GitHub.</span><span class="sxs-lookup"><span data-stu-id="212eb-188">In this tutorial, you configure a sample Node.js web app you can download from GitHub.</span></span> 

<span data-ttu-id="212eb-189">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi/archive/master.zip) or clone the sample web app from GitHub.</span><span class="sxs-lookup"><span data-stu-id="212eb-189">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi/archive/master.zip) or clone the sample web app from GitHub.</span></span>

```
git clone https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi.git
```
<span data-ttu-id="212eb-190">The Node.js web API sample uses the Passport.js library to enable Azure AD B2C to protect calls to the API.</span><span class="sxs-lookup"><span data-stu-id="212eb-190">The Node.js web API sample uses the Passport.js library to enable Azure AD B2C to protect calls to the API.</span></span> 

### <a name="configure-the-web-api"></a><span data-ttu-id="212eb-191">Configure the web API</span><span class="sxs-lookup"><span data-stu-id="212eb-191">Configure the web API</span></span>

1. <span data-ttu-id="212eb-192">Open the `index.html` file in the Node.js web API sample.</span><span class="sxs-lookup"><span data-stu-id="212eb-192">Open the `index.html` file in the Node.js web API sample.</span></span>
2. <span data-ttu-id="212eb-193">Configure the sample with the Azure AD B2C tenant registration information.</span><span class="sxs-lookup"><span data-stu-id="212eb-193">Configure the sample with the Azure AD B2C tenant registration information.</span></span> <span data-ttu-id="212eb-194">Change the following lines of code:</span><span class="sxs-lookup"><span data-stu-id="212eb-194">Change the following lines of code:</span></span>

```nodejs
var tenantID = "<your-tenant-name>.onmicrosoft.com";
var clientID = "<Application ID for your Node.js Web API>";
var policyName = "B2C_1_SiUpIn";  // Sign-in / sign-up policy name
```

### <a name="configure-the-desktop-app"></a><span data-ttu-id="212eb-195">Configure the desktop app</span><span class="sxs-lookup"><span data-stu-id="212eb-195">Configure the desktop app</span></span>

1. <span data-ttu-id="212eb-196">Open the `active-directory-b2c-wpf` solution from [Authenticate users with Azure Active Directory B2C in a desktop app tutorial](active-directory-b2c-tutorials-desktop-app.md) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="212eb-196">Open the `active-directory-b2c-wpf` solution from [Authenticate users with Azure Active Directory B2C in a desktop app tutorial](active-directory-b2c-tutorials-desktop-app.md) in Visual Studio.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="212eb-197">Run the sample</span><span class="sxs-lookup"><span data-stu-id="212eb-197">Run the sample</span></span>

<span data-ttu-id="212eb-198">Run the Node.js web API:</span><span class="sxs-lookup"><span data-stu-id="212eb-198">Run the Node.js web API:</span></span>

1. <span data-ttu-id="212eb-199">Launch a Node.js command prompt.</span><span class="sxs-lookup"><span data-stu-id="212eb-199">Launch a Node.js command prompt.</span></span>
2. <span data-ttu-id="212eb-200">Change to the directory containing the Node.js sample.</span><span class="sxs-lookup"><span data-stu-id="212eb-200">Change to the directory containing the Node.js sample.</span></span> <span data-ttu-id="212eb-201">For example `cd c:\active-directory-b2c-javascript-nodejs-webapi`</span><span class="sxs-lookup"><span data-stu-id="212eb-201">For example `cd c:\active-directory-b2c-javascript-nodejs-webapi`</span></span>
3. <span data-ttu-id="212eb-202">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="212eb-202">Run the following commands:</span></span>
    ```
    npm install && npm update
    ```
    ```
    node index.js
    ```
<span data-ttu-id="212eb-203">Run the desktop app:</span><span class="sxs-lookup"><span data-stu-id="212eb-203">Run the desktop app:</span></span>

1. <span data-ttu-id="212eb-204">Press **F5** to run the desktop app.</span><span class="sxs-lookup"><span data-stu-id="212eb-204">Press **F5** to run the desktop app.</span></span>
2. <span data-ttu-id="212eb-205">Sign in using the email address and password used in [Authenticate users with Azure Active Directory B2C in a desktop app tutorial](active-directory-b2c-tutorials-desktop-app.md).</span><span class="sxs-lookup"><span data-stu-id="212eb-205">Sign in using the email address and password used in [Authenticate users with Azure Active Directory B2C in a desktop app tutorial](active-directory-b2c-tutorials-desktop-app.md).</span></span>
3. <span data-ttu-id="212eb-206">Click the **Call API** button.</span><span class="sxs-lookup"><span data-stu-id="212eb-206">Click the **Call API** button.</span></span> 

<span data-ttu-id="212eb-207">The desktop app makes a request to the web API to and gets a response with the logged-in user's display name.</span><span class="sxs-lookup"><span data-stu-id="212eb-207">The desktop app makes a request to the web API to and gets a response with the logged-in user's display name.</span></span> <span data-ttu-id="212eb-208">You're protected desktop app is calling the protected web API in your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="212eb-208">You're protected desktop app is calling the protected web API in your Azure AD B2C tenant.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="212eb-209">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="212eb-209">Clean up resources</span></span>

<span data-ttu-id="212eb-210">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C tutorials.</span><span class="sxs-lookup"><span data-stu-id="212eb-210">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C tutorials.</span></span> <span data-ttu-id="212eb-211">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span><span class="sxs-lookup"><span data-stu-id="212eb-211">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="212eb-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="212eb-212">Next steps</span></span>

<span data-ttu-id="212eb-213">This article walked you through protecting a ASP.NET web API by registering and defining scopes in Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="212eb-213">This article walked you through protecting a ASP.NET web API by registering and defining scopes in Azure AD B2C.</span></span> <span data-ttu-id="212eb-214">Learn more by browsing the available Azure AD B2C code samples.</span><span class="sxs-lookup"><span data-stu-id="212eb-214">Learn more by browsing the available Azure AD B2C code samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="212eb-215">Azure AD B2C code samples</span><span class="sxs-lookup"><span data-stu-id="212eb-215">Azure AD B2C code samples</span></span>](https://azure.microsoft.com/resources/samples/?service=active-directory-b2c&sort=0)
