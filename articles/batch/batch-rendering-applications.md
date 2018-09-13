---
title: Batch rendering applications
description: Pre-installed Batch rendering applications
services: batch
author: mscurrell
ms.author: markscu
ms.date: 08/02/2018
ms.topic: conceptual
ms.openlocfilehash: 28acd1b7275694d38a52f14d2b2c32b79cc8183e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871081"
---
# <a name="pre-installed-applications-on-rendering-vm-images"></a><span data-ttu-id="d935a-103">Pre-installed applications on rendering VM images</span><span class="sxs-lookup"><span data-stu-id="d935a-103">Pre-installed applications on rendering VM images</span></span>

<span data-ttu-id="d935a-104">It's possible to use any rendering applications with Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d935a-104">It's possible to use any rendering applications with Azure Batch.</span></span> <span data-ttu-id="d935a-105">However, Azure Marketplace VM images are available with common applications pre-installed.</span><span class="sxs-lookup"><span data-stu-id="d935a-105">However, Azure Marketplace VM images are available with common applications pre-installed.</span></span>

<span data-ttu-id="d935a-106">Where applicable, pay-per-use licensing is available for the pre-installed rendering applications.</span><span class="sxs-lookup"><span data-stu-id="d935a-106">Where applicable, pay-per-use licensing is available for the pre-installed rendering applications.</span></span> <span data-ttu-id="d935a-107">When a Batch pool is created, the required applications can be specified and both the cost of VM and applications will be billed per minute.</span><span class="sxs-lookup"><span data-stu-id="d935a-107">When a Batch pool is created, the required applications can be specified and both the cost of VM and applications will be billed per minute.</span></span> <span data-ttu-id="d935a-108">Application prices are listed on the [Azure Batch pricing page](https://azure.microsoft.com/pricing/details/batch/#graphic-rendering).</span><span class="sxs-lookup"><span data-stu-id="d935a-108">Application prices are listed on the [Azure Batch pricing page](https://azure.microsoft.com/pricing/details/batch/#graphic-rendering).</span></span>

<span data-ttu-id="d935a-109">Some applications only support Windows, but most are supported on both Windows and Linux.</span><span class="sxs-lookup"><span data-stu-id="d935a-109">Some applications only support Windows, but most are supported on both Windows and Linux.</span></span>

## <a name="applications-on-centos-7-rendering-nodes"></a><span data-ttu-id="d935a-110">Applications on CentOS 7 rendering nodes</span><span class="sxs-lookup"><span data-stu-id="d935a-110">Applications on CentOS 7 rendering nodes</span></span>

* <span data-ttu-id="d935a-111">Autodesk Maya I/O 2017 Update 5 (cut 201708032230)</span><span class="sxs-lookup"><span data-stu-id="d935a-111">Autodesk Maya I/O 2017 Update 5 (cut 201708032230)</span></span>
* <span data-ttu-id="d935a-112">Autodesk Maya I/O 2018 Update 2 (cut 201711281015)</span><span class="sxs-lookup"><span data-stu-id="d935a-112">Autodesk Maya I/O 2018 Update 2 (cut 201711281015)</span></span>
* <span data-ttu-id="d935a-113">Autodesk Arnold for Maya 2017 (Arnold version 5.0.1.1) MtoA-2.0.1.1-2017</span><span class="sxs-lookup"><span data-stu-id="d935a-113">Autodesk Arnold for Maya 2017 (Arnold version 5.0.1.1) MtoA-2.0.1.1-2017</span></span>
* <span data-ttu-id="d935a-114">Autodesk Arnold for Maya 2018 (Arnold version 5.0.1.4) MtoA-2.1.0.3-2018</span><span class="sxs-lookup"><span data-stu-id="d935a-114">Autodesk Arnold for Maya 2018 (Arnold version 5.0.1.4) MtoA-2.1.0.3-2018</span></span>
* <span data-ttu-id="d935a-115">Chaos Group V-Ray for Maya 2017 (version 3.60.04)</span><span class="sxs-lookup"><span data-stu-id="d935a-115">Chaos Group V-Ray for Maya 2017 (version 3.60.04)</span></span>
* <span data-ttu-id="d935a-116">Chaos Group V-Ray for Maya 2018 (version 3.60.04)</span><span class="sxs-lookup"><span data-stu-id="d935a-116">Chaos Group V-Ray for Maya 2018 (version 3.60.04)</span></span>
* <span data-ttu-id="d935a-117">Blender (2.68)</span><span class="sxs-lookup"><span data-stu-id="d935a-117">Blender (2.68)</span></span>

## <a name="applications-on-windows-server-2016-rendering-nodes"></a><span data-ttu-id="d935a-118">Applications on Windows Server 2016 rendering nodes</span><span class="sxs-lookup"><span data-stu-id="d935a-118">Applications on Windows Server 2016 rendering nodes</span></span>

* <span data-ttu-id="d935a-119">Autodesk Maya I/O 2017 Update 5 (version 17.4.5459)</span><span class="sxs-lookup"><span data-stu-id="d935a-119">Autodesk Maya I/O 2017 Update 5 (version 17.4.5459)</span></span>
* <span data-ttu-id="d935a-120">Autodesk Maya I/O 2018 Update 3 (version 18.3.0.7040)</span><span class="sxs-lookup"><span data-stu-id="d935a-120">Autodesk Maya I/O 2018 Update 3 (version 18.3.0.7040)</span></span>  
* <span data-ttu-id="d935a-121">Autodesk 3ds Max I/O 2019 Update 1 (version 21.10.1314)</span><span class="sxs-lookup"><span data-stu-id="d935a-121">Autodesk 3ds Max I/O 2019 Update 1 (version 21.10.1314)</span></span>
* <span data-ttu-id="d935a-122">Autodesk 3ds Max I/O 2018 Update 4 (version 20.4.0.4254)</span><span class="sxs-lookup"><span data-stu-id="d935a-122">Autodesk 3ds Max I/O 2018 Update 4 (version 20.4.0.4254)</span></span>
* <span data-ttu-id="d935a-123">Autodesk Arnold for Maya (Arnold version 5.0.1.1) MtoA-2.0.1.1-2017</span><span class="sxs-lookup"><span data-stu-id="d935a-123">Autodesk Arnold for Maya (Arnold version 5.0.1.1) MtoA-2.0.1.1-2017</span></span>
* <span data-ttu-id="d935a-124">Autodesk Arnold for Maya (Arnold version 5.0.1.4) MtoA-2.0.2.3-2018</span><span class="sxs-lookup"><span data-stu-id="d935a-124">Autodesk Arnold for Maya (Arnold version 5.0.1.4) MtoA-2.0.2.3-2018</span></span>
* <span data-ttu-id="d935a-125">Autodesk Arnold for 3ds Max (Arnold version 5.0.2.4)(version 1.2.926)</span><span class="sxs-lookup"><span data-stu-id="d935a-125">Autodesk Arnold for 3ds Max (Arnold version 5.0.2.4)(version 1.2.926)</span></span>
* <span data-ttu-id="d935a-126">Chaos Group V-Ray for Maya (version 3.52.03)</span><span class="sxs-lookup"><span data-stu-id="d935a-126">Chaos Group V-Ray for Maya (version 3.52.03)</span></span>
* <span data-ttu-id="d935a-127">Chaos Group V-Ray for 3ds Max (version 3.60.02)</span><span class="sxs-lookup"><span data-stu-id="d935a-127">Chaos Group V-Ray for 3ds Max (version 3.60.02)</span></span>
* <span data-ttu-id="d935a-128">Blender (2.79)</span><span class="sxs-lookup"><span data-stu-id="d935a-128">Blender (2.79)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d935a-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="d935a-129">Next steps</span></span>

<span data-ttu-id="d935a-130">To use the rendering VM images, they need to be specified in the pool configuration when a pool is created; see the [Batch pool capabilities for rendering](https://docs.microsoft.com/azure/batch/batch-rendering-functionality#batch-pools).</span><span class="sxs-lookup"><span data-stu-id="d935a-130">To use the rendering VM images, they need to be specified in the pool configuration when a pool is created; see the [Batch pool capabilities for rendering](https://docs.microsoft.com/azure/batch/batch-rendering-functionality#batch-pools).</span></span>