---
title: Windows Universal Apps SDK Upgrade Procedures
description: Windows Universal Apps SDK Upgrade Procedures for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: fe85a99a92fb39082cafe7422b356de1f20f14bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549825"
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="ecfbf-103">Windows Universal Apps SDK Upgrade Procedures</span><span class="sxs-lookup"><span data-stu-id="ecfbf-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="ecfbf-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="ecfbf-105">You may have to follow several procedures if you missed several versions of the SDK.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="ecfbf-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-330-to-340"></a><span data-ttu-id="ecfbf-107">From 3.3.0 to 3.4.0</span><span class="sxs-lookup"><span data-stu-id="ecfbf-107">From 3.3.0 to 3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="ecfbf-108">Test logs</span><span class="sxs-lookup"><span data-stu-id="ecfbf-108">Test logs</span></span>
<span data-ttu-id="ecfbf-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="ecfbf-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="ecfbf-111">Resources</span><span class="sxs-lookup"><span data-stu-id="ecfbf-111">Resources</span></span>
<span data-ttu-id="ecfbf-112">The Reach overlay has been improved.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-112">The Reach overlay has been improved.</span></span> <span data-ttu-id="ecfbf-113">It is part of the SDK NuGet package resources.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-113">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="ecfbf-114">While upgrading to the new version of the SDK you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-114">While upgrading to the new version of the SDK you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="ecfbf-115">If the previous overlay is working for you or you are integrating the `WebView` elements manually then you can decide to keep your exiting files, it will still work.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-115">If the previous overlay is working for you or you are integrating the `WebView` elements manually then you can decide to keep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="ecfbf-116">If you want to update to the new overlay, just replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="ecfbf-116">If you want to update to the new overlay, just replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="ecfbf-117">Using the new overlay will overwrite any customizations made on the previous version.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-117">Using the new overlay will overwrite any customizations made on the previous version.</span></span>
> 
> 

## <a name="from-320-to-330"></a><span data-ttu-id="ecfbf-118">From 3.2.0 to 3.3.0</span><span class="sxs-lookup"><span data-stu-id="ecfbf-118">From 3.2.0 to 3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="ecfbf-119">Resources</span><span class="sxs-lookup"><span data-stu-id="ecfbf-119">Resources</span></span>
<span data-ttu-id="ecfbf-120">This step concerns customized resources only.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-120">This step concerns customized resources only.</span></span> <span data-ttu-id="ecfbf-121">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-121">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-to-320"></a><span data-ttu-id="ecfbf-122">From 3.1.0 to 3.2.0</span><span class="sxs-lookup"><span data-stu-id="ecfbf-122">From 3.1.0 to 3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="ecfbf-123">Resources</span><span class="sxs-lookup"><span data-stu-id="ecfbf-123">Resources</span></span>
<span data-ttu-id="ecfbf-124">This step concerns customized resources only.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-124">This step concerns customized resources only.</span></span> <span data-ttu-id="ecfbf-125">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-125">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="ecfbf-126">Webview integration</span><span class="sxs-lookup"><span data-stu-id="ecfbf-126">Webview integration</span></span>
<span data-ttu-id="ecfbf-127">Some improvements to match different device form factors were introduced in this version.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-127">Some improvements to match different device form factors were introduced in this version.</span></span> <span data-ttu-id="ecfbf-128">Make sure that your integration of the webview match the following:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-128">Make sure that your integration of the webview match the following:</span></span>

<span data-ttu-id="ecfbf-129">In your XAML page ():</span><span class="sxs-lookup"><span data-stu-id="ecfbf-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="ecfbf-130">And in your associated .cs file:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated to within a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

              #region to implement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update the webview when the app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update the webview when the app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure to detach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are the current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements to the correct size.
              /// </summary>
              /// <param name="width">The width of your current display.</param>
              /// <param name="height">The height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes the Windows.Current.SizeChanged and indicates that webviews have to be resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes the ApplicationView.VisibleBoundsChanged and indicates that webviews have to be resized
              /// </summary>
              /// <param name="sender">The related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-to-300"></a><span data-ttu-id="ecfbf-131">From 2.0.0 to 3.0.0</span><span class="sxs-lookup"><span data-stu-id="ecfbf-131">From 2.0.0 to 3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="ecfbf-132">Resources</span><span class="sxs-lookup"><span data-stu-id="ecfbf-132">Resources</span></span>
<span data-ttu-id="ecfbf-133">This step concerns customized resources only.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-133">This step concerns customized resources only.</span></span> <span data-ttu-id="ecfbf-134">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-134">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-to-200"></a><span data-ttu-id="ecfbf-135">From 1.1.1 to 2.0.0</span><span class="sxs-lookup"><span data-stu-id="ecfbf-135">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="ecfbf-136">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-136">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ecfbf-137">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-137">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="ecfbf-138">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span><span class="sxs-lookup"><span data-stu-id="ecfbf-138">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="ecfbf-139">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span><span class="sxs-lookup"><span data-stu-id="ecfbf-139">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="ecfbf-140">Nuget package</span><span class="sxs-lookup"><span data-stu-id="ecfbf-140">Nuget package</span></span>
<span data-ttu-id="ecfbf-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="ecfbf-142">Applying Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ecfbf-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="ecfbf-143">The SDK uses the term `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-143">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="ecfbf-144">You need to update your project to match this change.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-144">You need to update your project to match this change.</span></span>

