---
title: Tutorial - Enable desktop app authentication with accounts using Azure Active Directory B2C | Microsoft Docs
description: Tutorial on how to use Azure Active Directory B2C to provide user login for a .NET desktop app.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.author: davidmu
ms.date: 2/28/2018
ms.custom: mvc
ms.topic: tutorial
ms.service: active-directory
ms.component: B2C
ms.openlocfilehash: 18db911782e03d17f0b2e2ace3f8b00ddfdebf70
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869294"
---
# <a name="tutorial-enable-desktop-app-authentication-with-accounts-using-azure-active-directory-b2c"></a><span data-ttu-id="a0384-103">Tutorial: Enable desktop app authentication with accounts using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="a0384-103">Tutorial: Enable desktop app authentication with accounts using Azure Active Directory B2C</span></span>

<span data-ttu-id="a0384-104">This tutorial shows you how to use Azure Active Directory (Azure AD) B2C to sign in and sign up users in an Windows Presentation Foundation (WPF) desktop application.</span><span class="sxs-lookup"><span data-stu-id="a0384-104">This tutorial shows you how to use Azure Active Directory (Azure AD) B2C to sign in and sign up users in an Windows Presentation Foundation (WPF) desktop application.</span></span> <span data-ttu-id="a0384-105">Azure AD B2C enables your apps to authenticate to social accounts, enterprise accounts, and Azure Active Directory accounts using open standard protocols.</span><span class="sxs-lookup"><span data-stu-id="a0384-105">Azure AD B2C enables your apps to authenticate to social accounts, enterprise accounts, and Azure Active Directory accounts using open standard protocols.</span></span>

<span data-ttu-id="a0384-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="a0384-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a0384-107">Register the sample desktop app in your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="a0384-107">Register the sample desktop app in your Azure AD B2C tenant.</span></span>
> * <span data-ttu-id="a0384-108">Create policies for user sign-up, sign-in, editing a profile, and password reset.</span><span class="sxs-lookup"><span data-stu-id="a0384-108">Create policies for user sign-up, sign-in, editing a profile, and password reset.</span></span>
> * <span data-ttu-id="a0384-109">Configure the sample application to use your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="a0384-109">Configure the sample application to use your Azure AD B2C tenant.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="a0384-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a0384-110">Prerequisites</span></span>

