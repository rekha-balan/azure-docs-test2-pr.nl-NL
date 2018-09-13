---
title: Windows Universal Apps Engagement SDK Integration
description: How to Integrate Azure Mobile Engagement with Windows Universal Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 898160814304fa8ec65622056a77ca9d4caf2c99
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564537"
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="76926-103">Windows Universal Apps Engagement SDK Integration</span><span class="sxs-lookup"><span data-stu-id="76926-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [Universal Windows](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="76926-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span><span class="sxs-lookup"><span data-stu-id="76926-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="76926-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span><span class="sxs-lookup"><span data-stu-id="76926-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="76926-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span><span class="sxs-lookup"><span data-stu-id="76926-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="76926-111">Supported versions</span><span class="sxs-lookup"><span data-stu-id="76926-111">Supported versions</span></span>
<span data-ttu-id="76926-112">The Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span><span class="sxs-lookup"><span data-stu-id="76926-112">The Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="76926-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="76926-113">Windows 8</span></span>
* <span data-ttu-id="76926-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="76926-114">Windows 8.1</span></span>
* <span data-ttu-id="76926-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="76926-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="76926-116">Windows 10 (desktop and mobile families)</span><span class="sxs-lookup"><span data-stu-id="76926-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> If you are targeting Windows Phone Silverlight then refer to the [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).
> 
> 

## <a name="install-the-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="76926-118">Install the Mobile Engagement Universal Apps SDK</span><span class="sxs-lookup"><span data-stu-id="76926-118">Install the Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="76926-119">All platforms</span><span class="sxs-lookup"><span data-stu-id="76926-119">All platforms</span></span>
<span data-ttu-id="76926-120">The Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="76926-120">The Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="76926-121">You can install it from the Visual Studio Nuget Package Manager.</span><span class="sxs-lookup"><span data-stu-id="76926-121">You can install it from the Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="76926-122">Windows 8.x and Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="76926-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="76926-123">NuGet automatically deploys the SDK resources in the `Resources` folder at the root of your application project.</span><span class="sxs-lookup"><span data-stu-id="76926-123">NuGet automatically deploys the SDK resources in the `Resources` folder at the root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="76926-124">Windows 10 Universal Windows Platform applications</span><span class="sxs-lookup"><span data-stu-id="76926-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="76926-125">NuGet does not automatically deploy the SDK resources in your UWP application yet.</span><span class="sxs-lookup"><span data-stu-id="76926-125">NuGet does not automatically deploy the SDK resources in your UWP application yet.</span></span> <span data-ttu-id="76926-126">You have to do it manually until resources deployment is reintroduced in NuGet:</span><span class="sxs-lookup"><span data-stu-id="76926-126">You have to do it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="76926-127">Open your File Explorer.</span><span class="sxs-lookup"><span data-stu-id="76926-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="76926-128">Navigate to the following location (**x.x.x** is the version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="76926-128">Navigate to the following location (**x.x.x** is the version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="76926-129">Drag and drop the **Resources** folder from the file explorer to the root of your project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="76926-129">Drag and drop the **Resources** folder from the file explorer to the root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="76926-130">In Visual Studio select your project and activate the **Show All files** icon on top of the **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="76926-130">In Visual Studio select your project and activate the **Show All files** icon on top of the **Solution Explorer**.</span></span>
5. <span data-ttu-id="76926-131">Some files are not included in the project.</span><span class="sxs-lookup"><span data-stu-id="76926-131">Some files are not included in the project.</span></span> <span data-ttu-id="76926-132">To import them at once right click on the **Resources** folder, **Exclude from project** then another right click on the **Resources** folder, **Include in project** to re-include the whole folder.</span><span class="sxs-lookup"><span data-stu-id="76926-132">To import them at once right click on the **Resources** folder, **Exclude from project** then another right click on the **Resources** folder, **Include in project** to re-include the whole folder.</span></span> <span data-ttu-id="76926-133">All files from the **Resources** folder are now included in your project.</span><span class="sxs-lookup"><span data-stu-id="76926-133">All files from the **Resources** folder are now included in your project.</span></span>

## <a name="add-the-capabilities"></a><span data-ttu-id="76926-134">Add the capabilities</span><span class="sxs-lookup"><span data-stu-id="76926-134">Add the capabilities</span></span>
<span data-ttu-id="76926-135">The Engagement SDK needs some capabilities of the Windows SDK in order to work properly.</span><span class="sxs-lookup"><span data-stu-id="76926-135">The Engagement SDK needs some capabilities of the Windows SDK in order to work properly.</span></span>

