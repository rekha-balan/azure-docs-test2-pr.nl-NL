---
title: 'Tutorial: Configure Tableau Online for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Tableau Online.
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
ms.date: 07/30/2018
ms.author: v-wingf-msft
ms.openlocfilehash: 4f6297fa8477ff4794bee589737e047993427c06
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866423"
---
# <a name="tutorial-configure-tableau-online-for-automatic-user-provisioning"></a><span data-ttu-id="221bb-103">Tutorial: Configure Tableau Online for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="221bb-103">Tutorial: Configure Tableau Online for automatic user provisioning</span></span>

<span data-ttu-id="221bb-104">The objective of this tutorial is to demonstrate the steps to be performed in Tableau Online and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="221bb-104">The objective of this tutorial is to demonstrate the steps to be performed in Tableau Online and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to Tableau Online.</span></span>

> [!NOTE]
> <span data-ttu-id="221bb-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="221bb-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span></span> <span data-ttu-id="221bb-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="221bb-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="221bb-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="221bb-107">Prerequisites</span></span>

<span data-ttu-id="221bb-108">The scenario outlined in this tutorial assumes that you already have the following:</span><span class="sxs-lookup"><span data-stu-id="221bb-108">The scenario outlined in this tutorial assumes that you already have the following:</span></span>

*   <span data-ttu-id="221bb-109">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="221bb-109">An Azure AD tenant</span></span>
*   <span data-ttu-id="221bb-110">A [Tableau Online tenant](https://www.tableau.com/)</span><span class="sxs-lookup"><span data-stu-id="221bb-110">A [Tableau Online tenant](https://www.tableau.com/)</span></span>
*   <span data-ttu-id="221bb-111">A user account in Tableau Online with Admin permissions</span><span class="sxs-lookup"><span data-stu-id="221bb-111">A user account in Tableau Online with Admin permissions</span></span>

> [!NOTE]
> <span data-ttu-id="221bb-112">The Azure AD provisioning integration relies on the [Tableau Online Rest API](https://onlinehelp.tableau.com/current/api/rest_api/en-us/help.htm), which is available to Tableau Online developers.</span><span class="sxs-lookup"><span data-stu-id="221bb-112">The Azure AD provisioning integration relies on the [Tableau Online Rest API](https://onlinehelp.tableau.com/current/api/rest_api/en-us/help.htm), which is available to Tableau Online developers.</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="221bb-113">Adding Tableau Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="221bb-113">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="221bb-114">Before configuring Tableau Online for automatic user provisioning with Azure AD, you need to add Tableau Online from the Azure AD application gallery to your list of managed SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="221bb-114">Before configuring Tableau Online for automatic user provisioning with Azure AD, you need to add Tableau Online from the Azure AD application gallery to your list of managed SaaS applications.</span></span>

<span data-ttu-id="221bb-115">**To add Tableau Online from the Azure AD application gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="221bb-115">**To add Tableau Online from the Azure AD application gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="221bb-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="221bb-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="221bb-118">Navigate to **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="221bb-118">Navigate to **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications Section][2]

3. <span data-ttu-id="221bb-120">To add Tableau Online, click the **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="221bb-120">To add Tableau Online, click the **New application** button on the top of the dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="221bb-122">In the search box, type **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="221bb-122">In the search box, type **Tableau Online**.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/AppSearch.png)

5. <span data-ttu-id="221bb-124">In the results panel, select **Tableau Online**, and then click the **Add** button to add Tableau Online to your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="221bb-124">In the results panel, select **Tableau Online**, and then click the **Add** button to add Tableau Online to your list of SaaS applications.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/AppSearchResults.png)

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/AppCreation.png)

## <a name="assigning-users-to-tableau-online"></a><span data-ttu-id="221bb-127">Assigning users to Tableau Online</span><span class="sxs-lookup"><span data-stu-id="221bb-127">Assigning users to Tableau Online</span></span>

<span data-ttu-id="221bb-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="221bb-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="221bb-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="221bb-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="221bb-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="221bb-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to Tableau Online.</span></span> <span data-ttu-id="221bb-131">Once decided, you can assign these users and/or groups to Tableau Online by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="221bb-131">Once decided, you can assign these users and/or groups to Tableau Online by following the instructions here:</span></span>

