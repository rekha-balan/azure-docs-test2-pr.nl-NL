---
title: Tutorial - Enable single-page app authentication with accounts using Azure Active Directory B2C | Microsoft Docs
description: Tutorial on how to use Azure Active Directory B2C to provide user login for a single page application (JavaScript).
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.author: davidmu
ms.date: 3/02/2018
ms.custom: mvc
ms.topic: tutorial
ms.service: active-directory
ms.component: B2C
ms.openlocfilehash: 4953cb0db428de19268cdd90661f7818b06b6945
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967700"
---
# <a name="tutorial-enable-single-page-app-authentication-with-accounts-using-azure-active-directory-b2c"></a><span data-ttu-id="52a05-103">Tutorial: Enable single-page app authentication with accounts using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="52a05-103">Tutorial: Enable single-page app authentication with accounts using Azure Active Directory B2C</span></span>

<span data-ttu-id="52a05-104">This tutorial shows you how to use Azure Active Directory (Azure AD) B2C to sign in and sign up users in a single page application (SPA).</span><span class="sxs-lookup"><span data-stu-id="52a05-104">This tutorial shows you how to use Azure Active Directory (Azure AD) B2C to sign in and sign up users in a single page application (SPA).</span></span> <span data-ttu-id="52a05-105">Azure AD B2C enables your apps to authenticate to social accounts, enterprise accounts, and Azure Active Directory accounts using open standard protocols.</span><span class="sxs-lookup"><span data-stu-id="52a05-105">Azure AD B2C enables your apps to authenticate to social accounts, enterprise accounts, and Azure Active Directory accounts using open standard protocols.</span></span>

<span data-ttu-id="52a05-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="52a05-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52a05-107">Register a sample single page application in your Azure AD B2C directory.</span><span class="sxs-lookup"><span data-stu-id="52a05-107">Register a sample single page application in your Azure AD B2C directory.</span></span>
> * <span data-ttu-id="52a05-108">Create policies for user sign-up, sign-in, editing a profile, and password reset.</span><span class="sxs-lookup"><span data-stu-id="52a05-108">Create policies for user sign-up, sign-in, editing a profile, and password reset.</span></span>
> * <span data-ttu-id="52a05-109">Configure the sample application to use your Azure AD B2C directory.</span><span class="sxs-lookup"><span data-stu-id="52a05-109">Configure the sample application to use your Azure AD B2C directory.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="52a05-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="52a05-110">Prerequisites</span></span>

