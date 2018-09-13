---
title: Connect to Azure Data Lake Store from VNETs | Microsoft Docs
description: Connect to Azure Data Lake Store from Azure VNETs
services: data-lake-store,data-catalog
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: 6e4d702d92b680219bccb164539bcd13ae46a8eb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563308"
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a><span data-ttu-id="98c2a-103">Access Azure Data Lake Store from VMs within an Azure VNET</span><span class="sxs-lookup"><span data-stu-id="98c2a-103">Access Azure Data Lake Store from VMs within an Azure VNET</span></span>
<span data-ttu-id="98c2a-104">Azure Data Lake Store is a PaaS service that runs on public Internet IP addresses.</span><span class="sxs-lookup"><span data-stu-id="98c2a-104">Azure Data Lake Store is a PaaS service that runs on public Internet IP addresses.</span></span> <span data-ttu-id="98c2a-105">Any server that can connect to the public Internet can typically connect to Azure Data Lake Store endpoints as well.</span><span class="sxs-lookup"><span data-stu-id="98c2a-105">Any server that can connect to the public Internet can typically connect to Azure Data Lake Store endpoints as well.</span></span> <span data-ttu-id="98c2a-106">By default, all VMs that are in Azure VNETs can access the Internet and hence can access Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="98c2a-106">By default, all VMs that are in Azure VNETs can access the Internet and hence can access Azure Data Lake Store.</span></span> <span data-ttu-id="98c2a-107">However, it is possible to configure VMs in a VNET to not have access to the Internet.</span><span class="sxs-lookup"><span data-stu-id="98c2a-107">However, it is possible to configure VMs in a VNET to not have access to the Internet.</span></span> <span data-ttu-id="98c2a-108">For such VMs, access to Azure Data Lake Store is restricted as well.</span><span class="sxs-lookup"><span data-stu-id="98c2a-108">For such VMs, access to Azure Data Lake Store is restricted as well.</span></span> <span data-ttu-id="98c2a-109">Blocking public Internet access for VMs in Azure VNETs can be done using any of the following approach.</span><span class="sxs-lookup"><span data-stu-id="98c2a-109">Blocking public Internet access for VMs in Azure VNETs can be done using any of the following approach.</span></span>

* <span data-ttu-id="98c2a-110">By configuring Network Security Groups (NSG)</span><span class="sxs-lookup"><span data-stu-id="98c2a-110">By configuring Network Security Groups (NSG)</span></span>
* <span data-ttu-id="98c2a-111">By configuring User Defined Routes (UDR)</span><span class="sxs-lookup"><span data-stu-id="98c2a-111">By configuring User Defined Routes (UDR)</span></span>
* <span data-ttu-id="98c2a-112">By exchanging routes via BGP (industry standard dynamic routing protocol) when ExpressRoute is used that block access to the Internet</span><span class="sxs-lookup"><span data-stu-id="98c2a-112">By exchanging routes via BGP (industry standard dynamic routing protocol) when ExpressRoute is used that block access to the Internet</span></span>

<span data-ttu-id="98c2a-113">In this article, you will learn how to enable access to the Azure Data Lake Store from Azure VMs which have been restricted to access resources using one of the three methods listed above.</span><span class="sxs-lookup"><span data-stu-id="98c2a-113">In this article, you will learn how to enable access to the Azure Data Lake Store from Azure VMs which have been restricted to access resources using one of the three methods listed above.</span></span>

## <a name="enabling-connectivity-to-azure-data-lake-store-from-vms-with-restricted-connectivity"></a><span data-ttu-id="98c2a-114">Enabling connectivity to Azure Data Lake Store from VMs with restricted connectivity</span><span class="sxs-lookup"><span data-stu-id="98c2a-114">Enabling connectivity to Azure Data Lake Store from VMs with restricted connectivity</span></span>
<span data-ttu-id="98c2a-115">To access Azure Data Lake Store from such VMs, you must configure them to access the IP address where the Azure Data Lake Store account is available.</span><span class="sxs-lookup"><span data-stu-id="98c2a-115">To access Azure Data Lake Store from such VMs, you must configure them to access the IP address where the Azure Data Lake Store account is available.</span></span> <span data-ttu-id="98c2a-116">You can identify the IP addresses for your Data Lake Store accounts by resolving the DNS names of your accounts (`<account>.azuredatalakestore.net`).</span><span class="sxs-lookup"><span data-stu-id="98c2a-116">You can identify the IP addresses for your Data Lake Store accounts by resolving the DNS names of your accounts (`<account>.azuredatalakestore.net`).</span></span> <span data-ttu-id="98c2a-117">For this you can use tools such as **nslookup**.</span><span class="sxs-lookup"><span data-stu-id="98c2a-117">For this you can use tools such as **nslookup**.</span></span> <span data-ttu-id="98c2a-118">Open a command prompt on your computer and run the following command.</span><span class="sxs-lookup"><span data-stu-id="98c2a-118">Open a command prompt on your computer and run the following command.</span></span>

    nslookup mydatastore.azuredatalakestore.net

