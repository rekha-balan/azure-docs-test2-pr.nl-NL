---
title: Azure Government available services | Microsoft Docs
description: Provides an overview of the available services in Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: smichelotti
manager: liki
ms.assetid: a453a23c-bc0f-4203-9075-0f579dea7e23
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 02/13/2017
ms.author: stemi
ms.openlocfilehash: 21c2a0faad87b84058093f02c831b374a644b4b6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553610"
---
# <a name="available-services-on-azure-government"></a>Available Services on Azure Government
Azure Government is continually expanding the services that are available.  These services are deployed using the same code that is used in Azure Public.  This section documents the services that are currently available on Azure Government, including two key types of information:

* **Variations:** Variations due to features that have not been deployed yet or properties (for example, URLs) that are unique to the government environment.  
* **Considerations:** Government-specific implementation detail to ensure data stays within your compliance boundary.

Everything else you need to know about these services can be found in their general documentation.

For the most current list of services, see the [Products by Region](https://azure.microsoft.com/regions/services/). 

In the following tables, services specified as Resource Manager enabled have resource providers and can be managed using PowerShell. For detailed information on Resource Manager providers, API versions, and schemas, refer [here](../azure-resource-manager/resource-manager-supported-services.md). Services specified as available in the Portal, can be managed in the [Azure Government Portal](https://portal.azure.us/). 


## <a name="computedocumentation-government-computemd"></a>[Compute](documentation-government-compute.md)

| Service | Resource Manager Enabled | Portal |
| --- | --- | --- |
| [Virtual Machines](documentation-government-compute.md#virtual-machines) | Yes | Yes |
| Batch | Yes | Yes |
| Cloud Services | Yes | Yes |
| Service Fabric | Yes | Yes |
| VM Scale Sets | Yes | Yes |


## <a name="networkingdocumentation-government-networkingmd"></a>[Networking](documentation-government-networking.md)

| Service | Resource Manager Enabled | Portal |
| --- | --- | --- |
| [ExpressRoute](documentation-government-networking.md#expressroute-private-connectivity) | Yes | Yes |
| Virtual Network | Yes | Yes |
| [Load Balancer](documentation-government-networking.md#support-for-load-balancer) | Yes | Yes |
| [Traffic Manager](documentation-government-networking.md#support-for-traffic-manger) | Yes | Yes |
| [VPN Gateway](documentation-government-networking.md#support-for-vpn-gateway) | Yes | Yes |
| Application Gateway | Yes | Yes |
| ExpressRoute | Yes | Yes |



## <a name="storagedocumentation-government-services-storagemd"></a>[Storage](documentation-government-services-storage.md)

| Service | Resource Manager Enabled | Portal |
| --- | --- | --- |
| [Storage - Blobs](documentation-government-services-storage.md#azure-storage) | Yes | Yes |
| [Storage - Tables](documentation-government-services-storage.md#azure-storage) | Yes | Yes |
| [Storage - Queues](documentation-government-services-storage.md#azure-storage) | Yes | Yes |
| [Storage - Files](documentation-government-services-storage.md#azure-storage) | Yes | Yes |
| [Storage - Disks](documentation-government-services-storage.md#azure-storage) | Yes | Yes |
| [StorSimple](documentation-government-services-storage.md) | Yes | Yes |
| [Backup](documentation-government-services-storage.md#azure-storage) | Yes | Yes |
| [Site Recovery](documentation-government-services-storage.md#azure-storage) | Yes | Yes |
| [Import/Export](documentation-government-services-storage.md#azure-storage) | Yes | No |



## <a name="web--mobiledocumentation-government-services-webandmobilemd"></a>[Web + Mobile](documentation-government-services-webandmobile.md)

| Service | Resource Manager Enabled | Portal |
| --- | --- | --- |
| [App Service - Web Apps](documentation-government-services-webandmobile.md#app-services) | Yes | Yes |
| [App Service - API Apps](documentation-government-services-webandmobile.md#app-services) | Yes | Yes |
| [App Service - Mobile Apps](documentation-government-services-webandmobile.md#app-services) | Yes | Yes |
| Media Services | Yes | Yes |


## <a name="databasesdocumentation-government-services-databasemd"></a>[Databases](documentation-government-services-database.md)

| Service | Resource Manager Enabled | Portal |
| --- | --- | --- |
| [SQL Database](documentation-government-services-database.md#sql-database) | Yes | Yes |
| SQL Data Warehouse | Yes | Yes |
| SQL Server Stretch Database | Yes | Yes |
| [Redis Cache](documentation-government-services-database.md#azure-redis-cache) | Yes | Yes |


## <a name="intelligence--analyticsdocumentation-government-services-intelligenceandanalyticsmd"></a>[Intelligence + Analytics](documentation-government-services-intelligenceandanalytics.md)

| Service | Resource Manager Enabled | Portal |
| --- | --- | --- |
| [HDInsights](documentation-government-services-intelligenceandanalytics.md#hdinsight) | Yes | Yes |
| [Power BI Pro](documentation-government-services-intelligenceandanalytics.md#power-bi) | No | No (Office 365 Admin Portal) |


## <a name="internet-of-things-iot"></a>Internet of Things (IoT)

| Service | Resource Manager Enabled | Portal |
| --- | --- | --- |
| Event Hubs | Yes | Yes |
| Notification Hubs | No | No (Go to [Legacy portal](https://manage.windowsazure.us/)) |


## <a name="enterprise-integration"></a>Enterprise Integration

| Service | Resource Manager Enabled | Portal |
| --- | --- | --- |
| Service Bus | Yes | Yes |
| [StorSimple](documentation-government-services-storage.md) | Yes | Yes |
| SQL Server Stretch Database | Yes | Yes |



## <a name="security--identitydocumentation-government-services-securityandidentitymd"></a>[Security + Identity](documentation-government-services-securityandidentity.md)

| Service | Resource Manager Enabled | Portal |
| --- | --- | --- |
| Azure Active Directory | Yes | Yes |
| [Key Vault](documentation-government-services-securityandidentity.md#key-vault) | Yes | No (Coming soon) |
| Multi-Factory Authentication | Yes | Yes |


## <a name="intelligence--analytics"></a>Intelligence + Analytics

| Service | Resource Manager Enabled | Portal |
| --- | --- | --- |
| Power BI | Yes | No |
| HDInsight | Yes | Yes |



## <a name="monitoring--managementdocumentation-government-services-monitoringandmanagementmd"></a>[Monitoring + Management](documentation-government-services-monitoringandmanagement.md)

| Service | Resource Manager Enabled | Portal |
| --- | --- | --- |
| [Automation](documentation-government-services-monitoringandmanagement.md#automation) | Yes | Yes |
| [Backup](documentation-government-services-backup.md) | Yes | Yes |
| [Log Analytics](documentation-government-services-monitoringandmanagement.md#log-analytics) | Yes | Yes |
| [Site Recovery](documentation-government-services-monitoringandmanagement.md#site-recovery) | Yes | Yes |
| Scheduler | Yes | No |
| Monitoring and Diagnostics | Yes | Yes |




## <a name="next-steps"></a>Next Steps
For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).

