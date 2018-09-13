---
title: Automate NSG auditing with Azure Network Watcher Security group view | Microsoft Docs
description: This page provides instructions on how to configure auditing of a Network Security Group
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: 227ea446a75c167be27128b15de1d3c216e6856d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830375"
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="b847f-103">Automate NSG auditing with Azure Network Watcher Security group view</span><span class="sxs-lookup"><span data-stu-id="b847f-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="b847f-104">Customers are often faced with the challenge of verifying the security posture of their infrastructure.</span><span class="sxs-lookup"><span data-stu-id="b847f-104">Customers are often faced with the challenge of verifying the security posture of their infrastructure.</span></span> <span data-ttu-id="b847f-105">This challenge is no different for their VMs in Azure.</span><span class="sxs-lookup"><span data-stu-id="b847f-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="b847f-106">It is important to have a similar security profile based on the Network Security Group (NSG) rules applied.</span><span class="sxs-lookup"><span data-stu-id="b847f-106">It is important to have a similar security profile based on the Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="b847f-107">Using the Security Group View, you can now get the list of rules applied to a VM within an NSG.</span><span class="sxs-lookup"><span data-stu-id="b847f-107">Using the Security Group View, you can now get the list of rules applied to a VM within an NSG.</span></span> <span data-ttu-id="b847f-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare the output to the golden profile and create a report.</span><span class="sxs-lookup"><span data-stu-id="b847f-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare the output to the golden profile and create a report.</span></span> <span data-ttu-id="b847f-109">This way you can identify with ease all the VMs that do not conform to the prescribed security profile.</span><span class="sxs-lookup"><span data-stu-id="b847f-109">This way you can identify with ease all the VMs that do not conform to the prescribed security profile.</span></span>

<span data-ttu-id="b847f-110">If you are unfamiliar with Network Security Groups, see [Network Security Overview](../virtual-network/security-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b847f-110">If you are unfamiliar with Network Security Groups, see [Network Security Overview](../virtual-network/security-overview.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b847f-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="b847f-111">Before you begin</span></span>

<span data-ttu-id="b847f-112">In this scenario, you compare a known good baseline to the security group view results returned for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b847f-112">In this scenario, you compare a known good baseline to the security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="b847f-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="b847f-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="b847f-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span><span class="sxs-lookup"><span data-stu-id="b847f-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="b847f-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="b847f-115">Scenario</span></span>

<span data-ttu-id="b847f-116">The scenario covered in this article gets the security group view for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b847f-116">The scenario covered in this article gets the security group view for a virtual machine.</span></span>

<span data-ttu-id="b847f-117">In this scenario, you will:</span><span class="sxs-lookup"><span data-stu-id="b847f-117">In this scenario, you will:</span></span>

- <span data-ttu-id="b847f-118">Retrieve a known good rule set</span><span class="sxs-lookup"><span data-stu-id="b847f-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="b847f-119">Retrieve a virtual machine with Rest API</span><span class="sxs-lookup"><span data-stu-id="b847f-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="b847f-120">Get security group view for virtual machine</span><span class="sxs-lookup"><span data-stu-id="b847f-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="b847f-121">Evaluate Response</span><span class="sxs-lookup"><span data-stu-id="b847f-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="b847f-122">Retrieve rule set</span><span class="sxs-lookup"><span data-stu-id="b847f-122">Retrieve rule set</span></span>

<span data-ttu-id="b847f-123">The first step in this example is to work with an existing baseline.</span><span class="sxs-lookup"><span data-stu-id="b847f-123">The first step in this example is to work with an existing baseline.</span></span> <span data-ttu-id="b847f-124">The following example is some json extracted from an existing Network Security Group using the `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as the baseline for this example.</span><span class="sxs-lookup"><span data-stu-id="b847f-124">The following example is some json extracted from an existing Network Security Group using the `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as the baseline for this example.</span></span>

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-to-powershell-objects"></a><span data-ttu-id="b847f-125">Convert rule set to PowerShell objects</span><span class="sxs-lookup"><span data-stu-id="b847f-125">Convert rule set to PowerShell objects</span></span>

<span data-ttu-id="b847f-126">In this step, we are reading a json file that was created earlier with the rules that are expected to be on the Network Security Group for this example.</span><span class="sxs-lookup"><span data-stu-id="b847f-126">In this step, we are reading a json file that was created earlier with the rules that are expected to be on the Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="b847f-127">Retrieve Network Watcher</span><span class="sxs-lookup"><span data-stu-id="b847f-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="b847f-128">The next step is to retrieve the Network Watcher instance.</span><span class="sxs-lookup"><span data-stu-id="b847f-128">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="b847f-129">The `$networkWatcher` variable is passed to the `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b847f-129">The `$networkWatcher` variable is passed to the `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="b847f-130">Get a VM</span><span class="sxs-lookup"><span data-stu-id="b847f-130">Get a VM</span></span>

<span data-ttu-id="b847f-131">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span><span class="sxs-lookup"><span data-stu-id="b847f-131">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="b847f-132">The following example gets a VM object.</span><span class="sxs-lookup"><span data-stu-id="b847f-132">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="b847f-133">Retrieve security group view</span><span class="sxs-lookup"><span data-stu-id="b847f-133">Retrieve security group view</span></span>

<span data-ttu-id="b847f-134">The next step is to retrieve the security group view result.</span><span class="sxs-lookup"><span data-stu-id="b847f-134">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="b847f-135">This result is compared to the "baseline" json that was shown earlier.</span><span class="sxs-lookup"><span data-stu-id="b847f-135">This result is compared to the "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-the-results"></a><span data-ttu-id="b847f-136">Analyzing the results</span><span class="sxs-lookup"><span data-stu-id="b847f-136">Analyzing the results</span></span>

<span data-ttu-id="b847f-137">The response is grouped by Network interfaces.</span><span class="sxs-lookup"><span data-stu-id="b847f-137">The response is grouped by Network interfaces.</span></span> <span data-ttu-id="b847f-138">The different types of rules returned are effective and default security rules.</span><span class="sxs-lookup"><span data-stu-id="b847f-138">The different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="b847f-139">The result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span><span class="sxs-lookup"><span data-stu-id="b847f-139">The result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="b847f-140">The following PowerShell script compares the results of the Security Group View to an existing output of an NSG.</span><span class="sxs-lookup"><span data-stu-id="b847f-140">The following PowerShell script compares the results of the Security Group View to an existing output of an NSG.</span></span> <span data-ttu-id="b847f-141">The following example is a simple example of how the results can be compared with `Compare-Object` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b847f-141">The following example is a simple example of how the results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="b847f-142">The following example is the result.</span><span class="sxs-lookup"><span data-stu-id="b847f-142">The following example is the result.</span></span> <span data-ttu-id="b847f-143">You can see two of the rules that were in the first rule set were not present in the comparison.</span><span class="sxs-lookup"><span data-stu-id="b847f-143">You can see two of the rules that were in the first rule set were not present in the comparison.</span></span>

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a><span data-ttu-id="b847f-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="b847f-144">Next steps</span></span>

<span data-ttu-id="b847f-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/manage-network-security-group.md) to track down the network security group and security rules that are in question.</span><span class="sxs-lookup"><span data-stu-id="b847f-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/manage-network-security-group.md) to track down the network security group and security rules that are in question.</span></span>













