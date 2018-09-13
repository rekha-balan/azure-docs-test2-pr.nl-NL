---
title: Expiration policy quickstart for Office 365 groups in Azure Active Directory | Microsoft Docs
description: Expiration for Office 365 groups - Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: quickstart
ms.date: 08/07/2018
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 7008943e9077cbad3c58de43f64b105f35931bf3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870560"
---
# <a name="quickstart-set-office-365-groups-to-expire-in-azure-active-directory"></a><span data-ttu-id="3c303-103">Quickstart: Set Office 365 groups to expire in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3c303-103">Quickstart: Set Office 365 groups to expire in Azure Active Directory</span></span>

<span data-ttu-id="3c303-104">In this quickstart, you set the expiration policy for your Office 365 groups.</span><span class="sxs-lookup"><span data-stu-id="3c303-104">In this quickstart, you set the expiration policy for your Office 365 groups.</span></span> <span data-ttu-id="3c303-105">When users can set up their own groups, unused groups can multiply.</span><span class="sxs-lookup"><span data-stu-id="3c303-105">When users can set up their own groups, unused groups can multiply.</span></span> <span data-ttu-id="3c303-106">One way to manage unused groups is to set those groups to expire, to reduce the maintenance of manually deleting groups.</span><span class="sxs-lookup"><span data-stu-id="3c303-106">One way to manage unused groups is to set those groups to expire, to reduce the maintenance of manually deleting groups.</span></span>

<span data-ttu-id="3c303-107">Expiration policy is simple:</span><span class="sxs-lookup"><span data-stu-id="3c303-107">Expiration policy is simple:</span></span>

* <span data-ttu-id="3c303-108">Group owners are notified to renew an expiring group</span><span class="sxs-lookup"><span data-stu-id="3c303-108">Group owners are notified to renew an expiring group</span></span>
* <span data-ttu-id="3c303-109">A group that is not renewed is deleted</span><span class="sxs-lookup"><span data-stu-id="3c303-109">A group that is not renewed is deleted</span></span>
* <span data-ttu-id="3c303-110">A deleted Office 365 group can be restored within 30 days by a group owner or by an Azure AD administrator</span><span class="sxs-lookup"><span data-stu-id="3c303-110">A deleted Office 365 group can be restored within 30 days by a group owner or by an Azure AD administrator</span></span>

<span data-ttu-id="3c303-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="3c303-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisite"></a><span data-ttu-id="3c303-112">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="3c303-112">Prerequisite</span></span>

<span data-ttu-id="3c303-113">You must be a Global Administrator or User Account Administrator in the tenant to set up group expiration.</span><span class="sxs-lookup"><span data-stu-id="3c303-113">You must be a Global Administrator or User Account Administrator in the tenant to set up group expiration.</span></span>

## <a name="turn-on-user-creation-for-groups"></a><span data-ttu-id="3c303-114">Turn on user creation for groups</span><span class="sxs-lookup"><span data-stu-id="3c303-114">Turn on user creation for groups</span></span>

1. <span data-ttu-id="3c303-115">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a Global Administrator or User Account Administrator for the directory.</span><span class="sxs-lookup"><span data-stu-id="3c303-115">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a Global Administrator or User Account Administrator for the directory.</span></span>

2. <span data-ttu-id="3c303-116">Select **Groups**, and then select **General**.</span><span class="sxs-lookup"><span data-stu-id="3c303-116">Select **Groups**, and then select **General**.</span></span>
  
  ![Self-service group settings](./media/groups-quickstart-expiration/self-service-settings.png)

3. <span data-ttu-id="3c303-118">Set  **Users can create Office 365 groups** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="3c303-118">Set  **Users can create Office 365 groups** to **Yes**.</span></span>

4. <span data-ttu-id="3c303-119">Select **Save** to save the groups settings when you're done.</span><span class="sxs-lookup"><span data-stu-id="3c303-119">Select **Save** to save the groups settings when you're done.</span></span>

## <a name="set-group-expiration"></a><span data-ttu-id="3c303-120">Set group expiration</span><span class="sxs-lookup"><span data-stu-id="3c303-120">Set group expiration</span></span>