* <span data-ttu-id="a0384-111">Create your own [Azure AD B2C Tenant](active-directory-b2c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a0384-111">Create your own [Azure AD B2C Tenant](active-directory-b2c-get-started.md)</span></span>
* <span data-ttu-id="a0384-112">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with **.NET desktop development** and **ASP.NET and web development** workloads.</span><span class="sxs-lookup"><span data-stu-id="a0384-112">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with **.NET desktop development** and **ASP.NET and web development** workloads.</span></span>

## <a name="register-desktop-app"></a><span data-ttu-id="a0384-113">Register desktop app</span><span class="sxs-lookup"><span data-stu-id="a0384-113">Register desktop app</span></span>

<span data-ttu-id="a0384-114">Applications need to be [registered](../active-directory/develop/developer-glossary.md#application-registration) in your tenant before they can receive [access tokens](../active-directory/develop/developer-glossary.md#access-token) from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a0384-114">Applications need to be [registered](../active-directory/develop/developer-glossary.md#application-registration) in your tenant before they can receive [access tokens](../active-directory/develop/developer-glossary.md#access-token) from Azure Active Directory.</span></span> <span data-ttu-id="a0384-115">App registration creates an [application id](../active-directory/develop/developer-glossary.md#application-id-client-id) for the app in your tenant.</span><span class="sxs-lookup"><span data-stu-id="a0384-115">App registration creates an [application id](../active-directory/develop/developer-glossary.md#application-id-client-id) for the app in your tenant.</span></span> 

<span data-ttu-id="a0384-116">Log in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="a0384-116">Log in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

1. <span data-ttu-id="a0384-117">Select **Azure AD B2C** from the services list in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a0384-117">Select **Azure AD B2C** from the services list in the Azure portal.</span></span> 

2. <span data-ttu-id="a0384-118">In the B2C settings, click **Applications** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a0384-118">In the B2C settings, click **Applications** and then click **Add**.</span></span> 

    <span data-ttu-id="a0384-119">To register the sample web app in your tenant, use the following settings:</span><span class="sxs-lookup"><span data-stu-id="a0384-119">To register the sample web app in your tenant, use the following settings:</span></span>
    
    ![Add a new app](media/active-directory-b2c-tutorials-desktop-app/desktop-app-registration.png)
    
    | <span data-ttu-id="a0384-121">Setting</span><span class="sxs-lookup"><span data-stu-id="a0384-121">Setting</span></span>      | <span data-ttu-id="a0384-122">Suggested value</span><span class="sxs-lookup"><span data-stu-id="a0384-122">Suggested value</span></span>  | <span data-ttu-id="a0384-123">Description</span><span class="sxs-lookup"><span data-stu-id="a0384-123">Description</span></span>                                        |
    | ------------ | ------- | -------------------------------------------------- |
    | <span data-ttu-id="a0384-124">**Name**</span><span class="sxs-lookup"><span data-stu-id="a0384-124">**Name**</span></span> | <span data-ttu-id="a0384-125">My Sample WPF App</span><span class="sxs-lookup"><span data-stu-id="a0384-125">My Sample WPF App</span></span> | <span data-ttu-id="a0384-126">Enter a **Name** that describes your app to consumers.</span><span class="sxs-lookup"><span data-stu-id="a0384-126">Enter a **Name** that describes your app to consumers.</span></span> | 
    | <span data-ttu-id="a0384-127">**Include web app / web API**</span><span class="sxs-lookup"><span data-stu-id="a0384-127">**Include web app / web API**</span></span> | <span data-ttu-id="a0384-128">No</span><span class="sxs-lookup"><span data-stu-id="a0384-128">No</span></span> | <span data-ttu-id="a0384-129">Select **No** for a desktop app.</span><span class="sxs-lookup"><span data-stu-id="a0384-129">Select **No** for a desktop app.</span></span> |
    | <span data-ttu-id="a0384-130">**Include native client**</span><span class="sxs-lookup"><span data-stu-id="a0384-130">**Include native client**</span></span> | <span data-ttu-id="a0384-131">Yes</span><span class="sxs-lookup"><span data-stu-id="a0384-131">Yes</span></span> | <span data-ttu-id="a0384-132">Since this is a desktop app and is considered a native client.</span><span class="sxs-lookup"><span data-stu-id="a0384-132">Since this is a desktop app and is considered a native client.</span></span> |
    | <span data-ttu-id="a0384-133">**Redirect URI**</span><span class="sxs-lookup"><span data-stu-id="a0384-133">**Redirect URI**</span></span> | <span data-ttu-id="a0384-134">Default values</span><span class="sxs-lookup"><span data-stu-id="a0384-134">Default values</span></span> | <span data-ttu-id="a0384-135">Unique identifier to which Azure AD B2C redirects the user agent in an OAuth 2.0 response.</span><span class="sxs-lookup"><span data-stu-id="a0384-135">Unique identifier to which Azure AD B2C redirects the user agent in an OAuth 2.0 response.</span></span> |
    | <span data-ttu-id="a0384-136">**Custom Redirect URI**</span><span class="sxs-lookup"><span data-stu-id="a0384-136">**Custom Redirect URI**</span></span> | `com.onmicrosoft.contoso.appname://redirect/path` | <span data-ttu-id="a0384-137">Enter `com.onmicrosoft.<your tenant name>.<any app name>://redirect/path` Policies send tokens to this URI.</span><span class="sxs-lookup"><span data-stu-id="a0384-137">Enter `com.onmicrosoft.<your tenant name>.<any app name>://redirect/path` Policies send tokens to this URI.</span></span> |
    
3. <span data-ttu-id="a0384-138">Click **Create** to register your app.</span><span class="sxs-lookup"><span data-stu-id="a0384-138">Click **Create** to register your app.</span></span>

<span data-ttu-id="a0384-139">Registered apps are displayed in the applications list for the Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="a0384-139">Registered apps are displayed in the applications list for the Azure AD B2C tenant.</span></span> <span data-ttu-id="a0384-140">Select your desktop app from the list.</span><span class="sxs-lookup"><span data-stu-id="a0384-140">Select your desktop app from the list.</span></span> <span data-ttu-id="a0384-141">The registered desktop app's property pane is displayed.</span><span class="sxs-lookup"><span data-stu-id="a0384-141">The registered desktop app's property pane is displayed.</span></span>

![Desktop app properties](./media/active-directory-b2c-tutorials-desktop-app/b2c-desktop-app-properties.png)

<span data-ttu-id="a0384-143">Make note of the **Application Client ID**.</span><span class="sxs-lookup"><span data-stu-id="a0384-143">Make note of the **Application Client ID**.</span></span> <span data-ttu-id="a0384-144">The ID uniquely identifies the app and is needed when configuring the app later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="a0384-144">The ID uniquely identifies the app and is needed when configuring the app later in the tutorial.</span></span>

## <a name="create-policies"></a><span data-ttu-id="a0384-145">Create policies</span><span class="sxs-lookup"><span data-stu-id="a0384-145">Create policies</span></span>

<span data-ttu-id="a0384-146">An Azure AD B2C policy defines user workflows.</span><span class="sxs-lookup"><span data-stu-id="a0384-146">An Azure AD B2C policy defines user workflows.</span></span> <span data-ttu-id="a0384-147">For example, signing in, signing up, changing passwords, and editing profiles are common workflows.</span><span class="sxs-lookup"><span data-stu-id="a0384-147">For example, signing in, signing up, changing passwords, and editing profiles are common workflows.</span></span>

### <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="a0384-148">Create a sign-up or sign-in policy</span><span class="sxs-lookup"><span data-stu-id="a0384-148">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="a0384-149">To sign up users to access then sign in to the desktop app, create a **sign-up or sign-in policy**.</span><span class="sxs-lookup"><span data-stu-id="a0384-149">To sign up users to access then sign in to the desktop app, create a **sign-up or sign-in policy**.</span></span>

1. <span data-ttu-id="a0384-150">From the Azure AD B2C portal page, select **Sign-up or sign-in policies** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a0384-150">From the Azure AD B2C portal page, select **Sign-up or sign-in policies** and click **Add**.</span></span>

    <span data-ttu-id="a0384-151">To configure your policy, use the following settings:</span><span class="sxs-lookup"><span data-stu-id="a0384-151">To configure your policy, use the following settings:</span></span>

    ![Add a sign-up or sign-in policy](media/active-directory-b2c-tutorials-desktop-app/add-susi-policy.png)

    | <span data-ttu-id="a0384-153">Setting</span><span class="sxs-lookup"><span data-stu-id="a0384-153">Setting</span></span>      | <span data-ttu-id="a0384-154">Suggested value</span><span class="sxs-lookup"><span data-stu-id="a0384-154">Suggested value</span></span>  | <span data-ttu-id="a0384-155">Description</span><span class="sxs-lookup"><span data-stu-id="a0384-155">Description</span></span>                                        |
    | ------------ | ------- | -------------------------------------------------- |
    | <span data-ttu-id="a0384-156">**Name**</span><span class="sxs-lookup"><span data-stu-id="a0384-156">**Name**</span></span> | <span data-ttu-id="a0384-157">SiUpIn</span><span class="sxs-lookup"><span data-stu-id="a0384-157">SiUpIn</span></span> | <span data-ttu-id="a0384-158">Enter a **Name** for the policy.</span><span class="sxs-lookup"><span data-stu-id="a0384-158">Enter a **Name** for the policy.</span></span> <span data-ttu-id="a0384-159">The policy name is prefixed with **B2C_1_**.</span><span class="sxs-lookup"><span data-stu-id="a0384-159">The policy name is prefixed with **B2C_1_**.</span></span> <span data-ttu-id="a0384-160">You use the full policy name **B2C_1_SiUpIn** in the sample code.</span><span class="sxs-lookup"><span data-stu-id="a0384-160">You use the full policy name **B2C_1_SiUpIn** in the sample code.</span></span> | 
    | <span data-ttu-id="a0384-161">**Identity provider**</span><span class="sxs-lookup"><span data-stu-id="a0384-161">**Identity provider**</span></span> | <span data-ttu-id="a0384-162">Email signup</span><span class="sxs-lookup"><span data-stu-id="a0384-162">Email signup</span></span> | <span data-ttu-id="a0384-163">The identity provider used to uniquely identify the user.</span><span class="sxs-lookup"><span data-stu-id="a0384-163">The identity provider used to uniquely identify the user.</span></span> |
    | <span data-ttu-id="a0384-164">**Sign up attributes**</span><span class="sxs-lookup"><span data-stu-id="a0384-164">**Sign up attributes**</span></span> | <span data-ttu-id="a0384-165">Display Name and Postal Code</span><span class="sxs-lookup"><span data-stu-id="a0384-165">Display Name and Postal Code</span></span> | <span data-ttu-id="a0384-166">Select attributes to be collected from the user during signup.</span><span class="sxs-lookup"><span data-stu-id="a0384-166">Select attributes to be collected from the user during signup.</span></span> |
    | <span data-ttu-id="a0384-167">**Application claims**</span><span class="sxs-lookup"><span data-stu-id="a0384-167">**Application claims**</span></span> | <span data-ttu-id="a0384-168">Display Name, Postal Code, User is new, User's Object ID</span><span class="sxs-lookup"><span data-stu-id="a0384-168">Display Name, Postal Code, User is new, User's Object ID</span></span> | <span data-ttu-id="a0384-169">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token).</span><span class="sxs-lookup"><span data-stu-id="a0384-169">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token).</span></span> |

