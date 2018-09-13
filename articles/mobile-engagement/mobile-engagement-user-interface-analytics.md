---
title: Azure Mobile Engagement User Interface - Analytics
description: Learn how to analyze historical data about your application using Azure Mobile Engagement
services: mobile-engagement
documentationcenter: ''
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 67d088654e9ebb6e2c118e14c87a3bbbffa63590
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553657"
---
# <a name="how-to-analyze-historical-data-about-your-application"></a><span data-ttu-id="56003-103">How to analyze historical data about your application</span><span class="sxs-lookup"><span data-stu-id="56003-103">How to analyze historical data about your application</span></span>
<span data-ttu-id="56003-104">This article describes the **ANALYTICS** tab of the **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="56003-104">This article describes the **ANALYTICS** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="56003-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span><span class="sxs-lookup"><span data-stu-id="56003-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="56003-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span><span class="sxs-lookup"><span data-stu-id="56003-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span>

<span data-ttu-id="56003-107">The Analytics section of the UI provides aggregated information about your application based on historic data that is updated every 24 hours.</span><span class="sxs-lookup"><span data-stu-id="56003-107">The Analytics section of the UI provides aggregated information about your application based on historic data that is updated every 24 hours.</span></span> <span data-ttu-id="56003-108">The information is displayed on different dashboards composed of line/bar/pie charts, grids, and maps.</span><span class="sxs-lookup"><span data-stu-id="56003-108">The information is displayed on different dashboards composed of line/bar/pie charts, grids, and maps.</span></span> <span data-ttu-id="56003-109">The data can also be downloaded as .csv files.</span><span class="sxs-lookup"><span data-stu-id="56003-109">The data can also be downloaded as .csv files.</span></span> <span data-ttu-id="56003-110">Most of this same information is available in real time in the Monitor section of the UI, and it can also be accessed from the Analytics API.</span><span class="sxs-lookup"><span data-stu-id="56003-110">Most of this same information is available in real time in the Monitor section of the UI, and it can also be accessed from the Analytics API.</span></span>

> [!NOTE]
> <span data-ttu-id="56003-111">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span><span class="sxs-lookup"><span data-stu-id="56003-111">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="56003-112">Press this button to get more contextual information about a section.</span><span class="sxs-lookup"><span data-stu-id="56003-112">Press this button to get more contextual information about a section.</span></span>

## <a name="standard-and-custom-analytics"></a><span data-ttu-id="56003-113">Standard and Custom Analytics</span><span class="sxs-lookup"><span data-stu-id="56003-113">Standard and Custom Analytics</span></span>
<span data-ttu-id="56003-114">Azure Mobile Engagement provides a set of basic, standard analytic information about your applications that can be graphed as soon as you integrate your app with the SDK.</span><span class="sxs-lookup"><span data-stu-id="56003-114">Azure Mobile Engagement provides a set of basic, standard analytic information about your applications that can be graphed as soon as you integrate your app with the SDK.</span></span> <span data-ttu-id="56003-115">Azure Mobile Engagement also provides the ability to gather additional custom analytics information that you want about your end-users' behavior.</span><span class="sxs-lookup"><span data-stu-id="56003-115">Azure Mobile Engagement also provides the ability to gather additional custom analytics information that you want about your end-users' behavior.</span></span> <span data-ttu-id="56003-116">You can do this by creating a tag plan of custom "Tags (app info)", created from **Settings** so that Azure Mobile Engagement can collect this additional data for you.</span><span class="sxs-lookup"><span data-stu-id="56003-116">You can do this by creating a tag plan of custom "Tags (app info)", created from **Settings** so that Azure Mobile Engagement can collect this additional data for you.</span></span>

