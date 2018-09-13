---
title: 'Tutorial: Configure Cisco Spark for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Cisco Spark.
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
ms.openlocfilehash: aafbde6907e59be3b0ff1d5807ffe4a7d2fffaa4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870694"
---
# <a name="tutorial-configure-cisco-spark-for-automatic-user-provisioning"></a><span data-ttu-id="cde64-103">Tutorial: Configure Cisco Spark for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="cde64-103">Tutorial: Configure Cisco Spark for automatic user provisioning</span></span>


<span data-ttu-id="cde64-104">The objective of this tutorial is to demonstrate the steps to be performed in Cisco Spark and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users to Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="cde64-104">The objective of this tutorial is to demonstrate the steps to be performed in Cisco Spark and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users to Cisco Spark.</span></span>


> [!NOTE]
> <span data-ttu-id="cde64-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="cde64-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span></span> <span data-ttu-id="cde64-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="cde64-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cde64-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cde64-107">Prerequisites</span></span>

<span data-ttu-id="cde64-108">The scenario outlined in this tutorial assumes that you already have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="cde64-108">The scenario outlined in this tutorial assumes that you already have the following prerequisites:</span></span>

*   <span data-ttu-id="cde64-109">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="cde64-109">An Azure AD tenant</span></span>
*   <span data-ttu-id="cde64-110">A Cisco Spark tenant</span><span class="sxs-lookup"><span data-stu-id="cde64-110">A Cisco Spark tenant</span></span>
*   <span data-ttu-id="cde64-111">A user account in Cisco Spark with Admin permissions</span><span class="sxs-lookup"><span data-stu-id="cde64-111">A user account in Cisco Spark with Admin permissions</span></span>


> [!NOTE]
> <span data-ttu-id="cde64-112">The Azure AD provisioning integration relies on the [Cisco Spark Webservice](https://developer.webex.com/getting-started.html), which is available to Cisco Spark teams.</span><span class="sxs-lookup"><span data-stu-id="cde64-112">The Azure AD provisioning integration relies on the [Cisco Spark Webservice](https://developer.webex.com/getting-started.html), which is available to Cisco Spark teams.</span></span>

## <a name="adding-cisco-spark-from-the-gallery"></a><span data-ttu-id="cde64-113">Adding Cisco Spark from the gallery</span><span class="sxs-lookup"><span data-stu-id="cde64-113">Adding Cisco Spark from the gallery</span></span>
<span data-ttu-id="cde64-114">Before configuring Cisco Spark for automatic user provisioning with Azure AD, you need to add Cisco Spark from the Azure AD application gallery to your list of managed SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="cde64-114">Before configuring Cisco Spark for automatic user provisioning with Azure AD, you need to add Cisco Spark from the Azure AD application gallery to your list of managed SaaS applications.</span></span>

<span data-ttu-id="cde64-115">**To add Cisco Spark from the Azure AD application gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cde64-115">**To add Cisco Spark from the Azure AD application gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cde64-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cde64-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="cde64-118">Navigate to **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cde64-118">Navigate to **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications Section][2]

3. <span data-ttu-id="cde64-120">To add Cisco Spark, click the **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="cde64-120">To add Cisco Spark, click the **New application** button on the top of the dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="cde64-122">In the search box, type **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="cde64-122">In the search box, type **Cisco Spark**.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/AppSearch.png)

5. <span data-ttu-id="cde64-124">In the results panel, select **Cisco Spark**, and then click the **Add** button to add Cisco Spark to your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="cde64-124">In the results panel, select **Cisco Spark**, and then click the **Add** button to add Cisco Spark to your list of SaaS applications.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/AppSearchResults.png)

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/AppCreation.png)

## <a name="assigning-users-to-cisco-spark"></a><span data-ttu-id="cde64-127">Assigning users to Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="cde64-127">Assigning users to Cisco Spark</span></span>

