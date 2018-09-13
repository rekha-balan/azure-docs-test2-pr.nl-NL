---
title: How to plan your virtual network for an Azure RemoteApp collection | Microsoft Docs
description: Learn how to plan your virtual network for an Azure RemoteApp collection.
services: remoteapp
documentationcenter: ''
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 813334b9414be360339792aafb273bf844975857
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554440"
---
# <a name="how-to-plan-your-virtual-network-for-azure-remoteapp"></a><span data-ttu-id="b6658-103">How to plan your virtual network for Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b6658-103">How to plan your virtual network for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b6658-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="b6658-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b6658-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="b6658-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="b6658-106">This document describes how to set up your Azure virtual network (VNET) and the subnet for Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="b6658-106">This document describes how to set up your Azure virtual network (VNET) and the subnet for Azure RemoteApp.</span></span> <span data-ttu-id="b6658-107">If you are unfamiliar with Azure virtual networks, this is a capability that helps you to virtualize your network infrastructure to the cloud and to create hybrid solutions with Azure and your on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="b6658-107">If you are unfamiliar with Azure virtual networks, this is a capability that helps you to virtualize your network infrastructure to the cloud and to create hybrid solutions with Azure and your on-premises resources.</span></span> <span data-ttu-id="b6658-108">You can read more about it [here](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6658-108">You can read more about it [here](../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="b6658-109">If you want to define security policies for traffic (both incoming and outgoing) in your virtual network where you are deploying Azure RemoteApp, we strongly recommend creating a separate subnet for Azure RemoteApp from the rest of your deployments in the Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="b6658-109">If you want to define security policies for traffic (both incoming and outgoing) in your virtual network where you are deploying Azure RemoteApp, we strongly recommend creating a separate subnet for Azure RemoteApp from the rest of your deployments in the Azure virtual network.</span></span> <span data-ttu-id="b6658-110">For more information on how to define security policies on your Azure virtual network subnet, please read [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="b6658-110">For more information on how to define security policies on your Azure virtual network subnet, please read [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a><span data-ttu-id="b6658-111">Types of Azure RemoteApp collections with Azure virtual networks</span><span class="sxs-lookup"><span data-stu-id="b6658-111">Types of Azure RemoteApp collections with Azure virtual networks</span></span>
<span data-ttu-id="b6658-112">The following graphics show the two different collection options when you want to use a virtual network.</span><span class="sxs-lookup"><span data-stu-id="b6658-112">The following graphics show the two different collection options when you want to use a virtual network.</span></span>

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a><span data-ttu-id="b6658-113">Azure RemoteApp cloud collection with VNET</span><span class="sxs-lookup"><span data-stu-id="b6658-113">Azure RemoteApp cloud collection with VNET</span></span>
 ![Azure RemoteApp - Cloud collection with a VNET](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-planvpn/ra-cloudvpn.png)

<span data-ttu-id="b6658-115">This represents an Azure RemoteApp collection where all the resources that the RemoteApp session hosts need to access are deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="b6658-115">This represents an Azure RemoteApp collection where all the resources that the RemoteApp session hosts need to access are deployed in Azure.</span></span> <span data-ttu-id="b6658-116">They can be in the same VNET as the RemoteApp VNET or a different VNET in Azure.</span><span class="sxs-lookup"><span data-stu-id="b6658-116">They can be in the same VNET as the RemoteApp VNET or a different VNET in Azure.</span></span>

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a><span data-ttu-id="b6658-117">Azure RemoteApp hybrid collection with VNET</span><span class="sxs-lookup"><span data-stu-id="b6658-117">Azure RemoteApp hybrid collection with VNET</span></span>
![Azure RemoteApp - Hybrid collection with a VNET](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-planvpn/ra-hybridvpn.png)

<span data-ttu-id="b6658-119">This represents an Azure RemoteApp collection where some of the resources that the RemoteApp session hosts need to access are deployed on-premises.</span><span class="sxs-lookup"><span data-stu-id="b6658-119">This represents an Azure RemoteApp collection where some of the resources that the RemoteApp session hosts need to access are deployed on-premises.</span></span> <span data-ttu-id="b6658-120">The RemoteApp VNET is linked to the on-premises network using Azure hybrid technologies like site-to-site VPN or Express Route.</span><span class="sxs-lookup"><span data-stu-id="b6658-120">The RemoteApp VNET is linked to the on-premises network using Azure hybrid technologies like site-to-site VPN or Express Route.</span></span>

