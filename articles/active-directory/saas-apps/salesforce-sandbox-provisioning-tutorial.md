---
title: 'Tutorial: Configure Salesforce Sandbox for automatic user provisioning with Azure Active Directory| Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Salesforce Sandbox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: b1ad53c4ba1b79a1918177ce73862b603d157153
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864937"
---
# <a name="tutorial-configure-salesforce-sandbox-for-automatic-user-provisioning"></a><span data-ttu-id="81378-103">Tutorial: Configure Salesforce Sandbox for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="81378-103">Tutorial: Configure Salesforce Sandbox for automatic user provisioning</span></span>

<span data-ttu-id="81378-104">The objective of this tutorial is to show you the steps you need to perform in Salesforce Sandbox and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="81378-104">The objective of this tutorial is to show you the steps you need to perform in Salesforce Sandbox and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce Sandbox.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81378-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="81378-105">Prerequisites</span></span>

<span data-ttu-id="81378-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="81378-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="81378-107">An Azure Active directory tenant.</span><span class="sxs-lookup"><span data-stu-id="81378-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="81378-108">A valid tenant for Salesforce Sandbox for Work or Salesforce Sandbox for Education.</span><span class="sxs-lookup"><span data-stu-id="81378-108">A valid tenant for Salesforce Sandbox for Work or Salesforce Sandbox for Education.</span></span> <span data-ttu-id="81378-109">You may use a free trial     account for either service.</span><span class="sxs-lookup"><span data-stu-id="81378-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="81378-110">A user account in Salesforce Sandbox with Team Admin permissions.</span><span class="sxs-lookup"><span data-stu-id="81378-110">A user account in Salesforce Sandbox with Team Admin permissions.</span></span>

## <a name="assigning-users-to-salesforce-sandbox"></a><span data-ttu-id="81378-111">Assigning users to Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="81378-111">Assigning users to Salesforce Sandbox</span></span>

