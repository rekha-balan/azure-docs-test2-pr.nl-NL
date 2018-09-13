---
title: Create a virtual network | Azure Resource Manager template | Microsoft Docs
description: Learn how to create a virtual network using an Azure Resource Manager template.
services: virtual-network
documentationcenter: ''
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0069e3398f8f6529e5a87f8a5c715e6f614c675
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551737"
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="d27b6-103">Create a virtual network using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="d27b6-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="d27b6-104">Azure has two deployment models: Azure Resource Manager and classic.</span><span class="sxs-lookup"><span data-stu-id="d27b6-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="d27b6-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="d27b6-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="d27b6-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="d27b6-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="d27b6-107">This article explains how to create a VNet through the Resource Manager deployment model using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="d27b6-107">This article explains how to create a VNet through the Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="d27b6-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span><span class="sxs-lookup"><span data-stu-id="d27b6-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="d27b6-109">Portal</span><span class="sxs-lookup"><span data-stu-id="d27b6-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="d27b6-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d27b6-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="d27b6-111">CLI</span><span class="sxs-lookup"><span data-stu-id="d27b6-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="d27b6-112">Template</span><span class="sxs-lookup"><span data-stu-id="d27b6-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="d27b6-113">Portal (Classic)</span><span class="sxs-lookup"><span data-stu-id="d27b6-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="d27b6-114">PowerShell (Classic)</span><span class="sxs-lookup"><span data-stu-id="d27b6-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="d27b6-115">CLI (Classic)</span><span class="sxs-lookup"><span data-stu-id="d27b6-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="d27b6-116">You will learn how to download and modify and existing ARM template from GitHub, and deploy the template from GitHub, PowerShell, and the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d27b6-116">You will learn how to download and modify and existing ARM template from GitHub, and deploy the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="d27b6-117">If you are simply deploying the ARM template directly from GitHub, without any changes, skip to [deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="d27b6-117">If you are simply deploying the ARM template directly from GitHub, without any changes, skip to [deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="d27b6-118">Download and understand the Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="d27b6-118">Download and understand the Azure Resource Manager template</span></span>
<span data-ttu-id="d27b6-119">You can download the existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span><span class="sxs-lookup"><span data-stu-id="d27b6-119">You can download the existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="d27b6-120">To do so, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="d27b6-120">To do so, complete the following steps:</span></span>

1. <span data-ttu-id="d27b6-121">Navigate to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="d27b6-121">Navigate to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="d27b6-122">Click **azuredeploy.json**, and then click **RAW**.</span><span class="sxs-lookup"><span data-stu-id="d27b6-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="d27b6-123">Save the file to a a local folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="d27b6-123">Save the file to a a local folder on your computer.</span></span>
4. <span data-ttu-id="d27b6-124">If you are familiar with templates, skip to step 7.</span><span class="sxs-lookup"><span data-stu-id="d27b6-124">If you are familiar with templates, skip to step 7.</span></span>
5. <span data-ttu-id="d27b6-125">Open the file you just saved and look at the contents under **parameters** in line 5.</span><span class="sxs-lookup"><span data-stu-id="d27b6-125">Open the file you just saved and look at the contents under **parameters** in line 5.</span></span> <span data-ttu-id="d27b6-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span><span class="sxs-lookup"><span data-stu-id="d27b6-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="d27b6-127">Parameter</span><span class="sxs-lookup"><span data-stu-id="d27b6-127">Parameter</span></span> | <span data-ttu-id="d27b6-128">Description</span><span class="sxs-lookup"><span data-stu-id="d27b6-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="d27b6-129">**location**</span><span class="sxs-lookup"><span data-stu-id="d27b6-129">**location**</span></span> |<span data-ttu-id="d27b6-130">Azure region where the VNet will be created</span><span class="sxs-lookup"><span data-stu-id="d27b6-130">Azure region where the VNet will be created</span></span> |
   | <span data-ttu-id="d27b6-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="d27b6-131">**vnetName**</span></span> |<span data-ttu-id="d27b6-132">Name for the new VNet</span><span class="sxs-lookup"><span data-stu-id="d27b6-132">Name for the new VNet</span></span> |
   | <span data-ttu-id="d27b6-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="d27b6-133">**addressPrefix**</span></span> |<span data-ttu-id="d27b6-134">Address space for the VNet, in CIDR format</span><span class="sxs-lookup"><span data-stu-id="d27b6-134">Address space for the VNet, in CIDR format</span></span> |
   | <span data-ttu-id="d27b6-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="d27b6-135">**subnet1Name**</span></span> |<span data-ttu-id="d27b6-136">Name for the first VNet</span><span class="sxs-lookup"><span data-stu-id="d27b6-136">Name for the first VNet</span></span> |
   | <span data-ttu-id="d27b6-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="d27b6-137">**subnet1Prefix**</span></span> |<span data-ttu-id="d27b6-138">CIDR block for the first subnet</span><span class="sxs-lookup"><span data-stu-id="d27b6-138">CIDR block for the first subnet</span></span> |
   | <span data-ttu-id="d27b6-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="d27b6-139">**subnet2Name**</span></span> |<span data-ttu-id="d27b6-140">Name for the second VNet</span><span class="sxs-lookup"><span data-stu-id="d27b6-140">Name for the second VNet</span></span> |
   | <span data-ttu-id="d27b6-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="d27b6-141">**subnet2Prefix**</span></span> |<span data-ttu-id="d27b6-142">CIDR block for the second subnet</span><span class="sxs-lookup"><span data-stu-id="d27b6-142">CIDR block for the second subnet</span></span> |
   
   > [!IMPORTANT]
   > Azure Resource Manager templates maintained in GitHub can change over time. Make sure you check the template before using it.
   > 
   > 
6. <span data-ttu-id="d27b6-145">Check the content under **resources** and notice the following:</span><span class="sxs-lookup"><span data-stu-id="d27b6-145">Check the content under **resources** and notice the following:</span></span>
   
   * <span data-ttu-id="d27b6-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="d27b6-146">**type**.</span></span> <span data-ttu-id="d27b6-147">Type of resource being created by the template.</span><span class="sxs-lookup"><span data-stu-id="d27b6-147">Type of resource being created by the template.</span></span> <span data-ttu-id="d27b6-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span><span class="sxs-lookup"><span data-stu-id="d27b6-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="d27b6-149">**name**.</span><span class="sxs-lookup"><span data-stu-id="d27b6-149">**name**.</span></span> <span data-ttu-id="d27b6-150">Name for the resource.</span><span class="sxs-lookup"><span data-stu-id="d27b6-150">Name for the resource.</span></span> <span data-ttu-id="d27b6-151">Notice the use of **[parameters('vnetName')]**, which means the name will provided as input by the user or a parameter file during deployment.</span><span class="sxs-lookup"><span data-stu-id="d27b6-151">Notice the use of **[parameters('vnetName')]**, which means the name will provided as input by the user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="d27b6-152">**properties**.</span><span class="sxs-lookup"><span data-stu-id="d27b6-152">**properties**.</span></span> <span data-ttu-id="d27b6-153">List of properties for the resource.</span><span class="sxs-lookup"><span data-stu-id="d27b6-153">List of properties for the resource.</span></span> <span data-ttu-id="d27b6-154">This template uses the address space and subnet properties during VNet creation.</span><span class="sxs-lookup"><span data-stu-id="d27b6-154">This template uses the address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="d27b6-155">Navigate back to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="d27b6-155">Navigate back to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="d27b6-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span><span class="sxs-lookup"><span data-stu-id="d27b6-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="d27b6-157">Save the file to a a local folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="d27b6-157">Save the file to a a local folder on your computer.</span></span>
10. <span data-ttu-id="d27b6-158">Open the file you just saved and edit the values for the parameters.</span><span class="sxs-lookup"><span data-stu-id="d27b6-158">Open the file you just saved and edit the values for the parameters.</span></span> <span data-ttu-id="d27b6-159">Use the following values below to deploy the VNet described in the scenario:</span><span class="sxs-lookup"><span data-stu-id="d27b6-159">Use the following values below to deploy the VNet described in the scenario:</span></span>

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. <span data-ttu-id="d27b6-160">Save the file.</span><span class="sxs-lookup"><span data-stu-id="d27b6-160">Save the file.</span></span>


## <a name="deploy-the-template-using-powershell"></a><span data-ttu-id="d27b6-161">Deploy the template using PowerShell</span><span class="sxs-lookup"><span data-stu-id="d27b6-161">Deploy the template using PowerShell</span></span>

<span data-ttu-id="d27b6-162">Complete the following steps to deploy the template you downloaded by using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d27b6-162">Complete the following steps to deploy the template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="d27b6-163">Install and configure Azure PowerShell by completing the steps in the [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article.</span><span class="sxs-lookup"><span data-stu-id="d27b6-163">Install and configure Azure PowerShell by completing the steps in the [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article.</span></span>
2. <span data-ttu-id="d27b6-164">Run the following command to create a new resource group:</span><span class="sxs-lookup"><span data-stu-id="d27b6-164">Run the following command to create a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="d27b6-165">The command creates a resource group named *TestRG* in the *Central US* azure region.</span><span class="sxs-lookup"><span data-stu-id="d27b6-165">The command creates a resource group named *TestRG* in the *Central US* azure region.</span></span> <span data-ttu-id="d27b6-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d27b6-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="d27b6-167">Expected output:</span><span class="sxs-lookup"><span data-stu-id="d27b6-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="d27b6-168">Run the following command to deploy the new VNet using the template and parameter files you downloaded and modified above:</span><span class="sxs-lookup"><span data-stu-id="d27b6-168">Run the following command to deploy the new VNet using the template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="d27b6-169">Expected output:</span><span class="sxs-lookup"><span data-stu-id="d27b6-169">Expected output:</span></span>
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. <span data-ttu-id="d27b6-170">Run the following command to view the properties of the new VNet:</span><span class="sxs-lookup"><span data-stu-id="d27b6-170">Run the following command to view the properties of the new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="d27b6-171">Expected output:</span><span class="sxs-lookup"><span data-stu-id="d27b6-171">Expected output:</span></span>

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-the-template-using-click-to-deploy"></a><span data-ttu-id="d27b6-172">Deploy the template using click-to-deploy</span><span class="sxs-lookup"><span data-stu-id="d27b6-172">Deploy the template using click-to-deploy</span></span>

<span data-ttu-id="d27b6-173">You can reuse pre-defined Azure Resource Manager templates uploaded to a GitHub repository maintained by Microsoft and open to the community.</span><span class="sxs-lookup"><span data-stu-id="d27b6-173">You can reuse pre-defined Azure Resource Manager templates uploaded to a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="d27b6-174">These templates can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span><span class="sxs-lookup"><span data-stu-id="d27b6-174">These templates can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> <span data-ttu-id="d27b6-175">To deploy a template that creates a VNet with two subnets, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="d27b6-175">To deploy a template that creates a VNet with two subnets, complete the following steps:</span></span>

1. <span data-ttu-id="d27b6-176">From a browser, navigate to [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="d27b6-176">From a browser, navigate to [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="d27b6-177">Scroll down the list of templates, and click **101-vnet-two-subnets**.</span><span class="sxs-lookup"><span data-stu-id="d27b6-177">Scroll down the list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="d27b6-178">Check the **README.md** file, as shown below.</span><span class="sxs-lookup"><span data-stu-id="d27b6-178">Check the **README.md** file, as shown below.</span></span>

    ![READEME.md file in github](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="d27b6-180">Click **Deploy to Azure**.</span><span class="sxs-lookup"><span data-stu-id="d27b6-180">Click **Deploy to Azure**.</span></span> <span data-ttu-id="d27b6-181">If necessary, enter your Azure login credentials.</span><span class="sxs-lookup"><span data-stu-id="d27b6-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="d27b6-182">In the **Parameters** blade, enter the values you want to use to create your new VNet, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d27b6-182">In the **Parameters** blade, enter the values you want to use to create your new VNet, and then click **OK**.</span></span> <span data-ttu-id="d27b6-183">The following figure shows the values for the scenario:</span><span class="sxs-lookup"><span data-stu-id="d27b6-183">The following figure shows the values for the scenario:</span></span>
   
    ![ARM template parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="d27b6-185">Click **Resource group** and select a resource group to add the VNet to, or click **Create new** to add the VNet to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="d27b6-185">Click **Resource group** and select a resource group to add the VNet to, or click **Create new** to add the VNet to a new resource group.</span></span> <span data-ttu-id="d27b6-186">The following figure shows the resource group settings for a new resource group called **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="d27b6-186">The following figure shows the resource group settings for a new resource group called **TestRG**:</span></span>

    ![Resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="d27b6-188">If necessary, change the **Subscription** and **Location** settings for your VNet.</span><span class="sxs-lookup"><span data-stu-id="d27b6-188">If necessary, change the **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="d27b6-189">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span><span class="sxs-lookup"><span data-stu-id="d27b6-189">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span></span>
8. <span data-ttu-id="d27b6-190">Click **Legal terms**, read the terms, and click **Buy** to agree.</span><span class="sxs-lookup"><span data-stu-id="d27b6-190">Click **Legal terms**, read the terms, and click **Buy** to agree.</span></span> 
9. <span data-ttu-id="d27b6-191">Click **Create** to create the VNet.</span><span class="sxs-lookup"><span data-stu-id="d27b6-191">Click **Create** to create the VNet.</span></span>
   
    ![Submitting deployment tile in preview portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="d27b6-193">Once the deployment is complete, in the Azure portal click **More services**, type *virtual networks* in the filter box that appears, then click Virtual networks to see the Virtual networks blade.</span><span class="sxs-lookup"><span data-stu-id="d27b6-193">Once the deployment is complete, in the Azure portal click **More services**, type *virtual networks* in the filter box that appears, then click Virtual networks to see the Virtual networks blade.</span></span> <span data-ttu-id="d27b6-194">In the blade, click *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="d27b6-194">In the blade, click *TestVNet*.</span></span> <span data-ttu-id="d27b6-195">In the *TestVNet* blade, click **Subnets** to see the created subnets, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="d27b6-195">In the *TestVNet* blade, click **Subnets** to see the created subnets, as shown in the following picture:</span></span>
    
     ![Create VNet in preview portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="d27b6-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="d27b6-197">Next steps</span></span>

<span data-ttu-id="d27b6-198">Learn how to connect:</span><span class="sxs-lookup"><span data-stu-id="d27b6-198">Learn how to connect:</span></span>

- <span data-ttu-id="d27b6-199">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span><span class="sxs-lookup"><span data-stu-id="d27b6-199">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="d27b6-200">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span><span class="sxs-lookup"><span data-stu-id="d27b6-200">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="d27b6-201">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span><span class="sxs-lookup"><span data-stu-id="d27b6-201">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="d27b6-202">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d27b6-202">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="d27b6-203">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span><span class="sxs-lookup"><span data-stu-id="d27b6-203">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>