2. <span data-ttu-id="a0384-170">Click **Create** to create your policy.</span><span class="sxs-lookup"><span data-stu-id="a0384-170">Click **Create** to create your policy.</span></span> 

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="a0384-171">Create a profile editing policy</span><span class="sxs-lookup"><span data-stu-id="a0384-171">Create a profile editing policy</span></span>

<span data-ttu-id="a0384-172">To allow users to reset their user profile information on their own, create a **profile editing policy**.</span><span class="sxs-lookup"><span data-stu-id="a0384-172">To allow users to reset their user profile information on their own, create a **profile editing policy**.</span></span>

1. <span data-ttu-id="a0384-173">From the Azure AD B2C portal page, select **Profile editing policies** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a0384-173">From the Azure AD B2C portal page, select **Profile editing policies** and click **Add**.</span></span>

    <span data-ttu-id="a0384-174">To configure your policy, use the following settings:</span><span class="sxs-lookup"><span data-stu-id="a0384-174">To configure your policy, use the following settings:</span></span>

    | <span data-ttu-id="a0384-175">Setting</span><span class="sxs-lookup"><span data-stu-id="a0384-175">Setting</span></span>      | <span data-ttu-id="a0384-176">Suggested value</span><span class="sxs-lookup"><span data-stu-id="a0384-176">Suggested value</span></span>  | <span data-ttu-id="a0384-177">Description</span><span class="sxs-lookup"><span data-stu-id="a0384-177">Description</span></span>                                        |
    | ------------ | ------- | -------------------------------------------------- |
    | <span data-ttu-id="a0384-178">**Name**</span><span class="sxs-lookup"><span data-stu-id="a0384-178">**Name**</span></span> | <span data-ttu-id="a0384-179">SiPe</span><span class="sxs-lookup"><span data-stu-id="a0384-179">SiPe</span></span> | <span data-ttu-id="a0384-180">Enter a **Name** for the policy.</span><span class="sxs-lookup"><span data-stu-id="a0384-180">Enter a **Name** for the policy.</span></span> <span data-ttu-id="a0384-181">The policy name is prefixed with **B2C_1_**.</span><span class="sxs-lookup"><span data-stu-id="a0384-181">The policy name is prefixed with **B2C_1_**.</span></span> <span data-ttu-id="a0384-182">You use the full policy name **B2C_1_SiPe** in the sample code.</span><span class="sxs-lookup"><span data-stu-id="a0384-182">You use the full policy name **B2C_1_SiPe** in the sample code.</span></span> | 
    | <span data-ttu-id="a0384-183">**Identity provider**</span><span class="sxs-lookup"><span data-stu-id="a0384-183">**Identity provider**</span></span> | <span data-ttu-id="a0384-184">Local Account SignIn</span><span class="sxs-lookup"><span data-stu-id="a0384-184">Local Account SignIn</span></span> | <span data-ttu-id="a0384-185">The identity provider used to uniquely identify the user.</span><span class="sxs-lookup"><span data-stu-id="a0384-185">The identity provider used to uniquely identify the user.</span></span> |
    | <span data-ttu-id="a0384-186">**Profile attributes**</span><span class="sxs-lookup"><span data-stu-id="a0384-186">**Profile attributes**</span></span> | <span data-ttu-id="a0384-187">Display Name and Postal Code</span><span class="sxs-lookup"><span data-stu-id="a0384-187">Display Name and Postal Code</span></span> | <span data-ttu-id="a0384-188">Select attributes users can modify during profile edit.</span><span class="sxs-lookup"><span data-stu-id="a0384-188">Select attributes users can modify during profile edit.</span></span> |
    | <span data-ttu-id="a0384-189">**Application claims**</span><span class="sxs-lookup"><span data-stu-id="a0384-189">**Application claims**</span></span> | <span data-ttu-id="a0384-190">Display Name, Postal Code, User's Object ID</span><span class="sxs-lookup"><span data-stu-id="a0384-190">Display Name, Postal Code, User's Object ID</span></span> | <span data-ttu-id="a0384-191">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token) after a successful profile edit.</span><span class="sxs-lookup"><span data-stu-id="a0384-191">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token) after a successful profile edit.</span></span> |

