---
title: Get Started with authentication for Mobile Apps in Xamarin iOS
description: Learn how to use Mobile Apps to authenticate users of your Xamarin iOS app through a variety of identity providers, including AAD, Google, Facebook, Twitter, and Microsoft.
services: app-service\mobile
documentationcenter: xamarin
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: 0c42255158f7773a66933b910763ad3bc08f1636
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553106"
---
# <a name="add-authentication-to-your-xamarinios-app"></a><span data-ttu-id="7f530-103">Add authentication to your Xamarin.iOS app</span><span class="sxs-lookup"><span data-stu-id="7f530-103">Add authentication to your Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="7f530-104">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span><span class="sxs-lookup"><span data-stu-id="7f530-104">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="7f530-105">In this tutorial, you add authentication to the Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span><span class="sxs-lookup"><span data-stu-id="7f530-105">In this tutorial, you add authentication to the Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="7f530-106">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed and you will be able to access restricted table data.</span><span class="sxs-lookup"><span data-stu-id="7f530-106">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed and you will be able to access restricted table data.</span></span>

<span data-ttu-id="7f530-107">You must first complete the tutorial [Create a Xamarin.iOS app].</span><span class="sxs-lookup"><span data-stu-id="7f530-107">You must first complete the tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="7f530-108">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span><span class="sxs-lookup"><span data-stu-id="7f530-108">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="7f530-109">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7f530-109">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="7f530-110">Register your app for authentication and configure App Services</span><span class="sxs-lookup"><span data-stu-id="7f530-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="7f530-111">Restrict permissions to authenticated users</span><span class="sxs-lookup"><span data-stu-id="7f530-111">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="7f530-112">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="7f530-112">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="7f530-113">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span><span class="sxs-lookup"><span data-stu-id="7f530-113">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="7f530-114">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="7f530-114">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="7f530-115">The failure is logged to the console of the debugger.</span><span class="sxs-lookup"><span data-stu-id="7f530-115">The failure is logged to the console of the debugger.</span></span> <span data-ttu-id="7f530-116">So in Visual Studio, you should see the failure in the output window.</span><span class="sxs-lookup"><span data-stu-id="7f530-116">So in Visual Studio, you should see the failure in the output window.</span></span>

<span data-ttu-id="7f530-117">&nbsp;&nbsp;This unauthorized failure happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span><span class="sxs-lookup"><span data-stu-id="7f530-117">&nbsp;&nbsp;This unauthorized failure happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="7f530-118">The *TodoItem* table now requires authentication.</span><span class="sxs-lookup"><span data-stu-id="7f530-118">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="7f530-119">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span><span class="sxs-lookup"><span data-stu-id="7f530-119">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="7f530-120">Add authentication to the app</span><span class="sxs-lookup"><span data-stu-id="7f530-120">Add authentication to the app</span></span>
<span data-ttu-id="7f530-121">In this section, you will modify the app to display a login screen before displaying data.</span><span class="sxs-lookup"><span data-stu-id="7f530-121">In this section, you will modify the app to display a login screen before displaying data.</span></span> <span data-ttu-id="7f530-122">When the app starts, it will not not connect to your App Service and will not display any data.</span><span class="sxs-lookup"><span data-stu-id="7f530-122">When the app starts, it will not not connect to your App Service and will not display any data.</span></span> <span data-ttu-id="7f530-123">After the first time that the user performs the refresh gesture, the login screen will appear; after successful login the list of todo items will be displayed.</span><span class="sxs-lookup"><span data-stu-id="7f530-123">After the first time that the user performs the refresh gesture, the login screen will appear; after successful login the list of todo items will be displayed.</span></span>

1. <span data-ttu-id="7f530-124">In the client project, open the file **QSTodoService.cs** and add the following using statement and `MobileServiceUser` with accessor to the QSTodoService class:</span><span class="sxs-lookup"><span data-stu-id="7f530-124">In the client project, open the file **QSTodoService.cs** and add the following using statement and `MobileServiceUser` with accessor to the QSTodoService class:</span></span>
   
    ```
        using UIKit;
    ```
   
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="7f530-125">Add new method named **Authenticate** to **QSTodoService** with the following definition:</span><span class="sxs-lookup"><span data-stu-id="7f530-125">Add new method named **Authenticate** to **QSTodoService** with the following definition:</span></span>

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] <span data-ttu-id="7f530-126">If you are using an identity provider other than a Facebook, change the value passed to **LoginAsync** above to one of the following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="7f530-126">If you are using an identity provider other than a Facebook, change the value passed to **LoginAsync** above to one of the following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

1. <span data-ttu-id="7f530-127">Open **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="7f530-127">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="7f530-128">Modify the method definition of **ViewDidLoad** removing the call to **RefreshAsync()** near the end:</span><span class="sxs-lookup"><span data-stu-id="7f530-128">Modify the method definition of **ViewDidLoad** removing the call to **RefreshAsync()** near the end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
           await todoService.InitializeStoreAsync ();
   
           RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync ();
           }
   
            // Comment out the call to RefreshAsync
            // await RefreshAsync ();
        }
2. <span data-ttu-id="7f530-129">Modify the method **RefreshAsync** to authenticate if the **User** property is null.</span><span class="sxs-lookup"><span data-stu-id="7f530-129">Modify the method **RefreshAsync** to authenticate if the **User** property is null.</span></span> <span data-ttu-id="7f530-130">Add the following code at the top of the method definition:</span><span class="sxs-lookup"><span data-stu-id="7f530-130">Add the following code at the top of the method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate (this);
            if (todoService.User == null) {
                Console.WriteLine ("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
3. <span data-ttu-id="7f530-131">In Visual Studio or Xamarin Studio connected to your Xamarin Build Host on your Mac, run the client project targeting a device or emulator.</span><span class="sxs-lookup"><span data-stu-id="7f530-131">In Visual Studio or Xamarin Studio connected to your Xamarin Build Host on your Mac, run the client project targeting a device or emulator.</span></span> <span data-ttu-id="7f530-132">Verify that the app displays no data.</span><span class="sxs-lookup"><span data-stu-id="7f530-132">Verify that the app displays no data.</span></span>
   
    <span data-ttu-id="7f530-133">Perform the refresh gesture by pulling down the list of items, which will cause the login screen to appear.</span><span class="sxs-lookup"><span data-stu-id="7f530-133">Perform the refresh gesture by pulling down the list of items, which will cause the login screen to appear.</span></span> <span data-ttu-id="7f530-134">Once you have successfully entered valid credentials, the app will display the list of todo items, and you can make updates to the data.</span><span class="sxs-lookup"><span data-stu-id="7f530-134">Once you have successfully entered valid credentials, the app will display the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Create a Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started.md
