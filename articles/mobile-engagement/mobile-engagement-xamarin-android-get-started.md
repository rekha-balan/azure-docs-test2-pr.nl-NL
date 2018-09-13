---
title: Get Started with Azure Mobile Engagement for Xamarin.Android
description: Learn how to use Azure Mobile Engagement with Analytics and Push Notifications for Xamarin.Android Apps.
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: ''
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 1abbc6a1e097d8f5e0094a16904b6918e70ed63c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562747"
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="fcca6-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span><span class="sxs-lookup"><span data-stu-id="fcca6-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="fcca6-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Xamarin.Android application.</span><span class="sxs-lookup"><span data-stu-id="fcca6-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="fcca6-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fcca6-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="fcca6-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="fcca6-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

<span data-ttu-id="fcca6-107">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="fcca6-107">This tutorial requires the following:</span></span>

* <span data-ttu-id="fcca6-108">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="fcca6-108">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="fcca6-109">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="fcca6-109">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="fcca6-110">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="fcca6-110">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="fcca6-111">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="fcca6-111">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="fcca6-112">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="fcca6-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="fcca6-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="fcca6-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fcca6-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="fcca6-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <a id="setup-azme"></a><span data-ttu-id="fcca6-115">Setup Mobile Engagement for your Android app</span><span class="sxs-lookup"><span data-stu-id="fcca6-115">Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a><span data-ttu-id="fcca6-116">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="fcca6-116">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="fcca6-117">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span><span class="sxs-lookup"><span data-stu-id="fcca6-117">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="fcca6-118">We will create a basic app with Xamarin Studio to demonstrate the integration.</span><span class="sxs-lookup"><span data-stu-id="fcca6-118">We will create a basic app with Xamarin Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="fcca6-119">Create a new Xamarin.Android project</span><span class="sxs-lookup"><span data-stu-id="fcca6-119">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="fcca6-120">Launch **Xamarin Studio** Go to **File** -> **New** -> **Solution**</span><span class="sxs-lookup"><span data-stu-id="fcca6-120">Launch **Xamarin Studio** Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="fcca6-121">Select **Android App** then make sure the selected language is **C#** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-121">Select **Android App** then make sure the selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="fcca6-122">Fill in the **App Name** and the **Organization Identifier**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-122">Fill in the **App Name** and the **Organization Identifier**.</span></span> <span data-ttu-id="fcca6-123">Make sure to checkmark **Google Play Services** and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-123">Make sure to checkmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="fcca6-124">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-124">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="fcca6-125">Xamarin Studio will create the app in which we will integrate Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fcca6-125">Xamarin Studio will create the app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="fcca6-126">Connect your app to Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="fcca6-126">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="fcca6-127">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span><span class="sxs-lookup"><span data-stu-id="fcca6-127">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="fcca6-128">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span><span class="sxs-lookup"><span data-stu-id="fcca6-128">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="fcca6-129">Open **MainActivity.cs** and add the following using statements:</span><span class="sxs-lookup"><span data-stu-id="fcca6-129">Open **MainActivity.cs** and add the following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="fcca6-130">In the `OnCreate` method, add the following to initialize the connection with Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="fcca6-130">In the `OnCreate` method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="fcca6-131">Make sure to add your **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="fcca6-131">Make sure to add your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="fcca6-132">Add permissions and a service declaration</span><span class="sxs-lookup"><span data-stu-id="fcca6-132">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="fcca6-133">Open up the **Manifest.xml** file under the Properties folder.</span><span class="sxs-lookup"><span data-stu-id="fcca6-133">Open up the **Manifest.xml** file under the Properties folder.</span></span> <span data-ttu-id="fcca6-134">Select Source tab so that you directly update the XML source.</span><span class="sxs-lookup"><span data-stu-id="fcca6-134">Select Source tab so that you directly update the XML source.</span></span>
2. <span data-ttu-id="fcca6-135">Add these permissions to the Manifest.xml (which can be found under the **Properties** folder) of your project immediately before or after the `<application>` tag:</span><span class="sxs-lookup"><span data-stu-id="fcca6-135">Add these permissions to the Manifest.xml (which can be found under the **Properties** folder) of your project immediately before or after the `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="fcca6-136">Add the following between the `<application>` and `</application>` tags to declare the agent service:</span><span class="sxs-lookup"><span data-stu-id="fcca6-136">Add the following between the `<application>` and `</application>` tags to declare the agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="fcca6-137">In the code you just pasted, replace `"<Your application name>"` in the label.</span><span class="sxs-lookup"><span data-stu-id="fcca6-137">In the code you just pasted, replace `"<Your application name>"` in the label.</span></span> <span data-ttu-id="fcca6-138">This is displayed in the **Settings** menu where users can see services running on the device.</span><span class="sxs-lookup"><span data-stu-id="fcca6-138">This is displayed in the **Settings** menu where users can see services running on the device.</span></span> <span data-ttu-id="fcca6-139">You can add the word "Service" in that label for example.</span><span class="sxs-lookup"><span data-stu-id="fcca6-139">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="fcca6-140">Send a screen to Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="fcca6-140">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="fcca6-141">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="fcca6-141">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span> <span data-ttu-id="fcca6-142">For doing this - ensure that the `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span><span class="sxs-lookup"><span data-stu-id="fcca6-142">For doing this - ensure that the `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="fcca6-143">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span><span class="sxs-lookup"><span data-stu-id="fcca6-143">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <a id="monitor"></a><span data-ttu-id="fcca6-144">Connect app with real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="fcca6-144">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a><span data-ttu-id="fcca6-145">Enable push notifications and in-app messaging</span><span class="sxs-lookup"><span data-stu-id="fcca6-145">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="fcca6-146">Mobile Engagement allows you to interact with and REACH your users with push notifications and in-app messaging in the context of campaigns.</span><span class="sxs-lookup"><span data-stu-id="fcca6-146">Mobile Engagement allows you to interact with and REACH your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="fcca6-147">This module is called REACH in the Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="fcca6-147">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="fcca6-148">The following sections sets up your app to receive them.</span><span class="sxs-lookup"><span data-stu-id="fcca6-148">The following sections sets up your app to receive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-android-get-started/1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-android-get-started/2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-android-get-started/3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-android-get-started/4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-android-get-started/5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-xamarin-android-get-started/6.png






