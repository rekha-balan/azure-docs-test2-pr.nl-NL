---
title: Get Started with authentication for Mobile Apps in Xamarin Forms app | Microsoft Docs
description: Learn how to use Mobile Apps to authenticate users of your Xamarin Forms app through a variety of identity providers, including AAD, Google, Facebook, Twitter, and Microsoft.
services: app-service\mobile
documentationcenter: xamarin
author: adrianhall
manager: adrianha
editor: ''
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: adrianha
ms.openlocfilehash: fb4d41c2b1e8ef053276cd70c7eae76934abfe31
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550475"
---
# <a name="add-authentication-to-your-xamarin-forms-app"></a><span data-ttu-id="57501-103">Add authentication to your Xamarin Forms app</span><span class="sxs-lookup"><span data-stu-id="57501-103">Add authentication to your Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="57501-104">Overview</span><span class="sxs-lookup"><span data-stu-id="57501-104">Overview</span></span>
<span data-ttu-id="57501-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span><span class="sxs-lookup"><span data-stu-id="57501-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="57501-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span><span class="sxs-lookup"><span data-stu-id="57501-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="57501-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span><span class="sxs-lookup"><span data-stu-id="57501-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57501-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="57501-108">Prerequisites</span></span>
<span data-ttu-id="57501-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span><span class="sxs-lookup"><span data-stu-id="57501-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="57501-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span><span class="sxs-lookup"><span data-stu-id="57501-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="57501-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span><span class="sxs-lookup"><span data-stu-id="57501-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="57501-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="57501-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="57501-113">Register your app for authentication and configure App Services</span><span class="sxs-lookup"><span data-stu-id="57501-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="57501-114">Restrict permissions to authenticated users</span><span class="sxs-lookup"><span data-stu-id="57501-114">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-to-the-portable-class-library"></a><span data-ttu-id="57501-115">Add authentication to the portable class library</span><span class="sxs-lookup"><span data-stu-id="57501-115">Add authentication to the portable class library</span></span>
<span data-ttu-id="57501-116">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span><span class="sxs-lookup"><span data-stu-id="57501-116">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span></span> <span data-ttu-id="57501-117">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span><span class="sxs-lookup"><span data-stu-id="57501-117">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span></span> <span data-ttu-id="57501-118">For more information, see [Server-managed authentication][5].</span><span class="sxs-lookup"><span data-stu-id="57501-118">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="57501-119">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span><span class="sxs-lookup"><span data-stu-id="57501-119">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="57501-120">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span><span class="sxs-lookup"><span data-stu-id="57501-120">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span></span> <span data-ttu-id="57501-121">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span><span class="sxs-lookup"><span data-stu-id="57501-121">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span></span> <span data-ttu-id="57501-122">Data is loaded from the mobile app backend after successful authentication.</span><span class="sxs-lookup"><span data-stu-id="57501-122">Data is loaded from the mobile app backend after successful authentication.</span></span>

<span data-ttu-id="57501-123">Implement the **IAuthenticate** interface for each platform supported by your app.</span><span class="sxs-lookup"><span data-stu-id="57501-123">Implement the **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="57501-124">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span><span class="sxs-lookup"><span data-stu-id="57501-124">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span></span>
   
        using System.Threading.Tasks;
2. <span data-ttu-id="57501-125">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span><span class="sxs-lookup"><span data-stu-id="57501-125">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span></span>
   
        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="57501-126">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span><span class="sxs-lookup"><span data-stu-id="57501-126">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span></span>
   
        public static IAuthenticate Authenticator { get; private set; }
   
        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="57501-127">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span><span class="sxs-lookup"><span data-stu-id="57501-127">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span></span>
   
          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>
   
    <span data-ttu-id="57501-128">This button triggers server-managed authentication with your mobile app backend.</span><span class="sxs-lookup"><span data-stu-id="57501-128">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="57501-129">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span><span class="sxs-lookup"><span data-stu-id="57501-129">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span></span>
   
        // Track whether the user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="57501-130">Replace the **OnAppearing** method with the following code:</span><span class="sxs-lookup"><span data-stu-id="57501-130">Replace the **OnAppearing** method with the following code:</span></span>
   
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
   
    <span data-ttu-id="57501-131">This code makes sure that data is only refreshed from the service after you have been authenticated.</span><span class="sxs-lookup"><span data-stu-id="57501-131">This code makes sure that data is only refreshed from the service after you have been authenticated.</span></span>
