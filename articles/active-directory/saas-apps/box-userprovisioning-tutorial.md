---
title: 'Tutorial: Configure Box for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Box .
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: jeedes
ms.openlocfilehash: f7fa4c9b0926d796c0c12b39d0056fe72e4028c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869673"
---
# <a name="tutorial-configure-box-for-automatic-user-provisioning"></a><span data-ttu-id="0bf5b-103">Tutorial: Configure Box for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="0bf5b-103">Tutorial: Configure Box for automatic user provisioning</span></span>

<span data-ttu-id="0bf5b-104">The objective of this tutorial is to show the steps you need to perform in Box and Azure AD to automatically provision and de-provision user accounts from Azure AD to Box.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-104">The objective of this tutorial is to show the steps you need to perform in Box and Azure AD to automatically provision and de-provision user accounts from Azure AD to Box.</span></span>

> [!NOTE]
> <span data-ttu-id="0bf5b-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span></span> <span data-ttu-id="0bf5b-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="0bf5b-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bf5b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0bf5b-107">Prerequisites</span></span>

<span data-ttu-id="0bf5b-108">To configure Azure AD integration with Box, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0bf5b-108">To configure Azure AD integration with Box, you need the following items:</span></span>

- <span data-ttu-id="0bf5b-109">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="0bf5b-109">An Azure AD tenant</span></span>
- <span data-ttu-id="0bf5b-110">A Box Business plan or better</span><span class="sxs-lookup"><span data-stu-id="0bf5b-110">A Box Business plan or better</span></span>

> [!NOTE]
> <span data-ttu-id="0bf5b-111">When you test the steps in this tutorial, we recommend that you do *not* use a production environment.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-111">When you test the steps in this tutorial, we recommend that you do *not* use a production environment.</span></span>

<span data-ttu-id="0bf5b-112">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0bf5b-112">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="0bf5b-113">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-113">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0bf5b-114">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0bf5b-114">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-box"></a><span data-ttu-id="0bf5b-115">Assigning users to Box</span><span class="sxs-lookup"><span data-stu-id="0bf5b-115">Assigning users to Box</span></span> 

<span data-ttu-id="0bf5b-116">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-116">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="0bf5b-117">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-117">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="0bf5b-118">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Box app.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-118">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Box app.</span></span> <span data-ttu-id="0bf5b-119">Once decided, you can assign these users to your Box app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="0bf5b-119">Once decided, you can assign these users to your Box app by following the instructions here:</span></span>

