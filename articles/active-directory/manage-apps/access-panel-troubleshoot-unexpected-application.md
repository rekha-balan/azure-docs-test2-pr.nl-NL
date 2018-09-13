---
title: How applications appear on the access panel | Microsoft Docs
description: Troubleshoot why an application is appearing in the Access Panel
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: barbkess
ms.reviewr: japere
ms.openlocfilehash: 85e0eccf8ed30f5fc91bd892463fe6f1bd835d75
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866984"
---
# <a name="how-applications-appear-on-the-access-panel"></a><span data-ttu-id="bfcec-103">How applications appear on the access panel</span><span class="sxs-lookup"><span data-stu-id="bfcec-103">How applications appear on the access panel</span></span>

<span data-ttu-id="bfcec-104">The Access Panel is a web-based portal, which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span><span class="sxs-lookup"><span data-stu-id="bfcec-104">The Access Panel is a web-based portal, which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="bfcec-105">These applications are configured on behalf of the user in the Azure AD portal.</span><span class="sxs-lookup"><span data-stu-id="bfcec-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="bfcec-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bfcec-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="bfcec-107">General issues to check first</span><span class="sxs-lookup"><span data-stu-id="bfcec-107">General issues to check first</span></span>

-   <span data-ttu-id="bfcec-108">If an application was removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span><span class="sxs-lookup"><span data-stu-id="bfcec-108">If an application was removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span></span>

-   <span data-ttu-id="bfcec-109">If a license was removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span><span class="sxs-lookup"><span data-stu-id="bfcec-109">If a license was removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="bfcec-110">Allow for extra time before signing into the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bfcec-110">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="bfcec-111">Problems related to assigning applications to users</span><span class="sxs-lookup"><span data-stu-id="bfcec-111">Problems related to assigning applications to users</span></span>

<span data-ttu-id="bfcec-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span><span class="sxs-lookup"><span data-stu-id="bfcec-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span></span> <span data-ttu-id="bfcec-113">Following are some ways to check:</span><span class="sxs-lookup"><span data-stu-id="bfcec-113">Following are some ways to check:</span></span>

