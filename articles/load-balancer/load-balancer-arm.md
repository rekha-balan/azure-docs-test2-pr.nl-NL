---
title: Azure Resource Manager support for Load Balancer | Microsoft Docs
description: Using powershell for Load Balancer with Azure Resource Manager. Using templates for load balancer
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2bc7cd8e7a649810d0a510c478855171add2a432
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661598"
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="a89bd-104">Using Azure Resource Manager Support with Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="a89bd-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="a89bd-105">Azure Resource Manager is the preferred management framework for services in Azure.</span><span class="sxs-lookup"><span data-stu-id="a89bd-105">Azure Resource Manager is the preferred management framework for services in Azure.</span></span> <span data-ttu-id="a89bd-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span><span class="sxs-lookup"><span data-stu-id="a89bd-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="a89bd-107">Concepts</span><span class="sxs-lookup"><span data-stu-id="a89bd-107">Concepts</span></span>

<span data-ttu-id="a89bd-108">With Resource Manager, Azure Load Balancer contains the following child resources:</span><span class="sxs-lookup"><span data-stu-id="a89bd-108">With Resource Manager, Azure Load Balancer contains the following child resources:</span></span>

* <span data-ttu-id="a89bd-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span><span class="sxs-lookup"><span data-stu-id="a89bd-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="a89bd-110">These IP addresses serve as ingress for the traffic.</span><span class="sxs-lookup"><span data-stu-id="a89bd-110">These IP addresses serve as ingress for the traffic.</span></span>
* <span data-ttu-id="a89bd-111">Back-end address pool – these are IP addresses associated with the virtual machine Network Interface Card (NIC) to which load will be distributed.</span><span class="sxs-lookup"><span data-stu-id="a89bd-111">Back-end address pool – these are IP addresses associated with the virtual machine Network Interface Card (NIC) to which load will be distributed.</span></span>
* <span data-ttu-id="a89bd-112">Load balancing rules – a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span><span class="sxs-lookup"><span data-stu-id="a89bd-112">Load balancing rules – a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="a89bd-113">A single load balancer can have multiple load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="a89bd-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="a89bd-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span><span class="sxs-lookup"><span data-stu-id="a89bd-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="a89bd-115">Probes – probes enable you to keep track of the health of VM instances.</span><span class="sxs-lookup"><span data-stu-id="a89bd-115">Probes – probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="a89bd-116">If a health probe fails, the VM instance will be taken out of rotation automatically.</span><span class="sxs-lookup"><span data-stu-id="a89bd-116">If a health probe fails, the VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="a89bd-117">Inbound NAT rules – NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP.</span><span class="sxs-lookup"><span data-stu-id="a89bd-117">Inbound NAT rules – NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="a89bd-118">Quickstart templates</span><span class="sxs-lookup"><span data-stu-id="a89bd-118">Quickstart templates</span></span>

<span data-ttu-id="a89bd-119">Azure Resource Manager allows you to provision your applications using a declarative template.</span><span class="sxs-lookup"><span data-stu-id="a89bd-119">Azure Resource Manager allows you to provision your applications using a declarative template.</span></span> <span data-ttu-id="a89bd-120">In a single template, you can deploy multiple services along with their dependencies.</span><span class="sxs-lookup"><span data-stu-id="a89bd-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="a89bd-121">You use the same template to repeatedly deploy your application during every stage of the application lifecycle.</span><span class="sxs-lookup"><span data-stu-id="a89bd-121">You use the same template to repeatedly deploy your application during every stage of the application lifecycle.</span></span>

<span data-ttu-id="a89bd-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span><span class="sxs-lookup"><span data-stu-id="a89bd-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="a89bd-123">With templates you can create everything you need for a complex application.</span><span class="sxs-lookup"><span data-stu-id="a89bd-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="a89bd-124">The template file can be checked into content management system for version control and collaboration.</span><span class="sxs-lookup"><span data-stu-id="a89bd-124">The template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="a89bd-125">Learn more about templates</span><span class="sxs-lookup"><span data-stu-id="a89bd-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="a89bd-126">Learn more about Network Resources</span><span class="sxs-lookup"><span data-stu-id="a89bd-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="a89bd-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span><span class="sxs-lookup"><span data-stu-id="a89bd-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="a89bd-128">Examples of templates:</span><span class="sxs-lookup"><span data-stu-id="a89bd-128">Examples of templates:</span></span>

* [<span data-ttu-id="a89bd-129">2 VMs in a Load Balancer and load balancing rules</span><span class="sxs-lookup"><span data-stu-id="a89bd-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="a89bd-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span><span class="sxs-lookup"><span data-stu-id="a89bd-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="a89bd-131">2 VMs in a Load Balancer and configure NAT rules on the LB</span><span class="sxs-lookup"><span data-stu-id="a89bd-131">2 VMs in a Load Balancer and configure NAT rules on the LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="a89bd-132">Setting up Azure Load Balancer with a PowerShell or CLI</span><span class="sxs-lookup"><span data-stu-id="a89bd-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="a89bd-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span><span class="sxs-lookup"><span data-stu-id="a89bd-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="a89bd-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used to create a Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="a89bd-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used to create a Load Balancer.</span></span>
* [<span data-ttu-id="a89bd-135">How to create a load balancer using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a89bd-135">How to create a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="a89bd-136">Using the Azure CLI with Azure Resource Management</span><span class="sxs-lookup"><span data-stu-id="a89bd-136">Using the Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="a89bd-137">Load Balancer REST APIs</span><span class="sxs-lookup"><span data-stu-id="a89bd-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="a89bd-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="a89bd-138">Next steps</span></span>

<span data-ttu-id="a89bd-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span><span class="sxs-lookup"><span data-stu-id="a89bd-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="a89bd-140">Learn how to manage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="a89bd-140">Learn how to manage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="a89bd-141">This is important when your application needs to keep connections alive for servers behind a load balancer.</span><span class="sxs-lookup"><span data-stu-id="a89bd-141">This is important when your application needs to keep connections alive for servers behind a load balancer.</span></span>

