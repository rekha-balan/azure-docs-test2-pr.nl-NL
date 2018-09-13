---
title: 'Tutorial: Configure Cisco for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Cisco Webex.
services: active-directory
documentationcenter: ''
author: zhchia
writer: zhchia
manager: beatrizd
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2018
ms.author: v-wingf
ms.openlocfilehash: 8f5af3cba01e925591c9d90ea0e96ed78b2823e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855776"
---
# <a name="tutorial-configure-cisco-webex-for-automatic-user-provisioning"></a><span data-ttu-id="4087b-103">Tutorial: Configure Cisco Webex for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="4087b-103">Tutorial: Configure Cisco Webex for automatic user provisioning</span></span>


<span data-ttu-id="4087b-104">The objective of this tutorial is to demonstrate the steps to be performed in Cisco Webex and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users to Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="4087b-104">The objective of this tutorial is to demonstrate the steps to be performed in Cisco Webex and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users to Cisco Webex.</span></span>


> [!NOTE]
> <span data-ttu-id="4087b-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="4087b-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span></span> <span data-ttu-id="4087b-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="4087b-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4087b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4087b-107">Prerequisites</span></span>

<span data-ttu-id="4087b-108">The scenario outlined in this tutorial assumes that you already have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="4087b-108">The scenario outlined in this tutorial assumes that you already have the following prerequisites:</span></span>

*   <span data-ttu-id="4087b-109">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="4087b-109">An Azure AD tenant</span></span>
*   <span data-ttu-id="4087b-110">A Cisco Webex tenant</span><span class="sxs-lookup"><span data-stu-id="4087b-110">A Cisco Webex tenant</span></span>
*   <span data-ttu-id="4087b-111">A user account in Cisco Webex with Admin permissions</span><span class="sxs-lookup"><span data-stu-id="4087b-111">A user account in Cisco Webex with Admin permissions</span></span>


> [!NOTE]
> <span data-ttu-id="4087b-112">The Azure AD provisioning integration relies on the [Cisco Webex Webservice](https://developer.webex.com/getting-started.html), which is available to Cisco Webex teams.</span><span class="sxs-lookup"><span data-stu-id="4087b-112">The Azure AD provisioning integration relies on the [Cisco Webex Webservice](https://developer.webex.com/getting-started.html), which is available to Cisco Webex teams.</span></span>

## <a name="adding-cisco-webex-from-the-gallery"></a><span data-ttu-id="4087b-113">Adding Cisco Webex from the gallery</span><span class="sxs-lookup"><span data-stu-id="4087b-113">Adding Cisco Webex from the gallery</span></span>
<span data-ttu-id="4087b-114">Before configuring Cisco Webex for automatic user provisioning with Azure AD, you need to add Cisco Webex from the Azure AD application gallery to your list of managed SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="4087b-114">Before configuring Cisco Webex for automatic user provisioning with Azure AD, you need to add Cisco Webex from the Azure AD application gallery to your list of managed SaaS applications.</span></span>

<span data-ttu-id="4087b-115">**To add Cisco Webex from the Azure AD application gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4087b-115">**To add Cisco Webex from the Azure AD application gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4087b-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4087b-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="4087b-118">Navigate to **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4087b-118">Navigate to **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications Section][2]

3. <span data-ttu-id="4087b-120">To add Cisco Webex, click the **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4087b-120">To add Cisco Webex, click the **New application** button on the top of the dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="4087b-122">In the search box, type **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="4087b-122">In the search box, type **Cisco Webex**.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/AppSearch.png)

5. <span data-ttu-id="4087b-124">In the results panel, select **Cisco Webex**, and then click the **Add** button to add Cisco Webex to your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="4087b-124">In the results panel, select **Cisco Webex**, and then click the **Add** button to add Cisco Webex to your list of SaaS applications.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/AppSearchResults.png)

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/AppCreation.png)

## <a name="assigning-users-to-cisco-webex"></a><span data-ttu-id="4087b-127">Assigning users to Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="4087b-127">Assigning users to Cisco Webex</span></span>

