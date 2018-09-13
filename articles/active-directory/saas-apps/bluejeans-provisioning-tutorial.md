---
title: 'Tutorial: Configure BlueJeans for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to BlueJeans.
services: active-directory
documentationcenter: ''
author: zhchia
writer: zhchia
manager: beatrizd-msft
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2018
ms.author: v-ant
ms.openlocfilehash: ce27a6f78dfdeb00e1e7b2c82c928d28f1504a1d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871006"
---
# <a name="tutorial-configure-bluejeans-for-automatic-user-provisioning"></a><span data-ttu-id="9d68b-103">Tutorial: Configure BlueJeans for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="9d68b-103">Tutorial: Configure BlueJeans for automatic user provisioning</span></span>

<span data-ttu-id="9d68b-104">The objective of this tutorial is to demonstrate the steps to be performed in BlueJeans and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="9d68b-104">The objective of this tutorial is to demonstrate the steps to be performed in BlueJeans and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to BlueJeans.</span></span>

> [!NOTE]
> <span data-ttu-id="9d68b-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="9d68b-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span></span> <span data-ttu-id="9d68b-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="9d68b-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d68b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9d68b-107">Prerequisites</span></span>

<span data-ttu-id="9d68b-108">The scenario outlined in this tutorial assumes that you already have the following:</span><span class="sxs-lookup"><span data-stu-id="9d68b-108">The scenario outlined in this tutorial assumes that you already have the following:</span></span>

*   <span data-ttu-id="9d68b-109">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="9d68b-109">An Azure AD tenant</span></span>
*   <span data-ttu-id="9d68b-110">A BlueJeans tenant with the [My Company](https://www.BlueJeans.com/pricing) plan or better enabled</span><span class="sxs-lookup"><span data-stu-id="9d68b-110">A BlueJeans tenant with the [My Company](https://www.BlueJeans.com/pricing) plan or better enabled</span></span>
*   <span data-ttu-id="9d68b-111">A user account in BlueJeans with Admin permissions</span><span class="sxs-lookup"><span data-stu-id="9d68b-111">A user account in BlueJeans with Admin permissions</span></span>

> [!NOTE]
> <span data-ttu-id="9d68b-112">The Azure AD provisioning integration relies on the [BlueJeans API](https://BlueJeans.github.io/developer), which is available to BlueJeans teams on the Standard plan or better.</span><span class="sxs-lookup"><span data-stu-id="9d68b-112">The Azure AD provisioning integration relies on the [BlueJeans API](https://BlueJeans.github.io/developer), which is available to BlueJeans teams on the Standard plan or better.</span></span>

## <a name="adding-bluejeans-from-the-gallery"></a><span data-ttu-id="9d68b-113">Adding BlueJeans from the gallery</span><span class="sxs-lookup"><span data-stu-id="9d68b-113">Adding BlueJeans from the gallery</span></span>
<span data-ttu-id="9d68b-114">Before configuring BlueJeans for automatic user provisioning with Azure AD, you need to add BlueJeans from the Azure AD application gallery to your list of managed SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="9d68b-114">Before configuring BlueJeans for automatic user provisioning with Azure AD, you need to add BlueJeans from the Azure AD application gallery to your list of managed SaaS applications.</span></span>

<span data-ttu-id="9d68b-115">**To add BlueJeans from the Azure AD application gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9d68b-115">**To add BlueJeans from the Azure AD application gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d68b-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9d68b-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="9d68b-118">Navigate to **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9d68b-118">Navigate to **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications Section][2]
    
3. <span data-ttu-id="9d68b-120">To add BlueJeans, click the **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="9d68b-120">To add BlueJeans, click the **New application** button on the top of the dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="9d68b-122">In the search box, type **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="9d68b-122">In the search box, type **BlueJeans**.</span></span>

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/BluejeansAppSearch.png)

5. <span data-ttu-id="9d68b-124">In the results panel, select **BlueJeans**, and then click the **Add** button to add BlueJeans to your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="9d68b-124">In the results panel, select **BlueJeans**, and then click the **Add** button to add BlueJeans to your list of SaaS applications.</span></span>

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/BluejeansAppSearchResults.png)

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/BluejeansAppCreate.png)
    
## <a name="assigning-users-to-bluejeans"></a><span data-ttu-id="9d68b-127">Assigning users to BlueJeans</span><span class="sxs-lookup"><span data-stu-id="9d68b-127">Assigning users to BlueJeans</span></span>

