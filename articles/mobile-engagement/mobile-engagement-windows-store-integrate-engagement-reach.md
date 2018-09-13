---
title: Windows Universal Apps Reach SDK Integration
description: How to Integrate Azure Mobile Engagement Reach with Windows Universal Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 9311e998e67d8d0d56da68fc9460df32ce7ce5a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660718"
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="cebe8-103">Windows Universal Apps Reach SDK Integration</span><span class="sxs-lookup"><span data-stu-id="cebe8-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="cebe8-104">You must follow the integration procedure described in the [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span><span class="sxs-lookup"><span data-stu-id="cebe8-104">You must follow the integration procedure described in the [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="cebe8-105">Embed the Engagement Reach SDK into your Windows Universal project</span><span class="sxs-lookup"><span data-stu-id="cebe8-105">Embed the Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="cebe8-106">You do not have anything to add.</span><span class="sxs-lookup"><span data-stu-id="cebe8-106">You do not have anything to add.</span></span> <span data-ttu-id="cebe8-107">`EngagementReach` references and resources are already in your project.</span><span class="sxs-lookup"><span data-stu-id="cebe8-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="cebe8-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span><span class="sxs-lookup"><span data-stu-id="cebe8-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span> <span data-ttu-id="cebe8-109">On Universal Apps you can also move the `Resources` folder on your shared project to share its content between apps, but you will have to keep the `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span><span class="sxs-lookup"><span data-stu-id="cebe8-109">On Universal Apps you can also move the `Resources` folder on your shared project to share its content between apps, but you will have to keep the `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-the-windows-notification-service"></a><span data-ttu-id="cebe8-110">Enable the Windows Notification Service</span><span class="sxs-lookup"><span data-stu-id="cebe8-110">Enable the Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="cebe8-111">Windows 8.x and Windows Phone 8.1 only</span><span class="sxs-lookup"><span data-stu-id="cebe8-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="cebe8-112">In order to use the **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in the left bot box.</span><span class="sxs-lookup"><span data-stu-id="cebe8-112">In order to use the **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in the left bot box.</span></span> <span data-ttu-id="cebe8-113">At the right of the box in `Notifications`, change `toast capable` from `(not set)` to `(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="cebe8-113">At the right of the box in `Notifications`, change `toast capable` from `(not set)` to `(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="cebe8-114">All platforms</span><span class="sxs-lookup"><span data-stu-id="cebe8-114">All platforms</span></span>
<span data-ttu-id="cebe8-115">You need to synchronize your app to your Microsoft account and to the engagement platform.</span><span class="sxs-lookup"><span data-stu-id="cebe8-115">You need to synchronize your app to your Microsoft account and to the engagement platform.</span></span> <span data-ttu-id="cebe8-116">For this you need to create an account or log on [windows dev center](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="cebe8-116">For this you need to create an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="cebe8-117">After that create a new application and find the SID and secret key.</span><span class="sxs-lookup"><span data-stu-id="cebe8-117">After that create a new application and find the SID and secret key.</span></span> <span data-ttu-id="cebe8-118">On the engagement frontend, go on your app setting in `native push` and paste your credentials.</span><span class="sxs-lookup"><span data-stu-id="cebe8-118">On the engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="cebe8-119">After that, right click on your project, select `store` and `Associate App with the Store...`.</span><span class="sxs-lookup"><span data-stu-id="cebe8-119">After that, right click on your project, select `store` and `Associate App with the Store...`.</span></span> <span data-ttu-id="cebe8-120">You just need to select the application you have create before to synchronize it.</span><span class="sxs-lookup"><span data-stu-id="cebe8-120">You just need to select the application you have create before to synchronize it.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="cebe8-121">Initialize the Engagement Reach SDK</span><span class="sxs-lookup"><span data-stu-id="cebe8-121">Initialize the Engagement Reach SDK</span></span>
<span data-ttu-id="cebe8-122">Modify the `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="cebe8-122">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="cebe8-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span><span class="sxs-lookup"><span data-stu-id="cebe8-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="cebe8-124">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span><span class="sxs-lookup"><span data-stu-id="cebe8-124">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="cebe8-125">You do not have to do it yourself.</span><span class="sxs-lookup"><span data-stu-id="cebe8-125">You do not have to do it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="cebe8-126">If you are using push notifications elsewhere in your application then you have to [share your push channel](#push-channel-sharing) with Engagement Reach.</span><span class="sxs-lookup"><span data-stu-id="cebe8-126">If you are using push notifications elsewhere in your application then you have to [share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="cebe8-127">Integration</span><span class="sxs-lookup"><span data-stu-id="cebe8-127">Integration</span></span>
<span data-ttu-id="cebe8-128">Engagement provides two ways to add the Reach in-app banners and interstitial views for announcements and polls in your application: the overlay integration and the web views manual integration.</span><span class="sxs-lookup"><span data-stu-id="cebe8-128">Engagement provides two ways to add the Reach in-app banners and interstitial views for announcements and polls in your application: the overlay integration and the web views manual integration.</span></span> <span data-ttu-id="cebe8-129">You should not combine both approach on the same page.</span><span class="sxs-lookup"><span data-stu-id="cebe8-129">You should not combine both approach on the same page.</span></span>

<span data-ttu-id="cebe8-130">The choice between the two integration could be summarized this way:</span><span class="sxs-lookup"><span data-stu-id="cebe8-130">The choice between the two integration could be summarized this way:</span></span>

* <span data-ttu-id="cebe8-131">You may choose the overlay integration if your pages already inherits from the Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span><span class="sxs-lookup"><span data-stu-id="cebe8-131">You may choose the overlay integration if your pages already inherits from the Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="cebe8-132">You may choose the web views manual integration if you want to precisely place the Reach UI within your pages or if you don't want to add another inheritance level to your pages.</span><span class="sxs-lookup"><span data-stu-id="cebe8-132">You may choose the web views manual integration if you want to precisely place the Reach UI within your pages or if you don't want to add another inheritance level to your pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="cebe8-133">Overlay integration</span><span class="sxs-lookup"><span data-stu-id="cebe8-133">Overlay integration</span></span>
<span data-ttu-id="cebe8-134">The Engagement overlay dynamically adds the UI elements used to display Reach campaigns in your page.</span><span class="sxs-lookup"><span data-stu-id="cebe8-134">The Engagement overlay dynamically adds the UI elements used to display Reach campaigns in your page.</span></span> <span data-ttu-id="cebe8-135">If the overlay doesn't suit your layout you should consider the web views manual integration instead.</span><span class="sxs-lookup"><span data-stu-id="cebe8-135">If the overlay doesn't suit your layout you should consider the web views manual integration instead.</span></span>

<span data-ttu-id="cebe8-136">In your .xaml file change `EngagementPage` reference to `EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="cebe8-136">In your .xaml file change `EngagementPage` reference to `EngagementPageOverlay`</span></span>

* <span data-ttu-id="cebe8-137">Add to your namespaces declarations:</span><span class="sxs-lookup"><span data-stu-id="cebe8-137">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="cebe8-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="cebe8-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="cebe8-139">**With EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="cebe8-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="cebe8-140">**With EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="cebe8-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="cebe8-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="cebe8-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="cebe8-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="cebe8-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="cebe8-143">**With EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="cebe8-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="cebe8-144">**With EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="cebe8-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="cebe8-145">The Engagement overlay adds a `Grid` element on top of your page composed of your layout and the two `WebView` elements one for the banner and the other one for the interstitial view.</span><span class="sxs-lookup"><span data-stu-id="cebe8-145">The Engagement overlay adds a `Grid` element on top of your page composed of your layout and the two `WebView` elements one for the banner and the other one for the interstitial view.</span></span>

<span data-ttu-id="cebe8-146">You can customize the overlay elements directly in the `EngagementPageOverlay.cs` file.</span><span class="sxs-lookup"><span data-stu-id="cebe8-146">You can customize the overlay elements directly in the `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="cebe8-147">Web views manual integration</span><span class="sxs-lookup"><span data-stu-id="cebe8-147">Web views manual integration</span></span>
<span data-ttu-id="cebe8-148">Reach will be searching your pages for the two `WebView` elements responsible for displaying the banner and the interstitial view.</span><span class="sxs-lookup"><span data-stu-id="cebe8-148">Reach will be searching your pages for the two `WebView` elements responsible for displaying the banner and the interstitial view.</span></span> <span data-ttu-id="cebe8-149">The only thing you have to do is to add those two `WebView` elements somewhere in your pages, here is an example:</span><span class="sxs-lookup"><span data-stu-id="cebe8-149">The only thing you have to do is to add those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="cebe8-150">In this example the `WebView` elements are stretched to fit their container which automatically re-sizes them in case of screen rotation or window size change.</span><span class="sxs-lookup"><span data-stu-id="cebe8-150">In this example the `WebView` elements are stretched to fit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="cebe8-151">It is important to keep the same naming `engagement_notification_content` and `engagement_announcement_content` for the `WebView` elements.</span><span class="sxs-lookup"><span data-stu-id="cebe8-151">It is important to keep the same naming `engagement_notification_content` and `engagement_announcement_content` for the `WebView` elements.</span></span> <span data-ttu-id="cebe8-152">Reach is identifying them by their name.</span><span class="sxs-lookup"><span data-stu-id="cebe8-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="cebe8-153">Handle datapush (optional)</span><span class="sxs-lookup"><span data-stu-id="cebe8-153">Handle datapush (optional)</span></span>
<span data-ttu-id="cebe8-154">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span><span class="sxs-lookup"><span data-stu-id="cebe8-154">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

<span data-ttu-id="cebe8-155">In App.xaml.cs in the App() constructor add:</span><span class="sxs-lookup"><span data-stu-id="cebe8-155">In App.xaml.cs in the App() constructor add:</span></span>

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

<span data-ttu-id="cebe8-156">You can see that the callback of each method returns a boolean.</span><span class="sxs-lookup"><span data-stu-id="cebe8-156">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="cebe8-157">Engagement sends a feedback to its back-end after dispatching the data push.</span><span class="sxs-lookup"><span data-stu-id="cebe8-157">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="cebe8-158">If the callback returns false, the `exit` feedback will be send.</span><span class="sxs-lookup"><span data-stu-id="cebe8-158">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="cebe8-159">Otherwise, it will be `action`.</span><span class="sxs-lookup"><span data-stu-id="cebe8-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="cebe8-160">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span><span class="sxs-lookup"><span data-stu-id="cebe8-160">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="cebe8-161">Engagement is not able to receive multiples feedbacks for a data push.</span><span class="sxs-lookup"><span data-stu-id="cebe8-161">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="cebe8-162">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span><span class="sxs-lookup"><span data-stu-id="cebe8-162">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="cebe8-163">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span><span class="sxs-lookup"><span data-stu-id="cebe8-163">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="cebe8-164">Customize UI (optional)</span><span class="sxs-lookup"><span data-stu-id="cebe8-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="cebe8-165">First step</span><span class="sxs-lookup"><span data-stu-id="cebe8-165">First step</span></span>
<span data-ttu-id="cebe8-166">We allow you to customize the reach UI.</span><span class="sxs-lookup"><span data-stu-id="cebe8-166">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="cebe8-167">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span><span class="sxs-lookup"><span data-stu-id="cebe8-167">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="cebe8-168">**Sample Code :**</span><span class="sxs-lookup"><span data-stu-id="cebe8-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="cebe8-169">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `App()` method.</span><span class="sxs-lookup"><span data-stu-id="cebe8-169">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `App()` method.</span></span>

<span data-ttu-id="cebe8-170">**Sample Code :**</span><span class="sxs-lookup"><span data-stu-id="cebe8-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="cebe8-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="cebe8-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="cebe8-172">You don't have to create your own, and if you do so, you don't have to override every method.</span><span class="sxs-lookup"><span data-stu-id="cebe8-172">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="cebe8-173">The default behavior is to select the Engagement base object.</span><span class="sxs-lookup"><span data-stu-id="cebe8-173">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="cebe8-174">Web View</span><span class="sxs-lookup"><span data-stu-id="cebe8-174">Web View</span></span>
<span data-ttu-id="cebe8-175">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span><span class="sxs-lookup"><span data-stu-id="cebe8-175">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="cebe8-176">To provide a full customization possibilities we only use web view.</span><span class="sxs-lookup"><span data-stu-id="cebe8-176">To provide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="cebe8-177">If you want to customize layouts, override directly the resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="cebe8-177">If you want to customize layouts, override directly the resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="cebe8-178">Engagement needs all code in `<body></body>` to run correctly.</span><span class="sxs-lookup"><span data-stu-id="cebe8-178">Engagement needs all code in `<body></body>` to run correctly.</span></span> <span data-ttu-id="cebe8-179">But you can add tag outer `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="cebe8-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="cebe8-180">However, you can decide to use your own resources.</span><span class="sxs-lookup"><span data-stu-id="cebe8-180">However, you can decide to use your own resources.</span></span>

<span data-ttu-id="cebe8-181">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts, but take care to embedded the engagement mechanism:</span><span class="sxs-lookup"><span data-stu-id="cebe8-181">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts, but take care to embedded the engagement mechanism:</span></span>

<span data-ttu-id="cebe8-182">**Sample Code :**</span><span class="sxs-lookup"><span data-stu-id="cebe8-182">**Sample Code :**</span></span>

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


<span data-ttu-id="cebe8-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="cebe8-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="cebe8-184">It represents the html file that design the content of a push message (Text announcement, Web anoucement and Poll announcement).</span><span class="sxs-lookup"><span data-stu-id="cebe8-184">It represents the html file that design the content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="cebe8-185">AnnouncementName is `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="cebe8-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="cebe8-186">It is the name of the webview design in your xaml page.</span><span class="sxs-lookup"><span data-stu-id="cebe8-186">It is the name of the webview design in your xaml page.</span></span>

<span data-ttu-id="cebe8-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="cebe8-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="cebe8-188">It represents the html file that design the notification of a push message.</span><span class="sxs-lookup"><span data-stu-id="cebe8-188">It represents the html file that design the notification of a push message.</span></span> <span data-ttu-id="cebe8-189">NotfificationName is `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="cebe8-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="cebe8-190">It is the name of the webview design in your xaml page.</span><span class="sxs-lookup"><span data-stu-id="cebe8-190">It is the name of the webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="cebe8-191">Customization</span><span class="sxs-lookup"><span data-stu-id="cebe8-191">Customization</span></span>
<span data-ttu-id="cebe8-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span><span class="sxs-lookup"><span data-stu-id="cebe8-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="cebe8-193">Take care that webview object is described three times - the first time in your xaml, second time in your .cs file in the "setwebview()" method, and third time in the html file.</span><span class="sxs-lookup"><span data-stu-id="cebe8-193">Take care that webview object is described three times - the first time in your xaml, second time in your .cs file in the "setwebview()" method, and third time in the html file.</span></span>

* <span data-ttu-id="cebe8-194">In your xaml you describe the current graphical layout webview component.</span><span class="sxs-lookup"><span data-stu-id="cebe8-194">In your xaml you describe the current graphical layout webview component.</span></span>
* <span data-ttu-id="cebe8-195">In your .cs file you can define "setwebview()" in which you set the dimension of the two webview (notification, announcement).</span><span class="sxs-lookup"><span data-stu-id="cebe8-195">In your .cs file you can define "setwebview()" in which you set the dimension of the two webview (notification, announcement).</span></span> <span data-ttu-id="cebe8-196">It is very effective when the application is resizing.</span><span class="sxs-lookup"><span data-stu-id="cebe8-196">It is very effective when the application is resizing.</span></span>
* <span data-ttu-id="cebe8-197">In the Engagement html file we describe the webview content, design and the elements positions between each other.</span><span class="sxs-lookup"><span data-stu-id="cebe8-197">In the Engagement html file we describe the webview content, design and the elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="cebe8-198">Launch message</span><span class="sxs-lookup"><span data-stu-id="cebe8-198">Launch message</span></span>
<span data-ttu-id="cebe8-199">When a user clicks on a system notification (a toast), Engagement launches the application, load the content of the push messages, and display the page for the corresponding campaign.</span><span class="sxs-lookup"><span data-stu-id="cebe8-199">When a user clicks on a system notification (a toast), Engagement launches the application, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="cebe8-200">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span><span class="sxs-lookup"><span data-stu-id="cebe8-200">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="cebe8-201">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span><span class="sxs-lookup"><span data-stu-id="cebe8-201">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="cebe8-202">Engagement cannot handle that itself, but provides a few handlers for you.</span><span class="sxs-lookup"><span data-stu-id="cebe8-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="cebe8-203">To implement the callback, in App.xaml.cs in "Public App(){}" add:</span><span class="sxs-lookup"><span data-stu-id="cebe8-203">To implement the callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* The application has launched and the content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* The application has finished loading the content and the page
             * is about to be displayed.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* The content has been loaded, but an error has occurred.
             * You can provide an information to the user.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="cebe8-204">You can set the callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span><span class="sxs-lookup"><span data-stu-id="cebe8-204">You can set the callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="cebe8-205">Each handler is called by the UI Thread.</span><span class="sxs-lookup"><span data-stu-id="cebe8-205">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="cebe8-206">You do not have to worry when using a MessageBox or something UI-related.</span><span class="sxs-lookup"><span data-stu-id="cebe8-206">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <a id="push-channel-sharing"></a> <span data-ttu-id="cebe8-207">Push channel sharing</span><span class="sxs-lookup"><span data-stu-id="cebe8-207">Push channel sharing</span></span>
<span data-ttu-id="cebe8-208">If you are using push notifications for another purpose in your application then you have to use the push channel sharing feature of the Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="cebe8-208">If you are using push notifications for another purpose in your application then you have to use the push channel sharing feature of the Engagement SDK.</span></span> <span data-ttu-id="cebe8-209">This is to avoid missed push.</span><span class="sxs-lookup"><span data-stu-id="cebe8-209">This is to avoid missed push.</span></span>

* <span data-ttu-id="cebe8-210">You can provide your own push channel to the Engagement Reach initialization.</span><span class="sxs-lookup"><span data-stu-id="cebe8-210">You can provide your own push channel to the Engagement Reach initialization.</span></span> <span data-ttu-id="cebe8-211">The SDK will use it instead of requesting a new one.</span><span class="sxs-lookup"><span data-stu-id="cebe8-211">The SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="cebe8-212">Update the Engagement Reach initialization with your push channel in the `InitEngagement` method from the `App.xaml.cs` file:</span><span class="sxs-lookup"><span data-stu-id="cebe8-212">Update the Engagement Reach initialization with your push channel in the `InitEngagement` method from the `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="cebe8-213">Alternatively, if you just want to consume the push channel after the Reach initialization then you can set a callback on Engagement Reach to get the push channel once it is created by the SDK.</span><span class="sxs-lookup"><span data-stu-id="cebe8-213">Alternatively, if you just want to consume the push channel after the Reach initialization then you can set a callback on Engagement Reach to get the push channel once it is created by the SDK.</span></span>

<span data-ttu-id="cebe8-214">Set your callback at any place **after** the Reach initialization :</span><span class="sxs-lookup"><span data-stu-id="cebe8-214">Set your callback at any place **after** the Reach initialization :</span></span>

    /* Set action on the SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* The forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="cebe8-215">Custom scheme tip</span><span class="sxs-lookup"><span data-stu-id="cebe8-215">Custom scheme tip</span></span>
<span data-ttu-id="cebe8-216">We provide custom scheme use.</span><span class="sxs-lookup"><span data-stu-id="cebe8-216">We provide custom scheme use.</span></span> <span data-ttu-id="cebe8-217">You can send different type of URI from engagement frontend to be used in your engagement application.</span><span class="sxs-lookup"><span data-stu-id="cebe8-217">You can send different type of URI from engagement frontend to be used in your engagement application.</span></span> <span data-ttu-id="cebe8-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span><span class="sxs-lookup"><span data-stu-id="cebe8-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="cebe8-219">You can also create your own custom scheme for your application.</span><span class="sxs-lookup"><span data-stu-id="cebe8-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="cebe8-220">The simple way to set a custom scheme in your application is to open your `Package.appxmanifest` go in `Declarations` panel.</span><span class="sxs-lookup"><span data-stu-id="cebe8-220">The simple way to set a custom scheme in your application is to open your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="cebe8-221">Select `Protocol` in the Available Declarations scroll box and add it.</span><span class="sxs-lookup"><span data-stu-id="cebe8-221">Select `Protocol` in the Available Declarations scroll box and add it.</span></span> <span data-ttu-id="cebe8-222">Edit the `Name` field with your new protocol desired name.</span><span class="sxs-lookup"><span data-stu-id="cebe8-222">Edit the `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="cebe8-223">Now to use this protocol, edit your `App.xaml.cs` with the `OnActivated` method, and don't forget to initialize engagement here also:</span><span class="sxs-lookup"><span data-stu-id="cebe8-223">Now to use this protocol, edit your `App.xaml.cs` with the `OnActivated` method, and don't forget to initialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action to do when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

