---
title: 'Tutorial: Configure Cerner Central for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision users to a roster in Cerner Central.
services: active-directory
documentationcenter: ''
author: asmalser-msft
writer: asmalser-msft
manager: mtillman
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: asmalser-msft
ms.openlocfilehash: bc215061d5f2f139c5912f29f709346cb681ee86
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867847"
---
# <a name="tutorial-configure-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="04109-103">Tutorial: Configure Cerner Central for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="04109-103">Tutorial: Configure Cerner Central for automatic user provisioning</span></span>

<span data-ttu-id="04109-104">The objective of this tutorial is to show you the steps you need to perform in Cerner Central and Azure AD to automatically provision and de-provision user accounts from Azure AD to a user roster in Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="04109-104">The objective of this tutorial is to show you the steps you need to perform in Cerner Central and Azure AD to automatically provision and de-provision user accounts from Azure AD to a user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="04109-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="04109-105">Prerequisites</span></span>

<span data-ttu-id="04109-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="04109-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="04109-107">An Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="04109-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="04109-108">A Cerner Central tenant</span><span class="sxs-lookup"><span data-stu-id="04109-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="04109-109">Azure Active Directory integrates with Cerner Central using the [SCIM](http://www.simplecloud.info/) protocol.</span><span class="sxs-lookup"><span data-stu-id="04109-109">Azure Active Directory integrates with Cerner Central using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-cerner-central"></a><span data-ttu-id="04109-110">Assigning users to Cerner Central</span><span class="sxs-lookup"><span data-stu-id="04109-110">Assigning users to Cerner Central</span></span>

<span data-ttu-id="04109-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="04109-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="04109-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="04109-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="04109-113">Before configuring and enabling the provisioning service, you should decide what users and/or groups in Azure AD represent the users who need access to Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="04109-113">Before configuring and enabling the provisioning service, you should decide what users and/or groups in Azure AD represent the users who need access to Cerner Central.</span></span> <span data-ttu-id="04109-114">Once decided, you can assign these users to Cerner Central by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="04109-114">Once decided, you can assign these users to Cerner Central by following the instructions here:</span></span>

[<span data-ttu-id="04109-115">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="04109-115">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-cerner-central"></a><span data-ttu-id="04109-116">Important tips for assigning users to Cerner Central</span><span class="sxs-lookup"><span data-stu-id="04109-116">Important tips for assigning users to Cerner Central</span></span>

*   <span data-ttu-id="04109-117">It is recommended that a single Azure AD user be assigned to Cerner Central to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="04109-117">It is recommended that a single Azure AD user be assigned to Cerner Central to test the provisioning configuration.</span></span> <span data-ttu-id="04109-118">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="04109-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="04109-119">Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster.</span><span class="sxs-lookup"><span data-stu-id="04109-119">Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster.</span></span>  <span data-ttu-id="04109-120">Other Cerner solutions leverage this list of users in the user roster.</span><span class="sxs-lookup"><span data-stu-id="04109-120">Other Cerner solutions leverage this list of users in the user roster.</span></span>

*   <span data-ttu-id="04109-121">When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="04109-121">When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="04109-122">Users with the "Default Access" role are excluded from provisioning.</span><span class="sxs-lookup"><span data-stu-id="04109-122">Users with the "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-to-cerner-central"></a><span data-ttu-id="04109-123">Configuring user provisioning to Cerner Central</span><span class="sxs-lookup"><span data-stu-id="04109-123">Configuring user provisioning to Cerner Central</span></span>

<span data-ttu-id="04109-124">This section guides you through connecting your Azure AD to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04109-124">This section guides you through connecting your Azure AD to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="04109-125">You may also choose to enabled SAML-based Single Sign-On for Cerner Central, following the instructions provided in [Azure portal (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="04109-125">You may also choose to enabled SAML-based Single Sign-On for Cerner Central, following the instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="04109-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span><span class="sxs-lookup"><span data-stu-id="04109-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="04109-127">For more information, see the [Cerner Central single sign-on tutorial](cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="04109-127">For more information, see the [Cerner Central single sign-on tutorial](cernercentral-tutorial.md).</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-cerner-central-in-azure-ad"></a><span data-ttu-id="04109-128">To configure automatic user account provisioning to Cerner Central in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="04109-128">To configure automatic user account provisioning to Cerner Central in Azure AD:</span></span>


<span data-ttu-id="04109-129">In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use to connect to Cerner's SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="04109-129">In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use to connect to Cerner's SCIM endpoint.</span></span> <span data-ttu-id="04109-130">It is also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.</span><span class="sxs-lookup"><span data-stu-id="04109-130">It is also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.</span></span>

1.  <span data-ttu-id="04109-131">The first step is to ensure the people managing the Cerner and Azure AD integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions.</span><span class="sxs-lookup"><span data-stu-id="04109-131">The first step is to ensure the people managing the Cerner and Azure AD integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions.</span></span> <span data-ttu-id="04109-132">If necessary, use the URLs below to create CernerCare accounts in each applicable environment.</span><span class="sxs-lookup"><span data-stu-id="04109-132">If necessary, use the URLs below to create CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="04109-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="04109-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="04109-134">Production:  https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="04109-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="04109-135">Next, a system account must be created for Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04109-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="04109-136">Use the instructions below to request a System Account for your sandbox and production environments.</span><span class="sxs-lookup"><span data-stu-id="04109-136">Use the instructions below to request a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="04109-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="04109-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="04109-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="04109-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="04109-139">Production:  https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="04109-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="04109-140">Next, generate an OAuth bearer token for each of your system accounts.</span><span class="sxs-lookup"><span data-stu-id="04109-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="04109-141">To do this, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="04109-141">To do this, follow the instructions below.</span></span>

   * <span data-ttu-id="04109-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="04109-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="04109-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="04109-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="04109-144">Production:  https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="04109-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="04109-145">Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration.</span><span class="sxs-lookup"><span data-stu-id="04109-145">Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration.</span></span> <span data-ttu-id="04109-146">For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="04109-146">For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="04109-147">Now you can configure Azure AD to provision user accounts to Cerner.</span><span class="sxs-lookup"><span data-stu-id="04109-147">Now you can configure Azure AD to provision user accounts to Cerner.</span></span> <span data-ttu-id="04109-148">Sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span><span class="sxs-lookup"><span data-stu-id="04109-148">Sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="04109-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field.</span><span class="sxs-lookup"><span data-stu-id="04109-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field.</span></span> <span data-ttu-id="04109-150">Otherwise, select **Add** and search for **Cerner Central** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="04109-150">Otherwise, select **Add** and search for **Cerner Central** in the application gallery.</span></span> <span data-ttu-id="04109-151">Select Cerner Central from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="04109-151">Select Cerner Central from the search results, and add it to your list of applications.</span></span>

7.  <span data-ttu-id="04109-152">Select your instance of Cerner Central, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="04109-152">Select your instance of Cerner Central, then select the **Provisioning** tab.</span></span>

8.  <span data-ttu-id="04109-153">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="04109-153">Set the **Provisioning Mode** to **Automatic**.</span></span>

   ![Cerner Central Provisioning](./media/cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="04109-155">Fill in the following fields under **Admin Credentials**:</span><span class="sxs-lookup"><span data-stu-id="04109-155">Fill in the following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="04109-156">In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.</span><span class="sxs-lookup"><span data-stu-id="04109-156">In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="04109-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="04109-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="04109-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="04109-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="04109-159">In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and click **Test Connection**.</span><span class="sxs-lookup"><span data-stu-id="04109-159">In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="04109-160">You should see a success notification on the upper­right side of your portal.</span><span class="sxs-lookup"><span data-stu-id="04109-160">You should see a success notification on the upper­right side of your portal.</span></span>

10. <span data-ttu-id="04109-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span><span class="sxs-lookup"><span data-stu-id="04109-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

11. <span data-ttu-id="04109-162">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="04109-162">Click **Save**.</span></span> 

12. <span data-ttu-id="04109-163">In the **Attribute Mappings** section, review the user and group attributes to be synchronized from Azure AD to Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="04109-163">In the **Attribute Mappings** section, review the user and group attributes to be synchronized from Azure AD to Cerner Central.</span></span> <span data-ttu-id="04109-164">The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations.</span><span class="sxs-lookup"><span data-stu-id="04109-164">The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="04109-165">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="04109-165">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="04109-166">To enable the Azure AD provisioning service for Cerner Central, change the **Provisioning Status** to **On** in the **Settings** section</span><span class="sxs-lookup"><span data-stu-id="04109-166">To enable the Azure AD provisioning service for Cerner Central, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

14. <span data-ttu-id="04109-167">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="04109-167">Click **Save**.</span></span> 

<span data-ttu-id="04109-168">This starts the initial synchronization of any users and/or groups assigned to Cerner Central in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="04109-168">This starts the initial synchronization of any users and/or groups assigned to Cerner Central in the Users and Groups section.</span></span> <span data-ttu-id="04109-169">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span><span class="sxs-lookup"><span data-stu-id="04109-169">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="04109-170">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Cerner Central app.</span><span class="sxs-lookup"><span data-stu-id="04109-170">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="04109-171">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="04109-171">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="04109-172">Additional resources</span><span class="sxs-lookup"><span data-stu-id="04109-172">Additional resources</span></span>

* [<span data-ttu-id="04109-173">Cerner Central: Publishing identity data using Azure AD</span><span class="sxs-lookup"><span data-stu-id="04109-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="04109-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04109-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](cernercentral-tutorial.md)
* [<span data-ttu-id="04109-175">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="04109-175">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="04109-176">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="04109-176">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a><span data-ttu-id="04109-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="04109-177">Next steps</span></span>
* <span data-ttu-id="04109-178">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="04109-178">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
