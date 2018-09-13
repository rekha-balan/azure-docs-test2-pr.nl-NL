---
title: Collect and analyze Windows Event logs in OMS Log Analytics | Microsoft Docs
description: Windows Event logs are one of the most common data sources used by Log Analytics.  This article describes how to configure collection of Windows Event logs and details of the records they create in the OMS repository.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: bwren
ms.openlocfilehash: d6100d995f610c1407c965e3dec36d86c8eeb477
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553125"
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Windows event log data sources in Log Analytics
Windows Event logs are one of the most common [data sources](log-analytics-data-sources.md) for collecting data using Windows agents since many applications write to the Windows event log.  You can collect events from standard logs such as System and Application in addition to specifying any custom logs created by applications you need to monitor.

![Windows Events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Configuring Windows Event logs
Configure Windows Event logs from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).

Log Analytics only collects events from the Windows event logs that are specified in the settings.  You can add an event log by typing in the name of the log and clicking **+**.  For each log, only the events with the selected severities are collected.  Check the severities for the particular log that you want to collect.  You cannot provide any additional criteria to filter events.

As you type the name of an event log, Log Analytics provides suggestions of common event log names. If the log you want to add does not appear in the list, you can still add it by typing in the full name of the log. You can find the full name of the log by using event viewer. In event viewer, open the *Properties* page for the log and copy the string from the *Full Name* field.

![Configure Windows events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a>Data collection
Log Analytics collects each event that matches a selected severity from a monitored event log as the event is created.  The agent records its place in each event log that it collects from.  If the agent goes offline for a period of time, then Log Analytics collects events from where it last left off, even if those events were created while the agent was offline.  There is a potential for these events to not be collected if the event log wraps with uncollected events being overwritten while the agent is offline.



## <a name="windows-event-records-properties"></a>Windows event records properties
Windows event records have a type of **Event** and have the properties in the following table:

| Property | Description |
|:--- |:--- |
| Computer |Name of the computer that the event was collected from. |
| EventCategory |Category of the event. |
| EventData |All event data in raw format. |
| EventID |Number of the event. |
| EventLevel |Severity of the event in numeric form. |
| EventLevelName |Severity of the event in text form. |
| EventLog |Name of the event log that the event was collected from. |
| ParameterXml |Event parameter values in XML format. |
| ManagementGroupName |Name of the management group for System Center Operations Manager agents.  For other agents, this value is AOI-<workspace ID> |
| RenderedDescription |Event description with parameter values |
| Source |Source of the event. |
| SourceSystem |Type of agent the event was collected from. <br> OpsManager – Windows agent, either direct connect or Operations Manager managed <br> Linux – All Linux agents  <br> AzureStorage – Azure Diagnostics |
| TimeGenerated |Date and time the event was created in Windows. |
| UserName |User name of the account that logged the event. |

## <a name="log-searches-with-windows-events"></a>Log searches with Windows Events
The following table provides different examples of log searches that retrieve Windows Event records.

| Query | Description |
|:--- |:--- |
| Type=Event |All Windows events. |
| Type=Event EventLevelName=error |All Windows events with severity of error. |
| Type=Event &#124; Measure count() by Source |Count of Windows events by source. |
| Type=Event EventLevelName=error &#124; Measure count() by Source |Count of Windows error events by source. |

## <a name="next-steps"></a>Next steps
* Configure Log Analytics to collect other [data sources](log-analytics-data-sources.md) for analysis.
* Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.  
* Use [Custom Fields](log-analytics-custom-fields.md) to parse the event records into individual fields.
* Configure [collection of performance counters](log-analytics-data-sources-performance-counters.md) from your Windows agents.



