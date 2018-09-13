---
title: Monitor availability and responsiveness of any web site | Microsoft Docs
description: Set up web tests in Application Insights. Get alerts if a website becomes unavailable or responds slowly.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/12/2017
ms.author: awills
ms.openlocfilehash: fc2921deac627bdf0d6cc673ff3fde402ec681c5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660762"
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a><span data-ttu-id="4793f-104">Monitor availability and responsiveness of any web site</span><span class="sxs-lookup"><span data-stu-id="4793f-104">Monitor availability and responsiveness of any web site</span></span>
<span data-ttu-id="4793f-105">After you've deployed your web app or web site to any server, you can set up web tests to monitor its availability and responsiveness.</span><span class="sxs-lookup"><span data-stu-id="4793f-105">After you've deployed your web app or web site to any server, you can set up web tests to monitor its availability and responsiveness.</span></span> <span data-ttu-id="4793f-106">[Azure Application Insights](app-insights-overview.md) sends web requests to your application at regular intervals from points around the world.</span><span class="sxs-lookup"><span data-stu-id="4793f-106">[Azure Application Insights](app-insights-overview.md) sends web requests to your application at regular intervals from points around the world.</span></span> <span data-ttu-id="4793f-107">It alerts you if your application doesn't respond, or responds slowly.</span><span class="sxs-lookup"><span data-stu-id="4793f-107">It alerts you if your application doesn't respond, or responds slowly.</span></span>

![Web test example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/appinsights-10webtestresult.png)

<span data-ttu-id="4793f-109">You can set up web tests for any HTTP or HTTPS endpoint that is accessible from the public internet.</span><span class="sxs-lookup"><span data-stu-id="4793f-109">You can set up web tests for any HTTP or HTTPS endpoint that is accessible from the public internet.</span></span> <span data-ttu-id="4793f-110">You don't have to add anything to the web site you're testing.</span><span class="sxs-lookup"><span data-stu-id="4793f-110">You don't have to add anything to the web site you're testing.</span></span> <span data-ttu-id="4793f-111">It doesn't even have to be your site: you could test a REST API service on which you depend.</span><span class="sxs-lookup"><span data-stu-id="4793f-111">It doesn't even have to be your site: you could test a REST API service on which you depend.</span></span>

<span data-ttu-id="4793f-112">There are two types of web test:</span><span class="sxs-lookup"><span data-stu-id="4793f-112">There are two types of web test:</span></span>

