---
title: How to add an existing Azure subscription to your Azure AD directory | Microsoft Docs
description: How to add an existing subscription to your Azure AD directory
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: conceptual
ms.date: 12/12/2017
ms.author: lizross
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 6b0933e9aa732cb9a01a454764fb0425465ec078
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864481"
---
# <a name="how-to-associate-or-add-an-azure-subscription-to-azure-active-directory"></a><span data-ttu-id="c8ddd-103">How to associate or add an Azure subscription to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8ddd-103">How to associate or add an Azure subscription to Azure Active Directory</span></span>

<span data-ttu-id="c8ddd-104">This article covers information about the relationship between an Azure subscription and Azure Active Directory (Azure AD), and how to add an existing subscription to your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-104">This article covers information about the relationship between an Azure subscription and Azure Active Directory (Azure AD), and how to add an existing subscription to your Azure AD directory.</span></span> <span data-ttu-id="c8ddd-105">Your Azure subscription has a trust relationship with Azure AD, which means that it trusts the directory to authenticate users, services, and devices.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-105">Your Azure subscription has a trust relationship with Azure AD, which means that it trusts the directory to authenticate users, services, and devices.</span></span> <span data-ttu-id="c8ddd-106">Multiple subscriptions can trust the same directory, but each subscription trusts only one directory.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-106">Multiple subscriptions can trust the same directory, but each subscription trusts only one directory.</span></span> 

<span data-ttu-id="c8ddd-107">The trust relationship that a subscription has with a directory is unlike the relationship that it has with other resources in Azure (websites, databases, and so on).</span><span class="sxs-lookup"><span data-stu-id="c8ddd-107">The trust relationship that a subscription has with a directory is unlike the relationship that it has with other resources in Azure (websites, databases, and so on).</span></span> <span data-ttu-id="c8ddd-108">If a subscription expires, access to the other resources associated with the subscription also stops.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-108">If a subscription expires, access to the other resources associated with the subscription also stops.</span></span> <span data-ttu-id="c8ddd-109">But an Azure AD directory remains in Azure, and you can associate a different subscription with that directory and manage the directory using the new subscription.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-109">But an Azure AD directory remains in Azure, and you can associate a different subscription with that directory and manage the directory using the new subscription.</span></span>

<span data-ttu-id="c8ddd-110">All users have a single home directory that authenticates them, but they can also be guests in other directories.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-110">All users have a single home directory that authenticates them, but they can also be guests in other directories.</span></span> <span data-ttu-id="c8ddd-111">In Azure AD, you can see the directories of which your user account is a member or guest.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-111">In Azure AD, you can see the directories of which your user account is a member or guest.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c8ddd-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="c8ddd-112">Before you begin</span></span>

* <span data-ttu-id="c8ddd-113">You must sign in with account that has RBAC Owner access to the subscription.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-113">You must sign in with account that has RBAC Owner access to the subscription.</span></span>
* <span data-ttu-id="c8ddd-114">You must sign in with an account that exists in both the current directory with which the subscription is associated and in the directory you want to add it to.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-114">You must sign in with an account that exists in both the current directory with which the subscription is associated and in the directory you want to add it to.</span></span> <span data-ttu-id="c8ddd-115">To learn more about getting access to another directory, see [How do Azure Active Directory admins add B2B collaboration users?](../b2b/add-users-administrator.md)</span><span class="sxs-lookup"><span data-stu-id="c8ddd-115">To learn more about getting access to another directory, see [How do Azure Active Directory admins add B2B collaboration users?](../b2b/add-users-administrator.md)</span></span>
* <span data-ttu-id="c8ddd-116">This feature isn't available for CSP (MS-AZR-0145P, MS-AZR-0146P, MS-AZR-159P) and Microsoft Imagine (MS-AZR-0144P) subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-116">This feature isn't available for CSP (MS-AZR-0145P, MS-AZR-0146P, MS-AZR-159P) and Microsoft Imagine (MS-AZR-0144P) subscriptions.</span></span>

## <a name="to-associate-an-existing-subscription-to-your-azure-ad-directory"></a><span data-ttu-id="c8ddd-117">To associate an existing subscription to your Azure AD directory</span><span class="sxs-lookup"><span data-stu-id="c8ddd-117">To associate an existing subscription to your Azure AD directory</span></span>

