---
title: RequestDisallowedByPolicy error with Azure resource policy | Microsoft Docs
description: Describes the cause of the RequestDisallowedByPolicy error.
services: azure-resource-manager
documentationcenter: ''
author: genlin
manager: cshepard
editor: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 03/09/2018
ms.author: genli
ms.openlocfilehash: a9993942c20f2c33d944b74fb124a363d0663ced
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865316"
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>RequestDisallowedByPolicy error with Azure resource policy

This article describes the cause of the RequestDisallowedByPolicy error, it also provides solution for this error.

## <a name="symptom"></a>Symptom

During deployment, you might receive a **RequestDisallowedByPolicy** error that prevents you from creating the resources. The following example shows the error:

```json
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>Troubleshooting

To retrieve details about the policy that blocked your deployment, use the following one of the methods:

### <a name="powershell"></a>PowerShell

In PowerShell, provide that policy identifier as the `Id` parameter to retrieve details about the policy that blocked your deployment.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="azure-cli"></a>Azure CLI

In Azure CLI, provide the name of the policy definition:

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>Solution

For security or compliance, your subscription administrators might assign policies that limit how resources are deployed. For example, your subscription might have a policy that prevents creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables. The error message in the **Symptoms** section shows the name of the policy.
To resolve this problem, review the resource policies, and determine how to deploy resources that comply with those policies.

For more information, see the following articles:

- [What is Azure Policy?](../azure-policy/azure-policy-introduction.md)
- [Create and manage policies to enforce compliance](../azure-policy/create-manage-policy.md)