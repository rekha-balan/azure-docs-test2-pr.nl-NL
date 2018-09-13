---
title: Analyze network security with Azure Network Watcher Security Group View - PowerShell | Microsoft Docs
description: This article will describe how to use PowerShell to analyze a virtual machines security with Security Group View.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 44a59a43745494eb943711a5afcb6e436a25a44d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553075"
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="d3242-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3242-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

<span data-ttu-id="d3242-107">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d3242-107">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="d3242-108">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="d3242-108">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="d3242-109">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3242-109">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d3242-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="d3242-110">Before you begin</span></span>

<span data-ttu-id="d3242-111">In this scenario, you run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet to retrieve the security rule information.</span><span class="sxs-lookup"><span data-stu-id="d3242-111">In this scenario, you run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet to retrieve the security rule information.</span></span>

<span data-ttu-id="d3242-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="d3242-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="d3242-113">Scenario</span><span class="sxs-lookup"><span data-stu-id="d3242-113">Scenario</span></span>

<span data-ttu-id="d3242-114">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d3242-114">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="d3242-115">Retrieve Network Watcher</span><span class="sxs-lookup"><span data-stu-id="d3242-115">Retrieve Network Watcher</span></span>

<span data-ttu-id="d3242-116">The first step is to retrieve the Network Watcher instance.</span><span class="sxs-lookup"><span data-stu-id="d3242-116">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="d3242-117">This variable is passed to the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d3242-117">This variable is passed to the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="d3242-118">Get a VM</span><span class="sxs-lookup"><span data-stu-id="d3242-118">Get a VM</span></span>

<span data-ttu-id="d3242-119">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span><span class="sxs-lookup"><span data-stu-id="d3242-119">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="d3242-120">The following example gets a VM object.</span><span class="sxs-lookup"><span data-stu-id="d3242-120">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="d3242-121">Retrieve security group view</span><span class="sxs-lookup"><span data-stu-id="d3242-121">Retrieve security group view</span></span>

<span data-ttu-id="d3242-122">The next step is to retrieve the security group view result.</span><span class="sxs-lookup"><span data-stu-id="d3242-122">The next step is to retrieve the security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-the-results"></a><span data-ttu-id="d3242-123">Viewing the results</span><span class="sxs-lookup"><span data-stu-id="d3242-123">Viewing the results</span></span>

<span data-ttu-id="d3242-124">The following example is a shortened response of the results returned.</span><span class="sxs-lookup"><span data-stu-id="d3242-124">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="d3242-125">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="d3242-125">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a><span data-ttu-id="d3242-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3242-126">Next steps</span></span>

<span data-ttu-id="d3242-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="d3242-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


