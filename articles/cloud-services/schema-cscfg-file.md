---
title: Azure Cloud Services Definition Schema (.cscfg File) | Microsoft Docs
services: cloud-services
ms.custom: ''
ms.date: 12/07/2016
ms.reviewer: ''
ms.service: cloud-services
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 3ddc7fea-3339-4fc0-bdf9-853c32b25f69
caps.latest.revision: 35
author: jpconnock
ms.author: jeconnoc
manager: timlt
ms.openlocfilehash: 96df87a0d49296280140e392509c0d735f904957
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856680"
---
# <a name="azure-cloud-services-config-schema-cscfg-file"></a><span data-ttu-id="d3737-102">Azure Cloud Services Config Schema (.cscfg File)</span><span class="sxs-lookup"><span data-stu-id="d3737-102">Azure Cloud Services Config Schema (.cscfg File)</span></span>
<span data-ttu-id="d3737-103">The service configuration file specifies the number of role instances to deploy for each role in the service, the values of any configuration settings, and the thumbprints for any certificates associated with a role.</span><span class="sxs-lookup"><span data-stu-id="d3737-103">The service configuration file specifies the number of role instances to deploy for each role in the service, the values of any configuration settings, and the thumbprints for any certificates associated with a role.</span></span> <span data-ttu-id="d3737-104">If the service is part of a Virtual Network, configuration information for the network must be provided in the service configuration file, as well as in the virtual networking configuration file.</span><span class="sxs-lookup"><span data-stu-id="d3737-104">If the service is part of a Virtual Network, configuration information for the network must be provided in the service configuration file, as well as in the virtual networking configuration file.</span></span> <span data-ttu-id="d3737-105">The default extension for the service configuration file is .cscfg.</span><span class="sxs-lookup"><span data-stu-id="d3737-105">The default extension for the service configuration file is .cscfg.</span></span>

<span data-ttu-id="d3737-106">The service model is described by the [Cloud Service (classic) Definition Schema](schema-csdef-file.md).</span><span class="sxs-lookup"><span data-stu-id="d3737-106">The service model is described by the [Cloud Service (classic) Definition Schema](schema-csdef-file.md).</span></span>

<span data-ttu-id="d3737-107">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Windows Azure\.NET SDK\<version>\schemas` directory.</span><span class="sxs-lookup"><span data-stu-id="d3737-107">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Windows Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="d3737-108">Replace `<version>` with the installed version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d3737-108">Replace `<version>` with the installed version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="d3737-109">For more information about configuring roles in a service, see [What is the Cloud Service model](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="d3737-109">For more information about configuring roles in a service, see [What is the Cloud Service model](cloud-services-model-and-package.md).</span></span>

## <a name="basic-service-configuration-schema"></a><span data-ttu-id="d3737-110">Basic Service Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="d3737-110">Basic Service Configuration Schema</span></span>
<span data-ttu-id="d3737-111">The basic format of the service configuration file is as follows.</span><span class="sxs-lookup"><span data-stu-id="d3737-111">The basic format of the service configuration file is as follows.</span></span>

```xml
<ServiceConfiguration serviceName="<service-name>" osFamily="<osfamily-number>" osVersion="<os-version>" schemaVersion="<schema-version>">

  <Role …>
    …
  </Role>

  <NetworkConfiguration>
    …
  </NetworkConfiguration>

</ServiceConfiguration>
```

## <a name="schema-definitions"></a><span data-ttu-id="d3737-112">Schema definitions</span><span class="sxs-lookup"><span data-stu-id="d3737-112">Schema definitions</span></span>
<span data-ttu-id="d3737-113">The following topics describe the schema for the `ServiceConfiguration` element:</span><span class="sxs-lookup"><span data-stu-id="d3737-113">The following topics describe the schema for the `ServiceConfiguration` element:</span></span>

- [<span data-ttu-id="d3737-114">Role Schema</span><span class="sxs-lookup"><span data-stu-id="d3737-114">Role Schema</span></span>](schema-cscfg-role.md)
- [<span data-ttu-id="d3737-115">NetworkConfiguration Schema</span><span class="sxs-lookup"><span data-stu-id="d3737-115">NetworkConfiguration Schema</span></span>](schema-cscfg-networkconfiguration.md)

## <a name="service-configuration-namespace"></a><span data-ttu-id="d3737-116">Service Configuration Namespace</span><span class="sxs-lookup"><span data-stu-id="d3737-116">Service Configuration Namespace</span></span>
<span data-ttu-id="d3737-117">The XML namespace for the service configuration file is: `http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="d3737-117">The XML namespace for the service configuration file is: `http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration`.</span></span>

