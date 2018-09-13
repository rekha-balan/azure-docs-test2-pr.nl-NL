---
title: Add authentication to your Universal Windows Platform (UWP) app | Microsoft Docs
description: 'Learn how to use Azure App Service Mobile Apps to authenticate users of your Universal Windows Platform (UWP) app using a variety of identity providers, including: AAD, Google, Facebook, Twitter, and Microsoft.'
services: app-service\mobile
documentationcenter: windows
author: conceptdev
manager: panarasi
editor: ''
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 4cc597f8aca13445034c8a1691b41018d4d9bc4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804133"
---
# <a name="add-authentication-to-your-windows-app"></a><span data-ttu-id="3f26c-103">Add authentication to your Windows app</span><span class="sxs-lookup"><span data-stu-id="3f26c-103">Add authentication to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="3f26c-104">This topic shows you how to add cloud-based authentication to your mobile app.</span><span class="sxs-lookup"><span data-stu-id="3f26c-104">This topic shows you how to add cloud-based authentication to your mobile app.</span></span> <span data-ttu-id="3f26c-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3f26c-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="3f26c-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span><span class="sxs-lookup"><span data-stu-id="3f26c-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span></span>

<span data-ttu-id="3f26c-107">This tutorial is based on the Mobile Apps quickstart.</span><span class="sxs-lookup"><span data-stu-id="3f26c-107">This tutorial is based on the Mobile Apps quickstart.</span></span> <span data-ttu-id="3f26c-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3f26c-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <a name="register"></a><span data-ttu-id="3f26c-109">Register your app for authentication and configure the App Service</span><span class="sxs-lookup"><span data-stu-id="3f26c-109">Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a><span data-ttu-id="3f26c-110">Add your app to the Allowed External Redirect URLs</span><span class="sxs-lookup"><span data-stu-id="3f26c-110">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="3f26c-111">Secure authentication requires that you define a new URL scheme for your app.</span><span class="sxs-lookup"><span data-stu-id="3f26c-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="3f26c-112">This allows the authentication system to redirect back to your app once the authentication process is complete.</span><span class="sxs-lookup"><span data-stu-id="3f26c-112">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="3f26c-113">In this tutorial, we use the URL scheme _appname_ throughout.</span><span class="sxs-lookup"><span data-stu-id="3f26c-113">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="3f26c-114">However, you can use any URL scheme you choose.</span><span class="sxs-lookup"><span data-stu-id="3f26c-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="3f26c-115">It should be unique to your mobile application.</span><span class="sxs-lookup"><span data-stu-id="3f26c-115">It should be unique to your mobile application.</span></span> <span data-ttu-id="3f26c-116">To enable the redirection on the server side:</span><span class="sxs-lookup"><span data-stu-id="3f26c-116">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="3f26c-117">In the [Azure portal], select your App Service.</span><span class="sxs-lookup"><span data-stu-id="3f26c-117">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="3f26c-118">Click the **Authentication / Authorization** menu option.</span><span class="sxs-lookup"><span data-stu-id="3f26c-118">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="3f26c-119">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="3f26c-119">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="3f26c-120">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span><span class="sxs-lookup"><span data-stu-id="3f26c-120">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="3f26c-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span><span class="sxs-lookup"><span data-stu-id="3f26c-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="3f26c-122">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span><span class="sxs-lookup"><span data-stu-id="3f26c-122">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="3f26c-123">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f26c-123">Click **OK**.</span></span>

5. <span data-ttu-id="3f26c-124">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3f26c-124">Click **Save**.</span></span>

## <a name="permissions"></a><span data-ttu-id="3f26c-125">Restrict permissions to authenticated users</span><span class="sxs-lookup"><span data-stu-id="3f26c-125">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="3f26c-126">Now, you can verify that anonymous access to your backend has been disabled.</span><span class="sxs-lookup"><span data-stu-id="3f26c-126">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="3f26c-127">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="3f26c-127">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="3f26c-128">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span><span class="sxs-lookup"><span data-stu-id="3f26c-128">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="3f26c-129">Next, you will update the app to authenticate users before requesting resources from your App Service.</span><span class="sxs-lookup"><span data-stu-id="3f26c-129">Next, you will update the app to authenticate users before requesting resources from your App Service.</span></span>

