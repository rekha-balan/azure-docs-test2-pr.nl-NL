---
title: Microsoft Azure Stack Proof Of Concept (POC) architecture | Microsoft Docs
description: View the Microsoft Azure Stack POC architecture.
services: azure-stack
documentationcenter: ''
author: heathl17
manager: byronr
editor: ''
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: helaw
ms.openlocfilehash: 674fbea928b95c995e8896ecdd35cb9adbb1856d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556355"
---
# <a name="microsoft-azure-stack-poc-architecture"></a><span data-ttu-id="1b1d3-103">Microsoft Azure Stack POC architecture</span><span class="sxs-lookup"><span data-stu-id="1b1d3-103">Microsoft Azure Stack POC architecture</span></span>
<span data-ttu-id="1b1d3-104">The Azure Stack POC is a one-node deployment of Azure Stack Technical Preview 3.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-104">The Azure Stack POC is a one-node deployment of Azure Stack Technical Preview 3.</span></span> <span data-ttu-id="1b1d3-105">All the components are installed in virtual machines running on a single host machine.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-105">All the components are installed in virtual machines running on a single host machine.</span></span> 

## <a name="logical-architecture-diagram"></a><span data-ttu-id="1b1d3-106">Logical architecture diagram</span><span class="sxs-lookup"><span data-stu-id="1b1d3-106">Logical architecture diagram</span></span>
<span data-ttu-id="1b1d3-107">The following diagram illustrates the logical architecture of the Azure Stack POC and its components.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-107">The following diagram illustrates the logical architecture of the Azure Stack POC and its components.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-architecture/image1.png)

## <a name="virtual-machine-roles"></a><span data-ttu-id="1b1d3-108">Virtual machine roles</span><span class="sxs-lookup"><span data-stu-id="1b1d3-108">Virtual machine roles</span></span>
<span data-ttu-id="1b1d3-109">The Azure Stack POC offers services using the following VMs on the POC host:</span><span class="sxs-lookup"><span data-stu-id="1b1d3-109">The Azure Stack POC offers services using the following VMs on the POC host:</span></span>

| <span data-ttu-id="1b1d3-110">Name</span><span class="sxs-lookup"><span data-stu-id="1b1d3-110">Name</span></span> | <span data-ttu-id="1b1d3-111">Description</span><span class="sxs-lookup"><span data-stu-id="1b1d3-111">Description</span></span> |
| ----- | ----- |
| <span data-ttu-id="1b1d3-112">**MAS-ACS01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-112">**MAS-ACS01**</span></span> | <span data-ttu-id="1b1d3-113">Azure Stack storage services.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-113">Azure Stack storage services.</span></span>|
| <span data-ttu-id="1b1d3-114">**MAS-ADFS01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-114">**MAS-ADFS01**</span></span> | <span data-ttu-id="1b1d3-115">Active Directory Federation Services (ADFS).</span><span class="sxs-lookup"><span data-stu-id="1b1d3-115">Active Directory Federation Services (ADFS).</span></span>  |
| <span data-ttu-id="1b1d3-116">**MAS-BGPNAT01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-116">**MAS-BGPNAT01**</span></span> | <span data-ttu-id="1b1d3-117">Edge router and provides NAT and VPN capabilities for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-117">Edge router and provides NAT and VPN capabilities for Azure Stack.</span></span> |
| <span data-ttu-id="1b1d3-118">**MAS-CA01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-118">**MAS-CA01**</span></span> | <span data-ttu-id="1b1d3-119">Certificate authority services for Azure Stack role services.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-119">Certificate authority services for Azure Stack role services.</span></span>|
| <span data-ttu-id="1b1d3-120">**MAS-CON01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-120">**MAS-CON01**</span></span> | <span data-ttu-id="1b1d3-121">Console machine available for installing PowerShell, Visual Studio, and other tools.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-121">Console machine available for installing PowerShell, Visual Studio, and other tools.</span></span>|
| <span data-ttu-id="1b1d3-122">**MAS-DC01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-122">**MAS-DC01**</span></span> | <span data-ttu-id="1b1d3-123">Active Directory, DNS, and DHCP services for Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-123">Active Directory, DNS, and DHCP services for Microsoft Azure Stack.</span></span>|
| <span data-ttu-id="1b1d3-124">**MAS-ERCS01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-124">**MAS-ERCS01**</span></span> | <span data-ttu-id="1b1d3-125">Emergency Recovery Console VM.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-125">Emergency Recovery Console VM.</span></span> |
| <span data-ttu-id="1b1d3-126">**MAS-GWY01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-126">**MAS-GWY01**</span></span> | <span data-ttu-id="1b1d3-127">Edge gateway services such as VPN site-to-site connections for tenant networks.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-127">Edge gateway services such as VPN site-to-site connections for tenant networks.</span></span>|
| <span data-ttu-id="1b1d3-128">**MAS-NC01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-128">**MAS-NC01**</span></span> | <span data-ttu-id="1b1d3-129">Network Controller, which manages Azure Stack network services.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-129">Network Controller, which manages Azure Stack network services.</span></span>  |
| <span data-ttu-id="1b1d3-130">**MAS-SLB01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-130">**MAS-SLB01**</span></span> | <span data-ttu-id="1b1d3-131">Load balancing multiplexer services in Azure Stack for both tenants and Azure Stack infrastructure services.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-131">Load balancing multiplexer services in Azure Stack for both tenants and Azure Stack infrastructure services.</span></span>  |
| <span data-ttu-id="1b1d3-132">**MAS-SUS01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-132">**MAS-SUS01**</span></span> | <span data-ttu-id="1b1d3-133">Windows Server Update Services, and responsible for providing updates to other Azure Stack virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-133">Windows Server Update Services, and responsible for providing updates to other Azure Stack virtual machines.</span></span>|
| <span data-ttu-id="1b1d3-134">**MAS-SQL01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-134">**MAS-SQL01**</span></span> | <span data-ttu-id="1b1d3-135">Internal data store for Azure Stack infrastructure roles.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-135">Internal data store for Azure Stack infrastructure roles.</span></span>  |
| <span data-ttu-id="1b1d3-136">**MAS-WAS01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-136">**MAS-WAS01**</span></span> | <span data-ttu-id="1b1d3-137">Azure Stack administrative portal and Azure Resource Manager services.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-137">Azure Stack administrative portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="1b1d3-138">**MAS-WASP01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-138">**MAS-WASP01**</span></span>| <span data-ttu-id="1b1d3-139">Azure Stack user (tenant) portal and Azure Resource Manager services.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-139">Azure Stack user (tenant) portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="1b1d3-140">**MAS-XRP01**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-140">**MAS-XRP01**</span></span> | <span data-ttu-id="1b1d3-141">Infrastructure management controller for Microsoft Azure Stack, including the Compute, Network, and Storage resource providers.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-141">Infrastructure management controller for Microsoft Azure Stack, including the Compute, Network, and Storage resource providers.</span></span>|

