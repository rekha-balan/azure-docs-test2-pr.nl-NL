---
title: Azure AD Windows Store Getting Started | Microsoft Docs
description: Build Windows Store apps that integrate with Azure AD for sign-in and call Azure AD protected APIs using OAuth.
services: active-directory
documentationcenter: windows
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: dastrock
ms.openlocfilehash: adfc28c7e41f49ce65309a316703fba57463040f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554554"
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="d2d54-103">Integrate Azure AD with Windows Store apps</span><span class="sxs-lookup"><span data-stu-id="d2d54-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="d2d54-104">If you're developing apps for the Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward to authenticate your users with their Active Directory accounts.</span><span class="sxs-lookup"><span data-stu-id="d2d54-104">If you're developing apps for the Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward to authenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="d2d54-105">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span><span class="sxs-lookup"><span data-stu-id="d2d54-105">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="d2d54-106">For Windows Store desktop apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="d2d54-106">For Windows Store desktop apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="d2d54-107">The sole purpose of ADAL is to make it easy for the app to get access tokens.</span><span class="sxs-lookup"><span data-stu-id="d2d54-107">The sole purpose of ADAL is to make it easy for the app to get access tokens.</span></span> <span data-ttu-id="d2d54-108">To demonstrate how easy it is, this article shows how to build a DirectorySearcher Windows Store app that:</span><span class="sxs-lookup"><span data-stu-id="d2d54-108">To demonstrate how easy it is, this article shows how to build a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="d2d54-109">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2d54-109">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="d2d54-110">Searches a directory for users with a given user principal name (UPN).</span><span class="sxs-lookup"><span data-stu-id="d2d54-110">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="d2d54-111">Signs users out.</span><span class="sxs-lookup"><span data-stu-id="d2d54-111">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="d2d54-112">Before you get started</span><span class="sxs-lookup"><span data-stu-id="d2d54-112">Before you get started</span></span>
* <span data-ttu-id="d2d54-113">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d2d54-113">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="d2d54-114">Each download is a Visual Studio 2015 solution.</span><span class="sxs-lookup"><span data-stu-id="d2d54-114">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="d2d54-115">You also need an Azure AD tenant in which to create users and register the app.</span><span class="sxs-lookup"><span data-stu-id="d2d54-115">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="d2d54-116">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="d2d54-116">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="d2d54-117">When you are ready, follow the procedures in the next three sections.</span><span class="sxs-lookup"><span data-stu-id="d2d54-117">When you are ready, follow the procedures in the next three sections.</span></span>

## <a name="step-1-register-the-directorysearcher-app"></a><span data-ttu-id="d2d54-118">Step 1: Register the DirectorySearcher app</span><span class="sxs-lookup"><span data-stu-id="d2d54-118">Step 1: Register the DirectorySearcher app</span></span>
<span data-ttu-id="d2d54-119">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="d2d54-119">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="d2d54-120">Here's how:</span><span class="sxs-lookup"><span data-stu-id="d2d54-120">Here's how:</span></span>

1. <span data-ttu-id="d2d54-121">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2d54-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d2d54-122">On the top bar, click your account.</span><span class="sxs-lookup"><span data-stu-id="d2d54-122">On the top bar, click your account.</span></span> <span data-ttu-id="d2d54-123">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span><span class="sxs-lookup"><span data-stu-id="d2d54-123">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="d2d54-124">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d2d54-124">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="d2d54-125">Click **App registrations**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="d2d54-125">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="d2d54-126">Follow the prompts to create a **Native Client Application**.</span><span class="sxs-lookup"><span data-stu-id="d2d54-126">Follow the prompts to create a **Native Client Application**.</span></span>
  * <span data-ttu-id="d2d54-127">**Name** describes the app to users.</span><span class="sxs-lookup"><span data-stu-id="d2d54-127">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="d2d54-128">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span><span class="sxs-lookup"><span data-stu-id="d2d54-128">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="d2d54-129">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="d2d54-129">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="d2d54-130">You'll replace the value later.</span><span class="sxs-lookup"><span data-stu-id="d2d54-130">You'll replace the value later.</span></span>
