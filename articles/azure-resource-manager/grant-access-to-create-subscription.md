---
title: Grant access to create Azure Enterprise subscriptions| Microsoft Docs
description: Learn how to give a user or service principal the ability to programmatically create Azure Enterprise subscriptions.
services: azure-resource-manager
author: adpick
manager: adpick
editor: ''
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/05/2018
ms.author: adpick
ms.openlocfilehash: 86e457cf553c84386937c35bab1ab0fd20518bed
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857942"
---
# <a name="grant-access-to-create-azure-enterprise-subscriptions-preview"></a><span data-ttu-id="93d99-103">Grant access to create Azure Enterprise subscriptions (preview)</span><span class="sxs-lookup"><span data-stu-id="93d99-103">Grant access to create Azure Enterprise subscriptions (preview)</span></span>

<span data-ttu-id="93d99-104">As an Azure customer on [Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/), you can give another user or service principal permission to create subscriptions billed to your account.</span><span class="sxs-lookup"><span data-stu-id="93d99-104">As an Azure customer on [Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/), you can give another user or service principal permission to create subscriptions billed to your account.</span></span> <span data-ttu-id="93d99-105">In this article, you learn how to use [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) to share the ability to create subscriptions, and how to audit subscription creations.</span><span class="sxs-lookup"><span data-stu-id="93d99-105">In this article, you learn how to use [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) to share the ability to create subscriptions, and how to audit subscription creations.</span></span> <span data-ttu-id="93d99-106">You must have the Owner role on the account you wish to share.</span><span class="sxs-lookup"><span data-stu-id="93d99-106">You must have the Owner role on the account you wish to share.</span></span>

