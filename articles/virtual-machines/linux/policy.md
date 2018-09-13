---
title: Enforce security with policies on Linux VMs in Azure | Microsoft Docs
description: How to apply a policy to an Azure Resource Manager Linux Virtual Machine
services: virtual-machines-linux
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/13/2016
ms.author: singhkay
ms.openlocfilehash: bde2bcc335db33301fa474331043086b8b282052
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563079"
---
# <a name="apply-security-and-policies-to-linux-vms-with-azure-resource-manager"></a>Apply security and policies to Linux VMs with Azure Resource Manager
By using policies, an organization can enforce various conventions and rules throughout the enterprise. Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization. In this article, we will describe how you can use Azure Resource Manager policies to define the desired behavior for your organization’s Virtual Machines.

The outline for the steps to accomplish this is as below

1. Azure Resource Manager Policy 101
2. Define a policy for your Virtual Machine
3. Create the policy
4. Apply the policy

## <a name="azure-resource-manager-policy-101"></a>Azure Resource Manager Policy 101
For getting started with Azure Resource Manager policies, we recommend reading the article below and then continuing with the steps in this article. The article below describes the basic definition and structure of a policy, how policies get evaluated and gives various examples of policy definitions.

* [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md)

## <a name="define-a-policy-for-your-virtual-machine"></a>Define a policy for your Virtual Machine
One of the common scenarios for an enterprise might be to only allow their users to create Virtual Machines from specific operating systems that have been tested to be compatible with a LOB application. Using an Azure Resource Manager policy this task can be accomplished in a few steps.
In this policy example, we are going to allow only Ubuntu 14.04.2-LTS Virtual Machines to be created. The policy definition looks like below

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
            "equals": "Canonical"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/imageOffer",
            "equals": "UbuntuServer"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/imageSku",
            "equals": "14.04.2-LTS"
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

The above policy can easily be modified to a scenario where you might want to allow any Ubuntu LTS image to be used for a Virtual Machine deployment with the below change

```
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

#### <a name="virtual-machine-property-fields"></a>Virtual Machine Property Fields
The table below describes the Virtual Machine properties that can be used as fields in your policy definition. For more information about policy fields, see [Use policy to manage resources and control access](../../resource-manager-policy.md).

| Field Name | Description |
| --- | --- |
| imagePublisher |Specifies the publisher of the image |
| imageOffer |Specifies the offer for the chosen image publisher |
| imageSku |Specifies the SKU for the chosen offer |
| imageVersion |Specifies the image version for the chosen SKU |

## <a name="create-the-policy"></a>Create the Policy
A policy can easily be created using the REST API directly or the PowerShell cmdlets. You can read more about [creating and assigning a policy](../../resource-manager-policy.md).

## <a name="apply-the-policy"></a>Apply the Policy
After creating the policy you’ll need to apply it on a defined scope. The scope can be a subscription, resource group or even the resource. You can read more about [creating and assigning a policy](../../resource-manager-policy.md).
