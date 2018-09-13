---
title: Azure Mobile Engagement User Interface - Reach Criterion
description: Learn how to use targeting criteria to send push campaigns to a select subset of your users using Azure Mobile Engagement
services: mobile-engagement
documentationcenter: ''
author: piyushjo
manager: erikre
editor: ''
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a3189508d3f07887e97ce7bc9c9a77bb4d1bb125
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555304"
---
# <a name="how-to-use-targeting-criteria-to-send-push-campaigns-to-a-select-subset-of-your-users"></a><span data-ttu-id="7b990-103">How to use targeting criteria to send push campaigns to a select subset of your users</span><span class="sxs-lookup"><span data-stu-id="7b990-103">How to use targeting criteria to send push campaigns to a select subset of your users</span></span>
<span data-ttu-id="7b990-104">Targeting your audience by specific criteria with the "New Criteria" button is one of the most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that the customers will respond to instead of Spamming everyone.</span><span class="sxs-lookup"><span data-stu-id="7b990-104">Targeting your audience by specific criteria with the "New Criteria" button is one of the most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that the customers will respond to instead of Spamming everyone.</span></span> <span data-ttu-id="7b990-105">You can limit your audience based on standard criteria and simulate pushes to determine how many people will receive the notification.</span><span class="sxs-lookup"><span data-stu-id="7b990-105">You can limit your audience based on standard criteria and simulate pushes to determine how many people will receive the notification.</span></span>

<span data-ttu-id="7b990-106">**See also:**</span><span class="sxs-lookup"><span data-stu-id="7b990-106">**See also:**</span></span>

* <span data-ttu-id="7b990-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span><span class="sxs-lookup"><span data-stu-id="7b990-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="7b990-108">Audience criteria can include:</span><span class="sxs-lookup"><span data-stu-id="7b990-108">Audience criteria can include:</span></span>
* <span data-ttu-id="7b990-109">\*\*Technicals: \*\* You can target based on the same technical information you can see in the Analytics and Monitor sections.</span><span class="sxs-lookup"><span data-stu-id="7b990-109">\*\*Technicals: \*\* You can target based on the same technical information you can see in the Analytics and Monitor sections.</span></span> <span data-ttu-id="7b990-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span><span class="sxs-lookup"><span data-stu-id="7b990-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="7b990-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria to target an audience from the GPS location.</span><span class="sxs-lookup"><span data-stu-id="7b990-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria to target an audience from the GPS location.</span></span> <span data-ttu-id="7b990-112">"Lazy Area Location Reporting" call also be used to target an audience from the cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from the SDK).</span><span class="sxs-lookup"><span data-stu-id="7b990-112">"Lazy Area Location Reporting" call also be used to target an audience from the cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from the SDK).</span></span> <span data-ttu-id="7b990-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span><span class="sxs-lookup"><span data-stu-id="7b990-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="7b990-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span><span class="sxs-lookup"><span data-stu-id="7b990-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="7b990-115">This enables you to better target your audience after two or three reach campaigns than you could the first time.</span><span class="sxs-lookup"><span data-stu-id="7b990-115">This enables you to better target your audience after two or three reach campaigns than you could the first time.</span></span> <span data-ttu-id="7b990-116">It can also be used to filter out users who already received a notification with similar content, by setting a campaign to NOT be sent to users who already received a specific previous campaign.</span><span class="sxs-lookup"><span data-stu-id="7b990-116">It can also be used to filter out users who already received a notification with similar content, by setting a campaign to NOT be sent to users who already received a specific previous campaign.</span></span> <span data-ttu-id="7b990-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span><span class="sxs-lookup"><span data-stu-id="7b990-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="7b990-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span><span class="sxs-lookup"><span data-stu-id="7b990-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="7b990-119">**Install Tracking:** You can track information based on where your users installed your App.</span><span class="sxs-lookup"><span data-stu-id="7b990-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="7b990-120">**See also:** [UI Documentation -  Settings][Link 20]</span><span class="sxs-lookup"><span data-stu-id="7b990-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="7b990-121">**User Profile:** You can target based on standard user information and you can target based on the custom app info that you have created.</span><span class="sxs-lookup"><span data-stu-id="7b990-121">**User Profile:** You can target based on standard user information and you can target based on the custom app info that you have created.</span></span> <span data-ttu-id="7b990-122">This includes users who are currently logged in and users that have answered specific questions you have asked them to set in the app itself instead of just how they have responded to previous campaigns.</span><span class="sxs-lookup"><span data-stu-id="7b990-122">This includes users who are currently logged in and users that have answered specific questions you have asked them to set in the app itself instead of just how they have responded to previous campaigns.</span></span> <span data-ttu-id="7b990-123">All of your App Info's defined for your app show up on this list.</span><span class="sxs-lookup"><span data-stu-id="7b990-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="7b990-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span><span class="sxs-lookup"><span data-stu-id="7b990-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="7b990-125">All of your segments defined for your app show up on this list.</span><span class="sxs-lookup"><span data-stu-id="7b990-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="7b990-126">**See also:** [UI Documentation -  Segments][Link 18]</span><span class="sxs-lookup"><span data-stu-id="7b990-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="7b990-127">**App Info:** Custom App Info Tags can be created from “Settings” to track user behavior.</span><span class="sxs-lookup"><span data-stu-id="7b990-127">**App Info:** Custom App Info Tags can be created from “Settings” to track user behavior.</span></span> <span data-ttu-id="7b990-128">**See also:** [UI Documentation -  Settings][Link 20]</span><span class="sxs-lookup"><span data-stu-id="7b990-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="7b990-129">Example:</span><span class="sxs-lookup"><span data-stu-id="7b990-129">Example:</span></span>
<span data-ttu-id="7b990-130">If you want to push an announcement only to the sub-set of your users that have performed an in-app purchase action.</span><span class="sxs-lookup"><span data-stu-id="7b990-130">If you want to push an announcement only to the sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="7b990-131">Go to your application settings page, select the "App info" menu and select "New app info"</span><span class="sxs-lookup"><span data-stu-id="7b990-131">Go to your application settings page, select the "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="7b990-132">Register a new Boolean app info called "inAppPurchase"</span><span class="sxs-lookup"><span data-stu-id="7b990-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="7b990-133">Make your application set this app info to "true" when the user successfully performs an in-app purchase (by using the sendAppInfo("inAppPurchase", ...) function)</span><span class="sxs-lookup"><span data-stu-id="7b990-133">Make your application set this app info to "true" when the user successfully performs an in-app purchase (by using the sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="7b990-134">If you don't want to do this from your application, you can do it from your backend by using the device API)</span><span class="sxs-lookup"><span data-stu-id="7b990-134">If you don't want to do this from your application, you can do it from your backend by using the device API)</span></span>
5. <span data-ttu-id="7b990-135">Then, you just need to create your announcement, with a criterion limiting your audience to users having "inAppPurchase" set to "true")</span><span class="sxs-lookup"><span data-stu-id="7b990-135">Then, you just need to create your announcement, with a criterion limiting your audience to users having "inAppPurchase" set to "true")</span></span>

