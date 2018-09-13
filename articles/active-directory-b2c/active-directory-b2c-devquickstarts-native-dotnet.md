---
title: Azure Active Directory B2C | Microsoft Docs
description: How to build a Windows desktop application that includes sign-in, sign-up, and profile management by using Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: ''
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8e2b5c704230ee2ba1395dc76a1551aaa8e7af7f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555026"
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="4907c-103">Azure AD B2C: Build a Windows desktop app</span><span class="sxs-lookup"><span data-stu-id="4907c-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="4907c-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your desktop app in a few short steps.</span><span class="sxs-lookup"><span data-stu-id="4907c-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your desktop app in a few short steps.</span></span> <span data-ttu-id="4907c-105">This article will show you how to create a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span><span class="sxs-lookup"><span data-stu-id="4907c-105">This article will show you how to create a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="4907c-106">The app will include support for sign-up and sign-in by using a user name or email.</span><span class="sxs-lookup"><span data-stu-id="4907c-106">The app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="4907c-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span><span class="sxs-lookup"><span data-stu-id="4907c-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="4907c-108">Get an Azure AD B2C directory</span><span class="sxs-lookup"><span data-stu-id="4907c-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="4907c-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span><span class="sxs-lookup"><span data-stu-id="4907c-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="4907c-110">A directory is a container for all of your users, apps, groups, and more.</span><span class="sxs-lookup"><span data-stu-id="4907c-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="4907c-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span><span class="sxs-lookup"><span data-stu-id="4907c-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="4907c-112">Create an application</span><span class="sxs-lookup"><span data-stu-id="4907c-112">Create an application</span></span>
<span data-ttu-id="4907c-113">Next, you need to create an app in your B2C directory.</span><span class="sxs-lookup"><span data-stu-id="4907c-113">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="4907c-114">This gives Azure AD information that it needs to securely communicate with your app.</span><span class="sxs-lookup"><span data-stu-id="4907c-114">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="4907c-115">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="4907c-115">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="4907c-116">Be sure to:</span><span class="sxs-lookup"><span data-stu-id="4907c-116">Be sure to:</span></span>

* <span data-ttu-id="4907c-117">Include a **native client** in the application.</span><span class="sxs-lookup"><span data-stu-id="4907c-117">Include a **native client** in the application.</span></span>
* <span data-ttu-id="4907c-118">Copy the **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="4907c-118">Copy the **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="4907c-119">It is the default URL for this code sample.</span><span class="sxs-lookup"><span data-stu-id="4907c-119">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="4907c-120">Copy the **Application ID** that is assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="4907c-120">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="4907c-121">You will need it later.</span><span class="sxs-lookup"><span data-stu-id="4907c-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="4907c-122">Create your policies</span><span class="sxs-lookup"><span data-stu-id="4907c-122">Create your policies</span></span>
<span data-ttu-id="4907c-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4907c-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4907c-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span><span class="sxs-lookup"><span data-stu-id="4907c-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="4907c-125">You need to create a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="4907c-125">You need to create a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="4907c-126">When you create the three policies, be sure to:</span><span class="sxs-lookup"><span data-stu-id="4907c-126">When you create the three policies, be sure to:</span></span>

* <span data-ttu-id="4907c-127">Choose either **User ID sign-up** or **Email sign-up** in the identity providers blade.</span><span class="sxs-lookup"><span data-stu-id="4907c-127">Choose either **User ID sign-up** or **Email sign-up** in the identity providers blade.</span></span>
* <span data-ttu-id="4907c-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span><span class="sxs-lookup"><span data-stu-id="4907c-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="4907c-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span><span class="sxs-lookup"><span data-stu-id="4907c-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="4907c-130">You can choose other claims as well.</span><span class="sxs-lookup"><span data-stu-id="4907c-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="4907c-131">Copy the **Name** of each policy after you create it.</span><span class="sxs-lookup"><span data-stu-id="4907c-131">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="4907c-132">It should have the prefix `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="4907c-132">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="4907c-133">You'll need these policy names later.</span><span class="sxs-lookup"><span data-stu-id="4907c-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="4907c-134">After you have successfully created the three policies, you're ready to build your app.</span><span class="sxs-lookup"><span data-stu-id="4907c-134">After you have successfully created the three policies, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="4907c-135">Download the code</span><span class="sxs-lookup"><span data-stu-id="4907c-135">Download the code</span></span>
<span data-ttu-id="4907c-136">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="4907c-136">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="4907c-137">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="4907c-137">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="4907c-138">You can also clone the skeleton:</span><span class="sxs-lookup"><span data-stu-id="4907c-138">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="4907c-139">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span><span class="sxs-lookup"><span data-stu-id="4907c-139">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

