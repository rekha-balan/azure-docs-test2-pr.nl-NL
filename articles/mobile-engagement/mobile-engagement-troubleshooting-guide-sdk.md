---
title: Azure Mobile Engagement Troubleshooting Guide - SDK
description: Troubleshooting SDK integration issues in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: ''
author: piyushjo
manager: erikre
editor: ''
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4d9d6165deb4bd0c65f1841aa7c457363a1f2865
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671806"
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="65fa3-103">Troubleshooting guide for SDK integration issues</span><span class="sxs-lookup"><span data-stu-id="65fa3-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="65fa3-104">The following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span><span class="sxs-lookup"><span data-stu-id="65fa3-104">The following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="65fa3-105">SDK issues discovered by a failure in another area of your application</span><span class="sxs-lookup"><span data-stu-id="65fa3-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="65fa3-106">Issue</span><span class="sxs-lookup"><span data-stu-id="65fa3-106">Issue</span></span>
* <span data-ttu-id="65fa3-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span><span class="sxs-lookup"><span data-stu-id="65fa3-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="65fa3-108">Push Failures (Pushes don't work in app, out of app, or both).</span><span class="sxs-lookup"><span data-stu-id="65fa3-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="65fa3-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span><span class="sxs-lookup"><span data-stu-id="65fa3-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="65fa3-110">API Failures (APIs fail often silently without error messages).</span><span class="sxs-lookup"><span data-stu-id="65fa3-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="65fa3-111">Service Failures (none of Azure Mobile Engagement works for your application).</span><span class="sxs-lookup"><span data-stu-id="65fa3-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="65fa3-112">Causes</span><span class="sxs-lookup"><span data-stu-id="65fa3-112">Causes</span></span>
* <span data-ttu-id="65fa3-113">Most issues that need to be resolved with the Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span><span class="sxs-lookup"><span data-stu-id="65fa3-113">Most issues that need to be resolved with the Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="65fa3-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need to complete the integration.</span><span class="sxs-lookup"><span data-stu-id="65fa3-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need to complete the integration.</span></span> 
* <span data-ttu-id="65fa3-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need to upgrade to the last version with the Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="65fa3-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need to upgrade to the last version with the Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="65fa3-116">Remember that there is a different version of the Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="65fa3-116">Remember that there is a different version of the Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="65fa3-117">SDK Integration</span><span class="sxs-lookup"><span data-stu-id="65fa3-117">SDK Integration</span></span>
* <span data-ttu-id="65fa3-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span><span class="sxs-lookup"><span data-stu-id="65fa3-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="65fa3-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span><span class="sxs-lookup"><span data-stu-id="65fa3-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="65fa3-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span><span class="sxs-lookup"><span data-stu-id="65fa3-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="65fa3-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span><span class="sxs-lookup"><span data-stu-id="65fa3-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="65fa3-122">Tracking not correctly integrated in SDK (Install store tracking).</span><span class="sxs-lookup"><span data-stu-id="65fa3-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="65fa3-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span><span class="sxs-lookup"><span data-stu-id="65fa3-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="65fa3-124">**See also:**</span><span class="sxs-lookup"><span data-stu-id="65fa3-124">**See also:**</span></span>

* <span data-ttu-id="65fa3-125">[SDK Documentation - Integration Guides][Link 5]</span><span class="sxs-lookup"><span data-stu-id="65fa3-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="65fa3-126">[Troubleshooting Guide - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="65fa3-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="65fa3-127">SDK Upgrade</span><span class="sxs-lookup"><span data-stu-id="65fa3-127">SDK Upgrade</span></span>
* <span data-ttu-id="65fa3-128">Need to upgrade SDK to resolve issues with older versions of the SDK (often related to newer versions of the device OS).</span><span class="sxs-lookup"><span data-stu-id="65fa3-128">Need to upgrade SDK to resolve issues with older versions of the SDK (often related to newer versions of the device OS).</span></span>
* <span data-ttu-id="65fa3-129">Uninstall all previous versions of your app from your device and reinstall the newest version of your app, the re-register your Device ID from the Azure Mobile Engagement UI to confirm that your device is using the newest version of your app.</span><span class="sxs-lookup"><span data-stu-id="65fa3-129">Uninstall all previous versions of your app from your device and reinstall the newest version of your app, the re-register your Device ID from the Azure Mobile Engagement UI to confirm that your device is using the newest version of your app.</span></span>

<span data-ttu-id="65fa3-130">**See also:**</span><span class="sxs-lookup"><span data-stu-id="65fa3-130">**See also:**</span></span>

* [<span data-ttu-id="65fa3-131">SDK Documentation - Release Notes</span><span class="sxs-lookup"><span data-stu-id="65fa3-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="65fa3-132">SDK Documentation - Upgrade Guides</span><span class="sxs-lookup"><span data-stu-id="65fa3-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="65fa3-133">SDK Other</span><span class="sxs-lookup"><span data-stu-id="65fa3-133">SDK Other</span></span>
* <span data-ttu-id="65fa3-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not to work (Android only).</span><span class="sxs-lookup"><span data-stu-id="65fa3-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not to work (Android only).</span></span>
* <span data-ttu-id="65fa3-135">A common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span><span class="sxs-lookup"><span data-stu-id="65fa3-135">A common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>

<span data-ttu-id="65fa3-136">**See also:**</span><span class="sxs-lookup"><span data-stu-id="65fa3-136">**See also:**</span></span>

* <span data-ttu-id="65fa3-137">[Concepts - Glossary][Link 6]</span><span class="sxs-lookup"><span data-stu-id="65fa3-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="65fa3-138">Advanced coding issues</span><span class="sxs-lookup"><span data-stu-id="65fa3-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="65fa3-139">Issue</span><span class="sxs-lookup"><span data-stu-id="65fa3-139">Issue</span></span>
* <span data-ttu-id="65fa3-140">Platform specific code not directly related to Azure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="65fa3-140">Platform specific code not directly related to Azure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="65fa3-141">Causes</span><span class="sxs-lookup"><span data-stu-id="65fa3-141">Causes</span></span>
* <span data-ttu-id="65fa3-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related to Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="65fa3-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related to Azure Mobile Engagement.</span></span> <span data-ttu-id="65fa3-143">You will need to consult documentation specific to the platform you are developing for in addition to Azure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="65fa3-143">You will need to consult documentation specific to the platform you are developing for in addition to Azure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="65fa3-144">Not correctly configuring "categories", prevents linking from a notification to another location either inside or outside of the app (Android only).</span><span class="sxs-lookup"><span data-stu-id="65fa3-144">Not correctly configuring "categories", prevents linking from a notification to another location either inside or outside of the app (Android only).</span></span> 
* <span data-ttu-id="65fa3-145">Not setting "UIKit.framework" to "optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span><span class="sxs-lookup"><span data-stu-id="65fa3-145">Not setting "UIKit.framework" to "optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="65fa3-146">Expired certificates or not correctly using the DEV or Prod version of the cert, causes push issues (iOS only).</span><span class="sxs-lookup"><span data-stu-id="65fa3-146">Expired certificates or not correctly using the DEV or Prod version of the cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="65fa3-147">There are some limitations inherent to a platform that Azure Mobile Engagement can't control (like how the system center works for out of app pushes in Android and iOS).</span><span class="sxs-lookup"><span data-stu-id="65fa3-147">There are some limitations inherent to a platform that Azure Mobile Engagement can't control (like how the system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="65fa3-148">Azure Mobile Engagement publishes a full list of the internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span><span class="sxs-lookup"><span data-stu-id="65fa3-148">Azure Mobile Engagement publishes a full list of the internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="65fa3-149">Keep in mind that some features of Azure Mobile Engagement are specific to the platform (Android, iOS, Web, Windows, and Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="65fa3-149">Keep in mind that some features of Azure Mobile Engagement are specific to the platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="65fa3-150">See also</span><span class="sxs-lookup"><span data-stu-id="65fa3-150">See also</span></span>
* <span data-ttu-id="65fa3-151">[Troubleshooting Guide - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="65fa3-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="65fa3-152">[SDK Documentation - Release Notes][Link 5]</span><span class="sxs-lookup"><span data-stu-id="65fa3-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="65fa3-153">[SDK Documentation - Upgrade Guides][Link 5]</span><span class="sxs-lookup"><span data-stu-id="65fa3-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="65fa3-154">Application crashes</span><span class="sxs-lookup"><span data-stu-id="65fa3-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="65fa3-155">Issue</span><span class="sxs-lookup"><span data-stu-id="65fa3-155">Issue</span></span>
* <span data-ttu-id="65fa3-156">Your application crashes on the end users' device.</span><span class="sxs-lookup"><span data-stu-id="65fa3-156">Your application crashes on the end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="65fa3-157">Causes</span><span class="sxs-lookup"><span data-stu-id="65fa3-157">Causes</span></span>
* <span data-ttu-id="65fa3-158">Crash information can be viewed in the *Analytics UI* or the *Analytics API*</span><span class="sxs-lookup"><span data-stu-id="65fa3-158">Crash information can be viewed in the *Analytics UI* or the *Analytics API*</span></span>
* <span data-ttu-id="65fa3-159">You can find the Device ID of your test device and take the same action that caused your application to crash for an end user to help identify the cause of your crash.</span><span class="sxs-lookup"><span data-stu-id="65fa3-159">You can find the Device ID of your test device and take the same action that caused your application to crash for an end user to help identify the cause of your crash.</span></span>
* <span data-ttu-id="65fa3-160">Known issues with the Azure Mobile Engagement SDK that cause applications to crash are sometimes resolved by upgrading to the latest version of the SDK.</span><span class="sxs-lookup"><span data-stu-id="65fa3-160">Known issues with the Azure Mobile Engagement SDK that cause applications to crash are sometimes resolved by upgrading to the latest version of the SDK.</span></span> <span data-ttu-id="65fa3-161">Make sure to check the release notes about your platform when investigating crashes.</span><span class="sxs-lookup"><span data-stu-id="65fa3-161">Make sure to check the release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="65fa3-162">See also</span><span class="sxs-lookup"><span data-stu-id="65fa3-162">See also</span></span>
* <span data-ttu-id="65fa3-163">[SDK Documentation - Release Notes][Link 5]</span><span class="sxs-lookup"><span data-stu-id="65fa3-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="65fa3-164">[SDK Documentation - Upgrade Guides][Link 5]</span><span class="sxs-lookup"><span data-stu-id="65fa3-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="65fa3-165">App store upload failures</span><span class="sxs-lookup"><span data-stu-id="65fa3-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="65fa3-166">Issue</span><span class="sxs-lookup"><span data-stu-id="65fa3-166">Issue</span></span>
* <span data-ttu-id="65fa3-167">Errors related to uploading the latest version of your app to Apple, Google, or the Windows App store.</span><span class="sxs-lookup"><span data-stu-id="65fa3-167">Errors related to uploading the latest version of your app to Apple, Google, or the Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="65fa3-168">Causes</span><span class="sxs-lookup"><span data-stu-id="65fa3-168">Causes</span></span>
* <span data-ttu-id="65fa3-169">App stores sometimes block apps with certain features enabled (e.g. the Apple Store prevents the use of IDFV in apps in the store and the GooglePlay store prevents the sharing of application information between apps).</span><span class="sxs-lookup"><span data-stu-id="65fa3-169">App stores sometimes block apps with certain features enabled (e.g. the Apple Store prevents the use of IDFV in apps in the store and the GooglePlay store prevents the sharing of application information between apps).</span></span> 
* <span data-ttu-id="65fa3-170">Make sure that you check the release notes about your platform and current version of the SDK if you have difficulty uploading an app to the store.</span><span class="sxs-lookup"><span data-stu-id="65fa3-170">Make sure that you check the release notes about your platform and current version of the SDK if you have difficulty uploading an app to the store.</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
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

