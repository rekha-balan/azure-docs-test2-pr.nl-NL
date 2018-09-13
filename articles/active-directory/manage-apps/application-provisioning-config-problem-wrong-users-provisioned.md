---
title: Wrong set of users are being provisioned to an Azure AD Gallery application | Microsoft Docs
description: Learn how to find out why a different set of users are being provisioned to an application than those you expected
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
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: 2c2dd2208cf910456fa8f94ca739b7ef8875d475
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857048"
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a><span data-ttu-id="3e8e2-103">Wrong set of users are being provisioned to an Azure AD Gallery application</span><span class="sxs-lookup"><span data-stu-id="3e8e2-103">Wrong set of users are being provisioned to an Azure AD Gallery application</span></span>

<span data-ttu-id="3e8e2-104">Which users are provisioned to the app is primarily driven by which users and groups have been **assigned** to the application.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-104">Which users are provisioned to the app is primarily driven by which users and groups have been **assigned** to the application.</span></span>

<span data-ttu-id="3e8e2-105">Use the following resources to learn how to check which users and groups have been assigned to an application within Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-105">Use the following resources to learn how to check which users and groups have been assigned to an application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="3e8e2-106">Assign a user directly as an administrator</span><span class="sxs-lookup"><span data-stu-id="3e8e2-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="3e8e2-107">To assign one or more users to an application directly, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="3e8e2-107">To assign one or more users to an application directly, follow these steps:</span></span>

1.  <span data-ttu-id="3e8e2-108">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="3e8e2-108">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3e8e2-109">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-109">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="3e8e2-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3e8e2-111">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-111">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="3e8e2-112">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-112">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="3e8e2-113">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="3e8e2-113">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="3e8e2-114">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-114">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="3e8e2-115">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-115">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="3e8e2-116">To open the **Add Assignment** pane, click the **Add** button on top of the **Users and Groups** list.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-116">To open the **Add Assignment** pane, click the **Add** button on top of the **Users and Groups** list.</span></span>

9.  <span data-ttu-id="3e8e2-117">click the **Users and groups** selector from the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-117">click the **Users and groups** selector from the **Add Assignment** pane.</span></span>

10. <span data-ttu-id="3e8e2-118">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-118">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3e8e2-119">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-119">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="3e8e2-120">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-120">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="3e8e2-121">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-121">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="3e8e2-122">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-122">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="3e8e2-123">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-123">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="3e8e2-124">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-124">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="3e8e2-125">If provisioning is configured and already running for an app, new users should be provisioned to an application in approximately 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-125">If provisioning is configured and already running for an app, new users should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="3e8e2-126">Check the **Audit Logs** for details.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-126">Check the **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="3e8e2-127">Assign a group directly to an application as an administrator</span><span class="sxs-lookup"><span data-stu-id="3e8e2-127">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="3e8e2-128">To assign one or more groups to an application directly, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="3e8e2-128">To assign one or more groups to an application directly, follow these steps:</span></span>

1.  <span data-ttu-id="3e8e2-129">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="3e8e2-129">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3e8e2-130">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-130">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="3e8e2-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3e8e2-132">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-132">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="3e8e2-133">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-133">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="3e8e2-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="3e8e2-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="3e8e2-135">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-135">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="3e8e2-136">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-136">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="3e8e2-137">To open the **Add Assignment** pane, click the **Add** button on top of the **Users and Groups** list.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-137">To open the **Add Assignment** pane, click the **Add** button on top of the **Users and Groups** list.</span></span>

9.  <span data-ttu-id="3e8e2-138">click the **Users and groups** selector from the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-138">click the **Users and groups** selector from the **Add Assignment** pane.</span></span>

10. <span data-ttu-id="3e8e2-139">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-139">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3e8e2-140">Hover over the **group** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-140">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="3e8e2-141">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-141">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="3e8e2-142">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-142">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="3e8e2-143">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-143">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="3e8e2-144">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the groups you have selected.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-144">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="3e8e2-145">Click the **Assign** button to assign the application to the selected groups.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-145">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="3e8e2-146">If provisioning is configured and already running for an app, new users contained within the group should be provisioned to an application in approximately 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-146">If provisioning is configured and already running for an app, new users contained within the group should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="3e8e2-147">Check the **Audit Logs** for details.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-147">Check the **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="3e8e2-148">Provisioning of the group name and group details, in addition to the members, if supported for some applications.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-148">Provisioning of the group name and group details, in addition to the members, if supported for some applications.</span></span> <span data-ttu-id="3e8e2-149">You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-149">You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="3e8e2-150">If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-150">If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”.</span></span> <span data-ttu-id="3e8e2-151">This can be the display name or email alias, as the group and its members not be provisioned if the matching property is empty or not populated for a group in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e8e2-151">This can be the display name or email alias, as the group and its members not be provisioned if the matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e8e2-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="3e8e2-152">Next steps</span></span>
[<span data-ttu-id="3e8e2-153">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e8e2-153">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](user-provisioning.md)
