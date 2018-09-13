---
title: Configure Load Balancer for SQL Server Always On | Microsoft Docs
description: Configure Load Balancer to work with SQL Server Always On, and learn how to use PowerShell to create a load balancer for the SQL Server implementation
services: load-balancer
documentationcenter: na
author: KumudD
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/25/2017
ms.author: kumud
ms.openlocfilehash: a0c2345b47b9103ac6a7ae998f13a12332e3907e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44797672"
---
# <a name="configure-a-load-balancer-for-sql-server-always-on"></a><span data-ttu-id="cc6c0-103">Configure a load balancer for SQL Server Always On</span><span class="sxs-lookup"><span data-stu-id="cc6c0-103">Configure a load balancer for SQL Server Always On</span></span>



<span data-ttu-id="cc6c0-104">SQL Server Always On availability groups now can run with an internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-104">SQL Server Always On availability groups now can run with an internal load balancer.</span></span> <span data-ttu-id="cc6c0-105">An availability group is SQL Server's flagship solution for high availability and disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-105">An availability group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="cc6c0-106">The availability group listener allows client applications to seamlessly connect to the primary replica, irrespective of the number of replicas in the configuration.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-106">The availability group listener allows client applications to seamlessly connect to the primary replica, irrespective of the number of replicas in the configuration.</span></span>

<span data-ttu-id="cc6c0-107">The listener (DNS) name is mapped to a load-balanced IP address.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-107">The listener (DNS) name is mapped to a load-balanced IP address.</span></span> <span data-ttu-id="cc6c0-108">Azure Load Balancer directs the incoming traffic to only the primary server in the replica set.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-108">Azure Load Balancer directs the incoming traffic to only the primary server in the replica set.</span></span>

<span data-ttu-id="cc6c0-109">You can use internal load balancer support for SQL Server Always On (listener) endpoints.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-109">You can use internal load balancer support for SQL Server Always On (listener) endpoints.</span></span> <span data-ttu-id="cc6c0-110">You now have control over the accessibility of the listener.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-110">You now have control over the accessibility of the listener.</span></span> <span data-ttu-id="cc6c0-111">You can choose the load-balanced IP address from a specific subnet in your virtual network.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-111">You can choose the load-balanced IP address from a specific subnet in your virtual network.</span></span>

<span data-ttu-id="cc6c0-112">By using an internal load balancer on the listener, the SQL Server endpoint (for example, Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span><span class="sxs-lookup"><span data-stu-id="cc6c0-112">By using an internal load balancer on the listener, the SQL Server endpoint (for example, Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="cc6c0-113">Services and VMs in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-113">Services and VMs in the same virtual network.</span></span>
* <span data-ttu-id="cc6c0-114">Services and VMs from connected on-premises networks.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-114">Services and VMs from connected on-premises networks.</span></span>
* <span data-ttu-id="cc6c0-115">Services and VMs from interconnected virtual networks.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-115">Services and VMs from interconnected virtual networks.</span></span>

![Internal load balancer SQL Server Always On](./media/load-balancer-configure-sqlao/sqlao1.png)

## <a name="add-an-internal-load-balancer-to-the-service"></a><span data-ttu-id="cc6c0-117">Add an internal load balancer to the service</span><span class="sxs-lookup"><span data-stu-id="cc6c0-117">Add an internal load balancer to the service</span></span>

1. <span data-ttu-id="cc6c0-118">In the following example, you configure a virtual network that contains a subnet called 'Subnet-1':</span><span class="sxs-lookup"><span data-stu-id="cc6c0-118">In the following example, you configure a virtual network that contains a subnet called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="cc6c0-119">Add load-balanced endpoints for an internal load balancer on each VM.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-119">Add load-balanced endpoints for an internal load balancer on each VM.</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="cc6c0-120">In the previous example, you have two VMs called "sqlsvc1" and "sqlsvc2" that run in the cloud service "Sqlsvc".</span><span class="sxs-lookup"><span data-stu-id="cc6c0-120">In the previous example, you have two VMs called "sqlsvc1" and "sqlsvc2" that run in the cloud service "Sqlsvc".</span></span> <span data-ttu-id="cc6c0-121">After you create the internal load balancer with the `DirectServerReturn` switch, you add load-balanced endpoints to the internal load balancer.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-121">After you create the internal load balancer with the `DirectServerReturn` switch, you add load-balanced endpoints to the internal load balancer.</span></span> <span data-ttu-id="cc6c0-122">The load-balanced endpoints allow SQL Server to configure the listeners for the availability groups.</span><span class="sxs-lookup"><span data-stu-id="cc6c0-122">The load-balanced endpoints allow SQL Server to configure the listeners for the availability groups.</span></span>

<span data-ttu-id="cc6c0-123">For more information about SQL Server Always On, see [Configure an internal load balancer for an Always On availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="cc6c0-123">For more information about SQL Server Always On, see [Configure an internal load balancer for an Always On availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="cc6c0-124">See also</span><span class="sxs-lookup"><span data-stu-id="cc6c0-124">See also</span></span>
* [<span data-ttu-id="cc6c0-125">Get started configuring a public load balancer</span><span class="sxs-lookup"><span data-stu-id="cc6c0-125">Get started configuring a public load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)
* [<span data-ttu-id="cc6c0-126">Get started configuring an internal load balancer</span><span class="sxs-lookup"><span data-stu-id="cc6c0-126">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="cc6c0-127">Configure a load balancer distribution mode</span><span class="sxs-lookup"><span data-stu-id="cc6c0-127">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
* [<span data-ttu-id="cc6c0-128">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="cc6c0-128">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
