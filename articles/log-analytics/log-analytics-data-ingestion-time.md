---
title: Data ingestion time in Azure Log Analytics | Microsoft Docs
description: Explains the different factors that affect latency in collecting data in Azure Log Analytics.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/10/2018
ms.author: bwren
ms.openlocfilehash: 0e513cc4f6a7d5d030ded807870de9eb0fdc0ed8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867998"
---
# <a name="data-ingestion-time-in-log-analytics"></a>Data ingestion time in Log Analytics
Azure Log Analytics is a high scale data service that serves thousands of customers sending terabytes of data each month at a growing pace. There are often questions about the time it takes for data to become available in Log Analytics after it's collected. This article explains the different factors that affect this latency.

## <a name="typical-latency"></a>Typical latency
Latency refers to the time that data is created on the monitored system and the time that it comes available for analysis in Log Analytics. The typical latency to ingest data into Log Analytics is between 3 and 10 minutes, with 95% of data ingested in less than 7 minutes. The specific latency for any particular data will vary depending on a variety of factors explained below.

## <a name="sla-for-log-analytics"></a>SLA for Log Analytics
The [Log Analytics Service Level Agreement (SLA)](https://azure.microsoft.com/support/legal/sla/log-analytics/v1_1/) is a legal binding agreement that defines when Microsoft refunds customers when the service doesn’t meet its goals. This isn't based on the typical performance of the system but its worst case, which accounts for potential catastrophic situations.

## <a name="factors-affecting-latency"></a>Factors affecting latency
The total ingestion time for a particular set of data can be broken down into the following high-level areas. 

- Agent time - The time to discover an event, collect it, and then send it to Log Analytics ingestion point as a log record. In most cases, this process is handled by an agent.
- Pipeline time - The time for the ingestion pipeline to process the log record. This includes parsing the properties of the event and potentially adding calculated information.
- Indexing time – The time spent to ingest a log record into Log Analytics Big Data store.

Details on the different latency introduced in this process are described below.

### <a name="agent-collection-latency"></a>Agent collection latency
Agents and management solutions use different strategies to collect data from a virtual machine, which may affect the latency. Some specific examples include the following:

- Windows events, syslog events, and performance metrics are collected immediately. Linux performance counters are polled at 30-second intervals.
- IIS logs and custom logs are collected once their timestamp changes. For IIS logs, this is influenced by the [rollover schedule configured on IIS](log-analytics-data-sources-iis-logs.md). 
- Active Directory Replication solution performs its assessment every five days, while the Active Directory Assessment solution performs a weekly assessment of your Active Directory infrastructure. The agent will collect these logs only when assessment is complete.

### <a name="agent-upload-frequency"></a>Agent upload frequency
To ensure Log Analytics agent is lightweight, the agent buffers logs and periodically uploads them to Log Analytics. Upload frequency varies between 30 seconds and 2 minutes depending on the type of data. Most data is uploaded in under 1 minute. Network conditions may negatively affect the latency of this data to reach Log Analytics ingestion point.

### <a name="azure-logs-and-metrics"></a>Azure logs and metrics 
Activity log data will take about 5 minutes to come available in Log Analytics. Data from diagnostic logs and metrics can take 1-5 minutes to become available, depending on the Azure service. It will then take an additional 30-60 seconds for logs and 3 minutes for metrics for data to be sent to Log Analytics ingestion point.

### <a name="management-solutions-collection"></a>Management solutions collection
Some solutions do not collect their data from an agent and may use a collection method that introduces additional latency. Some solutions collect data at regular intervals without attempting near-real time collection. Specific examples include the following:

- Office 365 solution polls activity logs using the Office 365 Management Activity API, which currently does not provide any near-real time latency guarantees.
- Windows Analytics solutions (Update Compliance for example) data is collected by the solution at a daily frequency.

Refer to the documentation for each solution to determine its collection frequency.

### <a name="pipeline-process-time"></a>Pipeline-process time
Once log records are ingested into Log Analytics pipeline, they're written to temporary storage to ensure tenant isolation and to make sure that data isn't lost. This process typically adds 5-15 seconds. Some management solutions implement heavier algorithms to aggregate data and derive insights as data is streaming in. For example, the Network Performance Monitoring aggregates incoming data over 3-minute intervals, effectively adding 3-minute latency.

### <a name="new-custom-data-types-provisioning"></a>New custom data types provisioning
When a new type of custom data is created from a [custom log](../log-analytics/log-analytics-data-sources-custom-logs.md) or the [Data Collector API](../log-analytics/log-analytics-data-collector-api.md), the system creates a dedicated storage container. This is a one-time overhead that occurs only on the first appearance of this data type.

### <a name="surge-protection"></a>Surge protection
The top priority of Log Analytics is to ensure that no customer data is lost, so the system has built-in protection for data surges. This includes buffers to ensure that even under immense load, the system will keep functioning. Under normal load, these controls add less than a minute, but in extreme conditions and failures they could add significant time while ensuring data is safe.

### <a name="indexing-time"></a>Indexing time
There is a built-in balance for every Big Data platform between providing analytics and advanced search capabilities as opposed to providing immediate access to the data. Azure Log Analytics allows you to run powerful queries on billions of records and get results within a few seconds. This is made possible because the infrastructure transforms the data dramatically during its ingestion and stores it in unique compact structures. The system buffers the data until enough of it is available to create these structures. This must be completed before the log record appears in search results.

This process currently takes about 5 minutes when there is low volume of data but less time at higher data rates. This seems counterintuitive, but this process allows optimization of latency for high-volume production workloads.



## <a name="checking-ingestion-time"></a>Checking ingestion time
You can use the **Heartbeat** table to get an estimate of latency for data from agents. Since Heartbeat is sent once a minute, the difference between the current time and the last heartbeat record will ideally be as close to a minute as possible.

Use the following query to list the computers with the highest latency.

    Heartbeat 
    | summarize IngestionTime = now() - max(TimeGenerated) by Computer 
    | top 50 by IngestionTime asc

 
Use the following query in large environments summarize the latency for different percentages of total computers.

    Heartbeat 
    | summarize IngestionTime = now() - max(TimeGenerated) by Computer 
    | summarize percentiles(IngestionTime, 50,95,99)



## <a name="next-steps"></a>Next steps
* Read the [Service Level Agreement (SLA)](https://azure.microsoft.com/support/legal/sla/log-analytics/v1_1/) for Log Analytics.

