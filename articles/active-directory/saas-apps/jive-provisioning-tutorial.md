---
title: 'Tutorial: Configure Jive for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: 4396a16ec78d604b3d6c3bea5571d21ca48d5921
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869527"
---
# <a name="tutorial-configure-jive-for-automatic-user-provisioning"></a><span data-ttu-id="1a21a-103">Tutorial: Configure Jive for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="1a21a-103">Tutorial: Configure Jive for automatic user provisioning</span></span>

<span data-ttu-id="1a21a-104">The objective of this tutorial is to show you the steps you need to perform in Jive and Azure AD to automatically provision and de-provision user accounts from Azure AD to Jive.</span><span class="sxs-lookup"><span data-stu-id="1a21a-104">The objective of this tutorial is to show you the steps you need to perform in Jive and Azure AD to automatically provision and de-provision user accounts from Azure AD to Jive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a21a-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1a21a-105">Prerequisites</span></span>

<span data-ttu-id="1a21a-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="1a21a-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="1a21a-107">An Azure Active directory tenant.</span><span class="sxs-lookup"><span data-stu-id="1a21a-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="1a21a-108">A Jive single-sign on enabled subscription.</span><span class="sxs-lookup"><span data-stu-id="1a21a-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="1a21a-109">A user account in Jive with Team Admin permissions.</span><span class="sxs-lookup"><span data-stu-id="1a21a-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-to-jive"></a><span data-ttu-id="1a21a-110">Assigning users to Jive</span><span class="sxs-lookup"><span data-stu-id="1a21a-110">Assigning users to Jive</span></span>

<span data-ttu-id="1a21a-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="1a21a-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="1a21a-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span><span class="sxs-lookup"><span data-stu-id="1a21a-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="1a21a-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Jive app.</span><span class="sxs-lookup"><span data-stu-id="1a21a-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Jive app.</span></span> <span data-ttu-id="1a21a-114">Once decided, you can assign these users to your Jive app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="1a21a-114">Once decided, you can assign these users to your Jive app by following the instructions here:</span></span>

[<span data-ttu-id="1a21a-115">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="1a21a-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-jive"></a><span data-ttu-id="1a21a-116">Important tips for assigning users to Jive</span><span class="sxs-lookup"><span data-stu-id="1a21a-116">Important tips for assigning users to Jive</span></span>

*   <span data-ttu-id="1a21a-117">It is recommended that a single Azure AD user be assigned to Jive to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="1a21a-117">It is recommended that a single Azure AD user be assigned to Jive to test the provisioning configuration.</span></span> <span data-ttu-id="1a21a-118">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="1a21a-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1a21a-119">When assigning a user to Jive, you must select a valid user role.</span><span class="sxs-lookup"><span data-stu-id="1a21a-119">When assigning a user to Jive, you must select a valid user role.</span></span> <span data-ttu-id="1a21a-120">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="1a21a-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="1a21a-121">Enable User Provisioning</span><span class="sxs-lookup"><span data-stu-id="1a21a-121">Enable User Provisioning</span></span>

<span data-ttu-id="1a21a-122">This section guides you through connecting your Azure AD to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a21a-122">This section guides you through connecting your Azure AD to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="1a21a-123">You may also choose to enabled SAML-based Single Sign-On for Jive, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1a21a-123">You may also choose to enabled SAML-based Single Sign-On for Jive, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1a21a-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="1a21a-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="1a21a-125">To configure user account provisioning:</span><span class="sxs-lookup"><span data-stu-id="1a21a-125">To configure user account provisioning:</span></span>

<span data-ttu-id="1a21a-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span><span class="sxs-lookup"><span data-stu-id="1a21a-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>
<span data-ttu-id="1a21a-127">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span><span class="sxs-lookup"><span data-stu-id="1a21a-127">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span></span>

1. <span data-ttu-id="1a21a-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span><span class="sxs-lookup"><span data-stu-id="1a21a-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

1. <span data-ttu-id="1a21a-129">If you have already configured Jive for single sign-on, search for your instance of Jive using the search field.</span><span class="sxs-lookup"><span data-stu-id="1a21a-129">If you have already configured Jive for single sign-on, search for your instance of Jive using the search field.</span></span> <span data-ttu-id="1a21a-130">Otherwise, select **Add** and search for **Jive** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="1a21a-130">Otherwise, select **Add** and search for **Jive** in the application gallery.</span></span> <span data-ttu-id="1a21a-131">Select Jive from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="1a21a-131">Select Jive from the search results, and add it to your list of applications.</span></span>

1. <span data-ttu-id="1a21a-132">Select your instance of Jive, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="1a21a-132">Select your instance of Jive, then select the **Provisioning** tab.</span></span>

1. <span data-ttu-id="1a21a-133">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="1a21a-133">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisioning](./media/jive-provisioning-tutorial/provisioning.png)

