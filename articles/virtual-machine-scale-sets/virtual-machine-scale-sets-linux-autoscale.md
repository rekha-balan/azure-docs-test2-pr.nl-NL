---
title: Autoscale Linux Virtual Machine Scale Sets | Microsoft Docs
description: Set up autoscaling for a Linux Virtual Machine Scale Set using Azure CLI
services: virtual-machine-scale-sets
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 7d67ae1bd0c53f99d9c298f5ae8f161e6a484359
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556654"
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="34912-103">Automatically scale Linux machines in a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="34912-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="34912-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span><span class="sxs-lookup"><span data-stu-id="34912-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="34912-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span><span class="sxs-lookup"><span data-stu-id="34912-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="34912-106">To learn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34912-106">To learn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="34912-107">This tutorial shows you how to create a scale set of Linux virtual machines using the latest version of Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="34912-107">This tutorial shows you how to create a scale set of Linux virtual machines using the latest version of Ubuntu Linux.</span></span> <span data-ttu-id="34912-108">The tutorial also shows you how to automatically scale the machines in the set.</span><span class="sxs-lookup"><span data-stu-id="34912-108">The tutorial also shows you how to automatically scale the machines in the set.</span></span> <span data-ttu-id="34912-109">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="34912-109">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="34912-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="34912-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="34912-111">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34912-111">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="34912-112">In this tutorial, you deploy the following resources and extensions:</span><span class="sxs-lookup"><span data-stu-id="34912-112">In this tutorial, you deploy the following resources and extensions:</span></span>

