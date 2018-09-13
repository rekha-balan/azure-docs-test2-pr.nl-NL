---
title: 'Tutorial: Configure Salesforce for automatic user provisioning with Azure Active Directory| Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: a35682c1a647039fbb946c0ea79d92e0d3806d0c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870904"
---
# <a name="tutorial-configure-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="9c4b7-103">Tutorial: Configure Salesforce for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="9c4b7-103">Tutorial: Configure Salesforce for automatic user provisioning</span></span>

<span data-ttu-id="9c4b7-104">The objective of this tutorial is to show the steps required to perform in Salesforce and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-104">The objective of this tutorial is to show the steps required to perform in Salesforce and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c4b7-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9c4b7-105">Prerequisites</span></span>

<span data-ttu-id="9c4b7-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="9c4b7-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="9c4b7-107">An Azure Active directory tenant</span><span class="sxs-lookup"><span data-stu-id="9c4b7-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="9c4b7-108">A Salesforce.com tenant</span><span class="sxs-lookup"><span data-stu-id="9c4b7-108">A Salesforce.com tenant</span></span>

>[!IMPORTANT] 
><span data-ttu-id="9c4b7-109">If you are using a Salesforce.com trial account, then you will be unable to configure automated user provisioning.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-109">If you are using a Salesforce.com trial account, then you will be unable to configure automated user provisioning.</span></span> <span data-ttu-id="9c4b7-110">Trial accounts do not have the necessary API access enabled until they are purchased.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-110">Trial accounts do not have the necessary API access enabled until they are purchased.</span></span> <span data-ttu-id="9c4b7-111">You can get around this limitation by using a free [developer account](https://developer.salesforce.com/signup) to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-111">You can get around this limitation by using a free [developer account](https://developer.salesforce.com/signup) to complete this tutorial.</span></span>

<span data-ttu-id="9c4b7-112">If you are using a Salesforce Sandbox environment, please see the [Salesforce Sandbox integration tutorial](https://go.microsoft.com/fwLink/?LinkID=521879).</span><span class="sxs-lookup"><span data-stu-id="9c4b7-112">If you are using a Salesforce Sandbox environment, please see the [Salesforce Sandbox integration tutorial](https://go.microsoft.com/fwLink/?LinkID=521879).</span></span>

## <a name="assigning-users-to-salesforce"></a><span data-ttu-id="9c4b7-113">Assigning users to Salesforce</span><span class="sxs-lookup"><span data-stu-id="9c4b7-113">Assigning users to Salesforce</span></span>

<span data-ttu-id="9c4b7-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="9c4b7-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="9c4b7-116">Before configuring and enabling the provisioning service, you need to decide which users or groups in Azure AD need access to your Salesforce app.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-116">Before configuring and enabling the provisioning service, you need to decide which users or groups in Azure AD need access to your Salesforce app.</span></span> <span data-ttu-id="9c4b7-117">After you've made this decision, you can assign these users to your Salesforce app by following the instructions in [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="9c4b7-117">After you've made this decision, you can assign these users to your Salesforce app by following the instructions in [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

### <a name="important-tips-for-assigning-users-to-salesforce"></a><span data-ttu-id="9c4b7-118">Important tips for assigning users to Salesforce</span><span class="sxs-lookup"><span data-stu-id="9c4b7-118">Important tips for assigning users to Salesforce</span></span>

*   <span data-ttu-id="9c4b7-119">It is recommended that a single Azure AD user is assigned to Salesforce to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-119">It is recommended that a single Azure AD user is assigned to Salesforce to test the provisioning configuration.</span></span> <span data-ttu-id="9c4b7-120">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-120">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="9c4b7-121">When assigning a user to Salesforce, you must select a valid user role.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-121">When assigning a user to Salesforce, you must select a valid user role.</span></span> <span data-ttu-id="9c4b7-122">The "Default Access" role does not work for provisioning</span><span class="sxs-lookup"><span data-stu-id="9c4b7-122">The "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="9c4b7-123">This app imports custom roles from Salesforce as part of the provisioning process, which the customer may want to select when assigning users</span><span class="sxs-lookup"><span data-stu-id="9c4b7-123">This app imports custom roles from Salesforce as part of the provisioning process, which the customer may want to select when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="9c4b7-124">Enable automated user provisioning</span><span class="sxs-lookup"><span data-stu-id="9c4b7-124">Enable automated user provisioning</span></span>

<span data-ttu-id="9c4b7-125">This section guides you through connecting your Azure AD to Salesforce's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-125">This section guides you through connecting your Azure AD to Salesforce's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="9c4b7-126">You may also choose to enabled SAML-based Single Sign-On for Salesforce, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c4b7-126">You may also choose to enabled SAML-based Single Sign-On for Salesforce, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9c4b7-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="9c4b7-128">configure automatic user account provisioning</span><span class="sxs-lookup"><span data-stu-id="9c4b7-128">configure automatic user account provisioning</span></span>

<span data-ttu-id="9c4b7-129">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-129">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce.</span></span>

1. <span data-ttu-id="9c4b7-130">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-130">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

1. <span data-ttu-id="9c4b7-131">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using the search field.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-131">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using the search field.</span></span> <span data-ttu-id="9c4b7-132">Otherwise, select **Add** and search for **Salesforce** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-132">Otherwise, select **Add** and search for **Salesforce** in the application gallery.</span></span> <span data-ttu-id="9c4b7-133">Select Salesforce from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-133">Select Salesforce from the search results, and add it to your list of applications.</span></span>

1. <span data-ttu-id="9c4b7-134">Select your instance of Salesforce, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-134">Select your instance of Salesforce, then select the **Provisioning** tab.</span></span>

1. <span data-ttu-id="9c4b7-135">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-135">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![provisioning](./media/salesforce-provisioning-tutorial/provisioning.png)

1. <span data-ttu-id="9c4b7-137">Under the **Admin Credentials** section, provide the following configuration settings:</span><span class="sxs-lookup"><span data-stu-id="9c4b7-137">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="9c4b7-138">a.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-138">a.</span></span> <span data-ttu-id="9c4b7-139">In the **Admin Username** textbox, type a Salesforce account name that has the **System Administrator** profile in Salesforce.com assigned.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-139">In the **Admin Username** textbox, type a Salesforce account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="9c4b7-140">b.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-140">b.</span></span> <span data-ttu-id="9c4b7-141">In the **Admin Password** textbox, type the password for this account.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-141">In the **Admin Password** textbox, type the password for this account.</span></span>

1. <span data-ttu-id="9c4b7-142">To get your Salesforce security token, open a new tab and sign into the same Salesforce admin account.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-142">To get your Salesforce security token, open a new tab and sign into the same Salesforce admin account.</span></span> <span data-ttu-id="9c4b7-143">On the top right corner of the page, click your name, and then click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-143">On the top right corner of the page, click your name, and then click **Settings**.</span></span>

     <span data-ttu-id="9c4b7-144">![Enable automatic user provisioning](./media/salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="9c4b7-144">![Enable automatic user provisioning](./media/salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>

1. <span data-ttu-id="9c4b7-145">On the left navigation pane, click **My Personal Information** to expand the related section, and then click **Reset My Security Token**.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-145">On the left navigation pane, click **My Personal Information** to expand the related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="9c4b7-146">![Enable automatic user provisioning](./media/salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="9c4b7-146">![Enable automatic user provisioning](./media/salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>

1. <span data-ttu-id="9c4b7-147">On the **Reset Security Token** page, click **Reset Security Token** button.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-147">On the **Reset Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="9c4b7-148">![Enable automatic user provisioning](./media/salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="9c4b7-148">![Enable automatic user provisioning](./media/salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>

1. <span data-ttu-id="9c4b7-149">Check the email inbox associated with this admin account.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-149">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="9c4b7-150">Look for an email from Salesforce.com that contains the new security token.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-150">Look for an email from Salesforce.com that contains the new security token.</span></span>

1. <span data-ttu-id="9c4b7-151">Copy the token, go to your Azure AD window, and paste it into the **Secret Token** field.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-151">Copy the token, go to your Azure AD window, and paste it into the **Secret Token** field.</span></span>

1. <span data-ttu-id="9c4b7-152">The **Tenant URL** should be entered if the instance of Salesforce is on the Salesforce Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-152">The **Tenant URL** should be entered if the instance of Salesforce is on the Salesforce Government Cloud.</span></span> <span data-ttu-id="9c4b7-153">Otherwise, it is optional.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-153">Otherwise, it is optional.</span></span> <span data-ttu-id="9c4b7-154">Enter the tenant URL using the format of "https://\<your-instance\>.my.salesforce.com," replacing \<your-instance\> with the name of your Salesforce instance.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-154">Enter the tenant URL using the format of "https://\<your-instance\>.my.salesforce.com," replacing \<your-instance\> with the name of your Salesforce instance.</span></span>

1. <span data-ttu-id="9c4b7-155">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce app.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-155">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce app.</span></span>

1. <span data-ttu-id="9c4b7-156">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox below.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-156">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox below.</span></span>

1. <span data-ttu-id="9c4b7-157">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="9c4b7-157">Click **Save.**</span></span>  
    
1.  <span data-ttu-id="9c4b7-158">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce.**</span><span class="sxs-lookup"><span data-stu-id="9c4b7-158">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce.**</span></span>

1. <span data-ttu-id="9c4b7-159">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-159">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce.</span></span> <span data-ttu-id="9c4b7-160">Note that the attributes selected as **Matching** properties are used to match the user accounts in Salesforce for update operations.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-160">Note that the attributes selected as **Matching** properties are used to match the user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="9c4b7-161">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-161">Select the Save button to commit any changes.</span></span>

1. <span data-ttu-id="9c4b7-162">To enable the Azure AD provisioning service for Salesforce, change the **Provisioning Status** to **On** in the Settings section</span><span class="sxs-lookup"><span data-stu-id="9c4b7-162">To enable the Azure AD provisioning service for Salesforce, change the **Provisioning Status** to **On** in the Settings section</span></span>

1. <span data-ttu-id="9c4b7-163">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="9c4b7-163">Click **Save.**</span></span>

<span data-ttu-id="9c4b7-164">This starts the initial synchronization of any users and/or groups assigned to Salesforce in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-164">This starts the initial synchronization of any users and/or groups assigned to Salesforce in the Users and Groups section.</span></span> <span data-ttu-id="9c4b7-165">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-165">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="9c4b7-166">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Salesforce app.</span><span class="sxs-lookup"><span data-stu-id="9c4b7-166">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="9c4b7-167">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="9c4b7-167">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9c4b7-168">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9c4b7-168">Additional resources</span></span>

* [<span data-ttu-id="9c4b7-169">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="9c4b7-169">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="9c4b7-170">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9c4b7-170">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="9c4b7-171">Configure Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="9c4b7-171">Configure Single Sign-on</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-salesforce-tutorial)
