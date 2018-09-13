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
# <a name="grant-access-to-create-azure-enterprise-subscriptions-preview"></a>Grant access to create Azure Enterprise subscriptions (preview)

As an Azure customer on [Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/), you can give another user or service principal permission to create subscriptions billed to your account. In this article, you learn how to use [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) to share the ability to create subscriptions, and how to audit subscription creations. You must have the Owner role on the account you wish to share.

To create a subscription, see [Programmatically create Azure Enterprise subscriptions (preview)](programmatically-create-subscription.md).

## <a name="delegate-access-to-an-enrollment-account-using-rbac"></a>Delegate access to an enrollment account using RBAC

To give another user or service principal the ability to create subscriptions against a specific account, [give them an RBAC Owner role at the scope of the enrollment account](../active-directory/role-based-access-control-manage-access-rest.md). The following example gives a user in the tenant with `principalId` of `<userObjectId>` (for SignUpEngineering@contoso.com) an Owner role on the enrollment account. To find the enrollment account ID and principal ID, see [Programmatically create Azure Enterprise subscriptions (preview)](programmatically-create-subscription.md).

# <a name="resttabrest"></a>[REST](#tab/rest)

```json
PUT  https://management.azure.com/providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx/providers/Microsoft.Authorization/roleAssignments/<roleAssignmentGuid>?api-version=2015-07-01

{
  "properties": {
    "roleDefinitionId": "/providers/Microsoft.Billing/enrollmentAccounts/providers/Microsoft.Authorization/roleDefinitions/<ownerRoleDefinitionId>",
    "principalId": "<userObjectId>"
  }
}
```
When the Owner role is successfully assigned at the enrollment account scope, Azure responds with information of the role assignment:

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

# <a name="powershelltabazure-powershell"></a>[PowerShell](#tab/azure-powershell)

Use the [New-AzureRmRoleAssignment](../active-directory/role-based-access-control-manage-access-powershell.md) to give another user Owner access to your enrollment account.

```azurepowershell-interactive
New-AzureRmRoleAssignment -RoleDefinitionName Owner -ObjectId <userObjectId> -Scope /providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

# <a name="azure-clitabazure-cli"></a>[Azure CLI](#tab/azure-cli)

Use the [az role assignment create](../active-directory/role-based-access-control-manage-access-azure-cli.md) to give another user Owner access to your enrollment account.

```azurecli-interactive 
az role assignment create --role Owner --assignee-object-id <userObjectId> --scope /providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

----

Once a user becomes an RBAC Owner for your enrollment account, they can programmatically create subscriptions under it. A subscription created by a delegated user still has the original Account Owner as Service Admin, but it also has the delegated user as an Owner by default. 

## <a name="audit-who-created-subscriptions-using-activity-logs"></a>Audit who created subscriptions using activity logs

To track the subscriptions created via this API, use the [Tenant Activity Log API](/rest/api/monitor/tenantactivitylogs). It's currently not possible to use PowerShell, CLI, or Azure portal to track subscription creation.

1. As a tenant admin of the Azure AD tenant, [elevate access](../active-directory/role-based-access-control-tenant-admin-access.md) then assign a Reader role to the auditing user over the scope `/providers/microsoft.insights/eventtypes/management`.
1. As the auditing user, call the [Tenant Activity Log API](/rest/api/monitor/tenantactivitylogs) to see subscription creation activities. Example:

```
GET "/providers/Microsoft.Insights/eventtypes/management/values?api-version=2015-04-01&$filter=eventTimestamp ge '{greaterThanTimeStamp}' and eventTimestamp le '{lessThanTimestamp}' and eventChannels eq 'Operation' and resourceProvider eq 'Microsoft.Subscription'" 
```

> [!NOTE]
> To conveniently call this API from the command line, try [ARMClient](https://github.com/projectkudu/ARMClient).

## <a name="next-steps"></a>Next steps

* Now that the user or service principal has permission to create a subscription, you can use that identity to [programmatically create Azure Enterprise subscriptions](programmatically-create-subscription.md).
* For an example on creating subscriptions using .NET, see [sample code on GitHub](https://github.com/Azure-Samples/create-azure-subscription-dotnet-core).
* To learn more about Azure Resource Manager and its APIs, see [Azure Resource Manager overview](resource-group-overview.md).
* To learn more about managing large numbers of subscriptions using management groups, see [Organize your resources with Azure management groups](management-groups-overview.md)
* To see a comprehensive best practice guidance for large organizations on subscription governance, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance)
