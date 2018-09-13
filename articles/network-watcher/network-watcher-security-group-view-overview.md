---
title: Introduction to security group view in Azure Network Watcher | Microsoft Docs
description: This page provides an overview of the Network Watcher security view capability
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: jdial
ms.openlocfilehash: 15f6bd0d7da63924e52db8ec7e2cbb0ee7483f82
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830973"
---
# <a name="introduction-to-network-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="1a706-103">Introduction to network security group view in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="1a706-103">Introduction to network security group view in Azure Network Watcher</span></span>

<span data-ttu-id="1a706-104">Network Security groups are associated at a subnet level or at a NIC level.</span><span class="sxs-lookup"><span data-stu-id="1a706-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="1a706-105">When associated at a subnet level, it applies to all the VM instances in the subnet.</span><span class="sxs-lookup"><span data-stu-id="1a706-105">When associated at a subnet level, it applies to all the VM instances in the subnet.</span></span> <span data-ttu-id="1a706-106">Network Security Group view returns all the configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into the configuration.</span><span class="sxs-lookup"><span data-stu-id="1a706-106">Network Security Group view returns all the configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into the configuration.</span></span> <span data-ttu-id="1a706-107">In addition, the effective security rules are returned for each of the NICs in a VM.</span><span class="sxs-lookup"><span data-stu-id="1a706-107">In addition, the effective security rules are returned for each of the NICs in a VM.</span></span> <span data-ttu-id="1a706-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span><span class="sxs-lookup"><span data-stu-id="1a706-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="1a706-109">You can also validate if your Network Security Group is working as expected based on a [comparison between the configured and the approved security rules](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1a706-109">You can also validate if your Network Security Group is working as expected based on a [comparison between the configured and the approved security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="1a706-110">A more extended use case is in security compliance and auditing.</span><span class="sxs-lookup"><span data-stu-id="1a706-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="1a706-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span><span class="sxs-lookup"><span data-stu-id="1a706-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="1a706-112">A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.</span><span class="sxs-lookup"><span data-stu-id="1a706-112">A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.</span></span>

<span data-ttu-id="1a706-113">In the portal rules are divided by Effective, Subnet, Network Interface, and Default.</span><span class="sxs-lookup"><span data-stu-id="1a706-113">In the portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="1a706-114">This provides a simple view into the rules applied to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1a706-114">This provides a simple view into the rules applied to a virtual machine.</span></span> <span data-ttu-id="1a706-115">A download button is provided to easily download all the security rules no matter the tab into a CSV file.</span><span class="sxs-lookup"><span data-stu-id="1a706-115">A download button is provided to easily download all the security rules no matter the tab into a CSV file.</span></span>

![security group view][1]

<span data-ttu-id="1a706-117">Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes.</span><span class="sxs-lookup"><span data-stu-id="1a706-117">Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="1a706-118">From this blade you can navigate directly to the Network Security Group resource.</span><span class="sxs-lookup"><span data-stu-id="1a706-118">From this blade you can navigate directly to the Network Security Group resource.</span></span>

![drilldown][2]

### <a name="next-steps"></a><span data-ttu-id="1a706-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a706-120">Next steps</span></span>

<span data-ttu-id="1a706-121">Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="1a706-121">Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









