---
title: 'Tutorial: Configure Cornerstone OnDemand for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Cornerstone OnDemand.
services: active-directory
documentationcenter: ''
author: zhchia
writer: zhchia
manager: beatrizd
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2018
ms.author: v-ant
ms.openlocfilehash: 6a6cfb2cb1fd6b70be0437c8b6fa62f50e76e53b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868007"
---
# <a name="tutorial-configure-cornerstone-ondemand-for-automatic-user-provisioning"></a><span data-ttu-id="1fd50-103">Tutorial: Configure Cornerstone OnDemand for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="1fd50-103">Tutorial: Configure Cornerstone OnDemand for automatic user provisioning</span></span>


<span data-ttu-id="1fd50-104">The objective of this tutorial is to demonstrate the steps to be performed in Cornerstone OnDemand and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="1fd50-104">The objective of this tutorial is to demonstrate the steps to be performed in Cornerstone OnDemand and Azure Active Directory (Azure AD) to configure Azure AD to automatically provision and de-provision users and/or groups to Cornerstone OnDemand.</span></span>


> [!NOTE]
> <span data-ttu-id="1fd50-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="1fd50-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span></span> <span data-ttu-id="1fd50-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="1fd50-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fd50-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1fd50-107">Prerequisites</span></span>

<span data-ttu-id="1fd50-108">The scenario outlined in this tutorial assumes that you already have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="1fd50-108">The scenario outlined in this tutorial assumes that you already have the following prerequisites:</span></span>

*   <span data-ttu-id="1fd50-109">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="1fd50-109">An Azure AD tenant</span></span>
*   <span data-ttu-id="1fd50-110">A Cornerstone OnDemand tenant</span><span class="sxs-lookup"><span data-stu-id="1fd50-110">A Cornerstone OnDemand tenant</span></span>
*   <span data-ttu-id="1fd50-111">A user account in Cornerstone OnDemand with Admin permissions</span><span class="sxs-lookup"><span data-stu-id="1fd50-111">A user account in Cornerstone OnDemand with Admin permissions</span></span>


> [!NOTE]
> <span data-ttu-id="1fd50-112">The Azure AD provisioning integration relies on the [Cornerstone OnDemand Webservice](https://help.csod.com/help/csod_0/Content/Resources/Documents/WebServices/CSOD_-_Summary_of_Web_Services_v20151106.pdf), which is available to Cornerstone OnDemand teams.</span><span class="sxs-lookup"><span data-stu-id="1fd50-112">The Azure AD provisioning integration relies on the [Cornerstone OnDemand Webservice](https://help.csod.com/help/csod_0/Content/Resources/Documents/WebServices/CSOD_-_Summary_of_Web_Services_v20151106.pdf), which is available to Cornerstone OnDemand teams.</span></span>

## <a name="adding-cornerstone-ondemand-from-the-gallery"></a><span data-ttu-id="1fd50-113">Adding Cornerstone OnDemand from the gallery</span><span class="sxs-lookup"><span data-stu-id="1fd50-113">Adding Cornerstone OnDemand from the gallery</span></span>
<span data-ttu-id="1fd50-114">Before configuring Cornerstone OnDemand for automatic user provisioning with Azure AD, you need to add Cornerstone OnDemand from the Azure AD application gallery to your list of managed SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="1fd50-114">Before configuring Cornerstone OnDemand for automatic user provisioning with Azure AD, you need to add Cornerstone OnDemand from the Azure AD application gallery to your list of managed SaaS applications.</span></span>

<span data-ttu-id="1fd50-115">**To add Cornerstone OnDemand from the Azure AD application gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1fd50-115">**To add Cornerstone OnDemand from the Azure AD application gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1fd50-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1fd50-116">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click on the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="1fd50-118">Navigate to **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1fd50-118">Navigate to **Enterprise applications** > **All applications**.</span></span>

    ![The Enterprise applications Section][2]
    
3. <span data-ttu-id="1fd50-120">To add Cornerstone OnDemand, click the **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="1fd50-120">To add Cornerstone OnDemand, click the **New application** button on the top of the dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="1fd50-122">In the search box, type **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="1fd50-122">In the search box, type **Cornerstone OnDemand**.</span></span>

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/AppSearch.png)