* <span data-ttu-id="4793f-113">[URL ping test](#create): a simple test that you can create in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4793f-113">[URL ping test](#create): a simple test that you can create in the Azure portal.</span></span>
* <span data-ttu-id="4793f-114">[Multi-step web test](#multi-step-web-tests): which you create in Visual Studio Enterprise and upload to the portal.</span><span class="sxs-lookup"><span data-stu-id="4793f-114">[Multi-step web test](#multi-step-web-tests): which you create in Visual Studio Enterprise and upload to the portal.</span></span>

<span data-ttu-id="4793f-115">You can create up to 10 web tests per application resource.</span><span class="sxs-lookup"><span data-stu-id="4793f-115">You can create up to 10 web tests per application resource.</span></span>

## <a name="create"></a><span data-ttu-id="4793f-116">1. Open a resource for your web test reports</span><span class="sxs-lookup"><span data-stu-id="4793f-116">1. Open a resource for your web test reports</span></span>

<span data-ttu-id="4793f-117">**If you have already configured Application Insights** for your web app, open its Application Insights resource in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4793f-117">**If you have already configured Application Insights** for your web app, open its Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="4793f-118">**Or, if you want to see your reports in a new resource,** sign up to [Microsoft Azure](http://azure.com), go to the [Azure portal](https://portal.azure.com), and create an Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="4793f-118">**Or, if you want to see your reports in a new resource,** sign up to [Microsoft Azure](http://azure.com), go to the [Azure portal](https://portal.azure.com), and create an Application Insights resource.</span></span>

![New > Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/11-new-app.png)

<span data-ttu-id="4793f-120">Click **All resources** to open the Overview blade for the new resource.</span><span class="sxs-lookup"><span data-stu-id="4793f-120">Click **All resources** to open the Overview blade for the new resource.</span></span>

## <a name="setup"></a><span data-ttu-id="4793f-121">2. Create a URL ping test</span><span class="sxs-lookup"><span data-stu-id="4793f-121">2. Create a URL ping test</span></span>
<span data-ttu-id="4793f-122">Open the Availability blade and add a web test.</span><span class="sxs-lookup"><span data-stu-id="4793f-122">Open the Availability blade and add a web test.</span></span>

![Fill at least the URL of your website](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/13-availability.png)

* <span data-ttu-id="4793f-124">**The URL** can be any web page you want to test, but it must be visible from the public internet.</span><span class="sxs-lookup"><span data-stu-id="4793f-124">**The URL** can be any web page you want to test, but it must be visible from the public internet.</span></span> <span data-ttu-id="4793f-125">The URL can include a query string&#151;so, for example, you can exercise your database a little.</span><span class="sxs-lookup"><span data-stu-id="4793f-125">The URL can include a query string&#151;so, for example, you can exercise your database a little.</span></span> <span data-ttu-id="4793f-126">If the URL resolves to a redirect, we follow it up to 10 redirects.</span><span class="sxs-lookup"><span data-stu-id="4793f-126">If the URL resolves to a redirect, we follow it up to 10 redirects.</span></span>
* <span data-ttu-id="4793f-127">**Parse dependent requests**: If this option is checked, the test will request images, scripts, style files, and other files that are part of the web page under test.</span><span class="sxs-lookup"><span data-stu-id="4793f-127">**Parse dependent requests**: If this option is checked, the test will request images, scripts, style files, and other files that are part of the web page under test.</span></span> <span data-ttu-id="4793f-128">The recorded response time includes the time taken to get these files.</span><span class="sxs-lookup"><span data-stu-id="4793f-128">The recorded response time includes the time taken to get these files.</span></span> <span data-ttu-id="4793f-129">The test fails if all these resources cannot be successfully downloaded within the timeout for the whole test.</span><span class="sxs-lookup"><span data-stu-id="4793f-129">The test fails if all these resources cannot be successfully downloaded within the timeout for the whole test.</span></span> 

    <span data-ttu-id="4793f-130">If the option is not checked, the test only requests the file at the URL you specified.</span><span class="sxs-lookup"><span data-stu-id="4793f-130">If the option is not checked, the test only requests the file at the URL you specified.</span></span>
* <span data-ttu-id="4793f-131">**Enable retries**:  If this option is checked, when the test fails, it is retried after a short interval.</span><span class="sxs-lookup"><span data-stu-id="4793f-131">**Enable retries**:  If this option is checked, when the test fails, it is retried after a short interval.</span></span> <span data-ttu-id="4793f-132">A failure is reported only if three successive attempts fail.</span><span class="sxs-lookup"><span data-stu-id="4793f-132">A failure is reported only if three successive attempts fail.</span></span> <span data-ttu-id="4793f-133">Subsequent tests are then performed at the usual test frequency.</span><span class="sxs-lookup"><span data-stu-id="4793f-133">Subsequent tests are then performed at the usual test frequency.</span></span> <span data-ttu-id="4793f-134">Retry is temporarily suspended until the next success.</span><span class="sxs-lookup"><span data-stu-id="4793f-134">Retry is temporarily suspended until the next success.</span></span> <span data-ttu-id="4793f-135">This rule is applied independently at each test location.</span><span class="sxs-lookup"><span data-stu-id="4793f-135">This rule is applied independently at each test location.</span></span> <span data-ttu-id="4793f-136">We recommend this option.</span><span class="sxs-lookup"><span data-stu-id="4793f-136">We recommend this option.</span></span> <span data-ttu-id="4793f-137">On average, about 80% of failures disappear on retry.</span><span class="sxs-lookup"><span data-stu-id="4793f-137">On average, about 80% of failures disappear on retry.</span></span>
* <span data-ttu-id="4793f-138">**Test frequency**: Sets how often the test is run from each test location.</span><span class="sxs-lookup"><span data-stu-id="4793f-138">**Test frequency**: Sets how often the test is run from each test location.</span></span> <span data-ttu-id="4793f-139">With a frequency of five minutes and five test locations, your site is tested on average every minute.</span><span class="sxs-lookup"><span data-stu-id="4793f-139">With a frequency of five minutes and five test locations, your site is tested on average every minute.</span></span>
* <span data-ttu-id="4793f-140">**Test locations** are the places from where our servers send web requests to your URL.</span><span class="sxs-lookup"><span data-stu-id="4793f-140">**Test locations** are the places from where our servers send web requests to your URL.</span></span> <span data-ttu-id="4793f-141">Choose more than one so that you can distinguish problems in your website from network issues.</span><span class="sxs-lookup"><span data-stu-id="4793f-141">Choose more than one so that you can distinguish problems in your website from network issues.</span></span> <span data-ttu-id="4793f-142">You can select up to 16 locations.</span><span class="sxs-lookup"><span data-stu-id="4793f-142">You can select up to 16 locations.</span></span>
* <span data-ttu-id="4793f-143">**Success criteria**:</span><span class="sxs-lookup"><span data-stu-id="4793f-143">**Success criteria**:</span></span>

    <span data-ttu-id="4793f-144">**Test timeout**: Decrease this value to be alerted about slow responses.</span><span class="sxs-lookup"><span data-stu-id="4793f-144">**Test timeout**: Decrease this value to be alerted about slow responses.</span></span> <span data-ttu-id="4793f-145">The test is counted as a failure if the responses from your site have not been received within this period.</span><span class="sxs-lookup"><span data-stu-id="4793f-145">The test is counted as a failure if the responses from your site have not been received within this period.</span></span> <span data-ttu-id="4793f-146">If you selected **Parse dependent requests**, then all the images, style files, scripts, and other dependent resources must have been received within this period.</span><span class="sxs-lookup"><span data-stu-id="4793f-146">If you selected **Parse dependent requests**, then all the images, style files, scripts, and other dependent resources must have been received within this period.</span></span>

    <span data-ttu-id="4793f-147">**HTTP response**: The returned status code that is counted as a success.</span><span class="sxs-lookup"><span data-stu-id="4793f-147">**HTTP response**: The returned status code that is counted as a success.</span></span> <span data-ttu-id="4793f-148">200 is the code that indicates that a normal web page has been returned.</span><span class="sxs-lookup"><span data-stu-id="4793f-148">200 is the code that indicates that a normal web page has been returned.</span></span>

    <span data-ttu-id="4793f-149">**Content match**: a string, like "Welcome!"</span><span class="sxs-lookup"><span data-stu-id="4793f-149">**Content match**: a string, like "Welcome!"</span></span> <span data-ttu-id="4793f-150">We test that an exact case-sensitive match occurs in every response.</span><span class="sxs-lookup"><span data-stu-id="4793f-150">We test that an exact case-sensitive match occurs in every response.</span></span> <span data-ttu-id="4793f-151">It must be a plain string, without wildcards.</span><span class="sxs-lookup"><span data-stu-id="4793f-151">It must be a plain string, without wildcards.</span></span> <span data-ttu-id="4793f-152">Don't forget that if your page content changes you might have to update it.</span><span class="sxs-lookup"><span data-stu-id="4793f-152">Don't forget that if your page content changes you might have to update it.</span></span>
* <span data-ttu-id="4793f-153">**Alerts** are, by default, sent to you if there are failures in three locations over five minutes.</span><span class="sxs-lookup"><span data-stu-id="4793f-153">**Alerts** are, by default, sent to you if there are failures in three locations over five minutes.</span></span> <span data-ttu-id="4793f-154">A failure in one location is likely to be a network problem, and not a problem with your site.</span><span class="sxs-lookup"><span data-stu-id="4793f-154">A failure in one location is likely to be a network problem, and not a problem with your site.</span></span> <span data-ttu-id="4793f-155">But you can change the threshold to be more or less sensitive, and you can also change who the emails should be sent to.</span><span class="sxs-lookup"><span data-stu-id="4793f-155">But you can change the threshold to be more or less sensitive, and you can also change who the emails should be sent to.</span></span>

    <span data-ttu-id="4793f-156">You can set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span><span class="sxs-lookup"><span data-stu-id="4793f-156">You can set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span> <span data-ttu-id="4793f-157">(But note that, at present, query parameters are not passed through as Properties.)</span><span class="sxs-lookup"><span data-stu-id="4793f-157">(But note that, at present, query parameters are not passed through as Properties.)</span></span>

### <a name="test-more-urls"></a><span data-ttu-id="4793f-158">Test more URLs</span><span class="sxs-lookup"><span data-stu-id="4793f-158">Test more URLs</span></span>
<span data-ttu-id="4793f-159">Add more tests.</span><span class="sxs-lookup"><span data-stu-id="4793f-159">Add more tests.</span></span> <span data-ttu-id="4793f-160">For example, as well as testing your home page, you can make sure your database is running by testing the URL for a search.</span><span class="sxs-lookup"><span data-stu-id="4793f-160">For example, as well as testing your home page, you can make sure your database is running by testing the URL for a search.</span></span>


## <a name="monitor"></a><span data-ttu-id="4793f-161">3. See your web test results</span><span class="sxs-lookup"><span data-stu-id="4793f-161">3. See your web test results</span></span>

<span data-ttu-id="4793f-162">After 5 minutes, click **Refresh** to see test results.</span><span class="sxs-lookup"><span data-stu-id="4793f-162">After 5 minutes, click **Refresh** to see test results.</span></span> 

![Summary results on the home blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/14-availSummary.png)

<span data-ttu-id="4793f-164">Click any bar on the summary chart for a more detailed view of that time period.</span><span class="sxs-lookup"><span data-stu-id="4793f-164">Click any bar on the summary chart for a more detailed view of that time period.</span></span>

## <a name="edit"></a> <span data-ttu-id="4793f-165">Inspect and edit tests</span><span class="sxs-lookup"><span data-stu-id="4793f-165">Inspect and edit tests</span></span>

<span data-ttu-id="4793f-166">From the summary page, select a specific test.</span><span class="sxs-lookup"><span data-stu-id="4793f-166">From the summary page, select a specific test.</span></span> <span data-ttu-id="4793f-167">There, you can see its specific results, and edit or temporarily disable it.</span><span class="sxs-lookup"><span data-stu-id="4793f-167">There, you can see its specific results, and edit or temporarily disable it.</span></span>

![Edit or disable a web test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/19-availEdit.png)

<span data-ttu-id="4793f-169">You might want to disable web tests while you are performing maintenance on your service.</span><span class="sxs-lookup"><span data-stu-id="4793f-169">You might want to disable web tests while you are performing maintenance on your service.</span></span>


## <a name="failures"></a><span data-ttu-id="4793f-170">If you see failures</span><span class="sxs-lookup"><span data-stu-id="4793f-170">If you see failures</span></span>
<span data-ttu-id="4793f-171">Click a red dot.</span><span class="sxs-lookup"><span data-stu-id="4793f-171">Click a red dot.</span></span>

![Click a red dot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/open-instance.png)


<span data-ttu-id="4793f-173">From a web test result, you can:</span><span class="sxs-lookup"><span data-stu-id="4793f-173">From a web test result, you can:</span></span>

* <span data-ttu-id="4793f-174">Inspect the response received from your server.</span><span class="sxs-lookup"><span data-stu-id="4793f-174">Inspect the response received from your server.</span></span>
* <span data-ttu-id="4793f-175">Open the telemetry sent by your server app while processing the failed request instance.</span><span class="sxs-lookup"><span data-stu-id="4793f-175">Open the telemetry sent by your server app while processing the failed request instance.</span></span>
* <span data-ttu-id="4793f-176">Log an issue or work item in Git or VSTS to track the problem.</span><span class="sxs-lookup"><span data-stu-id="4793f-176">Log an issue or work item in Git or VSTS to track the problem.</span></span> <span data-ttu-id="4793f-177">The bug will contain a link to this event.</span><span class="sxs-lookup"><span data-stu-id="4793f-177">The bug will contain a link to this event.</span></span>
* <span data-ttu-id="4793f-178">Open the web test result in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4793f-178">Open the web test result in Visual Studio.</span></span>


<span data-ttu-id="4793f-179">*Looks OK but reported as a failure?*</span><span class="sxs-lookup"><span data-stu-id="4793f-179">*Looks OK but reported as a failure?*</span></span> <span data-ttu-id="4793f-180">Check all the images, scripts, style sheets, and any other files loaded by the page.</span><span class="sxs-lookup"><span data-stu-id="4793f-180">Check all the images, scripts, style sheets, and any other files loaded by the page.</span></span> <span data-ttu-id="4793f-181">If any of them fails, the test is reported as failed, even if the main html page loads OK.</span><span class="sxs-lookup"><span data-stu-id="4793f-181">If any of them fails, the test is reported as failed, even if the main html page loads OK.</span></span>

<span data-ttu-id="4793f-182">*No related items?*</span><span class="sxs-lookup"><span data-stu-id="4793f-182">*No related items?*</span></span> <span data-ttu-id="4793f-183">That may be because [sampling](app-insights-sampling.md) is in operation.</span><span class="sxs-lookup"><span data-stu-id="4793f-183">That may be because [sampling](app-insights-sampling.md) is in operation.</span></span>

## <a name="multi-step-web-tests"></a><span data-ttu-id="4793f-184">Multi-step web tests</span><span class="sxs-lookup"><span data-stu-id="4793f-184">Multi-step web tests</span></span>
<span data-ttu-id="4793f-185">You can monitor a scenario that involves a sequence of URLs.</span><span class="sxs-lookup"><span data-stu-id="4793f-185">You can monitor a scenario that involves a sequence of URLs.</span></span> <span data-ttu-id="4793f-186">For example, if you are monitoring a sales website, you can test that adding items to the shopping cart works correctly.</span><span class="sxs-lookup"><span data-stu-id="4793f-186">For example, if you are monitoring a sales website, you can test that adding items to the shopping cart works correctly.</span></span>

> [!NOTE] 
> <span data-ttu-id="4793f-187">There is a charge for multi-step web tests.</span><span class="sxs-lookup"><span data-stu-id="4793f-187">There is a charge for multi-step web tests.</span></span> <span data-ttu-id="4793f-188">[Pricing scheme](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="4793f-188">[Pricing scheme](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>
> 

<span data-ttu-id="4793f-189">To create a multi-step test, you record the scenario by using Visual Studio Enterprise, and then upload the recording to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4793f-189">To create a multi-step test, you record the scenario by using Visual Studio Enterprise, and then upload the recording to Application Insights.</span></span> <span data-ttu-id="4793f-190">Application Insights replays the scenario at intervals and verifies the responses.</span><span class="sxs-lookup"><span data-stu-id="4793f-190">Application Insights replays the scenario at intervals and verifies the responses.</span></span>

> [!NOTE]
> <span data-ttu-id="4793f-191">You can't use coded functions or loops in your tests.</span><span class="sxs-lookup"><span data-stu-id="4793f-191">You can't use coded functions or loops in your tests.</span></span> <span data-ttu-id="4793f-192">The test must be contained completely in the .webtest script.</span><span class="sxs-lookup"><span data-stu-id="4793f-192">The test must be contained completely in the .webtest script.</span></span> <span data-ttu-id="4793f-193">However, you can use standard plugins.</span><span class="sxs-lookup"><span data-stu-id="4793f-193">However, you can use standard plugins.</span></span>
>

#### <a name="1-record-a-scenario"></a><span data-ttu-id="4793f-194">1. Record a scenario</span><span class="sxs-lookup"><span data-stu-id="4793f-194">1. Record a scenario</span></span>
<span data-ttu-id="4793f-195">Use Visual Studio Enterprise to record a web session.</span><span class="sxs-lookup"><span data-stu-id="4793f-195">Use Visual Studio Enterprise to record a web session.</span></span>

1. <span data-ttu-id="4793f-196">Create a Web performance test project.</span><span class="sxs-lookup"><span data-stu-id="4793f-196">Create a Web performance test project.</span></span>

    ![In Visual Studio Enterprise edition, create a project from the Web Performance and Load Test template.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * <span data-ttu-id="4793f-198">*Don't see the Web Performance and Load Test template?*</span><span class="sxs-lookup"><span data-stu-id="4793f-198">*Don't see the Web Performance and Load Test template?*</span></span> <span data-ttu-id="4793f-199">- Close Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4793f-199">- Close Visual Studio Enterprise.</span></span> <span data-ttu-id="4793f-200">Open **Visual Studio Installer** to modify your Visual Studio Enterprise installation.</span><span class="sxs-lookup"><span data-stu-id="4793f-200">Open **Visual Studio Installer** to modify your Visual Studio Enterprise installation.</span></span> <span data-ttu-id="4793f-201">Under **Individual Components**, select **Web Performance and load testing tools**.</span><span class="sxs-lookup"><span data-stu-id="4793f-201">Under **Individual Components**, select **Web Performance and load testing tools**.</span></span>

2. <span data-ttu-id="4793f-202">Open the .webtest file and start recording.</span><span class="sxs-lookup"><span data-stu-id="4793f-202">Open the .webtest file and start recording.</span></span>

    ![Open the .webtest file and click Record.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. <span data-ttu-id="4793f-204">Do the user actions you want to simulate in your test: open your website, add a product to the cart, and so on.</span><span class="sxs-lookup"><span data-stu-id="4793f-204">Do the user actions you want to simulate in your test: open your website, add a product to the cart, and so on.</span></span> <span data-ttu-id="4793f-205">Then stop your test.</span><span class="sxs-lookup"><span data-stu-id="4793f-205">Then stop your test.</span></span>

    ![The web test recorder runs in Internet Explorer.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    <span data-ttu-id="4793f-207">Don't make a long scenario.</span><span class="sxs-lookup"><span data-stu-id="4793f-207">Don't make a long scenario.</span></span> <span data-ttu-id="4793f-208">There's a limit of 100 steps and 2 minutes.</span><span class="sxs-lookup"><span data-stu-id="4793f-208">There's a limit of 100 steps and 2 minutes.</span></span>
4. <span data-ttu-id="4793f-209">Edit the test to:</span><span class="sxs-lookup"><span data-stu-id="4793f-209">Edit the test to:</span></span>

   * <span data-ttu-id="4793f-210">Add validations to check the received text and response codes.</span><span class="sxs-lookup"><span data-stu-id="4793f-210">Add validations to check the received text and response codes.</span></span>
   * <span data-ttu-id="4793f-211">Remove any superfluous interactions.</span><span class="sxs-lookup"><span data-stu-id="4793f-211">Remove any superfluous interactions.</span></span> <span data-ttu-id="4793f-212">You could also remove dependent requests for pictures or to ad or tracking sites.</span><span class="sxs-lookup"><span data-stu-id="4793f-212">You could also remove dependent requests for pictures or to ad or tracking sites.</span></span>

     <span data-ttu-id="4793f-213">Remember that you can only edit the test script - you can't add custom code or call other web tests.</span><span class="sxs-lookup"><span data-stu-id="4793f-213">Remember that you can only edit the test script - you can't add custom code or call other web tests.</span></span> <span data-ttu-id="4793f-214">Don't insert loops in the test.</span><span class="sxs-lookup"><span data-stu-id="4793f-214">Don't insert loops in the test.</span></span> <span data-ttu-id="4793f-215">You can use standard web test plug-ins.</span><span class="sxs-lookup"><span data-stu-id="4793f-215">You can use standard web test plug-ins.</span></span>
5. <span data-ttu-id="4793f-216">Run the test in Visual Studio to make sure it works.</span><span class="sxs-lookup"><span data-stu-id="4793f-216">Run the test in Visual Studio to make sure it works.</span></span>

    <span data-ttu-id="4793f-217">The web test runner opens a web browser and repeats the actions you recorded.</span><span class="sxs-lookup"><span data-stu-id="4793f-217">The web test runner opens a web browser and repeats the actions you recorded.</span></span> <span data-ttu-id="4793f-218">Make sure it works as you expect.</span><span class="sxs-lookup"><span data-stu-id="4793f-218">Make sure it works as you expect.</span></span>

    ![In Visual Studio, open the .webtest file and click Run.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-the-web-test-to-application-insights"></a><span data-ttu-id="4793f-220">2. Upload the web test to Application Insights</span><span class="sxs-lookup"><span data-stu-id="4793f-220">2. Upload the web test to Application Insights</span></span>
1. <span data-ttu-id="4793f-221">In the Application Insights portal, create a new web test.</span><span class="sxs-lookup"><span data-stu-id="4793f-221">In the Application Insights portal, create a new web test.</span></span>

    ![On the web tests blade, choose Add.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/16-another-test.png)
2. <span data-ttu-id="4793f-223">Select multi-step test, and upload the .webtest file.</span><span class="sxs-lookup"><span data-stu-id="4793f-223">Select multi-step test, and upload the .webtest file.</span></span>

    ![Select multi-step webtest.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    <span data-ttu-id="4793f-225">Set the test locations, frequency, and alert parameters in the same way as for ping tests.</span><span class="sxs-lookup"><span data-stu-id="4793f-225">Set the test locations, frequency, and alert parameters in the same way as for ping tests.</span></span>

#### <a name="3-see-the-results"></a><span data-ttu-id="4793f-226">3. See the results</span><span class="sxs-lookup"><span data-stu-id="4793f-226">3. See the results</span></span>

<span data-ttu-id="4793f-227">View your test results and any failures in the same way as single-url tests.</span><span class="sxs-lookup"><span data-stu-id="4793f-227">View your test results and any failures in the same way as single-url tests.</span></span>

<span data-ttu-id="4793f-228">In addition, you can download the test results to view them in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4793f-228">In addition, you can download the test results to view them in Visual Studio.</span></span>

#### <a name="too-many-failures"></a><span data-ttu-id="4793f-229">Too many failures?</span><span class="sxs-lookup"><span data-stu-id="4793f-229">Too many failures?</span></span>

* <span data-ttu-id="4793f-230">A common reason for failure is that the test runs too long.</span><span class="sxs-lookup"><span data-stu-id="4793f-230">A common reason for failure is that the test runs too long.</span></span> <span data-ttu-id="4793f-231">It mustn't run longer than two minutes.</span><span class="sxs-lookup"><span data-stu-id="4793f-231">It mustn't run longer than two minutes.</span></span>

* <span data-ttu-id="4793f-232">Don't forget that all the resources of a page must load correctly for the test to succeed, including scripts, style sheets, images, and so forth.</span><span class="sxs-lookup"><span data-stu-id="4793f-232">Don't forget that all the resources of a page must load correctly for the test to succeed, including scripts, style sheets, images, and so forth.</span></span>

* <span data-ttu-id="4793f-233">The web test must be entirely contained in the .webtest script: you can't use coded functions in the test.</span><span class="sxs-lookup"><span data-stu-id="4793f-233">The web test must be entirely contained in the .webtest script: you can't use coded functions in the test.</span></span>

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a><span data-ttu-id="4793f-234">Plugging time and random numbers into your multi-step test</span><span class="sxs-lookup"><span data-stu-id="4793f-234">Plugging time and random numbers into your multi-step test</span></span>
<span data-ttu-id="4793f-235">Suppose you're testing a tool that gets time-dependent data such as stocks from an external feed.</span><span class="sxs-lookup"><span data-stu-id="4793f-235">Suppose you're testing a tool that gets time-dependent data such as stocks from an external feed.</span></span> <span data-ttu-id="4793f-236">When you record your web test, you have to use specific times, but you set them as parameters of the test, StartTime and EndTime.</span><span class="sxs-lookup"><span data-stu-id="4793f-236">When you record your web test, you have to use specific times, but you set them as parameters of the test, StartTime and EndTime.</span></span>

![A web test with parameters.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

<span data-ttu-id="4793f-238">When you run the test, you'd like EndTime always to be the present time, and StartTime should be 15 minutes ago.</span><span class="sxs-lookup"><span data-stu-id="4793f-238">When you run the test, you'd like EndTime always to be the present time, and StartTime should be 15 minutes ago.</span></span>

<span data-ttu-id="4793f-239">Web Test Plug-ins provide the way to do parameterize times.</span><span class="sxs-lookup"><span data-stu-id="4793f-239">Web Test Plug-ins provide the way to do parameterize times.</span></span>

1. <span data-ttu-id="4793f-240">Add a web test plug-in for each variable parameter value you want.</span><span class="sxs-lookup"><span data-stu-id="4793f-240">Add a web test plug-in for each variable parameter value you want.</span></span> <span data-ttu-id="4793f-241">In the web test toolbar, choose **Add Web Test Plugin**.</span><span class="sxs-lookup"><span data-stu-id="4793f-241">In the web test toolbar, choose **Add Web Test Plugin**.</span></span>

    ![Choose Add Web Test Plugin and select a type.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    <span data-ttu-id="4793f-243">In this example, we use two instances of the Date Time Plug-in.</span><span class="sxs-lookup"><span data-stu-id="4793f-243">In this example, we use two instances of the Date Time Plug-in.</span></span> <span data-ttu-id="4793f-244">One instance is for "15 minutes ago" and another for "now."</span><span class="sxs-lookup"><span data-stu-id="4793f-244">One instance is for "15 minutes ago" and another for "now."</span></span>
2. <span data-ttu-id="4793f-245">Open the properties of each plug-in.</span><span class="sxs-lookup"><span data-stu-id="4793f-245">Open the properties of each plug-in.</span></span> <span data-ttu-id="4793f-246">Give it a name and set it to use the current time.</span><span class="sxs-lookup"><span data-stu-id="4793f-246">Give it a name and set it to use the current time.</span></span> <span data-ttu-id="4793f-247">For one of them, set Add Minutes = -15.</span><span class="sxs-lookup"><span data-stu-id="4793f-247">For one of them, set Add Minutes = -15.</span></span>

    ![Set name, Use Current Time, and Add Minutes.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. <span data-ttu-id="4793f-249">In the web test parameters, use {{plug-in name}} to reference a plug-in name.</span><span class="sxs-lookup"><span data-stu-id="4793f-249">In the web test parameters, use {{plug-in name}} to reference a plug-in name.</span></span>

    ![In the test parameter, use {{plug-in name}}.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

<span data-ttu-id="4793f-251">Now, upload your test to the portal.</span><span class="sxs-lookup"><span data-stu-id="4793f-251">Now, upload your test to the portal.</span></span> <span data-ttu-id="4793f-252">It uses the dynamic values on every run of the test.</span><span class="sxs-lookup"><span data-stu-id="4793f-252">It uses the dynamic values on every run of the test.</span></span>

## <a name="dealing-with-sign-in"></a><span data-ttu-id="4793f-253">Dealing with sign-in</span><span class="sxs-lookup"><span data-stu-id="4793f-253">Dealing with sign-in</span></span>
<span data-ttu-id="4793f-254">If your users sign in to your app, you have various options for simulating sign-in so that you can test pages behind the sign-in.</span><span class="sxs-lookup"><span data-stu-id="4793f-254">If your users sign in to your app, you have various options for simulating sign-in so that you can test pages behind the sign-in.</span></span> <span data-ttu-id="4793f-255">The approach you use depends on the type of security provided by the app.</span><span class="sxs-lookup"><span data-stu-id="4793f-255">The approach you use depends on the type of security provided by the app.</span></span>

<span data-ttu-id="4793f-256">In all cases, you should create an account in your application just for the purpose of testing.</span><span class="sxs-lookup"><span data-stu-id="4793f-256">In all cases, you should create an account in your application just for the purpose of testing.</span></span> <span data-ttu-id="4793f-257">If possible, restrict the permissions of this test account so that there's no possibility of the web tests affecting real users.</span><span class="sxs-lookup"><span data-stu-id="4793f-257">If possible, restrict the permissions of this test account so that there's no possibility of the web tests affecting real users.</span></span>

### <a name="simple-username-and-password"></a><span data-ttu-id="4793f-258">Simple username and password</span><span class="sxs-lookup"><span data-stu-id="4793f-258">Simple username and password</span></span>
<span data-ttu-id="4793f-259">Record a web test in the usual way.</span><span class="sxs-lookup"><span data-stu-id="4793f-259">Record a web test in the usual way.</span></span> <span data-ttu-id="4793f-260">Delete cookies first.</span><span class="sxs-lookup"><span data-stu-id="4793f-260">Delete cookies first.</span></span>

### <a name="saml-authentication"></a><span data-ttu-id="4793f-261">SAML authentication</span><span class="sxs-lookup"><span data-stu-id="4793f-261">SAML authentication</span></span>
<span data-ttu-id="4793f-262">Use the SAML plugin that is available for web tests.</span><span class="sxs-lookup"><span data-stu-id="4793f-262">Use the SAML plugin that is available for web tests.</span></span>

### <a name="client-secret"></a><span data-ttu-id="4793f-263">Client secret</span><span class="sxs-lookup"><span data-stu-id="4793f-263">Client secret</span></span>
<span data-ttu-id="4793f-264">If your app has a sign-in route that involves a client secret, use that route.</span><span class="sxs-lookup"><span data-stu-id="4793f-264">If your app has a sign-in route that involves a client secret, use that route.</span></span> <span data-ttu-id="4793f-265">Azure Active Directory (AAD) is an example of a service that provides a client secret sign-in.</span><span class="sxs-lookup"><span data-stu-id="4793f-265">Azure Active Directory (AAD) is an example of a service that provides a client secret sign-in.</span></span> <span data-ttu-id="4793f-266">In AAD, the client secret is the App Key.</span><span class="sxs-lookup"><span data-stu-id="4793f-266">In AAD, the client secret is the App Key.</span></span>

<span data-ttu-id="4793f-267">Here's a sample web test of an Azure web app using an app key:</span><span class="sxs-lookup"><span data-stu-id="4793f-267">Here's a sample web test of an Azure web app using an app key:</span></span>

![Client secret sample](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-monitor-web-app-availability/110.png)

1. <span data-ttu-id="4793f-269">Get token from AAD using client secret (AppKey).</span><span class="sxs-lookup"><span data-stu-id="4793f-269">Get token from AAD using client secret (AppKey).</span></span>
2. <span data-ttu-id="4793f-270">Extract bearer token from response.</span><span class="sxs-lookup"><span data-stu-id="4793f-270">Extract bearer token from response.</span></span>
3. <span data-ttu-id="4793f-271">Call API using bearer token in the authorization header.</span><span class="sxs-lookup"><span data-stu-id="4793f-271">Call API using bearer token in the authorization header.</span></span>

<span data-ttu-id="4793f-272">Make sure that the web test is an actual client - that is, it has its own app in AAD - and use its clientId + appkey.</span><span class="sxs-lookup"><span data-stu-id="4793f-272">Make sure that the web test is an actual client - that is, it has its own app in AAD - and use its clientId + appkey.</span></span> <span data-ttu-id="4793f-273">Your service under test also has its own app in AAD: the appID URI of this app is reflected in the web test in the “resource” field.</span><span class="sxs-lookup"><span data-stu-id="4793f-273">Your service under test also has its own app in AAD: the appID URI of this app is reflected in the web test in the “resource” field.</span></span>

### <a name="open-authentication"></a><span data-ttu-id="4793f-274">Open Authentication</span><span class="sxs-lookup"><span data-stu-id="4793f-274">Open Authentication</span></span>
<span data-ttu-id="4793f-275">An example of open authentication is signing in with your Microsoft or Google account.</span><span class="sxs-lookup"><span data-stu-id="4793f-275">An example of open authentication is signing in with your Microsoft or Google account.</span></span> <span data-ttu-id="4793f-276">Many apps that use OAuth provide the client secret alternative, so your first tactic should be to investigate that possibility.</span><span class="sxs-lookup"><span data-stu-id="4793f-276">Many apps that use OAuth provide the client secret alternative, so your first tactic should be to investigate that possibility.</span></span>

<span data-ttu-id="4793f-277">If your test must sign in using OAuth, the general approach is:</span><span class="sxs-lookup"><span data-stu-id="4793f-277">If your test must sign in using OAuth, the general approach is:</span></span>

* <span data-ttu-id="4793f-278">Use a tool such as Fiddler to examine the traffic between your web browser, the authentication site, and your app.</span><span class="sxs-lookup"><span data-stu-id="4793f-278">Use a tool such as Fiddler to examine the traffic between your web browser, the authentication site, and your app.</span></span>
* <span data-ttu-id="4793f-279">Perform two or more sign-ins using different machines or browsers, or at long intervals (to allow tokens to expire).</span><span class="sxs-lookup"><span data-stu-id="4793f-279">Perform two or more sign-ins using different machines or browsers, or at long intervals (to allow tokens to expire).</span></span>
* <span data-ttu-id="4793f-280">By comparing different sessions, identify the token passed back from the authenticating site, that is then passed to your app server after sign-in.</span><span class="sxs-lookup"><span data-stu-id="4793f-280">By comparing different sessions, identify the token passed back from the authenticating site, that is then passed to your app server after sign-in.</span></span>
* <span data-ttu-id="4793f-281">Record a web test using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4793f-281">Record a web test using Visual Studio.</span></span>
* <span data-ttu-id="4793f-282">Parameterize the tokens, setting the parameter when the token is returned from the authenticator, and using it in the query to the site.</span><span class="sxs-lookup"><span data-stu-id="4793f-282">Parameterize the tokens, setting the parameter when the token is returned from the authenticator, and using it in the query to the site.</span></span>
  <span data-ttu-id="4793f-283">(Visual Studio attempts to parameterize the test, but does not correctly parameterize the tokens.)</span><span class="sxs-lookup"><span data-stu-id="4793f-283">(Visual Studio attempts to parameterize the test, but does not correctly parameterize the tokens.)</span></span>


## <a name="performance-tests"></a><span data-ttu-id="4793f-284">Performance tests</span><span class="sxs-lookup"><span data-stu-id="4793f-284">Performance tests</span></span>
<span data-ttu-id="4793f-285">You can run a load test on your website.</span><span class="sxs-lookup"><span data-stu-id="4793f-285">You can run a load test on your website.</span></span> <span data-ttu-id="4793f-286">Like the availability test, you can send either simple requests or multi-step requests from our points around the world.</span><span class="sxs-lookup"><span data-stu-id="4793f-286">Like the availability test, you can send either simple requests or multi-step requests from our points around the world.</span></span> <span data-ttu-id="4793f-287">Unlike an availability test, many requests are sent, simulating multiple simultaneous users.</span><span class="sxs-lookup"><span data-stu-id="4793f-287">Unlike an availability test, many requests are sent, simulating multiple simultaneous users.</span></span>

<span data-ttu-id="4793f-288">From the Overview blade, open **Settings**, **Performance Tests**.</span><span class="sxs-lookup"><span data-stu-id="4793f-288">From the Overview blade, open **Settings**, **Performance Tests**.</span></span> <span data-ttu-id="4793f-289">When you create a test, you are invited to connect to or create a Visual Studio Team Services account.</span><span class="sxs-lookup"><span data-stu-id="4793f-289">When you create a test, you are invited to connect to or create a Visual Studio Team Services account.</span></span>

<span data-ttu-id="4793f-290">When the test is complete, you are shown response times and success rates.</span><span class="sxs-lookup"><span data-stu-id="4793f-290">When the test is complete, you are shown response times and success rates.</span></span>

## <a name="automation"></a><span data-ttu-id="4793f-291">Automation</span><span class="sxs-lookup"><span data-stu-id="4793f-291">Automation</span></span>
* <span data-ttu-id="4793f-292">[Use PowerShell scripts to set up a web test](app-insights-powershell.md#add-an-availability-test) automatically.</span><span class="sxs-lookup"><span data-stu-id="4793f-292">[Use PowerShell scripts to set up a web test](app-insights-powershell.md#add-an-availability-test) automatically.</span></span>
* <span data-ttu-id="4793f-293">Set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span><span class="sxs-lookup"><span data-stu-id="4793f-293">Set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span>

## <a name="qna"></a><span data-ttu-id="4793f-294">Questions?</span><span class="sxs-lookup"><span data-stu-id="4793f-294">Questions?</span></span> <span data-ttu-id="4793f-295">Problems?</span><span class="sxs-lookup"><span data-stu-id="4793f-295">Problems?</span></span>
* <span data-ttu-id="4793f-296">*Can I call code from my web test?*</span><span class="sxs-lookup"><span data-stu-id="4793f-296">*Can I call code from my web test?*</span></span>

    <span data-ttu-id="4793f-297">No.</span><span class="sxs-lookup"><span data-stu-id="4793f-297">No.</span></span> <span data-ttu-id="4793f-298">The steps of the test must be in the .webtest file.</span><span class="sxs-lookup"><span data-stu-id="4793f-298">The steps of the test must be in the .webtest file.</span></span> <span data-ttu-id="4793f-299">And you can't call other web tests or use loops.</span><span class="sxs-lookup"><span data-stu-id="4793f-299">And you can't call other web tests or use loops.</span></span> <span data-ttu-id="4793f-300">But there are several plug-ins that you might find helpful.</span><span class="sxs-lookup"><span data-stu-id="4793f-300">But there are several plug-ins that you might find helpful.</span></span>
* <span data-ttu-id="4793f-301">*Is HTTPS supported?*</span><span class="sxs-lookup"><span data-stu-id="4793f-301">*Is HTTPS supported?*</span></span>

    <span data-ttu-id="4793f-302">We support TLS 1.1 and TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="4793f-302">We support TLS 1.1 and TLS 1.2.</span></span>
* <span data-ttu-id="4793f-303">*Is there a difference between "web tests" and "availability tests"?*</span><span class="sxs-lookup"><span data-stu-id="4793f-303">*Is there a difference between "web tests" and "availability tests"?*</span></span>

    <span data-ttu-id="4793f-304">We use the two terms interchangeably.</span><span class="sxs-lookup"><span data-stu-id="4793f-304">We use the two terms interchangeably.</span></span>
* <span data-ttu-id="4793f-305">*I'd like to use availability tests on our internal server that runs behind a firewall.*</span><span class="sxs-lookup"><span data-stu-id="4793f-305">*I'd like to use availability tests on our internal server that runs behind a firewall.*</span></span>

    <span data-ttu-id="4793f-306">There are two possible solutions:</span><span class="sxs-lookup"><span data-stu-id="4793f-306">There are two possible solutions:</span></span>
    
    * <span data-ttu-id="4793f-307">Configure your firewall to permit incoming requests from the [IP addresses of our web test agents](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="4793f-307">Configure your firewall to permit incoming requests from the [IP addresses of our web test agents](app-insights-ip-addresses.md).</span></span>
    * <span data-ttu-id="4793f-308">Write your own code to periodically test your internal server.</span><span class="sxs-lookup"><span data-stu-id="4793f-308">Write your own code to periodically test your internal server.</span></span> <span data-ttu-id="4793f-309">Run the code as a background process on a test server behind your firewall.</span><span class="sxs-lookup"><span data-stu-id="4793f-309">Run the code as a background process on a test server behind your firewall.</span></span> <span data-ttu-id="4793f-310">Your test process can send its results to Application Insights by using [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API in the core SDK package.</span><span class="sxs-lookup"><span data-stu-id="4793f-310">Your test process can send its results to Application Insights by using [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API in the core SDK package.</span></span> <span data-ttu-id="4793f-311">This requires your test server to have outgoing access to the Application Insights ingestion endpoint, but that is a much smaller security risk than the alternative of permitting incoming requests.</span><span class="sxs-lookup"><span data-stu-id="4793f-311">This requires your test server to have outgoing access to the Application Insights ingestion endpoint, but that is a much smaller security risk than the alternative of permitting incoming requests.</span></span> <span data-ttu-id="4793f-312">The results will not appear in the availability web tests blades, but will appear as availability results in Analytics, Search, and Metric Explorer.</span><span class="sxs-lookup"><span data-stu-id="4793f-312">The results will not appear in the availability web tests blades, but will appear as availability results in Analytics, Search, and Metric Explorer.</span></span>
* <span data-ttu-id="4793f-313">*Uploading a multi-step web test fails*</span><span class="sxs-lookup"><span data-stu-id="4793f-313">*Uploading a multi-step web test fails*</span></span>

    <span data-ttu-id="4793f-314">There's a size limit of 300 K.</span><span class="sxs-lookup"><span data-stu-id="4793f-314">There's a size limit of 300 K.</span></span>

    <span data-ttu-id="4793f-315">Loops aren't supported.</span><span class="sxs-lookup"><span data-stu-id="4793f-315">Loops aren't supported.</span></span>

    <span data-ttu-id="4793f-316">References to other web tests aren't supported.</span><span class="sxs-lookup"><span data-stu-id="4793f-316">References to other web tests aren't supported.</span></span>

    <span data-ttu-id="4793f-317">Data sources aren't supported.</span><span class="sxs-lookup"><span data-stu-id="4793f-317">Data sources aren't supported.</span></span>
* <span data-ttu-id="4793f-318">*My multi-step test doesn't complete*</span><span class="sxs-lookup"><span data-stu-id="4793f-318">*My multi-step test doesn't complete*</span></span>

    <span data-ttu-id="4793f-319">There's a limit of 100 requests per test.</span><span class="sxs-lookup"><span data-stu-id="4793f-319">There's a limit of 100 requests per test.</span></span>

    <span data-ttu-id="4793f-320">The test is stopped if it runs longer than two minutes.</span><span class="sxs-lookup"><span data-stu-id="4793f-320">The test is stopped if it runs longer than two minutes.</span></span>
* <span data-ttu-id="4793f-321">*How can I run a test with client certificates?*</span><span class="sxs-lookup"><span data-stu-id="4793f-321">*How can I run a test with client certificates?*</span></span>

    <span data-ttu-id="4793f-322">We don't support that, sorry.</span><span class="sxs-lookup"><span data-stu-id="4793f-322">We don't support that, sorry.</span></span>


## <a name="next"></a><span data-ttu-id="4793f-323">Next steps</span><span class="sxs-lookup"><span data-stu-id="4793f-323">Next steps</span></span>
<span data-ttu-id="4793f-324">[Search diagnostic logs][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="4793f-324">[Search diagnostic logs][diagnostic]</span></span>

<span data-ttu-id="4793f-325">[Troubleshooting][qna]</span><span class="sxs-lookup"><span data-stu-id="4793f-325">[Troubleshooting][qna]</span></span>

[<span data-ttu-id="4793f-326">IP addresses of web test agents</span><span class="sxs-lookup"><span data-stu-id="4793f-326">IP addresses of web test agents</span></span>](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md

















