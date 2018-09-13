---
title: Restore a deleted Office 365 group in Azure AD | Microsoft Docs
description: How to restore a deleted group, view restorable groups, and permamnently delete a group in Azure Active Directory
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: quickstart
ms.date: 08/28/2017
ms.author: lizross
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 3b2264817dce63885ce0c428fe4df8427f7cdde6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868194"
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="57ee4-103">Restore a deleted Office 365 group in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57ee4-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="57ee4-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD), the deleted group is retained but not visible for 30 days from the deletion date.</span><span class="sxs-lookup"><span data-stu-id="57ee4-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD), the deleted group is retained but not visible for 30 days from the deletion date.</span></span> <span data-ttu-id="57ee4-105">This behavior is so that the group and its contents can be restored if needed.</span><span class="sxs-lookup"><span data-stu-id="57ee4-105">This behavior is so that the group and its contents can be restored if needed.</span></span> <span data-ttu-id="57ee4-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57ee4-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span></span> <span data-ttu-id="57ee4-107">It is not available for security groups and distribution groups.</span><span class="sxs-lookup"><span data-stu-id="57ee4-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="57ee4-108">Don't use `Remove-MsolGroup` because it purges the group permanently.</span><span class="sxs-lookup"><span data-stu-id="57ee4-108">Don't use `Remove-MsolGroup` because it purges the group permanently.</span></span> <span data-ttu-id="57ee4-109">Always use `Remove-AzureADMSGroup` to delete an O365 group.</span><span class="sxs-lookup"><span data-stu-id="57ee4-109">Always use `Remove-AzureADMSGroup` to delete an O365 group.</span></span>

<span data-ttu-id="57ee4-110">The permissions required to restore a group can be any of the following:</span><span class="sxs-lookup"><span data-stu-id="57ee4-110">The permissions required to restore a group can be any of the following:</span></span>

<span data-ttu-id="57ee4-111">Role</span><span class="sxs-lookup"><span data-stu-id="57ee4-111">Role</span></span> | <span data-ttu-id="57ee4-112">Permissions</span><span class="sxs-lookup"><span data-stu-id="57ee4-112">Permissions</span></span>
--------- | ---------
<span data-ttu-id="57ee4-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span><span class="sxs-lookup"><span data-stu-id="57ee4-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="57ee4-114">Can restore any deleted Office 365 group</span><span class="sxs-lookup"><span data-stu-id="57ee4-114">Can restore any deleted Office 365 group</span></span>
<span data-ttu-id="57ee4-115">User Account Administrator and Partner Tier1 support</span><span class="sxs-lookup"><span data-stu-id="57ee4-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="57ee4-116">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span><span class="sxs-lookup"><span data-stu-id="57ee4-116">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span></span>
<span data-ttu-id="57ee4-117">User</span><span class="sxs-lookup"><span data-stu-id="57ee4-117">User</span></span> | <span data-ttu-id="57ee4-118">Can restore any deleted Office 365 group that they owned</span><span class="sxs-lookup"><span data-stu-id="57ee4-118">Can restore any deleted Office 365 group that they owned</span></span>


## <a name="view-the-deleted-office-365-groups-that-are-available-to-restore"></a><span data-ttu-id="57ee4-119">View the deleted Office 365 groups that are available to restore</span><span class="sxs-lookup"><span data-stu-id="57ee4-119">View the deleted Office 365 groups that are available to restore</span></span>

<span data-ttu-id="57ee4-120">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span><span class="sxs-lookup"><span data-stu-id="57ee4-120">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="57ee4-121">These cmdlets are part of the [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="57ee4-121">These cmdlets are part of the [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="57ee4-122">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span><span class="sxs-lookup"><span data-stu-id="57ee4-122">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="57ee4-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span><span class="sxs-lookup"><span data-stu-id="57ee4-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span></span>
   
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="57ee4-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span><span class="sxs-lookup"><span data-stu-id="57ee4-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span></span>
  
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```

## <a name="how-to-restore-your-deleted-office-365-group"></a><span data-ttu-id="57ee4-125">How to restore your deleted Office 365 group</span><span class="sxs-lookup"><span data-stu-id="57ee4-125">How to restore your deleted Office 365 group</span></span>
<span data-ttu-id="57ee4-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span><span class="sxs-lookup"><span data-stu-id="57ee4-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span></span> <span data-ttu-id="57ee4-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span><span class="sxs-lookup"><span data-stu-id="57ee4-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span></span>

1.  <span data-ttu-id="57ee4-128">Run the following cmdlet to restore the group and its contents.</span><span class="sxs-lookup"><span data-stu-id="57ee4-128">Run the following cmdlet to restore the group and its contents.</span></span>
 
 ```
 Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
 ``` 

<span data-ttu-id="57ee4-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span><span class="sxs-lookup"><span data-stu-id="57ee4-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span></span>
 ```
 Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
 ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="57ee4-130">How do you know this worked?</span><span class="sxs-lookup"><span data-stu-id="57ee4-130">How do you know this worked?</span></span>

<span data-ttu-id="57ee4-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span><span class="sxs-lookup"><span data-stu-id="57ee4-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span></span> <span data-ttu-id="57ee4-132">After the restore request is completed:</span><span class="sxs-lookup"><span data-stu-id="57ee4-132">After the restore request is completed:</span></span>

- <span data-ttu-id="57ee4-133">The group appears in the Left navigation bar on Exchange</span><span class="sxs-lookup"><span data-stu-id="57ee4-133">The group appears in the Left navigation bar on Exchange</span></span>
- <span data-ttu-id="57ee4-134">The plan for the group will appear in Planner</span><span class="sxs-lookup"><span data-stu-id="57ee4-134">The plan for the group will appear in Planner</span></span>
- <span data-ttu-id="57ee4-135">Any Sharepoint sites and all of their contents will be available</span><span class="sxs-lookup"><span data-stu-id="57ee4-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="57ee4-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span><span class="sxs-lookup"><span data-stu-id="57ee4-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>

## <a name="next-steps"></a><span data-ttu-id="57ee4-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="57ee4-137">Next steps</span></span>
<span data-ttu-id="57ee4-138">These articles provide additional information on Azure Active Directory groups.</span><span class="sxs-lookup"><span data-stu-id="57ee4-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="57ee4-139">See existing groups</span><span class="sxs-lookup"><span data-stu-id="57ee4-139">See existing groups</span></span>](../fundamentals/active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="57ee4-140">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="57ee4-140">Manage settings of a group</span></span>](../fundamentals/active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="57ee4-141">Manage members of a group</span><span class="sxs-lookup"><span data-stu-id="57ee4-141">Manage members of a group</span></span>](../fundamentals/active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="57ee4-142">Manage memberships of a group</span><span class="sxs-lookup"><span data-stu-id="57ee4-142">Manage memberships of a group</span></span>](../fundamentals/active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="57ee4-143">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="57ee4-143">Manage dynamic rules for users in a group</span></span>](groups-dynamic-membership.md)