<span data-ttu-id="cde64-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="cde64-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="cde64-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="cde64-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="cde64-130">Before configuring and enabling automatic user provisioning, you should decide which users in Azure AD need access to Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="cde64-130">Before configuring and enabling automatic user provisioning, you should decide which users in Azure AD need access to Cisco Spark.</span></span> <span data-ttu-id="cde64-131">Once decided, you can assign these users to Cisco Spark by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="cde64-131">Once decided, you can assign these users to Cisco Spark by following the instructions here:</span></span>

*   [<span data-ttu-id="cde64-132">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="cde64-132">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-cisco-spark"></a><span data-ttu-id="cde64-133">Important tips for assigning users to Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="cde64-133">Important tips for assigning users to Cisco Spark</span></span>

*   <span data-ttu-id="cde64-134">It is recommended that a single Azure AD user is assigned to Cisco Spark to test the automatic user provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="cde64-134">It is recommended that a single Azure AD user is assigned to Cisco Spark to test the automatic user provisioning configuration.</span></span> <span data-ttu-id="cde64-135">Additional users may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="cde64-135">Additional users may be assigned later.</span></span>

*   <span data-ttu-id="cde64-136">When assigning a user to Cisco Spark, you must select any valid application-specific role (if available) in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="cde64-136">When assigning a user to Cisco Spark, you must select any valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="cde64-137">Users with the **Default Access** role are excluded from provisioning.</span><span class="sxs-lookup"><span data-stu-id="cde64-137">Users with the **Default Access** role are excluded from provisioning.</span></span>

## <a name="configuring-automatic-user-provisioning-to-cisco-spark"></a><span data-ttu-id="cde64-138">Configuring automatic user provisioning to Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="cde64-138">Configuring automatic user provisioning to Cisco Spark</span></span>

<span data-ttu-id="cde64-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users in Cisco Spark based on user assignments in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cde64-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users in Cisco Spark based on user assignments in Azure AD.</span></span>


### <a name="to-configure-automatic-user-provisioning-for-cisco-spark-in-azure-ad"></a><span data-ttu-id="cde64-140">To configure automatic user provisioning for Cisco Spark in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="cde64-140">To configure automatic user provisioning for Cisco Spark in Azure AD:</span></span>


1. <span data-ttu-id="cde64-141">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span><span class="sxs-lookup"><span data-stu-id="cde64-141">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span></span>

2. <span data-ttu-id="cde64-142">Select Cisco Spark from your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="cde64-142">Select Cisco Spark from your list of SaaS applications.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/Successcenter2.png)

3. <span data-ttu-id="cde64-144">Select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="cde64-144">Select the **Provisioning** tab.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/ProvisioningTab.png)

4. <span data-ttu-id="cde64-146">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="cde64-146">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/ProvisioningCredentials.png)

5. <span data-ttu-id="cde64-148">Under the **Admin Credentials** section, input the **Tenant URL**, and **Secret Token** of your Cisco Spark's account.</span><span class="sxs-lookup"><span data-stu-id="cde64-148">Under the **Admin Credentials** section, input the **Tenant URL**, and **Secret Token** of your Cisco Spark's account.</span></span>

    *   <span data-ttu-id="cde64-149">In the **Tenant URL** field, populate the Cisco Spark SCIM API URL for your tenant, which takes the form of `https://api.ciscospark.com/v1/scim/[Tenant ID]/`, where `[Tenant ID]` is an alphanumeric string as described in step 6.</span><span class="sxs-lookup"><span data-stu-id="cde64-149">In the **Tenant URL** field, populate the Cisco Spark SCIM API URL for your tenant, which takes the form of `https://api.ciscospark.com/v1/scim/[Tenant ID]/`, where `[Tenant ID]` is an alphanumeric string as described in step 6.</span></span>

    *   <span data-ttu-id="cde64-150">In the **Secret Token** field, populate the Secret Token as described in step 6.</span><span class="sxs-lookup"><span data-stu-id="cde64-150">In the **Secret Token** field, populate the Secret Token as described in step 6.</span></span>

