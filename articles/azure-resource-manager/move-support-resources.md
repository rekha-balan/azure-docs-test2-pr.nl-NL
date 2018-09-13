---
title: Move operation support by Azure resource type | Microsoft Docs
description: Lists the Azure resource types that can be moved to a new resource group or subscription.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/07/2018
ms.author: tomfitz
ms.openlocfilehash: 45adce48e64ba185e3bb30ec5385ca8f8c523972
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867106"
---
# <a name="move-operation-support-for-resources"></a>Move operation support for resources

This article lists whether an Azure resource type supports the move operation. Although a resource type supports the move operation, there may be conditions that prevent the resource from being moved. For details about conditions that affect move operations, see [Move resources to new resource group or subscription](resource-group-move-resources.md).

## <a name="find-resource-provider-and-resource-type"></a>Find resource provider and resource type

To determine if a resource can be moved, you must find its resource provider and resource type.

For PowerShell, use:

```azurepowershell-interactive
Get-AzureRmResource -ResourceGroupName demogroup | Select Name, ResourceType | Format-table
```

For Azure CLI, use:

```azurecli-interactive
az resource list -g demogroup --query '[].{name:name, reourcetype:type}'
```

The resource type is returned in the format `<resource-provider>/<resource-type-name>`. So, the value `Microsoft.OperationalInsights/workspaces` has a resource provider of **Microsoft.OperationalInsights** and resource type name of **workspaces**.

After finding the resource provider and resource type, use the tables in this article to determine whether the resource type supports the move operation.

## <a name="microsoftaad"></a>Microsoft.AAD

| Resource type | Resource group | Subscription |
| ------------- | --------------- | ----------- |
| domainservices | No | No |

## <a name="microsoftanalysisservices"></a>Microsoft.AnalysisServices
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| servers | Yes | Yes |

## <a name="microsoftapimanagement"></a>Microsoft.ApiManagement
| Resource type | Resource group | Subscription |
| ------------- | --------------- | ----------- |
| service | Yes | Yes |

## <a name="microsoftauthorization"></a>Microsoft.Authorization
| Resource type | Resource group | Subscription |
| ------------- | --------------- | ----------- |
| policyassignments | No | No |

## <a name="microsoftautomation"></a>Microsoft.Automation
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| automationaccounts | Yes | Yes |
| automationaccounts/configurations | Yes | Yes |
| automationaccounts/runbooks | Yes | Yes |

## <a name="microsoftazureactivedirectory"></a>Microsoft.AzureActiveDirectory
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| b2cdirectories | Yes | Yes |

## <a name="microsoftazurestack"></a>Microsoft.AzureStack
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| registrations | Yes | Yes |

## <a name="microsoftbackup"></a>Microsoft.Backup
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| backupvault | No | No |

## <a name="microsoftbatch"></a>Microsoft.Batch
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| batchaccounts | Yes | Yes |

## <a name="microsoftbatchai"></a>Microsoft.BatchAI
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| clusters | No | No |
| fileservers | No | No |
| jobs | No | No |
| workspaces | No | No |

## <a name="microsoftbingmaps"></a>Microsoft.BingMaps
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| mapapis | No | No |

## <a name="microsoftbiztalkservices"></a>Microsoft.BizTalkServices
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| biztalk | Yes | Yes |

## <a name="microsoftblueprint"></a>Microsoft.Blueprint
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| blueprintassignments | No | No |

## <a name="microsoftbotservice"></a>Microsoft.BotService
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| botservices | Yes | Yes |

## <a name="microsoftcache"></a>Microsoft.Cache
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| redis | Yes | Yes |

## <a name="microsoftcdn"></a>Microsoft.Cdn
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| profiles | Yes | Yes |
| profiles/endpoints | Yes | Yes |

## <a name="microsoftcertificateregistration"></a>Microsoft.CertificateRegistration
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| certificateorders | Yes | Yes |

## <a name="microsoftclassiccompute"></a>Microsoft.ClassicCompute
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| domainnames | Yes | No |
| virtualmachines | Yes | No |

## <a name="microsoftclassicnetwork"></a>Microsoft.ClassicNetwork
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| networksecuritygroups | No | No |
| reservedips | No | No |
| virtualnetworks | No | No |

## <a name="microsoftclassicstorage"></a>Microsoft.ClassicStorage
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| storageaccounts | Yes | No |

## <a name="microsoftcognitiveservices"></a>Microsoft.CognitiveServices
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| accounts | Yes | Yes |

