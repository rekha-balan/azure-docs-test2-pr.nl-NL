---
title: Get Started with authentication for Mobile Apps in Xamarin Android
description: Learn how to use Mobile Apps to authenticate users of your Xamarin Android app through a variety of identity providers, including AAD, Google, Facebook, Twitter, and Microsoft.
services: app-service\mobile
documentationcenter: xamarin
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: 75ea2b1fe0a5232e774d5063eb49875cc7399bf2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671583"
---
# <a name="add-authentication-to-your-xamarinandroid-app"></a><span data-ttu-id="7f128-103">Add authentication to your Xamarin.Android app</span><span class="sxs-lookup"><span data-stu-id="7f128-103">Add authentication to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="7f128-104">This topic shows you how to authenticate users of a Mobile App from your client application.</span><span class="sxs-lookup"><span data-stu-id="7f128-104">This topic shows you how to authenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="7f128-105">In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="7f128-105">In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="7f128-106">After being successfully authenticated and authorized in the Mobile App, the user ID value is displayed.</span><span class="sxs-lookup"><span data-stu-id="7f128-106">After being successfully authenticated and authorized in the Mobile App, the user ID value is displayed.</span></span>

<span data-ttu-id="7f128-107">This tutorial is based on the Mobile App quickstart.</span><span class="sxs-lookup"><span data-stu-id="7f128-107">This tutorial is based on the Mobile App quickstart.</span></span> <span data-ttu-id="7f128-108">You must also first complete the tutorial [Create a Xamarin.Android app].</span><span class="sxs-lookup"><span data-stu-id="7f128-108">You must also first complete the tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="7f128-109">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span><span class="sxs-lookup"><span data-stu-id="7f128-109">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="7f128-110">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7f128-110">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register"></a><span data-ttu-id="7f128-111">Register your app for authentication and configure App Services</span><span class="sxs-lookup"><span data-stu-id="7f128-111">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="permissions"></a><span data-ttu-id="7f128-112">Restrict permissions to authenticated users</span><span class="sxs-lookup"><span data-stu-id="7f128-112">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="7f128-113">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span><span class="sxs-lookup"><span data-stu-id="7f128-113">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="7f128-114">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="7f128-114">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="7f128-115">This happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span><span class="sxs-lookup"><span data-stu-id="7f128-115">This happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="7f128-116">The *TodoItem* table now requires authentication.</span><span class="sxs-lookup"><span data-stu-id="7f128-116">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="7f128-117">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span><span class="sxs-lookup"><span data-stu-id="7f128-117">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication"></a><span data-ttu-id="7f128-118">Add authentication to the app</span><span class="sxs-lookup"><span data-stu-id="7f128-118">Add authentication to the app</span></span>
<span data-ttu-id="7f128-119">The app is updated to require users to tap the **Sign in** button and authenticate before data is displayed.</span><span class="sxs-lookup"><span data-stu-id="7f128-119">The app is updated to require users to tap the **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="7f128-120">Add the following code to the **TodoActivity** class:</span><span class="sxs-lookup"><span data-stu-id="7f128-120">Add the following code to the **TodoActivity** class:</span></span>
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook);
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide the button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load the data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="7f128-121">This creates a new method to authenticate a user and a method handler for a new **Sign in** button.</span><span class="sxs-lookup"><span data-stu-id="7f128-121">This creates a new method to authenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="7f128-122">The user in the example code above is authenticated by using a Facebook login.</span><span class="sxs-lookup"><span data-stu-id="7f128-122">The user in the example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="7f128-123">A dialog is used to display the user ID once authenticated.</span><span class="sxs-lookup"><span data-stu-id="7f128-123">A dialog is used to display the user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7f128-124">If you are using an identity provider other than Facebook, change the value passed to **LoginAsync** above to one of the following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="7f128-124">If you are using an identity provider other than Facebook, change the value passed to **LoginAsync** above to one of the following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="7f128-125">In the **OnCreate** method, delete or comment-out the following line of code:</span><span class="sxs-lookup"><span data-stu-id="7f128-125">In the **OnCreate** method, delete or comment-out the following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="7f128-126">In the Activity_To_Do.axml file, add the following *LoginUser* button definition before the existing *AddItem* button:</span><span class="sxs-lookup"><span data-stu-id="7f128-126">In the Activity_To_Do.axml file, add the following *LoginUser* button definition before the existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="7f128-127">Add the following element to the Strings.xml resources file:</span><span class="sxs-lookup"><span data-stu-id="7f128-127">Add the following element to the Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="7f128-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator and sign in with your chosen identity provider.</span><span class="sxs-lookup"><span data-stu-id="7f128-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator and sign in with your chosen identity provider.</span></span>
   
       When you are successfully logged-in, the app will display your login ID and the list of todo items, and you can make updates to the data.

<!-- URLs. -->
[Create a Xamarin.Android app]: app-service-mobile-xamarin-android-get-started.md