2. <span data-ttu-id="a0384-192">Click **Create** to create your policy.</span><span class="sxs-lookup"><span data-stu-id="a0384-192">Click **Create** to create your policy.</span></span> 

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="a0384-193">Create a password reset policy</span><span class="sxs-lookup"><span data-stu-id="a0384-193">Create a password reset policy</span></span>

<span data-ttu-id="a0384-194">To enable password reset on your application, you need to create a **password reset policy**.</span><span class="sxs-lookup"><span data-stu-id="a0384-194">To enable password reset on your application, you need to create a **password reset policy**.</span></span> <span data-ttu-id="a0384-195">This policy describes the consumer experience during password reset and the contents of tokens that the application receives on successful completion.</span><span class="sxs-lookup"><span data-stu-id="a0384-195">This policy describes the consumer experience during password reset and the contents of tokens that the application receives on successful completion.</span></span>

1. <span data-ttu-id="a0384-196">From the Azure AD B2C portal page, select **Password reset policies** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a0384-196">From the Azure AD B2C portal page, select **Password reset policies** and click **Add**.</span></span>

    <span data-ttu-id="a0384-197">To configure your policy, use the following settings.</span><span class="sxs-lookup"><span data-stu-id="a0384-197">To configure your policy, use the following settings.</span></span>

    | <span data-ttu-id="a0384-198">Setting</span><span class="sxs-lookup"><span data-stu-id="a0384-198">Setting</span></span>      | <span data-ttu-id="a0384-199">Suggested value</span><span class="sxs-lookup"><span data-stu-id="a0384-199">Suggested value</span></span>  | <span data-ttu-id="a0384-200">Description</span><span class="sxs-lookup"><span data-stu-id="a0384-200">Description</span></span>                                        |
    | ------------ | ------- | -------------------------------------------------- |
    | <span data-ttu-id="a0384-201">**Name**</span><span class="sxs-lookup"><span data-stu-id="a0384-201">**Name**</span></span> | <span data-ttu-id="a0384-202">SSPR</span><span class="sxs-lookup"><span data-stu-id="a0384-202">SSPR</span></span> | <span data-ttu-id="a0384-203">Enter a **Name** for the policy.</span><span class="sxs-lookup"><span data-stu-id="a0384-203">Enter a **Name** for the policy.</span></span> <span data-ttu-id="a0384-204">The policy name is prefixed with **B2C_1_**.</span><span class="sxs-lookup"><span data-stu-id="a0384-204">The policy name is prefixed with **B2C_1_**.</span></span> <span data-ttu-id="a0384-205">You use the full policy name **B2C_1_SSPR** in the sample code.</span><span class="sxs-lookup"><span data-stu-id="a0384-205">You use the full policy name **B2C_1_SSPR** in the sample code.</span></span> | 
    | <span data-ttu-id="a0384-206">**Identity provider**</span><span class="sxs-lookup"><span data-stu-id="a0384-206">**Identity provider**</span></span> | <span data-ttu-id="a0384-207">Reset password using email address</span><span class="sxs-lookup"><span data-stu-id="a0384-207">Reset password using email address</span></span> | <span data-ttu-id="a0384-208">This is the identity provider used to uniquely identify the user.</span><span class="sxs-lookup"><span data-stu-id="a0384-208">This is the identity provider used to uniquely identify the user.</span></span> |
    | <span data-ttu-id="a0384-209">**Application claims**</span><span class="sxs-lookup"><span data-stu-id="a0384-209">**Application claims**</span></span> | <span data-ttu-id="a0384-210">User's Object ID</span><span class="sxs-lookup"><span data-stu-id="a0384-210">User's Object ID</span></span> | <span data-ttu-id="a0384-211">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token) after a successful password reset.</span><span class="sxs-lookup"><span data-stu-id="a0384-211">Select [claims](../active-directory/develop/developer-glossary.md#claim) you want to be included in the [access token](../active-directory/develop/developer-glossary.md#access-token) after a successful password reset.</span></span> |

2. <span data-ttu-id="a0384-212">Click **Create** to create your policy.</span><span class="sxs-lookup"><span data-stu-id="a0384-212">Click **Create** to create your policy.</span></span> 

## <a name="update-desktop-app-code"></a><span data-ttu-id="a0384-213">Update desktop app code</span><span class="sxs-lookup"><span data-stu-id="a0384-213">Update desktop app code</span></span>

<span data-ttu-id="a0384-214">Now that you have a desktop app registered and policies created, you need to configure your app to use your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="a0384-214">Now that you have a desktop app registered and policies created, you need to configure your app to use your Azure AD B2C tenant.</span></span> <span data-ttu-id="a0384-215">In this tutorial, you configure a sample desktop app.</span><span class="sxs-lookup"><span data-stu-id="a0384-215">In this tutorial, you configure a sample desktop app.</span></span> 

<span data-ttu-id="a0384-216">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop/archive/master.zip) or clone the sample from GitHub.</span><span class="sxs-lookup"><span data-stu-id="a0384-216">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop/archive/master.zip) or clone the sample from GitHub.</span></span>

