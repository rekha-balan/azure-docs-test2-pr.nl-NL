---
title: Create a VM with a static public IP address - Azure Resource Manager template | Microsoft Docs
description: Learn how to create a VM with a static public IP address using an Azure Resource Manager template.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1bb49c0c03a3103194d068b511fa92ecb996caf3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552075"
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="f4640-103">Create a VM with a static public IP address using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="f4640-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [Template](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Classic)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md). This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="f4640-111">Public IP address resources in a template file</span><span class="sxs-lookup"><span data-stu-id="f4640-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="f4640-112">You can view and download the [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="f4640-112">You can view and download the [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="f4640-113">The following section shows the definition of the public IP resource, based on the scenario above:</span><span class="sxs-lookup"><span data-stu-id="f4640-113">The following section shows the definition of the public IP resource, based on the scenario above:</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

<span data-ttu-id="f4640-114">Notice the **publicIPAllocationMethod** property, which is set to *Static*.</span><span class="sxs-lookup"><span data-stu-id="f4640-114">Notice the **publicIPAllocationMethod** property, which is set to *Static*.</span></span> <span data-ttu-id="f4640-115">This property can be either *Dynamic* (default value) or *Static*.</span><span class="sxs-lookup"><span data-stu-id="f4640-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="f4640-116">Setting it to static guarantees that the public IP address assigned will never change.</span><span class="sxs-lookup"><span data-stu-id="f4640-116">Setting it to static guarantees that the public IP address assigned will never change.</span></span>

<span data-ttu-id="f4640-117">The following section shows the association of the public IP address with a network interface:</span><span class="sxs-lookup"><span data-stu-id="f4640-117">The following section shows the association of the public IP address with a network interface:</span></span>

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

<span data-ttu-id="f4640-118">Notice the **publicIPAddress** property pointing to the **Id** of a resource named **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="f4640-118">Notice the **publicIPAddress** property pointing to the **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="f4640-119">That is the name of the public IP resource shown above.</span><span class="sxs-lookup"><span data-stu-id="f4640-119">That is the name of the public IP resource shown above.</span></span>

<span data-ttu-id="f4640-120">Finally, the network interface above is listed in the **networkProfile** property of the VM being created.</span><span class="sxs-lookup"><span data-stu-id="f4640-120">Finally, the network interface above is listed in the **networkProfile** property of the VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="f4640-121">Deploy the template by using click to deploy</span><span class="sxs-lookup"><span data-stu-id="f4640-121">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="f4640-122">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span><span class="sxs-lookup"><span data-stu-id="f4640-122">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="f4640-123">To deploy this template using click to deploy, click **Deploy to Azure** in the Readme.md file for the [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span><span class="sxs-lookup"><span data-stu-id="f4640-123">To deploy this template using click to deploy, click **Deploy to Azure** in the Readme.md file for the [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="f4640-124">Replace the default parameter values if desired and enter values for the blank parameters.</span><span class="sxs-lookup"><span data-stu-id="f4640-124">Replace the default parameter values if desired and enter values for the blank parameters.</span></span>  <span data-ttu-id="f4640-125">Follow the instructions in the portal to create a virtual machine with a static public IP address.</span><span class="sxs-lookup"><span data-stu-id="f4640-125">Follow the instructions in the portal to create a virtual machine with a static public IP address.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="f4640-126">Deploy the template by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4640-126">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="f4640-127">To deploy the template you downloaded by using PowerShell, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="f4640-127">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="f4640-128">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article.</span><span class="sxs-lookup"><span data-stu-id="f4640-128">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article.</span></span>
2. <span data-ttu-id="f4640-129">In a PowerShell console, run the `New-AzureRmResourceGroup` cmdlet to create a new resource group, if necessary.</span><span class="sxs-lookup"><span data-stu-id="f4640-129">In a PowerShell console, run the `New-AzureRmResourceGroup` cmdlet to create a new resource group, if necessary.</span></span> <span data-ttu-id="f4640-130">If you already have a resource group created, go to step 3.</span><span class="sxs-lookup"><span data-stu-id="f4640-130">If you already have a resource group created, go to step 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="f4640-131">Expected output:</span><span class="sxs-lookup"><span data-stu-id="f4640-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="f4640-132">In a PowerShell console, run the `New-AzureRmResourceGroupDeployment` cmdlet to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="f4640-132">In a PowerShell console, run the `New-AzureRmResourceGroupDeployment` cmdlet to deploy the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="f4640-133">Expected output:</span><span class="sxs-lookup"><span data-stu-id="f4640-133">Expected output:</span></span>
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="f4640-134">Deploy the template by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f4640-134">Deploy the template by using the Azure CLI</span></span>
<span data-ttu-id="f4640-135">To deploy the template by using the Azure CLI, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="f4640-135">To deploy the template by using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="f4640-136">If you have never used Azure CLI, follow the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article to install and configure it.</span><span class="sxs-lookup"><span data-stu-id="f4640-136">If you have never used Azure CLI, follow the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article to install and configure it.</span></span>
2. <span data-ttu-id="f4640-137">Run the `azure config mode` command to switch to Resource Manager mode, as shown below.</span><span class="sxs-lookup"><span data-stu-id="f4640-137">Run the `azure config mode` command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="f4640-138">The expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="f4640-138">The expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="f4640-139">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it to a file in your computer.</span><span class="sxs-lookup"><span data-stu-id="f4640-139">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it to a file in your computer.</span></span> <span data-ttu-id="f4640-140">For this example, the parameters are saved to a file named *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="f4640-140">For this example, the parameters are saved to a file named *parameters.json*.</span></span> <span data-ttu-id="f4640-141">Change the parameter values within the file if desired, but at a minimum, it's recommended that you change the value for the adminPassword parameter to a unique, complex password.</span><span class="sxs-lookup"><span data-stu-id="f4640-141">Change the parameter values within the file if desired, but at a minimum, it's recommended that you change the value for the adminPassword parameter to a unique, complex password.</span></span>
4. <span data-ttu-id="f4640-142">Run the `azure group deployment create` cmd to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span><span class="sxs-lookup"><span data-stu-id="f4640-142">Run the `azure group deployment create` cmd to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="f4640-143">In the command below, replace <path> with the path you saved the file to.</span><span class="sxs-lookup"><span data-stu-id="f4640-143">In the command below, replace <path> with the path you saved the file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="f4640-144">Expected output (lists parameter values used):</span><span class="sxs-lookup"><span data-stu-id="f4640-144">Expected output (lists parameter values used):</span></span>

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