## <a name="storage-services"></a><span data-ttu-id="1b1d3-142">Storage services</span><span class="sxs-lookup"><span data-stu-id="1b1d3-142">Storage services</span></span>
<span data-ttu-id="1b1d3-143">**Virtual Disk**, **Storage Space**, and **Storage Spaces Direct** are the respective underlying storage technology in Windows Server that enable the Microsoft Azure Stack storage resource provider.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-143">**Virtual Disk**, **Storage Space**, and **Storage Spaces Direct** are the respective underlying storage technology in Windows Server that enable the Microsoft Azure Stack storage resource provider.</span></span>  <span data-ttu-id="1b1d3-144">Additional storage services installed in the operating system on the physical host include:</span><span class="sxs-lookup"><span data-stu-id="1b1d3-144">Additional storage services installed in the operating system on the physical host include:</span></span>

| <span data-ttu-id="1b1d3-145">Name</span><span class="sxs-lookup"><span data-stu-id="1b1d3-145">Name</span></span> | <span data-ttu-id="1b1d3-146">Description</span><span class="sxs-lookup"><span data-stu-id="1b1d3-146">Description</span></span> |
| ----- | ----- |
| <span data-ttu-id="1b1d3-147">**ACS Blob Service**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-147">**ACS Blob Service**</span></span> | <span data-ttu-id="1b1d3-148">Azure Consistent Storage Blob service, which provides blob and table storage services.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-148">Azure Consistent Storage Blob service, which provides blob and table storage services.</span></span> |
| <span data-ttu-id="1b1d3-149">**SoFS**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-149">**SoFS**</span></span> | <span data-ttu-id="1b1d3-150">Scale-out File Server.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-150">Scale-out File Server.</span></span>|
| <span data-ttu-id="1b1d3-151">**ReFS CSV**</span><span class="sxs-lookup"><span data-stu-id="1b1d3-151">**ReFS CSV**</span></span> |<span data-ttu-id="1b1d3-152">Resilient File System Cluster Shared Volume.</span><span class="sxs-lookup"><span data-stu-id="1b1d3-152">Resilient File System Cluster Shared Volume.</span></span>|


## <a name="next-steps"></a><span data-ttu-id="1b1d3-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b1d3-153">Next steps</span></span>
[<span data-ttu-id="1b1d3-154">Deploy Azure Stack</span><span class="sxs-lookup"><span data-stu-id="1b1d3-154">Deploy Azure Stack</span></span>](azure-stack-deploy.md)

[<span data-ttu-id="1b1d3-155">First scenarios to try</span><span class="sxs-lookup"><span data-stu-id="1b1d3-155">First scenarios to try</span></span>](azure-stack-first-scenarios.md)


