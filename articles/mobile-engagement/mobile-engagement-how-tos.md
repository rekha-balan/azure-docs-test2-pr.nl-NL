---
title: Azure Mobile Engagement User Interface - Reach How To
description: User Interface Overview for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: ''
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0fd8fa2aa15450ef81bd4062c70b5f7fef5b8139
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555298"
---
# <a name="how-to-get-started-using-and-managing-pushes-to-reach-out-to-your-end-users"></a><span data-ttu-id="63545-103">How to get started using and managing pushes to reach out to your end users</span><span class="sxs-lookup"><span data-stu-id="63545-103">How to get started using and managing pushes to reach out to your end users</span></span>
<span data-ttu-id="63545-104">Once the SDK is fully integrated into your app, you can get started using the the Reach section of the UI to Push notifications to the users of your app.</span><span class="sxs-lookup"><span data-stu-id="63545-104">Once the SDK is fully integrated into your app, you can get started using the the Reach section of the UI to Push notifications to the users of your app.</span></span>  

## <a name="do-your-first-push-notification-campaign"></a><span data-ttu-id="63545-105">Do Your First Push Notification Campaign</span><span class="sxs-lookup"><span data-stu-id="63545-105">Do Your First Push Notification Campaign</span></span>
* <span data-ttu-id="63545-106">Confirm that your Reach is integrated into your app with the SDK.</span><span class="sxs-lookup"><span data-stu-id="63545-106">Confirm that your Reach is integrated into your app with the SDK.</span></span> 
* <span data-ttu-id="63545-107">Select your application</span><span class="sxs-lookup"><span data-stu-id="63545-107">Select your application</span></span>

![First1][1]

* <span data-ttu-id="63545-109">Go to the "Reach" Section and Click "New announcement"</span><span class="sxs-lookup"><span data-stu-id="63545-109">Go to the "Reach" Section and Click "New announcement"</span></span>

![First2][2]

* <span data-ttu-id="63545-111">Create a new campaign and name it</span><span class="sxs-lookup"><span data-stu-id="63545-111">Create a new campaign and name it</span></span>
  
![First3][3]

* <span data-ttu-id="63545-113">Select how the notification should be delivered, as In-app only</span><span class="sxs-lookup"><span data-stu-id="63545-113">Select how the notification should be delivered, as In-app only</span></span>

![First4][4]

* <span data-ttu-id="63545-115">Create the message you want to push</span><span class="sxs-lookup"><span data-stu-id="63545-115">Create the message you want to push</span></span>

![First5][5]

* <span data-ttu-id="63545-117">You may write a title on the notification (Optional).</span><span class="sxs-lookup"><span data-stu-id="63545-117">You may write a title on the notification (Optional).</span></span>
* <span data-ttu-id="63545-118">Write push message content.</span><span class="sxs-lookup"><span data-stu-id="63545-118">Write push message content.</span></span>
* <span data-ttu-id="63545-119">You can upload an image.</span><span class="sxs-lookup"><span data-stu-id="63545-119">You can upload an image.</span></span> <span data-ttu-id="63545-120">Be aware that the size of the file cannot exceed 32,768 bytes.</span><span class="sxs-lookup"><span data-stu-id="63545-120">Be aware that the size of the file cannot exceed 32,768 bytes.</span></span>
* <span data-ttu-id="63545-121">You also have the ability to select further options, but for the focus of this tutorial, we will see that later.</span><span class="sxs-lookup"><span data-stu-id="63545-121">You also have the ability to select further options, but for the focus of this tutorial, we will see that later.</span></span>
* <span data-ttu-id="63545-122">Select the content type as Notification only</span><span class="sxs-lookup"><span data-stu-id="63545-122">Select the content type as Notification only</span></span>

![First6][6]

* <span data-ttu-id="63545-124">Create your push campaign and it will appear in your campaign list.</span><span class="sxs-lookup"><span data-stu-id="63545-124">Create your push campaign and it will appear in your campaign list.</span></span>

![First7][7]

