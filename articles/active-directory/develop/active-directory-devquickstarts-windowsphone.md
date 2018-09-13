---
title: Azure AD Windows Phone Getting Started | Microsoft Docs
description: How to build a Windows Phone application that integrates with Azure AD for sign in and calls Azure AD protected APIs using OAuth.
services: active-directory
documentationcenter: windows
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: e3f8db4560efc4c1425e1e88f2afee97ba7a8fea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551484"
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="e452c-103">Integrate Azure AD with a Windows Phone App</span><span class="sxs-lookup"><span data-stu-id="e452c-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="e452c-104">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span><span class="sxs-lookup"><span data-stu-id="e452c-104">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="e452c-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span><span class="sxs-lookup"><span data-stu-id="e452c-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="e452c-106">This code sample uses ADAL v2.0.</span><span class="sxs-lookup"><span data-stu-id="e452c-106">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="e452c-107">For the latest technology, you may want to instead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="e452c-107">For the latest technology, you may want to instead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="e452c-108">If you are indeed building an app for Windows Phone 8.1, this is the right place.</span><span class="sxs-lookup"><span data-stu-id="e452c-108">If you are indeed building an app for Windows Phone 8.1, this is the right place.</span></span>  <span data-ttu-id="e452c-109">ADAL v2.0 is still fully supported, and is the recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e452c-109">ADAL v2.0 is still fully supported, and is the recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="e452c-110">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span><span class="sxs-lookup"><span data-stu-id="e452c-110">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="e452c-111">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span><span class="sxs-lookup"><span data-stu-id="e452c-111">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="e452c-112">To demonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span><span class="sxs-lookup"><span data-stu-id="e452c-112">To demonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="e452c-113">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="e452c-113">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="e452c-114">Searches a directory for users with a given UPN.</span><span class="sxs-lookup"><span data-stu-id="e452c-114">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="e452c-115">Signs users out.</span><span class="sxs-lookup"><span data-stu-id="e452c-115">Signs users out.</span></span>

