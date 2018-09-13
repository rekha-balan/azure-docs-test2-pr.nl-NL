---
title: Convert an Azure Resource Manager scale set template to use managed disk | Microsoft Docs
description: Convert a scale set template to a managed disk scale set template.
keywords: virtual machine scale sets
services: virtual-machine-scale-sets
documentationcenter: ''
author: gatneil
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 760e30f5c6f4ecaff299bae1725548a6a7c5184c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827684"
---
# <a name="convert-a-scale-set-template-to-a-managed-disk-scale-set-template"></a><span data-ttu-id="1a655-104">Convert a scale set template to a managed disk scale set template</span><span class="sxs-lookup"><span data-stu-id="1a655-104">Convert a scale set template to a managed disk scale set template</span></span>

<span data-ttu-id="1a655-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish to modify it to use managed disk.</span><span class="sxs-lookup"><span data-stu-id="1a655-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish to modify it to use managed disk.</span></span> <span data-ttu-id="1a655-106">This article shows how to use managed disks, using as an example a pull request from the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="1a655-106">This article shows how to use managed disks, using as an example a pull request from the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="1a655-107">The full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and the relevant parts of the diff are below, along with explanations:</span><span class="sxs-lookup"><span data-stu-id="1a655-107">The full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and the relevant parts of the diff are below, along with explanations:</span></span>

## <a name="making-the-os-disks-managed"></a><span data-ttu-id="1a655-108">Making the OS disks managed</span><span class="sxs-lookup"><span data-stu-id="1a655-108">Making the OS disks managed</span></span>

<span data-ttu-id="1a655-109">In the following diff, several variables related to storage account and disk properties are removed.</span><span class="sxs-lookup"><span data-stu-id="1a655-109">In the following diff, several variables related to storage account and disk properties are removed.</span></span> <span data-ttu-id="1a655-110">Storage account type is no longer necessary (Standard_LRS is the default), but you could specify it if desired.</span><span class="sxs-lookup"><span data-stu-id="1a655-110">Storage account type is no longer necessary (Standard_LRS is the default), but you could specify it if desired.</span></span> <span data-ttu-id="1a655-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span><span class="sxs-lookup"><span data-stu-id="1a655-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="1a655-112">New storage account suffix, unique string array, and sa count were used in the old template to generate storage account names.</span><span class="sxs-lookup"><span data-stu-id="1a655-112">New storage account suffix, unique string array, and sa count were used in the old template to generate storage account names.</span></span> <span data-ttu-id="1a655-113">These variables are no longer necessary in the new template because managed disk automatically creates storage accounts on the customer's behalf.</span><span class="sxs-lookup"><span data-stu-id="1a655-113">These variables are no longer necessary in the new template because managed disk automatically creates storage accounts on the customer's behalf.</span></span> <span data-ttu-id="1a655-114">Similarly, vhd container name and OS disk name are no longer necessary because managed disk automatically names the underlying storage blob containers and disks.</span><span class="sxs-lookup"><span data-stu-id="1a655-114">Similarly, vhd container name and OS disk name are no longer necessary because managed disk automatically names the underlying storage blob containers and disks.</span></span>

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


<span data-ttu-id="1a655-115">In the following diff, you compute API is updated to version 2016-04-30-preview, which is the earliest required version for managed disk support with scale sets.</span><span class="sxs-lookup"><span data-stu-id="1a655-115">In the following diff, you compute API is updated to version 2016-04-30-preview, which is the earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="1a655-116">You could use unmanaged disks in the new API version with the old syntax if desired.</span><span class="sxs-lookup"><span data-stu-id="1a655-116">You could use unmanaged disks in the new API version with the old syntax if desired.</span></span> <span data-ttu-id="1a655-117">If you only update the compute API version and don't change anything else, the template should continue to work as before.</span><span class="sxs-lookup"><span data-stu-id="1a655-117">If you only update the compute API version and don't change anything else, the template should continue to work as before.</span></span>

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

<span data-ttu-id="1a655-118">In the following diff, the storage account resource is removed from the resources array completely.</span><span class="sxs-lookup"><span data-stu-id="1a655-118">In the following diff, the storage account resource is removed from the resources array completely.</span></span> <span data-ttu-id="1a655-119">The resource is no longer needed as managed disk creates them automatically.</span><span class="sxs-lookup"><span data-stu-id="1a655-119">The resource is no longer needed as managed disk creates them automatically.</span></span>

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

