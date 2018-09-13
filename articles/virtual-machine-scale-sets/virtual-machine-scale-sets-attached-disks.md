---
title: Azure Virtual Machine Scale Sets Attached Data Disks | Microsoft Docs
description: Learn how to use attached data disks with virtual machine scale sets
services: virtual-machine-scale-sets
documentationcenter: ''
author: gatneil
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: negat
ms.openlocfilehash: 4dd13f1feedf53255daa351bd087845ec5cc845a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773922"
---
# <a name="azure-virtual-machine-scale-sets-and-attached-data-disks"></a><span data-ttu-id="10567-103">Azure virtual machine scale sets and attached data disks</span><span class="sxs-lookup"><span data-stu-id="10567-103">Azure virtual machine scale sets and attached data disks</span></span>
<span data-ttu-id="10567-104">To expand your available storage, Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) support VM instances with attached data disks.</span><span class="sxs-lookup"><span data-stu-id="10567-104">To expand your available storage, Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) support VM instances with attached data disks.</span></span> <span data-ttu-id="10567-105">You can attach data disks when the scale set is created, or to an existing scale set.</span><span class="sxs-lookup"><span data-stu-id="10567-105">You can attach data disks when the scale set is created, or to an existing scale set.</span></span>

> [!NOTE]
>  <span data-ttu-id="10567-106">When you create a scale set with attached data disks, you need to mount and format the disks from within a VM to use them (just like for standalone Azure VMs).</span><span class="sxs-lookup"><span data-stu-id="10567-106">When you create a scale set with attached data disks, you need to mount and format the disks from within a VM to use them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="10567-107">A convenient way to complete this process is to use a Custom Script Extension that calls a script to partition and format all the data disks on a VM.</span><span class="sxs-lookup"><span data-stu-id="10567-107">A convenient way to complete this process is to use a Custom Script Extension that calls a script to partition and format all the data disks on a VM.</span></span> <span data-ttu-id="10567-108">For examples of this, see [Azure CLI 2.0](tutorial-use-disks-cli.md#prepare-the-data-disks) [Azure PowerShell](tutorial-use-disks-powershell.md#prepare-the-data-disks).</span><span class="sxs-lookup"><span data-stu-id="10567-108">For examples of this, see [Azure CLI 2.0](tutorial-use-disks-cli.md#prepare-the-data-disks) [Azure PowerShell](tutorial-use-disks-powershell.md#prepare-the-data-disks).</span></span>


## <a name="create-and-manage-disks-in-a-scale-set"></a><span data-ttu-id="10567-109">Create and manage disks in a scale set</span><span class="sxs-lookup"><span data-stu-id="10567-109">Create and manage disks in a scale set</span></span>
<span data-ttu-id="10567-110">For detailed information on how to create a scale set with attached data disks, prepare and format, or add and remove data disks, see one of the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="10567-110">For detailed information on how to create a scale set with attached data disks, prepare and format, or add and remove data disks, see one of the following tutorials:</span></span>

- [<span data-ttu-id="10567-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="10567-111">Azure CLI 2.0</span></span>](tutorial-use-disks-cli.md)
- [<span data-ttu-id="10567-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="10567-112">Azure PowerShell</span></span>](tutorial-use-disks-powershell.md)

<span data-ttu-id="10567-113">The rest of this article outlines specific use cases such as Service Fabric clusters that require data disks, or attaching existing data disks with content to a scale set.</span><span class="sxs-lookup"><span data-stu-id="10567-113">The rest of this article outlines specific use cases such as Service Fabric clusters that require data disks, or attaching existing data disks with content to a scale set.</span></span>


## <a name="create-a-service-fabric-cluster-with-attached-data-disks"></a><span data-ttu-id="10567-114">Create a Service Fabric cluster with attached data disks</span><span class="sxs-lookup"><span data-stu-id="10567-114">Create a Service Fabric cluster with attached data disks</span></span>
<span data-ttu-id="10567-115">Each [node type](../service-fabric/service-fabric-cluster-nodetypes.md) in a [Service Fabric](/azure/service-fabric) cluster running in Azure is backed by a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="10567-115">Each [node type](../service-fabric/service-fabric-cluster-nodetypes.md) in a [Service Fabric](/azure/service-fabric) cluster running in Azure is backed by a virtual machine scale set.</span></span>  <span data-ttu-id="10567-116">Using an Azure Resource Manager template, you can attach data disks to the scale set(s) that make up the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="10567-116">Using an Azure Resource Manager template, you can attach data disks to the scale set(s) that make up the Service Fabric cluster.</span></span> <span data-ttu-id="10567-117">You can use an [existing template](https://github.com/Azure-Samples/service-fabric-cluster-templates) as a starting point.</span><span class="sxs-lookup"><span data-stu-id="10567-117">You can use an [existing template](https://github.com/Azure-Samples/service-fabric-cluster-templates) as a starting point.</span></span> <span data-ttu-id="10567-118">In the template, include a _dataDisks_ section in the _storageProfile_ of the _Microsoft.Compute/virtualMachineScaleSets_ resource(s) and deploy the template.</span><span class="sxs-lookup"><span data-stu-id="10567-118">In the template, include a _dataDisks_ section in the _storageProfile_ of the _Microsoft.Compute/virtualMachineScaleSets_ resource(s) and deploy the template.</span></span> <span data-ttu-id="10567-119">The following example attaches a 128 GB data disk:</span><span class="sxs-lookup"><span data-stu-id="10567-119">The following example attaches a 128 GB data disk:</span></span>

```json
"dataDisks": [
    {
    "diskSizeGB": 128,
    "lun": 0,
    "createOption": "Empty"
    }
]
```

<span data-ttu-id="10567-120">You can automatically partition, format, and mount the data disks when the cluster is deployed.</span><span class="sxs-lookup"><span data-stu-id="10567-120">You can automatically partition, format, and mount the data disks when the cluster is deployed.</span></span>  <span data-ttu-id="10567-121">Add a custom script extension to the _extensionProfile_ of the _virtualMachineProfile_ of the scale set(s).</span><span class="sxs-lookup"><span data-stu-id="10567-121">Add a custom script extension to the _extensionProfile_ of the _virtualMachineProfile_ of the scale set(s).</span></span>

<span data-ttu-id="10567-122">To automatically prepare the data disk(s) in a Windows cluster, add the following:</span><span class="sxs-lookup"><span data-stu-id="10567-122">To automatically prepare the data disk(s) in a Windows cluster, add the following:</span></span>

```json
{
    "name": "customScript",    
    "properties": {    
        "publisher": "Microsoft.Compute",    
        "type": "CustomScriptExtension",    
        "typeHandlerVersion": "1.8",    
        "autoUpgradeMinorVersion": true,    
        "settings": {    
        "fileUris": [
            "https://raw.githubusercontent.com/Azure-Samples/compute-automation-configurations/master/prepare_vm_disks.ps1"
        ],
        "commandToExecute": "powershell -ExecutionPolicy Unrestricted -File prepare_vm_disks.ps1"
        }
    }
}
```
<span data-ttu-id="10567-123">To automatically prepare the data disk(s) in a Linux cluster, add the following:</span><span class="sxs-lookup"><span data-stu-id="10567-123">To automatically prepare the data disk(s) in a Linux cluster, add the following:</span></span>
```json
{
    "name": "lapextension",
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
        "fileUris": [
            "https://raw.githubusercontent.com/Azure-Samples/compute-automation-configurations/master/prepare_vm_disks.sh"
        ],
        "commandToExecute": "bash prepare_vm_disks.sh"
        }
    }
}
```


## <a name="adding-pre-populated-data-disks-to-an-existing-scale-set"></a><span data-ttu-id="10567-124">Adding pre-populated data disks to an existing scale set</span><span class="sxs-lookup"><span data-stu-id="10567-124">Adding pre-populated data disks to an existing scale set</span></span>
<span data-ttu-id="10567-125">Data disks specified in the scale set model are always empty.</span><span class="sxs-lookup"><span data-stu-id="10567-125">Data disks specified in the scale set model are always empty.</span></span> <span data-ttu-id="10567-126">However, you may attach an existing data disk to a specific VM in a scale set.</span><span class="sxs-lookup"><span data-stu-id="10567-126">However, you may attach an existing data disk to a specific VM in a scale set.</span></span> <span data-ttu-id="10567-127">This feature is in preview, with examples on [github](https://github.com/Azure/vm-scale-sets/tree/master/preview/disk).</span><span class="sxs-lookup"><span data-stu-id="10567-127">This feature is in preview, with examples on [github](https://github.com/Azure/vm-scale-sets/tree/master/preview/disk).</span></span> <span data-ttu-id="10567-128">If you wish to propagate data across all VMs in the scale set, you may duplicate your data disk and attach it to each VM in the scale set, you may create a custom image that contains the data and provision the scale set from this custom image, or you may use Azure Files or a similar data storage offering.</span><span class="sxs-lookup"><span data-stu-id="10567-128">If you wish to propagate data across all VMs in the scale set, you may duplicate your data disk and attach it to each VM in the scale set, you may create a custom image that contains the data and provision the scale set from this custom image, or you may use Azure Files or a similar data storage offering.</span></span>


## <a name="additional-notes"></a><span data-ttu-id="10567-129">Additional notes</span><span class="sxs-lookup"><span data-stu-id="10567-129">Additional notes</span></span>
<span data-ttu-id="10567-130">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of the Microsoft.Compute API.</span><span class="sxs-lookup"><span data-stu-id="10567-130">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of the Microsoft.Compute API.</span></span>

<span data-ttu-id="10567-131">Azure portal support for attached data disks in scale sets is initially limited.</span><span class="sxs-lookup"><span data-stu-id="10567-131">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="10567-132">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API to manage attached disks.</span><span class="sxs-lookup"><span data-stu-id="10567-132">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API to manage attached disks.</span></span>