<span data-ttu-id="e452c-116">To build the complete working application, you’ll need to:</span><span class="sxs-lookup"><span data-stu-id="e452c-116">To build the complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="e452c-117">Register your application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e452c-117">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="e452c-118">Install & Configure ADAL.</span><span class="sxs-lookup"><span data-stu-id="e452c-118">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="e452c-119">Use ADAL to get tokens from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e452c-119">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="e452c-120">To get started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="e452c-120">To get started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="e452c-121">Each is a Visual Studio 2013 solution.</span><span class="sxs-lookup"><span data-stu-id="e452c-121">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="e452c-122">You'll also need an Azure AD tenant in which you can create users and register an application.</span><span class="sxs-lookup"><span data-stu-id="e452c-122">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="e452c-123">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e452c-123">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directory-searcher-application"></a><span data-ttu-id="e452c-124">1. Register the Directory Searcher Application</span><span class="sxs-lookup"><span data-stu-id="e452c-124">1. Register the Directory Searcher Application</span></span>
<span data-ttu-id="e452c-125">To enable your app to get tokens, you’ll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="e452c-125">To enable your app to get tokens, you’ll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="e452c-126">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e452c-126">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e452c-127">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span><span class="sxs-lookup"><span data-stu-id="e452c-127">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="e452c-128">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e452c-128">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="e452c-129">Click on **App registrations** and choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="e452c-129">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="e452c-130">Follow the prompts and create a new **Native Client Application**.</span><span class="sxs-lookup"><span data-stu-id="e452c-130">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="e452c-131">The **Name** of the application will describe your application to end-users</span><span class="sxs-lookup"><span data-stu-id="e452c-131">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="e452c-132">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span><span class="sxs-lookup"><span data-stu-id="e452c-132">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="e452c-133">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="e452c-133">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="e452c-134">We'll replace this value later.</span><span class="sxs-lookup"><span data-stu-id="e452c-134">We'll replace this value later.</span></span>
6. <span data-ttu-id="e452c-135">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span><span class="sxs-lookup"><span data-stu-id="e452c-135">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="e452c-136">You’ll need this value in the next sections, so copy it from the application tab.</span><span class="sxs-lookup"><span data-stu-id="e452c-136">You’ll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="e452c-137">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="e452c-137">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="e452c-138">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span><span class="sxs-lookup"><span data-stu-id="e452c-138">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="e452c-139">This will enable your application to query the Graph API for users.</span><span class="sxs-lookup"><span data-stu-id="e452c-139">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="e452c-140">2. Install & Configure ADAL</span><span class="sxs-lookup"><span data-stu-id="e452c-140">2. Install & Configure ADAL</span></span>
<span data-ttu-id="e452c-141">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span><span class="sxs-lookup"><span data-stu-id="e452c-141">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="e452c-142">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span><span class="sxs-lookup"><span data-stu-id="e452c-142">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="e452c-143">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="e452c-143">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="e452c-144">In the DirectorySearcher project, open `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="e452c-144">In the DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="e452c-145">Replace the values in the `Config Values` region to reflect the values you input into the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e452c-145">Replace the values in the `Config Values` region to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="e452c-146">Your code will reference these values whenever it uses ADAL.</span><span class="sxs-lookup"><span data-stu-id="e452c-146">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="e452c-147">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="e452c-147">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="e452c-148">The `clientId` is the clientId of your application you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="e452c-148">The `clientId` is the clientId of your application you copied from the portal.</span></span>
* <span data-ttu-id="e452c-149">You now need to discover the callback uri for your Windows Phone app.</span><span class="sxs-lookup"><span data-stu-id="e452c-149">You now need to discover the callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="e452c-150">Set a breakpoint on this line in the `MainPage` method:</span><span class="sxs-lookup"><span data-stu-id="e452c-150">Set a breakpoint on this line in the `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="e452c-151">Run the app, and copy aside the value of `redirectUri` when the breakpoint is hit.</span><span class="sxs-lookup"><span data-stu-id="e452c-151">Run the app, and copy aside the value of `redirectUri` when the breakpoint is hit.</span></span>  <span data-ttu-id="e452c-152">It should look something like</span><span class="sxs-lookup"><span data-stu-id="e452c-152">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="e452c-153">Back on the **Configure** tab of your application in the Azure Management Portal, replace the value of the **RedirectUri** with this value.</span><span class="sxs-lookup"><span data-stu-id="e452c-153">Back on the **Configure** tab of your application in the Azure Management Portal, replace the value of the **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="e452c-154">3. Use ADAL to Get Tokens from AAD</span><span class="sxs-lookup"><span data-stu-id="e452c-154">3. Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="e452c-155">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span><span class="sxs-lookup"><span data-stu-id="e452c-155">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="e452c-156">The first step is to initialize your app’s `AuthenticationContext` - ADAL’s primary class.</span><span class="sxs-lookup"><span data-stu-id="e452c-156">The first step is to initialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="e452c-157">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span><span class="sxs-lookup"><span data-stu-id="e452c-157">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="e452c-158">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span><span class="sxs-lookup"><span data-stu-id="e452c-158">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="e452c-159">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span><span class="sxs-lookup"><span data-stu-id="e452c-159">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="e452c-160">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span><span class="sxs-lookup"><span data-stu-id="e452c-160">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try to get a token without triggering any user prompt.
    // ADAL will check whether the requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained the QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="e452c-161">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) to display the Azure AD sign in page.</span><span class="sxs-lookup"><span data-stu-id="e452c-161">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) to display the Azure AD sign in page.</span></span>  <span data-ttu-id="e452c-162">When the user signs in, your app needs to pass ADAL the results of the WAB interaction.</span><span class="sxs-lookup"><span data-stu-id="e452c-162">When the user signs in, your app needs to pass ADAL the results of the WAB interaction.</span></span>  <span data-ttu-id="e452c-163">This is as simple as implementing the `ContinueWebAuthentication` interface:</span><span class="sxs-lookup"><span data-stu-id="e452c-163">This is as simple as implementing the `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when the application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass the authentication interaction results to ADAL, which will
    // conclude the token acquisition operation and invoke the callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="e452c-164">Now it's time to use the `AuthenticationResult` that ADAL returned to your app.</span><span class="sxs-lookup"><span data-stu-id="e452c-164">Now it's time to use the `AuthenticationResult` that ADAL returned to your app.</span></span>  <span data-ttu-id="e452c-165">In the `QueryGraph(...)` callback, attach the access_token you acquired to the GET request in the Authorization header:</span><span class="sxs-lookup"><span data-stu-id="e452c-165">In the `QueryGraph(...)` callback, attach the access_token you acquired to the GET request in the Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add the access token to the Authorization Header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="e452c-166">You can also use the `AuthenticationResult` object to display information about the user in your app.</span><span class="sxs-lookup"><span data-stu-id="e452c-166">You can also use the `AuthenticationResult` object to display information about the user in your app.</span></span> <span data-ttu-id="e452c-167">In the `QueryGraph(...)` method, use the result to show the user's id on the page:</span><span class="sxs-lookup"><span data-stu-id="e452c-167">In the `QueryGraph(...)` method, use the result to show the user's id on the page:</span></span>

