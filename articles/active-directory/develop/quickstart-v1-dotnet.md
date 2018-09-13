---
title: Azure AD .NET Desktop (WPF) getting started | Microsoft Docs
description: How to build a .NET Windows Desktop application that integrates with Azure AD for sign in and calls Azure AD protected APIs using OAuth.
services: active-directory
documentationcenter: .net
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/30/2017
ms.author: celested
ms.reviewer: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c4bc777c36608ff9aeeec3428af0103fa3ae29c4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868968"
---
# <a name="azure-ad-net-desktop-wpf-getting-started"></a><span data-ttu-id="a220b-103">Azure AD .NET Desktop (WPF) getting started</span><span class="sxs-lookup"><span data-stu-id="a220b-103">Azure AD .NET Desktop (WPF) getting started</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="a220b-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span><span class="sxs-lookup"><span data-stu-id="a220b-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="a220b-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span><span class="sxs-lookup"><span data-stu-id="a220b-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="a220b-106">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span><span class="sxs-lookup"><span data-stu-id="a220b-106">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span> <span data-ttu-id="a220b-107">ADAL's sole purpose in life is to make it easy for your app to get access tokens.</span><span class="sxs-lookup"><span data-stu-id="a220b-107">ADAL's sole purpose in life is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="a220b-108">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span><span class="sxs-lookup"><span data-stu-id="a220b-108">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="a220b-109">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="a220b-109">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="a220b-110">Searches a directory for users with a given alias.</span><span class="sxs-lookup"><span data-stu-id="a220b-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="a220b-111">Signs users out.</span><span class="sxs-lookup"><span data-stu-id="a220b-111">Signs users out.</span></span>

<span data-ttu-id="a220b-112">To build the complete working application, you'll need to:</span><span class="sxs-lookup"><span data-stu-id="a220b-112">To build the complete working application, you'll need to:</span></span>

1. <span data-ttu-id="a220b-113">Register your application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a220b-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="a220b-114">Install & Configure ADAL.</span><span class="sxs-lookup"><span data-stu-id="a220b-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="a220b-115">Use ADAL to get tokens from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a220b-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="a220b-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a220b-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="a220b-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span><span class="sxs-lookup"><span data-stu-id="a220b-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="a220b-118">If you don't already have a tenant, [learn how to get one](quickstart-create-new-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="a220b-118">If you don't already have a tenant, [learn how to get one](quickstart-create-new-tenant.md).</span></span>

## <a name="1-register-the-directorysearcher-application"></a><span data-ttu-id="a220b-119">1. Register the DirectorySearcher Application</span><span class="sxs-lookup"><span data-stu-id="a220b-119">1. Register the DirectorySearcher Application</span></span>
<span data-ttu-id="a220b-120">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="a220b-120">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="a220b-121">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a220b-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a220b-122">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span><span class="sxs-lookup"><span data-stu-id="a220b-122">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="a220b-123">Click on **All services** in the left hand nav, and choose **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a220b-123">Click on **All services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="a220b-124">Click on **App registrations** and choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="a220b-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="a220b-125">Follow the prompts and create a new **Native Client Application**.</span><span class="sxs-lookup"><span data-stu-id="a220b-125">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="a220b-126">The **Name** of the application will describe your application to end-users</span><span class="sxs-lookup"><span data-stu-id="a220b-126">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="a220b-127">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span><span class="sxs-lookup"><span data-stu-id="a220b-127">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span> <span data-ttu-id="a220b-128">Enter a value specific to your application, e.g. `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="a220b-128">Enter a value specific to your application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="a220b-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span><span class="sxs-lookup"><span data-stu-id="a220b-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span> <span data-ttu-id="a220b-130">You'll need this value in the next sections, so copy it from the application page.</span><span class="sxs-lookup"><span data-stu-id="a220b-130">You'll need this value in the next sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="a220b-131">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="a220b-131">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="a220b-132">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span><span class="sxs-lookup"><span data-stu-id="a220b-132">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span> <span data-ttu-id="a220b-133">This will enable your application to query the Graph API for users.</span><span class="sxs-lookup"><span data-stu-id="a220b-133">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="a220b-134">2. Install & Configure ADAL</span><span class="sxs-lookup"><span data-stu-id="a220b-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="a220b-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span><span class="sxs-lookup"><span data-stu-id="a220b-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="a220b-136">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span><span class="sxs-lookup"><span data-stu-id="a220b-136">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="a220b-137">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="a220b-137">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="a220b-138">In the DirectorySearcher project, open `app.config`.</span><span class="sxs-lookup"><span data-stu-id="a220b-138">In the DirectorySearcher project, open `app.config`.</span></span> <span data-ttu-id="a220b-139">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a220b-139">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the Azure Portal.</span></span> <span data-ttu-id="a220b-140">Your code will reference these values whenever it uses ADAL.</span><span class="sxs-lookup"><span data-stu-id="a220b-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="a220b-141">The `ida:Tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="a220b-141">The `ida:Tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="a220b-142">The `ida:ClientId` is the clientId of your application you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="a220b-142">The `ida:ClientId` is the clientId of your application you copied from the portal.</span></span>
  * <span data-ttu-id="a220b-143">The `ida:RedirectUri` is the redirect url you registered in the portal.</span><span class="sxs-lookup"><span data-stu-id="a220b-143">The `ida:RedirectUri` is the redirect url you registered in the portal.</span></span>

