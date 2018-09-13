---
title: Get started with Android Apps Azure Mobile Engagement
description: Learn how to use Azure Mobile Engagement with analytics and push notifications for Android apps.
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: a5757286736fbd6615c3f716ecec560d8e6ba928
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552521"
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="74e59-103">Get started with Azure Mobile Engagement for Android apps</span><span class="sxs-lookup"><span data-stu-id="74e59-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="74e59-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of an Android application.</span><span class="sxs-lookup"><span data-stu-id="74e59-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of an Android application.</span></span>
<span data-ttu-id="74e59-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="74e59-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="74e59-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="74e59-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74e59-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="74e59-107">Prerequisites</span></span>
<span data-ttu-id="74e59-108">Completing this tutorial requires the [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span><span class="sxs-lookup"><span data-stu-id="74e59-108">Completing this tutorial requires the [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>

<span data-ttu-id="74e59-109">It also requires the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="74e59-109">It also requires the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74e59-110">To complete this tutorial, you need an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="74e59-110">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="74e59-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="74e59-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="74e59-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="74e59-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="74e59-113">Set up Mobile Engagement for your Android app</span><span class="sxs-lookup"><span data-stu-id="74e59-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="74e59-114">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="74e59-114">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="74e59-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span><span class="sxs-lookup"><span data-stu-id="74e59-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="74e59-116">You create a basic app with Android Studio to demonstrate the integration.</span><span class="sxs-lookup"><span data-stu-id="74e59-116">You create a basic app with Android Studio to demonstrate the integration.</span></span>

<span data-ttu-id="74e59-117">The complete integration documentation can be found in the [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74e59-117">The complete integration documentation can be found in the [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="74e59-118">Create an Android project</span><span class="sxs-lookup"><span data-stu-id="74e59-118">Create an Android project</span></span>
1. <span data-ttu-id="74e59-119">Start **Android Studio**, and in the pop-up, select **Start a new Android Studio project**.</span><span class="sxs-lookup"><span data-stu-id="74e59-119">Start **Android Studio**, and in the pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="74e59-120">Provide an app name and company domain.</span><span class="sxs-lookup"><span data-stu-id="74e59-120">Provide an app name and company domain.</span></span> <span data-ttu-id="74e59-121">Make a note of what you are filling, because you need it later.</span><span class="sxs-lookup"><span data-stu-id="74e59-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="74e59-122">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="74e59-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="74e59-123">Select the target form factor and API level, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="74e59-123">Select the target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="74e59-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span><span class="sxs-lookup"><span data-stu-id="74e59-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="74e59-125">Select **Blank Activity** here, which is the only screen for this app and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="74e59-125">Select **Blank Activity** here, which is the only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="74e59-126">Finally, leave the defaults as is and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="74e59-126">Finally, leave the defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="74e59-127">Android Studio now creates the demo app into which we integrate Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="74e59-127">Android Studio now creates the demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-the-sdk-library-in-your-project"></a><span data-ttu-id="74e59-128">Include the SDK library in your project</span><span class="sxs-lookup"><span data-stu-id="74e59-128">Include the SDK library in your project</span></span>
1. <span data-ttu-id="74e59-129">Download the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="74e59-129">Download the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="74e59-130">Extract the archive file to a folder in your computer.</span><span class="sxs-lookup"><span data-stu-id="74e59-130">Extract the archive file to a folder in your computer.</span></span>
3. <span data-ttu-id="74e59-131">Identify the .jar library for the current version of this SDK and copy it to the Clipboard.</span><span class="sxs-lookup"><span data-stu-id="74e59-131">Identify the .jar library for the current version of this SDK and copy it to the Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="74e59-132">Navigate to the **Project** section (1) and paste the .jar in the libs folder (2).</span><span class="sxs-lookup"><span data-stu-id="74e59-132">Navigate to the **Project** section (1) and paste the .jar in the libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="74e59-133">To load the library, sync the project .</span><span class="sxs-lookup"><span data-stu-id="74e59-133">To load the library, sync the project .</span></span>

      ![][8]

### <a name="connect-your-app-to-mobile-engagement-backend-with-the-connection-string"></a><span data-ttu-id="74e59-134">Connect your app to Mobile Engagement backend with the Connection String</span><span class="sxs-lookup"><span data-stu-id="74e59-134">Connect your app to Mobile Engagement backend with the Connection String</span></span>
1. <span data-ttu-id="74e59-135">Copy the following lines of code into the activity creation (must be done only in one place of your application, usually the main activity).</span><span class="sxs-lookup"><span data-stu-id="74e59-135">Copy the following lines of code into the activity creation (must be done only in one place of your application, usually the main activity).</span></span> <span data-ttu-id="74e59-136">For this sample app, open up the MainActivity under src -> main -> java folder and add the following:</span><span class="sxs-lookup"><span data-stu-id="74e59-136">For this sample app, open up the MainActivity under src -> main -> java folder and add the following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="74e59-137">Resolve the references by pressing Alt + Enter or adding the following import statements:</span><span class="sxs-lookup"><span data-stu-id="74e59-137">Resolve the references by pressing Alt + Enter or adding the following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="74e59-138">Go back to the Azure Classic Portal in your app's **Connection Info** page and copy the **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="74e59-138">Go back to the Azure Classic Portal in your app's **Connection Info** page and copy the **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="74e59-139">Paste it into the `setConnectionString` parameter, replacing the entire string shown in the following code:</span><span class="sxs-lookup"><span data-stu-id="74e59-139">Paste it into the `setConnectionString` parameter, replacing the entire string shown in the following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="74e59-140">Add permissions and a service declaration</span><span class="sxs-lookup"><span data-stu-id="74e59-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="74e59-141">Add these permissions to the Manifest.xml of your project immediately before or after the `<application>` tag:</span><span class="sxs-lookup"><span data-stu-id="74e59-141">Add these permissions to the Manifest.xml of your project immediately before or after the `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="74e59-142">To declare the agent service, add this code between the `<application>` and `</application>` tags:</span><span class="sxs-lookup"><span data-stu-id="74e59-142">To declare the agent service, add this code between the `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="74e59-143">In the code you pasted, replace `"<Your application name>"` in the label, which is displayed in the **Settings** menu where you can see services running on the device.</span><span class="sxs-lookup"><span data-stu-id="74e59-143">In the code you pasted, replace `"<Your application name>"` in the label, which is displayed in the **Settings** menu where you can see services running on the device.</span></span> <span data-ttu-id="74e59-144">You can add the word "Service" in that label for example.</span><span class="sxs-lookup"><span data-stu-id="74e59-144">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="74e59-145">Send a screen to Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="74e59-145">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="74e59-146">To start sending data and ensure that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="74e59-146">To start sending data and ensure that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

<span data-ttu-id="74e59-147">Go to **MainActivity.java** and add the following to replace the base class of **MainActivity** to **EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="74e59-147">Go to **MainActivity.java** and add the following to replace the base class of **MainActivity** to **EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="74e59-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how to inherit from different classes.</span><span class="sxs-lookup"><span data-stu-id="74e59-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how to inherit from different classes.</span></span>
>
>

<span data-ttu-id="74e59-149">Comment out the following line for this simple sample scenario:</span><span class="sxs-lookup"><span data-stu-id="74e59-149">Comment out the following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="74e59-150">If you want to keep the `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="74e59-150">If you want to keep the `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="74e59-151">Connect app with real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="74e59-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="74e59-152">Enable push notifications and in-app messaging</span><span class="sxs-lookup"><span data-stu-id="74e59-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="74e59-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span><span class="sxs-lookup"><span data-stu-id="74e59-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="74e59-154">This module is called REACH in the Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="74e59-154">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="74e59-155">The following section sets up your app to receive them.</span><span class="sxs-lookup"><span data-stu-id="74e59-155">The following section sets up your app to receive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="74e59-156">Copy SDK resources in your project</span><span class="sxs-lookup"><span data-stu-id="74e59-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="74e59-157">Navigate back to your SDK download content and copy the **res** folder.</span><span class="sxs-lookup"><span data-stu-id="74e59-157">Navigate back to your SDK download content and copy the **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="74e59-158">Go back to Android Studio, select the **main** directory of your project files, and then paste it to add the resources to your project.</span><span class="sxs-lookup"><span data-stu-id="74e59-158">Go back to Android Studio, select the **main** directory of your project files, and then paste it to add the resources to your project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="74e59-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="74e59-159">Next steps</span></span>
<span data-ttu-id="74e59-160">Go to [Android SDK](mobile-engagement-android-sdk-overview.md) to get detailed knowledge about the SDK integration.</span><span class="sxs-lookup"><span data-stu-id="74e59-160">Go to [Android SDK](mobile-engagement-android-sdk-overview.md) to get detailed knowledge about the SDK integration.</span></span>

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-android-get-started/sdk-content.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-android-get-started/paste-jar.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-android-get-started/sync-project.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-android-get-started/copy-resources.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-android-get-started/paste-resources.png











