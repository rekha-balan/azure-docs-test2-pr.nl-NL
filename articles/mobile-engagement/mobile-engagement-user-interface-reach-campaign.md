---
title: Azure Mobile Engagement User Interface - Reach Campaign
description: Laern how to create and manage push notification campaigns using Azure Mobile Engagement
services: mobile-engagement
documentationcenter: ''
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e279b497c95157c4c3bbb194024a7f5a31d81e3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564386"
---
# <a name="how-to-create-and-manage-push-notification-campaigns"></a><span data-ttu-id="685b3-103">How to create and manage push notification campaigns</span><span class="sxs-lookup"><span data-stu-id="685b3-103">How to create and manage push notification campaigns</span></span>
<span data-ttu-id="685b3-104">You can use the Reach section of the UI to create a new Push campaign with a complex formula by providing all the information you need to send a push notification.</span><span class="sxs-lookup"><span data-stu-id="685b3-104">You can use the Reach section of the UI to create a new Push campaign with a complex formula by providing all the information you need to send a push notification.</span></span> <span data-ttu-id="685b3-105">The options of a Push campaign vary slightly depending on the four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span><span class="sxs-lookup"><span data-stu-id="685b3-105">The options of a Push campaign vary slightly depending on the four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="685b3-106">Option Applies to:</span><span class="sxs-lookup"><span data-stu-id="685b3-106">Option Applies to:</span></span>
* <span data-ttu-id="685b3-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span><span class="sxs-lookup"><span data-stu-id="685b3-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="685b3-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span><span class="sxs-lookup"><span data-stu-id="685b3-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="685b3-109">Notification:     Announcements, Polls</span><span class="sxs-lookup"><span data-stu-id="685b3-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="685b3-110">Content:    Unique for each campaign type</span><span class="sxs-lookup"><span data-stu-id="685b3-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="685b3-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span><span class="sxs-lookup"><span data-stu-id="685b3-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="685b3-112">Time frame:     Announcements, Polls, Tiles</span><span class="sxs-lookup"><span data-stu-id="685b3-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="685b3-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span><span class="sxs-lookup"><span data-stu-id="685b3-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach-Campaign1][20]

