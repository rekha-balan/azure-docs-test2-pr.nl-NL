---
title: Introduction to Data Science Virtual Machine-based team environments - Azure | Microsoft Docs
description: Patterns for deploying the Data Science VM in an enterprise team environment.
keywords: deep learning, AI, data science tools, data science virtual machine, geospatial analytics, team data science process
services: machine-learning
documentationcenter: ''
author: gopitk
manager: cgronlun
ms.assetid: ''
ms.service: machine-learning
ms.component: data-science-vm
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2018
ms.author: gokuma
ms.openlocfilehash: 8486b0be1fb5e1385da3c7ad55f6410a1059df93
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855716"
---
# <a name="data-science-virtual-machine-based-team-analytics-and-ai-environment"></a><span data-ttu-id="87294-104">Data Science Virtual Machine-based team analytics and AI environment</span><span class="sxs-lookup"><span data-stu-id="87294-104">Data Science Virtual Machine-based team analytics and AI environment</span></span> 
<span data-ttu-id="87294-105">The [Data Science Virtual Machine](overview.md) (DSVM) provides a rich environment in the Azure platform with prebuilt software for artificial intelligence (AI) and data analytics.</span><span class="sxs-lookup"><span data-stu-id="87294-105">The [Data Science Virtual Machine](overview.md) (DSVM) provides a rich environment in the Azure platform with prebuilt software for artificial intelligence (AI) and data analytics.</span></span> 

<span data-ttu-id="87294-106">Traditionally, the DSVM has been used as an individual analytics desktop.</span><span class="sxs-lookup"><span data-stu-id="87294-106">Traditionally, the DSVM has been used as an individual analytics desktop.</span></span> <span data-ttu-id="87294-107">Individual data scientists gain productivity with this shared notion of their prebuilt analytics environment.</span><span class="sxs-lookup"><span data-stu-id="87294-107">Individual data scientists gain productivity with this shared notion of their prebuilt analytics environment.</span></span> <span data-ttu-id="87294-108">As large analytics teams plan their analytics environments for their data scientists and AI developers, one of the recurring themes is a shared analytics infrastructure for development and experimentation.</span><span class="sxs-lookup"><span data-stu-id="87294-108">As large analytics teams plan their analytics environments for their data scientists and AI developers, one of the recurring themes is a shared analytics infrastructure for development and experimentation.</span></span> <span data-ttu-id="87294-109">This infrastructure is managed in line with enterprise IT policies that also facilitate collaboration and consistency across the data science/analytics teams.</span><span class="sxs-lookup"><span data-stu-id="87294-109">This infrastructure is managed in line with enterprise IT policies that also facilitate collaboration and consistency across the data science/analytics teams.</span></span> 

<span data-ttu-id="87294-110">A shared infrastructure also enables IT to better utilize the analytics environment.</span><span class="sxs-lookup"><span data-stu-id="87294-110">A shared infrastructure also enables IT to better utilize the analytics environment.</span></span> <span data-ttu-id="87294-111">Some organizations call the team-based data science/analytics infrastructure an "analytics sandbox."</span><span class="sxs-lookup"><span data-stu-id="87294-111">Some organizations call the team-based data science/analytics infrastructure an "analytics sandbox."</span></span> <span data-ttu-id="87294-112">It enables data scientists to access various data assets to rapidly understand data, run experiments, validate hypotheses, and build predictive models without affecting the production environment.</span><span class="sxs-lookup"><span data-stu-id="87294-112">It enables data scientists to access various data assets to rapidly understand data, run experiments, validate hypotheses, and build predictive models without affecting the production environment.</span></span> 

<span data-ttu-id="87294-113">Because the DSVM operates at the Azure infrastructure level, IT administrators can readily configure the DSVM to operate in compliance with the IT policies of the enterprise.</span><span class="sxs-lookup"><span data-stu-id="87294-113">Because the DSVM operates at the Azure infrastructure level, IT administrators can readily configure the DSVM to operate in compliance with the IT policies of the enterprise.</span></span> <span data-ttu-id="87294-114">The DSVM offers full flexibility in implementing various sharing architectures with access to corporate data assets in a controlled way.</span><span class="sxs-lookup"><span data-stu-id="87294-114">The DSVM offers full flexibility in implementing various sharing architectures with access to corporate data assets in a controlled way.</span></span> 