7. <span data-ttu-id="57501-132">Add the following handler for the **Clicked** event to the **TodoList** class:</span><span class="sxs-lookup"><span data-stu-id="57501-132">Add the following handler for the **Clicked** event to the **TodoList** class:</span></span>
   
        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();
   
            // Set syncItems to true to synchronize the data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="57501-133">Save your changes and rebuild the Portable Class Library project verifying no errors.</span><span class="sxs-lookup"><span data-stu-id="57501-133">Save your changes and rebuild the Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-to-the-android-app"></a><span data-ttu-id="57501-134">Add authentication to the Android app</span><span class="sxs-lookup"><span data-stu-id="57501-134">Add authentication to the Android app</span></span>
<span data-ttu-id="57501-135">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span><span class="sxs-lookup"><span data-stu-id="57501-135">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span></span> <span data-ttu-id="57501-136">Skip this section if you are not supporting Android devices.</span><span class="sxs-lookup"><span data-stu-id="57501-136">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="57501-137">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span><span class="sxs-lookup"><span data-stu-id="57501-137">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="57501-138">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="57501-138">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="57501-139">The 401 code is produced because access on the backend is restricted to authorized users only.</span><span class="sxs-lookup"><span data-stu-id="57501-139">The 401 code is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="57501-140">Open MainActivity.cs in the Android project and add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="57501-140">Open MainActivity.cs in the Android project and add the following `using` statements:</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="57501-141">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="57501-141">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span></span>
   
        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="57501-142">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="57501-142">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>
   
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
                    MobileServiceAuthenticationProvider.Facebook);
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

    <span data-ttu-id="57501-143">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="57501-143">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

1. <span data-ttu-id="57501-144">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="57501-144">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span></span>
   
        // Initialize the authenticator before loading the app.
        App.Init((IAuthenticate)this);
   
    <span data-ttu-id="57501-145">This code ensures the authenticator is initialized before the app loads.</span><span class="sxs-lookup"><span data-stu-id="57501-145">This code ensures the authenticator is initialized before the app loads.</span></span>
2. <span data-ttu-id="57501-146">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span><span class="sxs-lookup"><span data-stu-id="57501-146">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-the-ios-app"></a><span data-ttu-id="57501-147">Add authentication to the iOS app</span><span class="sxs-lookup"><span data-stu-id="57501-147">Add authentication to the iOS app</span></span>
<span data-ttu-id="57501-148">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span><span class="sxs-lookup"><span data-stu-id="57501-148">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span></span> <span data-ttu-id="57501-149">Skip this section if you are not supporting iOS devices.</span><span class="sxs-lookup"><span data-stu-id="57501-149">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="57501-150">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span><span class="sxs-lookup"><span data-stu-id="57501-150">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="57501-151">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="57501-151">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="57501-152">The 401 response is produced because access on the backend is restricted to authorized users only.</span><span class="sxs-lookup"><span data-stu-id="57501-152">The 401 response is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="57501-153">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="57501-153">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="57501-154">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="57501-154">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span></span>
   
        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="57501-155">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="57501-155">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>
   
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
                        MobileServiceAuthenticationProvider.Facebook);
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
   
    <span data-ttu-id="57501-156">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="57501-156">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>
6. <span data-ttu-id="57501-157">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="57501-157">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span></span>
   
        App.Init(this);
   
    <span data-ttu-id="57501-158">This code ensures the authenticator is initialized before the app is loaded.</span><span class="sxs-lookup"><span data-stu-id="57501-158">This code ensures the authenticator is initialized before the app is loaded.</span></span>