*   [<span data-ttu-id="221bb-132">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="221bb-132">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-tableau-online"></a><span data-ttu-id="221bb-133">Important tips for assigning users to Tableau Online</span><span class="sxs-lookup"><span data-stu-id="221bb-133">Important tips for assigning users to Tableau Online</span></span>

*   <span data-ttu-id="221bb-134">It is recommended that a single Azure AD user is assigned to Tableau Online to test the automatic user provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="221bb-134">It is recommended that a single Azure AD user is assigned to Tableau Online to test the automatic user provisioning configuration.</span></span> <span data-ttu-id="221bb-135">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="221bb-135">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="221bb-136">When assigning a user to Tableau Online, you must select any valid application-specific role (if available) in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="221bb-136">When assigning a user to Tableau Online, you must select any valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="221bb-137">Users with the **Default Access** role are excluded from provisioning.</span><span class="sxs-lookup"><span data-stu-id="221bb-137">Users with the **Default Access** role are excluded from provisioning.</span></span>

## <a name="configuring-automatic-user-provisioning-to-tableau-online"></a><span data-ttu-id="221bb-138">Configuring automatic user provisioning to Tableau Online</span><span class="sxs-lookup"><span data-stu-id="221bb-138">Configuring automatic user provisioning to Tableau Online</span></span>

<span data-ttu-id="221bb-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in Tableau Online based on user and/or group assignments in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="221bb-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in Tableau Online based on user and/or group assignments in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="221bb-140">You may also choose to enable SAML-based single sign-on for Tableau Online, following the instructions provided in the [Tableau Online single sign-on tutorial](tableauonline-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="221bb-140">You may also choose to enable SAML-based single sign-on for Tableau Online, following the instructions provided in the [Tableau Online single sign-on tutorial](tableauonline-tutorial.md).</span></span> <span data-ttu-id="221bb-141">Single sign-on can be configured independently of automatic user provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="221bb-141">Single sign-on can be configured independently of automatic user provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-provisioning-for-tableau-online-in-azure-ad"></a><span data-ttu-id="221bb-142">To configure automatic user provisioning for Tableau Online in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="221bb-142">To configure automatic user provisioning for Tableau Online in Azure AD:</span></span>

1. <span data-ttu-id="221bb-143">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span><span class="sxs-lookup"><span data-stu-id="221bb-143">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span></span>

2. <span data-ttu-id="221bb-144">Select Tableau Online from your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="221bb-144">Select Tableau Online from your list of SaaS applications.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/AppInstanceSearch.png)

3. <span data-ttu-id="221bb-146">Select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="221bb-146">Select the **Provisioning** tab.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/ProvisioningTab.png)

4. <span data-ttu-id="221bb-148">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="221bb-148">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/ProvisioningCredentials.png)

5. <span data-ttu-id="221bb-150">Under the **Admin Credentials** section, input the **Domain**, **Admin Username**, **Admin Password**, and **Content URL** of your Tableau Online account:</span><span class="sxs-lookup"><span data-stu-id="221bb-150">Under the **Admin Credentials** section, input the **Domain**, **Admin Username**, **Admin Password**, and **Content URL** of your Tableau Online account:</span></span>

    *   <span data-ttu-id="221bb-151">In the **Domain** field, populate subdomain based on Step 6.</span><span class="sxs-lookup"><span data-stu-id="221bb-151">In the **Domain** field, populate subdomain based on Step 6.</span></span>

    *   <span data-ttu-id="221bb-152">In the **Admin Username** field, populate the username of the admin account on your Clarizen Tenant.</span><span class="sxs-lookup"><span data-stu-id="221bb-152">In the **Admin Username** field, populate the username of the admin account on your Clarizen Tenant.</span></span> <span data-ttu-id="221bb-153">Example: admin@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="221bb-153">Example: admin@contoso.com.</span></span>

    *   <span data-ttu-id="221bb-154">In the **Admin Password** field, populate the password of the admin account corresponding to the admin username.</span><span class="sxs-lookup"><span data-stu-id="221bb-154">In the **Admin Password** field, populate the password of the admin account corresponding to the admin username.</span></span>

    *   <span data-ttu-id="221bb-155">In the **Content URL** field, populate subdomain based on Step 6.</span><span class="sxs-lookup"><span data-stu-id="221bb-155">In the **Content URL** field, populate subdomain based on Step 6.</span></span>

6. <span data-ttu-id="221bb-156">After logging in to your administrative account for Tableau Online, the values for **Domain** and **Content URL** can be extracted from the URL of the Admin page.</span><span class="sxs-lookup"><span data-stu-id="221bb-156">After logging in to your administrative account for Tableau Online, the values for **Domain** and **Content URL** can be extracted from the URL of the Admin page.</span></span>

    *   <span data-ttu-id="221bb-157">The **Domain** for your Tableau Online account can be copied from this part of the URL: ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/DomainUrlPart.png)</span><span class="sxs-lookup"><span data-stu-id="221bb-157">The **Domain** for your Tableau Online account can be copied from this part of the URL: ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/DomainUrlPart.png)</span></span>

    *   <span data-ttu-id="221bb-158">The **Content URL** for your Tableau Online account can be copied from this section, and is a value defined during account set-up.</span><span class="sxs-lookup"><span data-stu-id="221bb-158">The **Content URL** for your Tableau Online account can be copied from this section, and is a value defined during account set-up.</span></span> <span data-ttu-id="221bb-159">In this example, the value is "contoso": ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/ContentUrlPart.png)</span><span class="sxs-lookup"><span data-stu-id="221bb-159">In this example, the value is "contoso": ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/ContentUrlPart.png)</span></span>

        > [!NOTE]
        > <span data-ttu-id="221bb-160">Your **Domain** may be different from the one shown here.</span><span class="sxs-lookup"><span data-stu-id="221bb-160">Your **Domain** may be different from the one shown here.</span></span> 


