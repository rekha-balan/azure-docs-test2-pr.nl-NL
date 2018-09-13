---
title: Create Azure managed application with Azure CLI | Microsoft Docs
description: Shows how to create an Azure managed application that is intended for members of your organization.
services: managed-applications
author: tfitzmac
manager: timlt
ms.service: managed-applications
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.date: 04/13/2018
ms.author: tomfitz
ms.openlocfilehash: f84fdd421ec6857cd940108546a16eb47770c766
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868856"
---
# <a name="create-and-deploy-an-azure-managed-application-with-azure-cli"></a><span data-ttu-id="7257c-103">Create and deploy an Azure managed application with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7257c-103">Create and deploy an Azure managed application with Azure CLI</span></span>

<span data-ttu-id="7257c-104">This article provides an introduction to working with managed applications.</span><span class="sxs-lookup"><span data-stu-id="7257c-104">This article provides an introduction to working with managed applications.</span></span> <span data-ttu-id="7257c-105">You add a managed application definition to an internal catalog for users in your organization.</span><span class="sxs-lookup"><span data-stu-id="7257c-105">You add a managed application definition to an internal catalog for users in your organization.</span></span> <span data-ttu-id="7257c-106">Then, you deploy that managed application to your subscription.</span><span class="sxs-lookup"><span data-stu-id="7257c-106">Then, you deploy that managed application to your subscription.</span></span> <span data-ttu-id="7257c-107">To simplify the introduction, we have already built the files for your managed application.</span><span class="sxs-lookup"><span data-stu-id="7257c-107">To simplify the introduction, we have already built the files for your managed application.</span></span> <span data-ttu-id="7257c-108">One file defines the infrastructure for your solution.</span><span class="sxs-lookup"><span data-stu-id="7257c-108">One file defines the infrastructure for your solution.</span></span> <span data-ttu-id="7257c-109">A second file that defines the user interface for deploying the managed application through the portal.</span><span class="sxs-lookup"><span data-stu-id="7257c-109">A second file that defines the user interface for deploying the managed application through the portal.</span></span> <span data-ttu-id="7257c-110">Those files are available through GitHub.</span><span class="sxs-lookup"><span data-stu-id="7257c-110">Those files are available through GitHub.</span></span> <span data-ttu-id="7257c-111">You learn how to build those files in the [Create service catalog application](publish-service-catalog-app.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="7257c-111">You learn how to build those files in the [Create service catalog application](publish-service-catalog-app.md) tutorial.</span></span>

<span data-ttu-id="7257c-112">When you are finished, you have three resource groups containing different parts of the managed application.</span><span class="sxs-lookup"><span data-stu-id="7257c-112">When you are finished, you have three resource groups containing different parts of the managed application.</span></span>

| <span data-ttu-id="7257c-113">Resource group</span><span class="sxs-lookup"><span data-stu-id="7257c-113">Resource group</span></span> | <span data-ttu-id="7257c-114">Contains</span><span class="sxs-lookup"><span data-stu-id="7257c-114">Contains</span></span> | <span data-ttu-id="7257c-115">Description</span><span class="sxs-lookup"><span data-stu-id="7257c-115">Description</span></span> |
| -------------- | -------- | ----------- |
| <span data-ttu-id="7257c-116">appDefinitionGroup</span><span class="sxs-lookup"><span data-stu-id="7257c-116">appDefinitionGroup</span></span> | <span data-ttu-id="7257c-117">The managed application definition.</span><span class="sxs-lookup"><span data-stu-id="7257c-117">The managed application definition.</span></span> | <span data-ttu-id="7257c-118">The publisher creates this resource group and the managed application definition.</span><span class="sxs-lookup"><span data-stu-id="7257c-118">The publisher creates this resource group and the managed application definition.</span></span> <span data-ttu-id="7257c-119">Anyone with access to the managed application definition can deploy it.</span><span class="sxs-lookup"><span data-stu-id="7257c-119">Anyone with access to the managed application definition can deploy it.</span></span> |
| <span data-ttu-id="7257c-120">applicationGroup</span><span class="sxs-lookup"><span data-stu-id="7257c-120">applicationGroup</span></span> | <span data-ttu-id="7257c-121">The managed application instance.</span><span class="sxs-lookup"><span data-stu-id="7257c-121">The managed application instance.</span></span> | <span data-ttu-id="7257c-122">The consumer creates this resource group and the managed application instance.</span><span class="sxs-lookup"><span data-stu-id="7257c-122">The consumer creates this resource group and the managed application instance.</span></span> <span data-ttu-id="7257c-123">The consumer can update the managed application through this instance.</span><span class="sxs-lookup"><span data-stu-id="7257c-123">The consumer can update the managed application through this instance.</span></span> |
| <span data-ttu-id="7257c-124">infrastructureGroup</span><span class="sxs-lookup"><span data-stu-id="7257c-124">infrastructureGroup</span></span> | <span data-ttu-id="7257c-125">The resources for the managed application.</span><span class="sxs-lookup"><span data-stu-id="7257c-125">The resources for the managed application.</span></span> | <span data-ttu-id="7257c-126">This resource group is automatically created when the managed application is created.</span><span class="sxs-lookup"><span data-stu-id="7257c-126">This resource group is automatically created when the managed application is created.</span></span> <span data-ttu-id="7257c-127">The publisher has access to this resource group to manage the application.</span><span class="sxs-lookup"><span data-stu-id="7257c-127">The publisher has access to this resource group to manage the application.</span></span> <span data-ttu-id="7257c-128">The consumer has limited access to the resource group.</span><span class="sxs-lookup"><span data-stu-id="7257c-128">The consumer has limited access to the resource group.</span></span> |

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-resource-group-for-definition"></a><span data-ttu-id="7257c-129">Create a resource group for definition</span><span class="sxs-lookup"><span data-stu-id="7257c-129">Create a resource group for definition</span></span>

<span data-ttu-id="7257c-130">Your managed application definition exists in a resource group.</span><span class="sxs-lookup"><span data-stu-id="7257c-130">Your managed application definition exists in a resource group.</span></span> <span data-ttu-id="7257c-131">The resource group is a logical collection into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="7257c-131">The resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="7257c-132">To create a resource group, use the following command:</span><span class="sxs-lookup"><span data-stu-id="7257c-132">To create a resource group, use the following command:</span></span>

```azurecli-interactive
az group create --name appDefinitionGroup --location westcentralus
```

## <a name="create-the-managed-application-definition"></a><span data-ttu-id="7257c-133">Create the managed application definition</span><span class="sxs-lookup"><span data-stu-id="7257c-133">Create the managed application definition</span></span>

<span data-ttu-id="7257c-134">When defining the managed application, you select a user, group, or application that manages the resources on behalf of the consumer.</span><span class="sxs-lookup"><span data-stu-id="7257c-134">When defining the managed application, you select a user, group, or application that manages the resources on behalf of the consumer.</span></span> <span data-ttu-id="7257c-135">This identity has permissions on the managed resource group according to the role that is assigned.</span><span class="sxs-lookup"><span data-stu-id="7257c-135">This identity has permissions on the managed resource group according to the role that is assigned.</span></span> <span data-ttu-id="7257c-136">Typically, you create an Azure Active Directory group to manage the resources.</span><span class="sxs-lookup"><span data-stu-id="7257c-136">Typically, you create an Azure Active Directory group to manage the resources.</span></span> <span data-ttu-id="7257c-137">However, for this article, use your own identity.</span><span class="sxs-lookup"><span data-stu-id="7257c-137">However, for this article, use your own identity.</span></span>

<span data-ttu-id="7257c-138">To get the object ID of your identity, provide your user principal name in the following command:</span><span class="sxs-lookup"><span data-stu-id="7257c-138">To get the object ID of your identity, provide your user principal name in the following command:</span></span>

```azurecli-interactive
userid=$(az ad user show --upn-or-object-id example@contoso.org --query objectId --output tsv)
```

<span data-ttu-id="7257c-139">Next, you need the role definition ID of the RBAC built-in role you want to grant access to the user.</span><span class="sxs-lookup"><span data-stu-id="7257c-139">Next, you need the role definition ID of the RBAC built-in role you want to grant access to the user.</span></span> <span data-ttu-id="7257c-140">The following command shows how to get the role definition ID for the Owner role:</span><span class="sxs-lookup"><span data-stu-id="7257c-140">The following command shows how to get the role definition ID for the Owner role:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

<span data-ttu-id="7257c-141">Now, create the managed application definition resource.</span><span class="sxs-lookup"><span data-stu-id="7257c-141">Now, create the managed application definition resource.</span></span> <span data-ttu-id="7257c-142">The managed application contains only a storage account.</span><span class="sxs-lookup"><span data-stu-id="7257c-142">The managed application contains only a storage account.</span></span>

```azurecli-interactive
az managedapp definition create \
  --name "ManagedStorage" \
  --location "westcentralus" \
  --resource-group appDefinitionGroup \
  --lock-level ReadOnly \
  --display-name "Managed Storage Account" \
  --description "Managed Azure Storage Account" \
  --authorizations "$userid:$roleid" \
  --package-file-uri "https://raw.githubusercontent.com/Azure/azure-managedapp-samples/master/samples/201-managed-storage-account/managedstorage.zip"
```

<span data-ttu-id="7257c-143">When the command completes, you have a managed application definition in your resource group.</span><span class="sxs-lookup"><span data-stu-id="7257c-143">When the command completes, you have a managed application definition in your resource group.</span></span> 

<span data-ttu-id="7257c-144">Some of the parameters used in the preceding example are:</span><span class="sxs-lookup"><span data-stu-id="7257c-144">Some of the parameters used in the preceding example are:</span></span>

* <span data-ttu-id="7257c-145">**resource-group**: The name of the resource group where the managed application definition is created.</span><span class="sxs-lookup"><span data-stu-id="7257c-145">**resource-group**: The name of the resource group where the managed application definition is created.</span></span>
* <span data-ttu-id="7257c-146">**lock-level**: The type of lock placed on the managed resource group.</span><span class="sxs-lookup"><span data-stu-id="7257c-146">**lock-level**: The type of lock placed on the managed resource group.</span></span> <span data-ttu-id="7257c-147">It prevents the customer from performing undesirable operations on this resource group.</span><span class="sxs-lookup"><span data-stu-id="7257c-147">It prevents the customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="7257c-148">Currently, ReadOnly is the only supported lock level.</span><span class="sxs-lookup"><span data-stu-id="7257c-148">Currently, ReadOnly is the only supported lock level.</span></span> <span data-ttu-id="7257c-149">When ReadOnly is specified, the customer can only read the resources present in the managed resource group.</span><span class="sxs-lookup"><span data-stu-id="7257c-149">When ReadOnly is specified, the customer can only read the resources present in the managed resource group.</span></span> <span data-ttu-id="7257c-150">The publisher identities that are granted access to the managed resource group are exempt from the lock.</span><span class="sxs-lookup"><span data-stu-id="7257c-150">The publisher identities that are granted access to the managed resource group are exempt from the lock.</span></span>
* <span data-ttu-id="7257c-151">**authorizations**: Describes the principal ID and the role definition ID that are used to grant permission to the managed resource group.</span><span class="sxs-lookup"><span data-stu-id="7257c-151">**authorizations**: Describes the principal ID and the role definition ID that are used to grant permission to the managed resource group.</span></span> <span data-ttu-id="7257c-152">It's specified in the format of `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="7257c-152">It's specified in the format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="7257c-153">Multiple values also can be specified for this property.</span><span class="sxs-lookup"><span data-stu-id="7257c-153">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="7257c-154">If multiple values are needed, they should be specified in the form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="7257c-154">If multiple values are needed, they should be specified in the form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="7257c-155">Multiple values are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="7257c-155">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="7257c-156">**package-file-uri**: The location of a .zip package that contains the required files.</span><span class="sxs-lookup"><span data-stu-id="7257c-156">**package-file-uri**: The location of a .zip package that contains the required files.</span></span> <span data-ttu-id="7257c-157">At a minimum, the package contains the **mainTemplate.json** and **createUiDefinition.json** files.</span><span class="sxs-lookup"><span data-stu-id="7257c-157">At a minimum, the package contains the **mainTemplate.json** and **createUiDefinition.json** files.</span></span> <span data-ttu-id="7257c-158">**mainTemplate.json** defines the Azure resources that are provisioned as part of the managed application.</span><span class="sxs-lookup"><span data-stu-id="7257c-158">**mainTemplate.json** defines the Azure resources that are provisioned as part of the managed application.</span></span> <span data-ttu-id="7257c-159">The template is no different than a regular Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="7257c-159">The template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="7257c-160">**createUiDefinition.json** generates the user interface for users who create the managed application through the portal.</span><span class="sxs-lookup"><span data-stu-id="7257c-160">**createUiDefinition.json** generates the user interface for users who create the managed application through the portal.</span></span>

## <a name="create-resource-group-for-managed-application"></a><span data-ttu-id="7257c-161">Create resource group for managed application</span><span class="sxs-lookup"><span data-stu-id="7257c-161">Create resource group for managed application</span></span>

<span data-ttu-id="7257c-162">Now, you are ready to deploy the managed application.</span><span class="sxs-lookup"><span data-stu-id="7257c-162">Now, you are ready to deploy the managed application.</span></span> 

<span data-ttu-id="7257c-163">To contain the deployed managed application, you need a resource group.</span><span class="sxs-lookup"><span data-stu-id="7257c-163">To contain the deployed managed application, you need a resource group.</span></span> <span data-ttu-id="7257c-164">Use **westcentralus** for the location.</span><span class="sxs-lookup"><span data-stu-id="7257c-164">Use **westcentralus** for the location.</span></span>

```azurecli-interactive
az group create --name applicationGroup --location westcentralus
```

## <a name="deploy-the-managed-application"></a><span data-ttu-id="7257c-165">Deploy the managed application</span><span class="sxs-lookup"><span data-stu-id="7257c-165">Deploy the managed application</span></span>

<span data-ttu-id="7257c-166">You deploy the application with the following commands:</span><span class="sxs-lookup"><span data-stu-id="7257c-166">You deploy the application with the following commands:</span></span>

```azurecli-interactive
appid=$(az managedapp definition show --name ManagedStorage --resource-group appDefinitionGroup --query id --output tsv)
subid=$(az account show --query id --output tsv)
managedGroupId=/subscriptions/$subid/resourceGroups/infrastructureGroup

az managedapp create \
  --name storageApp \
  --location "westcentralus" \
  --kind "Servicecatalog" \
  --resource-group applicationGroup \
  --managedapp-definition-id $appid \
  --managed-rg-id $managedGroupId \
  --parameters "{\"storageAccountNamePrefix\": {\"value\": \"storage\"}, \"storageAccountType\": {\"value\": \"Standard_LRS\"}}"
```

<span data-ttu-id="7257c-167">Some of the parameters used in the preceding example are:</span><span class="sxs-lookup"><span data-stu-id="7257c-167">Some of the parameters used in the preceding example are:</span></span>

* <span data-ttu-id="7257c-168">**managedapp-definition-id**: The ID of the definition you created earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="7257c-168">**managedapp-definition-id**: The ID of the definition you created earlier in this article.</span></span>
* <span data-ttu-id="7257c-169">**managed-rg-id**: The ID of the resource group for the resources associated with the managed application.</span><span class="sxs-lookup"><span data-stu-id="7257c-169">**managed-rg-id**: The ID of the resource group for the resources associated with the managed application.</span></span> <span data-ttu-id="7257c-170">The command creates this resource group.</span><span class="sxs-lookup"><span data-stu-id="7257c-170">The command creates this resource group.</span></span> <span data-ttu-id="7257c-171">It **must not exist prior to running the command**.</span><span class="sxs-lookup"><span data-stu-id="7257c-171">It **must not exist prior to running the command**.</span></span> <span data-ttu-id="7257c-172">This resource group is managed by the publisher.</span><span class="sxs-lookup"><span data-stu-id="7257c-172">This resource group is managed by the publisher.</span></span> 
* <span data-ttu-id="7257c-173">**resource-group**: The resource group where the managed application resource is created.</span><span class="sxs-lookup"><span data-stu-id="7257c-173">**resource-group**: The resource group where the managed application resource is created.</span></span>
* <span data-ttu-id="7257c-174">**parameters**: The parameters that are needed for the resources associated with the managed application.</span><span class="sxs-lookup"><span data-stu-id="7257c-174">**parameters**: The parameters that are needed for the resources associated with the managed application.</span></span>

<span data-ttu-id="7257c-175">After the deployment finishes successfully, you see the managed application is created in applicationGroup.</span><span class="sxs-lookup"><span data-stu-id="7257c-175">After the deployment finishes successfully, you see the managed application is created in applicationGroup.</span></span> <span data-ttu-id="7257c-176">The storageAccount resource is created in infrastructureGroup.</span><span class="sxs-lookup"><span data-stu-id="7257c-176">The storageAccount resource is created in infrastructureGroup.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7257c-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="7257c-177">Next steps</span></span>

* <span data-ttu-id="7257c-178">For an introduction to managed applications, see [Managed application overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="7257c-178">For an introduction to managed applications, see [Managed application overview](overview.md).</span></span>
* <span data-ttu-id="7257c-179">For examples of the files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="7257c-179">For examples of the files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="7257c-180">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7257c-180">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
