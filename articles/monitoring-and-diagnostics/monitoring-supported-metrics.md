---
title: Azure Monitor metrics - supported metrics per resource type  | Microsoft Docs
description: List of metrics available for each resource type with Azure Monitor.
author: johnkemnetz
manager: rboucher
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/17/2017
ms.author: johnkem
ms.openlocfilehash: deda64fb779e176bb00c3256fa3028e7e3567eb4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549151"
---
# <a name="supported-metrics-with-azure-monitor"></a>Supported metrics with Azure Monitor
Azure Monitor provides several ways to interact with metrics, including charting them in the portal, accessing them through the REST API, or querying them using PowerShell or CLI. Below is a complete list of all metrics currently available with Azure Monitor's metric pipeline.

> [!NOTE]
> Other metrics may be available in the portal or using legacy APIs. This list only includes public preview metrics available using the public preview of the consolidated Azure Monitor metric pipeline.
> 
> 

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|qpu_metric|QPU|Count|Average|QPU. Range 0-100 for S1, 0-200 for S2 and 0-400 for S4|
|memory_metric|Memory|Bytes|Average|Memory. Range 0-25 GB for S1, 0-50 GB for S2 and 0-100 GB for S4|
|TotalConnectionRequests|Total Connection Requests|Count|Average|Total connection requests. These are arrivals.|
|SuccessfullConnectionsPerSec|Successful Connections Per Sec|CountPerSecond|Average|Rate of successful connection completions.|
|TotalConnectionFailures|Total Connection Failures|Count|Average|Total failed connection attempts.|
|CurrentUserSessions|Current User Sessions|Count|Average|Current number of user sessions established.|
|QueryPoolBusyThreads|Query Pool Busy Threads|Count|Average|Number of busy threads in the query thread pool.|
|CommandPoolJobQueueLength|Command Pool Job Queue Length|Count|Average|Number of jobs in the queue of the command thread pool.|
|ProcessingPoolJobQueueLength|Processing Pool Job Queue Length|Count|Average|Number of non-I/O jobs in the queue of the processing thread pool.|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|TotalRequests|Total Gateway Requests|Count|Total|Number of gateway requests|
|SuccessfulRequests|Successful Gateway Requests|Count|Total|Number of successful gateway requests|
|UnauthorizedRequests|Unauthorized Gateway Requests|Count|Total|Number of unauthorized gateway requests|
|FailedRequests|Failed Gateway Requests|Count|Total|Number of failures in gateway requests|
|OtherRequests|Other Gateway Requests|Count|Total|Number of other gateway requests|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|CoreCount|Core Count|Count|Total|Total number of cores in the batch account|
|TotalNodeCount|Node Count|Count|Total|Total number of nodes in the batch account|
|CreatingNodeCount|Creating Node Count|Count|Total|Number of nodes being created|
|StartingNodeCount|Starting Node Count|Count|Total|Number of nodes starting|
|WaitingForStartTaskNodeCount|Waiting For Start Task Node Count|Count|Total|Number of nodes waiting for the Start Task to complete|
|StartTaskFailedNodeCount|Start Task Failed Node Count|Count|Total|Number of nodes where the Start Task has failed|
|IdleNodeCount|Idle Node Count|Count|Total|Number of idle nodes|
|OfflineNodeCount|Offline Node Count|Count|Total|Number of offline nodes|
|RebootingNodeCount|Rebooting Node Count|Count|Total|Number of rebooting nodes|
|ReimagingNodeCount|Reimaging Node Count|Count|Total|Number of reimaging nodes|
|RunningNodeCount|Running Node Count|Count|Total|Number of running nodes|
|LeavingPoolNodeCount|Leaving Pool Node Count|Count|Total|Number of nodes leaving the Pool|
|UnusableNodeCount|Unusable Node Count|Count|Total|Number of unusable nodes|
|TaskStartEvent|Task Start Events|Count|Total|Total number of tasks that have started|
|TaskCompleteEvent|Task Complete Events|Count|Total|Total number of tasks that have completed|
|TaskFailEvent|Task Fail Events|Count|Total|Total number of tasks that have completed in a failed state|
|PoolCreateEvent|Pool Create Events|Count|Total|Total number of pools that have been created|
|PoolResizeStartEvent|Pool Resize Start Events|Count|Total|Total number of pool resizes that have started|
|PoolResizeCompleteEvent|Pool Resize Complete Events|Count|Total|Total number of pool resizes that have completed|
|PoolDeleteStartEvent|Pool Delete Start Events|Count|Total|Total number of pool deletes that have started|
|PoolDeleteCompleteEvent|Pool Delete Complete Events|Count|Total|Total number of pool deletes that have completed|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|connectedclients|Connected Clients|Count|Maximum||
|totalcommandsprocessed|Total Operations|Count|Total||
|cachehits|Cache Hits|Count|Total||
|cachemisses|Cache Misses|Count|Total||
|getcommands|Gets|Count|Total||
|setcommands|Sets|Count|Total||
|evictedkeys|Evicted Keys|Count|Total||
|totalkeys|Total Keys|Count|Maximum||
|expiredkeys|Expired Keys|Count|Total||
|usedmemory|Used Memory|Bytes|Maximum||
|usedmemoryRss|Used Memory RSS|Bytes|Maximum||
|serverLoad|Server Load|Percent|Maximum||
|cacheWrite|Cache Write|BytesPerSecond|Maximum||
|cacheRead|Cache Read|BytesPerSecond|Maximum||
|percentProcessorTime|CPU|Percent|Maximum||
|connectedclients0|Connected Clients (Shard 0)|Count|Maximum||
|totalcommandsprocessed0|Total Operations (Shard 0)|Count|Total||
|cachehits0|Cache Hits (Shard 0)|Count|Total||
|cachemisses0|Cache Misses (Shard 0)|Count|Total||
|getcommands0|Gets (Shard 0)|Count|Total||
|setcommands0|Sets (Shard 0)|Count|Total||
|evictedkeys0|Evicted Keys (Shard 0)|Count|Total||
|totalkeys0|Total Keys (Shard 0)|Count|Maximum||
|expiredkeys0|Expired Keys (Shard 0)|Count|Total||
|usedmemory0|Used Memory (Shard 0)|Bytes|Maximum||
|usedmemoryRss0|Used Memory RSS (Shard 0)|Bytes|Maximum||
|serverLoad0|Server Load (Shard 0)|Percent|Maximum||
|cacheWrite0|Cache Write (Shard 0)|BytesPerSecond|Maximum||
|cacheRead0|Cache Read (Shard 0)|BytesPerSecond|Maximum||
|percentProcessorTime0|CPU (Shard 0)|Percent|Maximum||
|connectedclients1|Connected Clients (Shard 1)|Count|Maximum||
|totalcommandsprocessed1|Total Operations (Shard 1)|Count|Total||
|cachehits1|Cache Hits (Shard 1)|Count|Total||
|cachemisses1|Cache Misses (Shard 1)|Count|Total||
|getcommands1|Gets (Shard 1)|Count|Total||
|setcommands1|Sets (Shard 1)|Count|Total||
|evictedkeys1|Evicted Keys (Shard 1)|Count|Total||
|totalkeys1|Total Keys (Shard 1)|Count|Maximum||
|expiredkeys1|Expired Keys (Shard 1)|Count|Total||
|usedmemory1|Used Memory (Shard 1)|Bytes|Maximum||
|usedmemoryRss1|Used Memory RSS (Shard 1)|Bytes|Maximum||
|serverLoad1|Server Load (Shard 1)|Percent|Maximum||
|cacheWrite1|Cache Write (Shard 1)|BytesPerSecond|Maximum||
|cacheRead1|Cache Read (Shard 1)|BytesPerSecond|Maximum||
|percentProcessorTime1|CPU (Shard 1)|Percent|Maximum||
|connectedclients2|Connected Clients (Shard 2)|Count|Maximum||
|totalcommandsprocessed2|Total Operations (Shard 2)|Count|Total||
|cachehits2|Cache Hits (Shard 2)|Count|Total||
|cachemisses2|Cache Misses (Shard 2)|Count|Total||
|getcommands2|Gets (Shard 2)|Count|Total||
|setcommands2|Sets (Shard 2)|Count|Total||
|evictedkeys2|Evicted Keys (Shard 2)|Count|Total||
|totalkeys2|Total Keys (Shard 2)|Count|Maximum||
|expiredkeys2|Expired Keys (Shard 2)|Count|Total||
|usedmemory2|Used Memory (Shard 2)|Bytes|Maximum||
|usedmemoryRss2|Used Memory RSS (Shard 2)|Bytes|Maximum||
|serverLoad2|Server Load (Shard 2)|Percent|Maximum||
|cacheWrite2|Cache Write (Shard 2)|BytesPerSecond|Maximum||
|cacheRead2|Cache Read (Shard 2)|BytesPerSecond|Maximum||
|percentProcessorTime2|CPU (Shard 2)|Percent|Maximum||
|connectedclients3|Connected Clients (Shard 3)|Count|Maximum||
|totalcommandsprocessed3|Total Operations (Shard 3)|Count|Total||
|cachehits3|Cache Hits (Shard 3)|Count|Total||
|cachemisses3|Cache Misses (Shard 3)|Count|Total||
|getcommands3|Gets (Shard 3)|Count|Total||
|setcommands3|Sets (Shard 3)|Count|Total||
|evictedkeys3|Evicted Keys (Shard 3)|Count|Total||
|totalkeys3|Total Keys (Shard 3)|Count|Maximum||
|expiredkeys3|Expired Keys (Shard 3)|Count|Total||
|usedmemory3|Used Memory (Shard 3)|Bytes|Maximum||
|usedmemoryRss3|Used Memory RSS (Shard 3)|Bytes|Maximum||
|serverLoad3|Server Load (Shard 3)|Percent|Maximum||
|cacheWrite3|Cache Write (Shard 3)|BytesPerSecond|Maximum||
|cacheRead3|Cache Read (Shard 3)|BytesPerSecond|Maximum||
|percentProcessorTime3|CPU (Shard 3)|Percent|Maximum||
|connectedclients4|Connected Clients (Shard 4)|Count|Maximum||
|totalcommandsprocessed4|Total Operations (Shard 4)|Count|Total||
|cachehits4|Cache Hits (Shard 4)|Count|Total||
|cachemisses4|Cache Misses (Shard 4)|Count|Total||
|getcommands4|Gets (Shard 4)|Count|Total||
|setcommands4|Sets (Shard 4)|Count|Total||
|evictedkeys4|Evicted Keys (Shard 4)|Count|Total||
|totalkeys4|Total Keys (Shard 4)|Count|Maximum||
|expiredkeys4|Expired Keys (Shard 4)|Count|Total||
|usedmemory4|Used Memory (Shard 4)|Bytes|Maximum||
|usedmemoryRss4|Used Memory RSS (Shard 4)|Bytes|Maximum||
|serverLoad4|Server Load (Shard 4)|Percent|Maximum||
|cacheWrite4|Cache Write (Shard 4)|BytesPerSecond|Maximum||
|cacheRead4|Cache Read (Shard 4)|BytesPerSecond|Maximum||
|percentProcessorTime4|CPU (Shard 4)|Percent|Maximum||
|connectedclients5|Connected Clients (Shard 5)|Count|Maximum||
|totalcommandsprocessed5|Total Operations (Shard 5)|Count|Total||
|cachehits5|Cache Hits (Shard 5)|Count|Total||
|cachemisses5|Cache Misses (Shard 5)|Count|Total||
|getcommands5|Gets (Shard 5)|Count|Total||
|setcommands5|Sets (Shard 5)|Count|Total||
|evictedkeys5|Evicted Keys (Shard 5)|Count|Total||
|totalkeys5|Total Keys (Shard 5)|Count|Maximum||
|expiredkeys5|Expired Keys (Shard 5)|Count|Total||
|usedmemory5|Used Memory (Shard 5)|Bytes|Maximum||
|usedmemoryRss5|Used Memory RSS (Shard 5)|Bytes|Maximum||
|serverLoad5|Server Load (Shard 5)|Percent|Maximum||
|cacheWrite5|Cache Write (Shard 5)|BytesPerSecond|Maximum||
|cacheRead5|Cache Read (Shard 5)|BytesPerSecond|Maximum||
|percentProcessorTime5|CPU (Shard 5)|Percent|Maximum||
|connectedclients6|Connected Clients (Shard 6)|Count|Maximum||
|totalcommandsprocessed6|Total Operations (Shard 6)|Count|Total||
|cachehits6|Cache Hits (Shard 6)|Count|Total||
|cachemisses6|Cache Misses (Shard 6)|Count|Total||
|getcommands6|Gets (Shard 6)|Count|Total||
|setcommands6|Sets (Shard 6)|Count|Total||
|evictedkeys6|Evicted Keys (Shard 6)|Count|Total||
|totalkeys6|Total Keys (Shard 6)|Count|Maximum||
|expiredkeys6|Expired Keys (Shard 6)|Count|Total||
|usedmemory6|Used Memory (Shard 6)|Bytes|Maximum||
|usedmemoryRss6|Used Memory RSS (Shard 6)|Bytes|Maximum||
|serverLoad6|Server Load (Shard 6)|Percent|Maximum||
|cacheWrite6|Cache Write (Shard 6)|BytesPerSecond|Maximum||
|cacheRead6|Cache Read (Shard 6)|BytesPerSecond|Maximum||
|percentProcessorTime6|CPU (Shard 6)|Percent|Maximum||
|connectedclients7|Connected Clients (Shard 7)|Count|Maximum||
|totalcommandsprocessed7|Total Operations (Shard 7)|Count|Total||
|cachehits7|Cache Hits (Shard 7)|Count|Total||
|cachemisses7|Cache Misses (Shard 7)|Count|Total||
|getcommands7|Gets (Shard 7)|Count|Total||
|setcommands7|Sets (Shard 7)|Count|Total||
|evictedkeys7|Evicted Keys (Shard 7)|Count|Total||
|totalkeys7|Total Keys (Shard 7)|Count|Maximum||
|expiredkeys7|Expired Keys (Shard 7)|Count|Total||
|usedmemory7|Used Memory (Shard 7)|Bytes|Maximum||
|usedmemoryRss7|Used Memory RSS (Shard 7)|Bytes|Maximum||
|serverLoad7|Server Load (Shard 7)|Percent|Maximum||
|cacheWrite7|Cache Write (Shard 7)|BytesPerSecond|Maximum||
|cacheRead7|Cache Read (Shard 7)|BytesPerSecond|Maximum||
|percentProcessorTime7|CPU (Shard 7)|Percent|Maximum||
|connectedclients8|Connected Clients (Shard 8)|Count|Maximum||
|totalcommandsprocessed8|Total Operations (Shard 8)|Count|Total||
|cachehits8|Cache Hits (Shard 8)|Count|Total||
|cachemisses8|Cache Misses (Shard 8)|Count|Total||
|getcommands8|Gets (Shard 8)|Count|Total||
|setcommands8|Sets (Shard 8)|Count|Total||
|evictedkeys8|Evicted Keys (Shard 8)|Count|Total||
|totalkeys8|Total Keys (Shard 8)|Count|Maximum||
|expiredkeys8|Expired Keys (Shard 8)|Count|Total||
|usedmemory8|Used Memory (Shard 8)|Bytes|Maximum||
|usedmemoryRss8|Used Memory RSS (Shard 8)|Bytes|Maximum||
|serverLoad8|Server Load (Shard 8)|Percent|Maximum||
|cacheWrite8|Cache Write (Shard 8)|BytesPerSecond|Maximum||
|cacheRead8|Cache Read (Shard 8)|BytesPerSecond|Maximum||
|percentProcessorTime8|CPU (Shard 8)|Percent|Maximum||
|connectedclients9|Connected Clients (Shard 9)|Count|Maximum||
|totalcommandsprocessed9|Total Operations (Shard 9)|Count|Total||
|cachehits9|Cache Hits (Shard 9)|Count|Total||
|cachemisses9|Cache Misses (Shard 9)|Count|Total||
|getcommands9|Gets (Shard 9)|Count|Total||
|setcommands9|Sets (Shard 9)|Count|Total||
|evictedkeys9|Evicted Keys (Shard 9)|Count|Total||
|totalkeys9|Total Keys (Shard 9)|Count|Maximum||
|expiredkeys9|Expired Keys (Shard 9)|Count|Total||
|usedmemory9|Used Memory (Shard 9)|Bytes|Maximum||
|usedmemoryRss9|Used Memory RSS (Shard 9)|Bytes|Maximum||
|serverLoad9|Server Load (Shard 9)|Percent|Maximum||
|cacheWrite9|Cache Write (Shard 9)|BytesPerSecond|Maximum||
|cacheRead9|Cache Read (Shard 9)|BytesPerSecond|Maximum||
|percentProcessorTime9|CPU (Shard 9)|Percent|Maximum||

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|TotalCalls|Total Calls|Count|Total|Total number of calls.|
|SuccessfulCalls|Successful Calls|Count|Total|Number of successful calls.|
|TotalErrors|Total Errors|Count|Total|Total number of calls with error response (HTTP response code 4xx or 5xx).|
|BlockedCalls|Blocked Calls|Count|Total|Number of calls that exceeded rate or quota limit.|
|ServerErrors|Server Errors|Count|Total|Number of calls with service internal error (HTTP response code 5xx).|
|ClientErrors|Client Errors|Count|Total|Number of calls with client side error (HTTP response code 4xx).|
|DataIn|Data In|Bytes|Total|Size of incoming data in bytes.|
|DataOut|Data Out|Bytes|Total|Size of outgoing data in bytes.|
|Latency|Latency|MilliSeconds|Average|Latency in milliseconds.|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|Percentage CPU|Percentage CPU|Percent|Average|The percentage of allocated compute units that are currently in use by the Virtual Machine(s)|
|Network In|Network In|Bytes|Total|The number of bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic)|
|Network Out|Network Out|Bytes|Total|The number of bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic)|
|Disk Read Bytes|Disk Read Bytes|Bytes|Total|Total bytes read from disk during monitoring period|
|Disk Write Bytes|Disk Write Bytes|Bytes|Total|Total bytes written to disk during monitoring period|
|Disk Read Operations/Sec|Disk Read Operations/Sec|CountPerSecond|Average|Disk Read IOPS|
|Disk Write Operations/Sec|Disk Write Operations/Sec|CountPerSecond|Average|Disk Write IOPS|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|Percentage CPU|Percentage CPU|Percent|Average|The percentage of allocated compute units that are currently in use by the Virtual Machine(s)|
|Network In|Network In|Bytes|Total|The number of bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic)|
|Network Out|Network Out|Bytes|Total|The number of bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic)|
|Disk Read Bytes|Disk Read Bytes|Bytes|Total|Total bytes read from disk during monitoring period|
|Disk Write Bytes|Disk Write Bytes|Bytes|Total|Total bytes written to disk during monitoring period|
|Disk Read Operations/Sec|Disk Read Operations/Sec|CountPerSecond|Average|Disk Read IOPS|
|Disk Write Operations/Sec|Disk Write Operations/Sec|CountPerSecond|Average|Disk Write IOPS|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|Percentage CPU|Percentage CPU|Percent|Average|The percentage of allocated compute units that are currently in use by the Virtual Machine(s)|
|Network In|Network In|Bytes|Total|The number of bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic)|
|Network Out|Network Out|Bytes|Total|The number of bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic)|
|Disk Read Bytes|Disk Read Bytes|Bytes|Total|Total bytes read from disk during monitoring period|
|Disk Write Bytes|Disk Write Bytes|Bytes|Total|Total bytes written to disk during monitoring period|
|Disk Read Operations/Sec|Disk Read Operations/Sec|CountPerSecond|Average|Disk Read IOPS|
|Disk Write Operations/Sec|Disk Write Operations/Sec|CountPerSecond|Average|Disk Write IOPS|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Telemetry message send attempts|Count|Total|Number of device-to-cloud telemetry messages attempted to be sent to your IoT hub|
|d2c.telemetry.ingress.success|Telemetry messages sent|Count|Total|Number of device-to-cloud telemetry messages sent successfully to your IoT hub|
|c2d.commands.egress.complete.success|Commands completed|Count|Total|Number of cloud-to-device commands completed successfully by the device|
|c2d.commands.egress.abandon.success|Commands abandoned|Count|Total|Number of cloud-to-device commands abandoned by the device|
|c2d.commands.egress.reject.success|Commands rejected|Count|Total|Number of cloud-to-device commands rejected by the device|
|devices.totalDevices|Total devices|Count|Total|Number of devices registered to your IoT hub|
|devices.connectedDevices.allProtocol|Connected devices|Count|Total|Number of devices connected to your IoT hub|
|d2c.telemetry.egress.success|Telemetry messages delivered|Count|Total|Number of times messages were successfully written to endpoints (total)|
|d2c.telemetry.egress.dropped|Dropped messages|Count|Total|Number of messages dropped because they did not match any routes and the fallback route was disabled|
|d2c.telemetry.egress.orphaned|Orphaned messages|Count|Total|The count of messages not matching any routes including the fallback route|
|d2c.telemetry.egress.invalid|Invalid messages|Count|Total|The count of messages not delivered due to incompatibility with the endpoint|
|d2c.telemetry.egress.fallback|Messages matching fallback condition|Count|Total|Number of messages written to the fallback endpoint|
|d2c.endpoints.egress.eventHubs|Messages delivered to Event Hub endpoints|Count|Total|Number of times messages were successfully written to Event Hub endpoints|
|d2c.endpoints.latency.eventHubs|Message latency for Event Hub endpoints|Milliseconds|Average|The average latency between message ingress to the IoT hub and message ingress into an Event Hub endpoint, in milliseconds|
|d2c.endpoints.egress.serviceBusQueues|Messages delivered to Service Bus Queue endpoints|Count|Total|Number of times messages were successfully written to Service Bus Queue endpoints|
|d2c.endpoints.latency.serviceBusQueues|Message latency for Service Bus Queue endpoints|Milliseconds|Average|The average latency between message ingress to the IoT hub and message ingress into a Service Bus Queue endpoint, in milliseconds|
|d2c.endpoints.egress.serviceBusTopics|Messages delivered to Service Bus Topic endpoints|Count|Total|Number of times messages were successfully written to Service Bus Topic endpoints|
|d2c.endpoints.latency.serviceBusTopics|Message latency for Service Bus Topic endpoints|Milliseconds|Average|The average latency between message ingress to the IoT hub and message ingress into a Service Bus Topic endpoint, in milliseconds|
|d2c.endpoints.egress.builtIn.events|Messages delivered to the built-in endpoint (messages/events)|Count|Total|Number of times messages were successfully written to the built-in endpoint (messages/events)|
|d2c.endpoints.latency.builtIn.events|Message latency for the built-in endpoint (messages/events)|Milliseconds|Average|The average latency between message ingress to the IoT hub and message ingress into the built-in endpoint (messages/events), in milliseconds |
|d2c.twin.read.success|Successful twin reads from devices|Count|Total|The count of all successful device-initiated twin reads.|
|d2c.twin.read.failure|Failed twin reads from devices|Count|Total|The count of all failed device-initiated twin reads.|
|d2c.twin.read.size|Response size of twin reads from devices|Bytes|Average|The average, min, and max of all successful device-initiated twin reads.|
|d2c.twin.update.success|Successful twin updates from devices|Count|Total|The count of all successful device-initiated twin updates.|
|d2c.twin.update.failure|Failed twin updates from devices|Count|Total|The count of all failed device-initiated twin updates.|
|d2c.twin.update.size|Size of twin updates from devices|Bytes|Average|The average, min, and max size of all successful device-initiated twin updates.|
|c2d.methods.success|Successful direct method invocations|Count|Total|The count of all successful direct method calls.|
|c2d.methods.failure|Failed direct method invocations|Count|Total|The count of all failed direct method calls.|
|c2d.methods.requestSize|Request size of direct method invocations|Bytes|Average|The average, min, and max of all successful direct method requests.|
|c2d.methods.responseSize|Response size of direct method invocations|Bytes|Average|The average, min, and max of all successful direct method responses.|
|c2d.twin.read.success|Successful twin reads from back end|Count|Total|The count of all successful back-end-initiated twin reads.|
|c2d.twin.read.failure|Failed twin reads from back end|Count|Total|The count of all failed back-end-initiated twin reads.|
|c2d.twin.read.size|Response size of twin reads from back end|Bytes|Average|The average, min, and max of all successful back-end-initiated twin reads.|
|c2d.twin.update.success|Successful twin updates from back end|Count|Total|The count of all successful back-end-initiated twin updates.|
|c2d.twin.update.failure|Failed twin updates from back end|Count|Total|The count of all failed back-end-initiated twin updates.|
|c2d.twin.update.size|Size of twin updates from back end|Bytes|Average|The average, min, and max size of all successful back-end-initiated twin updates.|
|twinQueries.success|Successful twin queries|Count|Total|The count of all successful twin queries.|
|twinQueries.failure|Failed twin queries|Count|Total|The count of all failed twin queries.|
|twinQueries.resultSize|Twin queries result size|Bytes|Average|The average, min, and max of the result size of all successful twin queries.|
|jobs.createTwinUpdateJob.success|Successful creations of twin update jobs|Count|Total|The count of all successful creation of twin update jobs.|
|jobs.createTwinUpdateJob.failure|Failed creations of twin update jobs|Count|Total|The count of all failed creation of twin update jobs.|
|jobs.createDirectMethodJob.success|Successful creations of method invocation jobs|Count|Total|The count of all successful creation of direct method invocation jobs.|
|jobs.createDirectMethodJob.failure|Failed creations of method invocation jobs|Count|Total|The count of all failed creation of direct method invocation jobs.|
|jobs.listJobs.success|Successful calls to list jobs|Count|Total|The count of all successful calls to list jobs.|
|jobs.listJobs.failure|Failed calls to list jobs|Count|Total|The count of all failed calls to list jobs.|
|jobs.cancelJob.success|Successful job cancellations|Count|Total|The count of all successful calls to cancel a job.|
|jobs.cancelJob.failure|Failed job cancellations|Count|Total|The count of all failed calls to cancel a job.|
|jobs.queryJobs.success|Successful job queries|Count|Total|The count of all successful calls to query jobs.|
|jobs.queryJobs.failure|Failed job queries|Count|Total|The count of all failed calls to query jobs.|
|jobs.completed|Completed jobs|Count|Total|The count of all completed jobs.|
|jobs.failed|Failed jobs|Count|Total|The count of all failed jobs.|

## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|INREQS|Incoming Requests|Count|Total|Total incoming requests for a namespace|
|SUCCREQ|Successful Requests|Count|Total|Total successful requests for a namespace|
|FAILREQ|Failed Requests|Count|Total|Total failed requests for a namespace|
|SVRBSY|Server Busy Errors|Count|Total|Total server busy errors for a namespace|
|INTERR|Internal Server Errors|Count|Total|Total internal server errors for a namespace|
|MISCERR|Other Errors|Count|Total|Total failed requests for a namespace|
|INMSGS|Incoming Messages|Count|Total|Total incoming messages for a namespace|
|OUTMSGS|Outgoing Messages|Count|Total|Total outgoing messages for a namespace|
|EHINMBS|Incoming bytes|BytesPerSecond|Total|Event Hub incoming message throughput for a namespace|
|EHOUTMBS|Outgoing bytes|BytesPerSecond|Total|Total outgoing messages for a namespace|
|EHABL|Archive backlog messages|Count|Total|Event Hub archive messages in backlog for a namespace|
|EHAMSGS|Archive messages|Count|Total|Event Hub archived messages in a namespace|
|EHAMBS|Archive message throughput|BytesPerSecond|Total|Event Hub archived message throughput in a namespace|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|RunsStarted|Runs Started|Count|Total|Number of workflow runs started.|
|RunsCompleted|Runs Completed|Count|Total|Number of workflow runs completed.|
|RunsSucceeded|Runs Succeeded|Count|Total|Number of workflow runs succeeded.|
|RunsFailed|Runs Failed|Count|Total|Number of workflow runs failed.|
|RunsCancelled|Runs Cancelled|Count|Total|Number of workflow runs cancelled.|
|RunLatency|Run Latency|Seconds|Average|Latency of completed workflow runs.|
|RunSuccessLatency|Run Success Latency|Seconds|Average|Latency of succeeded workflow runs.|
|RunThrottledEvents|Run Throttled Events|Count|Total|Number of workflow action or trigger throttled events.|
|RunFailurePercentage|Run Failure Percentage|Percent|Total|Percentage of workflow runs failed.|
|ActionsStarted|Actions Started |Count|Total|Number of workflow actions started.|
|ActionsCompleted|Actions Completed |Count|Total|Number of workflow actions completed.|
|ActionsSucceeded|Actions Succeeded |Count|Total|Number of workflow actions succeeded.|
|ActionsFailed|Actions Failed|Count|Total|Number of workflow actions failed.|
|ActionsSkipped|Actions Skipped |Count|Total|Number of workflow actions skipped.|
|ActionLatency|Action Latency |Seconds|Average|Latency of completed workflow actions.|
|ActionSuccessLatency|Action Success Latency |Seconds|Average|Latency of succeeded workflow actions.|
|ActionThrottledEvents|Action Throttled Events|Count|Total|Number of workflow action throttled events..|
|TriggersStarted|Triggers Started |Count|Total|Number of workflow triggers started.|
|TriggersCompleted|Triggers Completed |Count|Total|Number of workflow triggers completed.|
|TriggersSucceeded|Triggers Succeeded |Count|Total|Number of workflow triggers succeeded.|
|TriggersFailed|Triggers Failed |Count|Total|Number of workflow triggers failed.|
|TriggersSkipped|Triggers Skipped|Count|Total|Number of workflow triggers skipped.|
|TriggersFired|Triggers Fired |Count|Total|Number of workflow triggers fired.|
|TriggerLatency|Trigger Latency |Seconds|Average|Latency of completed workflow triggers.|
|TriggerFireLatency|Trigger Fire Latency |Seconds|Average|Latency of fired workflow triggers.|
|TriggerSuccessLatency|Trigger Success Latency |Seconds|Average|Latency of succeeded workflow triggers.|
|TriggerThrottledEvents|Trigger Throttled Events|Count|Total|Number of workflow trigger throttled events.|
|BillableActionExecutions|Billable Action Executions|Count|Total|Number of workflow action executions getting billed.|
|BillableTriggerExecutions|Billable Trigger Executions|Count|Total|Number of workflow trigger executions getting billed.|
|TotalBillableExecutions|Total Billable Executions|Count|Total|Number of workflow executions getting billed.|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|Throughput|Throughput|BytesPerSecond|Average||

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|registration.all|Registration Operation|Count|Total|The count of all successful registration operations (creations updates queries and deletions). |
|registration.create|Registration Create Operations|Count|Total|The count of all successful registration creations.|
|registration.update|Registration Update Operations|Count|Total|The count of all successful registration updates.|
|registration.get|Registration Read Operations|Count|Total|The count of all successful registration queries.|
|registration.delete|Registration Delete Operations|Count|Total|The count of all successful registration deletions.|
|incoming|Incoming Messages|Count|Total|The count of all successful send API calls. |
|incoming.scheduled|Scheduled Push Notifications Sent|Count|Total|Scheduled Push Notifications Cancelled|
|incoming.scheduled.cancel|Scheduled Push Notifications Cancelled|Count|Total|Scheduled Push Notifications Cancelled|
|scheduled.pending|Pending Scheduled Notifications|Count|Total|Pending Scheduled Notifications|
|installation.all|Installation Management Operations|Count|Total|Installation Management Operations|
|installation.get|Get Installation Operations|Count|Total|Get Installation Operations|
|installation.upsert|Create or Update Installation Operations|Count|Total|Create or Update Installation Operations|
|installation.patch|Patch Installation Operations|Count|Total|Patch Installation Operations|
|installation.delete|Delete Installation Operations|Count|Total|Delete Installation Operations|
|outgoing.allpns.success|Successful notifications|Count|Total|The count of all successful notifications.|
|outgoing.allpns.invalidpayload|Payload Errors|Count|Total|The count of pushes that failed because the PNS returned a bad payload error.|
|outgoing.allpns.pnserror|External Notification System Errors|Count|Total|The count of pushes that failed because there was a problem communicating with the PNS (excludes authentication problems).|
|outgoing.allpns.channelerror|Channel Errors|Count|Total|The count of pushes that failed because the channel was invalid not associated with the correct app throttled or expired.|
|outgoing.allpns.badorexpiredchannel|Bad or Expired Channel Errors|Count|Total|The count of pushes that failed because the channel/token/registrationId in the registration was expired or invalid.|
|outgoing.wns.success|WNS Successful Notifications|Count|Total|The count of all successful notifications.|
|outgoing.wns.invalidcredentials|WNS Authorization Errors (Invalid Credentials)|Count|Total|The count of pushes that failed because the PNS did not accept the provided credentials or the credentials are blocked. (Windows Live does not recognize the credentials).|
|outgoing.wns.badchannel|WNS Bad Channel Error|Count|Total|The count of pushes that failed because the ChannelURI in the registration was not recognized (WNS status: 404 not found).|
|outgoing.wns.expiredchannel|WNS Expired Channel Error|Count|Total|The count of pushes that failed because the ChannelURI is expired (WNS status: 410 Gone).|
|outgoing.wns.throttled|WNS Throttled Notifications|Count|Total|The count of pushes that failed because WNS is throttling this app (WNS status: 406 Not Acceptable).|
|outgoing.wns.tokenproviderunreachable|WNS Authorization Errors (Unreachable)|Count|Total|Windows Live is not reachable.|
|outgoing.wns.invalidtoken|WNS Authorization Errors (Invalid Token)|Count|Total|The token provided to WNS is not valid (WNS status: 401 Unauthorized).|
|outgoing.wns.wrongtoken|WNS Authorization Errors (Wrong Token)|Count|Total|The token provided to WNS is valid but for another application (WNS status: 403 Forbidden). This can happen if the ChannelURI in the registration is associated with another app. Check that the client app is associated with the same app whose credentials are in the notification hub.|
|outgoing.wns.invalidnotificationformat|WNS Invalid Notification Format|Count|Total|The format of the notification is invalid (WNS status: 400). Note that WNS does not reject all invalid payloads.|
|outgoing.wns.invalidnotificationsize|WNS Invalid Notification Size Error|Count|Total|The notification payload is too large (WNS status: 413).|
|outgoing.wns.channelthrottled|WNS Channel Throttled|Count|Total|The notification was dropped because the ChannelURI in the registration is throttled (WNS response header: X-WNS-NotificationStatus:channelThrottled).|
|outgoing.wns.channeldisconnected|WNS Channel Disconnected|Count|Total|The notification was dropped because the ChannelURI in the registration is throttled (WNS response header: X-WNS-DeviceConnectionStatus: disconnected).|
|outgoing.wns.dropped|WNS Dropped Notifications|Count|Total|The notification was dropped because the ChannelURI in the registration is throttled (X-WNS-NotificationStatus: dropped but not X-WNS-DeviceConnectionStatus: disconnected).|
|outgoing.wns.pnserror|WNS Errors|Count|Total|Notification not delivered because of errors communicating with WNS.|
|outgoing.wns.authenticationerror|WNS Authentication Errors|Count|Total|Notification not delivered because of errors communicating with Windows Live invalid credentials or wrong token.|
|outgoing.apns.success|APNS Successful Notifications|Count|Total|The count of all successful notifications.|
|outgoing.apns.invalidcredentials|APNS Authorization Errors|Count|Total|The count of pushes that failed because the PNS did not accept the provided credentials or the credentials are blocked.|
|outgoing.apns.badchannel|APNS Bad Channel Error|Count|Total|The count of pushes that failed because the token is invalid (APNS status code: 8).|
|outgoing.apns.expiredchannel|APNS Expired Channel Error|Count|Total|The count of token that were invalidated by the APNS feedback channel.|
|outgoing.apns.invalidnotificationsize|APNS Invalid Notification Size Error|Count|Total|The count of pushes that failed because the payload was too large (APNS status code: 7).|
|outgoing.apns.pnserror|APNS Errors|Count|Total|The count of pushes that failed because of errors communicating with APNS.|
|outgoing.gcm.success|GCM Successful Notifications|Count|Total|The count of all successful notifications.|
|outgoing.gcm.invalidcredentials|GCM Authorization Errors (Invalid Credentials)|Count|Total|The count of pushes that failed because the PNS did not accept the provided credentials or the credentials are blocked.|
|outgoing.gcm.badchannel|GCM Bad Channel Error|Count|Total|The count of pushes that failed because the registrationId in the registration was not recognized (GCM result: Invalid Registration).|
|outgoing.gcm.expiredchannel|GCM Expired Channel Error|Count|Total|The count of pushes that failed because the registrationId in the registration was expired (GCM result: NotRegistered).|
|outgoing.gcm.throttled|GCM Throttled Notifications|Count|Total|The count of pushes that failed because GCM throttled this app (GCM status code: 501-599 or result:Unavailable).|
|outgoing.gcm.invalidnotificationformat|GCM Invalid Notification Format|Count|Total|The count of pushes that failed because the payload was not formatted correctly (GCM result: InvalidDataKey or InvalidTtl).|
|outgoing.gcm.invalidnotificationsize|GCM Invalid Notification Size Error|Count|Total|The count of pushes that failed because the payload was too large (GCM result: MessageTooBig).|
|outgoing.gcm.wrongchannel|GCM Wrong Channel Error|Count|Total|The count of pushes that failed because the registrationId in the registration is not associated to the current app (GCM result: InvalidPackageName).|
|outgoing.gcm.pnserror|GCM Errors|Count|Total|The count of pushes that failed because of errors communicating with GCM.|
|outgoing.gcm.authenticationerror|GCM Authentication Errors|Count|Total|The count of pushes that failed because the PNS did not accept the provided credentials the credentials are blocked or the SenderId is not correctly configured in the app (GCM result: MismatchedSenderId).|
|outgoing.mpns.success|MPNS Successful Notifications|Count|Total|The count of all successful notifications.|
|outgoing.mpns.invalidcredentials|MPNS Invalid Credentials|Count|Total|The count of pushes that failed because the PNS did not accept the provided credentials or the credentials are blocked.|
|outgoing.mpns.badchannel|MPNS Bad Channel Error|Count|Total|The count of pushes that failed because the ChannelURI in the registration was not recognized (MPNS status: 404 not found).|
|outgoing.mpns.throttled|MPNS Throttled Notifications|Count|Total|The count of pushes that failed because MPNS is throttling this app (WNS MPNS: 406 Not Acceptable).|
|outgoing.mpns.invalidnotificationformat|MPNS Invalid Notification Format|Count|Total|The count of pushes that failed because the payload of the notification was too large.|
|outgoing.mpns.channeldisconnected|MPNS Channel Disconnected|Count|Total|The count of pushes that failed because the ChannelURI in the registration was disconnected (MPNS status: 412 not found).|
|outgoing.mpns.dropped|MPNS Dropped Notifications|Count|Total|The count of pushes that were dropped by MPNS (MPNS response header: X-NotificationStatus: QueueFull or Suppressed).|
|outgoing.mpns.pnserror|MPNS Errors|Count|Total|The count of pushes that failed because of errors communicating with MPNS.|
|outgoing.mpns.authenticationerror|MPNS Authentication Errors|Count|Total|The count of pushes that failed because the PNS did not accept the provided credentials or the credentials are blocked.|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|SearchLatency|Search Latency|Seconds|Average|Average search latency for the search service|
|SearchQueriesPerSecond|Search queries per second|CountPerSecond|Average|Search queries per second for the search service|
|ThrottledSearchQueriesPercentage|Throttled search queries percentage|Percent|Average|Percentage of search queries that were throttled for the search service|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|CPUXNS|CPU usage per namespace|Percent|Maximum|Service bus premium namespace CPU usage metric|
|WSXNS|Memory size usage per namespace|Percent|Maximum|Service bus premium namespace memory usage metric|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|cpu_percent|CPU percentage|Percent|Average|CPU percentage|
|physical_data_read_percent|Data IO percentage|Percent|Average|Data IO percentage|
|log_write_percent|Log IO percentage|Percent|Average|Log IO percentage|
|dtu_consumption_percent|DTU percentage|Percent|Average|DTU percentage|
|storage|Total database size|Bytes|Maximum|Total database size|
|connection_successful|Successful Connections|Count|Total|Successful Connections|
|connection_failed|Failed Connections|Count|Total|Failed Connections|
|blocked_by_firewall|Blocked by Firewall|Count|Total|Blocked by Firewall|
|deadlock|Deadlocks|Count|Total|Deadlocks|
|storage_percent|Database size percentage|Percent|Maximum|Database size percentage|
|xtp_storage_percent|In-Memory OLTP storage percent|Percent|Average|In-Memory OLTP storage percent|
|workers_percent|Workers percentage|Percent|Average|Workers percentage|
|sessions_percent|Sessions percentage|Percent|Average|Sessions percentage|
|dtu_limit|DTU Limit|Count|Average|DTU Limit|
|dtu_used|DTU used|Count|Average|DTU used|
|service_level_objective|Service level objective of the database|Count|Total|Service level objective of the database|
|dwu_limit|DWU limit|Count|Maximum|DWU limit|
|dwu_consumption_percent|DWU percentage|Percent|Average|DWU percentage|
|dwu_used|DWU used|Count|Average|DWU used|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|cpu_percent|CPU percentage|Percent|Average|CPU percentage|
|physical_data_read_percent|Data IO percentage|Percent|Average|Data IO percentage|
|log_write_percent|Log IO percentage|Percent|Average|Log IO percentage|
|dtu_consumption_percent|DTU percentage|Percent|Average|DTU percentage|
|storage_percent|Storage percentage|Percent|Average|Storage percentage|
|workers_percent|Workers percentage|Percent|Average|Workers percentage|
|sessions_percent|Sessions percentage|Percent|Average|Sessions percentage|
|eDTU_limit|eDTU limit|Count|Average|eDTU limit|
|storage_limit|Storage limit|Bytes|Average|Storage limit|
|eDTU_used|eDTU used|Count|Average|eDTU used|
|storage_used|Storage used|Bytes|Average|Storage used|
|xtp_storage_percent|In-Memory OLTP storage percent|Percent|Average|In-Memory OLTP storage percent|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|ResourceUtilization|SU % Utilization|Percent|Maximum|SU % Utilization|
|InputEvents|Input Events|Count|Total|Input Events|
|InputEventBytes|Input Event Bytes|Bytes|Total|Input Event Bytes|
|LateInputEvents|Late Input Events|Count|Total|Late Input Events|
|OutputEvents|Output Events|Count|Total|Output Events|
|ConversionErrors|Data Conversion Errors|Count|Total|Data Conversion Errors|
|Errors|Runtime Errors|Count|Total|Runtime Errors|
|DroppedOrAdjustedEvents|Out of order Events|Count|Total|Out of order Events|
|AMLCalloutRequests|Function Requests|Count|Total|Function Requests|
|AMLCalloutFailedRequests|Failed Function Requests|Count|Total|Failed Function Requests|
|AMLCalloutInputEvents|Function Events|Count|Total|Function Events|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|CpuPercentage|CPU Percentage|Percent|Average|CPU Percentage|
|MemoryPercentage|Memory Percentage|Percent|Average|Memory Percentage|
|DiskQueueLength|Disk Queue Length|Count|Total|Disk Queue Length|
|HttpQueueLength|Http Queue Length|Count|Total|Http Queue Length|
|BytesReceived|Data In|Bytes|Total|Data In|
|BytesSent|Data Out|Bytes|Total|Data Out|

