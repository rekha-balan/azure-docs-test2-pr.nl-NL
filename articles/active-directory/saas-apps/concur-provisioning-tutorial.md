---
title: 'Tutorial: Configure Concur for automatic user provisioning with Azure Active Directory| Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Concur.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: 5832444cd30d60f7b5fe7fe6108acd5604389474
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867385"
---
# <a name="tutorial-configure-concur-for-automatic-user-provisioning"></a><span data-ttu-id="0c529-103">Tutorial: Configure Concur for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="0c529-103">Tutorial: Configure Concur for automatic user provisioning</span></span>

<span data-ttu-id="0c529-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span><span class="sxs-lookup"><span data-stu-id="0c529-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c529-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0c529-105">Prerequisites</span></span>

<span data-ttu-id="0c529-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="0c529-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="0c529-107">An Azure Active directory tenant.</span><span class="sxs-lookup"><span data-stu-id="0c529-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="0c529-108">A Concur single sign-on enabled subscription.</span><span class="sxs-lookup"><span data-stu-id="0c529-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="0c529-109">A user account in Concur with Team Admin permissions.</span><span class="sxs-lookup"><span data-stu-id="0c529-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-to-concur"></a><span data-ttu-id="0c529-110">Assigning users to Concur</span><span class="sxs-lookup"><span data-stu-id="0c529-110">Assigning users to Concur</span></span>

<span data-ttu-id="0c529-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="0c529-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="0c529-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span><span class="sxs-lookup"><span data-stu-id="0c529-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="0c529-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span><span class="sxs-lookup"><span data-stu-id="0c529-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span></span> <span data-ttu-id="0c529-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="0c529-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span></span>

