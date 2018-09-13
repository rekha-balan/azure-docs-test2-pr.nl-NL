---
title: Restore a deleted Office 365 group in Azure Active Directory preview | Microsoft Docs
description: How to restore a deleted group, view restorable groups, and permamnently delete a group in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: curtand
ms.openlocfilehash: 325d669f11891bf070d9bbb468af7427adda46d3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564056"
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="b9209-103">Restore a deleted Office 365 group in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9209-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="b9209-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD) preview, the deleted group is retained but not visible for 30 days from the deletion date.</span><span class="sxs-lookup"><span data-stu-id="b9209-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD) preview, the deleted group is retained but not visible for 30 days from the deletion date.</span></span> <span data-ttu-id="b9209-105">This is so that the group and its contents can be restored if needed.</span><span class="sxs-lookup"><span data-stu-id="b9209-105">This is so that the group and its contents can be restored if needed.</span></span> <span data-ttu-id="b9209-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9209-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span></span> <span data-ttu-id="b9209-107">It is not available for security groups and distribution groups.</span><span class="sxs-lookup"><span data-stu-id="b9209-107">It is not available for security groups and distribution groups.</span></span>

<span data-ttu-id="b9209-108">The permissions required to restore a group can be any of the following:</span><span class="sxs-lookup"><span data-stu-id="b9209-108">The permissions required to restore a group can be any of the following:</span></span>

<span data-ttu-id="b9209-109">Role</span><span class="sxs-lookup"><span data-stu-id="b9209-109">Role</span></span>  | <span data-ttu-id="b9209-110">Permissions</span><span class="sxs-lookup"><span data-stu-id="b9209-110">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="b9209-111">Company Administrator, Partner Tier2 support, and InTune Service Admins</span><span class="sxs-lookup"><span data-stu-id="b9209-111">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="b9209-112">Can restore any deleted Office 365 group</span><span class="sxs-lookup"><span data-stu-id="b9209-112">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="b9209-113">User Account Administrator and Partner Tier1 support</span><span class="sxs-lookup"><span data-stu-id="b9209-113">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="b9209-114">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span><span class="sxs-lookup"><span data-stu-id="b9209-114">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span></span> 
<span data-ttu-id="b9209-115">User</span><span class="sxs-lookup"><span data-stu-id="b9209-115">User</span></span> | <span data-ttu-id="b9209-116">Can restore any deleted Office 365 group that they owned</span><span class="sxs-lookup"><span data-stu-id="b9209-116">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="how-to-view-deleted-office-365-groups-that-are-available-to-restore"></a><span data-ttu-id="b9209-117">How to view deleted Office 365 groups that are available to restore</span><span class="sxs-lookup"><span data-stu-id="b9209-117">How to view deleted Office 365 groups that are available to restore</span></span>
<span data-ttu-id="b9209-118">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span><span class="sxs-lookup"><span data-stu-id="b9209-118">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="b9209-119">These cmdlets are part of the [Azure Active Directory PowerShell V2 Preview module](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="b9209-119">These cmdlets are part of the [Azure Active Directory PowerShell V2 Preview module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span> <span data-ttu-id="b9209-120">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/) article.</span><span class="sxs-lookup"><span data-stu-id="b9209-120">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/) article.</span></span>
<span data-ttu-id="b9209-121">Please note that the cmdlets for managing soft delete and revoery are in Public Preview and we sometimes need to make breaking changes to preview cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b9209-121">Please note that the cmdlets for managing soft delete and revoery are in Public Preview and we sometimes need to make breaking changes to preview cmdlets.</span></span> <span data-ttu-id="b9209-122">For this reason, using these cmdlets in a production environment is discouraged.</span><span class="sxs-lookup"><span data-stu-id="b9209-122">For this reason, using these cmdlets in a production environment is discouraged.</span></span>

1.  <span data-ttu-id="b9209-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span><span class="sxs-lookup"><span data-stu-id="b9209-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="b9209-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span><span class="sxs-lookup"><span data-stu-id="b9209-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-to-restore-an-office-365-group"></a><span data-ttu-id="b9209-125">How to restore an Office 365 group</span><span class="sxs-lookup"><span data-stu-id="b9209-125">How to restore an Office 365 group</span></span>
<span data-ttu-id="b9209-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span><span class="sxs-lookup"><span data-stu-id="b9209-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span></span> <span data-ttu-id="b9209-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span><span class="sxs-lookup"><span data-stu-id="b9209-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span></span>

1.  <span data-ttu-id="b9209-128">Run the following cmdlet to restore the group and its contents.</span><span class="sxs-lookup"><span data-stu-id="b9209-128">Run the following cmdlet to restore the group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="b9209-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span><span class="sxs-lookup"><span data-stu-id="b9209-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="b9209-130">How do you know this worked?</span><span class="sxs-lookup"><span data-stu-id="b9209-130">How do you know this worked?</span></span>
<span data-ttu-id="b9209-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span><span class="sxs-lookup"><span data-stu-id="b9209-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span></span> <span data-ttu-id="b9209-132">After the restore request is completed:</span><span class="sxs-lookup"><span data-stu-id="b9209-132">After the restore request is completed:</span></span>
- <span data-ttu-id="b9209-133">The group will appear in the Left nav bar on Exchange</span><span class="sxs-lookup"><span data-stu-id="b9209-133">The group will appear in the Left nav bar on Exchange</span></span>
- <span data-ttu-id="b9209-134">The plan for the group will appear in Planner</span><span class="sxs-lookup"><span data-stu-id="b9209-134">The plan for the group will appear in Planner</span></span>
- <span data-ttu-id="b9209-135">Any Sharepoint sites and all of their contents will be available</span><span class="sxs-lookup"><span data-stu-id="b9209-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="b9209-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span><span class="sxs-lookup"><span data-stu-id="b9209-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="b9209-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="b9209-137">Next steps</span></span>
<span data-ttu-id="b9209-138">These articles provide additional information on Azure Active Directory groups.</span><span class="sxs-lookup"><span data-stu-id="b9209-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="b9209-139">See existing groups</span><span class="sxs-lookup"><span data-stu-id="b9209-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="b9209-140">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="b9209-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="b9209-141">Manage members of a group</span><span class="sxs-lookup"><span data-stu-id="b9209-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="b9209-142">Manage memberships of a group</span><span class="sxs-lookup"><span data-stu-id="b9209-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="b9209-143">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="b9209-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
