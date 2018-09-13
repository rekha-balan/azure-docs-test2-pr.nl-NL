---
title: Role-Based Access Control with REST - Azure AD | Microsoft Docs
description: Managing role-based access control with the REST API
services: active-directory
documentationcenter: na
author: kgremban
manager: femila
editor: ''
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: kgremban
ms.openlocfilehash: f63381e3349063ba9dd4ceb67d644c1d71d73369
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550946"
---
# <a name="manage-role-based-access-control-with-the-rest-api"></a><span data-ttu-id="e9262-103">Manage Role-Based Access Control with the REST API</span><span class="sxs-lookup"><span data-stu-id="e9262-103">Manage Role-Based Access Control with the REST API</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="e9262-107">Role-Based Access Control (RBAC) in the Azure Portal and Azure Resource Manager API helps you manage access to your subscription and resources at a fine-grained level.</span><span class="sxs-lookup"><span data-stu-id="e9262-107">Role-Based Access Control (RBAC) in the Azure Portal and Azure Resource Manager API helps you manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="e9262-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span><span class="sxs-lookup"><span data-stu-id="e9262-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="e9262-109">List all role assignments</span><span class="sxs-lookup"><span data-stu-id="e9262-109">List all role assignments</span></span>
<span data-ttu-id="e9262-110">Lists all the role assignments at the specified scope and subscopes.</span><span class="sxs-lookup"><span data-stu-id="e9262-110">Lists all the role assignments at the specified scope and subscopes.</span></span>

<span data-ttu-id="e9262-111">To list role assignments, you must have access to `Microsoft.Authorization/roleAssignments/read` operation at the scope.</span><span class="sxs-lookup"><span data-stu-id="e9262-111">To list role assignments, you must have access to `Microsoft.Authorization/roleAssignments/read` operation at the scope.</span></span> <span data-ttu-id="e9262-112">All the built-in roles are granted access to this operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-112">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="e9262-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e9262-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e9262-114">Request</span><span class="sxs-lookup"><span data-stu-id="e9262-114">Request</span></span>
<span data-ttu-id="e9262-115">Use the **GET** method with the following URI:</span><span class="sxs-lookup"><span data-stu-id="e9262-115">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="e9262-116">Within the URI, make the following substitutions to customize your request:</span><span class="sxs-lookup"><span data-stu-id="e9262-116">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e9262-117">Replace *{scope}* with the scope for which you wish to list the role assignments.</span><span class="sxs-lookup"><span data-stu-id="e9262-117">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="e9262-118">The following examples show how to specify the scope for different levels:</span><span class="sxs-lookup"><span data-stu-id="e9262-118">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e9262-119">Subscription: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="e9262-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e9262-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e9262-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e9262-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e9262-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e9262-122">Replace *{api-version}* with 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e9262-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="e9262-123">Replace *{filter}* with the condition that you wish to apply to filter the role assignment list:</span><span class="sxs-lookup"><span data-stu-id="e9262-123">Replace *{filter}* with the condition that you wish to apply to filter the role assignment list:</span></span>

   * <span data-ttu-id="e9262-124">List role assignments for only the specified scope, not including the role assignments at subscopes: `atScope()`</span><span class="sxs-lookup"><span data-stu-id="e9262-124">List role assignments for only the specified scope, not including the role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="e9262-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="e9262-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="e9262-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="e9262-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="e9262-127">Response</span><span class="sxs-lookup"><span data-stu-id="e9262-127">Response</span></span>
<span data-ttu-id="e9262-128">Status code: 200</span><span class="sxs-lookup"><span data-stu-id="e9262-128">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="e9262-129">Get information about a role assignment</span><span class="sxs-lookup"><span data-stu-id="e9262-129">Get information about a role assignment</span></span>
<span data-ttu-id="e9262-130">Gets information about a single role assignment specified by the role assignment identifier.</span><span class="sxs-lookup"><span data-stu-id="e9262-130">Gets information about a single role assignment specified by the role assignment identifier.</span></span>

