---
title: Collect and analyze Syslog messages in OMS Log Analytics | Microsoft Docs
description: Syslog is an event logging protocol that is common to Linux.   This article describes how to configure collection of Syslog messages in Log Analytics and details of the records they create in the OMS repository.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: bwren
ms.openlocfilehash: 307749c1364d5b275068fcc90bf3a53903174070
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671723"
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="0ee32-104">Syslog data sources in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0ee32-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="0ee32-105">Syslog is an event logging protocol that is common to Linux.</span><span class="sxs-lookup"><span data-stu-id="0ee32-105">Syslog is an event logging protocol that is common to Linux.</span></span>  <span data-ttu-id="0ee32-106">Applications will send messages that may be stored on the local machine or delivered to a Syslog collector.</span><span class="sxs-lookup"><span data-stu-id="0ee32-106">Applications will send messages that may be stored on the local machine or delivered to a Syslog collector.</span></span>  <span data-ttu-id="0ee32-107">When the OMS Agent for Linux is installed, it configures the local Syslog daemon to forward messages to the agent.</span><span class="sxs-lookup"><span data-stu-id="0ee32-107">When the OMS Agent for Linux is installed, it configures the local Syslog daemon to forward messages to the agent.</span></span>  <span data-ttu-id="0ee32-108">The agent then sends the message to Log Analytics where a corresponding record is created in the OMS repository.</span><span class="sxs-lookup"><span data-stu-id="0ee32-108">The agent then sends the message to Log Analytics where a corresponding record is created in the OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="0ee32-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng.</span><span class="sxs-lookup"><span data-stu-id="0ee32-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng.</span></span> <span data-ttu-id="0ee32-110">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span><span class="sxs-lookup"><span data-stu-id="0ee32-110">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="0ee32-111">To collect syslog data from this version of these distributions, the [rsyslog daemon](http://rsyslog.com) should be installed and configured to replace sysklog.</span><span class="sxs-lookup"><span data-stu-id="0ee32-111">To collect syslog data from this version of these distributions, the [rsyslog daemon](http://rsyslog.com) should be installed and configured to replace sysklog.</span></span>
> 
> 

![Syslog collection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="0ee32-113">Configuring Syslog</span><span class="sxs-lookup"><span data-stu-id="0ee32-113">Configuring Syslog</span></span>
<span data-ttu-id="0ee32-114">The OMS Agent for Linux will only collect events with the facilities and severities that are specified in its configuration.</span><span class="sxs-lookup"><span data-stu-id="0ee32-114">The OMS Agent for Linux will only collect events with the facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="0ee32-115">You can configure Syslog through the OMS portal or by managing configuration files on your Linux agents.</span><span class="sxs-lookup"><span data-stu-id="0ee32-115">You can configure Syslog through the OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-the-oms-portal"></a><span data-ttu-id="0ee32-116">Configure Syslog in the OMS portal</span><span class="sxs-lookup"><span data-stu-id="0ee32-116">Configure Syslog in the OMS portal</span></span>
<span data-ttu-id="0ee32-117">Configure Syslog from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="0ee32-117">Configure Syslog from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="0ee32-118">This configuration is delivered to the configuration file on each Linux agent.</span><span class="sxs-lookup"><span data-stu-id="0ee32-118">This configuration is delivered to the configuration file on each Linux agent.</span></span>

<span data-ttu-id="0ee32-119">You can add a new facility by typing in its name and clicking **+**.</span><span class="sxs-lookup"><span data-stu-id="0ee32-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="0ee32-120">For each facility, only messages with the selected severities will be collected.</span><span class="sxs-lookup"><span data-stu-id="0ee32-120">For each facility, only messages with the selected severities will be collected.</span></span>  <span data-ttu-id="0ee32-121">Check the severities for the particular facility that you want to collect.</span><span class="sxs-lookup"><span data-stu-id="0ee32-121">Check the severities for the particular facility that you want to collect.</span></span>  <span data-ttu-id="0ee32-122">You cannot provide any additional criteria to filter messages.</span><span class="sxs-lookup"><span data-stu-id="0ee32-122">You cannot provide any additional criteria to filter messages.</span></span>

![Configure Syslog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="0ee32-124">By default, all configuration changes are automatically pushed to all agents.</span><span class="sxs-lookup"><span data-stu-id="0ee32-124">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="0ee32-125">If you want to configure Syslog manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span><span class="sxs-lookup"><span data-stu-id="0ee32-125">If you want to configure Syslog manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="0ee32-126">Configure Syslog on Linux agent</span><span class="sxs-lookup"><span data-stu-id="0ee32-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="0ee32-127">When the [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines the facility and severity of the messages that are collected.</span><span class="sxs-lookup"><span data-stu-id="0ee32-127">When the [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines the facility and severity of the messages that are collected.</span></span>  <span data-ttu-id="0ee32-128">You can modify this file to change the configuration.</span><span class="sxs-lookup"><span data-stu-id="0ee32-128">You can modify this file to change the configuration.</span></span>  <span data-ttu-id="0ee32-129">The configuration file is different depending on the Syslog daemon that the client has installed.</span><span class="sxs-lookup"><span data-stu-id="0ee32-129">The configuration file is different depending on the Syslog daemon that the client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="0ee32-130">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span><span class="sxs-lookup"><span data-stu-id="0ee32-130">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
> 
> 

#### <a name="rsyslog"></a><span data-ttu-id="0ee32-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="0ee32-131">rsyslog</span></span>
<span data-ttu-id="0ee32-132">The configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="0ee32-132">The configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="0ee32-133">Its default contents are shown below.</span><span class="sxs-lookup"><span data-stu-id="0ee32-133">Its default contents are shown below.</span></span>  <span data-ttu-id="0ee32-134">This collects syslog messages sent from the local agent for all facilities with a level of warning or higher.</span><span class="sxs-lookup"><span data-stu-id="0ee32-134">This collects syslog messages sent from the local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="0ee32-135">You can remove a facility by removing its section of the configuration file.</span><span class="sxs-lookup"><span data-stu-id="0ee32-135">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="0ee32-136">You can limit the severities that are collected for a particular facility by modifying that facility's entry.</span><span class="sxs-lookup"><span data-stu-id="0ee32-136">You can limit the severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="0ee32-137">For example, to limit the user facility to messages with a severity of error or higher you would modify that line of the configuration file to the following:</span><span class="sxs-lookup"><span data-stu-id="0ee32-137">For example, to limit the user facility to messages with a severity of error or higher you would modify that line of the configuration file to the following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="0ee32-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="0ee32-138">syslog-ng</span></span>
<span data-ttu-id="0ee32-139">The configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="0ee32-139">The configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="0ee32-140">Its default contents are shown below.</span><span class="sxs-lookup"><span data-stu-id="0ee32-140">Its default contents are shown below.</span></span>  <span data-ttu-id="0ee32-141">This collects syslog messages sent from the local agent for all facilities and all severities.</span><span class="sxs-lookup"><span data-stu-id="0ee32-141">This collects syslog messages sent from the local agent for all facilities and all severities.</span></span>   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

<span data-ttu-id="0ee32-142">You can remove a facility by removing its section of the configuration file.</span><span class="sxs-lookup"><span data-stu-id="0ee32-142">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="0ee32-143">You can limit the severities that are collected for a particular facility by removing them from its list.</span><span class="sxs-lookup"><span data-stu-id="0ee32-143">You can limit the severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="0ee32-144">For example, to limit the user facility to just alert and critical messages, you would modify that section of the configuration file to the following:</span><span class="sxs-lookup"><span data-stu-id="0ee32-144">For example, to limit the user facility to just alert and critical messages, you would modify that section of the configuration file to the following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="changing-the-syslog-port"></a><span data-ttu-id="0ee32-145">Changing the Syslog port</span><span class="sxs-lookup"><span data-stu-id="0ee32-145">Changing the Syslog port</span></span>
<span data-ttu-id="0ee32-146">The OMS agent listens for Syslog messages on the local client at port 25224.</span><span class="sxs-lookup"><span data-stu-id="0ee32-146">The OMS agent listens for Syslog messages on the local client at port 25224.</span></span>  <span data-ttu-id="0ee32-147">You can change this port by adding the following section to the OMS agent configuration file located at **/etc/opt/microsoft/omsagent/conf/omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="0ee32-147">You can change this port by adding the following section to the OMS agent configuration file located at **/etc/opt/microsoft/omsagent/conf/omsagent.conf**.</span></span>  <span data-ttu-id="0ee32-148">Replace 25224 in the **port** entry with the port number that you want.</span><span class="sxs-lookup"><span data-stu-id="0ee32-148">Replace 25224 in the **port** entry with the port number that you want.</span></span>  <span data-ttu-id="0ee32-149">Note that you will also need to modify the configuration file for the Syslog daemon to send messages to this port.</span><span class="sxs-lookup"><span data-stu-id="0ee32-149">Note that you will also need to modify the configuration file for the Syslog daemon to send messages to this port.</span></span>

    <source>
      type syslog
      port 25224
      bind 127.0.0.1
      protocol_type udp
      tag oms.syslog
    </source>


## <a name="data-collection"></a><span data-ttu-id="0ee32-150">Data collection</span><span class="sxs-lookup"><span data-stu-id="0ee32-150">Data collection</span></span>
<span data-ttu-id="0ee32-151">The OMS agent listens for Syslog messages on the local client at port 25224.</span><span class="sxs-lookup"><span data-stu-id="0ee32-151">The OMS agent listens for Syslog messages on the local client at port 25224.</span></span> <span data-ttu-id="0ee32-152">The configuration file for the Syslog daemon forwards Syslog messages sent from application to this port where they are collected by Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ee32-152">The configuration file for the Syslog daemon forwards Syslog messages sent from application to this port where they are collected by Log Analytics.</span></span>

## <a name="syslog-record-properties"></a><span data-ttu-id="0ee32-153">Syslog record properties</span><span class="sxs-lookup"><span data-stu-id="0ee32-153">Syslog record properties</span></span>
<span data-ttu-id="0ee32-154">Syslog records have a type of **Syslog** and have the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="0ee32-154">Syslog records have a type of **Syslog** and have the properties in the following table.</span></span>

| <span data-ttu-id="0ee32-155">Property</span><span class="sxs-lookup"><span data-stu-id="0ee32-155">Property</span></span> | <span data-ttu-id="0ee32-156">Description</span><span class="sxs-lookup"><span data-stu-id="0ee32-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0ee32-157">Computer</span><span class="sxs-lookup"><span data-stu-id="0ee32-157">Computer</span></span> |<span data-ttu-id="0ee32-158">Computer that the event was collected from.</span><span class="sxs-lookup"><span data-stu-id="0ee32-158">Computer that the event was collected from.</span></span> |
| <span data-ttu-id="0ee32-159">Facility</span><span class="sxs-lookup"><span data-stu-id="0ee32-159">Facility</span></span> |<span data-ttu-id="0ee32-160">Defines the part of the system that generated the message.</span><span class="sxs-lookup"><span data-stu-id="0ee32-160">Defines the part of the system that generated the message.</span></span> |
| <span data-ttu-id="0ee32-161">HostIP</span><span class="sxs-lookup"><span data-stu-id="0ee32-161">HostIP</span></span> |<span data-ttu-id="0ee32-162">IP address of the system sending the message.</span><span class="sxs-lookup"><span data-stu-id="0ee32-162">IP address of the system sending the message.</span></span> |
| <span data-ttu-id="0ee32-163">HostName</span><span class="sxs-lookup"><span data-stu-id="0ee32-163">HostName</span></span> |<span data-ttu-id="0ee32-164">Name of the system sending the message.</span><span class="sxs-lookup"><span data-stu-id="0ee32-164">Name of the system sending the message.</span></span> |
| <span data-ttu-id="0ee32-165">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="0ee32-165">SeverityLevel</span></span> |<span data-ttu-id="0ee32-166">Severity level of the event.</span><span class="sxs-lookup"><span data-stu-id="0ee32-166">Severity level of the event.</span></span> |
| <span data-ttu-id="0ee32-167">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="0ee32-167">SyslogMessage</span></span> |<span data-ttu-id="0ee32-168">Text of the message.</span><span class="sxs-lookup"><span data-stu-id="0ee32-168">Text of the message.</span></span> |
| <span data-ttu-id="0ee32-169">ProcessID</span><span class="sxs-lookup"><span data-stu-id="0ee32-169">ProcessID</span></span> |<span data-ttu-id="0ee32-170">ID of the process that generated the message.</span><span class="sxs-lookup"><span data-stu-id="0ee32-170">ID of the process that generated the message.</span></span> |
| <span data-ttu-id="0ee32-171">EventTime</span><span class="sxs-lookup"><span data-stu-id="0ee32-171">EventTime</span></span> |<span data-ttu-id="0ee32-172">Date and time that the event was generated.</span><span class="sxs-lookup"><span data-stu-id="0ee32-172">Date and time that the event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="0ee32-173">Log queries with Syslog records</span><span class="sxs-lookup"><span data-stu-id="0ee32-173">Log queries with Syslog records</span></span>
<span data-ttu-id="0ee32-174">The following table provides different examples of log queries that retrieve Syslog records.</span><span class="sxs-lookup"><span data-stu-id="0ee32-174">The following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="0ee32-175">Query</span><span class="sxs-lookup"><span data-stu-id="0ee32-175">Query</span></span> | <span data-ttu-id="0ee32-176">Description</span><span class="sxs-lookup"><span data-stu-id="0ee32-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0ee32-177">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="0ee32-177">Type=Syslog</span></span> |<span data-ttu-id="0ee32-178">All Syslogs.</span><span class="sxs-lookup"><span data-stu-id="0ee32-178">All Syslogs.</span></span> |
| <span data-ttu-id="0ee32-179">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="0ee32-179">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="0ee32-180">All Syslog records with severity of error.</span><span class="sxs-lookup"><span data-stu-id="0ee32-180">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="0ee32-181">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="0ee32-181">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="0ee32-182">Count of Syslog records by computer.</span><span class="sxs-lookup"><span data-stu-id="0ee32-182">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="0ee32-183">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="0ee32-183">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="0ee32-184">Count of Syslog records by facility.</span><span class="sxs-lookup"><span data-stu-id="0ee32-184">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0ee32-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ee32-185">Next steps</span></span>
* <span data-ttu-id="0ee32-186">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span><span class="sxs-lookup"><span data-stu-id="0ee32-186">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="0ee32-187">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span><span class="sxs-lookup"><span data-stu-id="0ee32-187">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="0ee32-188">[Configure Linux agents](log-analytics-linux-agents.md) to collect other types of data.</span><span class="sxs-lookup"><span data-stu-id="0ee32-188">[Configure Linux agents](log-analytics-linux-agents.md) to collect other types of data.</span></span> 