```C#
// Update the Page UI to represent the signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="e452c-168">Finally, you can use ADAL to sign the user out of hte application as well.</span><span class="sxs-lookup"><span data-stu-id="e452c-168">Finally, you can use ADAL to sign the user out of hte application as well.</span></span>  <span data-ttu-id="e452c-169">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenSilentAsync(...)` will fail.</span><span class="sxs-lookup"><span data-stu-id="e452c-169">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="e452c-170">With ADAL, this is as easy as clearing the token cache:</span><span class="sxs-lookup"><span data-stu-id="e452c-170">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from the token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="e452c-171">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="e452c-171">Congratulations!</span></span> <span data-ttu-id="e452c-172">You now have a working Windows Phone app that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span><span class="sxs-lookup"><span data-stu-id="e452c-172">You now have a working Windows Phone app that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="e452c-173">If you haven’t already, now is the time to populate your tenant with some users.</span><span class="sxs-lookup"><span data-stu-id="e452c-173">If you haven’t already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="e452c-174">Run your DirectorySearcher app, and sign in with one of those users.</span><span class="sxs-lookup"><span data-stu-id="e452c-174">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="e452c-175">Search for other users based on their UPN.</span><span class="sxs-lookup"><span data-stu-id="e452c-175">Search for other users based on their UPN.</span></span>  <span data-ttu-id="e452c-176">Close the app, and re-run it.</span><span class="sxs-lookup"><span data-stu-id="e452c-176">Close the app, and re-run it.</span></span>  <span data-ttu-id="e452c-177">Notice how the user’s session remains intact.</span><span class="sxs-lookup"><span data-stu-id="e452c-177">Notice how the user’s session remains intact.</span></span>  <span data-ttu-id="e452c-178">Sign out, and sign back in as another user.</span><span class="sxs-lookup"><span data-stu-id="e452c-178">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="e452c-179">ADAL makes it easy to incorporate all of these common identity features into your application.</span><span class="sxs-lookup"><span data-stu-id="e452c-179">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="e452c-180">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span><span class="sxs-lookup"><span data-stu-id="e452c-180">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="e452c-181">All you really need to know is a single API call, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="e452c-181">All you really need to know is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="e452c-182">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="e452c-182">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="e452c-183">You can now move on to additional identity scenarios.</span><span class="sxs-lookup"><span data-stu-id="e452c-183">You can now move on to additional identity scenarios.</span></span>  <span data-ttu-id="e452c-184">You may want to try:</span><span class="sxs-lookup"><span data-stu-id="e452c-184">You may want to try:</span></span>

[<span data-ttu-id="e452c-185">Secure a .NET Web API with Azure AD >></span><span class="sxs-lookup"><span data-stu-id="e452c-185">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

