---
title: Azure Mobile Engagement Web SDK APIs | Microsoft Docs
description: The latest updates and procedures for the Web SDK for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: 54c22ce6a03e382b1bbde102bccc97deec249b30
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549644"
---
# <a name="use-the-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="03e1a-103">Use the Azure Mobile Engagement API in a web application</span><span class="sxs-lookup"><span data-stu-id="03e1a-103">Use the Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="03e1a-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="03e1a-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="03e1a-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span><span class="sxs-lookup"><span data-stu-id="03e1a-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span></span>

<span data-ttu-id="03e1a-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span><span class="sxs-lookup"><span data-stu-id="03e1a-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span></span> <span data-ttu-id="03e1a-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span><span class="sxs-lookup"><span data-stu-id="03e1a-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="03e1a-108">You can redefine this alias from the SDK configuration.</span><span class="sxs-lookup"><span data-stu-id="03e1a-108">You can redefine this alias from the SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="03e1a-109">Mobile Engagement concepts</span><span class="sxs-lookup"><span data-stu-id="03e1a-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="03e1a-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span><span class="sxs-lookup"><span data-stu-id="03e1a-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="03e1a-111">`Session` and `Activity`</span><span class="sxs-lookup"><span data-stu-id="03e1a-111">`Session` and `Activity`</span></span>
<span data-ttu-id="03e1a-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span><span class="sxs-lookup"><span data-stu-id="03e1a-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="03e1a-113">These few seconds are called the session timeout.</span><span class="sxs-lookup"><span data-stu-id="03e1a-113">These few seconds are called the session timeout.</span></span>

<span data-ttu-id="03e1a-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span><span class="sxs-lookup"><span data-stu-id="03e1a-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span> <span data-ttu-id="03e1a-115">This is called the server session timeout.</span><span class="sxs-lookup"><span data-stu-id="03e1a-115">This is called the server session timeout.</span></span>

### `Crash`
<span data-ttu-id="03e1a-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span><span class="sxs-lookup"><span data-stu-id="03e1a-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="03e1a-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span><span class="sxs-lookup"><span data-stu-id="03e1a-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="03e1a-118">Reporting activities</span><span class="sxs-lookup"><span data-stu-id="03e1a-118">Reporting activities</span></span>
<span data-ttu-id="03e1a-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span><span class="sxs-lookup"><span data-stu-id="03e1a-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="03e1a-120">User starts a new activity</span><span class="sxs-lookup"><span data-stu-id="03e1a-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="03e1a-121">You need to call `startActivity()` each time user activity changes.</span><span class="sxs-lookup"><span data-stu-id="03e1a-121">You need to call `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="03e1a-122">The first call to this function starts a new user session.</span><span class="sxs-lookup"><span data-stu-id="03e1a-122">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-the-current-activity"></a><span data-ttu-id="03e1a-123">User ends the current activity</span><span class="sxs-lookup"><span data-stu-id="03e1a-123">User ends the current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="03e1a-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span><span class="sxs-lookup"><span data-stu-id="03e1a-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span></span> <span data-ttu-id="03e1a-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span><span class="sxs-lookup"><span data-stu-id="03e1a-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span></span> <span data-ttu-id="03e1a-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span><span class="sxs-lookup"><span data-stu-id="03e1a-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span></span>

<span data-ttu-id="03e1a-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span><span class="sxs-lookup"><span data-stu-id="03e1a-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span></span> <span data-ttu-id="03e1a-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span><span class="sxs-lookup"><span data-stu-id="03e1a-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="03e1a-129">Reporting events</span><span class="sxs-lookup"><span data-stu-id="03e1a-129">Reporting events</span></span>
<span data-ttu-id="03e1a-130">Reporting on events covers session events and standalone events.</span><span class="sxs-lookup"><span data-stu-id="03e1a-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="03e1a-131">Session events</span><span class="sxs-lookup"><span data-stu-id="03e1a-131">Session events</span></span>
<span data-ttu-id="03e1a-132">Session events usually are used to report the actions performed by a user during the user's session.</span><span class="sxs-lookup"><span data-stu-id="03e1a-132">Session events usually are used to report the actions performed by a user during the user's session.</span></span>

