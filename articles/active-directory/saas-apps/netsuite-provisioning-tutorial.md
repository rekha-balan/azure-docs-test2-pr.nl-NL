---
title: 'Tutorial: Configure Netsuite for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: e14f74f3dd6d49b882dedcb2ae01029a50a459a3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864441"
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="8b6da-103">Tutorial: Configuring Netsuite for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="8b6da-103">Tutorial: Configuring Netsuite for automatic user provisioning</span></span>

<span data-ttu-id="8b6da-104">The objective of this tutorial is to show you the steps you need to perform in Netsuite and Azure AD to automatically provision and de-provision user accounts from Azure AD to Netsuite.</span><span class="sxs-lookup"><span data-stu-id="8b6da-104">The objective of this tutorial is to show you the steps you need to perform in Netsuite and Azure AD to automatically provision and de-provision user accounts from Azure AD to Netsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b6da-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8b6da-105">Prerequisites</span></span>

<span data-ttu-id="8b6da-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="8b6da-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="8b6da-107">An Azure Active directory tenant.</span><span class="sxs-lookup"><span data-stu-id="8b6da-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="8b6da-108">A Netsuite single-sign on enabled subscription.</span><span class="sxs-lookup"><span data-stu-id="8b6da-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="8b6da-109">A user account in Netsuite with Team Admin permissions.</span><span class="sxs-lookup"><span data-stu-id="8b6da-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-to-netsuite"></a><span data-ttu-id="8b6da-110">Assigning users to Netsuite</span><span class="sxs-lookup"><span data-stu-id="8b6da-110">Assigning users to Netsuite</span></span>

<span data-ttu-id="8b6da-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="8b6da-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="8b6da-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="8b6da-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="8b6da-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Netsuite app.</span><span class="sxs-lookup"><span data-stu-id="8b6da-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Netsuite app.</span></span> <span data-ttu-id="8b6da-114">Once decided, you can assign these users to your Netsuite app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="8b6da-114">Once decided, you can assign these users to your Netsuite app by following the instructions here:</span></span>