* <span data-ttu-id="52a05-111">Create your own [Azure AD B2C Directory](active-directory-b2c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="52a05-111">Create your own [Azure AD B2C Directory](active-directory-b2c-get-started.md)</span></span>
* <span data-ttu-id="52a05-112">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span><span class="sxs-lookup"><span data-stu-id="52a05-112">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span></span>
* <span data-ttu-id="52a05-113">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later</span><span class="sxs-lookup"><span data-stu-id="52a05-113">[.NET Core 2.0.0 SDK](https://www.microsoft.com/net/core) or later</span></span>
* <span data-ttu-id="52a05-114">Install [Node.js](https://nodejs.org/en/download/)</span><span class="sxs-lookup"><span data-stu-id="52a05-114">Install [Node.js](https://nodejs.org/en/download/)</span></span>

## <a name="register-single-page-app"></a><span data-ttu-id="52a05-115">Register single page app</span><span class="sxs-lookup"><span data-stu-id="52a05-115">Register single page app</span></span>

<span data-ttu-id="52a05-116">Applications need to be [registered](../active-directory/develop/developer-glossary.md#application-registration) in your directory before they can receive [access tokens](../active-directory/develop/developer-glossary.md#access-token) from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52a05-116">Applications need to be [registered](../active-directory/develop/developer-glossary.md#application-registration) in your directory before they can receive [access tokens](../active-directory/develop/developer-glossary.md#access-token) from Azure Active Directory.</span></span> <span data-ttu-id="52a05-117">App registration creates an [application id](../active-directory/develop/developer-glossary.md#application-id-client-id) for the app in your directory.</span><span class="sxs-lookup"><span data-stu-id="52a05-117">App registration creates an [application id](../active-directory/develop/developer-glossary.md#application-id-client-id) for the app in your directory.</span></span> 

<span data-ttu-id="52a05-118">Log in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C directory.</span><span class="sxs-lookup"><span data-stu-id="52a05-118">Log in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C directory.</span></span>

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

1. <span data-ttu-id="52a05-119">Select **Azure AD B2C** from the services list in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="52a05-119">Select **Azure AD B2C** from the services list in the Azure portal.</span></span> 

2. <span data-ttu-id="52a05-120">In the B2C settings, click **Applications** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="52a05-120">In the B2C settings, click **Applications** and then click **Add**.</span></span> 

    <span data-ttu-id="52a05-121">To register the sample web app in your directory, use the following settings:</span><span class="sxs-lookup"><span data-stu-id="52a05-121">To register the sample web app in your directory, use the following settings:</span></span>
    
    ![Add a new app](media/active-directory-b2c-tutorials-spa/spa-registration.png)
    
    | <span data-ttu-id="52a05-123">Setting</span><span class="sxs-lookup"><span data-stu-id="52a05-123">Setting</span></span>      | <span data-ttu-id="52a05-124">Suggested value</span><span class="sxs-lookup"><span data-stu-id="52a05-124">Suggested value</span></span>  | <span data-ttu-id="52a05-125">Description</span><span class="sxs-lookup"><span data-stu-id="52a05-125">Description</span></span>                                        |
    | ------------ | ------- | -------------------------------------------------- |
    | <span data-ttu-id="52a05-126">**Name**</span><span class="sxs-lookup"><span data-stu-id="52a05-126">**Name**</span></span> | <span data-ttu-id="52a05-127">My sample single page app</span><span class="sxs-lookup"><span data-stu-id="52a05-127">My sample single page app</span></span> | <span data-ttu-id="52a05-128">Enter a **Name** that describes your app to consumers.</span><span class="sxs-lookup"><span data-stu-id="52a05-128">Enter a **Name** that describes your app to consumers.</span></span> | 
    | <span data-ttu-id="52a05-129">**Include web app / web API**</span><span class="sxs-lookup"><span data-stu-id="52a05-129">**Include web app / web API**</span></span> | <span data-ttu-id="52a05-130">Yes</span><span class="sxs-lookup"><span data-stu-id="52a05-130">Yes</span></span> | <span data-ttu-id="52a05-131">Select **Yes** for a single page app.</span><span class="sxs-lookup"><span data-stu-id="52a05-131">Select **Yes** for a single page app.</span></span> |
    | <span data-ttu-id="52a05-132">**Allow implicit flow**</span><span class="sxs-lookup"><span data-stu-id="52a05-132">**Allow implicit flow**</span></span> | <span data-ttu-id="52a05-133">Yes</span><span class="sxs-lookup"><span data-stu-id="52a05-133">Yes</span></span> | <span data-ttu-id="52a05-134">Select **Yes** since the app uses [OpenID Connect sign-in](active-directory-b2c-reference-oidc.md).</span><span class="sxs-lookup"><span data-stu-id="52a05-134">Select **Yes** since the app uses [OpenID Connect sign-in](active-directory-b2c-reference-oidc.md).</span></span> |
    | <span data-ttu-id="52a05-135">**Reply URL**</span><span class="sxs-lookup"><span data-stu-id="52a05-135">**Reply URL**</span></span> | `http://localhost:6420` | <span data-ttu-id="52a05-136">Reply URLs are endpoints where Azure AD B2C returns any tokens that your app requests.</span><span class="sxs-lookup"><span data-stu-id="52a05-136">Reply URLs are endpoints where Azure AD B2C returns any tokens that your app requests.</span></span> <span data-ttu-id="52a05-137">In this tutorial, the sample runs locally (localhost) and listens on port 6420.</span><span class="sxs-lookup"><span data-stu-id="52a05-137">In this tutorial, the sample runs locally (localhost) and listens on port 6420.</span></span> |
    | <span data-ttu-id="52a05-138">**Include native client**</span><span class="sxs-lookup"><span data-stu-id="52a05-138">**Include native client**</span></span> | <span data-ttu-id="52a05-139">No</span><span class="sxs-lookup"><span data-stu-id="52a05-139">No</span></span> | <span data-ttu-id="52a05-140">Since this is a single page app and not a native client, select No.</span><span class="sxs-lookup"><span data-stu-id="52a05-140">Since this is a single page app and not a native client, select No.</span></span> |
    
3. <span data-ttu-id="52a05-141">Click **Create** to register your app.</span><span class="sxs-lookup"><span data-stu-id="52a05-141">Click **Create** to register your app.</span></span>

<span data-ttu-id="52a05-142">Registered apps are displayed in the applications list for the Azure AD B2C directory.</span><span class="sxs-lookup"><span data-stu-id="52a05-142">Registered apps are displayed in the applications list for the Azure AD B2C directory.</span></span> <span data-ttu-id="52a05-143">Select your single page app from the list.</span><span class="sxs-lookup"><span data-stu-id="52a05-143">Select your single page app from the list.</span></span> <span data-ttu-id="52a05-144">The registered single page app's property pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="52a05-144">The registered single page app's property pane is displayed.</span></span>

![Single page app properties](./media/active-directory-b2c-tutorials-spa/b2c-spa-properties.png)

<span data-ttu-id="52a05-146">Make note of the **Application Client ID**.</span><span class="sxs-lookup"><span data-stu-id="52a05-146">Make note of the **Application Client ID**.</span></span> <span data-ttu-id="52a05-147">The ID uniquely identifies the app and is needed when configuring the app later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="52a05-147">The ID uniquely identifies the app and is needed when configuring the app later in the tutorial.</span></span>

## <a name="create-policies"></a><span data-ttu-id="52a05-148">Create policies</span><span class="sxs-lookup"><span data-stu-id="52a05-148">Create policies</span></span>

<span data-ttu-id="52a05-149">An Azure AD B2C policy defines user workflows.</span><span class="sxs-lookup"><span data-stu-id="52a05-149">An Azure AD B2C policy defines user workflows.</span></span> <span data-ttu-id="52a05-150">For example, signing in, signing up, changing passwords, and editing profiles are common workflows.</span><span class="sxs-lookup"><span data-stu-id="52a05-150">For example, signing in, signing up, changing passwords, and editing profiles are common workflows.</span></span>

### <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="52a05-151">Create a sign-up or sign-in policy</span><span class="sxs-lookup"><span data-stu-id="52a05-151">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="52a05-152">To sign up users to access then sign in to the web app, create a **sign-up or sign-in policy**.</span><span class="sxs-lookup"><span data-stu-id="52a05-152">To sign up users to access then sign in to the web app, create a **sign-up or sign-in policy**.</span></span>

1. <span data-ttu-id="52a05-153">From the Azure AD B2C portal page, select **Sign-up or sign-in policies** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="52a05-153">From the Azure AD B2C portal page, select **Sign-up or sign-in policies** and click **Add**.</span></span>

    <span data-ttu-id="52a05-154">To configure your policy, use the following settings:</span><span class="sxs-lookup"><span data-stu-id="52a05-154">To configure your policy, use the following settings:</span></span>

    ![Add a sign-up or sign-in policy](media/active-directory-b2c-tutorials-web-app/add-susi-policy.png)

    | <span data-ttu-id="52a05-156">Setting</span><span class="sxs-lookup"><span data-stu-id="52a05-156">Setting</span></span>      | <span data-ttu-id="52a05-157">Suggested value</span><span class="sxs-lookup"><span data-stu-id="52a05-157">Suggested value</span></span>  | <span data-ttu-id="52a05-158">Description</span><span class="sxs-lookup"><span data-stu-id="52a05-158">Description</span></span>                                        |
    | ------------ | ------- | -------------------------------------------------- |
    | <span data-ttu-id="52a05-159">**Name**</span><span class="sxs-lookup"><span data-stu-id="52a05-159">**Name**</span></span> | <span data-ttu-id="52a05-160">SiUpIn</span><span class="sxs-lookup"><span data-stu-id="52a05-160">SiUpIn</span></span> | <span data-ttu-id="52a05-161">Enter a **Name** for the policy.</span><span class="sxs-lookup"><span data-stu-id="52a05-161">Enter a **Name** for the policy.</span></span> <span data-ttu-id="52a05-162">The policy name is prefixed with **B2C_1_**.</span><span class="sxs-lookup"><span data-stu-id="52a05-162">The policy name is prefixed with **B2C_1_**.</span></span> <span data-ttu-id="52a05-163">You use the full policy name **B2C_1_SiUpIn** in the sample code.</span><span class="sxs-lookup"><span data-stu-id="52a05-163">You use the full policy name **B2C_1_SiUpIn** in the sample code.</span></span> | 
    | <span data-ttu-id="52a05-164">**Identity provider**</span><span class="sxs-lookup"><span data-stu-id="52a05-164">**Identity provider**</span></span> | <span data-ttu-id="52a05-165">Email signup</span><span class="sxs-lookup"><span data-stu-id="52a05-165">Email signup</span></span> | <span data-ttu-id="52a05-166">The identity provider used to uniquely identify the user.</span><span class="sxs-lookup"><span data-stu-id="52a05-166">The identity provider used to uniquely identify the user.</span></span> |
    | <span data-ttu-id="52a05-167">**Sign up attributes**</span><span class="sxs-lookup"><span data-stu-id="52a05-167">**Sign up attributes**</span></span> | <span data-ttu-id="52a05-168">Display Name and Postal Code</span><span class="sxs-lookup"><span data-stu-id="52a05-168">Display Name and Postal Code</span></span> | <span data-ttu-id="52a05-169">Select attributes to be collected from the user during signup.</span><span class="sxs-lookup"><span data-stu-id="52a05-169">Select attributes to be collected from the user during signup.</span></span> |
    | <span data-ttu-id="52a05-170">**Application claims**</span><span class="sxs-lookup"><span data-stu-id="52a05-170">**Application claims**</span></span> | <span data-ttu-id="52a05-171">Display Name, Postal Code, User is new, User's Object ID</span><span class="sxs-lookup"><span data-stu-id="52a05-171">Display Name, Postal Code, User is new, User's Object ID</span></span> | <span data-ttu-id="52a05-172">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token).</span><span class="sxs-lookup"><span data-stu-id="52a05-172">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token).</span></span> |

2. <span data-ttu-id="52a05-173">Click **Create** to create your policy.</span><span class="sxs-lookup"><span data-stu-id="52a05-173">Click **Create** to create your policy.</span></span> 

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="52a05-174">Create a profile editing policy</span><span class="sxs-lookup"><span data-stu-id="52a05-174">Create a profile editing policy</span></span>

<span data-ttu-id="52a05-175">To allow users to reset their user profile information on their own, create a **profile editing policy**.</span><span class="sxs-lookup"><span data-stu-id="52a05-175">To allow users to reset their user profile information on their own, create a **profile editing policy**.</span></span>

1. <span data-ttu-id="52a05-176">From the Azure AD B2C portal page, select **Profile editing policies** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="52a05-176">From the Azure AD B2C portal page, select **Profile editing policies** and click **Add**.</span></span>

    <span data-ttu-id="52a05-177">To configure your policy, use the following settings:</span><span class="sxs-lookup"><span data-stu-id="52a05-177">To configure your policy, use the following settings:</span></span>

    | <span data-ttu-id="52a05-178">Setting</span><span class="sxs-lookup"><span data-stu-id="52a05-178">Setting</span></span>      | <span data-ttu-id="52a05-179">Suggested value</span><span class="sxs-lookup"><span data-stu-id="52a05-179">Suggested value</span></span>  | <span data-ttu-id="52a05-180">Description</span><span class="sxs-lookup"><span data-stu-id="52a05-180">Description</span></span>                                        |
    | ------------ | ------- | -------------------------------------------------- |
    | <span data-ttu-id="52a05-181">**Name**</span><span class="sxs-lookup"><span data-stu-id="52a05-181">**Name**</span></span> | <span data-ttu-id="52a05-182">SiPe</span><span class="sxs-lookup"><span data-stu-id="52a05-182">SiPe</span></span> | <span data-ttu-id="52a05-183">Enter a **Name** for the policy.</span><span class="sxs-lookup"><span data-stu-id="52a05-183">Enter a **Name** for the policy.</span></span> <span data-ttu-id="52a05-184">The policy name is prefixed with **B2C_1_**.</span><span class="sxs-lookup"><span data-stu-id="52a05-184">The policy name is prefixed with **B2C_1_**.</span></span> <span data-ttu-id="52a05-185">You use the full policy name **B2C_1_SiPe** in the sample code.</span><span class="sxs-lookup"><span data-stu-id="52a05-185">You use the full policy name **B2C_1_SiPe** in the sample code.</span></span> | 
    | <span data-ttu-id="52a05-186">**Identity provider**</span><span class="sxs-lookup"><span data-stu-id="52a05-186">**Identity provider**</span></span> | <span data-ttu-id="52a05-187">Local Account SignIn</span><span class="sxs-lookup"><span data-stu-id="52a05-187">Local Account SignIn</span></span> | <span data-ttu-id="52a05-188">The identity provider used to uniquely identify the user.</span><span class="sxs-lookup"><span data-stu-id="52a05-188">The identity provider used to uniquely identify the user.</span></span> |
    | <span data-ttu-id="52a05-189">**Profile attributes**</span><span class="sxs-lookup"><span data-stu-id="52a05-189">**Profile attributes**</span></span> | <span data-ttu-id="52a05-190">Display Name and Postal Code</span><span class="sxs-lookup"><span data-stu-id="52a05-190">Display Name and Postal Code</span></span> | <span data-ttu-id="52a05-191">Select attributes users can modify during profile edit.</span><span class="sxs-lookup"><span data-stu-id="52a05-191">Select attributes users can modify during profile edit.</span></span> |
    | <span data-ttu-id="52a05-192">**Application claims**</span><span class="sxs-lookup"><span data-stu-id="52a05-192">**Application claims**</span></span> | <span data-ttu-id="52a05-193">Display Name, Postal Code, User's Object ID</span><span class="sxs-lookup"><span data-stu-id="52a05-193">Display Name, Postal Code, User's Object ID</span></span> | <span data-ttu-id="52a05-194">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token) after a successful profile edit.</span><span class="sxs-lookup"><span data-stu-id="52a05-194">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token) after a successful profile edit.</span></span> |

