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
# <a name="how-to-use-the-engagement-api-on-windows-phone-silverlight"></a>How to Use the Engagement API on Windows Phone Silverlight
This document is an add-on to the document [How to integrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md). It provides in depth details about how to use the Engagement API to report your application statistics.

If you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` class.

If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.

The Engagement API is provided by the `EngagementAgent` class. You can access to those methods through `EngagementAgent.Instance`.

Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.

## <a name="engagement-concepts"></a>Engagement concepts
The following parts refine the Mobile Engagement Concepts for the Windows Phone platform.

### <a name="session-and-activity"></a>`Session` and `Activity`
An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.

But *activities* can also be controlled manually by using the Engagement API. This allows to split a given page in several sub parts to get more details about the usage of this page (for example to known how often and how long dialogs are used inside this page).

## <a name="reporting-activities"></a>Reporting Activities
### <a name="user-starts-a-new-activity"></a>User starts a new Activity
#### <a name="reference"></a>Reference
            void StartActivity(string name, Dictionary<object, object> extras = null)

You need to call `StartActivity()` each time the user activity changes. The first call to this function starts a new user session.

> [!IMPORTANT]
> The SDK automatically call the EndActivity method when the application is closed. Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user change, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.
> 
> 

#### <a name="example"></a>Example
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>User ends his current Activity
#### <a name="reference"></a>Reference
            void EndActivity()

You need to call `EndActivity()` at least once when the user finishes his last activity. This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `StartActivity()` before the session timeout expires, the session is simply continued).

#### <a name="example"></a>Example
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>Reporting Jobs
### <a name="start-a-job"></a>Start a job
#### <a name="reference"></a>Reference
            void StartJob(string name, Dictionary<object, object> extras = null)

You can use the job to track certains tasks over a period of time.

#### <a name="example"></a>Example
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>End a job
#### <a name="reference"></a>Reference
            void EndJob(string name)

As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.

#### <a name="example"></a>Example
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>Reporting Events
There is three types of events :

* Standalone events
* Session events
* Job events

### <a name="standalone-events"></a>Standalone Events
#### <a name="reference"></a>Reference
            void SendEvent(string name, Dictionary<object, object> extras = null)

Standalone events can occur outside of the context of a session.

#### <a name="example"></a>Example
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>Session events
#### <a name="reference"></a>Reference
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

Session events are usually used to report the actions performed by a user during his session.

#### <a name="example"></a>Example
**Without data :**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**With data :**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>Job Events
#### <a name="reference"></a>Reference
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

Job events are usually used to report the actions performed by a user during a Job.

#### <a name="example"></a>Example
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>Reporting Errors
There is three types of errors :

* Standalone errors
* Session errors
* Job errors

### <a name="standalone-errors"></a>Standalone errors
#### <a name="reference"></a>Reference
            void SendError(string name, Dictionary<object, object> extras = null)

Contrary to session errors, standalone errors can occur outside of the context of a session.

#### <a name="example"></a>Example
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>Session errors
#### <a name="reference"></a>Reference
            void SendSessionError(string name, Dictionary<object, object> extras = null)

Session errors are usually used to report the errors impacting the user during his session.

#### <a name="example"></a>Example
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>Job Errors
#### <a name="reference"></a>Reference
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

Errors can be related to a running job instead of being related to the current user session.

#### <a name="example"></a>Example
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>Reporting Crashes
The agent provides two methods to deal with crashes.

### <a name="send-an-exception"></a>Send an exception
#### <a name="reference"></a>Reference
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>Example
You can send an exception at any time by calling :

            EngagementAgent.Instance.SendCrash(aCatchedException);

You can also use an optional parameter to terminate the engagement session at the same time than sending the crash. To do so, call :

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

If you do that, the session and jobs will be closed just after sending the crash.

### <a name="send-an-unhandled-exception"></a>Send an unhandled exception
#### <a name="reference"></a>Reference
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

Engagement also provides a method to send unhandled exceptions. This is especially useful when used inside the silverlight UnhandledException event handler.

This method will **ALWAYS** terminate the engagement session and jobs after being called.

#### <a name="example"></a>Example
You can use it to implement your own UnhandledException handler (especially if you have disabled the automatic crash reporting feature of Engagement). For example, in the `Application_UnhandledException` method of the `App.xaml.cs` file :

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a>OnActivated
### <a name="reference"></a>Reference
            void OnActivated(ActivatedEventArgs e)

When the user navigates forward, away from an application, after the Deactivated event is raised, the operating system will attempt to put the application into a dormant state. Then, the application is Tombstoning. In this process an application is terminated but some data about the state of the application and the individual pages within the application is preserved.

You have to insert `EngagementAgent.Instance.OnActivated(e)` in the `Application_Activated` method from the App.xaml.cs file to reset the Engagement Agent when the application has been Tombstoned.

### <a name="example"></a>Example
            // Inside your App.xaml.cs file

            // Code to execute when the application is activated (brought to foreground)
            // This code will not execute when the application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a>Device Id
            String GetDeviceId()

You can get the engagement device id by calling this method.

## <a name="extras-parameters"></a>Extras parameters
Arbitrary data can be attached to an event, an error, an activity or a job. These data can be structured using a dictionary. Keys and values can be of any type.

Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.

### <a name="example"></a>Example
We create a new class "Person".

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

Then, we will add a `Person` instance to an extra.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.
> 
> 

### <a name="limits"></a>Limits
#### <a name="keys"></a>Keys
Each key in the object must match the following regular expression:

`^[a-zA-Z][a-zA-Z_0-9]*$`

It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).

#### <a name="size"></a>Size
Extras are limited to **1024** characters per call.

## <a name="reporting-application-information"></a>Reporting Application Information
### <a name="reference"></a>Reference
            void SendAppInfo(Dictionary<object, object> appInfos)

You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.

Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device. Like event extras, use a Dictionary\<object, object\> to attach informations.

### <a name="example"></a>Example
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>Limits
#### <a name="keys"></a>Keys
Each key in the object must match the following regular expression:

`^[a-zA-Z][a-zA-Z_0-9]*$`

It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).

#### <a name="size"></a>Size
Application information are limited to **1024** characters per call.

In the previous example, the JSON sent to the server is 44 characters long:

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a>Logging
### <a name="enable-logging"></a>Enable Logging
The SDK can be configured to produce test logs in the IDE console.
These logs are not activated by default. To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
