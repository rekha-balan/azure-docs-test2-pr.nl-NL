---
title: Access and security in Azure templates for Windows VMs | Microsoft Docs
description: Azure Virtual Machine DotNet Core Tutorial
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d49ed334dfe7750a682793a737d2e3f0d4e2f36
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661446"
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="1d418-103">Access and security in Azure Resource Manager templates for Windows VMs</span><span class="sxs-lookup"><span data-stu-id="1d418-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="1d418-104">Applications hosted in Azure likely need to be access over the internet or a VPN / Express Route connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="1d418-104">Applications hosted in Azure likely need to be access over the internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="1d418-105">With the Music Store application sample, the web site is made available on the internet with a public IP address.</span><span class="sxs-lookup"><span data-stu-id="1d418-105">With the Music Store application sample, the web site is made available on the internet with a public IP address.</span></span> <span data-ttu-id="1d418-106">With access established, connections to the application and access to the virtual machine resources themselves should be secured.</span><span class="sxs-lookup"><span data-stu-id="1d418-106">With access established, connections to the application and access to the virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="1d418-107">This access security is provided with a Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="1d418-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="1d418-108">This document details how the Music Store application is secured in the sample Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="1d418-108">This document details how the Music Store application is secured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="1d418-109">All dependencies and unique configurations are highlighted.</span><span class="sxs-lookup"><span data-stu-id="1d418-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="1d418-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="1d418-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="1d418-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="1d418-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="1d418-112">Public IP Address</span><span class="sxs-lookup"><span data-stu-id="1d418-112">Public IP Address</span></span>
<span data-ttu-id="1d418-113">To provide public access to an Azure resource, a public IP address resource can be used.</span><span class="sxs-lookup"><span data-stu-id="1d418-113">To provide public access to an Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="1d418-114">Public IP address can be configured with a static or dynamic IP address.</span><span class="sxs-lookup"><span data-stu-id="1d418-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="1d418-115">If a dynamic address is used, and the virtual machine is stopped and deallocated, the addresses is removed.</span><span class="sxs-lookup"><span data-stu-id="1d418-115">If a dynamic address is used, and the virtual machine is stopped and deallocated, the addresses is removed.</span></span> <span data-ttu-id="1d418-116">When the machine is started again, it may be assigned a different public IP address.</span><span class="sxs-lookup"><span data-stu-id="1d418-116">When the machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="1d418-117">To prevent an IP address from changing, a reserved IP address can be used.</span><span class="sxs-lookup"><span data-stu-id="1d418-117">To prevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="1d418-118">A Public IP Address can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span><span class="sxs-lookup"><span data-stu-id="1d418-118">A Public IP Address can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="1d418-119">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span><span class="sxs-lookup"><span data-stu-id="1d418-119">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="1d418-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="1d418-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="1d418-121">In this example, because the Music Store website is load balanced across several virtual machines, the Public IP Address is attached to the Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="1d418-121">In this example, because the Music Store website is load balanced across several virtual machines, the Public IP Address is attached to the Load Balancer.</span></span>

<span data-ttu-id="1d418-122">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="1d418-122">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="1d418-123">The public IP Address as seen from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1d418-123">The public IP Address as seen from the Azure portal.</span></span> <span data-ttu-id="1d418-124">Notice that the public IP address is associated to a load balancer and not a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d418-124">Notice that the public IP address is associated to a load balancer and not a virtual machine.</span></span> <span data-ttu-id="1d418-125">Network load balancers are detailed in the next document of this series.</span><span class="sxs-lookup"><span data-stu-id="1d418-125">Network load balancers are detailed in the next document of this series.</span></span>

![Public IP Address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="1d418-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1d418-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="1d418-128">Network Security Group</span><span class="sxs-lookup"><span data-stu-id="1d418-128">Network Security Group</span></span>
<span data-ttu-id="1d418-129">Once access has been established to Azure resources, this access should be limited.</span><span class="sxs-lookup"><span data-stu-id="1d418-129">Once access has been established to Azure resources, this access should be limited.</span></span> <span data-ttu-id="1d418-130">For Azure virtual machines, secure access is accomplished using a network security group.</span><span class="sxs-lookup"><span data-stu-id="1d418-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="1d418-131">With the Music Store application sample, all access to the virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span><span class="sxs-lookup"><span data-stu-id="1d418-131">With the Music Store application sample, all access to the virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="1d418-132">A Network Security Group can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span><span class="sxs-lookup"><span data-stu-id="1d418-132">A Network Security Group can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="1d418-133">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span><span class="sxs-lookup"><span data-stu-id="1d418-133">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

<span data-ttu-id="1d418-134">In this example, the network security group is associate with the subnet object declared in the Virtual Network resource.</span><span class="sxs-lookup"><span data-stu-id="1d418-134">In this example, the network security group is associate with the subnet object declared in the Virtual Network resource.</span></span> 

<span data-ttu-id="1d418-135">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span><span class="sxs-lookup"><span data-stu-id="1d418-135">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

```json
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
```

<span data-ttu-id="1d418-136">Here is what the network security group looks like from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1d418-136">Here is what the network security group looks like from the Azure portal.</span></span> <span data-ttu-id="1d418-137">Notice that an NSG can be associate with a subnet and / or network interface.</span><span class="sxs-lookup"><span data-stu-id="1d418-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="1d418-138">In this case, the NSG is associated to a subnet.</span><span class="sxs-lookup"><span data-stu-id="1d418-138">In this case, the NSG is associated to a subnet.</span></span> <span data-ttu-id="1d418-139">In this configuration, the inbound rules apply to all virtual machines connected to the subnet.</span><span class="sxs-lookup"><span data-stu-id="1d418-139">In this configuration, the inbound rules apply to all virtual machines connected to the subnet.</span></span>

![Network Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="1d418-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="1d418-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="1d418-142">Next step</span><span class="sxs-lookup"><span data-stu-id="1d418-142">Next step</span></span>
<hr>

[<span data-ttu-id="1d418-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span><span class="sxs-lookup"><span data-stu-id="1d418-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)



