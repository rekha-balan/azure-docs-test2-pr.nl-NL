---
title: Analyze network security with Azure Network Watcher Security Group View - REST API | Microsoft Docs
description: This article will describe how to use PowerShell to analyze a virtual machines security with Security Group View.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 80ae80d3243b531c7348a709aa4ad6e6ed401980
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661322"
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="2f876-103">Analyze your Virtual Machine security with Security Group View using REST API</span><span class="sxs-lookup"><span data-stu-id="2f876-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

<span data-ttu-id="2f876-107">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f876-107">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="2f876-108">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="2f876-108">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="2f876-109">In this article, we show you how to retrieve the effective and applied security rules to a virtual machine using REST API</span><span class="sxs-lookup"><span data-stu-id="2f876-109">In this article, we show you how to retrieve the effective and applied security rules to a virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2f876-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="2f876-110">Before you begin</span></span>

<span data-ttu-id="2f876-111">In this scenario, you call the Network Watcher Rest API to get the security group view for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f876-111">In this scenario, you call the Network Watcher Rest API to get the security group view for a virtual machine.</span></span> <span data-ttu-id="2f876-112">ARMclient is used to call the REST API using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f876-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="2f876-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="2f876-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="2f876-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="2f876-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="2f876-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span><span class="sxs-lookup"><span data-stu-id="2f876-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2f876-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="2f876-116">Scenario</span></span>

<span data-ttu-id="2f876-117">The scenario covered in this article retrieves the effective and applied security rules for a given virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f876-117">The scenario covered in this article retrieves the effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="2f876-118">Log in with ARMClient</span><span class="sxs-lookup"><span data-stu-id="2f876-118">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="2f876-119">Retrieve a virtual machine</span><span class="sxs-lookup"><span data-stu-id="2f876-119">Retrieve a virtual machine</span></span>

<span data-ttu-id="2f876-120">Run the following script to return a virtual machineThe following code needs variables:</span><span class="sxs-lookup"><span data-stu-id="2f876-120">Run the following script to return a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="2f876-121">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f876-121">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="2f876-122">**resourceGroupName** - The name of a resource group that contains virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2f876-122">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="2f876-123">The information that is needed is the **id** under the type `Microsoft.Compute/virtualMachines` in response, as seen in the following example:</span><span class="sxs-lookup"><span data-stu-id="2f876-123">The information that is needed is the **id** under the type `Microsoft.Compute/virtualMachines` in response, as seen in the following example:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="2f876-124">Get security group view for virtual machine</span><span class="sxs-lookup"><span data-stu-id="2f876-124">Get security group view for virtual machine</span></span>

<span data-ttu-id="2f876-125">The following example requests the security group view of a targeted virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f876-125">The following example requests the security group view of a targeted virtual machine.</span></span> <span data-ttu-id="2f876-126">The results from this example can be used to compare to the rules and security defined by the origination to look for configuration drift.</span><span class="sxs-lookup"><span data-stu-id="2f876-126">The results from this example can be used to compare to the rules and security defined by the origination to look for configuration drift.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-the-response"></a><span data-ttu-id="2f876-127">View the response</span><span class="sxs-lookup"><span data-stu-id="2f876-127">View the response</span></span>

<span data-ttu-id="2f876-128">The following sample is the response returned from the preceding command.</span><span class="sxs-lookup"><span data-stu-id="2f876-128">The following sample is the response returned from the preceding command.</span></span> <span data-ttu-id="2f876-129">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="2f876-129">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="2f876-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f876-130">Next steps</span></span>

<span data-ttu-id="2f876-131">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) to learn how to automate validation of Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="2f876-131">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


