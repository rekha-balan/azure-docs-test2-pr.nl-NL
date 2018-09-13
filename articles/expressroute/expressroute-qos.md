---
title: QoS Requirements for ExpressRoute | Microsoft Docs
description: This page provides detailed requirements for configuring and managing QoS for ExpressRoute circuits.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: ''
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 62c74f59768c8bb28839659945b812d5aeb72625
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662778"
---
# <a name="expressroute-qos-requirements"></a>ExpressRoute QoS requirements
Skype for Business has various workloads that require differentiated QoS treatment. If you plan to consume voice services through ExpressRoute, you should adhere to the requirements described below.

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> QoS requirements apply to the Microsoft peering only. The DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset to 0. 
> 
> 

The following table provides a list of DSCP markings used by Skype for Business. Refer to [Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.

| **Traffic Class** | **Treatment (DSCP Marking)** | **Skype for Business Workloads** |
| --- | --- | --- |
| **Voice** |EF (46) |Skype / Lync voice |
| **Interactive** |AF41 (34) |Video |
| AF21 (18) |App sharing | |
| **Default** |AF11 (10) |File transfer |
| CS0 (0) |Anything else | |

* You should classify the workloads and mark the right DSCP values. Follow the guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how to set DSCP markings in your network.
* You should configure and support multiple QoS queues within your network. Voice must be a standalone class and receive the EF treatment specified in RFC 3246. 
* You can decide the queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class. But, the DSCP marking for Skype for Business workloads must be preserved. If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value to 0 before sending the packet to Microsoft. Microsoft only sends packets marked with the DSCP value shown in the above table. 

## <a name="next-steps"></a>Next steps
* Refer to the requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).
* See the following links to configure your ExpressRoute connection.
  
  * [Create an ExpressRoute circuit](expressroute-howto-circuit-classic.md)
  * [Configure routing](expressroute-howto-routing-classic.md)
  * [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md)


