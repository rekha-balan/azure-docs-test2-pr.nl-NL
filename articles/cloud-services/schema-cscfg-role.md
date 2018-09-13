---
title: Azure Cloud Services Role Schema | Microsoft Docs
ms.custom: ''
ms.date: 12/07/2016
services: cloud-services
ms.reviewer: ''
ms.service: cloud-services
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e4fbffc1-98eb-449c-971c-de415e45ab34
caps.latest.revision: 12
author: jpconnock
ms.author: jeconnoc
manager: timlt
ms.openlocfilehash: 20f4186426152d2dc9b445981a69881c35587eb6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870435"
---
# <a name="azure-cloud-services-config-role-schema"></a><span data-ttu-id="6ed01-102">Azure Cloud Services Config Role Schema</span><span class="sxs-lookup"><span data-stu-id="6ed01-102">Azure Cloud Services Config Role Schema</span></span>

<span data-ttu-id="6ed01-103">The `Role` element of the configuration file specifies the number of role instances to deploy for each role in the service, the values of any configuration settings, and the thumbprints for any certificates associated with a role.</span><span class="sxs-lookup"><span data-stu-id="6ed01-103">The `Role` element of the configuration file specifies the number of role instances to deploy for each role in the service, the values of any configuration settings, and the thumbprints for any certificates associated with a role.</span></span>

<span data-ttu-id="6ed01-104">For more information about the Azure Service Configuration Schema, see [Cloud Service (classic) Configuration Schema](schema-cscfg-file.md).</span><span class="sxs-lookup"><span data-stu-id="6ed01-104">For more information about the Azure Service Configuration Schema, see [Cloud Service (classic) Configuration Schema](schema-cscfg-file.md).</span></span> <span data-ttu-id="6ed01-105">For more information about the Azure Service Definition Schema, see [Cloud Service (classic) Definition Schema](schema-csdef-file.md).</span><span class="sxs-lookup"><span data-stu-id="6ed01-105">For more information about the Azure Service Definition Schema, see [Cloud Service (classic) Definition Schema](schema-csdef-file.md).</span></span>

##  <a name="Role"></a> <span data-ttu-id="6ed01-106">Role Element</span><span class="sxs-lookup"><span data-stu-id="6ed01-106">Role Element</span></span>
<span data-ttu-id="6ed01-107">The following example shows the `Role` element and its child elements.</span><span class="sxs-lookup"><span data-stu-id="6ed01-107">The following example shows the `Role` element and its child elements.</span></span>

