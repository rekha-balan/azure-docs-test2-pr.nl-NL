---
title: Deploying Windows Compute Resources with Azure Resource Manager Templates | Microsoft Docs
description: Azure Virtual Machine DotNet Core Tutorial
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60cb257d1918a5960648bdbed5a6766415808daf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563369"
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="0cace-103">Application architecture with Azure Resource Manager templates for Windows VMs</span><span class="sxs-lookup"><span data-stu-id="0cace-103">Application architecture with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="0cace-104">When developing an Azure Resource Manager deployment, compute requirements need to be mapped to Azure resources and services.</span><span class="sxs-lookup"><span data-stu-id="0cace-104">When developing an Azure Resource Manager deployment, compute requirements need to be mapped to Azure resources and services.</span></span> <span data-ttu-id="0cace-105">If an application consists of several http endpoints, a database, and a data caching service, the Azure resources that host each of these components needs to be rationalized.</span><span class="sxs-lookup"><span data-stu-id="0cace-105">If an application consists of several http endpoints, a database, and a data caching service, the Azure resources that host each of these components needs to be rationalized.</span></span> <span data-ttu-id="0cace-106">For instance, the sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0cace-106">For instance, the sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="0cace-107">This document details how the Music Store compute resources are configured in the sample Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="0cace-107">This document details how the Music Store compute resources are configured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="0cace-108">All dependencies and unique configurations are highlighted.</span><span class="sxs-lookup"><span data-stu-id="0cace-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="0cace-109">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="0cace-109">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="0cace-110">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="0cace-110">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="0cace-111">Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="0cace-111">Virtual Machine</span></span>
<span data-ttu-id="0cace-112">The Music Store application includes a web application where customers can browse and purchase music.</span><span class="sxs-lookup"><span data-stu-id="0cace-112">The Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="0cace-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span><span class="sxs-lookup"><span data-stu-id="0cace-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="0cace-114">Using the sample Music Store template, a virtual machine is deployed, a web server install, and the Music Store website installed and configured.</span><span class="sxs-lookup"><span data-stu-id="0cace-114">Using the sample Music Store template, a virtual machine is deployed, a web server install, and the Music Store website installed and configured.</span></span> <span data-ttu-id="0cace-115">For the sake of this article, only the virtual machine deployment is detailed.</span><span class="sxs-lookup"><span data-stu-id="0cace-115">For the sake of this article, only the virtual machine deployment is detailed.</span></span> <span data-ttu-id="0cace-116">The configuration of the web server and the application is detailed in a later article.</span><span class="sxs-lookup"><span data-stu-id="0cace-116">The configuration of the web server and the application is detailed in a later article.</span></span>

<span data-ttu-id="0cace-117">A virtual machine can be added to a template using the Visual Studio Add New Resource wizard, or by inserting valid JSON into the deployment template.</span><span class="sxs-lookup"><span data-stu-id="0cace-117">A virtual machine can be added to a template using the Visual Studio Add New Resource wizard, or by inserting valid JSON into the deployment template.</span></span> <span data-ttu-id="0cace-118">When deploying a virtual machine, several related resources are also needed.</span><span class="sxs-lookup"><span data-stu-id="0cace-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="0cace-119">If using Visual Studio to create the template, these resources are created for you.</span><span class="sxs-lookup"><span data-stu-id="0cace-119">If using Visual Studio to create the template, these resources are created for you.</span></span> <span data-ttu-id="0cace-120">If manually constructing the template, these resources need to be inserted and configured.</span><span class="sxs-lookup"><span data-stu-id="0cace-120">If manually constructing the template, these resources need to be inserted and configured.</span></span>

<span data-ttu-id="0cace-121">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span><span class="sxs-lookup"><span data-stu-id="0cace-121">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span></span>

```json
{
  {
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
  ........<truncated>  
}
```

<span data-ttu-id="0cace-122">Once deployed, the virtual machine properties can be seen in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0cace-122">Once deployed, the virtual machine properties can be seen in the Azure portal.</span></span>

