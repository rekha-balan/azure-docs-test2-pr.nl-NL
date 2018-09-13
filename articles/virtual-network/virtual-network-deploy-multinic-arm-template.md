---
title: Create a VM with multiple NICs - Azure Resource Manager template | Microsoft Docs
description: Create a VM with multiple NICs using an Azure Resource Manager template.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6630064df71afd31807d4f8daeb0e82df90153f1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563824"
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="8e23e-103">Create a VM with multiple NICs using a template</span><span class="sxs-lookup"><span data-stu-id="8e23e-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="8e23e-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8e23e-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8e23e-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8e23e-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="8e23e-106">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span><span class="sxs-lookup"><span data-stu-id="8e23e-106">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e23e-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8e23e-107">Prerequisites</span></span>
<span data-ttu-id="8e23e-108">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span><span class="sxs-lookup"><span data-stu-id="8e23e-108">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="8e23e-109">To create these resources, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="8e23e-109">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="8e23e-110">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="8e23e-110">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="8e23e-111">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e23e-111">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="8e23e-112">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span><span class="sxs-lookup"><span data-stu-id="8e23e-112">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e23e-113">Make sure your storage account names are unique.</span><span class="sxs-lookup"><span data-stu-id="8e23e-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="8e23e-114">You cannot have duplicate storage account names in Azure.</span><span class="sxs-lookup"><span data-stu-id="8e23e-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-the-deployment-template"></a><span data-ttu-id="8e23e-115">Understand the deployment template</span><span class="sxs-lookup"><span data-stu-id="8e23e-115">Understand the deployment template</span></span>
<span data-ttu-id="8e23e-116">Before you deploy the template provided with this documentation, make sure you understand what it does.</span><span class="sxs-lookup"><span data-stu-id="8e23e-116">Before you deploy the template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="8e23e-117">The following steps provide a good overview of the template:</span><span class="sxs-lookup"><span data-stu-id="8e23e-117">The following steps provide a good overview of the template:</span></span>

