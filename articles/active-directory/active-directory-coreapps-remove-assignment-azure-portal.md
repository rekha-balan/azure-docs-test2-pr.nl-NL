---
title: Remove a user or group assignment from an enterprise app in Azure Active Directory preview | Microsoft Docs
description: How to remove the access assignment of a user or group from an enterprise app in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: e45249713fa2b5a0f60dff2a5a00e04f7561c135
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552995"
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory-preview"></a><span data-ttu-id="bbe26-103">Remove a user or group assignment from an enterprise app in Azure Active Directory preview</span><span class="sxs-lookup"><span data-stu-id="bbe26-103">Remove a user or group assignment from an enterprise app in Azure Active Directory preview</span></span>
<span data-ttu-id="bbe26-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD) preview.</span><span class="sxs-lookup"><span data-stu-id="bbe26-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD) preview.</span></span> [<span data-ttu-id="bbe26-105">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="bbe26-105">What's in the preview?</span></span>](active-directory-preview-explainer.md) <span data-ttu-id="bbe26-106">You must have the appropriate permissions to manage the enterprise app.</span><span class="sxs-lookup"><span data-stu-id="bbe26-106">You must have the appropriate permissions to manage the enterprise app.</span></span> <span data-ttu-id="bbe26-107">In the current preview, you must be global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="bbe26-107">In the current preview, you must be global admin for the directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="bbe26-108">How do I remove a user or group assignment?</span><span class="sxs-lookup"><span data-stu-id="bbe26-108">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="bbe26-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="bbe26-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="bbe26-110">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="bbe26-110">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="bbe26-111">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="bbe26-111">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Opening Enterprise apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="bbe26-113">On the **Enterprise applications** blade, select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bbe26-113">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="bbe26-114">You'll see a list of the apps you can manage.</span><span class="sxs-lookup"><span data-stu-id="bbe26-114">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="bbe26-115">On the **Enterprise applications - All applications** blade, select an app.</span><span class="sxs-lookup"><span data-stu-id="bbe26-115">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="bbe26-116">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span><span class="sxs-lookup"><span data-stu-id="bbe26-116">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Selecting users or groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="bbe26-118">On the ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select the **Remove** command.</span><span class="sxs-lookup"><span data-stu-id="bbe26-118">On the ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select the **Remove** command.</span></span> <span data-ttu-id="bbe26-119">Confirm your decision at the prompt.</span><span class="sxs-lookup"><span data-stu-id="bbe26-119">Confirm your decision at the prompt.</span></span>

    ![Selecting the Remove command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="bbe26-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="bbe26-121">Next steps</span></span>
* [<span data-ttu-id="bbe26-122">See all of my groups</span><span class="sxs-lookup"><span data-stu-id="bbe26-122">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="bbe26-123">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="bbe26-123">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="bbe26-124">Disable user sign-ins for an enterprise app</span><span class="sxs-lookup"><span data-stu-id="bbe26-124">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="bbe26-125">Change the name or logo of an enterprise app</span><span class="sxs-lookup"><span data-stu-id="bbe26-125">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)



