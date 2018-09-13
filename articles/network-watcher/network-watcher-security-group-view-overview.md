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
# <a name="introduction-to-network-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="fbf7f-103">Introduction to network security group view in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="fbf7f-103">Introduction to network security group view in Azure Network Watcher</span></span>

<span data-ttu-id="fbf7f-104">Network Security group can be associated at a subnet level or at a NIC level.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-104">Network Security group can be associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="fbf7f-105">When associated at a subnet level, it applies to all the VM instances in the subnet.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-105">When associated at a subnet level, it applies to all the VM instances in the subnet.</span></span> <span data-ttu-id="fbf7f-106">Network Security Group view returns all the configured NSG and rules that are associated at a NIC and subnet level.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-106">Network Security Group view returns all the configured NSG and rules that are associated at a NIC and subnet level.</span></span> <span data-ttu-id="fbf7f-107">In addition, the effective security rules are returned for each of the NICs in a VM.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-107">In addition, the effective security rules are returned for each of the NICs in a VM.</span></span> <span data-ttu-id="fbf7f-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="fbf7f-109">You can also validate if your Network Security Group is working as expected based on a comparison between the configured and the effective security rules.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-109">You can also validate if your Network Security Group is working as expected based on a comparison between the configured and the effective security rules.</span></span>

<span data-ttu-id="fbf7f-110">A more extended use case is in security compliance and audit.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-110">A more extended use case is in security compliance and audit.</span></span> <span data-ttu-id="fbf7f-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="fbf7f-112">A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-112">A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.</span></span>

<span data-ttu-id="fbf7f-113">In the portal rules are divided by Effective, Subnet, Network Interface, and Default.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-113">In the portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="fbf7f-114">This provides a simple view into the rules applied to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-114">This provides a simple view into the rules applied to a virtual machine.</span></span> <span data-ttu-id="fbf7f-115">A download button is provided to easily download all the security rules no matter the tab into a CSV file.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-115">A download button is provided to easily download all the security rules no matter the tab into a CSV file.</span></span>

![security group view][1]

<span data-ttu-id="fbf7f-117">Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-117">Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="fbf7f-118">From this blade you can navigate directly to the Network Security Group resource.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-118">From this blade you can navigate directly to the Network Security Group resource.</span></span>

![drilldown][2]

### <a name="next-steps"></a><span data-ttu-id="fbf7f-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbf7f-120">Next steps</span></span>

<span data-ttu-id="fbf7f-121">Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="fbf7f-121">Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-security-group-view-overview/figure1.png











