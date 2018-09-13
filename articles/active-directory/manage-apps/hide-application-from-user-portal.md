---
title: Hide an application from user's experience in Azure Active Directory | Microsoft Docs
description: How to hide an application from user's experience in Azure Active Directory access panels or Office 365 launchers.
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
ms.date: 01/04/2018
ms.author: barbkess
ms.reviewer: asteen
ms.custom: it-pro
ms.openlocfilehash: 55f80396df4cbfe7d0a16a6a5066b68aadc0bdd3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867597"
---
# <a name="hide-an-application-from-users-experience-in-azure-active-directory"></a><span data-ttu-id="699c0-103">Hide an application from user's experience in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="699c0-103">Hide an application from user's experience in Azure Active Directory</span></span>

<span data-ttu-id="699c0-104">If you have an application that you do not want to show on users’ access panels or Office 365 launchers, there are options to hide this app tile.</span><span class="sxs-lookup"><span data-stu-id="699c0-104">If you have an application that you do not want to show on users’ access panels or Office 365 launchers, there are options to hide this app tile.</span></span>  <span data-ttu-id="699c0-105">The following two options are available for hiding applications from user's app launchers.</span><span class="sxs-lookup"><span data-stu-id="699c0-105">The following two options are available for hiding applications from user's app launchers.</span></span>

- <span data-ttu-id="699c0-106">Hide a third-party application from users access panels and Office 365 app launchers</span><span class="sxs-lookup"><span data-stu-id="699c0-106">Hide a third-party application from users access panels and Office 365 app launchers</span></span>
- <span data-ttu-id="699c0-107">Hide all Office 365 applications from users access panels</span><span class="sxs-lookup"><span data-stu-id="699c0-107">Hide all Office 365 applications from users access panels</span></span>

<span data-ttu-id="699c0-108">By hiding the app users still have permissions to the app but will not see them appear on their app launchers.</span><span class="sxs-lookup"><span data-stu-id="699c0-108">By hiding the app users still have permissions to the app but will not see them appear on their app launchers.</span></span> <span data-ttu-id="699c0-109">You must have the appropriate permissions to manage the enterprise app, and you must be a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="699c0-109">You must have the appropriate permissions to manage the enterprise app, and you must be a global admin for the directory.</span></span>


## <a name="hiding-an-application-from-users-end-user-experiences"></a><span data-ttu-id="699c0-110">Hiding an application from user's end user experiences</span><span class="sxs-lookup"><span data-stu-id="699c0-110">Hiding an application from user's end user experiences</span></span>
<span data-ttu-id="699c0-111">You can use the steps below, depending on your situation, to hide applications from the access panel.</span><span class="sxs-lookup"><span data-stu-id="699c0-111">You can use the steps below, depending on your situation, to hide applications from the access panel.</span></span>

### <a name="how-do-i-hide-a-third-party-app-from-users-access-panel-and-o365-app-launchers"></a><span data-ttu-id="699c0-112">How do I hide a third-party app from user’s access panel and O365 app launchers?</span><span class="sxs-lookup"><span data-stu-id="699c0-112">How do I hide a third-party app from user’s access panel and O365 app launchers?</span></span>
<span data-ttu-id="699c0-113">Use the following steps to hide an application from a user's access panel and Office 365 app launchers.</span><span class="sxs-lookup"><span data-stu-id="699c0-113">Use the following steps to hide an application from a user's access panel and Office 365 app launchers.</span></span>

