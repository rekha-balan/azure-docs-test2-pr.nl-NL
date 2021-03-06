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
ms.openlocfilehash: a8dec00373d991a7aeaf11f1a4d95463ab71d9a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45191411"
---
1. In the [portal](http://portal.azure.com), navigate to the Resource Manager virtual network for which you want to create a virtual network gateway.
2. In the **Settings** section of your VNet page, click **Subnets** to expand the **Subnets** page.
3. On the **Subnets** page, click **+Gateway subnet** to open the **Add subnet** page. 

  ![Add the gateway subnet](./media/vpn-gateway-add-gwsubnet-p2s-rm-portal-include/addgwsubnet.png "Add the gateway subnet")
4. The **Name** for your subnet is automatically filled in with the value 'GatewaySubnet'. This value is required in order for Azure to recognize the subnet as the gateway subnet. Adjust the auto-filled **Address range** values to match your configuration requirements, then click **OK** at the bottom of the page to create the subnet.

  ![Adding the subnet](./media/vpn-gateway-add-gwsubnet-p2s-rm-portal-include/p2sgwsub.png "Adding the subnet")