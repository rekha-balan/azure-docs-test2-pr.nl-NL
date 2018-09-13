---
title: Copy an Azure Managed Disk for Back up | Microsoft Docs
description: Learn how to create a copy of an Azure Managed Disk to use for back up or troubleshooting disk issues.
documentationcenter: ''
author: squillace
manager: timlt
editor: ''
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 23e05877061ac9dfa3c709c5632e6c866f35cbcd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563275"
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="11068-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span><span class="sxs-lookup"><span data-stu-id="11068-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="11068-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span><span class="sxs-lookup"><span data-stu-id="11068-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="11068-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span><span class="sxs-lookup"><span data-stu-id="11068-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="11068-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span><span class="sxs-lookup"><span data-stu-id="11068-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="11068-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="11068-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link to topic or blog post that explains managed disks. -->

<span data-ttu-id="11068-108">Use either the Azure portal or the Azure CLI 2.0 to take a snapshot of the Managed Disk.</span><span class="sxs-lookup"><span data-stu-id="11068-108">Use either the Azure portal or the Azure CLI 2.0 to take a snapshot of the Managed Disk.</span></span>

## <a name="use-azure-cli-20-to-take-a-snapshot"></a><span data-ttu-id="11068-109">Use Azure CLI 2.0 to take a snapshot</span><span class="sxs-lookup"><span data-stu-id="11068-109">Use Azure CLI 2.0 to take a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="11068-110">The following example requires the Azure CLI 2.0 installed and logged into your Azure account.</span><span class="sxs-lookup"><span data-stu-id="11068-110">The following example requires the Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="11068-111">The following steps show how to obtain and take a snapshot of a managed OS disk using the `az snapshot create` command with the `--source-disk` parameter.</span><span class="sxs-lookup"><span data-stu-id="11068-111">The following steps show how to obtain and take a snapshot of a managed OS disk using the `az snapshot create` command with the `--source-disk` parameter.</span></span> <span data-ttu-id="11068-112">The following example assumes that there is a VM called `myVM` created with a managed OS disk in the `myResourceGroup` resource group.</span><span class="sxs-lookup"><span data-stu-id="11068-112">The following example assumes that there is a VM called `myVM` created with a managed OS disk in the `myResourceGroup` resource group.</span></span>

```azure-cli
# take the disk id with which to create a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="11068-113">The output should look something like:</span><span class="sxs-lookup"><span data-stu-id="11068-113">The output should look something like:</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="11068-114">Use Azure portal to take a snapshot</span><span class="sxs-lookup"><span data-stu-id="11068-114">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="11068-115">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="11068-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="11068-116">Starting in the upper-left, click **New** and search for **snapshot**.</span><span class="sxs-lookup"><span data-stu-id="11068-116">Starting in the upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="11068-117">In the Snapshot blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="11068-117">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="11068-118">Enter a **Name** for the snapshot.</span><span class="sxs-lookup"><span data-stu-id="11068-118">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="11068-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span><span class="sxs-lookup"><span data-stu-id="11068-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="11068-120">Select an Azure datacenter Location.</span><span class="sxs-lookup"><span data-stu-id="11068-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="11068-121">For **Source disk**, select the Managed Disk to snapshot.</span><span class="sxs-lookup"><span data-stu-id="11068-121">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="11068-122">Select the **Account type** to use to store the snapshot.</span><span class="sxs-lookup"><span data-stu-id="11068-122">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="11068-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span><span class="sxs-lookup"><span data-stu-id="11068-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="11068-124">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="11068-124">Click **Create**.</span></span>

<span data-ttu-id="11068-125">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `--sku Premium_LRS` with the `az snapshot create` command.</span><span class="sxs-lookup"><span data-stu-id="11068-125">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `--sku Premium_LRS` with the `az snapshot create` command.</span></span> <span data-ttu-id="11068-126">This creates the snapshot so that it is stored as a Premium Managed Disk.</span><span class="sxs-lookup"><span data-stu-id="11068-126">This creates the snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="11068-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span><span class="sxs-lookup"><span data-stu-id="11068-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


