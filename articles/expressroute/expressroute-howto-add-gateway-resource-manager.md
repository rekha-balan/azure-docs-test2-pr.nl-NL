---
title: 'Add a virtual network gateway to a VNet for ExpressRoute: PowerShell: Azure | Microsoft Docs'
description: This article walks you through adding a VNet gateway to an already created Resource Manager VNet for ExpressRoute.
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 50af8a024c71cbe931cc944d052493bbb0fa9ad1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563979"
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="4ee04-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ee04-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Classic - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - Azure portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="4ee04-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span><span class="sxs-lookup"><span data-stu-id="4ee04-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="4ee04-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span><span class="sxs-lookup"><span data-stu-id="4ee04-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="4ee04-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="4ee04-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="4ee04-111">Before beginning</span><span class="sxs-lookup"><span data-stu-id="4ee04-111">Before beginning</span></span>
<span data-ttu-id="4ee04-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="4ee04-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="4ee04-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span><span class="sxs-lookup"><span data-stu-id="4ee04-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="4ee04-114">For more information, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="4ee04-114">For more information, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4ee04-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ee04-115">Next steps</span></span>
<span data-ttu-id="4ee04-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="4ee04-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="4ee04-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="4ee04-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

