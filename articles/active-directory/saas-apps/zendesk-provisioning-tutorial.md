---
title: 'Tutorial: Configure Zendesk for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Zendesk.
services: active-directory
documentationcenter: ''
author: zhchia
writer: zhchia
manager: beatrizd-msft
ms.assetid: na
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2018
ms.author: v-ant
ms.openlocfilehash: 2dc965547511d27ed43a88c1f45b50593b30a937
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857905"
---
# <a name="tutorial-configure-zendesk-for-automatic-user-provisioning"></a><span data-ttu-id="06430-103">Tutorial: Configure Zendesk for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="06430-103">Tutorial: Configure Zendesk for automatic user provisioning</span></span>

<span data-ttu-id="06430-104">The objective of this tutorial is to demonstrate the steps to be performed in Zendesk and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to Zendesk.</span><span class="sxs-lookup"><span data-stu-id="06430-104">The objective of this tutorial is to demonstrate the steps to be performed in Zendesk and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to Zendesk.</span></span> 

> [!NOTE]
> <span data-ttu-id="06430-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="06430-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span></span> <span data-ttu-id="06430-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="06430-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06430-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="06430-107">Prerequisites</span></span>

<span data-ttu-id="06430-108">The scenario outlined in this tutorial assumes that you already have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="06430-108">The scenario outlined in this tutorial assumes that you already have the following prerequisites:</span></span>

*   <span data-ttu-id="06430-109">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="06430-109">An Azure AD tenant</span></span>
*   <span data-ttu-id="06430-110">A Zendesk tenant with the [Enterprise](https://www.zendesk.com/product/pricing/) plan or better enabled</span><span class="sxs-lookup"><span data-stu-id="06430-110">A Zendesk tenant with the [Enterprise](https://www.zendesk.com/product/pricing/) plan or better enabled</span></span> 
*   <span data-ttu-id="06430-111">A user account in Zendesk with Admin permissions</span><span class="sxs-lookup"><span data-stu-id="06430-111">A user account in Zendesk with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="06430-112">The Azure AD provisioning integration relies on the [Zendesk Rest API](https://developer.zendesk.com/rest_api/docs/core/introduction), which is available to Zendesk teams on the Enterprise plan or better.</span><span class="sxs-lookup"><span data-stu-id="06430-112">The Azure AD provisioning integration relies on the [Zendesk Rest API](https://developer.zendesk.com/rest_api/docs/core/introduction), which is available to Zendesk teams on the Enterprise plan or better.</span></span>

## <a name="adding-zendesk-from-the-gallery"></a><span data-ttu-id="06430-113">Adding Zendesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="06430-113">Adding Zendesk from the gallery</span></span>
<span data-ttu-id="06430-114">Before configuring Zendesk for automatic user provisioning with Azure AD, you need to add Zendesk from the Azure AD application gallery to your list of managed SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="06430-114">Before configuring Zendesk for automatic user provisioning with Azure AD, you need to add Zendesk from the Azure AD application gallery to your list of managed SaaS applications.</span></span>

<span data-ttu-id="06430-115">**To add Zendesk from the Azure AD application gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="06430-115">**To add Zendesk from the Azure AD application gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="06430-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="06430-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="06430-118">Navigate to **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="06430-118">Navigate to **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications Section][2]
    
3. <span data-ttu-id="06430-120">To add Zendesk, click the **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="06430-120">To add Zendesk, click the **New application** button on the top of the dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="06430-122">In the search box, type **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="06430-122">In the search box, type **Zendesk**.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk6.png)

5. <span data-ttu-id="06430-124">In the results panel, select **Zendesk**, and then click the **Add** button to add Zendesk to your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="06430-124">In the results panel, select **Zendesk**, and then click the **Add** button to add Zendesk to your list of SaaS applications.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk7.png)

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk20.png)

## <a name="assigning-users-to-zendesk"></a><span data-ttu-id="06430-127">Assigning users to Zendesk</span><span class="sxs-lookup"><span data-stu-id="06430-127">Assigning users to Zendesk</span></span>

<span data-ttu-id="06430-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="06430-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="06430-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="06430-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="06430-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to Zendesk.</span><span class="sxs-lookup"><span data-stu-id="06430-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to Zendesk.</span></span> <span data-ttu-id="06430-131">Once decided, you can assign these users and/or groups to Zendesk by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="06430-131">Once decided, you can assign these users and/or groups to Zendesk by following the instructions here:</span></span>