1. <span data-ttu-id="1a21a-135">Under the **Admin Credentials** section, provide the following configuration settings:</span><span class="sxs-lookup"><span data-stu-id="1a21a-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="1a21a-136">a.</span><span class="sxs-lookup"><span data-stu-id="1a21a-136">a.</span></span> <span data-ttu-id="1a21a-137">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span><span class="sxs-lookup"><span data-stu-id="1a21a-137">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="1a21a-138">b.</span><span class="sxs-lookup"><span data-stu-id="1a21a-138">b.</span></span> <span data-ttu-id="1a21a-139">In the **Jive Admin Password** textbox, type the password for this account.</span><span class="sxs-lookup"><span data-stu-id="1a21a-139">In the **Jive Admin Password** textbox, type the password for this account.</span></span>
   
    <span data-ttu-id="1a21a-140">c.</span><span class="sxs-lookup"><span data-stu-id="1a21a-140">c.</span></span> <span data-ttu-id="1a21a-141">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span><span class="sxs-lookup"><span data-stu-id="1a21a-141">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="1a21a-142">The Jive tenant URL is URL that is used by your organization to log in to Jive.</span><span class="sxs-lookup"><span data-stu-id="1a21a-142">The Jive tenant URL is URL that is used by your organization to log in to Jive.</span></span>  
      > <span data-ttu-id="1a21a-143">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span><span class="sxs-lookup"><span data-stu-id="1a21a-143">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span></span>          

1. <span data-ttu-id="1a21a-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Jive app.</span><span class="sxs-lookup"><span data-stu-id="1a21a-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Jive app.</span></span>

1. <span data-ttu-id="1a21a-145">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span><span class="sxs-lookup"><span data-stu-id="1a21a-145">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

1. <span data-ttu-id="1a21a-146">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="1a21a-146">Click **Save.**</span></span>

1. <span data-ttu-id="1a21a-147">Under the Mappings section, select **Synchronize Azure Active Directory Users to Jive.**</span><span class="sxs-lookup"><span data-stu-id="1a21a-147">Under the Mappings section, select **Synchronize Azure Active Directory Users to Jive.**</span></span>

1. <span data-ttu-id="1a21a-148">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Jive.</span><span class="sxs-lookup"><span data-stu-id="1a21a-148">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Jive.</span></span> <span data-ttu-id="1a21a-149">The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations.</span><span class="sxs-lookup"><span data-stu-id="1a21a-149">The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations.</span></span> <span data-ttu-id="1a21a-150">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="1a21a-150">Select the Save button to commit any changes.</span></span>

1. <span data-ttu-id="1a21a-151">To enable the Azure AD provisioning service for Jive, change the **Provisioning Status** to **On** in the Settings section</span><span class="sxs-lookup"><span data-stu-id="1a21a-151">To enable the Azure AD provisioning service for Jive, change the **Provisioning Status** to **On** in the Settings section</span></span>

1. <span data-ttu-id="1a21a-152">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="1a21a-152">Click **Save.**</span></span>

<span data-ttu-id="1a21a-153">It starts the initial synchronization of any users and/or groups assigned to Jive in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="1a21a-153">It starts the initial synchronization of any users and/or groups assigned to Jive in the Users and Groups section.</span></span> <span data-ttu-id="1a21a-154">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="1a21a-154">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="1a21a-155">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Jive app.</span><span class="sxs-lookup"><span data-stu-id="1a21a-155">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Jive app.</span></span>

<span data-ttu-id="1a21a-156">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="1a21a-156">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a21a-157">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1a21a-157">Additional resources</span></span>

* [<span data-ttu-id="1a21a-158">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="1a21a-158">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="1a21a-159">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a21a-159">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="1a21a-160">Configure Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="1a21a-160">Configure Single Sign-on</span></span>](jive-tutorial.md)