1. <span data-ttu-id="8e23e-118">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="8e23e-118">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="8e23e-119">Click **azuredeploy.json** to open the template file.</span><span class="sxs-lookup"><span data-stu-id="8e23e-119">Click **azuredeploy.json** to open the template file.</span></span>
3. <span data-ttu-id="8e23e-120">Notice the *osType* parameter listed below.</span><span class="sxs-lookup"><span data-stu-id="8e23e-120">Notice the *osType* parameter listed below.</span></span> <span data-ttu-id="8e23e-121">This parameter is used to select what VM image to use for the database server, along with multiple operating system related settings.</span><span class="sxs-lookup"><span data-stu-id="8e23e-121">This parameter is used to select what VM image to use for the database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS to use for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="8e23e-122">Scroll down to the list of variables, and check the definition for the **dbVMSetting** variables, listed below.</span><span class="sxs-lookup"><span data-stu-id="8e23e-122">Scroll down to the list of variables, and check the definition for the **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="8e23e-123">It receives one of the array elements contained in the **dbVMSettings** variable.</span><span class="sxs-lookup"><span data-stu-id="8e23e-123">It receives one of the array elements contained in the **dbVMSettings** variable.</span></span> <span data-ttu-id="8e23e-124">If you are familiar with software development terminology, you can view the **dbVMSettings** variable as a hash table, or a dictionary.</span><span class="sxs-lookup"><span data-stu-id="8e23e-124">If you are familiar with software development terminology, you can view the **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="8e23e-125">Suppose you decide to deploy Windows VMs running SQL in the back-end.</span><span class="sxs-lookup"><span data-stu-id="8e23e-125">Suppose you decide to deploy Windows VMs running SQL in the back-end.</span></span> <span data-ttu-id="8e23e-126">Then the value for **osType** would be *Windows*, and the **dbVMSetting** variable would contain the element listed below, which represents the first value in the **dbVMSettings** variable.</span><span class="sxs-lookup"><span data-stu-id="8e23e-126">Then the value for **osType** would be *Windows*, and the **dbVMSetting** variable would contain the element listed below, which represents the first value in the **dbVMSettings** variable.</span></span>

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. <span data-ttu-id="8e23e-127">Notice the **vmSize** contains the value *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="8e23e-127">Notice the **vmSize** contains the value *Standard_DS3*.</span></span> <span data-ttu-id="8e23e-128">Only certain VM sizes allow for the use of multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="8e23e-128">Only certain VM sizes allow for the use of multiple NICs.</span></span> <span data-ttu-id="8e23e-129">You can verify which VM sizes support multiple NICs by reading the [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span><span class="sxs-lookup"><span data-stu-id="8e23e-129">You can verify which VM sizes support multiple NICs by reading the [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="8e23e-130">Scroll down to **resources** and notice the first element.</span><span class="sxs-lookup"><span data-stu-id="8e23e-130">Scroll down to **resources** and notice the first element.</span></span> <span data-ttu-id="8e23e-131">It describes a storage account.</span><span class="sxs-lookup"><span data-stu-id="8e23e-131">It describes a storage account.</span></span> <span data-ttu-id="8e23e-132">This storage account will be used to maintain the data disks used by each database VM.</span><span class="sxs-lookup"><span data-stu-id="8e23e-132">This storage account will be used to maintain the data disks used by each database VM.</span></span> <span data-ttu-id="8e23e-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span><span class="sxs-lookup"><span data-stu-id="8e23e-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. <span data-ttu-id="8e23e-134">Scroll down to the next resource, as listed below.</span><span class="sxs-lookup"><span data-stu-id="8e23e-134">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="8e23e-135">This resource represents the NIC used for database access in each database VM.</span><span class="sxs-lookup"><span data-stu-id="8e23e-135">This resource represents the NIC used for database access in each database VM.</span></span> <span data-ttu-id="8e23e-136">Notice the use of the **copy** function in this resource.</span><span class="sxs-lookup"><span data-stu-id="8e23e-136">Notice the use of the **copy** function in this resource.</span></span> <span data-ttu-id="8e23e-137">The template allows you to deploy as many VMs as you want, based on the **dbCount** parameter.</span><span class="sxs-lookup"><span data-stu-id="8e23e-137">The template allows you to deploy as many VMs as you want, based on the **dbCount** parameter.</span></span> <span data-ttu-id="8e23e-138">Therefore you need to create the same amount of NICs for database access, one for each VM.</span><span class="sxs-lookup"><span data-stu-id="8e23e-138">Therefore you need to create the same amount of NICs for database access, one for each VM.</span></span>

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. <span data-ttu-id="8e23e-139">Scroll down to the next resource, as listed below.</span><span class="sxs-lookup"><span data-stu-id="8e23e-139">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="8e23e-140">This resource represents the NIC used for management in each database VM.</span><span class="sxs-lookup"><span data-stu-id="8e23e-140">This resource represents the NIC used for management in each database VM.</span></span> <span data-ttu-id="8e23e-141">Once again, you need one of these NICs for each database VM.</span><span class="sxs-lookup"><span data-stu-id="8e23e-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="8e23e-142">Notice the **networkSecurityGroup** element, linking an NSG that allows access to RDP/SSH to this NIC only.</span><span class="sxs-lookup"><span data-stu-id="8e23e-142">Notice the **networkSecurityGroup** element, linking an NSG that allows access to RDP/SSH to this NIC only.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. <span data-ttu-id="8e23e-143">Scroll down to the next resource, as listed below.</span><span class="sxs-lookup"><span data-stu-id="8e23e-143">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="8e23e-144">This resource represents an availability set to be shared by all database VMs.</span><span class="sxs-lookup"><span data-stu-id="8e23e-144">This resource represents an availability set to be shared by all database VMs.</span></span> <span data-ttu-id="8e23e-145">That way, you guarantee that there will always be one VM in the set running during maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e23e-145">That way, you guarantee that there will always be one VM in the set running during maintenance.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. <span data-ttu-id="8e23e-146">Scroll down to the next resource.</span><span class="sxs-lookup"><span data-stu-id="8e23e-146">Scroll down to the next resource.</span></span> <span data-ttu-id="8e23e-147">This resource represents the database VMs, as seen in the first few lines listed below.</span><span class="sxs-lookup"><span data-stu-id="8e23e-147">This resource represents the database VMs, as seen in the first few lines listed below.</span></span> <span data-ttu-id="8e23e-148">Notice the use of the **copy** function again, ensuring that multiple VMs are created based on the **dbCount** parameter.</span><span class="sxs-lookup"><span data-stu-id="8e23e-148">Notice the use of the **copy** function again, ensuring that multiple VMs are created based on the **dbCount** parameter.</span></span> <span data-ttu-id="8e23e-149">Also notice the **dependsOn** collection.</span><span class="sxs-lookup"><span data-stu-id="8e23e-149">Also notice the **dependsOn** collection.</span></span> <span data-ttu-id="8e23e-150">It lists two NICs being necessary to be created before the VM is deployed, along with the availability set, and the storage account.</span><span class="sxs-lookup"><span data-stu-id="8e23e-150">It lists two NICs being necessary to be created before the VM is deployed, along with the availability set, and the storage account.</span></span>

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. <span data-ttu-id="8e23e-151">Scroll down in the VM resource to the **networkProfile** element, as listed below.</span><span class="sxs-lookup"><span data-stu-id="8e23e-151">Scroll down in the VM resource to the **networkProfile** element, as listed below.</span></span> <span data-ttu-id="8e23e-152">Notice that there are two NICs being reference for each VM.</span><span class="sxs-lookup"><span data-stu-id="8e23e-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="8e23e-153">When you create multiple NICs for a VM, you must set the **primary** property of one of the NICs to *true*, and the rest to *false*.</span><span class="sxs-lookup"><span data-stu-id="8e23e-153">When you create multiple NICs for a VM, you must set the **primary** property of one of the NICs to *true*, and the rest to *false*.</span></span>

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-the-arm-template-by-using-click-to-deploy"></a><span data-ttu-id="8e23e-154">Deploy the ARM template by using click to deploy</span><span class="sxs-lookup"><span data-stu-id="8e23e-154">Deploy the ARM template by using click to deploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e23e-155">Make sure you follow the [pre-requisites](#Pre-requisites) steps before following the instructions below.</span><span class="sxs-lookup"><span data-stu-id="8e23e-155">Make sure you follow the [pre-requisites](#Pre-requisites) steps before following the instructions below.</span></span>
> 

<span data-ttu-id="8e23e-156">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span><span class="sxs-lookup"><span data-stu-id="8e23e-156">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="8e23e-157">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), to the right of **Backend resource group (see documentation)** click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span><span class="sxs-lookup"><span data-stu-id="8e23e-157">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), to the right of **Backend resource group (see documentation)** click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

<span data-ttu-id="8e23e-158">The figure below shows the contents of the new resource group, after deployment.</span><span class="sxs-lookup"><span data-stu-id="8e23e-158">The figure below shows the contents of the new resource group, after deployment.</span></span>

![Back end resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="8e23e-160">Deploy the template by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e23e-160">Deploy the template by using PowerShell</span></span>
<span data-ttu-id="8e23e-161">To deploy the template you downloaded by using PowerShell, install and configure PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azureps-cmdlets-docs) article and then complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="8e23e-161">To deploy the template you downloaded by using PowerShell, install and configure PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azureps-cmdlets-docs) article and then complete the following steps:</span></span>

