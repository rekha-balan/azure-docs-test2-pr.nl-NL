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
# <a name="azure-cloud-services-definition-schema-csdef-file"></a><span data-ttu-id="053d7-102">Azure Cloud Services Definition Schema (.csdef File)</span><span class="sxs-lookup"><span data-stu-id="053d7-102">Azure Cloud Services Definition Schema (.csdef File)</span></span>
<span data-ttu-id="053d7-103">The service definition file defines the service model for an application.</span><span class="sxs-lookup"><span data-stu-id="053d7-103">The service definition file defines the service model for an application.</span></span> <span data-ttu-id="053d7-104">The file contains the definitions for the roles that are available to a cloud service, specifies the service endpoints, and establishes configuration settings for the service.</span><span class="sxs-lookup"><span data-stu-id="053d7-104">The file contains the definitions for the roles that are available to a cloud service, specifies the service endpoints, and establishes configuration settings for the service.</span></span> <span data-ttu-id="053d7-105">Configuration setting values are set in the service configuration file, as described by the [Cloud Service (classic) Configuration Schema](http://msdn.microsoft.com/library/b1ae68cd-cc95-48cb-a4a4-da91dc708a35).</span><span class="sxs-lookup"><span data-stu-id="053d7-105">Configuration setting values are set in the service configuration file, as described by the [Cloud Service (classic) Configuration Schema](http://msdn.microsoft.com/library/b1ae68cd-cc95-48cb-a4a4-da91dc708a35).</span></span>

<span data-ttu-id="053d7-106">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Windows Azure\.NET SDK\<version>\schemas` directory.</span><span class="sxs-lookup"><span data-stu-id="053d7-106">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Windows Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="053d7-107">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="053d7-107">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>

<span data-ttu-id="053d7-108">The default extension for the service definition file is .csdef.</span><span class="sxs-lookup"><span data-stu-id="053d7-108">The default extension for the service definition file is .csdef.</span></span>

## <a name="basic-service-definition-schema"></a><span data-ttu-id="053d7-109">Basic service definition schema</span><span class="sxs-lookup"><span data-stu-id="053d7-109">Basic service definition schema</span></span>
<span data-ttu-id="053d7-110">The service definition file must contain one `ServiceDefinition` element.</span><span class="sxs-lookup"><span data-stu-id="053d7-110">The service definition file must contain one `ServiceDefinition` element.</span></span> <span data-ttu-id="053d7-111">The service definition must contain at least one role (`WebRole` or `WorkerRole`) element.</span><span class="sxs-lookup"><span data-stu-id="053d7-111">The service definition must contain at least one role (`WebRole` or `WorkerRole`) element.</span></span> <span data-ttu-id="053d7-112">It can contain up to 25 roles defined in a single definition and you can mix role types.</span><span class="sxs-lookup"><span data-stu-id="053d7-112">It can contain up to 25 roles defined in a single definition and you can mix role types.</span></span> <span data-ttu-id="053d7-113">The service definition also contains the optional `NetworkTrafficRules` element which restricts which roles can communicate to specified internal endpoints.</span><span class="sxs-lookup"><span data-stu-id="053d7-113">The service definition also contains the optional `NetworkTrafficRules` element which restricts which roles can communicate to specified internal endpoints.</span></span> <span data-ttu-id="053d7-114">The service definition also contains the optional `LoadBalancerProbes` element which contains customer defined health probes of endpoints.</span><span class="sxs-lookup"><span data-stu-id="053d7-114">The service definition also contains the optional `LoadBalancerProbes` element which contains customer defined health probes of endpoints.</span></span>

<span data-ttu-id="053d7-115">The basic format of the service definition file is as follows.</span><span class="sxs-lookup"><span data-stu-id="053d7-115">The basic format of the service definition file is as follows.</span></span>

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

## <a name="schema-definitions"></a><span data-ttu-id="053d7-116">Schema definitions</span><span class="sxs-lookup"><span data-stu-id="053d7-116">Schema definitions</span></span>
<span data-ttu-id="053d7-117">The following topics describe the schema:</span><span class="sxs-lookup"><span data-stu-id="053d7-117">The following topics describe the schema:</span></span>

- [<span data-ttu-id="053d7-118">LoadBalancerProbe Schema</span><span class="sxs-lookup"><span data-stu-id="053d7-118">LoadBalancerProbe Schema</span></span>](schema-csdef-loadbalancerprobe.md)
- [<span data-ttu-id="053d7-119">WebRole Schema</span><span class="sxs-lookup"><span data-stu-id="053d7-119">WebRole Schema</span></span>](schema-csdef-webrole.md)
- [<span data-ttu-id="053d7-120">WorkerRole Schema</span><span class="sxs-lookup"><span data-stu-id="053d7-120">WorkerRole Schema</span></span>](schema-csdef-workerrole.md)
- [<span data-ttu-id="053d7-121">NetworkTrafficRules Schema</span><span class="sxs-lookup"><span data-stu-id="053d7-121">NetworkTrafficRules Schema</span></span>](schema-csdef-networktrafficrules.md)

##  <a name="ServiceDefinition"></a> <span data-ttu-id="053d7-122">ServiceDefinition Element</span><span class="sxs-lookup"><span data-stu-id="053d7-122">ServiceDefinition Element</span></span>
<span data-ttu-id="053d7-123">The `ServiceDefinition` element is the top-level element of the service definition file.</span><span class="sxs-lookup"><span data-stu-id="053d7-123">The `ServiceDefinition` element is the top-level element of the service definition file.</span></span>

<span data-ttu-id="053d7-124">The following table describes the attributes of the `ServiceDefinition` element.</span><span class="sxs-lookup"><span data-stu-id="053d7-124">The following table describes the attributes of the `ServiceDefinition` element.</span></span>

| <span data-ttu-id="053d7-125">Attribute</span><span class="sxs-lookup"><span data-stu-id="053d7-125">Attribute</span></span>               | <span data-ttu-id="053d7-126">Description</span><span class="sxs-lookup"><span data-stu-id="053d7-126">Description</span></span> |
| ----------------------- | ----------- |
| <span data-ttu-id="053d7-127">name</span><span class="sxs-lookup"><span data-stu-id="053d7-127">name</span></span>                    |<span data-ttu-id="053d7-128">Required.</span><span class="sxs-lookup"><span data-stu-id="053d7-128">Required.</span></span> <span data-ttu-id="053d7-129">The name of the service.</span><span class="sxs-lookup"><span data-stu-id="053d7-129">The name of the service.</span></span> <span data-ttu-id="053d7-130">The name must be unique within the service account.</span><span class="sxs-lookup"><span data-stu-id="053d7-130">The name must be unique within the service account.</span></span>|
| <span data-ttu-id="053d7-131">topologyChangeDiscovery</span><span class="sxs-lookup"><span data-stu-id="053d7-131">topologyChangeDiscovery</span></span> | <span data-ttu-id="053d7-132">Optional.</span><span class="sxs-lookup"><span data-stu-id="053d7-132">Optional.</span></span> <span data-ttu-id="053d7-133">Specifies the type of topology change notification.</span><span class="sxs-lookup"><span data-stu-id="053d7-133">Specifies the type of topology change notification.</span></span> <span data-ttu-id="053d7-134">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="053d7-134">Possible values are:</span></span><br /><br /> <span data-ttu-id="053d7-135">-   `Blast` - Sends the update as soon as possible to all role instances.</span><span class="sxs-lookup"><span data-stu-id="053d7-135">-   `Blast` - Sends the update as soon as possible to all role instances.</span></span> <span data-ttu-id="053d7-136">If you choose option, the role should be able to handle the topology update without being restarted.</span><span class="sxs-lookup"><span data-stu-id="053d7-136">If you choose option, the role should be able to handle the topology update without being restarted.</span></span><br /><span data-ttu-id="053d7-137">-   `UpgradeDomainWalk` – Sends the update to each role instance in a sequential manner after the previous instance has successfully accepted the update.</span><span class="sxs-lookup"><span data-stu-id="053d7-137">-   `UpgradeDomainWalk` – Sends the update to each role instance in a sequential manner after the previous instance has successfully accepted the update.</span></span>|
| <span data-ttu-id="053d7-138">schemaVersion</span><span class="sxs-lookup"><span data-stu-id="053d7-138">schemaVersion</span></span>           | <span data-ttu-id="053d7-139">Optional.</span><span class="sxs-lookup"><span data-stu-id="053d7-139">Optional.</span></span> <span data-ttu-id="053d7-140">Specifies the version of the service definition schema.</span><span class="sxs-lookup"><span data-stu-id="053d7-140">Specifies the version of the service definition schema.</span></span> <span data-ttu-id="053d7-141">The schema version allows Visual Studio to select the correct SDK tools to use for schema validation if more than one version of the SDK is installed side-by-side.</span><span class="sxs-lookup"><span data-stu-id="053d7-141">The schema version allows Visual Studio to select the correct SDK tools to use for schema validation if more than one version of the SDK is installed side-by-side.</span></span>|
| <span data-ttu-id="053d7-142">upgradeDomainCount</span><span class="sxs-lookup"><span data-stu-id="053d7-142">upgradeDomainCount</span></span>      | <span data-ttu-id="053d7-143">Optional.</span><span class="sxs-lookup"><span data-stu-id="053d7-143">Optional.</span></span> <span data-ttu-id="053d7-144">Specifies the number of upgrade domains across which roles in this service are allocated.</span><span class="sxs-lookup"><span data-stu-id="053d7-144">Specifies the number of upgrade domains across which roles in this service are allocated.</span></span> <span data-ttu-id="053d7-145">Role instances are allocated to an upgrade domain when the service is deployed.</span><span class="sxs-lookup"><span data-stu-id="053d7-145">Role instances are allocated to an upgrade domain when the service is deployed.</span></span> <span data-ttu-id="053d7-146">For more information, see [Update a cloud service role or deployment](cloud-services-how-to-manage-portal.md#update-a-cloud-service-role-or-deployment).</span><span class="sxs-lookup"><span data-stu-id="053d7-146">For more information, see [Update a cloud service role or deployment](cloud-services-how-to-manage-portal.md#update-a-cloud-service-role-or-deployment).</span></span><br /><br /> <span data-ttu-id="053d7-147">You can specify up to 20 upgrade domains.</span><span class="sxs-lookup"><span data-stu-id="053d7-147">You can specify up to 20 upgrade domains.</span></span> <span data-ttu-id="053d7-148">If not specified, the default number of upgrade domains is 5.</span><span class="sxs-lookup"><span data-stu-id="053d7-148">If not specified, the default number of upgrade domains is 5.</span></span>|