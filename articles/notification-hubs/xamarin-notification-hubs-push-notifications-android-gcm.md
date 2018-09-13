---
title: Get started with Notification Hubs for Xamarin.Android apps | Microsoft Docs
description: In this tutorial, you learn how to use Azure Notification Hubs to send push notifications to a Xamarin Android application.
author: ysxu
manager: erikre
editor: ''
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 69a177b91e02fddb1c3f01f0d0255932b6ea77d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551900"
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="e9cf3-103">Get started with Notification Hubs with Xamarin for Android</span><span class="sxs-lookup"><span data-stu-id="e9cf3-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="e9cf3-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e9cf3-104">Overview</span></span>
<span data-ttu-id="e9cf3-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Xamarin.Android application.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Xamarin.Android application.</span></span>
<span data-ttu-id="e9cf3-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="e9cf3-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="e9cf3-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="e9cf3-108">The finished code is available in the [NotificationHubs app][GitHub] sample.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-108">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="e9cf3-109">This tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-109">This tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e9cf3-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="e9cf3-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="e9cf3-111">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="e9cf3-111">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9cf3-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e9cf3-112">Prerequisites</span></span>
<span data-ttu-id="e9cf3-113">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-113">This tutorial requires the following:</span></span>

* <span data-ttu-id="e9cf3-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9cf3-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="e9cf3-115">Active Google account</span><span class="sxs-lookup"><span data-stu-id="e9cf3-115">Active Google account</span></span>
* <span data-ttu-id="e9cf3-116">[Azure Messaging Component]</span><span class="sxs-lookup"><span data-stu-id="e9cf3-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="e9cf3-117">[Google Cloud Messaging Client Component]</span><span class="sxs-lookup"><span data-stu-id="e9cf3-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="e9cf3-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9cf3-119">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-119">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e9cf3-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e9cf3-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="e9cf3-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="e9cf3-122">Enable Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="e9cf3-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="e9cf3-123">Configure your notification hub</span><span class="sxs-lookup"><span data-stu-id="e9cf3-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="e9cf3-124">Click the <b>Configure</b> tab at the top, enter the <b>API Key</b> value you obtained in the previous section, and then click <b>Save</b>.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-124">Click the <b>Configure</b> tab at the top, enter the <b>API Key</b> value you obtained in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="e9cf3-125">&emsp;&emsp;![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="e9cf3-125">&emsp;&emsp;![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="e9cf3-126">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive notifications and to send push notifications.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-126">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive notifications and to send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="e9cf3-127">Connect your app to the notification hub</span><span class="sxs-lookup"><span data-stu-id="e9cf3-127">Connect your app to the notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="e9cf3-128">Create a new project</span><span class="sxs-lookup"><span data-stu-id="e9cf3-128">Create a new project</span></span>
1. <span data-ttu-id="e9cf3-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="e9cf3-130">Enter your **App Name** and **Identifier**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="e9cf3-131">Click the **Target Plaforms** you want to support and then click **Next** and **Create**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-131">Click the **Target Plaforms** you want to support and then click **Next** and **Create**.</span></span>
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="e9cf3-132">This creates a new Android project.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="e9cf3-133">Open the project properties by right-clicking your new project in the Solution view and choosing **Options**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-133">Open the project properties by right-clicking your new project in the Solution view and choosing **Options**.</span></span> <span data-ttu-id="e9cf3-134">Select the **Android Application** item in the **Build** section.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-134">Select the **Android Application** item in the **Build** section.</span></span>
   
    <span data-ttu-id="e9cf3-135">Ensure that the first letter of your **Package name** is lowercase.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-135">Ensure that the first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="e9cf3-136">The first letter of the package name must be lowercase.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-136">The first letter of the package name must be lowercase.</span></span> <span data-ttu-id="e9cf3-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="e9cf3-138">Optionally, set the **Minimum Android version** to another API Level.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-138">Optionally, set the **Minimum Android version** to another API Level.</span></span>
3. <span data-ttu-id="e9cf3-139">Optionally, set the **Target Android version** to the another API version that you want to target (must be API level 8 or higher).</span><span class="sxs-lookup"><span data-stu-id="e9cf3-139">Optionally, set the **Target Android version** to the another API version that you want to target (must be API level 8 or higher).</span></span>

