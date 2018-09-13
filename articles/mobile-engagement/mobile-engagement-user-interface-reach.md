---
title: Azure Mobile Engagement User Interface - Reach
description: Learn how to reach out to the users of your application with push notifications using Azure Mobile Engagement
services: mobile-engagement
documentationcenter: ''
author: piyushjo
manager: erikre
editor: ''
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d77052bda09a7af6aee7c97f6ece6ff354b3878d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662978"
---
# <a name="how-to-reach-out-to-the-users-of-your-application-with-push-notifications"></a><span data-ttu-id="af843-103">How to reach out to the users of your application with push notifications</span><span class="sxs-lookup"><span data-stu-id="af843-103">How to reach out to the users of your application with push notifications</span></span>
<span data-ttu-id="af843-104">This article describes the **REACH** tab of the **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="af843-104">This article describes the **REACH** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="af843-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span><span class="sxs-lookup"><span data-stu-id="af843-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="af843-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span><span class="sxs-lookup"><span data-stu-id="af843-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="af843-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="af843-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="af843-108">The Reach section of the UI is the Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via the Reach API (and some elements of the low level Push API).</span><span class="sxs-lookup"><span data-stu-id="af843-108">The Reach section of the UI is the Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via the Reach API (and some elements of the low level Push API).</span></span> <span data-ttu-id="af843-109">Remember that whether you are using the APIs or the UI, you will need to integrate both Azure Mobile Engagement and Reach into your application for each platform with the SDK before you can use Reach campaigns.</span><span class="sxs-lookup"><span data-stu-id="af843-109">Remember that whether you are using the APIs or the UI, you will need to integrate both Azure Mobile Engagement and Reach into your application for each platform with the SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="af843-110">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span><span class="sxs-lookup"><span data-stu-id="af843-110">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="af843-111">Press this button to get more contextual information about a section.</span><span class="sxs-lookup"><span data-stu-id="af843-111">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="af843-112">Four types of Push notifications</span><span class="sxs-lookup"><span data-stu-id="af843-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="af843-113">Announcements - allow you to send advertising messages to users that redirect them to another location inside your app or to send them to a webpage or store outside of your app.</span><span class="sxs-lookup"><span data-stu-id="af843-113">Announcements - allow you to send advertising messages to users that redirect them to another location inside your app or to send them to a webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="af843-114">Polls - allow you to gather information from end users by asking them questions.</span><span class="sxs-lookup"><span data-stu-id="af843-114">Polls - allow you to gather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="af843-115">Data Pushes - allow you to send a binary or base64 data file.</span><span class="sxs-lookup"><span data-stu-id="af843-115">Data Pushes - allow you to send a binary or base64 data file.</span></span> <span data-ttu-id="af843-116">The information contained in a data push is sent to your application to modify your users' current experience in your app.</span><span class="sxs-lookup"><span data-stu-id="af843-116">The information contained in a data push is sent to your application to modify your users' current experience in your app.</span></span> <span data-ttu-id="af843-117">Your application needs to be able to process the data in a data push.</span><span class="sxs-lookup"><span data-stu-id="af843-117">Your application needs to be able to process the data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="af843-118">Campaign Details</span><span class="sxs-lookup"><span data-stu-id="af843-118">Campaign Details</span></span>
<span data-ttu-id="af843-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click to open them.</span><span class="sxs-lookup"><span data-stu-id="af843-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="af843-120">You can clone campaigns that have already been activated by hovering over their names or you can click to open them.</span><span class="sxs-lookup"><span data-stu-id="af843-120">You can clone campaigns that have already been activated by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="af843-121">However, you can't change a campaign once it has been activated.</span><span class="sxs-lookup"><span data-stu-id="af843-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="af843-123">Reach Feedback</span><span class="sxs-lookup"><span data-stu-id="af843-123">Reach Feedback</span></span>
<span data-ttu-id="af843-124">Click on **Statistics** to see the details of a Reach campaign.</span><span class="sxs-lookup"><span data-stu-id="af843-124">Click on **Statistics** to see the details of a Reach campaign.</span></span> <span data-ttu-id="af843-125">The **Simple** view provides a visual representation in the form of a column bar graph about what happened after a campaign was activated.</span><span class="sxs-lookup"><span data-stu-id="af843-125">The **Simple** view provides a visual representation in the form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="af843-126">The **Advanced** view provides more granular details about the push campaign.</span><span class="sxs-lookup"><span data-stu-id="af843-126">The **Advanced** view provides more granular details about the push campaign.</span></span> <span data-ttu-id="af843-127">These details will not be available if you are sending a test campaign i.e. a push sent to a test device.</span><span class="sxs-lookup"><span data-stu-id="af843-127">These details will not be available if you are sending a test campaign i.e. a push sent to a test device.</span></span> <span data-ttu-id="af843-128">Here is how you should interpret these details:</span><span class="sxs-lookup"><span data-stu-id="af843-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="af843-129">**Pushed** - This specifies the number of messages pushed to the devices.</span><span class="sxs-lookup"><span data-stu-id="af843-129">**Pushed** - This specifies the number of messages pushed to the devices.</span></span> <span data-ttu-id="af843-130">This number will depend on the target audience you specified while creating the push campaign.</span><span class="sxs-lookup"><span data-stu-id="af843-130">This number will depend on the target audience you specified while creating the push campaign.</span></span> <span data-ttu-id="af843-131">If you do not specify any target audience, then this push will be sent out to all the registered devices.</span><span class="sxs-lookup"><span data-stu-id="af843-131">If you do not specify any target audience, then this push will be sent out to all the registered devices.</span></span> <span data-ttu-id="af843-132">Like all other push services, we do not push the notifications directly to the devices but instead push them to the respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver the notifications to the devices.</span><span class="sxs-lookup"><span data-stu-id="af843-132">Like all other push services, we do not push the notifications directly to the devices but instead push them to the respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver the notifications to the devices.</span></span> 
2. <span data-ttu-id="af843-133">**Delivered** - This specifies the number of messages which are successfully delivered by the PNS to the device and acknowledged as received by Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="af843-133">**Delivered** - This specifies the number of messages which are successfully delivered by the PNS to the device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="af843-134">*Reasons for Delivered count being less than Pushed count:*</span><span class="sxs-lookup"><span data-stu-id="af843-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="af843-135">If the user has uninstalled the app from the device but the PNS doesn't know about it at the time we send the push to the PNS then the message will be dropped.</span><span class="sxs-lookup"><span data-stu-id="af843-135">If the user has uninstalled the app from the device but the PNS doesn't know about it at the time we send the push to the PNS then the message will be dropped.</span></span>
   2. <span data-ttu-id="af843-136">If the device has the app but the devices themselves were offline for long periods of time, then the PNS will fail to deliver the message to the device.</span><span class="sxs-lookup"><span data-stu-id="af843-136">If the device has the app but the devices themselves were offline for long periods of time, then the PNS will fail to deliver the message to the device.</span></span> 
   3. <span data-ttu-id="af843-137">If the message does get delivered to the device but the Mobile Engagement SDK in the app doesn’t recognize the content of the message, then it drops that message.</span><span class="sxs-lookup"><span data-stu-id="af843-137">If the message does get delivered to the device but the Mobile Engagement SDK in the app doesn’t recognize the content of the message, then it drops that message.</span></span> <span data-ttu-id="af843-138">This could happen if the customization of the notification in the app generates an exception which we catch in the SDK and drop the message.</span><span class="sxs-lookup"><span data-stu-id="af843-138">This could happen if the customization of the notification in the app generates an exception which we catch in the SDK and drop the message.</span></span> <span data-ttu-id="af843-139">This could also occur if the app on the device is using a version of the Mobile Engagement SDK which is not able to understand the newer version of the push message sent from the platform but this is only when the app was upgraded after the notification was dispatched from the service platform.</span><span class="sxs-lookup"><span data-stu-id="af843-139">This could also occur if the app on the device is using a version of the Mobile Engagement SDK which is not able to understand the newer version of the push message sent from the platform but this is only when the app was upgraded after the notification was dispatched from the service platform.</span></span> <span data-ttu-id="af843-140">The **Advanced** tab will tell how many messages were dropped.</span><span class="sxs-lookup"><span data-stu-id="af843-140">The **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="af843-141">On iOS devices, messages sometimes do not get delivered if either the device is on low battery or if the app is consuming significant amount of power when processing remote notifications.</span><span class="sxs-lookup"><span data-stu-id="af843-141">On iOS devices, messages sometimes do not get delivered if either the device is on low battery or if the app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="af843-142">This is a limitation of the iOS devices.</span><span class="sxs-lookup"><span data-stu-id="af843-142">This is a limitation of the iOS devices.</span></span>   
