---
title: Introduction to IP flow verify in Azure Network Watcher | Microsoft Docs
description: This page provides an overview of the Network Watcher IP flow verify capability
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c960a45a5e237e13f7cce6b4b2e3bd4827754b30
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556008"
---
# <a name="introduction-to-ip-flow-verify-in-azure-network-watcher"></a>Introduction to IP flow verify in Azure Network Watcher

IP flow verify checks if a packet is allowed or denied to or from a virtual machine based on 5-tuple information. This information consists of direction, protocol, local IP, remote IP, local port, and remote port. If the packet is denied by a security group, the name of the rule that denied the packet is returned. While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or to the internet and from or to the on-premises environment.

IP flow verify targets a network interface of a virtual machine. Traffic flow is then verified based on the configured settings to or from that network interface. This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic to or from a virtual machine.

An instance of Network Watcher needs to be created in all regions that you plan to run IP flow verify. Network Watcher is a regional service and can only be ran against resources in the same region. This does not affect the results of IP flow verify as the route associated with the NIC will still be returned.

![1][1]

## <a name="next-steps"></a>Next steps

Visit the following article to learn if a packet is allowed or denied for a specific virtual machine through the portal. [Check if traffic is allowed on a VM with IP Flow Verify using the portal](network-watcher-check-ip-flow-verify-portal.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-ip-flow-verify-overview/figure1.png