1. <span data-ttu-id="3c303-121">Iin to the [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Groups** > **Expiration** to open the expiration settings.</span><span class="sxs-lookup"><span data-stu-id="3c303-121">Iin to the [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Groups** > **Expiration** to open the expiration settings.</span></span>
  
  ![Expiration settings](./media/groups-quickstart-expiration/expiration-settings.png)

2. <span data-ttu-id="3c303-123">Set the expiration interval.</span><span class="sxs-lookup"><span data-stu-id="3c303-123">Set the expiration interval.</span></span> <span data-ttu-id="3c303-124">Select a preset value or enter a custom value over 31 days.</span><span class="sxs-lookup"><span data-stu-id="3c303-124">Select a preset value or enter a custom value over 31 days.</span></span> 

3. <span data-ttu-id="3c303-125">Provide an email address where expiration notifications should be sent when a group has no owner.</span><span class="sxs-lookup"><span data-stu-id="3c303-125">Provide an email address where expiration notifications should be sent when a group has no owner.</span></span>

4. <span data-ttu-id="3c303-126">For this quickstart, set **Enable expiration for these Office 365 groups** to **All**.</span><span class="sxs-lookup"><span data-stu-id="3c303-126">For this quickstart, set **Enable expiration for these Office 365 groups** to **All**.</span></span>

5. <span data-ttu-id="3c303-127">Select **Save** to save the expiration settings when you're done.</span><span class="sxs-lookup"><span data-stu-id="3c303-127">Select **Save** to save the expiration settings when you're done.</span></span>

<span data-ttu-id="3c303-128">That's it!</span><span class="sxs-lookup"><span data-stu-id="3c303-128">That's it!</span></span> <span data-ttu-id="3c303-129">In this quickstart, you successfully set the expiration policy for the selected Office 365 groups.</span><span class="sxs-lookup"><span data-stu-id="3c303-129">In this quickstart, you successfully set the expiration policy for the selected Office 365 groups.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="3c303-130">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="3c303-130">Clean up resources</span></span>

<span data-ttu-id="3c303-131">**To remove the expiration policy**</span><span class="sxs-lookup"><span data-stu-id="3c303-131">**To remove the expiration policy**</span></span>

1. <span data-ttu-id="3c303-132">Ensure that you are signed in to the [Azure portal](https://portal.azure.com) with an account that is the Global Administrator for your tenant.</span><span class="sxs-lookup"><span data-stu-id="3c303-132">Ensure that you are signed in to the [Azure portal](https://portal.azure.com) with an account that is the Global Administrator for your tenant.</span></span>
2. <span data-ttu-id="3c303-133">Select **Azure Active Directory** > **Groups** > **Expiration**.</span><span class="sxs-lookup"><span data-stu-id="3c303-133">Select **Azure Active Directory** > **Groups** > **Expiration**.</span></span>
3. <span data-ttu-id="3c303-134">Set **Enable expiration for these Office 365 groups** to **None**.</span><span class="sxs-lookup"><span data-stu-id="3c303-134">Set **Enable expiration for these Office 365 groups** to **None**.</span></span>

<span data-ttu-id="3c303-135">**To turn off user creation for groups**</span><span class="sxs-lookup"><span data-stu-id="3c303-135">**To turn off user creation for groups**</span></span>

1. <span data-ttu-id="3c303-136">Select **Azure Active Directory** > **Groups** > **General**.</span><span class="sxs-lookup"><span data-stu-id="3c303-136">Select **Azure Active Directory** > **Groups** > **General**.</span></span> 
2. <span data-ttu-id="3c303-137">Set **Users can create Office 365 groups in Azure portals** to **No**.</span><span class="sxs-lookup"><span data-stu-id="3c303-137">Set **Users can create Office 365 groups in Azure portals** to **No**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c303-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c303-138">Next steps</span></span>

<span data-ttu-id="3c303-139">For more information about expiration including technical constraints, adding a list of custom blocked words, and end user experiences across Office 365 apps, see the following article containing those expiration policy details:</span><span class="sxs-lookup"><span data-stu-id="3c303-139">For more information about expiration including technical constraints, adding a list of custom blocked words, and end user experiences across Office 365 apps, see the following article containing those expiration policy details:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3c303-140">Expiration policy all details</span><span class="sxs-lookup"><span data-stu-id="3c303-140">Expiration policy all details</span></span>](groups-lifecycle.md)