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
ms.openlocfilehash: d8091fdade9cd417af58755d8245c2fb091b86b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867871"
---
The following table lists the requirements for PolicyBased and RouteBased VPN gateways. This table applies to both the Resource Manager and classic deployment models. For the classic model, PolicyBased VPN gateways are the same as Static gateways, and Route-based gateways are the same as Dynamic gateways.

|  | **PolicyBased Basic VPN Gateway** | **RouteBased Basic VPN Gateway** | **RouteBased Standard VPN Gateway** | **RouteBased High Performance VPN Gateway** |
| --- | --- | --- | --- | --- |
| **Site-to-Site connectivity   (S2S)** |PolicyBased VPN configuration |RouteBased VPN configuration |RouteBased VPN configuration |RouteBased VPN configuration |
| **Point-to-Site connectivity (P2S**) |Not supported |Supported (Can coexist with S2S) |Supported (Can coexist with S2S) |Supported (Can coexist with S2S) |
| **Authentication method** |Pre-shared key |Pre-shared key for S2S connectivity, Certificates for P2S connectivity |Pre-shared key for S2S connectivity, Certificates for P2S connectivity |Pre-shared key for S2S connectivity, Certificates for P2S connectivity |
| **Maximum number of S2S connections** |1 |10 |10 |30 |
| **Maximum number of P2S connections** |Not supported |128 |128 |128 |
| **Active routing support (BGP)** |Not supported |Not supported |Supported |Supported |
