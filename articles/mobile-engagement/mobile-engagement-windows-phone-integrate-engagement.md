---
title: Windows Phone Silverlight Engagement SDK Integration
description: How to Integrate Azure Mobile Engagement with Windows Phone Silverlight Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 29b18aecff783cebf617995e2a19f16f0b68b51b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555250"
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="98739-103">Windows Phone Silverlight Engagement SDK Integration</span><span class="sxs-lookup"><span data-stu-id="98739-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="98739-108">This procedure describes the simplest way to activate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span><span class="sxs-lookup"><span data-stu-id="98739-108">This procedure describes the simplest way to activate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="98739-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span><span class="sxs-lookup"><span data-stu-id="98739-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="98739-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span><span class="sxs-lookup"><span data-stu-id="98739-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="98739-111">Supported versions</span><span class="sxs-lookup"><span data-stu-id="98739-111">Supported versions</span></span>
<span data-ttu-id="98739-112">The Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span><span class="sxs-lookup"><span data-stu-id="98739-112">The Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="98739-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="98739-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="98739-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="98739-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> If you are targeting Windows Phone 8.1 (non-Silverlight) then refer to the [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).
> 
> 

## <a name="install-the-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="98739-116">Install the Mobile Engagement Silverlight SDK</span><span class="sxs-lookup"><span data-stu-id="98739-116">Install the Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="98739-117">The Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="98739-117">The Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="98739-118">You can install it from the Visual Studio Nuget Package Manager.</span><span class="sxs-lookup"><span data-stu-id="98739-118">You can install it from the Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-the-capabilities"></a><span data-ttu-id="98739-119">Add the capabilities</span><span class="sxs-lookup"><span data-stu-id="98739-119">Add the capabilities</span></span>
<span data-ttu-id="98739-120">The Engagement SDK needs some capabilities of the Windows Phone Silverlight SDK in order to work properly.</span><span class="sxs-lookup"><span data-stu-id="98739-120">The Engagement SDK needs some capabilities of the Windows Phone Silverlight SDK in order to work properly.</span></span>

