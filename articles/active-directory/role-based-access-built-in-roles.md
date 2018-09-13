---
title: Actions and NotActions - roles in Azure RBAC | Microsoft Docs
description: This topic describes the built in roles for role-based access control (RBAC).
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: ''
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/21/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bb8d390a6ab045dc418bf80ec4fc218e0a35282b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554034"
---
# <a name="built-in-roles-for-azure-role-based-access-control"></a>Built-in roles for Azure Role-Based Access Control
Azure Role-Based Access Control (RBAC) comes with the following built-in roles that can be assigned to users, groups, and services. You can’t modify the definitions of built-in roles. However, you can create [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md) to fit the specific needs of your organization.

## <a name="roles-in-azure"></a>Roles in Azure
The following table provides brief descriptions of the built-in roles. Click the role name to see the detailed list of **actions** and **notactions** for the role. The **actions** property specifies the allowed actions on Azure resources. Action strings can use wildcard characters. The **notactions** property specifies the actions that are excluded from the allowed actions.

> [!NOTE]
> The Azure role definitions are constantly evolving. This article is kept as up to date as possible, but you can always find the latest roles definitions in Azure PowerShell. Use the cmdlets `(get-azurermroledefinition "<role name>").actions` or `(get-azurermroledefinition "<role name>").notactions` as applicable.
>
>

