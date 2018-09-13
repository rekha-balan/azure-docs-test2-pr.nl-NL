---
title: Add authentication to your Universal Windows Platform (UWP) app | Microsoft Docs
description: 'Learn how to use Azure App Service Mobile Apps to authenticate users of your Universal Windows Platform (UWP) app using a variety of identity providers, including: AAD, Google, Facebook, Twitter, and Microsoft.'
services: app-service\mobile
documentationcenter: windows
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: 96b87d4d6cc1adbc9700102ffd4a989451676d81
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550638"
---
# <a name="add-authentication-to-your-windows-app"></a><span data-ttu-id="93206-103">Add authentication to your Windows app</span><span class="sxs-lookup"><span data-stu-id="93206-103">Add authentication to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="93206-104">This topic shows you how to add cloud-based authentication to your mobile app.</span><span class="sxs-lookup"><span data-stu-id="93206-104">This topic shows you how to add cloud-based authentication to your mobile app.</span></span> <span data-ttu-id="93206-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="93206-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="93206-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span><span class="sxs-lookup"><span data-stu-id="93206-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span></span>

<span data-ttu-id="93206-107">This tutorial is based on the Mobile Apps quickstart.</span><span class="sxs-lookup"><span data-stu-id="93206-107">This tutorial is based on the Mobile Apps quickstart.</span></span> <span data-ttu-id="93206-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="93206-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <a name="register"></a><span data-ttu-id="93206-109">Register your app for authentication and configure the App Service</span><span class="sxs-lookup"><span data-stu-id="93206-109">Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="permissions"></a><span data-ttu-id="93206-110">Restrict permissions to authenticated users</span><span class="sxs-lookup"><span data-stu-id="93206-110">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="93206-111">Now, you can verify that anonymous access to your backend has been disabled.</span><span class="sxs-lookup"><span data-stu-id="93206-111">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="93206-112">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="93206-112">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="93206-113">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span><span class="sxs-lookup"><span data-stu-id="93206-113">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="93206-114">Next, you will update the app to authenticate users before requesting resources from your App Service.</span><span class="sxs-lookup"><span data-stu-id="93206-114">Next, you will update the app to authenticate users before requesting resources from your App Service.</span></span>

## <a name="add-authentication"></a><span data-ttu-id="93206-115">Add authentication to the app</span><span class="sxs-lookup"><span data-stu-id="93206-115">Add authentication to the app</span></span>
1. <span data-ttu-id="93206-116">In the UWP app project file MainPage.cs and add the following code snippet to the MainPage class:</span><span class="sxs-lookup"><span data-stu-id="93206-116">In the UWP app project file MainPage.cs and add the following code snippet to the MainPage class:</span></span>
   
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
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
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
   
    <span data-ttu-id="93206-117">This code authenticates the user with a Facebook login.</span><span class="sxs-lookup"><span data-stu-id="93206-117">This code authenticates the user with a Facebook login.</span></span> <span data-ttu-id="93206-118">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span><span class="sxs-lookup"><span data-stu-id="93206-118">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span></span>
2. <span data-ttu-id="93206-119">Comment-out or delete the call to the **ButtonRefresh_Click** method (or the **InitLocalStoreAsync** method) in the existing **OnNavigatedTo** method override.</span><span class="sxs-lookup"><span data-stu-id="93206-119">Comment-out or delete the call to the **ButtonRefresh_Click** method (or the **InitLocalStoreAsync** method) in the existing **OnNavigatedTo** method override.</span></span> <span data-ttu-id="93206-120">This prevents the data from being loaded before the user is authenticated.</span><span class="sxs-lookup"><span data-stu-id="93206-120">This prevents the data from being loaded before the user is authenticated.</span></span> <span data-ttu-id="93206-121">Next, you will add a **Sign in** button to the app that triggers authentication.</span><span class="sxs-lookup"><span data-stu-id="93206-121">Next, you will add a **Sign in** button to the app that triggers authentication.</span></span>
3. <span data-ttu-id="93206-122">Add the following code snippet to the MainPage class:</span><span class="sxs-lookup"><span data-stu-id="93206-122">Add the following code snippet to the MainPage class:</span></span>
   
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
4. <span data-ttu-id="93206-123">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span><span class="sxs-lookup"><span data-stu-id="93206-123">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span></span>
   
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
5. <span data-ttu-id="93206-124">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span><span class="sxs-lookup"><span data-stu-id="93206-124">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span></span> <span data-ttu-id="93206-125">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span><span class="sxs-lookup"><span data-stu-id="93206-125">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span></span>

## <a name="tokens"></a><span data-ttu-id="93206-126">Store the authentication token on the client</span><span class="sxs-lookup"><span data-stu-id="93206-126">Store the authentication token on the client</span></span>
<span data-ttu-id="93206-127">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span><span class="sxs-lookup"><span data-stu-id="93206-127">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span></span> <span data-ttu-id="93206-128">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span><span class="sxs-lookup"><span data-stu-id="93206-128">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span></span> <span data-ttu-id="93206-129">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span><span class="sxs-lookup"><span data-stu-id="93206-129">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="93206-130">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span><span class="sxs-lookup"><span data-stu-id="93206-130">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="93206-131">This tutorial uses service-managed authentication.</span><span class="sxs-lookup"><span data-stu-id="93206-131">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="93206-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="93206-132">Next steps</span></span>
<span data-ttu-id="93206-133">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="93206-133">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="93206-134">Add push notifications to your app</span><span class="sxs-lookup"><span data-stu-id="93206-134">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="93206-135">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="93206-135">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="93206-136">Enable offline sync for your app</span><span class="sxs-lookup"><span data-stu-id="93206-136">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="93206-137">Learn how to add offline support your app using an Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="93206-137">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="93206-138">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="93206-138">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md

