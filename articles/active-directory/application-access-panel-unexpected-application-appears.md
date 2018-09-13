---
title: How applications appear on the access panel | Microsoft Docs
description: Troubleshoot why an application is appearing in the Access Panel
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: 2429ebef69aaddf28d10cd77bf4ce9072ea71476
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672174"
---
# <a name="how-applications-appear-on-the-access-panel"></a><span data-ttu-id="0de6b-103">How applications appear on the access panel</span><span class="sxs-lookup"><span data-stu-id="0de6b-103">How applications appear on the access panel</span></span>

<span data-ttu-id="0de6b-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span><span class="sxs-lookup"><span data-stu-id="0de6b-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="0de6b-105">These applications are configured on behalf of the user in the Azure AD portal.</span><span class="sxs-lookup"><span data-stu-id="0de6b-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="0de6b-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0de6b-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="0de6b-107">General issues to check first</span><span class="sxs-lookup"><span data-stu-id="0de6b-107">General issues to check first</span></span>

-   <span data-ttu-id="0de6b-108">If an application was just removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span><span class="sxs-lookup"><span data-stu-id="0de6b-108">If an application was just removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span></span>

-   <span data-ttu-id="0de6b-109">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span><span class="sxs-lookup"><span data-stu-id="0de6b-109">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="0de6b-110">allow for extra time before signing into the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0de6b-110">allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="0de6b-111">Problems related to assigning applications to users</span><span class="sxs-lookup"><span data-stu-id="0de6b-111">Problems related to assigning applications to users</span></span>

<span data-ttu-id="0de6b-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span><span class="sxs-lookup"><span data-stu-id="0de6b-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span></span> <span data-ttu-id="0de6b-113">Below are some ways to check:</span><span class="sxs-lookup"><span data-stu-id="0de6b-113">Below are some ways to check:</span></span>