```
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop.git
```

<span data-ttu-id="a0384-217">The sample WPF desktop app demonstrates how a desktop app can use Azure AD B2C for user sign-up, sign-in, and call a protected web API.</span><span class="sxs-lookup"><span data-stu-id="a0384-217">The sample WPF desktop app demonstrates how a desktop app can use Azure AD B2C for user sign-up, sign-in, and call a protected web API.</span></span>

<span data-ttu-id="a0384-218">You need to change the app to use the app registration in your tenant and configure the policies you created.</span><span class="sxs-lookup"><span data-stu-id="a0384-218">You need to change the app to use the app registration in your tenant and configure the policies you created.</span></span> 

<span data-ttu-id="a0384-219">To change the app settings:</span><span class="sxs-lookup"><span data-stu-id="a0384-219">To change the app settings:</span></span>

1. <span data-ttu-id="a0384-220">Open the `active-directory-b2c-wpf` solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0384-220">Open the `active-directory-b2c-wpf` solution in Visual Studio.</span></span>

2. <span data-ttu-id="a0384-221">In the `active-directory-b2c-wpf` project, open the **App.xaml.cs** file and make the following updates:</span><span class="sxs-lookup"><span data-stu-id="a0384-221">In the `active-directory-b2c-wpf` project, open the **App.xaml.cs** file and make the following updates:</span></span>

    ```C#
    private static string Tenant = "<your-tenant-name>.onmicrosoft.com";
    private static string ClientId = "The Application ID for your desktop app registered in your tenant";
    ```

