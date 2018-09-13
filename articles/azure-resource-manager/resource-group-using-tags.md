---
title: Tag Azure resources for logical organization | Microsoft Docs
description: Shows how to apply tags to organize Azure resources for billing and managing.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: tomfitz
ms.openlocfilehash: 4665349a71c3ba1c7606c92d640d4c2302e252ca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660647"
---
# <a name="use-tags-to-organize-your-azure-resources"></a><span data-ttu-id="f94ed-103">Use tags to organize your Azure resources</span><span class="sxs-lookup"><span data-stu-id="f94ed-103">Use tags to organize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="f94ed-104">You can only apply tags to resources that support Resource Manager operations.</span><span class="sxs-lookup"><span data-stu-id="f94ed-104">You can only apply tags to resources that support Resource Manager operations.</span></span> <span data-ttu-id="f94ed-105">If you created a Virtual Machine, Virtual Network, or Storage through the classic deployment model (such as through the classic portal), you cannot apply a tag to that resource.</span><span class="sxs-lookup"><span data-stu-id="f94ed-105">If you created a Virtual Machine, Virtual Network, or Storage through the classic deployment model (such as through the classic portal), you cannot apply a tag to that resource.</span></span> <span data-ttu-id="f94ed-106">To support tagging, redeploy these resources through Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f94ed-106">To support tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="f94ed-107">All other resources support tagging.</span><span class="sxs-lookup"><span data-stu-id="f94ed-107">All other resources support tagging.</span></span>
> 
> 

## <a name="ensure-tag-consistency-with-policies"></a><span data-ttu-id="f94ed-108">Ensure tag consistency with policies</span><span class="sxs-lookup"><span data-stu-id="f94ed-108">Ensure tag consistency with policies</span></span>

<span data-ttu-id="f94ed-109">Resource policies enable you to create standard rules for your organization.</span><span class="sxs-lookup"><span data-stu-id="f94ed-109">Resource policies enable you to create standard rules for your organization.</span></span> <span data-ttu-id="f94ed-110">You can create policies that ensure resources are tagged with the appropriate values.</span><span class="sxs-lookup"><span data-stu-id="f94ed-110">You can create policies that ensure resources are tagged with the appropriate values.</span></span> <span data-ttu-id="f94ed-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="f94ed-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="templates"></a><span data-ttu-id="f94ed-112">Templates</span><span class="sxs-lookup"><span data-stu-id="f94ed-112">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="f94ed-113">Portal</span><span class="sxs-lookup"><span data-stu-id="f94ed-113">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="powershell"></a><span data-ttu-id="f94ed-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f94ed-114">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli-20"></a><span data-ttu-id="f94ed-115">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f94ed-115">Azure CLI 2.0</span></span>

<span data-ttu-id="f94ed-116">With Azure CLI 2.0, you can add tags to resources and resource group, and query resources by tag values.</span><span class="sxs-lookup"><span data-stu-id="f94ed-116">With Azure CLI 2.0, you can add tags to resources and resource group, and query resources by tag values.</span></span>

<span data-ttu-id="f94ed-117">Every time you apply tags to a resource or resource group, you overwrite the existing tags on that resource or resource group.</span><span class="sxs-lookup"><span data-stu-id="f94ed-117">Every time you apply tags to a resource or resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="f94ed-118">Therefore, you must use a different approach based on whether the resource or resource group has existing tags that you want to preserve.</span><span class="sxs-lookup"><span data-stu-id="f94ed-118">Therefore, you must use a different approach based on whether the resource or resource group has existing tags that you want to preserve.</span></span> <span data-ttu-id="f94ed-119">To add tags to a:</span><span class="sxs-lookup"><span data-stu-id="f94ed-119">To add tags to a:</span></span>

* <span data-ttu-id="f94ed-120">resource group without existing tags.</span><span class="sxs-lookup"><span data-stu-id="f94ed-120">resource group without existing tags.</span></span>

  ```azurecli
  az group update -n TagTestGroup --set tags.Environment=Test tags.Dept=IT
  ```

* <span data-ttu-id="f94ed-121">resource without existing tags.</span><span class="sxs-lookup"><span data-stu-id="f94ed-121">resource without existing tags.</span></span>

  ```azurecli
  az resource tag --tags Dept=IT Environment=Test -g TagTestGroup -n storageexample --resource-type "Microsoft.Storage/storageAccounts"
  ``` 

<span data-ttu-id="f94ed-122">To add tags to a resource that already has tags, first retrieve the existing tags:</span><span class="sxs-lookup"><span data-stu-id="f94ed-122">To add tags to a resource that already has tags, first retrieve the existing tags:</span></span> 

```azurecli
az resource show --query tags --output list -g TagTestGroup -n storageexample --resource-type "Microsoft.Storage/storageAccounts"
```

<span data-ttu-id="f94ed-123">Which returns the following format:</span><span class="sxs-lookup"><span data-stu-id="f94ed-123">Which returns the following format:</span></span>

```
Dept        : Finance
Environment : Test
```

<span data-ttu-id="f94ed-124">Reapply the existing tags to the resource, and add the new tags.</span><span class="sxs-lookup"><span data-stu-id="f94ed-124">Reapply the existing tags to the resource, and add the new tags.</span></span>

```azurecli
az resource tag --tags Dept=Finance Environment=Test CostCenter=IT -g TagTestGroup -n storageexample --resource-type "Microsoft.Storage/storageAccounts"
``` 

<span data-ttu-id="f94ed-125">To get resource groups with a specific tag, use `az group list`.</span><span class="sxs-lookup"><span data-stu-id="f94ed-125">To get resource groups with a specific tag, use `az group list`.</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="f94ed-126">To get all the resources with a particular tag and value, use `az resource list`.</span><span class="sxs-lookup"><span data-stu-id="f94ed-126">To get all the resources with a particular tag and value, use `az resource list`.</span></span>

```azurecli
az resource list --tag Dept=Finance
```

## <a name="azure-cli-10"></a><span data-ttu-id="f94ed-127">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f94ed-127">Azure CLI 1.0</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="rest-api"></a><span data-ttu-id="f94ed-128">REST API</span><span class="sxs-lookup"><span data-stu-id="f94ed-128">REST API</span></span>
<span data-ttu-id="f94ed-129">The portal and PowerShell both use the [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind the scenes.</span><span class="sxs-lookup"><span data-stu-id="f94ed-129">The portal and PowerShell both use the [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind the scenes.</span></span> <span data-ttu-id="f94ed-130">If you need to integrate tagging into another environment, you can get tags with a GET on the resource id and update the set of tags with a PATCH call.</span><span class="sxs-lookup"><span data-stu-id="f94ed-130">If you need to integrate tagging into another environment, you can get tags with a GET on the resource id and update the set of tags with a PATCH call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="f94ed-131">Tags and billing</span><span class="sxs-lookup"><span data-stu-id="f94ed-131">Tags and billing</span></span>
<span data-ttu-id="f94ed-132">Tags enable you to group your billing data.</span><span class="sxs-lookup"><span data-stu-id="f94ed-132">Tags enable you to group your billing data.</span></span> <span data-ttu-id="f94ed-133">For example, if you are running multiple VMs for different organizations, use the tags to group usage by cost center.</span><span class="sxs-lookup"><span data-stu-id="f94ed-133">For example, if you are running multiple VMs for different organizations, use the tags to group usage by cost center.</span></span> <span data-ttu-id="f94ed-134">You can also use tags to categorize costs by runtime environment; such as, the billing usage for VMs running in production environment.</span><span class="sxs-lookup"><span data-stu-id="f94ed-134">You can also use tags to categorize costs by runtime environment; such as, the billing usage for VMs running in production environment.</span></span>


<span data-ttu-id="f94ed-135">You can retrieve information about tags through the [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or the usage comma-separated values (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="f94ed-135">You can retrieve information about tags through the [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or the usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="f94ed-136">You download the usage file from the [Azure accounts portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f94ed-136">You download the usage file from the [Azure accounts portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="f94ed-137">For more information about programmatic access to billing information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f94ed-137">For more information about programmatic access to billing information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="f94ed-138">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span><span class="sxs-lookup"><span data-stu-id="f94ed-138">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="f94ed-139">When you download the usage CSV for services that support tags with billing, the tags appear in the **Tags** column.</span><span class="sxs-lookup"><span data-stu-id="f94ed-139">When you download the usage CSV for services that support tags with billing, the tags appear in the **Tags** column.</span></span> <span data-ttu-id="f94ed-140">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="f94ed-140">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![See tags in billing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="f94ed-142">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f94ed-142">Next Steps</span></span>
* <span data-ttu-id="f94ed-143">You can apply restrictions and conventions across your subscription with customized policies.</span><span class="sxs-lookup"><span data-stu-id="f94ed-143">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="f94ed-144">The policy you define could require that all resources have a value for a particular tag.</span><span class="sxs-lookup"><span data-stu-id="f94ed-144">The policy you define could require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="f94ed-145">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="f94ed-145">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="f94ed-146">For an introduction to using Azure PowerShell when deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f94ed-146">For an introduction to using Azure PowerShell when deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="f94ed-147">For an introduction to using Azure CLI when deploying resources, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f94ed-147">For an introduction to using Azure CLI when deploying resources, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="f94ed-148">For an introduction to using the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f94ed-148">For an introduction to using the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md)</span></span>  
* <span data-ttu-id="f94ed-149">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f94ed-149">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>