## <a name="test-your-push-notification-campaign"></a><span data-ttu-id="63545-126">Test Your Push Notification Campaign</span><span class="sxs-lookup"><span data-stu-id="63545-126">Test Your Push Notification Campaign</span></span>
![Test1][8]

* <span data-ttu-id="63545-128">Register your device.</span><span class="sxs-lookup"><span data-stu-id="63545-128">Register your device.</span></span>
* <span data-ttu-id="63545-129">Click on the checkbox of the device you want to push.</span><span class="sxs-lookup"><span data-stu-id="63545-129">Click on the checkbox of the device you want to push.</span></span>
* <span data-ttu-id="63545-130">Click on the "Test" button to send the push to the device.</span><span class="sxs-lookup"><span data-stu-id="63545-130">Click on the "Test" button to send the push to the device.</span></span>

![Test2][9]

* <span data-ttu-id="63545-132">Activate the campaign</span><span class="sxs-lookup"><span data-stu-id="63545-132">Activate the campaign</span></span>

![Test3][10]

* <span data-ttu-id="63545-134">Now that you have created your campaign you just need to activate it for the notification to be pushed to your users.</span><span class="sxs-lookup"><span data-stu-id="63545-134">Now that you have created your campaign you just need to activate it for the notification to be pushed to your users.</span></span>

## <a name="send-personalized-pushes"></a><span data-ttu-id="63545-135">Send Personalized Pushes</span><span class="sxs-lookup"><span data-stu-id="63545-135">Send Personalized Pushes</span></span>
* <span data-ttu-id="63545-136">This example creates a push where a custom rebate code is entered into the push notification.</span><span class="sxs-lookup"><span data-stu-id="63545-136">This example creates a push where a custom rebate code is entered into the push notification.</span></span>

![Personalize1][11]

<span data-ttu-id="63545-138">Personalization works by replacing a marker by from an app info tag so, you'll have to make sure the user has the proper app-info defined first.</span><span class="sxs-lookup"><span data-stu-id="63545-138">Personalization works by replacing a marker by from an app info tag so, you'll have to make sure the user has the proper app-info defined first.</span></span> <span data-ttu-id="63545-139">In this example the targeted users will have an app info tag named rebate_code defined.</span><span class="sxs-lookup"><span data-stu-id="63545-139">In this example the targeted users will have an app info tag named rebate_code defined.</span></span>
<span data-ttu-id="63545-140">As you see above the push notification content includes the marker ${rebate_code} which will indicate that it is to be replaced by the actual content of the app info tag.</span><span class="sxs-lookup"><span data-stu-id="63545-140">As you see above the push notification content includes the marker ${rebate_code} which will indicate that it is to be replaced by the actual content of the app info tag.</span></span>

> [!WARNING]
> <span data-ttu-id="63545-141">If the app info tag is not defined for the user, the user will not receive the push.</span><span class="sxs-lookup"><span data-stu-id="63545-141">If the app info tag is not defined for the user, the user will not receive the push.</span></span>

* <span data-ttu-id="63545-142">Result</span><span class="sxs-lookup"><span data-stu-id="63545-142">Result</span></span>

![Personalize2][12]

### <a name="you-can-further-personalize-the-text-your-notification"></a><span data-ttu-id="63545-144">You can further personalize the text your notification</span><span class="sxs-lookup"><span data-stu-id="63545-144">You can further personalize the text your notification</span></span>
![Personalize3][13]

* <span data-ttu-id="63545-146">Including the title of the notification,</span><span class="sxs-lookup"><span data-stu-id="63545-146">Including the title of the notification,</span></span>
* <span data-ttu-id="63545-147">And the content of the message.</span><span class="sxs-lookup"><span data-stu-id="63545-147">And the content of the message.</span></span>
* <span data-ttu-id="63545-148">Choose the type of announcement (Text view or Web view)</span><span class="sxs-lookup"><span data-stu-id="63545-148">Choose the type of announcement (Text view or Web view)</span></span>

