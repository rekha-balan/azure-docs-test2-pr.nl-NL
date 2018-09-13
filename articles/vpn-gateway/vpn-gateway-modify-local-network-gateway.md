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
# <a name="modify-local-network-gateway-settings-using-powershell"></a>Modify local network gateway settings using PowerShell
Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change. The instructions below will help you modify your local network gateway settings. You can also modify these settings in the Azure portal.

## <a name="before-you-begin"></a>Before you begin
You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets. See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.

## <a name="to-modify-ip-address-prefixes"></a>To modify IP address prefixes
[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="to-modify-the-gateway-ip-address"></a>To modify the gateway IP address
[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Next steps
You can verify your gateway connection. See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).

