---
title: How to assign users and groups to an application | Microsoft Docs
description: Assign users to the application to grant access
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
ms.openlocfilehash: 972ed736e63089a69726de5d26236b930b390a10
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669266"
---
# <a name="how-to-assign-users-and-groups-to-an-application"></a><span data-ttu-id="2f76c-103">How to assign users and groups to an application</span><span class="sxs-lookup"><span data-stu-id="2f76c-103">How to assign users and groups to an application</span></span>

<span data-ttu-id="2f76c-104">Before your users can do any of the below for a specific application, you need to first **assign them to the application** to grant them access:</span><span class="sxs-lookup"><span data-stu-id="2f76c-104">Before your users can do any of the below for a specific application, you need to first **assign them to the application** to grant them access:</span></span>

-   <span data-ttu-id="2f76c-105">Access an application by **navigating to the application’s URL directly** (also known as SP-initiated sign-on).</span><span class="sxs-lookup"><span data-stu-id="2f76c-105">Access an application by **navigating to the application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="2f76c-106">Access an application by using the **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span><span class="sxs-lookup"><span data-stu-id="2f76c-106">Access an application by using the **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="2f76c-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span><span class="sxs-lookup"><span data-stu-id="2f76c-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="2f76c-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="2f76c-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-to-assign-applications-with-azure-active-directory"></a><span data-ttu-id="2f76c-109">Methods to assign applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f76c-109">Methods to assign applications with Azure Active Directory</span></span> 

<span data-ttu-id="2f76c-110">There are 3 ways you can assign applications with Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="2f76c-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="2f76c-111">Assign a user directly to an application as an administrator</span><span class="sxs-lookup"><span data-stu-id="2f76c-111">Assign a user directly to an application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="2f76c-112">Assign a group directly to an application as an administrator</span><span class="sxs-lookup"><span data-stu-id="2f76c-112">Assign a group directly to an application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="2f76c-113">Enable self-service application access to allow users to find their own applications</span><span class="sxs-lookup"><span data-stu-id="2f76c-113">Enable self-service application access to allow users to find their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="2f76c-114">Assign a user directly as an administrator</span><span class="sxs-lookup"><span data-stu-id="2f76c-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="2f76c-115">To assign one or more users to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="2f76c-115">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="2f76c-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="2f76c-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2f76c-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="2f76c-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2f76c-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="2f76c-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2f76c-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="2f76c-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2f76c-120">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="2f76c-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="2f76c-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="2f76c-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="2f76c-122">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="2f76c-122">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="2f76c-123">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="2f76c-123">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2f76c-124">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="2f76c-124">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="2f76c-125">click the **Users and groups** selector from the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="2f76c-125">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="2f76c-126">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="2f76c-126">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="2f76c-127">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="2f76c-127">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="2f76c-128">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="2f76c-128">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="2f76c-129">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="2f76c-129">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="2f76c-130">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="2f76c-130">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="2f76c-131">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="2f76c-131">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="2f76c-132">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="2f76c-132">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="2f76c-133">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span><span class="sxs-lookup"><span data-stu-id="2f76c-133">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="2f76c-134">Assign a group directly to an application as an administrator</span><span class="sxs-lookup"><span data-stu-id="2f76c-134">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="2f76c-135">To assign one or more groups to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="2f76c-135">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="2f76c-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="2f76c-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2f76c-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="2f76c-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2f76c-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="2f76c-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2f76c-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="2f76c-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2f76c-140">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="2f76c-140">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="2f76c-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="2f76c-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="2f76c-142">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="2f76c-142">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="2f76c-143">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="2f76c-143">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2f76c-144">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="2f76c-144">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="2f76c-145">click the **Users and groups** selector from the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="2f76c-145">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="2f76c-146">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="2f76c-146">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="2f76c-147">Hover over the **group** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="2f76c-147">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="2f76c-148">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="2f76c-148">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="2f76c-149">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="2f76c-149">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="2f76c-150">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="2f76c-150">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="2f76c-151">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span><span class="sxs-lookup"><span data-stu-id="2f76c-151">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="2f76c-152">Click the **Assign** button to assign the application to the selected groups.</span><span class="sxs-lookup"><span data-stu-id="2f76c-152">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="2f76c-153">After a short period of time, the users within the groups you have selected be able to launch these applications using the methods described in the solution description section.</span><span class="sxs-lookup"><span data-stu-id="2f76c-153">After a short period of time, the users within the groups you have selected be able to launch these applications using the methods described in the solution description section.</span></span> <span data-ttu-id="2f76c-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span><span class="sxs-lookup"><span data-stu-id="2f76c-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="2f76c-155">Enable self-service application access to allow users to find their own applications</span><span class="sxs-lookup"><span data-stu-id="2f76c-155">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="2f76c-156">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span><span class="sxs-lookup"><span data-stu-id="2f76c-156">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="2f76c-157">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span><span class="sxs-lookup"><span data-stu-id="2f76c-157">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="2f76c-158">To enable self-service application access to an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="2f76c-158">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="2f76c-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="2f76c-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2f76c-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="2f76c-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2f76c-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="2f76c-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2f76c-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="2f76c-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2f76c-163">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="2f76c-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="2f76c-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="2f76c-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="2f76c-165">Select the application you want to enable Self-service access to from the list.</span><span class="sxs-lookup"><span data-stu-id="2f76c-165">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="2f76c-166">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="2f76c-166">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="2f76c-167">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span><span class="sxs-lookup"><span data-stu-id="2f76c-167">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="2f76c-168">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span><span class="sxs-lookup"><span data-stu-id="2f76c-168">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="2f76c-169">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="2f76c-169">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="2f76c-170">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="2f76c-170">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="2f76c-171">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span><span class="sxs-lookup"><span data-stu-id="2f76c-171">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="2f76c-172">Groups are not supported.</span><span class="sxs-lookup"><span data-stu-id="2f76c-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="2f76c-173">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span><span class="sxs-lookup"><span data-stu-id="2f76c-173">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="2f76c-174">Click the **Save** button at the top of the blade to finish.</span><span class="sxs-lookup"><span data-stu-id="2f76c-174">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="2f76c-175">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span><span class="sxs-lookup"><span data-stu-id="2f76c-175">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="2f76c-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="2f76c-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="2f76c-177">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span><span class="sxs-lookup"><span data-stu-id="2f76c-177">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="2f76c-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span><span class="sxs-lookup"><span data-stu-id="2f76c-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f76c-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f76c-179">Next steps</span></span>
[<span data-ttu-id="2f76c-180">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="2f76c-180">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
