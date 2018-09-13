---
title: Resource groups for Linux VMs in Azure | Microsoft Docs
description: Learn about the key design and implementation guidelines for deploying Resource Groups in Azure infrastructure services.
documentationcenter: ''
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 93ab9d93-965a-46b9-9c87-a10d652a6422
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fbdce33f54396ef33b860d67c947456d73a162dc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661547"
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a><span data-ttu-id="a2483-103">Azure resource group guidelines for Linux VMs</span><span class="sxs-lookup"><span data-stu-id="a2483-103">Azure resource group guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="a2483-104">This article focuses on understanding how to logically build out your environment and group all the components in Resource Groups.</span><span class="sxs-lookup"><span data-stu-id="a2483-104">This article focuses on understanding how to logically build out your environment and group all the components in Resource Groups.</span></span>

## <a name="implementation-guidelines-for-resource-groups"></a><span data-ttu-id="a2483-105">Implementation guidelines for Resource Groups</span><span class="sxs-lookup"><span data-stu-id="a2483-105">Implementation guidelines for Resource Groups</span></span>
<span data-ttu-id="a2483-106">Decisions:</span><span class="sxs-lookup"><span data-stu-id="a2483-106">Decisions:</span></span>

* <span data-ttu-id="a2483-107">Are you going to build out Resource Groups by the core infrastructure components, or by complete application deployment?</span><span class="sxs-lookup"><span data-stu-id="a2483-107">Are you going to build out Resource Groups by the core infrastructure components, or by complete application deployment?</span></span>
* <span data-ttu-id="a2483-108">Do you need to restrict access to Resource Groups using Role-Based Access Controls?</span><span class="sxs-lookup"><span data-stu-id="a2483-108">Do you need to restrict access to Resource Groups using Role-Based Access Controls?</span></span>

<span data-ttu-id="a2483-109">Tasks:</span><span class="sxs-lookup"><span data-stu-id="a2483-109">Tasks:</span></span>

* <span data-ttu-id="a2483-110">Define what core infrastructure components and dedicated Resource Groups you need.</span><span class="sxs-lookup"><span data-stu-id="a2483-110">Define what core infrastructure components and dedicated Resource Groups you need.</span></span>
* <span data-ttu-id="a2483-111">Review how to implement Resource Manager templates for consistent, reproducible deployments.</span><span class="sxs-lookup"><span data-stu-id="a2483-111">Review how to implement Resource Manager templates for consistent, reproducible deployments.</span></span>
* <span data-ttu-id="a2483-112">Define what user access roles you need for controlling access to Resource Groups.</span><span class="sxs-lookup"><span data-stu-id="a2483-112">Define what user access roles you need for controlling access to Resource Groups.</span></span>
* <span data-ttu-id="a2483-113">Create the set of Resource Groups using your naming convention.</span><span class="sxs-lookup"><span data-stu-id="a2483-113">Create the set of Resource Groups using your naming convention.</span></span> <span data-ttu-id="a2483-114">You can use the Azure CLI or portal.</span><span class="sxs-lookup"><span data-stu-id="a2483-114">You can use the Azure CLI or portal.</span></span>

## <a name="resource-groups"></a><span data-ttu-id="a2483-115">Resource Groups</span><span class="sxs-lookup"><span data-stu-id="a2483-115">Resource Groups</span></span>
<span data-ttu-id="a2483-116">In Azure, you logically group related resources such as storage accounts, virtual networks, and virtual machines (VMs) to deploy, manage, and maintain them as a single entity.</span><span class="sxs-lookup"><span data-stu-id="a2483-116">In Azure, you logically group related resources such as storage accounts, virtual networks, and virtual machines (VMs) to deploy, manage, and maintain them as a single entity.</span></span> <span data-ttu-id="a2483-117">This approach makes it easier to deploy applications while keeping all the related resources together from a management perspective, or to grant others access to that group of resources.</span><span class="sxs-lookup"><span data-stu-id="a2483-117">This approach makes it easier to deploy applications while keeping all the related resources together from a management perspective, or to grant others access to that group of resources.</span></span> <span data-ttu-id="a2483-118">For a more comprehensive understanding of Resource Groups, you can read the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2483-118">For a more comprehensive understanding of Resource Groups, you can read the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="a2483-119">A key feature to Resource Groups is the ability to build your environment using a JSON file that declares the storage, networking, and compute resources.</span><span class="sxs-lookup"><span data-stu-id="a2483-119">A key feature to Resource Groups is the ability to build your environment using a JSON file that declares the storage, networking, and compute resources.</span></span> <span data-ttu-id="a2483-120">You can also define any related custom scripts or configurations to apply.</span><span class="sxs-lookup"><span data-stu-id="a2483-120">You can also define any related custom scripts or configurations to apply.</span></span> <span data-ttu-id="a2483-121">By using these JSON templates, you create consistent, reproducible deployments for your applications.</span><span class="sxs-lookup"><span data-stu-id="a2483-121">By using these JSON templates, you create consistent, reproducible deployments for your applications.</span></span> <span data-ttu-id="a2483-122">This approach lets you build an environment in development and then use that same template to create a production deployment, or vice versa.</span><span class="sxs-lookup"><span data-stu-id="a2483-122">This approach lets you build an environment in development and then use that same template to create a production deployment, or vice versa.</span></span> <span data-ttu-id="a2483-123">For a better understanding about using templates, read [the template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md) that guides you through each step of building out a JSON template.</span><span class="sxs-lookup"><span data-stu-id="a2483-123">For a better understanding about using templates, read [the template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md) that guides you through each step of building out a JSON template.</span></span>

