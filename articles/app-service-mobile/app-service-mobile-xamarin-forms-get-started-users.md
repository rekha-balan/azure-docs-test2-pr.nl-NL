---
title: Get Started with authentication for Mobile Apps in Xamarin Forms app | Microsoft Docs
description: Learn how to use Mobile Apps to authenticate users of your Xamarin Forms app through a variety of identity providers, including AAD, Google, Facebook, Twitter, and Microsoft.
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: crdun
editor: ''
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: e3e8c843437558c6d5d3a3c39bed1e647f852b18
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793733"
---
# <a name="add-authentication-to-your-xamarin-forms-app"></a><span data-ttu-id="8d185-103">Add authentication to your Xamarin Forms app</span><span class="sxs-lookup"><span data-stu-id="8d185-103">Add authentication to your Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="8d185-104">Overview</span><span class="sxs-lookup"><span data-stu-id="8d185-104">Overview</span></span>
<span data-ttu-id="8d185-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span><span class="sxs-lookup"><span data-stu-id="8d185-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="8d185-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span><span class="sxs-lookup"><span data-stu-id="8d185-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="8d185-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span><span class="sxs-lookup"><span data-stu-id="8d185-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d185-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8d185-108">Prerequisites</span></span>
<span data-ttu-id="8d185-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span><span class="sxs-lookup"><span data-stu-id="8d185-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="8d185-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span><span class="sxs-lookup"><span data-stu-id="8d185-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="8d185-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span><span class="sxs-lookup"><span data-stu-id="8d185-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="8d185-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="8d185-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="8d185-113">Register your app for authentication and configure App Services</span><span class="sxs-lookup"><span data-stu-id="8d185-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a><span data-ttu-id="8d185-114">Add your app to the Allowed External Redirect URLs</span><span class="sxs-lookup"><span data-stu-id="8d185-114">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="8d185-115">Secure authentication requires that you define a new URL scheme for your app.</span><span class="sxs-lookup"><span data-stu-id="8d185-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="8d185-116">This allows the authentication system to redirect back to your app once the authentication process is complete.</span><span class="sxs-lookup"><span data-stu-id="8d185-116">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="8d185-117">In this tutorial, we use the URL scheme _appname_ throughout.</span><span class="sxs-lookup"><span data-stu-id="8d185-117">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="8d185-118">However, you can use any URL scheme you choose.</span><span class="sxs-lookup"><span data-stu-id="8d185-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="8d185-119">It should be unique to your mobile application.</span><span class="sxs-lookup"><span data-stu-id="8d185-119">It should be unique to your mobile application.</span></span> <span data-ttu-id="8d185-120">To enable the redirection on the server side:</span><span class="sxs-lookup"><span data-stu-id="8d185-120">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="8d185-121">In the [Azure portal][8], select your App Service.</span><span class="sxs-lookup"><span data-stu-id="8d185-121">In the [Azure portal][8], select your App Service.</span></span>

2. <span data-ttu-id="8d185-122">Click the **Authentication / Authorization** menu option.</span><span class="sxs-lookup"><span data-stu-id="8d185-122">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="8d185-123">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="8d185-123">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="8d185-124">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span><span class="sxs-lookup"><span data-stu-id="8d185-124">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="8d185-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span><span class="sxs-lookup"><span data-stu-id="8d185-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="8d185-126">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span><span class="sxs-lookup"><span data-stu-id="8d185-126">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="8d185-127">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d185-127">Click **OK**.</span></span>

5. <span data-ttu-id="8d185-128">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8d185-128">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="8d185-129">Restrict permissions to authenticated users</span><span class="sxs-lookup"><span data-stu-id="8d185-129">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-to-the-portable-class-library"></a><span data-ttu-id="8d185-130">Add authentication to the portable class library</span><span class="sxs-lookup"><span data-stu-id="8d185-130">Add authentication to the portable class library</span></span>
<span data-ttu-id="8d185-131">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span><span class="sxs-lookup"><span data-stu-id="8d185-131">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span></span> <span data-ttu-id="8d185-132">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span><span class="sxs-lookup"><span data-stu-id="8d185-132">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span></span> <span data-ttu-id="8d185-133">For more information, see [Server-managed authentication][5].</span><span class="sxs-lookup"><span data-stu-id="8d185-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="8d185-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span><span class="sxs-lookup"><span data-stu-id="8d185-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="8d185-135">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span><span class="sxs-lookup"><span data-stu-id="8d185-135">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span></span> <span data-ttu-id="8d185-136">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span><span class="sxs-lookup"><span data-stu-id="8d185-136">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span></span> <span data-ttu-id="8d185-137">Data is loaded from the mobile app backend after successful authentication.</span><span class="sxs-lookup"><span data-stu-id="8d185-137">Data is loaded from the mobile app backend after successful authentication.</span></span>

