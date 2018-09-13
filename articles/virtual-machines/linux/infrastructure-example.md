---
title: Example Azure Infrastructure Walkthrough | Microsoft Docs
description: Learn about the key design and implementation guidelines for deploying an example infrastructure in Azure.
documentationcenter: ''
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4295e8c572f5585c0d51eba52d7e70a658491ff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551034"
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a><span data-ttu-id="e8340-103">Example Azure infrastructure walkthrough for Linux VMs</span><span class="sxs-lookup"><span data-stu-id="e8340-103">Example Azure infrastructure walkthrough for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="e8340-104">This article walks through building out an example application infrastructure.</span><span class="sxs-lookup"><span data-stu-id="e8340-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="e8340-105">We detail designing an infrastructure for a simple on-line store that brings together all the guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="e8340-105">We detail designing an infrastructure for a simple on-line store that brings together all the guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="e8340-106">Example workload</span><span class="sxs-lookup"><span data-stu-id="e8340-106">Example workload</span></span>
<span data-ttu-id="e8340-107">Adventure Works Cycles wants to build an on-line store application in Azure that consists of:</span><span class="sxs-lookup"><span data-stu-id="e8340-107">Adventure Works Cycles wants to build an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="e8340-108">Two nginx servers running the client front-end in a web tier</span><span class="sxs-lookup"><span data-stu-id="e8340-108">Two nginx servers running the client front-end in a web tier</span></span>
* <span data-ttu-id="e8340-109">Two nginx servers processing data and orders in an application tier</span><span class="sxs-lookup"><span data-stu-id="e8340-109">Two nginx servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="e8340-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span><span class="sxs-lookup"><span data-stu-id="e8340-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="e8340-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span><span class="sxs-lookup"><span data-stu-id="e8340-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="e8340-112">All the servers are located in two subnets:</span><span class="sxs-lookup"><span data-stu-id="e8340-112">All the servers are located in two subnets:</span></span>
  * <span data-ttu-id="e8340-113">a front-end subnet for the web servers</span><span class="sxs-lookup"><span data-stu-id="e8340-113">a front-end subnet for the web servers</span></span> 
  * <span data-ttu-id="e8340-114">a back-end subnet for the application servers, MongoDB cluster, and domain controllers</span><span class="sxs-lookup"><span data-stu-id="e8340-114">a back-end subnet for the application servers, MongoDB cluster, and domain controllers</span></span>

![Diagram of different tiers for application infrastructure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/infrastructure-example/example-tiers.png)

<span data-ttu-id="e8340-116">Incoming secure web traffic must be load-balanced among the web servers as customers browse the on-line store.</span><span class="sxs-lookup"><span data-stu-id="e8340-116">Incoming secure web traffic must be load-balanced among the web servers as customers browse the on-line store.</span></span> <span data-ttu-id="e8340-117">Order processing traffic in the form of HTTP requests from the web servers must be load-balanced among the application servers.</span><span class="sxs-lookup"><span data-stu-id="e8340-117">Order processing traffic in the form of HTTP requests from the web servers must be load-balanced among the application servers.</span></span> <span data-ttu-id="e8340-118">Additionally, the infrastructure must be designed for high availability.</span><span class="sxs-lookup"><span data-stu-id="e8340-118">Additionally, the infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="e8340-119">The resulting design must incorporate:</span><span class="sxs-lookup"><span data-stu-id="e8340-119">The resulting design must incorporate:</span></span>

* <span data-ttu-id="e8340-120">An Azure subscription and account</span><span class="sxs-lookup"><span data-stu-id="e8340-120">An Azure subscription and account</span></span>
* <span data-ttu-id="e8340-121">A single resource group</span><span class="sxs-lookup"><span data-stu-id="e8340-121">A single resource group</span></span>
* <span data-ttu-id="e8340-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="e8340-122">Azure Managed Disks</span></span>
* <span data-ttu-id="e8340-123">A virtual network with two subnets</span><span class="sxs-lookup"><span data-stu-id="e8340-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="e8340-124">Availability sets for the VMs with a similar role</span><span class="sxs-lookup"><span data-stu-id="e8340-124">Availability sets for the VMs with a similar role</span></span>
* <span data-ttu-id="e8340-125">Virtual machines</span><span class="sxs-lookup"><span data-stu-id="e8340-125">Virtual machines</span></span>