1. <span data-ttu-id="c8ddd-118">Sign in and select a subscription from the [Subscriptions page in Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span><span class="sxs-lookup"><span data-stu-id="c8ddd-118">Sign in and select a subscription from the [Subscriptions page in Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>
2. <span data-ttu-id="c8ddd-119">Click **Change directory**.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-119">Click **Change directory**.</span></span>

    ![Screenshot showing the Change directory button](./media/active-directory-how-subscriptions-associated-directory/edit-directory-button.PNG)
3. <span data-ttu-id="c8ddd-121">Review the warnings.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-121">Review the warnings.</span></span> <span data-ttu-id="c8ddd-122">All [Role-Based Access Control (RBAC)](../../role-based-access-control/role-assignments-portal.md) users with assigned access and all subscription admins lose access when the subscription directory changes.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-122">All [Role-Based Access Control (RBAC)](../../role-based-access-control/role-assignments-portal.md) users with assigned access and all subscription admins lose access when the subscription directory changes.</span></span>
4. <span data-ttu-id="c8ddd-123">Select a directory.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-123">Select a directory.</span></span>

    ![Screenshot showing the change directory UI](./media/active-directory-how-subscriptions-associated-directory/edit-directory-ui.PNG)
5. <span data-ttu-id="c8ddd-125">Click **Change**.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-125">Click **Change**.</span></span>
6. <span data-ttu-id="c8ddd-126">Success!</span><span class="sxs-lookup"><span data-stu-id="c8ddd-126">Success!</span></span> <span data-ttu-id="c8ddd-127">Use the directory switcher to go to the new directory.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-127">Use the directory switcher to go to the new directory.</span></span> <span data-ttu-id="c8ddd-128">It might take up to 10 minutes for everything to show up properly.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-128">It might take up to 10 minutes for everything to show up properly.</span></span>

    ![Screenshot showing the change directory success notification](./media/active-directory-how-subscriptions-associated-directory/edit-directory-success.PNG)

    ![Screenshot showing the switcher](./media/active-directory-how-subscriptions-associated-directory/directory-switcher.PNG)


<span data-ttu-id="c8ddd-131">Any Azure key vaults that you have are also affected by a subscription move, so [change the key vault tenant ID](../../key-vault/key-vault-subscription-move-fix.md) before resuming operations.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-131">Any Azure key vaults that you have are also affected by a subscription move, so [change the key vault tenant ID](../../key-vault/key-vault-subscription-move-fix.md) before resuming operations.</span></span>

<span data-ttu-id="c8ddd-132">Changing the subscription directory is a service-level operation.</span><span class="sxs-lookup"><span data-stu-id="c8ddd-132">Changing the subscription directory is a service-level operation.</span></span> <span data-ttu-id="c8ddd-133">It doesn't affect subscription billing ownership, and the Account Admin can still change Service Admin using the [Account Center](https://account.azure.com/subscriptions).</span><span class="sxs-lookup"><span data-stu-id="c8ddd-133">It doesn't affect subscription billing ownership, and the Account Admin can still change Service Admin using the [Account Center](https://account.azure.com/subscriptions).</span></span> <span data-ttu-id="c8ddd-134">If you want to delete the original directory, you must transfer the subscription billing ownership to a new Account Admin. To learn more about transferring billing ownership, see [Transfer ownership of an Azure subscription to another account](../../billing/billing-subscription-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="c8ddd-134">If you want to delete the original directory, you must transfer the subscription billing ownership to a new Account Admin. To learn more about transferring billing ownership, see [Transfer ownership of an Azure subscription to another account](../../billing/billing-subscription-transfer.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c8ddd-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8ddd-135">Next steps</span></span>

* <span data-ttu-id="c8ddd-136">To learn more about creating a new Azure AD directory for free, see [How to get an Azure Active Directory tenant](../develop/quickstart-create-new-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="c8ddd-136">To learn more about creating a new Azure AD directory for free, see [How to get an Azure Active Directory tenant](../develop/quickstart-create-new-tenant.md)</span></span>
* <span data-ttu-id="c8ddd-137">To learn more about transferring billing ownership of an Azure subscription, see [Transfer ownership of an Azure subscription to another account](../../billing/billing-subscription-transfer.md)</span><span class="sxs-lookup"><span data-stu-id="c8ddd-137">To learn more about transferring billing ownership of an Azure subscription, see [Transfer ownership of an Azure subscription to another account](../../billing/billing-subscription-transfer.md)</span></span>
* <span data-ttu-id="c8ddd-138">To learn more about how resource access is controlled in Microsoft Azure, see [Understanding resource access in Azure](../../role-based-access-control/rbac-and-directory-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="c8ddd-138">To learn more about how resource access is controlled in Microsoft Azure, see [Understanding resource access in Azure](../../role-based-access-control/rbac-and-directory-admin-roles.md)</span></span>
* <span data-ttu-id="c8ddd-139">For more information on how to assign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="c8ddd-139">For more information on how to assign roles in Azure AD, see [Assigning administrator roles in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md)</span></span>

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
