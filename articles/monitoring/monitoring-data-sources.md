---
title: Sources of monitoring data in Azure | Microsoft Docs
description: Describes the data available to monitor the health and performance of your Azure resources and the applications running on them.
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.service: monitoring
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2018
ms.author: bwren
ms.openlocfilehash: 48cbfac78b41b47419799584837e094d45757628
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865109"
---
# <a name="sources-of-monitoring-data-in-azure"></a>Sources of monitoring data in Azure
This article describes the data available to monitor the health and performance of your Azure resources and the applications running on them.  Collect and analyze this data with the tools described in [Collecting monitoring data in Azure](monitoring-data-collection.md)

Monitoring data in Azure comes from a variety of sources that can be organized into tiers, the highest tier being your application and the lowest tier being the Azure platform. This is illustrated in the following diagram with each tier described in detail in the following sections.

![Tiers of monitoring data](media/monitoring-data-sources/monitoring-tiers.png)


## <a name="azure-platform"></a>Azure platform
Telemetry related to the health and operation of Azure itself includes data about the operation and management of your Azure subscription or tenant. It includes service health data stored in the Azure Activity log and audit logs from Azure Active Directory.

![Azure collection](media/monitoring-data-sources/azure-collection.png)

### <a name="azure-service-health"></a>Azure Service Health
[Azure Service Health](../monitoring-and-diagnostics/monitoring-service-notifications.md) provides information about the health of the Azure services in your subscription that your application and resources rely on. You can create alerts to be notified of current and expected critical issues that may affect your application. Service Health records are stored in the [Azure Activity log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), so you can view them in the Activity Log Explorer and copy them into Log Analytics.

### <a name="azure-activity-log"></a>Azure Activity Log
The [Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) includes service health records along with records on any configuration changes made to your Azure resources. The Activity log is available to all Azure resources and represents their _external_ view. The specific types of records in the Activity Log are described in [Azure Activity Log event schema](../monitoring-and-diagnostics/monitoring-activity-log-schema.md).

You can view the Activity Log for a particular resource on its page in the Azure portal or view logs from multiple resources in the [Activity Log Explorer](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md). It's particularly useful to copy the log entries to Log Analytics to combine it with other monitoring data. You can also send them to other locations using [Event Hubs](../monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs.md).


### <a name="azure-active-directory-audit-logs"></a>Azure Active Directory Audit Logs
[Azure Active Directory reporting](../active-directory/reports-monitoring/overview-reports.md) contains the history of sign-in activity and audit trail of changes made within a particular tenant. You can't currently combine Azure Active Directory audit data with other monitoring data as it's only accessible through Azure Active Directory and the [Azure Active Directory reporting API](../active-directory/reports-monitoring/concept-reporting-api.md).


## <a name="azure-services"></a>Azure Services
Metrics and resource level diagnostic logs provide information about the _internal_ operation of Azure resources. These are available for most Azure services, and management solutions provide additional insights into particular services.

![Azure resource collection](media/monitoring-data-sources/azure-resource-collection.png)


### <a name="metrics"></a>Metrics
Most Azure services will generate metrics that reflect their performance and operation. The specific [metrics will vary for each type of resource](../monitoring-and-diagnostics/monitoring-supported-metrics.md).  They are accessible from the Metrics Explorer and can be copied to Log Analytics for trending and other analysis.


