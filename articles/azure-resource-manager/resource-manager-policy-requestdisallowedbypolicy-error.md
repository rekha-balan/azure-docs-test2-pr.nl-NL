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
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="4696f-103">RequestDisallowedByPolicy error with Azure resource policy</span><span class="sxs-lookup"><span data-stu-id="4696f-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="4696f-104">This article describes the cause of the RequestDisallowedByPolicy error, it also provides solution for this error.</span><span class="sxs-lookup"><span data-stu-id="4696f-104">This article describes the cause of the RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="4696f-105">Symptom</span><span class="sxs-lookup"><span data-stu-id="4696f-105">Symptom</span></span>

<span data-ttu-id="4696f-106">During deployment, you might receive a **RequestDisallowedByPolicy** error that prevents you from creating the resources.</span><span class="sxs-lookup"><span data-stu-id="4696f-106">During deployment, you might receive a **RequestDisallowedByPolicy** error that prevents you from creating the resources.</span></span> <span data-ttu-id="4696f-107">The following example shows the error:</span><span class="sxs-lookup"><span data-stu-id="4696f-107">The following example shows the error:</span></span>

```json
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="4696f-108">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="4696f-108">Troubleshooting</span></span>

<span data-ttu-id="4696f-109">To retrieve details about the policy that blocked your deployment, use the following one of the methods:</span><span class="sxs-lookup"><span data-stu-id="4696f-109">To retrieve details about the policy that blocked your deployment, use the following one of the methods:</span></span>

### <a name="powershell"></a><span data-ttu-id="4696f-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4696f-110">PowerShell</span></span>

<span data-ttu-id="4696f-111">In PowerShell, provide that policy identifier as the `Id` parameter to retrieve details about the policy that blocked your deployment.</span><span class="sxs-lookup"><span data-stu-id="4696f-111">In PowerShell, provide that policy identifier as the `Id` parameter to retrieve details about the policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="azure-cli"></a><span data-ttu-id="4696f-112">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4696f-112">Azure CLI</span></span>

<span data-ttu-id="4696f-113">In Azure CLI, provide the name of the policy definition:</span><span class="sxs-lookup"><span data-stu-id="4696f-113">In Azure CLI, provide the name of the policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="4696f-114">Solution</span><span class="sxs-lookup"><span data-stu-id="4696f-114">Solution</span></span>

<span data-ttu-id="4696f-115">For security or compliance, your subscription administrators might assign policies that limit how resources are deployed.</span><span class="sxs-lookup"><span data-stu-id="4696f-115">For security or compliance, your subscription administrators might assign policies that limit how resources are deployed.</span></span> <span data-ttu-id="4696f-116">For example, your subscription might have a policy that prevents creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span><span class="sxs-lookup"><span data-stu-id="4696f-116">For example, your subscription might have a policy that prevents creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="4696f-117">The error message in the **Symptoms** section shows the name of the policy.</span><span class="sxs-lookup"><span data-stu-id="4696f-117">The error message in the **Symptoms** section shows the name of the policy.</span></span>
<span data-ttu-id="4696f-118">To resolve this problem, review the resource policies, and determine how to deploy resources that comply with those policies.</span><span class="sxs-lookup"><span data-stu-id="4696f-118">To resolve this problem, review the resource policies, and determine how to deploy resources that comply with those policies.</span></span>

<span data-ttu-id="4696f-119">For more information, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="4696f-119">For more information, see the following articles:</span></span>

- [<span data-ttu-id="4696f-120">What is Azure Policy?</span><span class="sxs-lookup"><span data-stu-id="4696f-120">What is Azure Policy?</span></span>](../azure-policy/azure-policy-introduction.md)
- [<span data-ttu-id="4696f-121">Create and manage policies to enforce compliance</span><span class="sxs-lookup"><span data-stu-id="4696f-121">Create and manage policies to enforce compliance</span></span>](../azure-policy/create-manage-policy.md)
