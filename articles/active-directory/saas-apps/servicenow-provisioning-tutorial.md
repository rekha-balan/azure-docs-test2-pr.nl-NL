---
title: 'Tutorial: Configure ServiceNow for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to automatically provision and de-provision user accounts from Azure AD to ServiceNow.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 4d6f06dd-a798-4c22-b84f-8a11f1b8592a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: b3ef6e2a6b9b51c271372aa3c9342b52a4260788
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857831"
---
# <a name="tutorial-configure-servicenow-for-automatic-user-provisioning-with-azure-active-directory"></a><span data-ttu-id="fb287-103">Tutorial: Configure ServiceNow for automatic user provisioning with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb287-103">Tutorial: Configure ServiceNow for automatic user provisioning with Azure Active Directory</span></span>

<span data-ttu-id="fb287-104">The objective of this tutorial is to show you the steps you need to perform in ServiceNow and Azure AD to automatically provision and de-provision user accounts from Azure AD to ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="fb287-104">The objective of this tutorial is to show you the steps you need to perform in ServiceNow and Azure AD to automatically provision and de-provision user accounts from Azure AD to ServiceNow.</span></span>

> [!NOTE]
> <span data-ttu-id="fb287-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="fb287-105">This tutorial describes a connector built on top of the Azure AD User Provisioning Service.</span></span> <span data-ttu-id="fb287-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="fb287-106">For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb287-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fb287-107">Prerequisites</span></span>

<span data-ttu-id="fb287-108">To configure Azure AD integration with ServiceNow, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="fb287-108">To configure Azure AD integration with ServiceNow, you need the following items:</span></span>

- <span data-ttu-id="fb287-109">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="fb287-109">An Azure AD subscription</span></span>
- <span data-ttu-id="fb287-110">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span><span class="sxs-lookup"><span data-stu-id="fb287-110">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
- <span data-ttu-id="fb287-111">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span><span class="sxs-lookup"><span data-stu-id="fb287-111">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>

> [!NOTE]
> <span data-ttu-id="fb287-112">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="fb287-112">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb287-113">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="fb287-113">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb287-114">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="fb287-114">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb287-115">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb287-115">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="assigning-users-to-servicenow"></a><span data-ttu-id="fb287-116">Assigning users to ServiceNow</span><span class="sxs-lookup"><span data-stu-id="fb287-116">Assigning users to ServiceNow</span></span>