## <a name="how-the-system-works"></a><span data-ttu-id="b6658-121">How the system works</span><span class="sxs-lookup"><span data-stu-id="b6658-121">How the system works</span></span>
<span data-ttu-id="b6658-122">Under the covers Azure RemoteApp deploys Azure virtual machines (with your uploaded image) to the virtual network subnet that you chose during provisioning.</span><span class="sxs-lookup"><span data-stu-id="b6658-122">Under the covers Azure RemoteApp deploys Azure virtual machines (with your uploaded image) to the virtual network subnet that you chose during provisioning.</span></span> <span data-ttu-id="b6658-123">If you opted for a hybrid collection, we try to resolve the FQDN of the domain controller you entered in the provisioning workflow with the DNS server provided in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="b6658-123">If you opted for a hybrid collection, we try to resolve the FQDN of the domain controller you entered in the provisioning workflow with the DNS server provided in the virtual network.</span></span>  
<span data-ttu-id="b6658-124">If you are connecting to an existing virtual network, make sure to expose the necessary ports in your network security groups in your Azure RemoteApp subnet.</span><span class="sxs-lookup"><span data-stu-id="b6658-124">If you are connecting to an existing virtual network, make sure to expose the necessary ports in your network security groups in your Azure RemoteApp subnet.</span></span> 

<span data-ttu-id="b6658-125">We recommend you use a [large enough  subnet for Azure RemoteApp](remoteapp-vnetsizing.md).</span><span class="sxs-lookup"><span data-stu-id="b6658-125">We recommend you use a [large enough  subnet for Azure RemoteApp](remoteapp-vnetsizing.md).</span></span> <span data-ttu-id="b6658-126">The largest supported by Azure Virtual network is /8 (using CIDR subnet definitions).</span><span class="sxs-lookup"><span data-stu-id="b6658-126">The largest supported by Azure Virtual network is /8 (using CIDR subnet definitions).</span></span> <span data-ttu-id="b6658-127">Your subnet should be large enough to accommodate all the Azure RemoteApp VMs during scale-up when more users are accessing the apps.</span><span class="sxs-lookup"><span data-stu-id="b6658-127">Your subnet should be large enough to accommodate all the Azure RemoteApp VMs during scale-up when more users are accessing the apps.</span></span> 

<span data-ttu-id="b6658-128">Following are the things you will need to enable on your virtual network subnet:</span><span class="sxs-lookup"><span data-stu-id="b6658-128">Following are the things you will need to enable on your virtual network subnet:</span></span> 

1. <span data-ttu-id="b6658-129">Outbound traffic from the subnet should be allowed on port range 10101-10175 to communicate with one of the internal Azure RemoteApp services.</span><span class="sxs-lookup"><span data-stu-id="b6658-129">Outbound traffic from the subnet should be allowed on port range 10101-10175 to communicate with one of the internal Azure RemoteApp services.</span></span>
2. <span data-ttu-id="b6658-130">Outbound traffic should be allowed from your subnet to connect to Azure Storage on port 443</span><span class="sxs-lookup"><span data-stu-id="b6658-130">Outbound traffic should be allowed from your subnet to connect to Azure Storage on port 443</span></span>
3. <span data-ttu-id="b6658-131">If you have Active Directory hosted in Azure, make sure any VM within the virtual network subnet for Azure RemoteApp is able to connect to that domain controller.</span><span class="sxs-lookup"><span data-stu-id="b6658-131">If you have Active Directory hosted in Azure, make sure any VM within the virtual network subnet for Azure RemoteApp is able to connect to that domain controller.</span></span> <span data-ttu-id="b6658-132">The DNS in the virtual network should be able to resolve the FQDN of this domain controller.</span><span class="sxs-lookup"><span data-stu-id="b6658-132">The DNS in the virtual network should be able to resolve the FQDN of this domain controller.</span></span>

## <a name="virtual-network-with-forced-tunneling"></a><span data-ttu-id="b6658-133">Virtual network with forced tunneling</span><span class="sxs-lookup"><span data-stu-id="b6658-133">Virtual network with forced tunneling</span></span>
<span data-ttu-id="b6658-134">[Forced tunneling](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) is now supported for all new Azure RemoteApp collections.</span><span class="sxs-lookup"><span data-stu-id="b6658-134">[Forced tunneling](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) is now supported for all new Azure RemoteApp collections.</span></span> <span data-ttu-id="b6658-135">We currently do not support the migration of an existing collection to support forced tunneling.</span><span class="sxs-lookup"><span data-stu-id="b6658-135">We currently do not support the migration of an existing collection to support forced tunneling.</span></span>  <span data-ttu-id="b6658-136">You will have to delete all your existing collections using the VNET that you are linking to Azure RemoteApp and create a new one to get forced tunneling enabled on your collections.</span><span class="sxs-lookup"><span data-stu-id="b6658-136">You will have to delete all your existing collections using the VNET that you are linking to Azure RemoteApp and create a new one to get forced tunneling enabled on your collections.</span></span> 