### <a name="resource-diagnostic-logs"></a>Resource diagnostic Logs
While the Activity Log provides information about operations performed on an Azure resources, resource level [Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) provide insights into the operation of the resource itself.   The configuration requirements and content of these logs [varies by resource type](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

You can't directly view diagnostic logs in the Azure portal, but you can [send them to Azure storage for archiving](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md) and export them to [Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md) for redirection to other services, or [to Log Analytics](../monitoring-and-diagnostics/monitor-stream-diagnostic-logs-log-analytics.md) for analysis. Some resources can write directly to Log Analytics while others write to a storage account before being [imported into Log Analytics](../log-analytics/log-analytics-azure-storage-iis-table.md#use-the-azure-portal-to-collect-logs-from-azure-storage).

### <a name="management-solutions"></a>Management Solutions
 [Management solutions](../monitoring/monitoring-solutions.md) collect data to provide additional insight into the operation of a particular service. They collect data into Log Analytics where it may be analyzed using the [query language](../log-analytics/log-analytics-log-search.md) or views that are typically included in the solution.

## <a name="guest-operating-system"></a>Guest Operating System
In addition to the telemetry generated by all Azure services, compute resources have a guest operating system to monitor. With the installation of one or more agents, you can gather telemetry from the guest into the same monitoring tools as the Azure services themselves.

![Azure compute resource collection](media/monitoring-data-sources/compute-resource-collection.png)

### <a name="diagnostic-extension"></a>Diagnostic Extension
With the [Azure Diagnostics Extension](../monitoring-and-diagnostics/azure-diagnostics.md), you can collect logs and performance data from the client operating system of Azure compute resources. Both metrics and logs collected from clients are stored in an Azure storage account that you can [configure Log Analytics to import from](../log-analytics/log-analytics-azure-storage-iis-table.md#use-the-azure-portal-to-collect-logs-from-azure-storage).  The Metrics Explorer understands how to read from  the storage account and will include client metrics with other collected metrics.


### <a name="log-analytics-agent"></a>Log Analytics Agent
You can install the Log Analytics agent on any Windows or Linux virtual machine or physical computer. The virtual machine can be running in Azure, another cloud, or on-premises.  The agent connects to Log Analytics either directly or through a [connected System Center Operations Manager management group](../log-analytics/log-analytics-om-agents.md) and allows you to collect data from [data sources](../log-analytics/log-analytics-data-sources.md) that you configure or from [management solutions](../monitoring/monitoring-solutions.md) that provide additional insights into applications running on the virtual machine.

### <a name="service-map"></a>Service Map
[Service Map](../operations-management-suite/operations-management-suite-service-map.md) requires a Dependency Agent on Windows and Linux virtual machines. This works with the Log Analytics agent to collects data about processes running on the virtual machine and dependencies on external processes. It stores this data in Log Analytics and includes a console that visually displays the data it collects in addition to other data stored in Log Analytics.

## <a name="applications"></a>Applications
In addition to telemetry that your application may write to the guest operating system, detailed application monitoring is done with [Application Insights](https://docs.microsoft.com/azure/application-insights/). Application Insights can collect data from applications running on a variety of platforms. The application can be running in Azure, another cloud, or on-premises.

![Application data collection](media/monitoring-data-sources/application-collection.png)


#### <a name="application-data"></a>Application data
When you enable Application Insights for an application by installing an instrumentation package, it collects metrics and logs related to the performance and operation of the application. This includes detailed information about page views, application requests, and exceptions. Application Insights stores the data it collects in Azure Metrics and Log Analytics. It includes extensive tools for analyzing this data, but you can also analyze it with data from other sources using tools such as Metrics Explorer and log searches.

You can also use Application Insights to [create a custom metric](../application-insights/app-insights-api-custom-events-metrics.md).  This allows you to define your own logic for calculating a numeric value and then storing that value with other metrics that can be accessed from the Metric Explorer and used for [Autoscale](../monitoring-and-diagnostics/monitoring-autoscale-scale-by-custom-metric.md) and Metric alerts.

#### <a name="dependencies"></a>Dependencies
In order to monitor different logical operations of an application, you must [collect telemetry across multiple components](../application-insights/app-insights-transaction-diagnostics.md). Application Insights supports [distributed telemetry correlation](../application-insights/application-insights-correlation.md) which identifies the dependencies between components allowing you to analyze them together.

#### <a name="availability-tests"></a>Availability tests
[Availability tests](../application-insights/app-insights-monitor-web-app-availability.md) in Application Insights allow you to test the availability and responsiveness of your application from different locations on the public Internet. You can do a simple ping test to verify that the application is alive or use Visual Studio to create a web test that simulates a user scenario.  Availability tests don't require any instrumentation in the application.

## <a name="next-steps"></a>Next steps

- Learn more about the [types of monitoring data and the Azure tools](monitoring-data-collection.md) used to collect and analyze them.
