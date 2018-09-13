---
title: Azure Virtual Machine Scale Sets Attached Data Disks | Microsoft Docs
description: Learn how to use attached data disks with virtual machine scale sets
services: virtual-machine-scale-sets
documentationcenter: ''
author: gbowerman
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 2/6/2017
ms.author: guybo
ms.openlocfilehash: 91d36d5321f455a2af31093fa460ddf6640942d4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663103"
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="9c616-103">Azure VM scale sets and attached data disks</span><span class="sxs-lookup"><span data-stu-id="9c616-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="9c616-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span><span class="sxs-lookup"><span data-stu-id="9c616-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="9c616-105">Data disks can be defined in the storage profile for scale sets created with Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="9c616-105">Data disks can be defined in the storage profile for scale sets created with Azure Managed Disks.</span></span> <span data-ttu-id="9c616-106">Previously the only directly attached storage options available with VMs in scale sets were the OS drive and temp drives.</span><span class="sxs-lookup"><span data-stu-id="9c616-106">Previously the only directly attached storage options available with VMs in scale sets were the OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="9c616-107">When you create a scale set with attached data disks defined, you still need to mount and format the disks from within a VM to use them (just like for standalone Azure VMs).</span><span class="sxs-lookup"><span data-stu-id="9c616-107">When you create a scale set with attached data disks defined, you still need to mount and format the disks from within a VM to use them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="9c616-108">A convenient way to do this is to use a custom script extension which calls a standard script to partition and format all the data disks on a VM.</span><span class="sxs-lookup"><span data-stu-id="9c616-108">A convenient way to do this is to use a custom script extension which calls a standard script to partition and format all the data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="9c616-109">Create a scale set with attached data disks</span><span class="sxs-lookup"><span data-stu-id="9c616-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="9c616-110">A simple way to create a scale set with attached disks is to use the [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span><span class="sxs-lookup"><span data-stu-id="9c616-110">A simple way to create a scale set with attached disks is to use the [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="9c616-111">The following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span><span class="sxs-lookup"><span data-stu-id="9c616-111">The following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="9c616-112">Note that the _vmss create_ command defaults certain configuration values if you do not specify them.</span><span class="sxs-lookup"><span data-stu-id="9c616-112">Note that the _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="9c616-113">To see the available options that you can override try:</span><span class="sxs-lookup"><span data-stu-id="9c616-113">To see the available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="9c616-114">Another way to create a scale set with attached data disks is to define a scale set in an Azure Resource Manager template, include a _dataDisks_ section in the _storageProfile_, and deploy the template.</span><span class="sxs-lookup"><span data-stu-id="9c616-114">Another way to create a scale set with attached data disks is to define a scale set in an Azure Resource Manager template, include a _dataDisks_ section in the _storageProfile_, and deploy the template.</span></span> <span data-ttu-id="9c616-115">The 50 GB and 100 GB disk example above would be defined like this in the template:</span><span class="sxs-lookup"><span data-stu-id="9c616-115">The 50 GB and 100 GB disk example above would be defined like this in the template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="9c616-116">You can see a complete, ready to deploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span><span class="sxs-lookup"><span data-stu-id="9c616-116">You can see a complete, ready to deploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-to-an-existing-scale-set"></a><span data-ttu-id="9c616-117">Adding a data disk to an existing scale set</span><span class="sxs-lookup"><span data-stu-id="9c616-117">Adding a data disk to an existing scale set</span></span>
<span data-ttu-id="9c616-118">You can add a data disk to a VM scale set using Azure CLI _az vmss disk attach_ command.</span><span class="sxs-lookup"><span data-stu-id="9c616-118">You can add a data disk to a VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="9c616-119">Make sure you specify a lun which is not already in use.</span><span class="sxs-lookup"><span data-stu-id="9c616-119">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="9c616-120">The following CLI example adds a 50 GB drive to lun 3:</span><span class="sxs-lookup"><span data-stu-id="9c616-120">The following CLI example adds a 50 GB drive to lun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```
> [!NOTE]
> <span data-ttu-id="9c616-121">Different VM sizes have different limits on the numbers of attached drives they support.</span><span class="sxs-lookup"><span data-stu-id="9c616-121">Different VM sizes have different limits on the numbers of attached drives they support.</span></span> <span data-ttu-id="9c616-122">Check the [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span><span class="sxs-lookup"><span data-stu-id="9c616-122">Check the [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="9c616-123">You can also add a disk by adding a new entry to the _dataDisks_ property in the _storageProfile_ of a scale set definition and applying the change.</span><span class="sxs-lookup"><span data-stu-id="9c616-123">You can also add a disk by adding a new entry to the _dataDisks_ property in the _storageProfile_ of a scale set definition and applying the change.</span></span> <span data-ttu-id="9c616-124">To test this, find an existing scale set definition in the [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9c616-124">To test this, find an existing scale set definition in the [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="9c616-125">Select _Edit_ and add a new disk to the list of data disks.</span><span class="sxs-lookup"><span data-stu-id="9c616-125">Select _Edit_ and add a new disk to the list of data disks.</span></span> <span data-ttu-id="9c616-126">E.g.</span><span class="sxs-lookup"><span data-stu-id="9c616-126">E.g.</span></span> <span data-ttu-id="9c616-127">using the example above:</span><span class="sxs-lookup"><span data-stu-id="9c616-127">using the example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```
<span data-ttu-id="9c616-128">Then select _PUT_ to apply the changes to your scale set.</span><span class="sxs-lookup"><span data-stu-id="9c616-128">Then select _PUT_ to apply the changes to your scale set.</span></span> <span data-ttu-id="9c616-129">This example would work as long as you are using a VM size which supports more than two attached data disks.</span><span class="sxs-lookup"><span data-stu-id="9c616-129">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="9c616-130">When you make a change to a scale set definition such as adding or removing a data disk, it applies to all newly created VMs, but only applies to existing VMs if the _upgradePolicy_ property is set to "Automatic".</span><span class="sxs-lookup"><span data-stu-id="9c616-130">When you make a change to a scale set definition such as adding or removing a data disk, it applies to all newly created VMs, but only applies to existing VMs if the _upgradePolicy_ property is set to "Automatic".</span></span> <span data-ttu-id="9c616-131">If it is set to "Manual", you need to manually apply the new model to existing VMs.</span><span class="sxs-lookup"><span data-stu-id="9c616-131">If it is set to "Manual", you need to manually apply the new model to existing VMs.</span></span> <span data-ttu-id="9c616-132">You can do this in the portal, using the _Update-AzureRmVmssInstance_ PowerShell command, or using the _az vmss update-instances_ CLI command.</span><span class="sxs-lookup"><span data-stu-id="9c616-132">You can do this in the portal, using the _Update-AzureRmVmssInstance_ PowerShell command, or using the _az vmss update-instances_ CLI command.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="9c616-133">Removing a data disk from a scale set</span><span class="sxs-lookup"><span data-stu-id="9c616-133">Removing a data disk from a scale set</span></span>
<span data-ttu-id="9c616-134">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span><span class="sxs-lookup"><span data-stu-id="9c616-134">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="9c616-135">For example the following command removes the disk defined at lun 2:</span><span class="sxs-lookup"><span data-stu-id="9c616-135">For example the following command removes the disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="9c616-136">Similarly you can also remove a disk from a scale set by removing an entry from the _dataDisks_ property in the _storageProfile_ and applying the change.</span><span class="sxs-lookup"><span data-stu-id="9c616-136">Similarly you can also remove a disk from a scale set by removing an entry from the _dataDisks_ property in the _storageProfile_ and applying the change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="9c616-137">Additional notes</span><span class="sxs-lookup"><span data-stu-id="9c616-137">Additional notes</span></span>
<span data-ttu-id="9c616-138">Support for Azure Managed disks, and scale set attached data disks was added to the [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) version of the Microsoft.Compute APi.</span><span class="sxs-lookup"><span data-stu-id="9c616-138">Support for Azure Managed disks, and scale set attached data disks was added to the [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) version of the Microsoft.Compute APi.</span></span> <span data-ttu-id="9c616-139">You can use any SDK or command-line tool built with this version or later of the API.</span><span class="sxs-lookup"><span data-stu-id="9c616-139">You can use any SDK or command-line tool built with this version or later of the API.</span></span>

<span data-ttu-id="9c616-140">In the initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span><span class="sxs-lookup"><span data-stu-id="9c616-140">In the initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="9c616-141">Azure portal support for attached data disks in scale sets is initially limited.</span><span class="sxs-lookup"><span data-stu-id="9c616-141">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="9c616-142">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API to manage attached disks.</span><span class="sxs-lookup"><span data-stu-id="9c616-142">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API to manage attached disks.</span></span>