![Virtual Machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a><span data-ttu-id="0cace-124">Storage Account</span><span class="sxs-lookup"><span data-stu-id="0cace-124">Storage Account</span></span>
<span data-ttu-id="0cace-125">Storage accounts have many storage options and capabilities.</span><span class="sxs-lookup"><span data-stu-id="0cace-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="0cace-126">For the context of Azure Virtual machines, a storage account holds the virtual hard drives of the virtual machine and any additional data disks.</span><span class="sxs-lookup"><span data-stu-id="0cace-126">For the context of Azure Virtual machines, a storage account holds the virtual hard drives of the virtual machine and any additional data disks.</span></span> <span data-ttu-id="0cace-127">The Music Store sample includes one storage account to hold the virtual hard drive of each virtual machine in the deployment.</span><span class="sxs-lookup"><span data-stu-id="0cace-127">The Music Store sample includes one storage account to hold the virtual hard drive of each virtual machine in the deployment.</span></span> 

<span data-ttu-id="0cace-128">Follow this link to see the JSON sample within the Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span><span class="sxs-lookup"><span data-stu-id="0cace-128">Follow this link to see the JSON sample within the Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

<span data-ttu-id="0cace-129">A storage account is associate with a virtual machine inside the Resource Manager template declaration of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0cace-129">A storage account is associate with a virtual machine inside the Resource Manager template declaration of the virtual machine.</span></span> 

<span data-ttu-id="0cace-130">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span><span class="sxs-lookup"><span data-stu-id="0cace-130">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span></span>

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

<span data-ttu-id="0cace-131">After deployment, the storage account can be viewed in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0cace-131">After deployment, the storage account can be viewed in the Azure portal.</span></span>

![Storage Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-2-architecture/storacct-win.png)

<span data-ttu-id="0cace-133">Clicking into the storage account blob container, the virtual hard drive file for each virtual machine deployed with the template can be seen.</span><span class="sxs-lookup"><span data-stu-id="0cace-133">Clicking into the storage account blob container, the virtual hard drive file for each virtual machine deployed with the template can be seen.</span></span>

![Virtual Hard Drives](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-2-architecture/vhd-win.png)

<span data-ttu-id="0cace-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="0cace-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="0cace-136">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="0cace-136">Virtual Network</span></span>
<span data-ttu-id="0cace-137">If a virtual machine requires internal networking such as the ability to communicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span><span class="sxs-lookup"><span data-stu-id="0cace-137">If a virtual machine requires internal networking such as the ability to communicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="0cace-138">A virtual network does not make the virtual machine accessible over the internet.</span><span class="sxs-lookup"><span data-stu-id="0cace-138">A virtual network does not make the virtual machine accessible over the internet.</span></span> <span data-ttu-id="0cace-139">Public connectivity requires a public IP address, which is detailed later in this series.</span><span class="sxs-lookup"><span data-stu-id="0cace-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="0cace-140">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span><span class="sxs-lookup"><span data-stu-id="0cace-140">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
    "subnets": [
      {
        "name": "[variables('subnetName')]",
        "properties": {
          "addressPrefix": "10.0.0.0/24",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
          }
        }
      }
    ]
  }
}
```

<span data-ttu-id="0cace-141">From the Azure portal, the virtual network looks like the following image.</span><span class="sxs-lookup"><span data-stu-id="0cace-141">From the Azure portal, the virtual network looks like the following image.</span></span> <span data-ttu-id="0cace-142">Notice that all virtual machines deployed with the template are attached to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="0cace-142">Notice that all virtual machines deployed with the template are attached to the virtual network.</span></span>

![Virtual Network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a><span data-ttu-id="0cace-144">Network Interface</span><span class="sxs-lookup"><span data-stu-id="0cace-144">Network Interface</span></span>
 <span data-ttu-id="0cace-145">A network interface connects a virtual machine to a virtual network, more specifically to a subnet that has been defined in the virtual network.</span><span class="sxs-lookup"><span data-stu-id="0cace-145">A network interface connects a virtual machine to a virtual network, more specifically to a subnet that has been defined in the virtual network.</span></span> 

 <span data-ttu-id="0cace-146">Follow this link to see the JSON sample within the Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span><span class="sxs-lookup"><span data-stu-id="0cace-146">Follow this link to see the JSON sample within the Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="0cace-147">Each virtual machine resource includes a network profile.</span><span class="sxs-lookup"><span data-stu-id="0cace-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="0cace-148">The network interface is associated with the virtual machine in this profile.</span><span class="sxs-lookup"><span data-stu-id="0cace-148">The network interface is associated with the virtual machine in this profile.</span></span>  

<span data-ttu-id="0cace-149">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span><span class="sxs-lookup"><span data-stu-id="0cace-149">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="0cace-150">From the Azure portal, the network interface looks like the following image.</span><span class="sxs-lookup"><span data-stu-id="0cace-150">From the Azure portal, the network interface looks like the following image.</span></span> <span data-ttu-id="0cace-151">The internal IP address and the virtual machine association can be seen on the network interface resource.</span><span class="sxs-lookup"><span data-stu-id="0cace-151">The internal IP address and the virtual machine association can be seen on the network interface resource.</span></span>

![Network Interface](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-2-architecture/nic-win.png)

<span data-ttu-id="0cace-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="0cace-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="0cace-154">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0cace-154">Azure SQL Database</span></span>
<span data-ttu-id="0cace-155">In addition to a virtual machine hosting the Music Store website, an Azure SQL Database is deployed to host the Music Store database.</span><span class="sxs-lookup"><span data-stu-id="0cace-155">In addition to a virtual machine hosting the Music Store website, an Azure SQL Database is deployed to host the Music Store database.</span></span> <span data-ttu-id="0cace-156">The advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into the service.</span><span class="sxs-lookup"><span data-stu-id="0cace-156">The advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into the service.</span></span>

<span data-ttu-id="0cace-157">An Azure SQL database can be added using the Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span><span class="sxs-lookup"><span data-stu-id="0cace-157">An Azure SQL database can be added using the Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="0cace-158">The SQL Server resource includes a user name and password that is granted administrative rights on the SQL instance.</span><span class="sxs-lookup"><span data-stu-id="0cace-158">The SQL Server resource includes a user name and password that is granted administrative rights on the SQL instance.</span></span> <span data-ttu-id="0cace-159">Also, a SQL firewall resource is added.</span><span class="sxs-lookup"><span data-stu-id="0cace-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="0cace-160">By default, applications hosted in Azure are able to connect with the SQL instance.</span><span class="sxs-lookup"><span data-stu-id="0cace-160">By default, applications hosted in Azure are able to connect with the SQL instance.</span></span> <span data-ttu-id="0cace-161">To allow external application such a SQL Server Management studio to connect to the SQL instance, the firewall needs to be configured.</span><span class="sxs-lookup"><span data-stu-id="0cace-161">To allow external application such a SQL Server Management studio to connect to the SQL instance, the firewall needs to be configured.</span></span> <span data-ttu-id="0cace-162">For the sake of the Music Store demo, the default configuration is fine.</span><span class="sxs-lookup"><span data-stu-id="0cace-162">For the sake of the Music Store demo, the default configuration is fine.</span></span> 

<span data-ttu-id="0cace-163">Follow this link to see the JSON sample within the Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span><span class="sxs-lookup"><span data-stu-id="0cace-163">Follow this link to see the JSON sample within the Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="0cace-164">A view of the SQL server and MusicStore database as seen in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0cace-164">A view of the SQL server and MusicStore database as seen in the Azure portal.</span></span>

![SQL Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-2-architecture/sql-win.png)

<span data-ttu-id="0cace-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="0cace-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="0cace-167">Next step</span><span class="sxs-lookup"><span data-stu-id="0cace-167">Next step</span></span>
<hr>

[<span data-ttu-id="0cace-168">Step 2 - Access and Security in Azure Resource Manager Templates</span><span class="sxs-lookup"><span data-stu-id="0cace-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)







