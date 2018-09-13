---
title: Azure AD Android getting started | Microsoft Docs
description: How to build an Android application that integrates with Azure AD for sign-in and calls Azure AD protected APIs using OAuth2.0.
services: active-directory
documentationcenter: android
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/30/2018
ms.author: celested
ms.reviewer: dadobali
ms.custom: aaddev
ms.openlocfilehash: c548f9287ce1326de3322950f297176b67ae61c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855674"
---
# <a name="azure-ad-android-getting-started"></a><span data-ttu-id="ae2d9-103">Azure AD Android getting started</span><span class="sxs-lookup"><span data-stu-id="ae2d9-103">Azure AD Android getting started</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

<span data-ttu-id="ae2d9-104">If you're developing an Android application, Microsoft makes it simple and straightforward to sign in Azure Active Directory (Azure AD) users.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-104">If you're developing an Android application, Microsoft makes it simple and straightforward to sign in Azure Active Directory (Azure AD) users.</span></span> <span data-ttu-id="ae2d9-105">Azure AD enables your application to access user data through the Microsoft Graph or your own protected web API.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-105">Azure AD enables your application to access user data through the Microsoft Graph or your own protected web API.</span></span> 

<span data-ttu-id="ae2d9-106">The Azure AD Authentication Library (ADAL) Android library gives your app the ability to begin using the [Microsoft Azure Cloud](https://cloud.microsoft.com) & [Microsoft Graph API](https://graph.microsoft.io) by supporting [Microsoft Azure Active Directory accounts](https://azure.microsoft.com/services/active-directory/) using industry standard OAuth2 and OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-106">The Azure AD Authentication Library (ADAL) Android library gives your app the ability to begin using the [Microsoft Azure Cloud](https://cloud.microsoft.com) & [Microsoft Graph API](https://graph.microsoft.io) by supporting [Microsoft Azure Active Directory accounts](https://azure.microsoft.com/services/active-directory/) using industry standard OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="ae2d9-107">This sample demonstrates all the normal lifecycles your application should experience, including:</span><span class="sxs-lookup"><span data-stu-id="ae2d9-107">This sample demonstrates all the normal lifecycles your application should experience, including:</span></span>

* <span data-ttu-id="ae2d9-108">Get a token for the Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="ae2d9-108">Get a token for the Microsoft Graph</span></span>
* <span data-ttu-id="ae2d9-109">Refresh a token</span><span class="sxs-lookup"><span data-stu-id="ae2d9-109">Refresh a token</span></span>
* <span data-ttu-id="ae2d9-110">Call the Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="ae2d9-110">Call the Microsoft Graph</span></span>
* <span data-ttu-id="ae2d9-111">Sign out the user</span><span class="sxs-lookup"><span data-stu-id="ae2d9-111">Sign out the user</span></span>

<span data-ttu-id="ae2d9-112">To get started, you'll need an Azure AD tenant where you can create users and register an application.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-112">To get started, you'll need an Azure AD tenant where you can create users and register an application.</span></span> <span data-ttu-id="ae2d9-113">If you don't already have a tenant, [learn how to get one](quickstart-create-new-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ae2d9-113">If you don't already have a tenant, [learn how to get one](quickstart-create-new-tenant.md).</span></span>

## <a name="scenario-sign-in-users-and-call-the-microsoft-graph"></a><span data-ttu-id="ae2d9-114">Scenario: Sign in users and call the Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="ae2d9-114">Scenario: Sign in users and call the Microsoft Graph</span></span>

![Topology](./media/quickstart-v1-android/active-directory-android-topology.png)

<span data-ttu-id="ae2d9-116">This app can be used for all Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-116">This app can be used for all Azure AD accounts.</span></span> <span data-ttu-id="ae2d9-117">It supports both single and multi-organizational scenarios (discussed in steps).</span><span class="sxs-lookup"><span data-stu-id="ae2d9-117">It supports both single and multi-organizational scenarios (discussed in steps).</span></span> <span data-ttu-id="ae2d9-118">It demonstrates how a developer can build apps to connect with enterprise users and access their Azure + O365 data via the Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-118">It demonstrates how a developer can build apps to connect with enterprise users and access their Azure + O365 data via the Microsoft Graph.</span></span> <span data-ttu-id="ae2d9-119">During the auth flow, end users will be required to sign in and consent to the permissions of the application, and in some cases may require an admin to consent to the app.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-119">During the auth flow, end users will be required to sign in and consent to the permissions of the application, and in some cases may require an admin to consent to the app.</span></span> <span data-ttu-id="ae2d9-120">The majority of the logic in this sample shows how to auth an end user and make a basic call to the Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-120">The majority of the logic in this sample shows how to auth an end user and make a basic call to the Microsoft Graph.</span></span>

## <a name="example-code"></a><span data-ttu-id="ae2d9-121">Example code</span><span class="sxs-lookup"><span data-stu-id="ae2d9-121">Example code</span></span>

<span data-ttu-id="ae2d9-122">You can find the full sample code [on Github](https://github.com/Azure-Samples/active-directory-android).</span><span class="sxs-lookup"><span data-stu-id="ae2d9-122">You can find the full sample code [on Github](https://github.com/Azure-Samples/active-directory-android).</span></span> 

```Java
// Initialize your app with MSAL
AuthenticationContext mAuthContext = new AuthenticationContext(
        MainActivity.this, 
        AUTHORITY, 
        false);


// Perform authentication requests
mAuthContext.acquireToken(
    getActivity(), 
    RESOURCE_ID, 
    CLIENT_ID, 
    REDIRECT_URI,  
    PromptBehavior.Auto, 
    getAuthInteractiveCallback());

// ...

// Get tokens to call APIs like the Microsoft Graph
mAuthResult.getAccessToken()
```

## <a name="steps-to-run"></a><span data-ttu-id="ae2d9-123">Steps to run</span><span class="sxs-lookup"><span data-stu-id="ae2d9-123">Steps to run</span></span>

### <a name="register-and-configure-your-app"></a><span data-ttu-id="ae2d9-124">Register and configure your app</span><span class="sxs-lookup"><span data-stu-id="ae2d9-124">Register and configure your app</span></span> 
<span data-ttu-id="ae2d9-125">You will need to have a native client application registered with Microsoft using the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ae2d9-125">You will need to have a native client application registered with Microsoft using the [Azure portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="ae2d9-126">Getting to app registration</span><span class="sxs-lookup"><span data-stu-id="ae2d9-126">Getting to app registration</span></span>
    - <span data-ttu-id="ae2d9-127">Navigate to the [Azure portal](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ae2d9-127">Navigate to the [Azure portal](https://aad.portal.azure.com).</span></span> 
    - <span data-ttu-id="ae2d9-128">Select ***Azure Active Directory*** > ***App Registrations***.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-128">Select ***Azure Active Directory*** > ***App Registrations***.</span></span> 

2. <span data-ttu-id="ae2d9-129">Create the app</span><span class="sxs-lookup"><span data-stu-id="ae2d9-129">Create the app</span></span>
    - <span data-ttu-id="ae2d9-130">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-130">Select **New application registration**.</span></span> 
    - <span data-ttu-id="ae2d9-131">Enter an app name in the **Name** field.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-131">Enter an app name in the **Name** field.</span></span> 
    - <span data-ttu-id="ae2d9-132">In **Application type** select **Native**.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-132">In **Application type** select **Native**.</span></span> 
    - <span data-ttu-id="ae2d9-133">In **Redirect URI**, enter `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-133">In **Redirect URI**, enter `http://localhost`.</span></span> 

3. <span data-ttu-id="ae2d9-134">Configure Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="ae2d9-134">Configure Microsoft Graph</span></span>
    - <span data-ttu-id="ae2d9-135">Select **Settings > Required Permissions**.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-135">Select **Settings > Required Permissions**.</span></span>
    - <span data-ttu-id="ae2d9-136">Select **Add**, inside **Select an API** select ***Microsoft Graph***.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-136">Select **Add**, inside **Select an API** select ***Microsoft Graph***.</span></span> 
    - <span data-ttu-id="ae2d9-137">Select the permission **Sign in and read user profile**, then hit **Select** to save.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-137">Select the permission **Sign in and read user profile**, then hit **Select** to save.</span></span> 
        - <span data-ttu-id="ae2d9-138">This permission maps to the `User.Read` scope.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-138">This permission maps to the `User.Read` scope.</span></span> 
    - <span data-ttu-id="ae2d9-139">Optional: Inside **Required permissions > Windows Azure Active Directory**, remove the selected permission **Sign in and read user profile**.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-139">Optional: Inside **Required permissions > Windows Azure Active Directory**, remove the selected permission **Sign in and read user profile**.</span></span> <span data-ttu-id="ae2d9-140">This will avoid the user consent page listing the permission twice.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-140">This will avoid the user consent page listing the permission twice.</span></span> 

4. <span data-ttu-id="ae2d9-141">Congrats!</span><span class="sxs-lookup"><span data-stu-id="ae2d9-141">Congrats!</span></span> <span data-ttu-id="ae2d9-142">Your app is successfully configured.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-142">Your app is successfully configured.</span></span> <span data-ttu-id="ae2d9-143">In the next section, you'll need:</span><span class="sxs-lookup"><span data-stu-id="ae2d9-143">In the next section, you'll need:</span></span>
    - `Application ID`
    - `Redirect URI`

### <a name="get-the-sample-code"></a><span data-ttu-id="ae2d9-144">Get the sample code</span><span class="sxs-lookup"><span data-stu-id="ae2d9-144">Get the sample code</span></span>

1. <span data-ttu-id="ae2d9-145">Clone the code.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-145">Clone the code.</span></span>
    ```
    git clone https://github.com/Azure-Samples/active-directory-android
    ```
2. <span data-ttu-id="ae2d9-146">Open the sample in Android Studio.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-146">Open the sample in Android Studio.</span></span>
    - <span data-ttu-id="ae2d9-147">Select **Open an existing Android Studio project**.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-147">Select **Open an existing Android Studio project**.</span></span>

### <a name="configure-your-code"></a><span data-ttu-id="ae2d9-148">Configure your code</span><span class="sxs-lookup"><span data-stu-id="ae2d9-148">Configure your code</span></span>

<span data-ttu-id="ae2d9-149">You can find all the configuration for this code sample in the ***src/main/java/com/azuresamples/azuresampleapp/MainActivity.java*** file.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-149">You can find all the configuration for this code sample in the ***src/main/java/com/azuresamples/azuresampleapp/MainActivity.java*** file.</span></span> 

1. <span data-ttu-id="ae2d9-150">Replace the constant `CLIENT_ID` with the `ApplicationID`.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-150">Replace the constant `CLIENT_ID` with the `ApplicationID`.</span></span>
2. <span data-ttu-id="ae2d9-151">Replace the constant `REDIRECT URI` with the `Redirect URI` you configured earlier (`http://localhost`).</span><span class="sxs-lookup"><span data-stu-id="ae2d9-151">Replace the constant `REDIRECT URI` with the `Redirect URI` you configured earlier (`http://localhost`).</span></span> 

### <a name="run-the-sample"></a><span data-ttu-id="ae2d9-152">Run the sample</span><span class="sxs-lookup"><span data-stu-id="ae2d9-152">Run the sample</span></span>

1. <span data-ttu-id="ae2d9-153">Select **Build > Clean Project**.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-153">Select **Build > Clean Project**.</span></span> 
2. <span data-ttu-id="ae2d9-154">Select **Run > Run app**.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-154">Select **Run > Run app**.</span></span> 
3. <span data-ttu-id="ae2d9-155">The app should build and show some basic UX.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-155">The app should build and show some basic UX.</span></span> <span data-ttu-id="ae2d9-156">When you click the `Call Graph API` button, it will prompt for a sign in, and then silently call the Microsoft Graph API with the new token.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-156">When you click the `Call Graph API` button, it will prompt for a sign in, and then silently call the Microsoft Graph API with the new token.</span></span> 

## <a name="important-info"></a><span data-ttu-id="ae2d9-157">Important info</span><span class="sxs-lookup"><span data-stu-id="ae2d9-157">Important info</span></span>

1. <span data-ttu-id="ae2d9-158">Checkout the [ADAL Android Wiki](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki) for more info on the library mechanics and how to configure new scenarios and capabilities.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-158">Checkout the [ADAL Android Wiki](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki) for more info on the library mechanics and how to configure new scenarios and capabilities.</span></span> 
2. <span data-ttu-id="ae2d9-159">In Native scenarios, the app will use an embedded Webview and will not leave the app.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-159">In Native scenarios, the app will use an embedded Webview and will not leave the app.</span></span> <span data-ttu-id="ae2d9-160">The `Redirect URI` can be arbitrary.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-160">The `Redirect URI` can be arbitrary.</span></span> 
3. <span data-ttu-id="ae2d9-161">Find any problems or have requests?</span><span class="sxs-lookup"><span data-stu-id="ae2d9-161">Find any problems or have requests?</span></span> <span data-ttu-id="ae2d9-162">You can create an issue or post on Stackoverflow with the tag `azure-active-directory`.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-162">You can create an issue or post on Stackoverflow with the tag `azure-active-directory`.</span></span> 

### <a name="cross-app-sso"></a><span data-ttu-id="ae2d9-163">Cross-app SSO</span><span class="sxs-lookup"><span data-stu-id="ae2d9-163">Cross-app SSO</span></span>
<span data-ttu-id="ae2d9-164">Learn [how to enable cross-app SSO on Android by using ADAL](howto-v1-enable-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="ae2d9-164">Learn [how to enable cross-app SSO on Android by using ADAL](howto-v1-enable-sso-android.md).</span></span> 

### <a name="auth-telemetry"></a><span data-ttu-id="ae2d9-165">Auth telemetry</span><span class="sxs-lookup"><span data-stu-id="ae2d9-165">Auth telemetry</span></span>
<span data-ttu-id="ae2d9-166">the ADAL library exposes auth telemetry to help app developers understand how their apps are behaving and build better experiences.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-166">the ADAL library exposes auth telemetry to help app developers understand how their apps are behaving and build better experiences.</span></span> <span data-ttu-id="ae2d9-167">This allows you to capture sign in success, active users, and several other interesting insights.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-167">This allows you to capture sign in success, active users, and several other interesting insights.</span></span> <span data-ttu-id="ae2d9-168">Using auth telemetry does require app developers to establish a telemetry service to aggregate and store events.</span><span class="sxs-lookup"><span data-stu-id="ae2d9-168">Using auth telemetry does require app developers to establish a telemetry service to aggregate and store events.</span></span>

<span data-ttu-id="ae2d9-169">To learn more about auth telemetry, checkout [ADAL Android auth telemetry](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/Telemetry).</span><span class="sxs-lookup"><span data-stu-id="ae2d9-169">To learn more about auth telemetry, checkout [ADAL Android auth telemetry](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/Telemetry).</span></span> 

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
