---
title: Azure CLI Samples for Load Balancer| Microsoft Docs
description: Azure CLI Samples
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: jeconnoc
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 06/14/2018
ms.author: kumud
ms.openlocfilehash: 41e80e04051a24fd32086c61c65bc3eec1564c57
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865343"
---
# <a name="azure-cli-samples-for-load-balancer"></a>Azure CLI Samples for Load Balancer

The following table includes links to bash scripts built using the Azure CLI.

| | |
|-|-|
| [Load balance traffic to VMs for high availability](./scripts/load-balancer-linux-cli-sample-nlb.md) | Creates several virtual machines in a highly available and load balanced configuration. |
| [Load balance VMs across availability zones](./scripts/load-balancer-linux-cli-sample-zone-redundant-frontend.md) | Creates three VMs in different availability zones within a region and Standard Load Balancer with a zone-redundant frontend IP address. This load balancer configuration helps to protect your apps and data from an unlikely failure or loss of an entire datacenter. |
|[Load balance VMs within a specific availability zone](./scripts/load-balancer-linux-cli-sample-zonal-frontend.md)|Creates three VMs, a Standard Load Balancer with zonal frontend IP that helps align data path and resources in a single zone for a given region.|
| [Load balance multiple websites on VMs](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md) | Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer. |
| | |

