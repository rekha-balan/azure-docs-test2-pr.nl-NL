---
title: Analyze network security with Azure Network Watcher Security Group View - Azure CLI | Microsoft Docs
description: This article will describe how to use Azure CLI to analyze a virtual machines security with Security Group View.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 3644d989444f5aa924f81ed1ffb30220c1daa5d3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554118"
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli"></a><span data-ttu-id="acd35-103">Analyze your Virtual Machine security with Security Group View using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="acd35-103">Analyze your Virtual Machine security with Security Group View using Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

<span data-ttu-id="acd35-107">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="acd35-107">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="acd35-108">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="acd35-108">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="acd35-109">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="acd35-109">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>

<span data-ttu-id="acd35-110">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="acd35-110">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="acd35-111">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span><span class="sxs-lookup"><span data-stu-id="acd35-111">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="acd35-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="acd35-112">Before you begin</span></span>

<span data-ttu-id="acd35-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="acd35-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="acd35-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="acd35-114">Scenario</span></span>

<span data-ttu-id="acd35-115">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span><span class="sxs-lookup"><span data-stu-id="acd35-115">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="acd35-116">Get a VM</span><span class="sxs-lookup"><span data-stu-id="acd35-116">Get a VM</span></span>

<span data-ttu-id="acd35-117">A virtual machine is required to run the `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="acd35-117">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="acd35-118">The following command lists the virtual machinese in a resource group:</span><span class="sxs-lookup"><span data-stu-id="acd35-118">The following command lists the virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="acd35-119">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span><span class="sxs-lookup"><span data-stu-id="acd35-119">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="acd35-120">Retrieve security group view</span><span class="sxs-lookup"><span data-stu-id="acd35-120">Retrieve security group view</span></span>

<span data-ttu-id="acd35-121">The next step is to retrieve the security group view result.</span><span class="sxs-lookup"><span data-stu-id="acd35-121">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="acd35-122">Adding the "--json" flag will format the results in json.</span><span class="sxs-lookup"><span data-stu-id="acd35-122">Adding the "--json" flag will format the results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-the-results"></a><span data-ttu-id="acd35-123">Viewing the results</span><span class="sxs-lookup"><span data-stu-id="acd35-123">Viewing the results</span></span>

<span data-ttu-id="acd35-124">The following example is a shortened response of the results returned.</span><span class="sxs-lookup"><span data-stu-id="acd35-124">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="acd35-125">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="acd35-125">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="acd35-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="acd35-126">Next steps</span></span>

<span data-ttu-id="acd35-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="acd35-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="acd35-128">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="acd35-128">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
