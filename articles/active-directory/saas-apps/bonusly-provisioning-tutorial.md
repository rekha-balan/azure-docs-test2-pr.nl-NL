---
title: 'Tutorial: Configure Bonusly for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Bonusly.
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
ms.date: 06/27/2018
ms.author: v-wingf-msft
ms.openlocfilehash: 9d9ad137ed8b42c388fdb2dac63846e27f884d56
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965701"
---
# <a name="tutorial-configure-bonusly-for-automatic-user-provisioning"></a><span data-ttu-id="9bb24-103">Tutorial: Configure Bonusly for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="9bb24-103">Tutorial: Configure Bonusly for automatic user provisioning</span></span>

<span data-ttu-id="9bb24-104">The objective of this tutorial is to demonstrate the steps to be performed in Bonusly and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to Bonusly.</span><span class="sxs-lookup"><span data-stu-id="9bb24-104">The objective of this tutorial is to demonstrate the steps to be performed in Bonusly and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to Bonusly.</span></span>

> [!NOTE]
> <span data-ttu-id="9bb24-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="9bb24-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span></span> <span data-ttu-id="9bb24-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="9bb24-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bb24-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9bb24-107">Prerequisites</span></span>

<span data-ttu-id="9bb24-108">The scenario outlined in this tutorial assumes that you already have the following:</span><span class="sxs-lookup"><span data-stu-id="9bb24-108">The scenario outlined in this tutorial assumes that you already have the following:</span></span>

*   <span data-ttu-id="9bb24-109">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="9bb24-109">An Azure AD tenant</span></span>
*   <span data-ttu-id="9bb24-110">A [Bonusly tenant](https://bonus.ly/pricing)</span><span class="sxs-lookup"><span data-stu-id="9bb24-110">A [Bonusly tenant](https://bonus.ly/pricing)</span></span>
*   <span data-ttu-id="9bb24-111">A user account in Bonusly with Admin permissions</span><span class="sxs-lookup"><span data-stu-id="9bb24-111">A user account in Bonusly with Admin permissions</span></span>

> [!NOTE]
> <span data-ttu-id="9bb24-112">The Azure AD provisioning integration relies on the [Bonusly Rest API](https://bonusly.gelato.io/reference), which is available to Bonusly developers.</span><span class="sxs-lookup"><span data-stu-id="9bb24-112">The Azure AD provisioning integration relies on the [Bonusly Rest API](https://bonusly.gelato.io/reference), which is available to Bonusly developers.</span></span>

## <a name="adding-bonusly-from-the-gallery"></a><span data-ttu-id="9bb24-113">Adding Bonusly from the gallery</span><span class="sxs-lookup"><span data-stu-id="9bb24-113">Adding Bonusly from the gallery</span></span>
<span data-ttu-id="9bb24-114">Before configuring Bonusly for automatic user provisioning with Azure AD, you need to add Bonusly from the Azure AD application gallery to your list of managed SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="9bb24-114">Before configuring Bonusly for automatic user provisioning with Azure AD, you need to add Bonusly from the Azure AD application gallery to your list of managed SaaS applications.</span></span>

<span data-ttu-id="9bb24-115">**To add Bonusly from the Azure AD application gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9bb24-115">**To add Bonusly from the Azure AD application gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9bb24-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9bb24-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="9bb24-118">Navigate to **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9bb24-118">Navigate to **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications Section][2]
    
3. <span data-ttu-id="9bb24-120">To add Bonusly, click the **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="9bb24-120">To add Bonusly, click the **New application** button on the top of the dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="9bb24-122">In the search box, type **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="9bb24-122">In the search box, type **Bonusly**.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/AppSearch.png)

5. <span data-ttu-id="9bb24-124">In the results panel, select **Bonusly**, and then click the **Add** button to add Bonusly to your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="9bb24-124">In the results panel, select **Bonusly**, and then click the **Add** button to add Bonusly to your list of SaaS applications.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/AppSearchResults.png)

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/AppCreation.png)

## <a name="assigning-users-to-bonusly"></a><span data-ttu-id="9bb24-127">Assigning users to Bonusly</span><span class="sxs-lookup"><span data-stu-id="9bb24-127">Assigning users to Bonusly</span></span>

