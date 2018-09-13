---
title: Get Started with authentication for Mobile Apps in Xamarin Android
description: Learn how to use Mobile Apps to authenticate users of your Xamarin Android app through a variety of identity providers, including AAD, Google, Facebook, Twitter, and Microsoft.
services: app-service\mobile
documentationcenter: xamarin
author: conceptdev
manager: panarasi
editor: ''
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 97207b722b65ccf98c57304cd559b0927aacd5a4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803353"
---
# <a name="add-authentication-to-your-xamarinandroid-app"></a><span data-ttu-id="96eb1-103">Add authentication to your Xamarin.Android app</span><span class="sxs-lookup"><span data-stu-id="96eb1-103">Add authentication to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="96eb1-104">This topic shows you how to authenticate users of a Mobile App from your client application.</span><span class="sxs-lookup"><span data-stu-id="96eb1-104">This topic shows you how to authenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="96eb1-105">In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="96eb1-105">In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="96eb1-106">After being successfully authenticated and authorized in the Mobile App, the user ID value is displayed.</span><span class="sxs-lookup"><span data-stu-id="96eb1-106">After being successfully authenticated and authorized in the Mobile App, the user ID value is displayed.</span></span>

<span data-ttu-id="96eb1-107">This tutorial is based on the Mobile App quickstart.</span><span class="sxs-lookup"><span data-stu-id="96eb1-107">This tutorial is based on the Mobile App quickstart.</span></span> <span data-ttu-id="96eb1-108">You must also first complete the tutorial [Create a Xamarin.Android app].</span><span class="sxs-lookup"><span data-stu-id="96eb1-108">You must also first complete the tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="96eb1-109">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span><span class="sxs-lookup"><span data-stu-id="96eb1-109">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="96eb1-110">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="96eb1-110">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register"></a><span data-ttu-id="96eb1-111">Register your app for authentication and configure App Services</span><span class="sxs-lookup"><span data-stu-id="96eb1-111">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a><span data-ttu-id="96eb1-112">Add your app to the Allowed External Redirect URLs</span><span class="sxs-lookup"><span data-stu-id="96eb1-112">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="96eb1-113">Secure authentication requires that you define a new URL scheme for your app.</span><span class="sxs-lookup"><span data-stu-id="96eb1-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="96eb1-114">This allows the authentication system to redirect back to your app once the authentication process is complete.</span><span class="sxs-lookup"><span data-stu-id="96eb1-114">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="96eb1-115">In this tutorial, we use the URL scheme _appname_ throughout.</span><span class="sxs-lookup"><span data-stu-id="96eb1-115">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="96eb1-116">However, you can use any URL scheme you choose.</span><span class="sxs-lookup"><span data-stu-id="96eb1-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="96eb1-117">It should be unique to your mobile application.</span><span class="sxs-lookup"><span data-stu-id="96eb1-117">It should be unique to your mobile application.</span></span> <span data-ttu-id="96eb1-118">To enable the redirection on the server side:</span><span class="sxs-lookup"><span data-stu-id="96eb1-118">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="96eb1-119">In the [Azure portal], select your App Service.</span><span class="sxs-lookup"><span data-stu-id="96eb1-119">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="96eb1-120">Click the **Authentication / Authorization** menu option.</span><span class="sxs-lookup"><span data-stu-id="96eb1-120">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="96eb1-121">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="96eb1-121">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="96eb1-122">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span><span class="sxs-lookup"><span data-stu-id="96eb1-122">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="96eb1-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span><span class="sxs-lookup"><span data-stu-id="96eb1-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="96eb1-124">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span><span class="sxs-lookup"><span data-stu-id="96eb1-124">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="96eb1-125">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="96eb1-125">Click **OK**.</span></span>

5. <span data-ttu-id="96eb1-126">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="96eb1-126">Click **Save**.</span></span>

## <a name="permissions"></a><span data-ttu-id="96eb1-127">Restrict permissions to authenticated users</span><span class="sxs-lookup"><span data-stu-id="96eb1-127">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="96eb1-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span><span class="sxs-lookup"><span data-stu-id="96eb1-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="96eb1-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="96eb1-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="96eb1-130">This happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span><span class="sxs-lookup"><span data-stu-id="96eb1-130">This happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="96eb1-131">The *TodoItem* table now requires authentication.</span><span class="sxs-lookup"><span data-stu-id="96eb1-131">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="96eb1-132">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span><span class="sxs-lookup"><span data-stu-id="96eb1-132">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication"></a><span data-ttu-id="96eb1-133">Add authentication to the app</span><span class="sxs-lookup"><span data-stu-id="96eb1-133">Add authentication to the app</span></span>
<span data-ttu-id="96eb1-134">The app is updated to require users to tap the **Sign in** button and authenticate before data is displayed.</span><span class="sxs-lookup"><span data-stu-id="96eb1-134">The app is updated to require users to tap the **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="96eb1-135">Add the following code to the **TodoActivity** class:</span><span class="sxs-lookup"><span data-stu-id="96eb1-135">Add the following code to the **TodoActivity** class:</span></span>
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
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
   
    <span data-ttu-id="96eb1-136">This creates a new method to authenticate a user and a method handler for a new **Sign in** button.</span><span class="sxs-lookup"><span data-stu-id="96eb1-136">This creates a new method to authenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="96eb1-137">The user in the example code above is authenticated by using a Facebook login.</span><span class="sxs-lookup"><span data-stu-id="96eb1-137">The user in the example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="96eb1-138">A dialog is used to display the user ID once authenticated.</span><span class="sxs-lookup"><span data-stu-id="96eb1-138">A dialog is used to display the user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="96eb1-139">If you are using an identity provider other than Facebook, change the value passed to **LoginAsync** above to one of the following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="96eb1-139">If you are using an identity provider other than Facebook, change the value passed to **LoginAsync** above to one of the following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="96eb1-140">In the **OnCreate** method, delete or comment-out the following line of code:</span><span class="sxs-lookup"><span data-stu-id="96eb1-140">In the **OnCreate** method, delete or comment-out the following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="96eb1-141">In the Activity_To_Do.axml file, add the following *LoginUser* button definition before the existing *AddItem* button:</span><span class="sxs-lookup"><span data-stu-id="96eb1-141">In the Activity_To_Do.axml file, add the following *LoginUser* button definition before the existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="96eb1-142">Add the following element to the Strings.xml resources file:</span><span class="sxs-lookup"><span data-stu-id="96eb1-142">Add the following element to the Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="96eb1-143">Open the AndroidManifest.xml file, add the following code inside `<application>` XML element:</span><span class="sxs-lookup"><span data-stu-id="96eb1-143">Open the AndroidManifest.xml file, add the following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="96eb1-144">In Visual Studio or Xamarin Studio, run the client project on a device or emulator and sign in with your chosen identity provider.</span><span class="sxs-lookup"><span data-stu-id="96eb1-144">In Visual Studio or Xamarin Studio, run the client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="96eb1-145">When you are successfully logged-in, the app will display your login ID and the list of todo items, and you can make updates to the data.</span><span class="sxs-lookup"><span data-stu-id="96eb1-145">When you are successfully logged-in, the app will display your login ID and the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
[Create a Xamarin.Android app]: app-service-mobile-xamarin-android-get-started.md