5. <span data-ttu-id="1fd50-124">In the results panel, select **Cornerstone OnDemand**, and then click the **Add** button to add Cornerstone OnDemand to your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="1fd50-124">In the results panel, select **Cornerstone OnDemand**, and then click the **Add** button to add Cornerstone OnDemand to your list of SaaS applications.</span></span>

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/AppSearchResults.png)

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/AppCreation.png)

## <a name="assigning-users-to-cornerstone-ondemand"></a><span data-ttu-id="1fd50-127">Assigning users to Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="1fd50-127">Assigning users to Cornerstone OnDemand</span></span>

<span data-ttu-id="1fd50-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="1fd50-128">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="1fd50-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="1fd50-129">In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="1fd50-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="1fd50-130">Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Azure AD need access to Cornerstone OnDemand.</span></span> <span data-ttu-id="1fd50-131">Once decided, you can assign these users and/or groups to Cornerstone OnDemand by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="1fd50-131">Once decided, you can assign these users and/or groups to Cornerstone OnDemand by following the instructions here:</span></span>

*   [<span data-ttu-id="1fd50-132">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="1fd50-132">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-cornerstone-ondemand"></a><span data-ttu-id="1fd50-133">Important tips for assigning users to Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="1fd50-133">Important tips for assigning users to Cornerstone OnDemand</span></span>

*   <span data-ttu-id="1fd50-134">It is recommended that a single Azure AD user is assigned to Cornerstone OnDemand to test the automatic user provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="1fd50-134">It is recommended that a single Azure AD user is assigned to Cornerstone OnDemand to test the automatic user provisioning configuration.</span></span> <span data-ttu-id="1fd50-135">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="1fd50-135">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1fd50-136">When assigning a user to Cornerstone OnDemand, you must select any valid application-specific role (if available) in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="1fd50-136">When assigning a user to Cornerstone OnDemand, you must select any valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="1fd50-137">Users with the **Default Access** role are excluded from provisioning.</span><span class="sxs-lookup"><span data-stu-id="1fd50-137">Users with the **Default Access** role are excluded from provisioning.</span></span>

## <a name="configuring-automatic-user-provisioning-to-cornerstone-ondemand"></a><span data-ttu-id="1fd50-138">Configuring automatic user provisioning to Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="1fd50-138">Configuring automatic user provisioning to Cornerstone OnDemand</span></span>

<span data-ttu-id="1fd50-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in Cornerstone OnDemand based on user and/or group assignments in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fd50-139">This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users and/or groups in Cornerstone OnDemand based on user and/or group assignments in Azure AD.</span></span>


### <a name="to-configure-automatic-user-provisioning-for-cornerstone-ondemand-in-azure-ad"></a><span data-ttu-id="1fd50-140">To configure automatic user provisioning for Cornerstone OnDemand in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1fd50-140">To configure automatic user provisioning for Cornerstone OnDemand in Azure AD:</span></span>


1. <span data-ttu-id="1fd50-141">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span><span class="sxs-lookup"><span data-stu-id="1fd50-141">Sign in to the [Azure portal](https://portal.azure.com) and browse to **Azure Active Directory > Enterprise applications > All applications**.</span></span>

2. <span data-ttu-id="1fd50-142">Select Cornerstone OnDemand from your list of SaaS applications.</span><span class="sxs-lookup"><span data-stu-id="1fd50-142">Select Cornerstone OnDemand from your list of SaaS applications.</span></span>
 
    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/Successcenter2.png)

3. <span data-ttu-id="1fd50-144">Select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="1fd50-144">Select the **Provisioning** tab.</span></span>

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/ProvisioningTab.png)

4. <span data-ttu-id="1fd50-146">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="1fd50-146">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/ProvisioningCredentials.png)