[<span data-ttu-id="0bf5b-120">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="0bf5b-120">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a><span data-ttu-id="0bf5b-121">Assign users and groups</span><span class="sxs-lookup"><span data-stu-id="0bf5b-121">Assign users and groups</span></span>
<span data-ttu-id="0bf5b-122">The **Box > Users and Groups** tab in the Azure portal allows you to specify which users and groups should be granted access to Box.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-122">The **Box > Users and Groups** tab in the Azure portal allows you to specify which users and groups should be granted access to Box.</span></span> <span data-ttu-id="0bf5b-123">Assignment of a user or group causes the following things to occur:</span><span class="sxs-lookup"><span data-stu-id="0bf5b-123">Assignment of a user or group causes the following things to occur:</span></span>

* <span data-ttu-id="0bf5b-124">Azure AD permits the assigned user (either by direct assignment or group membership) to authenticate to Box.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-124">Azure AD permits the assigned user (either by direct assignment or group membership) to authenticate to Box.</span></span> <span data-ttu-id="0bf5b-125">If a user is not assigned, then Azure AD does not permit them to sign in to Box and returns an error on the Azure AD sign-in page.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-125">If a user is not assigned, then Azure AD does not permit them to sign in to Box and returns an error on the Azure AD sign-in page.</span></span>
* <span data-ttu-id="0bf5b-126">An app tile for Box is added to the user's [application launcher](../manage-apps/what-is-single-sign-on.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="0bf5b-126">An app tile for Box is added to the user's [application launcher](../manage-apps/what-is-single-sign-on.md#deploying-azure-ad-integrated-applications-to-users).</span></span>
* <span data-ttu-id="0bf5b-127">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-127">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
  
  * <span data-ttu-id="0bf5b-128">If only user objects were configured to be provisioned, then all directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-128">If only user objects were configured to be provisioned, then all directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
  * <span data-ttu-id="0bf5b-129">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-129">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="0bf5b-130">The group and user memberships are preserved upon being written to Box.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-130">The group and user memberships are preserved upon being written to Box.</span></span>

<span data-ttu-id="0bf5b-131">You can use the **Attributes > Single Sign-On** tab to configure which user attributes (or claims) are presented to Box during SAML-based authentication, and the **Attributes > Provisioning** tab to configure how user and group attributes flow from Azure AD to Box during provisioning operations.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-131">You can use the **Attributes > Single Sign-On** tab to configure which user attributes (or claims) are presented to Box during SAML-based authentication, and the **Attributes > Provisioning** tab to configure how user and group attributes flow from Azure AD to Box during provisioning operations.</span></span>

### <a name="important-tips-for-assigning-users-to-box"></a><span data-ttu-id="0bf5b-132">Important tips for assigning users to Box</span><span class="sxs-lookup"><span data-stu-id="0bf5b-132">Important tips for assigning users to Box</span></span> 

*   <span data-ttu-id="0bf5b-133">It is recommended that a single Azure AD user assigned to Box to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-133">It is recommended that a single Azure AD user assigned to Box to test the provisioning configuration.</span></span> <span data-ttu-id="0bf5b-134">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-134">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="0bf5b-135">When assigning a user to box, you must select a valid user role.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-135">When assigning a user to box, you must select a valid user role.</span></span> <span data-ttu-id="0bf5b-136">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-136">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="0bf5b-137">Enable Automated User Provisioning</span><span class="sxs-lookup"><span data-stu-id="0bf5b-137">Enable Automated User Provisioning</span></span>

<span data-ttu-id="0bf5b-138">This section guides through connecting your Azure AD to Box's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Box based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-138">This section guides through connecting your Azure AD to Box's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Box based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="0bf5b-139">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-139">If automatic provisioning is enabled, then the assigned users and/or groups are added to the provisioning queue to be automatically provisioned.</span></span>
    
 * <span data-ttu-id="0bf5b-140">If only user objects are configured to be provisioned, then directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-140">If only user objects are configured to be provisioned, then directly assigned users are placed in the provisioning queue, and all users that are members of any assigned groups are placed in the provisioning queue.</span></span> 
    
 * <span data-ttu-id="0bf5b-141">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-141">If group objects were configured to be provisioned, then all assigned group objects are provisioned to Box, and all users that are members of those groups.</span></span> <span data-ttu-id="0bf5b-142">The group and user memberships are preserved upon being written to Box.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-142">The group and user memberships are preserved upon being written to Box.</span></span>

> [!TIP] 
> <span data-ttu-id="0bf5b-143">You may also choose to enabled SAML-based Single Sign-On for Box, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0bf5b-143">You may also choose to enabled SAML-based Single Sign-On for Box, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0bf5b-144">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-144">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="0bf5b-145">To configure automatic user account provisioning:</span><span class="sxs-lookup"><span data-stu-id="0bf5b-145">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="0bf5b-146">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Box.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-146">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Box.</span></span>

1. <span data-ttu-id="0bf5b-147">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-147">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="0bf5b-148">If you have already configured Box for single sign-on, search for your instance of Box using the search field.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-148">If you have already configured Box for single sign-on, search for your instance of Box using the search field.</span></span> <span data-ttu-id="0bf5b-149">Otherwise, select **Add** and search for **Box** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-149">Otherwise, select **Add** and search for **Box** in the application gallery.</span></span> <span data-ttu-id="0bf5b-150">Select Box from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-150">Select Box from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="0bf5b-151">Select your instance of Box, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-151">Select your instance of Box, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="0bf5b-152">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-152">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisioning](./media/box-userprovisioning-tutorial/provisioning.png)

5. <span data-ttu-id="0bf5b-154">Under the **Admin Credentials** section, click **Authorize** to open a Box login dialog in a new browser window.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-154">Under the **Admin Credentials** section, click **Authorize** to open a Box login dialog in a new browser window.</span></span>

6. <span data-ttu-id="0bf5b-155">On the **Login to grant access to Box** page, provide the required credentials, and then click **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-155">On the **Login to grant access to Box** page, provide the required credentials, and then click **Authorize**.</span></span> 
   
    <span data-ttu-id="0bf5b-156">![Enable automatic user provisioning](./media/box-userprovisioning-tutorial/IC769546.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="0bf5b-156">![Enable automatic user provisioning](./media/box-userprovisioning-tutorial/IC769546.png "Enable automatic user provisioning")</span></span>

7. <span data-ttu-id="0bf5b-157">Click **Grant access to Box** to authorize this operation and to return to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-157">Click **Grant access to Box** to authorize this operation and to return to the Azure portal.</span></span> 
   
    <span data-ttu-id="0bf5b-158">![Enable automatic user provisioning](./media/box-userprovisioning-tutorial/IC769549.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="0bf5b-158">![Enable automatic user provisioning](./media/box-userprovisioning-tutorial/IC769549.png "Enable automatic user provisioning")</span></span>

8. <span data-ttu-id="0bf5b-159">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Box app.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-159">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Box app.</span></span> <span data-ttu-id="0bf5b-160">If the connection fails, ensure your Box account has Team Admin permissions and try the **"Authorize"** step again.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-160">If the connection fails, ensure your Box account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="0bf5b-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="0bf5b-162">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="0bf5b-162">Click **Save.**</span></span>

11. <span data-ttu-id="0bf5b-163">Under the Mappings section, select **Synchronize Azure Active Directory Users to Box.**</span><span class="sxs-lookup"><span data-stu-id="0bf5b-163">Under the Mappings section, select **Synchronize Azure Active Directory Users to Box.**</span></span>

12. <span data-ttu-id="0bf5b-164">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Box.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-164">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Box.</span></span> <span data-ttu-id="0bf5b-165">The attributes selected as **Matching** properties are used to match the user accounts in Box for update operations.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-165">The attributes selected as **Matching** properties are used to match the user accounts in Box for update operations.</span></span> <span data-ttu-id="0bf5b-166">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-166">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="0bf5b-167">To enable the Azure AD provisioning service for Box, change the **Provisioning Status** to **On** in the Settings section</span><span class="sxs-lookup"><span data-stu-id="0bf5b-167">To enable the Azure AD provisioning service for Box, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="0bf5b-168">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="0bf5b-168">Click **Save.**</span></span>

<span data-ttu-id="0bf5b-169">That starts the initial synchronization of any users and/or groups assigned to Box in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-169">That starts the initial synchronization of any users and/or groups assigned to Box in the Users and Groups section.</span></span> <span data-ttu-id="0bf5b-170">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-170">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="0bf5b-171">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Box app.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-171">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Box app.</span></span>

<span data-ttu-id="0bf5b-172">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="0bf5b-172">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

<span data-ttu-id="0bf5b-173">In your Box tenant, synchronized users are listed under **Managed Users** in the **Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="0bf5b-173">In your Box tenant, synchronized users are listed under **Managed Users** in the **Admin Console**.</span></span>

<span data-ttu-id="0bf5b-174">![Integration status](./media/box-userprovisioning-tutorial/IC769556.png "Integration status")</span><span class="sxs-lookup"><span data-stu-id="0bf5b-174">![Integration status](./media/box-userprovisioning-tutorial/IC769556.png "Integration status")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0bf5b-175">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0bf5b-175">Additional resources</span></span>

* [<span data-ttu-id="0bf5b-176">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="0bf5b-176">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="0bf5b-177">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0bf5b-177">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="0bf5b-178">Configure Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="0bf5b-178">Configure Single Sign-on</span></span>](box-tutorial.md)