<span data-ttu-id="9bb24-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="9bb24-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="9bb24-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="9bb24-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="9bb24-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to Bonusly.</span><span class="sxs-lookup"><span data-stu-id="9bb24-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to Bonusly.</span></span> <span data-ttu-id="9bb24-131">Once decided, you can assign these users and/or groups to Bonusly by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="9bb24-131">Once decided, you can assign these users and/or groups to Bonusly by following the instructions here:</span></span>

*   [<span data-ttu-id="9bb24-132">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="9bb24-132">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-bonusly"></a><span data-ttu-id="9bb24-133">Important tips for assigning users to Bonusly</span><span class="sxs-lookup"><span data-stu-id="9bb24-133">Important tips for assigning users to Bonusly</span></span>

*   <span data-ttu-id="9bb24-134">It is recommended that a single Azure AD user is assigned to Bonusly to test the automatic user provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="9bb24-134">It is recommended that a single Azure AD user is assigned to Bonusly to test the automatic user provisioning configuration.</span></span> <span data-ttu-id="9bb24-135">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="9bb24-135">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="9bb24-136">When assigning a user to Bonusly, you must select any valid application-specific role (if available) in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="9bb24-136">When assigning a user to Bonusly, you must select any valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="9bb24-137">Users with the **Default Access** role are excluded from provisioning.</span><span class="sxs-lookup"><span data-stu-id="9bb24-137">Users with the **Default Access** role are excluded from provisioning.</span></span>

## <a name="configuring-automatic-user-provisioning-to-bonusly"></a><span data-ttu-id="9bb24-138">Configuring automatic user provisioning to Bonusly</span><span class="sxs-lookup"><span data-stu-id="9bb24-138">Configuring automatic user provisioning to Bonusly</span></span>

<span data-ttu-id="9bb24-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in Bonusly based on user and/or group assignments in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bb24-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in Bonusly based on user and/or group assignments in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="9bb24-140">You may also choose to enable SAML-based single sign-on for Bonusly, following the instructions provided in the [Bonusly single sign-on tutorial](bonus-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="9bb24-140">You may also choose to enable SAML-based single sign-on for Bonusly, following the instructions provided in the [Bonusly single sign-on tutorial](bonus-tutorial.md).</span></span> <span data-ttu-id="9bb24-141">Single sign-on can be configured independently of automatic user provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="9bb24-141">Single sign-on can be configured independently of automatic user provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-provisioning-for-bonusly-in-azure-ad"></a><span data-ttu-id="9bb24-142">To configure automatic user provisioning for Bonusly in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9bb24-142">To configure automatic user provisioning for Bonusly in Azure AD:</span></span>

1. <span data-ttu-id="9bb24-143">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span><span class="sxs-lookup"><span data-stu-id="9bb24-143">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span></span>

2. <span data-ttu-id="9bb24-144">Select Bonusly from your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="9bb24-144">Select Bonusly from your list of SaaS applications.</span></span>
 
    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/AppInstanceSearch.png)

3. <span data-ttu-id="9bb24-146">Select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="9bb24-146">Select the **Provisioning** tab.</span></span>
    
    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/ProvisioningTab.png)

4. <span data-ttu-id="9bb24-148">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="9bb24-148">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/ProvisioningCredentials.png)

5. <span data-ttu-id="9bb24-150">Under the **Admin Credentials** section, input the **Secret Token** of your Bonusly account as described in Step 6.</span><span class="sxs-lookup"><span data-stu-id="9bb24-150">Under the **Admin Credentials** section, input the **Secret Token** of your Bonusly account as described in Step 6.</span></span>

6. <span data-ttu-id="9bb24-151">The **Secret Token** for your Bonusly account is located in **Admin > Company > Integrations**.</span><span class="sxs-lookup"><span data-stu-id="9bb24-151">The **Secret Token** for your Bonusly account is located in **Admin > Company > Integrations**.</span></span> <span data-ttu-id="9bb24-152">In the **If you want to code** section, click on **API > Create New API Access Token** to create a new Secret Token.</span><span class="sxs-lookup"><span data-stu-id="9bb24-152">In the **If you want to code** section, click on **API > Create New API Access Token** to create a new Secret Token.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/BonuslyIntegrations.png)

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/BonsulyRestApi.png)

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/CreateToken.png)