3. <span data-ttu-id="a0384-222">Update the **PolicySignUpSignIn** variable with the *sign-up or sign-in policy* name you created in a previous step.</span><span class="sxs-lookup"><span data-stu-id="a0384-222">Update the **PolicySignUpSignIn** variable with the *sign-up or sign-in policy* name you created in a previous step.</span></span> <span data-ttu-id="a0384-223">Remember to include the *B2C_1_* prefix.</span><span class="sxs-lookup"><span data-stu-id="a0384-223">Remember to include the *B2C_1_* prefix.</span></span>

    ```C#
    public static string PolicySignUpSignIn = "B2C_1_SiUpIn";
    ```

## <a name="run-the-sample-desktop-application"></a><span data-ttu-id="a0384-224">Run the sample desktop application</span><span class="sxs-lookup"><span data-stu-id="a0384-224">Run the sample desktop application</span></span>

<span data-ttu-id="a0384-225">Press **F5** to build and run the desktop app.</span><span class="sxs-lookup"><span data-stu-id="a0384-225">Press **F5** to build and run the desktop app.</span></span> 

<span data-ttu-id="a0384-226">The sample app supports sign up, sign in, editing a profile, and password reset.</span><span class="sxs-lookup"><span data-stu-id="a0384-226">The sample app supports sign up, sign in, editing a profile, and password reset.</span></span> <span data-ttu-id="a0384-227">This tutorial highlights how a user signs up to use the app using an email address.</span><span class="sxs-lookup"><span data-stu-id="a0384-227">This tutorial highlights how a user signs up to use the app using an email address.</span></span> <span data-ttu-id="a0384-228">You can explore other scenarios on your own.</span><span class="sxs-lookup"><span data-stu-id="a0384-228">You can explore other scenarios on your own.</span></span>