<span data-ttu-id="4907c-140">After you download the sample code, open the Visual Studio .sln file to get started.</span><span class="sxs-lookup"><span data-stu-id="4907c-140">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="4907c-141">The `TaskClient` project is the WPF desktop application that the user interacts with.</span><span class="sxs-lookup"><span data-stu-id="4907c-141">The `TaskClient` project is the WPF desktop application that the user interacts with.</span></span> <span data-ttu-id="4907c-142">For the purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span><span class="sxs-lookup"><span data-stu-id="4907c-142">For the purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="4907c-143">You do not need to build the web API, we already have it running for you.</span><span class="sxs-lookup"><span data-stu-id="4907c-143">You do not need to build the web API, we already have it running for you.</span></span>

<span data-ttu-id="4907c-144">To learn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4907c-144">To learn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="4907c-145">Execute policies</span><span class="sxs-lookup"><span data-stu-id="4907c-145">Execute policies</span></span>
<span data-ttu-id="4907c-146">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="4907c-146">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span></span> <span data-ttu-id="4907c-147">For .NET desktop applications, you can use the preview Microsoft Authentication Library (MSAL) to send OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span><span class="sxs-lookup"><span data-stu-id="4907c-147">For .NET desktop applications, you can use the preview Microsoft Authentication Library (MSAL) to send OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="4907c-148">Install MSAL</span><span class="sxs-lookup"><span data-stu-id="4907c-148">Install MSAL</span></span>
<span data-ttu-id="4907c-149">Add MSAL to the `TaskClient` project by using the Visual Studio Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="4907c-149">Add MSAL to the `TaskClient` project by using the Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="4907c-150">Enter your B2C details</span><span class="sxs-lookup"><span data-stu-id="4907c-150">Enter your B2C details</span></span>
<span data-ttu-id="4907c-151">Open the file `Globals.cs` and replace each of the property values with your own.</span><span class="sxs-lookup"><span data-stu-id="4907c-151">Open the file `Globals.cs` and replace each of the property values with your own.</span></span> <span data-ttu-id="4907c-152">This class is used throughout `TaskClient` to reference commonly used values.</span><span class="sxs-lookup"><span data-stu-id="4907c-152">This class is used throughout `TaskClient` to reference commonly used values.</span></span>

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-the-publicclientapplication"></a><span data-ttu-id="4907c-153">Create the PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="4907c-153">Create the PublicClientApplication</span></span>
<span data-ttu-id="4907c-154">The primary class of MSAL is `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="4907c-154">The primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="4907c-155">This class represents your application in the Azure AD B2C system.</span><span class="sxs-lookup"><span data-stu-id="4907c-155">This class represents your application in the Azure AD B2C system.</span></span> <span data-ttu-id="4907c-156">When the app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="4907c-156">When the app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="4907c-157">This can be used throughout the window.</span><span class="sxs-lookup"><span data-stu-id="4907c-157">This can be used throughout the window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens to persist when the user closes the app,
        // we've extended the MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="4907c-158">Initiate a sign-up flow</span><span class="sxs-lookup"><span data-stu-id="4907c-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="4907c-159">When a user opts to signs up, you want to initiate a sign-up flow that uses the sign-up policy you created.</span><span class="sxs-lookup"><span data-stu-id="4907c-159">When a user opts to signs up, you want to initiate a sign-up flow that uses the sign-up policy you created.</span></span> <span data-ttu-id="4907c-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="4907c-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="4907c-161">The parameters you pass to `AcquireTokenAsync(...)` determine which token you receive, the policy used in the authentication request, and more.</span><span class="sxs-lookup"><span data-stu-id="4907c-161">The parameters you pass to `AcquireTokenAsync(...)` determine which token you receive, the policy used in the authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use the app's clientId here as the scope parameter, indicating that
        // you want a token to the your app's backend web API (represented by
        // the cloud hosted task API).  Use the UiOptions.ForceLogin flag to
        // indicate to MSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in the app that the user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When the request completes successfully, you can get user
        // information from the AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After the sign up successfully completes, display the user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of the policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }

            MessageBox.Show(message);
        }

        return;
    }
}
```

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="4907c-162">Initiate a sign-in flow</span><span class="sxs-lookup"><span data-stu-id="4907c-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="4907c-163">You can initiate a sign-in flow in the same way that you initiate a sign-up flow.</span><span class="sxs-lookup"><span data-stu-id="4907c-163">You can initiate a sign-in flow in the same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="4907c-164">When a user signs in, make the same call to MSAL, this time by using your sign-in policy:</span><span class="sxs-lookup"><span data-stu-id="4907c-164">When a user signs in, make the same call to MSAL, this time by using your sign-in policy:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="4907c-165">Initiate an edit-profile flow</span><span class="sxs-lookup"><span data-stu-id="4907c-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="4907c-166">Again, you can execute an edit-profile policy in the same fashion:</span><span class="sxs-lookup"><span data-stu-id="4907c-166">Again, you can execute an edit-profile policy in the same fashion:</span></span>

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