2. <span data-ttu-id="52a05-195">Click **Create** to create your policy.</span><span class="sxs-lookup"><span data-stu-id="52a05-195">Click **Create** to create your policy.</span></span> 

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="52a05-196">Create a password reset policy</span><span class="sxs-lookup"><span data-stu-id="52a05-196">Create a password reset policy</span></span>

<span data-ttu-id="52a05-197">To enable password reset on your application, you need to create a **password reset policy**.</span><span class="sxs-lookup"><span data-stu-id="52a05-197">To enable password reset on your application, you need to create a **password reset policy**.</span></span> <span data-ttu-id="52a05-198">This policy describes the consumer experience during password reset and the contents of tokens that the application receives on successful completion.</span><span class="sxs-lookup"><span data-stu-id="52a05-198">This policy describes the consumer experience during password reset and the contents of tokens that the application receives on successful completion.</span></span>

1. <span data-ttu-id="52a05-199">From the Azure AD B2C portal page, select **Password reset policies** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="52a05-199">From the Azure AD B2C portal page, select **Password reset policies** and click **Add**.</span></span>

    <span data-ttu-id="52a05-200">To configure your policy, use the following settings.</span><span class="sxs-lookup"><span data-stu-id="52a05-200">To configure your policy, use the following settings.</span></span>

    | <span data-ttu-id="52a05-201">Setting</span><span class="sxs-lookup"><span data-stu-id="52a05-201">Setting</span></span>      | <span data-ttu-id="52a05-202">Suggested value</span><span class="sxs-lookup"><span data-stu-id="52a05-202">Suggested value</span></span>  | <span data-ttu-id="52a05-203">Description</span><span class="sxs-lookup"><span data-stu-id="52a05-203">Description</span></span>                                        |
    | ------------ | ------- | -------------------------------------------------- |
    | <span data-ttu-id="52a05-204">**Name**</span><span class="sxs-lookup"><span data-stu-id="52a05-204">**Name**</span></span> | <span data-ttu-id="52a05-205">SSPR</span><span class="sxs-lookup"><span data-stu-id="52a05-205">SSPR</span></span> | <span data-ttu-id="52a05-206">Enter a **Name** for the policy.</span><span class="sxs-lookup"><span data-stu-id="52a05-206">Enter a **Name** for the policy.</span></span> <span data-ttu-id="52a05-207">The policy name is prefixed with **B2C_1_**.</span><span class="sxs-lookup"><span data-stu-id="52a05-207">The policy name is prefixed with **B2C_1_**.</span></span> <span data-ttu-id="52a05-208">You use the full policy name **B2C_1_SSPR** in the sample code.</span><span class="sxs-lookup"><span data-stu-id="52a05-208">You use the full policy name **B2C_1_SSPR** in the sample code.</span></span> | 
    | <span data-ttu-id="52a05-209">**Identity provider**</span><span class="sxs-lookup"><span data-stu-id="52a05-209">**Identity provider**</span></span> | <span data-ttu-id="52a05-210">Reset password using email address</span><span class="sxs-lookup"><span data-stu-id="52a05-210">Reset password using email address</span></span> | <span data-ttu-id="52a05-211">This is the identity provider used to uniquely identify the user.</span><span class="sxs-lookup"><span data-stu-id="52a05-211">This is the identity provider used to uniquely identify the user.</span></span> |
    | <span data-ttu-id="52a05-212">**Application claims**</span><span class="sxs-lookup"><span data-stu-id="52a05-212">**Application claims**</span></span> | <span data-ttu-id="52a05-213">User's Object ID</span><span class="sxs-lookup"><span data-stu-id="52a05-213">User's Object ID</span></span> | <span data-ttu-id="52a05-214">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token) after a successful password reset.</span><span class="sxs-lookup"><span data-stu-id="52a05-214">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token) after a successful password reset.</span></span> |

