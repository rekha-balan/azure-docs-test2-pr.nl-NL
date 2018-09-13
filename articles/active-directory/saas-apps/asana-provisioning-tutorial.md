---
title: 'Tutorial: Configure Asana for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Asana.
services: active-directory
documentationcenter: ''
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: 0b38ee73-168b-42cb-bd8b-9c5e5126d648
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: asmalser
ms.reviewer: asmalser
ms.openlocfilehash: 26642fefbb86b2709e110b13d782286fd18d5e60
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856588"
---
# <a name="tutorial-configure-asana-for-automatic-user-provisioning"></a><span data-ttu-id="6b1b8-103">Tutorial: Configure Asana for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="6b1b8-103">Tutorial: Configure Asana for automatic user provisioning</span></span>

<span data-ttu-id="6b1b8-104">The objective of this tutorial is to show you the steps you need to perform in Asana and Azure Active Directory (Azure AD) to automatically provision and de-provision user accounts from Azure AD to Asana.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-104">The objective of this tutorial is to show you the steps you need to perform in Asana and Azure Active Directory (Azure AD) to automatically provision and de-provision user accounts from Azure AD to Asana.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b1b8-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6b1b8-105">Prerequisites</span></span>

<span data-ttu-id="6b1b8-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="6b1b8-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="6b1b8-107">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="6b1b8-107">An Azure AD tenant</span></span>
*   <span data-ttu-id="6b1b8-108">An Asana tenant with an [Enterprise](https://www.asana.com/pricing) plan or better enabled</span><span class="sxs-lookup"><span data-stu-id="6b1b8-108">An Asana tenant with an [Enterprise](https://www.asana.com/pricing) plan or better enabled</span></span> 
*   <span data-ttu-id="6b1b8-109">A user account in Asana with admin permissions</span><span class="sxs-lookup"><span data-stu-id="6b1b8-109">A user account in Asana with admin permissions</span></span> 

> [!NOTE] 
> <span data-ttu-id="6b1b8-110">Azure AD provisioning integration relies on the [Asana API](https://asana.com/developers/api-reference/users), which is available to Asana.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-110">Azure AD provisioning integration relies on the [Asana API](https://asana.com/developers/api-reference/users), which is available to Asana.</span></span>

## <a name="assign-users-to-asana"></a><span data-ttu-id="6b1b8-111">Assign users to Asana</span><span class="sxs-lookup"><span data-stu-id="6b1b8-111">Assign users to Asana</span></span>

<span data-ttu-id="6b1b8-112">Azure AD uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-112">Azure AD uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="6b1b8-113">In the context of automatic user account provisioning, only the users assigned to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-113">In the context of automatic user account provisioning, only the users assigned to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="6b1b8-114">Before you configure and enable the provisioning service, you must decide which users in Azure AD need access to your Asana app.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-114">Before you configure and enable the provisioning service, you must decide which users in Azure AD need access to your Asana app.</span></span> <span data-ttu-id="6b1b8-115">Then you can assign these users to your Asana app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="6b1b8-115">Then you can assign these users to your Asana app by following the instructions here:</span></span>

[<span data-ttu-id="6b1b8-116">Assign a user to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="6b1b8-116">Assign a user to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-asana"></a><span data-ttu-id="6b1b8-117">Important tips for assigning users to Asana</span><span class="sxs-lookup"><span data-stu-id="6b1b8-117">Important tips for assigning users to Asana</span></span>

<span data-ttu-id="6b1b8-118">We recommend that you assign a single Azure AD user to Asana to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-118">We recommend that you assign a single Azure AD user to Asana to test the provisioning configuration.</span></span> <span data-ttu-id="6b1b8-119">Additional users can be assigned later.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-119">Additional users can be assigned later.</span></span>

## <a name="configure-user-provisioning-to-asana"></a><span data-ttu-id="6b1b8-120">Configure user provisioning to Asana</span><span class="sxs-lookup"><span data-stu-id="6b1b8-120">Configure user provisioning to Asana</span></span> 

<span data-ttu-id="6b1b8-121">This section guides you through connecting your Azure AD to Asana user account provisioning API.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-121">This section guides you through connecting your Azure AD to Asana user account provisioning API.</span></span> <span data-ttu-id="6b1b8-122">You also configure the provisioning service to create, update, and disable assigned user accounts in Asana based on user assignments in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-122">You also configure the provisioning service to create, update, and disable assigned user accounts in Asana based on user assignments in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="6b1b8-123">To enable SAML-based single sign-on for Asana, follow the instructions provided in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6b1b8-123">To enable SAML-based single sign-on for Asana, follow the instructions provided in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6b1b8-124">Single sign-on can be configured independently of automatic provisioning, although these two features complement each other.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-124">Single sign-on can be configured independently of automatic provisioning, although these two features complement each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning-to-asana-in-azure-ad"></a><span data-ttu-id="6b1b8-125">To configure automatic user account provisioning to Asana in Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b1b8-125">To configure automatic user account provisioning to Asana in Azure AD</span></span>

1. <span data-ttu-id="6b1b8-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

1. <span data-ttu-id="6b1b8-127">If you already configured Asana for single sign-on, search for your instance of Asana by using the search field.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-127">If you already configured Asana for single sign-on, search for your instance of Asana by using the search field.</span></span> <span data-ttu-id="6b1b8-128">Otherwise, select **Add** and search for **Asana** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-128">Otherwise, select **Add** and search for **Asana** in the application gallery.</span></span> <span data-ttu-id="6b1b8-129">Select **Asana** from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-129">Select **Asana** from the search results, and add it to your list of applications.</span></span>

1. <span data-ttu-id="6b1b8-130">Select your instance of Asana, and then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-130">Select your instance of Asana, and then select the **Provisioning** tab.</span></span>

1. <span data-ttu-id="6b1b8-131">Set **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-131">Set **Provisioning Mode** to **Automatic**.</span></span>

    ![Asana Provisioning](./media/asana-provisioning-tutorial/asanaazureprovisioning.png)

1. <span data-ttu-id="6b1b8-133">Under the **Admin Credentials** section, follow these instructions to generate the token and enter it in  **Secret Token**:</span><span class="sxs-lookup"><span data-stu-id="6b1b8-133">Under the **Admin Credentials** section, follow these instructions to generate the token and enter it in  **Secret Token**:</span></span>

    <span data-ttu-id="6b1b8-134">a.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-134">a.</span></span> <span data-ttu-id="6b1b8-135">Sign in to [Asana](https://app.asana.com) by using your admin account.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-135">Sign in to [Asana](https://app.asana.com) by using your admin account.</span></span>

    <span data-ttu-id="6b1b8-136">b.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-136">b.</span></span> <span data-ttu-id="6b1b8-137">Select the profile photo from the top bar, and select your current organization-name settings.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-137">Select the profile photo from the top bar, and select your current organization-name settings.</span></span>

    <span data-ttu-id="6b1b8-138">c.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-138">c.</span></span> <span data-ttu-id="6b1b8-139">Go to the **Service Accounts** tab.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-139">Go to the **Service Accounts** tab.</span></span>

    <span data-ttu-id="6b1b8-140">d.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-140">d.</span></span> <span data-ttu-id="6b1b8-141">Select **Add Service Account**.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-141">Select **Add Service Account**.</span></span>

    <span data-ttu-id="6b1b8-142">e.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-142">e.</span></span> <span data-ttu-id="6b1b8-143">Update **Name** and **About** and the profile photo as needed.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-143">Update **Name** and **About** and the profile photo as needed.</span></span> <span data-ttu-id="6b1b8-144">Copy the token in **Token**, and select it in **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-144">Copy the token in **Token**, and select it in **Save Changes**.</span></span>

1. <span data-ttu-id="6b1b8-145">In the Azure portal, select **Test Connection** to ensure that Azure AD can connect to your Asana app.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-145">In the Azure portal, select **Test Connection** to ensure that Azure AD can connect to your Asana app.</span></span> <span data-ttu-id="6b1b8-146">If the connection fails, ensure that your Asana account has admin permissions, and try the **Test Connection** step again.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-146">If the connection fails, ensure that your Asana account has admin permissions, and try the **Test Connection** step again.</span></span>

1. <span data-ttu-id="6b1b8-147">Enter the email address of a person or group that you want to receive provisioning error notifications in  **Notification Email**.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-147">Enter the email address of a person or group that you want to receive provisioning error notifications in  **Notification Email**.</span></span> <span data-ttu-id="6b1b8-148">Select the check box underneath.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-148">Select the check box underneath.</span></span>

1. <span data-ttu-id="6b1b8-149">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-149">Select **Save**.</span></span> 

1. <span data-ttu-id="6b1b8-150">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Asana**.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-150">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Asana**.</span></span>

1. <span data-ttu-id="6b1b8-151">In the **Attribute Mappings** section, review the user attributes to be synchronized from Azure AD to Asana.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-151">In the **Attribute Mappings** section, review the user attributes to be synchronized from Azure AD to Asana.</span></span> <span data-ttu-id="6b1b8-152">The attributes selected as **Matching** properties are used to match the user accounts in Asana for update operations.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-152">The attributes selected as **Matching** properties are used to match the user accounts in Asana for update operations.</span></span> <span data-ttu-id="6b1b8-153">Select **Save** to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-153">Select **Save** to commit any changes.</span></span> <span data-ttu-id="6b1b8-154">For more information, see [Customize user provision attribute mappings](../manage-apps/customize-application-attributes.md).</span><span class="sxs-lookup"><span data-stu-id="6b1b8-154">For more information, see [Customize user provision attribute mappings](../manage-apps/customize-application-attributes.md).</span></span>

1. <span data-ttu-id="6b1b8-155">To enable the Azure AD provisioning service for Asana, in the **Settings** section, change **Provisioning Status** to **On**.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-155">To enable the Azure AD provisioning service for Asana, in the **Settings** section, change **Provisioning Status** to **On**.</span></span>

1. <span data-ttu-id="6b1b8-156">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-156">Select **Save**.</span></span> 

<span data-ttu-id="6b1b8-157">Now the initial synchronization starts for any users assigned to Asana in the **Users** section.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-157">Now the initial synchronization starts for any users assigned to Asana in the **Users** section.</span></span> <span data-ttu-id="6b1b8-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="6b1b8-159">Use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-159">Use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs.</span></span> <span data-ttu-id="6b1b8-160">The audit logs describe all actions performed by the provisioning service on your Asana app.</span><span class="sxs-lookup"><span data-stu-id="6b1b8-160">The audit logs describe all actions performed by the provisioning service on your Asana app.</span></span>

<span data-ttu-id="6b1b8-161">For more information on how to read the Azure AD provisioning logs, see [Report on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="6b1b8-161">For more information on how to read the Azure AD provisioning logs, see [Report on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b1b8-162">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6b1b8-162">Additional resources</span></span>

* [<span data-ttu-id="6b1b8-163">Manage user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="6b1b8-163">Manage user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="6b1b8-164">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b1b8-164">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="6b1b8-165">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="6b1b8-165">Configure single sign-on</span></span>](asana-tutorial.md)
