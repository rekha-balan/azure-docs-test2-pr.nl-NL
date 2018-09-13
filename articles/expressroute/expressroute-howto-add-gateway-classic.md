---
title: 'Configure a VNet gateway for ExpressRoute using PowerShell: classic: Azure | Microsoft Docs'
description: Configure a VNet gateway for a classic deployment model VNet using PowerShell for an ExpressRoute configuration.
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: ''
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: badec4e0b542db52f34db3c50f7d906ed6a5a377
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556510"
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="b1a94-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span><span class="sxs-lookup"><span data-stu-id="b1a94-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Classic - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="b1a94-107">This article will walk you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span><span class="sxs-lookup"><span data-stu-id="b1a94-107">This article will walk you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="b1a94-108">The steps for this configuration are specifically for VNets that were created using the **classic deployment model** and that will be be used in an ExpressRoute configuration.</span><span class="sxs-lookup"><span data-stu-id="b1a94-108">The steps for this configuration are specifically for VNets that were created using the **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="b1a94-109">**About Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="b1a94-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="b1a94-110">Before beginning</span><span class="sxs-lookup"><span data-stu-id="b1a94-110">Before beginning</span></span>
<span data-ttu-id="b1a94-111">Verify that you have installed the Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span><span class="sxs-lookup"><span data-stu-id="b1a94-111">Verify that you have installed the Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="b1a94-112">If you haven't installed the cmdlets, you'll need to do so before beginning the configuration steps.</span><span class="sxs-lookup"><span data-stu-id="b1a94-112">If you haven't installed the cmdlets, you'll need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="b1a94-113">For more information about installing Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="b1a94-113">For more information about installing Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b1a94-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1a94-114">Next steps</span></span>
<span data-ttu-id="b1a94-115">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="b1a94-115">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="b1a94-116">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="b1a94-116">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

