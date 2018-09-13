---
title: Virtual machines in an Azure Resource Manager template | Microsoft Azure
description: Learn more about how the virtual machine resource is defined in an Azure Resource Manager template.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: cynthn
ms.openlocfilehash: ede6a0c4b981dcd06cbebdef3298bbbb05229c15
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803314"
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="f6c33-103">Virtual machines in an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="f6c33-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="f6c33-104">This article describes aspects of an Azure Resource Manager template that apply to virtual machines.</span><span class="sxs-lookup"><span data-stu-id="f6c33-104">This article describes aspects of an Azure Resource Manager template that apply to virtual machines.</span></span> <span data-ttu-id="f6c33-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span><span class="sxs-lookup"><span data-stu-id="f6c33-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="f6c33-106">For more information about how these resources can be defined together, see the [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f6c33-106">For more information about how these resources can be defined together, see the [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="f6c33-107">There are many [templates in the gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include the VM resource.</span><span class="sxs-lookup"><span data-stu-id="f6c33-107">There are many [templates in the gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include the VM resource.</span></span> <span data-ttu-id="f6c33-108">Not all elements that can be included in a template are described here.</span><span class="sxs-lookup"><span data-stu-id="f6c33-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="f6c33-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span><span class="sxs-lookup"><span data-stu-id="f6c33-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
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
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
><span data-ttu-id="f6c33-110">This example relies on a storage account that was previously created.</span><span class="sxs-lookup"><span data-stu-id="f6c33-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="f6c33-111">You could create the storage account by deploying it from the template.</span><span class="sxs-lookup"><span data-stu-id="f6c33-111">You could create the storage account by deploying it from the template.</span></span> <span data-ttu-id="f6c33-112">The example also relies on a network interface and its dependent resources that would be defined in the template.</span><span class="sxs-lookup"><span data-stu-id="f6c33-112">The example also relies on a network interface and its dependent resources that would be defined in the template.</span></span> <span data-ttu-id="f6c33-113">These resources are not shown in the example.</span><span class="sxs-lookup"><span data-stu-id="f6c33-113">These resources are not shown in the example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="f6c33-114">API Version</span><span class="sxs-lookup"><span data-stu-id="f6c33-114">API Version</span></span>

<span data-ttu-id="f6c33-115">When you deploy resources using a template, you have to specify a version of the API to use.</span><span class="sxs-lookup"><span data-stu-id="f6c33-115">When you deploy resources using a template, you have to specify a version of the API to use.</span></span> <span data-ttu-id="f6c33-116">The example shows the virtual machine resource using this apiVersion element:</span><span class="sxs-lookup"><span data-stu-id="f6c33-116">The example shows the virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="f6c33-117">The version of the API you specify in your template affects which properties you can define in the template.</span><span class="sxs-lookup"><span data-stu-id="f6c33-117">The version of the API you specify in your template affects which properties you can define in the template.</span></span> <span data-ttu-id="f6c33-118">In general, you should select the most recent API version when creating templates.</span><span class="sxs-lookup"><span data-stu-id="f6c33-118">In general, you should select the most recent API version when creating templates.</span></span> <span data-ttu-id="f6c33-119">For existing templates, you can decide whether you want to continue using an earlier API version, or update your template for the latest version to take advantage of new features.</span><span class="sxs-lookup"><span data-stu-id="f6c33-119">For existing templates, you can decide whether you want to continue using an earlier API version, or update your template for the latest version to take advantage of new features.</span></span>

<span data-ttu-id="f6c33-120">Use these opportunities for getting the latest API versions:</span><span class="sxs-lookup"><span data-stu-id="f6c33-120">Use these opportunities for getting the latest API versions:</span></span>

- <span data-ttu-id="f6c33-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="f6c33-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="f6c33-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="f6c33-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="f6c33-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#az_provider_show)</span><span class="sxs-lookup"><span data-stu-id="f6c33-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#az_provider_show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="f6c33-124">Parameters and variables</span><span class="sxs-lookup"><span data-stu-id="f6c33-124">Parameters and variables</span></span>

<span data-ttu-id="f6c33-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you to specify values for the template when you run it.</span><span class="sxs-lookup"><span data-stu-id="f6c33-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you to specify values for the template when you run it.</span></span> <span data-ttu-id="f6c33-126">This parameters section is used in the example:</span><span class="sxs-lookup"><span data-stu-id="f6c33-126">This parameters section is used in the example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="f6c33-127">When you deploy the example template, you enter values for the name and password of the administrator account on each VM and the number of VMs to create.</span><span class="sxs-lookup"><span data-stu-id="f6c33-127">When you deploy the example template, you enter values for the name and password of the administrator account on each VM and the number of VMs to create.</span></span> <span data-ttu-id="f6c33-128">You have the option of specifying parameter values in a separate file that's managed with the template, or providing values when prompted.</span><span class="sxs-lookup"><span data-stu-id="f6c33-128">You have the option of specifying parameter values in a separate file that's managed with the template, or providing values when prompted.</span></span>

<span data-ttu-id="f6c33-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you to set up values in the template that are used repeatedly throughout it or that can change over time.</span><span class="sxs-lookup"><span data-stu-id="f6c33-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you to set up values in the template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="f6c33-130">This variables section is used in the example:</span><span class="sxs-lookup"><span data-stu-id="f6c33-130">This variables section is used in the example:</span></span>

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

<span data-ttu-id="f6c33-131">When you deploy the example template, variable values are used for the name and identifier of the previously created storage account.</span><span class="sxs-lookup"><span data-stu-id="f6c33-131">When you deploy the example template, variable values are used for the name and identifier of the previously created storage account.</span></span> <span data-ttu-id="f6c33-132">Variables are also used to provide the settings for the diagnostic extension.</span><span class="sxs-lookup"><span data-stu-id="f6c33-132">Variables are also used to provide the settings for the diagnostic extension.</span></span> <span data-ttu-id="f6c33-133">Use the [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) to help you decide how you want to structure the parameters and variables in your template.</span><span class="sxs-lookup"><span data-stu-id="f6c33-133">Use the [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) to help you decide how you want to structure the parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="f6c33-134">Resource loops</span><span class="sxs-lookup"><span data-stu-id="f6c33-134">Resource loops</span></span>

<span data-ttu-id="f6c33-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span><span class="sxs-lookup"><span data-stu-id="f6c33-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="f6c33-136">This optional element loops through creating the number of VMs that you specified as a parameter:</span><span class="sxs-lookup"><span data-stu-id="f6c33-136">This optional element loops through creating the number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="f6c33-137">Also, notice in the example that the loop index is used when specifying some of the values for the resource.</span><span class="sxs-lookup"><span data-stu-id="f6c33-137">Also, notice in the example that the loop index is used when specifying some of the values for the resource.</span></span> <span data-ttu-id="f6c33-138">For example, if you entered an instance count of three, the names of the operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span><span class="sxs-lookup"><span data-stu-id="f6c33-138">For example, if you entered an instance count of three, the names of the operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="f6c33-139">This example uses managed disks for the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="f6c33-139">This example uses managed disks for the virtual machines.</span></span>
>
>

<span data-ttu-id="f6c33-140">Keep in mind that creating a loop for one resource in the template may require you to use the loop when creating or accessing other resources.</span><span class="sxs-lookup"><span data-stu-id="f6c33-140">Keep in mind that creating a loop for one resource in the template may require you to use the loop when creating or accessing other resources.</span></span> <span data-ttu-id="f6c33-141">For example, multiple VMs can’t use the same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span><span class="sxs-lookup"><span data-stu-id="f6c33-141">For example, multiple VMs can’t use the same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="f6c33-142">When assigning a network interface to a VM, the loop index is used to identify it:</span><span class="sxs-lookup"><span data-stu-id="f6c33-142">When assigning a network interface to a VM, the loop index is used to identify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="f6c33-143">Dependencies</span><span class="sxs-lookup"><span data-stu-id="f6c33-143">Dependencies</span></span>

<span data-ttu-id="f6c33-144">Most resources depend on other resources to work correctly.</span><span class="sxs-lookup"><span data-stu-id="f6c33-144">Most resources depend on other resources to work correctly.</span></span> <span data-ttu-id="f6c33-145">Virtual machines must be associated with a virtual network and to do that it needs a network interface.</span><span class="sxs-lookup"><span data-stu-id="f6c33-145">Virtual machines must be associated with a virtual network and to do that it needs a network interface.</span></span> <span data-ttu-id="f6c33-146">The [dependsOn](../../resource-group-define-dependencies.md) element is used to make sure that the network interface is ready to be used before the VMs are created:</span><span class="sxs-lookup"><span data-stu-id="f6c33-146">The [dependsOn](../../resource-group-define-dependencies.md) element is used to make sure that the network interface is ready to be used before the VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="f6c33-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span><span class="sxs-lookup"><span data-stu-id="f6c33-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="f6c33-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span><span class="sxs-lookup"><span data-stu-id="f6c33-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="f6c33-149">Dependencies can chain through multiple resources.</span><span class="sxs-lookup"><span data-stu-id="f6c33-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="f6c33-150">For example, the network interface depends on the public IP address and virtual network resources.</span><span class="sxs-lookup"><span data-stu-id="f6c33-150">For example, the network interface depends on the public IP address and virtual network resources.</span></span>

<span data-ttu-id="f6c33-151">How do you know if a dependency is required?</span><span class="sxs-lookup"><span data-stu-id="f6c33-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="f6c33-152">Look at the values you set in the template.</span><span class="sxs-lookup"><span data-stu-id="f6c33-152">Look at the values you set in the template.</span></span> <span data-ttu-id="f6c33-153">If an element in the virtual machine resource definition points to another resource that is deployed in the same template, you need a dependency.</span><span class="sxs-lookup"><span data-stu-id="f6c33-153">If an element in the virtual machine resource definition points to another resource that is deployed in the same template, you need a dependency.</span></span> <span data-ttu-id="f6c33-154">For example, your example virtual machine defines a network profile:</span><span class="sxs-lookup"><span data-stu-id="f6c33-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="f6c33-155">To set this property, the network interface must exist.</span><span class="sxs-lookup"><span data-stu-id="f6c33-155">To set this property, the network interface must exist.</span></span> <span data-ttu-id="f6c33-156">Therefore, you need a dependency.</span><span class="sxs-lookup"><span data-stu-id="f6c33-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="f6c33-157">You also need to set a dependency when one resource (a child) is defined within another resource (a parent).</span><span class="sxs-lookup"><span data-stu-id="f6c33-157">You also need to set a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="f6c33-158">For example, the diagnostic settings and custom script extensions are both defined as child resources of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f6c33-158">For example, the diagnostic settings and custom script extensions are both defined as child resources of the virtual machine.</span></span> <span data-ttu-id="f6c33-159">They cannot be created until the virtual machine exists.</span><span class="sxs-lookup"><span data-stu-id="f6c33-159">They cannot be created until the virtual machine exists.</span></span> <span data-ttu-id="f6c33-160">Therefore, both resources are marked as dependent on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f6c33-160">Therefore, both resources are marked as dependent on the virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="f6c33-161">Profiles</span><span class="sxs-lookup"><span data-stu-id="f6c33-161">Profiles</span></span>

<span data-ttu-id="f6c33-162">Several profile elements are used when defining a virtual machine resource.</span><span class="sxs-lookup"><span data-stu-id="f6c33-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="f6c33-163">Some are required and some are optional.</span><span class="sxs-lookup"><span data-stu-id="f6c33-163">Some are required and some are optional.</span></span> <span data-ttu-id="f6c33-164">For example, the hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but the diagnosticsProfile is optional.</span><span class="sxs-lookup"><span data-stu-id="f6c33-164">For example, the hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but the diagnosticsProfile is optional.</span></span> <span data-ttu-id="f6c33-165">These profiles define settings such as:</span><span class="sxs-lookup"><span data-stu-id="f6c33-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="f6c33-166">size</span><span class="sxs-lookup"><span data-stu-id="f6c33-166">size</span></span>](sizes.md)
- <span data-ttu-id="f6c33-167">[name](/azure/architecture/best-practices/naming-conventions) and credentials</span><span class="sxs-lookup"><span data-stu-id="f6c33-167">[name](/azure/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="f6c33-168">disk and [operating system settings](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="f6c33-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="f6c33-169">network interface</span><span class="sxs-lookup"><span data-stu-id="f6c33-169">network interface</span></span>](../../virtual-network/virtual-network-deploy-multinic-classic-ps.md) 
- <span data-ttu-id="f6c33-170">boot diagnostics</span><span class="sxs-lookup"><span data-stu-id="f6c33-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="f6c33-171">Disks and images</span><span class="sxs-lookup"><span data-stu-id="f6c33-171">Disks and images</span></span>
   
<span data-ttu-id="f6c33-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6c33-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f6c33-173">When the operating system in a vhd file is specialized to be a specific VM, it is referred to as a disk.</span><span class="sxs-lookup"><span data-stu-id="f6c33-173">When the operating system in a vhd file is specialized to be a specific VM, it is referred to as a disk.</span></span> <span data-ttu-id="f6c33-174">When the operating system in a vhd file is generalized to be used to create many VMs, it is referred to as an image.</span><span class="sxs-lookup"><span data-stu-id="f6c33-174">When the operating system in a vhd file is generalized to be used to create many VMs, it is referred to as an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="f6c33-175">Create new virtual machines and new disks from a platform image</span><span class="sxs-lookup"><span data-stu-id="f6c33-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="f6c33-176">When you create a VM, you must decide what operating system to use.</span><span class="sxs-lookup"><span data-stu-id="f6c33-176">When you create a VM, you must decide what operating system to use.</span></span> <span data-ttu-id="f6c33-177">The imageReference element is used to define the operating system of a new VM.</span><span class="sxs-lookup"><span data-stu-id="f6c33-177">The imageReference element is used to define the operating system of a new VM.</span></span> <span data-ttu-id="f6c33-178">The example shows a definition for a Windows Server operating system:</span><span class="sxs-lookup"><span data-stu-id="f6c33-178">The example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="f6c33-179">If you want to create a Linux operating system, you might use this definition:</span><span class="sxs-lookup"><span data-stu-id="f6c33-179">If you want to create a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="f6c33-180">Configuration settings for the operating system disk are assigned with the osDisk element.</span><span class="sxs-lookup"><span data-stu-id="f6c33-180">Configuration settings for the operating system disk are assigned with the osDisk element.</span></span> <span data-ttu-id="f6c33-181">The example defines a new managed disk with the caching mode set to **ReadWrite** and that the disk is being created from a [platform image](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="f6c33-181">The example defines a new managed disk with the caching mode set to **ReadWrite** and that the disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="f6c33-182">Create new virtual machines from existing managed disks</span><span class="sxs-lookup"><span data-stu-id="f6c33-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="f6c33-183">If you want to create virtual machines from existing disks, remove the imageReference and the osProfile elements and define these disk settings:</span><span class="sxs-lookup"><span data-stu-id="f6c33-183">If you want to create virtual machines from existing disks, remove the imageReference and the osProfile elements and define these disk settings:</span></span>

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="f6c33-184">Create new virtual machines from a managed image</span><span class="sxs-lookup"><span data-stu-id="f6c33-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="f6c33-185">If you want to create a virtual machine from a managed image, change the imageReference element and define these disk settings:</span><span class="sxs-lookup"><span data-stu-id="f6c33-185">If you want to create a virtual machine from a managed image, change the imageReference element and define these disk settings:</span></span>

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a><span data-ttu-id="f6c33-186">Attach data disks</span><span class="sxs-lookup"><span data-stu-id="f6c33-186">Attach data disks</span></span>

<span data-ttu-id="f6c33-187">You can optionally add data disks to the VMs.</span><span class="sxs-lookup"><span data-stu-id="f6c33-187">You can optionally add data disks to the VMs.</span></span> <span data-ttu-id="f6c33-188">The [number of disks](sizes.md) depends on the size of operating system disk that you use.</span><span class="sxs-lookup"><span data-stu-id="f6c33-188">The [number of disks](sizes.md) depends on the size of operating system disk that you use.</span></span> <span data-ttu-id="f6c33-189">With the size of the VMs set to Standard_DS1_v2, the maximum number of data disks that could be added to the them is two.</span><span class="sxs-lookup"><span data-stu-id="f6c33-189">With the size of the VMs set to Standard_DS1_v2, the maximum number of data disks that could be added to the them is two.</span></span> <span data-ttu-id="f6c33-190">In the example, one managed data disk is being added to each VM:</span><span class="sxs-lookup"><span data-stu-id="f6c33-190">In the example, one managed data disk is being added to each VM:</span></span>

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a><span data-ttu-id="f6c33-191">Extensions</span><span class="sxs-lookup"><span data-stu-id="f6c33-191">Extensions</span></span>

<span data-ttu-id="f6c33-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied to VMs.</span><span class="sxs-lookup"><span data-stu-id="f6c33-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied to VMs.</span></span> <span data-ttu-id="f6c33-193">Extensions can be added as a child resource of the VM or as a separate resource.</span><span class="sxs-lookup"><span data-stu-id="f6c33-193">Extensions can be added as a child resource of the VM or as a separate resource.</span></span> <span data-ttu-id="f6c33-194">The example shows the [Diagnostics Extension](extensions-diagnostics-template.md) being added to the VMs:</span><span class="sxs-lookup"><span data-stu-id="f6c33-194">The example shows the [Diagnostics Extension](extensions-diagnostics-template.md) being added to the VMs:</span></span>

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

<span data-ttu-id="f6c33-195">This extension resource uses the storageName variable and the diagnostic variables to provide values.</span><span class="sxs-lookup"><span data-stu-id="f6c33-195">This extension resource uses the storageName variable and the diagnostic variables to provide values.</span></span> <span data-ttu-id="f6c33-196">If you want to change the data that is collected by this extension, you can add more performance counters to the wadperfcounters variable.</span><span class="sxs-lookup"><span data-stu-id="f6c33-196">If you want to change the data that is collected by this extension, you can add more performance counters to the wadperfcounters variable.</span></span> <span data-ttu-id="f6c33-197">You could also choose to put the diagnostics data into a different storage account than where the VM disks are stored.</span><span class="sxs-lookup"><span data-stu-id="f6c33-197">You could also choose to put the diagnostics data into a different storage account than where the VM disks are stored.</span></span>

<span data-ttu-id="f6c33-198">There are many extensions that you can install on a VM, but the most useful is probably the [Custom Script Extension](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="f6c33-198">There are many extensions that you can install on a VM, but the most useful is probably the [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="f6c33-199">In the example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span><span class="sxs-lookup"><span data-stu-id="f6c33-199">In the example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

<span data-ttu-id="f6c33-200">The start.ps1 script can accomplish many configuration tasks.</span><span class="sxs-lookup"><span data-stu-id="f6c33-200">The start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="f6c33-201">For example, the data disks that are added to the VMs in the example are not initialized; you can use a custom script to initialize them.</span><span class="sxs-lookup"><span data-stu-id="f6c33-201">For example, the data disks that are added to the VMs in the example are not initialized; you can use a custom script to initialize them.</span></span> <span data-ttu-id="f6c33-202">If you have multiple startup tasks to do, you can use the start.ps1 file to call other PowerShell scripts in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="f6c33-202">If you have multiple startup tasks to do, you can use the start.ps1 file to call other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="f6c33-203">The example uses PowerShell, but you can use any scripting method that is available on the operating system that you are using.</span><span class="sxs-lookup"><span data-stu-id="f6c33-203">The example uses PowerShell, but you can use any scripting method that is available on the operating system that you are using.</span></span>

<span data-ttu-id="f6c33-204">You can see the status of the installed extensions from the Extensions settings in the portal:</span><span class="sxs-lookup"><span data-stu-id="f6c33-204">You can see the status of the installed extensions from the Extensions settings in the portal:</span></span>

![Get extension status](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="f6c33-206">You can also get extension information by using the **Get-AzureRmVMExtension** PowerShell command, the **vm extension get** Azure CLI 2.0 command, or the **Get extension information** REST API.</span><span class="sxs-lookup"><span data-stu-id="f6c33-206">You can also get extension information by using the **Get-AzureRmVMExtension** PowerShell command, the **vm extension get** Azure CLI 2.0 command, or the **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="f6c33-207">Deployments</span><span class="sxs-lookup"><span data-stu-id="f6c33-207">Deployments</span></span>

<span data-ttu-id="f6c33-208">When you deploy a template, Azure tracks the resources that you deployed as a group and automatically assigns a name to this deployed group.</span><span class="sxs-lookup"><span data-stu-id="f6c33-208">When you deploy a template, Azure tracks the resources that you deployed as a group and automatically assigns a name to this deployed group.</span></span> <span data-ttu-id="f6c33-209">The name of the deployment is the same as the name of the template.</span><span class="sxs-lookup"><span data-stu-id="f6c33-209">The name of the deployment is the same as the name of the template.</span></span>

<span data-ttu-id="f6c33-210">If you are curious about the status of resources in the deployment, you can use the Resource Group blade in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="f6c33-210">If you are curious about the status of resources in the deployment, you can use the Resource Group blade in the Azure portal:</span></span>

![Get deployment information](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="f6c33-212">It’s not a problem to use the same template to create resources or to update existing resources.</span><span class="sxs-lookup"><span data-stu-id="f6c33-212">It’s not a problem to use the same template to create resources or to update existing resources.</span></span> <span data-ttu-id="f6c33-213">When you use commands to deploy templates, you have the opportunity to say which [mode](../../resource-group-template-deploy.md) you want to use.</span><span class="sxs-lookup"><span data-stu-id="f6c33-213">When you use commands to deploy templates, you have the opportunity to say which [mode](../../resource-group-template-deploy.md) you want to use.</span></span> <span data-ttu-id="f6c33-214">The mode can be set to either **Complete** or **Incremental**.</span><span class="sxs-lookup"><span data-stu-id="f6c33-214">The mode can be set to either **Complete** or **Incremental**.</span></span> <span data-ttu-id="f6c33-215">The default is to do incremental updates.</span><span class="sxs-lookup"><span data-stu-id="f6c33-215">The default is to do incremental updates.</span></span> <span data-ttu-id="f6c33-216">Be careful when using the **Complete** mode because you may accidentally delete resources.</span><span class="sxs-lookup"><span data-stu-id="f6c33-216">Be careful when using the **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="f6c33-217">When you set the mode to **Complete**, Resource Manager deletes any resources in the resource group that are not in the template.</span><span class="sxs-lookup"><span data-stu-id="f6c33-217">When you set the mode to **Complete**, Resource Manager deletes any resources in the resource group that are not in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6c33-218">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f6c33-218">Next Steps</span></span>

- <span data-ttu-id="f6c33-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f6c33-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="f6c33-220">Deploy the template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="f6c33-220">Deploy the template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="f6c33-221">Learn how to manage the VMs that you created by reviewing [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6c33-221">Learn how to manage the VMs that you created by reviewing [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
