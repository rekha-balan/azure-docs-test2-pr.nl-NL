---
title: SQL Server Availability Groups - Azure Virtual Machines - Overview | Microsoft Docs
description: This article introduces SQL Server Availability Groups on Azure virtual machines.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: 68f602880d4e3a0498867aa7ef8d6aaa0f5f688a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553135"
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="0f99e-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="0f99e-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="0f99e-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="0f99e-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="0f99e-105">Always On availability groups on Azure Virtual Machines are similar to Always On availability groups on premises.</span><span class="sxs-lookup"><span data-stu-id="0f99e-105">Always On availability groups on Azure Virtual Machines are similar to Always On availability groups on premises.</span></span> <span data-ttu-id="0f99e-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f99e-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="0f99e-107">The diagram illustrates the parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="0f99e-107">The diagram illustrates the parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Availability Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="0f99e-109">The key difference for an Availability Group in Azure Virtual Machines is that the Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f99e-109">The key difference for an Availability Group in Azure Virtual Machines is that the Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="0f99e-110">The load balancer holds the IP addresses for the availability group listener.</span><span class="sxs-lookup"><span data-stu-id="0f99e-110">The load balancer holds the IP addresses for the availability group listener.</span></span> <span data-ttu-id="0f99e-111">If you have more than one availability group each group requires a listener.</span><span class="sxs-lookup"><span data-stu-id="0f99e-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="0f99e-112">One load balancer can support multiple listeners.</span><span class="sxs-lookup"><span data-stu-id="0f99e-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="0f99e-113">When you are ready to build a SQL Server availability aroup on Azure Virtual Machines, refer to these tutorials.</span><span class="sxs-lookup"><span data-stu-id="0f99e-113">When you are ready to build a SQL Server availability aroup on Azure Virtual Machines, refer to these tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="0f99e-114">Automatically create an availability group from a template</span><span class="sxs-lookup"><span data-stu-id="0f99e-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="0f99e-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0f99e-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="0f99e-116">Manually create an availability group in Azure portal</span><span class="sxs-lookup"><span data-stu-id="0f99e-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="0f99e-117">You can also create the virtual machines yourself without the template.</span><span class="sxs-lookup"><span data-stu-id="0f99e-117">You can also create the virtual machines yourself without the template.</span></span> <span data-ttu-id="0f99e-118">First, complete the prerequisites, then create the availability group.</span><span class="sxs-lookup"><span data-stu-id="0f99e-118">First, complete the prerequisites, then create the availability group.</span></span> <span data-ttu-id="0f99e-119">See the following topics:</span><span class="sxs-lookup"><span data-stu-id="0f99e-119">See the following topics:</span></span> 

- [<span data-ttu-id="0f99e-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="0f99e-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="0f99e-121">Create Always On Availability Group to improve availability and disaster recovery</span><span class="sxs-lookup"><span data-stu-id="0f99e-121">Create Always On Availability Group to improve availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="0f99e-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f99e-122">Next steps</span></span>

<span data-ttu-id="0f99e-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="0f99e-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>