3. <span data-ttu-id="af843-143">**Displayed** - This specifies the number of messages which are successfully shown to the app user on the device in the form of a system push/out-of-app notification in the notification center or an in-app notification within the mobile app.</span><span class="sxs-lookup"><span data-stu-id="af843-143">**Displayed** - This specifies the number of messages which are successfully shown to the app user on the device in the form of a system push/out-of-app notification in the notification center or an in-app notification within the mobile app.</span></span>  <span data-ttu-id="af843-144">The **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span><span class="sxs-lookup"><span data-stu-id="af843-144">The **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="af843-145">*Reasons for Displayed count being less than Delivered count (waiting to be displayed)*</span><span class="sxs-lookup"><span data-stu-id="af843-145">*Reasons for Displayed count being less than Delivered count (waiting to be displayed)*</span></span>
   
   1. <span data-ttu-id="af843-146">If the notification campaign had an end date on it then it is possible that the notification was delivered but when the time came to open and display it to the app user, it was already expired so it was never displayed.</span><span class="sxs-lookup"><span data-stu-id="af843-146">If the notification campaign had an end date on it then it is possible that the notification was delivered but when the time came to open and display it to the app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="af843-147">If the notification is an in-app notification then the notification is only displayed when the app user opens the app.</span><span class="sxs-lookup"><span data-stu-id="af843-147">If the notification is an in-app notification then the notification is only displayed when the app user opens the app.</span></span> <span data-ttu-id="af843-148">In cases where the app user hasn't opened the app, the SDK will report that the notification was delivered but not yet displayed until the app is opened.</span><span class="sxs-lookup"><span data-stu-id="af843-148">In cases where the app user hasn't opened the app, the SDK will report that the notification was delivered but not yet displayed until the app is opened.</span></span> 
   3. <span data-ttu-id="af843-149">If the notification is an in-app notification and configured to be shown on a specific activity/screen then also the notification will be reported as delivered but not yet delivered until the user opens the app on a specific screen.</span><span class="sxs-lookup"><span data-stu-id="af843-149">If the notification is an in-app notification and configured to be shown on a specific activity/screen then also the notification will be reported as delivered but not yet delivered until the user opens the app on a specific screen.</span></span> 
