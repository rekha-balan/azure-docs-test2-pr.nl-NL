---
title: Create management groups to organize Azure resources  | Microsoft Docs
description: Learn how to create Azure management groups to manage multiple resources.
author: rthorn17
manager: rithorn
editor: ''
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2018
ms.author: rithorn
ms.openlocfilehash: 114c3c03b49468b6130243bbf9f881a5de42740f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864785"
---
# <a name="create-management-groups-for-resource-organization-and-management"></a><span data-ttu-id="83b2c-103">Create management groups for resource organization and management</span><span class="sxs-lookup"><span data-stu-id="83b2c-103">Create management groups for resource organization and management</span></span>

<span data-ttu-id="83b2c-104">Management groups are containers that help you manage access, policy, and compliance across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="83b2c-104">Management groups are containers that help you manage access, policy, and compliance across multiple subscriptions.</span></span> <span data-ttu-id="83b2c-105">Create these containers to build an effective and efficient hierarchy that can be used with [Azure Policy](../azure-policy/azure-policy-introduction.md) and [Azure Role Based Access Controls](../role-based-access-control/overview.md).</span><span class="sxs-lookup"><span data-stu-id="83b2c-105">Create these containers to build an effective and efficient hierarchy that can be used with [Azure Policy](../azure-policy/azure-policy-introduction.md) and [Azure Role Based Access Controls](../role-based-access-control/overview.md).</span></span> <span data-ttu-id="83b2c-106">For more information on management groups, see [Organize your resources with Azure management groups ](management-groups-overview.md).</span><span class="sxs-lookup"><span data-stu-id="83b2c-106">For more information on management groups, see [Organize your resources with Azure management groups ](management-groups-overview.md).</span></span>

<span data-ttu-id="83b2c-107">The first management group created in the directory could take up to 15 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="83b2c-107">The first management group created in the directory could take up to 15 minutes to complete.</span></span> <span data-ttu-id="83b2c-108">There are processes that run the first time to set up the management groups service within Azure for your directory.</span><span class="sxs-lookup"><span data-stu-id="83b2c-108">There are processes that run the first time to set up the management groups service within Azure for your directory.</span></span> <span data-ttu-id="83b2c-109">You receive a notification when the process is complete.</span><span class="sxs-lookup"><span data-stu-id="83b2c-109">You receive a notification when the process is complete.</span></span>  

## <a name="create-a-management-group"></a><span data-ttu-id="83b2c-110">Create a management group</span><span class="sxs-lookup"><span data-stu-id="83b2c-110">Create a management group</span></span>

<span data-ttu-id="83b2c-111">You can create the management group by using the portal, PowerShell, or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="83b2c-111">You can create the management group by using the portal, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="83b2c-112">Currently, you can't use Resource Manager templates to create management groups.</span><span class="sxs-lookup"><span data-stu-id="83b2c-112">Currently, you can't use Resource Manager templates to create management groups.</span></span>

### <a name="create-in-portal"></a><span data-ttu-id="83b2c-113">Create in portal</span><span class="sxs-lookup"><span data-stu-id="83b2c-113">Create in portal</span></span>

1. <span data-ttu-id="83b2c-114">Log into the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83b2c-114">Log into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="83b2c-115">Select **All services** > **Management groups**.</span><span class="sxs-lookup"><span data-stu-id="83b2c-115">Select **All services** > **Management groups**.</span></span>
3. <span data-ttu-id="83b2c-116">On the main page, select **New Management group.**</span><span class="sxs-lookup"><span data-stu-id="83b2c-116">On the main page, select **New Management group.**</span></span>

    ![Main Group](media/management-groups/main.png)
4.  <span data-ttu-id="83b2c-118">Fill in the management group ID field.</span><span class="sxs-lookup"><span data-stu-id="83b2c-118">Fill in the management group ID field.</span></span>
    - <span data-ttu-id="83b2c-119">The **Management Group ID** is the directory unique identifier that is used to submit commands on this management group.</span><span class="sxs-lookup"><span data-stu-id="83b2c-119">The **Management Group ID** is the directory unique identifier that is used to submit commands on this management group.</span></span> <span data-ttu-id="83b2c-120">This identifier is not editable after creation as it is used throughout the Azure system to identify this group.</span><span class="sxs-lookup"><span data-stu-id="83b2c-120">This identifier is not editable after creation as it is used throughout the Azure system to identify this group.</span></span>
    - <span data-ttu-id="83b2c-121">The display name field is the name that is displayed within the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="83b2c-121">The display name field is the name that is displayed within the Azure portal.</span></span> <span data-ttu-id="83b2c-122">A separate display name is an optional field when creating the management group and can be changed at any time.</span><span class="sxs-lookup"><span data-stu-id="83b2c-122">A separate display name is an optional field when creating the management group and can be changed at any time.</span></span>  

    ![Create](media/management-groups/create_context_menu.png)  