## <a name="microsoftcompute"></a>Microsoft.Compute
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| availabilitysets | Yes | Yes |
| disks | Yes | Yes |
| galleries | No | No |
| galleries/images | No | No |
| galleries/images/versions | No | No |
| images | Yes | Yes |
| restorepointcollections | No | No |
| sharedvmimages | No | No |
| sharedvmimages/versions | No | No |
| snapshots | Yes | Yes |
| virtualmachines | Yes | Yes |
| virtualmachines/extensions | Yes | Yes |
| virtualmachinescalesets | Yes | Yes |

## <a name="microsoftcontainer"></a>Microsoft.Container
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| containergroups | No | No |

## <a name="microsoftcontainerinstance"></a>Microsoft.ContainerInstance
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| containergroups | No | No |

## <a name="microsoftcontainerregistry"></a>Microsoft.ContainerRegistry
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| registries | Yes | Yes |
| registries/buildtasks | Yes | Yes |
| registries/replications | No | No |
| registries/webhooks | Yes | Yes |

## <a name="microsoftcontainerservice"></a>Microsoft.ContainerService
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| containerservices | No | No |
| managedclusters | No | No |

## <a name="microsoftcontentmoderator"></a>Microsoft.ContentModerator
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| applications | Yes | Yes |

## <a name="microsoftcostmanagement"></a>Microsoft.CostManagement
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| connectors | Yes | Yes |

## <a name="microsoftcustomerinsights"></a>Microsoft.CustomerInsights
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| hubs | Yes | Yes |

## <a name="microsoftdatabox"></a>Microsoft.DataBox
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| jobs | No | No |

## <a name="microsoftdataboxedge"></a>Microsoft.DataBoxEdge
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| databoxedgedevices | No | No |

## <a name="microsoftdatabricks"></a>Microsoft.Databricks
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| workspaces | No | No |

## <a name="microsoftdatacatalog"></a>Microsoft.DataCatalog
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| catalogs | Yes | Yes |

## <a name="microsoftdatafactory"></a>Microsoft.DataFactory
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| datafactories | Yes | Yes |
| factories | Yes | Yes |

## <a name="microsoftdatalake"></a>Microsoft.DataLake
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| datalakeaccounts | No | No |

## <a name="microsoftdatalakeanalytics"></a>Microsoft.DataLakeAnalytics
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| accounts | Yes | Yes |

## <a name="microsoftdatalakestore"></a>Microsoft.DataLakeStore
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| accounts | Yes | Yes |

## <a name="microsoftdatamigration"></a>Microsoft.DataMigration
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| services | No | No |
| services/projects | No | No |
| slots | No | No |

## <a name="microsoftdbformariadb"></a>Microsoft.DBforMariaDB
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| servers | No | No |

## <a name="microsoftdbformysql"></a>Microsoft.DBforMySQL
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| servers | No | No |

## <a name="microsoftdbforpostgresql"></a>Microsoft.DBforPostgreSQL
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| servergroups | No | No |
| servers | No | No |

## <a name="microsoftdevices"></a>Microsoft.Devices
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| iothubs | Yes | Yes |
| provisioningservices | Yes | Yes |

## <a name="microsoftdevtestlab"></a>Microsoft.DevTestLab
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| labcenters | No | No |
| labs | Yes | No |
| labs/servicerunners | Yes | Yes |
| labs/virtualmachines | Yes | No |
| schedules | No | No |

## <a name="microsoftdns"></a>microsoft.dns
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| dnszones | No | No |
| dnszones/a | No | No |
| dnszones/aaaa | No | No |
| dnszones/cname | No | No |
| dnszones/mx | No | No |
| dnszones/ptr | No | No |
| dnszones/srv | No | No |
| dnszones/txt | No | No |
| trafficmanagerprofiles | No | No |

## <a name="microsoftdocumentdb"></a>Microsoft.DocumentDB
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| databaseaccounts | Yes | Yes |

## <a name="microsoftdomainregistration"></a>Microsoft.DomainRegistration
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| domains | Yes | Yes |

## <a name="microsofteventgrid"></a>Microsoft.EventGrid
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| topics | Yes | Yes |

## <a name="microsofteventhub"></a>Microsoft.EventHub
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| clusters | Yes | Yes |
| namespaces | Yes | Yes |

## <a name="microsofthanaonazure"></a>Microsoft.HanaOnAzure
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| hanainstances | Yes | Yes |

## <a name="microsofthardwaresecuritymodules"></a>Microsoft.HardwareSecurityModules
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| dedicatedhsms | No | No |

## <a name="microsofthdinsight"></a>Microsoft.HDInsight
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| clusters | Yes | Yes |

