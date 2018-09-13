---
title: Tenant admin elevate access - Azure AD | Microsoft Docs
description: This topic describes the built in roles for role-based access control (RBAC).
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2017
ms.author: kgremban
ms.openlocfilehash: 9bcad7aaf7f1bd8c51dbfa88381276a70a4def5c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563906"
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="632ef-103">Elevate access as a tenant admin with Role-Based Access Control</span><span class="sxs-lookup"><span data-stu-id="632ef-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="632ef-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span><span class="sxs-lookup"><span data-stu-id="632ef-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="632ef-105">A tenant admin can elevate herself to the User Access Administrator role when needed.</span><span class="sxs-lookup"><span data-stu-id="632ef-105">A tenant admin can elevate herself to the User Access Administrator role when needed.</span></span> <span data-ttu-id="632ef-106">That role gives the tenant admin permissions to grant herself or others roles at the "/" scope.</span><span class="sxs-lookup"><span data-stu-id="632ef-106">That role gives the tenant admin permissions to grant herself or others roles at the "/" scope.</span></span>

<span data-ttu-id="632ef-107">This feature is important because it allows the tenant admin to see all the subscriptions that exist in an organization.</span><span class="sxs-lookup"><span data-stu-id="632ef-107">This feature is important because it allows the tenant admin to see all the subscriptions that exist in an organization.</span></span> <span data-ttu-id="632ef-108">It also allows for automation apps (like invoicing and auditing) to access all the subscriptions and provide an accurate view of the state of the organization from a billing or asset management perspective.</span><span class="sxs-lookup"><span data-stu-id="632ef-108">It also allows for automation apps (like invoicing and auditing) to access all the subscriptions and provide an accurate view of the state of the organization from a billing or asset management perspective.</span></span>  

## <a name="how-to-use-elevateaccess-to-give-tenant-access"></a><span data-ttu-id="632ef-109">How to use elevateAccess to give tenant access</span><span class="sxs-lookup"><span data-stu-id="632ef-109">How to use elevateAccess to give tenant access</span></span>

<span data-ttu-id="632ef-110">The basic process works with the following steps:</span><span class="sxs-lookup"><span data-stu-id="632ef-110">The basic process works with the following steps:</span></span>

1. <span data-ttu-id="632ef-111">Using REST, call *elevateAccess*, which grants you the User Access Administrator role at "/" scope.</span><span class="sxs-lookup"><span data-stu-id="632ef-111">Using REST, call *elevateAccess*, which grants you the User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="632ef-112">Create a [role assignment](/rest/api/authorization/roleassignments) to assign any role at any scope.</span><span class="sxs-lookup"><span data-stu-id="632ef-112">Create a [role assignment](/rest/api/authorization/roleassignments) to assign any role at any scope.</span></span> <span data-ttu-id="632ef-113">The following example shows the properties for assigning the Reader role at "/" scope:</span><span class="sxs-lookup"><span data-stu-id="632ef-113">The following example shows the properties for assigning the Reader role at "/" scope:</span></span>

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. <span data-ttu-id="632ef-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span><span class="sxs-lookup"><span data-stu-id="632ef-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="632ef-115">Revoke your User Access Admin privileges until they're needed again.</span><span class="sxs-lookup"><span data-stu-id="632ef-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-to-undo-the-elevateaccess-action"></a><span data-ttu-id="632ef-116">How to undo the elevateAccess action</span><span class="sxs-lookup"><span data-stu-id="632ef-116">How to undo the elevateAccess action</span></span>

<span data-ttu-id="632ef-117">When you call *elevateAccess* you create a role assignment for yourself, so to revoke those privileges you need to delete the assignment.</span><span class="sxs-lookup"><span data-stu-id="632ef-117">When you call *elevateAccess* you create a role assignment for yourself, so to revoke those privileges you need to delete the assignment.</span></span>

1.  <span data-ttu-id="632ef-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator to determine the name GUID of the User Access Administrator role.</span><span class="sxs-lookup"><span data-stu-id="632ef-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator to determine the name GUID of the User Access Administrator role.</span></span> <span data-ttu-id="632ef-119">The response should look like this:</span><span class="sxs-lookup"><span data-stu-id="632ef-119">The response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access to Azure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    <span data-ttu-id="632ef-120">Save the GUID from the *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="632ef-120">Save the GUID from the *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="632ef-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span><span class="sxs-lookup"><span data-stu-id="632ef-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="632ef-122">This lists all your assignments in the tenant.</span><span class="sxs-lookup"><span data-stu-id="632ef-122">This lists all your assignments in the tenant.</span></span> <span data-ttu-id="632ef-123">Look for the one where the scope is "/" and the RoleDefinitionId ends with the role name GUID you found in step 1.</span><span class="sxs-lookup"><span data-stu-id="632ef-123">Look for the one where the scope is "/" and the RoleDefinitionId ends with the role name GUID you found in step 1.</span></span> <span data-ttu-id="632ef-124">The role assignment should look like this:</span><span class="sxs-lookup"><span data-stu-id="632ef-124">The role assignment should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    <span data-ttu-id="632ef-125">Again, save the GUID from the *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="632ef-125">Again, save the GUID from the *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="632ef-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = the name GUID you found in step 2.</span><span class="sxs-lookup"><span data-stu-id="632ef-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = the name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="632ef-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="632ef-127">Next steps</span></span>

- <span data-ttu-id="632ef-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="632ef-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="632ef-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="632ef-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in the Azure portal</span></span>