## <a name="3-use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="a220b-144">3. Use ADAL to Get Tokens from AAD</span><span class="sxs-lookup"><span data-stu-id="a220b-144">3. Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="a220b-145">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does the rest.</span><span class="sxs-lookup"><span data-stu-id="a220b-145">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does the rest.</span></span> 

* <span data-ttu-id="a220b-146">In the `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate the `MainWindow()` method.</span><span class="sxs-lookup"><span data-stu-id="a220b-146">In the `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate the `MainWindow()` method.</span></span> <span data-ttu-id="a220b-147">The first step is to initialize your app's `AuthenticationContext` - ADAL's primary class.</span><span class="sxs-lookup"><span data-stu-id="a220b-147">The first step is to initialize your app's `AuthenticationContext` - ADAL's primary class.</span></span> <span data-ttu-id="a220b-148">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span><span class="sxs-lookup"><span data-stu-id="a220b-148">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```csharp
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="a220b-149">Now locate the `Search(...)` method, which will be invoked when the user clicks the "Search" button in the app's UI.</span><span class="sxs-lookup"><span data-stu-id="a220b-149">Now locate the `Search(...)` method, which will be invoked when the user clicks the "Search" button in the app's UI.</span></span> <span data-ttu-id="a220b-150">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span><span class="sxs-lookup"><span data-stu-id="a220b-150">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="a220b-151">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span><span class="sxs-lookup"><span data-stu-id="a220b-151">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```csharp
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate the Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for the To Do item name");
        return;
    }

    // Get an Access Token for the Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled the sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="a220b-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt to return a token without asking the user for credentials.</span><span class="sxs-lookup"><span data-stu-id="a220b-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt to return a token without asking the user for credentials.</span></span> <span data-ttu-id="a220b-153">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span><span class="sxs-lookup"><span data-stu-id="a220b-153">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span></span> <span data-ttu-id="a220b-154">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="a220b-154">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="a220b-155">Notice that the `AuthenticationResult` object contains a `UserInfo` object that can be used to collect information your app may need.</span><span class="sxs-lookup"><span data-stu-id="a220b-155">Notice that the `AuthenticationResult` object contains a `UserInfo` object that can be used to collect information your app may need.</span></span> <span data-ttu-id="a220b-156">In the DirectorySearcher, `UserInfo` is used to customize the app's UI with the user's id.</span><span class="sxs-lookup"><span data-stu-id="a220b-156">In the DirectorySearcher, `UserInfo` is used to customize the app's UI with the user's id.</span></span>