7. <span data-ttu-id="9bb24-156">On the following screen, type a name for the access token in the provided text box, then press **Create Api Key**.</span><span class="sxs-lookup"><span data-stu-id="9bb24-156">On the following screen, type a name for the access token in the provided text box, then press **Create Api Key**.</span></span> <span data-ttu-id="9bb24-157">The new access token will appear for a few seconds in a pop-up.</span><span class="sxs-lookup"><span data-stu-id="9bb24-157">The new access token will appear for a few seconds in a pop-up.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/Token01.png)

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/Token02.png)

8. <span data-ttu-id="9bb24-160">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Bonusly.</span><span class="sxs-lookup"><span data-stu-id="9bb24-160">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Bonusly.</span></span> <span data-ttu-id="9bb24-161">If the connection fails, ensure your Bonusly account has Admin permissions and try again.</span><span class="sxs-lookup"><span data-stu-id="9bb24-161">If the connection fails, ensure your Bonusly account has Admin permissions and try again.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/TestConnection.png)
    
9. <span data-ttu-id="9bb24-163">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox **Send an email notification when a failure occurs**.</span><span class="sxs-lookup"><span data-stu-id="9bb24-163">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox **Send an email notification when a failure occurs**.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/EmailNotification.png)

10. <span data-ttu-id="9bb24-165">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9bb24-165">Click **Save**.</span></span>

11. <span data-ttu-id="9bb24-166">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="9bb24-166">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Bonusly**.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/UserMappings.png)

12. <span data-ttu-id="9bb24-168">Review the user attributes that are synchronized from Azure AD to Bonusly in the **Attribute Mapping** section.</span><span class="sxs-lookup"><span data-stu-id="9bb24-168">Review the user attributes that are synchronized from Azure AD to Bonusly in the **Attribute Mapping** section.</span></span> <span data-ttu-id="9bb24-169">The attributes selected as **Matching** properties are used to match the user accounts in Bonusly for update operations.</span><span class="sxs-lookup"><span data-stu-id="9bb24-169">The attributes selected as **Matching** properties are used to match the user accounts in Bonusly for update operations.</span></span> <span data-ttu-id="9bb24-170">Select the **Save** button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="9bb24-170">Select the **Save** button to commit any changes.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/UserAttributeMapping.png)

13. <span data-ttu-id="9bb24-172">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="9bb24-172">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span></span>

14. <span data-ttu-id="9bb24-173">To enable the Azure AD provisioning service for Bonusly, change the **Provisioning Status** to **On** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="9bb24-173">To enable the Azure AD provisioning service for Bonusly, change the **Provisioning Status** to **On** in the **Settings** section.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/ProvisioningStatus.png)

15. <span data-ttu-id="9bb24-175">Define the users and/or groups that you would like to provision to Bonusly by choosing the desired values in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="9bb24-175">Define the users and/or groups that you would like to provision to Bonusly by choosing the desired values in **Scope** in the **Settings** section.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/ScopeSync.png)

16. <span data-ttu-id="9bb24-177">When you are ready to provision, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9bb24-177">When you are ready to provision, click **Save**.</span></span>

    ![Bonusly Provisioning](./media/bonusly-provisioning-tutorial/SaveProvisioning.png)


<span data-ttu-id="9bb24-179">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="9bb24-179">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span></span> <span data-ttu-id="9bb24-180">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span><span class="sxs-lookup"><span data-stu-id="9bb24-180">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="9bb24-181">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Bonusly.</span><span class="sxs-lookup"><span data-stu-id="9bb24-181">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Bonusly.</span></span>

<span data-ttu-id="9bb24-182">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="9bb24-182">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9bb24-183">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9bb24-183">Additional resources</span></span>

* [<span data-ttu-id="9bb24-184">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="9bb24-184">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="9bb24-185">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9bb24-185">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


## <a name="next-steps"></a><span data-ttu-id="9bb24-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="9bb24-186">Next steps</span></span>

* [<span data-ttu-id="9bb24-187">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="9bb24-187">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)

<!--Image references-->
[1]: ./media/bonusly-provisioning-tutorial/tutorial_general_01.png
[2]: ./media/bonusly-provisioning-tutorial/tutorial_general_02.png
[3]: ./media/bonusly-provisioning-tutorial/tutorial_general_03.png
