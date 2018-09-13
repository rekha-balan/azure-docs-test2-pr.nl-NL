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
ms.openlocfilehash: 9b168231669c50c8f00d3527288fd03ab3bf9ce8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45408565"
---
### <a name="noconnection"></a><span data-ttu-id="900ee-103">To modify local network gateway IP address prefixes - no gateway connection</span><span class="sxs-lookup"><span data-stu-id="900ee-103">To modify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="900ee-104">If you don't have a gateway connection and you want to add or remove IP address prefixes, you use the same command that you use to create the local network gateway, [az network local-gateway create](https://docs.microsoft.com/cli/azure/network/local-gateway#az_network_local_gateway_create).</span><span class="sxs-lookup"><span data-stu-id="900ee-104">If you don't have a gateway connection and you want to add or remove IP address prefixes, you use the same command that you use to create the local network gateway, [az network local-gateway create](https://docs.microsoft.com/cli/azure/network/local-gateway#az_network_local_gateway_create).</span></span> <span data-ttu-id="900ee-105">You can also use this command to update the gateway IP address for the VPN device.</span><span class="sxs-lookup"><span data-stu-id="900ee-105">You can also use this command to update the gateway IP address for the VPN device.</span></span> <span data-ttu-id="900ee-106">To overwrite the current settings, use the existing name of your local network gateway.</span><span class="sxs-lookup"><span data-stu-id="900ee-106">To overwrite the current settings, use the existing name of your local network gateway.</span></span> <span data-ttu-id="900ee-107">If you use a different name, you create a new local network gateway, instead of overwriting the existing one.</span><span class="sxs-lookup"><span data-stu-id="900ee-107">If you use a different name, you create a new local network gateway, instead of overwriting the existing one.</span></span>

<span data-ttu-id="900ee-108">Each time you make a change, the entire list of prefixes must be specified, not just the prefixes that you want to change.</span><span class="sxs-lookup"><span data-stu-id="900ee-108">Each time you make a change, the entire list of prefixes must be specified, not just the prefixes that you want to change.</span></span> <span data-ttu-id="900ee-109">Specify only the prefixes that you want to keep.</span><span class="sxs-lookup"><span data-stu-id="900ee-109">Specify only the prefixes that you want to keep.</span></span> <span data-ttu-id="900ee-110">In this case, 10.0.0.0/24 and 20.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="900ee-110">In this case, 10.0.0.0/24 and 20.0.0.0/24</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 -g TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a><span data-ttu-id="900ee-111">To modify local network gateway IP address prefixes - existing gateway connection</span><span class="sxs-lookup"><span data-stu-id="900ee-111">To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="900ee-112">If you have a gateway connection and want to add or remove IP address prefixes, you can update the prefixes using [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#az_network_local_gateway_update).</span><span class="sxs-lookup"><span data-stu-id="900ee-112">If you have a gateway connection and want to add or remove IP address prefixes, you can update the prefixes using [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#az_network_local_gateway_update).</span></span> <span data-ttu-id="900ee-113">This results in some downtime for your VPN connection.</span><span class="sxs-lookup"><span data-stu-id="900ee-113">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="900ee-114">When modifying the IP address prefixes, you don't need to delete the VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="900ee-114">When modifying the IP address prefixes, you don't need to delete the VPN gateway.</span></span>

<span data-ttu-id="900ee-115">Each time you make a change, the entire list of prefixes must be specified, not just the prefixes that you want to change.</span><span class="sxs-lookup"><span data-stu-id="900ee-115">Each time you make a change, the entire list of prefixes must be specified, not just the prefixes that you want to change.</span></span> <span data-ttu-id="900ee-116">In this example, 10.0.0.0/24 and 20.0.0.0/24 are already present.</span><span class="sxs-lookup"><span data-stu-id="900ee-116">In this example, 10.0.0.0/24 and 20.0.0.0/24 are already present.</span></span> <span data-ttu-id="900ee-117">We add the prefixes 30.0.0.0/24 and 40.0.0.0/24 and specify all 4 of the prefixes when updating.</span><span class="sxs-lookup"><span data-stu-id="900ee-117">We add the prefixes 30.0.0.0/24 and 40.0.0.0/24 and specify all 4 of the prefixes when updating.</span></span>

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 -g TestRG1
```