<span data-ttu-id="e9cf3-140">Click **OK** and close the Project Options dialog.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-140">Click **OK** and close the Project Options dialog.</span></span>

### <a name="add-the-required-components-to-your-project"></a><span data-ttu-id="e9cf3-141">Add the required components to your project</span><span class="sxs-lookup"><span data-stu-id="e9cf3-141">Add the required components to your project</span></span>
<span data-ttu-id="e9cf3-142">The Google Cloud Messaging Client available on the Xamarin Component Store simplifies the process of supporting push notifications in Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-142">The Google Cloud Messaging Client available on the Xamarin Component Store simplifies the process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="e9cf3-143">Right-click the Components folder in Xamarin.Android app and choose **Get More Components**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-143">Right-click the Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="e9cf3-144">Search for the **Azure Messaging** component and add it to the project.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-144">Search for the **Azure Messaging** component and add it to the project.</span></span>
3. <span data-ttu-id="e9cf3-145">Search for the **Google Cloud Messaging Client** component and add it to the project.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-145">Search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="e9cf3-146">Set up notification hubs in your project</span><span class="sxs-lookup"><span data-stu-id="e9cf3-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="e9cf3-147">Gather the following information for your Android app and notification hub:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-147">Gather the following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="e9cf3-148">**GoogleProjectNumber**:  Get this Project Number value from the overview of your app on the Google Developer Portal.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-148">**GoogleProjectNumber**:  Get this Project Number value from the overview of your app on the Google Developer Portal.</span></span> <span data-ttu-id="e9cf3-149">You made a note of this value earlier when you created the app on the portal.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-149">You made a note of this value earlier when you created the app on the portal.</span></span>
   * <span data-ttu-id="e9cf3-150">**Listen connection string**: On the dashboard in the [Azure Classic Portal], click **View connection strings**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-150">**Listen connection string**: On the dashboard in the [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="e9cf3-151">Copy the *DefaultListenSharedAccessSignature* connection string for this value.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-151">Copy the *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="e9cf3-152">**Hub name**: This is the name of your hub from the [Azure Classic Portal].</span><span class="sxs-lookup"><span data-stu-id="e9cf3-152">**Hub name**: This is the name of your hub from the [Azure Classic Portal].</span></span> <span data-ttu-id="e9cf3-153">For example, *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="e9cf3-154">Create a **Constants.cs** class for your Xamarin project and define the following constant values in the class.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-154">Create a **Constants.cs** class for your Xamarin project and define the following constant values in the class.</span></span> <span data-ttu-id="e9cf3-155">Replace the placeholders with your values.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-155">Replace the placeholders with your values.</span></span>
     
       <span data-ttu-id="e9cf3-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="e9cf3-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="e9cf3-157">}</span><span class="sxs-lookup"><span data-stu-id="e9cf3-157">}</span></span>
