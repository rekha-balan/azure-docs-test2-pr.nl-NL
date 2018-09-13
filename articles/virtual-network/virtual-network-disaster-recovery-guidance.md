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
# <a name="virtual-network--business-continuity"></a><span data-ttu-id="ac275-103">Virtual Network – Business Continuity</span><span class="sxs-lookup"><span data-stu-id="ac275-103">Virtual Network – Business Continuity</span></span>
## <a name="overview"></a><span data-ttu-id="ac275-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ac275-104">Overview</span></span>
<span data-ttu-id="ac275-105">A Virtual Network (VNet) is a logical representation of your network in the cloud.</span><span class="sxs-lookup"><span data-stu-id="ac275-105">A Virtual Network (VNet) is a logical representation of your network in the cloud.</span></span> <span data-ttu-id="ac275-106">It allows you to define your own private IP address space and segment the network into subnets.</span><span class="sxs-lookup"><span data-stu-id="ac275-106">It allows you to define your own private IP address space and segment the network into subnets.</span></span> <span data-ttu-id="ac275-107">VNets serves as a trust boundary to host your compute resources such as Azure Virtual Machines and Cloud Services (web/worker roles).</span><span class="sxs-lookup"><span data-stu-id="ac275-107">VNets serves as a trust boundary to host your compute resources such as Azure Virtual Machines and Cloud Services (web/worker roles).</span></span> <span data-ttu-id="ac275-108">A VNet allows direct private IP communication between the resources hosted in it.</span><span class="sxs-lookup"><span data-stu-id="ac275-108">A VNet allows direct private IP communication between the resources hosted in it.</span></span> <span data-ttu-id="ac275-109">A Virtual Network can also be linked to an on-premises network through one of the hybrid options such as a VPN Gateway or ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ac275-109">A Virtual Network can also be linked to an on-premises network through one of the hybrid options such as a VPN Gateway or ExpressRoute.</span></span>

<span data-ttu-id="ac275-110">A VNet is created within the scope of a region.</span><span class="sxs-lookup"><span data-stu-id="ac275-110">A VNet is created within the scope of a region.</span></span> <span data-ttu-id="ac275-111">You can create VNets with same address space in two different regions (i.e. US East and US West but cannot connect them to one another directly).</span><span class="sxs-lookup"><span data-stu-id="ac275-111">You can create VNets with same address space in two different regions (i.e. US East and US West but cannot connect them to one another directly).</span></span> 

## <a name="business-continuity"></a><span data-ttu-id="ac275-112">Business Continuity</span><span class="sxs-lookup"><span data-stu-id="ac275-112">Business Continuity</span></span>
<span data-ttu-id="ac275-113">There could be several different ways that your application could be disrupted.</span><span class="sxs-lookup"><span data-stu-id="ac275-113">There could be several different ways that your application could be disrupted.</span></span> <span data-ttu-id="ac275-114">A given region could be completely cut off due to a natural disaster or a partial disaster due to a failure of multiple devices/services.</span><span class="sxs-lookup"><span data-stu-id="ac275-114">A given region could be completely cut off due to a natural disaster or a partial disaster due to a failure of multiple devices/services.</span></span> <span data-ttu-id="ac275-115">The impact on the VNet service is different in each of these situations.</span><span class="sxs-lookup"><span data-stu-id="ac275-115">The impact on the VNet service is different in each of these situations.</span></span>

<span data-ttu-id="ac275-116">**Q: What do you do in the event of an outage to an entire region? i.e. if a region is completely cutoff due to a natural disaster? What happens to the Virtual Networks hosted in the region?**</span><span class="sxs-lookup"><span data-stu-id="ac275-116">**Q: What do you do in the event of an outage to an entire region? i.e. if a region is completely cutoff due to a natural disaster? What happens to the Virtual Networks hosted in the region?**</span></span>

<span data-ttu-id="ac275-117">A: The Virtual Network and the resources in the affected region remains inaccessible during the time of the service disruption.</span><span class="sxs-lookup"><span data-stu-id="ac275-117">A: The Virtual Network and the resources in the affected region remains inaccessible during the time of the service disruption.</span></span>

![Simple Virtual Network Diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-disaster-recovery-guidance/vnet.png)

<span data-ttu-id="ac275-119">**Q: What can I to do re-create the same Virtual Network in a different region?**</span><span class="sxs-lookup"><span data-stu-id="ac275-119">**Q: What can I to do re-create the same Virtual Network in a different region?**</span></span>

<span data-ttu-id="ac275-120">A: Virtual Network (VNet) is fairly lightweight resource.</span><span class="sxs-lookup"><span data-stu-id="ac275-120">A: Virtual Network (VNet) is fairly lightweight resource.</span></span> <span data-ttu-id="ac275-121">You can invoke Azure APIs to create a VNet with the same address space in a different region.</span><span class="sxs-lookup"><span data-stu-id="ac275-121">You can invoke Azure APIs to create a VNet with the same address space in a different region.</span></span> <span data-ttu-id="ac275-122">To re-create the same environment that was present in the affected region, you have to make API calls to re-deploy your Cloud Services (web/worker roles) and Virtual Machines that you had.</span><span class="sxs-lookup"><span data-stu-id="ac275-122">To re-create the same environment that was present in the affected region, you have to make API calls to re-deploy your Cloud Services (web/worker roles) and Virtual Machines that you had.</span></span> <span data-ttu-id="ac275-123">You will also have to spin up a VPN Gateway and connect to your on-premises network if you had on-premises connectivity (such as in a hybrid deployment).</span><span class="sxs-lookup"><span data-stu-id="ac275-123">You will also have to spin up a VPN Gateway and connect to your on-premises network if you had on-premises connectivity (such as in a hybrid deployment).</span></span>

<span data-ttu-id="ac275-124">The instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="ac275-124">The instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span></span> 

<span data-ttu-id="ac275-125">**Q: Can a replica of a VNet in a given region be re-created in another region ahead of time?**</span><span class="sxs-lookup"><span data-stu-id="ac275-125">**Q: Can a replica of a VNet in a given region be re-created in another region ahead of time?**</span></span>

<span data-ttu-id="ac275-126">A: Yes, you can create two VNets using the same private IP address space and resources in two different regions ahead of time.</span><span class="sxs-lookup"><span data-stu-id="ac275-126">A: Yes, you can create two VNets using the same private IP address space and resources in two different regions ahead of time.</span></span> <span data-ttu-id="ac275-127">If a customer was hosting internet facing services in the VNet, they could have set up Traffic Manager to geo-route traffic to the region that is active.</span><span class="sxs-lookup"><span data-stu-id="ac275-127">If a customer was hosting internet facing services in the VNet, they could have set up Traffic Manager to geo-route traffic to the region that is active.</span></span> <span data-ttu-id="ac275-128">However, a customer cannot connect two VNets with the same address space to their on-premises network as it would cause routing issues.</span><span class="sxs-lookup"><span data-stu-id="ac275-128">However, a customer cannot connect two VNets with the same address space to their on-premises network as it would cause routing issues.</span></span> <span data-ttu-id="ac275-129">At the time of a disaster and loss of a VNet in one region, a customer can connect the other VNet in the available region with matching address space to their on-premises network.</span><span class="sxs-lookup"><span data-stu-id="ac275-129">At the time of a disaster and loss of a VNet in one region, a customer can connect the other VNet in the available region with matching address space to their on-premises network.</span></span>

<span data-ttu-id="ac275-130">The instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="ac275-130">The instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span></span>


