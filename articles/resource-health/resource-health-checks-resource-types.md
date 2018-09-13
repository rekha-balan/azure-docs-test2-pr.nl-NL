---
title: Supported Resource Types through Azure Resource health|Microsoft Docs
description: Supported Resource Types through Azure Resource health
services: Resource health
documentationcenter: ''
author: BernardoAMunoz
manager: ''
editor: ''
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: ece853d90f051828e07e48110c85dd9ad2dac5d8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562779"
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Resource types and health checks in Azure resource health
Below is a complete list of all the checks executed through resource health by resource types.

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|Executed Checks|
|---|
|<ul><li>Are all the Cache nodes up and running?</li><li>Can the Cache be reached from within the datacenter?</li><li>Has the Cache reached the maximum number of connections?</li><li> Has the cache exhausted its available memory? </li><li>Is the Cache experiencing a high number of page faults?</li><li>Is the Cache under heavy load?</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|Executed Checks|
|---|
|<ul> <li>Has any of the endpoints been stopped, removed, or misconfigured?</li><li>Is the supplemental portal accessible for CDN configuration operations?</li><li>Are there ongoing delivery issues with the CDN endpoints?</li><li>Can users change the configuration of their CDN resources?</li><li>Are configuration changes propagating at the expected rate?</li><li>Can users manage the CDN configuration using the Azure portal, PowerShell, or the API?</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|Executed Checks|
|---|
|<ul><li>Is the host server up and running?</li><li>Has the host OS booting completed?</li><li>Is the virtual machine container provisioned and powered up?</li><li>Is there network connectivity between the host and the storage account?</li><li>Has the booting of the guest OS completed?</li><li>Is there ongoing planned maintenance?</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/accounts
|Executed Checks|
|---|
|<ul><li>Can the account be reached from within the datacenter?</li><li>Is the Cognitive Services Resource Provider available?</li><li>Is the Cognitive Service available in the appropriate region?</li><li>Can read operations be performed on the storage account holding the resource metadata?</li><li>Has the API call quota been reached?</li><li>Has the API call read-limit been reached?</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.compute/virtualmachines
|Executed Checks|
|---|
|<ul><li>Is the server hosting this virtual machine up and running?</li><li>Has the host OS booting completed?</li><li>Is the virtual machine container provisioned and powered up?</li><li>Is there network connectivity between the host and the storage account?</li><li>Has the booting of the guest OS completed?</li><li>Is there ongoing planned maintenance?</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/accounts
|Executed Checks|
|---|
|<ul><li>Can users submit jobs to Data Lake Analytics in the region?</li><li>Do basic jobs run and complete successfully in the region?</li><li>Can users list catalog items in the region?</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/accounts
|Executed Checks|
|---|
|<ul><li>Can users upload data to Data Lake Store in the region?</li><li>Can users download data from Data Lake Store in the region?</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|Executed Checks|
|---|
|<ul><li>Have there been any database or collection requests not served due to a DocumentDB service unavailability?</li><li>Have there been any document requests not served due to a DocumentDB service unavailability?</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.network/connections
|Executed Checks|
|---|
|<ul><li>Is the VPN tunnel connected?</li><li>Are there configuration conflicts in the connection?</li><li>Are the pre-shared keys properly configured?</li><li>Is the VPN on-premise device reachable?</li><li>Are there mismatches in the IPSec/IKE security policy?</li><li>Is the S2S VPN connection properly provisioned or in a failed state?</li><li>Is the VNET-to-VNET connection properly provisioned or in a failed state?</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|Executed Checks|
|---|
|<ul><li>Is the VPN gateway reachable from the internet?</li><li>Is the VPN Gateway in standby mode?</li><li>Is the VPN service running on the gateway?</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|Executed Checks|
|---|
|<ul><li> Can runtime operations like registration, installation, or send be performed on the namespace?</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|Executed Checks|
|---|
|<ul><li>Is the host OS up and running?</li><li>Is the workspaceCollection reachable from outside the datacenter?</li><li>Is the PowerBI Resource Provider available?</li><li>Is the PowerBI Service available in the appropriate region?</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|Executed Checks|
|---|
|<ul><li>Can diagnostics operations be performed on the cluster?</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|Executed Checks|
|---|
|<ul><li> Have there been logins to the database?</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|Executed Checks|
|---|
|<ul><li>Are all the hosts where the job is executing up and running?</li><li>Was the job unable to start?</li><li>Are there ongoing runtime upgrades?</li><li>Is the job in an expected state (for example running or stopped by customer)?</li><li>Has the job encountered out of memory exceptions?</li><li>Are there ongoing scheduled compute updates?</li><li>Is the Execution Manager (control plan) available?</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|Executed Checks|
|---|
|<ul><li>Is the host server up and running?</li><li>Is Internet Information Services running?</li><li>Is the Load balancer running?</li><li>Can the Web Service Plan be reached from within the datacenter?</li><li>Is the storage account hosting the sites content for the serverFarm  available??</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.web/sites
|Executed Checks|
|---|
|<ul><li>Is the host server up and running?</li><li>Is Internet Information server running?</li><li>Is the Load balancer running?</li><li>Can the Web App be reached from within the datacenter?</li><li>Is the storage account hosting the site content available?</li></ul>|

See these resources to learn more about resource health:
-  [Introduction to Azure resource health](Resource-health-overview.md)
-  [Frequently asked questions about Azure resource health](Resource-health-faq.md)

