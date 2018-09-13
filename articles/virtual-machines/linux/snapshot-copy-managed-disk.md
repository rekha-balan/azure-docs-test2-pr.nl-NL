---
title: Create a snapshot of a VHD in Azure | Microsoft Docs
description: Learn how to create a copy of a VHD in Azure as a back up or for troubleshooting issues.
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/11/2018
ms.author: cynthn
ms.openlocfilehash: 2d0b71a614f453258277f1c1eae59ca75db14974
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783775"
---
# <a name="create-a-snapshot"></a><span data-ttu-id="88084-103">Create a snapshot</span><span class="sxs-lookup"><span data-stu-id="88084-103">Create a snapshot</span></span> 

<span data-ttu-id="88084-104">Take a snapshot of an OS or data disk for backup or to troubleshoot VM issues.</span><span class="sxs-lookup"><span data-stu-id="88084-104">Take a snapshot of an OS or data disk for backup or to troubleshoot VM issues.</span></span> <span data-ttu-id="88084-105">A snapshot is a full, read-only copy of a VHD.</span><span class="sxs-lookup"><span data-stu-id="88084-105">A snapshot is a full, read-only copy of a VHD.</span></span> 

## <a name="use-azure-cli"></a><span data-ttu-id="88084-106">Use Azure CLI</span><span class="sxs-lookup"><span data-stu-id="88084-106">Use Azure CLI</span></span> 

<span data-ttu-id="88084-107">The following example requires that you use [Cloud Shell](https://shell.azure.com/bash) or have Azure CLI 2.0 installed.</span><span class="sxs-lookup"><span data-stu-id="88084-107">The following example requires that you use [Cloud Shell](https://shell.azure.com/bash) or have Azure CLI 2.0 installed.</span></span> <span data-ttu-id="88084-108">Run **az --version** to find the version.</span><span class="sxs-lookup"><span data-stu-id="88084-108">Run **az --version** to find the version.</span></span> <span data-ttu-id="88084-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="88084-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="88084-110">The following steps show how to take a snapshot using the **az snapshot create** command with the **--source-disk** parameter.</span><span class="sxs-lookup"><span data-stu-id="88084-110">The following steps show how to take a snapshot using the **az snapshot create** command with the **--source-disk** parameter.</span></span> <span data-ttu-id="88084-111">The following example assumes that there is a VM called *myVM* in the *myResourceGroup* resource group.</span><span class="sxs-lookup"><span data-stu-id="88084-111">The following example assumes that there is a VM called *myVM* in the *myResourceGroup* resource group.</span></span>

<span data-ttu-id="88084-112">Get the disk ID using [az vm show](/cli/azure/vm#az-vm-show).</span><span class="sxs-lookup"><span data-stu-id="88084-112">Get the disk ID using [az vm show](/cli/azure/vm#az-vm-show).</span></span>

```azurecli-interactive
osDiskId=$(az vm show \
   -g myResourceGroup \
   -n myVM \
   --query "storageProfile.osDisk.managedDisk.id" \
   -o tsv)
```

<span data-ttu-id="88084-113">Take a snapshot named *osDisk-backup* using [az snapshot create](/cli/azure/snapshot#az-snapshot-create).</span><span class="sxs-lookup"><span data-stu-id="88084-113">Take a snapshot named *osDisk-backup* using [az snapshot create](/cli/azure/snapshot#az-snapshot-create).</span></span>

```azurecli-interactive
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDisk-backup
```

> [!NOTE]
> <span data-ttu-id="88084-114">If you would like to store your snapshot in zone-resilient storage, you need to create it in a region that supports [availability zones](../../availability-zones/az-overview.md) and include the **--sku Standard_ZRS** parameter.</span><span class="sxs-lookup"><span data-stu-id="88084-114">If you would like to store your snapshot in zone-resilient storage, you need to create it in a region that supports [availability zones](../../availability-zones/az-overview.md) and include the **--sku Standard_ZRS** parameter.</span></span>

<span data-ttu-id="88084-115">You can see a list of the snapshots using [az snapshot list](/cli/azure/snapshot#az-snapshot-list).</span><span class="sxs-lookup"><span data-stu-id="88084-115">You can see a list of the snapshots using [az snapshot list](/cli/azure/snapshot#az-snapshot-list).</span></span>

```azurecli-interactive
az snapshot list \
   -g myResourceGroup \
   - table
```

## <a name="use-azure-portal"></a><span data-ttu-id="88084-116">Use Azure portal</span><span class="sxs-lookup"><span data-stu-id="88084-116">Use Azure portal</span></span> 

1. <span data-ttu-id="88084-117">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="88084-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="88084-118">Starting in the upper-left, click **Create a resource** and search for **snapshot**.</span><span class="sxs-lookup"><span data-stu-id="88084-118">Starting in the upper-left, click **Create a resource** and search for **snapshot**.</span></span> <span data-ttu-id="88084-119">Select **Snapshot** from the search results.</span><span class="sxs-lookup"><span data-stu-id="88084-119">Select **Snapshot** from the search results.</span></span>
3. <span data-ttu-id="88084-120">In the **Snapshot** blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="88084-120">In the **Snapshot** blade, click **Create**.</span></span>
4. <span data-ttu-id="88084-121">Enter a **Name** for the snapshot.</span><span class="sxs-lookup"><span data-stu-id="88084-121">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="88084-122">Select an existing resource group or type the name for a new one.</span><span class="sxs-lookup"><span data-stu-id="88084-122">Select an existing resource group or type the name for a new one.</span></span> 
7. <span data-ttu-id="88084-123">For **Source disk**, select the managed disk to snapshot.</span><span class="sxs-lookup"><span data-stu-id="88084-123">For **Source disk**, select the managed disk to snapshot.</span></span>
8. <span data-ttu-id="88084-124">Select the **Account type** to use to store the snapshot.</span><span class="sxs-lookup"><span data-stu-id="88084-124">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="88084-125">Use **Standard HDD** unless you need it stored on a high performing SSD.</span><span class="sxs-lookup"><span data-stu-id="88084-125">Use **Standard HDD** unless you need it stored on a high performing SSD.</span></span>
9. <span data-ttu-id="88084-126">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="88084-126">Click **Create**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="88084-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="88084-127">Next steps</span></span>

 <span data-ttu-id="88084-128">Create a virtual machine from a snapshot by creating a managed disk from the snapshot and then attaching the new managed disk as the OS disk.</span><span class="sxs-lookup"><span data-stu-id="88084-128">Create a virtual machine from a snapshot by creating a managed disk from the snapshot and then attaching the new managed disk as the OS disk.</span></span> <span data-ttu-id="88084-129">For more information, see the [Create a VM from a snapshot](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) script.</span><span class="sxs-lookup"><span data-stu-id="88084-129">For more information, see the [Create a VM from a snapshot](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) script.</span></span>

