---
title: 'Tutorial: Configure Samanage for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Samanage.
services: active-directory
documentationcenter: ''
author: zchia
writer: zchia
manager: beatrizd-msft
ms.assetid: na
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2018
ms.author: v-wingf-msft
ms.openlocfilehash: e5a69fa2ee9a8c4baaeb6586627c7a9a3c9ba4a8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857400"
---
# <a name="tutorial-configure-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="1e4a6-103">Tutorial: Configure Samanage for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="1e4a6-103">Tutorial: Configure Samanage for automatic user provisioning</span></span>

<span data-ttu-id="1e4a6-104">The objective of this tutorial is to demonstrate the steps to be performed in Samanage and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to Samanage.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-104">The objective of this tutorial is to demonstrate the steps to be performed in Samanage and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to Samanage.</span></span>

> [!NOTE]
> <span data-ttu-id="1e4a6-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span></span> <span data-ttu-id="1e4a6-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="1e4a6-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e4a6-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1e4a6-107">Prerequisites</span></span>

<span data-ttu-id="1e4a6-108">The scenario outlined in this tutorial assumes that you already have the following:</span><span class="sxs-lookup"><span data-stu-id="1e4a6-108">The scenario outlined in this tutorial assumes that you already have the following:</span></span>

*   <span data-ttu-id="1e4a6-109">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="1e4a6-109">An Azure AD tenant</span></span>
*   <span data-ttu-id="1e4a6-110">A [Samanage tenant](https://www.samanage.com/pricing/) with the Professional package</span><span class="sxs-lookup"><span data-stu-id="1e4a6-110">A [Samanage tenant](https://www.samanage.com/pricing/) with the Professional package</span></span>
*   <span data-ttu-id="1e4a6-111">A user account in Samanage with Admin permissions</span><span class="sxs-lookup"><span data-stu-id="1e4a6-111">A user account in Samanage with Admin permissions</span></span>

> [!NOTE]
> <span data-ttu-id="1e4a6-112">The Azure AD provisioning integration relies on the [Samanage Rest API](https://www.samanage.com/api/), which is available to Samanage developers for accounts with the Professional package.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-112">The Azure AD provisioning integration relies on the [Samanage Rest API](https://www.samanage.com/api/), which is available to Samanage developers for accounts with the Professional package.</span></span>

## <a name="adding-samanage-from-the-gallery"></a><span data-ttu-id="1e4a6-113">Adding Samanage from the gallery</span><span class="sxs-lookup"><span data-stu-id="1e4a6-113">Adding Samanage from the gallery</span></span>
<span data-ttu-id="1e4a6-114">Before configuring Samanage for automatic user provisioning with Azure AD, you need to add Samanage from the Azure AD application gallery to your list of managed SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-114">Before configuring Samanage for automatic user provisioning with Azure AD, you need to add Samanage from the Azure AD application gallery to your list of managed SaaS applications.</span></span>

<span data-ttu-id="1e4a6-115">**To add Samanage from the Azure AD application gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1e4a6-115">**To add Samanage from the Azure AD application gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1e4a6-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="1e4a6-118">Navigate to **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-118">Navigate to **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications Section][2]

3. <span data-ttu-id="1e4a6-120">To add Samanage, click the **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-120">To add Samanage, click the **New application** button on the top of the dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="1e4a6-122">In the search box, type **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-122">In the search box, type **Samanage**.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/AppSearch.png)

5. <span data-ttu-id="1e4a6-124">In the results panel, select **Samanage**, and then click the **Add** button to add Samanage to your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-124">In the results panel, select **Samanage**, and then click the **Add** button to add Samanage to your list of SaaS applications.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/AppSearchResults.png)

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/AppCreation.png)

## <a name="assigning-users-to-samanage"></a><span data-ttu-id="1e4a6-127">Assigning users to Samanage</span><span class="sxs-lookup"><span data-stu-id="1e4a6-127">Assigning users to Samanage</span></span>