<span data-ttu-id="03e1a-133">**Example without extra data:**</span><span class="sxs-lookup"><span data-stu-id="03e1a-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="03e1a-134">**Example with extra data:**</span><span class="sxs-lookup"><span data-stu-id="03e1a-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="03e1a-135">Standalone events</span><span class="sxs-lookup"><span data-stu-id="03e1a-135">Standalone events</span></span>
<span data-ttu-id="03e1a-136">Unlike session events, standalone events can occur outside the context of a session.</span><span class="sxs-lookup"><span data-stu-id="03e1a-136">Unlike session events, standalone events can occur outside the context of a session.</span></span>

<span data-ttu-id="03e1a-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="03e1a-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="03e1a-138">Reporting errors</span><span class="sxs-lookup"><span data-stu-id="03e1a-138">Reporting errors</span></span>
<span data-ttu-id="03e1a-139">Reporting on errors covers session errors and standalone errors.</span><span class="sxs-lookup"><span data-stu-id="03e1a-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="03e1a-140">Session errors</span><span class="sxs-lookup"><span data-stu-id="03e1a-140">Session errors</span></span>
<span data-ttu-id="03e1a-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span><span class="sxs-lookup"><span data-stu-id="03e1a-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span></span>

<span data-ttu-id="03e1a-142">**Example without extra data:**</span><span class="sxs-lookup"><span data-stu-id="03e1a-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="03e1a-143">**Example with extra data:**</span><span class="sxs-lookup"><span data-stu-id="03e1a-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="03e1a-144">Standalone errors</span><span class="sxs-lookup"><span data-stu-id="03e1a-144">Standalone errors</span></span>
<span data-ttu-id="03e1a-145">Unlike session errors, standalone errors can occur outside the context of a session.</span><span class="sxs-lookup"><span data-stu-id="03e1a-145">Unlike session errors, standalone errors can occur outside the context of a session.</span></span>

<span data-ttu-id="03e1a-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="03e1a-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="03e1a-147">Reporting jobs</span><span class="sxs-lookup"><span data-stu-id="03e1a-147">Reporting jobs</span></span>
<span data-ttu-id="03e1a-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span><span class="sxs-lookup"><span data-stu-id="03e1a-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="03e1a-149">**Example:**</span><span class="sxs-lookup"><span data-stu-id="03e1a-149">**Example:**</span></span>

<span data-ttu-id="03e1a-150">If you want to monitor an AJAX request, you'd use the following:</span><span class="sxs-lookup"><span data-stu-id="03e1a-150">If you want to monitor an AJAX request, you'd use the following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="03e1a-151">Reporting errors during a job</span><span class="sxs-lookup"><span data-stu-id="03e1a-151">Reporting errors during a job</span></span>
<span data-ttu-id="03e1a-152">Errors can be related to a running job instead of to the current user session.</span><span class="sxs-lookup"><span data-stu-id="03e1a-152">Errors can be related to a running job instead of to the current user session.</span></span>

<span data-ttu-id="03e1a-153">**Example:**</span><span class="sxs-lookup"><span data-stu-id="03e1a-153">**Example:**</span></span>

