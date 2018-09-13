---
title: Azure Mobile Engagement Troubleshooting Guide - Analytics
description: Troubleshooting Analytics, Monitoring, Segmentation, and Dashboard issues in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: ''
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e30c9ac0a8421ffcf4fc3e2548cfd7ac49701900
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564275"
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="59283-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span><span class="sxs-lookup"><span data-stu-id="59283-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="59283-104">The following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span><span class="sxs-lookup"><span data-stu-id="59283-104">The following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="59283-105">Missing/Delayed information</span><span class="sxs-lookup"><span data-stu-id="59283-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="59283-106">Issue</span><span class="sxs-lookup"><span data-stu-id="59283-106">Issue</span></span>
* <span data-ttu-id="59283-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span><span class="sxs-lookup"><span data-stu-id="59283-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="59283-108">Information is missing from Monitoring.</span><span class="sxs-lookup"><span data-stu-id="59283-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="59283-109">Information is missing from Analytics, Segmentation, or Dashboard.</span><span class="sxs-lookup"><span data-stu-id="59283-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="59283-110">Hitting segmentation limits.</span><span class="sxs-lookup"><span data-stu-id="59283-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="59283-111">Causes</span><span class="sxs-lookup"><span data-stu-id="59283-111">Causes</span></span>
* <span data-ttu-id="59283-112">You can use the Analytics API, Monitor API, and Segments API to see if any data you are missing from the UI is visible through the APIs.</span><span class="sxs-lookup"><span data-stu-id="59283-112">You can use the Analytics API, Monitor API, and Segments API to see if any data you are missing from the UI is visible through the APIs.</span></span>
* <span data-ttu-id="59283-113">If the Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able to see information in the Analytics, Segmentation, Monitoring, or Dashboards.</span><span class="sxs-lookup"><span data-stu-id="59283-113">If the Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able to see information in the Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="59283-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span><span class="sxs-lookup"><span data-stu-id="59283-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="59283-115">Segments can only contain 10 criteria.</span><span class="sxs-lookup"><span data-stu-id="59283-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="59283-116">The best way to test missing information from monitoring is to setup a test device, uninstall and/or reinstall the app on the test device.</span><span class="sxs-lookup"><span data-stu-id="59283-116">The best way to test missing information from monitoring is to setup a test device, uninstall and/or reinstall the app on the test device.</span></span>
* <span data-ttu-id="59283-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span><span class="sxs-lookup"><span data-stu-id="59283-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="59283-118">Information in new segments may not be displayed until 24 hours after they are created even if the segment is based on previous information.</span><span class="sxs-lookup"><span data-stu-id="59283-118">Information in new segments may not be displayed until 24 hours after they are created even if the segment is based on previous information.</span></span>
* <span data-ttu-id="59283-119">Filtering your analytics data in the UI will show all examples of this type regardless of the version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span><span class="sxs-lookup"><span data-stu-id="59283-119">Filtering your analytics data in the UI will show all examples of this type regardless of the version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="59283-120">The time period for Analytics is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span><span class="sxs-lookup"><span data-stu-id="59283-120">The time period for Analytics is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span></span>
* <span data-ttu-id="59283-121">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span><span class="sxs-lookup"><span data-stu-id="59283-121">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="59283-122">Can't locate items in UI</span><span class="sxs-lookup"><span data-stu-id="59283-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="59283-123">Issue</span><span class="sxs-lookup"><span data-stu-id="59283-123">Issue</span></span>
* <span data-ttu-id="59283-124">Can't create segments based on certain built in or custom app info tag criteria.</span><span class="sxs-lookup"><span data-stu-id="59283-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="59283-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span><span class="sxs-lookup"><span data-stu-id="59283-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="59283-126">Can't interpret the data in Analytics, Monitoring, Segmentation, or Dashboards.</span><span class="sxs-lookup"><span data-stu-id="59283-126">Can't interpret the data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="59283-127">Causes</span><span class="sxs-lookup"><span data-stu-id="59283-127">Causes</span></span>
* <span data-ttu-id="59283-128">Some built in items and app info tags are only available as push criteria but may not be added to a segment or visible from Analytics, Monitoring, or Dashboard.</span><span class="sxs-lookup"><span data-stu-id="59283-128">Some built in items and app info tags are only available as push criteria but may not be added to a segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="59283-129">For built in items and app info tags that can't be added to a segment, you will need to setup list of targeting criteria in each campaign to perform the same function as targeting based on a segment.</span><span class="sxs-lookup"><span data-stu-id="59283-129">For built in items and app info tags that can't be added to a segment, you will need to setup list of targeting criteria in each campaign to perform the same function as targeting based on a segment.</span></span>
* <span data-ttu-id="59283-130">See the context menus in the Analytics, Monitoring, Segmentation, and Dashboards sections of the Azure Mobile Engagement UI for more help and how to information.</span><span class="sxs-lookup"><span data-stu-id="59283-130">See the context menus in the Analytics, Monitoring, Segmentation, and Dashboards sections of the Azure Mobile Engagement UI for more help and how to information.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="59283-131">Crash troubleshooting</span><span class="sxs-lookup"><span data-stu-id="59283-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="59283-132">Issue</span><span class="sxs-lookup"><span data-stu-id="59283-132">Issue</span></span>
* <span data-ttu-id="59283-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span><span class="sxs-lookup"><span data-stu-id="59283-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="59283-134">Causes</span><span class="sxs-lookup"><span data-stu-id="59283-134">Causes</span></span>
* <span data-ttu-id="59283-135">To troubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure to check the release notes for known issues with previous versions of the SDK.</span><span class="sxs-lookup"><span data-stu-id="59283-135">To troubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure to check the release notes for known issues with previous versions of the SDK.</span></span>
* <span data-ttu-id="59283-136">To further troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in the “Monitor – Events” section of the Azure Mobile Engagement UI.</span><span class="sxs-lookup"><span data-stu-id="59283-136">To further troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in the “Monitor – Events” section of the Azure Mobile Engagement UI.</span></span> <span data-ttu-id="59283-137">Then perform the event that is causing your application to crash and look up additional information in the “Monitor – Crash” section of the Azure Mobile Engagement UI.</span><span class="sxs-lookup"><span data-stu-id="59283-137">Then perform the event that is causing your application to crash and look up additional information in the “Monitor – Crash” section of the Azure Mobile Engagement UI.</span></span> 