2. <span data-ttu-id="52a05-215">Click **Create** to create your policy.</span><span class="sxs-lookup"><span data-stu-id="52a05-215">Click **Create** to create your policy.</span></span> 

## <a name="update-single-page-app-code"></a><span data-ttu-id="52a05-216">Update single page app code</span><span class="sxs-lookup"><span data-stu-id="52a05-216">Update single page app code</span></span>

<span data-ttu-id="52a05-217">Now that you have an app registered and policies created, you need to configure your app to use your Azure AD B2C directory.</span><span class="sxs-lookup"><span data-stu-id="52a05-217">Now that you have an app registered and policies created, you need to configure your app to use your Azure AD B2C directory.</span></span> <span data-ttu-id="52a05-218">In this tutorial, you configure a sample SPA JavaScript app you can download from GitHub.</span><span class="sxs-lookup"><span data-stu-id="52a05-218">In this tutorial, you configure a sample SPA JavaScript app you can download from GitHub.</span></span> 

<span data-ttu-id="52a05-219">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp/archive/master.zip) or clone the sample web app from GitHub.</span><span class="sxs-lookup"><span data-stu-id="52a05-219">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp/archive/master.zip) or clone the sample web app from GitHub.</span></span>

```
git clone https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp.git
```
<span data-ttu-id="52a05-220">The sample app demonstrates how a single page app can use Azure AD B2C for user sign-up, sign-in, and call a protected web API.</span><span class="sxs-lookup"><span data-stu-id="52a05-220">The sample app demonstrates how a single page app can use Azure AD B2C for user sign-up, sign-in, and call a protected web API.</span></span> <span data-ttu-id="52a05-221">You need to change the app to use the app registration in your directory and configure the policies you created.</span><span class="sxs-lookup"><span data-stu-id="52a05-221">You need to change the app to use the app registration in your directory and configure the policies you created.</span></span> 

