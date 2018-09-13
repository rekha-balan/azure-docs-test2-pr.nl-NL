---
title: Add B2B collaboration users as an information worker - Azure Active Directory | Microsoft Docs
description: B2B collaboration allows information workers and app owners to add guest users to Azure AD for access | Microsoft Docs
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 08/08/2018
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: mal
ms.openlocfilehash: 904f6b571c063dd760cfd2604a72a505112fe57a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871585"
---
# <a name="how-users-in-your-organization-can-invite-guest-users-to-an-app"></a><span data-ttu-id="d562f-103">How users in your organization can invite guest users to an app</span><span class="sxs-lookup"><span data-stu-id="d562f-103">How users in your organization can invite guest users to an app</span></span>

<span data-ttu-id="d562f-104">After a guest user has been added to the directory in Azure AD, an application owner can send the guest user a direct link to the app they want to share.</span><span class="sxs-lookup"><span data-stu-id="d562f-104">After a guest user has been added to the directory in Azure AD, an application owner can send the guest user a direct link to the app they want to share.</span></span> <span data-ttu-id="d562f-105">Azure AD admins can also set up self-service management so that application owners can manage their own guest users, even if the guest users haven’t been added to the directory yet.</span><span class="sxs-lookup"><span data-stu-id="d562f-105">Azure AD admins can also set up self-service management so that application owners can manage their own guest users, even if the guest users haven’t been added to the directory yet.</span></span> <span data-ttu-id="d562f-106">When an app is configured for self-service, the application owner uses their Access Panel to invite a guest user to an app or add a guest user to a group that has access to the app.</span><span class="sxs-lookup"><span data-stu-id="d562f-106">When an app is configured for self-service, the application owner uses their Access Panel to invite a guest user to an app or add a guest user to a group that has access to the app.</span></span> <span data-ttu-id="d562f-107">Self-service app management requires some initial setup by an admin. The following is a summary of the setup steps (for more detailed instructions, see [Prerequisites](#prerequisites) later on this page):</span><span class="sxs-lookup"><span data-stu-id="d562f-107">Self-service app management requires some initial setup by an admin. The following is a summary of the setup steps (for more detailed instructions, see [Prerequisites](#prerequisites) later on this page):</span></span>

 - <span data-ttu-id="d562f-108">Enable self-service group management for your tenant</span><span class="sxs-lookup"><span data-stu-id="d562f-108">Enable self-service group management for your tenant</span></span>
 - <span data-ttu-id="d562f-109">Create a group to assign to the app and make the user an owner</span><span class="sxs-lookup"><span data-stu-id="d562f-109">Create a group to assign to the app and make the user an owner</span></span>
 - <span data-ttu-id="d562f-110">Configure the app for self-service and assign the group to the app</span><span class="sxs-lookup"><span data-stu-id="d562f-110">Configure the app for self-service and assign the group to the app</span></span>

## <a name="invite-a-guest-user-to-an-app-from-the-access-panel"></a><span data-ttu-id="d562f-111">Invite a guest user to an app from the Access Panel</span><span class="sxs-lookup"><span data-stu-id="d562f-111">Invite a guest user to an app from the Access Panel</span></span>

<span data-ttu-id="d562f-112">After an app is configured for self-service, application owners can use their own Access Panel to invite a guest user to the app they want to share.</span><span class="sxs-lookup"><span data-stu-id="d562f-112">After an app is configured for self-service, application owners can use their own Access Panel to invite a guest user to the app they want to share.</span></span> <span data-ttu-id="d562f-113">The guest user doesn't necessarily need to be added to Azure AD in advance.</span><span class="sxs-lookup"><span data-stu-id="d562f-113">The guest user doesn't necessarily need to be added to Azure AD in advance.</span></span> 

1. <span data-ttu-id="d562f-114">Open your Access Panel by going to `https://myapps.microsoft.com`.</span><span class="sxs-lookup"><span data-stu-id="d562f-114">Open your Access Panel by going to `https://myapps.microsoft.com`.</span></span>
2. <span data-ttu-id="d562f-115">Point to the app, select the ellipses (**...**), and then select **Manage app**.</span><span class="sxs-lookup"><span data-stu-id="d562f-115">Point to the app, select the ellipses (**...**), and then select **Manage app**.</span></span>
 
   ![Access Panels manage app](media/add-users-iw/access-panel-manage-app.png)
 
3. <span data-ttu-id="d562f-117">At the top of the users list, select **+**.</span><span class="sxs-lookup"><span data-stu-id="d562f-117">At the top of the users list, select **+**.</span></span>
   
   ![Access Panel add a user](media/add-users-iw/access-panel-manage-app-add-user.png)
   
4. <span data-ttu-id="d562f-119">In the **Add members** search box, type the email address for the guest user.</span><span class="sxs-lookup"><span data-stu-id="d562f-119">In the **Add members** search box, type the email address for the guest user.</span></span> <span data-ttu-id="d562f-120">Optionally, include a welcome message.</span><span class="sxs-lookup"><span data-stu-id="d562f-120">Optionally, include a welcome message.</span></span>
   
   ![Access Panel invitation](media/add-users-iw/access-panel-invitation.png)
   
5. <span data-ttu-id="d562f-122">Select **Add** to send an invitation to the guest user.</span><span class="sxs-lookup"><span data-stu-id="d562f-122">Select **Add** to send an invitation to the guest user.</span></span> <span data-ttu-id="d562f-123">After you send the invitation, the user account is automatically added to the directory as a guest.</span><span class="sxs-lookup"><span data-stu-id="d562f-123">After you send the invitation, the user account is automatically added to the directory as a guest.</span></span>

## <a name="invite-someone-to-join-a-group-that-has-access-to-the-app"></a><span data-ttu-id="d562f-124">Invite someone to join a group that has access to the app</span><span class="sxs-lookup"><span data-stu-id="d562f-124">Invite someone to join a group that has access to the app</span></span>
<span data-ttu-id="d562f-125">After an app is configured for self-service, application owners can invite guest users to the groups they manage that have access to the apps they want to share.</span><span class="sxs-lookup"><span data-stu-id="d562f-125">After an app is configured for self-service, application owners can invite guest users to the groups they manage that have access to the apps they want to share.</span></span> <span data-ttu-id="d562f-126">The guest users don't have to already exist in the directory.</span><span class="sxs-lookup"><span data-stu-id="d562f-126">The guest users don't have to already exist in the directory.</span></span> <span data-ttu-id="d562f-127">The application owner follows these steps to invite a guest user to the group so that they can access the app.</span><span class="sxs-lookup"><span data-stu-id="d562f-127">The application owner follows these steps to invite a guest user to the group so that they can access the app.</span></span>

1. <span data-ttu-id="d562f-128">Make sure you're an owner of the self-service group that has access to the app you want to share.</span><span class="sxs-lookup"><span data-stu-id="d562f-128">Make sure you're an owner of the self-service group that has access to the app you want to share.</span></span>
2. <span data-ttu-id="d562f-129">Open your Access Panel by going to `https://myapps.microsoft.com`.</span><span class="sxs-lookup"><span data-stu-id="d562f-129">Open your Access Panel by going to `https://myapps.microsoft.com`.</span></span>
3. <span data-ttu-id="d562f-130">Select the **Groups** app.</span><span class="sxs-lookup"><span data-stu-id="d562f-130">Select the **Groups** app.</span></span>
   
   ![Access Panel groups app](media/add-users-iw/access-panel-groups.png)
   
4. <span data-ttu-id="d562f-132">Under **Groups I own**, select the group that has access to the app you want to share.</span><span class="sxs-lookup"><span data-stu-id="d562f-132">Under **Groups I own**, select the group that has access to the app you want to share.</span></span>
   
   ![Access Panel groups I own](media/add-users-iw/access-panel-groups-i-own.png)
   
5. <span data-ttu-id="d562f-134">At the top of the group members list, select **+**.</span><span class="sxs-lookup"><span data-stu-id="d562f-134">At the top of the group members list, select **+**.</span></span>
   
   ![Access Panel groups add a member](media/add-users-iw/access-panel-groups-add-member.png)
   
6. <span data-ttu-id="d562f-136">In the **Add members** search box, type the email address for the guest user.</span><span class="sxs-lookup"><span data-stu-id="d562f-136">In the **Add members** search box, type the email address for the guest user.</span></span> <span data-ttu-id="d562f-137">Optionally, include a welcome message.</span><span class="sxs-lookup"><span data-stu-id="d562f-137">Optionally, include a welcome message.</span></span>
   
   ![Access Panel group invitation](media/add-users-iw/access-panel-invitation.png)
   
7. <span data-ttu-id="d562f-139">Select **Add** to automatically send the invitation to the guest user.</span><span class="sxs-lookup"><span data-stu-id="d562f-139">Select **Add** to automatically send the invitation to the guest user.</span></span> <span data-ttu-id="d562f-140">After you send the invitation, the user account is automatically added to the directory as a guest.</span><span class="sxs-lookup"><span data-stu-id="d562f-140">After you send the invitation, the user account is automatically added to the directory as a guest.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d562f-141">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d562f-141">Prerequisites</span></span>

<span data-ttu-id="d562f-142">Self-service app management requires some initial setup by a Global Administrator and an Azure AD administrator.</span><span class="sxs-lookup"><span data-stu-id="d562f-142">Self-service app management requires some initial setup by a Global Administrator and an Azure AD administrator.</span></span> <span data-ttu-id="d562f-143">As part of this setup, you'll configure the app for self-service and assign a group to the app that the application owner can manage.</span><span class="sxs-lookup"><span data-stu-id="d562f-143">As part of this setup, you'll configure the app for self-service and assign a group to the app that the application owner can manage.</span></span> <span data-ttu-id="d562f-144">You can also configure the group to allow anyone to request membership but require a group owner's approval.</span><span class="sxs-lookup"><span data-stu-id="d562f-144">You can also configure the group to allow anyone to request membership but require a group owner's approval.</span></span> <span data-ttu-id="d562f-145">(Learn more about [self-service group management](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-self-service-management).)</span><span class="sxs-lookup"><span data-stu-id="d562f-145">(Learn more about [self-service group management](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-self-service-management).)</span></span> 

> [!NOTE]
> <span data-ttu-id="d562f-146">You cannot add guest users to a dynamic group or to a group that is synced with on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d562f-146">You cannot add guest users to a dynamic group or to a group that is synced with on-premises Active Directory.</span></span>

### <a name="enable-self-service-group-management-for-your-tenant"></a><span data-ttu-id="d562f-147">Enable self-service group management for your tenant</span><span class="sxs-lookup"><span data-stu-id="d562f-147">Enable self-service group management for your tenant</span></span>
1. <span data-ttu-id="d562f-148">Sign in to the [Azure portal](https://portal.azure.com) as a Global Administrator.</span><span class="sxs-lookup"><span data-stu-id="d562f-148">Sign in to the [Azure portal](https://portal.azure.com) as a Global Administrator.</span></span>
2. <span data-ttu-id="d562f-149">In the navigation panel, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d562f-149">In the navigation panel, select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="d562f-150">Select **Groups**.</span><span class="sxs-lookup"><span data-stu-id="d562f-150">Select **Groups**.</span></span>
4. <span data-ttu-id="d562f-151">Under **Settings**, select **General**.</span><span class="sxs-lookup"><span data-stu-id="d562f-151">Under **Settings**, select **General**.</span></span>
5. <span data-ttu-id="d562f-152">Under **Self Service Group Management**, next to **Owners can manage group membership requests in the Access Panel**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="d562f-152">Under **Self Service Group Management**, next to **Owners can manage group membership requests in the Access Panel**, select **Yes**.</span></span>
6. <span data-ttu-id="d562f-153">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d562f-153">Select **Save**.</span></span>

### <a name="create-a-group-to-assign-to-the-app-and-make-the-user-an-owner"></a><span data-ttu-id="d562f-154">Create a group to assign to the app and make the user an owner</span><span class="sxs-lookup"><span data-stu-id="d562f-154">Create a group to assign to the app and make the user an owner</span></span>
1. <span data-ttu-id="d562f-155">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator or Global Administrator.</span><span class="sxs-lookup"><span data-stu-id="d562f-155">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator or Global Administrator.</span></span>
2. <span data-ttu-id="d562f-156">In the navigation panel, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d562f-156">In the navigation panel, select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="d562f-157">Select **Groups**.</span><span class="sxs-lookup"><span data-stu-id="d562f-157">Select **Groups**.</span></span>
4. <span data-ttu-id="d562f-158">Select **New group**.</span><span class="sxs-lookup"><span data-stu-id="d562f-158">Select **New group**.</span></span>
5. <span data-ttu-id="d562f-159">Under **Group type**, select **Security**.</span><span class="sxs-lookup"><span data-stu-id="d562f-159">Under **Group type**, select **Security**.</span></span>
6. <span data-ttu-id="d562f-160">Type a **Group name** and **Group description**.</span><span class="sxs-lookup"><span data-stu-id="d562f-160">Type a **Group name** and **Group description**.</span></span>
7. <span data-ttu-id="d562f-161">Under **Membership type**, select **Assigned**.</span><span class="sxs-lookup"><span data-stu-id="d562f-161">Under **Membership type**, select **Assigned**.</span></span>
8. <span data-ttu-id="d562f-162">Select **Create**, and close the **Group** page.</span><span class="sxs-lookup"><span data-stu-id="d562f-162">Select **Create**, and close the **Group** page.</span></span>
9. <span data-ttu-id="d562f-163">On the **Groups - All groups** page, open the group.</span><span class="sxs-lookup"><span data-stu-id="d562f-163">On the **Groups - All groups** page, open the group.</span></span> 
10. <span data-ttu-id="d562f-164">Under **Manage**, select **Owners** > **Add owners**.</span><span class="sxs-lookup"><span data-stu-id="d562f-164">Under **Manage**, select **Owners** > **Add owners**.</span></span> <span data-ttu-id="d562f-165">Search for the user who should manage access to the application.</span><span class="sxs-lookup"><span data-stu-id="d562f-165">Search for the user who should manage access to the application.</span></span> <span data-ttu-id="d562f-166">Select the user, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="d562f-166">Select the user, and then click **Select**.</span></span>

### <a name="configure-the-app-for-self-service-and-assign-the-group-to-the-app"></a><span data-ttu-id="d562f-167">Configure the app for self-service and assign the group to the app</span><span class="sxs-lookup"><span data-stu-id="d562f-167">Configure the app for self-service and assign the group to the app</span></span>
1. <span data-ttu-id="d562f-168">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator or Global Administrator.</span><span class="sxs-lookup"><span data-stu-id="d562f-168">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator or Global Administrator.</span></span>
2. <span data-ttu-id="d562f-169">In the navigation pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d562f-169">In the navigation pane, select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="d562f-170">Under **Manage**, select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d562f-170">Under **Manage**, select **Enterprise applications** > **All applications**.</span></span>
4. <span data-ttu-id="d562f-171">In the application list, find and open the app.</span><span class="sxs-lookup"><span data-stu-id="d562f-171">In the application list, find and open the app.</span></span>
5. <span data-ttu-id="d562f-172">Under **Manage**, select **Single sign-on**, and configure the application for single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d562f-172">Under **Manage**, select **Single sign-on**, and configure the application for single sign-on.</span></span> <span data-ttu-id="d562f-173">(For details, see [how to manage single sign-on for enterprise apps](https://docs.microsoft.com/azure/active-directory/manage-apps/configure-single-sign-on-portal).)</span><span class="sxs-lookup"><span data-stu-id="d562f-173">(For details, see [how to manage single sign-on for enterprise apps](https://docs.microsoft.com/azure/active-directory/manage-apps/configure-single-sign-on-portal).)</span></span>
6. <span data-ttu-id="d562f-174">Under **Manage**, select **Self-service**, and set up self-service app access.</span><span class="sxs-lookup"><span data-stu-id="d562f-174">Under **Manage**, select **Self-service**, and set up self-service app access.</span></span> <span data-ttu-id="d562f-175">(For details, see [how to use self-service app access](https://docs.microsoft.com/azure/active-directory/application-access-panel-self-service-applications-how-to).)</span><span class="sxs-lookup"><span data-stu-id="d562f-175">(For details, see [how to use self-service app access](https://docs.microsoft.com/azure/active-directory/application-access-panel-self-service-applications-how-to).)</span></span> 
    > [!NOTE]
    > <span data-ttu-id="d562f-176">For the setting **To which group should assigned users be added?** select the group you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d562f-176">For the setting **To which group should assigned users be added?** select the group you created in the previous section.</span></span>
7. <span data-ttu-id="d562f-177">Under **Manage**, select **Users and groups**, and verify that the self-service group you created appears in the list.</span><span class="sxs-lookup"><span data-stu-id="d562f-177">Under **Manage**, select **Users and groups**, and verify that the self-service group you created appears in the list.</span></span>
8. <span data-ttu-id="d562f-178">To add the app to the group owner's Access Panel, select **Add user** > **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d562f-178">To add the app to the group owner's Access Panel, select **Add user** > **Users and groups**.</span></span> <span data-ttu-id="d562f-179">Search for the group owner and select the user, click **Select**, and then click **Assign** to add the user to the app.</span><span class="sxs-lookup"><span data-stu-id="d562f-179">Search for the group owner and select the user, click **Select**, and then click **Assign** to add the user to the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d562f-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="d562f-180">Next steps</span></span>

<span data-ttu-id="d562f-181">See the following articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="d562f-181">See the following articles on Azure AD B2B collaboration:</span></span>

- [<span data-ttu-id="d562f-182">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="d562f-182">What is Azure AD B2B collaboration?</span></span>](what-is-b2b.md)
- [<span data-ttu-id="d562f-183">How do Azure Active Directory admins add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="d562f-183">How do Azure Active Directory admins add B2B collaboration users?</span></span>](add-users-administrator.md)
- [<span data-ttu-id="d562f-184">B2B collaboration invitation redemption</span><span class="sxs-lookup"><span data-stu-id="d562f-184">B2B collaboration invitation redemption</span></span>](redemption-experience.md)
- [<span data-ttu-id="d562f-185">Azure AD B2B collaboration licensing</span><span class="sxs-lookup"><span data-stu-id="d562f-185">Azure AD B2B collaboration licensing</span></span>](licensing-guidance.md)
