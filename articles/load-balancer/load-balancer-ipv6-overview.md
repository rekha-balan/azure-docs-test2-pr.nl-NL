---
title: Overview of IPv6 for Azure Load Balancer | Microsoft Docs
description: Understanding IPv6 support for Azure Load Balancer and load-balanced VMs.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: ''
keywords: ipv6, azure load balancer, dual stack, public ip, native ipv6, mobile, iot
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 00341fae6c28c1e73a1eb5892773a8aecfa98d20
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550330"
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a><span data-ttu-id="94292-104">Overview of IPv6 for Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="94292-104">Overview of IPv6 for Azure Load Balancer</span></span>

<span data-ttu-id="94292-105">Internet-facing load balancers can be deployed with an IPv6 address.</span><span class="sxs-lookup"><span data-stu-id="94292-105">Internet-facing load balancers can be deployed with an IPv6 address.</span></span> <span data-ttu-id="94292-106">In addition to IPv4 connectivity, this enables the following capabilities:</span><span class="sxs-lookup"><span data-stu-id="94292-106">In addition to IPv4 connectivity, this enables the following capabilities:</span></span>

* <span data-ttu-id="94292-107">Native end-to-end IPv6 connectivity between public Internet clients and Azure Virtual Machines (VMs) through the load balancer.</span><span class="sxs-lookup"><span data-stu-id="94292-107">Native end-to-end IPv6 connectivity between public Internet clients and Azure Virtual Machines (VMs) through the load balancer.</span></span>
* <span data-ttu-id="94292-108">Native end-to-end IPv6 outbound connectivity between VMs and public Internet IPv6-enabled clients.</span><span class="sxs-lookup"><span data-stu-id="94292-108">Native end-to-end IPv6 outbound connectivity between VMs and public Internet IPv6-enabled clients.</span></span>

<span data-ttu-id="94292-109">The following picture illustrates the IPv6 functionality for Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="94292-109">The following picture illustrates the IPv6 functionality for Azure Load Balancer.</span></span>