<span data-ttu-id="52a05-222">To change the app settings:</span><span class="sxs-lookup"><span data-stu-id="52a05-222">To change the app settings:</span></span>

1. <span data-ttu-id="52a05-223">Open the `index.html` file in the Node.js single page app sample.</span><span class="sxs-lookup"><span data-stu-id="52a05-223">Open the `index.html` file in the Node.js single page app sample.</span></span>
2. <span data-ttu-id="52a05-224">Configure the sample with the Azure AD B2C directory registration information.</span><span class="sxs-lookup"><span data-stu-id="52a05-224">Configure the sample with the Azure AD B2C directory registration information.</span></span> <span data-ttu-id="52a05-225">Change the following lines of code (make sure to replace the values with the names of your directory and APIs):</span><span class="sxs-lookup"><span data-stu-id="52a05-225">Change the following lines of code (make sure to replace the values with the names of your directory and APIs):</span></span>

    ```javascript
    // The current application coordinates were pre-registered in a B2C directory.
    var applicationConfig = {
        clientID: '<Application ID for your SPA obtained from portal app registration>',
        authority: "https://fabrikamb2c.b2clogin.com/tfp/fabrikamb2c.onmicrosoft.com/B2C_1_SiUpIn",
        b2cScopes: ["https://fabrikamb2c.onmicrosoft.com/demoapi/demo.read"],
        webApi: 'https://fabrikamb2chello.azurewebsites.net/hello',
    };
    ```

    <span data-ttu-id="52a05-226">The policy name used in this tutorial is **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="52a05-226">The policy name used in this tutorial is **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="52a05-227">If you are using a different policy name, use your policy name in `authority` value.</span><span class="sxs-lookup"><span data-stu-id="52a05-227">If you are using a different policy name, use your policy name in `authority` value.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="52a05-228">Run the sample</span><span class="sxs-lookup"><span data-stu-id="52a05-228">Run the sample</span></span>

