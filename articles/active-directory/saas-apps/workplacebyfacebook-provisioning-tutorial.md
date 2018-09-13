---
title: 'Tutorial: Configure Workplace by Facebook for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Workplace by Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2018
ms.author: jeedes
ms.openlocfilehash: 2b085d8b825055b5cb318da200eafb6d9000bf4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864505"
---
# <a name="tutorial-configure-workplace-by-facebook-for-automatic-user-provisioning"></a><span data-ttu-id="4997b-103">Tutorial: Configure Workplace by Facebook for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="4997b-103">Tutorial: Configure Workplace by Facebook for automatic user provisioning</span></span>

<span data-ttu-id="4997b-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4997b-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4997b-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4997b-105">Prerequisites</span></span>

<span data-ttu-id="4997b-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4997b-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="4997b-107">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4997b-107">An Azure AD subscription</span></span>
- <span data-ttu-id="4997b-108">A Workplace by Facebook single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4997b-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4997b-109">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4997b-109">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4997b-110">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4997b-110">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4997b-111">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4997b-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4997b-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4997b-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="4997b-113">Assigning users to Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="4997b-113">Assigning users to Workplace by Facebook</span></span>

<span data-ttu-id="4997b-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="4997b-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="4997b-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span><span class="sxs-lookup"><span data-stu-id="4997b-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="4997b-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span><span class="sxs-lookup"><span data-stu-id="4997b-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="4997b-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="4997b-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span></span>

[<span data-ttu-id="4997b-118">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="4997b-118">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="4997b-119">Important tips for assigning users to Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="4997b-119">Important tips for assigning users to Workplace by Facebook</span></span>

*   <span data-ttu-id="4997b-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="4997b-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span></span> <span data-ttu-id="4997b-121">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="4997b-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4997b-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span><span class="sxs-lookup"><span data-stu-id="4997b-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="4997b-123">The "Default Access" role does not work for provisioning.</span><span class="sxs-lookup"><span data-stu-id="4997b-123">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="4997b-124">Enable User Provisioning</span><span class="sxs-lookup"><span data-stu-id="4997b-124">Enable User Provisioning</span></span>

<span data-ttu-id="4997b-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4997b-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="4997b-126">You may also choose to enable SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4997b-126">You may also choose to enable SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4997b-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="4997b-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="4997b-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4997b-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="4997b-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4997b-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span></span>

<span data-ttu-id="4997b-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4997b-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="4997b-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span><span class="sxs-lookup"><span data-stu-id="4997b-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="4997b-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4997b-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="4997b-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span><span class="sxs-lookup"><span data-stu-id="4997b-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="4997b-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span><span class="sxs-lookup"><span data-stu-id="4997b-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span></span> <span data-ttu-id="4997b-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="4997b-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="4997b-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="4997b-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="4997b-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="4997b-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="4997b-138">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="4997b-138">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisioning](./media/workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="4997b-140">Under the **Admin Credentials** section, enter the Access Token from your Workplace by Facebook administrator and set the Tenant URL value to `https://www.facebook.com/scim/v1/` .</span><span class="sxs-lookup"><span data-stu-id="4997b-140">Under the **Admin Credentials** section, enter the Access Token from your Workplace by Facebook administrator and set the Tenant URL value to `https://www.facebook.com/scim/v1/` .</span></span> <span data-ttu-id="4997b-141">See these [instructions](https://developers.facebook.com/docs/workplace/integrations/custom-integrations/apps) on creating an Access Token for Workplace.</span><span class="sxs-lookup"><span data-stu-id="4997b-141">See these [instructions](https://developers.facebook.com/docs/workplace/integrations/custom-integrations/apps) on creating an Access Token for Workplace.</span></span> 

6. <span data-ttu-id="4997b-142">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span><span class="sxs-lookup"><span data-stu-id="4997b-142">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="4997b-143">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span><span class="sxs-lookup"><span data-stu-id="4997b-143">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="4997b-144">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span><span class="sxs-lookup"><span data-stu-id="4997b-144">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="4997b-145">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="4997b-145">Click **Save.**</span></span>

9. <span data-ttu-id="4997b-146">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span><span class="sxs-lookup"><span data-stu-id="4997b-146">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span></span>

10. <span data-ttu-id="4997b-147">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4997b-147">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="4997b-148">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span><span class="sxs-lookup"><span data-stu-id="4997b-148">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="4997b-149">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="4997b-149">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="4997b-150">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span><span class="sxs-lookup"><span data-stu-id="4997b-150">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="4997b-151">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="4997b-151">Click **Save.**</span></span>

<span data-ttu-id="4997b-152">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="4997b-152">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="4997b-153">You can now create a test account.</span><span class="sxs-lookup"><span data-stu-id="4997b-153">You can now create a test account.</span></span> <span data-ttu-id="4997b-154">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="4997b-154">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4997b-155">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4997b-155">Additional resources</span></span>

* [<span data-ttu-id="4997b-156">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="4997b-156">Managing user account provisioning for Enterprise Apps</span></span>](tutorial-list.md)
* [<span data-ttu-id="4997b-157">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4997b-157">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="4997b-158">Configure Single Sign-on</span><span class="sxs-lookup"><span data-stu-id="4997b-158">Configure Single Sign-on</span></span>](workplacebyfacebook-tutorial.md)
