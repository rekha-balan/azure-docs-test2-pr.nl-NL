---
title: 'Tutorial: Configure LinkedIn Sales Navigator for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to LinkedIn Sales Navigator.
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
ms.openlocfilehash: 1c5b8f2f8f8ea43e37bc65eb8f6ad03c3f198878
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871198"
---
# <a name="tutorial-configure-linkedin-sales-navigator-for-automatic-user-provisioning"></a><span data-ttu-id="bbd91-103">Tutorial: Configure LinkedIn Sales Navigator for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="bbd91-103">Tutorial: Configure LinkedIn Sales Navigator for automatic user provisioning</span></span>


<span data-ttu-id="bbd91-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Sales Navigator and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="bbd91-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Sales Navigator and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Sales Navigator.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bbd91-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bbd91-105">Prerequisites</span></span>

<span data-ttu-id="bbd91-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="bbd91-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="bbd91-107">An Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="bbd91-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="bbd91-108">A LinkedIn Sales Navigator tenant</span><span class="sxs-lookup"><span data-stu-id="bbd91-108">A LinkedIn Sales Navigator tenant</span></span> 
*   <span data-ttu-id="bbd91-109">An administrator account in LinkedIn Sales Navigator with access to the LinkedIn Account Center</span><span class="sxs-lookup"><span data-stu-id="bbd91-109">An administrator account in LinkedIn Sales Navigator with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="bbd91-110">Azure Active Directory integrates with LinkedIn Sales Navigator using the [SCIM](http://www.simplecloud.info/) protocol.</span><span class="sxs-lookup"><span data-stu-id="bbd91-110">Azure Active Directory integrates with LinkedIn Sales Navigator using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-sales-navigator"></a><span data-ttu-id="bbd91-111">Assigning users to LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="bbd91-111">Assigning users to LinkedIn Sales Navigator</span></span>

<span data-ttu-id="bbd91-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="bbd91-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="bbd91-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span><span class="sxs-lookup"><span data-stu-id="bbd91-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="bbd91-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="bbd91-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Sales Navigator.</span></span> <span data-ttu-id="bbd91-115">Once decided, you can assign these users to LinkedIn Sales Navigator by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="bbd91-115">Once decided, you can assign these users to LinkedIn Sales Navigator by following the instructions here:</span></span>

[<span data-ttu-id="bbd91-116">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="bbd91-116">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-sales-navigator"></a><span data-ttu-id="bbd91-117">Important tips for assigning users to LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="bbd91-117">Important tips for assigning users to LinkedIn Sales Navigator</span></span>

*   <span data-ttu-id="bbd91-118">It is recommended that a single Azure AD user be assigned to LinkedIn Sales Navigator to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="bbd91-118">It is recommended that a single Azure AD user be assigned to LinkedIn Sales Navigator to test the provisioning configuration.</span></span> <span data-ttu-id="bbd91-119">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="bbd91-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bbd91-120">When assigning a user to LinkedIn Sales Navigator, you must select the **User** role in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="bbd91-120">When assigning a user to LinkedIn Sales Navigator, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="bbd91-121">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="bbd91-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-sales-navigator"></a><span data-ttu-id="bbd91-122">Configuring user provisioning to LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="bbd91-122">Configuring user provisioning to LinkedIn Sales Navigator</span></span>

<span data-ttu-id="bbd91-123">This section guides you through connecting your Azure AD to LinkedIn Sales Navigator's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Sales Navigator based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd91-123">This section guides you through connecting your Azure AD to LinkedIn Sales Navigator's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Sales Navigator based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="bbd91-124">You may also choose to enabled SAML-based Single Sign-On for LinkedIn Sales Navigator, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bbd91-124">You may also choose to enabled SAML-based Single Sign-On for LinkedIn Sales Navigator, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bbd91-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span><span class="sxs-lookup"><span data-stu-id="bbd91-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-sales-navigator-in-azure-ad"></a><span data-ttu-id="bbd91-126">To configure automatic user account provisioning to LinkedIn Sales Navigator in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="bbd91-126">To configure automatic user account provisioning to LinkedIn Sales Navigator in Azure AD:</span></span>


<span data-ttu-id="bbd91-127">The first step is to retrieve your LinkedIn access token.</span><span class="sxs-lookup"><span data-stu-id="bbd91-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="bbd91-128">If you are an Enterprise administrator, you can self-provision an access token.</span><span class="sxs-lookup"><span data-stu-id="bbd91-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="bbd91-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span><span class="sxs-lookup"><span data-stu-id="bbd91-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="bbd91-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span><span class="sxs-lookup"><span data-stu-id="bbd91-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="bbd91-131">Sign in to Account Center.</span><span class="sxs-lookup"><span data-stu-id="bbd91-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="bbd91-132">Select **Admin &gt; Admin Settings** .</span><span class="sxs-lookup"><span data-stu-id="bbd91-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="bbd91-133">Click **Advanced Integrations** on the left sidebar.</span><span class="sxs-lookup"><span data-stu-id="bbd91-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="bbd91-134">You are directed to the account center.</span><span class="sxs-lookup"><span data-stu-id="bbd91-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="bbd91-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span><span class="sxs-lookup"><span data-stu-id="bbd91-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="bbd91-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span><span class="sxs-lookup"><span data-stu-id="bbd91-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![LinkedIn Sales Navigator Provisioning](./media/linkedinsalesnavigator-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="bbd91-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span><span class="sxs-lookup"><span data-stu-id="bbd91-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="bbd91-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span><span class="sxs-lookup"><span data-stu-id="bbd91-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![LinkedIn Sales Navigator Provisioning](./media/linkedinsalesnavigator-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="bbd91-141">Click **Generate token**.</span><span class="sxs-lookup"><span data-stu-id="bbd91-141">Click **Generate token**.</span></span> <span data-ttu-id="bbd91-142">You should see your access token display under the **Access token** field.</span><span class="sxs-lookup"><span data-stu-id="bbd91-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="bbd91-143">Save your access token to your clipboard or computer before leaving the page.</span><span class="sxs-lookup"><span data-stu-id="bbd91-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="bbd91-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span><span class="sxs-lookup"><span data-stu-id="bbd91-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="bbd91-145">If you have already configured LinkedIn Sales Navigator for single sign-on, search for your instance of LinkedIn Sales Navigator using the search field.</span><span class="sxs-lookup"><span data-stu-id="bbd91-145">If you have already configured LinkedIn Sales Navigator for single sign-on, search for your instance of LinkedIn Sales Navigator using the search field.</span></span> <span data-ttu-id="bbd91-146">Otherwise, select **Add** and search for **LinkedIn Sales Navigator** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="bbd91-146">Otherwise, select **Add** and search for **LinkedIn Sales Navigator** in the application gallery.</span></span> <span data-ttu-id="bbd91-147">Select LinkedIn Sales Navigator from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="bbd91-147">Select LinkedIn Sales Navigator from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="bbd91-148">Select your instance of LinkedIn Sales Navigator, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="bbd91-148">Select your instance of LinkedIn Sales Navigator, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="bbd91-149">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="bbd91-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![LinkedIn Sales Navigator Provisioning](./media/linkedinsalesnavigator-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="bbd91-151">Fill in the following fields under **Admin Credentials** :</span><span class="sxs-lookup"><span data-stu-id="bbd91-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="bbd91-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="bbd91-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="bbd91-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span><span class="sxs-lookup"><span data-stu-id="bbd91-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="bbd91-154">You should see a success notification on the upper­right side of   your portal.</span><span class="sxs-lookup"><span data-stu-id="bbd91-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="bbd91-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span><span class="sxs-lookup"><span data-stu-id="bbd91-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="bbd91-156">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bbd91-156">Click **Save**.</span></span> 

14) <span data-ttu-id="bbd91-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="bbd91-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Sales Navigator.</span></span> <span data-ttu-id="bbd91-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Sales Navigator for update operations.</span><span class="sxs-lookup"><span data-stu-id="bbd91-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Sales Navigator for update operations.</span></span> <span data-ttu-id="bbd91-159">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="bbd91-159">Select the Save button to commit any changes.</span></span>

![LinkedIn Sales Navigator Provisioning](./media/linkedinsalesnavigator-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="bbd91-161">To enable the Azure AD provisioning service for LinkedIn Sales Navigator, change the **Provisioning Status** to **On** in the **Settings** section</span><span class="sxs-lookup"><span data-stu-id="bbd91-161">To enable the Azure AD provisioning service for LinkedIn Sales Navigator, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="bbd91-162">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bbd91-162">Click **Save**.</span></span> 

<span data-ttu-id="bbd91-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Sales Navigator in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="bbd91-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Sales Navigator in the Users and Groups section.</span></span> <span data-ttu-id="bbd91-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="bbd91-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="bbd91-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your LinkedIn Sales Navigator app.</span><span class="sxs-lookup"><span data-stu-id="bbd91-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your LinkedIn Sales Navigator app.</span></span>

<span data-ttu-id="bbd91-166">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="bbd91-166">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bbd91-167">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="bbd91-167">Additional Resources</span></span>

* [<span data-ttu-id="bbd91-168">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="bbd91-168">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="bbd91-169">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bbd91-169">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