6. <span data-ttu-id="d2d54-131">After you’ve completed the registration, Azure AD assigns the app a unique application ID.</span><span class="sxs-lookup"><span data-stu-id="d2d54-131">After you’ve completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="d2d54-132">Copy the value on the **Application** tab, because you'll need it later.</span><span class="sxs-lookup"><span data-stu-id="d2d54-132">Copy the value on the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="d2d54-133">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="d2d54-133">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="d2d54-134">For the **Azure Active Directory** app, select **Microsoft Graph** as the API.</span><span class="sxs-lookup"><span data-stu-id="d2d54-134">For the **Azure Active Directory** app, select **Microsoft Graph** as the API.</span></span>
9. <span data-ttu-id="d2d54-135">Under **Delegated Permissions**, add the **Access the directory as the signed-in user** permission.</span><span class="sxs-lookup"><span data-stu-id="d2d54-135">Under **Delegated Permissions**, add the **Access the directory as the signed-in user** permission.</span></span> <span data-ttu-id="d2d54-136">Doing so enables the app to query the Graph API for users.</span><span class="sxs-lookup"><span data-stu-id="d2d54-136">Doing so enables the app to query the Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="d2d54-137">Step 2: Install and configure ADAL</span><span class="sxs-lookup"><span data-stu-id="d2d54-137">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="d2d54-138">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span><span class="sxs-lookup"><span data-stu-id="d2d54-138">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="d2d54-139">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span><span class="sxs-lookup"><span data-stu-id="d2d54-139">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="d2d54-140">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="d2d54-140">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="d2d54-141">In the DirectorySearcher project, open MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="d2d54-141">In the DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="d2d54-142">Replace the values in the **Config Values** region with the values that you entered in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d2d54-142">Replace the values in the **Config Values** region with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="d2d54-143">Your code refers to these values whenever it uses ADAL.</span><span class="sxs-lookup"><span data-stu-id="d2d54-143">Your code refers to these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="d2d54-144">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="d2d54-144">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="d2d54-145">The *clientId* is the client ID of the app, which you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="d2d54-145">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
4. <span data-ttu-id="d2d54-146">You now need to discover the callback URI for your Windows Store app.</span><span class="sxs-lookup"><span data-stu-id="d2d54-146">You now need to discover the callback URI for your Windows Store app.</span></span> <span data-ttu-id="d2d54-147">Set a breakpoint on this line in the `MainPage` method:</span><span class="sxs-lookup"><span data-stu-id="d2d54-147">Set a breakpoint on this line in the `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="d2d54-148">Build the solution, making sure that all package references are restored.</span><span class="sxs-lookup"><span data-stu-id="d2d54-148">Build the solution, making sure that all package references are restored.</span></span> <span data-ttu-id="d2d54-149">If any packages are missing, open the NuGet Package Manager and restore them.</span><span class="sxs-lookup"><span data-stu-id="d2d54-149">If any packages are missing, open the NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="d2d54-150">Run the app, and copy the value of `redirectUri` when the breakpoint is hit.</span><span class="sxs-lookup"><span data-stu-id="d2d54-150">Run the app, and copy the value of `redirectUri` when the breakpoint is hit.</span></span> <span data-ttu-id="d2d54-151">The value should look something like the following:</span><span class="sxs-lookup"><span data-stu-id="d2d54-151">The value should look something like the following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="d2d54-152">Back on the **Settings** tab of the app in the Azure portal, add a **RedirectUri** with the preceding value.</span><span class="sxs-lookup"><span data-stu-id="d2d54-152">Back on the **Settings** tab of the app in the Azure portal, add a **RedirectUri** with the preceding value.</span></span>  

## <a name="step-3-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="d2d54-153">Step 3: Use ADAL to get tokens from Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2d54-153">Step 3: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="d2d54-154">The basic principle behind ADAL is that whenever the app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span><span class="sxs-lookup"><span data-stu-id="d2d54-154">The basic principle behind ADAL is that whenever the app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="d2d54-155">Initialize the app’s `AuthenticationContext`, which is the primary class of ADAL.</span><span class="sxs-lookup"><span data-stu-id="d2d54-155">Initialize the app’s `AuthenticationContext`, which is the primary class of ADAL.</span></span> <span data-ttu-id="d2d54-156">This action passes ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span><span class="sxs-lookup"><span data-stu-id="d2d54-156">This action passes ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="d2d54-157">Locate the `Search(...)` method, which is invoked when users click the **Search** button on the app's UI.</span><span class="sxs-lookup"><span data-stu-id="d2d54-157">Locate the `Search(...)` method, which is invoked when users click the **Search** button on the app's UI.</span></span> <span data-ttu-id="d2d54-158">This method makes a get request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span><span class="sxs-lookup"><span data-stu-id="d2d54-158">This method makes a get request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="d2d54-159">To query the Graph API, include an access token in the request's **Authorization** header.</span><span class="sxs-lookup"><span data-stu-id="d2d54-159">To query the Graph API, include an access token in the request's **Authorization** header.</span></span> <span data-ttu-id="d2d54-160">This is where ADAL comes in.</span><span class="sxs-lookup"><span data-stu-id="d2d54-160">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="d2d54-161">When the app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts to return a token without asking the user for credentials.</span><span class="sxs-lookup"><span data-stu-id="d2d54-161">When the app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span> <span data-ttu-id="d2d54-162">If ADAL determines that the user needs to sign in to get a token, it displays a sign-in dialog box, collects the user's credentials, and returns a token after authentication succeeds.</span><span class="sxs-lookup"><span data-stu-id="d2d54-162">If ADAL determines that the user needs to sign in to get a token, it displays a sign-in dialog box, collects the user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="d2d54-163">If ADAL is unable to return a token for any reason, the *AuthenticationResult* status is an error.</span><span class="sxs-lookup"><span data-stu-id="d2d54-163">If ADAL is unable to return a token for any reason, the *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="d2d54-164">Now it's time to use the access token you just acquired.</span><span class="sxs-lookup"><span data-stu-id="d2d54-164">Now it's time to use the access token you just acquired.</span></span> <span data-ttu-id="d2d54-165">Also in the `Search(...)` method, attach the token to the Graph API get request in the **Authorization** header:</span><span class="sxs-lookup"><span data-stu-id="d2d54-165">Also in the `Search(...)` method, attach the token to the Graph API get request in the **Authorization** header:</span></span>

    ```C#
    // Add the access token to the Authorization header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="d2d54-166">You can use the `AuthenticationResult` object to display information about the user in the app, such as the user's ID:</span><span class="sxs-lookup"><span data-stu-id="d2d54-166">You can use the `AuthenticationResult` object to display information about the user in the app, such as the user's ID:</span></span>

    ```C#
    // Update the page UI to represent the signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="d2d54-167">You can also use ADAL to sign users out of the app.</span><span class="sxs-lookup"><span data-stu-id="d2d54-167">You can also use ADAL to sign users out of the app.</span></span> <span data-ttu-id="d2d54-168">When the user clicks the **Sign Out** button, ensure that the next call to `AcquireTokenAsync(...)` shows a sign-in view.</span><span class="sxs-lookup"><span data-stu-id="d2d54-168">When the user clicks the **Sign Out** button, ensure that the next call to `AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="d2d54-169">With ADAL, this action is as easy as clearing the token cache:</span><span class="sxs-lookup"><span data-stu-id="d2d54-169">With ADAL, this action is as easy as clearing the token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from the token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="d2d54-170">What's next</span><span class="sxs-lookup"><span data-stu-id="d2d54-170">What's next</span></span>
