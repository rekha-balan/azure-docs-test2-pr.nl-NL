---
title: How to select permissions for a given API | Microsoft Docs
description: How to find the authentication endpoints for a custom application you are developing or registering with Azure AD.
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: 3578684ac8c92ff195b19740b28ef9adebdc7309
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549787"
---
# <a name="how-to-select-permissions-for-a-given-api"></a>How to select permissions for a given API

You can find the authentication endpoints for your application in the [Azure portal](https://portal.azure.com).

-   Navigate to the [Azure portal](https://portal.azure.com).

-   From the left navigation pane, click **Azure Active Directory**.

-   Click **App Registrations** and choose **Endpoints**.

-   This open up the **Endpoints** page, which list all the authentication endpoints for your tenant.

-   Use the endpoint specific to the authentication protocol you are using, in conjunction with the application ID to craft the authentication request specific to your application.

## <a name="next-steps"></a>Next steps
[Azure Active Directory developer's guide](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide#authentication-and-authorization-protocols)
