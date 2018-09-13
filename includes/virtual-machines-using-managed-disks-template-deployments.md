---
title: include file
description: include file
services: storage
author: jboeshart
ms.service: storage
ms.topic: include
ms.date: 06/05/2018
ms.author: jaboes
ms.custom: include file
ms.openlocfilehash: b2561f4b1b5ef27f389114c85f0646b968f7765e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871660"
---
# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="898d8-103">Using Managed Disks in Azure Resource Manager Templates</span><span class="sxs-lookup"><span data-stu-id="898d8-103">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="898d8-104">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span><span class="sxs-lookup"><span data-stu-id="898d8-104">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span></span> <span data-ttu-id="898d8-105">The examples help you to update existing templates that are using unmanaged Disks to managed disks.</span><span class="sxs-lookup"><span data-stu-id="898d8-105">The examples help you to update existing templates that are using unmanaged Disks to managed disks.</span></span> <span data-ttu-id="898d8-106">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span><span class="sxs-lookup"><span data-stu-id="898d8-106">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="898d8-107">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span><span class="sxs-lookup"><span data-stu-id="898d8-107">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="898d8-108">Unmanaged Disks template formatting</span><span class="sxs-lookup"><span data-stu-id="898d8-108">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="898d8-109">To begin, let's take a look at how unmanaged disks are deployed.</span><span class="sxs-lookup"><span data-stu-id="898d8-109">To begin, let's take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="898d8-110">When creating unmanaged disks, you need a storage account to hold the VHD files.</span><span class="sxs-lookup"><span data-stu-id="898d8-110">When creating unmanaged disks, you need a storage account to hold the VHD files.</span></span> <span data-ttu-id="898d8-111">You can create a new storage account or use one that already exists.</span><span class="sxs-lookup"><span data-stu-id="898d8-111">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="898d8-112">This article shows you how to create a new storage account.</span><span class="sxs-lookup"><span data-stu-id="898d8-112">This article shows you how to create a new storage account.</span></span> <span data-ttu-id="898d8-113">Create a storage account resource in the resources block as shown below.</span><span class="sxs-lookup"><span data-stu-id="898d8-113">Create a storage account resource in the resources block as shown below.</span></span>

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="898d8-114">Within the virtual machine object, add a dependency on the storage account to ensure that it's created before the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="898d8-114">Within the virtual machine object, add a dependency on the storage account to ensure that it's created before the virtual machine.</span></span> <span data-ttu-id="898d8-115">Within the `storageProfile` section, specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span><span class="sxs-lookup"><span data-stu-id="898d8-115">Within the `storageProfile` section, specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="898d8-116">Managed disks template formatting</span><span class="sxs-lookup"><span data-stu-id="898d8-116">Managed disks template formatting</span></span>

<span data-ttu-id="898d8-117">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span><span class="sxs-lookup"><span data-stu-id="898d8-117">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span></span> <span data-ttu-id="898d8-118">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span><span class="sxs-lookup"><span data-stu-id="898d8-118">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span></span> <span data-ttu-id="898d8-119">The following sections walk through the default settings and detail how to further customize your disks.</span><span class="sxs-lookup"><span data-stu-id="898d8-119">The following sections walk through the default settings and detail how to further customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="898d8-120">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="898d8-120">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="898d8-121">Default managed disk settings</span><span class="sxs-lookup"><span data-stu-id="898d8-121">Default managed disk settings</span></span>

<span data-ttu-id="898d8-122">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span><span class="sxs-lookup"><span data-stu-id="898d8-122">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="898d8-123">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span><span class="sxs-lookup"><span data-stu-id="898d8-123">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span></span> <span data-ttu-id="898d8-124">When deploying without specifying additional properties, the disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="898d8-124">When deploying without specifying additional properties, the disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="898d8-125">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span><span class="sxs-lookup"><span data-stu-id="898d8-125">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="898d8-126">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span><span class="sxs-lookup"><span data-stu-id="898d8-126">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span></span> <span data-ttu-id="898d8-127">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span><span class="sxs-lookup"><span data-stu-id="898d8-127">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

```json
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="898d8-128">Using a top-level managed disk resource</span><span class="sxs-lookup"><span data-stu-id="898d8-128">Using a top-level managed disk resource</span></span>

<span data-ttu-id="898d8-129">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span><span class="sxs-lookup"><span data-stu-id="898d8-129">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span></span> <span data-ttu-id="898d8-130">For example, you can create a disk resource as follows to use as a data disk.</span><span class="sxs-lookup"><span data-stu-id="898d8-130">For example, you can create a disk resource as follows to use as a data disk.</span></span>

```json
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