<span data-ttu-id="76926-136">Open your `Package.appxmanifest` file and be sure that the following capabilities are declared:</span><span class="sxs-lookup"><span data-stu-id="76926-136">Open your `Package.appxmanifest` file and be sure that the following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="76926-137">Initialize the Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="76926-137">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="76926-138">Engagement configuration</span><span class="sxs-lookup"><span data-stu-id="76926-138">Engagement configuration</span></span>
<span data-ttu-id="76926-139">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span><span class="sxs-lookup"><span data-stu-id="76926-139">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="76926-140">Edit this file to specify:</span><span class="sxs-lookup"><span data-stu-id="76926-140">Edit this file to specify:</span></span>

* <span data-ttu-id="76926-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="76926-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="76926-142">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span><span class="sxs-lookup"><span data-stu-id="76926-142">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="76926-143">The connection string for your application is displayed on the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="76926-143">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="76926-144">Engagement initialization</span><span class="sxs-lookup"><span data-stu-id="76926-144">Engagement initialization</span></span>
<span data-ttu-id="76926-145">When you create a new project, a `App.xaml.cs` file is generated.</span><span class="sxs-lookup"><span data-stu-id="76926-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="76926-146">This class inherits from `Application` and contains many important methods.</span><span class="sxs-lookup"><span data-stu-id="76926-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="76926-147">It will also be used to initialize the Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="76926-147">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="76926-148">Modify the `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="76926-148">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="76926-149">Add to your `using` statements:</span><span class="sxs-lookup"><span data-stu-id="76926-149">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="76926-150">Define a method to share the Engagement initialization once for all calls:</span><span class="sxs-lookup"><span data-stu-id="76926-150">Define a method to share the Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="76926-151">Call `InitEngagement` in the `OnLaunched` method:</span><span class="sxs-lookup"><span data-stu-id="76926-151">Call `InitEngagement` in the `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="76926-152">When your application is launched using a custom scheme, another application or the command line then the `OnActivated` method is called.</span><span class="sxs-lookup"><span data-stu-id="76926-152">When your application is launched using a custom scheme, another application or the command line then the `OnActivated` method is called.</span></span> <span data-ttu-id="76926-153">You also need to initiate the Engagement SDK when your app is activated.</span><span class="sxs-lookup"><span data-stu-id="76926-153">You also need to initiate the Engagement SDK when your app is activated.</span></span> <span data-ttu-id="76926-154">To do so, override `OnActivated` method:</span><span class="sxs-lookup"><span data-stu-id="76926-154">To do so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> We strongly discourage you to add the Engagement initialization in another place of your application.
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="76926-156">Basic reporting</span><span class="sxs-lookup"><span data-stu-id="76926-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="76926-157">Recommended method: overload your `Page` classes</span><span class="sxs-lookup"><span data-stu-id="76926-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="76926-158">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span><span class="sxs-lookup"><span data-stu-id="76926-158">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="76926-159">Here is an example of how to do this for a page of your application.</span><span class="sxs-lookup"><span data-stu-id="76926-159">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="76926-160">You can do the same thing for all pages of your application.</span><span class="sxs-lookup"><span data-stu-id="76926-160">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="76926-161">C# Source file</span><span class="sxs-lookup"><span data-stu-id="76926-161">C# Source file</span></span>
<span data-ttu-id="76926-162">Modify your page `.xaml.cs` file:</span><span class="sxs-lookup"><span data-stu-id="76926-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="76926-163">Add to your `using` statements:</span><span class="sxs-lookup"><span data-stu-id="76926-163">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="76926-164">Replace `Page` with `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="76926-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="76926-165">**Without Engagement:**</span><span class="sxs-lookup"><span data-stu-id="76926-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="76926-166">**With Engagement:**</span><span class="sxs-lookup"><span data-stu-id="76926-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`. Otherwise,  the activity will not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="76926-169">XAML file</span><span class="sxs-lookup"><span data-stu-id="76926-169">XAML file</span></span>
<span data-ttu-id="76926-170">Modify your page `.xaml` file:</span><span class="sxs-lookup"><span data-stu-id="76926-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="76926-171">Add to your namespaces declarations:</span><span class="sxs-lookup"><span data-stu-id="76926-171">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="76926-172">Replace `Page` with `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="76926-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="76926-173">**Without Engagement:**</span><span class="sxs-lookup"><span data-stu-id="76926-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="76926-174">**With Engagement:**</span><span class="sxs-lookup"><span data-stu-id="76926-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-the-default-behaviour"></a><span data-ttu-id="76926-175">Override the default behaviour</span><span class="sxs-lookup"><span data-stu-id="76926-175">Override the default behaviour</span></span>
<span data-ttu-id="76926-176">By default, the class name of the page is reported as the activity name, with no extra.</span><span class="sxs-lookup"><span data-stu-id="76926-176">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="76926-177">If the class uses the "Page" suffix, Engagement will also remove it.</span><span class="sxs-lookup"><span data-stu-id="76926-177">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="76926-178">If you want to override the default behaviour for the name, simply add this to your code:</span><span class="sxs-lookup"><span data-stu-id="76926-178">If you want to override the default behaviour for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="76926-179">If you want to report some extra informations with your activity, you can add this to your code:</span><span class="sxs-lookup"><span data-stu-id="76926-179">If you want to report some extra informations with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="76926-180">These methods are called from within the `OnNavigatedTo` method of your page.</span><span class="sxs-lookup"><span data-stu-id="76926-180">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="76926-181">Alternate method: call `StartActivity()` manually</span><span class="sxs-lookup"><span data-stu-id="76926-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="76926-182">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span><span class="sxs-lookup"><span data-stu-id="76926-182">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="76926-183">We recommend to call `StartActivity` inside your `OnNavigatedTo` method of your Page.</span><span class="sxs-lookup"><span data-stu-id="76926-183">We recommend to call `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Ensure you end your session correctly.
> 
> The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed. Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method, this method sends to Engagement server that current user has leave the application, this will impacts all application logs.
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="76926-187">Advanced reporting</span><span class="sxs-lookup"><span data-stu-id="76926-187">Advanced reporting</span></span>
<span data-ttu-id="76926-188">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span><span class="sxs-lookup"><span data-stu-id="76926-188">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="76926-189">The Engagement API allows to use all of Engagement's advanced capabilities.</span><span class="sxs-lookup"><span data-stu-id="76926-189">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="76926-190">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="76926-190">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="76926-191">Advanced configuration</span><span class="sxs-lookup"><span data-stu-id="76926-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="76926-192">Disable automatic crash reporting</span><span class="sxs-lookup"><span data-stu-id="76926-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="76926-193">You can disable the automatic crash reporting feature of Engagement.</span><span class="sxs-lookup"><span data-stu-id="76926-193">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="76926-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span><span class="sxs-lookup"><span data-stu-id="76926-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** will not close the session and jobs.
> 
> 

