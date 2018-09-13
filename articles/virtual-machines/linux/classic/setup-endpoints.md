---
title: Set up endpoints on a classic Linux VM | Microsoft Docs
description: Learn to set up endpoints for a Linux VM in the Azure classic portal to allow communication with a Linux virtual machine in Azure
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/13/2016
ms.author: cynthn
ms.openlocfilehash: 7e9658f902732b575d1578e673b0405a4aacf9c8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562752"
---
# <a name="how-to-set-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="8ee26-103">How to set up endpoints on a Linux classic virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="8ee26-103">How to set up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="8ee26-104">All Linux virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span><span class="sxs-lookup"><span data-stu-id="8ee26-104">All Linux virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="8ee26-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8ee26-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="8ee26-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ee26-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="8ee26-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8ee26-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8ee26-108">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="8ee26-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8ee26-109">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="8ee26-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="8ee26-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span><span class="sxs-lookup"><span data-stu-id="8ee26-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="8ee26-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ee26-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8ee26-112">When you create a Linux virtual machine in the Azure classic portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span><span class="sxs-lookup"><span data-stu-id="8ee26-112">When you create a Linux virtual machine in the Azure classic portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="8ee26-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span><span class="sxs-lookup"><span data-stu-id="8ee26-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="8ee26-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="8ee26-114">Next steps</span></span>
* <span data-ttu-id="8ee26-115">You can also create a VM endpoint by using the [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8ee26-115">You can also create a VM endpoint by using the [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="8ee26-116">Run the **azure vm endpoint create** command.</span><span class="sxs-lookup"><span data-stu-id="8ee26-116">Run the **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="8ee26-117">If you created a virtual machine in the Resource Manager deployment model, you can use the Azure CLI in Resource Manager mode to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) to control traffic to the VM.</span><span class="sxs-lookup"><span data-stu-id="8ee26-117">If you created a virtual machine in the Resource Manager deployment model, you can use the Azure CLI in Resource Manager mode to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) to control traffic to the VM.</span></span>

