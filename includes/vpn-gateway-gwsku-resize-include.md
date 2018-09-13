---
title: include file
description: include file
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: c06e69dd9d1997500589659e936dc25ee01ed145
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45108887"
---
<span data-ttu-id="7a842-103">For the current SKUs (VpnGw1, VpnGw2, and VPNGW3) you want to resize your gateway SKU to upgrade to a more powerful one, you can use the `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7a842-103">For the current SKUs (VpnGw1, VpnGw2, and VPNGW3) you want to resize your gateway SKU to upgrade to a more powerful one, you can use the `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="7a842-104">You can also downgrade the gateway SKU size using this cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7a842-104">You can also downgrade the gateway SKU size using this cmdlet.</span></span> <span data-ttu-id="7a842-105">If you are using the Basic gateway SKU, [use these instructions instead](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md#resize) to resize your gateway.</span><span class="sxs-lookup"><span data-stu-id="7a842-105">If you are using the Basic gateway SKU, [use these instructions instead](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md#resize) to resize your gateway.</span></span>

<span data-ttu-id="7a842-106">The following PowerShell example shows a gateway SKU being resized to VpnGw2.</span><span class="sxs-lookup"><span data-stu-id="7a842-106">The following PowerShell example shows a gateway SKU being resized to VpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

<span data-ttu-id="7a842-107">You can also resize a gateway in the Azure portal by going to the **Configuration** page for your virtual network gateway and selecting a different SKU from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="7a842-107">You can also resize a gateway in the Azure portal by going to the **Configuration** page for your virtual network gateway and selecting a different SKU from the dropdown.</span></span>