1. <span data-ttu-id="cde64-151">The **Tenant ID** and **Secret Token** for your Cisco Spark account can be found by logging into the [Cisco Spark developer site](https://developer.webex.com/) with your Admin account.</span><span class="sxs-lookup"><span data-stu-id="cde64-151">The **Tenant ID** and **Secret Token** for your Cisco Spark account can be found by logging into the [Cisco Spark developer site](https://developer.webex.com/) with your Admin account.</span></span> <span data-ttu-id="cde64-152">Once logged in -</span><span class="sxs-lookup"><span data-stu-id="cde64-152">Once logged in -</span></span>
    * <span data-ttu-id="cde64-153">Go to the [Getting Started page](https://developer.webex.com/getting-started.html)</span><span class="sxs-lookup"><span data-stu-id="cde64-153">Go to the [Getting Started page](https://developer.webex.com/getting-started.html)</span></span>
    * <span data-ttu-id="cde64-154">Scroll down to the [Authentication Section](https://developer.webex.com/getting-started.html#authentication)
    ![Cisco Spark Authentication Token](./media/cisco-spark-provisioning-tutorial/SecretToken.png)</span><span class="sxs-lookup"><span data-stu-id="cde64-154">Scroll down to the [Authentication Section](https://developer.webex.com/getting-started.html#authentication)
![Cisco Spark Authentication Token](./media/cisco-spark-provisioning-tutorial/SecretToken.png)</span></span>
    * <span data-ttu-id="cde64-155">The alphanumeric string in the box is your **Secret Token**.</span><span class="sxs-lookup"><span data-stu-id="cde64-155">The alphanumeric string in the box is your **Secret Token**.</span></span> <span data-ttu-id="cde64-156">Copy this token to the clipboard</span><span class="sxs-lookup"><span data-stu-id="cde64-156">Copy this token to the clipboard</span></span>
    * <span data-ttu-id="cde64-157">Go to the [Get My Own Details page](https://developer.webex.com/endpoint-people-me-get.html)</span><span class="sxs-lookup"><span data-stu-id="cde64-157">Go to the [Get My Own Details page](https://developer.webex.com/endpoint-people-me-get.html)</span></span>
        * <span data-ttu-id="cde64-158">Make sure that Test Mode is ON</span><span class="sxs-lookup"><span data-stu-id="cde64-158">Make sure that Test Mode is ON</span></span>
        * <span data-ttu-id="cde64-159">Type the word "Bearer" followed by a space, and then paste the Secret Token into the Authorization field ![Cisco Spark Authentication Token](./media/cisco-spark-provisioning-tutorial/GetMyDetails.png)</span><span class="sxs-lookup"><span data-stu-id="cde64-159">Type the word "Bearer" followed by a space, and then paste the Secret Token into the Authorization field ![Cisco Spark Authentication Token](./media/cisco-spark-provisioning-tutorial/GetMyDetails.png)</span></span>
        * <span data-ttu-id="cde64-160">Click Run</span><span class="sxs-lookup"><span data-stu-id="cde64-160">Click Run</span></span>
    * <span data-ttu-id="cde64-161">In the response text to the right, the **Tenant ID** appears as "orgId":</span><span class="sxs-lookup"><span data-stu-id="cde64-161">In the response text to the right, the **Tenant ID** appears as "orgId":</span></span>

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

1. <span data-ttu-id="cde64-162">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="cde64-162">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Cisco Spark.</span></span> <span data-ttu-id="cde64-163">If the connection fails, ensure your Cisco Spark account has Admin permissions and try again.</span><span class="sxs-lookup"><span data-stu-id="cde64-163">If the connection fails, ensure your Cisco Spark account has Admin permissions and try again.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/TestConnection.png)

8. <span data-ttu-id="cde64-165">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox - **Send an email notification when a failure occurs**.</span><span class="sxs-lookup"><span data-stu-id="cde64-165">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox - **Send an email notification when a failure occurs**.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/EmailNotification.png)

9. <span data-ttu-id="cde64-167">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cde64-167">Click **Save**.</span></span>

10. <span data-ttu-id="cde64-168">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="cde64-168">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Cisco Spark**.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/UserMapping.png)

11. <span data-ttu-id="cde64-170">Review the user attributes that are synchronized from Azure AD to Cisco Spark in the **Attribute Mapping** section.</span><span class="sxs-lookup"><span data-stu-id="cde64-170">Review the user attributes that are synchronized from Azure AD to Cisco Spark in the **Attribute Mapping** section.</span></span> <span data-ttu-id="cde64-171">The attributes selected as **Matching** properties are used to match the user accounts in Cisco Spark for update operations.</span><span class="sxs-lookup"><span data-stu-id="cde64-171">The attributes selected as **Matching** properties are used to match the user accounts in Cisco Spark for update operations.</span></span> <span data-ttu-id="cde64-172">Select the **Save** button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="cde64-172">Select the **Save** button to commit any changes.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/UserMappingAttributes.png)

12. <span data-ttu-id="cde64-174">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="cde64-174">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span></span>

13. <span data-ttu-id="cde64-175">To enable the Azure AD provisioning service for Cisco Spark, change the **Provisioning Status** to **On** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="cde64-175">To enable the Azure AD provisioning service for Cisco Spark, change the **Provisioning Status** to **On** in the **Settings** section.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/ProvisioningStatus.png)