<span data-ttu-id="8d185-138">Implement the **IAuthenticate** interface for each platform supported by your app.</span><span class="sxs-lookup"><span data-stu-id="8d185-138">Implement the **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="8d185-139">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span><span class="sxs-lookup"><span data-stu-id="8d185-139">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="8d185-140">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span><span class="sxs-lookup"><span data-stu-id="8d185-140">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="8d185-141">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="8d185-141">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="8d185-142">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span><span class="sxs-lookup"><span data-stu-id="8d185-142">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="8d185-143">This button triggers server-managed authentication with your mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="8d185-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="8d185-144">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span><span class="sxs-lookup"><span data-stu-id="8d185-144">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span></span>

        // Track whether the user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="8d185-145">Replace the **OnAppearing** method with the following code:</span><span class="sxs-lookup"><span data-stu-id="8d185-145">Replace the **OnAppearing** method with the following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems to true in order to synchronize the data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide the Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="8d185-146">This code makes sure that data is only refreshed from the service after you have been authenticated.</span><span class="sxs-lookup"><span data-stu-id="8d185-146">This code makes sure that data is only refreshed from the service after you have been authenticated.</span></span>
7. <span data-ttu-id="8d185-147">Add the following handler for the **Clicked** event to the **TodoList** class:</span><span class="sxs-lookup"><span data-stu-id="8d185-147">Add the following handler for the **Clicked** event to the **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems to true to synchronize the data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="8d185-148">Save your changes and rebuild the Portable Class Library project verifying no errors.</span><span class="sxs-lookup"><span data-stu-id="8d185-148">Save your changes and rebuild the Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-to-the-android-app"></a><span data-ttu-id="8d185-149">Add authentication to the Android app</span><span class="sxs-lookup"><span data-stu-id="8d185-149">Add authentication to the Android app</span></span>
<span data-ttu-id="8d185-150">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span><span class="sxs-lookup"><span data-stu-id="8d185-150">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span></span> <span data-ttu-id="8d185-151">Skip this section if you are not supporting Android devices.</span><span class="sxs-lookup"><span data-stu-id="8d185-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="8d185-152">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span><span class="sxs-lookup"><span data-stu-id="8d185-152">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="8d185-153">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="8d185-153">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="8d185-154">The 401 code is produced because access on the backend is restricted to authorized users only.</span><span class="sxs-lookup"><span data-stu-id="8d185-154">The 401 code is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="8d185-155">Open MainActivity.cs in the Android project and add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="8d185-155">Open MainActivity.cs in the Android project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="8d185-156">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="8d185-156">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="8d185-157">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="8d185-157">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display the success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="8d185-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="8d185-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="8d185-159">Update the **AndroidManifest.xml** file by adding the following XML inside the `<application>` element:</span><span class="sxs-lookup"><span data-stu-id="8d185-159">Update the **AndroidManifest.xml** file by adding the following XML inside the `<application>` element:</span></span>

    ```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
    ```
    <span data-ttu-id="8d185-160">Replace `{url_scheme_of_your_app}` with your URL scheme.</span><span class="sxs-lookup"><span data-stu-id="8d185-160">Replace `{url_scheme_of_your_app}` with your URL scheme.</span></span>
7. <span data-ttu-id="8d185-161">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="8d185-161">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="8d185-162">This code ensures the authenticator is initialized before the app loads.</span><span class="sxs-lookup"><span data-stu-id="8d185-162">This code ensures the authenticator is initialized before the app loads.</span></span>
8. <span data-ttu-id="8d185-163">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span><span class="sxs-lookup"><span data-stu-id="8d185-163">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-the-ios-app"></a><span data-ttu-id="8d185-164">Add authentication to the iOS app</span><span class="sxs-lookup"><span data-stu-id="8d185-164">Add authentication to the iOS app</span></span>
<span data-ttu-id="8d185-165">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span><span class="sxs-lookup"><span data-stu-id="8d185-165">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span></span> <span data-ttu-id="8d185-166">Skip this section if you are not supporting iOS devices.</span><span class="sxs-lookup"><span data-stu-id="8d185-166">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="8d185-167">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span><span class="sxs-lookup"><span data-stu-id="8d185-167">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="8d185-168">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="8d185-168">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="8d185-169">The 401 response is produced because access on the backend is restricted to authorized users only.</span><span class="sxs-lookup"><span data-stu-id="8d185-169">The 401 response is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="8d185-170">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="8d185-170">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="8d185-171">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="8d185-171">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="8d185-172">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="8d185-172">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display the success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="8d185-173">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="8d185-173">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>
    
