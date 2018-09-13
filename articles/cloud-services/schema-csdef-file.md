---
title: Azure Cloud Services Definition Schema (.csdef File) | Microsoft Docs
ms.custom: ''
ms.date: 04/14/2015
services: cloud-services
ms.reviewer: ''
ms.service: cloud-services
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: b7735dbf-8e91-4d1b-89f7-2f17e9302469
caps.latest.revision: 42
author: jpconnock
ms.author: jeconnoc
manager: timlt
ms.openlocfilehash: df2f7c1bf99c13779e5720e15d8d669aa4f945c0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868317"
---
# <a name="azure-cloud-services-definition-schema-csdef-file"></a>Azure Cloud Services Definition Schema (.csdef File)
The service definition file defines the service model for an application. The file contains the definitions for the roles that are available to a cloud service, specifies the service endpoints, and establishes configuration settings for the service. Configuration setting values are set in the service configuration file, as described by the [Cloud Service (classic) Configuration Schema](http://msdn.microsoft.com/library/b1ae68cd-cc95-48cb-a4a4-da91dc708a35).

By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Windows Azure\.NET SDK\<version>\schemas` directory. Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).

The default extension for the service definition file is .csdef.

## <a name="basic-service-definition-schema"></a>Basic service definition schema
The service definition file must contain one `ServiceDefinition` element. The service definition must contain at least one role (`WebRole` or `WorkerRole`) element. It can contain up to 25 roles defined in a single definition and you can mix role types. The service definition also contains the optional `NetworkTrafficRules` element which restricts which roles can communicate to specified internal endpoints. The service definition also contains the optional `LoadBalancerProbes` element which contains customer defined health probes of endpoints.

The basic format of the service definition file is as follows.

```xml
<ServiceDefinition name="<service-name>" topologyChangeDiscovery="<change-type>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" upgradeDomainCount="<number-of-upgrade-domains>" schemaVersion="<version>">
  
  <LoadBalancerProbes>
         …
  </LoadBalancerProbes>
  
  <WebRole …>
         …
  </WebRole>
  
  <WorkerRole …>
         …
  </WorkerRole>
  
  <NetworkTrafficRules>
         …
  </NetworkTrafficRules>

</ServiceDefinition>
```

## <a name="schema-definitions"></a>Schema definitions
The following topics describe the schema:

- [LoadBalancerProbe Schema](schema-csdef-loadbalancerprobe.md)
- [WebRole Schema](schema-csdef-webrole.md)
- [WorkerRole Schema](schema-csdef-workerrole.md)
- [NetworkTrafficRules Schema](schema-csdef-networktrafficrules.md)

##  <a name="ServiceDefinition"></a> ServiceDefinition Element
The `ServiceDefinition` element is the top-level element of the service definition file.

The following table describes the attributes of the `ServiceDefinition` element.

| Attribute               | Description |
| ----------------------- | ----------- |
| name                    |Required. The name of the service. The name must be unique within the service account.|
| topologyChangeDiscovery | Optional. Specifies the type of topology change notification. Possible values are:<br /><br /> -   `Blast` - Sends the update as soon as possible to all role instances. If you choose option, the role should be able to handle the topology update without being restarted.<br />-   `UpgradeDomainWalk` – Sends the update to each role instance in a sequential manner after the previous instance has successfully accepted the update.|
| schemaVersion           | Optional. Specifies the version of the service definition schema. The schema version allows Visual Studio to select the correct SDK tools to use for schema validation if more than one version of the SDK is installed side-by-side.|
| upgradeDomainCount      | Optional. Specifies the number of upgrade domains across which roles in this service are allocated. Role instances are allocated to an upgrade domain when the service is deployed. For more information, see [Update a cloud service role or deployment](cloud-services-how-to-manage-portal.md#update-a-cloud-service-role-or-deployment).<br /><br /> You can specify up to 20 upgrade domains. If not specified, the default number of upgrade domains is 5.|