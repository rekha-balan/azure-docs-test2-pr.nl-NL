---
title: Azure Stack Development Kit Architecture | Microsoft Docs
description: Describes the Azure Stack Development Kit (ASDK) architecture.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: 68da3ac0eb135f5956dfea76e186d9c57beea79c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858048"
---
# <a name="microsoft-azure-stack-development-kit-architecture"></a><span data-ttu-id="334ce-103">Microsoft Azure Stack Development Kit architecture</span><span class="sxs-lookup"><span data-stu-id="334ce-103">Microsoft Azure Stack Development Kit architecture</span></span>
<span data-ttu-id="334ce-104">The Azure Stack Development Kit (ASDK) is a single-node deployment of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="334ce-104">The Azure Stack Development Kit (ASDK) is a single-node deployment of Azure Stack.</span></span> <span data-ttu-id="334ce-105">All the components are installed in virtual machines running on a single host machine.</span><span class="sxs-lookup"><span data-stu-id="334ce-105">All the components are installed in virtual machines running on a single host machine.</span></span> 

## <a name="logical-architecture-diagram"></a><span data-ttu-id="334ce-106">Logical architecture diagram</span><span class="sxs-lookup"><span data-stu-id="334ce-106">Logical architecture diagram</span></span>
<span data-ttu-id="334ce-107">The following diagram illustrates the logical architecture of the ASDK and its components.</span><span class="sxs-lookup"><span data-stu-id="334ce-107">The following diagram illustrates the logical architecture of the ASDK and its components.</span></span>

![ASDK architecture](media/asdk-architecture/image1.png)

## <a name="virtual-machine-roles"></a><span data-ttu-id="334ce-109">Virtual machine roles</span><span class="sxs-lookup"><span data-stu-id="334ce-109">Virtual machine roles</span></span>
<span data-ttu-id="334ce-110">The ASDK offers services using the following VMs hosted on the development kit host computer:</span><span class="sxs-lookup"><span data-stu-id="334ce-110">The ASDK offers services using the following VMs hosted on the development kit host computer:</span></span>