![Personalize4][14]

### <a name="the-body-of-an-announcement-may-also-be-personalized-with"></a><span data-ttu-id="63545-150">The body of an announcement may also be personalized with:</span><span class="sxs-lookup"><span data-stu-id="63545-150">The body of an announcement may also be personalized with:</span></span>
* <span data-ttu-id="63545-151">The action URL, should you want to customize the landing page</span><span class="sxs-lookup"><span data-stu-id="63545-151">The action URL, should you want to customize the landing page</span></span>
* <span data-ttu-id="63545-152">The title,</span><span class="sxs-lookup"><span data-stu-id="63545-152">The title,</span></span>
* <span data-ttu-id="63545-153">The body of the message.</span><span class="sxs-lookup"><span data-stu-id="63545-153">The body of the message.</span></span>

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a><span data-ttu-id="63545-154">Differentiate Your Push Notification (in or out of app)</span><span class="sxs-lookup"><span data-stu-id="63545-154">Differentiate Your Push Notification (in or out of app)</span></span>
* <span data-ttu-id="63545-155">Choose the type of notification you will push, select your application, go to the "Reach" section, select or create a push campaign and go to the "Notification" section.</span><span class="sxs-lookup"><span data-stu-id="63545-155">Choose the type of notification you will push, select your application, go to the "Reach" section, select or create a push campaign and go to the "Notification" section.</span></span>
* <span data-ttu-id="63545-156">Click on the "delivery mode" you want.</span><span class="sxs-lookup"><span data-stu-id="63545-156">Click on the "delivery mode" you want.</span></span>
* <span data-ttu-id="63545-157">Click on the "Restrict Activities" checkbox when you want the notification occurs on specific activities (screens).</span><span class="sxs-lookup"><span data-stu-id="63545-157">Click on the "Restrict Activities" checkbox when you want the notification occurs on specific activities (screens).</span></span>

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a><span data-ttu-id="63545-159">"Out of App Only" delivery mode</span><span class="sxs-lookup"><span data-stu-id="63545-159">"Out of App Only" delivery mode</span></span>
![Differentiate2][16]

<span data-ttu-id="63545-161">"Out of App Only" delivery mode provides push notification when the application is closed.</span><span class="sxs-lookup"><span data-stu-id="63545-161">"Out of App Only" delivery mode provides push notification when the application is closed.</span></span> <span data-ttu-id="63545-162">This is the standard push notification.</span><span class="sxs-lookup"><span data-stu-id="63545-162">This is the standard push notification.</span></span>
<span data-ttu-id="63545-163">When you select "out of app only" ,you must have already provided the certificates from the platform that your application is building on (APNS or GCM).</span><span class="sxs-lookup"><span data-stu-id="63545-163">When you select "out of app only" ,you must have already provided the certificates from the platform that your application is building on (APNS or GCM).</span></span>

