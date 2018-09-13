---
title: What to do in the event of an Azure service disruption impacting Azure Virtual Networks | Microsoft Docs
description: Learn what to do in the event of an Azure service disruption impacting Azure Virtual Networks.
services: virtual-network
documentationcenter: ''
author: NarayanAnnamalai
manager: jefco
editor: ''
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: eff05815014a04c076bf0fd17981242962387d54
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661554"
---
# <a name="virtual-network--business-continuity"></a>Virtual Network – Business Continuity
## <a name="overview"></a>Overview
A Virtual Network (VNet) is a logical representation of your network in the cloud. It allows you to define your own private IP address space and segment the network into subnets. VNets serves as a trust boundary to host your compute resources such as Azure Virtual Machines and Cloud Services (web/worker roles). A VNet allows direct private IP communication between the resources hosted in it. A Virtual Network can also be linked to an on-premises network through one of the hybrid options such as a VPN Gateway or ExpressRoute.

A VNet is created within the scope of a region. You can create VNets with same address space in two different regions (i.e. US East and US West but cannot connect them to one another directly). 

## <a name="business-continuity"></a>Business Continuity
There could be several different ways that your application could be disrupted. A given region could be completely cut off due to a natural disaster or a partial disaster due to a failure of multiple devices/services. The impact on the VNet service is different in each of these situations.

**Q: What do you do in the event of an outage to an entire region? i.e. if a region is completely cutoff due to a natural disaster? What happens to the Virtual Networks hosted in the region?**

A: The Virtual Network and the resources in the affected region remains inaccessible during the time of the service disruption.

![Simple Virtual Network Diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-disaster-recovery-guidance/vnet.png)

**Q: What can I to do re-create the same Virtual Network in a different region?**

A: Virtual Network (VNet) is fairly lightweight resource. You can invoke Azure APIs to create a VNet with the same address space in a different region. To re-create the same environment that was present in the affected region, you have to make API calls to re-deploy your Cloud Services (web/worker roles) and Virtual Machines that you had. You will also have to spin up a VPN Gateway and connect to your on-premises network if you had on-premises connectivity (such as in a hybrid deployment).

The instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md). 

**Q: Can a replica of a VNet in a given region be re-created in another region ahead of time?**

A: Yes, you can create two VNets using the same private IP address space and resources in two different regions ahead of time. If a customer was hosting internet facing services in the VNet, they could have set up Traffic Manager to geo-route traffic to the region that is active. However, a customer cannot connect two VNets with the same address space to their on-premises network as it would cause routing issues. At the time of a disaster and loss of a VNet in one region, a customer can connect the other VNet in the available region with matching address space to their on-premises network.

The instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).