<span data-ttu-id="9d68b-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="9d68b-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="9d68b-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="9d68b-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="9d68b-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="9d68b-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to BlueJeans.</span></span> <span data-ttu-id="9d68b-131">Once decided, you can assign these users and/or groups to BlueJeans by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="9d68b-131">Once decided, you can assign these users and/or groups to BlueJeans by following the instructions here:</span></span>

*   [<span data-ttu-id="9d68b-132">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="9d68b-132">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-bluejeans"></a><span data-ttu-id="9d68b-133">Important tips for assigning users to BlueJeans</span><span class="sxs-lookup"><span data-stu-id="9d68b-133">Important tips for assigning users to BlueJeans</span></span>

*   <span data-ttu-id="9d68b-134">It is recommended that a single Azure AD user is assigned to BlueJeans to test the automatic user provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="9d68b-134">It is recommended that a single Azure AD user is assigned to BlueJeans to test the automatic user provisioning configuration.</span></span> <span data-ttu-id="9d68b-135">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="9d68b-135">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="9d68b-136">When assigning a user to BlueJeans, you must select any valid application-specific role (if available) in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="9d68b-136">When assigning a user to BlueJeans, you must select any valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="9d68b-137">Users with the **Default Access** role are excluded from provisioning.</span><span class="sxs-lookup"><span data-stu-id="9d68b-137">Users with the **Default Access** role are excluded from provisioning.</span></span>

## <a name="configuring-automatic-user-provisioning-to-bluejeans"></a><span data-ttu-id="9d68b-138">Configuring automatic user provisioning to BlueJeans</span><span class="sxs-lookup"><span data-stu-id="9d68b-138">Configuring automatic user provisioning to BlueJeans</span></span>

<span data-ttu-id="9d68b-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in BlueJeans based on user and/or group assignments in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d68b-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in BlueJeans based on user and/or group assignments in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="9d68b-140">You may also choose to enable SAML-based single sign-on for BlueJeans, following the instructions provided in the [BlueJeans single sign-on tutorial](bluejeans-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="9d68b-140">You may also choose to enable SAML-based single sign-on for BlueJeans, following the instructions provided in the [BlueJeans single sign-on tutorial](bluejeans-tutorial.md).</span></span> <span data-ttu-id="9d68b-141">Single sign-on can be configured independently of automatic user provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="9d68b-141">Single sign-on can be configured independently of automatic user provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-provisioning-for-bluejeans-in-azure-ad"></a><span data-ttu-id="9d68b-142">To configure automatic user provisioning for BlueJeans in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9d68b-142">To configure automatic user provisioning for BlueJeans in Azure AD:</span></span>

1. <span data-ttu-id="9d68b-143">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span><span class="sxs-lookup"><span data-stu-id="9d68b-143">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span></span>

2. <span data-ttu-id="9d68b-144">Select BlueJeans from your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="9d68b-144">Select BlueJeans from your list of SaaS applications.</span></span>
 
    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/Bluejeans2.png)

3. <span data-ttu-id="9d68b-146">Select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="9d68b-146">Select the **Provisioning** tab.</span></span>

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/BluejeansProvisioningTab.png)

4. <span data-ttu-id="9d68b-148">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="9d68b-148">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/Bluejeans1.png)

5. <span data-ttu-id="9d68b-150">Under the **Admin Credentials** section, input the **Admin Username**, and **Admin Password** of your BlueJeans account.</span><span class="sxs-lookup"><span data-stu-id="9d68b-150">Under the **Admin Credentials** section, input the **Admin Username**, and **Admin Password** of your BlueJeans account.</span></span> <span data-ttu-id="9d68b-151">Examples of these values are:</span><span class="sxs-lookup"><span data-stu-id="9d68b-151">Examples of these values are:</span></span>

    *   <span data-ttu-id="9d68b-152">In the **Admin Username** field, populate the username of the admin account on your BlueJeans tenant.</span><span class="sxs-lookup"><span data-stu-id="9d68b-152">In the **Admin Username** field, populate the username of the admin account on your BlueJeans tenant.</span></span> <span data-ttu-id="9d68b-153">Example: admin@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9d68b-153">Example: admin@contoso.com.</span></span>

    *   <span data-ttu-id="9d68b-154">In the **Admin Password** field, populate the password corresponding to the admin username.</span><span class="sxs-lookup"><span data-stu-id="9d68b-154">In the **Admin Password** field, populate the password corresponding to the admin username.</span></span>