5. <span data-ttu-id="1fd50-148">Under the **Admin Credentials** section, input the **Admin Username**, **Admin Password**, and **Domain** of your Cornerstone OnDemand's account.</span><span class="sxs-lookup"><span data-stu-id="1fd50-148">Under the **Admin Credentials** section, input the **Admin Username**, **Admin Password**, and **Domain** of your Cornerstone OnDemand's account.</span></span>

    *   <span data-ttu-id="1fd50-149">In the **Admin Username** field, populate the domain\username of the admin account on your Cornerstone OnDemand tenant.</span><span class="sxs-lookup"><span data-stu-id="1fd50-149">In the **Admin Username** field, populate the domain\username of the admin account on your Cornerstone OnDemand tenant.</span></span> <span data-ttu-id="1fd50-150">Example: contoso\admin.</span><span class="sxs-lookup"><span data-stu-id="1fd50-150">Example: contoso\admin.</span></span>

    *   <span data-ttu-id="1fd50-151">In the **Admin Password** field, populate the password corresponding to the admin username.</span><span class="sxs-lookup"><span data-stu-id="1fd50-151">In the **Admin Password** field, populate the password corresponding to the admin username.</span></span>

    *   <span data-ttu-id="1fd50-152">In the **Domain** field, populate the webservice URL of the Cornerstone OnDemand tenant.</span><span class="sxs-lookup"><span data-stu-id="1fd50-152">In the **Domain** field, populate the webservice URL of the Cornerstone OnDemand tenant.</span></span> <span data-ttu-id="1fd50-153">Example: The service is located at `https://ws-[corpname].csod.com/feed30/clientdataservice.asmx`, for Contoso the domain is `https://ws-contoso.csod.com/feed30/clientdataservice.asmx`.</span><span class="sxs-lookup"><span data-stu-id="1fd50-153">Example: The service is located at `https://ws-[corpname].csod.com/feed30/clientdataservice.asmx`, for Contoso the domain is `https://ws-contoso.csod.com/feed30/clientdataservice.asmx`.</span></span> <span data-ttu-id="1fd50-154">For more information on how to retrieve the webservice URL, see [here](https://help.csod.com/help/csod_0/Content/Resources/Documents/WebServices/CSOD_Web_Services_-_User-OU_Technical_Specification_v20160222.pdf).</span><span class="sxs-lookup"><span data-stu-id="1fd50-154">For more information on how to retrieve the webservice URL, see [here](https://help.csod.com/help/csod_0/Content/Resources/Documents/WebServices/CSOD_Web_Services_-_User-OU_Technical_Specification_v20160222.pdf).</span></span>

6. <span data-ttu-id="1fd50-155">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="1fd50-155">Upon populating the fields shown in Step 5, click **Test Connection** to ensure Azure AD can connect to Cornerstone OnDemand.</span></span> <span data-ttu-id="1fd50-156">If the connection fails, ensure your Cornerstone OnDemand account has Admin permissions and try again.</span><span class="sxs-lookup"><span data-stu-id="1fd50-156">If the connection fails, ensure your Cornerstone OnDemand account has Admin permissions and try again.</span></span>

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/TestConnection.png)

7. <span data-ttu-id="1fd50-158">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox - **Send an email notification when a failure occurs**.</span><span class="sxs-lookup"><span data-stu-id="1fd50-158">In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and check the checkbox - **Send an email notification when a failure occurs**.</span></span>

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/EmailNotification.png)

8. <span data-ttu-id="1fd50-160">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1fd50-160">Click **Save**.</span></span>

9. <span data-ttu-id="1fd50-161">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="1fd50-161">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Cornerstone OnDemand**.</span></span>

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/UserMapping.png)

10. <span data-ttu-id="1fd50-163">Review the user attributes that are synchronized from Azure AD to Cornerstone OnDemand in the **Attribute Mapping** section.</span><span class="sxs-lookup"><span data-stu-id="1fd50-163">Review the user attributes that are synchronized from Azure AD to Cornerstone OnDemand in the **Attribute Mapping** section.</span></span> <span data-ttu-id="1fd50-164">The attributes selected as **Matching** properties are used to match the user accounts in Cornerstone OnDemand for update operations.</span><span class="sxs-lookup"><span data-stu-id="1fd50-164">The attributes selected as **Matching** properties are used to match the user accounts in Cornerstone OnDemand for update operations.</span></span> <span data-ttu-id="1fd50-165">Select the **Save** button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="1fd50-165">Select the **Save** button to commit any changes.</span></span>

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/UserMappingAttributes.png)