5.  <span data-ttu-id="83b2c-124">Select **Save**</span><span class="sxs-lookup"><span data-stu-id="83b2c-124">Select **Save**</span></span>

### <a name="create-in-powershell"></a><span data-ttu-id="83b2c-125">Create in PowerShell</span><span class="sxs-lookup"><span data-stu-id="83b2c-125">Create in PowerShell</span></span>

<span data-ttu-id="83b2c-126">Within PowerShell, you use the Add-AzureRmManagementGroups cmdlets:</span><span class="sxs-lookup"><span data-stu-id="83b2c-126">Within PowerShell, you use the Add-AzureRmManagementGroups cmdlets:</span></span>

```azurepowershell-interactive
C:\> New-AzureRmManagementGroup -GroupName Contoso
```

<span data-ttu-id="83b2c-127">The **GroupName** is a unique identifier being created.</span><span class="sxs-lookup"><span data-stu-id="83b2c-127">The **GroupName** is a unique identifier being created.</span></span> <span data-ttu-id="83b2c-128">This ID is used by other commands to reference this group and it cannot be changed later.</span><span class="sxs-lookup"><span data-stu-id="83b2c-128">This ID is used by other commands to reference this group and it cannot be changed later.</span></span>

<span data-ttu-id="83b2c-129">If you wanted the management group to show a different name within the Azure portal, you would add the **DisplayName** parameter with the string.</span><span class="sxs-lookup"><span data-stu-id="83b2c-129">If you wanted the management group to show a different name within the Azure portal, you would add the **DisplayName** parameter with the string.</span></span> <span data-ttu-id="83b2c-130">For example, if you wanted to create a management group with the GroupName of Contoso and the display name of "Contoso Group", you would use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="83b2c-130">For example, if you wanted to create a management group with the GroupName of Contoso and the display name of "Contoso Group", you would use the following cmdlet:</span></span>

```azurepowershell-interactive
C:\> New-AzureRmManagementGroup -GroupName Contoso -DisplayName "Contoso Group" -ParentId ContosoTenant
```

<span data-ttu-id="83b2c-131">Use the **ParentId** parameter to have this management group be created under a different management.</span><span class="sxs-lookup"><span data-stu-id="83b2c-131">Use the **ParentId** parameter to have this management group be created under a different management.</span></span>  

### <a name="create-in-azure-cli"></a><span data-ttu-id="83b2c-132">Create in Azure CLI</span><span class="sxs-lookup"><span data-stu-id="83b2c-132">Create in Azure CLI</span></span>

<span data-ttu-id="83b2c-133">On Azure CLI, you use the az account management-group create command.</span><span class="sxs-lookup"><span data-stu-id="83b2c-133">On Azure CLI, you use the az account management-group create command.</span></span>

```azure-cli
C:\ az account management-group create --group-name <YourGroupName>
```

---

## <a name="next-steps"></a><span data-ttu-id="83b2c-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="83b2c-134">Next steps</span></span> 
<span data-ttu-id="83b2c-135">To Learn more about management groups, see:</span><span class="sxs-lookup"><span data-stu-id="83b2c-135">To Learn more about management groups, see:</span></span> 
- [<span data-ttu-id="83b2c-136">Organize your resources with Azure management groups </span><span class="sxs-lookup"><span data-stu-id="83b2c-136">Organize your resources with Azure management groups </span></span>](management-groups-overview.md)
- [<span data-ttu-id="83b2c-137">How to change, delete, or manage your management groups</span><span class="sxs-lookup"><span data-stu-id="83b2c-137">How to change, delete, or manage your management groups</span></span>](management-groups-manage.md)
- [<span data-ttu-id="83b2c-138">Install the Azure Powershell module</span><span class="sxs-lookup"><span data-stu-id="83b2c-138">Install the Azure Powershell module</span></span>](https://www.powershellgallery.com/packages/AzureRM.ManagementGroups/0.0.1-preview)
- [<span data-ttu-id="83b2c-139">Review the REST API Spec</span><span class="sxs-lookup"><span data-stu-id="83b2c-139">Review the REST API Spec</span></span>](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/managementgroups/resource-manager/Microsoft.Management/preview)
- [<span data-ttu-id="83b2c-140">Install the Azure CLI Extension</span><span class="sxs-lookup"><span data-stu-id="83b2c-140">Install the Azure CLI Extension</span></span>](https://docs.microsoft.com/cli/azure/extension?view=azure-cli-latest#az-extension-list-available)