[<span data-ttu-id="8b6da-115">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="8b6da-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-netsuite"></a><span data-ttu-id="8b6da-116">Important tips for assigning users to Netsuite</span><span class="sxs-lookup"><span data-stu-id="8b6da-116">Important tips for assigning users to Netsuite</span></span>

*   <span data-ttu-id="8b6da-117">It is recommended that a single Azure AD user is assigned to Netsuite to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="8b6da-117">It is recommended that a single Azure AD user is assigned to Netsuite to test the provisioning configuration.</span></span> <span data-ttu-id="8b6da-118">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="8b6da-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="8b6da-119">When assigning a user to Netsuite, you must select a valid user role.</span><span class="sxs-lookup"><span data-stu-id="8b6da-119">When assigning a user to Netsuite, you must select a valid user role.</span></span> <span data-ttu-id="8b6da-120">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="8b6da-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="8b6da-121">Enable User Provisioning</span><span class="sxs-lookup"><span data-stu-id="8b6da-121">Enable User Provisioning</span></span>

<span data-ttu-id="8b6da-122">This section guides you through connecting your Azure AD to Netsuite's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b6da-122">This section guides you through connecting your Azure AD to Netsuite's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="8b6da-123">You may also choose to enabled SAML-based Single Sign-On for Netsuite, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b6da-123">You may also choose to enabled SAML-based Single Sign-On for Netsuite, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8b6da-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="8b6da-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="8b6da-125">To configure user account provisioning:</span><span class="sxs-lookup"><span data-stu-id="8b6da-125">To configure user account provisioning:</span></span>

<span data-ttu-id="8b6da-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Netsuite.</span><span class="sxs-lookup"><span data-stu-id="8b6da-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Netsuite.</span></span>

1. <span data-ttu-id="8b6da-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span><span class="sxs-lookup"><span data-stu-id="8b6da-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

1. <span data-ttu-id="8b6da-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using the search field.</span><span class="sxs-lookup"><span data-stu-id="8b6da-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using the search field.</span></span> <span data-ttu-id="8b6da-129">Otherwise, select **Add** and search for **Netsuite** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="8b6da-129">Otherwise, select **Add** and search for **Netsuite** in the application gallery.</span></span> <span data-ttu-id="8b6da-130">Select Netsuite from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="8b6da-130">Select Netsuite from the search results, and add it to your list of applications.</span></span>

1. <span data-ttu-id="8b6da-131">Select your instance of Netsuite, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="8b6da-131">Select your instance of Netsuite, then select the **Provisioning** tab.</span></span>

1. <span data-ttu-id="8b6da-132">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="8b6da-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisioning](./media/netsuite-provisioning-tutorial/provisioning.png)

1. <span data-ttu-id="8b6da-134">Under the **Admin Credentials** section, provide the following configuration settings:</span><span class="sxs-lookup"><span data-stu-id="8b6da-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="8b6da-135">a.</span><span class="sxs-lookup"><span data-stu-id="8b6da-135">a.</span></span> <span data-ttu-id="8b6da-136">In the **Admin User Name** textbox, type a Netsuite account name that has the **System Administrator** profile in Netsuite.com assigned.</span><span class="sxs-lookup"><span data-stu-id="8b6da-136">In the **Admin User Name** textbox, type a Netsuite account name that has the **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="8b6da-137">b.</span><span class="sxs-lookup"><span data-stu-id="8b6da-137">b.</span></span> <span data-ttu-id="8b6da-138">In the **Admin Password** textbox, type the password for this account.</span><span class="sxs-lookup"><span data-stu-id="8b6da-138">In the **Admin Password** textbox, type the password for this account.</span></span>
      
1. <span data-ttu-id="8b6da-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Netsuite app.</span><span class="sxs-lookup"><span data-stu-id="8b6da-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Netsuite app.</span></span>

1. <span data-ttu-id="8b6da-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span><span class="sxs-lookup"><span data-stu-id="8b6da-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

1. <span data-ttu-id="8b6da-141">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="8b6da-141">Click **Save.**</span></span>

1. <span data-ttu-id="8b6da-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Netsuite.**</span><span class="sxs-lookup"><span data-stu-id="8b6da-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Netsuite.**</span></span>

1. <span data-ttu-id="8b6da-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Netsuite.</span><span class="sxs-lookup"><span data-stu-id="8b6da-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Netsuite.</span></span> <span data-ttu-id="8b6da-144">Note that the attributes selected as **Matching** properties are used to match the user accounts in Netsuite for update operations.</span><span class="sxs-lookup"><span data-stu-id="8b6da-144">Note that the attributes selected as **Matching** properties are used to match the user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="8b6da-145">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="8b6da-145">Select the Save button to commit any changes.</span></span>

1. <span data-ttu-id="8b6da-146">To enable the Azure AD provisioning service for Netsuite, change the **Provisioning Status** to **On** in the Settings section</span><span class="sxs-lookup"><span data-stu-id="8b6da-146">To enable the Azure AD provisioning service for Netsuite, change the **Provisioning Status** to **On** in the Settings section</span></span>

1. <span data-ttu-id="8b6da-147">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="8b6da-147">Click **Save.**</span></span>

<span data-ttu-id="8b6da-148">It starts the initial synchronization of any users and/or groups assigned to Netsuite in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="8b6da-148">It starts the initial synchronization of any users and/or groups assigned to Netsuite in the Users and Groups section.</span></span> <span data-ttu-id="8b6da-149">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="8b6da-149">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="8b6da-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Netsuite app.</span><span class="sxs-lookup"><span data-stu-id="8b6da-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="8b6da-151">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="8b6da-151">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b6da-152">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8b6da-152">Additional resources</span></span>

* [<span data-ttu-id="8b6da-153">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="8b6da-153">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="8b6da-154">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8b6da-154">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="8b6da-155">Configure Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="8b6da-155">Configure Single Sign-on</span></span>](netsuite-tutorial.md)