<span data-ttu-id="4087b-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="4087b-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="4087b-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="4087b-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="4087b-130">Before configuring and enabling automatic user provisioning, you should decide which users in Azure AD need access to Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="4087b-130">Before configuring and enabling automatic user provisioning, you should decide which users in Azure AD need access to Cisco Webex.</span></span> <span data-ttu-id="4087b-131">Once decided, you can assign these users to Cisco Webex by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="4087b-131">Once decided, you can assign these users to Cisco Webex by following the instructions here:</span></span>

*   [<span data-ttu-id="4087b-132">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="4087b-132">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-cisco-webex"></a><span data-ttu-id="4087b-133">Important tips for assigning users to Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="4087b-133">Important tips for assigning users to Cisco Webex</span></span>

*   <span data-ttu-id="4087b-134">It is recommended that a single Azure AD user is assigned to Cisco Webex to test the automatic user provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="4087b-134">It is recommended that a single Azure AD user is assigned to Cisco Webex to test the automatic user provisioning configuration.</span></span> <span data-ttu-id="4087b-135">Additional users may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="4087b-135">Additional users may be assigned later.</span></span>

*   <span data-ttu-id="4087b-136">When assigning a user to Cisco Webex, you must select any valid application-specific role (if available) in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="4087b-136">When assigning a user to Cisco Webex, you must select any valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="4087b-137">Users with the **Default Access** role are excluded from provisioning.</span><span class="sxs-lookup"><span data-stu-id="4087b-137">Users with the **Default Access** role are excluded from provisioning.</span></span>

## <a name="configuring-automatic-user-provisioning-to-cisco-webex"></a><span data-ttu-id="4087b-138">Configuring automatic user provisioning to Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="4087b-138">Configuring automatic user provisioning to Cisco Webex</span></span>

<span data-ttu-id="4087b-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users in Cisco Webex based on user assignments in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4087b-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users in Cisco Webex based on user assignments in Azure AD.</span></span>


### <a name="to-configure-automatic-user-provisioning-for-cisco-webex-in-azure-ad"></a><span data-ttu-id="4087b-140">To configure automatic user provisioning for Cisco Webex in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4087b-140">To configure automatic user provisioning for Cisco Webex in Azure AD:</span></span>


1. <span data-ttu-id="4087b-141">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span><span class="sxs-lookup"><span data-stu-id="4087b-141">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span></span>

2. <span data-ttu-id="4087b-142">Select Cisco Webex from your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="4087b-142">Select Cisco Webex from your list of SaaS applications.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/Successcenter2.png)

3. <span data-ttu-id="4087b-144">Select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="4087b-144">Select the **Provisioning** tab.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/ProvisioningTab.png)

4. <span data-ttu-id="4087b-146">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="4087b-146">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/ProvisioningCredentials.png)

5. <span data-ttu-id="4087b-148">Under the **Admin Credentials** section, input the **Tenant URL**, and **Secret Token** of your Cisco Webex's account.</span><span class="sxs-lookup"><span data-stu-id="4087b-148">Under the **Admin Credentials** section, input the **Tenant URL**, and **Secret Token** of your Cisco Webex's account.</span></span>

    *   <span data-ttu-id="4087b-149">In the **Tenant URL** field, populate the Cisco Webex SCIM API URL for your tenant, which takes the form of `https://api.webex.com/v1/scim/[Tenant ID]/`, where `[Tenant ID]` is an alphanumeric string as described in step 6.</span><span class="sxs-lookup"><span data-stu-id="4087b-149">In the **Tenant URL** field, populate the Cisco Webex SCIM API URL for your tenant, which takes the form of `https://api.webex.com/v1/scim/[Tenant ID]/`, where `[Tenant ID]` is an alphanumeric string as described in step 6.</span></span>

    *   <span data-ttu-id="4087b-150">In the **Secret Token** field, populate the Secret Token as described in step 6.</span><span class="sxs-lookup"><span data-stu-id="4087b-150">In the **Secret Token** field, populate the Secret Token as described in step 6.</span></span>

