---
title: Connect Linux computers to Azure Log Analytics | Microsoft Docs
description: Using Log Analytics, you can collect and act on data generated from Linux computers.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: ab5b76d8-9ab5-406e-8768-76fb0632d830
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e0bb8bc259aeb5ec8dd6ce980bcbb851e2f8c835
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671739"
---
# <a name="connect-your-linux-computers-to-log-analytics"></a><span data-ttu-id="8acbc-103">Connect your Linux computers to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8acbc-103">Connect your Linux computers to Log Analytics</span></span>
<span data-ttu-id="8acbc-104">Using Log Analytics, you can collect and act on data generated from Linux computers.</span><span class="sxs-lookup"><span data-stu-id="8acbc-104">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="8acbc-105">Adding data collected from Linux to OMS allows you to manage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span><span class="sxs-lookup"><span data-stu-id="8acbc-105">Adding data collected from Linux to OMS allows you to manage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="8acbc-106">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even the laptop on your desk.</span><span class="sxs-lookup"><span data-stu-id="8acbc-106">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even the laptop on your desk.</span></span> <span data-ttu-id="8acbc-107">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span><span class="sxs-lookup"><span data-stu-id="8acbc-107">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="8acbc-108">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span><span class="sxs-lookup"><span data-stu-id="8acbc-108">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="8acbc-109">This reduces the need to monitor it using many different systems, makes it easy to consume, and you can export any data you like to whatever business analytics solution or system that you already have.</span><span class="sxs-lookup"><span data-stu-id="8acbc-109">This reduces the need to monitor it using many different systems, makes it easy to consume, and you can export any data you like to whatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="8acbc-110">This article is a quick start guide that will help you collect and manage data for your Linux computers using the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="8acbc-110">This article is a quick start guide that will help you collect and manage data for your Linux computers using the OMS Agent for Linux.</span></span> <span data-ttu-id="8acbc-111">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="8acbc-111">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="8acbc-112">Currently, you can collect the following types of data from Linux computers:</span><span class="sxs-lookup"><span data-stu-id="8acbc-112">Currently, you can collect the following types of data from Linux computers:</span></span>

* <span data-ttu-id="8acbc-113">Performance metrics</span><span class="sxs-lookup"><span data-stu-id="8acbc-113">Performance metrics</span></span>
* <span data-ttu-id="8acbc-114">Syslog events</span><span class="sxs-lookup"><span data-stu-id="8acbc-114">Syslog events</span></span>
* <span data-ttu-id="8acbc-115">Alerts from Nagios and Zabbix</span><span class="sxs-lookup"><span data-stu-id="8acbc-115">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="8acbc-116">Docker container performance metrics, inventory and logs</span><span class="sxs-lookup"><span data-stu-id="8acbc-116">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="8acbc-117">Supported Linux versions</span><span class="sxs-lookup"><span data-stu-id="8acbc-117">Supported Linux versions</span></span>
<span data-ttu-id="8acbc-118">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span><span class="sxs-lookup"><span data-stu-id="8acbc-118">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="8acbc-119">However, the OMS Agent for Linux might also run on other distributions not listed.</span><span class="sxs-lookup"><span data-stu-id="8acbc-119">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="8acbc-120">Amazon Linux 2012.09 through 2015.09</span><span class="sxs-lookup"><span data-stu-id="8acbc-120">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="8acbc-121">CentOS Linux 5, 6, and 7</span><span class="sxs-lookup"><span data-stu-id="8acbc-121">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="8acbc-122">Oracle Linux 5, 6, and 7</span><span class="sxs-lookup"><span data-stu-id="8acbc-122">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="8acbc-123">Red Hat Enterprise Linux Server 5, 6 and 7</span><span class="sxs-lookup"><span data-stu-id="8acbc-123">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="8acbc-124">Debian GNU/Linux 6, 7, and 8</span><span class="sxs-lookup"><span data-stu-id="8acbc-124">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="8acbc-125">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="8acbc-125">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="8acbc-126">SUSE Linux Enterprise Server 11 and 12</span><span class="sxs-lookup"><span data-stu-id="8acbc-126">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="8acbc-127">OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="8acbc-127">OMS Agent for Linux</span></span>
<span data-ttu-id="8acbc-128">The Operations Management Suite Agent for Linux comprises multiple packages.</span><span class="sxs-lookup"><span data-stu-id="8acbc-128">The Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="8acbc-129">The release file contains the following packages, available by running the shell bundle with `--extract`.</span><span class="sxs-lookup"><span data-stu-id="8acbc-129">The release file contains the following packages, available by running the shell bundle with `--extract`.</span></span>