1.  <span data-ttu-id="699c0-114">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="699c0-114">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2.  <span data-ttu-id="699c0-115">Select **All services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="699c0-115">Select **All services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3.  <span data-ttu-id="699c0-116">On the **Azure Active Directory - *directoryname*** screen (that is, the Azure AD screen for the directory you are managing), select **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="699c0-116">On the **Azure Active Directory - *directoryname*** screen (that is, the Azure AD screen for the directory you are managing), select **Enterprise applications**.</span></span>
<span data-ttu-id="699c0-117">![Enterprise apps](./media/hide-application-from-user-portal/app1.png)</span><span class="sxs-lookup"><span data-stu-id="699c0-117">![Enterprise apps](./media/hide-application-from-user-portal/app1.png)</span></span>
4.  <span data-ttu-id="699c0-118">On the **Enterprise applications** screen, select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="699c0-118">On the **Enterprise applications** screen, select **All applications**.</span></span> <span data-ttu-id="699c0-119">You see a list of the apps you can manage.</span><span class="sxs-lookup"><span data-stu-id="699c0-119">You see a list of the apps you can manage.</span></span>
5.  <span data-ttu-id="699c0-120">On the **Enterprise applications - All applications** screen, select an app.</span><span class="sxs-lookup"><span data-stu-id="699c0-120">On the **Enterprise applications - All applications** screen, select an app.</span></span></br>
<span data-ttu-id="699c0-121">![Enterprise apps](./media/hide-application-from-user-portal/app2.png)</span><span class="sxs-lookup"><span data-stu-id="699c0-121">![Enterprise apps](./media/hide-application-from-user-portal/app2.png)</span></span>
6.  <span data-ttu-id="699c0-122">On the ***appname*** screen (that is, the screen with the name of the selected app in the title), select Properties.</span><span class="sxs-lookup"><span data-stu-id="699c0-122">On the ***appname*** screen (that is, the screen with the name of the selected app in the title), select Properties.</span></span>
7.  <span data-ttu-id="699c0-123">On the ***appname* - Properties** screen, select **Yes** for **Visible to users?**.</span><span class="sxs-lookup"><span data-stu-id="699c0-123">On the ***appname* - Properties** screen, select **Yes** for **Visible to users?**.</span></span>
<span data-ttu-id="699c0-124">![Enterprise apps](./media/hide-application-from-user-portal/app3.png)</span><span class="sxs-lookup"><span data-stu-id="699c0-124">![Enterprise apps](./media/hide-application-from-user-portal/app3.png)</span></span>
8.  <span data-ttu-id="699c0-125">Select the **Save** command.</span><span class="sxs-lookup"><span data-stu-id="699c0-125">Select the **Save** command.</span></span>

### <a name="how-do-i-hide-office-365-applications-from-users-access-panel"></a><span data-ttu-id="699c0-126">How do I hide Office 365 applications from user's access panel?</span><span class="sxs-lookup"><span data-stu-id="699c0-126">How do I hide Office 365 applications from user's access panel?</span></span>

<span data-ttu-id="699c0-127">Use the following steps to hide all Office 365 applications from the access panel.</span><span class="sxs-lookup"><span data-stu-id="699c0-127">Use the following steps to hide all Office 365 applications from the access panel.</span></span> <span data-ttu-id="699c0-128">These apps will still be visible in the Office 365 portal.</span><span class="sxs-lookup"><span data-stu-id="699c0-128">These apps will still be visible in the Office 365 portal.</span></span>

1.  <span data-ttu-id="699c0-129">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="699c0-129">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2.  <span data-ttu-id="699c0-130">Select **All services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="699c0-130">Select **All services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3.  <span data-ttu-id="699c0-131">On the **Azure Active Directory - *directoryname*** screen (that is, the Azure AD screen for the directory you are managing), select **User settings**.</span><span class="sxs-lookup"><span data-stu-id="699c0-131">On the **Azure Active Directory - *directoryname*** screen (that is, the Azure AD screen for the directory you are managing), select **User settings**.</span></span>
4.  <span data-ttu-id="699c0-132">On the **User settings** screen, under **Enterprise applications** select **Yes** for **Users can only see Office 365 apps in the Office 365 portal**.</span><span class="sxs-lookup"><span data-stu-id="699c0-132">On the **User settings** screen, under **Enterprise applications** select **Yes** for **Users can only see Office 365 apps in the Office 365 portal**.</span></span>

![Enterprise apps](./media/hide-application-from-user-portal/apps4.png)

## <a name="next-steps"></a><span data-ttu-id="699c0-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="699c0-134">Next steps</span></span>
* [<span data-ttu-id="699c0-135">See all my groups</span><span class="sxs-lookup"><span data-stu-id="699c0-135">See all my groups</span></span>](../fundamentals/active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="699c0-136">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="699c0-136">Assign a user or group to an enterprise app</span></span>](assign-user-or-group-access-portal.md)
* [<span data-ttu-id="699c0-137">Remove a user or group assignment from an enterprise app</span><span class="sxs-lookup"><span data-stu-id="699c0-137">Remove a user or group assignment from an enterprise app</span></span>](remove-user-or-group-access-portal.md)
* [<span data-ttu-id="699c0-138">Change the name or logo of an enterprise app</span><span class="sxs-lookup"><span data-stu-id="699c0-138">Change the name or logo of an enterprise app</span></span>](change-name-or-logo-portal.md)