1. <span data-ttu-id="4087b-151">The **Tenant ID** and **Secret Token** for your Cisco Webex account can be found by logging into the [Cisco Webex developer site](https://developer.webex.com/) with your Admin account.</span><span class="sxs-lookup"><span data-stu-id="4087b-151">The **Tenant ID** and **Secret Token** for your Cisco Webex account can be found by logging into the [Cisco Webex developer site](https://developer.webex.com/) with your Admin account.</span></span> <span data-ttu-id="4087b-152">Once logged in -</span><span class="sxs-lookup"><span data-stu-id="4087b-152">Once logged in -</span></span>
    * <span data-ttu-id="4087b-153">Go to the [Getting Started page](https://developer.webex.com/getting-started.html)</span><span class="sxs-lookup"><span data-stu-id="4087b-153">Go to the [Getting Started page](https://developer.webex.com/getting-started.html)</span></span>
    * <span data-ttu-id="4087b-154">Scroll down to the [Authentication Section](https://developer.webex.com/getting-started.html#authentication)
    ![Cisco Webex Authentication Token](./media/cisco-webex-provisioning-tutorial/SecretToken.png)</span><span class="sxs-lookup"><span data-stu-id="4087b-154">Scroll down to the [Authentication Section](https://developer.webex.com/getting-started.html#authentication)
![Cisco Webex Authentication Token](./media/cisco-webex-provisioning-tutorial/SecretToken.png)</span></span>
    * <span data-ttu-id="4087b-155">The alphanumeric string in the box is your **Secret Token**.</span><span class="sxs-lookup"><span data-stu-id="4087b-155">The alphanumeric string in the box is your **Secret Token**.</span></span> <span data-ttu-id="4087b-156">Copy this token to the clipboard</span><span class="sxs-lookup"><span data-stu-id="4087b-156">Copy this token to the clipboard</span></span>
    * <span data-ttu-id="4087b-157">Go to the [Get My Own Details page](https://developer.webex.com/endpoint-people-me-get.html)</span><span class="sxs-lookup"><span data-stu-id="4087b-157">Go to the [Get My Own Details page](https://developer.webex.com/endpoint-people-me-get.html)</span></span>
        * <span data-ttu-id="4087b-158">Make sure that Test Mode is ON</span><span class="sxs-lookup"><span data-stu-id="4087b-158">Make sure that Test Mode is ON</span></span>
        * <span data-ttu-id="4087b-159">Type the word "Bearer" followed by a space, and then paste the Secret Token into the Authorization field ![Cisco Webex Authentication Token](./media/cisco-webex-provisioning-tutorial/GetMyDetails.png)</span><span class="sxs-lookup"><span data-stu-id="4087b-159">Type the word "Bearer" followed by a space, and then paste the Secret Token into the Authorization field ![Cisco Webex Authentication Token](./media/cisco-webex-provisioning-tutorial/GetMyDetails.png)</span></span>
        * <span data-ttu-id="4087b-160">Click Run</span><span class="sxs-lookup"><span data-stu-id="4087b-160">Click Run</span></span>
    * <span data-ttu-id="4087b-161">In the response text to the right, the **Tenant ID** appears as "orgId":</span><span class="sxs-lookup"><span data-stu-id="4087b-161">In the response text to the right, the **Tenant ID** appears as "orgId":</span></span>

    ```json
    {
        "id": "(...)",
        "emails": [
            "admin.user@contoso.com"
        ],
        "displayName": "John Smith",
        "nickName": "John",
        "orgId": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
        (...)
    }
    ```

1. <span data-ttu-id="4087b-162">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="4087b-162">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Cisco Webex.</span></span> <span data-ttu-id="4087b-163">If the connection fails, ensure your Cisco Webex account has Admin permissions and try again.</span><span class="sxs-lookup"><span data-stu-id="4087b-163">If the connection fails, ensure your Cisco Webex account has Admin permissions and try again.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/TestConnection.png)

8. <span data-ttu-id="4087b-165">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox - **Send an email notification when a failure occurs**.</span><span class="sxs-lookup"><span data-stu-id="4087b-165">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox - **Send an email notification when a failure occurs**.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/EmailNotification.png)

9. <span data-ttu-id="4087b-167">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4087b-167">Click **Save**.</span></span>

10. <span data-ttu-id="4087b-168">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="4087b-168">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Cisco Webex**.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/UserMapping.png)

11. <span data-ttu-id="4087b-170">Review the user attributes that are synchronized from Azure AD to Cisco Webex in the **Attribute Mapping** section.</span><span class="sxs-lookup"><span data-stu-id="4087b-170">Review the user attributes that are synchronized from Azure AD to Cisco Webex in the **Attribute Mapping** section.</span></span> <span data-ttu-id="4087b-171">The attributes selected as **Matching** properties are used to match the user accounts in Cisco Webex for update operations.</span><span class="sxs-lookup"><span data-stu-id="4087b-171">The attributes selected as **Matching** properties are used to match the user accounts in Cisco Webex for update operations.</span></span> <span data-ttu-id="4087b-172">Select the **Save** button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="4087b-172">Select the **Save** button to commit any changes.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/UserMappingAttributes.png)

12. <span data-ttu-id="4087b-174">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="4087b-174">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span></span>

13. <span data-ttu-id="4087b-175">To enable the Azure AD provisioning service for Cisco Webex, change the **Provisioning Status** to **On** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="4087b-175">To enable the Azure AD provisioning service for Cisco Webex, change the **Provisioning Status** to **On** in the **Settings** section.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/ProvisioningStatus.png)

