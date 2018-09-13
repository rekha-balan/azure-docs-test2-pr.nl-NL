---
title: Azure resource providers and resource types | Microsoft Docs
description: Describes the resource providers that support Resource Manager, their schemas and available API versions, and the regions that can host the resources.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 811bb40816339dbe7097e429722625a3ae5c95c0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44811673"
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="8d9fa-103">Resource providers and types</span><span class="sxs-lookup"><span data-stu-id="8d9fa-103">Resource providers and types</span></span>

<span data-ttu-id="8d9fa-104">When deploying resources, you frequently need to retrieve information about the resource providers and types.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-104">When deploying resources, you frequently need to retrieve information about the resource providers and types.</span></span> <span data-ttu-id="8d9fa-105">In this article, you learn to:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-105">In this article, you learn to:</span></span>

* <span data-ttu-id="8d9fa-106">View all resource providers in Azure</span><span class="sxs-lookup"><span data-stu-id="8d9fa-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="8d9fa-107">Check registration status of a resource provider</span><span class="sxs-lookup"><span data-stu-id="8d9fa-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="8d9fa-108">Register a resource provider</span><span class="sxs-lookup"><span data-stu-id="8d9fa-108">Register a resource provider</span></span>
* <span data-ttu-id="8d9fa-109">View resource types for a resource provider</span><span class="sxs-lookup"><span data-stu-id="8d9fa-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="8d9fa-110">View valid locations for a resource type</span><span class="sxs-lookup"><span data-stu-id="8d9fa-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="8d9fa-111">View valid API versions for a resource type</span><span class="sxs-lookup"><span data-stu-id="8d9fa-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="8d9fa-112">You can perform these steps through the portal, PowerShell, or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-112">You can perform these steps through the portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="8d9fa-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d9fa-113">PowerShell</span></span>

<span data-ttu-id="8d9fa-114">To see all resource providers in Azure, and the registration status for your subscription, use:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-114">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="8d9fa-115">Which returns results similar to:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="8d9fa-116">Registering a resource provider configures your subscription to work with the resource provider.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-116">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="8d9fa-117">The scope for registration is always the subscription.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-117">The scope for registration is always the subscription.</span></span> <span data-ttu-id="8d9fa-118">By default, many resource providers are automatically registered.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="8d9fa-119">However, you may need to manually register some resource providers.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-119">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="8d9fa-120">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-120">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="8d9fa-121">This operation is included in the Contributor and Owner roles.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-121">This operation is included in the Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="8d9fa-122">Which returns results similar to:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="8d9fa-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="8d9fa-124">To see information for a particular resource provider, use:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-124">To see information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="8d9fa-125">Which returns results similar to:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="8d9fa-126">To see the resource types for a resource provider, use:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-126">To see the resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="8d9fa-127">Which returns:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="8d9fa-128">The API version corresponds to a version of REST API operations that are released by the resource provider.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-128">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="8d9fa-129">As a resource provider enables new features, it releases a new version of the REST API.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-129">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="8d9fa-130">To get the available API versions for a resource type, use:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-130">To get the available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="8d9fa-131">Which returns:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="8d9fa-132">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-132">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="8d9fa-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="8d9fa-134">To get the supported locations for a resource type, use.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-134">To get the supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="8d9fa-135">Which returns:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="8d9fa-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8d9fa-136">Azure CLI</span></span>
<span data-ttu-id="8d9fa-137">To see all resource providers in Azure, and the registration status for your subscription, use:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-137">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="8d9fa-138">Which returns results similar to:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="8d9fa-139">Registering a resource provider configures your subscription to work with the resource provider.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-139">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="8d9fa-140">The scope for registration is always the subscription.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-140">The scope for registration is always the subscription.</span></span> <span data-ttu-id="8d9fa-141">By default, many resource providers are automatically registered.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="8d9fa-142">However, you may need to manually register some resource providers.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-142">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="8d9fa-143">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-143">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="8d9fa-144">This operation is included in the Contributor and Owner roles.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-144">This operation is included in the Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="8d9fa-145">Which returns a message that registration is on-going.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="8d9fa-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="8d9fa-147">To see information for a particular resource provider, use:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-147">To see information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="8d9fa-148">Which returns results similar to:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-148">Which returns results similar to:</span></span>

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

<span data-ttu-id="8d9fa-149">To see the resource types for a resource provider, use:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-149">To see the resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="8d9fa-150">Which returns:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="8d9fa-151">The API version corresponds to a version of REST API operations that are released by the resource provider.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-151">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="8d9fa-152">As a resource provider enables new features, it releases a new version of the REST API.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-152">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="8d9fa-153">To get the available API versions for a resource type, use:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-153">To get the available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="8d9fa-154">Which returns:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="8d9fa-155">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-155">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="8d9fa-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="8d9fa-157">To get the supported locations for a resource type, use.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-157">To get the supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="8d9fa-158">Which returns:</span><span class="sxs-lookup"><span data-stu-id="8d9fa-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="8d9fa-159">Portal</span><span class="sxs-lookup"><span data-stu-id="8d9fa-159">Portal</span></span>

<span data-ttu-id="8d9fa-160">To see all resource providers in Azure, and the registration status for your subscription, select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-160">To see all resource providers in Azure, and the registration status for your subscription, select **Subscriptions**.</span></span>

![select subscriptions](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="8d9fa-162">Choose the subscription to view.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-162">Choose the subscription to view.</span></span>

![specify subscription](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="8d9fa-164">Select **Resource providers** and view the list of available resource providers.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-164">Select **Resource providers** and view the list of available resource providers.</span></span>

![show resource providers](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="8d9fa-166">Registering a resource provider configures your subscription to work with the resource provider.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-166">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="8d9fa-167">The scope for registration is always the subscription.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-167">The scope for registration is always the subscription.</span></span> <span data-ttu-id="8d9fa-168">By default, many resource providers are automatically registered.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="8d9fa-169">However, you may need to manually register some resource providers.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-169">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="8d9fa-170">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-170">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="8d9fa-171">This operation is included in the Contributor and Owner roles.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-171">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="8d9fa-172">To register a resource provider, select **Register**.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-172">To register a resource provider, select **Register**.</span></span>

![register resource provider](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="8d9fa-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="8d9fa-175">To see information for a particular resource provider, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-175">To see information for a particular resource provider, select **All services**.</span></span>

![select All services](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="8d9fa-177">Search for **Resource Explorer** and select it from the available options.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-177">Search for **Resource Explorer** and select it from the available options.</span></span>

![select resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="8d9fa-179">Select **Providers**.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-179">Select **Providers**.</span></span>

![Select providers](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="8d9fa-181">Select the resource provider and resource type that you want to view.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-181">Select the resource provider and resource type that you want to view.</span></span>

![Select resource type](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="8d9fa-183">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-183">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="8d9fa-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> <span data-ttu-id="8d9fa-185">The resource explorer displays valid locations for the resource type.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-185">The resource explorer displays valid locations for the resource type.</span></span>

![Show locations](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="8d9fa-187">The API version corresponds to a version of REST API operations that are released by the resource provider.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-187">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="8d9fa-188">As a resource provider enables new features, it releases a new version of the REST API.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-188">As a resource provider enables new features, it releases a new version of the REST API.</span></span> <span data-ttu-id="8d9fa-189">The resource explorer displays valid API versions for the resource type.</span><span class="sxs-lookup"><span data-stu-id="8d9fa-189">The resource explorer displays valid API versions for the resource type.</span></span>

![Show API versions](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="8d9fa-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="8d9fa-191">Next steps</span></span>
* <span data-ttu-id="8d9fa-192">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8d9fa-192">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8d9fa-193">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8d9fa-193">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="8d9fa-194">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="8d9fa-194">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