### <a name="see-also"></a><span data-ttu-id="63545-164">See also</span><span class="sxs-lookup"><span data-stu-id="63545-164">See also</span></span>
* <span data-ttu-id="63545-165">[Apple Push Notification Service – Certificates](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging – Certificate](http://developer.android.com/google/gcm/index.html)</span><span class="sxs-lookup"><span data-stu-id="63545-165">[Apple Push Notification Service – Certificates](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging – Certificate](http://developer.android.com/google/gcm/index.html)</span></span> 

### <a name="in-app-only-delivery-mode"></a><span data-ttu-id="63545-166">"in-App Only" delivery mode</span><span class="sxs-lookup"><span data-stu-id="63545-166">"in-App Only" delivery mode</span></span>
![Differentiate3][17]

<span data-ttu-id="63545-168">"In-App Only" delivery mode provides push notification when the application is running.</span><span class="sxs-lookup"><span data-stu-id="63545-168">"In-App Only" delivery mode provides push notification when the application is running.</span></span>
<span data-ttu-id="63545-169">For this notification, you do not need to go through the APNS and GCM system.</span><span class="sxs-lookup"><span data-stu-id="63545-169">For this notification, you do not need to go through the APNS and GCM system.</span></span>
<span data-ttu-id="63545-170">You can use the in-app delivery system to reach your end-users.</span><span class="sxs-lookup"><span data-stu-id="63545-170">You can use the in-app delivery system to reach your end-users.</span></span>
<span data-ttu-id="63545-171">You can fully customize the notification and decide in which activity (screen) the notification will appear.</span><span class="sxs-lookup"><span data-stu-id="63545-171">You can fully customize the notification and decide in which activity (screen) the notification will appear.</span></span>

### <a name="anytime-delivery-mode"></a><span data-ttu-id="63545-172">"Anytime" delivery mode</span><span class="sxs-lookup"><span data-stu-id="63545-172">"Anytime" delivery mode</span></span>
<span data-ttu-id="63545-173">You can choose an "Anytime" delivery mode, ensures you to reach your end-user whether the application is running or not.</span><span class="sxs-lookup"><span data-stu-id="63545-173">You can choose an "Anytime" delivery mode, ensures you to reach your end-user whether the application is running or not.</span></span>
<span data-ttu-id="63545-174">When you select "Anytime" , you must have already provided the certificates from the platform that your application is building upon (APNS or GCM).</span><span class="sxs-lookup"><span data-stu-id="63545-174">When you select "Anytime" , you must have already provided the certificates from the platform that your application is building upon (APNS or GCM).</span></span> 

## <a name="schedule-a-push-campaign"></a><span data-ttu-id="63545-175">Schedule a Push Campaign</span><span class="sxs-lookup"><span data-stu-id="63545-175">Schedule a Push Campaign</span></span>
### <a name="plan-to-start-a-campaign"></a><span data-ttu-id="63545-176">Plan to Start a campaign</span><span class="sxs-lookup"><span data-stu-id="63545-176">Plan to Start a campaign</span></span>
![Shedule1][18]

<span data-ttu-id="63545-178">It is the 21st of March and you have an announcement to make and planed for the 22nd of March at midnight.</span><span class="sxs-lookup"><span data-stu-id="63545-178">It is the 21st of March and you have an announcement to make and planed for the 22nd of March at midnight.</span></span> <span data-ttu-id="63545-179">You don’t have to stay in front of the interface to do a push!</span><span class="sxs-lookup"><span data-stu-id="63545-179">You don’t have to stay in front of the interface to do a push!</span></span> <span data-ttu-id="63545-180">You can plan in advance the exact minute notifications will be sent.</span><span class="sxs-lookup"><span data-stu-id="63545-180">You can plan in advance the exact minute notifications will be sent.</span></span>

* <span data-ttu-id="63545-181">Un-check the "None" checkbox and select a start time</span><span class="sxs-lookup"><span data-stu-id="63545-181">Un-check the "None" checkbox and select a start time</span></span> 
* <span data-ttu-id="63545-182">Choose the date and the time you want to start the push campaign.</span><span class="sxs-lookup"><span data-stu-id="63545-182">Choose the date and the time you want to start the push campaign.</span></span>

### <a name="plan-to-end-a-campaign"></a><span data-ttu-id="63545-183">Plan to end a campaign</span><span class="sxs-lookup"><span data-stu-id="63545-183">Plan to end a campaign</span></span>
![Shedule2][19]

<span data-ttu-id="63545-185">You want your campaign to stop on the 25th of March at 3.00 pm but you know you won't be there to do it.</span><span class="sxs-lookup"><span data-stu-id="63545-185">You want your campaign to stop on the 25th of March at 3.00 pm but you know you won't be there to do it.</span></span>
<span data-ttu-id="63545-186">You don’t have to stay in front of the interface to push!</span><span class="sxs-lookup"><span data-stu-id="63545-186">You don’t have to stay in front of the interface to push!</span></span> <span data-ttu-id="63545-187">You can plan in advance the exact minute your campaign will stop.</span><span class="sxs-lookup"><span data-stu-id="63545-187">You can plan in advance the exact minute your campaign will stop.</span></span>

* <span data-ttu-id="63545-188">Click on the "None" checkbox or select a end time</span><span class="sxs-lookup"><span data-stu-id="63545-188">Click on the "None" checkbox or select a end time</span></span>
* <span data-ttu-id="63545-189">Choose the date and the time you want to finish the push campaign.</span><span class="sxs-lookup"><span data-stu-id="63545-189">Choose the date and the time you want to finish the push campaign.</span></span>

### <a name="end-a-campaign-manually"></a><span data-ttu-id="63545-190">End a campaign manually</span><span class="sxs-lookup"><span data-stu-id="63545-190">End a campaign manually</span></span>
![Shedule3][20]

<span data-ttu-id="63545-192">By default, the "None" check-boxes are selected.</span><span class="sxs-lookup"><span data-stu-id="63545-192">By default, the "None" check-boxes are selected.</span></span>
<span data-ttu-id="63545-193">This means that the campaign will start as soon as you activate it in the reach section and will end when you will stop it on the reach section.</span><span class="sxs-lookup"><span data-stu-id="63545-193">This means that the campaign will start as soon as you activate it in the reach section and will end when you will stop it on the reach section.</span></span>

> [!NOTE]
> <span data-ttu-id="63545-194">Campaigns created without an end date store the push locally on the device and show it the next time the app is opened even if the campaign is manually ended.</span><span class="sxs-lookup"><span data-stu-id="63545-194">Campaigns created without an end date store the push locally on the device and show it the next time the app is opened even if the campaign is manually ended.</span></span>

## <a name="enhance-a-push-notification-with-a-text-view"></a><span data-ttu-id="63545-195">Enhance a Push Notification with a Text View</span><span class="sxs-lookup"><span data-stu-id="63545-195">Enhance a Push Notification with a Text View</span></span>
### <a name="what-is-a-text-view"></a><span data-ttu-id="63545-196">What is a Text View?</span><span class="sxs-lookup"><span data-stu-id="63545-196">What is a Text View?</span></span>
![TextView1][21]

<span data-ttu-id="63545-198">A text view is a pop-up with text content.</span><span class="sxs-lookup"><span data-stu-id="63545-198">A text view is a pop-up with text content.</span></span> <span data-ttu-id="63545-199">This pop-up appears after the end-user has clicked on the push notification.</span><span class="sxs-lookup"><span data-stu-id="63545-199">This pop-up appears after the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="63545-200">A text view allows you to present more content to your end-user.</span><span class="sxs-lookup"><span data-stu-id="63545-200">A text view allows you to present more content to your end-user.</span></span> <span data-ttu-id="63545-201">This is also the opportunity to present a call to action such as jumping to a page of your app, redirecting to a Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span><span class="sxs-lookup"><span data-stu-id="63545-201">This is also the opportunity to present a call to action such as jumping to a page of your app, redirecting to a Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-text-view"></a><span data-ttu-id="63545-202">Example: Text View</span><span class="sxs-lookup"><span data-stu-id="63545-202">Example: Text View</span></span>
* <span data-ttu-id="63545-203">Create your Push notification campaign in the "Reach" section and give your campaign a name</span><span class="sxs-lookup"><span data-stu-id="63545-203">Create your Push notification campaign in the "Reach" section and give your campaign a name</span></span>

![TextView2][22]

* <span data-ttu-id="63545-205">Write the message that will appear on the notification.</span><span class="sxs-lookup"><span data-stu-id="63545-205">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="63545-206">Select the Announcement Content Type of “text”</span><span class="sxs-lookup"><span data-stu-id="63545-206">Select the Announcement Content Type of “text”</span></span>

![TextView3][23]

> [!NOTE]
> <span data-ttu-id="63545-208">When you push a text view, it always comes with a notification first.</span><span class="sxs-lookup"><span data-stu-id="63545-208">When you push a text view, it always comes with a notification first.</span></span> 

* <span data-ttu-id="63545-209">Define the text (After having selected the text announcement content, the sub-section will appear, allowing you to define the text you want to be displayed.)</span><span class="sxs-lookup"><span data-stu-id="63545-209">Define the text (After having selected the text announcement content, the sub-section will appear, allowing you to define the text you want to be displayed.)</span></span>

![TextView4][24]

* <span data-ttu-id="63545-211">Write the title that will appear at the top of the message.</span><span class="sxs-lookup"><span data-stu-id="63545-211">Write the title that will appear at the top of the message.</span></span>
* <span data-ttu-id="63545-212">Write the main content of the text view.</span><span class="sxs-lookup"><span data-stu-id="63545-212">Write the main content of the text view.</span></span>
* <span data-ttu-id="63545-213">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to an App store or any kind of sources you can provide).</span><span class="sxs-lookup"><span data-stu-id="63545-213">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to an App store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="63545-214">Write the content that will appear on the exit button (by clicking on the exit button, the text view will disappear.)</span><span class="sxs-lookup"><span data-stu-id="63545-214">Write the content that will appear on the exit button (by clicking on the exit button, the text view will disappear.)</span></span>
* <span data-ttu-id="63545-215">Create your push notification campaign and it will appear on the campaign list.</span><span class="sxs-lookup"><span data-stu-id="63545-215">Create your push notification campaign and it will appear on the campaign list.</span></span>