## <a name="analytics"></a><span data-ttu-id="56003-117">Analytics</span><span class="sxs-lookup"><span data-stu-id="56003-117">Analytics</span></span>
* <span data-ttu-id="56003-118">Dashboard: Shows general information about your new and actives users and their trends.</span><span class="sxs-lookup"><span data-stu-id="56003-118">Dashboard: Shows general information about your new and actives users and their trends.</span></span>
* <span data-ttu-id="56003-119">Users: Users are identified by their device identifier: this identifier is unique for each device (one new user is actually one new device).</span><span class="sxs-lookup"><span data-stu-id="56003-119">Users: Users are identified by their device identifier: this identifier is unique for each device (one new user is actually one new device).</span></span> <span data-ttu-id="56003-120">A user is considered as new on a given time interval if he has performed his first session during this time interval.</span><span class="sxs-lookup"><span data-stu-id="56003-120">A user is considered as new on a given time interval if he has performed his first session during this time interval.</span></span> <span data-ttu-id="56003-121">A user is considered as retained if he has performed at least one session during the last 7 days.</span><span class="sxs-lookup"><span data-stu-id="56003-121">A user is considered as retained if he has performed at least one session during the last 7 days.</span></span> <span data-ttu-id="56003-122">Active Users are users that made at least one session during a given period.</span><span class="sxs-lookup"><span data-stu-id="56003-122">Active Users are users that made at least one session during a given period.</span></span> <span data-ttu-id="56003-123">You can sort by, monthly, weekly, daily, or hourly time periods.</span><span class="sxs-lookup"><span data-stu-id="56003-123">You can sort by, monthly, weekly, daily, or hourly time periods.</span></span> <span data-ttu-id="56003-124">All of the charts look similar but allow you to filter by different features, such as the version of your application, and then to sort by a period of time.</span><span class="sxs-lookup"><span data-stu-id="56003-124">All of the charts look similar but allow you to filter by different features, such as the version of your application, and then to sort by a period of time.</span></span> <span data-ttu-id="56003-125">The standard information gathered by integrating the SDK includes the following: Active users, new user, number of sessions, length of each session, technical information about the country, locals, location, language carrier, devices, firmware, network (WIFI), versions of the app and SDK, used by customers.</span><span class="sxs-lookup"><span data-stu-id="56003-125">The standard information gathered by integrating the SDK includes the following: Active users, new user, number of sessions, length of each session, technical information about the country, locals, location, language carrier, devices, firmware, network (WIFI), versions of the app and SDK, used by customers.</span></span> <span data-ttu-id="56003-126">This information can be viewed in real time from the monitor section.</span><span class="sxs-lookup"><span data-stu-id="56003-126">This information can be viewed in real time from the monitor section.</span></span>

> [!NOTE]
> <span data-ttu-id="56003-127">The time period is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span><span class="sxs-lookup"><span data-stu-id="56003-127">The time period is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span></span>

