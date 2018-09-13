---
title: Configure Load balancer for SQL always on | Microsoft Docs
description: Configure Load balancer to work with SQL always on and how to leverage powershell to create load balancer for the SQL implementation
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 8d126181d91a79f447e8313cc82a335a5b94710e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553996"
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="3c9c4-103">Configure load balancer for SQL always on</span><span class="sxs-lookup"><span data-stu-id="3c9c4-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="3c9c4-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span><span class="sxs-lookup"><span data-stu-id="3c9c4-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="3c9c4-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="3c9c4-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="3c9c4-106">The Availability Group Listener allows client applications to seamlessly connect to the primary replica, irrespective of the number of the replicas in the configuration.</span><span class="sxs-lookup"><span data-stu-id="3c9c4-106">The Availability Group Listener allows client applications to seamlessly connect to the primary replica, irrespective of the number of the replicas in the configuration.</span></span>

<span data-ttu-id="3c9c4-107">The listener (DNS) name is mapped to a load-balanced IP address and Azure's load balancer directs the incoming traffic to only the primary server in the replica set.</span><span class="sxs-lookup"><span data-stu-id="3c9c4-107">The listener (DNS) name is mapped to a load-balanced IP address and Azure's load balancer directs the incoming traffic to only the primary server in the replica set.</span></span>

<span data-ttu-id="3c9c4-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span><span class="sxs-lookup"><span data-stu-id="3c9c4-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="3c9c4-109">You now have control over the accessibility of the listener and can choose the load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span><span class="sxs-lookup"><span data-stu-id="3c9c4-109">You now have control over the accessibility of the listener and can choose the load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="3c9c4-110">By using ILB on the listener, the SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span><span class="sxs-lookup"><span data-stu-id="3c9c4-110">By using ILB on the listener, the SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="3c9c4-111">Services and VMs in the same Virtual network</span><span class="sxs-lookup"><span data-stu-id="3c9c4-111">Services and VMs in the same Virtual network</span></span>
* <span data-ttu-id="3c9c4-112">Services and VMs from connected on-premises network</span><span class="sxs-lookup"><span data-stu-id="3c9c4-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="3c9c4-113">Services and VMs from interconnected VNets</span><span class="sxs-lookup"><span data-stu-id="3c9c4-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="3c9c4-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span><span class="sxs-lookup"><span data-stu-id="3c9c4-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-to-the-service"></a><span data-ttu-id="3c9c4-116">Add Internal Load Balancer to the service</span><span class="sxs-lookup"><span data-stu-id="3c9c4-116">Add Internal Load Balancer to the service</span></span>

1. <span data-ttu-id="3c9c4-117">In the following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span><span class="sxs-lookup"><span data-stu-id="3c9c4-117">In the following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="3c9c4-118">Add load balanced endpoints for ILB on each VM</span><span class="sxs-lookup"><span data-stu-id="3c9c4-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="3c9c4-119">In the example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in the cloud service "Sqlsvc".</span><span class="sxs-lookup"><span data-stu-id="3c9c4-119">In the example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in the cloud service "Sqlsvc".</span></span> <span data-ttu-id="3c9c4-120">After creating the ILB with `DirectServerReturn` switch, you add load balanced endpoints to the ILB to allow SQL to configure the listeners for the availability groups.</span><span class="sxs-lookup"><span data-stu-id="3c9c4-120">After creating the ILB with `DirectServerReturn` switch, you add load balanced endpoints to the ILB to allow SQL to configure the listeners for the availability groups.</span></span>

<span data-ttu-id="3c9c4-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="3c9c4-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3c9c4-122">See Also</span><span class="sxs-lookup"><span data-stu-id="3c9c4-122">See Also</span></span>
[<span data-ttu-id="3c9c4-123">Get started configuring an Internet facing load balancer</span><span class="sxs-lookup"><span data-stu-id="3c9c4-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="3c9c4-124">Get started configuring an Internal load balancer</span><span class="sxs-lookup"><span data-stu-id="3c9c4-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="3c9c4-125">Configure a Load balancer distribution mode</span><span class="sxs-lookup"><span data-stu-id="3c9c4-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="3c9c4-126">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="3c9c4-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

