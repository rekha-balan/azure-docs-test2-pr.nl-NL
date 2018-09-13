---
title: Azure Mobile Engagement Troubleshooting Guide - Service
description: Troubleshooting Guides for Azure Mobile Engagement
services: mobile-engagement
documentationcenter: ''
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f13fd0540b783120014b3a8d4e41f78808c7fade
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540805"
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="ec8c9-103">Troubleshooting guide for Service issues</span><span class="sxs-lookup"><span data-stu-id="ec8c9-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="ec8c9-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="ec8c9-105">Service Outages</span><span class="sxs-lookup"><span data-stu-id="ec8c9-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="ec8c9-106">Issue</span><span class="sxs-lookup"><span data-stu-id="ec8c9-106">Issue</span></span>
* <span data-ttu-id="ec8c9-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="ec8c9-108">Causes</span><span class="sxs-lookup"><span data-stu-id="ec8c9-108">Causes</span></span>
* <span data-ttu-id="ec8c9-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span><span class="sxs-lookup"><span data-stu-id="ec8c9-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="ec8c9-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ec8c9-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="ec8c9-111">Known issues caused by server outages (not always shows in server status):</span><span class="sxs-lookup"><span data-stu-id="ec8c9-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="ec8c9-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="ec8c9-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="ec8c9-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="ec8c9-114">Push Notification Services (PNS) Dependency Outages</span><span class="sxs-lookup"><span data-stu-id="ec8c9-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="ec8c9-115">App Store Outages</span><span class="sxs-lookup"><span data-stu-id="ec8c9-115">App Store Outages</span></span>

1) <span data-ttu-id="ec8c9-116">To test to see if the problem is systemic you can test the same function from a different</span><span class="sxs-lookup"><span data-stu-id="ec8c9-116">To test to see if the problem is systemic you can test the same function from a different</span></span>

* <span data-ttu-id="ec8c9-117">Azure Mobile Engagement integrated application</span><span class="sxs-lookup"><span data-stu-id="ec8c9-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="ec8c9-118">Test device</span><span class="sxs-lookup"><span data-stu-id="ec8c9-118">Test device</span></span>
* <span data-ttu-id="ec8c9-119">Test device OS version</span><span class="sxs-lookup"><span data-stu-id="ec8c9-119">Test device OS version</span></span>
* <span data-ttu-id="ec8c9-120">Campaign</span><span class="sxs-lookup"><span data-stu-id="ec8c9-120">Campaign</span></span>
* <span data-ttu-id="ec8c9-121">Administrator user account</span><span class="sxs-lookup"><span data-stu-id="ec8c9-121">Administrator user account</span></span>
* <span data-ttu-id="ec8c9-122">Browser (IE, Firefox, Chrome, etc.)</span><span class="sxs-lookup"><span data-stu-id="ec8c9-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="ec8c9-123">Computer</span><span class="sxs-lookup"><span data-stu-id="ec8c9-123">Computer</span></span>

2) <span data-ttu-id="ec8c9-124">To test if the problem only affects the UI or the API's:</span><span class="sxs-lookup"><span data-stu-id="ec8c9-124">To test if the problem only affects the UI or the API's:</span></span>

* <span data-ttu-id="ec8c9-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="ec8c9-126">To test if the problem is with your Cellular Phone Network:</span><span class="sxs-lookup"><span data-stu-id="ec8c9-126">To test if the problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="ec8c9-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="ec8c9-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="ec8c9-129">To test if the problem is with your Device:</span><span class="sxs-lookup"><span data-stu-id="ec8c9-129">To test if the problem is with your Device:</span></span>

* <span data-ttu-id="ec8c9-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="ec8c9-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="ec8c9-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span></span> 

5) <span data-ttu-id="ec8c9-133">To test if the problem is with your App:</span><span class="sxs-lookup"><span data-stu-id="ec8c9-133">To test if the problem is with your App:</span></span>

* <span data-ttu-id="ec8c9-134">Install and test your application from an emulator instead of from a physical device:</span><span class="sxs-lookup"><span data-stu-id="ec8c9-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="ec8c9-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span><span class="sxs-lookup"><span data-stu-id="ec8c9-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span></span>

* <span data-ttu-id="ec8c9-136">Test your application on different devices with different versions of the OS.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-136">Test your application on different devices with different versions of the OS.</span></span>
* <span data-ttu-id="ec8c9-137">Confirm that you are using the most recent version of the SDK.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-137">Confirm that you are using the most recent version of the SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="ec8c9-138">Connectivity and Incorrect Information Issues</span><span class="sxs-lookup"><span data-stu-id="ec8c9-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="ec8c9-139">Issue</span><span class="sxs-lookup"><span data-stu-id="ec8c9-139">Issue</span></span>
* <span data-ttu-id="ec8c9-140">Problems logging into the Azure Mobile Engagement UI.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-140">Problems logging into the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="ec8c9-141">Connection errors with the Azure Mobile Engagement API's.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-141">Connection errors with the Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="ec8c9-142">Problems uploading App Info Tags via the Device API.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-142">Problems uploading App Info Tags via the Device API.</span></span>
* <span data-ttu-id="ec8c9-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="ec8c9-144">Incorrect information shown in the Azure Mobile Engagement UI.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-144">Incorrect information shown in the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="ec8c9-145">Incorrect information shown in Azure Mobile Engagement logs.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="ec8c9-146">Causes</span><span class="sxs-lookup"><span data-stu-id="ec8c9-146">Causes</span></span>
* <span data-ttu-id="ec8c9-147">Confirm your user account has sufficient permissions to perform the task.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-147">Confirm your user account has sufficient permissions to perform the task.</span></span>
* <span data-ttu-id="ec8c9-148">Confirm that the problem is not isolated to one computer or your local network.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-148">Confirm that the problem is not isolated to one computer or your local network.</span></span>
* <span data-ttu-id="ec8c9-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="ec8c9-150">Confirm that your App Info Tag files follow all of these rules:</span><span class="sxs-lookup"><span data-stu-id="ec8c9-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="ec8c9-151">Use only the UTF8 character set (the ANSI character set is not supported).</span><span class="sxs-lookup"><span data-stu-id="ec8c9-151">Use only the UTF8 character set (the ANSI character set is not supported).</span></span>
  * <span data-ttu-id="ec8c9-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span><span class="sxs-lookup"><span data-stu-id="ec8c9-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="ec8c9-153">Use all lower case for Boolean values "true" and "false".</span><span class="sxs-lookup"><span data-stu-id="ec8c9-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="ec8c9-154">Use a file that is smaller than the maximum file size of 35MB.</span><span class="sxs-lookup"><span data-stu-id="ec8c9-154">Use a file that is smaller than the maximum file size of 35MB.</span></span>