> [!NOTE]
> <span data-ttu-id="7b990-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement to gather information from your users' devices before the push is sent and so can cause a delay.</span><span class="sxs-lookup"><span data-stu-id="7b990-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement to gather information from your users' devices before the push is sent and so can cause a delay.</span></span> <span data-ttu-id="7b990-137">Complex push configuration options (like updating badges) can also delay pushes.</span><span class="sxs-lookup"><span data-stu-id="7b990-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="7b990-138">Using a "one shot" campaign from the Push API is the absolute fastest push method in Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7b990-138">Using a "one shot" campaign from the Push API is the absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="7b990-139">Using only app info tags as push criteria for a Reach campaign (either from the Reach API or the UI) is the next fastest method since app info tags are stored on the server side.</span><span class="sxs-lookup"><span data-stu-id="7b990-139">Using only app info tags as push criteria for a Reach campaign (either from the Reach API or the UI) is the next fastest method since app info tags are stored on the server side.</span></span> <span data-ttu-id="7b990-140">Using other targeting criteria for a push campaign is the most flexible but slowest push method since Azure Mobile Engagement has to query the devices in order to send the campaign.</span><span class="sxs-lookup"><span data-stu-id="7b990-140">Using other targeting criteria for a push campaign is the most flexible but slowest push method since Azure Mobile Engagement has to query the devices in order to send the campaign.</span></span>

