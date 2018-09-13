---
title: 'Tutorial: Configure LucidChart for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn how to configure Azure Active Directory to automatically provision and de-provision user accounts to LucidChart.
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
ms.openlocfilehash: 011fa2dcce390597337ec583c1d5704177fda251
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871371"
---
# <a name="tutorial-configure-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="70fae-103">Tutorial: Configure LucidChart for automatic user provisioning</span><span class="sxs-lookup"><span data-stu-id="70fae-103">Tutorial: Configure LucidChart for automatic user provisioning</span></span>


<span data-ttu-id="70fae-104">The objective of this tutorial is to show you the steps you need to perform in LucidChart and Azure AD to automatically provision and de-provision user accounts from Azure AD to LucidChart.</span><span class="sxs-lookup"><span data-stu-id="70fae-104">The objective of this tutorial is to show you the steps you need to perform in LucidChart and Azure AD to automatically provision and de-provision user accounts from Azure AD to LucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="70fae-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="70fae-105">Prerequisites</span></span>

<span data-ttu-id="70fae-106">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="70fae-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="70fae-107">An Azure Active directory tenant</span><span class="sxs-lookup"><span data-stu-id="70fae-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="70fae-108">A LucidChart tenant with the [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span><span class="sxs-lookup"><span data-stu-id="70fae-108">A LucidChart tenant with the [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="70fae-109">A user account in LucidChart with Admin permissions</span><span class="sxs-lookup"><span data-stu-id="70fae-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-to-lucidchart"></a><span data-ttu-id="70fae-110">Assigning users to LucidChart</span><span class="sxs-lookup"><span data-stu-id="70fae-110">Assigning users to LucidChart</span></span>

<span data-ttu-id="70fae-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span><span class="sxs-lookup"><span data-stu-id="70fae-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="70fae-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span><span class="sxs-lookup"><span data-stu-id="70fae-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="70fae-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your LucidChart app.</span><span class="sxs-lookup"><span data-stu-id="70fae-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your LucidChart app.</span></span> <span data-ttu-id="70fae-114">Once decided, you can assign these users to your LucidChart app by following the instructions here:</span><span class="sxs-lookup"><span data-stu-id="70fae-114">Once decided, you can assign these users to your LucidChart app by following the instructions here:</span></span>

[<span data-ttu-id="70fae-115">Assign a user or group to an enterprise app</span><span class="sxs-lookup"><span data-stu-id="70fae-115">Assign a user or group to an enterprise app</span></span>](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-lucidchart"></a><span data-ttu-id="70fae-116">Important tips for assigning users to LucidChart</span><span class="sxs-lookup"><span data-stu-id="70fae-116">Important tips for assigning users to LucidChart</span></span>

*   <span data-ttu-id="70fae-117">It is recommended that a single Azure AD user is assigned to LucidChart to test the provisioning configuration.</span><span class="sxs-lookup"><span data-stu-id="70fae-117">It is recommended that a single Azure AD user is assigned to LucidChart to test the provisioning configuration.</span></span> <span data-ttu-id="70fae-118">Additional users and/or groups may be assigned later.</span><span class="sxs-lookup"><span data-stu-id="70fae-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="70fae-119">When assigning a user to LucidChart, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span><span class="sxs-lookup"><span data-stu-id="70fae-119">When assigning a user to LucidChart, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="70fae-120">The **Default Access** role does not work for provisioning, and these users are skipped.</span><span class="sxs-lookup"><span data-stu-id="70fae-120">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-lucidchart"></a><span data-ttu-id="70fae-121">Configuring user provisioning to LucidChart</span><span class="sxs-lookup"><span data-stu-id="70fae-121">Configuring user provisioning to LucidChart</span></span> 

<span data-ttu-id="70fae-122">This section guides you through connecting your Azure AD to LucidChart's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70fae-122">This section guides you through connecting your Azure AD to LucidChart's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="70fae-123">You may also choose to enabled SAML-based Single Sign-On for LucidChart, following the instructions provided in [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70fae-123">You may also choose to enabled SAML-based Single Sign-On for LucidChart, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="70fae-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span><span class="sxs-lookup"><span data-stu-id="70fae-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-lucidchart-in-azure-ad"></a><span data-ttu-id="70fae-125">Configure automatic user account provisioning to LucidChart in Azure AD</span><span class="sxs-lookup"><span data-stu-id="70fae-125">Configure automatic user account provisioning to LucidChart in Azure AD</span></span>


1. <span data-ttu-id="70fae-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span><span class="sxs-lookup"><span data-stu-id="70fae-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="70fae-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using the search field.</span><span class="sxs-lookup"><span data-stu-id="70fae-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using the search field.</span></span> <span data-ttu-id="70fae-128">Otherwise, select **Add** and search for **LucidChart** in the application gallery.</span><span class="sxs-lookup"><span data-stu-id="70fae-128">Otherwise, select **Add** and search for **LucidChart** in the application gallery.</span></span> <span data-ttu-id="70fae-129">Select LucidChart from the search results, and add it to your list of applications.</span><span class="sxs-lookup"><span data-stu-id="70fae-129">Select LucidChart from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="70fae-130">Select your instance of LucidChart, then select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="70fae-130">Select your instance of LucidChart, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="70fae-131">Set the **Provisioning Mode** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="70fae-131">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![LucidChart Provisioning](./media/lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="70fae-133">Under the **Admin Credentials** section, input the **Secret Token** generated by your LucidChart's account (you can find the token under your account: **Team** > **App Integration** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="70fae-133">Under the **Admin Credentials** section, input the **Secret Token** generated by your LucidChart's account (you can find the token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![LucidChart Provisioning](./media/lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="70fae-135">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your LucidChart app.</span><span class="sxs-lookup"><span data-stu-id="70fae-135">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your LucidChart app.</span></span> <span data-ttu-id="70fae-136">If the connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span><span class="sxs-lookup"><span data-stu-id="70fae-136">If the connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="70fae-137">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span><span class="sxs-lookup"><span data-stu-id="70fae-137">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="70fae-138">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="70fae-138">Click **Save**.</span></span> 

9. <span data-ttu-id="70fae-139">Under the Mappings section, select **Synchronize Azure Active Directory Users to LucidChart**.</span><span class="sxs-lookup"><span data-stu-id="70fae-139">Under the Mappings section, select **Synchronize Azure Active Directory Users to LucidChart**.</span></span>

10. <span data-ttu-id="70fae-140">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to LucidChart.</span><span class="sxs-lookup"><span data-stu-id="70fae-140">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to LucidChart.</span></span> <span data-ttu-id="70fae-141">The attributes selected as **Matching** properties are used to match the user accounts in LucidChart for update operations.</span><span class="sxs-lookup"><span data-stu-id="70fae-141">The attributes selected as **Matching** properties are used to match the user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="70fae-142">Select the Save button to commit any changes.</span><span class="sxs-lookup"><span data-stu-id="70fae-142">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="70fae-143">To enable the Azure AD provisioning service for LucidChart, change the **Provisioning Status** to **On** in the **Settings** section</span><span class="sxs-lookup"><span data-stu-id="70fae-143">To enable the Azure AD provisioning service for LucidChart, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="70fae-144">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="70fae-144">Click **Save**.</span></span> 

<span data-ttu-id="70fae-145">This operation starts the initial synchronization of any users and/or groups assigned to LucidChart in the Users and Groups section.</span><span class="sxs-lookup"><span data-stu-id="70fae-145">This operation starts the initial synchronization of any users and/or groups assigned to LucidChart in the Users and Groups section.</span></span> <span data-ttu-id="70fae-146">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span><span class="sxs-lookup"><span data-stu-id="70fae-146">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the service is running.</span></span> <span data-ttu-id="70fae-147">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service.</span><span class="sxs-lookup"><span data-stu-id="70fae-147">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity logs, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="70fae-148">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="70fae-148">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](../manage-apps/check-status-user-account-provisioning.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="70fae-149">Additional resources</span><span class="sxs-lookup"><span data-stu-id="70fae-149">Additional resources</span></span>

* [<span data-ttu-id="70fae-150">Managing user account provisioning for Enterprise Apps</span><span class="sxs-lookup"><span data-stu-id="70fae-150">Managing user account provisioning for Enterprise Apps</span></span>](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [<span data-ttu-id="70fae-151">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="70fae-151">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a><span data-ttu-id="70fae-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="70fae-152">Next steps</span></span>

* [<span data-ttu-id="70fae-153">Learn how to review logs and get reports on provisioning activity</span><span class="sxs-lookup"><span data-stu-id="70fae-153">Learn how to review logs and get reports on provisioning activity</span></span>](../manage-apps/check-status-user-account-provisioning.md)