* <span data-ttu-id="a220b-157">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenAsync(...)` will ask the user to sign in.</span><span class="sxs-lookup"><span data-stu-id="a220b-157">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenAsync(...)` will ask the user to sign in.</span></span> <span data-ttu-id="a220b-158">With ADAL, this is as easy as clearing the token cache:</span><span class="sxs-lookup"><span data-stu-id="a220b-158">With ADAL, this is as easy as clearing the token cache:</span></span>

```csharp
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear the token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="a220b-159">However, if the user does not click the "Sign Out" button, you will want to maintain the user's session for the next time they run the DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="a220b-159">However, if the user does not click the "Sign Out" button, you will want to maintain the user's session for the next time they run the DirectorySearcher.</span></span> <span data-ttu-id="a220b-160">When the app launches, you can check ADAL's token cache for an existing token and update the UI accordingly.</span><span class="sxs-lookup"><span data-stu-id="a220b-160">When the app launches, you can check ADAL's token cache for an existing token and update the UI accordingly.</span></span> <span data-ttu-id="a220b-161">In the `CheckForCachedToken()` method, make another call to `AcquireTokenAsync(...)`, this time passing in the `PromptBehavior.Never` parameter.</span><span class="sxs-lookup"><span data-stu-id="a220b-161">In the `CheckForCachedToken()` method, make another call to `AcquireTokenAsync(...)`, this time passing in the `PromptBehavior.Never` parameter.</span></span> <span data-ttu-id="a220b-162">`PromptBehavior.Never` will tell ADAL that the user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable to return a token.</span><span class="sxs-lookup"><span data-stu-id="a220b-162">`PromptBehavior.Never` will tell ADAL that the user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable to return a token.</span></span>

```csharp
public async void CheckForCachedToken() 
{
    // As the application starts, try to get an access token without prompting the user. If one exists, show the user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed to main page without singing the user in.
        return;
    }

    // A valid token is in the cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="a220b-163">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="a220b-163">Congratulations!</span></span> <span data-ttu-id="a220b-164">You now have a working .NET WPF application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span><span class="sxs-lookup"><span data-stu-id="a220b-164">You now have a working .NET WPF application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="a220b-165">If you haven't already, now is the time to populate your tenant with some users.</span><span class="sxs-lookup"><span data-stu-id="a220b-165">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="a220b-166">Run your DirectorySearcher app, and sign in with one of those users.</span><span class="sxs-lookup"><span data-stu-id="a220b-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span> <span data-ttu-id="a220b-167">Search for other users based on their UPN.</span><span class="sxs-lookup"><span data-stu-id="a220b-167">Search for other users based on their UPN.</span></span> <span data-ttu-id="a220b-168">Close the app, and re-run it.</span><span class="sxs-lookup"><span data-stu-id="a220b-168">Close the app, and re-run it.</span></span> <span data-ttu-id="a220b-169">Notice how the user's session remains intact.</span><span class="sxs-lookup"><span data-stu-id="a220b-169">Notice how the user's session remains intact.</span></span> <span data-ttu-id="a220b-170">Sign out, and sign back in as another user.</span><span class="sxs-lookup"><span data-stu-id="a220b-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="a220b-171">ADAL makes it easy to incorporate all of these common identity features into your application.</span><span class="sxs-lookup"><span data-stu-id="a220b-171">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span> <span data-ttu-id="a220b-172">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span><span class="sxs-lookup"><span data-stu-id="a220b-172">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span> <span data-ttu-id="a220b-173">All you really need to know is a single API call, `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="a220b-173">All you really need to know is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="a220b-174">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a220b-174">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="a220b-175">You can now move on to additional scenarios.</span><span class="sxs-lookup"><span data-stu-id="a220b-175">You can now move on to additional scenarios.</span></span> <span data-ttu-id="a220b-176">You may want to try:</span><span class="sxs-lookup"><span data-stu-id="a220b-176">You may want to try:</span></span>

[<span data-ttu-id="a220b-177">Secure a .NET Web API with Azure AD >></span><span class="sxs-lookup"><span data-stu-id="a220b-177">Secure a .NET Web API with Azure AD >></span></span>](quickstart-v1-dotnet-webapi.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