-   [<span data-ttu-id="0de6b-114">Check if a user is assigned to the application</span><span class="sxs-lookup"><span data-stu-id="0de6b-114">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="0de6b-115">Check if a user is under a license related to the application</span><span class="sxs-lookup"><span data-stu-id="0de6b-115">Check if a user is under a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="0de6b-116">Check if a user is assigned to the application</span><span class="sxs-lookup"><span data-stu-id="0de6b-116">Check if a user is assigned to the application</span></span>

<span data-ttu-id="0de6b-117">To check if a user is assigned to the application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="0de6b-117">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="0de6b-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="0de6b-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0de6b-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="0de6b-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0de6b-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="0de6b-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0de6b-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="0de6b-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0de6b-122">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="0de6b-122">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="0de6b-123">**Search** for the name of the application in question.</span><span class="sxs-lookup"><span data-stu-id="0de6b-123">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="0de6b-124">click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0de6b-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="0de6b-125">Check to see if your user is assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="0de6b-125">Check to see if your user is assigned to the application.</span></span>

  * <span data-ttu-id="0de6b-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span><span class="sxs-lookup"><span data-stu-id="0de6b-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="0de6b-127">Check if a user is under a license related to the application</span><span class="sxs-lookup"><span data-stu-id="0de6b-127">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="0de6b-128">To check a user’s assigned licenses, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="0de6b-128">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="0de6b-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="0de6b-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0de6b-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="0de6b-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0de6b-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="0de6b-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0de6b-132">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="0de6b-132">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="0de6b-133">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0de6b-133">click **All users**.</span></span>

6.  <span data-ttu-id="0de6b-134">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="0de6b-134">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="0de6b-135">click **Licenses** to see which licenses the user currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="0de6b-135">click **Licenses** to see which licenses the user currently has assigned.</span></span>

   * <span data-ttu-id="0de6b-136">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0de6b-136">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="0de6b-137">Problems related to assigning applications to groups</span><span class="sxs-lookup"><span data-stu-id="0de6b-137">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="0de6b-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span><span class="sxs-lookup"><span data-stu-id="0de6b-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="0de6b-139">Below are some ways to check:</span><span class="sxs-lookup"><span data-stu-id="0de6b-139">Below are some ways to check:</span></span>

-   [<span data-ttu-id="0de6b-140">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="0de6b-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="0de6b-141">Check if a user is a member of a group assigned to a license</span><span class="sxs-lookup"><span data-stu-id="0de6b-141">Check if a user is a member of a group assigned to a license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="0de6b-142">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="0de6b-142">Check a user’s group memberships</span></span>

<span data-ttu-id="0de6b-143">To check a group’s membership, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="0de6b-143">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="0de6b-144">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="0de6b-144">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0de6b-145">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="0de6b-145">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0de6b-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="0de6b-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0de6b-147">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="0de6b-147">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="0de6b-148">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0de6b-148">click **All users**.</span></span>

6.  <span data-ttu-id="0de6b-149">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="0de6b-149">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="0de6b-150">click **Groups.**</span><span class="sxs-lookup"><span data-stu-id="0de6b-150">click **Groups.**</span></span>

8.  <span data-ttu-id="0de6b-151">Check to see if your user is part of a Group assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="0de6b-151">Check to see if your user is part of a Group assigned to the application.</span></span>

   * <span data-ttu-id="0de6b-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span><span class="sxs-lookup"><span data-stu-id="0de6b-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-to-a-license"></a><span data-ttu-id="0de6b-153">Check if a user is a member of a group assigned to a license</span><span class="sxs-lookup"><span data-stu-id="0de6b-153">Check if a user is a member of a group assigned to a license</span></span>

1.  <span data-ttu-id="0de6b-154">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="0de6b-154">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0de6b-155">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="0de6b-155">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0de6b-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="0de6b-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0de6b-157">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="0de6b-157">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="0de6b-158">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0de6b-158">click **All users**.</span></span>

6.  <span data-ttu-id="0de6b-159">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="0de6b-159">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="0de6b-160">click **Groups.**</span><span class="sxs-lookup"><span data-stu-id="0de6b-160">click **Groups.**</span></span>

8.  <span data-ttu-id="0de6b-161">click the row of a specific group.</span><span class="sxs-lookup"><span data-stu-id="0de6b-161">click the row of a specific group.</span></span>

9.  <span data-ttu-id="0de6b-162">click **Licenses** to see which licenses the group has assigned to it.</span><span class="sxs-lookup"><span data-stu-id="0de6b-162">click **Licenses** to see which licenses the group has assigned to it.</span></span>

  * <span data-ttu-id="0de6b-163">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0de6b-163">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="0de6b-164">If these troubleshooting steps do not the resolve the issue</span><span class="sxs-lookup"><span data-stu-id="0de6b-164">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="0de6b-165">open a support ticket with the following information if available:</span><span class="sxs-lookup"><span data-stu-id="0de6b-165">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="0de6b-166">Correlation error ID</span><span class="sxs-lookup"><span data-stu-id="0de6b-166">Correlation error ID</span></span>

-   <span data-ttu-id="0de6b-167">UPN (user email address)</span><span class="sxs-lookup"><span data-stu-id="0de6b-167">UPN (user email address)</span></span>

-   <span data-ttu-id="0de6b-168">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="0de6b-168">Tenant ID</span></span>

-   <span data-ttu-id="0de6b-169">Browser type</span><span class="sxs-lookup"><span data-stu-id="0de6b-169">Browser type</span></span>

-   <span data-ttu-id="0de6b-170">Time zone and time/timeframe during error occurs</span><span class="sxs-lookup"><span data-stu-id="0de6b-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="0de6b-171">Fiddler traces</span><span class="sxs-lookup"><span data-stu-id="0de6b-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="0de6b-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="0de6b-172">Next steps</span></span>
[<span data-ttu-id="0de6b-173">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0de6b-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