```xml 
<ServiceConfiguration>
  <Role name="<role-name>" vmName="<vm-name>">
    <Instances count="<number-of-instances>"/>
    <ConfigurationSettings>
      <Setting name="<setting-name>" value="<setting-value>" />
    </ConfigurationSettings>
    <Certificates>
      <Certificate name="<certificate-name>" thumbprint="<certificate-thumbprint>" thumbprintAlgorithm="<algorithm>"/>
    </Certificates>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="6ed01-108">The following table describes the attributes for the `Role` element.</span><span class="sxs-lookup"><span data-stu-id="6ed01-108">The following table describes the attributes for the `Role` element.</span></span>

| <span data-ttu-id="6ed01-109">Attribute</span><span class="sxs-lookup"><span data-stu-id="6ed01-109">Attribute</span></span> | <span data-ttu-id="6ed01-110">Description</span><span class="sxs-lookup"><span data-stu-id="6ed01-110">Description</span></span> |
| --------- | ----------- |
| <span data-ttu-id="6ed01-111">name</span><span class="sxs-lookup"><span data-stu-id="6ed01-111">name</span></span>   | <span data-ttu-id="6ed01-112">Required.</span><span class="sxs-lookup"><span data-stu-id="6ed01-112">Required.</span></span> <span data-ttu-id="6ed01-113">Specifies the name of the role.</span><span class="sxs-lookup"><span data-stu-id="6ed01-113">Specifies the name of the role.</span></span> <span data-ttu-id="6ed01-114">The name must match the name provided for the role in the service definition file.</span><span class="sxs-lookup"><span data-stu-id="6ed01-114">The name must match the name provided for the role in the service definition file.</span></span>|
| <span data-ttu-id="6ed01-115">vmName</span><span class="sxs-lookup"><span data-stu-id="6ed01-115">vmName</span></span> | <span data-ttu-id="6ed01-116">Optional.</span><span class="sxs-lookup"><span data-stu-id="6ed01-116">Optional.</span></span> <span data-ttu-id="6ed01-117">Specifies the DNS name for a Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="6ed01-117">Specifies the DNS name for a Virtual Machine.</span></span> <span data-ttu-id="6ed01-118">The name must be 10 characters or less.</span><span class="sxs-lookup"><span data-stu-id="6ed01-118">The name must be 10 characters or less.</span></span>|

<span data-ttu-id="6ed01-119">The following table describes the child elements of the `Role` element.</span><span class="sxs-lookup"><span data-stu-id="6ed01-119">The following table describes the child elements of the `Role` element.</span></span>

| <span data-ttu-id="6ed01-120">Element</span><span class="sxs-lookup"><span data-stu-id="6ed01-120">Element</span></span> | <span data-ttu-id="6ed01-121">Description</span><span class="sxs-lookup"><span data-stu-id="6ed01-121">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="6ed01-122">Instances</span><span class="sxs-lookup"><span data-stu-id="6ed01-122">Instances</span></span> | <span data-ttu-id="6ed01-123">Required.</span><span class="sxs-lookup"><span data-stu-id="6ed01-123">Required.</span></span> <span data-ttu-id="6ed01-124">Specifies the number of instances to deploy for the role.</span><span class="sxs-lookup"><span data-stu-id="6ed01-124">Specifies the number of instances to deploy for the role.</span></span> <span data-ttu-id="6ed01-125">The number of instances is defined by an integer for the `count` attribute.</span><span class="sxs-lookup"><span data-stu-id="6ed01-125">The number of instances is defined by an integer for the `count` attribute.</span></span>|
| <span data-ttu-id="6ed01-126">Setting</span><span class="sxs-lookup"><span data-stu-id="6ed01-126">Setting</span></span>   | <span data-ttu-id="6ed01-127">Optional.</span><span class="sxs-lookup"><span data-stu-id="6ed01-127">Optional.</span></span> <span data-ttu-id="6ed01-128">Specifies a setting name and value in a collection of settings for a role.</span><span class="sxs-lookup"><span data-stu-id="6ed01-128">Specifies a setting name and value in a collection of settings for a role.</span></span> <span data-ttu-id="6ed01-129">The setting name is defined by a string for the `name` attribute and the setting value is defined by a string for the `value` attribute.</span><span class="sxs-lookup"><span data-stu-id="6ed01-129">The setting name is defined by a string for the `name` attribute and the setting value is defined by a string for the `value` attribute.</span></span>|
| <span data-ttu-id="6ed01-130">Certificate</span><span class="sxs-lookup"><span data-stu-id="6ed01-130">Certificate</span></span> | <span data-ttu-id="6ed01-131">Optional.</span><span class="sxs-lookup"><span data-stu-id="6ed01-131">Optional.</span></span> <span data-ttu-id="6ed01-132">Specifies the name, thumbprint, and algorithm of a service certificate that is to be associated with the role.</span><span class="sxs-lookup"><span data-stu-id="6ed01-132">Specifies the name, thumbprint, and algorithm of a service certificate that is to be associated with the role.</span></span> <span data-ttu-id="6ed01-133">The certificate name is defined by a string for the `name` attribute.</span><span class="sxs-lookup"><span data-stu-id="6ed01-133">The certificate name is defined by a string for the `name` attribute.</span></span> <span data-ttu-id="6ed01-134">The certificate thumbprint is defined by a string of hexadecimal numbers containing no spaces for the `thumbprint` attribute.</span><span class="sxs-lookup"><span data-stu-id="6ed01-134">The certificate thumbprint is defined by a string of hexadecimal numbers containing no spaces for the `thumbprint` attribute.</span></span> <span data-ttu-id="6ed01-135">The hexadecimal numbers must be represented using digits and uppercase alpha characters.</span><span class="sxs-lookup"><span data-stu-id="6ed01-135">The hexadecimal numbers must be represented using digits and uppercase alpha characters.</span></span> <span data-ttu-id="6ed01-136">The certificate algorithm is defined by a string for the `thumbprintAlgorithm` attribute.</span><span class="sxs-lookup"><span data-stu-id="6ed01-136">The certificate algorithm is defined by a string for the `thumbprintAlgorithm` attribute.</span></span>|

## <a name="see-also"></a><span data-ttu-id="6ed01-137">See Also</span><span class="sxs-lookup"><span data-stu-id="6ed01-137">See Also</span></span>
[<span data-ttu-id="6ed01-138">Cloud Service (classic) Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="6ed01-138">Cloud Service (classic) Configuration Schema</span></span>](schema-cscfg-file.md)