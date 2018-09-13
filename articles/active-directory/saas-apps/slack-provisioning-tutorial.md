---
title: 'Tutorial: Configure Slack for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Slack.
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
ms.reviewer: asmalser
ms.openlocfilehash: 7d6056987ee05f68eecf026e954327a2f62cf886
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864586"
---
# <a name="tutorial-configure-slack-for-automatic-user-provisioning"></a><span data-ttu-id="dbe9f-103">Tutorial: Configure Slack for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="dbe9f-103">Tutorial: Configure Slack for automatic user provisioning</span></span>


<span data-ttu-id="dbe9f-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dbe9f-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dbe9f-105">Prerequisites</span></span>

<span data-ttu-id="dbe9f-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="dbe9f-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="dbe9f-107">An Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="dbe9f-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="dbe9f-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span><span class="sxs-lookup"><span data-stu-id="dbe9f-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="dbe9f-109">A user account in Slack with Team Admin permissions</span><span class="sxs-lookup"><span data-stu-id="dbe9f-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="dbe9f-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span></span>

## <a name="assigning-users-to-slack"></a><span data-ttu-id="dbe9f-111">Assigning users to Slack</span><span class="sxs-lookup"><span data-stu-id="dbe9f-111">Assigning users to Slack</span></span>

<span data-ttu-id="dbe9f-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="dbe9f-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="dbe9f-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span></span> <span data-ttu-id="dbe9f-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="dbe9f-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span></span>

[<span data-ttu-id="dbe9f-116">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="dbe9f-116">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-slack"></a><span data-ttu-id="dbe9f-117">Important tips for assigning users to Slack</span><span class="sxs-lookup"><span data-stu-id="dbe9f-117">Important tips for assigning users to Slack</span></span>

*   <span data-ttu-id="dbe9f-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span></span> <span data-ttu-id="dbe9f-119">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="dbe9f-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="dbe9f-121">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-slack"></a><span data-ttu-id="dbe9f-122">Configuring user provisioning to Slack</span><span class="sxs-lookup"><span data-stu-id="dbe9f-122">Configuring user provisioning to Slack</span></span> 

<span data-ttu-id="dbe9f-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="dbe9f-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="dbe9f-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="dbe9f-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-slack-in-azure-ad"></a><span data-ttu-id="dbe9f-126">To configure automatic user account provisioning to Slack in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="dbe9f-126">To configure automatic user account provisioning to Slack in Azure AD:</span></span>


1)  <span data-ttu-id="dbe9f-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="dbe9f-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span></span> <span data-ttu-id="dbe9f-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span></span> <span data-ttu-id="dbe9f-130">Select Slack from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-130">Select Slack from the search results, and add it to your list of applications.</span></span>

3)  <span data-ttu-id="dbe9f-131">Select your instance of Slack, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-131">Select your instance of Slack, then select the **Provisioning** tab.</span></span>

4)  <span data-ttu-id="dbe9f-132">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Slack Provisioning](./media/slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="dbe9f-134">Under the **Admin Credentials** section, click **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="dbe9f-135">This opens a Slack authorization dialog in a new browser window.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="dbe9f-136">In the new window, sign into Slack using your Team Admin account.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-136">In the new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="dbe9f-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="dbe9f-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

![Authorization Dialog](./media/slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="dbe9f-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span></span> <span data-ttu-id="dbe9f-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span></span>

8) <span data-ttu-id="dbe9f-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

9) <span data-ttu-id="dbe9f-143">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-143">Click **Save**.</span></span> 

10) <span data-ttu-id="dbe9f-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span></span>

11) <span data-ttu-id="dbe9f-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="dbe9f-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span></span> <span data-ttu-id="dbe9f-147">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-147">Select the Save button to commit any changes.</span></span>

12) <span data-ttu-id="dbe9f-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span><span class="sxs-lookup"><span data-stu-id="dbe9f-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13) <span data-ttu-id="dbe9f-149">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-149">Click **Save**.</span></span> 

<span data-ttu-id="dbe9f-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span></span> <span data-ttu-id="dbe9f-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span></span> <span data-ttu-id="dbe9f-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-to-slack"></a><span data-ttu-id="dbe9f-153">[Optional] Configuring group object provisioning to Slack</span><span class="sxs-lookup"><span data-stu-id="dbe9f-153">[Optional] Configuring group object provisioning to Slack</span></span> 

<span data-ttu-id="dbe9f-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span></span> <span data-ttu-id="dbe9f-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span></span> <span data-ttu-id="dbe9f-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="to-enable-provisioning-of-group-objects"></a><span data-ttu-id="dbe9f-157">To enable provisioning of group objects:</span><span class="sxs-lookup"><span data-stu-id="dbe9f-157">To enable provisioning of group objects:</span></span>

1) <span data-ttu-id="dbe9f-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span></span>

2) <span data-ttu-id="dbe9f-159">In the Attribute Mapping blade, set Enabled to Yes.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-159">In the Attribute Mapping blade, set Enabled to Yes.</span></span>

3) <span data-ttu-id="dbe9f-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="dbe9f-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="dbe9f-162">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-162">Click **Save**.</span></span>

<span data-ttu-id="dbe9f-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="dbe9f-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Slack app.</span><span class="sxs-lookup"><span data-stu-id="dbe9f-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Slack app.</span></span>

<span data-ttu-id="dbe9f-165">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="dbe9f-165">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="dbe9f-166">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="dbe9f-166">Additional Resources</span></span>

* [<span data-ttu-id="dbe9f-167">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="dbe9f-167">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="dbe9f-168">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dbe9f-168">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
