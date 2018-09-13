---
title: IIS logs in Log Analytics | Microsoft Docs
description: Internet Information Services (IIS) stores user activity in log files that can be collected by Log Analytics.  This article describes how to configure collection of IIS logs and details of the records they create in the OMS repository.
services: log-analytics
documentationcenter: ''
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2017
ms.author: bwren
ms.openlocfilehash: 198cc1dd540d0519c35208dd8ef1e2857c0b7b9b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563200"
---
# <a name="iis-logs-in-log-analytics"></a><span data-ttu-id="975f3-104">IIS logs in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="975f3-104">IIS logs in Log Analytics</span></span>
<span data-ttu-id="975f3-105">Internet Information Services (IIS) stores user activity in log files that can be collected by Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="975f3-105">Internet Information Services (IIS) stores user activity in log files that can be collected by Log Analytics.</span></span>  

![IIS logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a><span data-ttu-id="975f3-107">Configuring IIS logs</span><span class="sxs-lookup"><span data-stu-id="975f3-107">Configuring IIS logs</span></span>
<span data-ttu-id="975f3-108">Log Analytics collects entries from log files created by IIS, so you must [configure IIS for logging](https://technet.microsoft.com/library/hh831775.aspx).</span><span class="sxs-lookup"><span data-stu-id="975f3-108">Log Analytics collects entries from log files created by IIS, so you must [configure IIS for logging](https://technet.microsoft.com/library/hh831775.aspx).</span></span>

<span data-ttu-id="975f3-109">Log Analytics only supports IIS log files stored in W3C format and does not support custom fields or IIS Advanced Logging.</span><span class="sxs-lookup"><span data-stu-id="975f3-109">Log Analytics only supports IIS log files stored in W3C format and does not support custom fields or IIS Advanced Logging.</span></span>  
<span data-ttu-id="975f3-110">Log Analytics does not collect logs in NCSA or IIS native format.</span><span class="sxs-lookup"><span data-stu-id="975f3-110">Log Analytics does not collect logs in NCSA or IIS native format.</span></span>

<span data-ttu-id="975f3-111">Configure IIS logs in Log Analytics from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="975f3-111">Configure IIS logs in Log Analytics from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="975f3-112">There is no configuration required other than selecting **Collect W3C format IIS log files**.</span><span class="sxs-lookup"><span data-stu-id="975f3-112">There is no configuration required other than selecting **Collect W3C format IIS log files**.</span></span>

<span data-ttu-id="975f3-113">We recommend that when you enable IIS log collection, you should configure the IIS log rollover setting on each server.</span><span class="sxs-lookup"><span data-stu-id="975f3-113">We recommend that when you enable IIS log collection, you should configure the IIS log rollover setting on each server.</span></span>

## <a name="data-collection"></a><span data-ttu-id="975f3-114">Data collection</span><span class="sxs-lookup"><span data-stu-id="975f3-114">Data collection</span></span>
<span data-ttu-id="975f3-115">Log Analytics collects IIS log entries from each connected source approximately every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="975f3-115">Log Analytics collects IIS log entries from each connected source approximately every 15 minutes.</span></span>  <span data-ttu-id="975f3-116">The agent records its place in each event log that it collects from.</span><span class="sxs-lookup"><span data-stu-id="975f3-116">The agent records its place in each event log that it collects from.</span></span>  <span data-ttu-id="975f3-117">If the agent goes offline, then Log Analytics collects events from where it last left off, even if those events were created while the agent was offline.</span><span class="sxs-lookup"><span data-stu-id="975f3-117">If the agent goes offline, then Log Analytics collects events from where it last left off, even if those events were created while the agent was offline.</span></span>

## <a name="iis-log-record-properties"></a><span data-ttu-id="975f3-118">IIS log record properties</span><span class="sxs-lookup"><span data-stu-id="975f3-118">IIS log record properties</span></span>
<span data-ttu-id="975f3-119">IIS log records have a type of **W3CIISLog** and have the properties in the following table:</span><span class="sxs-lookup"><span data-stu-id="975f3-119">IIS log records have a type of **W3CIISLog** and have the properties in the following table:</span></span>

| <span data-ttu-id="975f3-120">Property</span><span class="sxs-lookup"><span data-stu-id="975f3-120">Property</span></span> | <span data-ttu-id="975f3-121">Description</span><span class="sxs-lookup"><span data-stu-id="975f3-121">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="975f3-122">Computer</span><span class="sxs-lookup"><span data-stu-id="975f3-122">Computer</span></span> |<span data-ttu-id="975f3-123">Name of the computer that the event was collected from.</span><span class="sxs-lookup"><span data-stu-id="975f3-123">Name of the computer that the event was collected from.</span></span> |
| <span data-ttu-id="975f3-124">cIP</span><span class="sxs-lookup"><span data-stu-id="975f3-124">cIP</span></span> |<span data-ttu-id="975f3-125">IP address of the client.</span><span class="sxs-lookup"><span data-stu-id="975f3-125">IP address of the client.</span></span> |
| <span data-ttu-id="975f3-126">csMethod</span><span class="sxs-lookup"><span data-stu-id="975f3-126">csMethod</span></span> |<span data-ttu-id="975f3-127">Method of the request such as GET or POST.</span><span class="sxs-lookup"><span data-stu-id="975f3-127">Method of the request such as GET or POST.</span></span> |
| <span data-ttu-id="975f3-128">csReferer</span><span class="sxs-lookup"><span data-stu-id="975f3-128">csReferer</span></span> |<span data-ttu-id="975f3-129">Site that the user followed a link from to the current site.</span><span class="sxs-lookup"><span data-stu-id="975f3-129">Site that the user followed a link from to the current site.</span></span> |
| <span data-ttu-id="975f3-130">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="975f3-130">csUserAgent</span></span> |<span data-ttu-id="975f3-131">Browser type of the client.</span><span class="sxs-lookup"><span data-stu-id="975f3-131">Browser type of the client.</span></span> |
| <span data-ttu-id="975f3-132">csUserName</span><span class="sxs-lookup"><span data-stu-id="975f3-132">csUserName</span></span> |<span data-ttu-id="975f3-133">Name of the authenticated user that accessed the server.</span><span class="sxs-lookup"><span data-stu-id="975f3-133">Name of the authenticated user that accessed the server.</span></span> <span data-ttu-id="975f3-134">Anonymous users are indicated by a hyphen.</span><span class="sxs-lookup"><span data-stu-id="975f3-134">Anonymous users are indicated by a hyphen.</span></span> |
| <span data-ttu-id="975f3-135">csUriStem</span><span class="sxs-lookup"><span data-stu-id="975f3-135">csUriStem</span></span> |<span data-ttu-id="975f3-136">Target of the request such as a web page.</span><span class="sxs-lookup"><span data-stu-id="975f3-136">Target of the request such as a web page.</span></span> |
| <span data-ttu-id="975f3-137">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="975f3-137">csUriQuery</span></span> |<span data-ttu-id="975f3-138">Query, if any, that the client was trying to perform.</span><span class="sxs-lookup"><span data-stu-id="975f3-138">Query, if any, that the client was trying to perform.</span></span> |
| <span data-ttu-id="975f3-139">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="975f3-139">ManagementGroupName</span></span> |<span data-ttu-id="975f3-140">Name of the management group for Operations Manager agents.</span><span class="sxs-lookup"><span data-stu-id="975f3-140">Name of the management group for Operations Manager agents.</span></span>  <span data-ttu-id="975f3-141">For other agents, this is AOI-\<workspace ID\></span><span class="sxs-lookup"><span data-stu-id="975f3-141">For other agents, this is AOI-\<workspace ID\></span></span> |
| <span data-ttu-id="975f3-142">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="975f3-142">RemoteIPCountry</span></span> |<span data-ttu-id="975f3-143">Country of the IP address of the client.</span><span class="sxs-lookup"><span data-stu-id="975f3-143">Country of the IP address of the client.</span></span> |
| <span data-ttu-id="975f3-144">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="975f3-144">RemoteIPLatitude</span></span> |<span data-ttu-id="975f3-145">Latitude of the client IP address.</span><span class="sxs-lookup"><span data-stu-id="975f3-145">Latitude of the client IP address.</span></span> |
| <span data-ttu-id="975f3-146">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="975f3-146">RemoteIPLongitude</span></span> |<span data-ttu-id="975f3-147">Longitude of the client IP address.</span><span class="sxs-lookup"><span data-stu-id="975f3-147">Longitude of the client IP address.</span></span> |
| <span data-ttu-id="975f3-148">scStatus</span><span class="sxs-lookup"><span data-stu-id="975f3-148">scStatus</span></span> |<span data-ttu-id="975f3-149">HTTP status code.</span><span class="sxs-lookup"><span data-stu-id="975f3-149">HTTP status code.</span></span> |
| <span data-ttu-id="975f3-150">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="975f3-150">scSubStatus</span></span> |<span data-ttu-id="975f3-151">Substatus error code.</span><span class="sxs-lookup"><span data-stu-id="975f3-151">Substatus error code.</span></span> |
| <span data-ttu-id="975f3-152">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="975f3-152">scWin32Status</span></span> |<span data-ttu-id="975f3-153">Windows status code.</span><span class="sxs-lookup"><span data-stu-id="975f3-153">Windows status code.</span></span> |
| <span data-ttu-id="975f3-154">sIP</span><span class="sxs-lookup"><span data-stu-id="975f3-154">sIP</span></span> |<span data-ttu-id="975f3-155">IP address of the web server.</span><span class="sxs-lookup"><span data-stu-id="975f3-155">IP address of the web server.</span></span> |
| <span data-ttu-id="975f3-156">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="975f3-156">SourceSystem</span></span> |<span data-ttu-id="975f3-157">OpsMgr</span><span class="sxs-lookup"><span data-stu-id="975f3-157">OpsMgr</span></span> |
| <span data-ttu-id="975f3-158">sPort</span><span class="sxs-lookup"><span data-stu-id="975f3-158">sPort</span></span> |<span data-ttu-id="975f3-159">Port on the server the client connected to.</span><span class="sxs-lookup"><span data-stu-id="975f3-159">Port on the server the client connected to.</span></span> |
| <span data-ttu-id="975f3-160">sSiteName</span><span class="sxs-lookup"><span data-stu-id="975f3-160">sSiteName</span></span> |<span data-ttu-id="975f3-161">Name of the IIS site.</span><span class="sxs-lookup"><span data-stu-id="975f3-161">Name of the IIS site.</span></span> |
| <span data-ttu-id="975f3-162">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="975f3-162">TimeGenerated</span></span> |<span data-ttu-id="975f3-163">Date and time the entry was logged.</span><span class="sxs-lookup"><span data-stu-id="975f3-163">Date and time the entry was logged.</span></span> |
| <span data-ttu-id="975f3-164">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="975f3-164">TimeTaken</span></span> |<span data-ttu-id="975f3-165">Length of time to process the request in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="975f3-165">Length of time to process the request in milliseconds.</span></span> |

## <a name="log-searches-with-iis-logs"></a><span data-ttu-id="975f3-166">Log searches with IIS logs</span><span class="sxs-lookup"><span data-stu-id="975f3-166">Log searches with IIS logs</span></span>
<span data-ttu-id="975f3-167">The following table provides different examples of log queries that retrieve IIS log records.</span><span class="sxs-lookup"><span data-stu-id="975f3-167">The following table provides different examples of log queries that retrieve IIS log records.</span></span>

| <span data-ttu-id="975f3-168">Query</span><span class="sxs-lookup"><span data-stu-id="975f3-168">Query</span></span> | <span data-ttu-id="975f3-169">Description</span><span class="sxs-lookup"><span data-stu-id="975f3-169">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="975f3-170">Type=W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="975f3-170">Type=W3CIISLog</span></span> |<span data-ttu-id="975f3-171">All IIS log records.</span><span class="sxs-lookup"><span data-stu-id="975f3-171">All IIS log records.</span></span> |
| <span data-ttu-id="975f3-172">Type=W3CIISLog scStatus=500</span><span class="sxs-lookup"><span data-stu-id="975f3-172">Type=W3CIISLog scStatus=500</span></span> |<span data-ttu-id="975f3-173">All IIS log records with a return status of 500.</span><span class="sxs-lookup"><span data-stu-id="975f3-173">All IIS log records with a return status of 500.</span></span> |
| <span data-ttu-id="975f3-174">Type=W3CIISLog &#124; Measure count() by cIP</span><span class="sxs-lookup"><span data-stu-id="975f3-174">Type=W3CIISLog &#124; Measure count() by cIP</span></span> |<span data-ttu-id="975f3-175">Count of IIS log entries by client IP address.</span><span class="sxs-lookup"><span data-stu-id="975f3-175">Count of IIS log entries by client IP address.</span></span> |
| <span data-ttu-id="975f3-176">Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem</span><span class="sxs-lookup"><span data-stu-id="975f3-176">Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem</span></span> |<span data-ttu-id="975f3-177">Count of IIS log entries by URL for the host www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="975f3-177">Count of IIS log entries by URL for the host www.contoso.com.</span></span> |
| <span data-ttu-id="975f3-178">Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000</span><span class="sxs-lookup"><span data-stu-id="975f3-178">Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000</span></span> |<span data-ttu-id="975f3-179">Total bytes received by each IIS computer.</span><span class="sxs-lookup"><span data-stu-id="975f3-179">Total bytes received by each IIS computer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="975f3-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="975f3-180">Next steps</span></span>
* <span data-ttu-id="975f3-181">Configure Log Analytics to collect other [data sources](log-analytics-data-sources.md) for analysis.</span><span class="sxs-lookup"><span data-stu-id="975f3-181">Configure Log Analytics to collect other [data sources](log-analytics-data-sources.md) for analysis.</span></span>
* <span data-ttu-id="975f3-182">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span><span class="sxs-lookup"><span data-stu-id="975f3-182">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="975f3-183">Configure alerts in Log Analytics to proactively notify you of important conditions found in IIS logs.</span><span class="sxs-lookup"><span data-stu-id="975f3-183">Configure alerts in Log Analytics to proactively notify you of important conditions found in IIS logs.</span></span>