4. <span data-ttu-id="af843-150">**User Interactions** - This specifies the number of messages which the app user has interacted with and will include the messages which are either actioned or exited.</span><span class="sxs-lookup"><span data-stu-id="af843-150">**User Interactions** - This specifies the number of messages which the app user has interacted with and will include the messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="af843-151">*The app user can action a notification in either of the following ways:*</span><span class="sxs-lookup"><span data-stu-id="af843-151">*The app user can action a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="af843-152">If the notification is a system/out-of-app notification or an in-app notification sent as notification-only then the app user clicks on the notification.</span><span class="sxs-lookup"><span data-stu-id="af843-152">If the notification is a system/out-of-app notification or an in-app notification sent as notification-only then the app user clicks on the notification.</span></span>
     2. <span data-ttu-id="af843-153">If the notification is an in-app notification with a text or web-view or polls then the app user clicks on the Action button in the notification.</span><span class="sxs-lookup"><span data-stu-id="af843-153">If the notification is an in-app notification with a text or web-view or polls then the app user clicks on the Action button in the notification.</span></span>
     3. <span data-ttu-id="af843-154">If the notification is an in-app notification with a web-view then the app user clicks on a URL in the web view [Android Only]</span><span class="sxs-lookup"><span data-stu-id="af843-154">If the notification is an in-app notification with a web-view then the app user clicks on a URL in the web view [Android Only]</span></span>
   * <span data-ttu-id="af843-155">*The app user can exit a notification in either of the following ways:*</span><span class="sxs-lookup"><span data-stu-id="af843-155">*The app user can exit a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="af843-156">Clicking the close button on the notification directly.</span><span class="sxs-lookup"><span data-stu-id="af843-156">Clicking the close button on the notification directly.</span></span> 
     2. <span data-ttu-id="af843-157">Swiping away or deleting the notification.</span><span class="sxs-lookup"><span data-stu-id="af843-157">Swiping away or deleting the notification.</span></span> 
     3. <span data-ttu-id="af843-158">In-app notifications with text/web content and polls are typically displayed to the app user in a two-step process.</span><span class="sxs-lookup"><span data-stu-id="af843-158">In-app notifications with text/web content and polls are typically displayed to the app user in a two-step process.</span></span> <span data-ttu-id="af843-159">They see a notification first and when they click on it, they see the subsequent text/web/poll content.</span><span class="sxs-lookup"><span data-stu-id="af843-159">They see a notification first and when they click on it, they see the subsequent text/web/poll content.</span></span> <span data-ttu-id="af843-160">The app user can exit a notification in either of these steps and the details in the Advanced view captures this.</span><span class="sxs-lookup"><span data-stu-id="af843-160">The app user can exit a notification in either of these steps and the details in the Advanced view captures this.</span></span> 
