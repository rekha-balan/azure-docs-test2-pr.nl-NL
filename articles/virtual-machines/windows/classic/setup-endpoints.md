---
title: Set up endpoints on a classic Windows VM | Microsoft Docs
description: Learn to set up endpoints for a classic Windows VM in the Azure portal to allow communication with a Windows virtual machine in Azure.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: ab18e4ea63b8c4e8156dfb0d4b04ae319ff60d17
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800987"
---
# <a name="how-to-set-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="6792d-103">How to set up endpoints on a classic Windows virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="6792d-103">How to set up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="6792d-104">All Windows virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span><span class="sxs-lookup"><span data-stu-id="6792d-104">All Windows virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="6792d-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6792d-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="6792d-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="6792d-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6792d-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6792d-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6792d-108">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="6792d-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="6792d-109">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="6792d-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> [!INCLUDE [virtual-machines-common-classic-createportal](../../../../includes/virtual-machines-classic-portal.md)]

<span data-ttu-id="6792d-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span><span class="sxs-lookup"><span data-stu-id="6792d-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="6792d-111">For more information, see [Allow external access to your VM using the Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6792d-111">For more information, see [Allow external access to your VM using the Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="6792d-112">When you create a Windows virtual machine in the Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span><span class="sxs-lookup"><span data-stu-id="6792d-112">When you create a Windows virtual machine in the Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="6792d-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span><span class="sxs-lookup"><span data-stu-id="6792d-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="6792d-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="6792d-114">Next steps</span></span>
* <span data-ttu-id="6792d-115">To use an Azure PowerShell cmdlet to set up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="6792d-115">To use an Azure PowerShell cmdlet to set up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="6792d-116">To use an Azure PowerShell cmdlet to manage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6792d-116">To use an Azure PowerShell cmdlet to manage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="6792d-117">If you created a virtual machine in the Resource Manager deployment model, you can use Azure PowerShell to [create network security groups](../../../virtual-network/tutorial-filter-network-traffic.md) to control traffic to the VM.</span><span class="sxs-lookup"><span data-stu-id="6792d-117">If you created a virtual machine in the Resource Manager deployment model, you can use Azure PowerShell to [create network security groups](../../../virtual-network/tutorial-filter-network-traffic.md) to control traffic to the VM.</span></span>
