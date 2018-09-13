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
ms.openlocfilehash: e021a1b109f735dee16d75c05c26ab35e599a3d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871738"
---
### <a name="to-view-local-network-gateways"></a><span data-ttu-id="b71b6-103">To view local network gateways</span><span class="sxs-lookup"><span data-stu-id="b71b6-103">To view local network gateways</span></span>

<span data-ttu-id="b71b6-104">To view a list of the local network gateways, use the [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#az_network_local_gateway_list) command.</span><span class="sxs-lookup"><span data-stu-id="b71b6-104">To view a list of the local network gateways, use the [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#az_network_local_gateway_list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="to-verify-the-shared-key-values"></a><span data-ttu-id="b71b6-105">To verify the shared key values</span><span class="sxs-lookup"><span data-stu-id="b71b6-105">To verify the shared key values</span></span>

<span data-ttu-id="b71b6-106">Verify that the shared key value is the same value that you used for your VPN device configuration.</span><span class="sxs-lookup"><span data-stu-id="b71b6-106">Verify that the shared key value is the same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="b71b6-107">If it is not, either run the connection again using the value from the device, or update the device with the value from the return.</span><span class="sxs-lookup"><span data-stu-id="b71b6-107">If it is not, either run the connection again using the value from the device, or update the device with the value from the return.</span></span> <span data-ttu-id="b71b6-108">The values must match.</span><span class="sxs-lookup"><span data-stu-id="b71b6-108">The values must match.</span></span> <span data-ttu-id="b71b6-109">To view the shared key, use the [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#az_network_vpn_connection_list).</span><span class="sxs-lookup"><span data-stu-id="b71b6-109">To view the shared key, use the [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#az_network_vpn_connection_list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="to-view-the-vpn-gateway-public-ip-address"></a><span data-ttu-id="b71b6-110">To view the VPN gateway Public IP address</span><span class="sxs-lookup"><span data-stu-id="b71b6-110">To view the VPN gateway Public IP address</span></span>

<span data-ttu-id="b71b6-111">To find the public IP address of your virtual network gateway, use the [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#az_network_public_ip_list) command.</span><span class="sxs-lookup"><span data-stu-id="b71b6-111">To find the public IP address of your virtual network gateway, use the [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#az_network_public_ip_list) command.</span></span> <span data-ttu-id="b71b6-112">For easy reading, the output for this example is formatted to display the list of public IPs in table format.</span><span class="sxs-lookup"><span data-stu-id="b71b6-112">For easy reading, the output for this example is formatted to display the list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