-   [<span data-ttu-id="bfcec-114">Check if a user is assigned to the application</span><span class="sxs-lookup"><span data-stu-id="bfcec-114">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="bfcec-115">Check if a user is under a license related to the application</span><span class="sxs-lookup"><span data-stu-id="bfcec-115">Check if a user is under a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="bfcec-116">Check if a user is assigned to the application</span><span class="sxs-lookup"><span data-stu-id="bfcec-116">Check if a user is assigned to the application</span></span>

<span data-ttu-id="bfcec-117">To check if a user is assigned to the application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="bfcec-117">To check if a user is assigned to the application, follow these steps:</span></span>

1.  <span data-ttu-id="bfcec-118">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="bfcec-118">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfcec-119">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="bfcec-119">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="bfcec-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="bfcec-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfcec-121">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="bfcec-121">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="bfcec-122">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="bfcec-122">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="bfcec-123">**Search** for the name of the application in question.</span><span class="sxs-lookup"><span data-stu-id="bfcec-123">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="bfcec-124">click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="bfcec-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="bfcec-125">Check to see if your user is assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="bfcec-125">Check to see if your user is assigned to the application.</span></span>

  * <span data-ttu-id="bfcec-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span><span class="sxs-lookup"><span data-stu-id="bfcec-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="bfcec-127">Check if a user is under a license related to the application</span><span class="sxs-lookup"><span data-stu-id="bfcec-127">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="bfcec-128">To check a user’s assigned licenses, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="bfcec-128">To check a user’s assigned licenses, follow these steps:</span></span>

1.  <span data-ttu-id="bfcec-129">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="bfcec-129">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfcec-130">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="bfcec-130">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="bfcec-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="bfcec-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfcec-132">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="bfcec-132">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="bfcec-133">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="bfcec-133">click **All users**.</span></span>

6.  <span data-ttu-id="bfcec-134">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="bfcec-134">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="bfcec-135">click **Licenses** to see which licenses the user currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="bfcec-135">click **Licenses** to see which licenses the user currently has assigned.</span></span>

   * <span data-ttu-id="bfcec-136">If the user is assigned to an Office license, this enables First Party Office applications to appear on the user’s Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bfcec-136">If the user is assigned to an Office license, this enables First Party Office applications to appear on the user’s Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="bfcec-137">Problems related to assigning applications to groups</span><span class="sxs-lookup"><span data-stu-id="bfcec-137">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="bfcec-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span><span class="sxs-lookup"><span data-stu-id="bfcec-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="bfcec-139">Following are some ways to check:</span><span class="sxs-lookup"><span data-stu-id="bfcec-139">Following are some ways to check:</span></span>

-   [<span data-ttu-id="bfcec-140">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="bfcec-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="bfcec-141">Check if a user is a member of a group assigned to a license</span><span class="sxs-lookup"><span data-stu-id="bfcec-141">Check if a user is a member of a group assigned to a license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="bfcec-142">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="bfcec-142">Check a user’s group memberships</span></span>

<span data-ttu-id="bfcec-143">To check a group’s membership, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="bfcec-143">To check a group’s membership, follow these steps:</span></span>

1.  <span data-ttu-id="bfcec-144">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="bfcec-144">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfcec-145">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="bfcec-145">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="bfcec-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="bfcec-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfcec-147">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="bfcec-147">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="bfcec-148">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="bfcec-148">click **All users**.</span></span>

6.  <span data-ttu-id="bfcec-149">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="bfcec-149">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="bfcec-150">click **Groups.**</span><span class="sxs-lookup"><span data-stu-id="bfcec-150">click **Groups.**</span></span>

8.  <span data-ttu-id="bfcec-151">Check to see if your user is part of a Group assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="bfcec-151">Check to see if your user is part of a Group assigned to the application.</span></span>

   * <span data-ttu-id="bfcec-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span><span class="sxs-lookup"><span data-stu-id="bfcec-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-to-a-license"></a><span data-ttu-id="bfcec-153">Check if a user is a member of a group assigned to a license</span><span class="sxs-lookup"><span data-stu-id="bfcec-153">Check if a user is a member of a group assigned to a license</span></span>

1.  <span data-ttu-id="bfcec-154">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="bfcec-154">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bfcec-155">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="bfcec-155">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="bfcec-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="bfcec-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bfcec-157">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="bfcec-157">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="bfcec-158">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="bfcec-158">click **All users**.</span></span>

6.  <span data-ttu-id="bfcec-159">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="bfcec-159">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="bfcec-160">click **Groups.**</span><span class="sxs-lookup"><span data-stu-id="bfcec-160">click **Groups.**</span></span>

8.  <span data-ttu-id="bfcec-161">click the row of a specific group.</span><span class="sxs-lookup"><span data-stu-id="bfcec-161">click the row of a specific group.</span></span>

9.  <span data-ttu-id="bfcec-162">click **Licenses** to see which licenses the group has assigned to it.</span><span class="sxs-lookup"><span data-stu-id="bfcec-162">click **Licenses** to see which licenses the group has assigned to it.</span></span>

  * <span data-ttu-id="bfcec-163">If the group is assigned to an Office license, this may enable certain First Party Office applications to appear on the user’s Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bfcec-163">If the group is assigned to an Office license, this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="bfcec-164">If these troubleshooting steps do not the resolve the issue</span><span class="sxs-lookup"><span data-stu-id="bfcec-164">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="bfcec-165">open a support ticket with the following information if available:</span><span class="sxs-lookup"><span data-stu-id="bfcec-165">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="bfcec-166">Correlation error ID</span><span class="sxs-lookup"><span data-stu-id="bfcec-166">Correlation error ID</span></span>

-   <span data-ttu-id="bfcec-167">UPN (user email address)</span><span class="sxs-lookup"><span data-stu-id="bfcec-167">UPN (user email address)</span></span>

-   <span data-ttu-id="bfcec-168">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="bfcec-168">Tenant ID</span></span>

-   <span data-ttu-id="bfcec-169">Browser type</span><span class="sxs-lookup"><span data-stu-id="bfcec-169">Browser type</span></span>

-   <span data-ttu-id="bfcec-170">Time zone and time/timeframe during error occurs</span><span class="sxs-lookup"><span data-stu-id="bfcec-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="bfcec-171">Fiddler traces</span><span class="sxs-lookup"><span data-stu-id="bfcec-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfcec-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfcec-172">Next steps</span></span>
[<span data-ttu-id="bfcec-173">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfcec-173">Managing Applications with Azure Active Directory</span></span>](what-is-application-management.md)
