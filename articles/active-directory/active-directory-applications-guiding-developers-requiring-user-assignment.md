---
title: Require user assignment - Azure AD | Microsoft Docs'
description: How to require user assignment for Azure applications.
services: active-directory
documentationcenter: ''
author: kgremban
manager: mtillman
editor: ''
ms.assetid: 30b78cba-1e0f-472f-8314-f2250a9b91c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 4519681d9b91383d27c00a992f85b0cb5d74f235
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810406"
---
# <a name="azure-ad-and-applications-require-user-assignment"></a>Azure AD and applications: Require user assignment
## <a name="requiring-user-assignment"></a>Requiring User Assignment
1. Log in to the Azure portal with an administrator account.
2. Click on the **All services** item in the main menu.
3. Choose the directory you are using for the application.
4. Click on the **Enterprise applications** tab.
5. Select the application from the list of applications associated with this directory.
6. Click the **Properties** tab.
7. Change the **User assignment required?** toggle to Yes.
8. Click the **Save** button at the top of the screen.

You will now have to assign users and/or groups to the application. See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) and [Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md).

## <a name="next-steps"></a>Next Steps
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