* <span data-ttu-id="56003-128">Retention: A user is considered as retained on a given time interval if he has performed his first session during this time interval.</span><span class="sxs-lookup"><span data-stu-id="56003-128">Retention: A user is considered as retained on a given time interval if he has performed his first session during this time interval.</span></span> <span data-ttu-id="56003-129">You can change the time intervals during which retained users (and new users) are counted to hours, days, weeks, or months.</span><span class="sxs-lookup"><span data-stu-id="56003-129">You can change the time intervals during which retained users (and new users) are counted to hours, days, weeks, or months.</span></span> <span data-ttu-id="56003-130">The user retention analytics is built on top of cohorts.</span><span class="sxs-lookup"><span data-stu-id="56003-130">The user retention analytics is built on top of cohorts.</span></span> <span data-ttu-id="56003-131">A cohort is the set of all the new users detected for a given period (i.e., the set of users performing their first session during this period).</span><span class="sxs-lookup"><span data-stu-id="56003-131">A cohort is the set of all the new users detected for a given period (i.e., the set of users performing their first session during this period).</span></span> <span data-ttu-id="56003-132">We use cohorts of 1-day, 2-day, 4-day, 7-day, or 1-month.</span><span class="sxs-lookup"><span data-stu-id="56003-132">We use cohorts of 1-day, 2-day, 4-day, 7-day, or 1-month.</span></span> <span data-ttu-id="56003-133">Given a cohort, every 1-day, 2-day, 4-day, 7-day, or 1-month, Azure Mobile Engagement computes the set of all users who belong to the cohort and are still active (i.e., the set of users who performed at least one session during the period).</span><span class="sxs-lookup"><span data-stu-id="56003-133">Given a cohort, every 1-day, 2-day, 4-day, 7-day, or 1-month, Azure Mobile Engagement computes the set of all users who belong to the cohort and are still active (i.e., the set of users who performed at least one session during the period).</span></span> <span data-ttu-id="56003-134">This set of users is called a cohort version.</span><span class="sxs-lookup"><span data-stu-id="56003-134">This set of users is called a cohort version.</span></span> <span data-ttu-id="56003-135">(Azure Mobile Engagement can show you how many of your users are still using your app, but only the platform specific store can tell you how many of your users uninstalled your app - for example, GooglePlay, iTunes, Windows Store, etc.).</span><span class="sxs-lookup"><span data-stu-id="56003-135">(Azure Mobile Engagement can show you how many of your users are still using your app, but only the platform specific store can tell you how many of your users uninstalled your app - for example, GooglePlay, iTunes, Windows Store, etc.).</span></span>
* <span data-ttu-id="56003-136">Sessions: One use of the application by a user.</span><span class="sxs-lookup"><span data-stu-id="56003-136">Sessions: One use of the application by a user.</span></span> <span data-ttu-id="56003-137">Sessions are generated from the sequence of activities performed by users (an activity is usually associated to the usage of one screen of the application, but this can vary depending on the way the SDK has been integrated in the application).</span><span class="sxs-lookup"><span data-stu-id="56003-137">Sessions are generated from the sequence of activities performed by users (an activity is usually associated to the usage of one screen of the application, but this can vary depending on the way the SDK has been integrated in the application).</span></span> <span data-ttu-id="56003-138">A user can only perform one activity at a time: a session starts as soon as the user starts his first activity and stops when he finishes his last activity.</span><span class="sxs-lookup"><span data-stu-id="56003-138">A user can only perform one activity at a time: a session starts as soon as the user starts his first activity and stops when he finishes his last activity.</span></span> <span data-ttu-id="56003-139">If a user stays more than a few seconds without performing any activity, then his sequence of activities is split into two distinct sessions.</span><span class="sxs-lookup"><span data-stu-id="56003-139">If a user stays more than a few seconds without performing any activity, then his sequence of activities is split into two distinct sessions.</span></span>
* <span data-ttu-id="56003-140">Activities: The names of each screen in your application and the length of time users spend on each screen.</span><span class="sxs-lookup"><span data-stu-id="56003-140">Activities: The names of each screen in your application and the length of time users spend on each screen.</span></span> <span data-ttu-id="56003-141">Activities are a custom analytic option that will correspond to the "app info" tags you have set up for your own app:</span><span class="sxs-lookup"><span data-stu-id="56003-141">Activities are a custom analytic option that will correspond to the "app info" tags you have set up for your own app:</span></span>
* <span data-ttu-id="56003-142">User Path:  Shows how your users navigate through your application's activities (screens).</span><span class="sxs-lookup"><span data-stu-id="56003-142">User Path:  Shows how your users navigate through your application's activities (screens).</span></span> <span data-ttu-id="56003-143">You can move the slider to adjust the level of details.</span><span class="sxs-lookup"><span data-stu-id="56003-143">You can move the slider to adjust the level of details.</span></span> <span data-ttu-id="56003-144">Blue nodes represent your application's activities.</span><span class="sxs-lookup"><span data-stu-id="56003-144">Blue nodes represent your application's activities.</span></span> <span data-ttu-id="56003-145">Their size is proportional to the time users spent in it.</span><span class="sxs-lookup"><span data-stu-id="56003-145">Their size is proportional to the time users spent in it.</span></span> <span data-ttu-id="56003-146">White nodes represent session start and stop.</span><span class="sxs-lookup"><span data-stu-id="56003-146">White nodes represent session start and stop.</span></span> <span data-ttu-id="56003-147">Red nodes represent crashes.</span><span class="sxs-lookup"><span data-stu-id="56003-147">Red nodes represent crashes.</span></span> <span data-ttu-id="56003-148">Links represent transitions between your application's activities (or between activities and crashes).</span><span class="sxs-lookup"><span data-stu-id="56003-148">Links represent transitions between your application's activities (or between activities and crashes).</span></span> <span data-ttu-id="56003-149">Click on a node or a link to display a tooltip with more information about your data: the time spent in a particular screen, the count of transitions, and the percentage of transitions from the source activity to the destination activity.</span><span class="sxs-lookup"><span data-stu-id="56003-149">Click on a node or a link to display a tooltip with more information about your data: the time spent in a particular screen, the count of transitions, and the percentage of transitions from the source activity to the destination activity.</span></span> <span data-ttu-id="56003-150">(A ---60% ---> B means that users being on activity A goes to activity B 60% of the time.) You can reorganize the graph as you want to clarify it; its position is saved every time you make a change.</span><span class="sxs-lookup"><span data-stu-id="56003-150">(A ---60% ---> B means that users being on activity A goes to activity B 60% of the time.) You can reorganize the graph as you want to clarify it; its position is saved every time you make a change.</span></span> <span data-ttu-id="56003-151">You can show or hide the crashes to lighten the graph.</span><span class="sxs-lookup"><span data-stu-id="56003-151">You can show or hide the crashes to lighten the graph.</span></span>
* <span data-ttu-id="56003-152">Events: Specific actions taken by a user in the application.</span><span class="sxs-lookup"><span data-stu-id="56003-152">Events: Specific actions taken by a user in the application.</span></span> <span data-ttu-id="56003-153">The distribution of events is shown as the count of events per user per session.</span><span class="sxs-lookup"><span data-stu-id="56003-153">The distribution of events is shown as the count of events per user per session.</span></span> <span data-ttu-id="56003-154">An event represents an instant action, for example, a click on a button or the reception of a notification.</span><span class="sxs-lookup"><span data-stu-id="56003-154">An event represents an instant action, for example, a click on a button or the reception of a notification.</span></span> <span data-ttu-id="56003-155">(The meaning of events depends on how the SDK has been integrated in the application.) An event can occur during a session or a job or can be stand alone.</span><span class="sxs-lookup"><span data-stu-id="56003-155">(The meaning of events depends on how the SDK has been integrated in the application.) An event can occur during a session or a job or can be stand alone.</span></span>
* <span data-ttu-id="56003-156">Jobs: Similar to events except they focus on the length of the action.</span><span class="sxs-lookup"><span data-stu-id="56003-156">Jobs: Similar to events except they focus on the length of the action.</span></span> <span data-ttu-id="56003-157">For example, Jobs could tell you technical information about how long it takes content to load or a call to web service.</span><span class="sxs-lookup"><span data-stu-id="56003-157">For example, Jobs could tell you technical information about how long it takes content to load or a call to web service.</span></span> <span data-ttu-id="56003-158">It could also show how long it takes a user to fill out a form, create an account, or make a purchase.</span><span class="sxs-lookup"><span data-stu-id="56003-158">It could also show how long it takes a user to fill out a form, create an account, or make a purchase.</span></span> <span data-ttu-id="56003-159">A job represents the duration of a task, for example, the duration of a download task or the time a banner is displayed on the screen.</span><span class="sxs-lookup"><span data-stu-id="56003-159">A job represents the duration of a task, for example, the duration of a download task or the time a banner is displayed on the screen.</span></span> <span data-ttu-id="56003-160">(The meaning of Jobs depends on how the SDK has been integrated in the application.) Jobs are usually associated with background tasks that are performed outside of the scope of a session (i.e., without any user activity).</span><span class="sxs-lookup"><span data-stu-id="56003-160">(The meaning of Jobs depends on how the SDK has been integrated in the application.) Jobs are usually associated with background tasks that are performed outside of the scope of a session (i.e., without any user activity).</span></span>
* <span data-ttu-id="56003-161">Technicals: Technical information about the devices of the users of your app that you can track, such as the Locale, Carrier, Network, Device, Firmware, and Screen size of the users' devices, and the Version of your App and the SDK version used in your app.</span><span class="sxs-lookup"><span data-stu-id="56003-161">Technicals: Technical information about the devices of the users of your app that you can track, such as the Locale, Carrier, Network, Device, Firmware, and Screen size of the users' devices, and the Version of your App and the SDK version used in your app.</span></span>
* <span data-ttu-id="56003-162">Errors: Information about technical errors inside the application that do not cause the application to crash.</span><span class="sxs-lookup"><span data-stu-id="56003-162">Errors: Information about technical errors inside the application that do not cause the application to crash.</span></span> <span data-ttu-id="56003-163">An error represents an instant issue, for example, a network failure or a bad manipulation.</span><span class="sxs-lookup"><span data-stu-id="56003-163">An error represents an instant issue, for example, a network failure or a bad manipulation.</span></span> <span data-ttu-id="56003-164">(The meaning of events depends on how the SDK has been integrated in the application.) An error can occur during a session or a job or can be stand alone.</span><span class="sxs-lookup"><span data-stu-id="56003-164">(The meaning of events depends on how the SDK has been integrated in the application.) An error can occur during a session or a job or can be stand alone.</span></span>
* <span data-ttu-id="56003-165">Crashes: Information about errors that cause your application to crash.</span><span class="sxs-lookup"><span data-stu-id="56003-165">Crashes: Information about errors that cause your application to crash.</span></span> <span data-ttu-id="56003-166">A crash is an unexpected condition where the application stops performing its expected functions and must be stopped.</span><span class="sxs-lookup"><span data-stu-id="56003-166">A crash is an unexpected condition where the application stops performing its expected functions and must be stopped.</span></span> <span data-ttu-id="56003-167">A crash is usually due to a bug in the application.</span><span class="sxs-lookup"><span data-stu-id="56003-167">A crash is usually due to a bug in the application.</span></span>

