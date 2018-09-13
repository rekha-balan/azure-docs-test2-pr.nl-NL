---
title: Require user assignment - Azure AD | Microsoft Docs'
description: How to require user assignment for Azure applications.
services: active-directory
documentationcenter: ''
author: IHenkel
manager: femila
editor: ''
ms.assetid: 30b78cba-1e0f-472f-8314-f2250a9b91c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: inhenk
ms.openlocfilehash: f5804d258c609f2bf289dcf4d173dc67137e7691
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550673"
---
# <a name="azure-ad-and-applications-require-user-assignment"></a>Azure AD and applications: Require user assignment
## <a name="requiring-user-assignment"></a>Requiring User Assignment
1. Log in to the Azure portal with an administrator account.
2. Click on the **All Items** item in the main menu.
3. Choose the directory you are using for the application.
4. Click on the **APPLICATIONS** tab.
5. Select the application from the list of applications associated with this directory.
6. Click the **CONFIGURE** tab.
7. Change the **User Assignment Required to Access App** toggle to Yes.
8. Click the **Save** button at the bottom of the screen.

You will now have to assign users and/or groups to the application. See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) and [Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md).

## <a name="next-steps"></a>Next Steps
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]