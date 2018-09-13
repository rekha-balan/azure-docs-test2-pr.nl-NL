---
title: Troubleshoot Azure Log Analytics Linux Agent | Microsoft Docs
description: Describe the symptoms, causes, and resolution for the most common issues with the Log Analytics Linux agent.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/14/2018
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 49a53b68fd394772f38b6040b80ec80c93d9c46c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869506"
---
# <a name="how-to-troubleshoot-issues-with-the-linux-agent-for-log-analytics"></a><span data-ttu-id="24a75-103">How to troubleshoot issues with the Linux agent for Log Analytics</span><span class="sxs-lookup"><span data-stu-id="24a75-103">How to troubleshoot issues with the Linux agent for Log Analytics</span></span>

<span data-ttu-id="24a75-104">This article provides help troubleshooting errors you might experience with the Linux agent for Log Analytics and suggests possible solutions to resolve them.</span><span class="sxs-lookup"><span data-stu-id="24a75-104">This article provides help troubleshooting errors you might experience with the Linux agent for Log Analytics and suggests possible solutions to resolve them.</span></span>

## <a name="issue-unable-to-connect-through-proxy-to-log-analytics"></a><span data-ttu-id="24a75-105">Issue: Unable to connect through proxy to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="24a75-105">Issue: Unable to connect through proxy to Log Analytics</span></span>

### <a name="probable-causes"></a><span data-ttu-id="24a75-106">Probable causes</span><span class="sxs-lookup"><span data-stu-id="24a75-106">Probable causes</span></span>
* <span data-ttu-id="24a75-107">The proxy specified during onboarding was incorrect</span><span class="sxs-lookup"><span data-stu-id="24a75-107">The proxy specified during onboarding was incorrect</span></span>
* <span data-ttu-id="24a75-108">The Log Analytics and Azure Automation Service Endpoints are not whitelisted in your datacenter</span><span class="sxs-lookup"><span data-stu-id="24a75-108">The Log Analytics and Azure Automation Service Endpoints are not whitelisted in your datacenter</span></span> 

