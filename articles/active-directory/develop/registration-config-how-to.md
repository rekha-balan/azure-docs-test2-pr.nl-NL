---
title: How to select permissions for a given API | Microsoft Docs
description: How to find the authentication endpoints for a custom application you are developing or registering with Azure AD.
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/11/2018
ms.author: celested
ms.openlocfilehash: f6c2540d8f0bb49491a428b085d20067a36d970a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866446"
---
# <a name="how-to-select-permissions-for-a-given-api"></a><span data-ttu-id="4de0b-103">How to select permissions for a given API</span><span class="sxs-lookup"><span data-stu-id="4de0b-103">How to select permissions for a given API</span></span>

<span data-ttu-id="4de0b-104">You can find the authentication endpoints for your application in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4de0b-104">You can find the authentication endpoints for your application in the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="4de0b-105">Navigate to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4de0b-105">Navigate to the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="4de0b-106">From the left navigation pane, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4de0b-106">From the left navigation pane, click **Azure Active Directory**.</span></span>

-   <span data-ttu-id="4de0b-107">Click **App Registrations** and choose **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="4de0b-107">Click **App Registrations** and choose **Endpoints**.</span></span>

-   <span data-ttu-id="4de0b-108">This open up the **Endpoints** page, which list all the authentication endpoints for your tenant.</span><span class="sxs-lookup"><span data-stu-id="4de0b-108">This open up the **Endpoints** page, which list all the authentication endpoints for your tenant.</span></span>

-   <span data-ttu-id="4de0b-109">Use the endpoint specific to the authentication protocol you are using, in conjunction with the application ID to craft the authentication request specific to your application.</span><span class="sxs-lookup"><span data-stu-id="4de0b-109">Use the endpoint specific to the authentication protocol you are using, in conjunction with the application ID to craft the authentication request specific to your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4de0b-110">Next steps</span><span class="sxs-lookup"><span data-stu-id="4de0b-110">Next steps</span></span>
[<span data-ttu-id="4de0b-111">Azure Active Directory developer's guide</span><span class="sxs-lookup"><span data-stu-id="4de0b-111">Azure Active Directory developer's guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide#authentication-and-authorization-protocols)