6. <span data-ttu-id="8d185-174">Update the **AppDelegate** class by adding the **OpenUrl** method overload, as follows:</span><span class="sxs-lookup"><span data-stu-id="8d185-174">Update the **AppDelegate** class by adding the **OpenUrl** method overload, as follows:</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }
   
7. <span data-ttu-id="8d185-175">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="8d185-175">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="8d185-176">This code ensures the authenticator is initialized before the app is loaded.</span><span class="sxs-lookup"><span data-stu-id="8d185-176">This code ensures the authenticator is initialized before the app is loaded.</span></span>

8. <span data-ttu-id="8d185-177">Open Info.plist and add a **URL Type**.</span><span class="sxs-lookup"><span data-stu-id="8d185-177">Open Info.plist and add a **URL Type**.</span></span> <span data-ttu-id="8d185-178">Set the **Identifier** to a name of your choosing, the **URL Schemes** to the URL scheme for your app, and the **Role** to None.</span><span class="sxs-lookup"><span data-stu-id="8d185-178">Set the **Identifier** to a name of your choosing, the **URL Schemes** to the URL scheme for your app, and the **Role** to None.</span></span>

9. <span data-ttu-id="8d185-179">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span><span class="sxs-lookup"><span data-stu-id="8d185-179">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-windows-10-including-phone-app-projects"></a><span data-ttu-id="8d185-180">Add authentication to Windows 10 (including Phone) app projects</span><span class="sxs-lookup"><span data-stu-id="8d185-180">Add authentication to Windows 10 (including Phone) app projects</span></span>
<span data-ttu-id="8d185-181">This section shows how to implement the **IAuthenticate** interface in the Windows 10 app projects.</span><span class="sxs-lookup"><span data-stu-id="8d185-181">This section shows how to implement the **IAuthenticate** interface in the Windows 10 app projects.</span></span> <span data-ttu-id="8d185-182">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span><span class="sxs-lookup"><span data-stu-id="8d185-182">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span></span> <span data-ttu-id="8d185-183">Skip this section if you are not supporting Windows devices.</span><span class="sxs-lookup"><span data-stu-id="8d185-183">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="8d185-184">In Visual Studio, right-click the **UWP** project, then **Set as StartUp Project**.</span><span class="sxs-lookup"><span data-stu-id="8d185-184">In Visual Studio, right-click the **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="8d185-185">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="8d185-185">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="8d185-186">The 401 response happens because access on the backend is restricted to authorized users only.</span><span class="sxs-lookup"><span data-stu-id="8d185-186">The 401 response happens because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="8d185-187">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="8d185-187">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="8d185-188">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span><span class="sxs-lookup"><span data-stu-id="8d185-188">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
4. <span data-ttu-id="8d185-189">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="8d185-189">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="8d185-190">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="8d185-190">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display the success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="8d185-191">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="8d185-191">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

1. <span data-ttu-id="8d185-192">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="8d185-192">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="8d185-193">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span><span class="sxs-lookup"><span data-stu-id="8d185-193">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>

3. <span data-ttu-id="8d185-194">If you are using **UWP**, add the following **OnActivated** method override to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="8d185-194">If you are using **UWP**, add the following **OnActivated** method override to the **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }
       }

3. <span data-ttu-id="8d185-195">Open Package.appxmanifest and add a **Protocol** declaration.</span><span class="sxs-lookup"><span data-stu-id="8d185-195">Open Package.appxmanifest and add a **Protocol** declaration.</span></span> <span data-ttu-id="8d185-196">Set the **Display name** to a name of your choosing, and the **Name** to the URL scheme for you app.</span><span class="sxs-lookup"><span data-stu-id="8d185-196">Set the **Display name** to a name of your choosing, and the **Name** to the URL scheme for you app.</span></span>

4. <span data-ttu-id="8d185-197">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span><span class="sxs-lookup"><span data-stu-id="8d185-197">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d185-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="8d185-198">Next steps</span></span>
<span data-ttu-id="8d185-199">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="8d185-199">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="8d185-200">Add push notifications to your app</span><span class="sxs-lookup"><span data-stu-id="8d185-200">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="8d185-201">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="8d185-201">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="8d185-202">Enable offline sync for your app</span><span class="sxs-lookup"><span data-stu-id="8d185-202">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="8d185-203">Learn how to add offline support your app using a Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="8d185-203">Learn how to add offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="8d185-204">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="8d185-204">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
[8]: https://portal.azure.com
