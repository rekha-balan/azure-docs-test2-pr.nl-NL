---
title: Add a user to your Azure RemoteApp collection | Microsoft Docs
description: Learn how to add users to your Azure RemoteApp collection
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: a84aa7e3ac7de717c2a628abcf6f5f11b05411e8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553734"
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a>How to add a user to your Azure RemoteApp collection
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
> 
> 

Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection. This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.

What account information do you need? That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.

## <a name="supported-user-identities"></a>Supported user identities
The different collection types (cloud vs. hybrid) support using different user identities for access to applications.  

For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on). Additionally, you need to create some Active Directory objects in the on-premises directory.  

For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.  See the table below.

Office 365 users are Azure Active Directory users. If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.   

You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.

| User accounts | Cloud | Hybrid |
| --- | --- | --- |
| Microsoft Account |Yes |No |
| Azure Active Directory (Azure AD) | | |
| Azure AD cloud only |Yes |No |
| ADsync with password sync |Yes |Yes |
| ADsync without password sync |Yes |No |
| ADsync with AD FS |Yes |Yes |
| [3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping) |Yes |Yes |
| Multi-Factor Authentication |Yes |Yes |

Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.

> [!NOTE]
> The Azure Active Directory users must be from the tenant that's associated with your subscription. (You can view and modify your subscription on the **Settings** tab in the portal. See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)
> 
> 

## <a name="office-365-proplus-user-account-information"></a>Office 365 ProPlus user account information
If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription. See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.

