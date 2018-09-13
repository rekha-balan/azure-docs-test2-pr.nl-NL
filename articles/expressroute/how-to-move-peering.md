---
title: Move a public peering on Azure ExpressRoute to Microsoft peering | Microsoft Docs
description: This article shows you the steps to move your public peering to Microsoft peering on ExpressRoute.
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2018
ms.author: cherylmc
ms.openlocfilehash: f34fabc95d5b56edc6e37c323bebf60bd98c8b90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858098"
---
# <a name="move-a-public-peering-to-microsoft-peering"></a><span data-ttu-id="d281e-103">Move a public peering to Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="d281e-103">Move a public peering to Microsoft peering</span></span>

<span data-ttu-id="d281e-104">ExpressRoute supports using Microsoft peering with route filters for Azure PaaS services, such as Azure storage and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d281e-104">ExpressRoute supports using Microsoft peering with route filters for Azure PaaS services, such as Azure storage and Azure SQL Database.</span></span> <span data-ttu-id="d281e-105">You now need only one routing domain to access Microsoft PaaS and SaaS services.</span><span class="sxs-lookup"><span data-stu-id="d281e-105">You now need only one routing domain to access Microsoft PaaS and SaaS services.</span></span> <span data-ttu-id="d281e-106">You can use route filters to selectively advertise the PaaS service prefixes for Azure regions you want to consume.</span><span class="sxs-lookup"><span data-stu-id="d281e-106">You can use route filters to selectively advertise the PaaS service prefixes for Azure regions you want to consume.</span></span>

<span data-ttu-id="d281e-107">This article helps you move a public peering configuration to Microsoft peering with no downtime.</span><span class="sxs-lookup"><span data-stu-id="d281e-107">This article helps you move a public peering configuration to Microsoft peering with no downtime.</span></span> <span data-ttu-id="d281e-108">For more information about routing domains and peerings, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="d281e-108">For more information about routing domains and peerings, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>


## <a name="before"></a><span data-ttu-id="d281e-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="d281e-109">Before you begin</span></span>