### <a name="sign-up-using-an-email-address"></a><span data-ttu-id="a0384-229">Sign up using an email address</span><span class="sxs-lookup"><span data-stu-id="a0384-229">Sign up using an email address</span></span>

1. <span data-ttu-id="a0384-230">Click the **Sign In** button to sign up as a user of the desktop app.</span><span class="sxs-lookup"><span data-stu-id="a0384-230">Click the **Sign In** button to sign up as a user of the desktop app.</span></span> <span data-ttu-id="a0384-231">This uses the **B2C_1_SiUpIn** policy you defined in a previous step.</span><span class="sxs-lookup"><span data-stu-id="a0384-231">This uses the **B2C_1_SiUpIn** policy you defined in a previous step.</span></span>

2. <span data-ttu-id="a0384-232">Azure AD B2C presents a sign-in page with a sign-up link.</span><span class="sxs-lookup"><span data-stu-id="a0384-232">Azure AD B2C presents a sign-in page with a sign-up link.</span></span> <span data-ttu-id="a0384-233">Since you don't have an account yet, click the **Sign up now** link.</span><span class="sxs-lookup"><span data-stu-id="a0384-233">Since you don't have an account yet, click the **Sign up now** link.</span></span> 

3. <span data-ttu-id="a0384-234">The sign-up workflow presents a page to collect and verify the user's identity using an email address.</span><span class="sxs-lookup"><span data-stu-id="a0384-234">The sign-up workflow presents a page to collect and verify the user's identity using an email address.</span></span> <span data-ttu-id="a0384-235">The sign-up workflow also collects the user's password and the requested attributes defined in the policy.</span><span class="sxs-lookup"><span data-stu-id="a0384-235">The sign-up workflow also collects the user's password and the requested attributes defined in the policy.</span></span>

    <span data-ttu-id="a0384-236">Use a valid email address and validate using the verification code.</span><span class="sxs-lookup"><span data-stu-id="a0384-236">Use a valid email address and validate using the verification code.</span></span> <span data-ttu-id="a0384-237">Set a password.</span><span class="sxs-lookup"><span data-stu-id="a0384-237">Set a password.</span></span> <span data-ttu-id="a0384-238">Enter values for the requested attributes.</span><span class="sxs-lookup"><span data-stu-id="a0384-238">Enter values for the requested attributes.</span></span> 

    ![Sign-up workflow](media/active-directory-b2c-tutorials-desktop-app/sign-up-workflow.png)

