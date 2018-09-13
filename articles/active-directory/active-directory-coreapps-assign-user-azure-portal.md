---
title: Assign a user or group to an enterprise app in Azure Active Directory preview | Microsoft Docs
description: How to select an enterprise app to assign a user or group to it in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 2d9add1a20e730e5ec1c4c0fb6e2b3d23145eb8a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551822"
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory-preview"></a><span data-ttu-id="f3397-103">Assign a user or group to an enterprise app in Azure Active Directory preview</span><span class="sxs-lookup"><span data-stu-id="f3397-103">Assign a user or group to an enterprise app in Azure Active Directory preview</span></span>
<span data-ttu-id="f3397-104">It's easy to assign a user or a group to your enterprise applications in Azure Active Directory (Azure AD) preview.</span><span class="sxs-lookup"><span data-stu-id="f3397-104">It's easy to assign a user or a group to your enterprise applications in Azure Active Directory (Azure AD) preview.</span></span> [<span data-ttu-id="f3397-105">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="f3397-105">What's in the preview?</span></span>](active-directory-preview-explainer.md) <span data-ttu-id="f3397-106">You must have the appropriate permissions to manage the enterprise app.</span><span class="sxs-lookup"><span data-stu-id="f3397-106">You must have the appropriate permissions to manage the enterprise app.</span></span> <span data-ttu-id="f3397-107">In the current preview, you must be global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="f3397-107">In the current preview, you must be global admin for the directory.</span></span>

## <a name="how-do-i-assign-user-access-to-an-enterprise-app"></a><span data-ttu-id="f3397-108">How do I assign user access to an enterprise app?</span><span class="sxs-lookup"><span data-stu-id="f3397-108">How do I assign user access to an enterprise app?</span></span>
1. <span data-ttu-id="f3397-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="f3397-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="f3397-110">Select **More services**, enter Azure Active Directory in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="f3397-110">Select **More services**, enter Azure Active Directory in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="f3397-111">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f3397-111">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Opening Enterprise apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="f3397-113">On the **Enterprise applications** blade, select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f3397-113">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="f3397-114">You'll see a list of the apps you can manage.</span><span class="sxs-lookup"><span data-stu-id="f3397-114">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="f3397-115">On the **Enterprise applications - All applications** blade, select an app.</span><span class="sxs-lookup"><span data-stu-id="f3397-115">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="f3397-116">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span><span class="sxs-lookup"><span data-stu-id="f3397-116">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Selecting the all applications command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="f3397-118">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span><span class="sxs-lookup"><span data-stu-id="f3397-118">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span></span>
8. <span data-ttu-id="f3397-119">On the **Add Assignment** blade, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f3397-119">On the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Assign a user or group to the app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="f3397-121">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="f3397-121">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span></span>
10. <span data-ttu-id="f3397-122">On the **Add Assignment** blade, select **Role**.</span><span class="sxs-lookup"><span data-stu-id="f3397-122">On the **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="f3397-123">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="f3397-123">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span></span>
11. <span data-ttu-id="f3397-124">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="f3397-124">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span></span> <span data-ttu-id="f3397-125">The assigned users or groups will have the permissions defined by the selected role for this enterprise app.</span><span class="sxs-lookup"><span data-stu-id="f3397-125">The assigned users or groups will have the permissions defined by the selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3397-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3397-126">Next steps</span></span>
* [<span data-ttu-id="f3397-127">See all of my groups</span><span class="sxs-lookup"><span data-stu-id="f3397-127">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="f3397-128">Remove a user or group assignment from an enterprise app</span><span class="sxs-lookup"><span data-stu-id="f3397-128">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="f3397-129">Disable user sign-ins for an enterprise app</span><span class="sxs-lookup"><span data-stu-id="f3397-129">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="f3397-130">Change the name or logo of an enterprise app</span><span class="sxs-lookup"><span data-stu-id="f3397-130">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)