7. <span data-ttu-id="221bb-161">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="221bb-161">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Tableau Online.</span></span> <span data-ttu-id="221bb-162">If the connection fails, ensure your Tableau Online account has Admin permissions and try again.</span><span class="sxs-lookup"><span data-stu-id="221bb-162">If the connection fails, ensure your Tableau Online account has Admin permissions and try again.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/TestConnection.png)

8. <span data-ttu-id="221bb-164">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox **Send an email notification when a failure occurs**.</span><span class="sxs-lookup"><span data-stu-id="221bb-164">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox **Send an email notification when a failure occurs**.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/EmailNotification.png)

10. <span data-ttu-id="221bb-166">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="221bb-166">Click **Save**.</span></span>

11. <span data-ttu-id="221bb-167">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Tableau**.</span><span class="sxs-lookup"><span data-stu-id="221bb-167">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Tableau**.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/UserMappings.png)

12. <span data-ttu-id="221bb-169">Review the user attributes that are synchronized from Azure AD to Tableau Online in the **Attribute Mapping** section.</span><span class="sxs-lookup"><span data-stu-id="221bb-169">Review the user attributes that are synchronized from Azure AD to Tableau Online in the **Attribute Mapping** section.</span></span> <span data-ttu-id="221bb-170">The attributes selected as **Matching** properties are used to match the user accounts in Tableau Online for update operations.</span><span class="sxs-lookup"><span data-stu-id="221bb-170">The attributes selected as **Matching** properties are used to match the user accounts in Tableau Online for update operations.</span></span> <span data-ttu-id="221bb-171">Select the **Save** button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="221bb-171">Select the **Save** button to commit any changes.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/UserAttributeMapping.png)

13. <span data-ttu-id="221bb-173">Under the **Mappings** section, select **Synchronize Azure Active Directory Groups to Tableau**.</span><span class="sxs-lookup"><span data-stu-id="221bb-173">Under the **Mappings** section, select **Synchronize Azure Active Directory Groups to Tableau**.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/GroupMappings.png)

14. <span data-ttu-id="221bb-175">Review the group attributes that are synchronized from Azure AD to Tableau Online in the **Attribute Mapping** section.</span><span class="sxs-lookup"><span data-stu-id="221bb-175">Review the group attributes that are synchronized from Azure AD to Tableau Online in the **Attribute Mapping** section.</span></span> <span data-ttu-id="221bb-176">The attributes selected as **Matching** properties are used to match the user accounts in Tableau Online for update operations.</span><span class="sxs-lookup"><span data-stu-id="221bb-176">The attributes selected as **Matching** properties are used to match the user accounts in Tableau Online for update operations.</span></span> <span data-ttu-id="221bb-177">Select the **Save** button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="221bb-177">Select the **Save** button to commit any changes.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/GroupAttributeMapping.png)

15. <span data-ttu-id="221bb-179">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="221bb-179">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span></span>

16. <span data-ttu-id="221bb-180">To enable the Azure AD provisioning service for Tableau Online, change the **Provisioning Status** to **On** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="221bb-180">To enable the Azure AD provisioning service for Tableau Online, change the **Provisioning Status** to **On** in the **Settings** section.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/ProvisioningStatus.png)

17. <span data-ttu-id="221bb-182">Define the users and/or groups that you would like to provision to Tableau Online by choosing the desired values in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="221bb-182">Define the users and/or groups that you would like to provision to Tableau Online by choosing the desired values in **Scope** in the **Settings** section.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/ScopeSync.png)

18. <span data-ttu-id="221bb-184">When you are ready to provision, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="221bb-184">When you are ready to provision, click **Save**.</span></span>

    ![Tableau Online Provisioning](./media/tableau-online-provisioning-tutorial/SaveProvisioning.png)

<span data-ttu-id="221bb-186">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="221bb-186">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span></span> <span data-ttu-id="221bb-187">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span><span class="sxs-lookup"><span data-stu-id="221bb-187">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="221bb-188">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="221bb-188">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Tableau Online.</span></span>

<span data-ttu-id="221bb-189">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="221bb-189">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="221bb-190">Additional resources</span><span class="sxs-lookup"><span data-stu-id="221bb-190">Additional resources</span></span>

* [<span data-ttu-id="221bb-191">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="221bb-191">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="221bb-192">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="221bb-192">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


## <a name="next-steps"></a><span data-ttu-id="221bb-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="221bb-193">Next steps</span></span>

* [<span data-ttu-id="221bb-194">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="221bb-194">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)

<!--Image references-->
[1]: ./media/tableau-online-provisioning-tutorial/tutorial_general_01.png
[2]: ./media/tableau-online-provisioning-tutorial/tutorial_general_02.png
[3]: ./media/tableau-online-provisioning-tutorial/tutorial_general_03.png
