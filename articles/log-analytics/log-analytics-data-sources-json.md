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
# <a name="collecting-custom-json-data-sources-with-the-oms-agent-for-linux-in-log-analytics"></a>Collecting custom JSON data sources with the OMS Agent for Linux in Log Analytics
Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.  These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all). This article describes the configuration required for this data collection.

> [!NOTE]
> OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data

## <a name="configuration"></a>Configuration

### <a name="configure-input-plugin"></a>Configure input plugin

To collect JSON data in Log Analytics, add `oms.api.` to the start of a FluentD tag in an input plugin.

For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.  This uses the FluentD plugin `exec` to run a curl command every 30 seconds.  The output from this command is collected by the JSON output plugin.

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
The configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require to have its ownership changed with the following command.

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>Configure output plugin 
Add the following output plugin configuration to the main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

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

### <a name="restart-oms-agent-for-linux"></a>Restart OMS Agent for Linux
Restart the OMS Agent for Linux service with the following command.

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>Output
The data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.

For example, the custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.  You could retrieve all records of this type with the following log search.

    Type=tomcat_CL

Nested JSON data sources are supported, but are indexed based off of parent field. For example, the following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>Next steps
* Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions. 
 