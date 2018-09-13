---
title: Azure AD v2 UWP getting started | Microsoft Docs
description: How Universal Windows Platform applications (UWP) can call an API that requires access tokens by the Azure Active Directory v2 endpoint
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: ''
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.component: develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/20/2018
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: cd6cf2e94b032408fd6c3b298294d84837e102a6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857547"
---
# <a name="call-microsoft-graph-api-from-a-universal-windows-platform-application-xaml"></a><span data-ttu-id="75d91-103">Call Microsoft Graph API from a Universal Windows Platform application (XAML)</span><span class="sxs-lookup"><span data-stu-id="75d91-103">Call Microsoft Graph API from a Universal Windows Platform application (XAML)</span></span>

<span data-ttu-id="75d91-104">This guide explains how a native Universal Windows Platform (UWP) application can request an access token and then call Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="75d91-104">This guide explains how a native Universal Windows Platform (UWP) application can request an access token and then call Microsoft Graph API.</span></span> <span data-ttu-id="75d91-105">The guide also applies to other APIs that require access tokens from the Azure Active Directory v2 endpoint.</span><span class="sxs-lookup"><span data-stu-id="75d91-105">The guide also applies to other APIs that require access tokens from the Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="75d91-106">At the end of this guide, your application calls a protected API by using personal accounts.</span><span class="sxs-lookup"><span data-stu-id="75d91-106">At the end of this guide, your application calls a protected API by using personal accounts.</span></span> <span data-ttu-id="75d91-107">Examples are outlook.com, live.com, and others.</span><span class="sxs-lookup"><span data-stu-id="75d91-107">Examples are outlook.com, live.com, and others.</span></span> <span data-ttu-id="75d91-108">Your application also calls work and school accounts from any company or organization that has Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="75d91-108">Your application also calls work and school accounts from any company or organization that has Azure Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="75d91-109">This guide requires Visual Studio 2017 with Universal Windows Platform development installed.</span><span class="sxs-lookup"><span data-stu-id="75d91-109">This guide requires Visual Studio 2017 with Universal Windows Platform development installed.</span></span> <span data-ttu-id="75d91-110">See [Get set up](https://docs.microsoft.com/windows/uwp/get-started/get-set-up) for instructions to download and configure Visual Studio to develop Universal Windows Platform apps.</span><span class="sxs-lookup"><span data-stu-id="75d91-110">See [Get set up](https://docs.microsoft.com/windows/uwp/get-started/get-set-up) for instructions to download and configure Visual Studio to develop Universal Windows Platform apps.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="75d91-111">How this guide works</span><span class="sxs-lookup"><span data-stu-id="75d91-111">How this guide works</span></span>

![How this guide works graph](./media/tutorial-v2-windows-uwp/uwp-intro.png)

<span data-ttu-id="75d91-113">This guide creates a sample UWP application that queries Microsoft Graph API or a Web API that accepts tokens from the Azure Active Directory v2 endpoint.</span><span class="sxs-lookup"><span data-stu-id="75d91-113">This guide creates a sample UWP application that queries Microsoft Graph API or a Web API that accepts tokens from the Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="75d91-114">For this scenario, a token is added to HTTP requests via the Authorization header.</span><span class="sxs-lookup"><span data-stu-id="75d91-114">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="75d91-115">Microsoft Authentication Library (MSAL) handles token acquisitions and renewals.</span><span class="sxs-lookup"><span data-stu-id="75d91-115">Microsoft Authentication Library (MSAL) handles token acquisitions and renewals.</span></span>

### <a name="nuget-packages"></a><span data-ttu-id="75d91-116">NuGet packages</span><span class="sxs-lookup"><span data-stu-id="75d91-116">NuGet packages</span></span>

<span data-ttu-id="75d91-117">This guide uses the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="75d91-117">This guide uses the following NuGet packages:</span></span>

|<span data-ttu-id="75d91-118">Library</span><span class="sxs-lookup"><span data-stu-id="75d91-118">Library</span></span>|<span data-ttu-id="75d91-119">Description</span><span class="sxs-lookup"><span data-stu-id="75d91-119">Description</span></span>|
|---|---|
|[<span data-ttu-id="75d91-120">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="75d91-120">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="75d91-121">Microsoft Authentication Library</span><span class="sxs-lookup"><span data-stu-id="75d91-121">Microsoft Authentication Library</span></span>|


## <a name="set-up-your-project"></a><span data-ttu-id="75d91-122">Set up your project</span><span class="sxs-lookup"><span data-stu-id="75d91-122">Set up your project</span></span>

<span data-ttu-id="75d91-123">This section provides step-by-step instructions to integrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="75d91-123">This section provides step-by-step instructions to integrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft*.</span></span> <span data-ttu-id="75d91-124">Then it can query Web APIs that require a token, such as Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="75d91-124">Then it can query Web APIs that require a token, such as Microsoft Graph API.</span></span>

<span data-ttu-id="75d91-125">This guide creates an application that displays a button that queries Graph API, a sign-out button, and text boxes that display the results of the calls.</span><span class="sxs-lookup"><span data-stu-id="75d91-125">This guide creates an application that displays a button that queries Graph API, a sign-out button, and text boxes that display the results of the calls.</span></span>

>[!NOTE]
> <span data-ttu-id="75d91-126">Do you want to download this sample's Visual Studio project instead?</span><span class="sxs-lookup"><span data-stu-id="75d91-126">Do you want to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="75d91-127">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-native-uwp-v2/archive/master.zip) and skip to the [application registration](#register-your-application "application registration step") step to configure the code sample before it runs.</span><span class="sxs-lookup"><span data-stu-id="75d91-127">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-native-uwp-v2/archive/master.zip) and skip to the [application registration](#register-your-application "application registration step") step to configure the code sample before it runs.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="75d91-128">Create your application</span><span class="sxs-lookup"><span data-stu-id="75d91-128">Create your application</span></span>
1. <span data-ttu-id="75d91-129">In Visual Studio, select **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="75d91-129">In Visual Studio, select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="75d91-130">Under **Templates**, select **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="75d91-130">Under **Templates**, select **Visual C#**.</span></span>
3. <span data-ttu-id="75d91-131">Select **Blank App (Universal Windows)**.</span><span class="sxs-lookup"><span data-stu-id="75d91-131">Select **Blank App (Universal Windows)**.</span></span>
4. <span data-ttu-id="75d91-132">Name the app, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="75d91-132">Name the app, and select **OK**.</span></span>
5. <span data-ttu-id="75d91-133">If prompted, select any version for **Target** and **Minimum** versions, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="75d91-133">If prompted, select any version for **Target** and **Minimum** versions, and select **OK**.</span></span>

    >![Minimum and Target versions](./media/tutorial-v2-windows-uwp/vs-minimum-target.png)

## <a name="add-microsoft-authentication-library-to-your-project"></a><span data-ttu-id="75d91-135">Add Microsoft Authentication Library to your project</span><span class="sxs-lookup"><span data-stu-id="75d91-135">Add Microsoft Authentication Library to your project</span></span>
1. <span data-ttu-id="75d91-136">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="75d91-136">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="75d91-137">Copy and paste the following command in the **Package Manager Console** window:</span><span class="sxs-lookup"><span data-stu-id="75d91-137">Copy and paste the following command in the **Package Manager Console** window:</span></span>

    ```powershell
    Install-Package Microsoft.Identity.Client -Pre -Version 1.1.4-preview0002
    ```

> [!NOTE]
> <span data-ttu-id="75d91-138">This command installs [Microsoft Authentication Library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet).</span><span class="sxs-lookup"><span data-stu-id="75d91-138">This command installs [Microsoft Authentication Library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet).</span></span> <span data-ttu-id="75d91-139">MSAL acquires, caches, and refreshes user tokens that access APIs protected by Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="75d91-139">MSAL acquires, caches, and refreshes user tokens that access APIs protected by Azure Active Directory v2.</span></span>

> [!NOTE]
> <span data-ttu-id="75d91-140">This tutorial does not use yet the latest version of MSAL.NET, but we are working on updating it.</span><span class="sxs-lookup"><span data-stu-id="75d91-140">This tutorial does not use yet the latest version of MSAL.NET, but we are working on updating it.</span></span>

## <a name="initialize-msal"></a><span data-ttu-id="75d91-141">Initialize MSAL</span><span class="sxs-lookup"><span data-stu-id="75d91-141">Initialize MSAL</span></span>
<span data-ttu-id="75d91-142">This step helps you create a class to handle interaction with MSAL, such as handling tokens.</span><span class="sxs-lookup"><span data-stu-id="75d91-142">This step helps you create a class to handle interaction with MSAL, such as handling tokens.</span></span>

1. <span data-ttu-id="75d91-143">Open the **App.xaml.cs** file and add the reference for MSAL to the class:</span><span class="sxs-lookup"><span data-stu-id="75d91-143">Open the **App.xaml.cs** file and add the reference for MSAL to the class:</span></span>

    ```csharp
    using Microsoft.Identity.Client;
    ```

2. <span data-ttu-id="75d91-144">Add the following two lines to the app's class (inside <code>sealed partial class App : Application</code> block):</span><span class="sxs-lookup"><span data-stu-id="75d91-144">Add the following two lines to the app's class (inside <code>sealed partial class App : Application</code> block):</span></span>

    ```csharp
    // Below is the clientId of your app registration. 
    // You have to replace the below with the Application Id for your app registration
    private static string ClientId = "your_client_id_here";
    
    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);
    ```

## <a name="create-your-applications-ui"></a><span data-ttu-id="75d91-145">Create your application’s UI</span><span class="sxs-lookup"><span data-stu-id="75d91-145">Create your application’s UI</span></span>

<span data-ttu-id="75d91-146">A **MainPage.xaml** file is created automatically as a part of your project template.</span><span class="sxs-lookup"><span data-stu-id="75d91-146">A **MainPage.xaml** file is created automatically as a part of your project template.</span></span> <span data-ttu-id="75d91-147">Open this file, and then follow the instructions:</span><span class="sxs-lookup"><span data-stu-id="75d91-147">Open this file, and then follow the instructions:</span></span>

* <span data-ttu-id="75d91-148">Replace your application’s **Grid** node with the following code:</span><span class="sxs-lookup"><span data-stu-id="75d91-148">Replace your application’s **Grid** node with the following code:</span></span>

    ```xml
    <Grid>
        <StackPanel Background="Azure">
            <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
                <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
                <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
            </StackPanel>
            <TextBlock Text="API Call Results" Margin="2,0,0,-5" FontFamily="Segoe Ui" />
            <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
            <TextBlock Text="Token Info" Margin="2,0,0,-5" FontFamily="Segoe Ui" />
            <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
        </StackPanel>
    </Grid>
    ```
    
## <a name="use-msal-to-get-a-token-for-microsoft-graph-api"></a><span data-ttu-id="75d91-149">Use MSAL to get a token for Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="75d91-149">Use MSAL to get a token for Microsoft Graph API</span></span>

<span data-ttu-id="75d91-150">This section shows how to use MSAL to get a token for Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="75d91-150">This section shows how to use MSAL to get a token for Microsoft Graph API.</span></span>

1.  <span data-ttu-id="75d91-151">In **MainPage.xaml.cs**, add the reference for MSAL to the class:</span><span class="sxs-lookup"><span data-stu-id="75d91-151">In **MainPage.xaml.cs**, add the reference for MSAL to the class:</span></span>

    ```csharp
    using Microsoft.Identity.Client;
    ```
2. <span data-ttu-id="75d91-152">Replace the code of your <code>MainPage</code> class with the following code:</span><span class="sxs-lookup"><span data-stu-id="75d91-152">Replace the code of your <code>MainPage</code> class with the following code:</span></span>

    ```csharp
    public sealed partial class MainPage : Page
    {
        // Set the API Endpoint to Graph 'me' endpoint
        string graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";
    
        // Set the scope for API call to user.read
        string[] scopes = new string[] { "user.read" };
    
        public MainPage()
        {
            this.InitializeComponent();
        }
    
        /// <summary>
        /// Call AcquireTokenAsync - to acquire a token requiring user to sign-in
        /// </summary>
        private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
        {
            AuthenticationResult authResult = null;
            ResultText.Text = string.Empty;
            TokenInfoText.Text = string.Empty;
    
            try
            {
                authResult = await App.PublicClientApp.AcquireTokenSilentAsync(scopes, App.PublicClientApp.Users.FirstOrDefault());
            }
            catch (MsalUiRequiredException ex)
            {
                // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need to call AcquireTokenAsync to acquire a token
                System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");
    
                try
                {
                    authResult = await App.PublicClientApp.AcquireTokenAsync(scopes);
                }
                catch (MsalException msalex)
                {
                    ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
                }
            }
            catch (Exception ex)
            {
                ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
                return;
            }
    
            if (authResult != null)
            {
                ResultText.Text = await GetHttpContentWithToken(graphAPIEndpoint, authResult.AccessToken);
                DisplayBasicTokenInfo(authResult);
                this.SignOutButton.Visibility = Visibility.Visible;
            }
        }
    }
    ```

### <a name="more-information"></a><span data-ttu-id="75d91-153">More information</span><span class="sxs-lookup"><span data-stu-id="75d91-153">More information</span></span>
#### <a name="get-a-user-token-interactively"></a><span data-ttu-id="75d91-154">Get a user token interactively</span><span class="sxs-lookup"><span data-stu-id="75d91-154">Get a user token interactively</span></span>
<span data-ttu-id="75d91-155">A call to the `AcquireTokenAsync` method results in a window that prompts users to sign in.</span><span class="sxs-lookup"><span data-stu-id="75d91-155">A call to the `AcquireTokenAsync` method results in a window that prompts users to sign in.</span></span> <span data-ttu-id="75d91-156">Applications usually require users to sign in interactively the first time they need to access a protected resource.</span><span class="sxs-lookup"><span data-stu-id="75d91-156">Applications usually require users to sign in interactively the first time they need to access a protected resource.</span></span> <span data-ttu-id="75d91-157">They might also need to sign in when a silent operation to acquire a token fails.</span><span class="sxs-lookup"><span data-stu-id="75d91-157">They might also need to sign in when a silent operation to acquire a token fails.</span></span> <span data-ttu-id="75d91-158">An example is when a user’s password is expired.</span><span class="sxs-lookup"><span data-stu-id="75d91-158">An example is when a user’s password is expired.</span></span>

#### <a name="get-a-user-token-silently"></a><span data-ttu-id="75d91-159">Get a user token silently</span><span class="sxs-lookup"><span data-stu-id="75d91-159">Get a user token silently</span></span>
<span data-ttu-id="75d91-160">The `AcquireTokenSilentAsync` method handles token acquisitions and renewals without any user interaction.</span><span class="sxs-lookup"><span data-stu-id="75d91-160">The `AcquireTokenSilentAsync` method handles token acquisitions and renewals without any user interaction.</span></span> <span data-ttu-id="75d91-161">After `AcquireTokenAsync` is executed for the first time and the user is prompted for credentials, the `AcquireTokenSilentAsync` method should be used to request tokens for subsequent calls because it acquire tokens silently.</span><span class="sxs-lookup"><span data-stu-id="75d91-161">After `AcquireTokenAsync` is executed for the first time and the user is prompted for credentials, the `AcquireTokenSilentAsync` method should be used to request tokens for subsequent calls because it acquire tokens silently.</span></span> <span data-ttu-id="75d91-162">MSAL will handle token cache and renewal.</span><span class="sxs-lookup"><span data-stu-id="75d91-162">MSAL will handle token cache and renewal.</span></span>

<span data-ttu-id="75d91-163">Eventually, the `AcquireTokenSilentAsync` method fails.</span><span class="sxs-lookup"><span data-stu-id="75d91-163">Eventually, the `AcquireTokenSilentAsync` method fails.</span></span> <span data-ttu-id="75d91-164">Reasons for failure might be that users have either signed out or changed their password on another device.</span><span class="sxs-lookup"><span data-stu-id="75d91-164">Reasons for failure might be that users have either signed out or changed their password on another device.</span></span> <span data-ttu-id="75d91-165">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException` exception.</span><span class="sxs-lookup"><span data-stu-id="75d91-165">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException` exception.</span></span> <span data-ttu-id="75d91-166">Your application can handle this exception in two ways:</span><span class="sxs-lookup"><span data-stu-id="75d91-166">Your application can handle this exception in two ways:</span></span>

* <span data-ttu-id="75d91-167">It can make a call against `AcquireTokenAsync` immediately.</span><span class="sxs-lookup"><span data-stu-id="75d91-167">It can make a call against `AcquireTokenAsync` immediately.</span></span> <span data-ttu-id="75d91-168">This call results in prompting the user to sign in.</span><span class="sxs-lookup"><span data-stu-id="75d91-168">This call results in prompting the user to sign in.</span></span> <span data-ttu-id="75d91-169">Normally, this pattern is used in online applications where there's no available offline content for the user.</span><span class="sxs-lookup"><span data-stu-id="75d91-169">Normally, this pattern is used in online applications where there's no available offline content for the user.</span></span> <span data-ttu-id="75d91-170">The sample generated by this guided setup follows the pattern.</span><span class="sxs-lookup"><span data-stu-id="75d91-170">The sample generated by this guided setup follows the pattern.</span></span> <span data-ttu-id="75d91-171">You see it in action the first time you run the sample.</span><span class="sxs-lookup"><span data-stu-id="75d91-171">You see it in action the first time you run the sample.</span></span> 
    * <span data-ttu-id="75d91-172">Because no user has used the application, `PublicClientApp.Users.FirstOrDefault()` contains a null value, and an `MsalUiRequiredException` exception is thrown.</span><span class="sxs-lookup"><span data-stu-id="75d91-172">Because no user has used the application, `PublicClientApp.Users.FirstOrDefault()` contains a null value, and an `MsalUiRequiredException` exception is thrown.</span></span>
    * <span data-ttu-id="75d91-173">The code in the sample then handles the exception by calling `AcquireTokenAsync`.</span><span class="sxs-lookup"><span data-stu-id="75d91-173">The code in the sample then handles the exception by calling `AcquireTokenAsync`.</span></span> <span data-ttu-id="75d91-174">This call results in prompting the user to sign in.</span><span class="sxs-lookup"><span data-stu-id="75d91-174">This call results in prompting the user to sign in.</span></span>

* <span data-ttu-id="75d91-175">Or instead, it presents a visual indication to users that an interactive sign in is required.</span><span class="sxs-lookup"><span data-stu-id="75d91-175">Or instead, it presents a visual indication to users that an interactive sign in is required.</span></span> <span data-ttu-id="75d91-176">Then they can select the right time to sign in.</span><span class="sxs-lookup"><span data-stu-id="75d91-176">Then they can select the right time to sign in.</span></span> <span data-ttu-id="75d91-177">Or the application can retry `AcquireTokenSilentAsync` later.</span><span class="sxs-lookup"><span data-stu-id="75d91-177">Or the application can retry `AcquireTokenSilentAsync` later.</span></span> <span data-ttu-id="75d91-178">Frequently, this pattern is used when users can use other application functionality without disruption.</span><span class="sxs-lookup"><span data-stu-id="75d91-178">Frequently, this pattern is used when users can use other application functionality without disruption.</span></span> <span data-ttu-id="75d91-179">An example is when offline content is available in the application.</span><span class="sxs-lookup"><span data-stu-id="75d91-179">An example is when offline content is available in the application.</span></span> <span data-ttu-id="75d91-180">In this case, users can decide when they want to sign in to either access the protected resource or refresh the outdated information.</span><span class="sxs-lookup"><span data-stu-id="75d91-180">In this case, users can decide when they want to sign in to either access the protected resource or refresh the outdated information.</span></span> <span data-ttu-id="75d91-181">Or else the application can decide to retry `AcquireTokenSilentAsync` when the network is restored after it was temporarily unavailable.</span><span class="sxs-lookup"><span data-stu-id="75d91-181">Or else the application can decide to retry `AcquireTokenSilentAsync` when the network is restored after it was temporarily unavailable.</span></span>

## <a name="call-microsoft-graph-api-by-using-the-token-you-just-obtained"></a><span data-ttu-id="75d91-182">Call Microsoft Graph API by using the token you just obtained</span><span class="sxs-lookup"><span data-stu-id="75d91-182">Call Microsoft Graph API by using the token you just obtained</span></span>

* <span data-ttu-id="75d91-183">Add the following new method to **MainPage.xaml.cs**.</span><span class="sxs-lookup"><span data-stu-id="75d91-183">Add the following new method to **MainPage.xaml.cs**.</span></span> <span data-ttu-id="75d91-184">This method is used to make a `GET` request against Graph API by using an [Authorize] header:</span><span class="sxs-lookup"><span data-stu-id="75d91-184">This method is used to make a `GET` request against Graph API by using an [Authorize] header:</span></span>

    ```csharp
    /// <summary>
    /// Perform an HTTP GET request to a URL using an HTTP Authorization header
    /// </summary>
    /// <param name="url">The URL</param>
    /// <param name="token">The token</param>
    /// <returns>String containing the results of the GET operation</returns>
    public async Task<string> GetHttpContentWithToken(string url, string token)
    {
        var httpClient = new System.Net.Http.HttpClient();
        System.Net.Http.HttpResponseMessage response;
        try
        {
            var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
            // Add the token in Authorization header
            request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
            response = await httpClient.SendAsync(request);
            var content = await response.Content.ReadAsStringAsync();
            return content;
        }
        catch (Exception ex)
        {
            return ex.ToString();
        }
    }
    ```

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="75d91-185">More information on making a REST call against a protected API</span><span class="sxs-lookup"><span data-stu-id="75d91-185">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="75d91-186">In this sample application, the `GetHttpContentWithToken` method is used to make an HTTP `GET` request against a protected resource that requires a token.</span><span class="sxs-lookup"><span data-stu-id="75d91-186">In this sample application, the `GetHttpContentWithToken` method is used to make an HTTP `GET` request against a protected resource that requires a token.</span></span> <span data-ttu-id="75d91-187">Then the method returns the content to the caller.</span><span class="sxs-lookup"><span data-stu-id="75d91-187">Then the method returns the content to the caller.</span></span> <span data-ttu-id="75d91-188">This method adds the acquired token in the **HTTP Authorization** header.</span><span class="sxs-lookup"><span data-stu-id="75d91-188">This method adds the acquired token in the **HTTP Authorization** header.</span></span> <span data-ttu-id="75d91-189">For this sample, the resource is the Microsoft Graph API **me** endpoint, which displays the user's profile information.</span><span class="sxs-lookup"><span data-stu-id="75d91-189">For this sample, the resource is the Microsoft Graph API **me** endpoint, which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-to-sign-out-the-user"></a><span data-ttu-id="75d91-190">Add a method to sign out the user</span><span class="sxs-lookup"><span data-stu-id="75d91-190">Add a method to sign out the user</span></span>

* <span data-ttu-id="75d91-191">To sign out the user, add the following method to **MainPage.xaml.cs**:</span><span class="sxs-lookup"><span data-stu-id="75d91-191">To sign out the user, add the following method to **MainPage.xaml.cs**:</span></span>

    ```csharp
    /// <summary>
    /// Sign out the current user
    /// </summary>
    private void SignOutButton_Click(object sender, RoutedEventArgs e)
    {
        if (App.PublicClientApp.Users.Any())
        {
            try
            {
                App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
                this.ResultText.Text = "User has signed-out";
                this.CallGraphButton.Visibility = Visibility.Visible;
                this.SignOutButton.Visibility = Visibility.Collapsed;
            }
            catch (MsalException ex)
            {
                ResultText.Text = $"Error signing-out user: {ex.Message}";
            }
        }
    }
    ```

### <a name="more-information-on-sign-out"></a><span data-ttu-id="75d91-192">More information on sign-out</span><span class="sxs-lookup"><span data-stu-id="75d91-192">More information on sign-out</span></span>

<span data-ttu-id="75d91-193">The `SignOutButton_Click` method removes the user from the MSAL user cache.</span><span class="sxs-lookup"><span data-stu-id="75d91-193">The `SignOutButton_Click` method removes the user from the MSAL user cache.</span></span> <span data-ttu-id="75d91-194">This method effectively tells MSAL to forget the current user.</span><span class="sxs-lookup"><span data-stu-id="75d91-194">This method effectively tells MSAL to forget the current user.</span></span> <span data-ttu-id="75d91-195">Then a future request to acquire a token succeeds only if it's made to be interactive.</span><span class="sxs-lookup"><span data-stu-id="75d91-195">Then a future request to acquire a token succeeds only if it's made to be interactive.</span></span>
<span data-ttu-id="75d91-196">The application in this sample supports a single user.</span><span class="sxs-lookup"><span data-stu-id="75d91-196">The application in this sample supports a single user.</span></span> <span data-ttu-id="75d91-197">But MSAL supports scenarios where more than one account can be signed in at the same time.</span><span class="sxs-lookup"><span data-stu-id="75d91-197">But MSAL supports scenarios where more than one account can be signed in at the same time.</span></span> <span data-ttu-id="75d91-198">An example is an email application where a user has several accounts.</span><span class="sxs-lookup"><span data-stu-id="75d91-198">An example is an email application where a user has several accounts.</span></span>

## <a name="display-basic-token-information"></a><span data-ttu-id="75d91-199">Display basic token information</span><span class="sxs-lookup"><span data-stu-id="75d91-199">Display basic token information</span></span>

* <span data-ttu-id="75d91-200">Add the following method to **MainPage.xaml.cs** to display basic information about the token:</span><span class="sxs-lookup"><span data-stu-id="75d91-200">Add the following method to **MainPage.xaml.cs** to display basic information about the token:</span></span>

    ```csharp
    /// <summary>
    /// Display basic information contained in the token
    /// </summary>
    private void DisplayBasicTokenInfo(AuthenticationResult authResult)
    {
        TokenInfoText.Text = "";
        if (authResult != null)
        {
            TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
            TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
            TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
            TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
        }
    }
    ```

### <a name="more-information"></a><span data-ttu-id="75d91-201">More information</span><span class="sxs-lookup"><span data-stu-id="75d91-201">More information</span></span>

<span data-ttu-id="75d91-202">ID tokens acquired via **OpenID Connect** also contain a small subset of information pertinent to the user.</span><span class="sxs-lookup"><span data-stu-id="75d91-202">ID tokens acquired via **OpenID Connect** also contain a small subset of information pertinent to the user.</span></span> <span data-ttu-id="75d91-203">`DisplayBasicTokenInfo` displays basic information contained in the token.</span><span class="sxs-lookup"><span data-stu-id="75d91-203">`DisplayBasicTokenInfo` displays basic information contained in the token.</span></span> <span data-ttu-id="75d91-204">Examples are the user's display name and ID, the expiration date of the token, and the string that represents the access token itself.</span><span class="sxs-lookup"><span data-stu-id="75d91-204">Examples are the user's display name and ID, the expiration date of the token, and the string that represents the access token itself.</span></span> <span data-ttu-id="75d91-205">If you select the **Call Microsoft Graph API** button several times, you'll see that the same token was reused for subsequent requests.</span><span class="sxs-lookup"><span data-stu-id="75d91-205">If you select the **Call Microsoft Graph API** button several times, you'll see that the same token was reused for subsequent requests.</span></span> <span data-ttu-id="75d91-206">You can also see the expiration date extended when MSAL decides it's time to renew the token.</span><span class="sxs-lookup"><span data-stu-id="75d91-206">You can also see the expiration date extended when MSAL decides it's time to renew the token.</span></span>

## <a name="register-your-application"></a><span data-ttu-id="75d91-207">Register your application</span><span class="sxs-lookup"><span data-stu-id="75d91-207">Register your application</span></span>

<span data-ttu-id="75d91-208">Now you need to register your application in the Microsoft Application Registration Portal:</span><span class="sxs-lookup"><span data-stu-id="75d91-208">Now you need to register your application in the Microsoft Application Registration Portal:</span></span>
1. <span data-ttu-id="75d91-209">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application.</span><span class="sxs-lookup"><span data-stu-id="75d91-209">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application.</span></span>
2. <span data-ttu-id="75d91-210">Enter a name for your application.</span><span class="sxs-lookup"><span data-stu-id="75d91-210">Enter a name for your application.</span></span>
3. <span data-ttu-id="75d91-211">Make sure that the option for **Guided Setup** is *not selected*.</span><span class="sxs-lookup"><span data-stu-id="75d91-211">Make sure that the option for **Guided Setup** is *not selected*.</span></span>
4. <span data-ttu-id="75d91-212">Select **Add Platforms**, select **Native Application**, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="75d91-212">Select **Add Platforms**, select **Native Application**, and then select **Save**.</span></span>
5. <span data-ttu-id="75d91-213">Copy the GUID in **Application ID**, go back to Visual Studio, open **App.xaml.cs**, and replace `your_client_id_here` with the Application ID you just registered:</span><span class="sxs-lookup"><span data-stu-id="75d91-213">Copy the GUID in **Application ID**, go back to Visual Studio, open **App.xaml.cs**, and replace `your_client_id_here` with the Application ID you just registered:</span></span>

    ```csharp
    private static string ClientId = "your_application_id_here";
    ```

## <a name="enable-integrated-authentication-on-federated-domains-optional"></a><span data-ttu-id="75d91-214">Enable integrated authentication on federated domains (optional)</span><span class="sxs-lookup"><span data-stu-id="75d91-214">Enable integrated authentication on federated domains (optional)</span></span>

<span data-ttu-id="75d91-215">To enable Windows Integrated Authentication when it's used with a federated Azure Active Directory domain, the application manifest must enable additional capabilities:</span><span class="sxs-lookup"><span data-stu-id="75d91-215">To enable Windows Integrated Authentication when it's used with a federated Azure Active Directory domain, the application manifest must enable additional capabilities:</span></span>

1. <span data-ttu-id="75d91-216">Double-click **Package.appxmanifest**.</span><span class="sxs-lookup"><span data-stu-id="75d91-216">Double-click **Package.appxmanifest**.</span></span>
2. <span data-ttu-id="75d91-217">Select the **Capabilities** tab and make sure that the following settings are enabled:</span><span class="sxs-lookup"><span data-stu-id="75d91-217">Select the **Capabilities** tab and make sure that the following settings are enabled:</span></span>

    - <span data-ttu-id="75d91-218">Enterprise Authentication</span><span class="sxs-lookup"><span data-stu-id="75d91-218">Enterprise Authentication</span></span>
    - <span data-ttu-id="75d91-219">Private Networks (Client & Server)</span><span class="sxs-lookup"><span data-stu-id="75d91-219">Private Networks (Client & Server)</span></span>
    - <span data-ttu-id="75d91-220">Shared User Certificates</span><span class="sxs-lookup"><span data-stu-id="75d91-220">Shared User Certificates</span></span>

3. <span data-ttu-id="75d91-221">Open **App.xaml.cs** and add the following line in the app constructor:</span><span class="sxs-lookup"><span data-stu-id="75d91-221">Open **App.xaml.cs** and add the following line in the app constructor:</span></span>

    ```csharp
    App.PublicClientApp.UseCorporateNetwork = true;
    ```

> [!IMPORTANT]
> <span data-ttu-id="75d91-222">Windows Integrated Authentication is not configured by default for this sample.</span><span class="sxs-lookup"><span data-stu-id="75d91-222">Windows Integrated Authentication is not configured by default for this sample.</span></span> <span data-ttu-id="75d91-223">Applications that request *Enterprise Authentication* or *Shared User Certificates* capabilities require a higher level of verification by the Windows Store.</span><span class="sxs-lookup"><span data-stu-id="75d91-223">Applications that request *Enterprise Authentication* or *Shared User Certificates* capabilities require a higher level of verification by the Windows Store.</span></span> <span data-ttu-id="75d91-224">Also, not all developers want to perform the higher level of verification.</span><span class="sxs-lookup"><span data-stu-id="75d91-224">Also, not all developers want to perform the higher level of verification.</span></span> <span data-ttu-id="75d91-225">Enable this setting only if you need Windows Integrated Authentication with a federated Azure Active Directory domain.</span><span class="sxs-lookup"><span data-stu-id="75d91-225">Enable this setting only if you need Windows Integrated Authentication with a federated Azure Active Directory domain.</span></span>


## <a name="test-your-code"></a><span data-ttu-id="75d91-226">Test your code</span><span class="sxs-lookup"><span data-stu-id="75d91-226">Test your code</span></span>

<span data-ttu-id="75d91-227">To test your application, select F5 to run your project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="75d91-227">To test your application, select F5 to run your project in Visual Studio.</span></span> <span data-ttu-id="75d91-228">Your main window appears:</span><span class="sxs-lookup"><span data-stu-id="75d91-228">Your main window appears:</span></span>

![Application's user interface](./media/tutorial-v2-windows-uwp/testapp-ui.png)

<span data-ttu-id="75d91-230">When you're ready to test, select **Call Microsoft Graph API**.</span><span class="sxs-lookup"><span data-stu-id="75d91-230">When you're ready to test, select **Call Microsoft Graph API**.</span></span> <span data-ttu-id="75d91-231">Then use a Microsoft Azure Active Directory organizational account or a Microsoft account, such as live.com or outlook.com, to sign in.</span><span class="sxs-lookup"><span data-stu-id="75d91-231">Then use a Microsoft Azure Active Directory organizational account or a Microsoft account, such as live.com or outlook.com, to sign in.</span></span> <span data-ttu-id="75d91-232">If it's your first time, you see a window asking the user to sign in:</span><span class="sxs-lookup"><span data-stu-id="75d91-232">If it's your first time, you see a window asking the user to sign in:</span></span>

![Sign-in page](./media/tutorial-v2-windows-uwp/sign-in-page.png)

### <a name="consent"></a><span data-ttu-id="75d91-234">Consent</span><span class="sxs-lookup"><span data-stu-id="75d91-234">Consent</span></span>
<span data-ttu-id="75d91-235">The first time you sign in to your application, you're presented with a consent screen similar to the following.</span><span class="sxs-lookup"><span data-stu-id="75d91-235">The first time you sign in to your application, you're presented with a consent screen similar to the following.</span></span> <span data-ttu-id="75d91-236">Select **Yes** to explicitly consent to access:</span><span class="sxs-lookup"><span data-stu-id="75d91-236">Select **Yes** to explicitly consent to access:</span></span>

![Access consent screen](./media/tutorial-v2-windows-uwp/consentscreen.png)
### <a name="expected-results"></a><span data-ttu-id="75d91-238">Expected results</span><span class="sxs-lookup"><span data-stu-id="75d91-238">Expected results</span></span>
<span data-ttu-id="75d91-239">You see user profile information returned by the Microsoft Graph API call on the **API Call Results** screen:</span><span class="sxs-lookup"><span data-stu-id="75d91-239">You see user profile information returned by the Microsoft Graph API call on the **API Call Results** screen:</span></span>

![API Call Results screen](./media/tutorial-v2-windows-uwp/uwp-results-screen.PNG)

<span data-ttu-id="75d91-241">You also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the **Token Info** box:</span><span class="sxs-lookup"><span data-stu-id="75d91-241">You also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the **Token Info** box:</span></span>

|<span data-ttu-id="75d91-242">Property</span><span class="sxs-lookup"><span data-stu-id="75d91-242">Property</span></span>  |<span data-ttu-id="75d91-243">Format</span><span class="sxs-lookup"><span data-stu-id="75d91-243">Format</span></span>  |<span data-ttu-id="75d91-244">Description</span><span class="sxs-lookup"><span data-stu-id="75d91-244">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="75d91-245">**Name**</span><span class="sxs-lookup"><span data-stu-id="75d91-245">**Name**</span></span> |<span data-ttu-id="75d91-246">User's full name</span><span class="sxs-lookup"><span data-stu-id="75d91-246">User's full name</span></span>|<span data-ttu-id="75d91-247">The user’s first and last name.</span><span class="sxs-lookup"><span data-stu-id="75d91-247">The user’s first and last name.</span></span>|
|<span data-ttu-id="75d91-248">**Username**</span><span class="sxs-lookup"><span data-stu-id="75d91-248">**Username**</span></span> |<span>user@domain.com</span> |<span data-ttu-id="75d91-249">The username that identifies the user.</span><span class="sxs-lookup"><span data-stu-id="75d91-249">The username that identifies the user.</span></span>|
|<span data-ttu-id="75d91-250">**Token Expires**</span><span class="sxs-lookup"><span data-stu-id="75d91-250">**Token Expires**</span></span> |<span data-ttu-id="75d91-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="75d91-251">DateTime</span></span> |<span data-ttu-id="75d91-252">The time when the token expires.</span><span class="sxs-lookup"><span data-stu-id="75d91-252">The time when the token expires.</span></span> <span data-ttu-id="75d91-253">MSAL extends the expiration date by renewing the token as necessary.</span><span class="sxs-lookup"><span data-stu-id="75d91-253">MSAL extends the expiration date by renewing the token as necessary.</span></span>|
|<span data-ttu-id="75d91-254">**Access Token**</span><span class="sxs-lookup"><span data-stu-id="75d91-254">**Access Token**</span></span> |<span data-ttu-id="75d91-255">String</span><span class="sxs-lookup"><span data-stu-id="75d91-255">String</span></span> |<span data-ttu-id="75d91-256">The token string that is sent to HTTP requests that require an *Authorization header*.</span><span class="sxs-lookup"><span data-stu-id="75d91-256">The token string that is sent to HTTP requests that require an *Authorization header*.</span></span>|

#### <a name="see-whats-in-the-access-token-optional"></a><span data-ttu-id="75d91-257">See what's in the access token (optional)</span><span class="sxs-lookup"><span data-stu-id="75d91-257">See what's in the access token (optional)</span></span>
<span data-ttu-id="75d91-258">Optionally, copy the value in **Access Token** and paste it in https://jwt.ms to decode it and see the list of claims.</span><span class="sxs-lookup"><span data-stu-id="75d91-258">Optionally, copy the value in **Access Token** and paste it in https://jwt.ms to decode it and see the list of claims.</span></span>

### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="75d91-259">More information about scopes and delegated permissions</span><span class="sxs-lookup"><span data-stu-id="75d91-259">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="75d91-260">Microsoft Graph API requires the *user.read* scope to read a user's profile.</span><span class="sxs-lookup"><span data-stu-id="75d91-260">Microsoft Graph API requires the *user.read* scope to read a user's profile.</span></span> <span data-ttu-id="75d91-261">This scope is added automatically by default in every application that's registered in the Application Registration Portal.</span><span class="sxs-lookup"><span data-stu-id="75d91-261">This scope is added automatically by default in every application that's registered in the Application Registration Portal.</span></span> <span data-ttu-id="75d91-262">Other APIs for Microsoft Graph, and custom APIs for your back-end server, might require additional scopes.</span><span class="sxs-lookup"><span data-stu-id="75d91-262">Other APIs for Microsoft Graph, and custom APIs for your back-end server, might require additional scopes.</span></span> <span data-ttu-id="75d91-263">Microsoft Graph API requires the *Calendars.Read* scope to list the user’s calendars.</span><span class="sxs-lookup"><span data-stu-id="75d91-263">Microsoft Graph API requires the *Calendars.Read* scope to list the user’s calendars.</span></span>

<span data-ttu-id="75d91-264">To access the user’s calendars in the context of an application, add the *Calendars.Read* delegated permission to the application registration information.</span><span class="sxs-lookup"><span data-stu-id="75d91-264">To access the user’s calendars in the context of an application, add the *Calendars.Read* delegated permission to the application registration information.</span></span> <span data-ttu-id="75d91-265">Then add the *Calendars.Read* scope to the `acquireTokenSilent` call.</span><span class="sxs-lookup"><span data-stu-id="75d91-265">Then add the *Calendars.Read* scope to the `acquireTokenSilent` call.</span></span> 

> [!NOTE]
> <span data-ttu-id="75d91-266">Users might be prompted for additional consents as you increase the number of scopes.</span><span class="sxs-lookup"><span data-stu-id="75d91-266">Users might be prompted for additional consents as you increase the number of scopes.</span></span>

## <a name="known-issues"></a><span data-ttu-id="75d91-267">Known issues</span><span class="sxs-lookup"><span data-stu-id="75d91-267">Known issues</span></span>

### <a name="issue-1"></a><span data-ttu-id="75d91-268">Issue 1</span><span class="sxs-lookup"><span data-stu-id="75d91-268">Issue 1</span></span>
<span data-ttu-id="75d91-269">You receive one of the following error messages when you sign in on your application on a federated Azure Active Directory domain:</span><span class="sxs-lookup"><span data-stu-id="75d91-269">You receive one of the following error messages when you sign in on your application on a federated Azure Active Directory domain:</span></span>
 - <span data-ttu-id="75d91-270">No valid client certificate found in the request.</span><span class="sxs-lookup"><span data-stu-id="75d91-270">No valid client certificate found in the request.</span></span>
 - <span data-ttu-id="75d91-271">No valid certificates found in the user's certificate store.</span><span class="sxs-lookup"><span data-stu-id="75d91-271">No valid certificates found in the user's certificate store.</span></span>
 - <span data-ttu-id="75d91-272">Try again choosing a different authentication method.</span><span class="sxs-lookup"><span data-stu-id="75d91-272">Try again choosing a different authentication method.</span></span>

<span data-ttu-id="75d91-273">**Cause:** Enterprise and certificate capabilities aren't enabled.</span><span class="sxs-lookup"><span data-stu-id="75d91-273">**Cause:** Enterprise and certificate capabilities aren't enabled.</span></span>

<span data-ttu-id="75d91-274">**Solution:** Follow the steps in [integrated authentication on federated domains](#enable-integrated-authentication-on-federated-domains-optional).</span><span class="sxs-lookup"><span data-stu-id="75d91-274">**Solution:** Follow the steps in [integrated authentication on federated domains](#enable-integrated-authentication-on-federated-domains-optional).</span></span>

### <a name="issue-2"></a><span data-ttu-id="75d91-275">Issue 2</span><span class="sxs-lookup"><span data-stu-id="75d91-275">Issue 2</span></span>
<span data-ttu-id="75d91-276">You enable [integrated authentication on federated domains](#enable-integrated-authentication-on-federated-domains-optional) and try to use Windows Hello on a Windows 10 computer to sign in on an environment with multifactor authentication configured.</span><span class="sxs-lookup"><span data-stu-id="75d91-276">You enable [integrated authentication on federated domains](#enable-integrated-authentication-on-federated-domains-optional) and try to use Windows Hello on a Windows 10 computer to sign in on an environment with multifactor authentication configured.</span></span> <span data-ttu-id="75d91-277">The list of certificates is presented.</span><span class="sxs-lookup"><span data-stu-id="75d91-277">The list of certificates is presented.</span></span> <span data-ttu-id="75d91-278">However, if you choose to use your PIN, the PIN window is never presented.</span><span class="sxs-lookup"><span data-stu-id="75d91-278">However, if you choose to use your PIN, the PIN window is never presented.</span></span>

<span data-ttu-id="75d91-279">**Cause:** This issue is a known limitation of the web authentication broker in UWP applications that run on Windows 10 desktop.</span><span class="sxs-lookup"><span data-stu-id="75d91-279">**Cause:** This issue is a known limitation of the web authentication broker in UWP applications that run on Windows 10 desktop.</span></span> <span data-ttu-id="75d91-280">It works fine on Windows 10 Mobile.</span><span class="sxs-lookup"><span data-stu-id="75d91-280">It works fine on Windows 10 Mobile.</span></span>

<span data-ttu-id="75d91-281">**Workaround:** Select **Sign in with other options**.</span><span class="sxs-lookup"><span data-stu-id="75d91-281">**Workaround:** Select **Sign in with other options**.</span></span> <span data-ttu-id="75d91-282">Then select **Sign in with a username and password**.</span><span class="sxs-lookup"><span data-stu-id="75d91-282">Then select **Sign in with a username and password**.</span></span> <span data-ttu-id="75d91-283">Select **Provide your password**.</span><span class="sxs-lookup"><span data-stu-id="75d91-283">Select **Provide your password**.</span></span> <span data-ttu-id="75d91-284">Then go through the phone authentication process.</span><span class="sxs-lookup"><span data-stu-id="75d91-284">Then go through the phone authentication process.</span></span>
