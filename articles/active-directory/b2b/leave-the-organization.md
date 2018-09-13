---
title: Leave an organization as a guest user - Azure Active Directory | Microsoft Docs
description: Shows how an Azure AD B2B guest user can leave an organization by using the Access Panel.
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 05/11/2018
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 17b34b173a10a355817fee0f5928b7fb478125e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856216"
---
# <a name="leave-an-organization-as-a-guest-user"></a><span data-ttu-id="a917b-103">Leave an organization as a guest user</span><span class="sxs-lookup"><span data-stu-id="a917b-103">Leave an organization as a guest user</span></span>

<span data-ttu-id="a917b-104">An Azure Active Directory (Azure AD) B2B guest user can decide to leave an organization at any time if they no longer need to use apps from that organization or maintain any association.</span><span class="sxs-lookup"><span data-stu-id="a917b-104">An Azure Active Directory (Azure AD) B2B guest user can decide to leave an organization at any time if they no longer need to use apps from that organization or maintain any association.</span></span> <span data-ttu-id="a917b-105">A user can leave an organization on their own, without having to contact an administrator.</span><span class="sxs-lookup"><span data-stu-id="a917b-105">A user can leave an organization on their own, without having to contact an administrator.</span></span>

## <a name="leave-an-organization"></a><span data-ttu-id="a917b-106">Leave an organization</span><span class="sxs-lookup"><span data-stu-id="a917b-106">Leave an organization</span></span>

<span data-ttu-id="a917b-107">To leave an organization, as a user signed in to the [Access Panel](https://myapps.microsoft.com), do the following:</span><span class="sxs-lookup"><span data-stu-id="a917b-107">To leave an organization, as a user signed in to the [Access Panel](https://myapps.microsoft.com), do the following:</span></span>

1. <span data-ttu-id="a917b-108">If you’re not already signed in to the organization that you want to leave, select your name in the upper-right corner, and click the organization you want to leave.</span><span class="sxs-lookup"><span data-stu-id="a917b-108">If you’re not already signed in to the organization that you want to leave, select your name in the upper-right corner, and click the organization you want to leave.</span></span>
2. <span data-ttu-id="a917b-109">In the upper-right corner, select your name.</span><span class="sxs-lookup"><span data-stu-id="a917b-109">In the upper-right corner, select your name.</span></span>
3. <span data-ttu-id="a917b-110">Next to **Organizations**, select the settings icon (gear).</span><span class="sxs-lookup"><span data-stu-id="a917b-110">Next to **Organizations**, select the settings icon (gear).</span></span>
 
   ![Screenshot showing user settings in Access Panel](media/leave-the-organization/UserSettings.png) 

3. <span data-ttu-id="a917b-112">Under **Organizations**, find the organization that you want to leave, and select **Leave organization**.</span><span class="sxs-lookup"><span data-stu-id="a917b-112">Under **Organizations**, find the organization that you want to leave, and select **Leave organization**.</span></span>

   ![Screenshot showing Leave organization option in the user interface](media/leave-the-organization/LeaveOrg.png)

4. <span data-ttu-id="a917b-114">When asked to confirm, select **Leave**.</span><span class="sxs-lookup"><span data-stu-id="a917b-114">When asked to confirm, select **Leave**.</span></span> 

## <a name="account-removal"></a><span data-ttu-id="a917b-115">Account removal</span><span class="sxs-lookup"><span data-stu-id="a917b-115">Account removal</span></span>

<span data-ttu-id="a917b-116">When a user leaves an organization, the user account is "soft deleted" in the directory.</span><span class="sxs-lookup"><span data-stu-id="a917b-116">When a user leaves an organization, the user account is "soft deleted" in the directory.</span></span> <span data-ttu-id="a917b-117">By default, the user object moves to the **Deleted users** area in Azure AD but is not permanently deleted for 30 days.</span><span class="sxs-lookup"><span data-stu-id="a917b-117">By default, the user object moves to the **Deleted users** area in Azure AD but is not permanently deleted for 30 days.</span></span> <span data-ttu-id="a917b-118">This soft deletion enables the administrator to restore the user account (including groups and permissions), if the user makes a request to restore the account within the 30-day period.</span><span class="sxs-lookup"><span data-stu-id="a917b-118">This soft deletion enables the administrator to restore the user account (including groups and permissions), if the user makes a request to restore the account within the 30-day period.</span></span>

<span data-ttu-id="a917b-119">If desired, a tenant administrator can permanently delete the account at any time during the 30-day period.</span><span class="sxs-lookup"><span data-stu-id="a917b-119">If desired, a tenant administrator can permanently delete the account at any time during the 30-day period.</span></span> <span data-ttu-id="a917b-120">To do this:</span><span class="sxs-lookup"><span data-stu-id="a917b-120">To do this:</span></span>

1. <span data-ttu-id="a917b-121">In the [Azure portal](https://portal.azure.com), select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a917b-121">In the [Azure portal](https://portal.azure.com), select **Azure Active Directory**.</span></span>
2. <span data-ttu-id="a917b-122">Under **Manage**, select **Users**.</span><span class="sxs-lookup"><span data-stu-id="a917b-122">Under **Manage**, select **Users**.</span></span>
3. <span data-ttu-id="a917b-123">Select **Deleted users**.</span><span class="sxs-lookup"><span data-stu-id="a917b-123">Select **Deleted users**.</span></span>
4. <span data-ttu-id="a917b-124">Select the check box next to a deleted user, and then select **Delete permanently**.</span><span class="sxs-lookup"><span data-stu-id="a917b-124">Select the check box next to a deleted user, and then select **Delete permanently**.</span></span>

<span data-ttu-id="a917b-125">If you permanently delete a user, this action is irrevocable.</span><span class="sxs-lookup"><span data-stu-id="a917b-125">If you permanently delete a user, this action is irrevocable.</span></span>

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-dsr-and-stp-note.md)]

## <a name="next-steps"></a><span data-ttu-id="a917b-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="a917b-126">Next steps</span></span>

- <span data-ttu-id="a917b-127">For an overview of Azure AD B2B, see [What is Azure AD B2B collaboration?](what-is-b2b.md)</span><span class="sxs-lookup"><span data-stu-id="a917b-127">For an overview of Azure AD B2B, see [What is Azure AD B2B collaboration?](what-is-b2b.md)</span></span>