![Reach-Criterion1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="7b990-142">Criterion Options Apply to:</span><span class="sxs-lookup"><span data-stu-id="7b990-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="7b990-143">**Technicals**</span><span class="sxs-lookup"><span data-stu-id="7b990-143">**Technicals**</span></span>     
* <span data-ttu-id="7b990-144">Firmware name:    Firmware name</span><span class="sxs-lookup"><span data-stu-id="7b990-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="7b990-145">Firmware version:    Firmware version</span><span class="sxs-lookup"><span data-stu-id="7b990-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="7b990-146">Device model:    Device model</span><span class="sxs-lookup"><span data-stu-id="7b990-146">Device model:    Device model</span></span>
* <span data-ttu-id="7b990-147">Device manufacturer:    Device manufacturer</span><span class="sxs-lookup"><span data-stu-id="7b990-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="7b990-148">Application version:    Application version</span><span class="sxs-lookup"><span data-stu-id="7b990-148">Application version:    Application version</span></span>
* <span data-ttu-id="7b990-149">Carrier name:    Carrier name, undefined</span><span class="sxs-lookup"><span data-stu-id="7b990-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="7b990-150">Carrier country:    Carrier country, undefined</span><span class="sxs-lookup"><span data-stu-id="7b990-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="7b990-151">Network type:    Network type</span><span class="sxs-lookup"><span data-stu-id="7b990-151">Network type:    Network type</span></span>
* <span data-ttu-id="7b990-152">Locale:    Locale</span><span class="sxs-lookup"><span data-stu-id="7b990-152">Locale:    Locale</span></span>
* <span data-ttu-id="7b990-153">Screen size:    Screen size</span><span class="sxs-lookup"><span data-stu-id="7b990-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="7b990-154">**Location**</span><span class="sxs-lookup"><span data-stu-id="7b990-154">**Location**</span></span>      
* <span data-ttu-id="7b990-155">Last known area:    Country, Region, Locality</span><span class="sxs-lookup"><span data-stu-id="7b990-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="7b990-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span><span class="sxs-lookup"><span data-stu-id="7b990-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="7b990-157">**Reach feedback**</span><span class="sxs-lookup"><span data-stu-id="7b990-157">**Reach feedback**</span></span>     
* <span data-ttu-id="7b990-158">Announcement feedback:    Announcement, feedback</span><span class="sxs-lookup"><span data-stu-id="7b990-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="7b990-159">Poll feedback:    Poll, feedback</span><span class="sxs-lookup"><span data-stu-id="7b990-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="7b990-160">Poll answer feedback:    Poll answer feedback, question, choice</span><span class="sxs-lookup"><span data-stu-id="7b990-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="7b990-161">Data Push feedback:    Data Push, feedback</span><span class="sxs-lookup"><span data-stu-id="7b990-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="7b990-162">**Install Tracking**</span><span class="sxs-lookup"><span data-stu-id="7b990-162">**Install Tracking**</span></span>     
* <span data-ttu-id="7b990-163">Store:    Store, Undefined</span><span class="sxs-lookup"><span data-stu-id="7b990-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="7b990-164">Source:    Source, Undefined</span><span class="sxs-lookup"><span data-stu-id="7b990-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="7b990-165">**User profile**</span><span class="sxs-lookup"><span data-stu-id="7b990-165">**User profile**</span></span>     
* <span data-ttu-id="7b990-166">Gender:    male or female, undefined</span><span class="sxs-lookup"><span data-stu-id="7b990-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="7b990-167">Birth date:    operator, date, undefined</span><span class="sxs-lookup"><span data-stu-id="7b990-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="7b990-168">Opt-in:    true or false, undefined</span><span class="sxs-lookup"><span data-stu-id="7b990-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="7b990-169">**App Info**</span><span class="sxs-lookup"><span data-stu-id="7b990-169">**App Info**</span></span>      
* <span data-ttu-id="7b990-170">String:    String, undefined</span><span class="sxs-lookup"><span data-stu-id="7b990-170">String:    String, undefined</span></span>
* <span data-ttu-id="7b990-171">Date:    operator, date, undefined</span><span class="sxs-lookup"><span data-stu-id="7b990-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="7b990-172">Integer:    operator, number, undefined</span><span class="sxs-lookup"><span data-stu-id="7b990-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="7b990-173">Boolean:    true or false, undefined</span><span class="sxs-lookup"><span data-stu-id="7b990-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="7b990-174">**Segment**</span><span class="sxs-lookup"><span data-stu-id="7b990-174">**Segment**</span></span>    
* <span data-ttu-id="7b990-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span><span class="sxs-lookup"><span data-stu-id="7b990-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

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

























