<span data-ttu-id="4907c-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span><span class="sxs-lookup"><span data-stu-id="4907c-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="4907c-168">Each time you get a token from MSAL, you can use the `AuthenticationResult.User` object to update the user data in the app, such as the UI.</span><span class="sxs-lookup"><span data-stu-id="4907c-168">Each time you get a token from MSAL, you can use the `AuthenticationResult.User` object to update the user data in the app, such as the UI.</span></span> <span data-ttu-id="4907c-169">ADAL also caches the token for use in other parts of the application.</span><span class="sxs-lookup"><span data-stu-id="4907c-169">ADAL also caches the token for use in other parts of the application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="4907c-170">Check for tokens on app start</span><span class="sxs-lookup"><span data-stu-id="4907c-170">Check for tokens on app start</span></span>
<span data-ttu-id="4907c-171">You can also use MSAL to keep track of the user's sign-in state.</span><span class="sxs-lookup"><span data-stu-id="4907c-171">You can also use MSAL to keep track of the user's sign-in state.</span></span>  <span data-ttu-id="4907c-172">In this app, we want the user to remain signed in even after they close the app & re-open it.</span><span class="sxs-lookup"><span data-stu-id="4907c-172">In this app, we want the user to remain signed in even after they close the app & re-open it.</span></span>  <span data-ttu-id="4907c-173">Back inside the `OnInitialized` override, use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span><span class="sxs-lookup"><span data-stu-id="4907c-173">Back inside the `OnInitialized` override, use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If the user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in the cache.  Proceed without calling the To Do list service.
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
    return;
}
```

## <a name="call-the-task-api"></a><span data-ttu-id="4907c-174">Call the task API</span><span class="sxs-lookup"><span data-stu-id="4907c-174">Call the task API</span></span>
<span data-ttu-id="4907c-175">You have now used MSAL to execute policies and get tokens.</span><span class="sxs-lookup"><span data-stu-id="4907c-175">You have now used MSAL to execute policies and get tokens.</span></span>  <span data-ttu-id="4907c-176">When you want to use one these tokens to call the task API, you can again use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span><span class="sxs-lookup"><span data-stu-id="4907c-176">When you want to use one these tokens to call the task API, you can again use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want to check for a cached token, independent of whatever policy was used to acquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent to indicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch the exception and show the user a message.
    catch (MsalException ex)
    {
        // There is no access token in the cache, so prompt the user to sign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
        }
        else
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }
            MessageBox.Show(message);
        }

        return;
    }
    ...
```

