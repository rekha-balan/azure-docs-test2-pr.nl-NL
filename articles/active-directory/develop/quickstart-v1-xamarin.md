---
title: Azure AD Xamarin getting started | Microsoft Docs
description: Build Xamarin applications that integrate with Azure AD for sign-in and call Azure AD-protected APIs using OAuth.
services: active-directory
documentationcenter: xamarin
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 11/30/2017
ms.author: celested
ms.reviewer: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 3479aa8dd319c81f320b6c7ead086c266454acc6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868385"
---
# <a name="azure-ad-xamarin-getting-started"></a><span data-ttu-id="c5501-103">Azure AD Xamarin getting started</span><span class="sxs-lookup"><span data-stu-id="c5501-103">Azure AD Xamarin getting started</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="c5501-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span><span class="sxs-lookup"><span data-stu-id="c5501-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="c5501-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple to authenticate users with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="c5501-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple to authenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="c5501-106">The app can also securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span><span class="sxs-lookup"><span data-stu-id="c5501-106">The app can also securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="c5501-107">For Xamarin apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="c5501-107">For Xamarin apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="c5501-108">The sole purpose of ADAL is to make it easy for apps to get access tokens.</span><span class="sxs-lookup"><span data-stu-id="c5501-108">The sole purpose of ADAL is to make it easy for apps to get access tokens.</span></span> <span data-ttu-id="c5501-109">To demonstrate how easy it is, this article shows how to build DirectorySearcher apps that:</span><span class="sxs-lookup"><span data-stu-id="c5501-109">To demonstrate how easy it is, this article shows how to build DirectorySearcher apps that:</span></span>

* <span data-ttu-id="c5501-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span><span class="sxs-lookup"><span data-stu-id="c5501-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="c5501-111">Use a single portable class library (PCL) to authenticate users and get tokens for the Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="c5501-111">Use a single portable class library (PCL) to authenticate users and get tokens for the Azure AD Graph API.</span></span>
* <span data-ttu-id="c5501-112">Search a directory for users with a given UPN.</span><span class="sxs-lookup"><span data-stu-id="c5501-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="c5501-113">Before you get started</span><span class="sxs-lookup"><span data-stu-id="c5501-113">Before you get started</span></span>
* <span data-ttu-id="c5501-114">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="c5501-114">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="c5501-115">Each download is a Visual Studio 2013 solution.</span><span class="sxs-lookup"><span data-stu-id="c5501-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="c5501-116">You also need an Azure AD tenant in which to create users and register the app.</span><span class="sxs-lookup"><span data-stu-id="c5501-116">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="c5501-117">If you don't already have a tenant, [learn how to get one](quickstart-create-new-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="c5501-117">If you don't already have a tenant, [learn how to get one](quickstart-create-new-tenant.md).</span></span>

<span data-ttu-id="c5501-118">When you are ready, follow the procedures in the next four sections.</span><span class="sxs-lookup"><span data-stu-id="c5501-118">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="c5501-119">Step 1: Set up your Xamarin development environment</span><span class="sxs-lookup"><span data-stu-id="c5501-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="c5501-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span><span class="sxs-lookup"><span data-stu-id="c5501-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="c5501-121">To create the necessary environment, complete the process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span><span class="sxs-lookup"><span data-stu-id="c5501-121">To create the necessary environment, complete the process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="c5501-122">The instructions include material that you can review to learn more about Xamarin while you're waiting for the installations to be completed.</span><span class="sxs-lookup"><span data-stu-id="c5501-122">The instructions include material that you can review to learn more about Xamarin while you're waiting for the installations to be completed.</span></span>

<span data-ttu-id="c5501-123">After you've completed the setup, open the solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c5501-123">After you've completed the setup, open the solution in Visual Studio.</span></span> <span data-ttu-id="c5501-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span><span class="sxs-lookup"><span data-stu-id="c5501-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-the-directorysearcher-app"></a><span data-ttu-id="c5501-125">Step 2: Register the DirectorySearcher app</span><span class="sxs-lookup"><span data-stu-id="c5501-125">Step 2: Register the DirectorySearcher app</span></span>
<span data-ttu-id="c5501-126">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="c5501-126">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="c5501-127">Here's how:</span><span class="sxs-lookup"><span data-stu-id="c5501-127">Here's how:</span></span>

