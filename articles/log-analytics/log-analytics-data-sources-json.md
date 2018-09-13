---
title: Collecting custom JSON data in OMS Log Analytics | Microsoft Docs
description: Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.  These custom data sources can be simple scripts returning JSON such as curl or one of FluentD's 300+ plugins. This article describes the configuration required for this data collection.
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
ms.date: 05/04/2017
ms.author: magoedte
ms.component: na
ms.openlocfilehash: d3c8807b7624e68ff55557922f97d51e24fc2c19
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864797"
---
# <a name="collecting-custom-json-data-sources-with-the-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="bf738-105">Collecting custom JSON data sources with the OMS Agent for Linux in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="bf738-105">Collecting custom JSON data sources with the OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="bf738-106">Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="bf738-106">Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.</span></span>  <span data-ttu-id="bf738-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="bf738-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="bf738-108">This article describes the configuration required for this data collection.</span><span class="sxs-lookup"><span data-stu-id="bf738-108">This article describes the configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="bf738-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span><span class="sxs-lookup"><span data-stu-id="bf738-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="bf738-110">Configuration</span><span class="sxs-lookup"><span data-stu-id="bf738-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="bf738-111">Configure input plugin</span><span class="sxs-lookup"><span data-stu-id="bf738-111">Configure input plugin</span></span>

<span data-ttu-id="bf738-112">To collect JSON data in Log Analytics, add `oms.api.` to the start of a FluentD tag in an input plugin.</span><span class="sxs-lookup"><span data-stu-id="bf738-112">To collect JSON data in Log Analytics, add `oms.api.` to the start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="bf738-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="bf738-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="bf738-114">This uses the FluentD plugin `exec` to run a curl command every 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="bf738-114">This uses the FluentD plugin `exec` to run a curl command every 30 seconds.</span></span>  <span data-ttu-id="bf738-115">The output from this command is collected by the JSON output plugin.</span><span class="sxs-lookup"><span data-stu-id="bf738-115">The output from this command is collected by the JSON output plugin.</span></span>

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
<span data-ttu-id="bf738-116">The configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require to have its ownership changed with the following command.</span><span class="sxs-lookup"><span data-stu-id="bf738-116">The configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require to have its ownership changed with the following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="bf738-117">Configure output plugin</span><span class="sxs-lookup"><span data-stu-id="bf738-117">Configure output plugin</span></span> 
<span data-ttu-id="bf738-118">Add the following output plugin configuration to the main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="bf738-118">Add the following output plugin configuration to the main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="bf738-119">Restart OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="bf738-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="bf738-120">Restart the OMS Agent for Linux service with the following command.</span><span class="sxs-lookup"><span data-stu-id="bf738-120">Restart the OMS Agent for Linux service with the following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="bf738-121">Output</span><span class="sxs-lookup"><span data-stu-id="bf738-121">Output</span></span>
<span data-ttu-id="bf738-122">The data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="bf738-122">The data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="bf738-123">For example, the custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="bf738-123">For example, the custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="bf738-124">You could retrieve all records of this type with the following log search.</span><span class="sxs-lookup"><span data-stu-id="bf738-124">You could retrieve all records of this type with the following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="bf738-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span><span class="sxs-lookup"><span data-stu-id="bf738-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="bf738-126">For example, the following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="bf738-126">For example, the following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="bf738-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="bf738-127">Next steps</span></span>
* <span data-ttu-id="bf738-128">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span><span class="sxs-lookup"><span data-stu-id="bf738-128">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
 