![Azure Load Balancer with IPv6](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

<span data-ttu-id="94292-111">Once deployed, an IPv4 or IPv6-enabled Internet client can communicate with the public IPv4 or IPv6 addresses (or hostnames) of the Azure Internet-facing Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="94292-111">Once deployed, an IPv4 or IPv6-enabled Internet client can communicate with the public IPv4 or IPv6 addresses (or hostnames) of the Azure Internet-facing Load Balancer.</span></span> <span data-ttu-id="94292-112">The load balancer routes the IPv6 packets to the private IPv6 addresses of the VMs using network address translation (NAT).</span><span class="sxs-lookup"><span data-stu-id="94292-112">The load balancer routes the IPv6 packets to the private IPv6 addresses of the VMs using network address translation (NAT).</span></span> <span data-ttu-id="94292-113">The IPv6 Internet client cannot communicate directly with the IPv6 address of the VMs.</span><span class="sxs-lookup"><span data-stu-id="94292-113">The IPv6 Internet client cannot communicate directly with the IPv6 address of the VMs.</span></span>

## <a name="features"></a><span data-ttu-id="94292-114">Features</span><span class="sxs-lookup"><span data-stu-id="94292-114">Features</span></span>

<span data-ttu-id="94292-115">Native IPv6 support for VMs deployed via Azure Resource Manager provides:</span><span class="sxs-lookup"><span data-stu-id="94292-115">Native IPv6 support for VMs deployed via Azure Resource Manager provides:</span></span>

1. <span data-ttu-id="94292-116">Load-balanced IPv6 services for IPv6 clients on the Internet</span><span class="sxs-lookup"><span data-stu-id="94292-116">Load-balanced IPv6 services for IPv6 clients on the Internet</span></span>
2. <span data-ttu-id="94292-117">Native IPv6 and IPv4 endpoints on VMs ("dual stacked")</span><span class="sxs-lookup"><span data-stu-id="94292-117">Native IPv6 and IPv4 endpoints on VMs ("dual stacked")</span></span>
3. <span data-ttu-id="94292-118">Inbound and outbound-initiated native IPv6 connections</span><span class="sxs-lookup"><span data-stu-id="94292-118">Inbound and outbound-initiated native IPv6 connections</span></span>
4. <span data-ttu-id="94292-119">Supported protocols such as TCP, UDP, and HTTP(S) enable a full range of service architectures</span><span class="sxs-lookup"><span data-stu-id="94292-119">Supported protocols such as TCP, UDP, and HTTP(S) enable a full range of service architectures</span></span>

## <a name="benefits"></a><span data-ttu-id="94292-120">Benefits</span><span class="sxs-lookup"><span data-stu-id="94292-120">Benefits</span></span>

<span data-ttu-id="94292-121">This functionality enables the following key benefits:</span><span class="sxs-lookup"><span data-stu-id="94292-121">This functionality enables the following key benefits:</span></span>

* <span data-ttu-id="94292-122">Meet government regulations requiring that new applications be accessible to IPv6-only clients</span><span class="sxs-lookup"><span data-stu-id="94292-122">Meet government regulations requiring that new applications be accessible to IPv6-only clients</span></span>
* <span data-ttu-id="94292-123">Enable mobile and Internet of things (IOT) developers to use dual-stacked (IPv4+IPv6) Azure Virtual Machines to address the growing mobile & IOT markets</span><span class="sxs-lookup"><span data-stu-id="94292-123">Enable mobile and Internet of things (IOT) developers to use dual-stacked (IPv4+IPv6) Azure Virtual Machines to address the growing mobile & IOT markets</span></span>

## <a name="details-and-limitations"></a><span data-ttu-id="94292-124">Details and limitations</span><span class="sxs-lookup"><span data-stu-id="94292-124">Details and limitations</span></span>

<span data-ttu-id="94292-125">Details</span><span class="sxs-lookup"><span data-stu-id="94292-125">Details</span></span>

* <span data-ttu-id="94292-126">The Azure DNS service contains both IPv4 A and IPv6 AAAA name records and responds with both records for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="94292-126">The Azure DNS service contains both IPv4 A and IPv6 AAAA name records and responds with both records for the load balancer.</span></span> <span data-ttu-id="94292-127">The client chooses which address (IPv4 or IPv6) to communicate with.</span><span class="sxs-lookup"><span data-stu-id="94292-127">The client chooses which address (IPv4 or IPv6) to communicate with.</span></span>
* <span data-ttu-id="94292-128">When a VM initiates a connection to a public Internet IPv6-connected device, the VM's source IPv6 address is network address translated (NAT) to the public IPv6 address of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="94292-128">When a VM initiates a connection to a public Internet IPv6-connected device, the VM's source IPv6 address is network address translated (NAT) to the public IPv6 address of the load balancer.</span></span>
* <span data-ttu-id="94292-129">VMs running the Linux operating system must be configured to receive an IPv6 IP address via DHCP.</span><span class="sxs-lookup"><span data-stu-id="94292-129">VMs running the Linux operating system must be configured to receive an IPv6 IP address via DHCP.</span></span> <span data-ttu-id="94292-130">Many of the Linux images in the Azure Gallery are already configured to support IPv6 without modification.</span><span class="sxs-lookup"><span data-stu-id="94292-130">Many of the Linux images in the Azure Gallery are already configured to support IPv6 without modification.</span></span> <span data-ttu-id="94292-131">For more information, see [Configuring DHCPv6 for Linux VMs](load-balancer-ipv6-for-linux.md)</span><span class="sxs-lookup"><span data-stu-id="94292-131">For more information, see [Configuring DHCPv6 for Linux VMs](load-balancer-ipv6-for-linux.md)</span></span>
* <span data-ttu-id="94292-132">If you choose to use a health probe with your load balancer, create an IPv4 probe and use it with both the IPv4 and IPv6 endpoints.</span><span class="sxs-lookup"><span data-stu-id="94292-132">If you choose to use a health probe with your load balancer, create an IPv4 probe and use it with both the IPv4 and IPv6 endpoints.</span></span> <span data-ttu-id="94292-133">If the service on your VM goes down, both the IPv4 and IPv6 endpoints are taken out of rotation.</span><span class="sxs-lookup"><span data-stu-id="94292-133">If the service on your VM goes down, both the IPv4 and IPv6 endpoints are taken out of rotation.</span></span>

<span data-ttu-id="94292-134">Limitations</span><span class="sxs-lookup"><span data-stu-id="94292-134">Limitations</span></span>

* <span data-ttu-id="94292-135">You cannot add IPv6 load balancing rules in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94292-135">You cannot add IPv6 load balancing rules in the Azure portal.</span></span> <span data-ttu-id="94292-136">The rules can only be created through the template, CLI, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94292-136">The rules can only be created through the template, CLI, PowerShell.</span></span>
* <span data-ttu-id="94292-137">You may not upgrade existing VMs to use IPv6 addresses.</span><span class="sxs-lookup"><span data-stu-id="94292-137">You may not upgrade existing VMs to use IPv6 addresses.</span></span> <span data-ttu-id="94292-138">You must deploy new VMs.</span><span class="sxs-lookup"><span data-stu-id="94292-138">You must deploy new VMs.</span></span>
* <span data-ttu-id="94292-139">A single IPv6 address can be assigned to a single network interface in each VM.</span><span class="sxs-lookup"><span data-stu-id="94292-139">A single IPv6 address can be assigned to a single network interface in each VM.</span></span>
* <span data-ttu-id="94292-140">The public IPv6 addresses cannot be assigned to a VM.</span><span class="sxs-lookup"><span data-stu-id="94292-140">The public IPv6 addresses cannot be assigned to a VM.</span></span> <span data-ttu-id="94292-141">They can only be assigned to a load balancer.</span><span class="sxs-lookup"><span data-stu-id="94292-141">They can only be assigned to a load balancer.</span></span>
* <span data-ttu-id="94292-142">You cannot configure the reverse DNS lookup for your public IPv6 addresses.</span><span class="sxs-lookup"><span data-stu-id="94292-142">You cannot configure the reverse DNS lookup for your public IPv6 addresses.</span></span>
* <span data-ttu-id="94292-143">The VMs with the IPv6 addresses cannot be members of an Azure Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="94292-143">The VMs with the IPv6 addresses cannot be members of an Azure Cloud Service.</span></span> <span data-ttu-id="94292-144">They can be connected to an Azure Virtual Network (VNet) and communicate with each other over their IPv4 addresses.</span><span class="sxs-lookup"><span data-stu-id="94292-144">They can be connected to an Azure Virtual Network (VNet) and communicate with each other over their IPv4 addresses.</span></span>
* <span data-ttu-id="94292-145">Private IPv6 addresses can be deployed on individual VMs in a resource group but cannot be deployed into a resource group via Scale Sets.</span><span class="sxs-lookup"><span data-stu-id="94292-145">Private IPv6 addresses can be deployed on individual VMs in a resource group but cannot be deployed into a resource group via Scale Sets.</span></span>
* <span data-ttu-id="94292-146">Azure VMs cannot connect over IPv6 to other VMs, other Azure services, or on-premises devices.</span><span class="sxs-lookup"><span data-stu-id="94292-146">Azure VMs cannot connect over IPv6 to other VMs, other Azure services, or on-premises devices.</span></span> <span data-ttu-id="94292-147">They can only communicate with the Azure load balancer over IPv6.</span><span class="sxs-lookup"><span data-stu-id="94292-147">They can only communicate with the Azure load balancer over IPv6.</span></span> <span data-ttu-id="94292-148">However, they can communicate with these other resources using IPv4.</span><span class="sxs-lookup"><span data-stu-id="94292-148">However, they can communicate with these other resources using IPv4.</span></span>
* <span data-ttu-id="94292-149">Network Security Group (NSG) protection for IPv4 is supported in dual-stack (IPv4+IPv6) deployments.</span><span class="sxs-lookup"><span data-stu-id="94292-149">Network Security Group (NSG) protection for IPv4 is supported in dual-stack (IPv4+IPv6) deployments.</span></span> <span data-ttu-id="94292-150">NSGs do not apply to the IPv6 endpoints.</span><span class="sxs-lookup"><span data-stu-id="94292-150">NSGs do not apply to the IPv6 endpoints.</span></span>
* <span data-ttu-id="94292-151">The IPv6 endpoint on the VM is not exposed directly to the internet.</span><span class="sxs-lookup"><span data-stu-id="94292-151">The IPv6 endpoint on the VM is not exposed directly to the internet.</span></span> <span data-ttu-id="94292-152">It is behind a load balancer.</span><span class="sxs-lookup"><span data-stu-id="94292-152">It is behind a load balancer.</span></span> <span data-ttu-id="94292-153">Only the ports specified in the load balancer rules are accessible over IPv6.</span><span class="sxs-lookup"><span data-stu-id="94292-153">Only the ports specified in the load balancer rules are accessible over IPv6.</span></span>
* <span data-ttu-id="94292-154">Changing the IdleTimeout parameter for IPv6 is **not currently supported**.</span><span class="sxs-lookup"><span data-stu-id="94292-154">Changing the IdleTimeout parameter for IPv6 is **not currently supported**.</span></span> <span data-ttu-id="94292-155">The default is four minutes.</span><span class="sxs-lookup"><span data-stu-id="94292-155">The default is four minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94292-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="94292-156">Next steps</span></span>

<span data-ttu-id="94292-157">Learn how to deploy a load balancer with IPv6.</span><span class="sxs-lookup"><span data-stu-id="94292-157">Learn how to deploy a load balancer with IPv6.</span></span>

* [<span data-ttu-id="94292-158">Availability of IPv6 by region</span><span class="sxs-lookup"><span data-stu-id="94292-158">Availability of IPv6 by region</span></span>](https://go.microsoft.com/fwlink/?linkid=828357)
* [<span data-ttu-id="94292-159">Deploy a load balancer with IPv6 using a template</span><span class="sxs-lookup"><span data-stu-id="94292-159">Deploy a load balancer with IPv6 using a template</span></span>](load-balancer-ipv6-internet-template.md)
* [<span data-ttu-id="94292-160">Deploy a load balancer with IPv6 using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="94292-160">Deploy a load balancer with IPv6 using Azure PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
* [<span data-ttu-id="94292-161">Deploy a load balancer with IPv6 using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="94292-161">Deploy a load balancer with IPv6 using Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)

