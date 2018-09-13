---
title: Create a Windows VM from a template in Azure | Microsoft Docs
description: Use a Resource Manager template and PowerShell to easily create a new Windows VM.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 336e597ccefd68603426b952b4dc304cb519dd9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44790275"
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="13d40-103">Create a Windows virtual machine from a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="13d40-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="13d40-104">This article shows you how to deploy an Azure Resource Manager template using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13d40-104">This article shows you how to deploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="13d40-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span><span class="sxs-lookup"><span data-stu-id="13d40-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="13d40-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="13d40-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="13d40-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="13d40-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="13d40-108">It should take about five minutes to do the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="13d40-108">It should take about five minutes to do the steps in this article.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="13d40-109">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.3 or later.</span><span class="sxs-lookup"><span data-stu-id="13d40-109">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.3 or later.</span></span> <span data-ttu-id="13d40-110">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="13d40-110">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="13d40-111">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="13d40-111">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="13d40-112">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="13d40-112">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="13d40-113">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="13d40-113">Create a resource group</span></span>

<span data-ttu-id="13d40-114">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13d40-114">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="13d40-115">Get a list of available locations where resources can be created.</span><span class="sxs-lookup"><span data-stu-id="13d40-115">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="13d40-116">Create the resource group in the location that you select.</span><span class="sxs-lookup"><span data-stu-id="13d40-116">Create the resource group in the location that you select.</span></span> <span data-ttu-id="13d40-117">This example shows the creation of a resource group named **myResourceGroup** in the **West US** location:</span><span class="sxs-lookup"><span data-stu-id="13d40-117">This example shows the creation of a resource group named **myResourceGroup** in the **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-the-files"></a><span data-ttu-id="13d40-118">Create the files</span><span class="sxs-lookup"><span data-stu-id="13d40-118">Create the files</span></span>

<span data-ttu-id="13d40-119">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span><span class="sxs-lookup"><span data-stu-id="13d40-119">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="13d40-120">You also create an authorization file that is used to perform Azure Resource Manager operations.</span><span class="sxs-lookup"><span data-stu-id="13d40-120">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="13d40-121">Create a file named *CreateVMTemplate.json* and add this JSON code to it:</span><span class="sxs-lookup"><span data-stu-id="13d40-121">Create a file named *CreateVMTemplate.json* and add this JSON code to it:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]" 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. <span data-ttu-id="13d40-122">Create a file named *Parameters.json* and add this JSON code to it:</span><span class="sxs-lookup"><span data-stu-id="13d40-122">Create a file named *Parameters.json* and add this JSON code to it:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. <span data-ttu-id="13d40-123">Create a new storage account and container:</span><span class="sxs-lookup"><span data-stu-id="13d40-123">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="13d40-124">Upload the files to the storage account:</span><span class="sxs-lookup"><span data-stu-id="13d40-124">Upload the files to the storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="13d40-125">Change the -File paths to the location where you stored the files.</span><span class="sxs-lookup"><span data-stu-id="13d40-125">Change the -File paths to the location where you stored the files.</span></span>

## <a name="create-the-resources"></a><span data-ttu-id="13d40-126">Create the resources</span><span class="sxs-lookup"><span data-stu-id="13d40-126">Create the resources</span></span>

<span data-ttu-id="13d40-127">Deploy the template using the parameters:</span><span class="sxs-lookup"><span data-stu-id="13d40-127">Deploy the template using the parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="13d40-128">You can also deploy templates and parameters from local files.</span><span class="sxs-lookup"><span data-stu-id="13d40-128">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="13d40-129">To learn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="13d40-129">To learn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="13d40-130">Next Steps</span><span class="sxs-lookup"><span data-stu-id="13d40-130">Next Steps</span></span>

- <span data-ttu-id="13d40-131">If there were issues with the deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="13d40-131">If there were issues with the deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="13d40-132">Learn how to create and manage a virtual machine in [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13d40-132">Learn how to create and manage a virtual machine in [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