![TextView5][25]

* <span data-ttu-id="63545-217">Activate your push notification campaign to send the text view to your users.</span><span class="sxs-lookup"><span data-stu-id="63545-217">Activate your push notification campaign to send the text view to your users.</span></span>

![TextView6][26]

* <span data-ttu-id="63545-219">Result</span><span class="sxs-lookup"><span data-stu-id="63545-219">Result</span></span>

![TextView7][27]

* <span data-ttu-id="63545-221">The user receives the notification and click on it.</span><span class="sxs-lookup"><span data-stu-id="63545-221">The user receives the notification and click on it.</span></span>
* <span data-ttu-id="63545-222">The text view appears as a pop-up allowing the user to interact with it.</span><span class="sxs-lookup"><span data-stu-id="63545-222">The text view appears as a pop-up allowing the user to interact with it.</span></span>

## <a name="enhance-a-push-notification-with-a-web-view"></a><span data-ttu-id="63545-223">Enhance a Push Notification with a Web View</span><span class="sxs-lookup"><span data-stu-id="63545-223">Enhance a Push Notification with a Web View</span></span>
### <a name="what-is-a-web-view"></a><span data-ttu-id="63545-224">What is a Web View?</span><span class="sxs-lookup"><span data-stu-id="63545-224">What is a Web View?</span></span>
![WebView1][28]