<span data-ttu-id="76926-196">To disable automatic crash reporting, just customize your configuration depending on the way you declared it:</span><span class="sxs-lookup"><span data-stu-id="76926-196">To disable automatic crash reporting, just customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="76926-197">From `EngagementConfiguration.xml` file</span><span class="sxs-lookup"><span data-stu-id="76926-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="76926-198">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span><span class="sxs-lookup"><span data-stu-id="76926-198">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="76926-199">From `EngagementConfiguration` object at run time</span><span class="sxs-lookup"><span data-stu-id="76926-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="76926-200">Set report crash to false using your EngagementConfiguration object.</span><span class="sxs-lookup"><span data-stu-id="76926-200">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="76926-201">Burst mode</span><span class="sxs-lookup"><span data-stu-id="76926-201">Burst mode</span></span>
<span data-ttu-id="76926-202">By default, the Engagement service reports logs in real time.</span><span class="sxs-lookup"><span data-stu-id="76926-202">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="76926-203">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span><span class="sxs-lookup"><span data-stu-id="76926-203">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="76926-204">To do so, call the method:</span><span class="sxs-lookup"><span data-stu-id="76926-204">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="76926-205">The argument is a value in **milliseconds**.</span><span class="sxs-lookup"><span data-stu-id="76926-205">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="76926-206">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span><span class="sxs-lookup"><span data-stu-id="76926-206">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="76926-207">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span><span class="sxs-lookup"><span data-stu-id="76926-207">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="76926-208">It is recommended to use a burst threshold no longer than 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="76926-208">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="76926-209">You have to be aware that saved logs are limited to 300 items.</span><span class="sxs-lookup"><span data-stu-id="76926-209">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="76926-210">If sending is too long you can lose some logs.</span><span class="sxs-lookup"><span data-stu-id="76926-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> The burst threshold cannot be configured to a period lesser than 1s. If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, i.e., 0s. This will trigger the SDK to report the logs in real-time.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