<span data-ttu-id="03e1a-154">If you want to report an error if an AJAX request fails:</span><span class="sxs-lookup"><span data-stu-id="03e1a-154">If you want to report an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="03e1a-155">Reporting events during a job</span><span class="sxs-lookup"><span data-stu-id="03e1a-155">Reporting events during a job</span></span>
<span data-ttu-id="03e1a-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span><span class="sxs-lookup"><span data-stu-id="03e1a-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="03e1a-157">This function works exactly like `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="03e1a-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="03e1a-158">Reporting crashes</span><span class="sxs-lookup"><span data-stu-id="03e1a-158">Reporting crashes</span></span>
<span data-ttu-id="03e1a-159">Use the `sendCrash` function to report crashes manually.</span><span class="sxs-lookup"><span data-stu-id="03e1a-159">Use the `sendCrash` function to report crashes manually.</span></span>

<span data-ttu-id="03e1a-160">The `crashid` argument is a string that identifies the type of crash.</span><span class="sxs-lookup"><span data-stu-id="03e1a-160">The `crashid` argument is a string that identifies the type of crash.</span></span>
<span data-ttu-id="03e1a-161">The `crash` argument usually is the stack trace of the crash as a string.</span><span class="sxs-lookup"><span data-stu-id="03e1a-161">The `crash` argument usually is the stack trace of the crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="03e1a-162">Extra parameters</span><span class="sxs-lookup"><span data-stu-id="03e1a-162">Extra parameters</span></span>
<span data-ttu-id="03e1a-163">You can attach arbitrary data to an event, error, activity, or job.</span><span class="sxs-lookup"><span data-stu-id="03e1a-163">You can attach arbitrary data to an event, error, activity, or job.</span></span>

<span data-ttu-id="03e1a-164">The data can be any JSON object (but not an array or primitive type).</span><span class="sxs-lookup"><span data-stu-id="03e1a-164">The data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="03e1a-165">**Example:**</span><span class="sxs-lookup"><span data-stu-id="03e1a-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="03e1a-166">Limits</span><span class="sxs-lookup"><span data-stu-id="03e1a-166">Limits</span></span>
<span data-ttu-id="03e1a-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span><span class="sxs-lookup"><span data-stu-id="03e1a-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="03e1a-168">Keys</span><span class="sxs-lookup"><span data-stu-id="03e1a-168">Keys</span></span>
<span data-ttu-id="03e1a-169">Each key in the object must match the following regular expression:</span><span class="sxs-lookup"><span data-stu-id="03e1a-169">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="03e1a-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span><span class="sxs-lookup"><span data-stu-id="03e1a-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="03e1a-171">Values</span><span class="sxs-lookup"><span data-stu-id="03e1a-171">Values</span></span>
<span data-ttu-id="03e1a-172">Values are limited to string, number, and Boolean types.</span><span class="sxs-lookup"><span data-stu-id="03e1a-172">Values are limited to string, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="03e1a-173">Size</span><span class="sxs-lookup"><span data-stu-id="03e1a-173">Size</span></span>
<span data-ttu-id="03e1a-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span><span class="sxs-lookup"><span data-stu-id="03e1a-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="03e1a-175">Reporting application information</span><span class="sxs-lookup"><span data-stu-id="03e1a-175">Reporting application information</span></span>
<span data-ttu-id="03e1a-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span><span class="sxs-lookup"><span data-stu-id="03e1a-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="03e1a-177">Note that this information can be sent incrementally.</span><span class="sxs-lookup"><span data-stu-id="03e1a-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="03e1a-178">Only the latest value for a specific key will be kept for a specific device.</span><span class="sxs-lookup"><span data-stu-id="03e1a-178">Only the latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="03e1a-179">Like event extras, you can use any JSON object to abstract application information.</span><span class="sxs-lookup"><span data-stu-id="03e1a-179">Like event extras, you can use any JSON object to abstract application information.</span></span> <span data-ttu-id="03e1a-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span><span class="sxs-lookup"><span data-stu-id="03e1a-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="03e1a-181">**Example:**</span><span class="sxs-lookup"><span data-stu-id="03e1a-181">**Example:**</span></span>

<span data-ttu-id="03e1a-182">Here is a code sample for sending the user's gender and birth date:</span><span class="sxs-lookup"><span data-stu-id="03e1a-182">Here is a code sample for sending the user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="03e1a-183">Limits</span><span class="sxs-lookup"><span data-stu-id="03e1a-183">Limits</span></span>
<span data-ttu-id="03e1a-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span><span class="sxs-lookup"><span data-stu-id="03e1a-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="03e1a-185">Keys</span><span class="sxs-lookup"><span data-stu-id="03e1a-185">Keys</span></span>
<span data-ttu-id="03e1a-186">Each key in the object must match the following regular expression:</span><span class="sxs-lookup"><span data-stu-id="03e1a-186">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="03e1a-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span><span class="sxs-lookup"><span data-stu-id="03e1a-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="03e1a-188">Size</span><span class="sxs-lookup"><span data-stu-id="03e1a-188">Size</span></span>
<span data-ttu-id="03e1a-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span><span class="sxs-lookup"><span data-stu-id="03e1a-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="03e1a-190">In the preceding example, the JSON sent to the server is 44 characters long:</span><span class="sxs-lookup"><span data-stu-id="03e1a-190">In the preceding example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