7. <span data-ttu-id="57501-159">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span><span class="sxs-lookup"><span data-stu-id="57501-159">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-windows-81-including-phone-app-projects"></a><span data-ttu-id="57501-160">Add authentication to Windows 8.1 (including Phone) app projects</span><span class="sxs-lookup"><span data-stu-id="57501-160">Add authentication to Windows 8.1 (including Phone) app projects</span></span>
<span data-ttu-id="57501-161">This section shows how to implement the **IAuthenticate** interface in the Windows 8.1 and Windows Phone 8.1 app projects.</span><span class="sxs-lookup"><span data-stu-id="57501-161">This section shows how to implement the **IAuthenticate** interface in the Windows 8.1 and Windows Phone 8.1 app projects.</span></span> <span data-ttu-id="57501-162">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span><span class="sxs-lookup"><span data-stu-id="57501-162">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span></span> <span data-ttu-id="57501-163">Skip this section if you are not supporting Windows devices.</span><span class="sxs-lookup"><span data-stu-id="57501-163">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="57501-164">In Visual Studio, right-click either the **WinApp** or the **WinPhone81** project, then **Set as StartUp Project**.</span><span class="sxs-lookup"><span data-stu-id="57501-164">In Visual Studio, right-click either the **WinApp** or the **WinPhone81** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="57501-165">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span><span class="sxs-lookup"><span data-stu-id="57501-165">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="57501-166">The 401 response happens because access on the backend is restricted to authorized users only.</span><span class="sxs-lookup"><span data-stu-id="57501-166">The 401 response happens because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="57501-167">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="57501-167">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;
   
    <span data-ttu-id="57501-168">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span><span class="sxs-lookup"><span data-stu-id="57501-168">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
4. <span data-ttu-id="57501-169">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="57501-169">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span></span>
   
        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="57501-170">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span><span class="sxs-lookup"><span data-stu-id="57501-170">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>
   
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
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
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

    <span data-ttu-id="57501-171">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="57501-171">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="57501-172">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="57501-172">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span></span>
   
        // Initialize the authenticator before loading the app.
        <your_Portable_Class_Library_namespace>.App.Init(this);
   
    <span data-ttu-id="57501-173">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span><span class="sxs-lookup"><span data-stu-id="57501-173">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
   
    <span data-ttu-id="57501-174">If you are modifying the WinApp project, skip to step 8.</span><span class="sxs-lookup"><span data-stu-id="57501-174">If you are modifying the WinApp project, skip to step 8.</span></span> <span data-ttu-id="57501-175">The next step applies only to the WinPhone81 project, where you need to complete the login callback.</span><span class="sxs-lookup"><span data-stu-id="57501-175">The next step applies only to the WinPhone81 project, where you need to complete the login callback.</span></span>
2. <span data-ttu-id="57501-176">(Optional) In the **WinPhone81** app project, open App.xaml.cs and add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="57501-176">(Optional) In the **WinPhone81** app project, open App.xaml.cs and add the following `using` statements:</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using <your_Portable_Class_Library_namespace>;
   
    <span data-ttu-id="57501-177">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span><span class="sxs-lookup"><span data-stu-id="57501-177">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
3. <span data-ttu-id="57501-178">If you are using **WinPhone81** or **WinApp**, add the following **OnActivated** method override to the **App** class:</span><span class="sxs-lookup"><span data-stu-id="57501-178">If you are using **WinPhone81** or **WinApp**, add the following **OnActivated** method override to the **App** class:</span></span>
   
       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);
   
           // We just need to handle activation that occurs after web authentication.
           if (args.Kind == ActivationKind.WebAuthenticationBrokerContinuation)
           {
               // Get the client and call the LoginComplete method to complete authentication.
               var client = TodoItemManager.DefaultManager.CurrentClient as MobileServiceClient;
               client.LoginComplete(args as WebAuthenticationBrokerContinuationEventArgs);
           }
       }
   
   <span data-ttu-id="57501-179">When the method override already exists, add the conditional code from the preceding snippet.</span><span class="sxs-lookup"><span data-stu-id="57501-179">When the method override already exists, add the conditional code from the preceding snippet.</span></span>  <span data-ttu-id="57501-180">This code is not required for Universal Windows projects.</span><span class="sxs-lookup"><span data-stu-id="57501-180">This code is not required for Universal Windows projects.</span></span>
4. <span data-ttu-id="57501-181">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span><span class="sxs-lookup"><span data-stu-id="57501-181">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57501-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="57501-182">Next steps</span></span>
<span data-ttu-id="57501-183">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="57501-183">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="57501-184">Add push notifications to your app</span><span class="sxs-lookup"><span data-stu-id="57501-184">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)
  
  <span data-ttu-id="57501-185">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="57501-185">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="57501-186">Enable offline sync for your app</span><span class="sxs-lookup"><span data-stu-id="57501-186">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)
  
  <span data-ttu-id="57501-187">Learn how to add offline support your app using a Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="57501-187">Learn how to add offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="57501-188">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span><span class="sxs-lookup"><span data-stu-id="57501-188">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