| <span data-ttu-id="8acbc-130">**Package**</span><span class="sxs-lookup"><span data-stu-id="8acbc-130">**Package**</span></span> | <span data-ttu-id="8acbc-131">**Version**</span><span class="sxs-lookup"><span data-stu-id="8acbc-131">**Version**</span></span> | <span data-ttu-id="8acbc-132">**Description**</span><span class="sxs-lookup"><span data-stu-id="8acbc-132">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8acbc-133">omsagent</span><span class="sxs-lookup"><span data-stu-id="8acbc-133">omsagent</span></span> |<span data-ttu-id="8acbc-134">1.1.0</span><span class="sxs-lookup"><span data-stu-id="8acbc-134">1.1.0</span></span> |<span data-ttu-id="8acbc-135">The Operations Management Suite Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="8acbc-135">The Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="8acbc-136">omsconfig</span><span class="sxs-lookup"><span data-stu-id="8acbc-136">omsconfig</span></span> |<span data-ttu-id="8acbc-137">1.1.1</span><span class="sxs-lookup"><span data-stu-id="8acbc-137">1.1.1</span></span> |<span data-ttu-id="8acbc-138">Configuration agent for the OMS Agent</span><span class="sxs-lookup"><span data-stu-id="8acbc-138">Configuration agent for the OMS Agent</span></span> |
| <span data-ttu-id="8acbc-139">omi</span><span class="sxs-lookup"><span data-stu-id="8acbc-139">omi</span></span> |<span data-ttu-id="8acbc-140">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="8acbc-140">1.0.8.3</span></span> |<span data-ttu-id="8acbc-141">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span><span class="sxs-lookup"><span data-stu-id="8acbc-141">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="8acbc-142">scx</span><span class="sxs-lookup"><span data-stu-id="8acbc-142">scx</span></span> |<span data-ttu-id="8acbc-143">1.6.2</span><span class="sxs-lookup"><span data-stu-id="8acbc-143">1.6.2</span></span> |<span data-ttu-id="8acbc-144">OMI CIM Providers for operating system performance metrics</span><span class="sxs-lookup"><span data-stu-id="8acbc-144">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="8acbc-145">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="8acbc-145">apache-cimprov</span></span> |<span data-ttu-id="8acbc-146">1.0.0</span><span class="sxs-lookup"><span data-stu-id="8acbc-146">1.0.0</span></span> |<span data-ttu-id="8acbc-147">Apache HTTP Server performance monitoring provider for OMI.</span><span class="sxs-lookup"><span data-stu-id="8acbc-147">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="8acbc-148">Only installed if Apache HTTP Server is detected.</span><span class="sxs-lookup"><span data-stu-id="8acbc-148">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="8acbc-149">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="8acbc-149">mysql-cimprov</span></span> |<span data-ttu-id="8acbc-150">1.0.0</span><span class="sxs-lookup"><span data-stu-id="8acbc-150">1.0.0</span></span> |<span data-ttu-id="8acbc-151">MySQL Server performance monitoring provider for OMI.</span><span class="sxs-lookup"><span data-stu-id="8acbc-151">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="8acbc-152">Only installed if MySQL/MariaDB server is detected.</span><span class="sxs-lookup"><span data-stu-id="8acbc-152">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="8acbc-153">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="8acbc-153">docker-cimprov</span></span> |<span data-ttu-id="8acbc-154">0.1.0</span><span class="sxs-lookup"><span data-stu-id="8acbc-154">0.1.0</span></span> |<span data-ttu-id="8acbc-155">Docker provider for OMI.</span><span class="sxs-lookup"><span data-stu-id="8acbc-155">Docker provider for OMI.</span></span> <span data-ttu-id="8acbc-156">Only installed if Docker is detected.</span><span class="sxs-lookup"><span data-stu-id="8acbc-156">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="8acbc-157">Additional installation artifacts</span><span class="sxs-lookup"><span data-stu-id="8acbc-157">Additional installation artifacts</span></span>
<span data-ttu-id="8acbc-158">After installing the OMS agent for Linux packages, the following additional system-wide configuration changes are applied.</span><span class="sxs-lookup"><span data-stu-id="8acbc-158">After installing the OMS agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="8acbc-159">These artifacts are removed when the omsagent package is uninstalled.</span><span class="sxs-lookup"><span data-stu-id="8acbc-159">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="8acbc-160">A non-privileged user named: `omsagent` is created.</span><span class="sxs-lookup"><span data-stu-id="8acbc-160">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="8acbc-161">This is the account the omsagent daemon runs as</span><span class="sxs-lookup"><span data-stu-id="8acbc-161">This is the account the omsagent daemon runs as</span></span>
* <span data-ttu-id="8acbc-162">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent to restart the syslog and omsagent daemons.</span><span class="sxs-lookup"><span data-stu-id="8acbc-162">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="8acbc-163">If sudo “include” directives are not supported in the installed version of sudo, these entries will be written to /etc/sudoers.</span><span class="sxs-lookup"><span data-stu-id="8acbc-163">If sudo “include” directives are not supported in the installed version of sudo, these entries will be written to /etc/sudoers.</span></span>
* <span data-ttu-id="8acbc-164">The syslog configuration is modified to forward a subset of events to the agent.</span><span class="sxs-lookup"><span data-stu-id="8acbc-164">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="8acbc-165">For more information, see the **Configuring Data Collection** section below</span><span class="sxs-lookup"><span data-stu-id="8acbc-165">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="8acbc-166">Linux data collection details</span><span class="sxs-lookup"><span data-stu-id="8acbc-166">Linux data collection details</span></span>
<span data-ttu-id="8acbc-167">The following table shows data collection methods and other details about how data is collected.</span><span class="sxs-lookup"><span data-stu-id="8acbc-167">The following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="8acbc-168">source</span><span class="sxs-lookup"><span data-stu-id="8acbc-168">source</span></span> | <span data-ttu-id="8acbc-169">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="8acbc-169">Direct Agent</span></span> | <span data-ttu-id="8acbc-170">SCOM agent</span><span class="sxs-lookup"><span data-stu-id="8acbc-170">SCOM agent</span></span> | <span data-ttu-id="8acbc-171">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8acbc-171">Azure Storage</span></span> | <span data-ttu-id="8acbc-172">SCOM required?</span><span class="sxs-lookup"><span data-stu-id="8acbc-172">SCOM required?</span></span> | <span data-ttu-id="8acbc-173">SCOM agent data sent via management group</span><span class="sxs-lookup"><span data-stu-id="8acbc-173">SCOM agent data sent via management group</span></span> | <span data-ttu-id="8acbc-174">collection frequency</span><span class="sxs-lookup"><span data-stu-id="8acbc-174">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="8acbc-175">Zabbix</span><span class="sxs-lookup"><span data-stu-id="8acbc-175">Zabbix</span></span> |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="8acbc-181">1 minute</span><span class="sxs-lookup"><span data-stu-id="8acbc-181">1 minute</span></span> |
| <span data-ttu-id="8acbc-182">Nagios</span><span class="sxs-lookup"><span data-stu-id="8acbc-182">Nagios</span></span> |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="8acbc-188">on arrival</span><span class="sxs-lookup"><span data-stu-id="8acbc-188">on arrival</span></span> |
| <span data-ttu-id="8acbc-189">syslog</span><span class="sxs-lookup"><span data-stu-id="8acbc-189">syslog</span></span> |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="8acbc-195">from Azure storage: 10 minutes; from agent: on arrival</span><span class="sxs-lookup"><span data-stu-id="8acbc-195">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="8acbc-196">Linux performance counters</span><span class="sxs-lookup"><span data-stu-id="8acbc-196">Linux performance counters</span></span> |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="8acbc-202">As scheduled, minimum of 10 seconds</span><span class="sxs-lookup"><span data-stu-id="8acbc-202">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="8acbc-203">change tracking</span><span class="sxs-lookup"><span data-stu-id="8acbc-203">change tracking</span></span> |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="8acbc-209">hourly</span><span class="sxs-lookup"><span data-stu-id="8acbc-209">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="8acbc-210">Package Requirements</span><span class="sxs-lookup"><span data-stu-id="8acbc-210">Package Requirements</span></span>
| <span data-ttu-id="8acbc-211">**Required package**</span><span class="sxs-lookup"><span data-stu-id="8acbc-211">**Required package**</span></span> | <span data-ttu-id="8acbc-212">**Description**</span><span class="sxs-lookup"><span data-stu-id="8acbc-212">**Description**</span></span> | <span data-ttu-id="8acbc-213">**Minimum version**</span><span class="sxs-lookup"><span data-stu-id="8acbc-213">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8acbc-214">Glibc</span><span class="sxs-lookup"><span data-stu-id="8acbc-214">Glibc</span></span> |<span data-ttu-id="8acbc-215">GNU C library</span><span class="sxs-lookup"><span data-stu-id="8acbc-215">GNU C library</span></span> |<span data-ttu-id="8acbc-216">2.5-12</span><span class="sxs-lookup"><span data-stu-id="8acbc-216">2.5-12</span></span> |
| <span data-ttu-id="8acbc-217">Openssl</span><span class="sxs-lookup"><span data-stu-id="8acbc-217">Openssl</span></span> |<span data-ttu-id="8acbc-218">OpenSSL libraries</span><span class="sxs-lookup"><span data-stu-id="8acbc-218">OpenSSL libraries</span></span> |<span data-ttu-id="8acbc-219">0.9.8e or 1.0</span><span class="sxs-lookup"><span data-stu-id="8acbc-219">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="8acbc-220">Curl</span><span class="sxs-lookup"><span data-stu-id="8acbc-220">Curl</span></span> |<span data-ttu-id="8acbc-221">cURL web client</span><span class="sxs-lookup"><span data-stu-id="8acbc-221">cURL web client</span></span> |<span data-ttu-id="8acbc-222">7.15.5</span><span class="sxs-lookup"><span data-stu-id="8acbc-222">7.15.5</span></span> |
| <span data-ttu-id="8acbc-223">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="8acbc-223">Python-ctypes</span></span> |<span data-ttu-id="8acbc-224">function libraries</span><span class="sxs-lookup"><span data-stu-id="8acbc-224">function libraries</span></span> |<span data-ttu-id="8acbc-225">n/a</span><span class="sxs-lookup"><span data-stu-id="8acbc-225">n/a</span></span> |
| <span data-ttu-id="8acbc-226">PAM</span><span class="sxs-lookup"><span data-stu-id="8acbc-226">PAM</span></span> |<span data-ttu-id="8acbc-227">Pluggable authentication Modules</span><span class="sxs-lookup"><span data-stu-id="8acbc-227">Pluggable authentication Modules</span></span> |<span data-ttu-id="8acbc-228">n/a</span><span class="sxs-lookup"><span data-stu-id="8acbc-228">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="8acbc-229">Either rsyslog or syslog-ng are required to collect syslog messages.</span><span class="sxs-lookup"><span data-stu-id="8acbc-229">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="8acbc-230">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span><span class="sxs-lookup"><span data-stu-id="8acbc-230">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="8acbc-231">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span><span class="sxs-lookup"><span data-stu-id="8acbc-231">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="8acbc-232">Quick install</span><span class="sxs-lookup"><span data-stu-id="8acbc-232">Quick install</span></span>
<span data-ttu-id="8acbc-233">Run the following commands to download the omsagent, validate the checksum, then  install and onboard the agent.</span><span class="sxs-lookup"><span data-stu-id="8acbc-233">Run the following commands to download the omsagent, validate the checksum, then  install and onboard the agent.</span></span> <span data-ttu-id="8acbc-234">Commands are for 64-bit.</span><span class="sxs-lookup"><span data-stu-id="8acbc-234">Commands are for 64-bit.</span></span> <span data-ttu-id="8acbc-235">The Workspace ID and Primary Key are found in the OMS portal under **Settings** on the **Connected Sources** tab.</span><span class="sxs-lookup"><span data-stu-id="8acbc-235">The Workspace ID and Primary Key are found in the OMS portal under **Settings** on the **Connected Sources** tab.</span></span>

