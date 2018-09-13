---
title: 'Tutorial: Configuring Slack for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Slack.
services: active-directory
documentationcenter: ''
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: asmalser-msft
ms.openlocfilehash: 97d3073d1f8dd29538fb2d192b0065be496e5277
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555964"
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="cf613-103">Tutorial: Configuring Slack for Automatic User Provisioning</span><span class="sxs-lookup"><span data-stu-id="cf613-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="cf613-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="cf613-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cf613-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cf613-105">Prerequisites</span></span>

<span data-ttu-id="cf613-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="cf613-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="cf613-107">An Azure Active Active directory tenant</span><span class="sxs-lookup"><span data-stu-id="cf613-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="cf613-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span><span class="sxs-lookup"><span data-stu-id="cf613-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="cf613-109">A user account in Slack with Team Admin permissions</span><span class="sxs-lookup"><span data-stu-id="cf613-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="cf613-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span><span class="sxs-lookup"><span data-stu-id="cf613-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span></span>

## <a name="assigning-users-to-slack"></a><span data-ttu-id="cf613-111">Assigning users to Slack</span><span class="sxs-lookup"><span data-stu-id="cf613-111">Assigning users to Slack</span></span>

<span data-ttu-id="cf613-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="cf613-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="cf613-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span><span class="sxs-lookup"><span data-stu-id="cf613-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="cf613-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span><span class="sxs-lookup"><span data-stu-id="cf613-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span></span> <span data-ttu-id="cf613-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="cf613-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span></span>

[<span data-ttu-id="cf613-116">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="cf613-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-slack"></a><span data-ttu-id="cf613-117">Important tips for assigning users to Slack</span><span class="sxs-lookup"><span data-stu-id="cf613-117">Important tips for assigning users to Slack</span></span>

*   <span data-ttu-id="cf613-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="cf613-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span></span> <span data-ttu-id="cf613-119">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="cf613-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="cf613-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="cf613-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="cf613-121">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="cf613-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-slack"></a><span data-ttu-id="cf613-122">Configuring user provisioning to Slack</span><span class="sxs-lookup"><span data-stu-id="cf613-122">Configuring user provisioning to Slack</span></span> 

<span data-ttu-id="cf613-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf613-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="cf613-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="cf613-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="cf613-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="cf613-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-slack-in-azure-ad"></a><span data-ttu-id="cf613-126">To configure automatic user account provisioning to Slack in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="cf613-126">To configure automatic user account provisioning to Slack in Azure AD:</span></span>


1)  <span data-ttu-id="cf613-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span><span class="sxs-lookup"><span data-stu-id="cf613-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="cf613-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span><span class="sxs-lookup"><span data-stu-id="cf613-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span></span> <span data-ttu-id="cf613-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="cf613-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span></span> <span data-ttu-id="cf613-130">Select Slack from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="cf613-130">Select Slack from the search results, and add it to your list of applications.</span></span>

3)  <span data-ttu-id="cf613-131">Select your instance of Slack, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="cf613-131">Select your instance of Slack, then select the **Provisioning** tab.</span></span>

4)  <span data-ttu-id="cf613-132">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="cf613-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Slack Provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="cf613-134">Under the **Admin Credentials** section, click **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="cf613-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="cf613-135">This opens a Slack authorization dialog in a new browser window.</span><span class="sxs-lookup"><span data-stu-id="cf613-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="cf613-136">In the new window, sign into Slack using your Team Admin account.</span><span class="sxs-lookup"><span data-stu-id="cf613-136">In the new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="cf613-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="cf613-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="cf613-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="cf613-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

![Authorization Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="cf613-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span><span class="sxs-lookup"><span data-stu-id="cf613-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span></span> <span data-ttu-id="cf613-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span><span class="sxs-lookup"><span data-stu-id="cf613-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span></span>

8) <span data-ttu-id="cf613-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span><span class="sxs-lookup"><span data-stu-id="cf613-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

9) <span data-ttu-id="cf613-143">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cf613-143">Click **Save**.</span></span> 

10) <span data-ttu-id="cf613-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span><span class="sxs-lookup"><span data-stu-id="cf613-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span></span>

11) <span data-ttu-id="cf613-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="cf613-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="cf613-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span><span class="sxs-lookup"><span data-stu-id="cf613-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span></span> <span data-ttu-id="cf613-147">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="cf613-147">Select the Save button to commit any changes.</span></span>

12) <span data-ttu-id="cf613-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span><span class="sxs-lookup"><span data-stu-id="cf613-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13) <span data-ttu-id="cf613-149">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cf613-149">Click **Save**.</span></span> 

<span data-ttu-id="cf613-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="cf613-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span></span> <span data-ttu-id="cf613-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="cf613-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span></span> <span data-ttu-id="cf613-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span><span class="sxs-lookup"><span data-stu-id="cf613-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-to-slack"></a><span data-ttu-id="cf613-153">[Optional] Configuring group object provisioning to Slack</span><span class="sxs-lookup"><span data-stu-id="cf613-153">[Optional] Configuring group object provisioning to Slack</span></span> 

<span data-ttu-id="cf613-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="cf613-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span></span> <span data-ttu-id="cf613-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="cf613-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span></span> <span data-ttu-id="cf613-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span><span class="sxs-lookup"><span data-stu-id="cf613-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="to-enable-provisioning-of-group-objects"></a><span data-ttu-id="cf613-157">To enable provisioning of group objects:</span><span class="sxs-lookup"><span data-stu-id="cf613-157">To enable provisioning of group objects:</span></span>

1) <span data-ttu-id="cf613-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span><span class="sxs-lookup"><span data-stu-id="cf613-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span></span>

2) <span data-ttu-id="cf613-159">In the Attribute Mapping blade, set Enabled to Yes.</span><span class="sxs-lookup"><span data-stu-id="cf613-159">In the Attribute Mapping blade, set Enabled to Yes.</span></span>

3) <span data-ttu-id="cf613-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="cf613-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="cf613-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span><span class="sxs-lookup"><span data-stu-id="cf613-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="cf613-162">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cf613-162">Click **Save**.</span></span>

<span data-ttu-id="cf613-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span><span class="sxs-lookup"><span data-stu-id="cf613-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="cf613-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span><span class="sxs-lookup"><span data-stu-id="cf613-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cf613-165">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="cf613-165">Additional Resources</span></span>

* [<span data-ttu-id="cf613-166">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="cf613-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="cf613-167">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cf613-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