<span data-ttu-id="fb287-117">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="fb287-117">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="fb287-118">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span><span class="sxs-lookup"><span data-stu-id="fb287-118">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="fb287-119">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ServiceNow app.</span><span class="sxs-lookup"><span data-stu-id="fb287-119">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ServiceNow app.</span></span> <span data-ttu-id="fb287-120">Once decided, you can assign these users to your ServiceNow app by following the instructions here: [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="fb287-120">Once decided, you can assign these users to your ServiceNow app by following the instructions here: [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>


> [!IMPORTANT]
>*   <span data-ttu-id="fb287-121">It is recommended that a single Azure AD user is assigned to ServiceNow to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="fb287-121">It is recommended that a single Azure AD user is assigned to ServiceNow to test the provisioning configuration.</span></span> <span data-ttu-id="fb287-122">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="fb287-122">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="fb287-123">When assigning a user to ServiceNow, you must select a valid user role.</span><span class="sxs-lookup"><span data-stu-id="fb287-123">When assigning a user to ServiceNow, you must select a valid user role.</span></span> <span data-ttu-id="fb287-124">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="fb287-124">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="fb287-125">Enable automated user provisioning</span><span class="sxs-lookup"><span data-stu-id="fb287-125">Enable automated user provisioning</span></span>

<span data-ttu-id="fb287-126">This section guides you through connecting your Azure AD to ServiceNow's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ServiceNow based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb287-126">This section guides you through connecting your Azure AD to ServiceNow's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ServiceNow based on user and group assignment in Azure AD.</span></span>

> [!TIP]
><span data-ttu-id="fb287-127">You may also choose to enabled SAML-based Single Sign-On for ServiceNow, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb287-127">You may also choose to enabled SAML-based Single Sign-On for ServiceNow, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fb287-128">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="fb287-128">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="fb287-129">Configure automatic user account provisioning</span><span class="sxs-lookup"><span data-stu-id="fb287-129">Configure automatic user account provisioning</span></span>

1. <span data-ttu-id="fb287-130">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span><span class="sxs-lookup"><span data-stu-id="fb287-130">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

1. <span data-ttu-id="fb287-131">If you have already configured ServiceNow for single sign-on, search for your instance of ServiceNow using the search field.</span><span class="sxs-lookup"><span data-stu-id="fb287-131">If you have already configured ServiceNow for single sign-on, search for your instance of ServiceNow using the search field.</span></span> <span data-ttu-id="fb287-132">Otherwise, select **Add** and search for **ServiceNow** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="fb287-132">Otherwise, select **Add** and search for **ServiceNow** in the application gallery.</span></span> <span data-ttu-id="fb287-133">Select ServiceNow from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="fb287-133">Select ServiceNow from the search results, and add it to your list of applications.</span></span>

1. <span data-ttu-id="fb287-134">Select your instance of ServiceNow, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="fb287-134">Select your instance of ServiceNow, then select the **Provisioning** tab.</span></span>

1. <span data-ttu-id="fb287-135">Set the **Provisioning** Mode to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="fb287-135">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![provisioning](./media/servicenow-provisioning-tutorial/provisioning.png)

1. <span data-ttu-id="fb287-137">Under the Admin Credentials section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fb287-137">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="fb287-138">a.</span><span class="sxs-lookup"><span data-stu-id="fb287-138">a.</span></span> <span data-ttu-id="fb287-139">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span><span class="sxs-lookup"><span data-stu-id="fb287-139">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span></span>

    <span data-ttu-id="fb287-140">b.</span><span class="sxs-lookup"><span data-stu-id="fb287-140">b.</span></span> <span data-ttu-id="fb287-141">In the **ServiceNow Admin User Name** textbox, type the user name of an administrator.</span><span class="sxs-lookup"><span data-stu-id="fb287-141">In the **ServiceNow Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="fb287-142">c.</span><span class="sxs-lookup"><span data-stu-id="fb287-142">c.</span></span> <span data-ttu-id="fb287-143">In the **ServiceNow Admin Password** textbox, the administrator's password.</span><span class="sxs-lookup"><span data-stu-id="fb287-143">In the **ServiceNow Admin Password** textbox, the administrator's password.</span></span>

1. <span data-ttu-id="fb287-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ServiceNow app.</span><span class="sxs-lookup"><span data-stu-id="fb287-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ServiceNow app.</span></span> <span data-ttu-id="fb287-145">If the connection fails, ensure your ServiceNow account has Team Admin permissions and try the **"Admin Credentials"** step again.</span><span class="sxs-lookup"><span data-stu-id="fb287-145">If the connection fails, ensure your ServiceNow account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

1. <span data-ttu-id="fb287-146">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span><span class="sxs-lookup"><span data-stu-id="fb287-146">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

1. <span data-ttu-id="fb287-147">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="fb287-147">Click **Save.**</span></span>

1. <span data-ttu-id="fb287-148">Under the Mappings section, select **Synchronize Azure Active Directory Users to ServiceNow.**</span><span class="sxs-lookup"><span data-stu-id="fb287-148">Under the Mappings section, select **Synchronize Azure Active Directory Users to ServiceNow.**</span></span>

1. <span data-ttu-id="fb287-149">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="fb287-149">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ServiceNow.</span></span> <span data-ttu-id="fb287-150">The attributes selected as **Matching** properties are used to match the user accounts in ServiceNow for update operations.</span><span class="sxs-lookup"><span data-stu-id="fb287-150">The attributes selected as **Matching** properties are used to match the user accounts in ServiceNow for update operations.</span></span> <span data-ttu-id="fb287-151">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="fb287-151">Select the Save button to commit any changes.</span></span>

1. <span data-ttu-id="fb287-152">To enable the Azure AD provisioning service for ServiceNow, change the **Provisioning Status** to **On** in the Settings section</span><span class="sxs-lookup"><span data-stu-id="fb287-152">To enable the Azure AD provisioning service for ServiceNow, change the **Provisioning Status** to **On** in the Settings section</span></span>

1. <span data-ttu-id="fb287-153">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="fb287-153">Click **Save.**</span></span>

<span data-ttu-id="fb287-154">It starts the initial synchronization of any users and/or groups assigned to ServiceNow in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="fb287-154">It starts the initial synchronization of any users and/or groups assigned to ServiceNow in the Users and Groups section.</span></span> <span data-ttu-id="fb287-155">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="fb287-155">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="fb287-156">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your ServiceNow app.</span><span class="sxs-lookup"><span data-stu-id="fb287-156">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service on your ServiceNow app.</span></span>

<span data-ttu-id="fb287-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="fb287-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb287-158">Additional resources</span><span class="sxs-lookup"><span data-stu-id="fb287-158">Additional resources</span></span>

* [<span data-ttu-id="fb287-159">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="fb287-159">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="fb287-160">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb287-160">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="fb287-161">Configure Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="fb287-161">Configure Single Sign-on</span></span>](servicenow-tutorial.md)