![Analytics2][11]

## <a name="accessing-the-retention-overview"></a><span data-ttu-id="56003-169">Accessing the Retention Overview</span><span class="sxs-lookup"><span data-stu-id="56003-169">Accessing the Retention Overview</span></span>
![Analytics3][12]

<span data-ttu-id="56003-171">The retention overview is broken down in the middle into several cards, each showing the overview for a certain retention period.</span><span class="sxs-lookup"><span data-stu-id="56003-171">The retention overview is broken down in the middle into several cards, each showing the overview for a certain retention period.</span></span> <span data-ttu-id="56003-172">The 2-day retention period is seen in the example.</span><span class="sxs-lookup"><span data-stu-id="56003-172">The 2-day retention period is seen in the example.</span></span> <span data-ttu-id="56003-173">The other cards show the 4-day and 7-day retention periods.</span><span class="sxs-lookup"><span data-stu-id="56003-173">The other cards show the 4-day and 7-day retention periods.</span></span>

## <a name="understanding-the-retention-overview-cards"></a><span data-ttu-id="56003-174">Understanding the Retention Overview cards</span><span class="sxs-lookup"><span data-stu-id="56003-174">Understanding the Retention Overview cards</span></span>
![Analytics4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a><span data-ttu-id="56003-176">Each card is composed of 3 main parts:</span><span class="sxs-lookup"><span data-stu-id="56003-176">Each card is composed of 3 main parts:</span></span>
1. <span data-ttu-id="56003-177">1: The cohort and the period considered</span><span class="sxs-lookup"><span data-stu-id="56003-177">1: The cohort and the period considered</span></span>
2. <span data-ttu-id="56003-178">2-4: The retention for the current period</span><span class="sxs-lookup"><span data-stu-id="56003-178">2-4: The retention for the current period</span></span>
3. <span data-ttu-id="56003-179">5: A Sparkline of the history</span><span class="sxs-lookup"><span data-stu-id="56003-179">5: A Sparkline of the history</span></span>

### <a name="here-is-detailed-information-about-each-element"></a><span data-ttu-id="56003-180">Here is detailed information about each element:</span><span class="sxs-lookup"><span data-stu-id="56003-180">Here is detailed information about each element:</span></span>
1. <span data-ttu-id="56003-181">Cohort and period: This headline gives the type of cohort.</span><span class="sxs-lookup"><span data-stu-id="56003-181">Cohort and period: This headline gives the type of cohort.</span></span> <span data-ttu-id="56003-182">Here "2-day period" means that we will look at the behavior of users over 2 days, Users that arrived over a period of 2 days, and whether they connect in the following blocks of 2 days.</span><span class="sxs-lookup"><span data-stu-id="56003-182">Here "2-day period" means that we will look at the behavior of users over 2 days, Users that arrived over a period of 2 days, and whether they connect in the following blocks of 2 days.</span></span> <span data-ttu-id="56003-183">The example above considers the activity of users between the 21st and 22nd of November.</span><span class="sxs-lookup"><span data-stu-id="56003-183">The example above considers the activity of users between the 21st and 22nd of November.</span></span>
2. <span data-ttu-id="56003-184">This gives the retention rate over the 21 and 22 of November for the users arriving in 19 and 20 of November.</span><span class="sxs-lookup"><span data-stu-id="56003-184">This gives the retention rate over the 21 and 22 of November for the users arriving in 19 and 20 of November.</span></span> <span data-ttu-id="56003-185">Here we had 1 active user between the 21st and 22nd, over the 3 that were new users between the 19th and 20th.</span><span class="sxs-lookup"><span data-stu-id="56003-185">Here we had 1 active user between the 21st and 22nd, over the 3 that were new users between the 19th and 20th.</span></span>
3. <span data-ttu-id="56003-186">This visual indicator gives the same information as above represented graphically.</span><span class="sxs-lookup"><span data-stu-id="56003-186">This visual indicator gives the same information as above represented graphically.</span></span> <span data-ttu-id="56003-187">(The third of the circle is from the 33% number.) The color gives additional information: Green indicates this number is growing from the previous calculation.</span><span class="sxs-lookup"><span data-stu-id="56003-187">(The third of the circle is from the 33% number.) The color gives additional information: Green indicates this number is growing from the previous calculation.</span></span> <span data-ttu-id="56003-188">Yellow means stable, and red means decreasing.</span><span class="sxs-lookup"><span data-stu-id="56003-188">Yellow means stable, and red means decreasing.</span></span>
4. <span data-ttu-id="56003-189">This indicates the values used for the calculation.</span><span class="sxs-lookup"><span data-stu-id="56003-189">This indicates the values used for the calculation.</span></span>
5. <span data-ttu-id="56003-190">This is a Sparkline of the history of the retention values.</span><span class="sxs-lookup"><span data-stu-id="56003-190">This is a Sparkline of the history of the retention values.</span></span> <span data-ttu-id="56003-191">It allows you to see the values in the past to have a broad view of how it evolved.</span><span class="sxs-lookup"><span data-stu-id="56003-191">It allows you to see the values in the past to have a broad view of how it evolved.</span></span>

## <a name="see-also"></a><span data-ttu-id="56003-192">See also</span><span class="sxs-lookup"><span data-stu-id="56003-192">See also</span></span>
* <span data-ttu-id="56003-193">[Concepts][Link 6]</span><span class="sxs-lookup"><span data-stu-id="56003-193">[Concepts][Link 6]</span></span>
* <span data-ttu-id="56003-194">[Troubleshooting Guide Service][Link 24]</span><span class="sxs-lookup"><span data-stu-id="56003-194">[Troubleshooting Guide Service][Link 24]</span></span>

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md
























