6. <span data-ttu-id="9d68b-155">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="9d68b-155">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to BlueJeans.</span></span> <span data-ttu-id="9d68b-156">If the connection fails, ensure your BlueJeans account has Admin permissions and try again.</span><span class="sxs-lookup"><span data-stu-id="9d68b-156">If the connection fails, ensure your BlueJeans account has Admin permissions and try again.</span></span>

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/BluejeansTestConnection.png)

7. <span data-ttu-id="9d68b-158">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox - **Send an email notification when a failure occurs**.</span><span class="sxs-lookup"><span data-stu-id="9d68b-158">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox - **Send an email notification when a failure occurs**.</span></span>

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/BluejeansNotificationEmail.png)

8. <span data-ttu-id="9d68b-160">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9d68b-160">Click **Save**.</span></span>

9. <span data-ttu-id="9d68b-161">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="9d68b-161">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to BlueJeans**.</span></span>

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/BluejeansMapping.png)

10. <span data-ttu-id="9d68b-163">Review the user attributes that are synchronized from Azure AD to BlueJeans in the **Attribute Mapping** section.</span><span class="sxs-lookup"><span data-stu-id="9d68b-163">Review the user attributes that are synchronized from Azure AD to BlueJeans in the **Attribute Mapping** section.</span></span> <span data-ttu-id="9d68b-164">The attributes selected as **Matching** properties are used to match the user accounts in BlueJeans for update operations.</span><span class="sxs-lookup"><span data-stu-id="9d68b-164">The attributes selected as **Matching** properties are used to match the user accounts in BlueJeans for update operations.</span></span> <span data-ttu-id="9d68b-165">Select the **Save** button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="9d68b-165">Select the **Save** button to commit any changes.</span></span>

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/BluejeansUserMappingAtrributes.png)

11. <span data-ttu-id="9d68b-167">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="9d68b-167">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span></span>

12. <span data-ttu-id="9d68b-168">To enable the Azure AD provisioning service for BlueJeans, change the **Provisioning Status** to **On** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="9d68b-168">To enable the Azure AD provisioning service for BlueJeans, change the **Provisioning Status** to **On** in the **Settings** section.</span></span>

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/BluejeansProvisioningStatus.png)

13. <span data-ttu-id="9d68b-170">Define the users and/or groups that you would like to provision to BlueJeans by choosing the desired values in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="9d68b-170">Define the users and/or groups that you would like to provision to BlueJeans by choosing the desired values in **Scope** in the **Settings** section.</span></span>

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/UserGroupSelection.png)

14. <span data-ttu-id="9d68b-172">When you are ready to provision, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9d68b-172">When you are ready to provision, click **Save**.</span></span>

    ![BlueJeans Provisioning](./media/bluejeans-provisioning-tutorial/SaveProvisioning.png)

<span data-ttu-id="9d68b-174">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="9d68b-174">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span></span> <span data-ttu-id="9d68b-175">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span><span class="sxs-lookup"><span data-stu-id="9d68b-175">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="9d68b-176">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="9d68b-176">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on BlueJeans.</span></span>

<span data-ttu-id="9d68b-177">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="9d68b-177">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="connector-limitations"></a><span data-ttu-id="9d68b-178">Connector Limitations</span><span class="sxs-lookup"><span data-stu-id="9d68b-178">Connector Limitations</span></span>

* <span data-ttu-id="9d68b-179">Bluejeans does not allow usernames that exceed 30 characters.</span><span class="sxs-lookup"><span data-stu-id="9d68b-179">Bluejeans does not allow usernames that exceed 30 characters.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d68b-180">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9d68b-180">Additional resources</span></span>

* [<span data-ttu-id="9d68b-181">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="9d68b-181">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="9d68b-182">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d68b-182">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a><span data-ttu-id="9d68b-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d68b-183">Next steps</span></span>

* [<span data-ttu-id="9d68b-184">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="9d68b-184">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)

<!--Image references-->
[1]: ./media/bluejeans-provisioning-tutorial/tutorial_general_01.png
[2]: ./media/bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/bluejeans-tutorial/tutorial_general_03.png