## <a name="languages"></a><span data-ttu-id="685b3-115">Languages</span><span class="sxs-lookup"><span data-stu-id="685b3-115">Languages</span></span>
<span data-ttu-id="685b3-116">You can use the Languages drop-down menu to send a different version of your Push to devices that are set to use different languages.</span><span class="sxs-lookup"><span data-stu-id="685b3-116">You can use the Languages drop-down menu to send a different version of your Push to devices that are set to use different languages.</span></span> <span data-ttu-id="685b3-117">By default, all devices will receive the same Push regardless of what language they are set to use.</span><span class="sxs-lookup"><span data-stu-id="685b3-117">By default, all devices will receive the same Push regardless of what language they are set to use.</span></span> <span data-ttu-id="685b3-118">Users with their device set to a different language will receive the Default Language version of the Push.</span><span class="sxs-lookup"><span data-stu-id="685b3-118">Users with their device set to a different language will receive the Default Language version of the Push.</span></span> <span data-ttu-id="685b3-119">Many of the push campaign options allow you to specify alternate content for each of the additional languages you select.</span><span class="sxs-lookup"><span data-stu-id="685b3-119">Many of the push campaign options allow you to specify alternate content for each of the additional languages you select.</span></span> 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="685b3-121">Language differences apply to:</span><span class="sxs-lookup"><span data-stu-id="685b3-121">Language differences apply to:</span></span>
* <span data-ttu-id="685b3-122">Languages:    Unique languages may be selected in addition to the default language</span><span class="sxs-lookup"><span data-stu-id="685b3-122">Languages:    Unique languages may be selected in addition to the default language</span></span>
* <span data-ttu-id="685b3-123">Campaign:    Same for all languages</span><span class="sxs-lookup"><span data-stu-id="685b3-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="685b3-124">Notification:    Unique for each language in addition to the default language</span><span class="sxs-lookup"><span data-stu-id="685b3-124">Notification:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="685b3-125">Content:    Unique for each language in addition to the default language</span><span class="sxs-lookup"><span data-stu-id="685b3-125">Content:    Unique for each language in addition to the default language</span></span>
* <span data-ttu-id="685b3-126">Audience:     May be filtered by a separate language criterion</span><span class="sxs-lookup"><span data-stu-id="685b3-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="685b3-127">Time frame:     Same for all languages</span><span class="sxs-lookup"><span data-stu-id="685b3-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="685b3-128">Test:    May be sent to each language at a time</span><span class="sxs-lookup"><span data-stu-id="685b3-128">Test:    May be sent to each language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="685b3-129">Supported Languages:</span><span class="sxs-lookup"><span data-stu-id="685b3-129">Supported Languages:</span></span>
* <span data-ttu-id="685b3-130">Arabic (ar)</span><span class="sxs-lookup"><span data-stu-id="685b3-130">Arabic (ar)</span></span> 
* <span data-ttu-id="685b3-131">Bulgarian (bg)</span><span class="sxs-lookup"><span data-stu-id="685b3-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="685b3-132">Catalan (ca)</span><span class="sxs-lookup"><span data-stu-id="685b3-132">Catalan (ca)</span></span> 
* <span data-ttu-id="685b3-133">Chinese (zh)</span><span class="sxs-lookup"><span data-stu-id="685b3-133">Chinese (zh)</span></span> 
* <span data-ttu-id="685b3-134">Croatian (hr)</span><span class="sxs-lookup"><span data-stu-id="685b3-134">Croatian (hr)</span></span> 
* <span data-ttu-id="685b3-135">Czech (cs)</span><span class="sxs-lookup"><span data-stu-id="685b3-135">Czech (cs)</span></span> 
* <span data-ttu-id="685b3-136">Danish (da)</span><span class="sxs-lookup"><span data-stu-id="685b3-136">Danish (da)</span></span> 
* <span data-ttu-id="685b3-137">Dutch (nl)</span><span class="sxs-lookup"><span data-stu-id="685b3-137">Dutch (nl)</span></span> 
* <span data-ttu-id="685b3-138">English (en)</span><span class="sxs-lookup"><span data-stu-id="685b3-138">English (en)</span></span> 
* <span data-ttu-id="685b3-139">Finnish (fi)</span><span class="sxs-lookup"><span data-stu-id="685b3-139">Finnish (fi)</span></span> 
* <span data-ttu-id="685b3-140">French (fr)</span><span class="sxs-lookup"><span data-stu-id="685b3-140">French (fr)</span></span> 
* <span data-ttu-id="685b3-141">German (de)</span><span class="sxs-lookup"><span data-stu-id="685b3-141">German (de)</span></span> 
* <span data-ttu-id="685b3-142">Greek (el)</span><span class="sxs-lookup"><span data-stu-id="685b3-142">Greek (el)</span></span> 
* <span data-ttu-id="685b3-143">Hebrew (he)</span><span class="sxs-lookup"><span data-stu-id="685b3-143">Hebrew (he)</span></span> 
* <span data-ttu-id="685b3-144">Hindi (hi)</span><span class="sxs-lookup"><span data-stu-id="685b3-144">Hindi (hi)</span></span> 
* <span data-ttu-id="685b3-145">Hungarian (hu)</span><span class="sxs-lookup"><span data-stu-id="685b3-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="685b3-146">Indonesian (id)</span><span class="sxs-lookup"><span data-stu-id="685b3-146">Indonesian (id)</span></span> 
* <span data-ttu-id="685b3-147">Italian (it)</span><span class="sxs-lookup"><span data-stu-id="685b3-147">Italian (it)</span></span> 
* <span data-ttu-id="685b3-148">Japanese (ja)</span><span class="sxs-lookup"><span data-stu-id="685b3-148">Japanese (ja)</span></span> 
* <span data-ttu-id="685b3-149">Korean (ko)</span><span class="sxs-lookup"><span data-stu-id="685b3-149">Korean (ko)</span></span> 
* <span data-ttu-id="685b3-150">Latvian (lv)</span><span class="sxs-lookup"><span data-stu-id="685b3-150">Latvian (lv)</span></span> 
* <span data-ttu-id="685b3-151">Lithuanian (lt)</span><span class="sxs-lookup"><span data-stu-id="685b3-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="685b3-152">Malay (macrolanguage) (ms)</span><span class="sxs-lookup"><span data-stu-id="685b3-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="685b3-153">Norwegian Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="685b3-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="685b3-154">Polish (pl)</span><span class="sxs-lookup"><span data-stu-id="685b3-154">Polish (pl)</span></span> 
* <span data-ttu-id="685b3-155">Portuguese (pt)</span><span class="sxs-lookup"><span data-stu-id="685b3-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="685b3-156">Romanian (ro)</span><span class="sxs-lookup"><span data-stu-id="685b3-156">Romanian (ro)</span></span> 
* <span data-ttu-id="685b3-157">Russian (ru)</span><span class="sxs-lookup"><span data-stu-id="685b3-157">Russian (ru)</span></span> 
* <span data-ttu-id="685b3-158">Serbian (sr)</span><span class="sxs-lookup"><span data-stu-id="685b3-158">Serbian (sr)</span></span> 
* <span data-ttu-id="685b3-159">Slovak (sk)</span><span class="sxs-lookup"><span data-stu-id="685b3-159">Slovak (sk)</span></span> 
* <span data-ttu-id="685b3-160">Slovenian (sl)</span><span class="sxs-lookup"><span data-stu-id="685b3-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="685b3-161">Spanish (es)</span><span class="sxs-lookup"><span data-stu-id="685b3-161">Spanish (es)</span></span> 
* <span data-ttu-id="685b3-162">Swedish (sv)</span><span class="sxs-lookup"><span data-stu-id="685b3-162">Swedish (sv)</span></span> 
* <span data-ttu-id="685b3-163">Tagalog (tl)</span><span class="sxs-lookup"><span data-stu-id="685b3-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="685b3-164">Thai (th)</span><span class="sxs-lookup"><span data-stu-id="685b3-164">Thai (th)</span></span> 
* <span data-ttu-id="685b3-165">Turkish (tr)</span><span class="sxs-lookup"><span data-stu-id="685b3-165">Turkish (tr)</span></span> 
* <span data-ttu-id="685b3-166">Ukrainian (uk)</span><span class="sxs-lookup"><span data-stu-id="685b3-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="685b3-167">Vietnamese (vi)</span><span class="sxs-lookup"><span data-stu-id="685b3-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="685b3-168">Campaign</span><span class="sxs-lookup"><span data-stu-id="685b3-168">Campaign</span></span>
<span data-ttu-id="685b3-169">You can use the Campaign section to set the name and category of your campaign as well as if you plan to ignore the audience section of a Push campaign and send this campaign via the Reach API (and some elements with the low level Push API) instead.</span><span class="sxs-lookup"><span data-stu-id="685b3-169">You can use the Campaign section to set the name and category of your campaign as well as if you plan to ignore the audience section of a Push campaign and send this campaign via the Reach API (and some elements with the low level Push API) instead.</span></span> <span data-ttu-id="685b3-170">Categories can be used with a custom notification template to control in-app notifications based on predefined settings.</span><span class="sxs-lookup"><span data-stu-id="685b3-170">Categories can be used with a custom notification template to control in-app notifications based on predefined settings.</span></span> <span data-ttu-id="685b3-171">You can get a list of your existing “Categories” via the Reach API.</span><span class="sxs-lookup"><span data-stu-id="685b3-171">You can get a list of your existing “Categories” via the Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="685b3-172">If you use the "Ignore Audience, push will be sent to users via the API" option in the "Campaign" section of a Reach campaign, the campaign will NOT automatically send, you will need to send it manually via the Reach API.</span><span class="sxs-lookup"><span data-stu-id="685b3-172">If you use the "Ignore Audience, push will be sent to users via the API" option in the "Campaign" section of a Reach campaign, the campaign will NOT automatically send, you will need to send it manually via the Reach API.</span></span>