11. <span data-ttu-id="1fd50-167">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="1fd50-167">To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).</span></span>

12. <span data-ttu-id="1fd50-168">To enable the Azure AD provisioning service for Cornerstone OnDemand, change the **Provisioning Status** to **On** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="1fd50-168">To enable the Azure AD provisioning service for Cornerstone OnDemand, change the **Provisioning Status** to **On** in the **Settings** section.</span></span>

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/ProvisioningStatus.png)

13. <span data-ttu-id="1fd50-170">Define the users and/or groups that you would like to provision to Cornerstone OnDemand by choosing the desired values in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="1fd50-170">Define the users and/or groups that you would like to provision to Cornerstone OnDemand by choosing the desired values in **Scope** in the **Settings** section.</span></span>

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/SyncScope.png)

14. <span data-ttu-id="1fd50-172">When you are ready to provision, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1fd50-172">When you are ready to provision, click **Save**.</span></span>

    ![Cornerstone OnDemand Provisioning](./media/cornerstone-ondemand-provisioning-tutorial/Save.png)


<span data-ttu-id="1fd50-174">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="1fd50-174">This operation starts the initial synchronization of all users and/or groups defined in **Scope** in the **Settings** section.</span></span> <span data-ttu-id="1fd50-175">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span><span class="sxs-lookup"><span data-stu-id="1fd50-175">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="1fd50-176">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="1fd50-176">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Azure AD provisioning service on Cornerstone OnDemand.</span></span>

<span data-ttu-id="1fd50-177">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="1fd50-177">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>
## <a name="connector-limitations"></a><span data-ttu-id="1fd50-178">Connector Limitations</span><span class="sxs-lookup"><span data-stu-id="1fd50-178">Connector Limitations</span></span>

* <span data-ttu-id="1fd50-179">The Cornerstone OnDemand **Position** attribute expects a value that corresponds to the roles on the Cornerstone OnDemand portal.</span><span class="sxs-lookup"><span data-stu-id="1fd50-179">The Cornerstone OnDemand **Position** attribute expects a value that corresponds to the roles on the Cornerstone OnDemand portal.</span></span> <span data-ttu-id="1fd50-180">The list of valid **Position** values can be obtained by navigating to **Edit User Record > Organization Structure > Position** in the Cornerstone OnDemand portal.</span><span class="sxs-lookup"><span data-stu-id="1fd50-180">The list of valid **Position** values can be obtained by navigating to **Edit User Record > Organization Structure > Position** in the Cornerstone OnDemand portal.</span></span>
    <span data-ttu-id="1fd50-181">![Cornerstone OnDemand Provisioning Edit User](./media/cornerstone-ondemand-provisioning-tutorial/UserEdit.png) ![Cornerstone OnDemand Provisioning Position](./media/cornerstone-ondemand-provisioning-tutorial/UserPosition.png) ![Cornerstone OnDemand Provisioning Positions List](./media/cornerstone-ondemand-provisioning-tutorial/PostionId.png)</span><span class="sxs-lookup"><span data-stu-id="1fd50-181">![Cornerstone OnDemand Provisioning Edit User](./media/cornerstone-ondemand-provisioning-tutorial/UserEdit.png) ![Cornerstone OnDemand Provisioning Position](./media/cornerstone-ondemand-provisioning-tutorial/UserPosition.png) ![Cornerstone OnDemand Provisioning Positions List](./media/cornerstone-ondemand-provisioning-tutorial/PostionId.png)</span></span>
    
## <a name="additional-resources"></a><span data-ttu-id="1fd50-182">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1fd50-182">Additional resources</span></span>

* [<span data-ttu-id="1fd50-183">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="1fd50-183">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="1fd50-184">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1fd50-184">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



## <a name="next-steps"></a><span data-ttu-id="1fd50-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="1fd50-185">Next steps</span></span>

* [<span data-ttu-id="1fd50-186">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="1fd50-186">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)

<!--Image references-->
[1]: ./media/cornerstone-ondemand-provisioning-tutorial/tutorial_general_01.png
[2]: ./media/cornerstone-ondemand-provisioning-tutorial/tutorial_general_02.png
[3]: ./media/cornerstone-ondemand-provisioning-tutorial/tutorial_general_03.png
