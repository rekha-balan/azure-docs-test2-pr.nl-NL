---
title: 'Tutorial: Configure Dropbox for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Dropbox for Business.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: 8e61fe4af83ee72df74027b2e52a3e81db486798
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855736"
---
# <a name="tutorial-configure-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="95472-103">Tutorial: Configure Dropbox for Business for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="95472-103">Tutorial: Configure Dropbox for Business for automatic user provisioning</span></span>

<span data-ttu-id="95472-104">The objective of this tutorial is to show you the steps you need to perform in Dropbox for Business and Azure AD to automatically provision and de-provision user accounts from Azure AD to Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="95472-104">The objective of this tutorial is to show you the steps you need to perform in Dropbox for Business and Azure AD to automatically provision and de-provision user accounts from Azure AD to Dropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95472-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="95472-105">Prerequisites</span></span>

<span data-ttu-id="95472-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="95472-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="95472-107">An Azure Active directory tenant.</span><span class="sxs-lookup"><span data-stu-id="95472-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="95472-108">A Dropbox for Business single-sign on enabled subscription.</span><span class="sxs-lookup"><span data-stu-id="95472-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="95472-109">A user account in Dropbox for Business with Team Admin permissions.</span><span class="sxs-lookup"><span data-stu-id="95472-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-to-dropbox-for-business"></a><span data-ttu-id="95472-110">Assigning users to Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="95472-110">Assigning users to Dropbox for Business</span></span>

<span data-ttu-id="95472-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="95472-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="95472-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span><span class="sxs-lookup"><span data-stu-id="95472-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="95472-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Dropbox for Business app.</span><span class="sxs-lookup"><span data-stu-id="95472-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Dropbox for Business app.</span></span> <span data-ttu-id="95472-114">Once decided, you can assign these users to your Dropbox for Business app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="95472-114">Once decided, you can assign these users to your Dropbox for Business app by following the instructions here:</span></span>

[<span data-ttu-id="95472-115">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="95472-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-dropbox-for-business"></a><span data-ttu-id="95472-116">Important tips for assigning users to Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="95472-116">Important tips for assigning users to Dropbox for Business</span></span>

*   <span data-ttu-id="95472-117">It is recommended that a single Azure AD user is assigned to Dropbox for Business to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="95472-117">It is recommended that a single Azure AD user is assigned to Dropbox for Business to test the provisioning configuration.</span></span> <span data-ttu-id="95472-118">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="95472-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="95472-119">When assigning a user to Dropbox for Business, you must select a valid user role.</span><span class="sxs-lookup"><span data-stu-id="95472-119">When assigning a user to Dropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="95472-120">The "Default Access" role does not work for provisioning..</span><span class="sxs-lookup"><span data-stu-id="95472-120">The "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="95472-121">Enable Automated User Provisioning</span><span class="sxs-lookup"><span data-stu-id="95472-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="95472-122">This section guides you through connecting your Azure AD to Dropbox for Business's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95472-122">This section guides you through connecting your Azure AD to Dropbox for Business's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="95472-123">You may also choose to enabled SAML-based Single Sign-On for Dropbox for Business, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="95472-123">You may also choose to enabled SAML-based Single Sign-On for Dropbox for Business, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="95472-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="95472-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="95472-125">To configure automatic user account provisioning:</span><span class="sxs-lookup"><span data-stu-id="95472-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="95472-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span><span class="sxs-lookup"><span data-stu-id="95472-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="95472-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using the search field.</span><span class="sxs-lookup"><span data-stu-id="95472-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using the search field.</span></span> <span data-ttu-id="95472-128">Otherwise, select **Add** and search for **Dropbox for Business** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="95472-128">Otherwise, select **Add** and search for **Dropbox for Business** in the application gallery.</span></span> <span data-ttu-id="95472-129">Select Dropbox for Business from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="95472-129">Select Dropbox for Business from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="95472-130">Select your instance of Dropbox for Business, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="95472-130">Select your instance of Dropbox for Business, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="95472-131">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="95472-131">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisioning](./media/dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="95472-133">Under the **Admin Credentials** section, click **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="95472-133">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="95472-134">It opens a Dropbox for Business login dialog in a new browser window.</span><span class="sxs-lookup"><span data-stu-id="95472-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="95472-135">On the **Sign-in to Dropbox to link with Azure AD** dialog, sign in to your Dropbox for Business tenant.</span><span class="sxs-lookup"><span data-stu-id="95472-135">On the **Sign-in to Dropbox to link with Azure AD** dialog, sign in to your Dropbox for Business tenant.</span></span>

     <span data-ttu-id="95472-136">![User provisioning](./media/dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span><span class="sxs-lookup"><span data-stu-id="95472-136">![User provisioning](./media/dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="95472-137">Confirm that you would like to give Azure Active Directory permission to make changes to your Dropbox for Business tenant.</span><span class="sxs-lookup"><span data-stu-id="95472-137">Confirm that you would like to give Azure Active Directory permission to make changes to your Dropbox for Business tenant.</span></span> <span data-ttu-id="95472-138">Click **Allow**.</span><span class="sxs-lookup"><span data-stu-id="95472-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="95472-139">![User provisioning](./media/dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span><span class="sxs-lookup"><span data-stu-id="95472-139">![User provisioning](./media/dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="95472-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Dropbox for Business app.</span><span class="sxs-lookup"><span data-stu-id="95472-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Dropbox for Business app.</span></span> <span data-ttu-id="95472-141">If the connection fails, ensure your Dropbox for Business account has Team Admin permissions and try the **"Authorize"** step again.</span><span class="sxs-lookup"><span data-stu-id="95472-141">If the connection fails, ensure your Dropbox for Business account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="95472-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span><span class="sxs-lookup"><span data-stu-id="95472-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="95472-143">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="95472-143">Click **Save.**</span></span>

11. <span data-ttu-id="95472-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Dropbox for Business.**</span><span class="sxs-lookup"><span data-stu-id="95472-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Dropbox for Business.**</span></span>

12. <span data-ttu-id="95472-145">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="95472-145">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Dropbox for Business.</span></span> <span data-ttu-id="95472-146">The attributes selected as **Matching** properties are used to match the user accounts in Dropbox for Business for update operations.</span><span class="sxs-lookup"><span data-stu-id="95472-146">The attributes selected as **Matching** properties are used to match the user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="95472-147">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="95472-147">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="95472-148">To enable the Azure AD provisioning service for Dropbox for Business, change the **Provisioning Status** to **On** in the Settings section</span><span class="sxs-lookup"><span data-stu-id="95472-148">To enable the Azure AD provisioning service for Dropbox for Business, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="95472-149">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="95472-149">Click **Save.**</span></span>

<span data-ttu-id="95472-150">It starts the initial synchronization of any users and/or groups assigned to Dropbox for Business in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="95472-150">It starts the initial synchronization of any users and/or groups assigned to Dropbox for Business in the Users and Groups section.</span></span> <span data-ttu-id="95472-151">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="95472-151">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="95472-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Dropbox for Business app.</span><span class="sxs-lookup"><span data-stu-id="95472-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="95472-153">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="95472-153">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="95472-154">Additional resources</span><span class="sxs-lookup"><span data-stu-id="95472-154">Additional resources</span></span>

* [<span data-ttu-id="95472-155">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="95472-155">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="95472-156">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="95472-156">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="95472-157">Configure Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="95472-157">Configure Single Sign-on</span></span>](dropboxforbusiness-tutorial.md)