![Reach-Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="685b3-174">Option Applies to:</span><span class="sxs-lookup"><span data-stu-id="685b3-174">Option Applies to:</span></span>
* <span data-ttu-id="685b3-175">Name:    All</span><span class="sxs-lookup"><span data-stu-id="685b3-175">Name:    All</span></span>
* <span data-ttu-id="685b3-176">Category:    Announcements, Polls</span><span class="sxs-lookup"><span data-stu-id="685b3-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="685b3-177">Ignore Audience, push will be sent to users via the API:    All</span><span class="sxs-lookup"><span data-stu-id="685b3-177">Ignore Audience, push will be sent to users via the API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="685b3-178">Notification</span><span class="sxs-lookup"><span data-stu-id="685b3-178">Notification</span></span>
<span data-ttu-id="685b3-179">You can use the Notification section to set basic settings for your push including: The title of the Push, the message, an in-app image, or if it is dismissible.</span><span class="sxs-lookup"><span data-stu-id="685b3-179">You can use the Notification section to set basic settings for your push including: The title of the Push, the message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="685b3-180">Many notification settings are specific to the platform of your device.</span><span class="sxs-lookup"><span data-stu-id="685b3-180">Many notification settings are specific to the platform of your device.</span></span> <span data-ttu-id="685b3-181">You can select whether your push will be sent "in app" or "out of app" or both.</span><span class="sxs-lookup"><span data-stu-id="685b3-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="685b3-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at the Operating System level on their devices, and Azure Mobile Engagement will not be able to override this setting.</span><span class="sxs-lookup"><span data-stu-id="685b3-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at the Operating System level on their devices, and Azure Mobile Engagement will not be able to override this setting.</span></span> <span data-ttu-id="685b3-183">Also remember that the Reach API handles "in app" and "out of app" Pushes.</span><span class="sxs-lookup"><span data-stu-id="685b3-183">Also remember that the Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="685b3-184">The Push API can be used to handle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or to another location in your App (Android SDK 2.1.0 or later intent categories required).</span><span class="sxs-lookup"><span data-stu-id="685b3-184">The Push API can be used to handle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or to another location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="685b3-185">You can change the icon or iOS badge, and send either text or web content (a popup with html content, URL link to another location either inside or outside of the app).</span><span class="sxs-lookup"><span data-stu-id="685b3-185">You can change the icon or iOS badge, and send either text or web content (a popup with html content, URL link to another location either inside or outside of the app).</span></span> <span data-ttu-id="685b3-186">You can also make Android devices ring or vibrate with the Push.</span><span class="sxs-lookup"><span data-stu-id="685b3-186">You can also make Android devices ring or vibrate with the Push.</span></span> <span data-ttu-id="685b3-187">(Remember that you will need the correct SDK permissions in your Android manifest file to ring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span><span class="sxs-lookup"><span data-stu-id="685b3-187">(Remember that you will need the correct SDK permissions in your Android manifest file to ring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="685b3-188">Delivery Types:</span><span class="sxs-lookup"><span data-stu-id="685b3-188">Delivery Types:</span></span>
* <span data-ttu-id="685b3-189">Out of app only: the notification will be delivered when the user does not use the application.</span><span class="sxs-lookup"><span data-stu-id="685b3-189">Out of app only: the notification will be delivered when the user does not use the application.</span></span>
* <span data-ttu-id="685b3-190">The out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span><span class="sxs-lookup"><span data-stu-id="685b3-190">The out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="685b3-191">In-app only: The notification appears only when the application is running.</span><span class="sxs-lookup"><span data-stu-id="685b3-191">In-app only: The notification appears only when the application is running.</span></span>
* <span data-ttu-id="685b3-192">The notification uses the Capptain delivery system to reach the user.</span><span class="sxs-lookup"><span data-stu-id="685b3-192">The notification uses the Capptain delivery system to reach the user.</span></span> <span data-ttu-id="685b3-193">You can fully customize the visual layout/display of your push.</span><span class="sxs-lookup"><span data-stu-id="685b3-193">You can fully customize the visual layout/display of your push.</span></span>
* <span data-ttu-id="685b3-194">Anytime: This option ensures that you send a notification either the application is running or not.</span><span class="sxs-lookup"><span data-stu-id="685b3-194">Anytime: This option ensures that you send a notification either the application is running or not.</span></span>

![Reach-Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="685b3-196">Option Applies to:</span><span class="sxs-lookup"><span data-stu-id="685b3-196">Option Applies to:</span></span>
* <span data-ttu-id="685b3-197">Notification:     Announcements, Polls</span><span class="sxs-lookup"><span data-stu-id="685b3-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="685b3-198">Content</span><span class="sxs-lookup"><span data-stu-id="685b3-198">Content</span></span>
<span data-ttu-id="685b3-199">You can use the Content section to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span><span class="sxs-lookup"><span data-stu-id="685b3-199">You can use the Content section to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="685b3-200">The Content setting of Push campaigns is specific to the type of campaign.</span><span class="sxs-lookup"><span data-stu-id="685b3-200">The Content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="685b3-201">See also</span><span class="sxs-lookup"><span data-stu-id="685b3-201">See also</span></span>
* <span data-ttu-id="685b3-202">[UI Documentation - Reach - Push Content][Link 29]</span><span class="sxs-lookup"><span data-stu-id="685b3-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach-Campaign5][24]

## <a name="audience"></a><span data-ttu-id="685b3-204">Audience</span><span class="sxs-lookup"><span data-stu-id="685b3-204">Audience</span></span>
<span data-ttu-id="685b3-205">You can use the Audience section to define a standard list of items to limit your campaign or limits your campaign based on customized criteria.</span><span class="sxs-lookup"><span data-stu-id="685b3-205">You can use the Audience section to define a standard list of items to limit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="685b3-206">The standard set of options to Limit your Audience allows you to push to either new or old users or native push users only.</span><span class="sxs-lookup"><span data-stu-id="685b3-206">The standard set of options to Limit your Audience allows you to push to either new or old users or native push users only.</span></span> <span data-ttu-id="685b3-207">You can also set a quota to limit the number of users who receive the push.</span><span class="sxs-lookup"><span data-stu-id="685b3-207">You can also set a quota to limit the number of users who receive the push.</span></span> <span data-ttu-id="685b3-208">You can manually Edit the expression for how your campaign is filtered to include one or more criterion to target users.</span><span class="sxs-lookup"><span data-stu-id="685b3-208">You can manually Edit the expression for how your campaign is filtered to include one or more criterion to target users.</span></span> <span data-ttu-id="685b3-209">You can manually type an audience expression.</span><span class="sxs-lookup"><span data-stu-id="685b3-209">You can manually type an audience expression.</span></span> <span data-ttu-id="685b3-210">Such an expression must explicitly define the relation between criteria.</span><span class="sxs-lookup"><span data-stu-id="685b3-210">Such an expression must explicitly define the relation between criteria.</span></span> <span data-ttu-id="685b3-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span><span class="sxs-lookup"><span data-stu-id="685b3-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="685b3-212">The relation between the criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span><span class="sxs-lookup"><span data-stu-id="685b3-212">The relation between the criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="685b3-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span><span class="sxs-lookup"><span data-stu-id="685b3-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="685b3-214">With a large audience included in campaigns, the server side targeting scan can be slow, especially if you attempt to start multiple campaigns at the same time.</span><span class="sxs-lookup"><span data-stu-id="685b3-214">With a large audience included in campaigns, the server side targeting scan can be slow, especially if you attempt to start multiple campaigns at the same time.</span></span>

* <span data-ttu-id="685b3-215">If possible, only start one campaign at a time.</span><span class="sxs-lookup"><span data-stu-id="685b3-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="685b3-216">At the most, only start four campaigns at a time.</span><span class="sxs-lookup"><span data-stu-id="685b3-216">At the most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="685b3-217">Push only to your active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have the app installed and use it will need to be scanned.</span><span class="sxs-lookup"><span data-stu-id="685b3-217">Push only to your active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have the app installed and use it will need to be scanned.</span></span>
  <span data-ttu-id="685b3-218">Once your audience is defined, you can use the simulate button to find out how many users will receive this Push.</span><span class="sxs-lookup"><span data-stu-id="685b3-218">Once your audience is defined, you can use the simulate button to find out how many users will receive this Push.</span></span> <span data-ttu-id="685b3-219">This will compute the number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span><span class="sxs-lookup"><span data-stu-id="685b3-219">This will compute the number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="685b3-220">Be aware that users who have uninstalled the application are also part of this audience, but cannot be reached.</span><span class="sxs-lookup"><span data-stu-id="685b3-220">Be aware that users who have uninstalled the application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="685b3-221">See also</span><span class="sxs-lookup"><span data-stu-id="685b3-221">See also</span></span>
* <span data-ttu-id="685b3-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span><span class="sxs-lookup"><span data-stu-id="685b3-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach-Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="685b3-224">Edit expression</span><span class="sxs-lookup"><span data-stu-id="685b3-224">Edit expression</span></span>
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="685b3-226">Limit your audience option applies to:</span><span class="sxs-lookup"><span data-stu-id="685b3-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="685b3-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span><span class="sxs-lookup"><span data-stu-id="685b3-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="685b3-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span><span class="sxs-lookup"><span data-stu-id="685b3-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="685b3-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span><span class="sxs-lookup"><span data-stu-id="685b3-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="685b3-230">Engage only idle users:    Announcements, Polls, Tiles</span><span class="sxs-lookup"><span data-stu-id="685b3-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="685b3-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span><span class="sxs-lookup"><span data-stu-id="685b3-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="685b3-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span><span class="sxs-lookup"><span data-stu-id="685b3-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="685b3-233">Time Frame</span><span class="sxs-lookup"><span data-stu-id="685b3-233">Time Frame</span></span>
<span data-ttu-id="685b3-234">You can use the Time Frame section to set when the push will be sent or you can leave the time frame blank to start the campaign immediately.</span><span class="sxs-lookup"><span data-stu-id="685b3-234">You can use the Time Frame section to set when the push will be sent or you can leave the time frame blank to start the campaign immediately.</span></span> <span data-ttu-id="685b3-235">Remember that using the end-users' time zone may start the campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in the world match the time frame set for your campaign.</span><span class="sxs-lookup"><span data-stu-id="685b3-235">Remember that using the end-users' time zone may start the campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in the world match the time frame set for your campaign.</span></span> <span data-ttu-id="685b3-236">Using the end users' time zone can also cause delays in campaigns since it has to request the time from the phone before starting the push.</span><span class="sxs-lookup"><span data-stu-id="685b3-236">Using the end users' time zone can also cause delays in campaigns since it has to request the time from the phone before starting the push.</span></span>

> [!NOTE]
> <span data-ttu-id="685b3-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span><span class="sxs-lookup"><span data-stu-id="685b3-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="685b3-238">To avoid this behavior, specific an end time for campaigns.</span><span class="sxs-lookup"><span data-stu-id="685b3-238">To avoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="685b3-239">See also</span><span class="sxs-lookup"><span data-stu-id="685b3-239">See also</span></span>
* <span data-ttu-id="685b3-240">[Reach - How Tos – Scheduling][Link 3]</span><span class="sxs-lookup"><span data-stu-id="685b3-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="685b3-242">Settings Apply to:</span><span class="sxs-lookup"><span data-stu-id="685b3-242">Settings Apply to:</span></span>
* <span data-ttu-id="685b3-243">Time frame:     Announcements, Polls, Tiles</span><span class="sxs-lookup"><span data-stu-id="685b3-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="685b3-244">Test</span><span class="sxs-lookup"><span data-stu-id="685b3-244">Test</span></span>
<span data-ttu-id="685b3-245">You can use the Test section to send this push to your own test device before saving the campaign.</span><span class="sxs-lookup"><span data-stu-id="685b3-245">You can use the Test section to send this push to your own test device before saving the campaign.</span></span> <span data-ttu-id="685b3-246">If you have configured any custom languages for this campaign, you can test the push in each language.</span><span class="sxs-lookup"><span data-stu-id="685b3-246">If you have configured any custom languages for this campaign, you can test the push in each language.</span></span> <span data-ttu-id="685b3-247">You can setup a test device from “My Account”.</span><span class="sxs-lookup"><span data-stu-id="685b3-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="685b3-248">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span><span class="sxs-lookup"><span data-stu-id="685b3-248">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="685b3-249">See also</span><span class="sxs-lookup"><span data-stu-id="685b3-249">See also</span></span>
* <span data-ttu-id="685b3-250">[UI Documentation - My Account][Link 14]</span><span class="sxs-lookup"><span data-stu-id="685b3-250">[UI Documentation - My Account][Link 14]</span></span>

![Reach-Campaign9][28]

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

























































