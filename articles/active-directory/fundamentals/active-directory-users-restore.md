---
title: Restore or permanently remove a recently deleted user in Azure Active Directory | Microsoft Docs
description: How to restore a deleted user, view restorable users, or permanently delete a user in Azure Active Directory
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: quickstart
ms.date: 05/09/2018
ms.author: lizross
ms.reviewer: jeffsta
ms.custom: it-pro
ms.openlocfilehash: 6cd772638ed10e9cac52352e4b602d41a784bba0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866709"
---
# <a name="restore-a-deleted-user-in-azure-active-directory"></a><span data-ttu-id="0bf72-103">Restore a deleted user in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bf72-103">Restore a deleted user in Azure Active Directory</span></span>

<span data-ttu-id="0bf72-104">This article contains instructions to restore or permanently delete a previously deleted user.</span><span class="sxs-lookup"><span data-stu-id="0bf72-104">This article contains instructions to restore or permanently delete a previously deleted user.</span></span> <span data-ttu-id="0bf72-105">When you delete a user in the Azure Active Directory (Azure AD), the deleted user is retained for 30 days from the deletion date.</span><span class="sxs-lookup"><span data-stu-id="0bf72-105">When you delete a user in the Azure Active Directory (Azure AD), the deleted user is retained for 30 days from the deletion date.</span></span> <span data-ttu-id="0bf72-106">During that time, the user and its properties can be restored.</span><span class="sxs-lookup"><span data-stu-id="0bf72-106">During that time, the user and its properties can be restored.</span></span> 

> [!WARNING]
> <span data-ttu-id="0bf72-107">After it is permanently deleted, the user cannot be restored.</span><span class="sxs-lookup"><span data-stu-id="0bf72-107">After it is permanently deleted, the user cannot be restored.</span></span>

## <a name="how-to-restore-a-recently-deleted-user"></a><span data-ttu-id="0bf72-108">How to restore a recently deleted user</span><span class="sxs-lookup"><span data-stu-id="0bf72-108">How to restore a recently deleted user</span></span>
<span data-ttu-id="0bf72-109">When a user is recently deleted, all directory information is preserved.</span><span class="sxs-lookup"><span data-stu-id="0bf72-109">When a user is recently deleted, all directory information is preserved.</span></span> <span data-ttu-id="0bf72-110">If the user is restored, that information is restored as well.</span><span class="sxs-lookup"><span data-stu-id="0bf72-110">If the user is restored, that information is restored as well.</span></span>

1. <span data-ttu-id="0bf72-111">In the [Azure AD admin center](https://aad.portal.azure.com), select **Users** &gt; **Deleted users**.</span><span class="sxs-lookup"><span data-stu-id="0bf72-111">In the [Azure AD admin center](https://aad.portal.azure.com), select **Users** &gt; **Deleted users**.</span></span> 
2. <span data-ttu-id="0bf72-112">Select one or more recently deleted users.</span><span class="sxs-lookup"><span data-stu-id="0bf72-112">Select one or more recently deleted users.</span></span>
3. <span data-ttu-id="0bf72-113">Select **Restore user**.</span><span class="sxs-lookup"><span data-stu-id="0bf72-113">Select **Restore user**.</span></span>

## <a name="how-to-permanently-delete-a-recently-deleted-user"></a><span data-ttu-id="0bf72-114">How to permanently delete a recently deleted user</span><span class="sxs-lookup"><span data-stu-id="0bf72-114">How to permanently delete a recently deleted user</span></span>

1. <span data-ttu-id="0bf72-115">In the [Azure AD admin center](https://aad.portal.azure.com), select **Users** &gt; **Deleted users**.</span><span class="sxs-lookup"><span data-stu-id="0bf72-115">In the [Azure AD admin center](https://aad.portal.azure.com), select **Users** &gt; **Deleted users**.</span></span> 
2. <span data-ttu-id="0bf72-116">Select one or more recently deleted users.</span><span class="sxs-lookup"><span data-stu-id="0bf72-116">Select one or more recently deleted users.</span></span>
3. <span data-ttu-id="0bf72-117">Select **Delete permanently**.</span><span class="sxs-lookup"><span data-stu-id="0bf72-117">Select **Delete permanently**.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="0bf72-118">Required permissions</span><span class="sxs-lookup"><span data-stu-id="0bf72-118">Required permissions</span></span>
<span data-ttu-id="0bf72-119">The following permissions are sufficient to restore a user.</span><span class="sxs-lookup"><span data-stu-id="0bf72-119">The following permissions are sufficient to restore a user.</span></span>

<span data-ttu-id="0bf72-120">Role</span><span class="sxs-lookup"><span data-stu-id="0bf72-120">Role</span></span> | <span data-ttu-id="0bf72-121">Permissions</span><span class="sxs-lookup"><span data-stu-id="0bf72-121">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="0bf72-122">Company Administrator</span><span class="sxs-lookup"><span data-stu-id="0bf72-122">Company Administrator</span></span><p><span data-ttu-id="0bf72-123">Partner Tier1 Support</span><span class="sxs-lookup"><span data-stu-id="0bf72-123">Partner Tier1 Support</span></span><p><span data-ttu-id="0bf72-124">Partner Tier2 Support</span><span class="sxs-lookup"><span data-stu-id="0bf72-124">Partner Tier2 Support</span></span><p><span data-ttu-id="0bf72-125">User Account Administrator</span><span class="sxs-lookup"><span data-stu-id="0bf72-125">User Account Administrator</span></span> | <span data-ttu-id="0bf72-126">Can restore deleted users</span><span class="sxs-lookup"><span data-stu-id="0bf72-126">Can restore deleted users</span></span> 
<span data-ttu-id="0bf72-127">Company Administrator</span><span class="sxs-lookup"><span data-stu-id="0bf72-127">Company Administrator</span></span><p><span data-ttu-id="0bf72-128">Partner Tier1 Support</span><span class="sxs-lookup"><span data-stu-id="0bf72-128">Partner Tier1 Support</span></span><p><span data-ttu-id="0bf72-129">Partner Tier2 Support</span><span class="sxs-lookup"><span data-stu-id="0bf72-129">Partner Tier2 Support</span></span><p><span data-ttu-id="0bf72-130">User Account Administrator</span><span class="sxs-lookup"><span data-stu-id="0bf72-130">User Account Administrator</span></span> | <span data-ttu-id="0bf72-131">Can permanently delete users</span><span class="sxs-lookup"><span data-stu-id="0bf72-131">Can permanently delete users</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bf72-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="0bf72-132">Next steps</span></span>
<span data-ttu-id="0bf72-133">These articles provide additional information on Azure Active Directory user management.</span><span class="sxs-lookup"><span data-stu-id="0bf72-133">These articles provide additional information on Azure Active Directory user management.</span></span>

* [<span data-ttu-id="0bf72-134">Quickstart: Add or delete users to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bf72-134">Quickstart: Add or delete users to Azure Active Directory</span></span>](add-users-azure-active-directory.md)
* [<span data-ttu-id="0bf72-135">Manage user profiles</span><span class="sxs-lookup"><span data-stu-id="0bf72-135">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="0bf72-136">Add guest users from another directory</span><span class="sxs-lookup"><span data-stu-id="0bf72-136">Add guest users from another directory</span></span>](../b2b/what-is-b2b.md) 
* [<span data-ttu-id="0bf72-137">Assign a user to a role in your Azure AD</span><span class="sxs-lookup"><span data-stu-id="0bf72-137">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