<span data-ttu-id="63545-226">A web view is a pop-up with web content.</span><span class="sxs-lookup"><span data-stu-id="63545-226">A web view is a pop-up with web content.</span></span> <span data-ttu-id="63545-227">This pop-up appears when the end-user has clicked on the push notification.</span><span class="sxs-lookup"><span data-stu-id="63545-227">This pop-up appears when the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="63545-228">A web view allows you to have more interaction with the end-user.</span><span class="sxs-lookup"><span data-stu-id="63545-228">A web view allows you to have more interaction with the end-user.</span></span>
<span data-ttu-id="63545-229">This is also the opportunity to present a call to action such as redirection to App Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span><span class="sxs-lookup"><span data-stu-id="63545-229">This is also the opportunity to present a call to action such as redirection to App Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-web-view"></a><span data-ttu-id="63545-230">Example: Web View</span><span class="sxs-lookup"><span data-stu-id="63545-230">Example: Web View</span></span>
* <span data-ttu-id="63545-231">Create your Push campaign in the "Reach" section and give your campaign a name.</span><span class="sxs-lookup"><span data-stu-id="63545-231">Create your Push campaign in the "Reach" section and give your campaign a name.</span></span>

![WebView2][29]

* <span data-ttu-id="63545-233">Write the message that will appear on the notification.</span><span class="sxs-lookup"><span data-stu-id="63545-233">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="63545-234">Select the Announcement Content Type as “web”</span><span class="sxs-lookup"><span data-stu-id="63545-234">Select the Announcement Content Type as “web”</span></span>

