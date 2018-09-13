---
title: Create an Internet-facing load balancer - Azure portal classic | Microsoft Docs
description: Learn how to create an Internet facing load balancer in classic deployment model using the Azure classic portal
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: a022154f5eca6de2d2dbfc1b9aa30d2ea0a7d650
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660886"
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-classic-portal"></a><span data-ttu-id="ae6d3-103">Get started creating an Internet facing load balancer (classic) in the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="ae6d3-103">Get started creating an Internet facing load balancer (classic) in the Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [Azure classic portal](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic. Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource. You can view the documentation for different tools by clicking the tabs at the top of this article. This article covers the classic deployment model. You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="ae6d3-113">Set up an Internet-facing load balancer for virtual machines</span><span class="sxs-lookup"><span data-stu-id="ae6d3-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="ae6d3-114">In order to load balance network traffic from the Internet across the virtual machines of a cloud service, you must create a load-balanced set.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-114">In order to load balance network traffic from the Internet across the virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="ae6d3-115">This procedure assumes that you have already created the virtual machines and that they are all within the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-115">This procedure assumes that you have already created the virtual machines and that they are all within the same cloud service.</span></span>

<span data-ttu-id="ae6d3-116">**To configure a load-balanced set for virtual machines**</span><span class="sxs-lookup"><span data-stu-id="ae6d3-116">**To configure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="ae6d3-117">In the Azure classic portal, click **Virtual Machines**, and then click the name of a virtual machine in the load-balanced set.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-117">In the Azure classic portal, click **Virtual Machines**, and then click the name of a virtual machine in the load-balanced set.</span></span>
2. <span data-ttu-id="ae6d3-118">Click **Endpoints**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="ae6d3-119">On the **Add an endpoint to a virtual machine** page, click the right arrow.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-119">On the **Add an endpoint to a virtual machine** page, click the right arrow.</span></span>
4. <span data-ttu-id="ae6d3-120">On the **Specify the details of the endpoint** page:</span><span class="sxs-lookup"><span data-stu-id="ae6d3-120">On the **Specify the details of the endpoint** page:</span></span>

   * <span data-ttu-id="ae6d3-121">In **Name**, type a name for the endpoint or select the name from the list of predefined endpoints for common protocols.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-121">In **Name**, type a name for the endpoint or select the name from the list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="ae6d3-122">In **Protocol**, select the protocol required by the type of endpoint, either TCP or UDP, as needed.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-122">In **Protocol**, select the protocol required by the type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="ae6d3-123">In **Public Port and Private Port**, type the port numbers that you want the virtual machine to use, as needed.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-123">In **Public Port and Private Port**, type the port numbers that you want the virtual machine to use, as needed.</span></span> <span data-ttu-id="ae6d3-124">You can use the private port and firewall rules on the virtual machine to redirect traffic in a way that is appropriate for your application.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-124">You can use the private port and firewall rules on the virtual machine to redirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="ae6d3-125">The private port can be the same as the public port.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-125">The private port can be the same as the public port.</span></span> <span data-ttu-id="ae6d3-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 to both the public and private port.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 to both the public and private port.</span></span>

5. <span data-ttu-id="ae6d3-127">Select **Create a load-balanced set**, and then click the right arrow.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-127">Select **Create a load-balanced set**, and then click the right arrow.</span></span>
6. <span data-ttu-id="ae6d3-128">On the **Configure the load-balanced set** page, type a name for the load-balanced set, and then assign the values for probe behavior of the Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-128">On the **Configure the load-balanced set** page, type a name for the load-balanced set, and then assign the values for probe behavior of the Azure Load Balancer.</span></span> <span data-ttu-id="ae6d3-129">The Load Balancer uses probes to determine if the virtual machines in the load-balanced set are available to receive incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-129">The Load Balancer uses probes to determine if the virtual machines in the load-balanced set are available to receive incoming traffic.</span></span>
7. <span data-ttu-id="ae6d3-130">Click the check mark to create the load-balanced endpoint.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-130">Click the check mark to create the load-balanced endpoint.</span></span> <span data-ttu-id="ae6d3-131">You will see **Yes** in the **Load-balanced set name** column of the **Endpoints** page for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-131">You will see **Yes** in the **Load-balanced set name** column of the **Endpoints** page for the virtual machine.</span></span>
8. <span data-ttu-id="ae6d3-132">In the portal, click **Virtual Machines**, click the name of an additional virtual machine in the load-balanced set, click **Endpoints**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-132">In the portal, click **Virtual Machines**, click the name of an additional virtual machine in the load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="ae6d3-133">On the **Add an endpoint to a virtual machine** page, click **Add endpoint to an existing load-balanced set**, select the name of the load-balanced set, and then click the right arrow.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-133">On the **Add an endpoint to a virtual machine** page, click **Add endpoint to an existing load-balanced set**, select the name of the load-balanced set, and then click the right arrow.</span></span>
10. <span data-ttu-id="ae6d3-134">On the **Specify the details of the endpoint** page, type a name for the endpoint, and then click the check mark.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-134">On the **Specify the details of the endpoint** page, type a name for the endpoint, and then click the check mark.</span></span>

<span data-ttu-id="ae6d3-135">For the additional virtual machines in the load-balanced set, repeat steps 8-10.</span><span class="sxs-lookup"><span data-stu-id="ae6d3-135">For the additional virtual machines in the load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae6d3-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae6d3-136">Next steps</span></span>

[<span data-ttu-id="ae6d3-137">Get started configuring an internal load balancer</span><span class="sxs-lookup"><span data-stu-id="ae6d3-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="ae6d3-138">Configure a load balancer distribution mode</span><span class="sxs-lookup"><span data-stu-id="ae6d3-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="ae6d3-139">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="ae6d3-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
