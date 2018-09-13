---
title: Troubleshoot Analytics in Azure Application Insights | Microsoft Docs
description: 'Problems with Application Insights analytics? Start here. '
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2016
ms.author: mbullwin
ms.openlocfilehash: eeda0fa6ad8faa05baf0a9344e958d298fb80d8e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782284"
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="eff58-104">Troubleshoot Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="eff58-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="eff58-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="eff58-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="eff58-106">Start here.</span><span class="sxs-lookup"><span data-stu-id="eff58-106">Start here.</span></span> <span data-ttu-id="eff58-107">Analytics is the powerful search tool of Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="eff58-107">Analytics is the powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="eff58-108">Limits</span><span class="sxs-lookup"><span data-stu-id="eff58-108">Limits</span></span>
* <span data-ttu-id="eff58-109">At present, query results are limited to just over a week of past data.</span><span class="sxs-lookup"><span data-stu-id="eff58-109">At present, query results are limited to just over a week of past data.</span></span>
* <span data-ttu-id="eff58-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="eff58-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="eff58-111">Known incompatible browser extensions</span><span class="sxs-lookup"><span data-stu-id="eff58-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="eff58-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="eff58-112">Ghostery</span></span>

<span data-ttu-id="eff58-113">Disable the extension or use a different browser.</span><span class="sxs-lookup"><span data-stu-id="eff58-113">Disable the extension or use a different browser.</span></span>

