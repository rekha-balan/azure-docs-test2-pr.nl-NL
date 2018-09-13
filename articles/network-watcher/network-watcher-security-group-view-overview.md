---
title: Introduction to security group view in Azure Network Watcher | Microsoft Docs
description: This page provides an overview of the Network Watcher security view capability
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 6c72073727423120e68edc683546ae1c9eb48f5f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670976"
---
# <a name="introduction-to-network-security-group-view-in-azure-network-watcher"></a>Introduction to network security group view in Azure Network Watcher

Network Security group can be associated at a subnet level or at a NIC level. When associated at a subnet level, it applies to all the VM instances in the subnet. Network Security Group view returns all the configured NSG and rules that are associated at a NIC and subnet level. In addition, the effective security rules are returned for each of the NICs in a VM. Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports. You can also validate if your Network Security Group is working as expected based on a comparison between the configured and the effective security rules.

A more extended use case is in security compliance and audit. You can define a prescriptive set of security rules as a model for security governance in your organization. A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.

In the portal rules are divided by Effective, Subnet, Network Interface, and Default. This provides a simple view into the rules applied to a virtual machine. A download button is provided to easily download all the security rules no matter the tab into a CSV file.

![security group view][1]

Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes. From this blade you can navigate directly to the Network Security Group resource.

![drilldown][2]

### <a name="next-steps"></a>Next steps

Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-security-group-view-overview/figure1.png











