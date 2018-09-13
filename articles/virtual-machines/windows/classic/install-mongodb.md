---
title: Install MongoDB on a Windows VM in Azure | Microsoft Docs
description: Learn how to install MongoDB on an Azure VM created with the classic deployment model running Windows Server.
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: 7cf2c0a9e5e7785397a7229e3b44e9dbcc26f429
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662070"
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="8457d-103">Install MongoDB on a Windows VM in Azure</span><span class="sxs-lookup"><span data-stu-id="8457d-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8457d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8457d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8457d-105">This article covers using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="8457d-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="8457d-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="8457d-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8457d-107">To install and configure MongoDB using the Resource Manager deployment model, see [this article](../../virtual-machines-windows-install-mongodb.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8457d-107">To install and configure MongoDB using the Resource Manager deployment model, see [this article](../../virtual-machines-windows-install-mongodb.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="8457d-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span><span class="sxs-lookup"><span data-stu-id="8457d-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="8457d-109">This article guides you through creating a Windows Server virtual machine (VM) using the [Azure portal][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="8457d-109">This article guides you through creating a Windows Server virtual machine (VM) using the [Azure portal][AzurePortal].</span></span> <span data-ttu-id="8457d-110">You then create and attach a data disk to the VM before installing and configuring MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8457d-110">You then create and attach a data disk to the VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="8457d-111">If you have an existing VM in Azure that you would like to use, you can jump straight to [installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="8457d-111">If you have an existing VM in Azure that you would like to use, you can jump straight to [installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="8457d-112">Create a virtual machine running Windows Server</span><span class="sxs-lookup"><span data-stu-id="8457d-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="8457d-113">Follow these instructions to create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8457d-113">Follow these instructions to create a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="8457d-114">You can add an endpoint for MongoDB while creating the virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as the protocol, and set both the public and private ports to **27017**.</span><span class="sxs-lookup"><span data-stu-id="8457d-114">You can add an endpoint for MongoDB while creating the virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as the protocol, and set both the public and private ports to **27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="8457d-115">Attach a data disk</span><span class="sxs-lookup"><span data-stu-id="8457d-115">Attach a data disk</span></span>
<span data-ttu-id="8457d-116">To provide storage for the virtual machine, attach a data disk and then initialize it so that Windows can use it.</span><span class="sxs-lookup"><span data-stu-id="8457d-116">To provide storage for the virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="8457d-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span><span class="sxs-lookup"><span data-stu-id="8457d-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="8457d-118">For instructions on initializing the disk, see "How to: Initialize a new data disk in Windows Server" in [How to attach a data disk to a Windows virtual machine](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="8457d-118">For instructions on initializing the disk, see "How to: Initialize a new data disk in Windows Server" in [How to attach a data disk to a Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-the-virtual-machine"></a><span data-ttu-id="8457d-119">Install and run MongoDB on the virtual machine</span><span class="sxs-lookup"><span data-stu-id="8457d-119">Install and run MongoDB on the virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="8457d-120">Summary</span><span class="sxs-lookup"><span data-stu-id="8457d-120">Summary</span></span>
<span data-ttu-id="8457d-121">In this tutorial, you learned how to create a virtual machine running Windows Server, remotely connect to it, and attach a data disk.</span><span class="sxs-lookup"><span data-stu-id="8457d-121">In this tutorial, you learned how to create a virtual machine running Windows Server, remotely connect to it, and attach a data disk.</span></span>  <span data-ttu-id="8457d-122">You also learned how to install and configure MongoDB on the Windows-based virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8457d-122">You also learned how to install and configure MongoDB on the Windows-based virtual machine.</span></span> <span data-ttu-id="8457d-123">You can now access MongoDB on the Windows-based virtual machine, by following the advanced topics in the [MongoDB documentation][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="8457d-123">You can now access MongoDB on the Windows-based virtual machine, by following the advanced topics in the [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

<!-- Classic portal. Removed 03/07/2017 -->
<!-- [AzurePortal]: http://manage.windowsazure.com  -->