<span data-ttu-id="a2483-124">There are two different approaches you can take when designing your environment with Resource Groups:</span><span class="sxs-lookup"><span data-stu-id="a2483-124">There are two different approaches you can take when designing your environment with Resource Groups:</span></span>

* <span data-ttu-id="a2483-125">Resource Groups for each application deployment that combines the storage accounts, virtual networks, and subnets, VMs, load balancers, etc.</span><span class="sxs-lookup"><span data-stu-id="a2483-125">Resource Groups for each application deployment that combines the storage accounts, virtual networks, and subnets, VMs, load balancers, etc.</span></span>
* <span data-ttu-id="a2483-126">Centralized Resource Groups that contain your core virtual networking and subnets or storage accounts.</span><span class="sxs-lookup"><span data-stu-id="a2483-126">Centralized Resource Groups that contain your core virtual networking and subnets or storage accounts.</span></span> <span data-ttu-id="a2483-127">Your applications are then in their own Resource Groups that only contain VMs, load balancers, network interfaces, etc.</span><span class="sxs-lookup"><span data-stu-id="a2483-127">Your applications are then in their own Resource Groups that only contain VMs, load balancers, network interfaces, etc.</span></span>

<span data-ttu-id="a2483-128">As you scale out, creating centralized Resource Groups for your virtual networking and subnets makes it easier to build cross-premises network connections for hybrid connectivity options.</span><span class="sxs-lookup"><span data-stu-id="a2483-128">As you scale out, creating centralized Resource Groups for your virtual networking and subnets makes it easier to build cross-premises network connections for hybrid connectivity options.</span></span> <span data-ttu-id="a2483-129">The alternative approach is for each application to have their own virtual network that requires configuration and maintenance.</span><span class="sxs-lookup"><span data-stu-id="a2483-129">The alternative approach is for each application to have their own virtual network that requires configuration and maintenance.</span></span> <span data-ttu-id="a2483-130">[Role-Based Access Controls](../../active-directory/role-based-access-control-what-is.md) provide a granular way to control access to Resource Groups.</span><span class="sxs-lookup"><span data-stu-id="a2483-130">[Role-Based Access Controls](../../active-directory/role-based-access-control-what-is.md) provide a granular way to control access to Resource Groups.</span></span> <span data-ttu-id="a2483-131">For production applications, you can control the users that may access those resources, or for the core infrastructure resources you can limit only infrastructure engineers to work with them.</span><span class="sxs-lookup"><span data-stu-id="a2483-131">For production applications, you can control the users that may access those resources, or for the core infrastructure resources you can limit only infrastructure engineers to work with them.</span></span> <span data-ttu-id="a2483-132">Your application owners only have access to the application components within their Resource Group and not the core Azure infrastructure of your environment.</span><span class="sxs-lookup"><span data-stu-id="a2483-132">Your application owners only have access to the application components within their Resource Group and not the core Azure infrastructure of your environment.</span></span> <span data-ttu-id="a2483-133">As you design your environment, consider the users that require access to the resources and design your Resource Groups accordingly.</span><span class="sxs-lookup"><span data-stu-id="a2483-133">As you design your environment, consider the users that require access to the resources and design your Resource Groups accordingly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a2483-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2483-134">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

