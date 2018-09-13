---
title: How to Use the Engagement API on Windows Phone Silverlight
description: How to Use the Engagement API on Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: ec8b6c13ea052c8063dfde4321cdd286ab6cb817
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549072"
---
# <a name="how-to-use-the-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="3b674-103">How to Use the Engagement API on Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="3b674-103">How to Use the Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="3b674-104">This document is an add-on to the document [How to integrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="3b674-104">This document is an add-on to the document [How to integrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="3b674-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span><span class="sxs-lookup"><span data-stu-id="3b674-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="3b674-106">If you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` class.</span><span class="sxs-lookup"><span data-stu-id="3b674-106">If you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="3b674-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span><span class="sxs-lookup"><span data-stu-id="3b674-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="3b674-108">The Engagement API is provided by the `EngagementAgent` class.</span><span class="sxs-lookup"><span data-stu-id="3b674-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="3b674-109">You can access to those methods through `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="3b674-109">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="3b674-110">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span><span class="sxs-lookup"><span data-stu-id="3b674-110">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="3b674-111">Engagement concepts</span><span class="sxs-lookup"><span data-stu-id="3b674-111">Engagement concepts</span></span>
<span data-ttu-id="3b674-112">The following parts refine the Mobile Engagement Concepts for the Windows Phone platform.</span><span class="sxs-lookup"><span data-stu-id="3b674-112">The following parts refine the Mobile Engagement Concepts for the Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="3b674-113">`Session` and `Activity`</span><span class="sxs-lookup"><span data-stu-id="3b674-113">`Session` and `Activity`</span></span>
<span data-ttu-id="3b674-114">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span><span class="sxs-lookup"><span data-stu-id="3b674-114">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="3b674-115">But *activities* can also be controlled manually by using the Engagement API.</span><span class="sxs-lookup"><span data-stu-id="3b674-115">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="3b674-116">This allows to split a given page in several sub parts to get more details about the usage of this page (for example to known how often and how long dialogs are used inside this page).</span><span class="sxs-lookup"><span data-stu-id="3b674-116">This allows to split a given page in several sub parts to get more details about the usage of this page (for example to known how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="3b674-117">Reporting Activities</span><span class="sxs-lookup"><span data-stu-id="3b674-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="3b674-118">User starts a new Activity</span><span class="sxs-lookup"><span data-stu-id="3b674-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-119">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3b674-120">You need to call `StartActivity()` each time the user activity changes.</span><span class="sxs-lookup"><span data-stu-id="3b674-120">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="3b674-121">The first call to this function starts a new user session.</span><span class="sxs-lookup"><span data-stu-id="3b674-121">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b674-122">The SDK automatically call the EndActivity method when the application is closed.</span><span class="sxs-lookup"><span data-stu-id="3b674-122">The SDK automatically call the EndActivity method when the application is closed.</span></span> <span data-ttu-id="3b674-123">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user change, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span><span class="sxs-lookup"><span data-stu-id="3b674-123">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user change, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="3b674-124">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="3b674-125">User ends his current Activity</span><span class="sxs-lookup"><span data-stu-id="3b674-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-126">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="3b674-127">You need to call `EndActivity()` at least once when the user finishes his last activity.</span><span class="sxs-lookup"><span data-stu-id="3b674-127">You need to call `EndActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="3b674-128">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `StartActivity()` before the session timeout expires, the session is simply continued).</span><span class="sxs-lookup"><span data-stu-id="3b674-128">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `StartActivity()` before the session timeout expires, the session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="3b674-129">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="3b674-130">Reporting Jobs</span><span class="sxs-lookup"><span data-stu-id="3b674-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="3b674-131">Start a job</span><span class="sxs-lookup"><span data-stu-id="3b674-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-132">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3b674-133">You can use the job to track certains tasks over a period of time.</span><span class="sxs-lookup"><span data-stu-id="3b674-133">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="3b674-134">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-134">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="3b674-135">End a job</span><span class="sxs-lookup"><span data-stu-id="3b674-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-136">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="3b674-137">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span><span class="sxs-lookup"><span data-stu-id="3b674-137">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="3b674-138">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-138">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="3b674-139">Reporting Events</span><span class="sxs-lookup"><span data-stu-id="3b674-139">Reporting Events</span></span>
<span data-ttu-id="3b674-140">There is three types of events :</span><span class="sxs-lookup"><span data-stu-id="3b674-140">There is three types of events :</span></span>

* <span data-ttu-id="3b674-141">Standalone events</span><span class="sxs-lookup"><span data-stu-id="3b674-141">Standalone events</span></span>
* <span data-ttu-id="3b674-142">Session events</span><span class="sxs-lookup"><span data-stu-id="3b674-142">Session events</span></span>
* <span data-ttu-id="3b674-143">Job events</span><span class="sxs-lookup"><span data-stu-id="3b674-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="3b674-144">Standalone Events</span><span class="sxs-lookup"><span data-stu-id="3b674-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-145">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3b674-146">Standalone events can occur outside of the context of a session.</span><span class="sxs-lookup"><span data-stu-id="3b674-146">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="3b674-147">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="3b674-148">Session events</span><span class="sxs-lookup"><span data-stu-id="3b674-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-149">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3b674-150">Session events are usually used to report the actions performed by a user during his session.</span><span class="sxs-lookup"><span data-stu-id="3b674-150">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="3b674-151">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-151">Example</span></span>
<span data-ttu-id="3b674-152">**Without data :**</span><span class="sxs-lookup"><span data-stu-id="3b674-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="3b674-153">**With data :**</span><span class="sxs-lookup"><span data-stu-id="3b674-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="3b674-154">Job Events</span><span class="sxs-lookup"><span data-stu-id="3b674-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-155">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="3b674-156">Job events are usually used to report the actions performed by a user during a Job.</span><span class="sxs-lookup"><span data-stu-id="3b674-156">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="3b674-157">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="3b674-158">Reporting Errors</span><span class="sxs-lookup"><span data-stu-id="3b674-158">Reporting Errors</span></span>
<span data-ttu-id="3b674-159">There is three types of errors :</span><span class="sxs-lookup"><span data-stu-id="3b674-159">There is three types of errors :</span></span>

* <span data-ttu-id="3b674-160">Standalone errors</span><span class="sxs-lookup"><span data-stu-id="3b674-160">Standalone errors</span></span>
* <span data-ttu-id="3b674-161">Session errors</span><span class="sxs-lookup"><span data-stu-id="3b674-161">Session errors</span></span>
* <span data-ttu-id="3b674-162">Job errors</span><span class="sxs-lookup"><span data-stu-id="3b674-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="3b674-163">Standalone errors</span><span class="sxs-lookup"><span data-stu-id="3b674-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-164">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3b674-165">Contrary to session errors, standalone errors can occur outside of the context of a session.</span><span class="sxs-lookup"><span data-stu-id="3b674-165">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="3b674-166">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="3b674-167">Session errors</span><span class="sxs-lookup"><span data-stu-id="3b674-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-168">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="3b674-169">Session errors are usually used to report the errors impacting the user during his session.</span><span class="sxs-lookup"><span data-stu-id="3b674-169">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="3b674-170">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="3b674-171">Job Errors</span><span class="sxs-lookup"><span data-stu-id="3b674-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-172">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="3b674-173">Errors can be related to a running job instead of being related to the current user session.</span><span class="sxs-lookup"><span data-stu-id="3b674-173">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="3b674-174">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="3b674-175">Reporting Crashes</span><span class="sxs-lookup"><span data-stu-id="3b674-175">Reporting Crashes</span></span>
<span data-ttu-id="3b674-176">The agent provides two methods to deal with crashes.</span><span class="sxs-lookup"><span data-stu-id="3b674-176">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="3b674-177">Send an exception</span><span class="sxs-lookup"><span data-stu-id="3b674-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-178">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="3b674-179">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-179">Example</span></span>
<span data-ttu-id="3b674-180">You can send an exception at any time by calling :</span><span class="sxs-lookup"><span data-stu-id="3b674-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="3b674-181">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span><span class="sxs-lookup"><span data-stu-id="3b674-181">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="3b674-182">To do so, call :</span><span class="sxs-lookup"><span data-stu-id="3b674-182">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="3b674-183">If you do that, the session and jobs will be closed just after sending the crash.</span><span class="sxs-lookup"><span data-stu-id="3b674-183">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="3b674-184">Send an unhandled exception</span><span class="sxs-lookup"><span data-stu-id="3b674-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="3b674-185">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="3b674-186">Engagement also provides a method to send unhandled exceptions.</span><span class="sxs-lookup"><span data-stu-id="3b674-186">Engagement also provides a method to send unhandled exceptions.</span></span> <span data-ttu-id="3b674-187">This is especially useful when used inside the silverlight UnhandledException event handler.</span><span class="sxs-lookup"><span data-stu-id="3b674-187">This is especially useful when used inside the silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="3b674-188">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span><span class="sxs-lookup"><span data-stu-id="3b674-188">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="3b674-189">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-189">Example</span></span>
<span data-ttu-id="3b674-190">You can use it to implement your own UnhandledException handler (especially if you have disabled the automatic crash reporting feature of Engagement).</span><span class="sxs-lookup"><span data-stu-id="3b674-190">You can use it to implement your own UnhandledException handler (especially if you have disabled the automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="3b674-191">For example, in the `Application_UnhandledException` method of the `App.xaml.cs` file :</span><span class="sxs-lookup"><span data-stu-id="3b674-191">For example, in the `Application_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="3b674-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="3b674-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="3b674-193">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="3b674-194">When the user navigates forward, away from an application, after the Deactivated event is raised, the operating system will attempt to put the application into a dormant state.</span><span class="sxs-lookup"><span data-stu-id="3b674-194">When the user navigates forward, away from an application, after the Deactivated event is raised, the operating system will attempt to put the application into a dormant state.</span></span> <span data-ttu-id="3b674-195">Then, the application is Tombstoning.</span><span class="sxs-lookup"><span data-stu-id="3b674-195">Then, the application is Tombstoning.</span></span> <span data-ttu-id="3b674-196">In this process an application is terminated but some data about the state of the application and the individual pages within the application is preserved.</span><span class="sxs-lookup"><span data-stu-id="3b674-196">In this process an application is terminated but some data about the state of the application and the individual pages within the application is preserved.</span></span>

<span data-ttu-id="3b674-197">You have to insert `EngagementAgent.Instance.OnActivated(e)` in the `Application_Activated` method from the App.xaml.cs file to reset the Engagement Agent when the application has been Tombstoned.</span><span class="sxs-lookup"><span data-stu-id="3b674-197">You have to insert `EngagementAgent.Instance.OnActivated(e)` in the `Application_Activated` method from the App.xaml.cs file to reset the Engagement Agent when the application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="3b674-198">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code to execute when the application is activated (brought to foreground)
            // This code will not execute when the application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="3b674-199">Device Id</span><span class="sxs-lookup"><span data-stu-id="3b674-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="3b674-200">You can get the engagement device id by calling this method.</span><span class="sxs-lookup"><span data-stu-id="3b674-200">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="3b674-201">Extras parameters</span><span class="sxs-lookup"><span data-stu-id="3b674-201">Extras parameters</span></span>
<span data-ttu-id="3b674-202">Arbitrary data can be attached to an event, an error, an activity or a job.</span><span class="sxs-lookup"><span data-stu-id="3b674-202">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="3b674-203">These data can be structured using a dictionary.</span><span class="sxs-lookup"><span data-stu-id="3b674-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="3b674-204">Keys and values can be of any type.</span><span class="sxs-lookup"><span data-stu-id="3b674-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="3b674-205">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span><span class="sxs-lookup"><span data-stu-id="3b674-205">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="3b674-206">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-206">Example</span></span>
<span data-ttu-id="3b674-207">We create a new class "Person".</span><span class="sxs-lookup"><span data-stu-id="3b674-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="3b674-208">Then, we will add a `Person` instance to an extra.</span><span class="sxs-lookup"><span data-stu-id="3b674-208">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="3b674-209">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span><span class="sxs-lookup"><span data-stu-id="3b674-209">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="3b674-210">Limits</span><span class="sxs-lookup"><span data-stu-id="3b674-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3b674-211">Keys</span><span class="sxs-lookup"><span data-stu-id="3b674-211">Keys</span></span>
<span data-ttu-id="3b674-212">Each key in the object must match the following regular expression:</span><span class="sxs-lookup"><span data-stu-id="3b674-212">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="3b674-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span><span class="sxs-lookup"><span data-stu-id="3b674-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3b674-214">Size</span><span class="sxs-lookup"><span data-stu-id="3b674-214">Size</span></span>
<span data-ttu-id="3b674-215">Extras are limited to **1024** characters per call.</span><span class="sxs-lookup"><span data-stu-id="3b674-215">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="3b674-216">Reporting Application Information</span><span class="sxs-lookup"><span data-stu-id="3b674-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="3b674-217">Reference</span><span class="sxs-lookup"><span data-stu-id="3b674-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="3b674-218">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span><span class="sxs-lookup"><span data-stu-id="3b674-218">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="3b674-219">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span><span class="sxs-lookup"><span data-stu-id="3b674-219">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="3b674-220">Like event extras, use a Dictionary\<object, object\> to attach informations.</span><span class="sxs-lookup"><span data-stu-id="3b674-220">Like event extras, use a Dictionary\<object, object\> to attach informations.</span></span>

### <a name="example"></a><span data-ttu-id="3b674-221">Example</span><span class="sxs-lookup"><span data-stu-id="3b674-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="3b674-222">Limits</span><span class="sxs-lookup"><span data-stu-id="3b674-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3b674-223">Keys</span><span class="sxs-lookup"><span data-stu-id="3b674-223">Keys</span></span>
<span data-ttu-id="3b674-224">Each key in the object must match the following regular expression:</span><span class="sxs-lookup"><span data-stu-id="3b674-224">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="3b674-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span><span class="sxs-lookup"><span data-stu-id="3b674-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3b674-226">Size</span><span class="sxs-lookup"><span data-stu-id="3b674-226">Size</span></span>
<span data-ttu-id="3b674-227">Application information are limited to **1024** characters per call.</span><span class="sxs-lookup"><span data-stu-id="3b674-227">Application information are limited to **1024** characters per call.</span></span>

<span data-ttu-id="3b674-228">In the previous example, the JSON sent to the server is 44 characters long:</span><span class="sxs-lookup"><span data-stu-id="3b674-228">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="3b674-229">Logging</span><span class="sxs-lookup"><span data-stu-id="3b674-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="3b674-230">Enable Logging</span><span class="sxs-lookup"><span data-stu-id="3b674-230">Enable Logging</span></span>
<span data-ttu-id="3b674-231">The SDK can be configured to produce test logs in the IDE console.</span><span class="sxs-lookup"><span data-stu-id="3b674-231">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="3b674-232">These logs are not activated by default.</span><span class="sxs-lookup"><span data-stu-id="3b674-232">These logs are not activated by default.</span></span> <span data-ttu-id="3b674-233">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span><span class="sxs-lookup"><span data-stu-id="3b674-233">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
