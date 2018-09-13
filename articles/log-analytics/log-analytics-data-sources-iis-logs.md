---
title: IIS logs in Azure Log Analytics | Microsoft Docs
description: Internet Information Services (IIS) stores user activity in log files that can be collected by Log Analytics.  This article describes how to configure collection of IIS logs and details of the records they create in the Log Analytics workspace.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/12/2018
ms.author: bwren
ms.comopnent: na
ms.openlocfilehash: 65320e7d3cc97a3d53fd1a00fbbeab5559c02fce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830882"
---
# <a name="iis-logs-in-log-analytics"></a><span data-ttu-id="e86c8-104">IIS logs in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e86c8-104">IIS logs in Log Analytics</span></span>
<span data-ttu-id="e86c8-105">Internet Information Services (IIS) stores user activity in log files that can be collected by Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e86c8-105">Internet Information Services (IIS) stores user activity in log files that can be collected by Log Analytics.</span></span>  

![IIS logs](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a><span data-ttu-id="e86c8-107">Configuring IIS logs</span><span class="sxs-lookup"><span data-stu-id="e86c8-107">Configuring IIS logs</span></span>
<span data-ttu-id="e86c8-108">Log Analytics collects entries from log files created by IIS, so you must [configure IIS for logging](https://technet.microsoft.com/library/hh831775.aspx).</span><span class="sxs-lookup"><span data-stu-id="e86c8-108">Log Analytics collects entries from log files created by IIS, so you must [configure IIS for logging](https://technet.microsoft.com/library/hh831775.aspx).</span></span>

<span data-ttu-id="e86c8-109">Log Analytics only supports IIS log files stored in W3C format and does not support custom fields or IIS Advanced Logging.</span><span class="sxs-lookup"><span data-stu-id="e86c8-109">Log Analytics only supports IIS log files stored in W3C format and does not support custom fields or IIS Advanced Logging.</span></span>  
<span data-ttu-id="e86c8-110">Log Analytics does not collect logs in NCSA or IIS native format.</span><span class="sxs-lookup"><span data-stu-id="e86c8-110">Log Analytics does not collect logs in NCSA or IIS native format.</span></span>

<span data-ttu-id="e86c8-111">Configure IIS logs in Log Analytics from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="e86c8-111">Configure IIS logs in Log Analytics from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="e86c8-112">There is no configuration required other than selecting **Collect W3C format IIS log files**.</span><span class="sxs-lookup"><span data-stu-id="e86c8-112">There is no configuration required other than selecting **Collect W3C format IIS log files**.</span></span>


## <a name="data-collection"></a><span data-ttu-id="e86c8-113">Data collection</span><span class="sxs-lookup"><span data-stu-id="e86c8-113">Data collection</span></span>
<span data-ttu-id="e86c8-114">Log Analytics collects IIS log entries from each agent each time the log is closed and a new one is created.</span><span class="sxs-lookup"><span data-stu-id="e86c8-114">Log Analytics collects IIS log entries from each agent each time the log is closed and a new one is created.</span></span> <span data-ttu-id="e86c8-115">This frequency is controlled by the **Log File Rollover Schedule** setting for the IIS site which is once a day by default.</span><span class="sxs-lookup"><span data-stu-id="e86c8-115">This frequency is controlled by the **Log File Rollover Schedule** setting for the IIS site which is once a day by default.</span></span> <span data-ttu-id="e86c8-116">For example, if the settings is **Hourly**, then Log Analytics will collect the log each hour.</span><span class="sxs-lookup"><span data-stu-id="e86c8-116">For example, if the settings is **Hourly**, then Log Analytics will collect the log each hour.</span></span>  <span data-ttu-id="e86c8-117">If the setting is **Daily**, then Log Analytics will collect the log every 24 hours.</span><span class="sxs-lookup"><span data-stu-id="e86c8-117">If the setting is **Daily**, then Log Analytics will collect the log every 24 hours.</span></span>


## <a name="iis-log-record-properties"></a><span data-ttu-id="e86c8-118">IIS log record properties</span><span class="sxs-lookup"><span data-stu-id="e86c8-118">IIS log record properties</span></span>
<span data-ttu-id="e86c8-119">IIS log records have a type of **W3CIISLog** and have the properties in the following table:</span><span class="sxs-lookup"><span data-stu-id="e86c8-119">IIS log records have a type of **W3CIISLog** and have the properties in the following table:</span></span>

| <span data-ttu-id="e86c8-120">Property</span><span class="sxs-lookup"><span data-stu-id="e86c8-120">Property</span></span> | <span data-ttu-id="e86c8-121">Description</span><span class="sxs-lookup"><span data-stu-id="e86c8-121">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e86c8-122">Computer</span><span class="sxs-lookup"><span data-stu-id="e86c8-122">Computer</span></span> |<span data-ttu-id="e86c8-123">Name of the computer that the event was collected from.</span><span class="sxs-lookup"><span data-stu-id="e86c8-123">Name of the computer that the event was collected from.</span></span> |
| <span data-ttu-id="e86c8-124">cIP</span><span class="sxs-lookup"><span data-stu-id="e86c8-124">cIP</span></span> |<span data-ttu-id="e86c8-125">IP address of the client.</span><span class="sxs-lookup"><span data-stu-id="e86c8-125">IP address of the client.</span></span> |
| <span data-ttu-id="e86c8-126">csMethod</span><span class="sxs-lookup"><span data-stu-id="e86c8-126">csMethod</span></span> |<span data-ttu-id="e86c8-127">Method of the request such as GET or POST.</span><span class="sxs-lookup"><span data-stu-id="e86c8-127">Method of the request such as GET or POST.</span></span> |
| <span data-ttu-id="e86c8-128">csReferer</span><span class="sxs-lookup"><span data-stu-id="e86c8-128">csReferer</span></span> |<span data-ttu-id="e86c8-129">Site that the user followed a link from to the current site.</span><span class="sxs-lookup"><span data-stu-id="e86c8-129">Site that the user followed a link from to the current site.</span></span> |
| <span data-ttu-id="e86c8-130">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="e86c8-130">csUserAgent</span></span> |<span data-ttu-id="e86c8-131">Browser type of the client.</span><span class="sxs-lookup"><span data-stu-id="e86c8-131">Browser type of the client.</span></span> |
| <span data-ttu-id="e86c8-132">csUserName</span><span class="sxs-lookup"><span data-stu-id="e86c8-132">csUserName</span></span> |<span data-ttu-id="e86c8-133">Name of the authenticated user that accessed the server.</span><span class="sxs-lookup"><span data-stu-id="e86c8-133">Name of the authenticated user that accessed the server.</span></span> <span data-ttu-id="e86c8-134">Anonymous users are indicated by a hyphen.</span><span class="sxs-lookup"><span data-stu-id="e86c8-134">Anonymous users are indicated by a hyphen.</span></span> |
| <span data-ttu-id="e86c8-135">csUriStem</span><span class="sxs-lookup"><span data-stu-id="e86c8-135">csUriStem</span></span> |<span data-ttu-id="e86c8-136">Target of the request such as a web page.</span><span class="sxs-lookup"><span data-stu-id="e86c8-136">Target of the request such as a web page.</span></span> |
| <span data-ttu-id="e86c8-137">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="e86c8-137">csUriQuery</span></span> |<span data-ttu-id="e86c8-138">Query, if any, that the client was trying to perform.</span><span class="sxs-lookup"><span data-stu-id="e86c8-138">Query, if any, that the client was trying to perform.</span></span> |
| <span data-ttu-id="e86c8-139">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="e86c8-139">ManagementGroupName</span></span> |<span data-ttu-id="e86c8-140">Name of the management group for Operations Manager agents.</span><span class="sxs-lookup"><span data-stu-id="e86c8-140">Name of the management group for Operations Manager agents.</span></span>  <span data-ttu-id="e86c8-141">For other agents, this is AOI-\<workspace ID\></span><span class="sxs-lookup"><span data-stu-id="e86c8-141">For other agents, this is AOI-\<workspace ID\></span></span> |
| <span data-ttu-id="e86c8-142">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="e86c8-142">RemoteIPCountry</span></span> |<span data-ttu-id="e86c8-143">Country of the IP address of the client.</span><span class="sxs-lookup"><span data-stu-id="e86c8-143">Country of the IP address of the client.</span></span> |
| <span data-ttu-id="e86c8-144">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="e86c8-144">RemoteIPLatitude</span></span> |<span data-ttu-id="e86c8-145">Latitude of the client IP address.</span><span class="sxs-lookup"><span data-stu-id="e86c8-145">Latitude of the client IP address.</span></span> |
| <span data-ttu-id="e86c8-146">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="e86c8-146">RemoteIPLongitude</span></span> |<span data-ttu-id="e86c8-147">Longitude of the client IP address.</span><span class="sxs-lookup"><span data-stu-id="e86c8-147">Longitude of the client IP address.</span></span> |
| <span data-ttu-id="e86c8-148">scStatus</span><span class="sxs-lookup"><span data-stu-id="e86c8-148">scStatus</span></span> |<span data-ttu-id="e86c8-149">HTTP status code.</span><span class="sxs-lookup"><span data-stu-id="e86c8-149">HTTP status code.</span></span> |
| <span data-ttu-id="e86c8-150">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="e86c8-150">scSubStatus</span></span> |<span data-ttu-id="e86c8-151">Substatus error code.</span><span class="sxs-lookup"><span data-stu-id="e86c8-151">Substatus error code.</span></span> |
| <span data-ttu-id="e86c8-152">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="e86c8-152">scWin32Status</span></span> |<span data-ttu-id="e86c8-153">Windows status code.</span><span class="sxs-lookup"><span data-stu-id="e86c8-153">Windows status code.</span></span> |
| <span data-ttu-id="e86c8-154">sIP</span><span class="sxs-lookup"><span data-stu-id="e86c8-154">sIP</span></span> |<span data-ttu-id="e86c8-155">IP address of the web server.</span><span class="sxs-lookup"><span data-stu-id="e86c8-155">IP address of the web server.</span></span> |
| <span data-ttu-id="e86c8-156">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="e86c8-156">SourceSystem</span></span> |<span data-ttu-id="e86c8-157">OpsMgr</span><span class="sxs-lookup"><span data-stu-id="e86c8-157">OpsMgr</span></span> |
| <span data-ttu-id="e86c8-158">sPort</span><span class="sxs-lookup"><span data-stu-id="e86c8-158">sPort</span></span> |<span data-ttu-id="e86c8-159">Port on the server the client connected to.</span><span class="sxs-lookup"><span data-stu-id="e86c8-159">Port on the server the client connected to.</span></span> |
| <span data-ttu-id="e86c8-160">sSiteName</span><span class="sxs-lookup"><span data-stu-id="e86c8-160">sSiteName</span></span> |<span data-ttu-id="e86c8-161">Name of the IIS site.</span><span class="sxs-lookup"><span data-stu-id="e86c8-161">Name of the IIS site.</span></span> |
| <span data-ttu-id="e86c8-162">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="e86c8-162">TimeGenerated</span></span> |<span data-ttu-id="e86c8-163">Date and time the entry was logged.</span><span class="sxs-lookup"><span data-stu-id="e86c8-163">Date and time the entry was logged.</span></span> |
| <span data-ttu-id="e86c8-164">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="e86c8-164">TimeTaken</span></span> |<span data-ttu-id="e86c8-165">Length of time to process the request in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="e86c8-165">Length of time to process the request in milliseconds.</span></span> |

## <a name="log-searches-with-iis-logs"></a><span data-ttu-id="e86c8-166">Log searches with IIS logs</span><span class="sxs-lookup"><span data-stu-id="e86c8-166">Log searches with IIS logs</span></span>
<span data-ttu-id="e86c8-167">The following table provides different examples of log queries that retrieve IIS log records.</span><span class="sxs-lookup"><span data-stu-id="e86c8-167">The following table provides different examples of log queries that retrieve IIS log records.</span></span>

| <span data-ttu-id="e86c8-168">Query</span><span class="sxs-lookup"><span data-stu-id="e86c8-168">Query</span></span> | <span data-ttu-id="e86c8-169">Description</span><span class="sxs-lookup"><span data-stu-id="e86c8-169">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e86c8-170">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="e86c8-170">W3CIISLog</span></span> |<span data-ttu-id="e86c8-171">All IIS log records.</span><span class="sxs-lookup"><span data-stu-id="e86c8-171">All IIS log records.</span></span> |
| <span data-ttu-id="e86c8-172">W3CIISLog &#124; where scStatus==500</span><span class="sxs-lookup"><span data-stu-id="e86c8-172">W3CIISLog &#124; where scStatus==500</span></span> |<span data-ttu-id="e86c8-173">All IIS log records with a return status of 500.</span><span class="sxs-lookup"><span data-stu-id="e86c8-173">All IIS log records with a return status of 500.</span></span> |
| <span data-ttu-id="e86c8-174">W3CIISLog &#124; summarize count() by cIP</span><span class="sxs-lookup"><span data-stu-id="e86c8-174">W3CIISLog &#124; summarize count() by cIP</span></span> |<span data-ttu-id="e86c8-175">Count of IIS log entries by client IP address.</span><span class="sxs-lookup"><span data-stu-id="e86c8-175">Count of IIS log entries by client IP address.</span></span> |
| <span data-ttu-id="e86c8-176">W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem</span><span class="sxs-lookup"><span data-stu-id="e86c8-176">W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem</span></span> |<span data-ttu-id="e86c8-177">Count of IIS log entries by URL for the host www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e86c8-177">Count of IIS log entries by URL for the host www.contoso.com.</span></span> |
| <span data-ttu-id="e86c8-178">W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000</span><span class="sxs-lookup"><span data-stu-id="e86c8-178">W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000</span></span> |<span data-ttu-id="e86c8-179">Total bytes received by each IIS computer.</span><span class="sxs-lookup"><span data-stu-id="e86c8-179">Total bytes received by each IIS computer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e86c8-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="e86c8-180">Next steps</span></span>
* <span data-ttu-id="e86c8-181">Configure Log Analytics to collect other [data sources](log-analytics-data-sources.md) for analysis.</span><span class="sxs-lookup"><span data-stu-id="e86c8-181">Configure Log Analytics to collect other [data sources](log-analytics-data-sources.md) for analysis.</span></span>
* <span data-ttu-id="e86c8-182">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span><span class="sxs-lookup"><span data-stu-id="e86c8-182">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="e86c8-183">Configure alerts in Log Analytics to proactively notify you of important conditions found in IIS logs.</span><span class="sxs-lookup"><span data-stu-id="e86c8-183">Configure alerts in Log Analytics to proactively notify you of important conditions found in IIS logs.</span></span>