<span data-ttu-id="898d8-131">Within the VM object, reference the disk object to be attached.</span><span class="sxs-lookup"><span data-stu-id="898d8-131">Within the VM object, reference the disk object to be attached.</span></span> <span data-ttu-id="898d8-132">Specifying the resource ID of the managed disk created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span><span class="sxs-lookup"><span data-stu-id="898d8-132">Specifying the resource ID of the managed disk created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span></span> <span data-ttu-id="898d8-133">The `apiVersion` for the VM resource is set to `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="898d8-133">The `apiVersion` for the VM resource is set to `2017-03-30`.</span></span> <span data-ttu-id="898d8-134">A dependency on the disk resource is added to ensure it's successfully created before VM creation.</span><span class="sxs-lookup"><span data-stu-id="898d8-134">A dependency on the disk resource is added to ensure it's successfully created before VM creation.</span></span> 

```json
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="898d8-135">Create managed availability sets with VMs using managed disks</span><span class="sxs-lookup"><span data-stu-id="898d8-135">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="898d8-136">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span><span class="sxs-lookup"><span data-stu-id="898d8-136">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span></span> <span data-ttu-id="898d8-137">This property ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span><span class="sxs-lookup"><span data-stu-id="898d8-137">This property ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span></span> <span data-ttu-id="898d8-138">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="898d8-138">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span></span>

```json
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="standard-ssd-disks"></a><span data-ttu-id="898d8-139">Standard SSD disks</span><span class="sxs-lookup"><span data-stu-id="898d8-139">Standard SSD disks</span></span>

<span data-ttu-id="898d8-140">Below are the parameters needed in the Resource Manager template to create Standard SSD Disks:</span><span class="sxs-lookup"><span data-stu-id="898d8-140">Below are the parameters needed in the Resource Manager template to create Standard SSD Disks:</span></span>

* <span data-ttu-id="898d8-141">*apiVersion* for Microsoft.Compute must be set as `2018-04-01` (or later)</span><span class="sxs-lookup"><span data-stu-id="898d8-141">*apiVersion* for Microsoft.Compute must be set as `2018-04-01` (or later)</span></span>
* <span data-ttu-id="898d8-142">Specify *managedDisk.storageAccountType* as `StandardSSD_LRS`</span><span class="sxs-lookup"><span data-stu-id="898d8-142">Specify *managedDisk.storageAccountType* as `StandardSSD_LRS`</span></span>

<span data-ttu-id="898d8-143">The following example shows the *properties.storageProfile.osDisk* section for a VM that uses Standard SSD Disks:</span><span class="sxs-lookup"><span data-stu-id="898d8-143">The following example shows the *properties.storageProfile.osDisk* section for a VM that uses Standard SSD Disks:</span></span>

```json
"osDisk": {
    "osType": "Windows",
    "name": "myOsDisk",
    "caching": "ReadWrite",
    "createOption": "FromImage",
    "managedDisk": {
        "storageAccountType": "StandardSSD_LRS"
    }
}
```

<span data-ttu-id="898d8-144">For a complete template example of how to create a Standard SSD disk with a template, see [Create a VM from a Windows Image with Standard SSD Data Disks](https://github.com/azure/azure-quickstart-templates/tree/master/101-vm-with-standardssd-disk/).</span><span class="sxs-lookup"><span data-stu-id="898d8-144">For a complete template example of how to create a Standard SSD disk with a template, see [Create a VM from a Windows Image with Standard SSD Data Disks](https://github.com/azure/azure-quickstart-templates/tree/master/101-vm-with-standardssd-disk/).</span></span>

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="898d8-145">Additional scenarios and customizations</span><span class="sxs-lookup"><span data-stu-id="898d8-145">Additional scenarios and customizations</span></span>

<span data-ttu-id="898d8-146">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="898d8-146">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="898d8-147">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span><span class="sxs-lookup"><span data-stu-id="898d8-147">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="898d8-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="898d8-148">Next steps</span></span>

* <span data-ttu-id="898d8-149">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span><span class="sxs-lookup"><span data-stu-id="898d8-149">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="898d8-150">Windows VM with managed disk</span><span class="sxs-lookup"><span data-stu-id="898d8-150">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="898d8-151">Linux VM with managed disk</span><span class="sxs-lookup"><span data-stu-id="898d8-151">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="898d8-152">Full list of managed disk templates</span><span class="sxs-lookup"><span data-stu-id="898d8-152">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="898d8-153">Visit the [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document to learn more about managed disks.</span><span class="sxs-lookup"><span data-stu-id="898d8-153">Visit the [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document to learn more about managed disks.</span></span>
* <span data-ttu-id="898d8-154">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/azure/templates/microsoft.compute/virtualmachines) document.</span><span class="sxs-lookup"><span data-stu-id="898d8-154">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/azure/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="898d8-155">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/azure/templates/microsoft.compute/disks) document.</span><span class="sxs-lookup"><span data-stu-id="898d8-155">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/azure/templates/microsoft.compute/disks) document.</span></span>
* <span data-ttu-id="898d8-156">For information on how to use managed disks in Azure virtual machine scale sets, visit the [Use data disks with scale sets](https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-attached-disks) document.</span><span class="sxs-lookup"><span data-stu-id="898d8-156">For information on how to use managed disks in Azure virtual machine scale sets, visit the [Use data disks with scale sets](https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-attached-disks) document.</span></span>