<span data-ttu-id="4907c-177">When the call to `AcquireTokenSilentAsync(...)` succeeds and a token is found in the cache, you can add the token to the `Authorization` header of the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="4907c-177">When the call to `AcquireTokenSilentAsync(...)` succeeds and a token is found in the cache, you can add the token to the `Authorization` header of the HTTP request.</span></span> <span data-ttu-id="4907c-178">The task web API will use this header to authenticate the request to read the user's to-do list:</span><span class="sxs-lookup"><span data-stu-id="4907c-178">The task web API will use this header to authenticate the request to read the user's to-do list:</span></span>

```C#
    ...
    // Once the token has been returned by MSAL, add it to the http authorization header, before making the call to access the To Do list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call the To Do list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-the-user-out"></a><span data-ttu-id="4907c-179">Sign the user out</span><span class="sxs-lookup"><span data-stu-id="4907c-179">Sign the user out</span></span>
<span data-ttu-id="4907c-180">Finally, you can use MSAL to end a user's session with the app when the user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of the tokens from the token cache:</span><span class="sxs-lookup"><span data-stu-id="4907c-180">Finally, you can use MSAL to end a user's session with the app when the user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of the tokens from the token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of the user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in the browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update the UI to show the user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="4907c-181">Run the sample app</span><span class="sxs-lookup"><span data-stu-id="4907c-181">Run the sample app</span></span>
<span data-ttu-id="4907c-182">Finally, build and run the sample.</span><span class="sxs-lookup"><span data-stu-id="4907c-182">Finally, build and run the sample.</span></span>  <span data-ttu-id="4907c-183">Sign up for the app by using an email address or user name.</span><span class="sxs-lookup"><span data-stu-id="4907c-183">Sign up for the app by using an email address or user name.</span></span> <span data-ttu-id="4907c-184">Sign out and sign back in as the same user.</span><span class="sxs-lookup"><span data-stu-id="4907c-184">Sign out and sign back in as the same user.</span></span> <span data-ttu-id="4907c-185">Edit that user's profile.</span><span class="sxs-lookup"><span data-stu-id="4907c-185">Edit that user's profile.</span></span> <span data-ttu-id="4907c-186">Sign out and sign up by using a different user.</span><span class="sxs-lookup"><span data-stu-id="4907c-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="4907c-187">Add social IDPs</span><span class="sxs-lookup"><span data-stu-id="4907c-187">Add social IDPs</span></span>
<span data-ttu-id="4907c-188">Currently, the app supports only user sign-up and sign-in that use **local accounts**.</span><span class="sxs-lookup"><span data-stu-id="4907c-188">Currently, the app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="4907c-189">These are accounts stored in your B2C directory that use a user name and password.</span><span class="sxs-lookup"><span data-stu-id="4907c-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="4907c-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span><span class="sxs-lookup"><span data-stu-id="4907c-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="4907c-191">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span><span class="sxs-lookup"><span data-stu-id="4907c-191">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="4907c-192">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span><span class="sxs-lookup"><span data-stu-id="4907c-192">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="4907c-193">Set up Facebook as an IDP</span><span class="sxs-lookup"><span data-stu-id="4907c-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="4907c-194">Set up Google as an IDP</span><span class="sxs-lookup"><span data-stu-id="4907c-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="4907c-195">Set up Amazon as an IDP</span><span class="sxs-lookup"><span data-stu-id="4907c-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="4907c-196">Set up LinkedIn as an IDP</span><span class="sxs-lookup"><span data-stu-id="4907c-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="4907c-197">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4907c-197">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4907c-198">After you save your policies, run the app again.</span><span class="sxs-lookup"><span data-stu-id="4907c-198">After you save your policies, run the app again.</span></span> <span data-ttu-id="4907c-199">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span><span class="sxs-lookup"><span data-stu-id="4907c-199">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="4907c-200">You can experiment with your policies and observe the effects on your sample app.</span><span class="sxs-lookup"><span data-stu-id="4907c-200">You can experiment with your policies and observe the effects on your sample app.</span></span> <span data-ttu-id="4907c-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span><span class="sxs-lookup"><span data-stu-id="4907c-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="4907c-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span><span class="sxs-lookup"><span data-stu-id="4907c-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="4907c-203">For reference, the completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="4907c-203">For reference, the completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="4907c-204">You can also clone it from GitHub:</span><span class="sxs-lookup"><span data-stu-id="4907c-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
