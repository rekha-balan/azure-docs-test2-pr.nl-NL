---
title: Azure Active Directory preview explainer | Microsoft Docs
description: A topic that explains the differences between Azure Active Directory in the classic portal and the Azure Active Directory preview in the Azure portal.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: e717c11c-e7c9-4565-8e47-1950905e5b3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 8f7a679dc5b5726107503a9f7363ab162b1770d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548882"
---
# <a name="preview-of-the-azure-active-directory-management-experience-in-the-azure-portal"></a>Preview of the Azure Active Directory management experience in the Azure portal
The Azure Active Directory (Azure AD) management experience is in preview in the Azure portal. You can try it out by signing in to [the Azure portal](https://portal.azure.com) as a global administrator of your directory. Then, select Azure Active Directory in the services list if it is visible, or select **More services** to view the list of all services. You do not need an Azure subscription to use the Azure AD management experience in the Azure portal.

## <a name="learn-about-what-you-can-do-in-the-preview-experience"></a>Learn about what you can do in the preview experience
The preview experience enables you to manage many directory resources such as users, groups,  applications, and directory settings in the Azure portal. We are improving this experience to include all the capabilities that exist in the Azure AD management experience in the [Azure classic portal](https://manage.windowsazure.com). Until then, there are some directory management tasks that you must still complete in the classic portal.

## <a name="manage-the-same-azure-ad-tenants"></a>Manage the same Azure AD tenants
The preview experience reads and writes to the same Azure Active Directory tenant as the classic portal and the Office 365 Admin center. Changes that are made in any of these portals are reflected in all the other portals.

## <a name="use-the-same-authorization-logic"></a>Use the same authorization logic
The preview experience uses the same authorization logic as existing Active Directory clients. Users are authorized to make changes to directory resources based on their directory role, such as global administrator, user administrator, and password administrator. Having a role on Azure resources or an Azure subscription doesn't give users the authorization to manage directory resources. For more information about Azure AD management roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).

The preview experience is optimized for global administrators. If you use the preview experience while signed in as a user that is not a global administrator, you might have a degraded experience. For example, you might be able to select a button that lets you begin a task that you can't complete in the directory. We will be improving this experience soon.

## <a name="next-steps"></a>Next steps
You can provide feedback on the preview experience in the admin portal section of the [Azure AD feedback forum](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD&filter=alltypes&sort=lastpostdesc).