<span data-ttu-id="d2d54-171">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the user.</span><span class="sxs-lookup"><span data-stu-id="d2d54-171">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the user.</span></span>

<span data-ttu-id="d2d54-172">If you haven’t already populated your tenant with users, now is the time to do so.</span><span class="sxs-lookup"><span data-stu-id="d2d54-172">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>
1. <span data-ttu-id="d2d54-173">Run your DirectorySearcher app, and then sign in with one of the users.</span><span class="sxs-lookup"><span data-stu-id="d2d54-173">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="d2d54-174">Search for other users based on their UPN.</span><span class="sxs-lookup"><span data-stu-id="d2d54-174">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="d2d54-175">Close the app, and rerun it.</span><span class="sxs-lookup"><span data-stu-id="d2d54-175">Close the app, and rerun it.</span></span> <span data-ttu-id="d2d54-176">Notice how the user’s session remains intact.</span><span class="sxs-lookup"><span data-stu-id="d2d54-176">Notice how the user’s session remains intact.</span></span>
4. <span data-ttu-id="d2d54-177">Sign out by right-clicking to display the bottom bar, and then sign back in as another user.</span><span class="sxs-lookup"><span data-stu-id="d2d54-177">Sign out by right-clicking to display the bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="d2d54-178">ADAL makes it easy to incorporate all these common identity features into the app.</span><span class="sxs-lookup"><span data-stu-id="d2d54-178">ADAL makes it easy to incorporate all these common identity features into the app.</span></span> <span data-ttu-id="d2d54-179">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span><span class="sxs-lookup"><span data-stu-id="d2d54-179">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="d2d54-180">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="d2d54-180">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="d2d54-181">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span><span class="sxs-lookup"><span data-stu-id="d2d54-181">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="d2d54-182">You can now move on to additional identity scenarios.</span><span class="sxs-lookup"><span data-stu-id="d2d54-182">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="d2d54-183">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d2d54-183">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