<span data-ttu-id="ecfbf-145">You need to uninstall your current Capptain nuget package.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-145">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="ecfbf-146">Consider that all your changes in Capptain Resources folder will be removed.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="ecfbf-147">If you want to keep those files then make a copy of them.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-147">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="ecfbf-148">After that, install the new Microsoft Azure Engagement nuget package on your project.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-148">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="ecfbf-149">You can find it directly on [nuget website].</span><span class="sxs-lookup"><span data-stu-id="ecfbf-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="ecfbf-150">or here index.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-150">or here index.</span></span> <span data-ttu-id="ecfbf-151">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-151">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="ecfbf-152">You have to clean your project references by deleting Capptain DLL references.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-152">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="ecfbf-153">If you do not make this, the version of Capptain will conflict and errors will happen.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-153">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="ecfbf-154">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-154">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="ecfbf-155">Please note that both xaml and cs files have to be updated.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-155">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="ecfbf-156">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-156">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="ecfbf-157">All Capptain namespaces have to be updated.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-157">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="ecfbf-158">Before migration:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="ecfbf-159">After migration:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="ecfbf-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span><span class="sxs-lookup"><span data-stu-id="ecfbf-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="ecfbf-161">Before migration:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="ecfbf-162">After migration:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="ecfbf-163">For xaml files Capptain namespace and attributes also change.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="ecfbf-164">Before migration:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="ecfbf-165">After migration:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="ecfbf-166">Overlay page changes</span><span class="sxs-lookup"><span data-stu-id="ecfbf-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ecfbf-167">Overlay also changes.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-167">Overlay also changes.</span></span> <span data-ttu-id="ecfbf-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="ecfbf-169">It has to be used in both xaml and cs files.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-169">It has to be used in both xaml and cs files.</span></span> <span data-ttu-id="ecfbf-170">Moreover `CapptainGrid` is to be named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-170">Moreover `CapptainGrid` is to be named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="ecfbf-171">For overlay :</span><span class="sxs-lookup"><span data-stu-id="ecfbf-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="ecfbf-172">It becomes :</span><span class="sxs-lookup"><span data-stu-id="ecfbf-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="ecfbf-173">For the other resources like Capptain pictures and HTML files, please note that they also have been renamed to use "Engagement".</span><span class="sxs-lookup"><span data-stu-id="ecfbf-173">For the other resources like Capptain pictures and HTML files, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="ecfbf-174">Project declaration</span><span class="sxs-lookup"><span data-stu-id="ecfbf-174">Project declaration</span></span>
<span data-ttu-id="ecfbf-175">On Package.appxmanifest `File Type Associations` has been updated from :</span><span class="sxs-lookup"><span data-stu-id="ecfbf-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="ecfbf-176">capptain\_reach\_content to engagement\_reach\_content</span><span class="sxs-lookup"><span data-stu-id="ecfbf-176">capptain\_reach\_content to engagement\_reach\_content</span></span>
* <span data-ttu-id="ecfbf-177">capptain\_log\_file to engagement\_log\_file</span><span class="sxs-lookup"><span data-stu-id="ecfbf-177">capptain\_log\_file to engagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="ecfbf-178">Application ID / SDK Key</span><span class="sxs-lookup"><span data-stu-id="ecfbf-178">Application ID / SDK Key</span></span>
<span data-ttu-id="ecfbf-179">Engagement uses a connection string.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-179">Engagement uses a connection string.</span></span> <span data-ttu-id="ecfbf-180">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-180">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="ecfbf-181">You can set it up on your EngagementConfiguration file.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="ecfbf-182">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-182">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="ecfbf-183">Edit this file to specify:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-183">Edit this file to specify:</span></span>

* <span data-ttu-id="ecfbf-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="ecfbf-185">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span><span class="sxs-lookup"><span data-stu-id="ecfbf-185">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="ecfbf-186">The connection string for your application is displayed on the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-186">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="ecfbf-187">Items name change</span><span class="sxs-lookup"><span data-stu-id="ecfbf-187">Items name change</span></span>
<span data-ttu-id="ecfbf-188">All items named *capptain* have been named *engagement*.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="ecfbf-189">Similarly for *Capptain* to *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-189">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="ecfbf-190">Examples of commonly used Capptain items :</span><span class="sxs-lookup"><span data-stu-id="ecfbf-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="ecfbf-191">CapptainConfiguration now named EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="ecfbf-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="ecfbf-192">CapptainAgent now named EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="ecfbf-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="ecfbf-193">CapptainReach now named EngagementReach</span><span class="sxs-lookup"><span data-stu-id="ecfbf-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="ecfbf-194">CapptainHttpConfig now named EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="ecfbf-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="ecfbf-195">GetCapptainPageName now named GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="ecfbf-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="ecfbf-196">Note that rename also affects overridden methods.</span><span class="sxs-lookup"><span data-stu-id="ecfbf-196">Note that rename also affects overridden methods.</span></span>

