---
title: Connect Linux VMs in a cloud service | Microsoft Docs
description: Connect Linux virtual machines created with the classic deployment model to an Azure cloud service or virtual network.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 2fd23055-6b34-4ef0-88a8-fc19e32fb3c9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cynthn
ms.openlocfilehash: 92787b7ba6927ecea3e3ee074ed5e1cb869094d1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554274"
---
# <a name="connect-linux-virtual-machines-created-with-the-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a><span data-ttu-id="66bff-103">Connect Linux virtual machines created with the classic deployment model with a virtual network or cloud service</span><span class="sxs-lookup"><span data-stu-id="66bff-103">Connect Linux virtual machines created with the classic deployment model with a virtual network or cloud service</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="66bff-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="66bff-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="66bff-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="66bff-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="66bff-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="66bff-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="66bff-107">Linux virtual machines created with the classic deployment model are always placed in a cloud service.</span><span class="sxs-lookup"><span data-stu-id="66bff-107">Linux virtual machines created with the classic deployment model are always placed in a cloud service.</span></span> <span data-ttu-id="66bff-108">The cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints to access the virtual machine over the Internet.</span><span class="sxs-lookup"><span data-stu-id="66bff-108">The cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints to access the virtual machine over the Internet.</span></span> <span data-ttu-id="66bff-109">The cloud service can be in a virtual network, but that's not a requirement.</span><span class="sxs-lookup"><span data-stu-id="66bff-109">The cloud service can be in a virtual network, but that's not a requirement.</span></span> <span data-ttu-id="66bff-110">You can also [connect Windows virtual machines with a virtual network or cloud service](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66bff-110">You can also [connect Windows virtual machines with a virtual network or cloud service](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="66bff-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span><span class="sxs-lookup"><span data-stu-id="66bff-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span></span> <span data-ttu-id="66bff-112">The virtual machines in a standalone cloud service can only communicate with other virtual machines by using the other virtual machines’ public DNS names, and the traffic travels over the Internet.</span><span class="sxs-lookup"><span data-stu-id="66bff-112">The virtual machines in a standalone cloud service can only communicate with other virtual machines by using the other virtual machines’ public DNS names, and the traffic travels over the Internet.</span></span> <span data-ttu-id="66bff-113">If a cloud service is in a virtual network, the virtual machines in that cloud service can communicate with all other virtual machines in the virtual network without sending any traffic over the Internet.</span><span class="sxs-lookup"><span data-stu-id="66bff-113">If a cloud service is in a virtual network, the virtual machines in that cloud service can communicate with all other virtual machines in the virtual network without sending any traffic over the Internet.</span></span>

<span data-ttu-id="66bff-114">If you place your virtual machines in the same standalone cloud service, you can still use load balancing and availability sets.</span><span class="sxs-lookup"><span data-stu-id="66bff-114">If you place your virtual machines in the same standalone cloud service, you can still use load balancing and availability sets.</span></span> <span data-ttu-id="66bff-115">For details, see [Load balancing virtual machines](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Manage the availability of virtual machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66bff-115">For details, see [Load balancing virtual machines](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Manage the availability of virtual machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="66bff-116">However, you can't organize the virtual machines on subnets or connect a standalone cloud service to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="66bff-116">However, you can't organize the virtual machines on subnets or connect a standalone cloud service to your on-premises network.</span></span> <span data-ttu-id="66bff-117">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="66bff-117">Here's an example:</span></span>

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a><span data-ttu-id="66bff-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="66bff-118">Next steps</span></span>
<span data-ttu-id="66bff-119">After you create a virtual machine, it's a good idea to [add a data disk](attach-disk.md) so your services and workloads have a location to store data.</span><span class="sxs-lookup"><span data-stu-id="66bff-119">After you create a virtual machine, it's a good idea to [add a data disk](attach-disk.md) so your services and workloads have a location to store data.</span></span> 

