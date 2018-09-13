---
title: Windows Phone Silverlight Reach SDK Integration
description: How to Integrate Azure Mobile Engagement Reach with Windows Phone Silverlight Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0738f33df94d14fbb393bfaaf09e94c6560213cc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551949"
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="29616-103">Windows Phone Silverlight Reach SDK Integration</span><span class="sxs-lookup"><span data-stu-id="29616-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="29616-104">You must follow the integration procedure described in the [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span><span class="sxs-lookup"><span data-stu-id="29616-104">You must follow the integration procedure described in the [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="29616-105">Embed the Engagement Reach SDK into your Windows Phone Silverlight project</span><span class="sxs-lookup"><span data-stu-id="29616-105">Embed the Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="29616-106">You do not have anything to add.</span><span class="sxs-lookup"><span data-stu-id="29616-106">You do not have anything to add.</span></span> <span data-ttu-id="29616-107">`EngagementReach` references and resources are already in your project.</span><span class="sxs-lookup"><span data-stu-id="29616-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="29616-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span><span class="sxs-lookup"><span data-stu-id="29616-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span>
> 
> 

## <a name="add-the-capabilities"></a><span data-ttu-id="29616-109">Add the capabilities</span><span class="sxs-lookup"><span data-stu-id="29616-109">Add the capabilities</span></span>
<span data-ttu-id="29616-110">The Engagement Reach SDK needs some additional capabilities.</span><span class="sxs-lookup"><span data-stu-id="29616-110">The Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="29616-111">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared:</span><span class="sxs-lookup"><span data-stu-id="29616-111">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="29616-112">The first one is used by the MPNS service to allow the display of toast notification.</span><span class="sxs-lookup"><span data-stu-id="29616-112">The first one is used by the MPNS service to allow the display of toast notification.</span></span> <span data-ttu-id="29616-113">The second one is used to embed a browser task into the SDK.</span><span class="sxs-lookup"><span data-stu-id="29616-113">The second one is used to embed a browser task into the SDK.</span></span>