<span data-ttu-id="93d99-107">To create a subscription, see [Programmatically create Azure Enterprise subscriptions (preview)](programmatically-create-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="93d99-107">To create a subscription, see [Programmatically create Azure Enterprise subscriptions (preview)](programmatically-create-subscription.md).</span></span>

## <a name="delegate-access-to-an-enrollment-account-using-rbac"></a><span data-ttu-id="93d99-108">Delegate access to an enrollment account using RBAC</span><span class="sxs-lookup"><span data-stu-id="93d99-108">Delegate access to an enrollment account using RBAC</span></span>

<span data-ttu-id="93d99-109">To give another user or service principal the ability to create subscriptions against a specific account, [give them an RBAC Owner role at the scope of the enrollment account](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="93d99-109">To give another user or service principal the ability to create subscriptions against a specific account, [give them an RBAC Owner role at the scope of the enrollment account](../active-directory/role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="93d99-110">The following example gives a user in the tenant with `principalId` of `<userObjectId>` (for SignUpEngineering@contoso.com) an Owner role on the enrollment account.</span><span class="sxs-lookup"><span data-stu-id="93d99-110">The following example gives a user in the tenant with `principalId` of `<userObjectId>` (for SignUpEngineering@contoso.com) an Owner role on the enrollment account.</span></span> <span data-ttu-id="93d99-111">To find the enrollment account ID and principal ID, see [Programmatically create Azure Enterprise subscriptions (preview)](programmatically-create-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="93d99-111">To find the enrollment account ID and principal ID, see [Programmatically create Azure Enterprise subscriptions (preview)](programmatically-create-subscription.md).</span></span>

# <a name="resttabrest"></a>[<span data-ttu-id="93d99-112">REST</span><span class="sxs-lookup"><span data-stu-id="93d99-112">REST</span></span>](#tab/rest)

```json
PUT  https://management.azure.com/providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx/providers/Microsoft.Authorization/roleAssignments/<roleAssignmentGuid>?api-version=2015-07-01

{
  "properties": {
    "roleDefinitionId": "/providers/Microsoft.Billing/enrollmentAccounts/providers/Microsoft.Authorization/roleDefinitions/<ownerRoleDefinitionId>",
    "principalId": "<userObjectId>"
  }
}
```
<span data-ttu-id="93d99-113">When the Owner role is successfully assigned at the enrollment account scope, Azure responds with information of the role assignment:</span><span class="sxs-lookup"><span data-stu-id="93d99-113">When the Owner role is successfully assigned at the enrollment account scope, Azure responds with information of the role assignment:</span></span>

```json
{
  "properties": {
    "roleDefinitionId": "/providers/Microsoft.Billing/enrollmentAccounts/providers/Microsoft.Authorization/roleDefinitions/<ownerRoleDefinitionId>",
    "principalId": "<userObjectId>",
    "scope": "/providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "createdOn": "2018-03-05T08:36:26.4014813Z",
    "updatedOn": "2018-03-05T08:36:26.4014813Z",
    "createdBy": "<assignerObjectId>",
    "updatedBy": "<assignerObjectId>"
  },
  "id": "/providers/Microsoft.Billing/enrollmentAccounts/providers/Microsoft.Authorization/roleDefinitions/<ownerRoleDefinitionId>",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "<roleAssignmentGuid>"
}
```

# <a name="powershelltabazure-powershell"></a>[<span data-ttu-id="93d99-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93d99-114">PowerShell</span></span>](#tab/azure-powershell)

<span data-ttu-id="93d99-115">Use the [New-AzureRmRoleAssignment](../active-directory/role-based-access-control-manage-access-powershell.md) to give another user Owner access to your enrollment account.</span><span class="sxs-lookup"><span data-stu-id="93d99-115">Use the [New-AzureRmRoleAssignment](../active-directory/role-based-access-control-manage-access-powershell.md) to give another user Owner access to your enrollment account.</span></span>

```azurepowershell-interactive
New-AzureRmRoleAssignment -RoleDefinitionName Owner -ObjectId <userObjectId> -Scope /providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

# <a name="azure-clitabazure-cli"></a>[<span data-ttu-id="93d99-116">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="93d99-116">Azure CLI</span></span>](#tab/azure-cli)

<span data-ttu-id="93d99-117">Use the [az role assignment create](../active-directory/role-based-access-control-manage-access-azure-cli.md) to give another user Owner access to your enrollment account.</span><span class="sxs-lookup"><span data-stu-id="93d99-117">Use the [az role assignment create](../active-directory/role-based-access-control-manage-access-azure-cli.md) to give another user Owner access to your enrollment account.</span></span>

```azurecli-interactive 
az role assignment create --role Owner --assignee-object-id <userObjectId> --scope /providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

----

<span data-ttu-id="93d99-118">Once a user becomes an RBAC Owner for your enrollment account, they can programmatically create subscriptions under it.</span><span class="sxs-lookup"><span data-stu-id="93d99-118">Once a user becomes an RBAC Owner for your enrollment account, they can programmatically create subscriptions under it.</span></span> <span data-ttu-id="93d99-119">A subscription created by a delegated user still has the original Account Owner as Service Admin, but it also has the delegated user as an Owner by default.</span><span class="sxs-lookup"><span data-stu-id="93d99-119">A subscription created by a delegated user still has the original Account Owner as Service Admin, but it also has the delegated user as an Owner by default.</span></span> 

## <a name="audit-who-created-subscriptions-using-activity-logs"></a><span data-ttu-id="93d99-120">Audit who created subscriptions using activity logs</span><span class="sxs-lookup"><span data-stu-id="93d99-120">Audit who created subscriptions using activity logs</span></span>

<span data-ttu-id="93d99-121">To track the subscriptions created via this API, use the [Tenant Activity Log API](/rest/api/monitor/tenantactivitylogs).</span><span class="sxs-lookup"><span data-stu-id="93d99-121">To track the subscriptions created via this API, use the [Tenant Activity Log API](/rest/api/monitor/tenantactivitylogs).</span></span> <span data-ttu-id="93d99-122">It's currently not possible to use PowerShell, CLI, or Azure portal to track subscription creation.</span><span class="sxs-lookup"><span data-stu-id="93d99-122">It's currently not possible to use PowerShell, CLI, or Azure portal to track subscription creation.</span></span>

1. <span data-ttu-id="93d99-123">As a tenant admin of the Azure AD tenant, [elevate access](../active-directory/role-based-access-control-tenant-admin-access.md) then assign a Reader role to the auditing user over the scope `/providers/microsoft.insights/eventtypes/management`.</span><span class="sxs-lookup"><span data-stu-id="93d99-123">As a tenant admin of the Azure AD tenant, [elevate access](../active-directory/role-based-access-control-tenant-admin-access.md) then assign a Reader role to the auditing user over the scope `/providers/microsoft.insights/eventtypes/management`.</span></span>
1. <span data-ttu-id="93d99-124">As the auditing user, call the [Tenant Activity Log API](/rest/api/monitor/tenantactivitylogs) to see subscription creation activities.</span><span class="sxs-lookup"><span data-stu-id="93d99-124">As the auditing user, call the [Tenant Activity Log API](/rest/api/monitor/tenantactivitylogs) to see subscription creation activities.</span></span> <span data-ttu-id="93d99-125">Example:</span><span class="sxs-lookup"><span data-stu-id="93d99-125">Example:</span></span>

```
GET "/providers/Microsoft.Insights/eventtypes/management/values?api-version=2015-04-01&$filter=eventTimestamp ge '{greaterThanTimeStamp}' and eventTimestamp le '{lessThanTimestamp}' and eventChannels eq 'Operation' and resourceProvider eq 'Microsoft.Subscription'" 
```

> [!NOTE]
> <span data-ttu-id="93d99-126">To conveniently call this API from the command line, try [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="93d99-126">To conveniently call this API from the command line, try [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93d99-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="93d99-127">Next steps</span></span>

* <span data-ttu-id="93d99-128">Now that the user or service principal has permission to create a subscription, you can use that identity to [programmatically create Azure Enterprise subscriptions](programmatically-create-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="93d99-128">Now that the user or service principal has permission to create a subscription, you can use that identity to [programmatically create Azure Enterprise subscriptions](programmatically-create-subscription.md).</span></span>
* <span data-ttu-id="93d99-129">For an example on creating subscriptions using .NET, see [sample code on GitHub](https://github.com/Azure-Samples/create-azure-subscription-dotnet-core).</span><span class="sxs-lookup"><span data-stu-id="93d99-129">For an example on creating subscriptions using .NET, see [sample code on GitHub](https://github.com/Azure-Samples/create-azure-subscription-dotnet-core).</span></span>
* <span data-ttu-id="93d99-130">To learn more about Azure Resource Manager and its APIs, see [Azure Resource Manager overview](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93d99-130">To learn more about Azure Resource Manager and its APIs, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>
* <span data-ttu-id="93d99-131">To learn more about managing large numbers of subscriptions using management groups, see [Organize your resources with Azure management groups](management-groups-overview.md)</span><span class="sxs-lookup"><span data-stu-id="93d99-131">To learn more about managing large numbers of subscriptions using management groups, see [Organize your resources with Azure management groups](management-groups-overview.md)</span></span>
* <span data-ttu-id="93d99-132">To see a comprehensive best practice guidance for large organizations on subscription governance, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance)</span><span class="sxs-lookup"><span data-stu-id="93d99-132">To see a comprehensive best practice guidance for large organizations on subscription governance, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance)</span></span>
