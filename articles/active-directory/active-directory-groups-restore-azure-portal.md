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
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a>Restore a deleted Office 365 group in Azure Active Directory

When you delete an Office 365 group in the Azure Active Directory (Azure AD) preview, the deleted group is retained but not visible for 30 days from the deletion date. This is so that the group and its contents can be restored if needed. This functionality is restricted exclusively to Office 365 groups in Azure AD. It is not available for security groups and distribution groups.

The permissions required to restore a group can be any of the following:

Role  | Permissions 
--------- | ---------
Company Administrator, Partner Tier2 support, and InTune Service Admins | Can restore any deleted Office 365 group 
User Account Administrator and Partner Tier1 support | Can restore any deleted Office 365 group except those assigned to the Company Administrator role 
User | Can restore any deleted Office 365 group that they owned 


## <a name="how-to-view-deleted-office-365-groups-that-are-available-to-restore"></a>How to view deleted Office 365 groups that are available to restore
The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged. These cmdlets are part of the [Azure Active Directory PowerShell V2 Preview module](https://www.powershellgallery.com/packages/AzureADPreview). More information about this module can be found in the [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/) article.
Please note that the cmdlets for managing soft delete and revoery are in Public Preview and we sometimes need to make breaking changes to preview cmdlets. For this reason, using these cmdlets in a production environment is discouraged.

1.  Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-to-restore-an-office-365-group"></a>How to restore an Office 365 group
Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps. If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.

1.  Run the following cmdlet to restore the group and its contents.
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

Alternatively, the following cmdlet can be run to permanently remove the deleted group.
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a>How do you know this worked?
To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group. After the restore request is completed:
- The group will appear in the Left nav bar on Exchange
- The plan for the group will appear in Planner
- Any Sharepoint sites and all of their contents will be available
- The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups


## <a name="next-steps"></a>Next steps
These articles provide additional information on Azure Active Directory groups.

* [See existing groups](active-directory-groups-view-azure-portal.md)
* [Manage settings of a group](active-directory-groups-settings-azure-portal.md)
* [Manage members of a group](active-directory-groups-members-azure-portal.md)
* [Manage memberships of a group](active-directory-groups-membership-azure-portal.md)
* [Manage dynamic rules for users in a group](active-directory-groups-dynamic-membership-azure-portal.md)
