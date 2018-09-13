---
title: Enforce security with policies on Windows VMs in Azure | Microsoft Docs
description: How to apply a policy to an Azure Resource Manager Windows Virtual Machine
services: virtual-machines-windows
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 0b71ba54-01db-43ad-9bca-8ab358ae141b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 04/13/2016
ms.author: kasing
ms.openlocfilehash: 6c91d47b11fa18ead0076c470930e8c4e5537784
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553791"
---
# <a name="apply-security-and-policies-to-windows-vms-with-azure-resource-manager"></a>Apply security and policies to Windows VMs with Azure Resource Manager
By using policies, an organization can enforce various conventions and rules throughout the enterprise. Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization. In this article, we will describe how you can use Azure Resource Manager policies to define the desired behavior for your organization’s Virtual Machines.

The outline for the steps to accomplish this is as below

1. Azure Resource Manager Policy 101
2. Define a policy for your Virtual Machine
3. Create the policy
4. Apply the policy

## <a name="azure-resource-manager-policy-101"></a>Azure Resource Manager Policy 101
For getting started with Azure Resource Manager policies, we recommend reading the article below and then continuing with the steps in this article. The article below describes the basic definition and structure of a policy, how policies get evaluated and gives various examples of policy definitions.

* [Use Policy to manage resources and control access](../../resource-manager-policy.md)

## <a name="define-a-policy-for-your-virtual-machine"></a>Define a policy for your Virtual Machine
One of the common scenarios for an enterprise might be to only allow their users to create Virtual Machines from specific operating systems that have been tested to be compatible with a LOB application. Using an Azure Resource Manager policy this task can be accomplished in a few steps.
In this policy example, we are going to allow only Windows Server 2012 R2 Datacenter Virtual Machines to be created. The policy definition looks like below

```
"if": {
  "allOf": [
    {
      "field": "type",
      "equals": "Microsoft.Compute/virtualMachines"
    },
    {
      "not": {
        "allOf": [
          {
            "field": "Microsoft.Compute/virtualMachines/imagePublisher",
            "equals": "MicrosoftWindowsServer"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/imageOffer",
            "equals": "WindowsServer"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/imageSku",
            "equals": "2012-R2-Datacenter"
          }
        ]
      }
    }
  ]
},
"then": {
  "effect": "deny"
}
```

The above policy can easily be modified to a scenario where you might want to allow any Windows Server Datacenter image to be used for a Virtual Machine deployment with the below change

```
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*Datacenter"
}
```

#### <a name="virtual-machine-property-fields"></a>Virtual Machine Property Fields
The table below describes the Virtual Machine properties that can be used as fields in your policy definition. For more on policy fields, see the article below:

* [Fields and Sources](../../azure-resource-manager/resource-manager-policy.md#conditions)

| Field Name | Description |
| --- | --- |
| imagePublisher |Specifies the publisher of the image |
| imageOffer |Specifies the offer for the chosen image publisher |
| imageSku |Specifies the SKU for the chosen offer |
| imageVersion |Specifies the image version for the chosen SKU |

## <a name="create-the-policy"></a>Create the Policy
A policy can easily be created using the REST API directly or the PowerShell cmdlets. For creating the policy, see the article below:

* [Creating a Policy](../../resource-manager-policy.md)

## <a name="apply-the-policy"></a>Apply the Policy
After creating the policy you’ll need to apply it on a defined scope. The scope can be a subscription, resource group or even the resource. For applying the policy, see the article below:

* [Creating a Policy](../../resource-manager-policy.md)
