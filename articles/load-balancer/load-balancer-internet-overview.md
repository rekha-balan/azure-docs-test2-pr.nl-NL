---
title: Internet facing load balancer overview | Microsoft Docs
description: Overview for Internet facing load balancer and its features. How a load balancer works for Azure using virtual machines and cloud services.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 70db43d56327e5c6bb67445a3b53f68389109bce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556412"
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="8fc50-104">Internet facing load balancer overview</span><span class="sxs-lookup"><span data-stu-id="8fc50-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="8fc50-105">Azure load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the virtual machine and vice versa for the response traffic from the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8fc50-105">Azure load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the virtual machine and vice versa for the response traffic from the virtual machine.</span></span> <span data-ttu-id="8fc50-106">Load balancing rules allow you to distribute specific types of traffic between multiple virtual machines or services.</span><span class="sxs-lookup"><span data-stu-id="8fc50-106">Load balancing rules allow you to distribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="8fc50-107">For example, you can spread the load of web request traffic across multiple web servers or web roles.</span><span class="sxs-lookup"><span data-stu-id="8fc50-107">For example, you can spread the load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="8fc50-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in the service definition (.csdef) file.</span><span class="sxs-lookup"><span data-stu-id="8fc50-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in the service definition (.csdef) file.</span></span>

<span data-ttu-id="8fc50-109">The *servicedefinition.csdef* file contains the endpoint configuration and when you have multiple role instances for a web or worker role deployment, the load balancer will be setup for it.</span><span class="sxs-lookup"><span data-stu-id="8fc50-109">The *servicedefinition.csdef* file contains the endpoint configuration and when you have multiple role instances for a web or worker role deployment, the load balancer will be setup for it.</span></span> <span data-ttu-id="8fc50-110">The way to add instances to your cloud deployment is changing the instance count on the service configuration file (.csfg).</span><span class="sxs-lookup"><span data-stu-id="8fc50-110">The way to add instances to your cloud deployment is changing the instance count on the service configuration file (.csfg).</span></span>

<span data-ttu-id="8fc50-111">The following figure shows a load-balanced endpoint for encrypted web traffic that is shared among three virtual machines for the public and private TCP port of 80.</span><span class="sxs-lookup"><span data-stu-id="8fc50-111">The following figure shows a load-balanced endpoint for encrypted web traffic that is shared among three virtual machines for the public and private TCP port of 80.</span></span> <span data-ttu-id="8fc50-112">These three virtual machines are in a load-balanced set.</span><span class="sxs-lookup"><span data-stu-id="8fc50-112">These three virtual machines are in a load-balanced set.</span></span>

![public load balancer example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-internet-overview/IC727496.png)<span data-ttu-id="8fc50-114">)</span><span class="sxs-lookup"><span data-stu-id="8fc50-114">)</span></span>

<span data-ttu-id="8fc50-115">Figure 1 - Load-balanced endpoint for web traffic</span><span class="sxs-lookup"><span data-stu-id="8fc50-115">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="8fc50-116">When Internet clients send web page requests to the public IP address of the cloud service on TCP port 80, the Azure Load Balancer distributes the requests between the three virtual machines in the load-balanced set.</span><span class="sxs-lookup"><span data-stu-id="8fc50-116">When Internet clients send web page requests to the public IP address of the cloud service on TCP port 80, the Azure Load Balancer distributes the requests between the three virtual machines in the load-balanced set.</span></span> <span data-ttu-id="8fc50-117">For more information about load balancer algorithms, see the [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="8fc50-117">For more information about load balancer algorithms, see the [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="8fc50-118">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span><span class="sxs-lookup"><span data-stu-id="8fc50-118">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="8fc50-119">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="8fc50-119">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fc50-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="8fc50-120">Next steps</span></span>

<span data-ttu-id="8fc50-121">Learn about [Internal load balancer](load-balancer-internal-overview.md) to better understand which load balancer is a better fit for your cloud deployment.</span><span class="sxs-lookup"><span data-stu-id="8fc50-121">Learn about [Internal load balancer](load-balancer-internal-overview.md) to better understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="8fc50-122">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span><span class="sxs-lookup"><span data-stu-id="8fc50-122">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="8fc50-123">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="8fc50-123">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="8fc50-124">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="8fc50-124">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>