## <a name="microsoftwebsites-including-functions"></a>Microsoft.Web/sites (including Functions)

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|CpuTime|CPU Time|Seconds|Total|CPU Time|
|Requests|Requests|Count|Total|Requests|
|BytesReceived|Data In|Bytes|Total|Data In|
|BytesSent|Data Out|Bytes|Total|Data Out|
|Http101|Http 101|Count|Total|Http 101|
|Http2xx|Http 2xx|Count|Total|Http 2xx|
|Http3xx|Http 3xx|Count|Total|Http 3xx|
|Http401|Http 401|Count|Total|Http 401|
|Http403|Http 403|Count|Total|Http 403|
|Http404|Http 404|Count|Total|Http 404|
|Http406|Http 406|Count|Total|Http 406|
|Http4xx|Http 4xx|Count|Total|Http 4xx|
|Http5xx|Http Server Errors|Count|Total|Http Server Errors|
|MemoryWorkingSet|Memory working set|Bytes|Average|Memory working set|
|AverageMemoryWorkingSet|Average memory working set|Bytes|Average|Average memory working set|
|AverageResponseTime|Average Response Time|Seconds|Average|Average Response Time|
|FunctionExecutionUnits|Function Execution Units|Count|Average|Function Execution Units|
|FunctionExecutionCount|Function Execution Count|Count|Average|Function Execution Count|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|Metric|Metric Display Name|Unit|Aggregation Type|Description|
|---|---|---|---|---|
|CpuTime|CPU Time|Seconds|Total|CPU Time|
|Requests|Requests|Count|Total|Requests|
|BytesReceived|Data In|Bytes|Total|Data In|
|BytesSent|Data Out|Bytes|Total|Data Out|
|Http101|Http 101|Count|Total|Http 101|
|Http2xx|Http 2xx|Count|Total|Http 2xx|
|Http3xx|Http 3xx|Count|Total|Http 3xx|
|Http401|Http 401|Count|Total|Http 401|
|Http403|Http 403|Count|Total|Http 403|
|Http404|Http 404|Count|Total|Http 404|
|Http406|Http 406|Count|Total|Http 406|
|Http4xx|Http 4xx|Count|Total|Http 4xx|
|Http5xx|Http Server Errors|Count|Total|Http Server Errors|
|MemoryWorkingSet|Memory working set|Bytes|Average|Memory working set|
|AverageMemoryWorkingSet|Average memory working set|Bytes|Average|Average memory working set|
|AverageResponseTime|Average Response Time|Seconds|Average|Average Response Time|
|FunctionExecutionUnits|Function Execution Units|Count|Average|Function Execution Units|
|FunctionExecutionCount|Function Execution Count|Count|Average|Function Execution Count|

## <a name="next-steps"></a>Next steps
* [Read about metrics in Azure Monitor](monitoring-overview.md#monitoring-sources)
* [Create alerts on metrics](insights-receive-alert-notifications.md)
* [Export metrics to storage, Event Hub, or Log Analytics](monitoring-overview-of-diagnostic-logs.md)