<span data-ttu-id="81378-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="81378-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="81378-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="81378-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="81378-114">Before configuring and enabling the provisioning service, you need to decide which users or groups in Azure AD need access to your Salesforce Sandbox app.</span><span class="sxs-lookup"><span data-stu-id="81378-114">Before configuring and enabling the provisioning service, you need to decide which users or groups in Azure AD need access to your Salesforce Sandbox app.</span></span> <span data-ttu-id="81378-115">After you've made this decision, you can assign these users to your Salesforce Sandbox app by following the instructions in [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="81378-115">After you've made this decision, you can assign these users to your Salesforce Sandbox app by following the instructions in [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

### <a name="important-tips-for-assigning-users-to-salesforce-sandbox"></a><span data-ttu-id="81378-116">Important tips for assigning users to Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="81378-116">Important tips for assigning users to Salesforce Sandbox</span></span>

* <span data-ttu-id="81378-117">It is recommended that a single Azure AD user is assigned to Salesforce Sandbox to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="81378-117">It is recommended that a single Azure AD user is assigned to Salesforce Sandbox to test the provisioning configuration.</span></span> <span data-ttu-id="81378-118">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="81378-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="81378-119">When assigning a user to Salesforce Sandbox, you must select a valid user role.</span><span class="sxs-lookup"><span data-stu-id="81378-119">When assigning a user to Salesforce Sandbox, you must select a valid user role.</span></span> <span data-ttu-id="81378-120">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="81378-120">The "Default Access" role does not work for provisioning.</span></span>

> [!NOTE]
> <span data-ttu-id="81378-121">This app imports custom roles from Salesforce Sandbox as part of the provisioning process, which the customer may want to select when assigning users.</span><span class="sxs-lookup"><span data-stu-id="81378-121">This app imports custom roles from Salesforce Sandbox as part of the provisioning process, which the customer may want to select when assigning users.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="81378-122">Enable automated user provisioning</span><span class="sxs-lookup"><span data-stu-id="81378-122">Enable automated user provisioning</span></span>

<span data-ttu-id="81378-123">This section guides you through connecting your Azure AD to Salesforce Sandbox's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce Sandbox based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81378-123">This section guides you through connecting your Azure AD to Salesforce Sandbox's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce Sandbox based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="81378-124">You may also choose to enabled SAML-based Single Sign-On for Salesforce Sandbox, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81378-124">You may also choose to enabled SAML-based Single Sign-On for Salesforce Sandbox, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="81378-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="81378-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="81378-126">Configure automatic user account provisioning</span><span class="sxs-lookup"><span data-stu-id="81378-126">Configure automatic user account provisioning</span></span>

<span data-ttu-id="81378-127">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="81378-127">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

1. <span data-ttu-id="81378-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span><span class="sxs-lookup"><span data-stu-id="81378-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

1. <span data-ttu-id="81378-129">If you have already configured Salesforce Sandbox for single sign-on, search for your instance of Salesforce Sandbox using the search field.</span><span class="sxs-lookup"><span data-stu-id="81378-129">If you have already configured Salesforce Sandbox for single sign-on, search for your instance of Salesforce Sandbox using the search field.</span></span> <span data-ttu-id="81378-130">Otherwise, select **Add** and search for **Salesforce Sandbox** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="81378-130">Otherwise, select **Add** and search for **Salesforce Sandbox** in the application gallery.</span></span> <span data-ttu-id="81378-131">Select Salesforce Sandbox from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="81378-131">Select Salesforce Sandbox from the search results, and add it to your list of applications.</span></span>

1. <span data-ttu-id="81378-132">Select your instance of Salesforce Sandbox, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="81378-132">Select your instance of Salesforce Sandbox, then select the **Provisioning** tab.</span></span>

1. <span data-ttu-id="81378-133">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="81378-133">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![provisioning](./media/salesforce-sandbox-provisioning-tutorial/provisioning.png)

1. <span data-ttu-id="81378-135">Under the **Admin Credentials** section, provide the following configuration settings:</span><span class="sxs-lookup"><span data-stu-id="81378-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="81378-136">a.</span><span class="sxs-lookup"><span data-stu-id="81378-136">a.</span></span> <span data-ttu-id="81378-137">In the **Admin Username** textbox, type a Salesforce Sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span><span class="sxs-lookup"><span data-stu-id="81378-137">In the **Admin Username** textbox, type a Salesforce Sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="81378-138">b.</span><span class="sxs-lookup"><span data-stu-id="81378-138">b.</span></span> <span data-ttu-id="81378-139">In the **Admin Password** textbox, type the password for this account.</span><span class="sxs-lookup"><span data-stu-id="81378-139">In the **Admin Password** textbox, type the password for this account.</span></span>

1. <span data-ttu-id="81378-140">To get your Salesforce Sandbox security token, open a new tab and sign into the same Salesforce Sandbox admin account.</span><span class="sxs-lookup"><span data-stu-id="81378-140">To get your Salesforce Sandbox security token, open a new tab and sign into the same Salesforce Sandbox admin account.</span></span> <span data-ttu-id="81378-141">On the top right corner of the page, click your name, and then click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="81378-141">On the top right corner of the page, click your name, and then click **Settings**.</span></span>

     <span data-ttu-id="81378-142">![Enable automatic user provisioning](./media/salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="81378-142">![Enable automatic user provisioning](./media/salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>

1. <span data-ttu-id="81378-143">On the left navigation pane, click **My Personal Information** to expand the related section, and then click **Reset My Security Token**.</span><span class="sxs-lookup"><span data-stu-id="81378-143">On the left navigation pane, click **My Personal Information** to expand the related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="81378-144">![Enable automatic user provisioning](./media/salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="81378-144">![Enable automatic user provisioning](./media/salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>

1. <span data-ttu-id="81378-145">On the **Reset Security Token** page, click the **Reset Security Token** button.</span><span class="sxs-lookup"><span data-stu-id="81378-145">On the **Reset Security Token** page, click the **Reset Security Token** button.</span></span>

    <span data-ttu-id="81378-146">![Enable automatic user provisioning](./media/salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="81378-146">![Enable automatic user provisioning](./media/salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>

1. <span data-ttu-id="81378-147">Check the email inbox associated with this admin account.</span><span class="sxs-lookup"><span data-stu-id="81378-147">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="81378-148">Look for an email from Salesforce Sandbox.com that contains the new security token.</span><span class="sxs-lookup"><span data-stu-id="81378-148">Look for an email from Salesforce Sandbox.com that contains the new security token.</span></span>

1. <span data-ttu-id="81378-149">Copy the token, go to your Azure AD window, and paste it into the **Secret Token** field.</span><span class="sxs-lookup"><span data-stu-id="81378-149">Copy the token, go to your Azure AD window, and paste it into the **Secret Token** field.</span></span>

1. <span data-ttu-id="81378-150">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce Sandbox app.</span><span class="sxs-lookup"><span data-stu-id="81378-150">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce Sandbox app.</span></span>

1. <span data-ttu-id="81378-151">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span><span class="sxs-lookup"><span data-stu-id="81378-151">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

1. <span data-ttu-id="81378-152">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="81378-152">Click **Save.**</span></span>  
    
1.  <span data-ttu-id="81378-153">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce Sandbox.**</span><span class="sxs-lookup"><span data-stu-id="81378-153">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce Sandbox.**</span></span>

1. <span data-ttu-id="81378-154">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="81378-154">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce Sandbox.</span></span> <span data-ttu-id="81378-155">The attributes selected as **Matching** properties are used to match the user accounts in Salesforce Sandbox for update operations.</span><span class="sxs-lookup"><span data-stu-id="81378-155">The attributes selected as **Matching** properties are used to match the user accounts in Salesforce Sandbox for update operations.</span></span> <span data-ttu-id="81378-156">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="81378-156">Select the Save button to commit any changes.</span></span>

1. <span data-ttu-id="81378-157">To enable the Azure AD provisioning service for Salesforce Sandbox, change the **Provisioning Status** to **On** in the Settings section</span><span class="sxs-lookup"><span data-stu-id="81378-157">To enable the Azure AD provisioning service for Salesforce Sandbox, change the **Provisioning Status** to **On** in the Settings section</span></span>

1. <span data-ttu-id="81378-158">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="81378-158">Click **Save.**</span></span>

<span data-ttu-id="81378-159">It starts the initial synchronization of any users and/or groups assigned to Salesforce Sandbox in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="81378-159">It starts the initial synchronization of any users and/or groups assigned to Salesforce Sandbox in the Users and Groups section.</span></span> <span data-ttu-id="81378-160">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="81378-160">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="81378-161">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on Salesforce Sandbox app.</span><span class="sxs-lookup"><span data-stu-id="81378-161">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on Salesforce Sandbox app.</span></span>

<span data-ttu-id="81378-162">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="81378-162">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81378-163">Additional resources</span><span class="sxs-lookup"><span data-stu-id="81378-163">Additional resources</span></span>

* [<span data-ttu-id="81378-164">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="81378-164">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="81378-165">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81378-165">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="81378-166">Configure Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="81378-166">Configure Single Sign-on</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-salesforce-sandbox-tutorial)
