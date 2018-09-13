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
ms.openlocfilehash: a79184a5e08aa43a4675194adf5f10b9807418db
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868201"
---
### <a name="gwipnoconnection"></a> To modify the local network gateway IP address - no gateway connection

Use the example to modify a local network gateway that does not have a gateway connection. When modifying this value, you can also modify the address prefixes at the same time.

1. On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.
2. In the **IP address** box, modify the IP address.
3. Click **Save** to save the settings.

### <a name="gwipwithconnection"></a>To modify the local network gateway IP address - existing gateway connection

To modify a local network gateway that has a connection, you need to first remove the connection. After the connection is removed, you can modify the gateway IP address and recreate a new connection. You can also modify the address prefixes at the same time. This results in some downtime for your VPN connection. When modifying the gateway IP address, you don't need to delete the VPN gateway. You only need to remove the connection.
 
#### <a name="1-remove-the-connection"></a>1. Remove the connection.

1. On the Local Network Gateway resource, in the **Settings** section, click **Connections**.
2. Click the **...** on the line for the connection, then click **Delete**.
3. Click **Save** to save your settings.

#### <a name="2-modify-the-ip-address"></a>2. Modify the IP address.

You can also modify the address prefixes at the same time.

1. In the **IP address** box, modify the IP address.
2. Click **Save** to save the settings.

#### <a name="3-recreate-the-connection"></a>3. Recreate the connection.

1. Navigate to the Virtual Network Gateway for your VNet. (Not the Local Network Gateway.)
2. On the Virtual Network Gateway, in the **Settings** section, click **Connections**.
3. Click the **+ Add** to open the **Add connection** blade.
4. Recreate your connection.
5. Click **OK** to create the connection.