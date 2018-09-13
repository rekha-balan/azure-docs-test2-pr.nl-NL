---
title: Collect data from CollectD in OMS Log Analytics | Microsoft Docs
description: CollectD is an open source Linux daemon that periodically collects data from applications and system level information.  This article provides information on collecting data from CollectD in Log Analytics.
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
ms.date: 05/02/2017
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 59b6f8b82d0f714d4526147b42f68e14bf0aa2bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966440"
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="5114b-104">Collect data from CollectD on Linux agents in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5114b-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="5114b-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span><span class="sxs-lookup"><span data-stu-id="5114b-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="5114b-106">Example applications include the Java Virtual Machine (JVM), MySQL Server, and Nginx.</span><span class="sxs-lookup"><span data-stu-id="5114b-106">Example applications include the Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="5114b-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="5114b-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="5114b-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="5114b-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![CollectD overview](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="5114b-110">The following CollectD configuration is included in the OMS Agent for Linux to route  CollectD data to the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="5114b-110">The following CollectD configuration is included in the OMS Agent for Linux to route  CollectD data to the OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="5114b-111">Additionally, if using an versions of collectD before 5.5 use the following configuration instead.</span><span class="sxs-lookup"><span data-stu-id="5114b-111">Additionally, if using an versions of collectD before 5.5 use the following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="5114b-112">The CollectD configuration uses the default`write_http` plugin to send performance metric data over port 26000 to OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="5114b-112">The CollectD configuration uses the default`write_http` plugin to send performance metric data over port 26000 to OMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="5114b-113">This port can be configured to a custom-defined port if needed.</span><span class="sxs-lookup"><span data-stu-id="5114b-113">This port can be configured to a custom-defined port if needed.</span></span>

<span data-ttu-id="5114b-114">The OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them to OMS schema metrics.</span><span class="sxs-lookup"><span data-stu-id="5114b-114">The OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them to OMS schema metrics.</span></span> <span data-ttu-id="5114b-115">The following is the OMS Agent for Linux configuration  `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="5114b-115">The following is the OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="5114b-116">Versions supported</span><span class="sxs-lookup"><span data-stu-id="5114b-116">Versions supported</span></span>
- <span data-ttu-id="5114b-117">Log Analytics currently supports CollectD version 4.8 and above.</span><span class="sxs-lookup"><span data-stu-id="5114b-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="5114b-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span><span class="sxs-lookup"><span data-stu-id="5114b-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="5114b-119">Configuration</span><span class="sxs-lookup"><span data-stu-id="5114b-119">Configuration</span></span>
<span data-ttu-id="5114b-120">The following are basic steps to configure collection of CollectD data in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="5114b-120">The following are basic steps to configure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="5114b-121">Configure CollectD to send data to the OMS Agent for Linux using the write_http plugin.</span><span class="sxs-lookup"><span data-stu-id="5114b-121">Configure CollectD to send data to the OMS Agent for Linux using the write_http plugin.</span></span>  
2. <span data-ttu-id="5114b-122">Configure the OMS Agent for Linux to listen for the CollectD data on the appropriate port.</span><span class="sxs-lookup"><span data-stu-id="5114b-122">Configure the OMS Agent for Linux to listen for the CollectD data on the appropriate port.</span></span>
3. <span data-ttu-id="5114b-123">Restart CollectD and OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="5114b-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-to-forward-data"></a><span data-ttu-id="5114b-124">Configure CollectD to forward data</span><span class="sxs-lookup"><span data-stu-id="5114b-124">Configure CollectD to forward data</span></span> 

1. <span data-ttu-id="5114b-125">To route CollectD data to the OMS Agent for Linux, `oms.conf` needs to be added to CollectD's configuration directory.</span><span class="sxs-lookup"><span data-stu-id="5114b-125">To route CollectD data to the OMS Agent for Linux, `oms.conf` needs to be added to CollectD's configuration directory.</span></span> <span data-ttu-id="5114b-126">The destination of this file depends on the Linux  distro of your machine.</span><span class="sxs-lookup"><span data-stu-id="5114b-126">The destination of this file depends on the Linux  distro of your machine.</span></span>

    <span data-ttu-id="5114b-127">If your CollectD config directory is located in /etc/collectd.d/:</span><span class="sxs-lookup"><span data-stu-id="5114b-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="5114b-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span><span class="sxs-lookup"><span data-stu-id="5114b-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="5114b-129">For CollectD versions before 5.5 you will have to modify the tags in `oms.conf` as shown above.</span><span class="sxs-lookup"><span data-stu-id="5114b-129">For CollectD versions before 5.5 you will have to modify the tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="5114b-130">Copy collectd.conf to the desired workspace's omsagent configuration directory.</span><span class="sxs-lookup"><span data-stu-id="5114b-130">Copy collectd.conf to the desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="5114b-131">Restart CollectD and OMS Agent for Linux with the following commands.</span><span class="sxs-lookup"><span data-stu-id="5114b-131">Restart CollectD and OMS Agent for Linux with the following commands.</span></span>

    <span data-ttu-id="5114b-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="5114b-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-to-log-analytics-schema-conversion"></a><span data-ttu-id="5114b-133">CollectD metrics to Log Analytics schema conversion</span><span class="sxs-lookup"><span data-stu-id="5114b-133">CollectD metrics to Log Analytics schema conversion</span></span>
<span data-ttu-id="5114b-134">To maintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and the new metrics collected by CollectD the following schema mapping is used:</span><span class="sxs-lookup"><span data-stu-id="5114b-134">To maintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and the new metrics collected by CollectD the following schema mapping is used:</span></span>

| <span data-ttu-id="5114b-135">CollectD Metric field</span><span class="sxs-lookup"><span data-stu-id="5114b-135">CollectD Metric field</span></span> | <span data-ttu-id="5114b-136">Log Analytics field</span><span class="sxs-lookup"><span data-stu-id="5114b-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="5114b-137">host</span><span class="sxs-lookup"><span data-stu-id="5114b-137">host</span></span> | <span data-ttu-id="5114b-138">Computer</span><span class="sxs-lookup"><span data-stu-id="5114b-138">Computer</span></span> |
| <span data-ttu-id="5114b-139">plugin</span><span class="sxs-lookup"><span data-stu-id="5114b-139">plugin</span></span> | <span data-ttu-id="5114b-140">None</span><span class="sxs-lookup"><span data-stu-id="5114b-140">None</span></span> |
| <span data-ttu-id="5114b-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="5114b-141">plugin_instance</span></span> | <span data-ttu-id="5114b-142">Instance Name</span><span class="sxs-lookup"><span data-stu-id="5114b-142">Instance Name</span></span><br><span data-ttu-id="5114b-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="5114b-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="5114b-144">type</span><span class="sxs-lookup"><span data-stu-id="5114b-144">type</span></span> | <span data-ttu-id="5114b-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="5114b-145">ObjectName</span></span> |
| <span data-ttu-id="5114b-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="5114b-146">type_instance</span></span> | <span data-ttu-id="5114b-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="5114b-147">CounterName</span></span><br><span data-ttu-id="5114b-148">If **type_instance** is *null* then CounterName=**blank**</span><span class="sxs-lookup"><span data-stu-id="5114b-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="5114b-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="5114b-149">dsnames[]</span></span> | <span data-ttu-id="5114b-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="5114b-150">CounterName</span></span> |
| <span data-ttu-id="5114b-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="5114b-151">dstypes</span></span> | <span data-ttu-id="5114b-152">None</span><span class="sxs-lookup"><span data-stu-id="5114b-152">None</span></span> |
| <span data-ttu-id="5114b-153">values[]</span><span class="sxs-lookup"><span data-stu-id="5114b-153">values[]</span></span> | <span data-ttu-id="5114b-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="5114b-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5114b-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="5114b-155">Next steps</span></span>
* <span data-ttu-id="5114b-156">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span><span class="sxs-lookup"><span data-stu-id="5114b-156">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="5114b-157">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span><span class="sxs-lookup"><span data-stu-id="5114b-157">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>

