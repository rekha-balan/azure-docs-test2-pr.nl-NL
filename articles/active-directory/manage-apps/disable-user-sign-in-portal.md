---
title: Disable user sign-ins for an enterprise app in Azure Active Directory | Microsoft Docs
description: How to disable an enterprise application so that no users may sign in to it in Azure Active Directory
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/28/2017
ms.author: barbkess
ms.reviewer: asteen
ms.custom: it-pro
ms.openlocfilehash: 39e926a392cbd87eff23e25d9708792ec7c40a2c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868047"
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="ce256-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce256-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="ce256-104">It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce256-104">It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ce256-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="ce256-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="ce256-106">How do I disable user sign-ins?</span><span class="sxs-lookup"><span data-stu-id="ce256-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="ce256-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="ce256-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="ce256-108">Select **All services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ce256-108">Select **All services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="ce256-109">On the **Azure Active Directory** -  ***directoryname*** pane (that is, the Azure AD pane for the directory you are managing), select **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ce256-109">On the **Azure Active Directory** -  ***directoryname*** pane (that is, the Azure AD pane for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Opening Enterprise apps](./media/disable-user-sign-in-portal/open-enterprise-apps.png)
4. <span data-ttu-id="ce256-111">On the **Enterprise applications** pane, select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ce256-111">On the **Enterprise applications** pane, select **All applications**.</span></span> <span data-ttu-id="ce256-112">You see a list of the apps you can manage.</span><span class="sxs-lookup"><span data-stu-id="ce256-112">You see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="ce256-113">On the **Enterprise applications - All applications** pane, select an app.</span><span class="sxs-lookup"><span data-stu-id="ce256-113">On the **Enterprise applications - All applications** pane, select an app.</span></span>
6. <span data-ttu-id="ce256-114">On the ***appname*** pane (that is, the pane with the name of the selected app in the title), select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ce256-114">On the ***appname*** pane (that is, the pane with the name of the selected app in the title), select **Properties**.</span></span>

    ![Selecting the all applications command](./media/disable-user-sign-in-portal/select-app.png)
7. <span data-ttu-id="ce256-116">On the ***appname*** - **Properties** pane, select **No** for **Enabled for users to sign-in?**.</span><span class="sxs-lookup"><span data-stu-id="ce256-116">On the ***appname*** - **Properties** pane, select **No** for **Enabled for users to sign-in?**.</span></span>
8. <span data-ttu-id="ce256-117">Select the **Save** command.</span><span class="sxs-lookup"><span data-stu-id="ce256-117">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce256-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="ce256-118">Next steps</span></span>
* [<span data-ttu-id="ce256-119">See all my groups</span><span class="sxs-lookup"><span data-stu-id="ce256-119">See all my groups</span></span>](../fundamentals/active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="ce256-120">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="ce256-120">Assign a user or group to an enterprise app</span></span>](assign-user-or-group-access-portal.md)
* [<span data-ttu-id="ce256-121">Remove a user or group assignment from an enterprise app</span><span class="sxs-lookup"><span data-stu-id="ce256-121">Remove a user or group assignment from an enterprise app</span></span>](remove-user-or-group-access-portal.md)
* [<span data-ttu-id="ce256-122">Change the name or logo of an enterprise app</span><span class="sxs-lookup"><span data-stu-id="ce256-122">Change the name or logo of an enterprise app</span></span>](change-name-or-logo-portal.md)