1. <span data-ttu-id="52a05-229">Launch a Node.js command prompt.</span><span class="sxs-lookup"><span data-stu-id="52a05-229">Launch a Node.js command prompt.</span></span>
2. <span data-ttu-id="52a05-230">Change to the directory containing the Node.js sample.</span><span class="sxs-lookup"><span data-stu-id="52a05-230">Change to the directory containing the Node.js sample.</span></span> <span data-ttu-id="52a05-231">For example `cd c:\active-directory-b2c-javascript-msal-singlepageapp`</span><span class="sxs-lookup"><span data-stu-id="52a05-231">For example `cd c:\active-directory-b2c-javascript-msal-singlepageapp`</span></span>
3. <span data-ttu-id="52a05-232">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="52a05-232">Run the following commands:</span></span>
    ```
    npm install && npm update
    node server.js
    ```

    <span data-ttu-id="52a05-233">The console window displays the port number of where the app is hosted.</span><span class="sxs-lookup"><span data-stu-id="52a05-233">The console window displays the port number of where the app is hosted.</span></span>
    
    ```
    Listening on port 6420...
    ```

4. <span data-ttu-id="52a05-234">Use a browser to navigate to the address `http://localhost:6420` to view the app.</span><span class="sxs-lookup"><span data-stu-id="52a05-234">Use a browser to navigate to the address `http://localhost:6420` to view the app.</span></span>