* <span data-ttu-id="34912-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="34912-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="34912-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="34912-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="34912-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="34912-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="34912-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="34912-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="34912-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="34912-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="34912-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="34912-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="34912-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="34912-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="34912-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="34912-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="34912-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="34912-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="34912-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="34912-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="34912-123">Before you get started with the steps in this tutorial, [install the Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="34912-123">Before you get started with the steps in this tutorial, [install the Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="34912-124">Step 1: Create a resource group and a storage account</span><span class="sxs-lookup"><span data-stu-id="34912-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="34912-125">**Sign in to Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="34912-125">**Sign in to Microsoft Azure**</span></span>  
<span data-ttu-id="34912-126">In your command-line interface (Bash, Terminal, Command prompt), switch to Resource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow the prompts for an interactive login experience to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="34912-126">In your command-line interface (Bash, Terminal, Command prompt), switch to Resource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow the prompts for an interactive login experience to your Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="34912-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with the ID to log in without an interactive session.</span><span class="sxs-lookup"><span data-stu-id="34912-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with the ID to log in without an interactive session.</span></span> <span data-ttu-id="34912-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../virtual-machines/linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="34912-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../virtual-machines/linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    
2. <span data-ttu-id="34912-129">**Create a resource group**</span><span class="sxs-lookup"><span data-stu-id="34912-129">**Create a resource group**</span></span>  
<span data-ttu-id="34912-130">All resources must be deployed to a resource group.</span><span class="sxs-lookup"><span data-stu-id="34912-130">All resources must be deployed to a resource group.</span></span> <span data-ttu-id="34912-131">For this tutorial, name the resource group **vmsstest1**.</span><span class="sxs-lookup"><span data-stu-id="34912-131">For this tutorial, name the resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="34912-132">**Deploy a storage account into the new resource group**</span><span class="sxs-lookup"><span data-stu-id="34912-132">**Deploy a storage account into the new resource group**</span></span>  
<span data-ttu-id="34912-133">This storage account is where the template is stored.</span><span class="sxs-lookup"><span data-stu-id="34912-133">This storage account is where the template is stored.</span></span> <span data-ttu-id="34912-134">Create a storage account named **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="34912-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-the-template"></a><span data-ttu-id="34912-135">Step 2: Create the template</span><span class="sxs-lookup"><span data-stu-id="34912-135">Step 2: Create the template</span></span>
<span data-ttu-id="34912-136">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span><span class="sxs-lookup"><span data-stu-id="34912-136">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="34912-137">In your favorite editor, create the file VMSSTemplate.json and add the initial JSON structure to support the template.</span><span class="sxs-lookup"><span data-stu-id="34912-137">In your favorite editor, create the file VMSSTemplate.json and add the initial JSON structure to support the template.</span></span>

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. <span data-ttu-id="34912-138">Parameters are not always required, but they provide a way to input values when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="34912-138">Parameters are not always required, but they provide a way to input values when the template is deployed.</span></span> <span data-ttu-id="34912-139">Add these parameters under the parameters parent element that you added to the template.</span><span class="sxs-lookup"><span data-stu-id="34912-139">Add these parameters under the parameters parent element that you added to the template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="34912-140">A name for the separate virtual machine that is used to access the machines in the scale set.</span><span class="sxs-lookup"><span data-stu-id="34912-140">A name for the separate virtual machine that is used to access the machines in the scale set.</span></span>
   * <span data-ttu-id="34912-141">A name for the storage account where the template is stored.</span><span class="sxs-lookup"><span data-stu-id="34912-141">A name for the storage account where the template is stored.</span></span>
   * <span data-ttu-id="34912-142">The number of instances of virtual machines to initially create in the scale set.</span><span class="sxs-lookup"><span data-stu-id="34912-142">The number of instances of virtual machines to initially create in the scale set.</span></span>
   * <span data-ttu-id="34912-143">A name and password of the administrator account on the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="34912-143">A name and password of the administrator account on the virtual machines.</span></span>
   * <span data-ttu-id="34912-144">A name prefix for the resources that are created to support the scale set.</span><span class="sxs-lookup"><span data-stu-id="34912-144">A name prefix for the resources that are created to support the scale set.</span></span>

3. <span data-ttu-id="34912-145">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span><span class="sxs-lookup"><span data-stu-id="34912-145">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span></span> <span data-ttu-id="34912-146">Add these variables under the variables parent element that you added to the template.</span><span class="sxs-lookup"><span data-stu-id="34912-146">Add these variables under the variables parent element that you added to the template.</span></span>

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * <span data-ttu-id="34912-147">DNS names that are used by the network interfaces.</span><span class="sxs-lookup"><span data-stu-id="34912-147">DNS names that are used by the network interfaces.</span></span>
   * <span data-ttu-id="34912-148">The IP address names and prefixes for the virtual network and subnets.</span><span class="sxs-lookup"><span data-stu-id="34912-148">The IP address names and prefixes for the virtual network and subnets.</span></span>
   * <span data-ttu-id="34912-149">The names and identifiers of the virtual network, load balancer, and network interfaces.</span><span class="sxs-lookup"><span data-stu-id="34912-149">The names and identifiers of the virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="34912-150">Storage account names for the accounts associated with the machines in the scale set.</span><span class="sxs-lookup"><span data-stu-id="34912-150">Storage account names for the accounts associated with the machines in the scale set.</span></span>
   * <span data-ttu-id="34912-151">Settings for the Diagnostics extension that is installed on the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="34912-151">Settings for the Diagnostics extension that is installed on the virtual machines.</span></span> <span data-ttu-id="34912-152">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="34912-152">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="34912-153">Add the storage account resource under the resources parent element that you added to the template.</span><span class="sxs-lookup"><span data-stu-id="34912-153">Add the storage account resource under the resources parent element that you added to the template.</span></span> <span data-ttu-id="34912-154">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span><span class="sxs-lookup"><span data-stu-id="34912-154">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="34912-155">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span><span class="sxs-lookup"><span data-stu-id="34912-155">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span></span> <span data-ttu-id="34912-156">Each storage account is named with a letter designator that was defined in the variables combined with the suffix that you provide in the parameters for the template.</span><span class="sxs-lookup"><span data-stu-id="34912-156">Each storage account is named with a letter designator that was defined in the variables combined with the suffix that you provide in the parameters for the template.</span></span>
   
        {
          "type": "Microsoft.Storage/storageAccounts",
          "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
          "apiVersion": "2015-06-15",
          "copy": {
            "name": "storageLoop",
            "count": 5
          },
          "location": "[resourceGroup().location]",
          "properties": { "accountType": "Standard_LRS" }
        },

5. <span data-ttu-id="34912-157">Add the virtual network resource.</span><span class="sxs-lookup"><span data-stu-id="34912-157">Add the virtual network resource.</span></span> <span data-ttu-id="34912-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="34912-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. <span data-ttu-id="34912-159">Add the public IP address resources that are used by the load balancer and network interface.</span><span class="sxs-lookup"><span data-stu-id="34912-159">Add the public IP address resources that are used by the load balancer and network interface.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. <span data-ttu-id="34912-160">Add the load balancer resource that is used by the scale set.</span><span class="sxs-lookup"><span data-stu-id="34912-160">Add the load balancer resource that is used by the scale set.</span></span> <span data-ttu-id="34912-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="34912-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="34912-162">Add the network interface resource that is used by the separate virtual machine.</span><span class="sxs-lookup"><span data-stu-id="34912-162">Add the network interface resource that is used by the separate virtual machine.</span></span> <span data-ttu-id="34912-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span><span class="sxs-lookup"><span data-stu-id="34912-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. <span data-ttu-id="34912-164">Add the separate virtual machine in the same network as the scale set.</span><span class="sxs-lookup"><span data-stu-id="34912-164">Add the separate virtual machine in the same network as the scale set.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. <span data-ttu-id="34912-165">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span><span class="sxs-lookup"><span data-stu-id="34912-165">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span></span> <span data-ttu-id="34912-166">Many of the settings for this resource are similar with the virtual machine resource.</span><span class="sxs-lookup"><span data-stu-id="34912-166">Many of the settings for this resource are similar with the virtual machine resource.</span></span> <span data-ttu-id="34912-167">The main differences are the capacity element that specifies the number of virtual machines in the scale set and upgradePolicy that specifies how updates are made to virtual machines.</span><span class="sxs-lookup"><span data-stu-id="34912-167">The main differences are the capacity element that specifies the number of virtual machines in the scale set and upgradePolicy that specifies how updates are made to virtual machines.</span></span> <span data-ttu-id="34912-168">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span><span class="sxs-lookup"><span data-stu-id="34912-168">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span></span>

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="34912-169">Add the autoscaleSettings resource that defines how the scale set adjusts based on processor usage on the machines in the set.</span><span class="sxs-lookup"><span data-stu-id="34912-169">Add the autoscaleSettings resource that defines how the scale set adjusts based on processor usage on the machines in the set.</span></span>

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor\\PercentProcessorTime",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```
    
    <span data-ttu-id="34912-170">For this tutorial, these values are important:</span><span class="sxs-lookup"><span data-stu-id="34912-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="34912-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="34912-171">**metricName**</span></span>  
    <span data-ttu-id="34912-172">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span><span class="sxs-lookup"><span data-stu-id="34912-172">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span></span> <span data-ttu-id="34912-173">Using that variable, the Diagnostics extension collects the **Processor\PercentProcessorTime** counter.</span><span class="sxs-lookup"><span data-stu-id="34912-173">Using that variable, the Diagnostics extension collects the **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="34912-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="34912-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="34912-175">This value is the resource identifier of the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="34912-175">This value is the resource identifier of the virtual machine scale set.</span></span>
    
    * <span data-ttu-id="34912-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="34912-176">**timeGrain**</span></span>  
    <span data-ttu-id="34912-177">This value is the granularity of the metrics that are collected.</span><span class="sxs-lookup"><span data-stu-id="34912-177">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="34912-178">In this template, it is set to one minute.</span><span class="sxs-lookup"><span data-stu-id="34912-178">In this template, it is set to one minute.</span></span>
    
    * <span data-ttu-id="34912-179">**statistic**</span><span class="sxs-lookup"><span data-stu-id="34912-179">**statistic**</span></span>  
    <span data-ttu-id="34912-180">This value determines how the metrics are combined to accommodate the automatic scaling action.</span><span class="sxs-lookup"><span data-stu-id="34912-180">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="34912-181">The possible values are: Average, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="34912-181">The possible values are: Average, Min, Max.</span></span> <span data-ttu-id="34912-182">In this template, the average total CPU usage of the virtual machines is collected.</span><span class="sxs-lookup"><span data-stu-id="34912-182">In this template, the average total CPU usage of the virtual machines is collected.</span></span>

    * <span data-ttu-id="34912-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="34912-183">**timeWindow**</span></span>  
    <span data-ttu-id="34912-184">This value is the range of time in which instance data is collected.</span><span class="sxs-lookup"><span data-stu-id="34912-184">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="34912-185">It must be between 5 minutes and 12 hours.</span><span class="sxs-lookup"><span data-stu-id="34912-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="34912-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="34912-186">**timeAggregation**</span></span>  
    <span data-ttu-id="34912-187">his value determines how the data that is collected should be combined over time.</span><span class="sxs-lookup"><span data-stu-id="34912-187">his value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="34912-188">The default value is Average.</span><span class="sxs-lookup"><span data-stu-id="34912-188">The default value is Average.</span></span> <span data-ttu-id="34912-189">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span><span class="sxs-lookup"><span data-stu-id="34912-189">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="34912-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="34912-190">**operator**</span></span>  
    <span data-ttu-id="34912-191">This value is the operator that is used to compare the metric data and the threshold.</span><span class="sxs-lookup"><span data-stu-id="34912-191">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="34912-192">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="34912-192">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="34912-193">**threshold**</span><span class="sxs-lookup"><span data-stu-id="34912-193">**threshold**</span></span>  
    <span data-ttu-id="34912-194">This value triggers the scale action.</span><span class="sxs-lookup"><span data-stu-id="34912-194">This value triggers the scale action.</span></span> <span data-ttu-id="34912-195">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span><span class="sxs-lookup"><span data-stu-id="34912-195">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span></span>
    
    * <span data-ttu-id="34912-196">**direction**</span><span class="sxs-lookup"><span data-stu-id="34912-196">**direction**</span></span>  
    <span data-ttu-id="34912-197">This value determines the action that is taken when the threshold value is achieved.</span><span class="sxs-lookup"><span data-stu-id="34912-197">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="34912-198">The possible values are Increase or Decrease.</span><span class="sxs-lookup"><span data-stu-id="34912-198">The possible values are Increase or Decrease.</span></span> <span data-ttu-id="34912-199">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span><span class="sxs-lookup"><span data-stu-id="34912-199">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span></span>

    * <span data-ttu-id="34912-200">**type**</span><span class="sxs-lookup"><span data-stu-id="34912-200">**type**</span></span>  
    <span data-ttu-id="34912-201">This value is the type of action that should occur and must be set to ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="34912-201">This value is the type of action that should occur and must be set to ChangeCount.</span></span>
    
    * <span data-ttu-id="34912-202">**value**</span><span class="sxs-lookup"><span data-stu-id="34912-202">**value**</span></span>  
    <span data-ttu-id="34912-203">This value is the number of virtual machines that are added or removed from the scale set.</span><span class="sxs-lookup"><span data-stu-id="34912-203">This value is the number of virtual machines that are added or removed from the scale set.</span></span> <span data-ttu-id="34912-204">This value must be 1 or greater.</span><span class="sxs-lookup"><span data-stu-id="34912-204">This value must be 1 or greater.</span></span> <span data-ttu-id="34912-205">The default value is 1.</span><span class="sxs-lookup"><span data-stu-id="34912-205">The default value is 1.</span></span> <span data-ttu-id="34912-206">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span><span class="sxs-lookup"><span data-stu-id="34912-206">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span></span>

    * <span data-ttu-id="34912-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="34912-207">**cooldown**</span></span>  
    <span data-ttu-id="34912-208">This value is the amount of time to wait since the last scaling action before the next action occurs.</span><span class="sxs-lookup"><span data-stu-id="34912-208">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="34912-209">This value must be between one minute and one week.</span><span class="sxs-lookup"><span data-stu-id="34912-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="34912-210">Save the template file.</span><span class="sxs-lookup"><span data-stu-id="34912-210">Save the template file.</span></span>    

## <a name="step-3-upload-the-template-to-storage"></a><span data-ttu-id="34912-211">Step 3: Upload the template to storage</span><span class="sxs-lookup"><span data-stu-id="34912-211">Step 3: Upload the template to storage</span></span>
<span data-ttu-id="34912-212">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span><span class="sxs-lookup"><span data-stu-id="34912-212">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span></span>

1. <span data-ttu-id="34912-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands to set the environment variables needed to access the storage account:</span><span class="sxs-lookup"><span data-stu-id="34912-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands to set the environment variables needed to access the storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="34912-214">You can get the key by clicking the key icon when viewing the storage account resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="34912-214">You can get the key by clicking the key icon when viewing the storage account resource in the Azure portal.</span></span> <span data-ttu-id="34912-215">When using a Windows command prompt, type **set** instead of export.</span><span class="sxs-lookup"><span data-stu-id="34912-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="34912-216">Create the container for storing the template.</span><span class="sxs-lookup"><span data-stu-id="34912-216">Create the container for storing the template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="34912-217">Upload the template file to the new container.</span><span class="sxs-lookup"><span data-stu-id="34912-217">Upload the template file to the new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-the-template"></a><span data-ttu-id="34912-218">Step 4: Deploy the template</span><span class="sxs-lookup"><span data-stu-id="34912-218">Step 4: Deploy the template</span></span>
<span data-ttu-id="34912-219">Now that you created the template, you can start deploying the resources.</span><span class="sxs-lookup"><span data-stu-id="34912-219">Now that you created the template, you can start deploying the resources.</span></span> <span data-ttu-id="34912-220">Use this command to start the process:</span><span class="sxs-lookup"><span data-stu-id="34912-220">Use this command to start the process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="34912-221">When you press enter, you are prompted to provide values for the variables you assigned.</span><span class="sxs-lookup"><span data-stu-id="34912-221">When you press enter, you are prompted to provide values for the variables you assigned.</span></span> <span data-ttu-id="34912-222">Provide these values:</span><span class="sxs-lookup"><span data-stu-id="34912-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="34912-223">It should take about 15 minutes for all the resources to successfully be deployed.</span><span class="sxs-lookup"><span data-stu-id="34912-223">It should take about 15 minutes for all the resources to successfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="34912-224">You can also use the portal’s ability to deploy the resources.</span><span class="sxs-lookup"><span data-stu-id="34912-224">You can also use the portal’s ability to deploy the resources.</span></span> <span data-ttu-id="34912-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="34912-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="34912-226">Step 5: Monitor resources</span><span class="sxs-lookup"><span data-stu-id="34912-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="34912-227">You can get some information about virtual machine scale sets using these methods:</span><span class="sxs-lookup"><span data-stu-id="34912-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="34912-228">The Azure portal - You can currently get a limited amount of information using the portal.</span><span class="sxs-lookup"><span data-stu-id="34912-228">The Azure portal - You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="34912-229">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span><span class="sxs-lookup"><span data-stu-id="34912-229">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="34912-230">Follow this path and you should see the instance view of the scale set that you created:</span><span class="sxs-lookup"><span data-stu-id="34912-230">Follow this path and you should see the instance view of the scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="34912-231">Azure CLI - Use this command to get some information:</span><span class="sxs-lookup"><span data-stu-id="34912-231">Azure CLI - Use this command to get some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="34912-232">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span><span class="sxs-lookup"><span data-stu-id="34912-232">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="34912-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span><span class="sxs-lookup"><span data-stu-id="34912-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-the-resources"></a><span data-ttu-id="34912-234">Step 6: Remove the resources</span><span class="sxs-lookup"><span data-stu-id="34912-234">Step 6: Remove the resources</span></span>
<span data-ttu-id="34912-235">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span><span class="sxs-lookup"><span data-stu-id="34912-235">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="34912-236">You don’t need to delete each resource separately from a resource group.</span><span class="sxs-lookup"><span data-stu-id="34912-236">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="34912-237">You can delete the resource group and all its resources are automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="34912-237">You can delete the resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="34912-238">Next steps</span><span class="sxs-lookup"><span data-stu-id="34912-238">Next steps</span></span>
* <span data-ttu-id="34912-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="34912-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="34912-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="34912-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="34912-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="34912-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="34912-242">Check out the [Autoscale a VM Scale Set running a Ubuntu/Apache/PHP app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-lapstack-autoscale) template that sets up a LAMP stack to exercise the automatic scaling functionality of Virtual Machine Scale Sets.</span><span class="sxs-lookup"><span data-stu-id="34912-242">Check out the [Autoscale a VM Scale Set running a Ubuntu/Apache/PHP app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-lapstack-autoscale) template that sets up a LAMP stack to exercise the automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

