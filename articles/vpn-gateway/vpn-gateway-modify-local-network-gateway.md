---
title: Modify the local network gateway IP address prefixes and the VPN Gateway IP address| Azure| PowerShell| Microsoft Docs
description: This article walks you through changing IP address prefixes for your local network gateway
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/05/2017
ms.author: cherylmc
ms.openlocfilehash: a26cbe2172dc27c152246d70b7f6b504ec4a08a5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555867"
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="b15cb-103">Modify local network gateway settings using PowerShell</span><span class="sxs-lookup"><span data-stu-id="b15cb-103">Modify local network gateway settings using PowerShell</span></span>
<span data-ttu-id="b15cb-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span><span class="sxs-lookup"><span data-stu-id="b15cb-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="b15cb-105">The instructions below will help you modify your local network gateway settings.</span><span class="sxs-lookup"><span data-stu-id="b15cb-105">The instructions below will help you modify your local network gateway settings.</span></span> <span data-ttu-id="b15cb-106">You can also modify these settings in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b15cb-106">You can also modify these settings in the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b15cb-107">Before you begin</span><span class="sxs-lookup"><span data-stu-id="b15cb-107">Before you begin</span></span>
<span data-ttu-id="b15cb-108">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b15cb-108">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="b15cb-109">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b15cb-109">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span>

## <a name="to-modify-ip-address-prefixes"></a><span data-ttu-id="b15cb-110">To modify IP address prefixes</span><span class="sxs-lookup"><span data-stu-id="b15cb-110">To modify IP address prefixes</span></span>
[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="to-modify-the-gateway-ip-address"></a><span data-ttu-id="b15cb-111">To modify the gateway IP address</span><span class="sxs-lookup"><span data-stu-id="b15cb-111">To modify the gateway IP address</span></span>
[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b15cb-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="b15cb-112">Next steps</span></span>
<span data-ttu-id="b15cb-113">You can verify your gateway connection.</span><span class="sxs-lookup"><span data-stu-id="b15cb-113">You can verify your gateway connection.</span></span> <span data-ttu-id="b15cb-114">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b15cb-114">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