<span data-ttu-id="e9262-131">To get information about a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/read` operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-131">To get information about a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="e9262-132">All the built-in roles are granted access to this operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-132">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="e9262-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e9262-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e9262-134">Request</span><span class="sxs-lookup"><span data-stu-id="e9262-134">Request</span></span>
<span data-ttu-id="e9262-135">Use the **GET** method with the following URI:</span><span class="sxs-lookup"><span data-stu-id="e9262-135">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="e9262-136">Within the URI, make the following substitutions to customize your request:</span><span class="sxs-lookup"><span data-stu-id="e9262-136">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e9262-137">Replace *{scope}* with the scope for which you wish to list the role assignments.</span><span class="sxs-lookup"><span data-stu-id="e9262-137">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="e9262-138">The following examples show how to specify the scope for different levels:</span><span class="sxs-lookup"><span data-stu-id="e9262-138">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e9262-139">Subscription: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="e9262-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e9262-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e9262-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e9262-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e9262-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e9262-142">Replace *{role-assignment-id}* with the GUID identifier of the role assignment.</span><span class="sxs-lookup"><span data-stu-id="e9262-142">Replace *{role-assignment-id}* with the GUID identifier of the role assignment.</span></span>
3. <span data-ttu-id="e9262-143">Replace *{api-version}* with 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e9262-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="e9262-144">Response</span><span class="sxs-lookup"><span data-stu-id="e9262-144">Response</span></span>
<span data-ttu-id="e9262-145">Status code: 200</span><span class="sxs-lookup"><span data-stu-id="e9262-145">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a><span data-ttu-id="e9262-146">Create a Role Assignment</span><span class="sxs-lookup"><span data-stu-id="e9262-146">Create a Role Assignment</span></span>
<span data-ttu-id="e9262-147">Create a role assignment at the specified scope for the specified principal granting the specified role.</span><span class="sxs-lookup"><span data-stu-id="e9262-147">Create a role assignment at the specified scope for the specified principal granting the specified role.</span></span>

<span data-ttu-id="e9262-148">To create a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/write` operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-148">To create a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="e9262-149">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-149">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="e9262-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e9262-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e9262-151">Request</span><span class="sxs-lookup"><span data-stu-id="e9262-151">Request</span></span>
<span data-ttu-id="e9262-152">Use the **PUT** method with the following URI:</span><span class="sxs-lookup"><span data-stu-id="e9262-152">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="e9262-153">Within the URI, make the following substitutions to customize your request:</span><span class="sxs-lookup"><span data-stu-id="e9262-153">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e9262-154">Replace *{scope}* with the scope at which you wish to create the role assignments.</span><span class="sxs-lookup"><span data-stu-id="e9262-154">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="e9262-155">When you create a role assignment at a parent scope, all child scopes inherit the same role assignment.</span><span class="sxs-lookup"><span data-stu-id="e9262-155">When you create a role assignment at a parent scope, all child scopes inherit the same role assignment.</span></span> <span data-ttu-id="e9262-156">The following examples show how to specify the scope for different levels:</span><span class="sxs-lookup"><span data-stu-id="e9262-156">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e9262-157">Subscription: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="e9262-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e9262-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e9262-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="e9262-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e9262-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e9262-160">Replace *{role-assignment-id}* with a new GUID, which becomes the GUID identifier of the new role assignment.</span><span class="sxs-lookup"><span data-stu-id="e9262-160">Replace *{role-assignment-id}* with a new GUID, which becomes the GUID identifier of the new role assignment.</span></span>
3. <span data-ttu-id="e9262-161">Replace *{api-version}* with 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e9262-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="e9262-162">For the request body, provide the values in the following format:</span><span class="sxs-lookup"><span data-stu-id="e9262-162">For the request body, provide the values in the following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="e9262-163">Element Name</span><span class="sxs-lookup"><span data-stu-id="e9262-163">Element Name</span></span> | <span data-ttu-id="e9262-164">Required</span><span class="sxs-lookup"><span data-stu-id="e9262-164">Required</span></span> | <span data-ttu-id="e9262-165">Type</span><span class="sxs-lookup"><span data-stu-id="e9262-165">Type</span></span> | <span data-ttu-id="e9262-166">Description</span><span class="sxs-lookup"><span data-stu-id="e9262-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e9262-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="e9262-167">roleDefinitionId</span></span> |<span data-ttu-id="e9262-168">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-168">Yes</span></span> |<span data-ttu-id="e9262-169">String</span><span class="sxs-lookup"><span data-stu-id="e9262-169">String</span></span> |<span data-ttu-id="e9262-170">The identifier of the role.</span><span class="sxs-lookup"><span data-stu-id="e9262-170">The identifier of the role.</span></span> <span data-ttu-id="e9262-171">The format of the identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="e9262-171">The format of the identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="e9262-172">principalId</span><span class="sxs-lookup"><span data-stu-id="e9262-172">principalId</span></span> |<span data-ttu-id="e9262-173">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-173">Yes</span></span> |<span data-ttu-id="e9262-174">String</span><span class="sxs-lookup"><span data-stu-id="e9262-174">String</span></span> |<span data-ttu-id="e9262-175">objectId of the Azure AD principal (user, group, or service principal) to which the role is assigned.</span><span class="sxs-lookup"><span data-stu-id="e9262-175">objectId of the Azure AD principal (user, group, or service principal) to which the role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="e9262-176">Response</span><span class="sxs-lookup"><span data-stu-id="e9262-176">Response</span></span>
<span data-ttu-id="e9262-177">Status code: 201</span><span class="sxs-lookup"><span data-stu-id="e9262-177">Status code: 201</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a><span data-ttu-id="e9262-178">Delete a Role Assignment</span><span class="sxs-lookup"><span data-stu-id="e9262-178">Delete a Role Assignment</span></span>
<span data-ttu-id="e9262-179">Delete a role assignment at the specified scope.</span><span class="sxs-lookup"><span data-stu-id="e9262-179">Delete a role assignment at the specified scope.</span></span>