### <a name="resolutions"></a><span data-ttu-id="24a75-109">Resolutions</span><span class="sxs-lookup"><span data-stu-id="24a75-109">Resolutions</span></span>
1. <span data-ttu-id="24a75-110">Reonboard to the Log Analytics service with the OMS Agent for Linux by using the following command with the option `-v` enabled.</span><span class="sxs-lookup"><span data-stu-id="24a75-110">Reonboard to the Log Analytics service with the OMS Agent for Linux by using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="24a75-111">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span><span class="sxs-lookup"><span data-stu-id="24a75-111">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span> 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. <span data-ttu-id="24a75-112">Review the section [Update proxy settings](log-analytics-agent-manage.md#update-proxy-settings) to verify you have properly configured the agent to communicate through a proxy server.</span><span class="sxs-lookup"><span data-stu-id="24a75-112">Review the section [Update proxy settings](log-analytics-agent-manage.md#update-proxy-settings) to verify you have properly configured the agent to communicate through a proxy server.</span></span>    
* <span data-ttu-id="24a75-113">Double check that the following Log Analytics service endpoints are whitelisted:</span><span class="sxs-lookup"><span data-stu-id="24a75-113">Double check that the following Log Analytics service endpoints are whitelisted:</span></span>

    |<span data-ttu-id="24a75-114">Agent Resource</span><span class="sxs-lookup"><span data-stu-id="24a75-114">Agent Resource</span></span>| <span data-ttu-id="24a75-115">Ports</span><span class="sxs-lookup"><span data-stu-id="24a75-115">Ports</span></span> | <span data-ttu-id="24a75-116">Direction</span><span class="sxs-lookup"><span data-stu-id="24a75-116">Direction</span></span> |
    |------|---------|----------|  
    |<span data-ttu-id="24a75-117">\*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="24a75-117">\*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="24a75-118">Port 443</span><span class="sxs-lookup"><span data-stu-id="24a75-118">Port 443</span></span>| <span data-ttu-id="24a75-119">Inbound and outbound</span><span class="sxs-lookup"><span data-stu-id="24a75-119">Inbound and outbound</span></span> |  
    |<span data-ttu-id="24a75-120">\*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="24a75-120">\*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="24a75-121">Port 443</span><span class="sxs-lookup"><span data-stu-id="24a75-121">Port 443</span></span>| <span data-ttu-id="24a75-122">Inbound and outbound</span><span class="sxs-lookup"><span data-stu-id="24a75-122">Inbound and outbound</span></span> |  
    |<span data-ttu-id="24a75-123">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="24a75-123">\*.blob.core.windows.net</span></span> | <span data-ttu-id="24a75-124">Port 443</span><span class="sxs-lookup"><span data-stu-id="24a75-124">Port 443</span></span>| <span data-ttu-id="24a75-125">Inbound and outbound</span><span class="sxs-lookup"><span data-stu-id="24a75-125">Inbound and outbound</span></span> |  
    |<span data-ttu-id="24a75-126">\*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="24a75-126">\*.azure-automation.net</span></span> | <span data-ttu-id="24a75-127">Port 443</span><span class="sxs-lookup"><span data-stu-id="24a75-127">Port 443</span></span>| <span data-ttu-id="24a75-128">Inbound and outbound</span><span class="sxs-lookup"><span data-stu-id="24a75-128">Inbound and outbound</span></span> | 

## <a name="issue-you-receive-a-403-error-when-trying-to-onboard"></a><span data-ttu-id="24a75-129">Issue: You receive a 403 error when trying to onboard</span><span class="sxs-lookup"><span data-stu-id="24a75-129">Issue: You receive a 403 error when trying to onboard</span></span>

### <a name="probable-causes"></a><span data-ttu-id="24a75-130">Probable causes</span><span class="sxs-lookup"><span data-stu-id="24a75-130">Probable causes</span></span>
* <span data-ttu-id="24a75-131">Date and Time is incorrect on Linux Server</span><span class="sxs-lookup"><span data-stu-id="24a75-131">Date and Time is incorrect on Linux Server</span></span> 
* <span data-ttu-id="24a75-132">Workspace ID and Workspace Key used are not correct</span><span class="sxs-lookup"><span data-stu-id="24a75-132">Workspace ID and Workspace Key used are not correct</span></span>

### <a name="resolution"></a><span data-ttu-id="24a75-133">Resolution</span><span class="sxs-lookup"><span data-stu-id="24a75-133">Resolution</span></span>

1. <span data-ttu-id="24a75-134">Check the time on your Linux server with the command date.</span><span class="sxs-lookup"><span data-stu-id="24a75-134">Check the time on your Linux server with the command date.</span></span> <span data-ttu-id="24a75-135">If the time is +/- 15 minutes from current time, then onboarding fails.</span><span class="sxs-lookup"><span data-stu-id="24a75-135">If the time is +/- 15 minutes from current time, then onboarding fails.</span></span> <span data-ttu-id="24a75-136">To correct this update the date and/or timezone of your Linux server.</span><span class="sxs-lookup"><span data-stu-id="24a75-136">To correct this update the date and/or timezone of your Linux server.</span></span> 
2. <span data-ttu-id="24a75-137">Verify you have installed the latest version of the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="24a75-137">Verify you have installed the latest version of the OMS Agent for Linux.</span></span>  <span data-ttu-id="24a75-138">The newest version now notifies you if time skew is causing the onboarding failure.</span><span class="sxs-lookup"><span data-stu-id="24a75-138">The newest version now notifies you if time skew is causing the onboarding failure.</span></span>
3. <span data-ttu-id="24a75-139">Reonboard using correct Workspace ID and Workspace Key following the installation instructions earlier in this topic.</span><span class="sxs-lookup"><span data-stu-id="24a75-139">Reonboard using correct Workspace ID and Workspace Key following the installation instructions earlier in this topic.</span></span>

## <a name="issue-you-see-a-500-and-404-error-in-the-log-file-right-after-onboarding"></a><span data-ttu-id="24a75-140">Issue: You see a 500 and 404 error in the log file right after onboarding</span><span class="sxs-lookup"><span data-stu-id="24a75-140">Issue: You see a 500 and 404 error in the log file right after onboarding</span></span>
<span data-ttu-id="24a75-141">This is a known issue that occurs on first upload of Linux data into a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="24a75-141">This is a known issue that occurs on first upload of Linux data into a Log Analytics workspace.</span></span> <span data-ttu-id="24a75-142">This does not affect data being sent or service experience.</span><span class="sxs-lookup"><span data-stu-id="24a75-142">This does not affect data being sent or service experience.</span></span>

## <a name="issue-you-are-not-seeing-any-data-in-the-azure-portal"></a><span data-ttu-id="24a75-143">Issue: You are not seeing any data in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="24a75-143">Issue: You are not seeing any data in the Azure portal</span></span>

### <a name="probable-causes"></a><span data-ttu-id="24a75-144">Probable causes</span><span class="sxs-lookup"><span data-stu-id="24a75-144">Probable causes</span></span>

- <span data-ttu-id="24a75-145">Onboarding to the Log Analytics service failed</span><span class="sxs-lookup"><span data-stu-id="24a75-145">Onboarding to the Log Analytics service failed</span></span>
- <span data-ttu-id="24a75-146">Connection to the Log Analytics service is blocked</span><span class="sxs-lookup"><span data-stu-id="24a75-146">Connection to the Log Analytics service is blocked</span></span>
- <span data-ttu-id="24a75-147">OMS Agent for Linux data is backed up</span><span class="sxs-lookup"><span data-stu-id="24a75-147">OMS Agent for Linux data is backed up</span></span>

### <a name="resolutions"></a><span data-ttu-id="24a75-148">Resolutions</span><span class="sxs-lookup"><span data-stu-id="24a75-148">Resolutions</span></span>
1. <span data-ttu-id="24a75-149">Check if onboarding the Log Analytics service was successful by checking if the following file exists: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span><span class="sxs-lookup"><span data-stu-id="24a75-149">Check if onboarding the Log Analytics service was successful by checking if the following file exists: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span></span>
2. <span data-ttu-id="24a75-150">Reonboard using the `omsadmin.sh` command-line instructions</span><span class="sxs-lookup"><span data-stu-id="24a75-150">Reonboard using the `omsadmin.sh` command-line instructions</span></span>
3. <span data-ttu-id="24a75-151">If using a proxy, refer to the proxy resolution steps provided earlier.</span><span class="sxs-lookup"><span data-stu-id="24a75-151">If using a proxy, refer to the proxy resolution steps provided earlier.</span></span>
4. <span data-ttu-id="24a75-152">In some cases, when the OMS Agent for Linux cannot communicate with the service, data on the agent is queued to the full buffer size, which is 50 MB.</span><span class="sxs-lookup"><span data-stu-id="24a75-152">In some cases, when the OMS Agent for Linux cannot communicate with the service, data on the agent is queued to the full buffer size, which is 50 MB.</span></span> <span data-ttu-id="24a75-153">The OMS Agent for Linux should be restarted by running the following command: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span><span class="sxs-lookup"><span data-stu-id="24a75-153">The OMS Agent for Linux should be restarted by running the following command: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="24a75-154">This issue is fixed in agent version 1.1.0-28 and later.</span><span class="sxs-lookup"><span data-stu-id="24a75-154">This issue is fixed in agent version 1.1.0-28 and later.</span></span>

