---
title: Assign icenses for Azure MFA | Microsoft Docs
description: Learn how to assign user licenses for Microsoft Azure Multi-Factor Authentication.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/13/2017
ms.author: kgremban
ROBOTS: NOINDEX
ms.openlocfilehash: 566d268d682b7471ea5162a436397122430095c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562748"
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-to-users"></a>Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license to users
If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need to create a Multi-Factor Auth provider. Once you assign the licenses to your users, you can begin enabling them for MFA.

## <a name="to-assign-a-license"></a>To assign a license
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.
2. On the left, select **Active Directory**.
3. On the Active Directory page, double-click the directory that has the users you wish to enable.
4. At the top of the directory page, select **Licenses**.
   ![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign1.png)
5. On the Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.  If you only have one, then it should be selected automatically.
6. At the bottom of the page, click **Assign**.
   ![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign3.png)
7. In the box that comes up, click next to the users or groups you want to assign licenses to.  You should see a green check mark appear.
8. Click the check mark icon to save the changes.
   ![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign4.png)
9. You should see a message saying how many licenses were assigned and how many may have failed.  Click **Ok**.
   ![Assign Licenses](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-assign-licenses/assign5.png)

## <a name="next-steps"></a>Next steps

- For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)



