---
title: 'Tutorial: Configure Pingboard for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to Pingboard.
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
ms.date: 10/19/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.openlocfilehash: e96ea7d212f1a34bb6d10f8c49a15e1b34bfc469
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856805"
---
# <a name="tutorial-configure-pingboard-for-automatic-user-provisioning"></a><span data-ttu-id="8094a-103">Tutorial: Configure Pingboard for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="8094a-103">Tutorial: Configure Pingboard for automatic user provisioning</span></span>

<span data-ttu-id="8094a-104">The purpose of this tutorial is to show you the steps you need to follow to enable automatic provisioning and de-provisioning of user accounts from Azure Active Directory (Azure AD) to Pingboard.</span><span class="sxs-lookup"><span data-stu-id="8094a-104">The purpose of this tutorial is to show you the steps you need to follow to enable automatic provisioning and de-provisioning of user accounts from Azure Active Directory (Azure AD) to Pingboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8094a-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8094a-105">Prerequisites</span></span>

<span data-ttu-id="8094a-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="8094a-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="8094a-107">An Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="8094a-107">An Azure AD tenant</span></span>
*   <span data-ttu-id="8094a-108">A Pingboard tenant [Pro account](https://pingboard.com/pricing)</span><span class="sxs-lookup"><span data-stu-id="8094a-108">A Pingboard tenant [Pro account](https://pingboard.com/pricing)</span></span> 
*   <span data-ttu-id="8094a-109">A user account in Pingboard with admin permissions</span><span class="sxs-lookup"><span data-stu-id="8094a-109">A user account in Pingboard with admin permissions</span></span> 

> [!NOTE] 
> <span data-ttu-id="8094a-110">Azure AD provisioning integration relies on the [Pingboard API](https://pingboard.docs.apiary.io/#), which is available to your account.</span><span class="sxs-lookup"><span data-stu-id="8094a-110">Azure AD provisioning integration relies on the [Pingboard API](https://pingboard.docs.apiary.io/#), which is available to your account.</span></span>

## <a name="assign-users-to-pingboard"></a><span data-ttu-id="8094a-111">Assign users to Pingboard</span><span class="sxs-lookup"><span data-stu-id="8094a-111">Assign users to Pingboard</span></span>

<span data-ttu-id="8094a-112">Azure AD uses a concept called "assignments" to determine which users should receive access to selected applications.</span><span class="sxs-lookup"><span data-stu-id="8094a-112">Azure AD uses a concept called "assignments" to determine which users should receive access to selected applications.</span></span> <span data-ttu-id="8094a-113">In the context of automatic user account provisioning, only the users assigned to an application in Azure AD are synchronized.</span><span class="sxs-lookup"><span data-stu-id="8094a-113">In the context of automatic user account provisioning, only the users assigned to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="8094a-114">Before you configure and enable the provisioning service, you must decide which users in Azure AD need access to your Pingboard app.</span><span class="sxs-lookup"><span data-stu-id="8094a-114">Before you configure and enable the provisioning service, you must decide which users in Azure AD need access to your Pingboard app.</span></span> <span data-ttu-id="8094a-115">Then you can assign these users to your Pingboard app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="8094a-115">Then you can assign these users to your Pingboard app by following the instructions here:</span></span>

[<span data-ttu-id="8094a-116">Assign a user to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="8094a-116">Assign a user to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-pingboard"></a><span data-ttu-id="8094a-117">Important tips for assigning users to Pingboard</span><span class="sxs-lookup"><span data-stu-id="8094a-117">Important tips for assigning users to Pingboard</span></span>

<span data-ttu-id="8094a-118">We recommend that you assign a single Azure AD user to Pingboard to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="8094a-118">We recommend that you assign a single Azure AD user to Pingboard to test the provisioning configuration.</span></span> <span data-ttu-id="8094a-119">Additional users can be assigned later.</span><span class="sxs-lookup"><span data-stu-id="8094a-119">Additional users can be assigned later.</span></span>

## <a name="configure-user-provisioning-to-pingboard"></a><span data-ttu-id="8094a-120">Configure user provisioning to Pingboard</span><span class="sxs-lookup"><span data-stu-id="8094a-120">Configure user provisioning to Pingboard</span></span> 

<span data-ttu-id="8094a-121">This section guides you through connecting your Azure AD to the Pingboard user account provisioning API.</span><span class="sxs-lookup"><span data-stu-id="8094a-121">This section guides you through connecting your Azure AD to the Pingboard user account provisioning API.</span></span> <span data-ttu-id="8094a-122">You also configure the provisioning service to create, update, and disable assigned user accounts in Pingboard that are based on user assignments in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8094a-122">You also configure the provisioning service to create, update, and disable assigned user accounts in Pingboard that are based on user assignments in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="8094a-123">To enable SAML-based single sign-on for Pingboard, follow the instructions provided in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8094a-123">To enable SAML-based single sign-on for Pingboard, follow the instructions provided in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8094a-124">Single sign-on can be configured independently of automatic provisioning, although these two features complement each other.</span><span class="sxs-lookup"><span data-stu-id="8094a-124">Single sign-on can be configured independently of automatic provisioning, although these two features complement each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning-to-pingboard-in-azure-ad"></a><span data-ttu-id="8094a-125">To configure automatic user account provisioning to Pingboard in Azure AD</span><span class="sxs-lookup"><span data-stu-id="8094a-125">To configure automatic user account provisioning to Pingboard in Azure AD</span></span>

1. <span data-ttu-id="8094a-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span><span class="sxs-lookup"><span data-stu-id="8094a-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

1. <span data-ttu-id="8094a-127">If you already configured Pingboard for single sign-on, search for your instance of Pingboard by using the search field.</span><span class="sxs-lookup"><span data-stu-id="8094a-127">If you already configured Pingboard for single sign-on, search for your instance of Pingboard by using the search field.</span></span> <span data-ttu-id="8094a-128">Otherwise, select **Add** and search for **Pingboard** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="8094a-128">Otherwise, select **Add** and search for **Pingboard** in the application gallery.</span></span> <span data-ttu-id="8094a-129">Select **Pingboard** from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="8094a-129">Select **Pingboard** from the search results, and add it to your list of applications.</span></span>

1. <span data-ttu-id="8094a-130">Select your instance of Pingboard, and then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="8094a-130">Select your instance of Pingboard, and then select the **Provisioning** tab.</span></span>

1. <span data-ttu-id="8094a-131">Set **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="8094a-131">Set **Provisioning Mode** to **Automatic**.</span></span>

    ![Pingboard Provisioning](./media/pingboard-provisioning-tutorial/pingboardazureprovisioning.png)
    
1. <span data-ttu-id="8094a-133">Under the **Admin Credentials** section, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="8094a-133">Under the **Admin Credentials** section, use the following steps:</span></span>

    <span data-ttu-id="8094a-134">a.</span><span class="sxs-lookup"><span data-stu-id="8094a-134">a.</span></span> <span data-ttu-id="8094a-135">In **Tenant URL**, enter `https://your_domain.pingboard.com/scim/v2`, and replace "your_domain" with your real domain.</span><span class="sxs-lookup"><span data-stu-id="8094a-135">In **Tenant URL**, enter `https://your_domain.pingboard.com/scim/v2`, and replace "your_domain" with your real domain.</span></span>

    <span data-ttu-id="8094a-136">b.</span><span class="sxs-lookup"><span data-stu-id="8094a-136">b.</span></span> <span data-ttu-id="8094a-137">Sign in to [Pingboard](https://pingboard.com/) by using your admin account.</span><span class="sxs-lookup"><span data-stu-id="8094a-137">Sign in to [Pingboard](https://pingboard.com/) by using your admin account.</span></span>

    <span data-ttu-id="8094a-138">c.</span><span class="sxs-lookup"><span data-stu-id="8094a-138">c.</span></span> <span data-ttu-id="8094a-139">Select **Add-Ons** > **Integrations** > **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8094a-139">Select **Add-Ons** > **Integrations** > **Azure Active Directory**.</span></span>

    <span data-ttu-id="8094a-140">d.</span><span class="sxs-lookup"><span data-stu-id="8094a-140">d.</span></span> <span data-ttu-id="8094a-141">Go to the **Configure** tab, and select **Enable user provisioning from Azure**.</span><span class="sxs-lookup"><span data-stu-id="8094a-141">Go to the **Configure** tab, and select **Enable user provisioning from Azure**.</span></span>

    <span data-ttu-id="8094a-142">e.</span><span class="sxs-lookup"><span data-stu-id="8094a-142">e.</span></span> <span data-ttu-id="8094a-143">Copy the token in **OAuth Bearer Token**, and enter it in **Secret Token**.</span><span class="sxs-lookup"><span data-stu-id="8094a-143">Copy the token in **OAuth Bearer Token**, and enter it in **Secret Token**.</span></span>

1. <span data-ttu-id="8094a-144">In the Azure portal, select **Test Connection** to test Azure AD can connect to your Pingboard app.</span><span class="sxs-lookup"><span data-stu-id="8094a-144">In the Azure portal, select **Test Connection** to test Azure AD can connect to your Pingboard app.</span></span> <span data-ttu-id="8094a-145">If the connection fails, test that your Pingboard account has admin permissions, and try the **Test Connection** step again.</span><span class="sxs-lookup"><span data-stu-id="8094a-145">If the connection fails, test that your Pingboard account has admin permissions, and try the **Test Connection** step again.</span></span>

1. <span data-ttu-id="8094a-146">Enter the email address of a person or group that you want to receive provisioning error notifications in **Notification Email**.</span><span class="sxs-lookup"><span data-stu-id="8094a-146">Enter the email address of a person or group that you want to receive provisioning error notifications in **Notification Email**.</span></span> <span data-ttu-id="8094a-147">Select the check box underneath.</span><span class="sxs-lookup"><span data-stu-id="8094a-147">Select the check box underneath.</span></span>

1. <span data-ttu-id="8094a-148">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="8094a-148">Select **Save**.</span></span> 

1. <span data-ttu-id="8094a-149">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="8094a-149">Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Pingboard**.</span></span>

1. <span data-ttu-id="8094a-150">In the **Attribute Mappings** section, review the user attributes to be synchronized from Azure AD to Pingboard.</span><span class="sxs-lookup"><span data-stu-id="8094a-150">In the **Attribute Mappings** section, review the user attributes to be synchronized from Azure AD to Pingboard.</span></span> <span data-ttu-id="8094a-151">The attributes selected as **Matching** properties are used to match the user accounts in Pingboard for update operations.</span><span class="sxs-lookup"><span data-stu-id="8094a-151">The attributes selected as **Matching** properties are used to match the user accounts in Pingboard for update operations.</span></span> <span data-ttu-id="8094a-152">Select **Save** to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="8094a-152">Select **Save** to commit any changes.</span></span> <span data-ttu-id="8094a-153">For more information, see [Customize user provisioning attribute mappings](../manage-apps/customize-application-attributes.md).</span><span class="sxs-lookup"><span data-stu-id="8094a-153">For more information, see [Customize user provisioning attribute mappings](../manage-apps/customize-application-attributes.md).</span></span>

1. <span data-ttu-id="8094a-154">To enable the Azure AD provisioning service for Pingboard, in the **Settings** section, change **Provisioning Status** to **On**.</span><span class="sxs-lookup"><span data-stu-id="8094a-154">To enable the Azure AD provisioning service for Pingboard, in the **Settings** section, change **Provisioning Status** to **On**.</span></span>

1. <span data-ttu-id="8094a-155">Select **Save** to start the initial synchronization of users assigned to Pingboard.</span><span class="sxs-lookup"><span data-stu-id="8094a-155">Select **Save** to start the initial synchronization of users assigned to Pingboard.</span></span>

<span data-ttu-id="8094a-156">The initial synchronization takes longer to run than following syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="8094a-156">The initial synchronization takes longer to run than following syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="8094a-157">Use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs.</span><span class="sxs-lookup"><span data-stu-id="8094a-157">Use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs.</span></span> <span data-ttu-id="8094a-158">The logs describe all actions taken by the provisioning service on your Pingboard app.</span><span class="sxs-lookup"><span data-stu-id="8094a-158">The logs describe all actions taken by the provisioning service on your Pingboard app.</span></span>

<span data-ttu-id="8094a-159">For more information on how to read the Azure AD provisioning logs, see [Report on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="8094a-159">For more information on how to read the Azure AD provisioning logs, see [Report on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8094a-160">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8094a-160">Additional resources</span></span>

* [<span data-ttu-id="8094a-161">Manage user account provisioning for enterprise apps</span><span class="sxs-lookup"><span data-stu-id="8094a-161">Manage user account provisioning for enterprise apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="8094a-162">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8094a-162">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="8094a-163">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="8094a-163">Configure single sign-on</span></span>](pingboard-tutorial.md)