<span data-ttu-id="e8340-126">All the above follow these naming conventions:</span><span class="sxs-lookup"><span data-stu-id="e8340-126">All the above follow these naming conventions:</span></span>

* <span data-ttu-id="e8340-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span><span class="sxs-lookup"><span data-stu-id="e8340-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="e8340-128">For this example, "**azos**" (Azure On-line Store) is the IT workload name and "**use**" (East US 2) is the location</span><span class="sxs-lookup"><span data-stu-id="e8340-128">For this example, "**azos**" (Azure On-line Store) is the IT workload name and "**use**" (East US 2) is the location</span></span>
* <span data-ttu-id="e8340-129">Virtual networks use AZOS-USE-VN **[number]**</span><span class="sxs-lookup"><span data-stu-id="e8340-129">Virtual networks use AZOS-USE-VN **[number]**</span></span>
* <span data-ttu-id="e8340-130">Availability sets use azos-use-as-**[role]**</span><span class="sxs-lookup"><span data-stu-id="e8340-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="e8340-131">Virtual machine names use azos-use-vm-**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="e8340-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="e8340-132">Azure subscriptions and accounts</span><span class="sxs-lookup"><span data-stu-id="e8340-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="e8340-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, to provide billing for this IT workload.</span><span class="sxs-lookup"><span data-stu-id="e8340-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, to provide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="e8340-134">Storage</span><span class="sxs-lookup"><span data-stu-id="e8340-134">Storage</span></span>
<span data-ttu-id="e8340-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="e8340-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="e8340-136">When creating VMs, both storage available storage tiers are used:</span><span class="sxs-lookup"><span data-stu-id="e8340-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="e8340-137">**Standard storage** for the web servers, application servers, and domain controllers and their data disks.</span><span class="sxs-lookup"><span data-stu-id="e8340-137">**Standard storage** for the web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="e8340-138">**Premium storage** for the MongoDB sharded cluster servers and their data disks.</span><span class="sxs-lookup"><span data-stu-id="e8340-138">**Premium storage** for the MongoDB sharded cluster servers and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="e8340-139">Virtual network and subnets</span><span class="sxs-lookup"><span data-stu-id="e8340-139">Virtual network and subnets</span></span>
<span data-ttu-id="e8340-140">Because the virtual network does not need ongoing connectivity to the Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span><span class="sxs-lookup"><span data-stu-id="e8340-140">Because the virtual network does not need ongoing connectivity to the Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="e8340-141">They created a cloud-only virtual network with the following settings using the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="e8340-141">They created a cloud-only virtual network with the following settings using the Azure portal:</span></span>

* <span data-ttu-id="e8340-142">Name: AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="e8340-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="e8340-143">Location: East US 2</span><span class="sxs-lookup"><span data-stu-id="e8340-143">Location: East US 2</span></span>
* <span data-ttu-id="e8340-144">Virtual network address space: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="e8340-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="e8340-145">First subnet:</span><span class="sxs-lookup"><span data-stu-id="e8340-145">First subnet:</span></span>
  * <span data-ttu-id="e8340-146">Name: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="e8340-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="e8340-147">Address space: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="e8340-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="e8340-148">Second subnet:</span><span class="sxs-lookup"><span data-stu-id="e8340-148">Second subnet:</span></span>
  * <span data-ttu-id="e8340-149">Name: BackEnd</span><span class="sxs-lookup"><span data-stu-id="e8340-149">Name: BackEnd</span></span>
  * <span data-ttu-id="e8340-150">Address space: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="e8340-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="e8340-151">Availability sets</span><span class="sxs-lookup"><span data-stu-id="e8340-151">Availability sets</span></span>
<span data-ttu-id="e8340-152">To maintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span><span class="sxs-lookup"><span data-stu-id="e8340-152">To maintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="e8340-153">**azos-use-as-web** for the web servers</span><span class="sxs-lookup"><span data-stu-id="e8340-153">**azos-use-as-web** for the web servers</span></span>
* <span data-ttu-id="e8340-154">**azos-use-as-app** for the application servers</span><span class="sxs-lookup"><span data-stu-id="e8340-154">**azos-use-as-app** for the application servers</span></span>
* <span data-ttu-id="e8340-155">**azos-use-as-db** for the servers in the MongoDB sharded cluster</span><span class="sxs-lookup"><span data-stu-id="e8340-155">**azos-use-as-db** for the servers in the MongoDB sharded cluster</span></span>
* <span data-ttu-id="e8340-156">**azos-use-as-dc** for the domain controllers</span><span class="sxs-lookup"><span data-stu-id="e8340-156">**azos-use-as-dc** for the domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="e8340-157">Virtual machines</span><span class="sxs-lookup"><span data-stu-id="e8340-157">Virtual machines</span></span>
<span data-ttu-id="e8340-158">Adventure Works Cycles decided on the following names for their Azure VMs:</span><span class="sxs-lookup"><span data-stu-id="e8340-158">Adventure Works Cycles decided on the following names for their Azure VMs:</span></span>