[<span data-ttu-id="0c529-115">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="0c529-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-concur"></a><span data-ttu-id="0c529-116">Important tips for assigning users to Concur</span><span class="sxs-lookup"><span data-stu-id="0c529-116">Important tips for assigning users to Concur</span></span>

*   <span data-ttu-id="0c529-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="0c529-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span></span> <span data-ttu-id="0c529-118">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="0c529-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="0c529-119">When assigning a user to Concur, you must select a valid user role.</span><span class="sxs-lookup"><span data-stu-id="0c529-119">When assigning a user to Concur, you must select a valid user role.</span></span> <span data-ttu-id="0c529-120">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="0c529-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="0c529-121">Enable user provisioning</span><span class="sxs-lookup"><span data-stu-id="0c529-121">Enable user provisioning</span></span>

<span data-ttu-id="0c529-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c529-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="0c529-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c529-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0c529-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="0c529-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="0c529-125">To configure user account provisioning:</span><span class="sxs-lookup"><span data-stu-id="0c529-125">To configure user account provisioning:</span></span>

<span data-ttu-id="0c529-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span><span class="sxs-lookup"><span data-stu-id="0c529-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="0c529-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span><span class="sxs-lookup"><span data-stu-id="0c529-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="0c529-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span><span class="sxs-lookup"><span data-stu-id="0c529-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="0c529-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span><span class="sxs-lookup"><span data-stu-id="0c529-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="0c529-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span><span class="sxs-lookup"><span data-stu-id="0c529-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="0c529-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span><span class="sxs-lookup"><span data-stu-id="0c529-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="0c529-132">This assigns ownership to the profile.</span><span class="sxs-lookup"><span data-stu-id="0c529-132">This assigns ownership to the profile.</span></span> <span data-ttu-id="0c529-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span><span class="sxs-lookup"><span data-stu-id="0c529-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="0c529-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span><span class="sxs-lookup"><span data-stu-id="0c529-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="0c529-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span><span class="sxs-lookup"><span data-stu-id="0c529-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="0c529-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span><span class="sxs-lookup"><span data-stu-id="0c529-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="0c529-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span><span class="sxs-lookup"><span data-stu-id="0c529-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="0c529-138">This is why you are supposed to create distinct WS Admin profiles.</span><span class="sxs-lookup"><span data-stu-id="0c529-138">This is why you are supposed to create distinct WS Admin profiles.</span></span>

* <span data-ttu-id="0c529-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span><span class="sxs-lookup"><span data-stu-id="0c529-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="0c529-140">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0c529-140">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="0c529-141">Log on to your **Concur** tenant.</span><span class="sxs-lookup"><span data-stu-id="0c529-141">Log on to your **Concur** tenant.</span></span>

2. <span data-ttu-id="0c529-142">From the **Administration** menu, select **Web Services**.</span><span class="sxs-lookup"><span data-stu-id="0c529-142">From the **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="0c529-143">![Concur tenant](./media/concur-provisioning-tutorial/IC721729.png "Concur tenant")</span><span class="sxs-lookup"><span data-stu-id="0c529-143">![Concur tenant](./media/concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="0c529-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span><span class="sxs-lookup"><span data-stu-id="0c529-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="0c529-145">![Enable Partner Application](./media/concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span><span class="sxs-lookup"><span data-stu-id="0c529-145">![Enable Partner Application](./media/concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="0c529-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="0c529-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="0c529-147">![Microsoft Azure Active Directory](./media/concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="0c529-147">![Microsoft Azure Active Directory](./media/concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="0c529-148">Click **Yes** to close the **Confirm Action** dialog.</span><span class="sxs-lookup"><span data-stu-id="0c529-148">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="0c529-149">![Confirm Action](./media/concur-provisioning-tutorial/ic721732.png "Confirm Action")</span><span class="sxs-lookup"><span data-stu-id="0c529-149">![Confirm Action](./media/concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="0c529-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span><span class="sxs-lookup"><span data-stu-id="0c529-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="0c529-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span><span class="sxs-lookup"><span data-stu-id="0c529-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span></span> <span data-ttu-id="0c529-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="0c529-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span></span> <span data-ttu-id="0c529-153">Select Concur from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="0c529-153">Select Concur from the search results, and add it to your list of applications.</span></span>

8. <span data-ttu-id="0c529-154">Select your instance of Concur, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="0c529-154">Select your instance of Concur, then select the **Provisioning** tab.</span></span>

9. <span data-ttu-id="0c529-155">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="0c529-155">Set the **Provisioning Mode** to **Automatic**.</span></span> 
 
    ![provisioning](./media/concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="0c529-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span><span class="sxs-lookup"><span data-stu-id="0c529-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="0c529-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span><span class="sxs-lookup"><span data-stu-id="0c529-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span></span> <span data-ttu-id="0c529-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span><span class="sxs-lookup"><span data-stu-id="0c529-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="0c529-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span><span class="sxs-lookup"><span data-stu-id="0c529-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

13. <span data-ttu-id="0c529-161">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="0c529-161">Click **Save.**</span></span>

14. <span data-ttu-id="0c529-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span><span class="sxs-lookup"><span data-stu-id="0c529-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span></span>

15. <span data-ttu-id="0c529-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span><span class="sxs-lookup"><span data-stu-id="0c529-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span></span> <span data-ttu-id="0c529-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span><span class="sxs-lookup"><span data-stu-id="0c529-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span></span> <span data-ttu-id="0c529-165">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="0c529-165">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="0c529-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span><span class="sxs-lookup"><span data-stu-id="0c529-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

17. <span data-ttu-id="0c529-167">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="0c529-167">Click **Save.**</span></span>

<span data-ttu-id="0c529-168">You can now create a test account.</span><span class="sxs-lookup"><span data-stu-id="0c529-168">You can now create a test account.</span></span> <span data-ttu-id="0c529-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span><span class="sxs-lookup"><span data-stu-id="0c529-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0c529-170">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0c529-170">Additional resources</span></span>

* [<span data-ttu-id="0c529-171">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="0c529-171">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="0c529-172">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0c529-172">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="0c529-173">Configure Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="0c529-173">Configure Single Sign-on</span></span>](concur-tutorial.md)