<span data-ttu-id="52a05-235">The sample app supports sign up, sign in, editing a profile, and password reset.</span><span class="sxs-lookup"><span data-stu-id="52a05-235">The sample app supports sign up, sign in, editing a profile, and password reset.</span></span> <span data-ttu-id="52a05-236">This tutorial highlights how a user signs up to use the app using an email address.</span><span class="sxs-lookup"><span data-stu-id="52a05-236">This tutorial highlights how a user signs up to use the app using an email address.</span></span> <span data-ttu-id="52a05-237">You can explore other scenarios on your own.</span><span class="sxs-lookup"><span data-stu-id="52a05-237">You can explore other scenarios on your own.</span></span>

### <a name="sign-up-using-an-email-address"></a><span data-ttu-id="52a05-238">Sign up using an email address</span><span class="sxs-lookup"><span data-stu-id="52a05-238">Sign up using an email address</span></span>

1. <span data-ttu-id="52a05-239">Click **Login** to sign up as a user of the SPA app.</span><span class="sxs-lookup"><span data-stu-id="52a05-239">Click **Login** to sign up as a user of the SPA app.</span></span> <span data-ttu-id="52a05-240">This uses the **B2C_1_SiUpIn** policy you defined in a previous step.</span><span class="sxs-lookup"><span data-stu-id="52a05-240">This uses the **B2C_1_SiUpIn** policy you defined in a previous step.</span></span>

2. <span data-ttu-id="52a05-241">Azure AD B2C presents a sign-in page with a sign-up link.</span><span class="sxs-lookup"><span data-stu-id="52a05-241">Azure AD B2C presents a sign-in page with a sign-up link.</span></span> <span data-ttu-id="52a05-242">Since you don't have an account yet, click the **Sign up now** link.</span><span class="sxs-lookup"><span data-stu-id="52a05-242">Since you don't have an account yet, click the **Sign up now** link.</span></span> 