4. <span data-ttu-id="a0384-240">Click **Create** to create a local account in the Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="a0384-240">Click **Create** to create a local account in the Azure AD B2C tenant.</span></span>

<span data-ttu-id="a0384-241">Now, the user can use their email address to sign in and use the desktop app.</span><span class="sxs-lookup"><span data-stu-id="a0384-241">Now, the user can use their email address to sign in and use the desktop app.</span></span>

> [!NOTE]
> <span data-ttu-id="a0384-242">If you click the **Call API** button, you will receive an "Unauthorized" error.</span><span class="sxs-lookup"><span data-stu-id="a0384-242">If you click the **Call API** button, you will receive an "Unauthorized" error.</span></span> <span data-ttu-id="a0384-243">You receive this error because you are attempting to access a resource from the demo tenant.</span><span class="sxs-lookup"><span data-stu-id="a0384-243">You receive this error because you are attempting to access a resource from the demo tenant.</span></span> <span data-ttu-id="a0384-244">Since your access token is only valid for your Azure AD tenant, the API call is unauthorized.</span><span class="sxs-lookup"><span data-stu-id="a0384-244">Since your access token is only valid for your Azure AD tenant, the API call is unauthorized.</span></span> <span data-ttu-id="a0384-245">Continue with the next tutorial to create a protected web API for your tenant.</span><span class="sxs-lookup"><span data-stu-id="a0384-245">Continue with the next tutorial to create a protected web API for your tenant.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="a0384-246">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a0384-246">Clean up resources</span></span>

<span data-ttu-id="a0384-247">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C tutorials.</span><span class="sxs-lookup"><span data-stu-id="a0384-247">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C tutorials.</span></span> <span data-ttu-id="a0384-248">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span><span class="sxs-lookup"><span data-stu-id="a0384-248">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0384-249">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0384-249">Next steps</span></span>

<span data-ttu-id="a0384-250">In this tutorial, you learned how to create an Azure AD B2C tenant, create policies, and update the sample desktop app to use your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="a0384-250">In this tutorial, you learned how to create an Azure AD B2C tenant, create policies, and update the sample desktop app to use your Azure AD B2C tenant.</span></span> <span data-ttu-id="a0384-251">Continue to the next tutorial to learn how to register, configure, and call a protected web API from a desktop app.</span><span class="sxs-lookup"><span data-stu-id="a0384-251">Continue to the next tutorial to learn how to register, configure, and call a protected web API from a desktop app.</span></span>

> [!div class="nextstepaction"]
> 