---
title: 'Tutorial: Configure DocuSign for automatic user provisioning with Azure Active Directory| Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and DocuSign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: 6099c07a0f27966eb4c253b85d24afb0561a708b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867835"
---
# <a name="tutorial-configure-docusign-for-automatic-user-provisioning"></a><span data-ttu-id="ccc1c-103">Tutorial: Configure DocuSign for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="ccc1c-103">Tutorial: Configure DocuSign for automatic user provisioning</span></span>

<span data-ttu-id="ccc1c-104">The objective of this tutorial is to show you the steps you need to perform in DocuSign and Azure AD to automatically provision and de-provision user accounts from Azure AD to DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-104">The objective of this tutorial is to show you the steps you need to perform in DocuSign and Azure AD to automatically provision and de-provision user accounts from Azure AD to DocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccc1c-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ccc1c-105">Prerequisites</span></span>

<span data-ttu-id="ccc1c-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="ccc1c-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="ccc1c-107">An Azure Active directory tenant.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="ccc1c-108">A DocuSign single sign-on enabled subscription.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="ccc1c-109">A user account in DocuSign with Team Admin permissions.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-to-docusign"></a><span data-ttu-id="ccc1c-110">Assigning users to DocuSign</span><span class="sxs-lookup"><span data-stu-id="ccc1c-110">Assigning users to DocuSign</span></span>

<span data-ttu-id="ccc1c-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="ccc1c-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="ccc1c-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your DocuSign app.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your DocuSign app.</span></span> <span data-ttu-id="ccc1c-114">Once decided, you can assign these users to your DocuSign app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="ccc1c-114">Once decided, you can assign these users to your DocuSign app by following the instructions here:</span></span>

[<span data-ttu-id="ccc1c-115">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="ccc1c-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-docusign"></a><span data-ttu-id="ccc1c-116">Important tips for assigning users to DocuSign</span><span class="sxs-lookup"><span data-stu-id="ccc1c-116">Important tips for assigning users to DocuSign</span></span>

*   <span data-ttu-id="ccc1c-117">It is recommended that a single Azure AD user is assigned to DocuSign to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-117">It is recommended that a single Azure AD user is assigned to DocuSign to test the provisioning configuration.</span></span> <span data-ttu-id="ccc1c-118">Additional users may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-118">Additional users may be assigned later.</span></span>

*   <span data-ttu-id="ccc1c-119">When assigning a user to DocuSign, you must select a valid user role.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-119">When assigning a user to DocuSign, you must select a valid user role.</span></span> <span data-ttu-id="ccc1c-120">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-120">The "Default Access" role does not work for provisioning.</span></span>

> [!NOTE]
> <span data-ttu-id="ccc1c-121">Azure AD does not support group provisioning with the Docusign application, only users can be provisioned.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-121">Azure AD does not support group provisioning with the Docusign application, only users can be provisioned.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="ccc1c-122">Enable User Provisioning</span><span class="sxs-lookup"><span data-stu-id="ccc1c-122">Enable User Provisioning</span></span>

<span data-ttu-id="ccc1c-123">This section guides you through connecting your Azure AD to DocuSign's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-123">This section guides you through connecting your Azure AD to DocuSign's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="ccc1c-124">You may also choose to enabled SAML-based Single Sign-On for DocuSign, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ccc1c-124">You may also choose to enabled SAML-based Single Sign-On for DocuSign, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ccc1c-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="ccc1c-126">To configure user account provisioning:</span><span class="sxs-lookup"><span data-stu-id="ccc1c-126">To configure user account provisioning:</span></span>

<span data-ttu-id="ccc1c-127">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-127">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to DocuSign.</span></span>

1. <span data-ttu-id="ccc1c-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

1. <span data-ttu-id="ccc1c-129">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using the search field.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-129">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using the search field.</span></span> <span data-ttu-id="ccc1c-130">Otherwise, select **Add** and search for **DocuSign** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-130">Otherwise, select **Add** and search for **DocuSign** in the application gallery.</span></span> <span data-ttu-id="ccc1c-131">Select DocuSign from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-131">Select DocuSign from the search results, and add it to your list of applications.</span></span>

1. <span data-ttu-id="ccc1c-132">Select your instance of DocuSign, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-132">Select your instance of DocuSign, then select the **Provisioning** tab.</span></span>

1. <span data-ttu-id="ccc1c-133">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-133">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisioning](./media/docusign-provisioning-tutorial/provisioning.png)

1. <span data-ttu-id="ccc1c-135">Under the **Admin Credentials** section, provide the following configuration settings:</span><span class="sxs-lookup"><span data-stu-id="ccc1c-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="ccc1c-136">a.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-136">a.</span></span> <span data-ttu-id="ccc1c-137">In the **Admin User Name** textbox, type a DocuSign account name that has the **System Administrator** profile in DocuSign.com assigned.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-137">In the **Admin User Name** textbox, type a DocuSign account name that has the **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="ccc1c-138">b.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-138">b.</span></span> <span data-ttu-id="ccc1c-139">In the **Admin Password** textbox, type the password for this account.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-139">In the **Admin Password** textbox, type the password for this account.</span></span>

1. <span data-ttu-id="ccc1c-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your DocuSign app.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your DocuSign app.</span></span>

1. <span data-ttu-id="ccc1c-141">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-141">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

1. <span data-ttu-id="ccc1c-142">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="ccc1c-142">Click **Save.**</span></span>

1. <span data-ttu-id="ccc1c-143">Under the Mappings section, select **Synchronize Azure Active Directory Users to DocuSign.**</span><span class="sxs-lookup"><span data-stu-id="ccc1c-143">Under the Mappings section, select **Synchronize Azure Active Directory Users to DocuSign.**</span></span>

1. <span data-ttu-id="ccc1c-144">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-144">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to DocuSign.</span></span> <span data-ttu-id="ccc1c-145">The attributes selected as **Matching** properties are used to match the user accounts in DocuSign for update operations.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-145">The attributes selected as **Matching** properties are used to match the user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="ccc1c-146">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-146">Select the Save button to commit any changes.</span></span>

1. <span data-ttu-id="ccc1c-147">To enable the Azure AD provisioning service for DocuSign, change the **Provisioning Status** to **On** in the Settings section</span><span class="sxs-lookup"><span data-stu-id="ccc1c-147">To enable the Azure AD provisioning service for DocuSign, change the **Provisioning Status** to **On** in the Settings section</span></span>

1. <span data-ttu-id="ccc1c-148">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="ccc1c-148">Click **Save.**</span></span>

<span data-ttu-id="ccc1c-149">It starts the initial synchronization of any users assigned to DocuSign in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-149">It starts the initial synchronization of any users assigned to DocuSign in the Users and Groups section.</span></span> <span data-ttu-id="ccc1c-150">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-150">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="ccc1c-151">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your DocuSign app.</span><span class="sxs-lookup"><span data-stu-id="ccc1c-151">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="ccc1c-152">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="ccc1c-152">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ccc1c-153">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ccc1c-153">Additional resources</span></span>

* [<span data-ttu-id="ccc1c-154">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="ccc1c-154">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="ccc1c-155">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ccc1c-155">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="ccc1c-156">Configure Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="ccc1c-156">Configure Single Sign-on</span></span>](docusign-tutorial.md)