<span data-ttu-id="e9262-180">To delete a role assignment, you must have access to the `Microsoft.Authorization/roleAssignments/delete` operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-180">To delete a role assignment, you must have access to the `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="e9262-181">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-181">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="e9262-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e9262-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e9262-183">Request</span><span class="sxs-lookup"><span data-stu-id="e9262-183">Request</span></span>
<span data-ttu-id="e9262-184">Use the **DELETE** method with the following URI:</span><span class="sxs-lookup"><span data-stu-id="e9262-184">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="e9262-185">Within the URI, make the following substitutions to customize your request:</span><span class="sxs-lookup"><span data-stu-id="e9262-185">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e9262-186">Replace *{scope}* with the scope at which you wish to create the role assignments.</span><span class="sxs-lookup"><span data-stu-id="e9262-186">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="e9262-187">The following examples show how to specify the scope for different levels:</span><span class="sxs-lookup"><span data-stu-id="e9262-187">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e9262-188">Subscription: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="e9262-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e9262-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e9262-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e9262-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e9262-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e9262-191">Replace *{role-assignment-id}* with the role assignment id GUID.</span><span class="sxs-lookup"><span data-stu-id="e9262-191">Replace *{role-assignment-id}* with the role assignment id GUID.</span></span>
3. <span data-ttu-id="e9262-192">Replace *{api-version}* with 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e9262-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="e9262-193">Response</span><span class="sxs-lookup"><span data-stu-id="e9262-193">Response</span></span>
<span data-ttu-id="e9262-194">Status code: 200</span><span class="sxs-lookup"><span data-stu-id="e9262-194">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a><span data-ttu-id="e9262-195">List all Roles</span><span class="sxs-lookup"><span data-stu-id="e9262-195">List all Roles</span></span>
<span data-ttu-id="e9262-196">Lists all the roles that are available for assignment at the specified scope.</span><span class="sxs-lookup"><span data-stu-id="e9262-196">Lists all the roles that are available for assignment at the specified scope.</span></span>

