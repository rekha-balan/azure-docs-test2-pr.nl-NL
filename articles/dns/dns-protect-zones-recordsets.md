---
title: Protecting DNS Zones and Records | Microsoft Docs
description: How to protect DNS zones and record sets in Microsoft Azure DNS.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: de8ac70ccf46faaa55e2f0556fad124e56627a35
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552885"
---
# <a name="how-to-protect-dns-zones-and-records"></a><span data-ttu-id="32120-103">How to protect DNS zones and records</span><span class="sxs-lookup"><span data-stu-id="32120-103">How to protect DNS zones and records</span></span>

<span data-ttu-id="32120-104">DNS zones and records are critical resources.</span><span class="sxs-lookup"><span data-stu-id="32120-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="32120-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span><span class="sxs-lookup"><span data-stu-id="32120-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="32120-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span><span class="sxs-lookup"><span data-stu-id="32120-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="32120-107">This article explains how Azure DNS enables you to protect your DNS zones and records against such changes.</span><span class="sxs-lookup"><span data-stu-id="32120-107">This article explains how Azure DNS enables you to protect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="32120-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="32120-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="32120-109">Role-based access control</span><span class="sxs-lookup"><span data-stu-id="32120-109">Role-based access control</span></span>

<span data-ttu-id="32120-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span><span class="sxs-lookup"><span data-stu-id="32120-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="32120-111">Using RBAC, you can grant precisely the amount of access that users need to perform their jobs.</span><span class="sxs-lookup"><span data-stu-id="32120-111">Using RBAC, you can grant precisely the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="32120-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="32120-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="the-dns-zone-contributor-role"></a><span data-ttu-id="32120-113">The 'DNS Zone Contributor' role</span><span class="sxs-lookup"><span data-stu-id="32120-113">The 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="32120-114">The 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span><span class="sxs-lookup"><span data-stu-id="32120-114">The 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="32120-115">Assigning DNS Zone Contributor permissions to a user or group enables that group to manage DNS resources, but not resources of any other type.</span><span class="sxs-lookup"><span data-stu-id="32120-115">Assigning DNS Zone Contributor permissions to a user or group enables that group to manage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="32120-116">For example, suppose the resource group 'myzones' contains five zones for Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="32120-116">For example, suppose the resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="32120-117">Granting the DNS administrator 'DNS Zone Contributor' permissions to that resource group, enables full control over those DNS zones.</span><span class="sxs-lookup"><span data-stu-id="32120-117">Granting the DNS administrator 'DNS Zone Contributor' permissions to that resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="32120-118">It also avoids granting unnecessary permissions, for example the DNS administrator cannot create or stop Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="32120-118">It also avoids granting unnecessary permissions, for example the DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="32120-119">The simplest way to assign RBAC permissions is [via the Azure portal](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="32120-119">The simplest way to assign RBAC permissions is [via the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="32120-120">Open the 'Access control (IAM)' blade for the resource group, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span><span class="sxs-lookup"><span data-stu-id="32120-120">Open the 'Access control (IAM)' blade for the resource group, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![Resource group level RBAC via the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="32120-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="32120-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="32120-123">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="32120-123">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="32120-124">Zone level RBAC</span><span class="sxs-lookup"><span data-stu-id="32120-124">Zone level RBAC</span></span>

<span data-ttu-id="32120-125">Azure RBAC rules can be applied to a subscription, a resource group or to an individual resource.</span><span class="sxs-lookup"><span data-stu-id="32120-125">Azure RBAC rules can be applied to a subscription, a resource group or to an individual resource.</span></span> <span data-ttu-id="32120-126">In the case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span><span class="sxs-lookup"><span data-stu-id="32120-126">In the case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="32120-127">For example, suppose the resource group 'myzones' contains the zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span><span class="sxs-lookup"><span data-stu-id="32120-127">For example, suppose the resource group 'myzones' contains the zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="32120-128">The account used to manage these CNAME records should be assigned permissions to create records in the 'customers.contoso.com' zone only, it should not have access to the other zones.</span><span class="sxs-lookup"><span data-stu-id="32120-128">The account used to manage these CNAME records should be assigned permissions to create records in the 'customers.contoso.com' zone only, it should not have access to the other zones.</span></span>

<span data-ttu-id="32120-129">Zone-level RBAC permissions can be granted via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="32120-129">Zone-level RBAC permissions can be granted via the Azure portal.</span></span>  <span data-ttu-id="32120-130">Open the 'Access control (IAM)' blade for the zone, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span><span class="sxs-lookup"><span data-stu-id="32120-130">Open the 'Access control (IAM)' blade for the zone, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![DNS Zone level RBAC via the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="32120-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="32120-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to a specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="32120-133">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="32120-133">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to a specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="32120-134">Record set level RBAC</span><span class="sxs-lookup"><span data-stu-id="32120-134">Record set level RBAC</span></span>

<span data-ttu-id="32120-135">We can go one step further.</span><span class="sxs-lookup"><span data-stu-id="32120-135">We can go one step further.</span></span> <span data-ttu-id="32120-136">Consider the mail administrator for Contoso Corporation, who needs access to the MX and TXT records at the apex of the 'contoso.com' zone.</span><span class="sxs-lookup"><span data-stu-id="32120-136">Consider the mail administrator for Contoso Corporation, who needs access to the MX and TXT records at the apex of the 'contoso.com' zone.</span></span>  <span data-ttu-id="32120-137">She doesn't need access to any other MX or TXT records, or to any records of any other type.</span><span class="sxs-lookup"><span data-stu-id="32120-137">She doesn't need access to any other MX or TXT records, or to any records of any other type.</span></span>  <span data-ttu-id="32120-138">Azure DNS allows you to assign permissions at the record set level, to precisely the records that the mail administrator needs access to.</span><span class="sxs-lookup"><span data-stu-id="32120-138">Azure DNS allows you to assign permissions at the record set level, to precisely the records that the mail administrator needs access to.</span></span>  <span data-ttu-id="32120-139">The mail administrator is granted precisely the control she needs, and is unable to make any other changes.</span><span class="sxs-lookup"><span data-stu-id="32120-139">The mail administrator is granted precisely the control she needs, and is unable to make any other changes.</span></span>

<span data-ttu-id="32120-140">Record-set level RBAC permissions can be configured via the Azure portal, using the 'Users' button in the record set blade:</span><span class="sxs-lookup"><span data-stu-id="32120-140">Record-set level RBAC permissions can be configured via the Azure portal, using the 'Users' button in the record set blade:</span></span>

![Record set level RBAC via the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="32120-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="32120-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions to a specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="32120-143">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="32120-143">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions to a specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="32120-144">Custom roles</span><span class="sxs-lookup"><span data-stu-id="32120-144">Custom roles</span></span>

<span data-ttu-id="32120-145">The built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span><span class="sxs-lookup"><span data-stu-id="32120-145">The built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="32120-146">It is also possible to build your own customer Azure roles, to provide even finer-grained control.</span><span class="sxs-lookup"><span data-stu-id="32120-146">It is also possible to build your own customer Azure roles, to provide even finer-grained control.</span></span>

<span data-ttu-id="32120-147">Consider again the example in which a CNAME record in the zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span><span class="sxs-lookup"><span data-stu-id="32120-147">Consider again the example in which a CNAME record in the zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="32120-148">The account used to manage these CNAMEs should be granted permission to manage CNAME records only.</span><span class="sxs-lookup"><span data-stu-id="32120-148">The account used to manage these CNAMEs should be granted permission to manage CNAME records only.</span></span>  <span data-ttu-id="32120-149">It is then unable to modify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span><span class="sxs-lookup"><span data-stu-id="32120-149">It is then unable to modify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="32120-150">The following example shows a custom role definition for managing CNAME records only:</span><span class="sxs-lookup"><span data-stu-id="32120-150">The following example shows a custom role definition for managing CNAME records only:</span></span>

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

<span data-ttu-id="32120-151">The Actions property defines the following DNS-specific permissions:</span><span class="sxs-lookup"><span data-stu-id="32120-151">The Actions property defines the following DNS-specific permissions:</span></span>

* <span data-ttu-id="32120-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span><span class="sxs-lookup"><span data-stu-id="32120-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="32120-153">`Microsoft.Network/dnsZones/read` grants permission to read DNS zones, but not to modify them, enabling you to see the zone in which the CNAME is being created.</span><span class="sxs-lookup"><span data-stu-id="32120-153">`Microsoft.Network/dnsZones/read` grants permission to read DNS zones, but not to modify them, enabling you to see the zone in which the CNAME is being created.</span></span>

<span data-ttu-id="32120-154">The remaining Actions are copied from the [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="32120-154">The remaining Actions are copied from the [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="32120-155">Using a custom RBAC role to prevent deleting record sets while still allowing them to be updated is not an effective control.</span><span class="sxs-lookup"><span data-stu-id="32120-155">Using a custom RBAC role to prevent deleting record sets while still allowing them to be updated is not an effective control.</span></span> <span data-ttu-id="32120-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span><span class="sxs-lookup"><span data-stu-id="32120-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="32120-157">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span><span class="sxs-lookup"><span data-stu-id="32120-157">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="32120-158">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span><span class="sxs-lookup"><span data-stu-id="32120-158">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="32120-159">Custom role definitions cannot currently be defined via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="32120-159">Custom role definitions cannot currently be defined via the Azure portal.</span></span> <span data-ttu-id="32120-160">A custom role based on this role definition can be created using Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="32120-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="32120-161">It can also be created via the Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="32120-161">It can also be created via the Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="32120-162">The role can then be assigned in the same way as built-in roles, as described earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="32120-162">The role can then be assigned in the same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="32120-163">For more information on how to create, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="32120-163">For more information on how to create, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="32120-164">Resource locks</span><span class="sxs-lookup"><span data-stu-id="32120-164">Resource locks</span></span>

<span data-ttu-id="32120-165">In addition to RBAC, Azure Resource Manager supports another type of security control, namely the ability to 'lock' resources.</span><span class="sxs-lookup"><span data-stu-id="32120-165">In addition to RBAC, Azure Resource Manager supports another type of security control, namely the ability to 'lock' resources.</span></span> <span data-ttu-id="32120-166">Where RBAC rules allow you to control the actions of specific users and groups, resource locks are applied to the resource, and are effective across all users and roles.</span><span class="sxs-lookup"><span data-stu-id="32120-166">Where RBAC rules allow you to control the actions of specific users and groups, resource locks are applied to the resource, and are effective across all users and roles.</span></span> <span data-ttu-id="32120-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="32120-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="32120-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="32120-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="32120-169">These can be applied either to a DNS zone, or to an individual record set.</span><span class="sxs-lookup"><span data-stu-id="32120-169">These can be applied either to a DNS zone, or to an individual record set.</span></span>  <span data-ttu-id="32120-170">The following sections describe several common scenarios, and how to support them using resource locks.</span><span class="sxs-lookup"><span data-stu-id="32120-170">The following sections describe several common scenarios, and how to support them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="32120-171">Protecting against all changes</span><span class="sxs-lookup"><span data-stu-id="32120-171">Protecting against all changes</span></span>

<span data-ttu-id="32120-172">To prevent any changes being made, apply a ReadOnly lock to the zone.</span><span class="sxs-lookup"><span data-stu-id="32120-172">To prevent any changes being made, apply a ReadOnly lock to the zone.</span></span>  <span data-ttu-id="32120-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span><span class="sxs-lookup"><span data-stu-id="32120-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="32120-174">Zone level resource locks can be created via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="32120-174">Zone level resource locks can be created via the Azure portal.</span></span>  <span data-ttu-id="32120-175">From the DNS zone blade, click 'Locks', then 'Add':</span><span class="sxs-lookup"><span data-stu-id="32120-175">From the DNS zone blade, click 'Locks', then 'Add':</span></span>

![Zone level resource locks via the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="32120-177">Zone-level resource locks can also be created via Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="32120-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="32120-178">Configuring Azure resource locks is not currently supported via the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="32120-178">Configuring Azure resource locks is not currently supported via the Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="32120-179">Protecting individual records</span><span class="sxs-lookup"><span data-stu-id="32120-179">Protecting individual records</span></span>

<span data-ttu-id="32120-180">To prevent an existing DNS record set against modification, apply a ReadOnly lock to the record set.</span><span class="sxs-lookup"><span data-stu-id="32120-180">To prevent an existing DNS record set against modification, apply a ReadOnly lock to the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="32120-181">Applying a DoNotDelete lock to a record set is not an effective control.</span><span class="sxs-lookup"><span data-stu-id="32120-181">Applying a DoNotDelete lock to a record set is not an effective control.</span></span> <span data-ttu-id="32120-182">It prevents the record set from being deleted, but it does not prevent it from being modified.</span><span class="sxs-lookup"><span data-stu-id="32120-182">It prevents the record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="32120-183">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span><span class="sxs-lookup"><span data-stu-id="32120-183">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="32120-184">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span><span class="sxs-lookup"><span data-stu-id="32120-184">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="32120-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32120-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="32120-186">They are not supported in the Azure portal or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="32120-186">They are not supported in the Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="32120-187">Protecting against zone deletion</span><span class="sxs-lookup"><span data-stu-id="32120-187">Protecting against zone deletion</span></span>

<span data-ttu-id="32120-188">When a zone is deleted in Azure DNS, all record sets in the zone are also deleted.</span><span class="sxs-lookup"><span data-stu-id="32120-188">When a zone is deleted in Azure DNS, all record sets in the zone are also deleted.</span></span>  <span data-ttu-id="32120-189">This operation cannot be undone.</span><span class="sxs-lookup"><span data-stu-id="32120-189">This operation cannot be undone.</span></span>  <span data-ttu-id="32120-190">Accidentally deleting a critical zone has the potential to have a significant business impact.</span><span class="sxs-lookup"><span data-stu-id="32120-190">Accidentally deleting a critical zone has the potential to have a significant business impact.</span></span>  <span data-ttu-id="32120-191">It is therefore very important to protect against accidental zone deletion.</span><span class="sxs-lookup"><span data-stu-id="32120-191">It is therefore very important to protect against accidental zone deletion.</span></span>

<span data-ttu-id="32120-192">Applying a DoNotDelete lock to a zone prevents the zone from being deleted.</span><span class="sxs-lookup"><span data-stu-id="32120-192">Applying a DoNotDelete lock to a zone prevents the zone from being deleted.</span></span>  <span data-ttu-id="32120-193">However, since locks are inherited by child resources, it also prevents any record sets in the zone from being deleted, which may be undesirable.</span><span class="sxs-lookup"><span data-stu-id="32120-193">However, since locks are inherited by child resources, it also prevents any record sets in the zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="32120-194">Furthermore, as described in the note above, it is also ineffective since records can still be removed from the existing record sets.</span><span class="sxs-lookup"><span data-stu-id="32120-194">Furthermore, as described in the note above, it is also ineffective since records can still be removed from the existing record sets.</span></span>

<span data-ttu-id="32120-195">As an alternative, consider applying a DoNotDelete lock to a record set in the zone, such as the SOA record set.</span><span class="sxs-lookup"><span data-stu-id="32120-195">As an alternative, consider applying a DoNotDelete lock to a record set in the zone, such as the SOA record set.</span></span>  <span data-ttu-id="32120-196">Since the zone cannot be deleted without also deleting the record sets, this protects against zone deletion, while still allowing record sets within the zone to be modified freely.</span><span class="sxs-lookup"><span data-stu-id="32120-196">Since the zone cannot be deleted without also deleting the record sets, this protects against zone deletion, while still allowing record sets within the zone to be modified freely.</span></span> <span data-ttu-id="32120-197">If an attempt is made to delete the zone, Azure Resource Manager detects this would also delete the SOA record set, and blocks the call because the SOA is locked.</span><span class="sxs-lookup"><span data-stu-id="32120-197">If an attempt is made to delete the zone, Azure Resource Manager detects this would also delete the SOA record set, and blocks the call because the SOA is locked.</span></span>  <span data-ttu-id="32120-198">No record sets are deleted.</span><span class="sxs-lookup"><span data-stu-id="32120-198">No record sets are deleted.</span></span>

<span data-ttu-id="32120-199">The following PowerShell command creates a DoNotDelete lock against the SOA record of the given zone:</span><span class="sxs-lookup"><span data-stu-id="32120-199">The following PowerShell command creates a DoNotDelete lock against the SOA record of the given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on the record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="32120-200">Another way to prevent accidental zone deletion is by using a custom role to ensure the operator and service accounts used to manage your zones do not have zone delete permissions.</span><span class="sxs-lookup"><span data-stu-id="32120-200">Another way to prevent accidental zone deletion is by using a custom role to ensure the operator and service accounts used to manage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="32120-201">When you do need to delete a zone, you can enforce a two-step delete, first granting zone delete permissions (at the zone scope, to prevent deleting the wrong zone) and second to delete the zone.</span><span class="sxs-lookup"><span data-stu-id="32120-201">When you do need to delete a zone, you can enforce a two-step delete, first granting zone delete permissions (at the zone scope, to prevent deleting the wrong zone) and second to delete the zone.</span></span>

<span data-ttu-id="32120-202">This second approach has the advantage that it works for all zones accessed by those accounts, without having to remember to create any locks.</span><span class="sxs-lookup"><span data-stu-id="32120-202">This second approach has the advantage that it works for all zones accessed by those accounts, without having to remember to create any locks.</span></span> <span data-ttu-id="32120-203">It has the disadvantage that any accounts with zone delete permissions, such as the subscription owner, can still accidentally delete a critical zone.</span><span class="sxs-lookup"><span data-stu-id="32120-203">It has the disadvantage that any accounts with zone delete permissions, such as the subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="32120-204">It is possible to use both approaches - resource locks and custom roles - at the same time, as a defense-in-depth approach to DNS zone protection.</span><span class="sxs-lookup"><span data-stu-id="32120-204">It is possible to use both approaches - resource locks and custom roles - at the same time, as a defense-in-depth approach to DNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32120-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="32120-205">Next steps</span></span>

* <span data-ttu-id="32120-206">For more information about working with RBAC, see [Get started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="32120-206">For more information about working with RBAC, see [Get started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="32120-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="32120-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>
* <span data-ttu-id="32120-208">For more information about securing your Azure resources, see [Security considerations for Azure Resource Manager](../best-practices-resource-manager-security.md).</span><span class="sxs-lookup"><span data-stu-id="32120-208">For more information about securing your Azure resources, see [Security considerations for Azure Resource Manager](../best-practices-resource-manager-security.md).</span></span>





