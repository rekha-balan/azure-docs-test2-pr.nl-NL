---
title: Get started with Windows Universal Apps Azure Mobile Engagement
description: Learn how to use Azure Mobile Engagement with analytics and push notifications for Windows Universal Apps.
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 2498f6a96f6b2158542e1a2a192bb926337e07d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552714"
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="2b2cf-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span><span class="sxs-lookup"><span data-stu-id="2b2cf-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="2b2cf-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Universal application.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Universal application.</span></span>
<span data-ttu-id="2b2cf-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="2b2cf-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span><span class="sxs-lookup"><span data-stu-id="2b2cf-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b2cf-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2b2cf-107">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="2b2cf-108">Set up Mobile Engagement for your Windows Universal app</span><span class="sxs-lookup"><span data-stu-id="2b2cf-108">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a><span data-ttu-id="2b2cf-109">Connect your app to the Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="2b2cf-109">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="2b2cf-110">This tutorial presents a "basic integration," which is the minimal set required to collect data and send a push notification.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-110">This tutorial presents a "basic integration," which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="2b2cf-111">The complete integration documentation can be found in the [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2b2cf-111">The complete integration documentation can be found in the [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="2b2cf-112">You create a basic app with Visual Studio to demonstrate the integration.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-112">You create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="2b2cf-113">Create a Windows Universal App project</span><span class="sxs-lookup"><span data-stu-id="2b2cf-113">Create a Windows Universal App project</span></span>
<span data-ttu-id="2b2cf-114">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-114">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="2b2cf-115">Start Visual Studio, and in the **Home** screen, select **New Project**.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-115">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="2b2cf-116">In the pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-116">In the pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="2b2cf-117">Fill in the app **Name** and **Solution name**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-117">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="2b2cf-118">You have now created a Windows Universal App project into which you next integrate the Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-118">You have now created a Windows Universal App project into which you next integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="2b2cf-119">Connect your app to Mobile Engagement backend</span><span class="sxs-lookup"><span data-stu-id="2b2cf-119">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="2b2cf-120">Install the [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-120">Install the [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="2b2cf-121">If you are targeting both Windows and Windows Phone platforms, you need to do this for both projects.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-121">If you are targeting both Windows and Windows Phone platforms, you need to do this for both projects.</span></span> <span data-ttu-id="2b2cf-122">For Windows 8.x and Windows Phone 8.1, the same Nuget package places the correct platform-specific binaries in each project.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-122">For Windows 8.x and Windows Phone 8.1, the same Nuget package places the correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="2b2cf-123">Open **Package.appxmanifest** and make sure that the following capability is added there:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-123">Open **Package.appxmanifest** and make sure that the following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="2b2cf-124">Now copy the connection string that you copied earlier for your Mobile Engagement App and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-124">Now copy the connection string that you copied earlier for your Mobile Engagement App and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="2b2cf-125">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-125">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="2b2cf-126">Having two apps ensures that you can create correct segmentation of the audience and can send appropriately targeted notifications for each platform.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-126">Having two apps ensures that you can create correct segmentation of the audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2b2cf-127">NuGet does not automatically copy the SDK resources in your Windows 10 UWP application.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-127">NuGet does not automatically copy the SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="2b2cf-128">You have to do it manually following the steps which show up (readme.txt) when the Nuget package is installed.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-128">You have to do it manually following the steps which show up (readme.txt) when the Nuget package is installed.</span></span>  

1. <span data-ttu-id="2b2cf-129">In the `App.xaml.cs` file:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-129">In the `App.xaml.cs` file:</span></span>

    <span data-ttu-id="2b2cf-130">a.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-130">a.</span></span> <span data-ttu-id="2b2cf-131">Add the `using` statement:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-131">Add the `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="2b2cf-132">b.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-132">b.</span></span> <span data-ttu-id="2b2cf-133">Add a method that initializes the Engagement:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-133">Add a method that initializes the Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of the code
           }

    <span data-ttu-id="2b2cf-134">c.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-134">c.</span></span> <span data-ttu-id="2b2cf-135">Initialize the SDK in the **OnLaunched** method:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-135">Initialize the SDK in the **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

    <span data-ttu-id="2b2cf-136">c.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-136">c.</span></span> <span data-ttu-id="2b2cf-137">Insert the following in the **OnActivated** method and add the method if it is not already present:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-137">Insert the following in the **OnActivated** method and add the method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

## <a id="monitor"></a><span data-ttu-id="2b2cf-138">Enable real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="2b2cf-138">Enable real-time monitoring</span></span>
<span data-ttu-id="2b2cf-139">To start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-139">To start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="2b2cf-140">In the **MainPage.xaml.cs**, add the following `using` statement:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-140">In the **MainPage.xaml.cs**, add the following `using` statement:</span></span>

    <span data-ttu-id="2b2cf-141">using Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="2b2cf-141">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="2b2cf-142">Change the base class of **MainPage** from **Page** to **EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-142">Change the base class of **MainPage** from **Page** to **EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="2b2cf-143">In the `MainPage.xaml` file:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-143">In the `MainPage.xaml` file:</span></span>

    <span data-ttu-id="2b2cf-144">a.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-144">a.</span></span> <span data-ttu-id="2b2cf-145">Add to your namespaces declarations:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-145">Add to your namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="2b2cf-146">b.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-146">b.</span></span> <span data-ttu-id="2b2cf-147">Replace the **Page** in the XML tag name with **engagement:EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="2b2cf-147">Replace the **Page** in the XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b2cf-148">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-148">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="2b2cf-149">Otherwise, the activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span><span class="sxs-lookup"><span data-stu-id="2b2cf-149">Otherwise, the activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="2b2cf-150">This is especially important in a Windows Phone project where the default template has an `OnNavigatedTo` method.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-150">This is especially important in a Windows Phone project where the default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="2b2cf-151">For **Windows 10 Universal apps**, use the method recommended in the "Recommended method: overload your Page classes" section of [Advanced Reporting with the Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than the one mentioned above.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-151">For **Windows 10 Universal apps**, use the method recommended in the "Recommended method: overload your Page classes" section of [Advanced Reporting with the Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than the one mentioned above.</span></span>

## <a id="monitor"></a><span data-ttu-id="2b2cf-152">Connect app with real-time monitoring</span><span class="sxs-lookup"><span data-stu-id="2b2cf-152">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a><span data-ttu-id="2b2cf-153">Enable push notifications and in-app messaging</span><span class="sxs-lookup"><span data-stu-id="2b2cf-153">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="2b2cf-154">Mobile Engagement allows you to interact and reach your users with push notifications and in-app messaging in the context of campaigns.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-154">Mobile Engagement allows you to interact and reach your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="2b2cf-155">This module is called REACH in the Mobile Engagement portal.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-155">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="2b2cf-156">The following sections set up your app to receive them.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-156">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-wns-push-notifications"></a><span data-ttu-id="2b2cf-157">Enable your app to receive WNS Push Notifications</span><span class="sxs-lookup"><span data-stu-id="2b2cf-157">Enable your app to receive WNS Push Notifications</span></span>
1. <span data-ttu-id="2b2cf-158">In the `Package.appxmanifest` file, in the **Application** tab, under **Notifications**, set **Toast capable:** to **Yes**</span><span class="sxs-lookup"><span data-stu-id="2b2cf-158">In the `Package.appxmanifest` file, in the **Application** tab, under **Notifications**, set **Toast capable:** to **Yes**</span></span>

    ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="2b2cf-159">Initialize the REACH SDK</span><span class="sxs-lookup"><span data-stu-id="2b2cf-159">Initialize the REACH SDK</span></span>
<span data-ttu-id="2b2cf-160">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in the **InitEngagement** function right after the agent initialization:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-160">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in the **InitEngagement** function right after the agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="2b2cf-161">You're ready to send a toast.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-161">You're ready to send a toast.</span></span> <span data-ttu-id="2b2cf-162">Next we verify that you have correctly carried out this basic integration.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-162">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-to-mobile-engagement-to-send-notifications"></a><span data-ttu-id="2b2cf-163">Grant access to Mobile Engagement to send notifications</span><span class="sxs-lookup"><span data-stu-id="2b2cf-163">Grant access to Mobile Engagement to send notifications</span></span>
1. <span data-ttu-id="2b2cf-164">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-164">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="2b2cf-165">Click **Dashboard** at the top right corner and then click **Create a new app** from the left panel menu.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-165">Click **Dashboard** at the top right corner and then click **Create a new app** from the left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="2b2cf-166">Create your app by reserving its name.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-166">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="2b2cf-167">Once the app has been created, navigate to **Services -> Push notifications** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-167">Once the app has been created, navigate to **Services -> Push notifications** from the left menu.</span></span>

    ![][11]
5. <span data-ttu-id="2b2cf-168">In the Push notifications section, click the **Live Services site** link.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-168">In the Push notifications section, click the **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="2b2cf-169">You navigate to the Push credentials section.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-169">You navigate to the Push credentials section.</span></span> <span data-ttu-id="2b2cf-170">Make sure you are in the **App Settings** section and then copy your **Package SID** and **Client secret**</span><span class="sxs-lookup"><span data-stu-id="2b2cf-170">Make sure you are in the **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="2b2cf-171">Navigate to the **Settings** of your Mobile Engagement portal, and click the **Native Push** section on the left.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-171">Navigate to the **Settings** of your Mobile Engagement portal, and click the **Native Push** section on the left.</span></span> <span data-ttu-id="2b2cf-172">Then, click the **Edit** button to enter your **Package security identifier (SID)** and your **Secret Key** as shown:</span><span class="sxs-lookup"><span data-stu-id="2b2cf-172">Then, click the **Edit** button to enter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="2b2cf-173">Finally make sure that you have associated your Visual Studio app with this created app in the App store.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-173">Finally make sure that you have associated your Visual Studio app with this created app in the App store.</span></span> <span data-ttu-id="2b2cf-174">Click **Associate App with Store** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-174">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <a id="send"></a><span data-ttu-id="2b2cf-175">Send a notification to your app</span><span class="sxs-lookup"><span data-stu-id="2b2cf-175">Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="2b2cf-176">If the app is running, you see an in-app notification.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-176">If the app is running, you see an in-app notification.</span></span> <span data-ttu-id="2b2cf-177">otherwise if the app is closed, you see a toast notification.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-177">otherwise if the app is closed, you see a toast notification.</span></span>
<span data-ttu-id="2b2cf-178">If you see an in-app notification but not a toast notification, and you are running the app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in the toolbar to ensure that the app is suspended.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-178">If you see an in-app notification but not a toast notification, and you are running the app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in the toolbar to ensure that the app is suspended.</span></span> <span data-ttu-id="2b2cf-179">If you clicked the Home button while debugging the application in Visual Studio, then it doesn't always get suspended and while you see the notification as in-app, it doesn't show up as a toast notification.</span><span class="sxs-lookup"><span data-stu-id="2b2cf-179">If you clicked the Home button while debugging the application in Visual Studio, then it doesn't always get suspended and while you see the notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Windows Store Dev Center]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png