2. <span data-ttu-id="e9cf3-158">Add the following using statements to **MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-158">Add the following using statements to **MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="e9cf3-159">Add an instance variable to the `MainActivity` class that will be used to show an alert dialog when the app is running:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-159">Add an instance variable to the `MainActivity` class that will be used to show an alert dialog when the app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="e9cf3-160">Create the following method in the **MainActivity** class:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-160">Create the following method in the **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="e9cf3-161">In the `OnCreate` method of **MainActivity.cs**, initialize the `instance` variable and add a call to `RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-161">In the `OnCreate` method of **MainActivity.cs**, initialize the `instance` variable and add a call to `RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from the "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from the layout resource,
            // and attach an event to it
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="e9cf3-162">Create a new class, **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e9cf3-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="e9cf3-164">However, a quick alternative to manually creating **MyBroadcastReceiver.cs** is to refer to the **GcmService.cs** file found in the sample Xamarin.Android project included with the [NotificationHubs samples][GitHub].</span><span class="sxs-lookup"><span data-stu-id="e9cf3-164">However, a quick alternative to manually creating **MyBroadcastReceiver.cs** is to refer to the **GcmService.cs** file found in the sample Xamarin.Android project included with the [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="e9cf3-165">Duplicating **GcmService.cs** and changing class names can be a great place to start as well.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-165">Duplicating **GcmService.cs** and changing class names can be a great place to start as well.</span></span>
   > 
   > 
7. <span data-ttu-id="e9cf3-166">Add the following using statements to **MyBroadcastReceiver.cs** (referring to the component and assembly that you added earlier):</span><span class="sxs-lookup"><span data-stu-id="e9cf3-166">Add the following using statements to **MyBroadcastReceiver.cs** (referring to the component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="e9cf3-167">In **MyBroadcastReceiver.cs**, add the following permission requests between the **using** statements and the **namespace** declaration:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-167">In **MyBroadcastReceiver.cs**, add the following permission requests between the **using** statements and the **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="e9cf3-168">In **MyBroadcastReceiver.cs**, change the **MyBroadcastReceiver** class to match the following:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-168">In **MyBroadcastReceiver.cs**, change the **MyBroadcastReceiver** class to match the following:</span></span>
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. <span data-ttu-id="e9cf3-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="e9cf3-170">Make sure to apply the **Service** attribute to the class:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-170">Make sure to apply the **Service** attribute to the class:</span></span>
    
         [Service] // Must use the service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="e9cf3-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="e9cf3-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response to interacting with the notification hub.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response to interacting with the notification hub.</span></span>
12. <span data-ttu-id="e9cf3-173">Override the **OnRegistered()** method in **PushHandlerService** by using the following code:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-173">Override the **OnRegistered()** method in **PushHandlerService** by using the following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "The device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > <span data-ttu-id="e9cf3-174">In the **OnRegistered()** code above, you should note the ability to specify tags to register for specific messaging channels.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-174">In the **OnRegistered()** code above, you should note the ability to specify tags to register for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="e9cf3-175">Override the **OnMessage** method in **PushHandlerService** by using the following code:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-175">Override the **OnMessage** method in **PushHandlerService** by using the following code:</span></span>
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. <span data-ttu-id="e9cf3-176">Add the following **createNotification** and **dialogNotify** methods to **PushHandlerService** for notifying users when a notification is received.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-176">Add the following **createNotification** and **dialogNotify** methods to **PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e9cf3-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="e9cf3-178">If you test this on Android 5.0 or later, the app will need to be running to receive the notification.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-178">If you test this on Android 5.0 or later, the app will need to be running to receive the notification.</span></span> <span data-ttu-id="e9cf3-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="e9cf3-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent to show UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create the notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove the notification once the user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set the notification info
            //we use the pending intent, passing our ui intent over, which will get called
            //when the notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show the notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. <span data-ttu-id="e9cf3-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "The device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-the-emulator"></a><span data-ttu-id="e9cf3-181">Run your app in the emulator</span><span class="sxs-lookup"><span data-stu-id="e9cf3-181">Run your app in the emulator</span></span>
<span data-ttu-id="e9cf3-182">If you run this app in the emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-182">If you run this app in the emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9cf3-183">In order to receive push notifications, you must set up a Google account on your Android Virtual Device.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-183">In order to receive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="e9cf3-184">(In the emulator, navigate to **Settings** and click **Add Account**.) Also, make sure that the emulator is connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-184">(In the emulator, navigate to **Settings** and click **Add Account**.) Also, make sure that the emulator is connected to the Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="e9cf3-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="e9cf3-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="e9cf3-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="e9cf3-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="e9cf3-188">Select **Google APIs** in **Target**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="e9cf3-189">On the top toolbar, click **Run**, and then select your app.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-189">On the top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="e9cf3-190">This starts the emulator and runs the app.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-190">This starts the emulator and runs the app.</span></span>
   
   <span data-ttu-id="e9cf3-191">The app retrieves the *registrationId* from GCM and registers with the notification hub.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-191">The app retrieves the *registrationId* from GCM and registers with the notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="e9cf3-192">Send notifications from your backend</span><span class="sxs-lookup"><span data-stu-id="e9cf3-192">Send notifications from your backend</span></span>
<span data-ttu-id="e9cf3-193">You can test receiving notifications in your app by sending notifications in the [Azure Classic Portal] via the debug tab on the notification hub, as shown in the screen below.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-193">You can test receiving notifications in your app by sending notifications in the [Azure Classic Portal] via the debug tab on the notification hub, as shown in the screen below.</span></span>

![][30]

<span data-ttu-id="e9cf3-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="e9cf3-195">You can also use the REST API directly to send notification messages if a library is not available for your backend.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-195">You can also use the REST API directly to send notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="e9cf3-196">Here is a list of some other tutorials that you may want to review for sending notifications:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-196">Here is a list of some other tutorials that you may want to review for sending notifications:</span></span>

* <span data-ttu-id="e9cf3-197">ASP.NET: See [Use Notification Hubs to push notifications to users].</span><span class="sxs-lookup"><span data-stu-id="e9cf3-197">ASP.NET: See [Use Notification Hubs to push notifications to users].</span></span>
* <span data-ttu-id="e9cf3-198">Azure Notification Hubs Java SDK: See [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-198">Azure Notification Hubs Java SDK: See [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="e9cf3-199">This has been tested in Eclipse for Android Development.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="e9cf3-200">PHP: See [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e9cf3-200">PHP: See [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="e9cf3-201">In the next subsections of the tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-201">In the next subsections of the tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="e9cf3-202">(Optional) Send notifications by using a .NET app</span><span class="sxs-lookup"><span data-stu-id="e9cf3-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="e9cf3-203">In this section, we will send notifications by using a .NET console app</span><span class="sxs-lookup"><span data-stu-id="e9cf3-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="e9cf3-204">Create a new Visual C# console application:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="e9cf3-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="e9cf3-206">This displays the Package Manager Console in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-206">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="e9cf3-207">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-207">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="e9cf3-208">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-208">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="e9cf3-209">Open the Program.cs file and add the following `using` statement:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-209">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="e9cf3-210">In your `Program` class, add the following method.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-210">In your `Program` class, add the following method.</span></span> <span data-ttu-id="e9cf3-211">Update the placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from the [Azure Classic Portal].</span><span class="sxs-lookup"><span data-stu-id="e9cf3-211">Update the placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from the [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="e9cf3-212">Add the following lines in your **Main** method:</span><span class="sxs-lookup"><span data-stu-id="e9cf3-212">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="e9cf3-213">Press the F5 key to run the app.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-213">Press the F5 key to run the app.</span></span> <span data-ttu-id="e9cf3-214">You should receive a notification in the app.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-214">You should receive a notification in the app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="e9cf3-215">(Optional) Send notifications by using a mobile service</span><span class="sxs-lookup"><span data-stu-id="e9cf3-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="e9cf3-216">Follow [Get started with Mobile Services].</span><span class="sxs-lookup"><span data-stu-id="e9cf3-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="e9cf3-217">Sign in to the [Azure Classic Portal], and select your mobile service.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-217">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="e9cf3-218">Select the **Scheduler** tab on the top.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-218">Select the **Scheduler** tab on the top.</span></span>
   
      ![][22]
4. <span data-ttu-id="e9cf3-219">Create a new scheduled job, insert a name, and select **On demand**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="e9cf3-220">When the job is created, click the job name.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-220">When the job is created, click the job name.</span></span> <span data-ttu-id="e9cf3-221">Then click the **Script** tab on the top bar.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-221">Then click the **Script** tab on the top bar.</span></span>
6. <span data-ttu-id="e9cf3-222">Insert the following script inside your scheduler function.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-222">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="e9cf3-223">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-223">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="e9cf3-224">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-224">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. <span data-ttu-id="e9cf3-225">Click **Run Once** on the bottom bar.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-225">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="e9cf3-226">You should receive a toast notification.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9cf3-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="e9cf3-227">Next steps</span></span>
<span data-ttu-id="e9cf3-228">In this simple example, you broadcasted notifications to all your Android devices.</span><span class="sxs-lookup"><span data-stu-id="e9cf3-228">In this simple example, you broadcasted notifications to all your Android devices.</span></span> <span data-ttu-id="e9cf3-229">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span><span class="sxs-lookup"><span data-stu-id="e9cf3-229">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="e9cf3-230">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span><span class="sxs-lookup"><span data-stu-id="e9cf3-230">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="e9cf3-231">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for Android].</span><span class="sxs-lookup"><span data-stu-id="e9cf3-231">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app to the Notification Hub]: #connecting-app
[Run your app with the emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/notification-hubs/media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[Azure Classic Portal]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Android]: http://msdn.microsoft.com/library/dn282661.aspx

[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet
[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Messaging Component]: http://components.xamarin.com/view/azure-messaging












