---
title: Create network security groups - Azure PowerShell | Microsoft Docs
description: Learn how to create and deploy network security groups using PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9cef62b8-d889-4d16-b4d0-58639539a418
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6215abf064227f0d75a50e866b09ca2083a269d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556043"
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="53dc1-103">Create network security groups using PowerShell</span><span class="sxs-lookup"><span data-stu-id="53dc1-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="53dc1-104">Azure has two deployment models: Azure Resource Manager and classic.</span><span class="sxs-lookup"><span data-stu-id="53dc1-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="53dc1-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="53dc1-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="53dc1-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="53dc1-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="53dc1-107">This article covers the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="53dc1-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="53dc1-108">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="53dc1-108">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="53dc1-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span><span class="sxs-lookup"><span data-stu-id="53dc1-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="53dc1-110">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span><span class="sxs-lookup"><span data-stu-id="53dc1-110">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="53dc1-111">How to create the NSG for the front end subnet</span><span class="sxs-lookup"><span data-stu-id="53dc1-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="53dc1-112">To create an NSG named *NSG-FrontEnd* based on the scenario, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="53dc1-112">To create an NSG named *NSG-FrontEnd* based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="53dc1-113">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="53dc1-113">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="53dc1-114">Create a security rule allowing access from the Internet to port 3389.</span><span class="sxs-lookup"><span data-stu-id="53dc1-114">Create a security rule allowing access from the Internet to port 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="53dc1-115">Create a security rule allowing access from the Internet to port 80.</span><span class="sxs-lookup"><span data-stu-id="53dc1-115">Create a security rule allowing access from the Internet to port 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="53dc1-116">Add the rules created above to a new NSG named **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="53dc1-116">Add the rules created above to a new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="53dc1-117">Check the rules created in the NSG by typing the following:</span><span class="sxs-lookup"><span data-stu-id="53dc1-117">Check the rules created in the NSG by typing the following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="53dc1-118">Output showing just the security rules:</span><span class="sxs-lookup"><span data-stu-id="53dc1-118">Output showing just the security rules:</span></span>
   
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
                                   "Description": "Allow RDP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "3389",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 100,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 },
                                 {
                                   "Name": "web-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
                                   "Description": "Allow HTTP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "80",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 101,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
6. <span data-ttu-id="53dc1-119">Associate the NSG created above to the *FrontEnd* subnet.</span><span class="sxs-lookup"><span data-stu-id="53dc1-119">Associate the NSG created above to the *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="53dc1-120">Output showing only the *FrontEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span><span class="sxs-lookup"><span data-stu-id="53dc1-120">Output showing only the *FrontEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
                    Subnets           : [
                                          {
                                            "Name": "FrontEnd",
                                            "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                            "AddressPrefix": "192.168.1.0/24",
                                            "IpConfigurations": [
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                              },
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                              }
                                            ],
                                            "NetworkSecurityGroup": {
                                              "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                            },
                                            "RouteTable": null,
                                            "ProvisioningState": "Succeeded"
                                          }
   
   > [!WARNING]
   > <span data-ttu-id="53dc1-121">The output for the command above shows the content for the virtual network configuration object, which only exists on the computer where you are running PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53dc1-121">The output for the command above shows the content for the virtual network configuration object, which only exists on the computer where you are running PowerShell.</span></span> <span data-ttu-id="53dc1-122">You need to run the `Set-AzureRmVirtualNetwork` cmdlet to save these settings to Azure.</span><span class="sxs-lookup"><span data-stu-id="53dc1-122">You need to run the `Set-AzureRmVirtualNetwork` cmdlet to save these settings to Azure.</span></span>
   > 
   > 
7. <span data-ttu-id="53dc1-123">Save the new VNet settings to Azure.</span><span class="sxs-lookup"><span data-stu-id="53dc1-123">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="53dc1-124">Output showing just the NSG portion:</span><span class="sxs-lookup"><span data-stu-id="53dc1-124">Output showing just the NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="53dc1-125">How to create the NSG for the back-end subnet</span><span class="sxs-lookup"><span data-stu-id="53dc1-125">How to create the NSG for the back-end subnet</span></span>
<span data-ttu-id="53dc1-126">To create an NSG named *NSG-BackEnd* based on the scenario above, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="53dc1-126">To create an NSG named *NSG-BackEnd* based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="53dc1-127">Create a security rule allowing access from the front-end subnet to port 1433 (default port used by SQL Server).</span><span class="sxs-lookup"><span data-stu-id="53dc1-127">Create a security rule allowing access from the front-end subnet to port 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="53dc1-128">Create a security rule blocking access to the Internet.</span><span class="sxs-lookup"><span data-stu-id="53dc1-128">Create a security rule blocking access to the Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="53dc1-129">Add the rules created above to a new NSG named **NSG-BackEnd**.</span><span class="sxs-lookup"><span data-stu-id="53dc1-129">Add the rules created above to a new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="53dc1-130">Associate the NSG created above to the *BackEnd* subnet.</span><span class="sxs-lookup"><span data-stu-id="53dc1-130">Associate the NSG created above to the *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="53dc1-131">Output showing only the *BackEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span><span class="sxs-lookup"><span data-stu-id="53dc1-131">Output showing only the *BackEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
        Subnets           : [
                      {
                        "Name": "BackEnd",
                        "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                        "AddressPrefix": "192.168.2.0/24",
                        "IpConfigurations": [...],
                        "NetworkSecurityGroup": {
                          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "RouteTable": null,
                        "ProvisioningState": "Succeeded"
                      }
5. <span data-ttu-id="53dc1-132">Save the new VNet settings to Azure.</span><span class="sxs-lookup"><span data-stu-id="53dc1-132">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-to-remove-an-nsg"></a><span data-ttu-id="53dc1-133">How to remove an NSG</span><span class="sxs-lookup"><span data-stu-id="53dc1-133">How to remove an NSG</span></span>
<span data-ttu-id="53dc1-134">To delete an existing NSG, called *NSG-Frontend* in this case, follow the step below:</span><span class="sxs-lookup"><span data-stu-id="53dc1-134">To delete an existing NSG, called *NSG-Frontend* in this case, follow the step below:</span></span>

<span data-ttu-id="53dc1-135">Run the **Remove-AzureRmNetworkSecurityGroup** shown below and be sure to include the resource group the NSG is in.</span><span class="sxs-lookup"><span data-stu-id="53dc1-135">Run the **Remove-AzureRmNetworkSecurityGroup** shown below and be sure to include the resource group the NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