<span data-ttu-id="98739-121">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared in the `Capabilities` panel:</span><span class="sxs-lookup"><span data-stu-id="98739-121">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared in the `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="98739-122">Initialize the Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="98739-122">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="98739-123">Engagement configuration</span><span class="sxs-lookup"><span data-stu-id="98739-123">Engagement configuration</span></span>
<span data-ttu-id="98739-124">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span><span class="sxs-lookup"><span data-stu-id="98739-124">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="98739-125">Edit this file to specify :</span><span class="sxs-lookup"><span data-stu-id="98739-125">Edit this file to specify :</span></span>

* <span data-ttu-id="98739-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="98739-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="98739-127">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span><span class="sxs-lookup"><span data-stu-id="98739-127">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="98739-128">The connection string for your application is displayed on the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="98739-128">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="98739-129">Engagement initialization</span><span class="sxs-lookup"><span data-stu-id="98739-129">Engagement initialization</span></span>
<span data-ttu-id="98739-130">When you create a new project, a `App.xaml.cs` file is generated.</span><span class="sxs-lookup"><span data-stu-id="98739-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="98739-131">This class inherits from `Application` and contains many important methods.</span><span class="sxs-lookup"><span data-stu-id="98739-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="98739-132">It will also be used to initialize the Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="98739-132">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="98739-133">Modify the `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="98739-133">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="98739-134">Add to your `using` statements :</span><span class="sxs-lookup"><span data-stu-id="98739-134">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="98739-135">Insert `EngagementAgent.Instance.Init` in the `Application_Launching` method :</span><span class="sxs-lookup"><span data-stu-id="98739-135">Insert `EngagementAgent.Instance.Init` in the `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="98739-136">Insert `EngagementAgent.Instance.OnActivated` in the `Application_Activated` method :</span><span class="sxs-lookup"><span data-stu-id="98739-136">Insert `EngagementAgent.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> We strongly discourage you to add the Engagement initialization in another place of your application. However, be aware that the `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on the UI thread.
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="98739-139">Basic reporting</span><span class="sxs-lookup"><span data-stu-id="98739-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="98739-140">Recommended method : overload your `PhoneApplicationPage` classes</span><span class="sxs-lookup"><span data-stu-id="98739-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="98739-141">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` classes.</span><span class="sxs-lookup"><span data-stu-id="98739-141">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="98739-142">Here is an example of how to do this for a page of your application.</span><span class="sxs-lookup"><span data-stu-id="98739-142">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="98739-143">You can do the same thing for all pages of your application.</span><span class="sxs-lookup"><span data-stu-id="98739-143">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="98739-144">C# Source file</span><span class="sxs-lookup"><span data-stu-id="98739-144">C# Source file</span></span>
<span data-ttu-id="98739-145">Modify your page `.xaml.cs` file :</span><span class="sxs-lookup"><span data-stu-id="98739-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="98739-146">Add to your `using` statements :</span><span class="sxs-lookup"><span data-stu-id="98739-146">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="98739-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="98739-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="98739-148">**Without Engagement:**</span><span class="sxs-lookup"><span data-stu-id="98739-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="98739-149">**With Engagement:**</span><span class="sxs-lookup"><span data-stu-id="98739-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> If your page inherits from the `OnNavigatedTo` method, be careful to let the `base.OnNavigatedTo(e)` call. Otherwise, the activity will not be reported. Indeed, the `EngagementPage` is calling `StartActivity` inside the `OnNavigatedTo` method.
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="98739-153">XAML file</span><span class="sxs-lookup"><span data-stu-id="98739-153">XAML file</span></span>
<span data-ttu-id="98739-154">Modify your page `.xaml` file :</span><span class="sxs-lookup"><span data-stu-id="98739-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="98739-155">Add to your namespaces declarations :</span><span class="sxs-lookup"><span data-stu-id="98739-155">Add to your namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="98739-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="98739-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="98739-157">**Without Engagement:**</span><span class="sxs-lookup"><span data-stu-id="98739-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="98739-158">**With Engagement:**</span><span class="sxs-lookup"><span data-stu-id="98739-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-the-default-behavior"></a><span data-ttu-id="98739-159">Override the default behavior</span><span class="sxs-lookup"><span data-stu-id="98739-159">Override the default behavior</span></span>
<span data-ttu-id="98739-160">By default, the class name of the page is reported as the activity name, with no extra.</span><span class="sxs-lookup"><span data-stu-id="98739-160">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="98739-161">If the class uses the "Page" suffix, Engagement will also remove it.</span><span class="sxs-lookup"><span data-stu-id="98739-161">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="98739-162">If you want to override the default behavior for the name, simply add this to your code:</span><span class="sxs-lookup"><span data-stu-id="98739-162">If you want to override the default behavior for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="98739-163">If you want to report some extra information with your activity, you can add this to your code:</span><span class="sxs-lookup"><span data-stu-id="98739-163">If you want to report some extra information with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="98739-164">These methods are called from within the `OnNavigatedTo` method of your page.</span><span class="sxs-lookup"><span data-stu-id="98739-164">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="98739-165">Alternate method: call `StartActivity()` manually</span><span class="sxs-lookup"><span data-stu-id="98739-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="98739-166">If you cannot or do not want to overload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span><span class="sxs-lookup"><span data-stu-id="98739-166">If you cannot or do not want to overload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="98739-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="98739-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> Ensure you end your session correctly.
> 
> The SDK automatically calls the `EndActivity` method when the application is closed. Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method. This method sends a message to the Engagement server that the current user has left the application and this impacts all application logs.
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="98739-172">Advanced reporting</span><span class="sxs-lookup"><span data-stu-id="98739-172">Advanced reporting</span></span>
<span data-ttu-id="98739-173">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span><span class="sxs-lookup"><span data-stu-id="98739-173">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="98739-174">The Engagement API allows to use all of Engagement's advanced capabilities.</span><span class="sxs-lookup"><span data-stu-id="98739-174">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="98739-175">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="98739-175">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="98739-176">Advanced configuration</span><span class="sxs-lookup"><span data-stu-id="98739-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="98739-177">Disable automatic crash reporting</span><span class="sxs-lookup"><span data-stu-id="98739-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="98739-178">You can disable the automatic crash reporting feature of Engagement.</span><span class="sxs-lookup"><span data-stu-id="98739-178">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="98739-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span><span class="sxs-lookup"><span data-stu-id="98739-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** it will not close the session and jobs.
> 
> 

<span data-ttu-id="98739-181">To disable automatic crash reporting, just customize your configuration depending on the way you declared it :</span><span class="sxs-lookup"><span data-stu-id="98739-181">To disable automatic crash reporting, just customize your configuration depending on the way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="98739-182">From `EngagementConfiguration.xml` file</span><span class="sxs-lookup"><span data-stu-id="98739-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="98739-183">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span><span class="sxs-lookup"><span data-stu-id="98739-183">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="98739-184">From `EngagementConfiguration` object at run time</span><span class="sxs-lookup"><span data-stu-id="98739-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="98739-185">Set report crash to false using your EngagementConfiguration object.</span><span class="sxs-lookup"><span data-stu-id="98739-185">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="98739-186">Burst mode</span><span class="sxs-lookup"><span data-stu-id="98739-186">Burst mode</span></span>
<span data-ttu-id="98739-187">By default, the Engagement service reports logs in real time.</span><span class="sxs-lookup"><span data-stu-id="98739-187">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="98739-188">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span><span class="sxs-lookup"><span data-stu-id="98739-188">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="98739-189">To do so, call the method:</span><span class="sxs-lookup"><span data-stu-id="98739-189">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="98739-190">The argument is a value in **milliseconds**.</span><span class="sxs-lookup"><span data-stu-id="98739-190">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="98739-191">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span><span class="sxs-lookup"><span data-stu-id="98739-191">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="98739-192">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span><span class="sxs-lookup"><span data-stu-id="98739-192">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="98739-193">It is recommended to use a burst threshold no longer than 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="98739-193">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="98739-194">You have to be aware that saved logs are limited to 300 items.</span><span class="sxs-lookup"><span data-stu-id="98739-194">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="98739-195">If sending is too long you can lose some logs.</span><span class="sxs-lookup"><span data-stu-id="98739-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> The burst threshold cannot be configured to a period lesser than one second. If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, that is, zero seconds. This will trigger the SDK to report the logs in real-time.
> 
> 