3. <span data-ttu-id="52a05-243">The sign-up workflow presents a page to collect and verify the user's identity using an email address.</span><span class="sxs-lookup"><span data-stu-id="52a05-243">The sign-up workflow presents a page to collect and verify the user's identity using an email address.</span></span> <span data-ttu-id="52a05-244">The sign-up workflow also collects the user's password and the requested attributes defined in the policy.</span><span class="sxs-lookup"><span data-stu-id="52a05-244">The sign-up workflow also collects the user's password and the requested attributes defined in the policy.</span></span>

    <span data-ttu-id="52a05-245">Use a valid email address and validate using the verification code.</span><span class="sxs-lookup"><span data-stu-id="52a05-245">Use a valid email address and validate using the verification code.</span></span> <span data-ttu-id="52a05-246">Set a password.</span><span class="sxs-lookup"><span data-stu-id="52a05-246">Set a password.</span></span> <span data-ttu-id="52a05-247">Enter values for the requested attributes.</span><span class="sxs-lookup"><span data-stu-id="52a05-247">Enter values for the requested attributes.</span></span> 

    ![Sign-up workflow](media/active-directory-b2c-tutorials-desktop-app/sign-up-workflow.png)

4. <span data-ttu-id="52a05-249">Click **Create** to create a local account in the Azure AD B2C directory.</span><span class="sxs-lookup"><span data-stu-id="52a05-249">Click **Create** to create a local account in the Azure AD B2C directory.</span></span>

<span data-ttu-id="52a05-250">Now, the user can use their email address to sign in and use the SPA app.</span><span class="sxs-lookup"><span data-stu-id="52a05-250">Now, the user can use their email address to sign in and use the SPA app.</span></span>

> [!NOTE]
> <span data-ttu-id="52a05-251">After login, the app displays an "insufficient permissions" error.</span><span class="sxs-lookup"><span data-stu-id="52a05-251">After login, the app displays an "insufficient permissions" error.</span></span> <span data-ttu-id="52a05-252">You receive this error because you are attempting to access a resource from the demo directory.</span><span class="sxs-lookup"><span data-stu-id="52a05-252">You receive this error because you are attempting to access a resource from the demo directory.</span></span> <span data-ttu-id="52a05-253">Since your access token is only valid for your Azure AD directory, the API call is unauthorized.</span><span class="sxs-lookup"><span data-stu-id="52a05-253">Since your access token is only valid for your Azure AD directory, the API call is unauthorized.</span></span> <span data-ttu-id="52a05-254">Continue with the next tutorial to create a protected web API for your directory.</span><span class="sxs-lookup"><span data-stu-id="52a05-254">Continue with the next tutorial to create a protected web API for your directory.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="52a05-255">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="52a05-255">Clean up resources</span></span>

<span data-ttu-id="52a05-256">You can use your Azure AD B2C directory if you plan to try other Azure AD B2C tutorials.</span><span class="sxs-lookup"><span data-stu-id="52a05-256">You can use your Azure AD B2C directory if you plan to try other Azure AD B2C tutorials.</span></span> <span data-ttu-id="52a05-257">When no longer needed, you can [delete your Azure AD B2C directory](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span><span class="sxs-lookup"><span data-stu-id="52a05-257">When no longer needed, you can [delete your Azure AD B2C directory](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="52a05-258">Next steps</span><span class="sxs-lookup"><span data-stu-id="52a05-258">Next steps</span></span>

<span data-ttu-id="52a05-259">In this tutorial, you learned how to create an Azure AD B2C directory, create policies, and update the sample single page app to use your Azure AD B2C directory.</span><span class="sxs-lookup"><span data-stu-id="52a05-259">In this tutorial, you learned how to create an Azure AD B2C directory, create policies, and update the sample single page app to use your Azure AD B2C directory.</span></span> <span data-ttu-id="52a05-260">Continue to the next tutorial to learn how to register, configure, and call a protected web API from a desktop app.</span><span class="sxs-lookup"><span data-stu-id="52a05-260">Continue to the next tutorial to learn how to register, configure, and call a protected web API from a desktop app.</span></span>

> [!div class="nextstepaction"]
> 