<span data-ttu-id="98c2a-119">The output resembles the following.</span><span class="sxs-lookup"><span data-stu-id="98c2a-119">The output resembles the following.</span></span> <span data-ttu-id="98c2a-120">The value against **Address** property is the IP address associated with your Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="98c2a-120">The value against **Address** property is the IP address associated with your Data Lake Store account.</span></span>

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a><span data-ttu-id="98c2a-121">Enabling connectivity from VMs restricted by using NSG</span><span class="sxs-lookup"><span data-stu-id="98c2a-121">Enabling connectivity from VMs restricted by using NSG</span></span>
<span data-ttu-id="98c2a-122">When a NSG rule is used to block access to the Internet, then you can create another NSG that allows access to the Data Lake Store IP Address.</span><span class="sxs-lookup"><span data-stu-id="98c2a-122">When a NSG rule is used to block access to the Internet, then you can create another NSG that allows access to the Data Lake Store IP Address.</span></span> <span data-ttu-id="98c2a-123">More information on NSG rules is available at [What is a Network Security Group?](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="98c2a-123">More information on NSG rules is available at [What is a Network Security Group?](../virtual-network/virtual-networks-nsg.md).</span></span> <span data-ttu-id="98c2a-124">For instructions on how to create NSGs see [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="98c2a-124">For instructions on how to create NSGs see [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a><span data-ttu-id="98c2a-125">Enabling connectivity from VMs restricted by using UDR or ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="98c2a-125">Enabling connectivity from VMs restricted by using UDR or ExpressRoute</span></span>
<span data-ttu-id="98c2a-126">When routes, either UDRs or BGP-exchanged routes, are used to block access to the Internet, a special route needs to be configured so that VMs in such subnets can access Data Lake Store endpoints.</span><span class="sxs-lookup"><span data-stu-id="98c2a-126">When routes, either UDRs or BGP-exchanged routes, are used to block access to the Internet, a special route needs to be configured so that VMs in such subnets can access Data Lake Store endpoints.</span></span> <span data-ttu-id="98c2a-127">For more information, see [What are User Defined Routes?](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98c2a-127">For more information, see [What are User Defined Routes?](../virtual-network/virtual-networks-udr-overview.md).</span></span> <span data-ttu-id="98c2a-128">For instructions on creating UDRs, see [Create UDRs in Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="98c2a-128">For instructions on creating UDRs, see [Create UDRs in Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a><span data-ttu-id="98c2a-129">Enabling connectivity from VMs restricted by using ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="98c2a-129">Enabling connectivity from VMs restricted by using ExpressRoute</span></span>
<span data-ttu-id="98c2a-130">When an ExpressRoute circuit is configured, the on-premises servers can access Data Lake Store through public peering.</span><span class="sxs-lookup"><span data-stu-id="98c2a-130">When an ExpressRoute circuit is configured, the on-premises servers can access Data Lake Store through public peering.</span></span> <span data-ttu-id="98c2a-131">More details on configuring ExpressRoute for public peering is available at [ExpressRoute FAQs](../expressroute/expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="98c2a-131">More details on configuring ExpressRoute for public peering is available at [ExpressRoute FAQs](../expressroute/expressroute-faqs.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="98c2a-132">See also</span><span class="sxs-lookup"><span data-stu-id="98c2a-132">See also</span></span>
* [<span data-ttu-id="98c2a-133">Overview of Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="98c2a-133">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="98c2a-134">Securing data stored in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="98c2a-134">Securing data stored in Azure Data Lake Store</span></span>](data-lake-store-security-overview.md)