<span data-ttu-id="29616-114">Edit the `WMAppManifest.xml` file and add inside the `<Capabilities />` tag :</span><span class="sxs-lookup"><span data-stu-id="29616-114">Edit the `WMAppManifest.xml` file and add inside the `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-the-microsoft-push-notification-service"></a><span data-ttu-id="29616-115">Enable the Microsoft Push Notification Service</span><span class="sxs-lookup"><span data-stu-id="29616-115">Enable the Microsoft Push Notification Service</span></span>
<span data-ttu-id="29616-116">In order to use the **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set to the name of your project.</span><span class="sxs-lookup"><span data-stu-id="29616-116">In order to use the **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set to the name of your project.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="29616-117">Initialize the Engagement Reach SDK</span><span class="sxs-lookup"><span data-stu-id="29616-117">Initialize the Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="29616-118">Engagement configuration</span><span class="sxs-lookup"><span data-stu-id="29616-118">Engagement configuration</span></span>
<span data-ttu-id="29616-119">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span><span class="sxs-lookup"><span data-stu-id="29616-119">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="29616-120">Edit this file to specify reach configuration :</span><span class="sxs-lookup"><span data-stu-id="29616-120">Edit this file to specify reach configuration :</span></span>

* <span data-ttu-id="29616-121">*Optional*, indicate whether the native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span><span class="sxs-lookup"><span data-stu-id="29616-121">*Optional*, indicate whether the native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="29616-122">*Optional*, indicate the name of the push channel between `<channelName>` and `</channelName>` tags, provide the same that your application may currently use or leave it empty.</span><span class="sxs-lookup"><span data-stu-id="29616-122">*Optional*, indicate the name of the push channel between `<channelName>` and `</channelName>` tags, provide the same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="29616-123">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization :</span><span class="sxs-lookup"><span data-stu-id="29616-123">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether the native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide the same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="29616-124">You can specify the name of the MPNS push channel of your application.</span><span class="sxs-lookup"><span data-stu-id="29616-124">You can specify the name of the MPNS push channel of your application.</span></span> <span data-ttu-id="29616-125">By default, Engagement creates a name based on the appId.</span><span class="sxs-lookup"><span data-stu-id="29616-125">By default, Engagement creates a name based on the appId.</span></span> <span data-ttu-id="29616-126">You have no need to specify the name yourself, except if you plan to use the push channel outside of Engagement.</span><span class="sxs-lookup"><span data-stu-id="29616-126">You have no need to specify the name yourself, except if you plan to use the push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="29616-127">Engagement initialization</span><span class="sxs-lookup"><span data-stu-id="29616-127">Engagement initialization</span></span>
<span data-ttu-id="29616-128">Modify the `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="29616-128">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="29616-129">Add to your `using` statements :</span><span class="sxs-lookup"><span data-stu-id="29616-129">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="29616-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="29616-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="29616-131">Insert `EngagementReach.Instance.OnActivated` in the `Application_Activated` method :</span><span class="sxs-lookup"><span data-stu-id="29616-131">Insert `EngagementReach.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="29616-132">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span><span class="sxs-lookup"><span data-stu-id="29616-132">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="29616-133">You do not have to do it yourself.</span><span class="sxs-lookup"><span data-stu-id="29616-133">You do not have to do it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="29616-134">App store submission considerations</span><span class="sxs-lookup"><span data-stu-id="29616-134">App store submission considerations</span></span>
<span data-ttu-id="29616-135">Microsoft imposes some rules when using the push notifications:</span><span class="sxs-lookup"><span data-stu-id="29616-135">Microsoft imposes some rules when using the push notifications:</span></span>

<span data-ttu-id="29616-136">From the Microsoft [Application Policies] documentation, section 2.9:</span><span class="sxs-lookup"><span data-stu-id="29616-136">From the Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="29616-137">You must ask the user to accept to receive push notifications.</span><span class="sxs-lookup"><span data-stu-id="29616-137">You must ask the user to accept to receive push notifications.</span></span> <span data-ttu-id="29616-138">Then, in your settings, add a way to disable the push notifications.</span><span class="sxs-lookup"><span data-stu-id="29616-138">Then, in your settings, add a way to disable the push notifications.</span></span>

<span data-ttu-id="29616-139">The EngagementReach object provides two methods to manage the opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="29616-139">The EngagementReach object provides two methods to manage the opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="29616-140">You could, for example, create an option in the settings with a toggle to disable or enable MPNS.</span><span class="sxs-lookup"><span data-stu-id="29616-140">You could, for example, create an option in the settings with a toggle to disable or enable MPNS.</span></span>

<span data-ttu-id="29616-141">You can also decide to deactivate MPNS through the Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span><span class="sxs-lookup"><span data-stu-id="29616-141">You can also decide to deactivate MPNS through the Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="29616-142">2.9.1) The application must first describe the notifications to be provided and **obtain the user’s express permission (opt-in)**, and **must provide a mechanism through which the user can opt out of receiving push notifications**.</span><span class="sxs-lookup"><span data-stu-id="29616-142">2.9.1) The application must first describe the notifications to be provided and **obtain the user’s express permission (opt-in)**, and **must provide a mechanism through which the user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="29616-143">All notifications provided using the Microsoft Push Notification Service must be consistent with the description provided to the user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span><span class="sxs-lookup"><span data-stu-id="29616-143">All notifications provided using the Microsoft Push Notification Service must be consistent with the description provided to the user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="29616-144">You should not use too many push notifications.</span><span class="sxs-lookup"><span data-stu-id="29616-144">You should not use too many push notifications.</span></span> <span data-ttu-id="29616-145">Engagement will handle notifications for you.</span><span class="sxs-lookup"><span data-stu-id="29616-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="29616-146">2.9.2) The application and its use of the Microsoft Push Notification Service must not excessively use network capacity or bandwidth of the Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected to the Microsoft Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="29616-146">2.9.2) The application and its use of the Microsoft Push Notification Service must not excessively use network capacity or bandwidth of the Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected to the Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="29616-147">Do not rely on MPNS to send criticals information.</span><span class="sxs-lookup"><span data-stu-id="29616-147">Do not rely on MPNS to send criticals information.</span></span> <span data-ttu-id="29616-148">Engagement uses MPNS, so this rule also applies for the campaigns created inside the Engagement front-end.</span><span class="sxs-lookup"><span data-stu-id="29616-148">Engagement uses MPNS, so this rule also applies for the campaigns created inside the Engagement front-end.</span></span>

> <span data-ttu-id="29616-149">2.9.3) The Microsoft Push Notification Service may not be used to send notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related to a medical device or condition.</span><span class="sxs-lookup"><span data-stu-id="29616-149">2.9.3) The Microsoft Push Notification Service may not be used to send notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related to a medical device or condition.</span></span> <span data-ttu-id="29616-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT THE USE OF THE MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED TO OCCUR ON A REAL-TIME BASIS.</span><span class="sxs-lookup"><span data-stu-id="29616-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT THE USE OF THE MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED TO OCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="29616-151">**We cannot guarantee that your application will pass the validation process if you do not respect these recommendations.**</span><span class="sxs-lookup"><span data-stu-id="29616-151">**We cannot guarantee that your application will pass the validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="29616-152">Handle data push (optional)</span><span class="sxs-lookup"><span data-stu-id="29616-152">Handle data push (optional)</span></span>
<span data-ttu-id="29616-153">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span><span class="sxs-lookup"><span data-stu-id="29616-153">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

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

<span data-ttu-id="29616-154">You can see that the callback of each method returns a boolean.</span><span class="sxs-lookup"><span data-stu-id="29616-154">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="29616-155">Engagement sends a feedback to its back-end after dispatching the data push.</span><span class="sxs-lookup"><span data-stu-id="29616-155">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="29616-156">If the callback returns false, the `exit` feedback will be send.</span><span class="sxs-lookup"><span data-stu-id="29616-156">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="29616-157">Otherwise, it will be `action`.</span><span class="sxs-lookup"><span data-stu-id="29616-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="29616-158">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span><span class="sxs-lookup"><span data-stu-id="29616-158">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="29616-159">Engagement is not able to receive multiples feedbacks for a data push.</span><span class="sxs-lookup"><span data-stu-id="29616-159">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="29616-160">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span><span class="sxs-lookup"><span data-stu-id="29616-160">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="29616-161">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span><span class="sxs-lookup"><span data-stu-id="29616-161">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="29616-162">Customize UI (optional)</span><span class="sxs-lookup"><span data-stu-id="29616-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="29616-163">First step</span><span class="sxs-lookup"><span data-stu-id="29616-163">First step</span></span>
<span data-ttu-id="29616-164">We allow you to customize the reach UI.</span><span class="sxs-lookup"><span data-stu-id="29616-164">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="29616-165">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span><span class="sxs-lookup"><span data-stu-id="29616-165">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="29616-166">**Sample Code :**</span><span class="sxs-lookup"><span data-stu-id="29616-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="29616-167">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `Application_Launching` method.</span><span class="sxs-lookup"><span data-stu-id="29616-167">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `Application_Launching` method.</span></span>

<span data-ttu-id="29616-168">**Sample Code :**</span><span class="sxs-lookup"><span data-stu-id="29616-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="29616-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="29616-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="29616-170">You don't have to create your own, and if you do so, you don't have to override every method.</span><span class="sxs-lookup"><span data-stu-id="29616-170">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="29616-171">The default behavior is to select the Engagement base object.</span><span class="sxs-lookup"><span data-stu-id="29616-171">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="29616-172">Layouts</span><span class="sxs-lookup"><span data-stu-id="29616-172">Layouts</span></span>
<span data-ttu-id="29616-173">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span><span class="sxs-lookup"><span data-stu-id="29616-173">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="29616-174">However, you can decide to use your own resources to reflect your brand in these components.</span><span class="sxs-lookup"><span data-stu-id="29616-174">However, you can decide to use your own resources to reflect your brand in these components.</span></span>

<span data-ttu-id="29616-175">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts :</span><span class="sxs-lookup"><span data-stu-id="29616-175">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts :</span></span>

<span data-ttu-id="29616-176">**Sample Code :**</span><span class="sxs-lookup"><span data-stu-id="29616-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetPollUri()
    {
       // return the path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="29616-177">The `CreateNotification` method can return null.</span><span class="sxs-lookup"><span data-stu-id="29616-177">The `CreateNotification` method can return null.</span></span> <span data-ttu-id="29616-178">The notification won't be displayed and the reach campaign will be dropped.</span><span class="sxs-lookup"><span data-stu-id="29616-178">The notification won't be displayed and the reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="29616-179">To simplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span><span class="sxs-lookup"><span data-stu-id="29616-179">To simplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="29616-180">They are located in the Engagement SDK archive (/src/reach/).</span><span class="sxs-lookup"><span data-stu-id="29616-180">They are located in the Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="29616-181">The sources that we provide are the exact same ones that we use.</span><span class="sxs-lookup"><span data-stu-id="29616-181">The sources that we provide are the exact same ones that we use.</span></span> <span data-ttu-id="29616-182">So if you want to modify them directly, don't forget to change the namespace and the name.</span><span class="sxs-lookup"><span data-stu-id="29616-182">So if you want to modify them directly, don't forget to change the namespace and the name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="29616-183">Notification position</span><span class="sxs-lookup"><span data-stu-id="29616-183">Notification position</span></span>
<span data-ttu-id="29616-184">By default, an in-app notification is displayed at the bottom left side of the application.</span><span class="sxs-lookup"><span data-stu-id="29616-184">By default, an in-app notification is displayed at the bottom left side of the application.</span></span> <span data-ttu-id="29616-185">You can change this behavior by overriding the `GetNotificationPosition` method of the `EngagementReachHandler` object.</span><span class="sxs-lookup"><span data-stu-id="29616-185">You can change this behavior by overriding the `GetNotificationPosition` method of the `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of the EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="29616-186">Currently, you can choose between the `BOTTOM` (default) and `TOP` positions.</span><span class="sxs-lookup"><span data-stu-id="29616-186">Currently, you can choose between the `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="29616-187">Launch message</span><span class="sxs-lookup"><span data-stu-id="29616-187">Launch message</span></span>
<span data-ttu-id="29616-188">When a user clicks on a system notification (a toast), Engagement launches the app, load the content of the push messages, and display the page for the corresponding campaign.</span><span class="sxs-lookup"><span data-stu-id="29616-188">When a user clicks on a system notification (a toast), Engagement launches the app, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="29616-189">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span><span class="sxs-lookup"><span data-stu-id="29616-189">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="29616-190">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span><span class="sxs-lookup"><span data-stu-id="29616-190">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="29616-191">Engagement cannot handle that itself, but provides a few handlers for you.</span><span class="sxs-lookup"><span data-stu-id="29616-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="29616-192">To implement the callback, do:</span><span class="sxs-lookup"><span data-stu-id="29616-192">To implement the callback, do:</span></span>

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

<span data-ttu-id="29616-193">You can set the callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span><span class="sxs-lookup"><span data-stu-id="29616-193">You can set the callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="29616-194">Each handler is called by the UI Thread.</span><span class="sxs-lookup"><span data-stu-id="29616-194">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="29616-195">You do not have to worry when using a MessageBox or something UI-related.</span><span class="sxs-lookup"><span data-stu-id="29616-195">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

[Application Policies]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[Additional Requirements for Specific Application Types]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

