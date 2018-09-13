---
title: Collect Nagios and Zabbix alerts in OMS Log Analytics | Microsoft Docs
description: Nagios and Zabbix are open source monitoring tools. You can collect alerts from these tools into Log Analytics in order to analyze them along with alerts from other sources.  This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/13/2018
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 240e56e3e482b81d6336f7d6d2a1f5688953ecd8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966966"
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="4ff40-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="4ff40-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="4ff40-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span><span class="sxs-lookup"><span data-stu-id="4ff40-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span> <span data-ttu-id="4ff40-107">You can collect alerts from these tools into Log Analytics in order to analyze them along with [alerts from other sources](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4ff40-107">You can collect alerts from these tools into Log Analytics in order to analyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="4ff40-108">This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.</span><span class="sxs-lookup"><span data-stu-id="4ff40-108">This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="4ff40-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4ff40-109">Prerequisites</span></span>
<span data-ttu-id="4ff40-110">The OMS Agent for Linux supports collecting alerts from Nagios up to version 4.2.x, and Zabbix up to version 2.x.</span><span class="sxs-lookup"><span data-stu-id="4ff40-110">The OMS Agent for Linux supports collecting alerts from Nagios up to version 4.2.x, and Zabbix up to version 2.x.</span></span>

## <a name="configure-alert-collection"></a><span data-ttu-id="4ff40-111">Configure alert collection</span><span class="sxs-lookup"><span data-stu-id="4ff40-111">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="4ff40-112">Configuring Nagios alert collection</span><span class="sxs-lookup"><span data-stu-id="4ff40-112">Configuring Nagios alert collection</span></span>
<span data-ttu-id="4ff40-113">To collect alerts, perform the following steps on the Nagios server.</span><span class="sxs-lookup"><span data-stu-id="4ff40-113">To collect alerts, perform the following steps on the Nagios server.</span></span>

1. <span data-ttu-id="4ff40-114">Grant the user **omsagent** read access to the Nagios log file `/var/log/nagios/nagios.log`.</span><span class="sxs-lookup"><span data-stu-id="4ff40-114">Grant the user **omsagent** read access to the Nagios log file `/var/log/nagios/nagios.log`.</span></span> <span data-ttu-id="4ff40-115">Assuming the nagios.log file is owned by the group `nagios`, you can add the user **omsagent** to the **nagios** group.</span><span class="sxs-lookup"><span data-stu-id="4ff40-115">Assuming the nagios.log file is owned by the group `nagios`, you can add the user **omsagent** to the **nagios** group.</span></span> 

    <span data-ttu-id="4ff40-116">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="4ff40-116">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="4ff40-117">Modify the configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`.</span><span class="sxs-lookup"><span data-stu-id="4ff40-117">Modify the configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`.</span></span> <span data-ttu-id="4ff40-118">Ensure the following entries are present and not commented out:</span><span class="sxs-lookup"><span data-stu-id="4ff40-118">Ensure the following entries are present and not commented out:</span></span>  

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

3. <span data-ttu-id="4ff40-119">Restart the omsagent daemon</span><span class="sxs-lookup"><span data-stu-id="4ff40-119">Restart the omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="4ff40-120">Configuring Zabbix alert collection</span><span class="sxs-lookup"><span data-stu-id="4ff40-120">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="4ff40-121">To collect alerts from a Zabbix server, you need to specify a user and password in *clear text*.</span><span class="sxs-lookup"><span data-stu-id="4ff40-121">To collect alerts from a Zabbix server, you need to specify a user and password in *clear text*.</span></span>  <span data-ttu-id="4ff40-122">While not ideal, we recommend that you create a Zabbix user with read-only permissions to catch relevant alarms.</span><span class="sxs-lookup"><span data-stu-id="4ff40-122">While not ideal, we recommend that you create a Zabbix user with read-only permissions to catch relevant alarms.</span></span>

<span data-ttu-id="4ff40-123">To collect alerts on the Nagios server, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="4ff40-123">To collect alerts on the Nagios server, perform the following steps.</span></span>

1. <span data-ttu-id="4ff40-124">Modify the configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`.</span><span class="sxs-lookup"><span data-stu-id="4ff40-124">Modify the configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`.</span></span> <span data-ttu-id="4ff40-125">Ensure the following entries are present and not commented out.  Change the user name and password to values for your Zabbix environment.</span><span class="sxs-lookup"><span data-stu-id="4ff40-125">Ensure the following entries are present and not commented out.  Change the user name and password to values for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="4ff40-126">Restart the omsagent daemon</span><span class="sxs-lookup"><span data-stu-id="4ff40-126">Restart the omsagent daemon</span></span>

    `sudo sh /opt/microsoft/omsagent/bin/service_control restart`


## <a name="alert-records"></a><span data-ttu-id="4ff40-127">Alert records</span><span class="sxs-lookup"><span data-stu-id="4ff40-127">Alert records</span></span>
<span data-ttu-id="4ff40-128">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4ff40-128">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="4ff40-129">Nagios Alert records</span><span class="sxs-lookup"><span data-stu-id="4ff40-129">Nagios Alert records</span></span>

<span data-ttu-id="4ff40-130">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="4ff40-130">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="4ff40-131">They have the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="4ff40-131">They have the properties in the following table.</span></span>

| <span data-ttu-id="4ff40-132">Property</span><span class="sxs-lookup"><span data-stu-id="4ff40-132">Property</span></span> | <span data-ttu-id="4ff40-133">Description</span><span class="sxs-lookup"><span data-stu-id="4ff40-133">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ff40-134">Type</span><span class="sxs-lookup"><span data-stu-id="4ff40-134">Type</span></span> |<span data-ttu-id="4ff40-135">*Alert*</span><span class="sxs-lookup"><span data-stu-id="4ff40-135">*Alert*</span></span> |
| <span data-ttu-id="4ff40-136">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="4ff40-136">SourceSystem</span></span> |<span data-ttu-id="4ff40-137">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="4ff40-137">*Nagios*</span></span> |
| <span data-ttu-id="4ff40-138">AlertName</span><span class="sxs-lookup"><span data-stu-id="4ff40-138">AlertName</span></span> |<span data-ttu-id="4ff40-139">Name of the alert.</span><span class="sxs-lookup"><span data-stu-id="4ff40-139">Name of the alert.</span></span> |
| <span data-ttu-id="4ff40-140">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="4ff40-140">AlertDescription</span></span> | <span data-ttu-id="4ff40-141">Description of the alert.</span><span class="sxs-lookup"><span data-stu-id="4ff40-141">Description of the alert.</span></span> |
| <span data-ttu-id="4ff40-142">AlertState</span><span class="sxs-lookup"><span data-stu-id="4ff40-142">AlertState</span></span> | <span data-ttu-id="4ff40-143">Status of the service or host.</span><span class="sxs-lookup"><span data-stu-id="4ff40-143">Status of the service or host.</span></span><br><br><span data-ttu-id="4ff40-144">OK</span><span class="sxs-lookup"><span data-stu-id="4ff40-144">OK</span></span><br><span data-ttu-id="4ff40-145">WARNING</span><span class="sxs-lookup"><span data-stu-id="4ff40-145">WARNING</span></span><br><span data-ttu-id="4ff40-146">UP</span><span class="sxs-lookup"><span data-stu-id="4ff40-146">UP</span></span><br><span data-ttu-id="4ff40-147">DOWN</span><span class="sxs-lookup"><span data-stu-id="4ff40-147">DOWN</span></span> |
| <span data-ttu-id="4ff40-148">HostName</span><span class="sxs-lookup"><span data-stu-id="4ff40-148">HostName</span></span> | <span data-ttu-id="4ff40-149">Name of the host that created the alert.</span><span class="sxs-lookup"><span data-stu-id="4ff40-149">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="4ff40-150">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="4ff40-150">PriorityNumber</span></span> | <span data-ttu-id="4ff40-151">Priority level of the alert.</span><span class="sxs-lookup"><span data-stu-id="4ff40-151">Priority level of the alert.</span></span> |
| <span data-ttu-id="4ff40-152">StateType</span><span class="sxs-lookup"><span data-stu-id="4ff40-152">StateType</span></span> | <span data-ttu-id="4ff40-153">The type of state of the alert.</span><span class="sxs-lookup"><span data-stu-id="4ff40-153">The type of state of the alert.</span></span><br><br><span data-ttu-id="4ff40-154">SOFT - Issue that has not been rechecked.</span><span class="sxs-lookup"><span data-stu-id="4ff40-154">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="4ff40-155">HARD - Issue that has been rechecked a specified number of times.</span><span class="sxs-lookup"><span data-stu-id="4ff40-155">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="4ff40-156">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="4ff40-156">TimeGenerated</span></span> |<span data-ttu-id="4ff40-157">Date and time the alert was created.</span><span class="sxs-lookup"><span data-stu-id="4ff40-157">Date and time the alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="4ff40-158">Zabbix alert records</span><span class="sxs-lookup"><span data-stu-id="4ff40-158">Zabbix alert records</span></span>
<span data-ttu-id="4ff40-159">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="4ff40-159">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="4ff40-160">They have the properties in the following table.</span><span class="sxs-lookup"><span data-stu-id="4ff40-160">They have the properties in the following table.</span></span>

| <span data-ttu-id="4ff40-161">Property</span><span class="sxs-lookup"><span data-stu-id="4ff40-161">Property</span></span> | <span data-ttu-id="4ff40-162">Description</span><span class="sxs-lookup"><span data-stu-id="4ff40-162">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ff40-163">Type</span><span class="sxs-lookup"><span data-stu-id="4ff40-163">Type</span></span> |<span data-ttu-id="4ff40-164">*Alert*</span><span class="sxs-lookup"><span data-stu-id="4ff40-164">*Alert*</span></span> |
| <span data-ttu-id="4ff40-165">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="4ff40-165">SourceSystem</span></span> |<span data-ttu-id="4ff40-166">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="4ff40-166">*Zabbix*</span></span> |
| <span data-ttu-id="4ff40-167">AlertName</span><span class="sxs-lookup"><span data-stu-id="4ff40-167">AlertName</span></span> | <span data-ttu-id="4ff40-168">Name of the alert.</span><span class="sxs-lookup"><span data-stu-id="4ff40-168">Name of the alert.</span></span> |
| <span data-ttu-id="4ff40-169">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="4ff40-169">AlertPriority</span></span> | <span data-ttu-id="4ff40-170">Severity of the alert.</span><span class="sxs-lookup"><span data-stu-id="4ff40-170">Severity of the alert.</span></span><br><br><span data-ttu-id="4ff40-171">not classified</span><span class="sxs-lookup"><span data-stu-id="4ff40-171">not classified</span></span><br><span data-ttu-id="4ff40-172">information</span><span class="sxs-lookup"><span data-stu-id="4ff40-172">information</span></span><br><span data-ttu-id="4ff40-173">warning</span><span class="sxs-lookup"><span data-stu-id="4ff40-173">warning</span></span><br><span data-ttu-id="4ff40-174">average</span><span class="sxs-lookup"><span data-stu-id="4ff40-174">average</span></span><br><span data-ttu-id="4ff40-175">high</span><span class="sxs-lookup"><span data-stu-id="4ff40-175">high</span></span><br><span data-ttu-id="4ff40-176">disaster</span><span class="sxs-lookup"><span data-stu-id="4ff40-176">disaster</span></span>  |
| <span data-ttu-id="4ff40-177">AlertState</span><span class="sxs-lookup"><span data-stu-id="4ff40-177">AlertState</span></span> | <span data-ttu-id="4ff40-178">State of the alert.</span><span class="sxs-lookup"><span data-stu-id="4ff40-178">State of the alert.</span></span><br><br><span data-ttu-id="4ff40-179">0 - State is up-to-date.</span><span class="sxs-lookup"><span data-stu-id="4ff40-179">0 - State is up-to-date.</span></span><br><span data-ttu-id="4ff40-180">1 - State is unknown.</span><span class="sxs-lookup"><span data-stu-id="4ff40-180">1 - State is unknown.</span></span>  |
| <span data-ttu-id="4ff40-181">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="4ff40-181">AlertTypeNumber</span></span> | <span data-ttu-id="4ff40-182">Specifies whether alert can generate multiple problem events.</span><span class="sxs-lookup"><span data-stu-id="4ff40-182">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="4ff40-183">0 - State is up-to-date.</span><span class="sxs-lookup"><span data-stu-id="4ff40-183">0 - State is up-to-date.</span></span><br><span data-ttu-id="4ff40-184">1 - State is unknown.</span><span class="sxs-lookup"><span data-stu-id="4ff40-184">1 - State is unknown.</span></span>    |
| <span data-ttu-id="4ff40-185">Comments</span><span class="sxs-lookup"><span data-stu-id="4ff40-185">Comments</span></span> | <span data-ttu-id="4ff40-186">Additional comments for alert.</span><span class="sxs-lookup"><span data-stu-id="4ff40-186">Additional comments for alert.</span></span> |
| <span data-ttu-id="4ff40-187">HostName</span><span class="sxs-lookup"><span data-stu-id="4ff40-187">HostName</span></span> | <span data-ttu-id="4ff40-188">Name of the host that created the alert.</span><span class="sxs-lookup"><span data-stu-id="4ff40-188">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="4ff40-189">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="4ff40-189">PriorityNumber</span></span> | <span data-ttu-id="4ff40-190">Value indicating severity of the alert.</span><span class="sxs-lookup"><span data-stu-id="4ff40-190">Value indicating severity of the alert.</span></span><br><br><span data-ttu-id="4ff40-191">0 - not classified</span><span class="sxs-lookup"><span data-stu-id="4ff40-191">0 - not classified</span></span><br><span data-ttu-id="4ff40-192">1 - information</span><span class="sxs-lookup"><span data-stu-id="4ff40-192">1 - information</span></span><br><span data-ttu-id="4ff40-193">2 - warning</span><span class="sxs-lookup"><span data-stu-id="4ff40-193">2 - warning</span></span><br><span data-ttu-id="4ff40-194">3 - average</span><span class="sxs-lookup"><span data-stu-id="4ff40-194">3 - average</span></span><br><span data-ttu-id="4ff40-195">4 - high</span><span class="sxs-lookup"><span data-stu-id="4ff40-195">4 - high</span></span><br><span data-ttu-id="4ff40-196">5 - disaster</span><span class="sxs-lookup"><span data-stu-id="4ff40-196">5 - disaster</span></span> |
| <span data-ttu-id="4ff40-197">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="4ff40-197">TimeGenerated</span></span> |<span data-ttu-id="4ff40-198">Date and time the alert was created.</span><span class="sxs-lookup"><span data-stu-id="4ff40-198">Date and time the alert was created.</span></span> |
| <span data-ttu-id="4ff40-199">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="4ff40-199">TimeLastModified</span></span> |<span data-ttu-id="4ff40-200">Date and time the state of the alert was last changed.</span><span class="sxs-lookup"><span data-stu-id="4ff40-200">Date and time the state of the alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="4ff40-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ff40-201">Next steps</span></span>
* <span data-ttu-id="4ff40-202">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4ff40-202">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="4ff40-203">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span><span class="sxs-lookup"><span data-stu-id="4ff40-203">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
