---
title: 'Tutorial: Configure LinkedIn Elevate for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to LinkedIn Elevate.
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
ms.date: 01/28/2018
ms.author: asmalser-msft
ms.openlocfilehash: 1dcc198c1a1cc798e991f489e6897d4b930c0593
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969135"
---
# <a name="tutorial-configure-linkedin-elevate-for-automatic-user-provisioning"></a><span data-ttu-id="ad6d3-103">Tutorial: Configure LinkedIn Elevate for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="ad6d3-103">Tutorial: Configure LinkedIn Elevate for automatic user provisioning</span></span>


<span data-ttu-id="ad6d3-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Elevate and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Elevate and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Elevate.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ad6d3-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ad6d3-105">Prerequisites</span></span>

<span data-ttu-id="ad6d3-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="ad6d3-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="ad6d3-107">An Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="ad6d3-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="ad6d3-108">A LinkedIn Elevate tenant</span><span class="sxs-lookup"><span data-stu-id="ad6d3-108">A LinkedIn Elevate tenant</span></span> 
*   <span data-ttu-id="ad6d3-109">An administrator account in LinkedIn Elevate with access to the LinkedIn Account Center</span><span class="sxs-lookup"><span data-stu-id="ad6d3-109">An administrator account in LinkedIn Elevate with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="ad6d3-110">Azure Active Directory integrates with LinkedIn Elevate using the [SCIM](http://www.simplecloud.info/) protocol.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-110">Azure Active Directory integrates with LinkedIn Elevate using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-elevate"></a><span data-ttu-id="ad6d3-111">Assigning users to LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="ad6d3-111">Assigning users to LinkedIn Elevate</span></span>

<span data-ttu-id="ad6d3-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="ad6d3-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="ad6d3-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Elevate.</span></span> <span data-ttu-id="ad6d3-115">Once decided, you can assign these users to LinkedIn Elevate by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="ad6d3-115">Once decided, you can assign these users to LinkedIn Elevate by following the instructions here:</span></span>

[<span data-ttu-id="ad6d3-116">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="ad6d3-116">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-elevate"></a><span data-ttu-id="ad6d3-117">Important tips for assigning users to LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="ad6d3-117">Important tips for assigning users to LinkedIn Elevate</span></span>

*   <span data-ttu-id="ad6d3-118">It is recommended that a single Azure AD user be assigned to LinkedIn Elevate to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-118">It is recommended that a single Azure AD user be assigned to LinkedIn Elevate to test the provisioning configuration.</span></span> <span data-ttu-id="ad6d3-119">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ad6d3-120">When assigning a user to LinkedIn Elevate, you must select the **User** role in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-120">When assigning a user to LinkedIn Elevate, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="ad6d3-121">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-elevate"></a><span data-ttu-id="ad6d3-122">Configuring user provisioning to LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="ad6d3-122">Configuring user provisioning to LinkedIn Elevate</span></span>

<span data-ttu-id="ad6d3-123">This section guides you through connecting your Azure AD to LinkedIn Elevate's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Elevate based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-123">This section guides you through connecting your Azure AD to LinkedIn Elevate's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Elevate based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="ad6d3-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for LinkedIn Elevate, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad6d3-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for LinkedIn Elevate, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ad6d3-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-elevate-in-azure-ad"></a><span data-ttu-id="ad6d3-126">To configure automatic user account provisioning to LinkedIn Elevate in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="ad6d3-126">To configure automatic user account provisioning to LinkedIn Elevate in Azure AD:</span></span>


<span data-ttu-id="ad6d3-127">The first step is to retrieve your LinkedIn access token.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="ad6d3-128">If you are an Enterprise administrator, you can self-provision an access token.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="ad6d3-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="ad6d3-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="ad6d3-131">Sign in to Account Center.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="ad6d3-132">Select **Admin &gt; Admin Settings** .</span><span class="sxs-lookup"><span data-stu-id="ad6d3-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="ad6d3-133">Click **Advanced Integrations** on the left sidebar.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="ad6d3-134">You are directed to the account center.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="ad6d3-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="ad6d3-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![LinkedIn Elevate Provisioning](./media/linkedinelevate-provisioning-tutorial/linkedin_elevate1.PNG)

> <span data-ttu-id="ad6d3-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="ad6d3-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![LinkedIn Elevate Provisioning](./media/linkedinelevate-provisioning-tutorial/linkedin_elevate2.PNG)

5)  <span data-ttu-id="ad6d3-141">Click **Generate token**.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-141">Click **Generate token**.</span></span> <span data-ttu-id="ad6d3-142">You should see your access token display under the **Access token** field.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="ad6d3-143">Save your access token to your clipboard or computer before leaving the page.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="ad6d3-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="ad6d3-145">If you have already configured LinkedIn Elevate for single sign-on, search for your instance of LinkedIn Elevate using the search field.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-145">If you have already configured LinkedIn Elevate for single sign-on, search for your instance of LinkedIn Elevate using the search field.</span></span> <span data-ttu-id="ad6d3-146">Otherwise, select **Add** and search for **LinkedIn Elevate** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-146">Otherwise, select **Add** and search for **LinkedIn Elevate** in the application gallery.</span></span> <span data-ttu-id="ad6d3-147">Select LinkedIn Elevate from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-147">Select LinkedIn Elevate from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="ad6d3-148">Select your instance of LinkedIn Elevate, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-148">Select your instance of LinkedIn Elevate, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="ad6d3-149">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![LinkedIn Elevate Provisioning](./media/linkedinelevate-provisioning-tutorial/linkedin_elevate3.PNG)

11)  <span data-ttu-id="ad6d3-151">Fill in the following fields under **Admin Credentials** :</span><span class="sxs-lookup"><span data-stu-id="ad6d3-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="ad6d3-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="ad6d3-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span><span class="sxs-lookup"><span data-stu-id="ad6d3-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="ad6d3-154">You should see a success notification on the upper­right side of   your portal.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="ad6d3-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="ad6d3-156">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-156">Click **Save**.</span></span> 

14) <span data-ttu-id="ad6d3-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Elevate.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Elevate.</span></span> <span data-ttu-id="ad6d3-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Elevate for update operations.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Elevate for update operations.</span></span> <span data-ttu-id="ad6d3-159">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-159">Select the Save button to commit any changes.</span></span>

![LinkedIn Elevate Provisioning](./media/linkedinelevate-provisioning-tutorial/linkedin_elevate4.PNG)

15) <span data-ttu-id="ad6d3-161">To enable the Azure AD provisioning service for LinkedIn Elevate, change the **Provisioning Status** to **On** in the **Settings** section</span><span class="sxs-lookup"><span data-stu-id="ad6d3-161">To enable the Azure AD provisioning service for LinkedIn Elevate, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="ad6d3-162">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-162">Click **Save**.</span></span> 

<span data-ttu-id="ad6d3-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Elevate in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Elevate in the Users and Groups section.</span></span> <span data-ttu-id="ad6d3-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="ad6d3-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your LinkedIn Elevate app.</span><span class="sxs-lookup"><span data-stu-id="ad6d3-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your LinkedIn Elevate app.</span></span>

<span data-ttu-id="ad6d3-166">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="ad6d3-166">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ad6d3-167">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="ad6d3-167">Additional Resources</span></span>

* [<span data-ttu-id="ad6d3-168">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="ad6d3-168">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="ad6d3-169">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad6d3-169">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
