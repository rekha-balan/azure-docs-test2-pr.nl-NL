---
title: 'Tutorial: Configure GoToMeeting for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: 3d2dafd409c6c7b2be06a6f18c3d392aff681efe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856436"
---
# <a name="tutorial-configure-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="6d95b-103">Tutorial: Configure GoToMeeting for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="6d95b-103">Tutorial: Configure GoToMeeting for automatic user provisioning</span></span>

<span data-ttu-id="6d95b-104">The objective of this tutorial is to show you the steps you need to perform in GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="6d95b-104">The objective of this tutorial is to show you the steps you need to perform in GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d95b-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6d95b-105">Prerequisites</span></span>

<span data-ttu-id="6d95b-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="6d95b-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="6d95b-107">An Azure Active directory tenant.</span><span class="sxs-lookup"><span data-stu-id="6d95b-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="6d95b-108">A GoToMeeting single  sign-on enabled subscription.</span><span class="sxs-lookup"><span data-stu-id="6d95b-108">A GoToMeeting single  sign-on enabled subscription.</span></span>
*   <span data-ttu-id="6d95b-109">A user account in GoToMeeting with Team Admin permissions.</span><span class="sxs-lookup"><span data-stu-id="6d95b-109">A user account in GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-to-gotomeeting"></a><span data-ttu-id="6d95b-110">Assigning users to GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="6d95b-110">Assigning users to GoToMeeting</span></span>

<span data-ttu-id="6d95b-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="6d95b-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="6d95b-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span><span class="sxs-lookup"><span data-stu-id="6d95b-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="6d95b-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your GoToMeeting app.</span><span class="sxs-lookup"><span data-stu-id="6d95b-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your GoToMeeting app.</span></span> <span data-ttu-id="6d95b-114">Once decided, you can assign these users to your GoToMeeting app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="6d95b-114">Once decided, you can assign these users to your GoToMeeting app by following the instructions here:</span></span>

[<span data-ttu-id="6d95b-115">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="6d95b-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-gotomeeting"></a><span data-ttu-id="6d95b-116">Important tips for assigning users to GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="6d95b-116">Important tips for assigning users to GoToMeeting</span></span>

*   <span data-ttu-id="6d95b-117">It is recommended that a single Azure AD user is assigned to GoToMeeting to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="6d95b-117">It is recommended that a single Azure AD user is assigned to GoToMeeting to test the provisioning configuration.</span></span> <span data-ttu-id="6d95b-118">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="6d95b-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="6d95b-119">When assigning a user to GoToMeeting, you must select a valid user role.</span><span class="sxs-lookup"><span data-stu-id="6d95b-119">When assigning a user to GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="6d95b-120">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="6d95b-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="6d95b-121">Enable Automated User Provisioning</span><span class="sxs-lookup"><span data-stu-id="6d95b-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="6d95b-122">This section guides you through connecting your Azure AD to GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in GoToMeeting based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d95b-122">This section guides you through connecting your Azure AD to GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="6d95b-123">You may also choose to enabled SAML-based Single Sign-On for GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6d95b-123">You may also choose to enabled SAML-based Single Sign-On for GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6d95b-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="6d95b-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="6d95b-125">To configure automatic user account provisioning:</span><span class="sxs-lookup"><span data-stu-id="6d95b-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="6d95b-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span><span class="sxs-lookup"><span data-stu-id="6d95b-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

1. <span data-ttu-id="6d95b-127">If you have already configured GoToMeeting for single sign-on, search for your instance of GoToMeeting using the search field.</span><span class="sxs-lookup"><span data-stu-id="6d95b-127">If you have already configured GoToMeeting for single sign-on, search for your instance of GoToMeeting using the search field.</span></span> <span data-ttu-id="6d95b-128">Otherwise, select **Add** and search for **GoToMeeting** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="6d95b-128">Otherwise, select **Add** and search for **GoToMeeting** in the application gallery.</span></span> <span data-ttu-id="6d95b-129">Select GoToMeeting from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="6d95b-129">Select GoToMeeting from the search results, and add it to your list of applications.</span></span>

1. <span data-ttu-id="6d95b-130">Select your instance of GoToMeeting, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="6d95b-130">Select your instance of GoToMeeting, then select the **Provisioning** tab.</span></span>

1. <span data-ttu-id="6d95b-131">Set the **Provisioning** Mode to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="6d95b-131">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![provisioning](./media/citrixgotomeeting-provisioning-tutorial/provisioning.png)

1. <span data-ttu-id="6d95b-133">Under the Admin Credentials section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6d95b-133">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="6d95b-134">a.</span><span class="sxs-lookup"><span data-stu-id="6d95b-134">a.</span></span> <span data-ttu-id="6d95b-135">In the **GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span><span class="sxs-lookup"><span data-stu-id="6d95b-135">In the **GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="6d95b-136">b.</span><span class="sxs-lookup"><span data-stu-id="6d95b-136">b.</span></span> <span data-ttu-id="6d95b-137">In the **GoToMeeting Admin Password** textbox, the administrator's password.</span><span class="sxs-lookup"><span data-stu-id="6d95b-137">In the **GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

1. <span data-ttu-id="6d95b-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your GoToMeeting app.</span><span class="sxs-lookup"><span data-stu-id="6d95b-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your GoToMeeting app.</span></span> <span data-ttu-id="6d95b-139">If the connection fails, ensure your GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span><span class="sxs-lookup"><span data-stu-id="6d95b-139">If the connection fails, ensure your GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

1. <span data-ttu-id="6d95b-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span><span class="sxs-lookup"><span data-stu-id="6d95b-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

1. <span data-ttu-id="6d95b-141">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="6d95b-141">Click **Save.**</span></span>

1. <span data-ttu-id="6d95b-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="6d95b-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to GoToMeeting.**</span></span>

1. <span data-ttu-id="6d95b-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="6d95b-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to GoToMeeting.</span></span> <span data-ttu-id="6d95b-144">The attributes selected as **Matching** properties are used to match the user accounts in GoToMeeting for update operations.</span><span class="sxs-lookup"><span data-stu-id="6d95b-144">The attributes selected as **Matching** properties are used to match the user accounts in GoToMeeting for update operations.</span></span> <span data-ttu-id="6d95b-145">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="6d95b-145">Select the Save button to commit any changes.</span></span>

1. <span data-ttu-id="6d95b-146">To enable the Azure AD provisioning service for GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span><span class="sxs-lookup"><span data-stu-id="6d95b-146">To enable the Azure AD provisioning service for GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span></span>

1. <span data-ttu-id="6d95b-147">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="6d95b-147">Click **Save.**</span></span>

<span data-ttu-id="6d95b-148">It starts the initial synchronization of any users and/or groups assigned to GoToMeeting in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="6d95b-148">It starts the initial synchronization of any users and/or groups assigned to GoToMeeting in the Users and Groups section.</span></span> <span data-ttu-id="6d95b-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="6d95b-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="6d95b-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your GoToMeeting app.</span><span class="sxs-lookup"><span data-stu-id="6d95b-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your GoToMeeting app.</span></span>

<span data-ttu-id="6d95b-151">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="6d95b-151">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6d95b-152">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6d95b-152">Additional resources</span></span>

* [<span data-ttu-id="6d95b-153">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="6d95b-153">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="6d95b-154">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6d95b-154">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="6d95b-155">Configure Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="6d95b-155">Configure Single Sign-on</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-citrix-gotomeeting-tutorial)


