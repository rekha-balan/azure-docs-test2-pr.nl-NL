---
title: Access reporting - Azure RBAC | Microsoft Docs
description: Generate a report that lists all changes in access to your Azure subscriptions with Role-Based Access Control over the past 90 days.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: ''
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e0b49302c0799d33e5dec008e8a298343b6570f5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554538"
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="66623-103">Create an access report for Role-Based Access Control</span><span class="sxs-lookup"><span data-stu-id="66623-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="66623-104">Any time someone grants or revokes access within your subscriptions, the changes get logged in Azure events.</span><span class="sxs-lookup"><span data-stu-id="66623-104">Any time someone grants or revokes access within your subscriptions, the changes get logged in Azure events.</span></span> <span data-ttu-id="66623-105">You can create access change history reports to see all changes for the past 90 days.</span><span class="sxs-lookup"><span data-stu-id="66623-105">You can create access change history reports to see all changes for the past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="66623-106">Create a report with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="66623-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="66623-107">To create an access change history report in PowerShell, use the `Get-AzureRMAuthorizationChangeLog` command.</span><span class="sxs-lookup"><span data-stu-id="66623-107">To create an access change history report in PowerShell, use the `Get-AzureRMAuthorizationChangeLog` command.</span></span> <span data-ttu-id="66623-108">More details about this cmdlet are available in the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureRM.Storage/1.0.6/Content/ResourceManagerStartup.ps1).</span><span class="sxs-lookup"><span data-stu-id="66623-108">More details about this cmdlet are available in the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureRM.Storage/1.0.6/Content/ResourceManagerStartup.ps1).</span></span>

<span data-ttu-id="66623-109">When you call this command, you can specify which property of the assignments you want listed, including the following:</span><span class="sxs-lookup"><span data-stu-id="66623-109">When you call this command, you can specify which property of the assignments you want listed, including the following:</span></span>

| <span data-ttu-id="66623-110">Property</span><span class="sxs-lookup"><span data-stu-id="66623-110">Property</span></span> | <span data-ttu-id="66623-111">Description</span><span class="sxs-lookup"><span data-stu-id="66623-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66623-112">**Action**</span><span class="sxs-lookup"><span data-stu-id="66623-112">**Action**</span></span> |<span data-ttu-id="66623-113">Whether access was granted or revoked</span><span class="sxs-lookup"><span data-stu-id="66623-113">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="66623-114">**Caller**</span><span class="sxs-lookup"><span data-stu-id="66623-114">**Caller**</span></span> |<span data-ttu-id="66623-115">The owner responsible for the access change</span><span class="sxs-lookup"><span data-stu-id="66623-115">The owner responsible for the access change</span></span> |
| <span data-ttu-id="66623-116">**Date**</span><span class="sxs-lookup"><span data-stu-id="66623-116">**Date**</span></span> |<span data-ttu-id="66623-117">The date and time that access was changed</span><span class="sxs-lookup"><span data-stu-id="66623-117">The date and time that access was changed</span></span> |
| <span data-ttu-id="66623-118">**DirectoryName**</span><span class="sxs-lookup"><span data-stu-id="66623-118">**DirectoryName**</span></span> |<span data-ttu-id="66623-119">The Azure Active Directory directory</span><span class="sxs-lookup"><span data-stu-id="66623-119">The Azure Active Directory directory</span></span> |
| <span data-ttu-id="66623-120">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="66623-120">**PrincipalName**</span></span> |<span data-ttu-id="66623-121">The name of the user, group, or application</span><span class="sxs-lookup"><span data-stu-id="66623-121">The name of the user, group, or application</span></span> |
| <span data-ttu-id="66623-122">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="66623-122">**PrincipalType**</span></span> |<span data-ttu-id="66623-123">Whether the assignment was for a user, group, or application</span><span class="sxs-lookup"><span data-stu-id="66623-123">Whether the assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="66623-124">**RoleId**</span><span class="sxs-lookup"><span data-stu-id="66623-124">**RoleId**</span></span> |<span data-ttu-id="66623-125">The GUID of the role that was granted or revoked</span><span class="sxs-lookup"><span data-stu-id="66623-125">The GUID of the role that was granted or revoked</span></span> |
| <span data-ttu-id="66623-126">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="66623-126">**RoleName**</span></span> |<span data-ttu-id="66623-127">The role that was granted or revoked</span><span class="sxs-lookup"><span data-stu-id="66623-127">The role that was granted or revoked</span></span> |
| <span data-ttu-id="66623-128">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="66623-128">**ScopeName**</span></span> |<span data-ttu-id="66623-129">The name of the subscription, resource group, or resource</span><span class="sxs-lookup"><span data-stu-id="66623-129">The name of the subscription, resource group, or resource</span></span> |
| <span data-ttu-id="66623-130">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="66623-130">**ScopeType**</span></span> |<span data-ttu-id="66623-131">Whether the assignment was at the subscription, resource group, or resource scope</span><span class="sxs-lookup"><span data-stu-id="66623-131">Whether the assignment was at the subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="66623-132">**SubscriptionId**</span><span class="sxs-lookup"><span data-stu-id="66623-132">**SubscriptionId**</span></span> |<span data-ttu-id="66623-133">The GUID of the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="66623-133">The GUID of the Azure subscription</span></span> |
| <span data-ttu-id="66623-134">**SubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="66623-134">**SubscriptionName**</span></span> |<span data-ttu-id="66623-135">The name of the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="66623-135">The name of the Azure subscription</span></span> |

<span data-ttu-id="66623-136">This example command lists all access changes in the subscription for the past seven days:</span><span class="sxs-lookup"><span data-stu-id="66623-136">This example command lists all access changes in the subscription for the past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="66623-138">Create a report with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="66623-138">Create a report with Azure CLI</span></span>
<span data-ttu-id="66623-139">To create an access change history report in the Azure command-line interface (CLI), use the `azure role assignment changelog list` command.</span><span class="sxs-lookup"><span data-stu-id="66623-139">To create an access change history report in the Azure command-line interface (CLI), use the `azure role assignment changelog list` command.</span></span>

## <a name="export-to-a-spreadsheet"></a><span data-ttu-id="66623-140">Export to a spreadsheet</span><span class="sxs-lookup"><span data-stu-id="66623-140">Export to a spreadsheet</span></span>
<span data-ttu-id="66623-141">To save the report, or manipulate the data, export the access changes into a .csv file.</span><span class="sxs-lookup"><span data-stu-id="66623-141">To save the report, or manipulate the data, export the access changes into a .csv file.</span></span> <span data-ttu-id="66623-142">You can then view the report in a spreadsheet for review.</span><span class="sxs-lookup"><span data-stu-id="66623-142">You can then view the report in a spreadsheet for review.</span></span>

![Changelog viewed as spreadsheet - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="66623-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="66623-144">Next steps</span></span>
* <span data-ttu-id="66623-145">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="66623-145">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="66623-146">Learn how to manage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="66623-146">Learn how to manage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>