![workspace details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="8acbc-237">There are a variety of other methods to install the agent and upgrade it.</span><span class="sxs-lookup"><span data-stu-id="8acbc-237">There are a variety of other methods to install the agent and upgrade it.</span></span> <span data-ttu-id="8acbc-238">You can read more about them at [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="8acbc-238">You can read more about them at [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="8acbc-239">You can also view the [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="8acbc-239">You can also view the [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="8acbc-240">Choose your Linux data collection method</span><span class="sxs-lookup"><span data-stu-id="8acbc-240">Choose your Linux data collection method</span></span>
<span data-ttu-id="8acbc-241">How you choose the data types you'd like to collect depends on whether you want to use the OMS portal or if you want edit various configuration files directly on your Linux clients.</span><span class="sxs-lookup"><span data-stu-id="8acbc-241">How you choose the data types you'd like to collect depends on whether you want to use the OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="8acbc-242">If you choose to use the portal, the configuration is sent to all of your Linux clients automatically.</span><span class="sxs-lookup"><span data-stu-id="8acbc-242">If you choose to use the portal, the configuration is sent to all of your Linux clients automatically.</span></span> <span data-ttu-id="8acbc-243">If you need different configurations for different Linux clients, you will need to edit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span><span class="sxs-lookup"><span data-stu-id="8acbc-243">If you need different configurations for different Linux clients, you will need to edit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="8acbc-244">You can specify the syslog events and performance counters that you want to collect using configuration files on the Linux computers.</span><span class="sxs-lookup"><span data-stu-id="8acbc-244">You can specify the syslog events and performance counters that you want to collect using configuration files on the Linux computers.</span></span> <span data-ttu-id="8acbc-245">*If you chose to configure data collection by editing agent configuration files, you should disable the centralized configuration.*</span><span class="sxs-lookup"><span data-stu-id="8acbc-245">*If you chose to configure data collection by editing agent configuration files, you should disable the centralized configuration.*</span></span>  <span data-ttu-id="8acbc-246">Instructions are provided below to configure data collection in the agent's configuration files as well as to disable central configuration for all OMS Agents for Linux, or individual computers.</span><span class="sxs-lookup"><span data-stu-id="8acbc-246">Instructions are provided below to configure data collection in the agent's configuration files as well as to disable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="8acbc-247">Disable OMS management for an individual Linux computer</span><span class="sxs-lookup"><span data-stu-id="8acbc-247">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="8acbc-248">Centralized data collection for configuration data is disabled for an individual Linux computer with the OMS_MetaConfigHelper.py script.</span><span class="sxs-lookup"><span data-stu-id="8acbc-248">Centralized data collection for configuration data is disabled for an individual Linux computer with the OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="8acbc-249">This can be useful if a subset of computers should have a specialized configuration.</span><span class="sxs-lookup"><span data-stu-id="8acbc-249">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="8acbc-250">To disable centralized configuration:</span><span class="sxs-lookup"><span data-stu-id="8acbc-250">To disable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="8acbc-251">To re-enable centralized configuration:</span><span class="sxs-lookup"><span data-stu-id="8acbc-251">To re-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="8acbc-252">Linux performance counters</span><span class="sxs-lookup"><span data-stu-id="8acbc-252">Linux performance counters</span></span>
<span data-ttu-id="8acbc-253">Linux performance counters are similar to Windows performance counters—both operate similarly.</span><span class="sxs-lookup"><span data-stu-id="8acbc-253">Linux performance counters are similar to Windows performance counters—both operate similarly.</span></span> <span data-ttu-id="8acbc-254">You can use the following procedures to add and configure them.</span><span class="sxs-lookup"><span data-stu-id="8acbc-254">You can use the following procedures to add and configure them.</span></span> <span data-ttu-id="8acbc-255">After they are added to OMS, data is collected for them every 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="8acbc-255">After they are added to OMS, data is collected for them every 30 seconds.</span></span>

### <a name="to-add-a-linux-performance-counter-in-oms"></a><span data-ttu-id="8acbc-256">To add a Linux performance counter in OMS</span><span class="sxs-lookup"><span data-stu-id="8acbc-256">To add a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="8acbc-257">To configure OMS Agents for Linux using the OMS portal, you can add Linux performance counters on the Settings page, click **Data**.</span><span class="sxs-lookup"><span data-stu-id="8acbc-257">To configure OMS Agents for Linux using the OMS portal, you can add Linux performance counters on the Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="8acbc-258">On the **Settings** page under **Data** , click **Linux performance counters** and then select or type the name of the counter you want to add.</span><span class="sxs-lookup"><span data-stu-id="8acbc-258">On the **Settings** page under **Data** , click **Linux performance counters** and then select or type the name of the counter you want to add.</span></span>  
    <span data-ttu-id="8acbc-259">![data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="8acbc-259">![data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="8acbc-260">If you don't know the full name of the counter, you can start typing a partial name and a list of available counters will appear.</span><span class="sxs-lookup"><span data-stu-id="8acbc-260">If you don't know the full name of the counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="8acbc-261">When you find the counter you want to add, click the name in the list and then click the plus icon to add the counter.</span><span class="sxs-lookup"><span data-stu-id="8acbc-261">When you find the counter you want to add, click the name in the list and then click the plus icon to add the counter.</span></span>
4. <span data-ttu-id="8acbc-262">After you add the counter, it appears in the list of counters highlighted with a colored bar.</span><span class="sxs-lookup"><span data-stu-id="8acbc-262">After you add the counter, it appears in the list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="8acbc-263">By default, the **Apply below configuration to my machines** option is selected.</span><span class="sxs-lookup"><span data-stu-id="8acbc-263">By default, the **Apply below configuration to my machines** option is selected.</span></span> <span data-ttu-id="8acbc-264">If you want to disable sending configuration data, clear the selection.</span><span class="sxs-lookup"><span data-stu-id="8acbc-264">If you want to disable sending configuration data, clear the selection.</span></span>
6. <span data-ttu-id="8acbc-265">When you are done modifying performance counters, at the bottom of the page click **Save** to finalize your changes.</span><span class="sxs-lookup"><span data-stu-id="8acbc-265">When you are done modifying performance counters, at the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="8acbc-266">The configuration changes that you've made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="8acbc-266">The configuration changes that you've made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="8acbc-267">Configure Linux performance counters in OMS</span><span class="sxs-lookup"><span data-stu-id="8acbc-267">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="8acbc-268">For Windows performance counters, you can choose a specific instance for each performance counter.</span><span class="sxs-lookup"><span data-stu-id="8acbc-268">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="8acbc-269">However, for Linux performance counters, whatever instance of a counter that you choose applies to all child counters of the parent counter.</span><span class="sxs-lookup"><span data-stu-id="8acbc-269">However, for Linux performance counters, whatever instance of a counter that you choose applies to all child counters of the parent counter.</span></span> <span data-ttu-id="8acbc-270">The following table shows the common instances available to both Linux and Windows performance counters.</span><span class="sxs-lookup"><span data-stu-id="8acbc-270">The following table shows the common instances available to both Linux and Windows performance counters.</span></span>

| <span data-ttu-id="8acbc-271">**Instance name**</span><span class="sxs-lookup"><span data-stu-id="8acbc-271">**Instance name**</span></span> | <span data-ttu-id="8acbc-272">**Meaning**</span><span class="sxs-lookup"><span data-stu-id="8acbc-272">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="8acbc-273">\_Total</span><span class="sxs-lookup"><span data-stu-id="8acbc-273">\_Total</span></span> |<span data-ttu-id="8acbc-274">Total of all the instances</span><span class="sxs-lookup"><span data-stu-id="8acbc-274">Total of all the instances</span></span> |
| \* |<span data-ttu-id="8acbc-275">All instances</span><span class="sxs-lookup"><span data-stu-id="8acbc-275">All instances</span></span> |
| <span data-ttu-id="8acbc-276">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="8acbc-276">(/&#124;/var)</span></span> |<span data-ttu-id="8acbc-277">Matches instances named: / or /var</span><span class="sxs-lookup"><span data-stu-id="8acbc-277">Matches instances named: / or /var</span></span> |

<span data-ttu-id="8acbc-278">Similarly, the sample interval that you choose for a parent counter applies to all its child counters.</span><span class="sxs-lookup"><span data-stu-id="8acbc-278">Similarly, the sample interval that you choose for a parent counter applies to all its child counters.</span></span> <span data-ttu-id="8acbc-279">In other words, all the child counter sample intervals and instances are tied together.</span><span class="sxs-lookup"><span data-stu-id="8acbc-279">In other words, all the child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="8acbc-280">Add and configure performance metrics with Linux</span><span class="sxs-lookup"><span data-stu-id="8acbc-280">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="8acbc-281">Performance metrics to collect are controlled by the configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="8acbc-281">Performance metrics to collect are controlled by the configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="8acbc-282">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="8acbc-282">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for the OMS Agent for Linux.</span></span>

<span data-ttu-id="8acbc-283">Each object, or category, of performance metrics to collect should be defined in the configuration file as a single `<source>` element.</span><span class="sxs-lookup"><span data-stu-id="8acbc-283">Each object, or category, of performance metrics to collect should be defined in the configuration file as a single `<source>` element.</span></span> <span data-ttu-id="8acbc-284">The syntax follows the pattern below.</span><span class="sxs-lookup"><span data-stu-id="8acbc-284">The syntax follows the pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="8acbc-285">The configurable parameters of this element are:</span><span class="sxs-lookup"><span data-stu-id="8acbc-285">The configurable parameters of this element are:</span></span>

* <span data-ttu-id="8acbc-286">**Object\_name**: the object name for the collection.</span><span class="sxs-lookup"><span data-stu-id="8acbc-286">**Object\_name**: the object name for the collection.</span></span>
* <span data-ttu-id="8acbc-287">**Instance\_regex**: a *regular expression* defining which instances to collect.</span><span class="sxs-lookup"><span data-stu-id="8acbc-287">**Instance\_regex**: a *regular expression* defining which instances to collect.</span></span> <span data-ttu-id="8acbc-288">The value: `.*` specifies all instances.</span><span class="sxs-lookup"><span data-stu-id="8acbc-288">The value: `.*` specifies all instances.</span></span> <span data-ttu-id="8acbc-289">To collect processor metrics for only the \_Total instance, you could specify `_Total`.</span><span class="sxs-lookup"><span data-stu-id="8acbc-289">To collect processor metrics for only the \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="8acbc-290">To collect process metrics for only the crond or sshd instances, you could specify: `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="8acbc-290">To collect process metrics for only the crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="8acbc-291">**Counter\_name\_regex**: a *regular expression* defining which counters (for the object) to collect.</span><span class="sxs-lookup"><span data-stu-id="8acbc-291">**Counter\_name\_regex**: a *regular expression* defining which counters (for the object) to collect.</span></span> <span data-ttu-id="8acbc-292">To collect all counters for the object, specify: `.*`.</span><span class="sxs-lookup"><span data-stu-id="8acbc-292">To collect all counters for the object, specify: `.*`.</span></span> <span data-ttu-id="8acbc-293">To collect only swap space counters for the memory object, you could specify: `.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="8acbc-293">To collect only swap space counters for the memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="8acbc-294">**Interval:**: the frequency at which the object's counters are collected.</span><span class="sxs-lookup"><span data-stu-id="8acbc-294">**Interval:**: the frequency at which the object's counters are collected.</span></span>

<span data-ttu-id="8acbc-295">The default configuration for performance metrics is:</span><span class="sxs-lookup"><span data-stu-id="8acbc-295">The default configuration for performance metrics is:</span></span>

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="8acbc-296">Enable MySQL performance counters using Linux commands</span><span class="sxs-lookup"><span data-stu-id="8acbc-296">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="8acbc-297">If MySQL Server or MariaDB Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span><span class="sxs-lookup"><span data-stu-id="8acbc-297">If MySQL Server or MariaDB Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="8acbc-298">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span><span class="sxs-lookup"><span data-stu-id="8acbc-298">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="8acbc-299">You need to configure MySQL user credentials so that the provider can access the MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="8acbc-299">You need to configure MySQL user credentials so that the provider can access the MySQL Server.</span></span>

<span data-ttu-id="8acbc-300">To define a default user account for the MySQL server on localhost, use the following command example.</span><span class="sxs-lookup"><span data-stu-id="8acbc-300">To define a default user account for the MySQL server on localhost, use the following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="8acbc-301">The credentials file must be readable by the omsagent account.</span><span class="sxs-lookup"><span data-stu-id="8acbc-301">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="8acbc-302">Running the mycimprovauth command as omsgent is recommended.</span><span class="sxs-lookup"><span data-stu-id="8acbc-302">Running the mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="8acbc-303">Alternatively, you can specify the required MySQL credentials in a file, by creating the file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through the mysql-auth file, see [Manage MySQL monitoring credentials in the authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="8acbc-303">Alternatively, you can specify the required MySQL credentials in a file, by creating the file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through the mysql-auth file, see [Manage MySQL monitoring credentials in the authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="8acbc-304">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by the MySQL user to collect MySQL Server performance data.</span><span class="sxs-lookup"><span data-stu-id="8acbc-304">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by the MySQL user to collect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="8acbc-305">Enable Apache HTTP Server performance counters using Linux commands</span><span class="sxs-lookup"><span data-stu-id="8acbc-305">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="8acbc-306">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span><span class="sxs-lookup"><span data-stu-id="8acbc-306">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="8acbc-307">This provider relies on an Apache "module" that must be loaded into the Apache HTTP Server in order to access performance data.</span><span class="sxs-lookup"><span data-stu-id="8acbc-307">This provider relies on an Apache "module" that must be loaded into the Apache HTTP Server in order to access performance data.</span></span>

<span data-ttu-id="8acbc-308">You can load the module with the following command:</span><span class="sxs-lookup"><span data-stu-id="8acbc-308">You can load the module with the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="8acbc-309">To unload the Apache monitoring module, run the following command:</span><span class="sxs-lookup"><span data-stu-id="8acbc-309">To unload the Apache monitoring module, run the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="to-view-performance-data-with-log-analytics"></a><span data-ttu-id="8acbc-310">To view performance data with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8acbc-310">To view performance data with Log Analytics</span></span>
1. <span data-ttu-id="8acbc-311">In the Operations Management Suite portal, click the Log Search tile.</span><span class="sxs-lookup"><span data-stu-id="8acbc-311">In the Operations Management Suite portal, click the Log Search tile.</span></span>
2. <span data-ttu-id="8acbc-312">In the search bar, type `* (Type=Perf)` to view all performance counters.</span><span class="sxs-lookup"><span data-stu-id="8acbc-312">In the search bar, type `* (Type=Perf)` to view all performance counters.</span></span>

<span data-ttu-id="8acbc-313">Because OMS also collects Windows performance counter data, you should scope-down the search to Linux-specific data.</span><span class="sxs-lookup"><span data-stu-id="8acbc-313">Because OMS also collects Windows performance counter data, you should scope-down the search to Linux-specific data.</span></span> <span data-ttu-id="8acbc-314">So, the following example would show performance data specific to an example Linux server named Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="8acbc-314">So, the following example would show performance data specific to an example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![example server shown in search results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="8acbc-316">In the results, you can click **Metrics** to view the counters that data was collected for.</span><span class="sxs-lookup"><span data-stu-id="8acbc-316">In the results, you can click **Metrics** to view the counters that data was collected for.</span></span> <span data-ttu-id="8acbc-317">Real-time data is shown as graphs for each counter.</span><span class="sxs-lookup"><span data-stu-id="8acbc-317">Real-time data is shown as graphs for each counter.</span></span>

![metrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="8acbc-319">Syslog</span><span class="sxs-lookup"><span data-stu-id="8acbc-319">Syslog</span></span>
<span data-ttu-id="8acbc-320">Syslog is an event logging protocol similar to Windows Event logs—both operate similarly when displayed in OMS.</span><span class="sxs-lookup"><span data-stu-id="8acbc-320">Syslog is an event logging protocol similar to Windows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="to-add-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="8acbc-321">To add a new Linux syslog facility in OMS</span><span class="sxs-lookup"><span data-stu-id="8acbc-321">To add a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="8acbc-322">On the **Settings** page under **Data** , click **Syslog** and then to the left of the plus icon, type the name of the syslog facility that you want to add.</span><span class="sxs-lookup"><span data-stu-id="8acbc-322">On the **Settings** page under **Data** , click **Syslog** and then to the left of the plus icon, type the name of the syslog facility that you want to add.</span></span>
    <span data-ttu-id="8acbc-323">![Linux syslog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="8acbc-323">![Linux syslog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="8acbc-324">If you don’t know the full name of the facility, you can start typing a partial name and a list of available syslog facilities will appear.</span><span class="sxs-lookup"><span data-stu-id="8acbc-324">If you don’t know the full name of the facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="8acbc-325">When you find the syslog facility that you want to add, click the name in the list and then click the plus icon to add the syslog facility.</span><span class="sxs-lookup"><span data-stu-id="8acbc-325">When you find the syslog facility that you want to add, click the name in the list and then click the plus icon to add the syslog facility.</span></span>
3. <span data-ttu-id="8acbc-326">After you add the facility, it appears in the list of highlighted with a colored bar.</span><span class="sxs-lookup"><span data-stu-id="8acbc-326">After you add the facility, it appears in the list of highlighted with a colored bar.</span></span> <span data-ttu-id="8acbc-327">Next, choose the severities (categories of syslog facility information) that you want to collect.</span><span class="sxs-lookup"><span data-stu-id="8acbc-327">Next, choose the severities (categories of syslog facility information) that you want to collect.</span></span>
4. <span data-ttu-id="8acbc-328">At the bottom of the page click **Save** to finalize your changes.</span><span class="sxs-lookup"><span data-stu-id="8acbc-328">At the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="8acbc-329">The configuration changes that you’ve made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="8acbc-329">The configuration changes that you’ve made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="8acbc-330">Configure Linux syslog facilities in Linux</span><span class="sxs-lookup"><span data-stu-id="8acbc-330">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="8acbc-331">Syslog events are sent from the syslog daemon, for example rsyslog or syslog-ng, to a local port that the agent is listening on.</span><span class="sxs-lookup"><span data-stu-id="8acbc-331">Syslog events are sent from the syslog daemon, for example rsyslog or syslog-ng, to a local port that the agent is listening on.</span></span> <span data-ttu-id="8acbc-332">By default, port 25224.</span><span class="sxs-lookup"><span data-stu-id="8acbc-332">By default, port 25224.</span></span> <span data-ttu-id="8acbc-333">When the agent is installed, a default syslog configuration is applied.</span><span class="sxs-lookup"><span data-stu-id="8acbc-333">When the agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="8acbc-334">This is found at:</span><span class="sxs-lookup"><span data-stu-id="8acbc-334">This is found at:</span></span>

<span data-ttu-id="8acbc-335">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="8acbc-335">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="8acbc-336">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="8acbc-336">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="8acbc-337">The default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span><span class="sxs-lookup"><span data-stu-id="8acbc-337">The default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="8acbc-338">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span><span class="sxs-lookup"><span data-stu-id="8acbc-338">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

<span data-ttu-id="8acbc-339">The default syslog configuration for the OMS Agent for Linux for OMS is:</span><span class="sxs-lookup"><span data-stu-id="8acbc-339">The default syslog configuration for the OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="8acbc-340">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="8acbc-340">Rsyslog</span></span>
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a><span data-ttu-id="8acbc-341">Syslog-ng</span><span class="sxs-lookup"><span data-stu-id="8acbc-341">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="to-view-all-syslog-events-with-log-analytics"></a><span data-ttu-id="8acbc-342">To view all Syslog events with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8acbc-342">To view all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="8acbc-343">In the Operations Management Suite portal, click the **Log Search** tile.</span><span class="sxs-lookup"><span data-stu-id="8acbc-343">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="8acbc-344">In the **Log Management** grouping, choose a predefined syslog search and then select one to run it.</span><span class="sxs-lookup"><span data-stu-id="8acbc-344">In the **Log Management** grouping, choose a predefined syslog search and then select one to run it.</span></span>

<span data-ttu-id="8acbc-345">This example shows all Syslog events.</span><span class="sxs-lookup"><span data-stu-id="8acbc-345">This example shows all Syslog events.</span></span>

![Syslog events shown in Log Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="8acbc-347">Now you can drill into search results.</span><span class="sxs-lookup"><span data-stu-id="8acbc-347">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="8acbc-348">Linux alerts</span><span class="sxs-lookup"><span data-stu-id="8acbc-348">Linux alerts</span></span>
<span data-ttu-id="8acbc-349">If you use Nagios or Zabbix to manage your Linux machines, then OMS can receive the alerts generated from those tools.</span><span class="sxs-lookup"><span data-stu-id="8acbc-349">If you use Nagios or Zabbix to manage your Linux machines, then OMS can receive the alerts generated from those tools.</span></span> <span data-ttu-id="8acbc-350">However, there is currently no method to configure incoming alert data using the OMS portal.</span><span class="sxs-lookup"><span data-stu-id="8acbc-350">However, there is currently no method to configure incoming alert data using the OMS portal.</span></span> <span data-ttu-id="8acbc-351">Instead, you will need to edit a config file to start sending alerts to OMS.</span><span class="sxs-lookup"><span data-stu-id="8acbc-351">Instead, you will need to edit a config file to start sending alerts to OMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="8acbc-352">Collect alerts from Nagios</span><span class="sxs-lookup"><span data-stu-id="8acbc-352">Collect alerts from Nagios</span></span>
<span data-ttu-id="8acbc-353">To collect alerts from a Nagios server, you need to make the following configuration changes.</span><span class="sxs-lookup"><span data-stu-id="8acbc-353">To collect alerts from a Nagios server, you need to make the following configuration changes.</span></span>

1. <span data-ttu-id="8acbc-354">Grant the user **omsagent** read access to the Nagios log file (i.e. /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="8acbc-354">Grant the user **omsagent** read access to the Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="8acbc-355">Assuming the nagios.log file is owned by the group **nagios** , you can add the user **omsagent** to the **nagios** group.</span><span class="sxs-lookup"><span data-stu-id="8acbc-355">Assuming the nagios.log file is owned by the group **nagios** , you can add the user **omsagent** to the **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="8acbc-356">Modify the omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="8acbc-356">Modify the omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="8acbc-357">Ensure the following entries are present and not commented out:</span><span class="sxs-lookup"><span data-stu-id="8acbc-357">Ensure the following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path to point to your nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="8acbc-358">Restart the omsagent daemon:</span><span class="sxs-lookup"><span data-stu-id="8acbc-358">Restart the omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="8acbc-359">Collect alerts from Zabbix</span><span class="sxs-lookup"><span data-stu-id="8acbc-359">Collect alerts from Zabbix</span></span>
<span data-ttu-id="8acbc-360">To collect alerts from a Zabbix server, you'll perform similar steps to those for Nagios above, except you'll need to specify a user and password in *clear text*.</span><span class="sxs-lookup"><span data-stu-id="8acbc-360">To collect alerts from a Zabbix server, you'll perform similar steps to those for Nagios above, except you'll need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="8acbc-361">This is not ideal, but will likely change soon.</span><span class="sxs-lookup"><span data-stu-id="8acbc-361">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="8acbc-362">To address this issue, we recommend that you create the user and grant it permission to monitor only.</span><span class="sxs-lookup"><span data-stu-id="8acbc-362">To address this issue, we recommend that you create the user and grant it permission to monitor only.</span></span>

<span data-ttu-id="8acbc-363">An example section of the omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble the following:</span><span class="sxs-lookup"><span data-stu-id="8acbc-363">An example section of the omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble the following:</span></span>

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="8acbc-364">View alerts in Log Analytics search</span><span class="sxs-lookup"><span data-stu-id="8acbc-364">View alerts in Log Analytics search</span></span>
<span data-ttu-id="8acbc-365">After you've configured your Linux computers to send alerts to OMS, you can use a few simple log search queries to view the alerts.</span><span class="sxs-lookup"><span data-stu-id="8acbc-365">After you've configured your Linux computers to send alerts to OMS, you can use a few simple log search queries to view the alerts.</span></span> <span data-ttu-id="8acbc-366">The following search query example returns all the recorded alerts that were generated.</span><span class="sxs-lookup"><span data-stu-id="8acbc-366">The following search query example returns all the recorded alerts that were generated.</span></span> <span data-ttu-id="8acbc-367">For example, if some sort of problem occurs in your IT infrastructure, then results for the following example query might indicate where the problem might originate.</span><span class="sxs-lookup"><span data-stu-id="8acbc-367">For example, if some sort of problem occurs in your IT infrastructure, then results for the following example query might indicate where the problem might originate.</span></span> <span data-ttu-id="8acbc-368">And, you can easily drill in to the alerts by source system to help narrow your investigation.</span><span class="sxs-lookup"><span data-stu-id="8acbc-368">And, you can easily drill in to the alerts by source system to help narrow your investigation.</span></span> <span data-ttu-id="8acbc-369">The benefit is that you don't necessarily have to go to various management systems from the start—provided that your alerts are sent to OMS, you can start there.</span><span class="sxs-lookup"><span data-stu-id="8acbc-369">The benefit is that you don't necessarily have to go to various management systems from the start—provided that your alerts are sent to OMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="to-view-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="8acbc-370">To view all Nagios alerts with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8acbc-370">To view all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="8acbc-371">In the Operations Management Suite portal, click the **Log Search** tile.</span><span class="sxs-lookup"><span data-stu-id="8acbc-371">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="8acbc-372">In the query bar, type the following search query</span><span class="sxs-lookup"><span data-stu-id="8acbc-372">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Nagios alerts shown in Log Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="8acbc-374">After you see the search results, you can drill into additional details such as *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="8acbc-374">After you see the search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="to-view-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="8acbc-375">To view all Zabbix alerts with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8acbc-375">To view all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="8acbc-376">In the Operations Management Suite portal, click the **Log Search** tile.</span><span class="sxs-lookup"><span data-stu-id="8acbc-376">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="8acbc-377">In the query bar, type the following search query</span><span class="sxs-lookup"><span data-stu-id="8acbc-377">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Zabbix alerts shown in Log Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="8acbc-379">After you see the search results, you can drill into additional details such as *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="8acbc-379">After you see the search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="8acbc-380">Compatibility with System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="8acbc-380">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="8acbc-381">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span><span class="sxs-lookup"><span data-stu-id="8acbc-381">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="8acbc-382">Installing the OMS Agent for Linux on a system currently managed by Operations Manager upgrades the OMI and SCX packages on the computer to a newer version.</span><span class="sxs-lookup"><span data-stu-id="8acbc-382">Installing the OMS Agent for Linux on a system currently managed by Operations Manager upgrades the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="8acbc-383">The OMS Agent for Linux and System Center 2012 R2 are compatible.</span><span class="sxs-lookup"><span data-stu-id="8acbc-383">The OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="8acbc-384">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.**</span><span class="sxs-lookup"><span data-stu-id="8acbc-384">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="8acbc-385">If the OMS Agent for Linux is installed to a computer that is not currently managed by Operations Manager, and you later want to manage the computer with Operations Manager, you must modify the OMI configuration before you discover the computer.</span><span class="sxs-lookup"><span data-stu-id="8acbc-385">If the OMS Agent for Linux is installed to a computer that is not currently managed by Operations Manager, and you later want to manage the computer with Operations Manager, you must modify the OMI configuration before you discover the computer.</span></span> <span data-ttu-id="8acbc-386">**This step is not needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span><span class="sxs-lookup"><span data-stu-id="8acbc-386">**This step is not needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>
>
>

### <a name="to-enable-the-oms-agent-for-linux-to-communicate-with-operations-manager"></a><span data-ttu-id="8acbc-387">To enable the OMS Agent for Linux to communicate with Operations Manager</span><span class="sxs-lookup"><span data-stu-id="8acbc-387">To enable the OMS Agent for Linux to communicate with Operations Manager</span></span>
1. <span data-ttu-id="8acbc-388">Edit the file /etc/opt/omi/conf/omiserver.conf</span><span class="sxs-lookup"><span data-stu-id="8acbc-388">Edit the file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="8acbc-389">Ensure that the line beginning with **httpsport=** defines the port 1270.</span><span class="sxs-lookup"><span data-stu-id="8acbc-389">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="8acbc-390">Such as `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="8acbc-390">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="8acbc-391">Restart the OMI server:</span><span class="sxs-lookup"><span data-stu-id="8acbc-391">Restart the OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="8acbc-392">Database permissions required for MySQL performance counters</span><span class="sxs-lookup"><span data-stu-id="8acbc-392">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="8acbc-393">To grant permissions to a MySQL monitoring user, the granting user must have the 'GRANT option' privilege as well as the privilege being granted.</span><span class="sxs-lookup"><span data-stu-id="8acbc-393">To grant permissions to a MySQL monitoring user, the granting user must have the 'GRANT option' privilege as well as the privilege being granted.</span></span>

<span data-ttu-id="8acbc-394">In order for the MySQL User to return performance data the user will need access to the following queries:</span><span class="sxs-lookup"><span data-stu-id="8acbc-394">In order for the MySQL User to return performance data the user will need access to the following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="8acbc-395">In addition to these queries the MySQL user requires SELECT access to the following default tables:</span><span class="sxs-lookup"><span data-stu-id="8acbc-395">In addition to these queries the MySQL user requires SELECT access to the following default tables:</span></span>

* <span data-ttu-id="8acbc-396">information_schema</span><span class="sxs-lookup"><span data-stu-id="8acbc-396">information_schema</span></span>
* <span data-ttu-id="8acbc-397">mysql</span><span class="sxs-lookup"><span data-stu-id="8acbc-397">mysql</span></span>

<span data-ttu-id="8acbc-398">These privileges can be granted by running the following grant commands.</span><span class="sxs-lookup"><span data-stu-id="8acbc-398">These privileges can be granted by running the following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-the-authentication-file"></a><span data-ttu-id="8acbc-399">Manage MySQL monitoring credentials in the authentication file</span><span class="sxs-lookup"><span data-stu-id="8acbc-399">Manage MySQL monitoring credentials in the authentication file</span></span>
<span data-ttu-id="8acbc-400">The following sections help you manage MySQL credentials.</span><span class="sxs-lookup"><span data-stu-id="8acbc-400">The following sections help you manage MySQL credentials.</span></span>

### <a name="configure-the-mysql-omi-provider"></a><span data-ttu-id="8acbc-401">Configure the MySQL OMI provider</span><span class="sxs-lookup"><span data-stu-id="8acbc-401">Configure the MySQL OMI provider</span></span>
<span data-ttu-id="8acbc-402">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance/health information from the MySQL instance.</span><span class="sxs-lookup"><span data-stu-id="8acbc-402">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance/health information from the MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="8acbc-403">MySQL OMI authentication file</span><span class="sxs-lookup"><span data-stu-id="8acbc-403">MySQL OMI authentication file</span></span>
<span data-ttu-id="8acbc-404">MySQL OMI provider uses an authentication file to determine what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span><span class="sxs-lookup"><span data-stu-id="8acbc-404">MySQL OMI provider uses an authentication file to determine what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span> <span data-ttu-id="8acbc-405">During installation the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span><span class="sxs-lookup"><span data-stu-id="8acbc-405">During installation the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="8acbc-406">To complete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into the correct directory.</span><span class="sxs-lookup"><span data-stu-id="8acbc-406">To complete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into the correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="8acbc-407">Authentication file format</span><span class="sxs-lookup"><span data-stu-id="8acbc-407">Authentication file format</span></span>
<span data-ttu-id="8acbc-408">The MySQL OMI authentication file is a text file that contains information about:</span><span class="sxs-lookup"><span data-stu-id="8acbc-408">The MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="8acbc-409">Port</span><span class="sxs-lookup"><span data-stu-id="8acbc-409">Port</span></span>
* <span data-ttu-id="8acbc-410">Bind-Address</span><span class="sxs-lookup"><span data-stu-id="8acbc-410">Bind-Address</span></span>
* <span data-ttu-id="8acbc-411">MySQL username</span><span class="sxs-lookup"><span data-stu-id="8acbc-411">MySQL username</span></span>
* <span data-ttu-id="8acbc-412">Base64 encoded password</span><span class="sxs-lookup"><span data-stu-id="8acbc-412">Base64 encoded password</span></span>

<span data-ttu-id="8acbc-413">The MySQL OMI authentication file only grants privileges for read/write to the Linux user that generated it.</span><span class="sxs-lookup"><span data-stu-id="8acbc-413">The MySQL OMI authentication file only grants privileges for read/write to the Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="8acbc-414">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from the found MySQL configuration file.</span><span class="sxs-lookup"><span data-stu-id="8acbc-414">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from the found MySQL configuration file.</span></span>

<span data-ttu-id="8acbc-415">The default instance is a means to make managing multiple MySQL instances on one Linux host easier, and is denoted by the instance with port 0.</span><span class="sxs-lookup"><span data-stu-id="8acbc-415">The default instance is a means to make managing multiple MySQL instances on one Linux host easier, and is denoted by the instance with port 0.</span></span> <span data-ttu-id="8acbc-416">All added instances will inherit properties set from the default instance.</span><span class="sxs-lookup"><span data-stu-id="8acbc-416">All added instances will inherit properties set from the default instance.</span></span> <span data-ttu-id="8acbc-417">For example, if MySQL instance listening on port '3308' is added, the default instance's bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span><span class="sxs-lookup"><span data-stu-id="8acbc-417">For example, if MySQL instance listening on port '3308' is added, the default instance's bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="8acbc-418">If the instance on 3308 is binded to another address and uses the same MySQL username and password pair only the respecification of the bind-address is needed and the other properties will be inherited.</span><span class="sxs-lookup"><span data-stu-id="8acbc-418">If the instance on 3308 is binded to another address and uses the same MySQL username and password pair only the respecification of the bind-address is needed and the other properties will be inherited.</span></span>

<span data-ttu-id="8acbc-419">Examples of the authentication file resemble the following.</span><span class="sxs-lookup"><span data-stu-id="8acbc-419">Examples of the authentication file resemble the following.</span></span>

<span data-ttu-id="8acbc-420">Default instance and instance with port 3308:</span><span class="sxs-lookup"><span data-stu-id="8acbc-420">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="8acbc-421">Default instance and instance with port 3308 + different Base 64 encoded password:</span><span class="sxs-lookup"><span data-stu-id="8acbc-421">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="8acbc-422">**Property**</span><span class="sxs-lookup"><span data-stu-id="8acbc-422">**Property**</span></span> | <span data-ttu-id="8acbc-423">**Description**</span><span class="sxs-lookup"><span data-stu-id="8acbc-423">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="8acbc-424">Port</span><span class="sxs-lookup"><span data-stu-id="8acbc-424">Port</span></span> |<span data-ttu-id="8acbc-425">Port represents the current port the MySQL instance is listening on.</span><span class="sxs-lookup"><span data-stu-id="8acbc-425">Port represents the current port the MySQL instance is listening on.</span></span>  <span data-ttu-id="8acbc-426">The port 0 implies that the properties following are used for default instance.</span><span class="sxs-lookup"><span data-stu-id="8acbc-426">The port 0 implies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="8acbc-427">Bind-Address</span><span class="sxs-lookup"><span data-stu-id="8acbc-427">Bind-Address</span></span> |<span data-ttu-id="8acbc-428">the Bind Address is the current MySQL bind-address</span><span class="sxs-lookup"><span data-stu-id="8acbc-428">the Bind Address is the current MySQL bind-address</span></span> |
| <span data-ttu-id="8acbc-429">username</span><span class="sxs-lookup"><span data-stu-id="8acbc-429">username</span></span> |<span data-ttu-id="8acbc-430">This the username of the MySQL user you wish to use to monitor the MySQL server instance.</span><span class="sxs-lookup"><span data-stu-id="8acbc-430">This the username of the MySQL user you wish to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="8acbc-431">Base64 encoded Password</span><span class="sxs-lookup"><span data-stu-id="8acbc-431">Base64 encoded Password</span></span> |<span data-ttu-id="8acbc-432">This is the password of the MySQL monitoring user encoded in Base64.</span><span class="sxs-lookup"><span data-stu-id="8acbc-432">This is the password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="8acbc-433">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="8acbc-433">AutoUpdate</span></span> |<span data-ttu-id="8acbc-434">When the MySQL OMI Provider is upgraded the provider will rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file.</span><span class="sxs-lookup"><span data-stu-id="8acbc-434">When the MySQL OMI Provider is upgraded the provider will rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file.</span></span> <span data-ttu-id="8acbc-435">Set this flag to true or false depending on required updates to the MySQL OMI authentication file.</span><span class="sxs-lookup"><span data-stu-id="8acbc-435">Set this flag to true or false depending on required updates to the MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="8acbc-436">Authentication file location</span><span class="sxs-lookup"><span data-stu-id="8acbc-436">Authentication file location</span></span>
<span data-ttu-id="8acbc-437">The MySQL OMI Authentication File should be located in the following location and named "mysql-auth":</span><span class="sxs-lookup"><span data-stu-id="8acbc-437">The MySQL OMI Authentication File should be located in the following location and named "mysql-auth":</span></span>

<span data-ttu-id="8acbc-438">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="8acbc-438">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="8acbc-439">The file (and auth/omsagent directory) should be owned by the omsagent user.</span><span class="sxs-lookup"><span data-stu-id="8acbc-439">The file (and auth/omsagent directory) should be owned by the omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="8acbc-440">Agent logs</span><span class="sxs-lookup"><span data-stu-id="8acbc-440">Agent logs</span></span>
<span data-ttu-id="8acbc-441">The logs for the OMS Agent for Linux is at:</span><span class="sxs-lookup"><span data-stu-id="8acbc-441">The logs for the OMS Agent for Linux is at:</span></span>

<span data-ttu-id="8acbc-442">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="8acbc-442">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="8acbc-443">The logs for the OMS Agent for Linux for omsconfig (agent configuration) program is at:</span><span class="sxs-lookup"><span data-stu-id="8acbc-443">The logs for the OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="8acbc-444">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="8acbc-444">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="8acbc-445">Logs for the OMI and SCX components (which provide performance metrics data) is at:</span><span class="sxs-lookup"><span data-stu-id="8acbc-445">Logs for the OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="8acbc-446">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="8acbc-446">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-the-oms-agent-for-linux"></a><span data-ttu-id="8acbc-447">Troubleshooting the OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="8acbc-447">Troubleshooting the OMS Agent for Linux</span></span>
<span data-ttu-id="8acbc-448">Use the following information to diagnose and troubleshoot common issues.</span><span class="sxs-lookup"><span data-stu-id="8acbc-448">Use the following information to diagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="8acbc-449">If none of the troubleshooting information in this section helps you, you can also use the following resources to help resolve your problem.</span><span class="sxs-lookup"><span data-stu-id="8acbc-449">If none of the troubleshooting information in this section helps you, you can also use the following resources to help resolve your problem.</span></span>

* <span data-ttu-id="8acbc-450">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="8acbc-450">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="8acbc-451">Customers with Azure support agreements can log support cases in the [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="8acbc-451">Customers with Azure support agreements can log support cases in the [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="8acbc-452">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span><span class="sxs-lookup"><span data-stu-id="8acbc-452">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="8acbc-453">Feedback forum for ideas and to create a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="8acbc-453">Feedback forum for ideas and to create a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="8acbc-454">Important log locations</span><span class="sxs-lookup"><span data-stu-id="8acbc-454">Important log locations</span></span>
| <span data-ttu-id="8acbc-455">File</span><span class="sxs-lookup"><span data-stu-id="8acbc-455">File</span></span> | <span data-ttu-id="8acbc-456">Path</span><span class="sxs-lookup"><span data-stu-id="8acbc-456">Path</span></span> |
| --- | --- |
| <span data-ttu-id="8acbc-457">OMS Agent for Linux Log File</span><span class="sxs-lookup"><span data-stu-id="8acbc-457">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="8acbc-458">OMS Agent Configuration Log File</span><span class="sxs-lookup"><span data-stu-id="8acbc-458">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="8acbc-459">Important configuration files</span><span class="sxs-lookup"><span data-stu-id="8acbc-459">Important configuration files</span></span>
| <span data-ttu-id="8acbc-460">Catergory</span><span class="sxs-lookup"><span data-stu-id="8acbc-460">Catergory</span></span> | <span data-ttu-id="8acbc-461">File Location</span><span class="sxs-lookup"><span data-stu-id="8acbc-461">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="8acbc-462">Syslog</span><span class="sxs-lookup"><span data-stu-id="8acbc-462">Syslog</span></span> |<span data-ttu-id="8acbc-463">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="8acbc-463">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="8acbc-464">Performance, Nagios, Zabbix, OMS output and general agent</span><span class="sxs-lookup"><span data-stu-id="8acbc-464">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="8acbc-465">Additional configurations</span><span class="sxs-lookup"><span data-stu-id="8acbc-465">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="8acbc-466">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span><span class="sxs-lookup"><span data-stu-id="8acbc-466">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="8acbc-467">You can disable configuration in the OMS Portal (for all nodes) or for single nodes by running the following:</span><span class="sxs-lookup"><span data-stu-id="8acbc-467">You can disable configuration in the OMS Portal (for all nodes) or for single nodes by running the following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="8acbc-468">Enable debug logging</span><span class="sxs-lookup"><span data-stu-id="8acbc-468">Enable debug logging</span></span>
<span data-ttu-id="8acbc-469">To enable debug logging, you can use the OMS output plugin and verbose output.</span><span class="sxs-lookup"><span data-stu-id="8acbc-469">To enable debug logging, you can use the OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="8acbc-470">OMS output plugin</span><span class="sxs-lookup"><span data-stu-id="8acbc-470">OMS output plugin</span></span>
<span data-ttu-id="8acbc-471">FluentD allows the plugin to specify logging levels for different log levels for inputs and outputs.</span><span class="sxs-lookup"><span data-stu-id="8acbc-471">FluentD allows the plugin to specify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="8acbc-472">To specify a different log level for OMS output, edit the general agent configuration in the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span><span class="sxs-lookup"><span data-stu-id="8acbc-472">To specify a different log level for OMS output, edit the general agent configuration in the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="8acbc-473">Near the bottom of the configuration file, change the `log_level` property from `info` to `debug`.</span><span class="sxs-lookup"><span data-stu-id="8acbc-473">Near the bottom of the configuration file, change the `log_level` property from `info` to `debug`.</span></span>

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

<span data-ttu-id="8acbc-474">Debug logging allows you to see batched uploads to the OMS Service separated by type, number of data items, and time taken to send.</span><span class="sxs-lookup"><span data-stu-id="8acbc-474">Debug logging allows you to see batched uploads to the OMS Service separated by type, number of data items, and time taken to send.</span></span>

<span data-ttu-id="8acbc-475">*Example debug enabled log:*</span><span class="sxs-lookup"><span data-stu-id="8acbc-475">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="8acbc-476">Verbose output</span><span class="sxs-lookup"><span data-stu-id="8acbc-476">Verbose output</span></span>
<span data-ttu-id="8acbc-477">Instead of using the OMS output plugin, you can also output data items directly to `stdout`, which is visible in the OMS Agent for Linux log file.</span><span class="sxs-lookup"><span data-stu-id="8acbc-477">Instead of using the OMS output plugin, you can also output data items directly to `stdout`, which is visible in the OMS Agent for Linux log file.</span></span>

<span data-ttu-id="8acbc-478">In the OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out the OMS output plugin by adding a `#` in front of each line.</span><span class="sxs-lookup"><span data-stu-id="8acbc-478">In the OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out the OMS output plugin by adding a `#` in front of each line.</span></span>

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

<span data-ttu-id="8acbc-479">Below the output plugin, remove the comment in the following section by removing the `#` symbol at the beginning of each line.</span><span class="sxs-lookup"><span data-stu-id="8acbc-479">Below the output plugin, remove the comment in the following section by removing the `#` symbol at the beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-the-log"></a><span data-ttu-id="8acbc-480">Forwarded Syslog messages do not appear in the log</span><span class="sxs-lookup"><span data-stu-id="8acbc-480">Forwarded Syslog messages do not appear in the log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="8acbc-481">Probable causes</span><span class="sxs-lookup"><span data-stu-id="8acbc-481">Probable causes</span></span>
* <span data-ttu-id="8acbc-482">The configuration applied to the Linux server does not allow collection of the sent facilities and/or log levels</span><span class="sxs-lookup"><span data-stu-id="8acbc-482">The configuration applied to the Linux server does not allow collection of the sent facilities and/or log levels</span></span>
* <span data-ttu-id="8acbc-483">Syslog is not being forwarded correctly to the Linux server</span><span class="sxs-lookup"><span data-stu-id="8acbc-483">Syslog is not being forwarded correctly to the Linux server</span></span>
* <span data-ttu-id="8acbc-484">The number of messages being forwarded per second are too large for the base configuration of the OMS Agent for Linux to handle</span><span class="sxs-lookup"><span data-stu-id="8acbc-484">The number of messages being forwarded per second are too large for the base configuration of the OMS Agent for Linux to handle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="8acbc-485">Resolutions</span><span class="sxs-lookup"><span data-stu-id="8acbc-485">Resolutions</span></span>
* <span data-ttu-id="8acbc-486">Verify that the configuration in the OMS Portal for Syslog has all the facilities and the correct log levels</span><span class="sxs-lookup"><span data-stu-id="8acbc-486">Verify that the configuration in the OMS Portal for Syslog has all the facilities and the correct log levels</span></span>
  * <span data-ttu-id="8acbc-487">**OMS Portal > Settings > Data > Syslog**</span><span class="sxs-lookup"><span data-stu-id="8acbc-487">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="8acbc-488">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able to receive the forwarded messages</span><span class="sxs-lookup"><span data-stu-id="8acbc-488">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able to receive the forwarded messages</span></span>
* <span data-ttu-id="8acbc-489">Check firewall settings on the Syslog server to ensure that messages are not being blocked</span><span class="sxs-lookup"><span data-stu-id="8acbc-489">Check firewall settings on the Syslog server to ensure that messages are not being blocked</span></span>
* <span data-ttu-id="8acbc-490">Simulate a Syslog message to OMS using the `logger` command - for example:</span><span class="sxs-lookup"><span data-stu-id="8acbc-490">Simulate a Syslog message to OMS using the `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-to-oms-when-using-a-proxy"></a><span data-ttu-id="8acbc-491">Problems connecting to OMS when using a proxy</span><span class="sxs-lookup"><span data-stu-id="8acbc-491">Problems connecting to OMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="8acbc-492">Probable causes</span><span class="sxs-lookup"><span data-stu-id="8acbc-492">Probable causes</span></span>
* <span data-ttu-id="8acbc-493">The proxy specified when installing and configuring the agent is incorrect</span><span class="sxs-lookup"><span data-stu-id="8acbc-493">The proxy specified when installing and configuring the agent is incorrect</span></span>
* <span data-ttu-id="8acbc-494">The OMS Service endpoints are not whitelistested in your datacenter</span><span class="sxs-lookup"><span data-stu-id="8acbc-494">The OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="8acbc-495">Resolutions</span><span class="sxs-lookup"><span data-stu-id="8acbc-495">Resolutions</span></span>
* <span data-ttu-id="8acbc-496">Reinstall the OMS Agent for Linux using the following command with the option `-v` enabled.</span><span class="sxs-lookup"><span data-stu-id="8acbc-496">Reinstall the OMS Agent for Linux using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="8acbc-497">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span><span class="sxs-lookup"><span data-stu-id="8acbc-497">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="8acbc-498">Review the documentation for OMS proxy at [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="8acbc-498">Review the documentation for OMS proxy at [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="8acbc-499">Verify that the following OMS Service endpoints are whitelisted</span><span class="sxs-lookup"><span data-stu-id="8acbc-499">Verify that the following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="8acbc-500">Agent Resource</span><span class="sxs-lookup"><span data-stu-id="8acbc-500">Agent Resource</span></span> | <span data-ttu-id="8acbc-501">Ports</span><span class="sxs-lookup"><span data-stu-id="8acbc-501">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="8acbc-502">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="8acbc-502">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="8acbc-503">Port 443</span><span class="sxs-lookup"><span data-stu-id="8acbc-503">Port 443</span></span> |
| <span data-ttu-id="8acbc-504">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="8acbc-504">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="8acbc-505">Port 443</span><span class="sxs-lookup"><span data-stu-id="8acbc-505">Port 443</span></span> |
| <span data-ttu-id="8acbc-506">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="8acbc-506">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="8acbc-507">Port 443</span><span class="sxs-lookup"><span data-stu-id="8acbc-507">Port 443</span></span> |
| <span data-ttu-id="8acbc-508">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="8acbc-508">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="8acbc-509">Port 443</span><span class="sxs-lookup"><span data-stu-id="8acbc-509">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="8acbc-510">A 403 error is displayed when onboarding</span><span class="sxs-lookup"><span data-stu-id="8acbc-510">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="8acbc-511">Probable causes</span><span class="sxs-lookup"><span data-stu-id="8acbc-511">Probable causes</span></span>
* <span data-ttu-id="8acbc-512">The date and time are incorrect on Linux Server</span><span class="sxs-lookup"><span data-stu-id="8acbc-512">The date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="8acbc-513">The Workspace ID and Workspace Key used are incorrect</span><span class="sxs-lookup"><span data-stu-id="8acbc-513">The Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="8acbc-514">Resolution</span><span class="sxs-lookup"><span data-stu-id="8acbc-514">Resolution</span></span>
* <span data-ttu-id="8acbc-515">Verify the time on your Linux server with the `date` command.</span><span class="sxs-lookup"><span data-stu-id="8acbc-515">Verify the time on your Linux server with the `date` command.</span></span> <span data-ttu-id="8acbc-516">If the data is greater than or less than 15 minutes from the current time, then onboarding fails.</span><span class="sxs-lookup"><span data-stu-id="8acbc-516">If the data is greater than or less than 15 minutes from the current time, then onboarding fails.</span></span> <span data-ttu-id="8acbc-517">To correct this, update the date and/or timezone of your Linux server.</span><span class="sxs-lookup"><span data-stu-id="8acbc-517">To correct this, update the date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="8acbc-518">The latest version of the OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span><span class="sxs-lookup"><span data-stu-id="8acbc-518">The latest version of the OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="8acbc-519">Re-onboard using the correct Workspace ID and Workspace Key.</span><span class="sxs-lookup"><span data-stu-id="8acbc-519">Re-onboard using the correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="8acbc-520">See  [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span><span class="sxs-lookup"><span data-stu-id="8acbc-520">See  [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-the-log-file-after-onboarding"></a><span data-ttu-id="8acbc-521">A 500 error or 404 error appears in the log file after onboarding</span><span class="sxs-lookup"><span data-stu-id="8acbc-521">A 500 error or 404 error appears in the log file after onboarding</span></span>
<span data-ttu-id="8acbc-522">This is a known issue that occurs during the first upload of Linux data into an OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="8acbc-522">This is a known issue that occurs during the first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="8acbc-523">This does not affect data being sent or other problems.</span><span class="sxs-lookup"><span data-stu-id="8acbc-523">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="8acbc-524">You can ignore the errors when initially onboarding.</span><span class="sxs-lookup"><span data-stu-id="8acbc-524">You can ignore the errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="8acbc-525">Nagios data does not appear in the OMS Portal</span><span class="sxs-lookup"><span data-stu-id="8acbc-525">Nagios data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="8acbc-526">Probable causes</span><span class="sxs-lookup"><span data-stu-id="8acbc-526">Probable causes</span></span>
* <span data-ttu-id="8acbc-527">The omsagent user does not have permissions to read from the Nagios log file</span><span class="sxs-lookup"><span data-stu-id="8acbc-527">The omsagent user does not have permissions to read from the Nagios log file</span></span>
* <span data-ttu-id="8acbc-528">The Nagios source and filter sections are still commented in the omsagent.conf file</span><span class="sxs-lookup"><span data-stu-id="8acbc-528">The Nagios source and filter sections are still commented in the omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="8acbc-529">Resolutions</span><span class="sxs-lookup"><span data-stu-id="8acbc-529">Resolutions</span></span>
* <span data-ttu-id="8acbc-530">Add the omsagent user in order to read from the Nagios file.</span><span class="sxs-lookup"><span data-stu-id="8acbc-530">Add the omsagent user in order to read from the Nagios file.</span></span> <span data-ttu-id="8acbc-531">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span><span class="sxs-lookup"><span data-stu-id="8acbc-531">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="8acbc-532">In the OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** the Nagios source and filter sections have comments removed, similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="8acbc-532">In the OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** the Nagios source and filter sections have comments removed, similar to the following example.</span></span>

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-the-oms-portal"></a><span data-ttu-id="8acbc-533">Linux data doesn't appear in the OMS Portal</span><span class="sxs-lookup"><span data-stu-id="8acbc-533">Linux data doesn't appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="8acbc-534">Probable causes</span><span class="sxs-lookup"><span data-stu-id="8acbc-534">Probable causes</span></span>
* <span data-ttu-id="8acbc-535">Onboarding to the OMS Service failed</span><span class="sxs-lookup"><span data-stu-id="8acbc-535">Onboarding to the OMS Service failed</span></span>
* <span data-ttu-id="8acbc-536">Connection to the OMS Service is blocked</span><span class="sxs-lookup"><span data-stu-id="8acbc-536">Connection to the OMS Service is blocked</span></span>
* <span data-ttu-id="8acbc-537">The OMS Agent for Linux data is backed-up</span><span class="sxs-lookup"><span data-stu-id="8acbc-537">The OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="8acbc-538">Resolutions</span><span class="sxs-lookup"><span data-stu-id="8acbc-538">Resolutions</span></span>
* <span data-ttu-id="8acbc-539">Verify that onboarding to the OMS Service was successful by verifying that the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span><span class="sxs-lookup"><span data-stu-id="8acbc-539">Verify that onboarding to the OMS Service was successful by verifying that the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="8acbc-540">Re-onboard using the omsadmin.sh command line.</span><span class="sxs-lookup"><span data-stu-id="8acbc-540">Re-onboard using the omsadmin.sh command line.</span></span> <span data-ttu-id="8acbc-541">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span><span class="sxs-lookup"><span data-stu-id="8acbc-541">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="8acbc-542">If using a proxy, use the proxy troubleshooting steps above</span><span class="sxs-lookup"><span data-stu-id="8acbc-542">If using a proxy, use the proxy troubleshooting steps above</span></span>
* <span data-ttu-id="8acbc-543">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the Agent is backed-up to the full buffer size of 50 MB.</span><span class="sxs-lookup"><span data-stu-id="8acbc-543">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the Agent is backed-up to the full buffer size of 50 MB.</span></span> <span data-ttu-id="8acbc-544">Restart the OMS Agent for Linux by running the `/opt/microsoft/omsagent/bin/service_control restart` command.</span><span class="sxs-lookup"><span data-stu-id="8acbc-544">Restart the OMS Agent for Linux by running the `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="8acbc-545">This issue is fixed in Agent version 1.1.0-28 and later.</span><span class="sxs-lookup"><span data-stu-id="8acbc-545">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-the-oms-portal"></a><span data-ttu-id="8acbc-546">Syslog Linux performance counter configuration is not applied in the OMS portal</span><span class="sxs-lookup"><span data-stu-id="8acbc-546">Syslog Linux performance counter configuration is not applied in the OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="8acbc-547">Probable causes</span><span class="sxs-lookup"><span data-stu-id="8acbc-547">Probable causes</span></span>
* <span data-ttu-id="8acbc-548">The configuration agent in the OMS Agent for Linux has not retrieved the latest configuration from the OMS portal.</span><span class="sxs-lookup"><span data-stu-id="8acbc-548">The configuration agent in the OMS Agent for Linux has not retrieved the latest configuration from the OMS portal.</span></span>
* <span data-ttu-id="8acbc-549">The revised settings in the portal were not applied</span><span class="sxs-lookup"><span data-stu-id="8acbc-549">The revised settings in the portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="8acbc-550">Resolutions</span><span class="sxs-lookup"><span data-stu-id="8acbc-550">Resolutions</span></span>
<span data-ttu-id="8acbc-551">`omsconfig` is the configuration agent in the OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="8acbc-551">`omsconfig` is the configuration agent in the OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="8acbc-552">This configuration is then applied to the OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="8acbc-552">This configuration is then applied to the OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="8acbc-553">In some cases, the OMS Agent for Linux configuration agent might not be able to communicate with the portal configuration service resulting in latest configuration not being applied.</span><span class="sxs-lookup"><span data-stu-id="8acbc-553">In some cases, the OMS Agent for Linux configuration agent might not be able to communicate with the portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="8acbc-554">Verify that the `omsconfig` agent is installed with the following:</span><span class="sxs-lookup"><span data-stu-id="8acbc-554">Verify that the `omsconfig` agent is installed with the following:</span></span>

  * <span data-ttu-id="8acbc-555">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="8acbc-555">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="8acbc-556">If not installed, reinstall the latest version of the OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="8acbc-556">If not installed, reinstall the latest version of the OMS Agent for Linux</span></span>
* <span data-ttu-id="8acbc-557">Verify that the `omsconfig` agent can communicate with the OMS service</span><span class="sxs-lookup"><span data-stu-id="8acbc-557">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="8acbc-558">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span><span class="sxs-lookup"><span data-stu-id="8acbc-558">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="8acbc-559">The command above returns the configuration that agent retrieves from the portal, including Syslog settings, Linux performance counters, and custom logs</span><span class="sxs-lookup"><span data-stu-id="8acbc-559">The command above returns the configuration that agent retrieves from the portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="8acbc-560">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span><span class="sxs-lookup"><span data-stu-id="8acbc-560">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="8acbc-561">This command forces the omsconfig agent to communicate with the OMS service to retrieve the latest configuration.</span><span class="sxs-lookup"><span data-stu-id="8acbc-561">This command forces the omsconfig agent to communicate with the OMS service to retrieve the latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="8acbc-562">Custom Linux log data does not appear in the OMS Portal</span><span class="sxs-lookup"><span data-stu-id="8acbc-562">Custom Linux log data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="8acbc-563">Probable causes</span><span class="sxs-lookup"><span data-stu-id="8acbc-563">Probable causes</span></span>
* <span data-ttu-id="8acbc-564">Onboarding to OMS Service failed</span><span class="sxs-lookup"><span data-stu-id="8acbc-564">Onboarding to OMS Service failed</span></span>
* <span data-ttu-id="8acbc-565">The **Apply the following configuration to my Linux Servers** setting has not been selected</span><span class="sxs-lookup"><span data-stu-id="8acbc-565">The **Apply the following configuration to my Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="8acbc-566">omsconfig has not picked up the latest custom log from the portal</span><span class="sxs-lookup"><span data-stu-id="8acbc-566">omsconfig has not picked up the latest custom log from the portal</span></span>
* <span data-ttu-id="8acbc-567">The `omsagent` use is unable to access the custom log due to a permissions problem or `omsagent` was not found.</span><span class="sxs-lookup"><span data-stu-id="8acbc-567">The `omsagent` use is unable to access the custom log due to a permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="8acbc-568">In this case, you'll see the following output:</span><span class="sxs-lookup"><span data-stu-id="8acbc-568">In this case, you'll see the following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="8acbc-569">This is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217</span><span class="sxs-lookup"><span data-stu-id="8acbc-569">This is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="8acbc-570">Resolutions</span><span class="sxs-lookup"><span data-stu-id="8acbc-570">Resolutions</span></span>
* <span data-ttu-id="8acbc-571">Verify that you've successfully onboarded, by determining whether the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span><span class="sxs-lookup"><span data-stu-id="8acbc-571">Verify that you've successfully onboarded, by determining whether the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="8acbc-572">If needed, onboard again using the omsadmin.sh command line.</span><span class="sxs-lookup"><span data-stu-id="8acbc-572">If needed, onboard again using the omsadmin.sh command line.</span></span> <span data-ttu-id="8acbc-573">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span><span class="sxs-lookup"><span data-stu-id="8acbc-573">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="8acbc-574">In the OMS Portal, under **Settings** on the **Data** tab, ensure that the **Apply the following configuration to my Linux Servers** setting is selected</span><span class="sxs-lookup"><span data-stu-id="8acbc-574">In the OMS Portal, under **Settings** on the **Data** tab, ensure that the **Apply the following configuration to my Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="8acbc-575">![apply configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="8acbc-575">![apply configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="8acbc-576">Verify that the `omsconfig` agent can communicate with the OMS service</span><span class="sxs-lookup"><span data-stu-id="8acbc-576">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="8acbc-577">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span><span class="sxs-lookup"><span data-stu-id="8acbc-577">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="8acbc-578">The command above returns the configuration that agent retrieves from the Portal, including Syslog settings, Linux performance counters, and custom Logs</span><span class="sxs-lookup"><span data-stu-id="8acbc-578">The command above returns the configuration that agent retrieves from the Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="8acbc-579">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span><span class="sxs-lookup"><span data-stu-id="8acbc-579">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="8acbc-580">This command forces the omsconfig agent to communicate with OMS service and retrieve the latest configuration.</span><span class="sxs-lookup"><span data-stu-id="8acbc-580">This command forces the omsconfig agent to communicate with OMS service and retrieve the latest configuration.</span></span>

<span data-ttu-id="8acbc-581">Instead of the OMS Agent for Linux user running as a privileged user `root`, the OMS Agent for Linux runs as the `omsagent` user.</span><span class="sxs-lookup"><span data-stu-id="8acbc-581">Instead of the OMS Agent for Linux user running as a privileged user `root`, the OMS Agent for Linux runs as the `omsagent` user.</span></span> <span data-ttu-id="8acbc-582">In most cases, explicit permission must be granted to the user in order to read certain files.</span><span class="sxs-lookup"><span data-stu-id="8acbc-582">In most cases, explicit permission must be granted to the user in order to read certain files.</span></span>

<span data-ttu-id="8acbc-583">To grant permission to `omsagent` user, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="8acbc-583">To grant permission to `omsagent` user, run the following commands:</span></span>

1. <span data-ttu-id="8acbc-584">Add the `omsagent` user to a specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="8acbc-584">Add the `omsagent` user to a specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="8acbc-585">Grant universal read access to the required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="8acbc-585">Grant universal read access to the required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="8acbc-586">There is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217.</span><span class="sxs-lookup"><span data-stu-id="8acbc-586">There is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="8acbc-587">After updating to the latest agent, run the following command to get the latest version of the output plugin:</span><span class="sxs-lookup"><span data-stu-id="8acbc-587">After updating to the latest agent, run the following command to get the latest version of the output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="8acbc-588">Known limitations</span><span class="sxs-lookup"><span data-stu-id="8acbc-588">Known limitations</span></span>
<span data-ttu-id="8acbc-589">Review the following sections to learn about current limitations of the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="8acbc-589">Review the following sections to learn about current limitations of the OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="8acbc-590">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="8acbc-590">Azure Diagnostics</span></span>
<span data-ttu-id="8acbc-591">For Linux virtual machines running in Azure, additional steps may be required to allow data collection by Azure Diagnostics and Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="8acbc-591">For Linux virtual machines running in Azure, additional steps may be required to allow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="8acbc-592">**Version 2.2** of the Diagnostics Extension for Linux is required for compatibility with the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="8acbc-592">**Version 2.2** of the Diagnostics Extension for Linux is required for compatibility with the OMS Agent for Linux.</span></span>

<span data-ttu-id="8acbc-593">For more information on installing and configuring the Diagnostic Extension for Linux, see [Use the Azure CLI command to enable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="8acbc-593">For more information on installing and configuring the Diagnostic Extension for Linux, see [Use the Azure CLI command to enable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="8acbc-594">**Upgrading the Linux Diagnostics Extension from 2.0 to 2.2 Azure CLI ASM:**</span><span class="sxs-lookup"><span data-stu-id="8acbc-594">**Upgrading the Linux Diagnostics Extension from 2.0 to 2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="8acbc-595">**ARM**</span><span class="sxs-lookup"><span data-stu-id="8acbc-595">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="8acbc-596">These command examples reference a file named PrivateConfig.json.</span><span class="sxs-lookup"><span data-stu-id="8acbc-596">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="8acbc-597">The format of that file should resemble the following sample.</span><span class="sxs-lookup"><span data-stu-id="8acbc-597">The format of that file should resemble the following sample.</span></span>

```
    {
    "storageAccountName":"the storage account to receive data",
    "storageAccountKey":"the key of the account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="8acbc-598">Sysklog is not supported</span><span class="sxs-lookup"><span data-stu-id="8acbc-598">Sysklog is not supported</span></span>
<span data-ttu-id="8acbc-599">Either rsyslog or syslog-ng are required to collect syslog messages.</span><span class="sxs-lookup"><span data-stu-id="8acbc-599">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="8acbc-600">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span><span class="sxs-lookup"><span data-stu-id="8acbc-600">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="8acbc-601">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span><span class="sxs-lookup"><span data-stu-id="8acbc-601">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span> <span data-ttu-id="8acbc-602">For more information on replacing sysklog with rsyslog, see [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="8acbc-602">For more information on replacing sysklog with rsyslog, see [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8acbc-603">Next Steps</span><span class="sxs-lookup"><span data-stu-id="8acbc-603">Next Steps</span></span>
* <span data-ttu-id="8acbc-604">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span><span class="sxs-lookup"><span data-stu-id="8acbc-604">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
* <span data-ttu-id="8acbc-605">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span><span class="sxs-lookup"><span data-stu-id="8acbc-605">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="8acbc-606">Use [dashboards](log-analytics-dashboards.md) to save and display your own custom searches.</span><span class="sxs-lookup"><span data-stu-id="8acbc-606">Use [dashboards](log-analytics-dashboards.md) to save and display your own custom searches.</span></span>


