| Role name | Description |
| --- | --- |
| [API Management Service Contributor](#api-management-service-contributor) |Can manage API Management services |
| [Application Insights Component Contributor](#application-insights-component-contributor) |Can manage Application Insights components |
| [Automation Operator](#automation-operator) |Able to start, stop, suspend, and resume jobs |
| [Backup Contributor](#backup-contributor) | Can manage backup in Recovery Services vault |
| [Backup Operator](#backup-operator) | Can manage backup except removing backup, in Recovery Services vault |
| [Backup Reader](#backup-reader) | Can view all backup management services  |
| [BizTalk Contributor](#biztalk-contributor) |Can manage BizTalk services |
| [ClearDB MySQL DB Contributor](#cleardb-mysql-db-contributor) |Can manage ClearDB MySQL databases |
| [Contributor](#contributor) |Can manage everything except access. |
| [Data Factory Contributor](#data-factory-contributor) |Can create and manage data factories, and child resources within them. |
| [DevTest Labs User](#devtest-labs-user) |Can view everything and connect, start, restart, and shutdown virtual machines |
| [DNS Zone Contributor](#dns-zone-contributor) |Can manage DNS zones and records |
| [DocumentDB Account Contributor](#documentdb-account-contributor) |Can manage DocumentDB accounts |
| [Intelligent Systems Account Contributor](#intelligent-systems-account-contributor) |Can manage Intelligent Systems accounts |
| [Monitoring Reader](#monitoring-reader) |Can read all monitoring data |
| [Monitoring Contributor](#monitoring-contributor) |Can read monitoring data and edit monitoring settings |
| [Network Contributor](#network-contributor) |Can manage all network resources |
| [New Relic APM Account Contributor](#new-relic-apm-account-contributor) |Can manage New Relic Application Performance Management accounts and applications |
| [Owner](#owner) |Can manage everything, including access |
| [Reader](#reader) |Can view everything, but can't make changes |
| [Redis Cache Contributor](#redis-cache-contributor) |Can manage Redis caches |
| [Scheduler Job Collections Contributor](#scheduler-job-collections-contributor) |Can manage scheduler job collections |
| [Search Service Contributor](#search-service-contributor) |Can manage search services |
| [Security Manager](#security-manager) |Can manage security components, security policies, and virtual machines |
| [SQL DB Contributor](#sql-db-contributor) |Can manage SQL databases, but not their security-related policies |
| [SQL Security Manager](#sql-security-manager) |Can manage the security-related policies of SQL servers and databases |
| [SQL Server Contributor](#sql-server-contributor) |Can manage SQL servers and databases, but not their security-related policies |
| [Classic Storage Account Contributor](#classic-storage-account-contributor) |Can manage classic storage accounts |
| [Storage Account Contributor](#storage-account-contributor) |Can manage storage accounts |
| [User Access Administrator](#user-access-administrator) |Can manage user access to Azure resources |
| [Classic Virtual Machine Contributor](#classic-virtual-machine-contributor) |Can manage classic virtual machines, but not the virtual network or storage account to which they are connected |
| [Virtual Machine Contributor](#virtual-machine-contributor) |Can manage virtual machines, but not the virtual network or storage account to which they are connected |
| [Classic Network Contributor](#classic-network-contributor) |Can manage classic virtual networks and reserved IPs |
| [Web Plan Contributor](#web-plan-contributor) |Can manage web plans |
| [Website Contributor](#website-contributor) |Can manage websites, but not the web plans to which they are connected |

## <a name="role-permissions"></a>Role permissions
The following tables describe the specific permissions given to each role. This can include **Actions**, which give permissions, and **NotActions**, which restrict them.

### <a name="api-management-service-contributor"></a>API Management Service Contributor
Can manage API Management services

| **Actions** |  |
| --- | --- |
| Microsoft.ApiManagement/Service/* |Create and manage API Management Services |
| Microsoft.Authorization/*/read |Read authorization |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read roles and role assignments |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="application-insights-component-contributor"></a>Application Insights Component Contributor
Can manage Application Insights components

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role assignments |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.Insights/components/* |Create and manage Insights components |
| Microsoft.Insights/webtests/* |Create and manage web tests |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="automation-operator"></a>Automation Operator
Able to start, stop, suspend, and resume jobs

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role assignments |
| Microsoft.Automation/automationAccounts/jobs/read |Read automation account jobs |
| Microsoft.Automation/automationAccounts/jobs/resume/action |Resume an automation account job |
| Microsoft.Automation/automationAccounts/jobs/stop/action |Stop an automation account job |
| Microsoft.Automation/automationAccounts/jobs/streams/read |Read automation account job streams |
| Microsoft.Automation/automationAccounts/jobs/suspend/action |Suspend an automation account job |
| Microsoft.Automation/automationAccounts/jobs/write |Write automation account jobs |
| Microsoft.Automation/automationAccounts/jobSchedules/read |Read an automation account job schedule |
| Microsoft.Automation/automationAccounts/jobSchedules/write |Read an automation account job schedule |
| Microsoft.Automation/automationAccounts/read |Read automation accounts |
| Microsoft.Automation/automationAccounts/runbooks/read |Read automation runbooks |
| Microsoft.Automation/automationAccounts/schedules/read |Read automation account schedules |
| Microsoft.Automation/automationAccounts/schedules/write |Write automation account schedules |
| Microsoft.Insights/components/* |Create and manage Insights components |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="backup-contributor"></a>Backup Contributor
Can manage all backup management actions, except creating Recovery Services vault and giving access to others

| **Actions** | |
| --- | --- |
| Microsoft.Network/virtualNetworks/read | Read virtual networks |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/* | Manage results of operation on backup management |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/* | Create and manage backup containers inside backup fabrics of Recovery Services vault |
| Microsoft.RecoveryServices/Vaults/backupJobs/* | Create and manage backup jobs |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | Export backup jobs into an excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/* | Create and manage meta data related to backup management |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/* | Create and manage Results of backup management operations |
| Microsoft.RecoveryServices/Vaults/backupPolicies/* | Create and manage backup policies |
| Microsoft.RecoveryServices/Vaults/backupProtectableItems/* | Create and manage items which can be backed up |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/* | Create and manage backed up items |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/* | Create and manage containers holding backup items |
| Microsoft.RecoveryServices/Vaults/certificates/* | Create and manage certificates related to backup in Recovery Services vault |
| Microsoft.RecoveryServices/Vaults/extendedInformation/* | Create and manage extended info related to vault | 
| Microsoft.RecoveryServices/Vaults/read | Read recovery services vaults |
| Microsoft.RecoveryServices/Vaults/refreshContainers/* | Manage discovery operation for fetching newly created containers |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/* | Create and manage registered identities |
| Microsoft.RecoveryServices/Vaults/usages/* | Create and manage usage of Recovery Services vault |
| Microsoft.Resources/deployments/* | Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read | Read resource groups |
| Microsoft.Storage/storageAccounts/read | Read storage accounts |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="backup-operator"></a>Backup Operator
Can manage all backup management actions except creating vaults, removing backup and giving access to others

| **Actions** | |
| --- | --- |
| Microsoft.Network/virtualNetworks/read | Read virtual networks |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/read | Read results of operation on backup management |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/operationResults/read | Read operation results on protection containers |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/backup/action | Perform on-demand backup operation on a backed up item |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationResults/read | Read result of operation performed on backed up item |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationStatus/read | Read status of operation performed on backed up item |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read | Read backed up items |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/recoveryPoints/read | Read recovery point of a backed up item |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/recoveryPoints/restore/action | Perform a restore operation using a recovery point of a backed up item |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/write | Create a backup item |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/read | Read containers holding backup item |
| Microsoft.RecoveryServices/Vaults/backupJobs/* | Create and manage backup jobs |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | Export backup jobs into an excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/read | Read meta data related to backup management |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/* | Create and manage Results of backup management operations |
| Microsoft.RecoveryServices/Vaults/backupPolicies/operationResults/read | Read results of operations performed on backup policies |
| Microsoft.RecoveryServices/Vaults/backupPolicies/read | Read backup policies |
| Microsoft.RecoveryServices/Vaults/backupProtectableItems/* | Create and manage items which can be backed up |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/read | Read backed up items |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/read | Read backed up containers holding backup items |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read | Read extended info related to vault | 
| Microsoft.RecoveryServices/Vaults/extendedInformation/write | Write extended info related to vault | 
| Microsoft.RecoveryServices/Vaults/read | Read recovery services vaults |
| Microsoft.RecoveryServices/Vaults/refreshContainers/* | Manage discovery operation for fetching newly created containers |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read | Read results of operation performed on Registered items of the vault |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read | Read registered items of the vault |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/write | Write registered items to vault |
| Microsoft.RecoveryServices/Vaults/usages/read | Read usage of the Recovery Services vault |
| Microsoft.Resources/deployments/* | Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read | Read resource groups |
| Microsoft.Storage/storageAccounts/read | Read storage accounts |
| Microsoft.Support/* | Create and manage support tickets |

### <a name="backup-reader"></a>Backup Reader
Can monitor backup management in Recovery Services vault

| **Actions** | |
| --- | --- |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/read  | Read results of operation on backup management |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/operationResults/read  | Read operation results on protection containers |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationResults/read  | Read result of operation performed on backed up item |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationStatus/read  | Read status of operation performed on backed up item |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read  | Read backed up items |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/read  | Read containers holding backup item |
| Microsoft.RecoveryServices/Vaults/backupJobs/operationResults/read  | Read results of backup jobs |
| Microsoft.RecoveryServices/Vaults/backupJobs/read  | Read backup jobs |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | Export backup jobs into an excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/read  | Read meta data related to backup management |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/read  | Read backup management operation results |
| Microsoft.RecoveryServices/Vaults/backupPolicies/operationResults/read  | Read results of operations performed on backup policies |
| Microsoft.RecoveryServices/Vaults/backupPolicies/read  | Read backup policies |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/read  |  Read backed up items |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/read  | Read backed up containers holding backup items |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read  | Read extended info related to vault |
| Microsoft.RecoveryServices/Vaults/read  | Read recovery services vaults |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read  | Read result of discovery operation for fetching newly created containers |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read  | Read results of operation performed on Registered items of the vault |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read  | Read registered items of the vault |
| Microsoft.RecoveryServices/Vaults/usages/read  |  Read usage of the Recovery Services vault |

### <a name="biztalk-contributor"></a>BizTalk Contributor
Can manage BizTalk services

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role assignments |
| Microsoft.BizTalkServices/BizTalk/* |Create and manage BizTalk services |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="cleardb-mysql-db-contributor"></a>ClearDB MySQL DB Contributor
Can manage ClearDB MySQL databases

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role assignments |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |
| successbricks.cleardb/databases/* |Create and manage ClearDB MySQL databases |

### <a name="contributor"></a>Contributor
Can manage everything except access

| **Actions** |  |
| --- | --- |
| * |Create and manage resources of all types |

| **NotActions** |  |
| --- | --- |
| Microsoft.Authorization/*/Delete |Can’t delete roles and role assignments |
| Microsoft.Authorization/*/Write |Can’t create roles and role assignments |

### <a name="data-factory-contributor"></a>Data Factory Contributor
Create and manage data factories, and child resources within them.

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role Assignments |
| Microsoft.DataFactory/dataFactories/* |Create and manage data factories, and child resources within them. |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="devtest-labs-user"></a>DevTest Labs User
Can view everything and connect, start, restart, and shutdown virtual machines

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role Assignments |
| Microsoft.Compute/availabilitySets/read |Read the properties of availability sets |
| Microsoft.Compute/virtualMachines/*/read |Read the properties of a virtual machine (VM sizes, runtime status, VM extensions, etc.) |
| Microsoft.Compute/virtualMachines/deallocate/action |Deallocate virtual machines |
| Microsoft.Compute/virtualMachines/read |Read the properties of a virtual machine |
| Microsoft.Compute/virtualMachines/restart/action |Restart virtual machines |
| Microsoft.Compute/virtualMachines/start/action |Start virtual machines |
| Microsoft.DevTestLab/*/read |Read the properties of a lab |
| Microsoft.DevTestLab/labs/createEnvironment/action |Create a lab environment |
| Microsoft.DevTestLab/labs/formulas/delete |Delete formulas |
| Microsoft.DevTestLab/labs/formulas/read |Read formulas |
| Microsoft.DevTestLab/labs/formulas/write |Add or modify formulas |
| Microsoft.DevTestLab/labs/policySets/evaluatePolicies/action |Evaluate lab policies |
| Microsoft.Network/loadBalancers/backendAddressPools/join/action |Join a load balancer backend address pool |
| Microsoft.Network/loadBalancers/inboundNatRules/join/action |Join a load balancer inbound NAT rule |
| Microsoft.Network/networkInterfaces/*/read |Read the properties of a network interface (for example, all the load balancers that the network interface is a part of) |
| Microsoft.Network/networkInterfaces/join/action |Join a Virtual Machine to a network interface |
| Microsoft.Network/networkInterfaces/read |Read network interfaces |
| Microsoft.Network/networkInterfaces/write |Write network interfaces |
| Microsoft.Network/publicIPAddresses/*/read |Read the properties of a public IP address |
| Microsoft.Network/publicIPAddresses/join/action |Join a public IP address |
| Microsoft.Network/publicIPAddresses/read |Read network public IP addresses |
| Microsoft.Network/virtualNetworks/subnets/join/action |Join a virtual network |
| Microsoft.Resources/deployments/operations/read |Read deployment operations |
| Microsoft.Resources/deployments/read |Read deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Storage/storageAccounts/listKeys/action |List storage account keys |

### <a name="dns-zone-contributor"></a>DNS Zone Contributor
Can manage DNS zones and records.

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/\*/read |Read roles and role assignments |
| Microsoft.Insights/alertRules/\* |Create and manage alert rules |
| Microsoft.Network/dnsZones/\* |Create and manage DNS zones and records |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read the health of the resources |
| Microsoft.Resources/deployments/\* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/\* |Create and manage Support tickets |

### <a name="documentdb-account-contributor"></a>DocumentDB Account Contributor
Can manage DocumentDB accounts

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role Assignments |
| Microsoft.DocumentDb/databaseAccounts/* |Create and manage DocumentDB accounts |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="intelligent-systems-account-contributor"></a>Intelligent Systems Account Contributor
Can manage Intelligent Systems accounts

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role Assignments |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.IntelligentSystems/accounts/* |Create and manage intelligent systems accounts |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="monitoring-reader"></a>Monitoring Reader
Can read all monitoring data (metrics, logs, etc.). See also [Get started with roles, permissions, and security with Azure Monitor](/monitoring-and-diagnostics/monitoring-roles-permissions-security.md#built-in-monitoring-roles).

| **Actions** |  |
| --- | --- |
| */read |Read resources of all types, except secrets. |
| Microsoft.OperationalInsights/workspaces/search/action |Search Log Analytics data |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="monitoring-contributor"></a>Monitoring Contributor
Can read all monitoring data and edit monitoring settings. See also [Get started with roles, permissions, and security with Azure Monitor](/monitoring-and-diagnostics/monitoring-roles-permissions-security.md#built-in-monitoring-roles).

| **Actions** |  |
| --- | --- |
| */read |Read resources of all types, except secrets. |
| Microsoft.Insights/AlertRules/* |Read/write/delete alert rules. |
| Microsoft.Insights/components/* |Read/write/delete Application Insights components. |
| Microsoft.Insights/DiagnosticSettings/* |Read/write/delete diagnostic settings. |
| Microsoft.Insights/eventtypes/* |List Activity Log events (management events) in a subscription. This permission is applicable to both programmatic and portal access to the Activity Log. |
| Microsoft.Insights/LogDefinitions/* |This permission is necessary for users who need access to Activity Logs via the portal. List log categories in Activity Log. |
| Microsoft.Insights/MetricDefinitions/* |Read metric definitions (list of available metric types for a resource). |
| Microsoft.Insights/Metrics/* |Read metrics for a resource. |
| Microsoft.Insights/Register/Action |Register the Microsoft.Insights provider. |
| Microsoft.Insights/webtests/* |Read/write/delete Application Insights web tests. |
| Microsoft.OperationalInsights/workspaces/intelligencepacks/* |Read/write/delete Log Analytics solution packs. |
| Microsoft.OperationalInsights/workspaces/savedSearches/* |Read/write/delete Log Analytics saved searches. |
| Microsoft.OperationalInsights/workspaces/search/action |Search Log Analytics workspaces. |
| Microsoft.OperationalInsights/workspaces/sharedKeys/action |List keys for a Log Analytics workspace. |
| Microsoft.OperationalInsights/workspaces/storageinsightconfigs/* |Read/write/delete Log Analytics storage insight configurations. |

### <a name="network-contributor"></a>Network Contributor
Can manage all network resources

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role Assignments |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.Network/* |Create and manage networks |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="new-relic-apm-account-contributor"></a>New Relic APM Account Contributor
Can manage New Relic Application Performance Management accounts and applications

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role Assignments |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |
| NewRelic.APM/accounts/* |Create and manage New Relic application performance management accounts |

### <a name="owner"></a>Owner
Can manage everything, including access

| **Actions** |  |
| --- | --- |
| * |Create and manage resources of all types |

### <a name="reader"></a>Reader
Can view everything, but can't make changes

| **Actions** |  |
| --- | --- |
| */read |Read resources of all types, except secrets. |

### <a name="redis-cache-contributor"></a>Redis Cache Contributor
Can manage Redis caches

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role Assignments |
| Microsoft.Cache/redis/* |Create and manage Redis caches |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="scheduler-job-collections-contributor"></a>Scheduler Job Collections Contributor
Can manage Scheduler job collections

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role Assignments |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Scheduler/jobcollections/* |Create and manage job collections |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="search-service-contributor"></a>Search Service Contributor
Can manage Search services

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role Assignments |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Search/searchServices/* |Create and manage search services |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="security-manager"></a>Security Manager
Can manage security components, security policies, and virtual machines

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role Assignments |
| Microsoft.ClassicCompute/*/read |Read configuration information classic compute virtual machines |
| Microsoft.ClassicCompute/virtualMachines/*/write |Write configuration for virtual machines |
| Microsoft.ClassicNetwork/*/read |Read configuration information about classic network |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Security/* |Create and manage security components and policies |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="sql-db-contributor"></a>SQL DB Contributor
Can manage SQL databases but not their security-related policies

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read roles and role Assignments |
| Microsoft.Insights/alertRules/* |Create and manage alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Sql/servers/databases/* |Create and manage SQL databases |
| Microsoft.Sql/servers/read |Read SQL Servers |
| Microsoft.Support/* |Create and manage support tickets |

| **NotActions** |  |
| --- | --- |
| Microsoft.Sql/servers/databases/auditingPolicies/* |Can't edit audit policies |
| Microsoft.Sql/servers/databases/auditingSettings/* |Can't edit audit settings |
| Microsoft.Sql/servers/databases/auditRecords/read |Can't read audit records |
| Microsoft.Sql/servers/databases/connectionPolicies/* |Can't edit connection policies |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |Can't edit data masking policies |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |Can't edit security alert policies |
| Microsoft.Sql/servers/databases/securityMetrics/* |Can't edit security metrics |

### <a name="sql-security-manager"></a>SQL Security Manager
Can manage the security-related policies of SQL servers and databases

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read Microsoft authorization |
| Microsoft.Insights/alertRules/* |Create and manage Insights alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Sql/servers/auditingPolicies/* |Create and manage SQL server auditing policies |
| Microsoft.Sql/servers/auditingSettings/* |Create and manage SQL server auditing setting |
| Microsoft.Sql/servers/databases/auditingPolicies/* |Create and manage SQL server database auditing policies |
| Microsoft.Sql/servers/databases/auditingSettings/* |Create and manage SQL server database auditing settings |
| Microsoft.Sql/servers/databases/auditRecords/read |Read audit records |
| Microsoft.Sql/servers/databases/connectionPolicies/* |Create and manage SQL server database connection policies |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |Create and manage SQL server database data masking policies |
| Microsoft.Sql/servers/databases/read |Read SQL databases |
| Microsoft.Sql/servers/databases/schemas/read |Read SQL server database schemas |
| Microsoft.Sql/servers/databases/schemas/tables/columns/read |Read SQL server database table columns |
| Microsoft.Sql/servers/databases/schemas/tables/read |Read SQL server database tables |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |Create and manage SQL server database security alert policies |
| Microsoft.Sql/servers/databases/securityMetrics/* |Create and manage SQL server database security metrics |
| Microsoft.Sql/servers/read |Read SQL Servers |
| Microsoft.Sql/servers/securityAlertPolicies/* |Create and manage SQL server security alert policies |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="sql-server-contributor"></a>SQL Server Contributor
Can manage SQL servers and databases but not their security-related policies

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read authorization |
| Microsoft.Insights/alertRules/* |Create and manage Insights alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Sql/servers/* |Create and manage SQL servers |
| Microsoft.Support/* |Create and manage support tickets |

| **NotActions** |  |
| --- | --- |
| Microsoft.Sql/servers/auditingPolicies/* |Can't edit SQL server auditing policies |
| Microsoft.Sql/servers/auditingSettings/* |Can't edit SQL server auditing settings |
| Microsoft.Sql/servers/databases/auditingPolicies/* |Can't edit SQL server database auditing policies |
| Microsoft.Sql/servers/databases/auditingSettings/* |Can't edit SQL server database auditing settings |
| Microsoft.Sql/servers/databases/auditRecords/read |Can't read audit records |
| Microsoft.Sql/servers/databases/connectionPolicies/* |Can't edit SQL server database connection policies |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |Can't edit SQL server database data masking policies |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |Can't edit SQL server database security alert policies |
| Microsoft.Sql/servers/databases/securityMetrics/* |Can't edit SQL server database security metrics |
| Microsoft.Sql/servers/securityAlertPolicies/* |Can't edit SQL server security alert policies |

### <a name="classic-storage-account-contributor"></a>Classic Storage Account Contributor
Can manage classic storage accounts

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read authorization |
| Microsoft.ClassicStorage/storageAccounts/* |Create and manage storage accounts |
| Microsoft.Insights/alertRules/* |Create and manage Insights alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="storage-account-contributor"></a>Storage Account Contributor
Can manage storage accounts, but not access to them.

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read all authorization |
| Microsoft.Insights/alertRules/* |Create and manage Insights alert rules |
| Microsoft.Insights/diagnosticSettings/* |Manage diagnostic settings |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Storage/storageAccounts/* |Create and manage storage accounts |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="user-access-administrator"></a>User Access Administrator
Can manage user access to Azure resources

| **Actions** |  |
| --- | --- |
| */read |Read resources of all Types, except secrets. |
| Microsoft.Authorization/* |Manage authorization |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="classic-virtual-machine-contributor"></a>Classic Virtual Machine Contributor
Can manage classic virtual machines but not the virtual network or storage account to which they are connected

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read authorization |
| Microsoft.ClassicCompute/domainNames/* |Create and manage classic compute domain names |
| Microsoft.ClassicCompute/virtualMachines/* |Create and manage virtual machines |
| Microsoft.ClassicNetwork/networkSecurityGroups/join/action |Join network security groups |
| Microsoft.ClassicNetwork/reservedIps/link/action |Link reserved IPs |
| Microsoft.ClassicNetwork/reservedIps/read |Read reserved IP addresses |
| Microsoft.ClassicNetwork/virtualNetworks/join/action |Join virtual networks |
| Microsoft.ClassicNetwork/virtualNetworks/read |Read virtual networks |
| Microsoft.ClassicStorage/storageAccounts/disks/read |Read storage account disks |
| Microsoft.ClassicStorage/storageAccounts/images/read |Read storage account images |
| Microsoft.ClassicStorage/storageAccounts/listKeys/action |List storage account keys |
| Microsoft.ClassicStorage/storageAccounts/read |Read classic storage accounts |
| Microsoft.Insights/alertRules/* |Create and manage Insights alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="virtual-machine-contributor"></a>Virtual Machine Contributor
Can manage virtual machines but not the virtual network or storage account to which they are connected

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read authorization |
| Microsoft.Compute/availabilitySets/* |Create and manage compute availability sets |
| Microsoft.Compute/locations/* |Create and manage compute locations |
| Microsoft.Compute/virtualMachines/* |Create and manage virtual machines |
| Microsoft.Compute/virtualMachineScaleSets/* |Create and manage virtual machine scale sets |
| Microsoft.Insights/alertRules/* |Create and manage Insights alert rules |
| Microsoft.Network/applicationGateways/backendAddressPools/join/action |Join network application gateway backend address pools |
| Microsoft.Network/loadBalancers/backendAddressPools/join/action |Join load balancer backend address pools |
| Microsoft.Network/loadBalancers/inboundNatPools/join/action |Join load balancer inbound NAT pools |
| Microsoft.Network/loadBalancers/inboundNatRules/join/action |Join load balancer inbound NAT rules |
| Microsoft.Network/loadBalancers/read |Read load balancers |
| Microsoft.Network/locations/* |Create and manage network locations |
| Microsoft.Network/networkInterfaces/* |Create and manage network interfaces |
| Microsoft.Network/networkSecurityGroups/join/action |Join network security groups |
| Microsoft.Network/networkSecurityGroups/read |Read network security groups |
| Microsoft.Network/publicIPAddresses/join/action |Join network public IP addresses |
| Microsoft.Network/publicIPAddresses/read |Read network public IP addresses |
| Microsoft.Network/virtualNetworks/read |Read virtual networks |
| Microsoft.Network/virtualNetworks/subnets/join/action |Join virtual network subnets |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Storage/storageAccounts/listKeys/action |List storage account keys |
| Microsoft.Storage/storageAccounts/read |Read storage accounts |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="classic-network-contributor"></a>Classic Network Contributor
Can manage classic virtual networks and reserved IPs

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read authorization |
| Microsoft.ClassicNetwork/* |Create and manage classic networks |
| Microsoft.Insights/alertRules/* |Create and manage Insights alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |

### <a name="web-plan-contributor"></a>Web Plan Contributor
Can manage web plans

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read authorization |
| Microsoft.Insights/alertRules/* |Create and manage Insights alert rules |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |
| Microsoft.Web/serverFarms/* |Create and manage server farms |

### <a name="website-contributor"></a>Website Contributor
Can manage websites but not the web plans to which they are connected

| **Actions** |  |
| --- | --- |
| Microsoft.Authorization/*/read |Read authorization |
| Microsoft.Insights/alertRules/* |Create and manage Insights alert rules |
| Microsoft.Insights/components/* |Create and manage Insights components |
| Microsoft.ResourceHealth/availabilityStatuses/read |Read health of the resources |
| Microsoft.Resources/deployments/* |Create and manage resource group deployments |
| Microsoft.Resources/subscriptions/resourceGroups/read |Read resource groups |
| Microsoft.Support/* |Create and manage support tickets |
| Microsoft.Web/certificates/* |Create and manage website certificates |
| Microsoft.Web/listSitesAssignedToHostName/read |Read sites assigned to a host name |
| Microsoft.Web/serverFarms/join/action |Join server farms |
| Microsoft.Web/serverFarms/read |Read server farms |
| Microsoft.Web/sites/* |Create and manage websites (site creation also requires write permissions to the associated App Service Plan) |

## <a name="see-also"></a>See also
* [Role-Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.
* [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.
* [Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.
* [Role-Based Access Control troubleshooting](role-based-access-control-troubleshooting.md): Get suggestions for fixing common issues.