<span data-ttu-id="1a655-120">In the following diff, we can see that we are removing the depends on clause referring from the scale set to the loop that was creating storage accounts.</span><span class="sxs-lookup"><span data-stu-id="1a655-120">In the following diff, we can see that we are removing the depends on clause referring from the scale set to the loop that was creating storage accounts.</span></span> <span data-ttu-id="1a655-121">In the old template, this was ensuring that the storage accounts were created before the scale set began creation, but this clause is no longer necessary with managed disk.</span><span class="sxs-lookup"><span data-stu-id="1a655-121">In the old template, this was ensuring that the storage accounts were created before the scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="1a655-122">The vhd containers property is also removed, along with the OS disk name property as these properties are automatically handled under the hood by managed disk.</span><span class="sxs-lookup"><span data-stu-id="1a655-122">The vhd containers property is also removed, along with the OS disk name property as these properties are automatically handled under the hood by managed disk.</span></span> <span data-ttu-id="1a655-123">You could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in the "osDisk" configuration if you wanted premium OS disks.</span><span class="sxs-lookup"><span data-stu-id="1a655-123">You could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in the "osDisk" configuration if you wanted premium OS disks.</span></span> <span data-ttu-id="1a655-124">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span><span class="sxs-lookup"><span data-stu-id="1a655-124">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

<span data-ttu-id="1a655-125">There is no explicit property in the scale set configuration for whether to use managed or unmanaged disk.</span><span class="sxs-lookup"><span data-stu-id="1a655-125">There is no explicit property in the scale set configuration for whether to use managed or unmanaged disk.</span></span> <span data-ttu-id="1a655-126">The scale set knows which to use based on the properties that are present in the storage profile.</span><span class="sxs-lookup"><span data-stu-id="1a655-126">The scale set knows which to use based on the properties that are present in the storage profile.</span></span> <span data-ttu-id="1a655-127">Thus, it is important when modifying the template to ensure that the right properties are in the storage profile of the scale set.</span><span class="sxs-lookup"><span data-stu-id="1a655-127">Thus, it is important when modifying the template to ensure that the right properties are in the storage profile of the scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="1a655-128">Data disks</span><span class="sxs-lookup"><span data-stu-id="1a655-128">Data disks</span></span>

<span data-ttu-id="1a655-129">With the changes above, the scale set uses managed disks for the OS disk, but what about data disks?</span><span class="sxs-lookup"><span data-stu-id="1a655-129">With the changes above, the scale set uses managed disks for the OS disk, but what about data disks?</span></span> <span data-ttu-id="1a655-130">To add data disks, add the "dataDisks" property under "storageProfile" at the same level as "osDisk".</span><span class="sxs-lookup"><span data-stu-id="1a655-130">To add data disks, add the "dataDisks" property under "storageProfile" at the same level as "osDisk".</span></span> <span data-ttu-id="1a655-131">The value of the property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently the only supported option), and "diskSizeGB" (the size of the disk in gigabytes; must be greater than 0 and less than 1024) as in the following example:</span><span class="sxs-lookup"><span data-stu-id="1a655-131">The value of the property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently the only supported option), and "diskSizeGB" (the size of the disk in gigabytes; must be greater than 0 and less than 1024) as in the following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="1a655-132">If you specify `n` disks in this array, each VM in the scale set gets `n` data disks.</span><span class="sxs-lookup"><span data-stu-id="1a655-132">If you specify `n` disks in this array, each VM in the scale set gets `n` data disks.</span></span> <span data-ttu-id="1a655-133">Do note, however, that these data disks are raw devices.</span><span class="sxs-lookup"><span data-stu-id="1a655-133">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="1a655-134">They are not formatted.</span><span class="sxs-lookup"><span data-stu-id="1a655-134">They are not formatted.</span></span> <span data-ttu-id="1a655-135">It is up to the customer to attach, partition, and format the disks before using them.</span><span class="sxs-lookup"><span data-stu-id="1a655-135">It is up to the customer to attach, partition, and format the disks before using them.</span></span> <span data-ttu-id="1a655-136">Optionally, you could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object to specify that it should be a premium data disk.</span><span class="sxs-lookup"><span data-stu-id="1a655-136">Optionally, you could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object to specify that it should be a premium data disk.</span></span> <span data-ttu-id="1a655-137">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span><span class="sxs-lookup"><span data-stu-id="1a655-137">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

<span data-ttu-id="1a655-138">To learn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="1a655-138">To learn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="1a655-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a655-139">Next steps</span></span>
<span data-ttu-id="1a655-140">For example Resource Manager templates using scale sets, search for "vmss" in the [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="1a655-140">For example Resource Manager templates using scale sets, search for "vmss" in the [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="1a655-141">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="1a655-141">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

