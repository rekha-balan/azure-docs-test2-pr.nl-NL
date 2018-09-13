---
title: include file
description: include file
services: azure-resource-manager
author: tfitzmac
ms.service: azure-resource-manager
ms.topic: include
ms.date: 02/20/2018
ms.author: tomfitz
ms.custom: include file
ms.openlocfilehash: b9484336add0719749e9f0af56bdd70fa3906ef5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869758"
---
<span data-ttu-id="4f12e-103">To add two tags to a resource group, use the [az group update](/cli/azure/group#az_group_update) command:</span><span class="sxs-lookup"><span data-stu-id="4f12e-103">To add two tags to a resource group, use the [az group update](/cli/azure/group#az_group_update) command:</span></span>

```azurecli-interactive
az group update -n myResourceGroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="4f12e-104">Let's suppose you want to add a third tag.</span><span class="sxs-lookup"><span data-stu-id="4f12e-104">Let's suppose you want to add a third tag.</span></span> <span data-ttu-id="4f12e-105">Run the command again with the new tag.</span><span class="sxs-lookup"><span data-stu-id="4f12e-105">Run the command again with the new tag.</span></span> <span data-ttu-id="4f12e-106">It is appended to the existing tags.</span><span class="sxs-lookup"><span data-stu-id="4f12e-106">It is appended to the existing tags.</span></span>

```azurecli-interactive
az group update -n myResourceGroup --set tags.Project=Documentation
```

<span data-ttu-id="4f12e-107">Resources don't inherit tags from the resource group.</span><span class="sxs-lookup"><span data-stu-id="4f12e-107">Resources don't inherit tags from the resource group.</span></span> <span data-ttu-id="4f12e-108">Currently, your resource group has three tags but the resources do not have any tags.</span><span class="sxs-lookup"><span data-stu-id="4f12e-108">Currently, your resource group has three tags but the resources do not have any tags.</span></span> <span data-ttu-id="4f12e-109">To apply all tags from a resource group to its resources, and retain existing tags on resources, use the following script:</span><span class="sxs-lookup"><span data-stu-id="4f12e-109">To apply all tags from a resource group to its resources, and retain existing tags on resources, use the following script:</span></span>

```azurecli-interactive
# Get the tags for the resource group
jsontag=$(az group show -n myResourceGroup --query tags)

# Reformat from JSON to space-delimited and equals sign
t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')

# Get the resource IDs for all resources in the resource group
r=$(az resource list -g myResourceGroup --query [].id --output tsv)

# Loop through each resource ID
for resid in $r
do
  # Get the tags for this resource
  jsonrtag=$(az resource show --id $resid --query tags)
  
  # Reformat from JSON to space-delimited and equals sign
  rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
  
  # Reapply the updated tags to this resource
  az resource tag --tags $t$rt --id $resid
done
```

<span data-ttu-id="4f12e-110">Alternatively, you can apply tags from the resource group to the resources without keeping the existing tags:</span><span class="sxs-lookup"><span data-stu-id="4f12e-110">Alternatively, you can apply tags from the resource group to the resources without keeping the existing tags:</span></span>

```azurecli-interactive
# Get the tags for the resource group
jsontag=$(az group show -n myResourceGroup --query tags)

# Reformat from JSON to space-delimited and equals sign
t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')

# Get the resource IDs for all resources in the resource group
r=$(az resource list -g myResourceGroup --query [].id --output tsv)

# Loop through each resource ID
for resid in $r
do
  # Apply tags from resource group to this resource
  az resource tag --tags $t --id $resid
done
```

<span data-ttu-id="4f12e-111">To combine several values in a single tag, use a JSON string.</span><span class="sxs-lookup"><span data-stu-id="4f12e-111">To combine several values in a single tag, use a JSON string.</span></span>

```azurecli-interactive
az group update -n myResourceGroup --set tags.CostCenter='{"Dept":"IT","Environment":"Test"}'
```

<span data-ttu-id="4f12e-112">To remove all tags on a resource group, use:</span><span class="sxs-lookup"><span data-stu-id="4f12e-112">To remove all tags on a resource group, use:</span></span>

```azurecli-interactive
az group update -n myResourceGroup --remove tags
```
