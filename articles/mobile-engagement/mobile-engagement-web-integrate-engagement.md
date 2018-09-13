---
title: Azure Mobile Engagement Web SDK integration | Microsoft Docs
description: The latest updates and procedures for the Azure Mobile Engagement Web SDK
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 7d8eaa180e277741a583522ee62d68f5247b92bb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671947"
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="df3ce-103">Integrate Azure Mobile Engagement in a web application</span><span class="sxs-lookup"><span data-stu-id="df3ce-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="df3ce-108">The procedures in this article describe the simplest way to activate the analytics and monitoring functions in Azure Mobile Engagement in your web application.</span><span class="sxs-lookup"><span data-stu-id="df3ce-108">The procedures in this article describe the simplest way to activate the analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="df3ce-109">Follow the steps to activate the log reports that are needed to compute all statistics about users, sessions, activities, crashes, and technicals.</span><span class="sxs-lookup"><span data-stu-id="df3ce-109">Follow the steps to activate the log reports that are needed to compute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="df3ce-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using the Azure Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="df3ce-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using the Azure Mobile Engagement API.</span></span> <span data-ttu-id="df3ce-111">For more information, learn [how to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="df3ce-111">For more information, learn [how to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="df3ce-112">Introduction</span><span class="sxs-lookup"><span data-stu-id="df3ce-112">Introduction</span></span>
<span data-ttu-id="df3ce-113">[Download the Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="df3ce-113">[Download the Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="df3ce-114">The Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have to include in each page of your site or web application.</span><span class="sxs-lookup"><span data-stu-id="df3ce-114">The Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have to include in each page of your site or web application.</span></span>

> [!IMPORTANT]
> Before you run this script, you must run a script or code snippet that you write to configure Mobile Engagement for your application.
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="df3ce-116">Browser compatibility</span><span class="sxs-lookup"><span data-stu-id="df3ce-116">Browser compatibility</span></span>
<span data-ttu-id="df3ce-117">The Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition to cross-domain AJAX requests (relying on the W3C CORS specification).</span><span class="sxs-lookup"><span data-stu-id="df3ce-117">The Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition to cross-domain AJAX requests (relying on the W3C CORS specification).</span></span> <span data-ttu-id="df3ce-118">It's compatible with the following browsers:</span><span class="sxs-lookup"><span data-stu-id="df3ce-118">It's compatible with the following browsers:</span></span>

* <span data-ttu-id="df3ce-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="df3ce-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="df3ce-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="df3ce-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="df3ce-121">Firefox 3.5+</span><span class="sxs-lookup"><span data-stu-id="df3ce-121">Firefox 3.5+</span></span>
* <span data-ttu-id="df3ce-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="df3ce-122">Chrome 4+</span></span>
* <span data-ttu-id="df3ce-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="df3ce-123">Safari 6+</span></span>
* <span data-ttu-id="df3ce-124">Opera 12+</span><span class="sxs-lookup"><span data-stu-id="df3ce-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="df3ce-125">Configure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="df3ce-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="df3ce-126">Write a script that creates a global `azureEngagement` JavaScript object, as in the following example.</span><span class="sxs-lookup"><span data-stu-id="df3ce-126">Write a script that creates a global `azureEngagement` JavaScript object, as in the following example.</span></span> <span data-ttu-id="df3ce-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span><span class="sxs-lookup"><span data-stu-id="df3ce-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="df3ce-128">In this example, the JavaScript object is named `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="df3ce-128">In this example, the JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="df3ce-129">The `connectionString` value for your application is displayed in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="df3ce-129">The `connectionString` value for your application is displayed in the Azure portal.</span></span>

> [!NOTE]
> `appVersionName` and `appVersionCode` are optional. However, we recommend that you configure them so that analytics can process version information.
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="df3ce-132">Include Mobile Engagement scripts in your pages</span><span class="sxs-lookup"><span data-stu-id="df3ce-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="df3ce-133">Add Mobile Engagement scripts to your pages in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="df3ce-133">Add Mobile Engagement scripts to your pages in one of the following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="df3ce-134">Or this:</span><span class="sxs-lookup"><span data-stu-id="df3ce-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="df3ce-135">Alias</span><span class="sxs-lookup"><span data-stu-id="df3ce-135">Alias</span></span>
<span data-ttu-id="df3ce-136">After the Mobile Engagement Web SDK script is loaded, it creates the **engagement** alias to access the SDK APIs.</span><span class="sxs-lookup"><span data-stu-id="df3ce-136">After the Mobile Engagement Web SDK script is loaded, it creates the **engagement** alias to access the SDK APIs.</span></span> <span data-ttu-id="df3ce-137">You cannot use this alias to define the SDK configuration.</span><span class="sxs-lookup"><span data-stu-id="df3ce-137">You cannot use this alias to define the SDK configuration.</span></span> <span data-ttu-id="df3ce-138">This alias is used as a reference in this documentation.</span><span class="sxs-lookup"><span data-stu-id="df3ce-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="df3ce-139">Note that if the default alias conflicts with another global variable from your page, you can redefine it in the configuration as follows before you load the Mobile Engagement Web SDK:</span><span class="sxs-lookup"><span data-stu-id="df3ce-139">Note that if the default alias conflicts with another global variable from your page, you can redefine it in the configuration as follows before you load the Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="df3ce-140">Basic reporting</span><span class="sxs-lookup"><span data-stu-id="df3ce-140">Basic reporting</span></span>
<span data-ttu-id="df3ce-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span><span class="sxs-lookup"><span data-stu-id="df3ce-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="df3ce-142">Session tracking</span><span class="sxs-lookup"><span data-stu-id="df3ce-142">Session tracking</span></span>
<span data-ttu-id="df3ce-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span><span class="sxs-lookup"><span data-stu-id="df3ce-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="df3ce-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span><span class="sxs-lookup"><span data-stu-id="df3ce-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="df3ce-145">For a website or web application in which the current page never changes, you might want to track the activities on a smaller scale, such as within the page.</span><span class="sxs-lookup"><span data-stu-id="df3ce-145">For a website or web application in which the current page never changes, you might want to track the activities on a smaller scale, such as within the page.</span></span>

<span data-ttu-id="df3ce-146">Either way, to start or change the current user activity, call the `engagement.agent.startActivity` function.</span><span class="sxs-lookup"><span data-stu-id="df3ce-146">Either way, to start or change the current user activity, call the `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="df3ce-147">For example:</span><span class="sxs-lookup"><span data-stu-id="df3ce-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="df3ce-148">The Mobile Engagement server automatically ends an open session within three minutes after the application page is closed.</span><span class="sxs-lookup"><span data-stu-id="df3ce-148">The Mobile Engagement server automatically ends an open session within three minutes after the application page is closed.</span></span>

<span data-ttu-id="df3ce-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="df3ce-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="df3ce-150">This sets the current user activity to 'Idle.'</span><span class="sxs-lookup"><span data-stu-id="df3ce-150">This sets the current user activity to 'Idle.'</span></span>  <span data-ttu-id="df3ce-151">The session will end 10 seconds later unless a new call to `engagement.agent.startActivity` resumes the session.</span><span class="sxs-lookup"><span data-stu-id="df3ce-151">The session will end 10 seconds later unless a new call to `engagement.agent.startActivity` resumes the session.</span></span>

<span data-ttu-id="df3ce-152">You can configure the 10-second delay in the global engagement object, as follows:</span><span class="sxs-lookup"><span data-stu-id="df3ce-152">You can configure the 10-second delay in the global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end the session as soon as endActivity is called

> [!NOTE]
> You cannot use `engagement.agent.endActivity` in the `onunload` callback because you cannot make AJAX calls at this stage.
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="df3ce-154">Advanced reporting</span><span class="sxs-lookup"><span data-stu-id="df3ce-154">Advanced reporting</span></span>
<span data-ttu-id="df3ce-155">Optionally, if you want to report application-specific events, errors, and jobs, you need to use the Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="df3ce-155">Optionally, if you want to report application-specific events, errors, and jobs, you need to use the Mobile Engagement API.</span></span> <span data-ttu-id="df3ce-156">You access the Mobile Engagement API through the `engagement.agent` object.</span><span class="sxs-lookup"><span data-stu-id="df3ce-156">You access the Mobile Engagement API through the `engagement.agent` object.</span></span>

<span data-ttu-id="df3ce-157">You can access all of the advanced capabilities in Mobile Engagement in the Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="df3ce-157">You can access all of the advanced capabilities in Mobile Engagement in the Mobile Engagement API.</span></span> <span data-ttu-id="df3ce-158">The API is detailed in the article [How to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="df3ce-158">The API is detailed in the article [How to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-the-urls-used-for-ajax-calls"></a><span data-ttu-id="df3ce-159">Customize the URLs used for AJAX calls</span><span class="sxs-lookup"><span data-stu-id="df3ce-159">Customize the URLs used for AJAX calls</span></span>
<span data-ttu-id="df3ce-160">You can customize URLs that the Mobile Engagement Web SDK uses.</span><span class="sxs-lookup"><span data-stu-id="df3ce-160">You can customize URLs that the Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="df3ce-161">For example, to redefine the log URL (the SDK endpoint for logging), you can override the configuration like this:</span><span class="sxs-lookup"><span data-stu-id="df3ce-161">For example, to redefine the log URL (the SDK endpoint for logging), you can override the configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="df3ce-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, the default scheme is not used.</span><span class="sxs-lookup"><span data-stu-id="df3ce-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, the default scheme is not used.</span></span> <span data-ttu-id="df3ce-163">By default, the `https://` scheme is used for those URLs.</span><span class="sxs-lookup"><span data-stu-id="df3ce-163">By default, the `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="df3ce-164">If you want to customize the default scheme, override the configuration, like this:</span><span class="sxs-lookup"><span data-stu-id="df3ce-164">If you want to customize the default scheme, override the configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