## <a name="add-authentication"></a><span data-ttu-id="3f26c-130">Add authentication to the app</span><span class="sxs-lookup"><span data-stu-id="3f26c-130">Add authentication to the app</span></span>
1. <span data-ttu-id="3f26c-131">In the UWP app project file MainPage.xaml.cs and add the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="3f26c-131">In the UWP app project file MainPage.xaml.cs and add the following code snippet:</span></span>
   
        // Define a member variable for storing the signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs the authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' to the name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    <span data-ttu-id="3f26c-132">This code authenticates the user with a Facebook login.</span><span class="sxs-lookup"><span data-stu-id="3f26c-132">This code authenticates the user with a Facebook login.</span></span> <span data-ttu-id="3f26c-133">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span><span class="sxs-lookup"><span data-stu-id="3f26c-133">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span></span>
2. <span data-ttu-id="3f26c-134">Replace the **OnNavigatedTo()** method in MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="3f26c-134">Replace the **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="3f26c-135">Next, you will add a **Sign in** button to the app that triggers authentication.</span><span class="sxs-lookup"><span data-stu-id="3f26c-135">Next, you will add a **Sign in** button to the app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="3f26c-136">Add the following code snippet to the MainPage.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="3f26c-136">Add the following code snippet to the MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login the user and then load data from the mobile app.
            if (await AuthenticateAsync())
            {
                // Switch the buttons and load items from the mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="3f26c-137">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span><span class="sxs-lookup"><span data-stu-id="3f26c-137">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span></span>
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. <span data-ttu-id="3f26c-138">Add the following code snippet to the App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="3f26c-138">Add the following code snippet to the App.xaml.cs:</span></span>

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. <span data-ttu-id="3f26c-139">Open Package.appxmanifest file, navigate to **Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="3f26c-139">Open Package.appxmanifest file, navigate to **Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="3f26c-140">Now configure the **Properties** of the **Protocol** declaration.</span><span class="sxs-lookup"><span data-stu-id="3f26c-140">Now configure the **Properties** of the **Protocol** declaration.</span></span> <span data-ttu-id="3f26c-141">In **Display name**, add the name you wish to display to users of your application.</span><span class="sxs-lookup"><span data-stu-id="3f26c-141">In **Display name**, add the name you wish to display to users of your application.</span></span> <span data-ttu-id="3f26c-142">In **Name**, add your {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="3f26c-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="3f26c-143">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span><span class="sxs-lookup"><span data-stu-id="3f26c-143">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span></span> <span data-ttu-id="3f26c-144">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span><span class="sxs-lookup"><span data-stu-id="3f26c-144">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span></span>

## <a name="tokens"></a><span data-ttu-id="3f26c-145">Store the authentication token on the client</span><span class="sxs-lookup"><span data-stu-id="3f26c-145">Store the authentication token on the client</span></span>
<span data-ttu-id="3f26c-146">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span><span class="sxs-lookup"><span data-stu-id="3f26c-146">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span></span> <span data-ttu-id="3f26c-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span><span class="sxs-lookup"><span data-stu-id="3f26c-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span></span> <span data-ttu-id="3f26c-148">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span><span class="sxs-lookup"><span data-stu-id="3f26c-148">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="3f26c-149">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span><span class="sxs-lookup"><span data-stu-id="3f26c-149">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="3f26c-150">This tutorial uses service-managed authentication.</span><span class="sxs-lookup"><span data-stu-id="3f26c-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="3f26c-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f26c-151">Next steps</span></span>
<span data-ttu-id="3f26c-152">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="3f26c-152">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="3f26c-153">Add push notifications to your app</span><span class="sxs-lookup"><span data-stu-id="3f26c-153">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="3f26c-154">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="3f26c-154">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="3f26c-155">Enable offline sync for your app</span><span class="sxs-lookup"><span data-stu-id="3f26c-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="3f26c-156">Learn how to add offline support your app using an Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="3f26c-156">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="3f26c-157">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="3f26c-157">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