14. <span data-ttu-id="4087b-177">Define the users and/or groups that you would like to provision to Cisco Webex by choosing the desired values in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="4087b-177">Define the users and/or groups that you would like to provision to Cisco Webex by choosing the desired values in **Scope** in the **Settings** section.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/SyncScope.png)

15. <span data-ttu-id="4087b-179">When you are ready to provision, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4087b-179">When you are ready to provision, click **Save**.</span></span>

    ![Cisco Webex Provisioning](./media/cisco-webex-provisioning-tutorial/Save.png)


<span data-ttu-id="4087b-181">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="4087b-181">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span></span> <span data-ttu-id="4087b-182">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span><span class="sxs-lookup"><span data-stu-id="4087b-182">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="4087b-183">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="4087b-183">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Cisco Webex.</span></span>

<span data-ttu-id="4087b-184">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="4087b-184">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="connector-limitations"></a><span data-ttu-id="4087b-185">Connector Limitations</span><span class="sxs-lookup"><span data-stu-id="4087b-185">Connector Limitations</span></span>

* <span data-ttu-id="4087b-186">Cisco Webex is currently in Cisco's Early Field Testing (EFT) phase.</span><span class="sxs-lookup"><span data-stu-id="4087b-186">Cisco Webex is currently in Cisco's Early Field Testing (EFT) phase.</span></span> <span data-ttu-id="4087b-187">For more information, please contact [Cisco's support team](https://www.webex.co.in/support/support-overview.html).</span><span class="sxs-lookup"><span data-stu-id="4087b-187">For more information, please contact [Cisco's support team](https://www.webex.co.in/support/support-overview.html).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4087b-188">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4087b-188">Additional resources</span></span>

* [<span data-ttu-id="4087b-189">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="4087b-189">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="4087b-190">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4087b-190">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


## <a name="next-steps"></a><span data-ttu-id="4087b-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="4087b-191">Next steps</span></span>

* [<span data-ttu-id="4087b-192">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="4087b-192">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)

<!--Image references-->
[1]: ./media/cisco-webex-provisioning-tutorial/tutorial_general_01.png
[2]: ./media/cisco-webex-provisioning-tutorial/tutorial_general_02.png
[3]: ./media/cisco-webex-provisioning-tutorial/tutorial_general_03.png