5. <span data-ttu-id="af843-161">**Actioned** - This specifies the number of messages which were explicitly actioned by the app user.</span><span class="sxs-lookup"><span data-stu-id="af843-161">**Actioned** - This specifies the number of messages which were explicitly actioned by the app user.</span></span> <span data-ttu-id="af843-162">This is the most interesting number as this tells how many app users were interested by the message you pushed out in the notification.</span><span class="sxs-lookup"><span data-stu-id="af843-162">This is the most interesting number as this tells how many app users were interested by the message you pushed out in the notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="af843-163">On iOS & Windows platforms, if the user has the app open and the campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at the same time.</span><span class="sxs-lookup"><span data-stu-id="af843-163">On iOS & Windows platforms, if the user has the app open and the campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at the same time.</span></span> <span data-ttu-id="af843-164">This may cause a Displayed count higher than the Delivered.</span><span class="sxs-lookup"><span data-stu-id="af843-164">This may cause a Displayed count higher than the Delivered.</span></span> <span data-ttu-id="af843-165">If the user interacts or actions the notification, then even the User Interactions/Actioned count could be greater than Delivered.</span><span class="sxs-lookup"><span data-stu-id="af843-165">If the user interacts or actions the notification, then even the User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="af843-167">See also</span><span class="sxs-lookup"><span data-stu-id="af843-167">See also</span></span>
* <span data-ttu-id="af843-168">[Concepts][Link 6]</span><span class="sxs-lookup"><span data-stu-id="af843-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="af843-169">[Troubleshooting Guide Service][Link 24]</span><span class="sxs-lookup"><span data-stu-id="af843-169">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-home/home1.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-home/home5.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach/reach1.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach/reach2.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments1.png
[36]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments2.png
[37]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments3.png
[38]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments4.png
[39]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments5.png
[40]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments6.png
[41]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments7.png
[42]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments8.png
[43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments9.png
[44]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments10.png
[45]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-segments/segments11.png
[46]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings1.png
[47]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings2.png
[48]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings3.png
[49]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings4.png
[50]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings5.png
[51]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings6.png
[52]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings7.png
[53]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings8.png
[54]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings9.png
[55]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings10.png
[56]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings11.png
[57]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings12.png
[58]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

























































