---
title: How to Use the Engagement API on Windows Universal
description: How to Use the Engagement API on Windows Universal
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 75fc134a5535e6113331470cf61df9c06eb8e2ab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549291"
---
# <a name="how-to-use-the-engagement-api-on-windows-universal"></a><span data-ttu-id="d11de-103">How to Use the Engagement API on Windows Universal</span><span class="sxs-lookup"><span data-stu-id="d11de-103">How to Use the Engagement API on Windows Universal</span></span>
<span data-ttu-id="d11de-104">This document is an add-on to the document [How to Integrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how to use the Engagement API to report your application statistics.</span><span class="sxs-lookup"><span data-stu-id="d11de-104">This document is an add-on to the document [How to Integrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="d11de-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Page` sub-classes inherit from the `EngagementPage` class.</span><span class="sxs-lookup"><span data-stu-id="d11de-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Page` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="d11de-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span><span class="sxs-lookup"><span data-stu-id="d11de-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="d11de-107">The Engagement API is provided by the `EngagementAgent` class.</span><span class="sxs-lookup"><span data-stu-id="d11de-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="d11de-108">You can access to those methods through `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="d11de-108">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="d11de-109">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span><span class="sxs-lookup"><span data-stu-id="d11de-109">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="d11de-110">Engagement concepts</span><span class="sxs-lookup"><span data-stu-id="d11de-110">Engagement concepts</span></span>
<span data-ttu-id="d11de-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the Windows Universal platform.</span><span class="sxs-lookup"><span data-stu-id="d11de-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="d11de-112">`Session` and `Activity`</span><span class="sxs-lookup"><span data-stu-id="d11de-112">`Session` and `Activity`</span></span>
<span data-ttu-id="d11de-113">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span><span class="sxs-lookup"><span data-stu-id="d11de-113">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="d11de-114">But *activities* can also be controlled manually by using the Engagement API.</span><span class="sxs-lookup"><span data-stu-id="d11de-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="d11de-115">This allows you to split a given page in several sub parts to get more details about the usage of this page (for example to know how often and how long dialogs are used inside this page).</span><span class="sxs-lookup"><span data-stu-id="d11de-115">This allows you to split a given page in several sub parts to get more details about the usage of this page (for example to know how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="d11de-116">Reporting Activities</span><span class="sxs-lookup"><span data-stu-id="d11de-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="d11de-117">User starts a new Activity</span><span class="sxs-lookup"><span data-stu-id="d11de-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-118">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d11de-119">You need to call `StartActivity()` each time the user activity changes.</span><span class="sxs-lookup"><span data-stu-id="d11de-119">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="d11de-120">The first call to this function starts a new user session.</span><span class="sxs-lookup"><span data-stu-id="d11de-120">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d11de-121">The SDK automatically calls the EndActivity method when the application is closed.</span><span class="sxs-lookup"><span data-stu-id="d11de-121">The SDK automatically calls the EndActivity method when the application is closed.</span></span> <span data-ttu-id="d11de-122">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user changes, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span><span class="sxs-lookup"><span data-stu-id="d11de-122">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user changes, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="d11de-123">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="d11de-124">User ends his current Activity</span><span class="sxs-lookup"><span data-stu-id="d11de-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-125">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="d11de-126">This ends the activity and the session.</span><span class="sxs-lookup"><span data-stu-id="d11de-126">This ends the activity and the session.</span></span> <span data-ttu-id="d11de-127">You should not call this method unless you really know what you're doing.</span><span class="sxs-lookup"><span data-stu-id="d11de-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="d11de-128">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="d11de-129">Reporting Jobs</span><span class="sxs-lookup"><span data-stu-id="d11de-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="d11de-130">Start a job</span><span class="sxs-lookup"><span data-stu-id="d11de-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-131">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d11de-132">You can use the job to track certains tasks over a period of time.</span><span class="sxs-lookup"><span data-stu-id="d11de-132">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="d11de-133">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-133">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="d11de-134">End a job</span><span class="sxs-lookup"><span data-stu-id="d11de-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-135">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="d11de-136">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span><span class="sxs-lookup"><span data-stu-id="d11de-136">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="d11de-137">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-137">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="d11de-138">Reporting Events</span><span class="sxs-lookup"><span data-stu-id="d11de-138">Reporting Events</span></span>
<span data-ttu-id="d11de-139">There is three types of events :</span><span class="sxs-lookup"><span data-stu-id="d11de-139">There is three types of events :</span></span>

* <span data-ttu-id="d11de-140">Standalone events</span><span class="sxs-lookup"><span data-stu-id="d11de-140">Standalone events</span></span>
* <span data-ttu-id="d11de-141">Session events</span><span class="sxs-lookup"><span data-stu-id="d11de-141">Session events</span></span>
* <span data-ttu-id="d11de-142">Job events</span><span class="sxs-lookup"><span data-stu-id="d11de-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="d11de-143">Standalone Events</span><span class="sxs-lookup"><span data-stu-id="d11de-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-144">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d11de-145">Standalone events can occur outside of the context of a session.</span><span class="sxs-lookup"><span data-stu-id="d11de-145">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="d11de-146">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="d11de-147">Session events</span><span class="sxs-lookup"><span data-stu-id="d11de-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-148">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d11de-149">Session events are usually used to report the actions performed by a user during his session.</span><span class="sxs-lookup"><span data-stu-id="d11de-149">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="d11de-150">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-150">Example</span></span>
<span data-ttu-id="d11de-151">**Without data :**</span><span class="sxs-lookup"><span data-stu-id="d11de-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="d11de-152">**With data :**</span><span class="sxs-lookup"><span data-stu-id="d11de-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="d11de-153">Job Events</span><span class="sxs-lookup"><span data-stu-id="d11de-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-154">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="d11de-155">Job events are usually used to report the actions performed by a user during a Job.</span><span class="sxs-lookup"><span data-stu-id="d11de-155">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="d11de-156">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="d11de-157">Reporting Errors</span><span class="sxs-lookup"><span data-stu-id="d11de-157">Reporting Errors</span></span>
<span data-ttu-id="d11de-158">There are three types of errors :</span><span class="sxs-lookup"><span data-stu-id="d11de-158">There are three types of errors :</span></span>

* <span data-ttu-id="d11de-159">Standalone errors</span><span class="sxs-lookup"><span data-stu-id="d11de-159">Standalone errors</span></span>
* <span data-ttu-id="d11de-160">Session errors</span><span class="sxs-lookup"><span data-stu-id="d11de-160">Session errors</span></span>
* <span data-ttu-id="d11de-161">Job errors</span><span class="sxs-lookup"><span data-stu-id="d11de-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="d11de-162">Standalone errors</span><span class="sxs-lookup"><span data-stu-id="d11de-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-163">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d11de-164">Contrary to session errors, standalone errors can occur outside of the context of a session.</span><span class="sxs-lookup"><span data-stu-id="d11de-164">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="d11de-165">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="d11de-166">Session errors</span><span class="sxs-lookup"><span data-stu-id="d11de-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-167">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="d11de-168">Session errors are usually used to report the errors impacting the user during his session.</span><span class="sxs-lookup"><span data-stu-id="d11de-168">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="d11de-169">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="d11de-170">Job Errors</span><span class="sxs-lookup"><span data-stu-id="d11de-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-171">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="d11de-172">Errors can be related to a running job instead of being related to the current user session.</span><span class="sxs-lookup"><span data-stu-id="d11de-172">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="d11de-173">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="d11de-174">Reporting Crashes</span><span class="sxs-lookup"><span data-stu-id="d11de-174">Reporting Crashes</span></span>
<span data-ttu-id="d11de-175">The agent provides two methods to deal with crashes.</span><span class="sxs-lookup"><span data-stu-id="d11de-175">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="d11de-176">Send an exception</span><span class="sxs-lookup"><span data-stu-id="d11de-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-177">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="d11de-178">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-178">Example</span></span>
<span data-ttu-id="d11de-179">You can send an exception at any time by calling :</span><span class="sxs-lookup"><span data-stu-id="d11de-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="d11de-180">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span><span class="sxs-lookup"><span data-stu-id="d11de-180">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="d11de-181">To do so, call :</span><span class="sxs-lookup"><span data-stu-id="d11de-181">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="d11de-182">If you do that, the session and jobs will be closed just after sending the crash.</span><span class="sxs-lookup"><span data-stu-id="d11de-182">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="d11de-183">Send an unhandled exception</span><span class="sxs-lookup"><span data-stu-id="d11de-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="d11de-184">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="d11de-185">Engagement also provides a method to send unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span><span class="sxs-lookup"><span data-stu-id="d11de-185">Engagement also provides a method to send unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="d11de-186">This is especially useful when used inside the application UnhandledException event handler.</span><span class="sxs-lookup"><span data-stu-id="d11de-186">This is especially useful when used inside the application UnhandledException event handler.</span></span>

<span data-ttu-id="d11de-187">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span><span class="sxs-lookup"><span data-stu-id="d11de-187">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="d11de-188">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-188">Example</span></span>
<span data-ttu-id="d11de-189">You can use it to implement your own UnhandledExceptionEventArgs handler.</span><span class="sxs-lookup"><span data-stu-id="d11de-189">You can use it to implement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="d11de-190">For example, add the `Current_UnhandledException` method of the `App.xaml.cs` file :</span><span class="sxs-lookup"><span data-stu-id="d11de-190">For example, add the `Current_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="d11de-191">In App.xaml.cs in "Public App(){}" add:</span><span class="sxs-lookup"><span data-stu-id="d11de-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="d11de-192">Device Id</span><span class="sxs-lookup"><span data-stu-id="d11de-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="d11de-193">You can get the engagement device id by calling this method.</span><span class="sxs-lookup"><span data-stu-id="d11de-193">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="d11de-194">Extras parameters</span><span class="sxs-lookup"><span data-stu-id="d11de-194">Extras parameters</span></span>
<span data-ttu-id="d11de-195">Arbitrary data can be attached to an event, an error, an activity or a job.</span><span class="sxs-lookup"><span data-stu-id="d11de-195">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="d11de-196">These data can be structured using a dictionary.</span><span class="sxs-lookup"><span data-stu-id="d11de-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="d11de-197">Keys and values can be of any type.</span><span class="sxs-lookup"><span data-stu-id="d11de-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="d11de-198">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span><span class="sxs-lookup"><span data-stu-id="d11de-198">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="d11de-199">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-199">Example</span></span>
<span data-ttu-id="d11de-200">We create a new class "Person".</span><span class="sxs-lookup"><span data-stu-id="d11de-200">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
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

<span data-ttu-id="d11de-201">Then, we will add a `Person` instance to an extra.</span><span class="sxs-lookup"><span data-stu-id="d11de-201">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="d11de-202">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span><span class="sxs-lookup"><span data-stu-id="d11de-202">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="d11de-203">Limits</span><span class="sxs-lookup"><span data-stu-id="d11de-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="d11de-204">Keys</span><span class="sxs-lookup"><span data-stu-id="d11de-204">Keys</span></span>
<span data-ttu-id="d11de-205">Each key in the object must match the following regular expression:</span><span class="sxs-lookup"><span data-stu-id="d11de-205">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="d11de-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span><span class="sxs-lookup"><span data-stu-id="d11de-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="d11de-207">Size</span><span class="sxs-lookup"><span data-stu-id="d11de-207">Size</span></span>
<span data-ttu-id="d11de-208">Extras are limited to **1024** characters per call.</span><span class="sxs-lookup"><span data-stu-id="d11de-208">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="d11de-209">Reporting Application Information</span><span class="sxs-lookup"><span data-stu-id="d11de-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="d11de-210">Reference</span><span class="sxs-lookup"><span data-stu-id="d11de-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="d11de-211">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span><span class="sxs-lookup"><span data-stu-id="d11de-211">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="d11de-212">Note that this data can be sent incrementally: only the latest value for a given key will be kept for a given device.</span><span class="sxs-lookup"><span data-stu-id="d11de-212">Note that this data can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="d11de-213">Like event extras, use a Dictionary\<object, object\> to attach data.</span><span class="sxs-lookup"><span data-stu-id="d11de-213">Like event extras, use a Dictionary\<object, object\> to attach data.</span></span>

### <a name="example"></a><span data-ttu-id="d11de-214">Example</span><span class="sxs-lookup"><span data-stu-id="d11de-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="d11de-215">Limits</span><span class="sxs-lookup"><span data-stu-id="d11de-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="d11de-216">Keys</span><span class="sxs-lookup"><span data-stu-id="d11de-216">Keys</span></span>
<span data-ttu-id="d11de-217">Each key in the object must match the following regular expression:</span><span class="sxs-lookup"><span data-stu-id="d11de-217">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="d11de-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span><span class="sxs-lookup"><span data-stu-id="d11de-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="d11de-219">Size</span><span class="sxs-lookup"><span data-stu-id="d11de-219">Size</span></span>
<span data-ttu-id="d11de-220">Application information is limited to **1024** characters per call.</span><span class="sxs-lookup"><span data-stu-id="d11de-220">Application information is limited to **1024** characters per call.</span></span>

<span data-ttu-id="d11de-221">In the previous example, the JSON sent to the server is 44 characters long:</span><span class="sxs-lookup"><span data-stu-id="d11de-221">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="d11de-222">Logging</span><span class="sxs-lookup"><span data-stu-id="d11de-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="d11de-223">Enable Logging</span><span class="sxs-lookup"><span data-stu-id="d11de-223">Enable Logging</span></span>
<span data-ttu-id="d11de-224">The SDK can be configured to produce test logs in the IDE console.</span><span class="sxs-lookup"><span data-stu-id="d11de-224">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="d11de-225">These logs are not activated by default.</span><span class="sxs-lookup"><span data-stu-id="d11de-225">These logs are not activated by default.</span></span> <span data-ttu-id="d11de-226">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span><span class="sxs-lookup"><span data-stu-id="d11de-226">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