14. <span data-ttu-id="cde64-177">Define the users and/or groups that you would like to provision to Cisco Spark by choosing the desired values in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="cde64-177">Define the users and/or groups that you would like to provision to Cisco Spark by choosing the desired values in **Scope** in the **Settings** section.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/SyncScope.png)

15. <span data-ttu-id="cde64-179">When you are ready to provision, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cde64-179">When you are ready to provision, click **Save**.</span></span>

    ![Cisco Spark Provisioning](./media/cisco-spark-provisioning-tutorial/Save.png)


<span data-ttu-id="cde64-181">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="cde64-181">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span></span> <span data-ttu-id="cde64-182">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span><span class="sxs-lookup"><span data-stu-id="cde64-182">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="cde64-183">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="cde64-183">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Cisco Spark.</span></span>

<span data-ttu-id="cde64-184">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="cde64-184">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="connector-limitations"></a><span data-ttu-id="cde64-185">Connector Limitations</span><span class="sxs-lookup"><span data-stu-id="cde64-185">Connector Limitations</span></span>

* <span data-ttu-id="cde64-186">Cisco Spark is currently in Cisco's Early Field Testing (EFT) phase.</span><span class="sxs-lookup"><span data-stu-id="cde64-186">Cisco Spark is currently in Cisco's Early Field Testing (EFT) phase.</span></span> <span data-ttu-id="cde64-187">For more information, please contact [Cisco's support team](https://www.webex.co.in/support/support-overview.html).</span><span class="sxs-lookup"><span data-stu-id="cde64-187">For more information, please contact [Cisco's support team](https://www.webex.co.in/support/support-overview.html).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cde64-188">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cde64-188">Additional resources</span></span>

* [<span data-ttu-id="cde64-189">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="cde64-189">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="cde64-190">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cde64-190">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


## <a name="next-steps"></a><span data-ttu-id="cde64-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="cde64-191">Next steps</span></span>

* [<span data-ttu-id="cde64-192">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="cde64-192">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)

<!--Image references-->
[1]: ./media/cisco-spark-provisioning-tutorial/tutorial_general_01.png
[2]: ./media/cisco-spark-provisioning-tutorial/tutorial_general_02.png
[3]: ./media/cisco-spark-provisioning-tutorial/tutorial_general_03.png
