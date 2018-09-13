---
title: Windows Universal Advanced Reporting with MobileApps Engagement
description: How to Integrate Azure Mobile Engagement with Windows Universal Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: feac309db1ffce0945012e293bfc1df417aed876
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553333"
---
# <a name="advanced-reporting-with-the-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="a3b69-103">Advanced Reporting with the Windows Universal Apps Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="a3b69-103">Advanced Reporting with the Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [Universal Windows](mobile-engagement-windows-store-advanced-reporting.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="a3b69-108">This topic describes additional reporting scenarios in your Windows Universal application.</span><span class="sxs-lookup"><span data-stu-id="a3b69-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="a3b69-109">These scenarios include options that you can choose to apply to the app created in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3b69-109">These scenarios include options that you can choose to apply to the app created in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3b69-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a3b69-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="a3b69-111">Before starting this tutorial, you must first complete the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span><span class="sxs-lookup"><span data-stu-id="a3b69-111">Before starting this tutorial, you must first complete the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="a3b69-112">This tutorial covers additional options you can choose from.</span><span class="sxs-lookup"><span data-stu-id="a3b69-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="a3b69-113">Specifying engagement configuration at runtime</span><span class="sxs-lookup"><span data-stu-id="a3b69-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="a3b69-114">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span><span class="sxs-lookup"><span data-stu-id="a3b69-114">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="a3b69-115">But you can also specify it at runtime: you can call the following method before the Engagement agent initialization:</span><span class="sxs-lookup"><span data-stu-id="a3b69-115">But you can also specify it at runtime: you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="a3b69-116">Recommended method: overload your `Page` classes</span><span class="sxs-lookup"><span data-stu-id="a3b69-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="a3b69-117">To activate the reporting of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span><span class="sxs-lookup"><span data-stu-id="a3b69-117">To activate the reporting of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="a3b69-118">Here is an example for a page of your application.</span><span class="sxs-lookup"><span data-stu-id="a3b69-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="a3b69-119">You can do the same thing for all pages of your application.</span><span class="sxs-lookup"><span data-stu-id="a3b69-119">You can do the same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="a3b69-120">C# Source file</span><span class="sxs-lookup"><span data-stu-id="a3b69-120">C# Source file</span></span>
<span data-ttu-id="a3b69-121">Modify your page `.xaml.cs` file:</span><span class="sxs-lookup"><span data-stu-id="a3b69-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="a3b69-122">Add to your `using` statements:</span><span class="sxs-lookup"><span data-stu-id="a3b69-122">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="a3b69-123">Replace `Page` with `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="a3b69-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="a3b69-124">**Without Engagement:**</span><span class="sxs-lookup"><span data-stu-id="a3b69-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="a3b69-125">**With Engagement:**</span><span class="sxs-lookup"><span data-stu-id="a3b69-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`. Otherwise, the activity is not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="a3b69-128">XAML file</span><span class="sxs-lookup"><span data-stu-id="a3b69-128">XAML file</span></span>
<span data-ttu-id="a3b69-129">Modify your page `.xaml` file:</span><span class="sxs-lookup"><span data-stu-id="a3b69-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="a3b69-130">Add to your namespaces declarations:</span><span class="sxs-lookup"><span data-stu-id="a3b69-130">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="a3b69-131">Replace `Page` with `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="a3b69-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="a3b69-132">**Without Engagement:**</span><span class="sxs-lookup"><span data-stu-id="a3b69-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="a3b69-133">**With Engagement:**</span><span class="sxs-lookup"><span data-stu-id="a3b69-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-the-default-behaviour"></a><span data-ttu-id="a3b69-134">Override the default behaviour</span><span class="sxs-lookup"><span data-stu-id="a3b69-134">Override the default behaviour</span></span>
<span data-ttu-id="a3b69-135">By default, the class name of the page is reported as the activity name, with no extra.</span><span class="sxs-lookup"><span data-stu-id="a3b69-135">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="a3b69-136">If the class uses the "Page" suffix, Engagement removes it.</span><span class="sxs-lookup"><span data-stu-id="a3b69-136">If the class uses the "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="a3b69-137">To override the default behavior for the name, add this code:</span><span class="sxs-lookup"><span data-stu-id="a3b69-137">To override the default behavior for the name, add this code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="a3b69-138">To report extra information with your activity, add this code:</span><span class="sxs-lookup"><span data-stu-id="a3b69-138">To report extra information with your activity, add this code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="a3b69-139">These methods are called from within the `OnNavigatedTo` method of your page.</span><span class="sxs-lookup"><span data-stu-id="a3b69-139">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="a3b69-140">Alternate method: call `StartActivity()` manually</span><span class="sxs-lookup"><span data-stu-id="a3b69-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="a3b69-141">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span><span class="sxs-lookup"><span data-stu-id="a3b69-141">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="a3b69-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span><span class="sxs-lookup"><span data-stu-id="a3b69-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Ensure you end your session correctly.
> 
> The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed. Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method. This method notifies the Engagement server that the current user has left the application, which will impact all application logs.
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="a3b69-147">Advanced reporting</span><span class="sxs-lookup"><span data-stu-id="a3b69-147">Advanced reporting</span></span>
<span data-ttu-id="a3b69-148">Optionally, you may want to report application-specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span><span class="sxs-lookup"><span data-stu-id="a3b69-148">Optionally, you may want to report application-specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="a3b69-149">The Engagement API allows use of all Engagement's advanced capabilities.</span><span class="sxs-lookup"><span data-stu-id="a3b69-149">The Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="a3b69-150">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="a3b69-150">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