| <span data-ttu-id="334ce-111">Name</span><span class="sxs-lookup"><span data-stu-id="334ce-111">Name</span></span> | <span data-ttu-id="334ce-112">Description</span><span class="sxs-lookup"><span data-stu-id="334ce-112">Description</span></span> |
| ----- | ----- |
| <span data-ttu-id="334ce-113">**AzS-ACS01**</span><span class="sxs-lookup"><span data-stu-id="334ce-113">**AzS-ACS01**</span></span> | <span data-ttu-id="334ce-114">Azure Stack storage services.</span><span class="sxs-lookup"><span data-stu-id="334ce-114">Azure Stack storage services.</span></span>|
| <span data-ttu-id="334ce-115">**AzS-ADFS01**</span><span class="sxs-lookup"><span data-stu-id="334ce-115">**AzS-ADFS01**</span></span> | <span data-ttu-id="334ce-116">Active Directory Federation Services (ADFS).</span><span class="sxs-lookup"><span data-stu-id="334ce-116">Active Directory Federation Services (ADFS).</span></span>  |
| <span data-ttu-id="334ce-117">**AzS-BGPNAT01**</span><span class="sxs-lookup"><span data-stu-id="334ce-117">**AzS-BGPNAT01**</span></span> | <span data-ttu-id="334ce-118">Edge router and provides NAT and VPN capabilities for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="334ce-118">Edge router and provides NAT and VPN capabilities for Azure Stack.</span></span> |
| <span data-ttu-id="334ce-119">**AzS-CA01**</span><span class="sxs-lookup"><span data-stu-id="334ce-119">**AzS-CA01**</span></span> | <span data-ttu-id="334ce-120">Certificate authority services for Azure Stack role services.</span><span class="sxs-lookup"><span data-stu-id="334ce-120">Certificate authority services for Azure Stack role services.</span></span>|
| <span data-ttu-id="334ce-121">**AzS-DC01**</span><span class="sxs-lookup"><span data-stu-id="334ce-121">**AzS-DC01**</span></span> | <span data-ttu-id="334ce-122">Active Directory, DNS, and DHCP services for Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="334ce-122">Active Directory, DNS, and DHCP services for Microsoft Azure Stack.</span></span>|
| <span data-ttu-id="334ce-123">**AzS-ERCS01**</span><span class="sxs-lookup"><span data-stu-id="334ce-123">**AzS-ERCS01**</span></span> | <span data-ttu-id="334ce-124">Emergency Recovery Console VM.</span><span class="sxs-lookup"><span data-stu-id="334ce-124">Emergency Recovery Console VM.</span></span> |
| <span data-ttu-id="334ce-125">**AzS-GWY01**</span><span class="sxs-lookup"><span data-stu-id="334ce-125">**AzS-GWY01**</span></span> | <span data-ttu-id="334ce-126">Edge gateway services such as VPN site-to-site connections for tenant networks.</span><span class="sxs-lookup"><span data-stu-id="334ce-126">Edge gateway services such as VPN site-to-site connections for tenant networks.</span></span>|
| <span data-ttu-id="334ce-127">**AzS-NC01**</span><span class="sxs-lookup"><span data-stu-id="334ce-127">**AzS-NC01**</span></span> | <span data-ttu-id="334ce-128">Network Controller, which manages Azure Stack network services.</span><span class="sxs-lookup"><span data-stu-id="334ce-128">Network Controller, which manages Azure Stack network services.</span></span>  |
| <span data-ttu-id="334ce-129">**AzS-SLB01**</span><span class="sxs-lookup"><span data-stu-id="334ce-129">**AzS-SLB01**</span></span> | <span data-ttu-id="334ce-130">Load balancing multiplexer services in Azure Stack for both tenants and Azure Stack infrastructure services.</span><span class="sxs-lookup"><span data-stu-id="334ce-130">Load balancing multiplexer services in Azure Stack for both tenants and Azure Stack infrastructure services.</span></span>  |
| <span data-ttu-id="334ce-131">**AzS-SQL01**</span><span class="sxs-lookup"><span data-stu-id="334ce-131">**AzS-SQL01**</span></span> | <span data-ttu-id="334ce-132">Internal data store for Azure Stack infrastructure roles.</span><span class="sxs-lookup"><span data-stu-id="334ce-132">Internal data store for Azure Stack infrastructure roles.</span></span>  |
| <span data-ttu-id="334ce-133">**AzS-WAS01**</span><span class="sxs-lookup"><span data-stu-id="334ce-133">**AzS-WAS01**</span></span> | <span data-ttu-id="334ce-134">Azure Stack administrative portal and Azure Resource Manager services.</span><span class="sxs-lookup"><span data-stu-id="334ce-134">Azure Stack administrative portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="334ce-135">**AzS-WASP01**</span><span class="sxs-lookup"><span data-stu-id="334ce-135">**AzS-WASP01**</span></span>| <span data-ttu-id="334ce-136">Azure Stack user (tenant) portal and Azure Resource Manager services.</span><span class="sxs-lookup"><span data-stu-id="334ce-136">Azure Stack user (tenant) portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="334ce-137">**AzS-XRP01**</span><span class="sxs-lookup"><span data-stu-id="334ce-137">**AzS-XRP01**</span></span> | <span data-ttu-id="334ce-138">Infrastructure management controller for Microsoft Azure Stack, including the Compute, Network, and Storage resource providers.</span><span class="sxs-lookup"><span data-stu-id="334ce-138">Infrastructure management controller for Microsoft Azure Stack, including the Compute, Network, and Storage resource providers.</span></span>|


## <a name="next-steps"></a><span data-ttu-id="334ce-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="334ce-139">Next steps</span></span>
[<span data-ttu-id="334ce-140">Learn about basic ASDK administration tasks</span><span class="sxs-lookup"><span data-stu-id="334ce-140">Learn about basic ASDK administration tasks</span></span>](asdk-admin-basics.md)