<span data-ttu-id="1e4a6-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="1e4a6-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="1e4a6-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to Samanage.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to Samanage.</span></span> <span data-ttu-id="1e4a6-131">Once decided, you can assign these users and/or groups to Samanage by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="1e4a6-131">Once decided, you can assign these users and/or groups to Samanage by following the instructions here:</span></span>

*   [<span data-ttu-id="1e4a6-132">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="1e4a6-132">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-samanage"></a><span data-ttu-id="1e4a6-133">Important tips for assigning users to Samanage</span><span class="sxs-lookup"><span data-stu-id="1e4a6-133">Important tips for assigning users to Samanage</span></span>

*   <span data-ttu-id="1e4a6-134">It is recommended that a single Azure AD user is assigned to Samanage to test the automatic user provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-134">It is recommended that a single Azure AD user is assigned to Samanage to test the automatic user provisioning configuration.</span></span> <span data-ttu-id="1e4a6-135">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-135">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1e4a6-136">When assigning a user to Samanage, you must select any valid application-specific role (if available) in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-136">When assigning a user to Samanage, you must select any valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="1e4a6-137">Users with the **Default Access** role are excluded from provisioning.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-137">Users with the **Default Access** role are excluded from provisioning.</span></span>

## <a name="configuring-automatic-user-provisioning-to-samanage"></a><span data-ttu-id="1e4a6-138">Configuring automatic user provisioning to Samanage</span><span class="sxs-lookup"><span data-stu-id="1e4a6-138">Configuring automatic user provisioning to Samanage</span></span>

<span data-ttu-id="1e4a6-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in Samanage based on user and/or group assignments in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in Samanage based on user and/or group assignments in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="1e4a6-140">You may also choose to enable SAML-based single sign-on for Samanage, following the instructions provided in the [Samanage single sign-on tutorial](samanage-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="1e4a6-140">You may also choose to enable SAML-based single sign-on for Samanage, following the instructions provided in the [Samanage single sign-on tutorial](samanage-tutorial.md).</span></span> <span data-ttu-id="1e4a6-141">Single sign-on can be configured independently of automatic user provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-141">Single sign-on can be configured independently of automatic user provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-provisioning-for-samanage-in-azure-ad"></a><span data-ttu-id="1e4a6-142">To configure automatic user provisioning for Samanage in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1e4a6-142">To configure automatic user provisioning for Samanage in Azure AD:</span></span>

1. <span data-ttu-id="1e4a6-143">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-143">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span></span>

2. <span data-ttu-id="1e4a6-144">Select Samanage from your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-144">Select Samanage from your list of SaaS applications.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/AppInstanceSearch.png)

3. <span data-ttu-id="1e4a6-146">Select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-146">Select the **Provisioning** tab.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/ProvisioningTab.png)

4. <span data-ttu-id="1e4a6-148">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-148">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/ProvisioningCredentials.png)

5. <span data-ttu-id="1e4a6-150">Under the **Admin Credentials** section, input the **Admin Username** and **Admin Password** of your Samanage account.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-150">Under the **Admin Credentials** section, input the **Admin Username** and **Admin Password** of your Samanage account.</span></span> <span data-ttu-id="1e4a6-151">Examples of these values are:</span><span class="sxs-lookup"><span data-stu-id="1e4a6-151">Examples of these values are:</span></span>

    *   <span data-ttu-id="1e4a6-152">In the **Admin Username** field, populate the username of the admin account on your Samanage tenant.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-152">In the **Admin Username** field, populate the username of the admin account on your Samanage tenant.</span></span> <span data-ttu-id="1e4a6-153">Example: admin@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-153">Example: admin@contoso.com.</span></span>

    *   <span data-ttu-id="1e4a6-154">In the **Admin Password** field, populate the password of the admin account corresponding to the admin username.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-154">In the **Admin Password** field, populate the password of the admin account corresponding to the admin username.</span></span>

6. <span data-ttu-id="1e4a6-155">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Samanage.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-155">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Samanage.</span></span> <span data-ttu-id="1e4a6-156">If the connection fails, ensure your Samanage account has Admin permissions and try again.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-156">If the connection fails, ensure your Samanage account has Admin permissions and try again.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/TestConnection.png)

