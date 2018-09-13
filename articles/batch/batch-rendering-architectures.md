---
title: Azure rendering - reference architectures
description: Architectures for using Azure Batch and other Azure services to extend an on-premises render farm by bursting to the cloud
services: batch
author: davefellows
manager: jeconnoc
ms.author: danlep
ms.date: 08/13/2018
ms.topic: conceptual
ms.openlocfilehash: 0fe101ee6eb88094034b90c4d39f06ba509c9512
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866911"
---
# <a name="reference-architectures-for-azure-rendering"></a><span data-ttu-id="99469-103">Reference architectures for Azure rendering</span><span class="sxs-lookup"><span data-stu-id="99469-103">Reference architectures for Azure rendering</span></span>

<span data-ttu-id="99469-104">This article shows high-level architecture diagrams for scenarios to extend, or "burst", an on-premises render farm to Azure.</span><span class="sxs-lookup"><span data-stu-id="99469-104">This article shows high-level architecture diagrams for scenarios to extend, or "burst", an on-premises render farm to Azure.</span></span> <span data-ttu-id="99469-105">The examples show different options for Azure compute, networking, and storage services.</span><span class="sxs-lookup"><span data-stu-id="99469-105">The examples show different options for Azure compute, networking, and storage services.</span></span>

## <a name="hybrid-with-nfs-or-cfs"></a><span data-ttu-id="99469-106">Hybrid with NFS or CFS</span><span class="sxs-lookup"><span data-stu-id="99469-106">Hybrid with NFS or CFS</span></span>

<span data-ttu-id="99469-107">The following diagram shows a hybrid scenario that includes the following Azure services:</span><span class="sxs-lookup"><span data-stu-id="99469-107">The following diagram shows a hybrid scenario that includes the following Azure services:</span></span>

* <span data-ttu-id="99469-108">**Compute** - Azure Batch pool or Virtual Machine Scale Set.</span><span class="sxs-lookup"><span data-stu-id="99469-108">**Compute** - Azure Batch pool or Virtual Machine Scale Set.</span></span>

* <span data-ttu-id="99469-109">**Network** - On-premises: Azure ExpressRoute or VPN.</span><span class="sxs-lookup"><span data-stu-id="99469-109">**Network** - On-premises: Azure ExpressRoute or VPN.</span></span> <span data-ttu-id="99469-110">Azure: Azure VNet.</span><span class="sxs-lookup"><span data-stu-id="99469-110">Azure: Azure VNet.</span></span>

* <span data-ttu-id="99469-111">**Storage** - Input and output files: NFS or CFS using Azure VMs, synchronized with on-premises storage via Azure File Sync or RSync.</span><span class="sxs-lookup"><span data-stu-id="99469-111">**Storage** - Input and output files: NFS or CFS using Azure VMs, synchronized with on-premises storage via Azure File Sync or RSync.</span></span>

  ![Cloud bursting - Hybrid with NFS or CFS](./media/batch-rendering-architectures/hybrid-nfs-cfs.png)

## <a name="hybrid-with-blobfuse"></a><span data-ttu-id="99469-113">Hybrid with Blobfuse</span><span class="sxs-lookup"><span data-stu-id="99469-113">Hybrid with Blobfuse</span></span>

<span data-ttu-id="99469-114">The following diagram shows a hybrid scenario that includes the following Azure services:</span><span class="sxs-lookup"><span data-stu-id="99469-114">The following diagram shows a hybrid scenario that includes the following Azure services:</span></span>

* <span data-ttu-id="99469-115">**Compute** - Azure Batch pool or Virtual Machine Scale Set.</span><span class="sxs-lookup"><span data-stu-id="99469-115">**Compute** - Azure Batch pool or Virtual Machine Scale Set.</span></span>

* <span data-ttu-id="99469-116">**Network** - On-premises: Azure ExpressRoute or VPN.</span><span class="sxs-lookup"><span data-stu-id="99469-116">**Network** - On-premises: Azure ExpressRoute or VPN.</span></span> <span data-ttu-id="99469-117">Azure: Azure VNet.</span><span class="sxs-lookup"><span data-stu-id="99469-117">Azure: Azure VNet.</span></span>

* <span data-ttu-id="99469-118">**Storage** - Input and output files: Blob storage, mounted to compute resources via Azure Blobfuse.</span><span class="sxs-lookup"><span data-stu-id="99469-118">**Storage** - Input and output files: Blob storage, mounted to compute resources via Azure Blobfuse.</span></span>

  ![Cloud bursting - Hybrid with Blobfuse](./media/batch-rendering-architectures/hybrid-blob-fuse.png)

## <a name="hybrid-compute-and-storage"></a><span data-ttu-id="99469-120">Hybrid compute and storage</span><span class="sxs-lookup"><span data-stu-id="99469-120">Hybrid compute and storage</span></span>

<span data-ttu-id="99469-121">The following diagram shows a fully connected hybrid scenario for both compute and storage and includes the following Azure services:</span><span class="sxs-lookup"><span data-stu-id="99469-121">The following diagram shows a fully connected hybrid scenario for both compute and storage and includes the following Azure services:</span></span>

* <span data-ttu-id="99469-122">**Compute** - Azure Batch pool or Virtual Machine Scale Set.</span><span class="sxs-lookup"><span data-stu-id="99469-122">**Compute** - Azure Batch pool or Virtual Machine Scale Set.</span></span>

* <span data-ttu-id="99469-123">**Network** - On-premises: Azure ExpressRoute or VPN.</span><span class="sxs-lookup"><span data-stu-id="99469-123">**Network** - On-premises: Azure ExpressRoute or VPN.</span></span> <span data-ttu-id="99469-124">Azure: Azure VNet.</span><span class="sxs-lookup"><span data-stu-id="99469-124">Azure: Azure VNet.</span></span>

* <span data-ttu-id="99469-125">**Storage** - Cross-premises: Avere vFXT.</span><span class="sxs-lookup"><span data-stu-id="99469-125">**Storage** - Cross-premises: Avere vFXT.</span></span> <span data-ttu-id="99469-126">Optional archiving of on-premises files via Azure Data Box to Blob storage.</span><span class="sxs-lookup"><span data-stu-id="99469-126">Optional archiving of on-premises files via Azure Data Box to Blob storage.</span></span>

  ![Cloud bursting - Hybrid compute and storage](./media/batch-rendering-architectures/hybrid-compute-storage.png)


## <a name="next-steps"></a><span data-ttu-id="99469-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="99469-128">Next steps</span></span>

* <span data-ttu-id="99469-129">Learn more about using [Render managers](batch-rendering-render-managers.md) with Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="99469-129">Learn more about using [Render managers](batch-rendering-render-managers.md) with Azure Batch.</span></span>

* <span data-ttu-id="99469-130">Learn more about options for [Rendering in Azure](batch-rendering-service.md).</span><span class="sxs-lookup"><span data-stu-id="99469-130">Learn more about options for [Rendering in Azure](batch-rendering-service.md).</span></span>