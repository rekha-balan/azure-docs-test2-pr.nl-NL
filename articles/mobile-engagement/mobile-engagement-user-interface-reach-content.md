---
title: Azure Mobile Engagement User Interface - Reach Content
description: Learn how to manage the unique content of the different types of push notification campaigns in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: ''
author: piyushjo
manager: erikre
editor: ''
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 498e176efc8c78a54858eb4a8f6b8d1d48e7a379
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556313"
---
# <a name="how-to-manage-the-unique-content-of-the-different-types-of-push-notification-campaigns"></a><span data-ttu-id="30fbd-103">How to manage the unique content of the different types of push notification campaigns</span><span class="sxs-lookup"><span data-stu-id="30fbd-103">How to manage the unique content of the different types of push notification campaigns</span></span>
<span data-ttu-id="30fbd-104">You can use the Content section of a new reach campaign to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span><span class="sxs-lookup"><span data-stu-id="30fbd-104">You can use the Content section of a new reach campaign to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="30fbd-105">The content setting of Push campaigns is specific to the type of campaign.</span><span class="sxs-lookup"><span data-stu-id="30fbd-105">The content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="30fbd-106">Content types:</span><span class="sxs-lookup"><span data-stu-id="30fbd-106">Content types:</span></span>
* <span data-ttu-id="30fbd-107">Announcements</span><span class="sxs-lookup"><span data-stu-id="30fbd-107">Announcements</span></span>
* <span data-ttu-id="30fbd-108">Polls</span><span class="sxs-lookup"><span data-stu-id="30fbd-108">Polls</span></span>
* <span data-ttu-id="30fbd-109">Data pushes</span><span class="sxs-lookup"><span data-stu-id="30fbd-109">Data pushes</span></span>
* <span data-ttu-id="30fbd-110">Tiles (Windows Phone Only)</span><span class="sxs-lookup"><span data-stu-id="30fbd-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="30fbd-111">Content of Announcements</span><span class="sxs-lookup"><span data-stu-id="30fbd-111">Content of Announcements</span></span>
 ![Reach-Content1][30] 