## <a name="microsoftimportexport"></a>Microsoft.ImportExport
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| jobs | Yes | Yes |

## <a name="microsoftinsights"></a>microsoft.insights
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| actiongroups | Yes | Yes |
| activitylogalerts | No | No |
| alertrules | Yes | Yes |
| autoscalesettings | Yes | Yes |
| components | Yes | Yes |
| metricalerts | No | No |
| scheduledqueryrules | Yes | Yes |
| webtests | Yes | Yes |
| workbooks | Yes | Yes |

## <a name="microsoftiotcentral"></a>Microsoft.IoTCentral
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| iotapps | Yes | Yes |

## <a name="microsoftkeyvault"></a>Microsoft.KeyVault
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| vaults | Yes | Yes |

## <a name="microsoftlabservices"></a>Microsoft.LabServices
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| labaccounts | Yes | Yes |

## <a name="microsoftlocationbasedservices"></a>Microsoft.LocationBasedServices
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| accounts | Yes | Yes |

## <a name="microsoftlocationservices"></a>Microsoft.LocationServices
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| accounts | Yes | Yes |

## <a name="microsoftlogic"></a>Microsoft.Logic
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| integrationaccounts | Yes | Yes |
| workflows | Yes | Yes |

## <a name="microsoftmachinelearning"></a>Microsoft.MachineLearning
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| commitmentplans | Yes | Yes |
| webservices | Yes | No |
| workspaces | Yes | Yes |

## <a name="microsoftmachinelearningcompute"></a>Microsoft.MachineLearningCompute
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| operationalizationclusters | Yes | Yes |

## <a name="microsoftmachinelearningexperimentation"></a>Microsoft.MachineLearningExperimentation
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| accounts | Yes | Yes |
| accounts/workspaces | Yes | Yes |
| accounts/workspaces/projects | Yes | Yes |
| teamaccounts | Yes | Yes |
| teamaccounts/workspaces | Yes | Yes |
| teamaccounts/workspaces/projects | Yes | Yes |

## <a name="microsoftmachinelearningmodelmanagement"></a>Microsoft.MachineLearningModelManagement
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| accounts | Yes | Yes |

## <a name="microsoftmanagedidentity"></a>Microsoft.ManagedIdentity
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| userassignedidentities | Yes | Yes |

## <a name="microsoftmaps"></a>Microsoft.Maps
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| accounts | Yes | Yes |

## <a name="microsoftmarketplaceapps"></a>Microsoft.MarketplaceApps
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| classicdevservices | No | No |

## <a name="microsoftmedia"></a>Microsoft.Media
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| mediaservices | Yes | Yes |
| mediaservices/liveevents | Yes | Yes |
| mediaservices/streamingendpoints | Yes | Yes |

## <a name="microsoftmigrate"></a>Microsoft.Migrate
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| projects | No | No |

## <a name="microsoftnetwork"></a>Microsoft.Network
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| applicationgateways | No | No |
| applicationsecuritygroups | Yes | Yes |
| connections | Yes | Yes |
| ddosprotectionplans | No | No |
| dnszones | Yes | Yes |
| expressroutecircuits | No | No |
| expressrouteports | No | No |
| loadbalancers | Yes | Yes |
| localnetworkgateways | Yes | Yes |
| networkintentpolicies | Yes | Yes |
| networkinterfaces | Yes | Yes |
| networksecuritygroups | Yes | Yes |
| networkwatchers | Yes | Yes |
| networkwatchers/connectionmonitors | Yes | Yes |
| networkwatchers/lenses | Yes | Yes |
| networkwatchers/pingmeshes | Yes | Yes |
| publicipaddresses | Yes | Yes |
| publicipprefixes | Yes | Yes |
| routefilters | No | No |
| routetables | Yes | Yes |
| trafficmanagerprofiles | Yes | Yes |
| virtualnetworkgateways | Yes | Yes |
| virtualnetworks | Yes | Yes |

## <a name="microsoftnotificationhubs"></a>Microsoft.NotificationHubs
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| namespaces | Yes | Yes |
| namespaces/notificationhubs | Yes | Yes |

## <a name="microsoftoperationalinsights"></a>Microsoft.OperationalInsights
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| workspaces | Yes | Yes |

## <a name="microsoftoperationsmanagement"></a>Microsoft.OperationsManagement
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| managementconfigurations | Yes | Yes |
| solutions | Yes | Yes |
| views | Yes | Yes |

## <a name="microsoftportal"></a>Microsoft.Portal
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| dashboards | Yes | Yes |

## <a name="microsoftpowerbi"></a>Microsoft.PowerBI
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| workspacecollections | Yes | Yes |