1. <span data-ttu-id="c5501-128">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c5501-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c5501-129">On the top bar, click your account.</span><span class="sxs-lookup"><span data-stu-id="c5501-129">On the top bar, click your account.</span></span> <span data-ttu-id="c5501-130">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span><span class="sxs-lookup"><span data-stu-id="c5501-130">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="c5501-131">Click **All services** in the left pane, and then select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5501-131">Click **All services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="c5501-132">Click **App registrations**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="c5501-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="c5501-133">To create a new **Native Client Application**, follow the prompts.</span><span class="sxs-lookup"><span data-stu-id="c5501-133">To create a new **Native Client Application**, follow the prompts.</span></span>
  * <span data-ttu-id="c5501-134">**Name** describes the app to users.</span><span class="sxs-lookup"><span data-stu-id="c5501-134">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="c5501-135">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span><span class="sxs-lookup"><span data-stu-id="c5501-135">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="c5501-136">Enter a value (for example, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="c5501-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="c5501-137">After you’ve completed registration, Azure AD assigns the app a unique application ID.</span><span class="sxs-lookup"><span data-stu-id="c5501-137">After you’ve completed registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="c5501-138">Copy the value from the **Application** tab, because you'll need it later.</span><span class="sxs-lookup"><span data-stu-id="c5501-138">Copy the value from the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="c5501-139">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="c5501-139">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="c5501-140">Select **Microsoft Graph** as the API.</span><span class="sxs-lookup"><span data-stu-id="c5501-140">Select **Microsoft Graph** as the API.</span></span> <span data-ttu-id="c5501-141">Under **Delegated Permissions**, add the **Read Directory Data** permission.</span><span class="sxs-lookup"><span data-stu-id="c5501-141">Under **Delegated Permissions**, add the **Read Directory Data** permission.</span></span> <span data-ttu-id="c5501-142">This action enables the app to query the Graph API for users.</span><span class="sxs-lookup"><span data-stu-id="c5501-142">This action enables the app to query the Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="c5501-143">Step 3: Install and configure ADAL</span><span class="sxs-lookup"><span data-stu-id="c5501-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="c5501-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span><span class="sxs-lookup"><span data-stu-id="c5501-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="c5501-145">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span><span class="sxs-lookup"><span data-stu-id="c5501-145">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="c5501-146">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="c5501-146">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    <span data-ttu-id="c5501-147">Note that two library references are added to each project: the PCL portion of ADAL and a platform-specific portion.</span><span class="sxs-lookup"><span data-stu-id="c5501-147">Note that two library references are added to each project: the PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="c5501-148">In the DirectorySearcherLib project, open DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="c5501-148">In the DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="c5501-149">Replace the class member values with the values that you entered in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c5501-149">Replace the class member values with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="c5501-150">Your code refers to these values whenever it uses ADAL.</span><span class="sxs-lookup"><span data-stu-id="c5501-150">Your code refers to these values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="c5501-151">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="c5501-151">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="c5501-152">The *clientId* is the client ID of the app, which you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="c5501-152">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
  * <span data-ttu-id="c5501-153">The *returnUri* is the redirect URI that you entered in the portal (for example, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="c5501-153">The *returnUri* is the redirect URI that you entered in the portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="c5501-154">Step 4: Use ADAL to get tokens from Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5501-154">Step 4: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="c5501-155">Almost all of the app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="c5501-155">Almost all of the app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="c5501-156">All that's necessary in the platform-specific projects is to pass a contextual parameter to the `DirectorySearcher` PCL.</span><span class="sxs-lookup"><span data-stu-id="c5501-156">All that's necessary in the platform-specific projects is to pass a contextual parameter to the `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="c5501-157">Open DirectorySearcher.cs, and then add a new parameter to the `SearchByAlias(...)` method.</span><span class="sxs-lookup"><span data-stu-id="c5501-157">Open DirectorySearcher.cs, and then add a new parameter to the `SearchByAlias(...)` method.</span></span> <span data-ttu-id="c5501-158">`IPlatformParameters` is the contextual parameter that encapsulates the platform-specific objects that ADAL needs to perform the authentication.</span><span class="sxs-lookup"><span data-stu-id="c5501-158">`IPlatformParameters` is the contextual parameter that encapsulates the platform-specific objects that ADAL needs to perform the authentication.</span></span>

    ```csharp
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="c5501-159">Initialize `AuthenticationContext`, which is the primary class of ADAL.</span><span class="sxs-lookup"><span data-stu-id="c5501-159">Initialize `AuthenticationContext`, which is the primary class of ADAL.</span></span> <span data-ttu-id="c5501-160">This action passes ADAL the coordinates it needs to communicate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5501-160">This action passes ADAL the coordinates it needs to communicate with Azure AD.</span></span>
3. <span data-ttu-id="c5501-161">Call `AcquireTokenAsync(...)`, which accepts the `IPlatformParameters` object and invokes the authentication flow that's necessary to return a token to the app.</span><span class="sxs-lookup"><span data-stu-id="c5501-161">Call `AcquireTokenAsync(...)`, which accepts the `IPlatformParameters` object and invokes the authentication flow that's necessary to return a token to the app.</span></span>

    ```csharp
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    <span data-ttu-id="c5501-162">`AcquireTokenAsync(...)` first attempts to return a token for the requested resource (the Graph API in this case) without prompting users to enter their credentials (via caching or refreshing old tokens).</span><span class="sxs-lookup"><span data-stu-id="c5501-162">`AcquireTokenAsync(...)` first attempts to return a token for the requested resource (the Graph API in this case) without prompting users to enter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="c5501-163">As necessary, it shows users the Azure AD sign-in page before acquiring the requested token.</span><span class="sxs-lookup"><span data-stu-id="c5501-163">As necessary, it shows users the Azure AD sign-in page before acquiring the requested token.</span></span>
4. <span data-ttu-id="c5501-164">Attach the access token to the Graph API request in the **Authorization** header:</span><span class="sxs-lookup"><span data-stu-id="c5501-164">Attach the access token to the Graph API request in the **Authorization** header:</span></span>

    ```csharp
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="c5501-165">That's all for the `DirectorySearcher` PCL and the app's identity-related code.</span><span class="sxs-lookup"><span data-stu-id="c5501-165">That's all for the `DirectorySearcher` PCL and the app's identity-related code.</span></span> <span data-ttu-id="c5501-166">All that remains is to call the `SearchByAlias(...)` method in each platform's views and, where necessary, to add code for correctly handling the UI lifecycle.</span><span class="sxs-lookup"><span data-stu-id="c5501-166">All that remains is to call the `SearchByAlias(...)` method in each platform's views and, where necessary, to add code for correctly handling the UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="c5501-167">Android</span><span class="sxs-lookup"><span data-stu-id="c5501-167">Android</span></span>
1. <span data-ttu-id="c5501-168">In MainActivity.cs, add a call to `SearchByAlias(...)` in the button click handler:</span><span class="sxs-lookup"><span data-stu-id="c5501-168">In MainActivity.cs, add a call to `SearchByAlias(...)` in the button click handler:</span></span>

    ```csharp
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="c5501-169">Override the `OnActivityResult` lifecycle method to forward any authentication redirects back to the appropriate method.</span><span class="sxs-lookup"><span data-stu-id="c5501-169">Override the `OnActivityResult` lifecycle method to forward any authentication redirects back to the appropriate method.</span></span> <span data-ttu-id="c5501-170">ADAL provides a helper method for this in Android:</span><span class="sxs-lookup"><span data-stu-id="c5501-170">ADAL provides a helper method for this in Android:</span></span>

    ```csharp
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="c5501-171">Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="c5501-171">Windows Desktop</span></span>
<span data-ttu-id="c5501-172">In MainWindow.xaml.cs, make a call to `SearchByAlias(...)` by passing a `WindowInteropHelper` in the desktop's `PlatformParameters` object:</span><span class="sxs-lookup"><span data-stu-id="c5501-172">In MainWindow.xaml.cs, make a call to `SearchByAlias(...)` by passing a `WindowInteropHelper` in the desktop's `PlatformParameters` object:</span></span>

```csharp
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="c5501-173">iOS</span><span class="sxs-lookup"><span data-stu-id="c5501-173">iOS</span></span>
<span data-ttu-id="c5501-174">In DirSearchClient_iOSViewController.cs, the iOS `PlatformParameters` object takes a reference to the View Controller:</span><span class="sxs-lookup"><span data-stu-id="c5501-174">In DirSearchClient_iOSViewController.cs, the iOS `PlatformParameters` object takes a reference to the View Controller:</span></span>

```csharp
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="c5501-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="c5501-175">Windows Universal</span></span>
<span data-ttu-id="c5501-176">In Windows Universal, open MainPage.xaml.cs, and then implement the `Search` method.</span><span class="sxs-lookup"><span data-stu-id="c5501-176">In Windows Universal, open MainPage.xaml.cs, and then implement the `Search` method.</span></span> <span data-ttu-id="c5501-177">This method uses a helper method in a shared project to update UI as necessary.</span><span class="sxs-lookup"><span data-stu-id="c5501-177">This method uses a helper method in a shared project to update UI as necessary.</span></span>

```csharp
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="c5501-178">What's next</span><span class="sxs-lookup"><span data-stu-id="c5501-178">What's next</span></span>
<span data-ttu-id="c5501-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span><span class="sxs-lookup"><span data-stu-id="c5501-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="c5501-180">If you haven’t already populated your tenant with users, now is the time to do so.</span><span class="sxs-lookup"><span data-stu-id="c5501-180">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>

1. <span data-ttu-id="c5501-181">Run your DirectorySearcher app, and then sign in with one of the users.</span><span class="sxs-lookup"><span data-stu-id="c5501-181">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="c5501-182">Search for other users based on their UPN.</span><span class="sxs-lookup"><span data-stu-id="c5501-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="c5501-183">ADAL makes it easy to incorporate common identity features into the app.</span><span class="sxs-lookup"><span data-stu-id="c5501-183">ADAL makes it easy to incorporate common identity features into the app.</span></span> <span data-ttu-id="c5501-184">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span><span class="sxs-lookup"><span data-stu-id="c5501-184">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="c5501-185">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="c5501-185">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="c5501-186">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span><span class="sxs-lookup"><span data-stu-id="c5501-186">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="c5501-187">You can now move on to additional identity scenarios.</span><span class="sxs-lookup"><span data-stu-id="c5501-187">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="c5501-188">For example, try [Secure a .NET Web API with Azure AD](quickstart-v1-dotnet-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="c5501-188">For example, try [Secure a .NET Web API with Azure AD](quickstart-v1-dotnet-webapi.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