* <span data-ttu-id="d281e-110">To connect to Microsoft peering, you need to set up and manage NAT.</span><span class="sxs-lookup"><span data-stu-id="d281e-110">To connect to Microsoft peering, you need to set up and manage NAT.</span></span> <span data-ttu-id="d281e-111">Your connectivity provider may set up and manage the NAT as a managed service.</span><span class="sxs-lookup"><span data-stu-id="d281e-111">Your connectivity provider may set up and manage the NAT as a managed service.</span></span> <span data-ttu-id="d281e-112">If you are planning to access the Azure PaaS and Azure SaaS services on Microsoft peering, it's important to size the NAT IP pool correctly.</span><span class="sxs-lookup"><span data-stu-id="d281e-112">If you are planning to access the Azure PaaS and Azure SaaS services on Microsoft peering, it's important to size the NAT IP pool correctly.</span></span> <span data-ttu-id="d281e-113">For more information about NAT for ExpressRoute, see the [NAT requirements for Microsoft peering](expressroute-nat.md#nat-requirements-for-microsoft-peering).</span><span class="sxs-lookup"><span data-stu-id="d281e-113">For more information about NAT for ExpressRoute, see the [NAT requirements for Microsoft peering](expressroute-nat.md#nat-requirements-for-microsoft-peering).</span></span>

* <span data-ttu-id="d281e-114">If you are using public peering and currently have IP Network rules for public IP addresses that are used to access [Azure Storage](../storage/common/storage-network-security.md) or [Azure SQL Database](../sql-database/sql-database-vnet-service-endpoint-rule-overview.md), you need to make sure that the NAT IP pool configured with Microsoft peering is included in the list of public IP addresses for the Azure storage account or Azure SQL account.</span><span class="sxs-lookup"><span data-stu-id="d281e-114">If you are using public peering and currently have IP Network rules for public IP addresses that are used to access [Azure Storage](../storage/common/storage-network-security.md) or [Azure SQL Database](../sql-database/sql-database-vnet-service-endpoint-rule-overview.md), you need to make sure that the NAT IP pool configured with Microsoft peering is included in the list of public IP addresses for the Azure storage account or Azure SQL account.</span></span>

* <span data-ttu-id="d281e-115">In order to move to Microsoft peering with no downtime, use the steps in this article in the order that they are presented.</span><span class="sxs-lookup"><span data-stu-id="d281e-115">In order to move to Microsoft peering with no downtime, use the steps in this article in the order that they are presented.</span></span>

## <a name="create"></a><span data-ttu-id="d281e-116">1. Create Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="d281e-116">1. Create Microsoft peering</span></span>

<span data-ttu-id="d281e-117">If Microsoft peering has not been created, use any of the following articles to create Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="d281e-117">If Microsoft peering has not been created, use any of the following articles to create Microsoft peering.</span></span> <span data-ttu-id="d281e-118">If your connectivity provider offers managed layer 3 services, you can ask the connectivity provider to enable Microsoft peering for your circuit.</span><span class="sxs-lookup"><span data-stu-id="d281e-118">If your connectivity provider offers managed layer 3 services, you can ask the connectivity provider to enable Microsoft peering for your circuit.</span></span>

  * [<span data-ttu-id="d281e-119">Create Microsoft peering using Azure portal</span><span class="sxs-lookup"><span data-stu-id="d281e-119">Create Microsoft peering using Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md#msft)
  * [<span data-ttu-id="d281e-120">Create Microsoft peering using Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="d281e-120">Create Microsoft peering using Azure Powershell</span></span>](expressroute-howto-routing-arm.md#msft)
  * [<span data-ttu-id="d281e-121">Create Microsoft peering using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d281e-121">Create Microsoft peering using Azure CLI</span></span>](howto-routing-cli.md#msft)

## <a name="validate"></a><span data-ttu-id="d281e-122">2. Validate Microsoft peering is enabled</span><span class="sxs-lookup"><span data-stu-id="d281e-122">2. Validate Microsoft peering is enabled</span></span>

<span data-ttu-id="d281e-123">Verify that the Microsoft peering is enabled and the advertised public prefixes are in the configured state.</span><span class="sxs-lookup"><span data-stu-id="d281e-123">Verify that the Microsoft peering is enabled and the advertised public prefixes are in the configured state.</span></span>

  * [<span data-ttu-id="d281e-124">Azure portal</span><span class="sxs-lookup"><span data-stu-id="d281e-124">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md#getmsft)
  * [<span data-ttu-id="d281e-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d281e-125">Azure PowerShell</span></span>](expressroute-howto-routing-arm.md#getmsft)
  * [<span data-ttu-id="d281e-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d281e-126">Azure CLI</span></span>](howto-routing-cli.md#getmsft)

## <a name="routefilter"></a><span data-ttu-id="d281e-127">3. Configure and attach a route filter to the circuit</span><span class="sxs-lookup"><span data-stu-id="d281e-127">3. Configure and attach a route filter to the circuit</span></span>

<span data-ttu-id="d281e-128">By default, new Microsoft peerings do not advertise any prefixes until a route filter is attached to the circuit.</span><span class="sxs-lookup"><span data-stu-id="d281e-128">By default, new Microsoft peerings do not advertise any prefixes until a route filter is attached to the circuit.</span></span> <span data-ttu-id="d281e-129">When you create a route filter rule, you can specify the list of service communities for Azure regions that you want to consume for Azure PaaS services, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="d281e-129">When you create a route filter rule, you can specify the list of service communities for Azure regions that you want to consume for Azure PaaS services, as shown in the following screenshot:</span></span>

![Merge public peering](.\media\how-to-move-peering\public.png)

<span data-ttu-id="d281e-131">Configure route filters using any of the following articles:</span><span class="sxs-lookup"><span data-stu-id="d281e-131">Configure route filters using any of the following articles:</span></span>

  * [<span data-ttu-id="d281e-132">Configure route filters for Microsoft peering using Azure portal</span><span class="sxs-lookup"><span data-stu-id="d281e-132">Configure route filters for Microsoft peering using Azure portal</span></span>](how-to-routefilter-portal.md)
  * [<span data-ttu-id="d281e-133">Configure route filters for Microsoft peering using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d281e-133">Configure route filters for Microsoft peering using Azure PowerShell</span></span>](how-to-routefilter-powershell.md)
  * [<span data-ttu-id="d281e-134">Configure route filters for Microsoft peering using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d281e-134">Configure route filters for Microsoft peering using Azure CLI</span></span>](how-to-routefilter-cli.md)

## <a name="delete"></a><span data-ttu-id="d281e-135">4. Delete the public peering</span><span class="sxs-lookup"><span data-stu-id="d281e-135">4. Delete the public peering</span></span>

<span data-ttu-id="d281e-136">After verifying that the Microsoft peering is configured and the prefixes you wish to consume are correctly advertised on Microsoft peering, you can then delete the public peering.</span><span class="sxs-lookup"><span data-stu-id="d281e-136">After verifying that the Microsoft peering is configured and the prefixes you wish to consume are correctly advertised on Microsoft peering, you can then delete the public peering.</span></span> <span data-ttu-id="d281e-137">To delete the public peering, use any of the following articles:</span><span class="sxs-lookup"><span data-stu-id="d281e-137">To delete the public peering, use any of the following articles:</span></span>

  * [<span data-ttu-id="d281e-138">Delete Azure public peering using Azure portal</span><span class="sxs-lookup"><span data-stu-id="d281e-138">Delete Azure public peering using Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md#deletepublic)
  * [<span data-ttu-id="d281e-139">Delete Azure public peering using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d281e-139">Delete Azure public peering using Azure PowerShell</span></span>](expressroute-howto-routing-arm.md#deletepublic)
  * [<span data-ttu-id="d281e-140">Delete Azure public peering using CLI</span><span class="sxs-lookup"><span data-stu-id="d281e-140">Delete Azure public peering using CLI</span></span>](howto-routing-cli.md#deletepublic)
  
## <a name="view"></a><span data-ttu-id="d281e-141">5. View peerings</span><span class="sxs-lookup"><span data-stu-id="d281e-141">5. View peerings</span></span>
  
<span data-ttu-id="d281e-142">You can see a list of all ExpressRoute circuits and peerings in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d281e-142">You can see a list of all ExpressRoute circuits and peerings in the Azure portal.</span></span> <span data-ttu-id="d281e-143">For more information, see [View Microsoft peering details](expressroute-howto-routing-portal-resource-manager.md#getmsft).</span><span class="sxs-lookup"><span data-stu-id="d281e-143">For more information, see [View Microsoft peering details](expressroute-howto-routing-portal-resource-manager.md#getmsft).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d281e-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="d281e-144">Next steps</span></span>

<span data-ttu-id="d281e-145">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="d281e-145">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