<span data-ttu-id="87294-115">This section discusses some patterns and guidelines that you can use to deploy the DSVM as a team-based data science infrastructure.</span><span class="sxs-lookup"><span data-stu-id="87294-115">This section discusses some patterns and guidelines that you can use to deploy the DSVM as a team-based data science infrastructure.</span></span> <span data-ttu-id="87294-116">The building blocks for these patterns come from Azure infrastructure as a service (IaaS), so they apply to any Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="87294-116">The building blocks for these patterns come from Azure infrastructure as a service (IaaS), so they apply to any Azure VMs.</span></span> <span data-ttu-id="87294-117">The focus of this series of articles is on applying these standard Azure infrastructure capabilities to the Data Science VM.</span><span class="sxs-lookup"><span data-stu-id="87294-117">The focus of this series of articles is on applying these standard Azure infrastructure capabilities to the Data Science VM.</span></span> 

<span data-ttu-id="87294-118">Some of the key building blocks of an enterprise team analytics environment are:</span><span class="sxs-lookup"><span data-stu-id="87294-118">Some of the key building blocks of an enterprise team analytics environment are:</span></span>

* [<span data-ttu-id="87294-119">Autoscaled pool of Data Science Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="87294-119">Autoscaled pool of Data Science Virtual Machines</span></span>](dsvm-pools.md)
* [<span data-ttu-id="87294-120">Common identity and access to a workspace from any of the DSVMs in the pool</span><span class="sxs-lookup"><span data-stu-id="87294-120">Common identity and access to a workspace from any of the DSVMs in the pool</span></span>](dsvm-common-identity.md)
* [<span data-ttu-id="87294-121">Secure access to data sources</span><span class="sxs-lookup"><span data-stu-id="87294-121">Secure access to data sources</span></span>](dsvm-secure-access-keys.md)


<span data-ttu-id="87294-122">This series of articles provides guidance and pointers for each of the preceding items.</span><span class="sxs-lookup"><span data-stu-id="87294-122">This series of articles provides guidance and pointers for each of the preceding items.</span></span> <span data-ttu-id="87294-123">It doesn't cover all the considerations and needs in deploying DSVM in large enterprise configurations.</span><span class="sxs-lookup"><span data-stu-id="87294-123">It doesn't cover all the considerations and needs in deploying DSVM in large enterprise configurations.</span></span> <span data-ttu-id="87294-124">Here's other Azure documentation that you can use while implementing DSVM instances in your enterprise:</span><span class="sxs-lookup"><span data-stu-id="87294-124">Here's other Azure documentation that you can use while implementing DSVM instances in your enterprise:</span></span> 

* [<span data-ttu-id="87294-125">Network security</span><span class="sxs-lookup"><span data-stu-id="87294-125">Network security</span></span>](https://docs.microsoft.com/azure/security/azure-network-security)
* <span data-ttu-id="87294-126">[Monitoring](https://docs.microsoft.com/azure/virtual-machines/windows/monitor) and [management](https://docs.microsoft.com/azure/virtual-machines/windows/maintenance-and-updates)</span><span class="sxs-lookup"><span data-stu-id="87294-126">[Monitoring](https://docs.microsoft.com/azure/virtual-machines/windows/monitor) and [management](https://docs.microsoft.com/azure/virtual-machines/windows/maintenance-and-updates)</span></span>
* [<span data-ttu-id="87294-127">Logging and auditing</span><span class="sxs-lookup"><span data-stu-id="87294-127">Logging and auditing</span></span>](https://docs.microsoft.com/azure/security/azure-log-audit)
* [<span data-ttu-id="87294-128">Role-based access control</span><span class="sxs-lookup"><span data-stu-id="87294-128">Role-based access control</span></span>](https://docs.microsoft.com/azure/role-based-access-control/overview)
* [<span data-ttu-id="87294-129">Policy setting and enforcement</span><span class="sxs-lookup"><span data-stu-id="87294-129">Policy setting and enforcement</span></span>](https://docs.microsoft.com/azure/azure-policy/azure-policy-introduction)
* [<span data-ttu-id="87294-130">Antimalware</span><span class="sxs-lookup"><span data-stu-id="87294-130">Antimalware</span></span>](https://docs.microsoft.com/azure/security/azure-security-antimalware)
* [<span data-ttu-id="87294-131">Encryption</span><span class="sxs-lookup"><span data-stu-id="87294-131">Encryption</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/encrypt-disks)
* [<span data-ttu-id="87294-132">Data discovery and governance</span><span class="sxs-lookup"><span data-stu-id="87294-132">Data discovery and governance</span></span>](https://docs.microsoft.com/azure/data-catalog/)

<span data-ttu-id="87294-133">The [Azure Architecture Center](https://docs.microsoft.com/en-us/azure/architecture/) provides a detailed end-to-end architecture and patterns for building and managing your cloud-based analytics infrastructure.</span><span class="sxs-lookup"><span data-stu-id="87294-133">The [Azure Architecture Center](https://docs.microsoft.com/en-us/azure/architecture/) provides a detailed end-to-end architecture and patterns for building and managing your cloud-based analytics infrastructure.</span></span> 
