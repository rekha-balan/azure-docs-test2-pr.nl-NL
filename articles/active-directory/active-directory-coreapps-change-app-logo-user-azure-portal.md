---
title: Change the name or logo of an enterprise app in Azure Active Directory preview | Microsoft Docs
description: How to change the name or logo for a custom enterprise app in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 0e4d6eff2a950e61be4551b675beedd299cf523b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540994"
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory-preview"></a><span data-ttu-id="6e75a-103">Change the name or logo of an enterprise app in Azure Active Directory preview</span><span class="sxs-lookup"><span data-stu-id="6e75a-103">Change the name or logo of an enterprise app in Azure Active Directory preview</span></span>
<span data-ttu-id="6e75a-104">It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD) preview.</span><span class="sxs-lookup"><span data-stu-id="6e75a-104">It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD) preview.</span></span> [<span data-ttu-id="6e75a-105">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="6e75a-105">What's in the preview?</span></span>](active-directory-preview-explainer.md) <span data-ttu-id="6e75a-106">You must have the appropriate permissions to make these changes.</span><span class="sxs-lookup"><span data-stu-id="6e75a-106">You must have the appropriate permissions to make these changes.</span></span> <span data-ttu-id="6e75a-107">In the current preview, you must be the creator of the custom app.</span><span class="sxs-lookup"><span data-stu-id="6e75a-107">In the current preview, you must be the creator of the custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="6e75a-108">How do I change an enterprise app's name or logo?</span><span class="sxs-lookup"><span data-stu-id="6e75a-108">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="6e75a-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="6e75a-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="6e75a-110">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="6e75a-110">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="6e75a-111">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6e75a-111">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Opening Enterprise apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="6e75a-113">On the **Enterprise applications** blade, select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6e75a-113">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="6e75a-114">You'll see a list of the apps you can manage.</span><span class="sxs-lookup"><span data-stu-id="6e75a-114">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="6e75a-115">On the **Enterprise applications - All applications** blade, select an app.</span><span class="sxs-lookup"><span data-stu-id="6e75a-115">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="6e75a-116">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="6e75a-116">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Selecting the properties command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="6e75a-118">On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.</span><span class="sxs-lookup"><span data-stu-id="6e75a-118">On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.</span></span>

    ![Changing the app logo or nameproperties command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="6e75a-120">Select the **Save** command.</span><span class="sxs-lookup"><span data-stu-id="6e75a-120">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e75a-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="6e75a-121">Next steps</span></span>
* [<span data-ttu-id="6e75a-122">See all of my groups</span><span class="sxs-lookup"><span data-stu-id="6e75a-122">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="6e75a-123">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="6e75a-123">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="6e75a-124">Remove a user or group assignment from an enterprise app</span><span class="sxs-lookup"><span data-stu-id="6e75a-124">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="6e75a-125">Disable user sign-ins for an enterprise app</span><span class="sxs-lookup"><span data-stu-id="6e75a-125">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)