* <span data-ttu-id="e8340-159">**azos-use-vm-web01** for the first web server</span><span class="sxs-lookup"><span data-stu-id="e8340-159">**azos-use-vm-web01** for the first web server</span></span>
* <span data-ttu-id="e8340-160">**azos-use-vm-web02** for the second web server</span><span class="sxs-lookup"><span data-stu-id="e8340-160">**azos-use-vm-web02** for the second web server</span></span>
* <span data-ttu-id="e8340-161">**azos-use-vm-app01** for the first application server</span><span class="sxs-lookup"><span data-stu-id="e8340-161">**azos-use-vm-app01** for the first application server</span></span>
* <span data-ttu-id="e8340-162">**azos-use-vm-app02** for the second application server</span><span class="sxs-lookup"><span data-stu-id="e8340-162">**azos-use-vm-app02** for the second application server</span></span>
* <span data-ttu-id="e8340-163">**azos-use-vm-db01** for the first MongoDB server in the cluster</span><span class="sxs-lookup"><span data-stu-id="e8340-163">**azos-use-vm-db01** for the first MongoDB server in the cluster</span></span>
* <span data-ttu-id="e8340-164">**azos-use-vm-db02** for the second MongoDB server in the cluster</span><span class="sxs-lookup"><span data-stu-id="e8340-164">**azos-use-vm-db02** for the second MongoDB server in the cluster</span></span>
* <span data-ttu-id="e8340-165">**azos-use-vm-dc01** for the first domain controller</span><span class="sxs-lookup"><span data-stu-id="e8340-165">**azos-use-vm-dc01** for the first domain controller</span></span>
* <span data-ttu-id="e8340-166">**azos-use-vm-dc02** for the second domain controller</span><span class="sxs-lookup"><span data-stu-id="e8340-166">**azos-use-vm-dc02** for the second domain controller</span></span>

<span data-ttu-id="e8340-167">Here is the resulting configuration.</span><span class="sxs-lookup"><span data-stu-id="e8340-167">Here is the resulting configuration.</span></span>

![Final application infrastructure deployed in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/infrastructure-example/example-config.png)

<span data-ttu-id="e8340-169">This configuration incorporates:</span><span class="sxs-lookup"><span data-stu-id="e8340-169">This configuration incorporates:</span></span>

* <span data-ttu-id="e8340-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span><span class="sxs-lookup"><span data-stu-id="e8340-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="e8340-171">Azure Managed Disks using both Standard and Premium disks</span><span class="sxs-lookup"><span data-stu-id="e8340-171">Azure Managed Disks using both Standard and Premium disks</span></span>
* <span data-ttu-id="e8340-172">Four availability sets, one for each tier of the on-line store</span><span class="sxs-lookup"><span data-stu-id="e8340-172">Four availability sets, one for each tier of the on-line store</span></span>
* <span data-ttu-id="e8340-173">The virtual machines for the four tiers</span><span class="sxs-lookup"><span data-stu-id="e8340-173">The virtual machines for the four tiers</span></span>
* <span data-ttu-id="e8340-174">An external load balanced set for HTTPS-based web traffic from the Internet to the web servers</span><span class="sxs-lookup"><span data-stu-id="e8340-174">An external load balanced set for HTTPS-based web traffic from the Internet to the web servers</span></span>
* <span data-ttu-id="e8340-175">An internal load balanced set for unencrypted web traffic from the web servers to the application servers</span><span class="sxs-lookup"><span data-stu-id="e8340-175">An internal load balanced set for unencrypted web traffic from the web servers to the application servers</span></span>
* <span data-ttu-id="e8340-176">A single resource group</span><span class="sxs-lookup"><span data-stu-id="e8340-176">A single resource group</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8340-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8340-177">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]