<span data-ttu-id="e9262-197">To list roles, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation at the scope.</span><span class="sxs-lookup"><span data-stu-id="e9262-197">To list roles, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation at the scope.</span></span> <span data-ttu-id="e9262-198">All the built-in roles are granted access to this operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-198">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="e9262-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e9262-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e9262-200">Request</span><span class="sxs-lookup"><span data-stu-id="e9262-200">Request</span></span>
<span data-ttu-id="e9262-201">Use the **GET** method with the following URI:</span><span class="sxs-lookup"><span data-stu-id="e9262-201">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="e9262-202">Within the URI, make the following substitutions to customize your request:</span><span class="sxs-lookup"><span data-stu-id="e9262-202">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e9262-203">Replace *{scope}* with the scope for which you wish to list the roles.</span><span class="sxs-lookup"><span data-stu-id="e9262-203">Replace *{scope}* with the scope for which you wish to list the roles.</span></span> <span data-ttu-id="e9262-204">The following examples show how to specify the scope for different levels:</span><span class="sxs-lookup"><span data-stu-id="e9262-204">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e9262-205">Subscription: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="e9262-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e9262-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e9262-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e9262-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e9262-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e9262-208">Replace *{api-version}* with 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e9262-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="e9262-209">Replace *{filter}* with the condition that you wish to apply to filter the list of roles:</span><span class="sxs-lookup"><span data-stu-id="e9262-209">Replace *{filter}* with the condition that you wish to apply to filter the list of roles:</span></span>

   * <span data-ttu-id="e9262-210">List roles available for assignment at the specified scope and any of its child scopes: `atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="e9262-210">List roles available for assignment at the specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="e9262-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="e9262-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="e9262-212">Use the URL encoded form of the exact display name of the role.</span><span class="sxs-lookup"><span data-stu-id="e9262-212">Use the URL encoded form of the exact display name of the role.</span></span> <span data-ttu-id="e9262-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="e9262-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="e9262-214">Response</span><span class="sxs-lookup"><span data-stu-id="e9262-214">Response</span></span>
<span data-ttu-id="e9262-215">Status code: 200</span><span class="sxs-lookup"><span data-stu-id="e9262-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a><span data-ttu-id="e9262-216">Get information about a Role</span><span class="sxs-lookup"><span data-stu-id="e9262-216">Get information about a Role</span></span>
<span data-ttu-id="e9262-217">Gets information about a single role specified by the role definition identifier.</span><span class="sxs-lookup"><span data-stu-id="e9262-217">Gets information about a single role specified by the role definition identifier.</span></span> <span data-ttu-id="e9262-218">To get information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="e9262-218">To get information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="e9262-219">To get information about a role, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-219">To get information about a role, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="e9262-220">All the built-in roles are granted access to this operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-220">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="e9262-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e9262-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e9262-222">Request</span><span class="sxs-lookup"><span data-stu-id="e9262-222">Request</span></span>
<span data-ttu-id="e9262-223">Use the **GET** method with the following URI:</span><span class="sxs-lookup"><span data-stu-id="e9262-223">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="e9262-224">Within the URI, make the following substitutions to customize your request:</span><span class="sxs-lookup"><span data-stu-id="e9262-224">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e9262-225">Replace *{scope}* with the scope for which you wish to list the role assignments.</span><span class="sxs-lookup"><span data-stu-id="e9262-225">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="e9262-226">The following examples show how to specify the scope for different levels:</span><span class="sxs-lookup"><span data-stu-id="e9262-226">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e9262-227">Subscription: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="e9262-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e9262-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e9262-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e9262-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e9262-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e9262-230">Replace *{role-definition-id}* with the GUID identifier of the role definition.</span><span class="sxs-lookup"><span data-stu-id="e9262-230">Replace *{role-definition-id}* with the GUID identifier of the role definition.</span></span>
3. <span data-ttu-id="e9262-231">Replace *{api-version}* with 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e9262-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="e9262-232">Response</span><span class="sxs-lookup"><span data-stu-id="e9262-232">Response</span></span>
<span data-ttu-id="e9262-233">Status code: 200</span><span class="sxs-lookup"><span data-stu-id="e9262-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a><span data-ttu-id="e9262-234">Create a Custom Role</span><span class="sxs-lookup"><span data-stu-id="e9262-234">Create a Custom Role</span></span>
<span data-ttu-id="e9262-235">Create a custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-235">Create a custom role.</span></span>

<span data-ttu-id="e9262-236">To create a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="e9262-236">To create a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="e9262-237">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-237">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="e9262-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e9262-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e9262-239">Request</span><span class="sxs-lookup"><span data-stu-id="e9262-239">Request</span></span>
<span data-ttu-id="e9262-240">Use the **PUT** method with the following URI:</span><span class="sxs-lookup"><span data-stu-id="e9262-240">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="e9262-241">Within the URI, make the following substitutions to customize your request:</span><span class="sxs-lookup"><span data-stu-id="e9262-241">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e9262-242">Replace *{scope}* with the first *AssignableScope* of the custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-242">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="e9262-243">The following examples show how to specify the scope for different levels.</span><span class="sxs-lookup"><span data-stu-id="e9262-243">The following examples show how to specify the scope for different levels.</span></span>

   * <span data-ttu-id="e9262-244">Subscription: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="e9262-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e9262-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e9262-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e9262-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e9262-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e9262-247">Replace *{role-definition-id}* with a new GUID, which becomes the GUID identifier of the new custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-247">Replace *{role-definition-id}* with a new GUID, which becomes the GUID identifier of the new custom role.</span></span>
3. <span data-ttu-id="e9262-248">Replace *{api-version}* with 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e9262-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="e9262-249">For the request body, provide the values in the following format:</span><span class="sxs-lookup"><span data-stu-id="e9262-249">For the request body, provide the values in the following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="e9262-250">Element Name</span><span class="sxs-lookup"><span data-stu-id="e9262-250">Element Name</span></span> | <span data-ttu-id="e9262-251">Required</span><span class="sxs-lookup"><span data-stu-id="e9262-251">Required</span></span> | <span data-ttu-id="e9262-252">Type</span><span class="sxs-lookup"><span data-stu-id="e9262-252">Type</span></span> | <span data-ttu-id="e9262-253">Description</span><span class="sxs-lookup"><span data-stu-id="e9262-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e9262-254">name</span><span class="sxs-lookup"><span data-stu-id="e9262-254">name</span></span> |<span data-ttu-id="e9262-255">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-255">Yes</span></span> |<span data-ttu-id="e9262-256">String</span><span class="sxs-lookup"><span data-stu-id="e9262-256">String</span></span> |<span data-ttu-id="e9262-257">GUID identifier of the custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-257">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="e9262-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="e9262-258">properties.roleName</span></span> |<span data-ttu-id="e9262-259">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-259">Yes</span></span> |<span data-ttu-id="e9262-260">String</span><span class="sxs-lookup"><span data-stu-id="e9262-260">String</span></span> |<span data-ttu-id="e9262-261">Display name of the custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-261">Display name of the custom role.</span></span> <span data-ttu-id="e9262-262">Maximum size 128 characters.</span><span class="sxs-lookup"><span data-stu-id="e9262-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="e9262-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="e9262-263">properties.description</span></span> |<span data-ttu-id="e9262-264">No</span><span class="sxs-lookup"><span data-stu-id="e9262-264">No</span></span> |<span data-ttu-id="e9262-265">String</span><span class="sxs-lookup"><span data-stu-id="e9262-265">String</span></span> |<span data-ttu-id="e9262-266">Description of the custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-266">Description of the custom role.</span></span> <span data-ttu-id="e9262-267">Maximum size 1024 characters.</span><span class="sxs-lookup"><span data-stu-id="e9262-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="e9262-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="e9262-268">properties.type</span></span> |<span data-ttu-id="e9262-269">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-269">Yes</span></span> |<span data-ttu-id="e9262-270">String</span><span class="sxs-lookup"><span data-stu-id="e9262-270">String</span></span> |<span data-ttu-id="e9262-271">Set to "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="e9262-271">Set to "CustomRole."</span></span> |
| <span data-ttu-id="e9262-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="e9262-272">properties.permissions.actions</span></span> |<span data-ttu-id="e9262-273">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-273">Yes</span></span> |<span data-ttu-id="e9262-274">String[]</span><span class="sxs-lookup"><span data-stu-id="e9262-274">String[]</span></span> |<span data-ttu-id="e9262-275">An array of action strings specifying the operations granted by the custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-275">An array of action strings specifying the operations granted by the custom role.</span></span> |
| <span data-ttu-id="e9262-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="e9262-276">properties.permissions.notActions</span></span> |<span data-ttu-id="e9262-277">No</span><span class="sxs-lookup"><span data-stu-id="e9262-277">No</span></span> |<span data-ttu-id="e9262-278">String[]</span><span class="sxs-lookup"><span data-stu-id="e9262-278">String[]</span></span> |<span data-ttu-id="e9262-279">An array of action strings specifying the operations to exclude from the operations granted by the custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-279">An array of action strings specifying the operations to exclude from the operations granted by the custom role.</span></span> |
| <span data-ttu-id="e9262-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="e9262-280">properties.assignableScopes</span></span> |<span data-ttu-id="e9262-281">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-281">Yes</span></span> |<span data-ttu-id="e9262-282">String[]</span><span class="sxs-lookup"><span data-stu-id="e9262-282">String[]</span></span> |<span data-ttu-id="e9262-283">An array of scopes in which the custom role can be used.</span><span class="sxs-lookup"><span data-stu-id="e9262-283">An array of scopes in which the custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="e9262-284">Response</span><span class="sxs-lookup"><span data-stu-id="e9262-284">Response</span></span>
<span data-ttu-id="e9262-285">Status code: 201</span><span class="sxs-lookup"><span data-stu-id="e9262-285">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a><span data-ttu-id="e9262-286">Update a Custom Role</span><span class="sxs-lookup"><span data-stu-id="e9262-286">Update a Custom Role</span></span>
<span data-ttu-id="e9262-287">Modify a custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-287">Modify a custom role.</span></span>

<span data-ttu-id="e9262-288">To modify a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="e9262-288">To modify a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="e9262-289">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-289">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="e9262-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e9262-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e9262-291">Request</span><span class="sxs-lookup"><span data-stu-id="e9262-291">Request</span></span>
<span data-ttu-id="e9262-292">Use the **PUT** method with the following URI:</span><span class="sxs-lookup"><span data-stu-id="e9262-292">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="e9262-293">Within the URI, make the following substitutions to customize your request:</span><span class="sxs-lookup"><span data-stu-id="e9262-293">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e9262-294">Replace *{scope}* with the first *AssignableScope* of the custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-294">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="e9262-295">The following examples show how to specify the scope for different levels:</span><span class="sxs-lookup"><span data-stu-id="e9262-295">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e9262-296">Subscription: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="e9262-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e9262-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e9262-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e9262-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e9262-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e9262-299">Replace *{role-definition-id}* with the GUID identifier of the custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-299">Replace *{role-definition-id}* with the GUID identifier of the custom role.</span></span>
3. <span data-ttu-id="e9262-300">Replace *{api-version}* with 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e9262-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="e9262-301">For the request body, provide the values in the following format:</span><span class="sxs-lookup"><span data-stu-id="e9262-301">For the request body, provide the values in the following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="e9262-302">Element Name</span><span class="sxs-lookup"><span data-stu-id="e9262-302">Element Name</span></span> | <span data-ttu-id="e9262-303">Required</span><span class="sxs-lookup"><span data-stu-id="e9262-303">Required</span></span> | <span data-ttu-id="e9262-304">Type</span><span class="sxs-lookup"><span data-stu-id="e9262-304">Type</span></span> | <span data-ttu-id="e9262-305">Description</span><span class="sxs-lookup"><span data-stu-id="e9262-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e9262-306">name</span><span class="sxs-lookup"><span data-stu-id="e9262-306">name</span></span> |<span data-ttu-id="e9262-307">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-307">Yes</span></span> |<span data-ttu-id="e9262-308">String</span><span class="sxs-lookup"><span data-stu-id="e9262-308">String</span></span> |<span data-ttu-id="e9262-309">GUID identifier of the custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-309">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="e9262-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="e9262-310">properties.roleName</span></span> |<span data-ttu-id="e9262-311">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-311">Yes</span></span> |<span data-ttu-id="e9262-312">String</span><span class="sxs-lookup"><span data-stu-id="e9262-312">String</span></span> |<span data-ttu-id="e9262-313">Display name of the updated custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-313">Display name of the updated custom role.</span></span> |
| <span data-ttu-id="e9262-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="e9262-314">properties.description</span></span> |<span data-ttu-id="e9262-315">No</span><span class="sxs-lookup"><span data-stu-id="e9262-315">No</span></span> |<span data-ttu-id="e9262-316">String</span><span class="sxs-lookup"><span data-stu-id="e9262-316">String</span></span> |<span data-ttu-id="e9262-317">Description of the updated custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-317">Description of the updated custom role.</span></span> |
| <span data-ttu-id="e9262-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="e9262-318">properties.type</span></span> |<span data-ttu-id="e9262-319">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-319">Yes</span></span> |<span data-ttu-id="e9262-320">String</span><span class="sxs-lookup"><span data-stu-id="e9262-320">String</span></span> |<span data-ttu-id="e9262-321">Set to "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="e9262-321">Set to "CustomRole."</span></span> |
| <span data-ttu-id="e9262-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="e9262-322">properties.permissions.actions</span></span> |<span data-ttu-id="e9262-323">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-323">Yes</span></span> |<span data-ttu-id="e9262-324">String[]</span><span class="sxs-lookup"><span data-stu-id="e9262-324">String[]</span></span> |<span data-ttu-id="e9262-325">An array of action strings specifying the operations to which the updated custom role grants access.</span><span class="sxs-lookup"><span data-stu-id="e9262-325">An array of action strings specifying the operations to which the updated custom role grants access.</span></span> |
| <span data-ttu-id="e9262-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="e9262-326">properties.permissions.notActions</span></span> |<span data-ttu-id="e9262-327">No</span><span class="sxs-lookup"><span data-stu-id="e9262-327">No</span></span> |<span data-ttu-id="e9262-328">String[]</span><span class="sxs-lookup"><span data-stu-id="e9262-328">String[]</span></span> |<span data-ttu-id="e9262-329">An array of action strings specifying the operations to exclude from the operations which the updated custom role grants.</span><span class="sxs-lookup"><span data-stu-id="e9262-329">An array of action strings specifying the operations to exclude from the operations which the updated custom role grants.</span></span> |
| <span data-ttu-id="e9262-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="e9262-330">properties.assignableScopes</span></span> |<span data-ttu-id="e9262-331">Yes</span><span class="sxs-lookup"><span data-stu-id="e9262-331">Yes</span></span> |<span data-ttu-id="e9262-332">String[]</span><span class="sxs-lookup"><span data-stu-id="e9262-332">String[]</span></span> |<span data-ttu-id="e9262-333">An array of scopes in which the updated custom role can be used.</span><span class="sxs-lookup"><span data-stu-id="e9262-333">An array of scopes in which the updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="e9262-334">Response</span><span class="sxs-lookup"><span data-stu-id="e9262-334">Response</span></span>
<span data-ttu-id="e9262-335">Status code: 201</span><span class="sxs-lookup"><span data-stu-id="e9262-335">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a><span data-ttu-id="e9262-336">Delete a Custom Role</span><span class="sxs-lookup"><span data-stu-id="e9262-336">Delete a Custom Role</span></span>
<span data-ttu-id="e9262-337">Delete a custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-337">Delete a custom role.</span></span>

<span data-ttu-id="e9262-338">To delete a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/delete` operation on all the `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="e9262-338">To delete a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/delete` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="e9262-339">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span><span class="sxs-lookup"><span data-stu-id="e9262-339">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="e9262-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e9262-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="e9262-341">Request</span><span class="sxs-lookup"><span data-stu-id="e9262-341">Request</span></span>
<span data-ttu-id="e9262-342">Use the **DELETE** method with the following URI:</span><span class="sxs-lookup"><span data-stu-id="e9262-342">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="e9262-343">Within the URI, make the following substitutions to customize your request:</span><span class="sxs-lookup"><span data-stu-id="e9262-343">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="e9262-344">Replace *{scope}* with the scope at which you wish to delete the role definition.</span><span class="sxs-lookup"><span data-stu-id="e9262-344">Replace *{scope}* with the scope at which you wish to delete the role definition.</span></span> <span data-ttu-id="e9262-345">The following examples show how to specify the scope for different levels:</span><span class="sxs-lookup"><span data-stu-id="e9262-345">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="e9262-346">Subscription: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="e9262-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="e9262-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="e9262-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="e9262-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="e9262-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="e9262-349">Replace *{role-definition-id}* with the GUID role definition id of the custom role.</span><span class="sxs-lookup"><span data-stu-id="e9262-349">Replace *{role-definition-id}* with the GUID role definition id of the custom role.</span></span>
3. <span data-ttu-id="e9262-350">Replace *{api-version}* with 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="e9262-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="e9262-351">Response</span><span class="sxs-lookup"><span data-stu-id="e9262-351">Response</span></span>
<span data-ttu-id="e9262-352">Status code: 200</span><span class="sxs-lookup"><span data-stu-id="e9262-352">Status code: 200</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a><span data-ttu-id="e9262-353">Next steps</span><span class="sxs-lookup"><span data-stu-id="e9262-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
