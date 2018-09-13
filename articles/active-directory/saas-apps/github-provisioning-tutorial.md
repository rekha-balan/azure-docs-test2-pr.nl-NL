---
title: 'Tutorial: Configure GitHub for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to GitHub.
services: active-directory
documentationcenter: ''
author: asmalser-msft
writer: asmalser-msft
manager: mtillman
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: asmalser-msft
ms.openlocfilehash: f069134c0665769316b794122cc077b05941f635
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866289"
---
# <a name="tutorial-configure-github-for-automatic-user-provisioning"></a><span data-ttu-id="4608e-103">Tutorial: Configure GitHub for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="4608e-103">Tutorial: Configure GitHub for automatic user provisioning</span></span>


<span data-ttu-id="4608e-104">The objective of this tutorial is to show you the steps you need to perform in GitHub and Azure AD to automatically provision and de-provision user accounts from Azure AD to GitHub.</span><span class="sxs-lookup"><span data-stu-id="4608e-104">The objective of this tutorial is to show you the steps you need to perform in GitHub and Azure AD to automatically provision and de-provision user accounts from Azure AD to GitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4608e-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4608e-105">Prerequisites</span></span>

<span data-ttu-id="4608e-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="4608e-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="4608e-107">An Azure Active directory tenant</span><span class="sxs-lookup"><span data-stu-id="4608e-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="4608e-108">A Github tenant with the [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span><span class="sxs-lookup"><span data-stu-id="4608e-108">A Github tenant with the [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="4608e-109">A user account in GitHub with Admin permissions</span><span class="sxs-lookup"><span data-stu-id="4608e-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="4608e-110">The Azure AD provisioning integration relies on the [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available to Github teams on the Business plan or better.</span><span class="sxs-lookup"><span data-stu-id="4608e-110">The Azure AD provisioning integration relies on the [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available to Github teams on the Business plan or better.</span></span>

## <a name="assigning-users-to-github"></a><span data-ttu-id="4608e-111">Assigning users to GitHub</span><span class="sxs-lookup"><span data-stu-id="4608e-111">Assigning users to GitHub</span></span>

<span data-ttu-id="4608e-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="4608e-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="4608e-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span><span class="sxs-lookup"><span data-stu-id="4608e-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="4608e-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your GitHub app.</span><span class="sxs-lookup"><span data-stu-id="4608e-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your GitHub app.</span></span> <span data-ttu-id="4608e-115">Once decided, you can assign these users to your GitHub app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="4608e-115">Once decided, you can assign these users to your GitHub app by following the instructions here:</span></span>

[<span data-ttu-id="4608e-116">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="4608e-116">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-github"></a><span data-ttu-id="4608e-117">Important tips for assigning users to GitHub</span><span class="sxs-lookup"><span data-stu-id="4608e-117">Important tips for assigning users to GitHub</span></span>

*   <span data-ttu-id="4608e-118">It is recommended that a single Azure AD user is assigned to GitHub to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="4608e-118">It is recommended that a single Azure AD user is assigned to GitHub to test the provisioning configuration.</span></span> <span data-ttu-id="4608e-119">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="4608e-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4608e-120">When assigning a user to GitHub, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="4608e-120">When assigning a user to GitHub, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="4608e-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span><span class="sxs-lookup"><span data-stu-id="4608e-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-github"></a><span data-ttu-id="4608e-122">Configuring user provisioning to GitHub</span><span class="sxs-lookup"><span data-stu-id="4608e-122">Configuring user provisioning to GitHub</span></span> 

<span data-ttu-id="4608e-123">This section guides you through connecting your Azure AD to GitHub's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4608e-123">This section guides you through connecting your Azure AD to GitHub's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="4608e-124">You may also choose to enabled SAML-based Single Sign-On for GitHub, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4608e-124">You may also choose to enabled SAML-based Single Sign-On for GitHub, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4608e-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="4608e-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-github-in-azure-ad"></a><span data-ttu-id="4608e-126">Configure automatic user account provisioning to GitHub in Azure AD</span><span class="sxs-lookup"><span data-stu-id="4608e-126">Configure automatic user account provisioning to GitHub in Azure AD</span></span>


1. <span data-ttu-id="4608e-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span><span class="sxs-lookup"><span data-stu-id="4608e-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="4608e-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using the search field.</span><span class="sxs-lookup"><span data-stu-id="4608e-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using the search field.</span></span> <span data-ttu-id="4608e-129">Otherwise, select **Add** and search for **GitHub** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="4608e-129">Otherwise, select **Add** and search for **GitHub** in the application gallery.</span></span> <span data-ttu-id="4608e-130">Select GitHub from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="4608e-130">Select GitHub from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="4608e-131">Select your instance of GitHub, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="4608e-131">Select your instance of GitHub, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="4608e-132">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="4608e-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![GitHub Provisioning](./media/github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="4608e-134">Under the **Admin Credentials** section, click **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="4608e-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="4608e-135">This operation opens a GitHub authorization dialog in a new browser window.</span><span class="sxs-lookup"><span data-stu-id="4608e-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="4608e-136">In the new window, sign into GitHub using your Admin account.</span><span class="sxs-lookup"><span data-stu-id="4608e-136">In the new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="4608e-137">In the resulting authorization dialog, select the GitHub team that you want to enable provisioning for, and then select **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="4608e-137">In the resulting authorization dialog, select the GitHub team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="4608e-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="4608e-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

    ![Authorization Dialog](./media/github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="4608e-140">In the Azure portal, input **Tenant URL** and click **Test Connection** to ensure Azure AD can connect to your GitHub app.</span><span class="sxs-lookup"><span data-stu-id="4608e-140">In the Azure portal, input **Tenant URL** and click **Test Connection** to ensure Azure AD can connect to your GitHub app.</span></span> <span data-ttu-id="4608e-141">If the connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try the "Authorize" step again (you can constitute **Tenant URL** by rule: `https://api.github.com/scim/v2/<Organizations_name>`, you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span><span class="sxs-lookup"><span data-stu-id="4608e-141">If the connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try the "Authorize" step again (you can constitute **Tenant URL** by rule: `https://api.github.com/scim/v2/<Organizations_name>`, you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Authorization Dialog](./media/github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="4608e-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span><span class="sxs-lookup"><span data-stu-id="4608e-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="4608e-144">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4608e-144">Click **Save**.</span></span> 

10. <span data-ttu-id="4608e-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to GitHub**.</span><span class="sxs-lookup"><span data-stu-id="4608e-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to GitHub**.</span></span>

11. <span data-ttu-id="4608e-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to GitHub.</span><span class="sxs-lookup"><span data-stu-id="4608e-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to GitHub.</span></span> <span data-ttu-id="4608e-147">The attributes selected as **Matching** properties are used to match the user accounts in GitHub for update operations.</span><span class="sxs-lookup"><span data-stu-id="4608e-147">The attributes selected as **Matching** properties are used to match the user accounts in GitHub for update operations.</span></span> <span data-ttu-id="4608e-148">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="4608e-148">Select the Save button to commit any changes.</span></span>

12. <span data-ttu-id="4608e-149">To enable the Azure AD provisioning service for GitHub, change the **Provisioning Status** to **On** in the **Settings** section</span><span class="sxs-lookup"><span data-stu-id="4608e-149">To enable the Azure AD provisioning service for GitHub, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13. <span data-ttu-id="4608e-150">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4608e-150">Click **Save**.</span></span> 

<span data-ttu-id="4608e-151">This operation starts the initial synchronization of any users and/or groups assigned to GitHub in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="4608e-151">This operation starts the initial synchronization of any users and/or groups assigned to GitHub in the Users and Groups section.</span></span> <span data-ttu-id="4608e-152">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="4608e-152">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="4608e-153">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service.</span><span class="sxs-lookup"><span data-stu-id="4608e-153">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="4608e-154">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="4608e-154">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4608e-155">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4608e-155">Additional resources</span></span>

* [<span data-ttu-id="4608e-156">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="4608e-156">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="4608e-157">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4608e-157">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a><span data-ttu-id="4608e-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="4608e-158">Next steps</span></span>

* [<span data-ttu-id="4608e-159">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="4608e-159">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)
