---
title: Get started with Azure Mobile Engagement for Windows Phone Silverlight apps
description: Learn how to use Azure Mobile Engagement with analytics and push notifications for Windows Phone Silverlight apps.
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: ''
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 67fd8e9903f3cc8de488dea545496e25580ab5dc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669104"
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="cfb75-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span><span class="sxs-lookup"><span data-stu-id="cfb75-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="cfb75-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Phone Silverlight application.</span><span class="sxs-lookup"><span data-stu-id="cfb75-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="cfb75-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="cfb75-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="cfb75-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span><span class="sxs-lookup"><span data-stu-id="cfb75-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="cfb75-107">If you are targeting Windows Phone 8.1 (non-Silverlight), refer to the [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cfb75-107">If you are targeting Windows Phone 8.1 (non-Silverlight), refer to the [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="cfb75-108">This tutorial requires the following:</span><span class="sxs-lookup"><span data-stu-id="cfb75-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="cfb75-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="cfb75-109">Visual Studio 2013</span></span>
* <span data-ttu-id="cfb75-110">[MicrosoftAzure.MobileEngagement] Nuget package</span><span class="sxs-lookup"><span data-stu-id="cfb75-110">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="cfb75-111">To complete this tutorial, you must have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="cfb75-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="cfb75-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="cfb75-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cfb75-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="cfb75-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <a id="setup-azme"></a><span data-ttu-id="cfb75-114">Setup Mobile Engagement for your Windows Phone app</span><span class="sxs-lookup"><span data-stu-id="cfb75-114">Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a><span data-ttu-id="cfb75-115">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="cfb75-115">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="cfb75-116">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span><span class="sxs-lookup"><span data-stu-id="cfb75-116">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="cfb75-117">The complete integration documentation can be found in the [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="cfb75-117">The complete integration documentation can be found in the [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="cfb75-118">We will create a basic app with Visual Studio to demonstrate the integration.</span><span class="sxs-lookup"><span data-stu-id="cfb75-118">We will create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="cfb75-119">Create a new Windows Phone Silverlight project</span><span class="sxs-lookup"><span data-stu-id="cfb75-119">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="cfb75-120">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cfb75-120">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="cfb75-121">Start Visual Studio, and in the **Home** screen, select **New Project**.</span><span class="sxs-lookup"><span data-stu-id="cfb75-121">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="cfb75-122">In the pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span><span class="sxs-lookup"><span data-stu-id="cfb75-122">In the pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="cfb75-123">Fill in the app **Name** and **Solution name**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="cfb75-123">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="cfb75-124">You can choose to target either **Windows Phone 8.0** or **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="cfb75-124">You can choose to target either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="cfb75-125">You have now created a new Windows Phone Silverlight app into which we will integrate the Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="cfb75-125">You have now created a new Windows Phone Silverlight app into which we will integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="cfb75-126">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="cfb75-126">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="cfb75-127">Install the [MicrosoftAzure.MobileEngagement] nuget package in your project.</span><span class="sxs-lookup"><span data-stu-id="cfb75-127">Install the [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="cfb75-128">Open `WMAppManifest.xml` (under the Properties folder) and make sure the following are declared (add them if they are not) in the `<Capabilities />` tag:</span><span class="sxs-lookup"><span data-stu-id="cfb75-128">Open `WMAppManifest.xml` (under the Properties folder) and make sure the following are declared (add them if they are not) in the `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="cfb75-129">Now paste the connection string that you copied earlier for your Mobile Engagement app and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span><span class="sxs-lookup"><span data-stu-id="cfb75-129">Now paste the connection string that you copied earlier for your Mobile Engagement app and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="cfb75-130">In the `App.xaml.cs` file:</span><span class="sxs-lookup"><span data-stu-id="cfb75-130">In the `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="cfb75-131">a.</span><span class="sxs-lookup"><span data-stu-id="cfb75-131">a.</span></span> <span data-ttu-id="cfb75-132">Add the `using` statement:</span><span class="sxs-lookup"><span data-stu-id="cfb75-132">Add the `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="cfb75-133">b.</span><span class="sxs-lookup"><span data-stu-id="cfb75-133">b.</span></span> <span data-ttu-id="cfb75-134">Initialize the SDK in the `Application_Launching` method:</span><span class="sxs-lookup"><span data-stu-id="cfb75-134">Initialize the SDK in the `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="cfb75-135">c.</span><span class="sxs-lookup"><span data-stu-id="cfb75-135">c.</span></span> <span data-ttu-id="cfb75-136">Insert the following in the `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="cfb75-136">Insert the following in the `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <a id="monitor"></a><span data-ttu-id="cfb75-137">Enable real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="cfb75-137">Enable real-time monitoring</span></span>
<span data-ttu-id="cfb75-138">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="cfb75-138">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="cfb75-139">In the MainPage.xaml.cs, add the `using` statement:</span><span class="sxs-lookup"><span data-stu-id="cfb75-139">In the MainPage.xaml.cs, add the `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="cfb75-140">Replace the base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="cfb75-140">Replace the base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="cfb75-141">In your `MainPage.xml` file:</span><span class="sxs-lookup"><span data-stu-id="cfb75-141">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="cfb75-142">a.</span><span class="sxs-lookup"><span data-stu-id="cfb75-142">a.</span></span> <span data-ttu-id="cfb75-143">Add to your namespaces declarations:</span><span class="sxs-lookup"><span data-stu-id="cfb75-143">Add to your namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="cfb75-144">b.</span><span class="sxs-lookup"><span data-stu-id="cfb75-144">b.</span></span> <span data-ttu-id="cfb75-145">Replace `phone:PhoneApplicationPage` in the XML tag name with `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="cfb75-145">Replace `phone:PhoneApplicationPage` in the XML tag name with `engagement:EngagementPage`.</span></span>

## <a id="monitor"></a><span data-ttu-id="cfb75-146">Connect app with real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="cfb75-146">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a><span data-ttu-id="cfb75-147">Enable push notifications and in-app messaging</span><span class="sxs-lookup"><span data-stu-id="cfb75-147">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="cfb75-148">Mobile Engagement allows you to interact and reach your users with Push Notifications and in-app Messaging in the context of campaigns.</span><span class="sxs-lookup"><span data-stu-id="cfb75-148">Mobile Engagement allows you to interact and reach your users with Push Notifications and in-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="cfb75-149">This module is called REACH in the Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="cfb75-149">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="cfb75-150">The following sections set up your app to receive them.</span><span class="sxs-lookup"><span data-stu-id="cfb75-150">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-mpns-push-notifications"></a><span data-ttu-id="cfb75-151">Enable your app to receive MPNS Push Notifications</span><span class="sxs-lookup"><span data-stu-id="cfb75-151">Enable your app to receive MPNS Push Notifications</span></span>
<span data-ttu-id="cfb75-152">Add new Capabilities to your `WMAppManifest.xml` file:</span><span class="sxs-lookup"><span data-stu-id="cfb75-152">Add new Capabilities to your `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="cfb75-153">Initialize the REACH SDK</span><span class="sxs-lookup"><span data-stu-id="cfb75-153">Initialize the REACH SDK</span></span>
1. <span data-ttu-id="cfb75-154">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in the **Application_Launching** function, right after the agent initialization:</span><span class="sxs-lookup"><span data-stu-id="cfb75-154">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in the **Application_Launching** function, right after the agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="cfb75-155">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in the **Application_Activated** function, right after the agent initialization:</span><span class="sxs-lookup"><span data-stu-id="cfb75-155">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in the **Application_Activated** function, right after the agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="cfb75-156">You're all set.</span><span class="sxs-lookup"><span data-stu-id="cfb75-156">You're all set.</span></span> <span data-ttu-id="cfb75-157">Now we will verify that you have correctly cried out this basic integration.</span><span class="sxs-lookup"><span data-stu-id="cfb75-157">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <a id="send"></a><span data-ttu-id="cfb75-158">Send a notification to your app</span><span class="sxs-lookup"><span data-stu-id="cfb75-158">Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="cfb75-159">You should now see a notification on your device which will show up as an in-app notification if the app is open otherwise as a toast notification like the following:</span><span class="sxs-lookup"><span data-stu-id="cfb75-159">You should now see a notification on your device which will show up as an in-app notification if the app is open otherwise as a toast notification like the following:</span></span> 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-phone-get-started/push-screenshot.png