7. <span data-ttu-id="1e4a6-158">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox **Send an email notification when a failure occurs**.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-158">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox **Send an email notification when a failure occurs**.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/EmailNotification.png)

8. <span data-ttu-id="1e4a6-160">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-160">Click **Save**.</span></span>

9. <span data-ttu-id="1e4a6-161">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Samanage**.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-161">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Samanage**.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/UserMappings.png)

10. <span data-ttu-id="1e4a6-163">Review the user attributes that are synchronized from Azure AD to Samanage in the **Attribute Mappings** section.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-163">Review the user attributes that are synchronized from Azure AD to Samanage in the **Attribute Mappings** section.</span></span> <span data-ttu-id="1e4a6-164">The attributes selected as **Matching** properties are used to match the user accounts in Samanage for update operations.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-164">The attributes selected as **Matching** properties are used to match the user accounts in Samanage for update operations.</span></span> <span data-ttu-id="1e4a6-165">Select the **Save** button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-165">Select the **Save** button to commit any changes.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/UserAttributeMapping.png)

11. <span data-ttu-id="1e4a6-167">To enable group mappings, under the **Mappings** section, select **Synchronize Azure Active Directory Groups to Samanage**.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-167">To enable group mappings, under the **Mappings** section, select **Synchronize Azure Active Directory Groups to Samanage**.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/GroupMappings.png)

12. <span data-ttu-id="1e4a6-169">Set **Enabled** to **Yes** to synchronize groups.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-169">Set **Enabled** to **Yes** to synchronize groups.</span></span> <span data-ttu-id="1e4a6-170">Review the group attributes that are synchronized from Azure AD to Samanage in the **Attribute Mappings** section.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-170">Review the group attributes that are synchronized from Azure AD to Samanage in the **Attribute Mappings** section.</span></span> <span data-ttu-id="1e4a6-171">The attributes selected as **Matching** properties are used to match the user accounts in Samanage for update operations.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-171">The attributes selected as **Matching** properties are used to match the user accounts in Samanage for update operations.</span></span> <span data-ttu-id="1e4a6-172">Select the **Save** button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-172">Select the **Save** button to commit any changes.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/GroupAttributeMapping.png)

13. <span data-ttu-id="1e4a6-174">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="1e4a6-174">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span></span>

14. <span data-ttu-id="1e4a6-175">To enable the Azure AD provisioning service for Samanage, change the **Provisioning Status** to **On** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-175">To enable the Azure AD provisioning service for Samanage, change the **Provisioning Status** to **On** in the **Settings** section.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/ProvisioningStatus.png)

15. <span data-ttu-id="1e4a6-177">Define the users and/or groups that you would like to provision to Samanage by choosing the desired values in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-177">Define the users and/or groups that you would like to provision to Samanage by choosing the desired values in **Scope** in the **Settings** section.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/ScopeSync.png)

16. <span data-ttu-id="1e4a6-179">When you are ready to provision, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-179">When you are ready to provision, click **Save**.</span></span>

    ![Samanage Provisioning](./media/samanage-provisioning-tutorial/SaveProvisioning.png)


<span data-ttu-id="1e4a6-181">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-181">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span></span> <span data-ttu-id="1e4a6-182">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-182">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="1e4a6-183">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Samanage.</span><span class="sxs-lookup"><span data-stu-id="1e4a6-183">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Samanage.</span></span>

<span data-ttu-id="1e4a6-184">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="1e4a6-184">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e4a6-185">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1e4a6-185">Additional resources</span></span>

* [<span data-ttu-id="1e4a6-186">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="1e4a6-186">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="1e4a6-187">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e4a6-187">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


## <a name="next-steps"></a><span data-ttu-id="1e4a6-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e4a6-188">Next steps</span></span>

* [<span data-ttu-id="1e4a6-189">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="1e4a6-189">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)

<!--Image references-->
[1]: ./media/samanage-provisioning-tutorial/tutorial_general_01.png
[2]: ./media/samanage-provisioning-tutorial/tutorial_general_02.png
[3]: ./media/samanage-provisioning-tutorial/tutorial_general_03.png
