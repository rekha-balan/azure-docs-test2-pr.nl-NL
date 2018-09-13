---
title: Azure quota errors | Microsoft Docs
description: Describes how to resolve resource qouta errors.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 03/09/2018
ms.author: tomfitz
ms.openlocfilehash: 6d9048ae531abedb89b70989ce1c962357c514cd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966044"
---
# <a name="resolve-errors-for-resource-quotas"></a><span data-ttu-id="0e604-103">Resolve errors for resource quotas</span><span class="sxs-lookup"><span data-stu-id="0e604-103">Resolve errors for resource quotas</span></span>

<span data-ttu-id="0e604-104">This article describes quota errors you may encounter when deploying resources.</span><span class="sxs-lookup"><span data-stu-id="0e604-104">This article describes quota errors you may encounter when deploying resources.</span></span>

## <a name="symptom"></a><span data-ttu-id="0e604-105">Symptom</span><span class="sxs-lookup"><span data-stu-id="0e604-105">Symptom</span></span>

<span data-ttu-id="0e604-106">If you deploy a template that creates resources that exceed your Azure quotas, you get a deployment error that looks like:</span><span class="sxs-lookup"><span data-stu-id="0e604-106">If you deploy a template that creates resources that exceed your Azure quotas, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="0e604-107">Or, you may see:</span><span class="sxs-lookup"><span data-stu-id="0e604-107">Or, you may see:</span></span>

```
Code=ResourceQuotaExceeded
Message=Creating the resource of type <resource-type> would exceed the quota of <number>
resources of type <resource-type> per resource group. The current resource count is <number>,
please delete some resources of this type before creating a new one.
```

## <a name="cause"></a><span data-ttu-id="0e604-108">Cause</span><span class="sxs-lookup"><span data-stu-id="0e604-108">Cause</span></span>

<span data-ttu-id="0e604-109">Quotas are applied per resource group, subscriptions, accounts, and other scopes.</span><span class="sxs-lookup"><span data-stu-id="0e604-109">Quotas are applied per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="0e604-110">For example, your subscription may be configured to limit the number of cores for a region.</span><span class="sxs-lookup"><span data-stu-id="0e604-110">For example, your subscription may be configured to limit the number of cores for a region.</span></span> <span data-ttu-id="0e604-111">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span><span class="sxs-lookup"><span data-stu-id="0e604-111">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span></span>
<span data-ttu-id="0e604-112">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="0e604-112">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0e604-113">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="0e604-113">Troubleshooting</span></span>

### <a name="azure-cli"></a><span data-ttu-id="0e604-114">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0e604-114">Azure CLI</span></span>

<span data-ttu-id="0e604-115">For Azure CLI, use the `az vm list-usage` command to find virtual machine quotas.</span><span class="sxs-lookup"><span data-stu-id="0e604-115">For Azure CLI, use the `az vm list-usage` command to find virtual machine quotas.</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="0e604-116">Which returns:</span><span class="sxs-lookup"><span data-stu-id="0e604-116">Which returns:</span></span>

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

### <a name="powershell"></a><span data-ttu-id="0e604-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e604-117">PowerShell</span></span>

<span data-ttu-id="0e604-118">For PowerShell, use the **Get-AzureRmVMUsage** command to find virtual machine quotas.</span><span class="sxs-lookup"><span data-stu-id="0e604-118">For PowerShell, use the **Get-AzureRmVMUsage** command to find virtual machine quotas.</span></span>

```powershell
Get-AzureRmVMUsage -Location "South Central US"
```

<span data-ttu-id="0e604-119">Which returns:</span><span class="sxs-lookup"><span data-stu-id="0e604-119">Which returns:</span></span>

```powershell
Name                             Current Value Limit  Unit
----                             ------------- -----  ----
Availability Sets                            0  2000 Count
Total Regional Cores                         0   100 Count
Virtual Machines                             0 10000 Count
```

## <a name="solution"></a><span data-ttu-id="0e604-120">Solution</span><span class="sxs-lookup"><span data-stu-id="0e604-120">Solution</span></span>

<span data-ttu-id="0e604-121">To request a quota increase, go to the portal and file a support issue.</span><span class="sxs-lookup"><span data-stu-id="0e604-121">To request a quota increase, go to the portal and file a support issue.</span></span> <span data-ttu-id="0e604-122">In the support issue, request an increase in your quota for the region into which you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="0e604-122">In the support issue, request an increase in your quota for the region into which you want to deploy.</span></span>

> [!NOTE]
> <span data-ttu-id="0e604-123">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span><span class="sxs-lookup"><span data-stu-id="0e604-123">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span></span> <span data-ttu-id="0e604-124">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span><span class="sxs-lookup"><span data-stu-id="0e604-124">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="0e604-125">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span><span class="sxs-lookup"><span data-stu-id="0e604-125">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

1. <span data-ttu-id="0e604-126">Select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="0e604-126">Select **Subscriptions**.</span></span>

   ![Subscriptions](./media/resource-manager-quota-errors/subscriptions.png)

2. <span data-ttu-id="0e604-128">Select the subscription that needs an increased quota.</span><span class="sxs-lookup"><span data-stu-id="0e604-128">Select the subscription that needs an increased quota.</span></span>

   ![Select subscription](./media/resource-manager-quota-errors/select-subscription.png)

3. <span data-ttu-id="0e604-130">Select **Usage + quotas**</span><span class="sxs-lookup"><span data-stu-id="0e604-130">Select **Usage + quotas**</span></span>

   ![Select usage and quotas](./media/resource-manager-quota-errors/select-usage-quotas.png)

4. <span data-ttu-id="0e604-132">In the upper right corner, select **Request increase**.</span><span class="sxs-lookup"><span data-stu-id="0e604-132">In the upper right corner, select **Request increase**.</span></span>

   ![Request increase](./media/resource-manager-quota-errors/request-increase.png)

5. <span data-ttu-id="0e604-134">Fill in the forms for the type of quota you need to increase.</span><span class="sxs-lookup"><span data-stu-id="0e604-134">Fill in the forms for the type of quota you need to increase.</span></span>

   ![Fill in form](./media/resource-manager-quota-errors/forms.png)