## <a name="e-a"></a> <span data-ttu-id="eff58-114">"Unexpected error"</span><span class="sxs-lookup"><span data-stu-id="eff58-114">"Unexpected error"</span></span>
![Unexpected error screen](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="eff58-116">Internal error occurred during portal runtime – unhandled exception.</span><span class="sxs-lookup"><span data-stu-id="eff58-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="eff58-117">Clean the browser's cache.</span><span class="sxs-lookup"><span data-stu-id="eff58-117">Clean the browser's cache.</span></span> 

## <a name="e-b"></a><span data-ttu-id="eff58-118">403 ... please try to reload</span><span class="sxs-lookup"><span data-stu-id="eff58-118">403 ... please try to reload</span></span>
![403 ... please try to reload](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="eff58-120">An authentication related error occurred (during authentication or during access token generation).</span><span class="sxs-lookup"><span data-stu-id="eff58-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="eff58-121">The portal may have no way to  recover without changing browser settings.</span><span class="sxs-lookup"><span data-stu-id="eff58-121">The portal may have no way to  recover without changing browser settings.</span></span>

* <span data-ttu-id="eff58-122">Verify [third party cookies are enabled](#cookies) in the browser.</span><span class="sxs-lookup"><span data-stu-id="eff58-122">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 

## <a name="authentication"></a><span data-ttu-id="eff58-123">403 ... verify security zone</span><span class="sxs-lookup"><span data-stu-id="eff58-123">403 ... verify security zone</span></span>
![403 ...verify security zone](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="eff58-125">An authentication related error occurred (during authentication or during access token generation).</span><span class="sxs-lookup"><span data-stu-id="eff58-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="eff58-126">The portal may have no way to  recover without changing browser settings.</span><span class="sxs-lookup"><span data-stu-id="eff58-126">The portal may have no way to  recover without changing browser settings.</span></span>

1. <span data-ttu-id="eff58-127">Verify [third party cookies are enabled](#cookies) in the browser.</span><span class="sxs-lookup"><span data-stu-id="eff58-127">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 
2. <span data-ttu-id="eff58-128">Did you use a favorite, bookmark or saved link to open the Analytics portal?</span><span class="sxs-lookup"><span data-stu-id="eff58-128">Did you use a favorite, bookmark or saved link to open the Analytics portal?</span></span> <span data-ttu-id="eff58-129">Are you signed in with different credentials than you used when you saved the link?</span><span class="sxs-lookup"><span data-stu-id="eff58-129">Are you signed in with different credentials than you used when you saved the link?</span></span>
3. <span data-ttu-id="eff58-130">Try using an in-private/incognito browser window (after closing all such windows).</span><span class="sxs-lookup"><span data-stu-id="eff58-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="eff58-131">You'll have to provide your credentials.</span><span class="sxs-lookup"><span data-stu-id="eff58-131">You'll have to provide your credentials.</span></span> 
4. <span data-ttu-id="eff58-132">Open another (ordinary) browser window and go to [Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eff58-132">Open another (ordinary) browser window and go to [Azure](https://portal.azure.com).</span></span> <span data-ttu-id="eff58-133">Sign out. Then open your link and sign in with the correct credentials.</span><span class="sxs-lookup"><span data-stu-id="eff58-133">Sign out. Then open your link and sign in with the correct credentials.</span></span>
5. <span data-ttu-id="eff58-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span><span class="sxs-lookup"><span data-stu-id="eff58-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="eff58-135">Verify both [Analytics portal](https://portal.azure.com) and [Azure Active Directory portal](https://portal.azure.com) are in the same security zone:</span><span class="sxs-lookup"><span data-stu-id="eff58-135">Verify both [Analytics portal](https://portal.azure.com) and [Azure Active Directory portal](https://portal.azure.com) are in the same security zone:</span></span>
   
   * <span data-ttu-id="eff58-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span><span class="sxs-lookup"><span data-stu-id="eff58-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Internet Options dialog, adding a site to Trusted Sites](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="eff58-138">In the Websites list, if any of the following URLs are included, make sure that the others are included also:</span><span class="sxs-lookup"><span data-stu-id="eff58-138">In the Websites list, if any of the following URLs are included, make sure that the others are included also:</span></span>
     
     https://analytics.applicationinsights.io<br/>
     <span data-ttu-id="eff58-139">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="eff58-139">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="eff58-140">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="eff58-140">https://login.windows.net</span></span>

## <a name="e-d"></a><span data-ttu-id="eff58-141">404 ... Resource not found</span><span class="sxs-lookup"><span data-stu-id="eff58-141">404 ... Resource not found</span></span>
![404 ... resource not found](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="eff58-143">Application resource was deleted from Application Insights and isn’t available anymore.</span><span class="sxs-lookup"><span data-stu-id="eff58-143">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="eff58-144">This can happen if you saved the URL to the Analytics page.</span><span class="sxs-lookup"><span data-stu-id="eff58-144">This can happen if you saved the URL to the Analytics page.</span></span>

## <a name="e-e"></a><span data-ttu-id="eff58-145">403 ... No authorization</span><span class="sxs-lookup"><span data-stu-id="eff58-145">403 ... No authorization</span></span>
![403 ... not authorized](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="eff58-147">You don't have permission to open this application in Analytics.</span><span class="sxs-lookup"><span data-stu-id="eff58-147">You don't have permission to open this application in Analytics.</span></span>

* <span data-ttu-id="eff58-148">Did you get the link from someone else?</span><span class="sxs-lookup"><span data-stu-id="eff58-148">Did you get the link from someone else?</span></span> <span data-ttu-id="eff58-149">Ask them to make sure you are in the [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="eff58-149">Ask them to make sure you are in the [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="eff58-150">Did you save the link using different credentials?</span><span class="sxs-lookup"><span data-stu-id="eff58-150">Did you save the link using different credentials?</span></span> <span data-ttu-id="eff58-151">Open the [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing the correct credentials.</span><span class="sxs-lookup"><span data-stu-id="eff58-151">Open the [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing the correct credentials.</span></span>

## <a name="html-storage"></a><span data-ttu-id="eff58-152">403 ... HTML5 Storage</span><span class="sxs-lookup"><span data-stu-id="eff58-152">403 ... HTML5 Storage</span></span>
<span data-ttu-id="eff58-153">Our portal uses HTML5 localStorage and sessionStorage.</span><span class="sxs-lookup"><span data-stu-id="eff58-153">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="eff58-154">Chrome: Settings, privacy, content settings.</span><span class="sxs-lookup"><span data-stu-id="eff58-154">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="eff58-155">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span><span class="sxs-lookup"><span data-stu-id="eff58-155">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403 ... try to enable HTML5 storage](./media/app-insights-analytics-troubleshooting/060.png)

## <a name="e-g"></a><span data-ttu-id="eff58-157">404 ... Subscription not found</span><span class="sxs-lookup"><span data-stu-id="eff58-157">404 ... Subscription not found</span></span>
![404 ... Subscription not found](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="eff58-159">The URL is invalid.</span><span class="sxs-lookup"><span data-stu-id="eff58-159">The URL is invalid.</span></span> 

* <span data-ttu-id="eff58-160">Open the app resource in [Application Insights portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eff58-160">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="eff58-161">Then use the Analytics button.</span><span class="sxs-lookup"><span data-stu-id="eff58-161">Then use the Analytics button.</span></span>

## <a name="e-h"></a><span data-ttu-id="eff58-162">404 ... page doesn't exist</span><span class="sxs-lookup"><span data-stu-id="eff58-162">404 ... page doesn't exist</span></span>
![404 ... Page does not exist](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="eff58-164">The URL is invalid.</span><span class="sxs-lookup"><span data-stu-id="eff58-164">The URL is invalid.</span></span>

* <span data-ttu-id="eff58-165">Open the app resource in [Application Insights portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eff58-165">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="eff58-166">Then use the Analytics button.</span><span class="sxs-lookup"><span data-stu-id="eff58-166">Then use the Analytics button.</span></span>

## <a name="cookies"></a><span data-ttu-id="eff58-167">Enable third-party cookies</span><span class="sxs-lookup"><span data-stu-id="eff58-167">Enable third-party cookies</span></span>
  <span data-ttu-id="eff58-168">See [how to disable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need to **enable** them.</span><span class="sxs-lookup"><span data-stu-id="eff58-168">See [how to disable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need to **enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