##  <a name="ServiceConfiguration"></a> <span data-ttu-id="d3737-118">ServiceConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="d3737-118">ServiceConfiguration Element</span></span>
<span data-ttu-id="d3737-119">The `ServiceConfiguration` element is the top-level element of the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="d3737-119">The `ServiceConfiguration` element is the top-level element of the service configuration file.</span></span>

<span data-ttu-id="d3737-120">The following table describes the attributes of the `ServiceConfiguration` element.</span><span class="sxs-lookup"><span data-stu-id="d3737-120">The following table describes the attributes of the `ServiceConfiguration` element.</span></span> <span data-ttu-id="d3737-121">All attributes values are string types.</span><span class="sxs-lookup"><span data-stu-id="d3737-121">All attributes values are string types.</span></span>

| <span data-ttu-id="d3737-122">Attribute</span><span class="sxs-lookup"><span data-stu-id="d3737-122">Attribute</span></span> | <span data-ttu-id="d3737-123">Description</span><span class="sxs-lookup"><span data-stu-id="d3737-123">Description</span></span> |
| --------- | ----------- |
|<span data-ttu-id="d3737-124">serviceName</span><span class="sxs-lookup"><span data-stu-id="d3737-124">serviceName</span></span>|<span data-ttu-id="d3737-125">Required.</span><span class="sxs-lookup"><span data-stu-id="d3737-125">Required.</span></span> <span data-ttu-id="d3737-126">The name of the cloud service.</span><span class="sxs-lookup"><span data-stu-id="d3737-126">The name of the cloud service.</span></span> <span data-ttu-id="d3737-127">The name given here must match the name specified in the service definition file.</span><span class="sxs-lookup"><span data-stu-id="d3737-127">The name given here must match the name specified in the service definition file.</span></span>|
|<span data-ttu-id="d3737-128">osFamily</span><span class="sxs-lookup"><span data-stu-id="d3737-128">osFamily</span></span>|<span data-ttu-id="d3737-129">Optional.</span><span class="sxs-lookup"><span data-stu-id="d3737-129">Optional.</span></span> <span data-ttu-id="d3737-130">Specifies the Guest OS that will run on role instances in the cloud service.</span><span class="sxs-lookup"><span data-stu-id="d3737-130">Specifies the Guest OS that will run on role instances in the cloud service.</span></span> <span data-ttu-id="d3737-131">For information about supported Guest OS releases, see [Azure Guest OS Releases and SDK Compatibility Matrix](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="d3737-131">For information about supported Guest OS releases, see [Azure Guest OS Releases and SDK Compatibility Matrix](cloud-services-guestos-update-matrix.md).</span></span><br /><br /> <span data-ttu-id="d3737-132">If you do not include an `osFamily` value and you have not set the `osVersion` attribute to a specific Guest OS version, a default value of 1 is used.</span><span class="sxs-lookup"><span data-stu-id="d3737-132">If you do not include an `osFamily` value and you have not set the `osVersion` attribute to a specific Guest OS version, a default value of 1 is used.</span></span>|
|<span data-ttu-id="d3737-133">osVersion</span><span class="sxs-lookup"><span data-stu-id="d3737-133">osVersion</span></span>|<span data-ttu-id="d3737-134">Optional.</span><span class="sxs-lookup"><span data-stu-id="d3737-134">Optional.</span></span> <span data-ttu-id="d3737-135">Specifies the version of the Guest OS that will run on role instances in the cloud service.</span><span class="sxs-lookup"><span data-stu-id="d3737-135">Specifies the version of the Guest OS that will run on role instances in the cloud service.</span></span> <span data-ttu-id="d3737-136">For more information about Guest OS versions, see [Azure Guest OS Releases and SDK Compatibility Matrix](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="d3737-136">For more information about Guest OS versions, see [Azure Guest OS Releases and SDK Compatibility Matrix](cloud-services-guestos-update-matrix.md).</span></span><br /><br /> <span data-ttu-id="d3737-137">You can specify that the Guest OS should be automatically upgraded to the latest version.</span><span class="sxs-lookup"><span data-stu-id="d3737-137">You can specify that the Guest OS should be automatically upgraded to the latest version.</span></span> <span data-ttu-id="d3737-138">To do this, set the value of the `osVersion` attribute to `*`.</span><span class="sxs-lookup"><span data-stu-id="d3737-138">To do this, set the value of the `osVersion` attribute to `*`.</span></span> <span data-ttu-id="d3737-139">When set to `*`, the role instances are deployed using the latest version of the Guest OS for the specified OS family and will be automatically upgraded when new versions of the Guest OS are released.</span><span class="sxs-lookup"><span data-stu-id="d3737-139">When set to `*`, the role instances are deployed using the latest version of the Guest OS for the specified OS family and will be automatically upgraded when new versions of the Guest OS are released.</span></span><br /><br /> <span data-ttu-id="d3737-140">To specify a specific version manually, use the `Configuration String` from the table in the **Future, Current and Transitional Guest OS Versions** section of [Azure Guest OS Releases and SDK Compatibility Matrix](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="d3737-140">To specify a specific version manually, use the `Configuration String` from the table in the **Future, Current and Transitional Guest OS Versions** section of [Azure Guest OS Releases and SDK Compatibility Matrix](cloud-services-guestos-update-matrix.md).</span></span><br /><br /> <span data-ttu-id="d3737-141">The default value for the `osVersion` attribute is `*`.</span><span class="sxs-lookup"><span data-stu-id="d3737-141">The default value for the `osVersion` attribute is `*`.</span></span>|
|<span data-ttu-id="d3737-142">schemaVersion</span><span class="sxs-lookup"><span data-stu-id="d3737-142">schemaVersion</span></span>|<span data-ttu-id="d3737-143">Optional.</span><span class="sxs-lookup"><span data-stu-id="d3737-143">Optional.</span></span> <span data-ttu-id="d3737-144">Specifies the version of the Service Configuration schema.</span><span class="sxs-lookup"><span data-stu-id="d3737-144">Specifies the version of the Service Configuration schema.</span></span> <span data-ttu-id="d3737-145">The schema version allows Visual Studio to select the correct SDK tools to use for schema validation if more than one version of the SDK is installed side-by-side.</span><span class="sxs-lookup"><span data-stu-id="d3737-145">The schema version allows Visual Studio to select the correct SDK tools to use for schema validation if more than one version of the SDK is installed side-by-side.</span></span> <span data-ttu-id="d3737-146">For more information about schema and version compatibility, see [Azure Guest OS Releases and SDK Compatibility Matrix](cloud-services-guestos-update-matrix.md)</span><span class="sxs-lookup"><span data-stu-id="d3737-146">For more information about schema and version compatibility, see [Azure Guest OS Releases and SDK Compatibility Matrix](cloud-services-guestos-update-matrix.md)</span></span>|

<span data-ttu-id="d3737-147">The service configuration file must contain one `ServiceConfiguration` element.</span><span class="sxs-lookup"><span data-stu-id="d3737-147">The service configuration file must contain one `ServiceConfiguration` element.</span></span> <span data-ttu-id="d3737-148">The `ServiceConfiguration` element may include any number of `Role` elements and zero or 1 `NetworkConfiguration` elements.</span><span class="sxs-lookup"><span data-stu-id="d3737-148">The `ServiceConfiguration` element may include any number of `Role` elements and zero or 1 `NetworkConfiguration` elements.</span></span>