<span data-ttu-id="8e23e-162">Run the **`New-AzureRmResourceGroup`** cmdlet to create a resource group using the template.</span><span class="sxs-lookup"><span data-stu-id="8e23e-162">Run the **`New-AzureRmResourceGroup`** cmdlet to create a resource group using the template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="8e23e-163">Expected output:</span><span class="sxs-lookup"><span data-stu-id="8e23e-163">Expected output:</span></span>

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="8e23e-164">Deploy the template by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8e23e-164">Deploy the template by using the Azure CLI</span></span>
<span data-ttu-id="8e23e-165">To deploy the template by using the Azure CLI, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="8e23e-165">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="8e23e-166">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="8e23e-166">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="8e23e-167">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span><span class="sxs-lookup"><span data-stu-id="8e23e-167">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="8e23e-168">The expected output follows:</span><span class="sxs-lookup"><span data-stu-id="8e23e-168">The expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="8e23e-169">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it to a file in your computer.</span><span class="sxs-lookup"><span data-stu-id="8e23e-169">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it to a file in your computer.</span></span> <span data-ttu-id="8e23e-170">For this example, we saved the parameters file to *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="8e23e-170">For this example, we saved the parameters file to *parameters.json*.</span></span>
4. <span data-ttu-id="8e23e-171">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span><span class="sxs-lookup"><span data-stu-id="8e23e-171">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="8e23e-172">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="8e23e-172">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="8e23e-173">Expected output:</span><span class="sxs-lookup"><span data-stu-id="8e23e-173">Expected output:</span></span>
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK


