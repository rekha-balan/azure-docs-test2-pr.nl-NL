---
title: Manage resources with the Azure CLI | Microsoft Docs
description: Use the Azure Command-Line Interface (CLI) to manage Azure resources and groups
editor: ''
manager: timlt
documentationcenter: ''
author: tfitzmac
services: azure-resource-manager
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: conceptual
ms.date: 10/06/2017
ms.author: tomfitz
ms.openlocfilehash: dd111c33cbd348a05ed0f0c04f7325347612e54d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868910"
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a><span data-ttu-id="fa917-103">Use the Azure CLI to manage Azure resources and resource groups</span><span class="sxs-lookup"><span data-stu-id="fa917-103">Use the Azure CLI to manage Azure resources and resource groups</span></span>

<span data-ttu-id="fa917-104">In this article, you learn how to manage your solutions with Azure CLI and Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa917-104">In this article, you learn how to manage your solutions with Azure CLI and Azure Resource Manager.</span></span> <span data-ttu-id="fa917-105">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fa917-105">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="fa917-106">This article focuses on management tasks.</span><span class="sxs-lookup"><span data-stu-id="fa917-106">This article focuses on management tasks.</span></span> <span data-ttu-id="fa917-107">You will:</span><span class="sxs-lookup"><span data-stu-id="fa917-107">You will:</span></span>

1. <span data-ttu-id="fa917-108">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="fa917-108">Create a resource group</span></span>
2. <span data-ttu-id="fa917-109">Add a resource to the resource group</span><span class="sxs-lookup"><span data-stu-id="fa917-109">Add a resource to the resource group</span></span>
3. <span data-ttu-id="fa917-110">Add a tag to the resource</span><span class="sxs-lookup"><span data-stu-id="fa917-110">Add a tag to the resource</span></span>
4. <span data-ttu-id="fa917-111">Query resources based on names or tag values</span><span class="sxs-lookup"><span data-stu-id="fa917-111">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="fa917-112">Apply and remove a lock on the resource</span><span class="sxs-lookup"><span data-stu-id="fa917-112">Apply and remove a lock on the resource</span></span>
6. <span data-ttu-id="fa917-113">Delete a resource group</span><span class="sxs-lookup"><span data-stu-id="fa917-113">Delete a resource group</span></span>

<span data-ttu-id="fa917-114">This article does not show how to deploy a Resource Manager template to your subscription.</span><span class="sxs-lookup"><span data-stu-id="fa917-114">This article does not show how to deploy a Resource Manager template to your subscription.</span></span> <span data-ttu-id="fa917-115">For that information, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fa917-115">For that information, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fa917-116">To install and use the CLI locally, see [Install Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fa917-116">To install and use the CLI locally, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="set-subscription"></a><span data-ttu-id="fa917-117">Set subscription</span><span class="sxs-lookup"><span data-stu-id="fa917-117">Set subscription</span></span>

<span data-ttu-id="fa917-118">If you have more than one subscription, you can switch to a different subscription.</span><span class="sxs-lookup"><span data-stu-id="fa917-118">If you have more than one subscription, you can switch to a different subscription.</span></span> <span data-ttu-id="fa917-119">First, let's see all the subscriptions for your account.</span><span class="sxs-lookup"><span data-stu-id="fa917-119">First, let's see all the subscriptions for your account.</span></span>

```azurecli-interactive
az account list
```

<span data-ttu-id="fa917-120">It returns a list of your enabled and disabled subscriptions.</span><span class="sxs-lookup"><span data-stu-id="fa917-120">It returns a list of your enabled and disabled subscriptions.</span></span>

```json
[
  {
    "cloudName": "AzureCloud",
    "id": "<guid>",
    "isDefault": true,
    "name": "Example Subscription One",
    "registeredProviders": [],
    "state": "Enabled",
    "tenantId": "<guid>",
    "user": {
      "name": "example@contoso.org",
      "type": "user"
    }
  },
  ...
]
```

<span data-ttu-id="fa917-121">Notice that one subscription is marked as the default.</span><span class="sxs-lookup"><span data-stu-id="fa917-121">Notice that one subscription is marked as the default.</span></span> <span data-ttu-id="fa917-122">This subscription is your current context for operations.</span><span class="sxs-lookup"><span data-stu-id="fa917-122">This subscription is your current context for operations.</span></span> <span data-ttu-id="fa917-123">To switch to a different subscription, provide the subscription name with the **az account set** command.</span><span class="sxs-lookup"><span data-stu-id="fa917-123">To switch to a different subscription, provide the subscription name with the **az account set** command.</span></span>

```azurecli-interactive
az account set -s "Example Subscription Two"
```

<span data-ttu-id="fa917-124">To show the current subscription context, use **az account show** without a parameter:</span><span class="sxs-lookup"><span data-stu-id="fa917-124">To show the current subscription context, use **az account show** without a parameter:</span></span>

```azurecli-interactive
az account show
```

## <a name="create-a-resource-group"></a><span data-ttu-id="fa917-125">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="fa917-125">Create a resource group</span></span>

<span data-ttu-id="fa917-126">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span><span class="sxs-lookup"><span data-stu-id="fa917-126">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span></span>

<span data-ttu-id="fa917-127">To create a resource group, use the **az group create** command.</span><span class="sxs-lookup"><span data-stu-id="fa917-127">To create a resource group, use the **az group create** command.</span></span> <span data-ttu-id="fa917-128">The command uses the **name** parameter to specify a name for the resource group and the **location** parameter to specify its location.</span><span class="sxs-lookup"><span data-stu-id="fa917-128">The command uses the **name** parameter to specify a name for the resource group and the **location** parameter to specify its location.</span></span>

```azurecli-interactive
az group create --name TestRG1 --location "South Central US"
```

<span data-ttu-id="fa917-129">The output is in the following format:</span><span class="sxs-lookup"><span data-stu-id="fa917-129">The output is in the following format:</span></span>

```json
{
  "id": "/subscriptions/<subscription-id>/resourceGroups/TestRG1",
  "location": "southcentralus",
  "managedBy": null,
  "name": "TestRG1",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

<span data-ttu-id="fa917-130">If you need to retrieve the resource group later, use the following command:</span><span class="sxs-lookup"><span data-stu-id="fa917-130">If you need to retrieve the resource group later, use the following command:</span></span>

```azurecli-interactive
az group show --name TestRG1
```

<span data-ttu-id="fa917-131">To get all the resource groups in your subscription, use:</span><span class="sxs-lookup"><span data-stu-id="fa917-131">To get all the resource groups in your subscription, use:</span></span>

```azurecli-interactive
az group list
```

## <a name="add-resources-to-a-resource-group"></a><span data-ttu-id="fa917-132">Add resources to a resource group</span><span class="sxs-lookup"><span data-stu-id="fa917-132">Add resources to a resource group</span></span>

<span data-ttu-id="fa917-133">To add a resource to the resource group, you can use the **az resource create** command or a command that is specific to the type of resource you are creating (like **az storage account create**).</span><span class="sxs-lookup"><span data-stu-id="fa917-133">To add a resource to the resource group, you can use the **az resource create** command or a command that is specific to the type of resource you are creating (like **az storage account create**).</span></span> <span data-ttu-id="fa917-134">You might find it easier to use a command that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span><span class="sxs-lookup"><span data-stu-id="fa917-134">You might find it easier to use a command that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span></span> <span data-ttu-id="fa917-135">To use **az resource create**, you must know all the properties to set without being prompted for them.</span><span class="sxs-lookup"><span data-stu-id="fa917-135">To use **az resource create**, you must know all the properties to set without being prompted for them.</span></span>

<span data-ttu-id="fa917-136">However, adding a resource through script might cause future confusion because the new resource does not exist in a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="fa917-136">However, adding a resource through script might cause future confusion because the new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="fa917-137">Templates enable you to reliably and repeatedly deploy your solution.</span><span class="sxs-lookup"><span data-stu-id="fa917-137">Templates enable you to reliably and repeatedly deploy your solution.</span></span>

<span data-ttu-id="fa917-138">The following command creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="fa917-138">The following command creates a storage account.</span></span> <span data-ttu-id="fa917-139">Instead of using the name shown in the example, provide a unique name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="fa917-139">Instead of using the name shown in the example, provide a unique name for the storage account.</span></span> <span data-ttu-id="fa917-140">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span><span class="sxs-lookup"><span data-stu-id="fa917-140">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="fa917-141">If you use the name shown in the example, you receive an error because that name is already in use.</span><span class="sxs-lookup"><span data-stu-id="fa917-141">If you use the name shown in the example, you receive an error because that name is already in use.</span></span>

```azurecli-interactive
az storage account create -n myuniquestorage -g TestRG1 -l westus --sku Standard_LRS
```

<span data-ttu-id="fa917-142">If you need to retrieve this resource later, use the following command:</span><span class="sxs-lookup"><span data-stu-id="fa917-142">If you need to retrieve this resource later, use the following command:</span></span>

```azurecli-interactive
az storage account show --name myuniquestorage --resource-group TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="fa917-143">Add a tag</span><span class="sxs-lookup"><span data-stu-id="fa917-143">Add a tag</span></span>

<span data-ttu-id="fa917-144">Tags enable you to organize your resources according to different properties.</span><span class="sxs-lookup"><span data-stu-id="fa917-144">Tags enable you to organize your resources according to different properties.</span></span> <span data-ttu-id="fa917-145">For example, you may have several resources in different resource groups that belong to the same department.</span><span class="sxs-lookup"><span data-stu-id="fa917-145">For example, you may have several resources in different resource groups that belong to the same department.</span></span> <span data-ttu-id="fa917-146">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span><span class="sxs-lookup"><span data-stu-id="fa917-146">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span></span> <span data-ttu-id="fa917-147">Or, you can mark whether a resource is used in a production or test environment.</span><span class="sxs-lookup"><span data-stu-id="fa917-147">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="fa917-148">In this article, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span><span class="sxs-lookup"><span data-stu-id="fa917-148">In this article, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span></span>

<span data-ttu-id="fa917-149">The following command applies two tags to your storage account:</span><span class="sxs-lookup"><span data-stu-id="fa917-149">The following command applies two tags to your storage account:</span></span>

```azurecli-interactive
az resource tag --tags Dept=IT Environment=Test -g TestRG1 -n myuniquestorage --resource-type "Microsoft.Storage/storageAccounts"
```

<span data-ttu-id="fa917-150">Tags are updated as a single object.</span><span class="sxs-lookup"><span data-stu-id="fa917-150">Tags are updated as a single object.</span></span> <span data-ttu-id="fa917-151">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span><span class="sxs-lookup"><span data-stu-id="fa917-151">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span></span> <span data-ttu-id="fa917-152">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span><span class="sxs-lookup"><span data-stu-id="fa917-152">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span></span>

```azurecli-interactive
jsonrtag=$(az resource show -g TestRG1 -n myuniquestorage --resource-type "Microsoft.Storage/storageAccounts" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g TestRG1 -n myuniquestorage --resource-type "Microsoft.Storage/storageAccounts"
```

## <a name="search-for-resources"></a><span data-ttu-id="fa917-153">Search for resources</span><span class="sxs-lookup"><span data-stu-id="fa917-153">Search for resources</span></span>

<span data-ttu-id="fa917-154">Use the **az resource list** command to retrieve resources for different search conditions.</span><span class="sxs-lookup"><span data-stu-id="fa917-154">Use the **az resource list** command to retrieve resources for different search conditions.</span></span>

* <span data-ttu-id="fa917-155">To get a resource by name, provide the **name** parameter:</span><span class="sxs-lookup"><span data-stu-id="fa917-155">To get a resource by name, provide the **name** parameter:</span></span>

  ```azurecli-interactive
  az resource list -n myuniquestorage
  ```

* <span data-ttu-id="fa917-156">To get all the resources in a resource group, provide the **resource-group** parameter:</span><span class="sxs-lookup"><span data-stu-id="fa917-156">To get all the resources in a resource group, provide the **resource-group** parameter:</span></span>

  ```azurecli-interactive
  az resource list --resource-group TestRG1
  ```

* <span data-ttu-id="fa917-157">To get all the resources with a tag name and value, provide the **tag** parameter:</span><span class="sxs-lookup"><span data-stu-id="fa917-157">To get all the resources with a tag name and value, provide the **tag** parameter:</span></span>

  ```azurecli-interactive
  az resource list --tag Dept=IT
  ```

* <span data-ttu-id="fa917-158">To all the resources with a particular resource type, provide the **resource-type** parameter:</span><span class="sxs-lookup"><span data-stu-id="fa917-158">To all the resources with a particular resource type, provide the **resource-type** parameter:</span></span>

  ```azurecli-interactive
  az resource list --resource-type "Microsoft.Storage/storageAccounts"
  ```

## <a name="get-resource-id"></a><span data-ttu-id="fa917-159">Get resource ID</span><span class="sxs-lookup"><span data-stu-id="fa917-159">Get resource ID</span></span>

<span data-ttu-id="fa917-160">Many commands take a resource ID as a parameter.</span><span class="sxs-lookup"><span data-stu-id="fa917-160">Many commands take a resource ID as a parameter.</span></span> <span data-ttu-id="fa917-161">To get the ID for a resource and store in a variable, use:</span><span class="sxs-lookup"><span data-stu-id="fa917-161">To get the ID for a resource and store in a variable, use:</span></span>

```azurecli-interactive
webappID=$(az resource show -g exampleGroup -n exampleSite --resource-type "Microsoft.Web/sites" --query id --output tsv)
```

## <a name="lock-a-resource"></a><span data-ttu-id="fa917-162">Lock a resource</span><span class="sxs-lookup"><span data-stu-id="fa917-162">Lock a resource</span></span>

<span data-ttu-id="fa917-163">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span><span class="sxs-lookup"><span data-stu-id="fa917-163">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span></span> <span data-ttu-id="fa917-164">You can specify either a **CanNotDelete** or **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="fa917-164">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="fa917-165">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span><span class="sxs-lookup"><span data-stu-id="fa917-165">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="fa917-166">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span><span class="sxs-lookup"><span data-stu-id="fa917-166">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="fa917-167">To apply a lock, use the following command:</span><span class="sxs-lookup"><span data-stu-id="fa917-167">To apply a lock, use the following command:</span></span>

```azurecli-interactive
az lock create --lock-type CanNotDelete --resource-name myuniquestorage --resource-group TestRG1 --resource-type Microsoft.Storage/storageAccounts --name storagelock
```

<span data-ttu-id="fa917-168">The locked resource in the preceding example cannot be deleted until the lock is removed.</span><span class="sxs-lookup"><span data-stu-id="fa917-168">The locked resource in the preceding example cannot be deleted until the lock is removed.</span></span> <span data-ttu-id="fa917-169">To remove a lock, use:</span><span class="sxs-lookup"><span data-stu-id="fa917-169">To remove a lock, use:</span></span>

```azurecli-interactive
az lock delete --name storagelock --resource-group TestRG1 --resource-type Microsoft.Storage/storageAccounts --resource-name myuniquestorage
```

<span data-ttu-id="fa917-170">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="fa917-170">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="fa917-171">Remove resources or resource group</span><span class="sxs-lookup"><span data-stu-id="fa917-171">Remove resources or resource group</span></span>
<span data-ttu-id="fa917-172">You can remove a resource or resource group.</span><span class="sxs-lookup"><span data-stu-id="fa917-172">You can remove a resource or resource group.</span></span> <span data-ttu-id="fa917-173">When you remove a resource group, you also remove all the resources within that resource group.</span><span class="sxs-lookup"><span data-stu-id="fa917-173">When you remove a resource group, you also remove all the resources within that resource group.</span></span>

* <span data-ttu-id="fa917-174">To delete a resource from the resource group, use the delete command for the resource type you are deleting.</span><span class="sxs-lookup"><span data-stu-id="fa917-174">To delete a resource from the resource group, use the delete command for the resource type you are deleting.</span></span> <span data-ttu-id="fa917-175">The command deletes the resource, but does not delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="fa917-175">The command deletes the resource, but does not delete the resource group.</span></span>

  ```azurecli-interactive
  az storage account delete -n myuniquestorage -g TestRG1
  ```

* <span data-ttu-id="fa917-176">To delete a resource group and all its resources, use the **az group delete** command.</span><span class="sxs-lookup"><span data-stu-id="fa917-176">To delete a resource group and all its resources, use the **az group delete** command.</span></span>

  ```azurecli-interactive
  az group delete -n TestRG1
  ```

<span data-ttu-id="fa917-177">For both commands, you are asked to confirm that you wish to remove the resource or resource group.</span><span class="sxs-lookup"><span data-stu-id="fa917-177">For both commands, you are asked to confirm that you wish to remove the resource or resource group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa917-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="fa917-178">Next steps</span></span>
* <span data-ttu-id="fa917-179">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fa917-179">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="fa917-180">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fa917-180">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="fa917-181">You can move existing resources to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="fa917-181">You can move existing resources to a new resource group.</span></span> <span data-ttu-id="fa917-182">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="fa917-182">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="fa917-183">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance).</span><span class="sxs-lookup"><span data-stu-id="fa917-183">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance).</span></span>