## <a name="microsoftpowerbidedicated"></a>Microsoft.PowerBIDedicated
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| capacities | Yes | Yes |

## <a name="microsoftrecoveryservices"></a>Microsoft.RecoveryServices
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| vaults | Yes | Yes |

## <a name="microsoftrelay"></a>Microsoft.Relay
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| namespaces | Yes | Yes |

## <a name="microsoftsaas"></a>Microsoft.SaaS
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| applications | Yes | No |

## <a name="microsoftscheduler"></a>Microsoft.Scheduler
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| flows | Yes | Yes |
| jobcollections | Yes | Yes |

## <a name="microsoftsearch"></a>Microsoft.Search
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| searchservices | Yes | Yes |

## <a name="microsoftservicebus"></a>Microsoft.ServiceBus
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| namespaces | Yes | Yes |

## <a name="microsoftservicefabric"></a>Microsoft.ServiceFabric
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| clusters | Yes | Yes |

## <a name="microsoftservicefabricmesh"></a>Microsoft.ServiceFabricMesh
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| applications | Yes | Yes |
| networks | Yes | Yes |
| volumes | Yes | Yes |

## <a name="microsoftsignalrservice"></a>Microsoft.SignalRService
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| signalr | Yes | Yes |

## <a name="microsoftsiterecovery"></a>Microsoft.SiteRecovery
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| siterecoveryvault | No | No |

## <a name="microsoftsolutions"></a>Microsoft.Solutions
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| appliancedefinitions | No | No |
| appliances | No | No |
| applicationdefinitions | No | No |
| applications | No | No |

## <a name="microsoftsql"></a>Microsoft.Sql
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| servers | Yes | Yes |
| servers/databases | Yes | Yes |
| servers/elasticpools | Yes | Yes |
| virtualclusters | Yes | Yes |

## <a name="microsoftstorage"></a>Microsoft.Storage
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| storageaccounts | Yes | Yes |

## <a name="microsoftstoragesync"></a>Microsoft.StorageSync
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| storagesyncservices | Yes | Yes |

## <a name="microsoftstorsimple"></a>Microsoft.StorSimple
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| managers | No | No |

## <a name="microsoftstreamanalytics"></a>Microsoft.StreamAnalytics
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| streamingjobs | Yes | Yes |

## <a name="microsofttimeseriesinsights"></a>Microsoft.TimeSeriesInsights
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| environments | Yes | Yes |
| environments/eventsources | Yes | Yes |
| environments/referencedatasets | Yes | Yes |

## <a name="microsoftvisualstudio"></a>microsoft.visualstudio
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| account | Yes | Yes |
| account/extension | Yes | Yes |
| account/project | Yes | Yes |

## <a name="microsoftweb"></a>Microsoft.Web
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| certificates | No | Yes |
| classicmobileservices | No | No |
| connectiongateways | Yes | Yes |
| connections | Yes | Yes |
| customapis | Yes | Yes |
| hostingenvironments | No | No |
| serverfarms | Yes | Yes |
| sites | Yes | Yes |
| sites/premieraddons | Yes | Yes |
| sites/slots | Yes | Yes |

## <a name="microsoftwindowsiot"></a>Microsoft.WindowsIoT
| Resource type | Resource group | Subscription |
| ------------- | -------------- | ------------ |
| deviceservices | Yes | Yes |


## <a name="third-party-services"></a>Third-party services

Third-party services currently don't support the move operation. These resource providers are:

* 84codes.CloudAMQP
* AppDynamics.APM
* Aspera.Transfers
* Auth0.Cloud
* Citrix.Cloud
* Citrix.Services
* CloudSimple.PrivateCloudIaaS
* Cloudyn.Analytics
* Conexlink.MyCloudIT
* Crypteron.DataSecurity
* Dynatrace.DynatraceSaaS
* Dynatrace.Ruxit
* LiveArena.Broadcast
* Lombiq.DotNest
* Mailjet.Email
* Myget.PackageManagement
* NewRelic.APM
* nuubit.nextgencdn
* Paraleap.CloudMonix
* Pokitdok.Platform
* RavenHq.Db
* Raygun.CrashReporting
* RevAPM.MobileCDN
* Sendgrid.Email
* Sparkpost.Basic
* stackify.retrace
* SuccessBricks.ClearDB
* TrendMicro.DeepSecurity
* U2uconsult.TheIdentityHub


## <a name="next-steps"></a>Next steps

* For commands to move resources, see [Move resources to new resource group or subscription](resource-group-move-resources.md).