*   [<span data-ttu-id="06430-132">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="06430-132">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-zendesk"></a><span data-ttu-id="06430-133">Important tips for assigning users to Zendesk</span><span class="sxs-lookup"><span data-stu-id="06430-133">Important tips for assigning users to Zendesk</span></span>

*   <span data-ttu-id="06430-134">It is recommended that a single Azure AD user is assigned to Zendesk to test the automatic user provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="06430-134">It is recommended that a single Azure AD user is assigned to Zendesk to test the automatic user provisioning configuration.</span></span> <span data-ttu-id="06430-135">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="06430-135">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="06430-136">When assigning a user to Zendesk, you must select any valid application-specific role (if available) in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="06430-136">When assigning a user to Zendesk, you must select any valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="06430-137">Users with the **Default Access** role are excluded from provisioning.</span><span class="sxs-lookup"><span data-stu-id="06430-137">Users with the **Default Access** role are excluded from provisioning.</span></span>

## <a name="configuring-automatic-user-provisioning-to-zendesk"></a><span data-ttu-id="06430-138">Configuring automatic user provisioning to Zendesk</span><span class="sxs-lookup"><span data-stu-id="06430-138">Configuring automatic user provisioning to Zendesk</span></span> 

<span data-ttu-id="06430-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in Zendesk based on user and/or group assignments in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06430-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in Zendesk based on user and/or group assignments in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="06430-140">You may also choose to enable SAML-based single sign-on for Zendesk, following the instructions provided in the [Zendesk single sign-on tutorial](zendesk-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="06430-140">You may also choose to enable SAML-based single sign-on for Zendesk, following the instructions provided in the [Zendesk single sign-on tutorial](zendesk-tutorial.md).</span></span> <span data-ttu-id="06430-141">Single sign-on can be configured independently of automatic user provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="06430-141">Single sign-on can be configured independently of automatic user provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-provisioning-for-zendesk-in-azure-ad"></a><span data-ttu-id="06430-142">To configure automatic user provisioning for Zendesk in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="06430-142">To configure automatic user provisioning for Zendesk in Azure AD:</span></span>

1. <span data-ttu-id="06430-143">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span><span class="sxs-lookup"><span data-stu-id="06430-143">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span></span>

2. <span data-ttu-id="06430-144">Select Zendesk from your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="06430-144">Select Zendesk from your list of SaaS applications.</span></span>
 
    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk3.png)

3. <span data-ttu-id="06430-146">Select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="06430-146">Select the **Provisioning** tab.</span></span>
    
    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk16.png)

4. <span data-ttu-id="06430-148">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="06430-148">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk1.png)

5. <span data-ttu-id="06430-150">Under the **Admin Credentials** section, input the **Admin Username**, **Secret Token**, and **Domain** of your Zendesk's account.</span><span class="sxs-lookup"><span data-stu-id="06430-150">Under the **Admin Credentials** section, input the **Admin Username**, **Secret Token**, and **Domain** of your Zendesk's account.</span></span> <span data-ttu-id="06430-151">Examples of these values are:</span><span class="sxs-lookup"><span data-stu-id="06430-151">Examples of these values are:</span></span>

    *   <span data-ttu-id="06430-152">In the **Admin Username** field, populate the username of the admin account on your Zendesk tenant.</span><span class="sxs-lookup"><span data-stu-id="06430-152">In the **Admin Username** field, populate the username of the admin account on your Zendesk tenant.</span></span> <span data-ttu-id="06430-153">Example: admin@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="06430-153">Example: admin@contoso.com.</span></span>

    *   <span data-ttu-id="06430-154">In the **Secret Token** field, populate the secret token as described in Step 6.</span><span class="sxs-lookup"><span data-stu-id="06430-154">In the **Secret Token** field, populate the secret token as described in Step 6.</span></span>

    *   <span data-ttu-id="06430-155">In the **Domain** field, populate the subdomain of your Zendesk tenant.</span><span class="sxs-lookup"><span data-stu-id="06430-155">In the **Domain** field, populate the subdomain of your Zendesk tenant.</span></span>
    <span data-ttu-id="06430-156">Example: For an account with a tenant URL of https://my-tenant.zendesk.com, your subdomain would be **my-tenant**.</span><span class="sxs-lookup"><span data-stu-id="06430-156">Example: For an account with a tenant URL of https://my-tenant.zendesk.com, your subdomain would be **my-tenant**.</span></span>

6. <span data-ttu-id="06430-157">The **Secret Token** for your Zendesk account is located in **Admin > API > Settings**.</span><span class="sxs-lookup"><span data-stu-id="06430-157">The **Secret Token** for your Zendesk account is located in **Admin > API > Settings**.</span></span> 

    <span data-ttu-id="06430-158">![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk4.png) ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk2.png)</span><span class="sxs-lookup"><span data-stu-id="06430-158">![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk4.png) ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk2.png)</span></span>

7. <span data-ttu-id="06430-159">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Zendesk.</span><span class="sxs-lookup"><span data-stu-id="06430-159">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Zendesk.</span></span> <span data-ttu-id="06430-160">If the connection fails, ensure your Zendesk account has Admin permissions and try again.</span><span class="sxs-lookup"><span data-stu-id="06430-160">If the connection fails, ensure your Zendesk account has Admin permissions and try again.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk19.png)
    
