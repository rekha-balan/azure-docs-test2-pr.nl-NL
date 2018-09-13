---
title: 'Tutorial: Configure ThousandEyes for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to ThousandEyes.
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
ms.openlocfilehash: d2912c687d4968a239d5af747df4115ffd71bbeb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871058"
---
# <a name="tutorial-configure-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="4f717-103">Tutorial: Configure ThousandEyes for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="4f717-103">Tutorial: Configure ThousandEyes for automatic user provisioning</span></span>


<span data-ttu-id="4f717-104">The objective of this tutorial is to show you the steps you need to perform in ThousandEyes and Azure AD to automatically provision and de-provision user accounts from Azure AD to ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="4f717-104">The objective of this tutorial is to show you the steps you need to perform in ThousandEyes and Azure AD to automatically provision and de-provision user accounts from Azure AD to ThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4f717-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4f717-105">Prerequisites</span></span>

<span data-ttu-id="4f717-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="4f717-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="4f717-107">An Azure Active directory tenant</span><span class="sxs-lookup"><span data-stu-id="4f717-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="4f717-108">A ThousandEyes tenant with the [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span><span class="sxs-lookup"><span data-stu-id="4f717-108">A ThousandEyes tenant with the [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="4f717-109">A user account in ThousandEyes with Admin permissions</span><span class="sxs-lookup"><span data-stu-id="4f717-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="4f717-110">The Azure AD provisioning integration relies on the [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available to ThousandEyes teams on the Standard plan or better.</span><span class="sxs-lookup"><span data-stu-id="4f717-110">The Azure AD provisioning integration relies on the [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available to ThousandEyes teams on the Standard plan or better.</span></span>

## <a name="assigning-users-to-thousandeyes"></a><span data-ttu-id="4f717-111">Assigning users to ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="4f717-111">Assigning users to ThousandEyes</span></span>

<span data-ttu-id="4f717-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="4f717-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="4f717-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span><span class="sxs-lookup"><span data-stu-id="4f717-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="4f717-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ThousandEyes app.</span><span class="sxs-lookup"><span data-stu-id="4f717-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ThousandEyes app.</span></span> <span data-ttu-id="4f717-115">Once decided, you can assign these users to your ThousandEyes app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="4f717-115">Once decided, you can assign these users to your ThousandEyes app by following the instructions here:</span></span>

[<span data-ttu-id="4f717-116">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="4f717-116">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-thousandeyes"></a><span data-ttu-id="4f717-117">Important tips for assigning users to ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="4f717-117">Important tips for assigning users to ThousandEyes</span></span>

*   <span data-ttu-id="4f717-118">It is recommended that a single Azure AD user is assigned to ThousandEyes to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="4f717-118">It is recommended that a single Azure AD user is assigned to ThousandEyes to test the provisioning configuration.</span></span> <span data-ttu-id="4f717-119">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="4f717-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4f717-120">When assigning a user to ThousandEyes, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="4f717-120">When assigning a user to ThousandEyes, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="4f717-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span><span class="sxs-lookup"><span data-stu-id="4f717-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-thousandeyes"></a><span data-ttu-id="4f717-122">Configuring user provisioning to ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="4f717-122">Configuring user provisioning to ThousandEyes</span></span> 

<span data-ttu-id="4f717-123">This section guides you through connecting your Azure AD to ThousandEyes's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f717-123">This section guides you through connecting your Azure AD to ThousandEyes's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="4f717-124">You may also choose to enabled SAML-based Single Sign-On for ThousandEyes, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4f717-124">You may also choose to enabled SAML-based Single Sign-On for ThousandEyes, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4f717-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="4f717-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-thousandeyes-in-azure-ad"></a><span data-ttu-id="4f717-126">Configure automatic user account provisioning to ThousandEyes in Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f717-126">Configure automatic user account provisioning to ThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="4f717-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span><span class="sxs-lookup"><span data-stu-id="4f717-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="4f717-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using the search field.</span><span class="sxs-lookup"><span data-stu-id="4f717-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using the search field.</span></span> <span data-ttu-id="4f717-129">Otherwise, select **Add** and search for **ThousandEyes** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="4f717-129">Otherwise, select **Add** and search for **ThousandEyes** in the application gallery.</span></span> <span data-ttu-id="4f717-130">Select ThousandEyes from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="4f717-130">Select ThousandEyes from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="4f717-131">Select your instance of ThousandEyes, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="4f717-131">Select your instance of ThousandEyes, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="4f717-132">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="4f717-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![ThousandEyes Provisioning](./media/thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="4f717-134">Under the **Admin Credentials** section, input the **Secret Token** generated by your ThousandEyes's account (you can find the token under your ThousandEyes account: **Security & Authentication**).</span><span class="sxs-lookup"><span data-stu-id="4f717-134">Under the **Admin Credentials** section, input the **Secret Token** generated by your ThousandEyes's account (you can find the token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![ThousandEyes Provisioning](./media/thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="4f717-136">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ThousandEyes app.</span><span class="sxs-lookup"><span data-stu-id="4f717-136">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ThousandEyes app.</span></span> <span data-ttu-id="4f717-137">If the connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span><span class="sxs-lookup"><span data-stu-id="4f717-137">If the connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="4f717-138">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span><span class="sxs-lookup"><span data-stu-id="4f717-138">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="4f717-139">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4f717-139">Click **Save**.</span></span> 

9. <span data-ttu-id="4f717-140">Under the Mappings section, select **Synchronize Azure Active Directory Users to ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="4f717-140">Under the Mappings section, select **Synchronize Azure Active Directory Users to ThousandEyes**.</span></span>

10. <span data-ttu-id="4f717-141">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="4f717-141">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ThousandEyes.</span></span> <span data-ttu-id="4f717-142">The attributes selected as **Matching** properties are used to match the user accounts in ThousandEyes for update operations.</span><span class="sxs-lookup"><span data-stu-id="4f717-142">The attributes selected as **Matching** properties are used to match the user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="4f717-143">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="4f717-143">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="4f717-144">To enable the Azure AD provisioning service for ThousandEyes, change the **Provisioning Status** to **On** in the **Settings** section</span><span class="sxs-lookup"><span data-stu-id="4f717-144">To enable the Azure AD provisioning service for ThousandEyes, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="4f717-145">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4f717-145">Click **Save**.</span></span> 

<span data-ttu-id="4f717-146">This operation starts the initial synchronization of any users and/or groups assigned to ThousandEyes in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="4f717-146">This operation starts the initial synchronization of any users and/or groups assigned to ThousandEyes in the Users and Groups section.</span></span> <span data-ttu-id="4f717-147">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="4f717-147">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="4f717-148">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service.</span><span class="sxs-lookup"><span data-stu-id="4f717-148">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="4f717-149">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="4f717-149">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4f717-150">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4f717-150">Additional resources</span></span>

* [<span data-ttu-id="4f717-151">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="4f717-151">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="4f717-152">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4f717-152">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a><span data-ttu-id="4f717-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="4f717-153">Next steps</span></span>

* [<span data-ttu-id="4f717-154">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="4f717-154">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)