### <a name="choose-the-type-of-your-announcement"></a><span data-ttu-id="30fbd-113">Choose the type of your announcement:</span><span class="sxs-lookup"><span data-stu-id="30fbd-113">Choose the type of your announcement:</span></span>
* <span data-ttu-id="30fbd-114">Notification only: It is a simple standard notification.</span><span class="sxs-lookup"><span data-stu-id="30fbd-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="30fbd-115">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span><span class="sxs-lookup"><span data-stu-id="30fbd-115">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="30fbd-116">Text announcement: It is a notification that engages the user to have a look at a text view.</span><span class="sxs-lookup"><span data-stu-id="30fbd-116">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="30fbd-117">Web announcement: It is a notification that engages the user to have a look at a web view.</span><span class="sxs-lookup"><span data-stu-id="30fbd-117">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="30fbd-118">See also</span><span class="sxs-lookup"><span data-stu-id="30fbd-118">See also</span></span>
* <span data-ttu-id="30fbd-119">[Reach - How Tos - Announcements][Link 3]</span><span class="sxs-lookup"><span data-stu-id="30fbd-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="30fbd-120">About Web View Announcements:</span><span class="sxs-lookup"><span data-stu-id="30fbd-120">About Web View Announcements:</span></span>
<span data-ttu-id="30fbd-121">Occurrences of the pattern "{deviceid}" in the HTML code or JavaScript code you provide here will be automatically replaced by the identifier of the device displaying the announcement.</span><span class="sxs-lookup"><span data-stu-id="30fbd-121">Occurrences of the pattern "{deviceid}" in the HTML code or JavaScript code you provide here will be automatically replaced by the identifier of the device displaying the announcement.</span></span> <span data-ttu-id="30fbd-122">This is an easy way to retrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span><span class="sxs-lookup"><span data-stu-id="30fbd-122">This is an easy way to retrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="30fbd-123">If you want to create a full screen web view (without the default Action and Exit buttons we provide) you can use the following functions from your web view announcement's JavaScript code:</span><span class="sxs-lookup"><span data-stu-id="30fbd-123">If you want to create a full screen web view (without the default Action and Exit buttons we provide) you can use the following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="30fbd-124">perform the announcement action: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="30fbd-124">perform the announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="30fbd-125">exit from the announcement: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="30fbd-125">exit from the announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="30fbd-126">Choose your Action:</span><span class="sxs-lookup"><span data-stu-id="30fbd-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="30fbd-127">About Action URLs:</span><span class="sxs-lookup"><span data-stu-id="30fbd-127">About Action URLs:</span></span>
<span data-ttu-id="30fbd-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span><span class="sxs-lookup"><span data-stu-id="30fbd-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="30fbd-129">Any dedicated URL that your application might support (e.g. to make users jump to a particular screen) can also be used as an action URL.</span><span class="sxs-lookup"><span data-stu-id="30fbd-129">Any dedicated URL that your application might support (e.g. to make users jump to a particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="30fbd-130">Each occurrence of the {deviceid} pattern is automatically replaced by the identifier of the device performing the action.</span><span class="sxs-lookup"><span data-stu-id="30fbd-130">Each occurrence of the {deviceid} pattern is automatically replaced by the identifier of the device performing the action.</span></span> <span data-ttu-id="30fbd-131">This can be used to easily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span><span class="sxs-lookup"><span data-stu-id="30fbd-131">This can be used to easily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="30fbd-132">**Android + iOS actions**</span><span class="sxs-lookup"><span data-stu-id="30fbd-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="30fbd-133">Open a web page</span><span class="sxs-lookup"><span data-stu-id="30fbd-133">Open a web page</span></span>
  * <span data-ttu-id="30fbd-134">http://\[web-site-domain\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="30fbd-135">Example:http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="30fbd-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="30fbd-136">Send an e-mail</span><span class="sxs-lookup"><span data-stu-id="30fbd-136">Send an e-mail</span></span>
  * <span data-ttu-id="30fbd-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="30fbd-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="30fbd-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="30fbd-139">Send a SMS</span><span class="sxs-lookup"><span data-stu-id="30fbd-139">Send a SMS</span></span>
  * <span data-ttu-id="30fbd-140">sms:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="30fbd-141">Example:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="30fbd-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="30fbd-142">Dial a phone number</span><span class="sxs-lookup"><span data-stu-id="30fbd-142">Dial a phone number</span></span>
  * <span data-ttu-id="30fbd-143">tel:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="30fbd-144">Example:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="30fbd-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="30fbd-145">**Android only actions**</span><span class="sxs-lookup"><span data-stu-id="30fbd-145">**Android only actions**</span></span>
  * <span data-ttu-id="30fbd-146">Download an application on the Play Store</span><span class="sxs-lookup"><span data-stu-id="30fbd-146">Download an application on the Play Store</span></span>
  * <span data-ttu-id="30fbd-147">market://details?id=\[app package\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="30fbd-148">Example:market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="30fbd-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="30fbd-149">Start a geo-localized search</span><span class="sxs-lookup"><span data-stu-id="30fbd-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="30fbd-150">geo:0,0?q=\[search query\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="30fbd-151">Example:geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="30fbd-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="30fbd-152">**iOS only actions**</span><span class="sxs-lookup"><span data-stu-id="30fbd-152">**iOS only actions**</span></span>
  * <span data-ttu-id="30fbd-153">Download an application on the App Store</span><span class="sxs-lookup"><span data-stu-id="30fbd-153">Download an application on the App Store</span></span>
  * <span data-ttu-id="30fbd-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span><span class="sxs-lookup"><span data-stu-id="30fbd-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="30fbd-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="30fbd-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="30fbd-156">Windows Actions</span><span class="sxs-lookup"><span data-stu-id="30fbd-156">Windows Actions</span></span>
  * <span data-ttu-id="30fbd-157">Open a web page</span><span class="sxs-lookup"><span data-stu-id="30fbd-157">Open a web page</span></span>
  * <span data-ttu-id="30fbd-158">http://\[web-site-domain\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="30fbd-159">Example:http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="30fbd-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="30fbd-160">Send an e-mail</span><span class="sxs-lookup"><span data-stu-id="30fbd-160">Send an e-mail</span></span>
  * <span data-ttu-id="30fbd-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="30fbd-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="30fbd-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="30fbd-163">Send a SMS (Skype Store App required)</span><span class="sxs-lookup"><span data-stu-id="30fbd-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="30fbd-164">sms:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="30fbd-165">Example:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="30fbd-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="30fbd-166">Dial a phone number (Skype Store App required)</span><span class="sxs-lookup"><span data-stu-id="30fbd-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="30fbd-167">tel:\[phone-number\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="30fbd-168">Example:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="30fbd-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="30fbd-169">Download an application on the Play Store</span><span class="sxs-lookup"><span data-stu-id="30fbd-169">Download an application on the Play Store</span></span>
  * <span data-ttu-id="30fbd-170">ms-windows-store:PDP?PFN=\[app package ID\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="30fbd-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="30fbd-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="30fbd-172">Start a bingmaps search</span><span class="sxs-lookup"><span data-stu-id="30fbd-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="30fbd-173">bingmaps:?q=\[search query\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="30fbd-174">Example:bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="30fbd-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="30fbd-175">Use a custom scheme</span><span class="sxs-lookup"><span data-stu-id="30fbd-175">Use a custom scheme</span></span>
  * <span data-ttu-id="30fbd-176">\[custom scheme\]://\[custom scheme params\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="30fbd-177">Example:myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="30fbd-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="30fbd-178">Use a package data (Store App for extension read required)</span><span class="sxs-lookup"><span data-stu-id="30fbd-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="30fbd-179">\[folder\]\[data\].\[extension\]</span><span class="sxs-lookup"><span data-stu-id="30fbd-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="30fbd-180">Example:myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="30fbd-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="30fbd-181">Build a Tracking URL:</span><span class="sxs-lookup"><span data-stu-id="30fbd-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="30fbd-182">See the “Settings” section of the <UI Documentation> for instruction on building a tracking URL that will allow users to download one of your other applications.</span><span class="sxs-lookup"><span data-stu-id="30fbd-182">See the “Settings” section of the <UI Documentation> for instruction on building a tracking URL that will allow users to download one of your other applications.</span></span>

### <a name="define-the-texts-of-your-announcement"></a><span data-ttu-id="30fbd-183">Define the texts of your announcement</span><span class="sxs-lookup"><span data-stu-id="30fbd-183">Define the texts of your announcement</span></span>
<span data-ttu-id="30fbd-184">Fill in the title, content, and button texts of your announcement.</span><span class="sxs-lookup"><span data-stu-id="30fbd-184">Fill in the title, content, and button texts of your announcement.</span></span> <span data-ttu-id="30fbd-185">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span><span class="sxs-lookup"><span data-stu-id="30fbd-185">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="30fbd-186">Audience targeting can be based on the feedback of whether this campaign was just pushed, replied, actioned, or exited.</span><span class="sxs-lookup"><span data-stu-id="30fbd-186">Audience targeting can be based on the feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="30fbd-187">See also</span><span class="sxs-lookup"><span data-stu-id="30fbd-187">See also</span></span>
* <span data-ttu-id="30fbd-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span><span class="sxs-lookup"><span data-stu-id="30fbd-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="30fbd-189">Content of Polls</span><span class="sxs-lookup"><span data-stu-id="30fbd-189">Content of Polls</span></span>
![Reach-Content2][31] 

<span data-ttu-id="30fbd-191">Fill in the title, description, and button texts of your announcement.</span><span class="sxs-lookup"><span data-stu-id="30fbd-191">Fill in the title, description, and button texts of your announcement.</span></span> <span data-ttu-id="30fbd-192">Then, add questions and choices for the answers to your questions.</span><span class="sxs-lookup"><span data-stu-id="30fbd-192">Then, add questions and choices for the answers to your questions.</span></span>
<span data-ttu-id="30fbd-193">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span><span class="sxs-lookup"><span data-stu-id="30fbd-193">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="30fbd-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span><span class="sxs-lookup"><span data-stu-id="30fbd-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="30fbd-195">Audience targeting can also be based on Poll answer feedback, where the question and answer choice are used as criteria.</span><span class="sxs-lookup"><span data-stu-id="30fbd-195">Audience targeting can also be based on Poll answer feedback, where the question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="30fbd-196">See also</span><span class="sxs-lookup"><span data-stu-id="30fbd-196">See also</span></span>
* <span data-ttu-id="30fbd-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span><span class="sxs-lookup"><span data-stu-id="30fbd-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="30fbd-198">Content of Data Pushes</span><span class="sxs-lookup"><span data-stu-id="30fbd-198">Content of Data Pushes</span></span>
![Reach-Content3][32] 

### <a name="choose-the-type-of-your-data"></a><span data-ttu-id="30fbd-200">Choose the type of your data:</span><span class="sxs-lookup"><span data-stu-id="30fbd-200">Choose the type of your data:</span></span>
* <span data-ttu-id="30fbd-201">Text</span><span class="sxs-lookup"><span data-stu-id="30fbd-201">Text</span></span>
* <span data-ttu-id="30fbd-202">Binary data</span><span class="sxs-lookup"><span data-stu-id="30fbd-202">Binary data</span></span>
* <span data-ttu-id="30fbd-203">Base64 data</span><span class="sxs-lookup"><span data-stu-id="30fbd-203">Base64 data</span></span>

### <a name="define-the-content-of-your-data"></a><span data-ttu-id="30fbd-204">Define the content of your data</span><span class="sxs-lookup"><span data-stu-id="30fbd-204">Define the content of your data</span></span>
* <span data-ttu-id="30fbd-205">If you selected to push text data, copy and paste the text into the "content" box.</span><span class="sxs-lookup"><span data-stu-id="30fbd-205">If you selected to push text data, copy and paste the text into the "content" box.</span></span>
* <span data-ttu-id="30fbd-206">If you selected to push either binary or base64 data, use the "upload your file" button to upload your file.</span><span class="sxs-lookup"><span data-stu-id="30fbd-206">If you selected to push either binary or base64 data, use the "upload your file" button to upload your file.</span></span>
* <span data-ttu-id="30fbd-207">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span><span class="sxs-lookup"><span data-stu-id="30fbd-207">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="30fbd-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span><span class="sxs-lookup"><span data-stu-id="30fbd-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="30fbd-209">See also</span><span class="sxs-lookup"><span data-stu-id="30fbd-209">See also</span></span>
* <span data-ttu-id="30fbd-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span><span class="sxs-lookup"><span data-stu-id="30fbd-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="30fbd-211">Content of Tiles (Windows Phone only)</span><span class="sxs-lookup"><span data-stu-id="30fbd-211">Content of Tiles (Windows Phone only)</span></span>
![Reach-Content4][33]

### <a name="define-the-content-of-your-tile"></a><span data-ttu-id="30fbd-213">Define the content of your tile</span><span class="sxs-lookup"><span data-stu-id="30fbd-213">Define the content of your tile</span></span>
<span data-ttu-id="30fbd-214">The tile payload is the text to be displayed in the tile of your app on Windows Phone devices.</span><span class="sxs-lookup"><span data-stu-id="30fbd-214">The tile payload is the text to be displayed in the tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="30fbd-215">A tile push is the Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="30fbd-215">A tile push is the Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="30fbd-216">The tile push type is the only push type that does not have a response and so the audience of future campaigns can't be built on the results of a tile push campaign.</span><span class="sxs-lookup"><span data-stu-id="30fbd-216">The tile push type is the only push type that does not have a response and so the audience of future campaigns can't be built on the results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="30fbd-217">See also</span><span class="sxs-lookup"><span data-stu-id="30fbd-217">See also</span></span>
* <span data-ttu-id="30fbd-218">[API Documentation - Reach API - Native Push][Link 4]</span><span class="sxs-lookup"><span data-stu-id="30fbd-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

























