8. <span data-ttu-id="06430-162">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox - **Send an email notification when a failure occurs**.</span><span class="sxs-lookup"><span data-stu-id="06430-162">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox - **Send an email notification when a failure occurs**.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk9.png)

9. <span data-ttu-id="06430-164">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="06430-164">Click **Save**.</span></span>

10. <span data-ttu-id="06430-165">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="06430-165">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Zendesk**.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk10.png)

11. <span data-ttu-id="06430-167">Review the user attributes that are synchronized from Azure AD to Zendesk in the **Attribute Mapping** section.</span><span class="sxs-lookup"><span data-stu-id="06430-167">Review the user attributes that are synchronized from Azure AD to Zendesk in the **Attribute Mapping** section.</span></span> <span data-ttu-id="06430-168">The attributes selected as **Matching** properties are used to match the user accounts in Zendesk for update operations.</span><span class="sxs-lookup"><span data-stu-id="06430-168">The attributes selected as **Matching** properties are used to match the user accounts in Zendesk for update operations.</span></span> <span data-ttu-id="06430-169">Select the **Save** button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="06430-169">Select the **Save** button to commit any changes.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk11.png)

12. <span data-ttu-id="06430-171">Under the **Mappings** section, select **Synchronize Azure Active Directory Groups to ZenDesk**.</span><span class="sxs-lookup"><span data-stu-id="06430-171">Under the **Mappings** section, select **Synchronize Azure Active Directory Groups to ZenDesk**.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk12.png)

13. <span data-ttu-id="06430-173">Review the group attributes that are synchronized from Azure AD to Zendesk in the **Attribute Mapping** section.</span><span class="sxs-lookup"><span data-stu-id="06430-173">Review the group attributes that are synchronized from Azure AD to Zendesk in the **Attribute Mapping** section.</span></span> <span data-ttu-id="06430-174">The attributes selected as **Matching** properties are used to match the groups in Zendesk for update operations.</span><span class="sxs-lookup"><span data-stu-id="06430-174">The attributes selected as **Matching** properties are used to match the groups in Zendesk for update operations.</span></span> <span data-ttu-id="06430-175">Select the **Save** button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="06430-175">Select the **Save** button to commit any changes.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk13.png)

14. <span data-ttu-id="06430-177">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="06430-177">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span></span>

15. <span data-ttu-id="06430-178">To enable the Azure AD provisioning service for Zendesk, change the **Provisioning Status** to **On** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="06430-178">To enable the Azure AD provisioning service for Zendesk, change the **Provisioning Status** to **On** in the **Settings** section.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk14.png)

16. <span data-ttu-id="06430-180">Define the users and/or groups that you would like to provision to Zendesk by choosing the desired values in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="06430-180">Define the users and/or groups that you would like to provision to Zendesk by choosing the desired values in **Scope** in the **Settings** section.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk15.png)

17. <span data-ttu-id="06430-182">When you are ready to provision, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="06430-182">When you are ready to provision, click **Save**.</span></span>

    ![Zendesk Provisioning](./media/zendesk-provisioning-tutorial/ZenDesk18.png)


<span data-ttu-id="06430-184">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="06430-184">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span></span> <span data-ttu-id="06430-185">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span><span class="sxs-lookup"><span data-stu-id="06430-185">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="06430-186">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Zendesk.</span><span class="sxs-lookup"><span data-stu-id="06430-186">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Zendesk.</span></span>

<span data-ttu-id="06430-187">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="06430-187">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="connector-limitations"></a><span data-ttu-id="06430-188">Connector Limitations</span><span class="sxs-lookup"><span data-stu-id="06430-188">Connector Limitations</span></span>
* <span data-ttu-id="06430-189">Zendesk supports usage of groups for Users with Agent roles only.</span><span class="sxs-lookup"><span data-stu-id="06430-189">Zendesk supports usage of groups for Users with Agent roles only.</span></span> <span data-ttu-id="06430-190">For more information, please refer to [Zendesk's documentation](https://support.zendesk.com/hc/en-us/articles/203661966-Creating-managing-and-using-groups).</span><span class="sxs-lookup"><span data-stu-id="06430-190">For more information, please refer to [Zendesk's documentation](https://support.zendesk.com/hc/en-us/articles/203661966-Creating-managing-and-using-groups).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="06430-191">Additional resources</span><span class="sxs-lookup"><span data-stu-id="06430-191">Additional resources</span></span>

* [<span data-ttu-id="06430-192">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="06430-192">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="06430-193">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="06430-193">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a><span data-ttu-id="06430-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="06430-194">Next steps</span></span>

* [<span data-ttu-id="06430-195">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="06430-195">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)

<!--Image references-->
[1]: ./media/zendesk-tutorial/tutorial_general_01.png
[2]: ./media/zendesk-tutorial/tutorial_general_02.png
[3]: ./media/zendesk-tutorial/tutorial_general_03.png