![WebView3][30]

### <a name="about-announcement-types"></a><span data-ttu-id="63545-236">About Announcement types:</span><span class="sxs-lookup"><span data-stu-id="63545-236">About Announcement types:</span></span>
* <span data-ttu-id="63545-237">Notification only: It is a simple standard notification.</span><span class="sxs-lookup"><span data-stu-id="63545-237">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="63545-238">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span><span class="sxs-lookup"><span data-stu-id="63545-238">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="63545-239">Text announcement: It is a notification that engages the user to have a look at a text view.</span><span class="sxs-lookup"><span data-stu-id="63545-239">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="63545-240">Web announcement: It is a notification that engages the user to have a look at a web view.</span><span class="sxs-lookup"><span data-stu-id="63545-240">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>
  <span data-ttu-id="63545-241">Select the "Web announcement" content.</span><span class="sxs-lookup"><span data-stu-id="63545-241">Select the "Web announcement" content.</span></span>

> [!NOTE]
> <span data-ttu-id="63545-242">When you push a web view, it always comes with a notification first.</span><span class="sxs-lookup"><span data-stu-id="63545-242">When you push a web view, it always comes with a notification first.</span></span>

* <span data-ttu-id="63545-243">Define the web content (After having selected the web announcement content, the subsection will appear, allowing you to define the web view content you want to be displayed.)</span><span class="sxs-lookup"><span data-stu-id="63545-243">Define the web content (After having selected the web announcement content, the subsection will appear, allowing you to define the web view content you want to be displayed.)</span></span>

![WebView4][31]

* <span data-ttu-id="63545-245">Write the title that will appear at the top of the message (optional).</span><span class="sxs-lookup"><span data-stu-id="63545-245">Write the title that will appear at the top of the message (optional).</span></span>
* <span data-ttu-id="63545-246">Write your HTML code here.</span><span class="sxs-lookup"><span data-stu-id="63545-246">Write your HTML code here.</span></span>
* <span data-ttu-id="63545-247">Click on the source editing mode button to switch edition and see how it looks like.</span><span class="sxs-lookup"><span data-stu-id="63545-247">Click on the source editing mode button to switch edition and see how it looks like.</span></span>
* <span data-ttu-id="63545-248">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to a Store or any kind of sources you can provide).</span><span class="sxs-lookup"><span data-stu-id="63545-248">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to a Store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="63545-249">Write the content that will appear on the exit button (by clicking on the exit button, the web view will disappear).</span><span class="sxs-lookup"><span data-stu-id="63545-249">Write the content that will appear on the exit button (by clicking on the exit button, the web view will disappear).</span></span>
* <span data-ttu-id="63545-250">Result</span><span class="sxs-lookup"><span data-stu-id="63545-250">Result</span></span>

![WebView5][32]

* <span data-ttu-id="63545-252">The user receive the notification and click on it.</span><span class="sxs-lookup"><span data-stu-id="63545-252">The user receive the notification and click on it.</span></span>
* <span data-ttu-id="63545-253">The text view appears as a pop-up allowing the user to interact with it.</span><span class="sxs-lookup"><span data-stu-id="63545-253">The text view appears as a pop-up allowing the user to interact with it.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/First1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/First2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/First3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/First4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/First5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/First6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/First7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Test1.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Test2.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Test3.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Personalize1.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Personalize2.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Personalize3.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Personalize4.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Differentiate1.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Differentiate2.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Differentiate3.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Schedule1.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Schedule2.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/Schedule3.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/TextView1.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/TextView2.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/TextView3.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/TextView4.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/TextView5.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/TextView6.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/TextView7.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/WebView1.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/WebView2.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/WebView3.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/WebView4.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-how-tos/WebView5.png

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

































