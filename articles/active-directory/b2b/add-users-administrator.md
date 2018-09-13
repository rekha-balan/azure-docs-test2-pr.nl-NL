---
title: Add B2B collaboration users in the Azure portal - Azure Active Directory | Microsoft Docs
description: Shows how an admin can add guest users to their directory from a partner organization using Azure Active Directory (Azure AD) B2B collaboration.
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 07/10/2018
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 6dfa1f247a079bf801f28d1083c86d36a74117c5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870929"
---
# <a name="add-azure-active-directory-b2b-collaboration-users-in-the-azure-portal"></a><span data-ttu-id="8238e-103">Add Azure Active Directory B2B collaboration users in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8238e-103">Add Azure Active Directory B2B collaboration users in the Azure portal</span></span>

<span data-ttu-id="8238e-104">As a global administrator, or a user who is assigned any of the limited administrator directory roles, you can use the Azure portal to invite B2B collaboration users.</span><span class="sxs-lookup"><span data-stu-id="8238e-104">As a global administrator, or a user who is assigned any of the limited administrator directory roles, you can use the Azure portal to invite B2B collaboration users.</span></span> <span data-ttu-id="8238e-105">You can invite guest users to the directory, to a group, or to an application.</span><span class="sxs-lookup"><span data-stu-id="8238e-105">You can invite guest users to the directory, to a group, or to an application.</span></span> <span data-ttu-id="8238e-106">After you invite a user through any of these methods, the invited user's account is added to Azure Active Directory (Azure AD), with a user type of *Guest*.</span><span class="sxs-lookup"><span data-stu-id="8238e-106">After you invite a user through any of these methods, the invited user's account is added to Azure Active Directory (Azure AD), with a user type of *Guest*.</span></span> <span data-ttu-id="8238e-107">The guest user must then redeem their invitation to access resources.</span><span class="sxs-lookup"><span data-stu-id="8238e-107">The guest user must then redeem their invitation to access resources.</span></span>

<span data-ttu-id="8238e-108">After you add a guest user to the directory, you can either send the guest user a direct link to a shared app, or the guest user can click the redemption URL in the invitation email.</span><span class="sxs-lookup"><span data-stu-id="8238e-108">After you add a guest user to the directory, you can either send the guest user a direct link to a shared app, or the guest user can click the redemption URL in the invitation email.</span></span> <span data-ttu-id="8238e-109">For more information about the redemption process, see [B2B collaboration invitation redemption](redemption-experience.md).</span><span class="sxs-lookup"><span data-stu-id="8238e-109">For more information about the redemption process, see [B2B collaboration invitation redemption](redemption-experience.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8238e-110">You should follow the steps in [How-to: Add your organization's privacy info in Azure Active Directory](https://aka.ms/adprivacystatement) to add the URL of your organization's privacy statement.</span><span class="sxs-lookup"><span data-stu-id="8238e-110">You should follow the steps in [How-to: Add your organization's privacy info in Azure Active Directory](https://aka.ms/adprivacystatement) to add the URL of your organization's privacy statement.</span></span> <span data-ttu-id="8238e-111">As part of the first time invitation redemption process, an invited user must consent to your privacy terms to continue.</span><span class="sxs-lookup"><span data-stu-id="8238e-111">As part of the first time invitation redemption process, an invited user must consent to your privacy terms to continue.</span></span> 

## <a name="add-guest-users-to-the-directory"></a><span data-ttu-id="8238e-112">Add guest users to the directory</span><span class="sxs-lookup"><span data-stu-id="8238e-112">Add guest users to the directory</span></span>

<span data-ttu-id="8238e-113">To add B2B collaboration users to the directory, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="8238e-113">To add B2B collaboration users to the directory, follow these steps:</span></span>

1. <span data-ttu-id="8238e-114">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator.</span><span class="sxs-lookup"><span data-stu-id="8238e-114">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator.</span></span>
2. <span data-ttu-id="8238e-115">In the navigation pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8238e-115">In the navigation pane, select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="8238e-116">Under **Manage**, select **Users**.</span><span class="sxs-lookup"><span data-stu-id="8238e-116">Under **Manage**, select **Users**.</span></span>
4. <span data-ttu-id="8238e-117">Select **New guest user**.</span><span class="sxs-lookup"><span data-stu-id="8238e-117">Select **New guest user**.</span></span>

   ![Shows where New guest user is in the UI](./media/add-users-administrator/NewGuestUser-Directory.png) 
 
5. <span data-ttu-id="8238e-119">Under **User name**, enter the email address of the external user.</span><span class="sxs-lookup"><span data-stu-id="8238e-119">Under **User name**, enter the email address of the external user.</span></span> <span data-ttu-id="8238e-120">Optionally, include a welcome message.</span><span class="sxs-lookup"><span data-stu-id="8238e-120">Optionally, include a welcome message.</span></span> <span data-ttu-id="8238e-121">For example:</span><span class="sxs-lookup"><span data-stu-id="8238e-121">For example:</span></span>

   ![Shows where New guest user is in the UI](./media/add-users-administrator/InviteGuest.png) 

    > [!NOTE]
    > <span data-ttu-id="8238e-123">Some email providers allow users to add a plus symbol (+) and additional text to their email addresses to help with things like inbox filtering.</span><span class="sxs-lookup"><span data-stu-id="8238e-123">Some email providers allow users to add a plus symbol (+) and additional text to their email addresses to help with things like inbox filtering.</span></span> <span data-ttu-id="8238e-124">However, Azure AD doesn’t currently support plus symbols in email addresses.</span><span class="sxs-lookup"><span data-stu-id="8238e-124">However, Azure AD doesn’t currently support plus symbols in email addresses.</span></span> <span data-ttu-id="8238e-125">To avoid delivery issues, omit the plus symbol and any characters following it up to the @ symbol.</span><span class="sxs-lookup"><span data-stu-id="8238e-125">To avoid delivery issues, omit the plus symbol and any characters following it up to the @ symbol.</span></span>

6. <span data-ttu-id="8238e-126">Select **Invite** to automatically send the invitation to the guest user.</span><span class="sxs-lookup"><span data-stu-id="8238e-126">Select **Invite** to automatically send the invitation to the guest user.</span></span> 
 
<span data-ttu-id="8238e-127">After you send the invitation, the user account is automatically added to the directory as a guest.</span><span class="sxs-lookup"><span data-stu-id="8238e-127">After you send the invitation, the user account is automatically added to the directory as a guest.</span></span>


![Shows B2B user with Guest user type](./media/add-users-administrator/GuestUserType.png)  

## <a name="add-guest-users-to-a-group"></a><span data-ttu-id="8238e-129">Add guest users to a group</span><span class="sxs-lookup"><span data-stu-id="8238e-129">Add guest users to a group</span></span>
<span data-ttu-id="8238e-130">If you need to manually add B2B collaboration users to a group as an Azure AD administrator, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="8238e-130">If you need to manually add B2B collaboration users to a group as an Azure AD administrator, follow these steps:</span></span>

1. <span data-ttu-id="8238e-131">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator.</span><span class="sxs-lookup"><span data-stu-id="8238e-131">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator.</span></span>
2. <span data-ttu-id="8238e-132">In the navigation pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8238e-132">In the navigation pane, select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="8238e-133">Under **Manage**, select **Groups**.</span><span class="sxs-lookup"><span data-stu-id="8238e-133">Under **Manage**, select **Groups**.</span></span>
4. <span data-ttu-id="8238e-134">Select a group (or click **New group** to create a new one).</span><span class="sxs-lookup"><span data-stu-id="8238e-134">Select a group (or click **New group** to create a new one).</span></span> <span data-ttu-id="8238e-135">It's a good idea to include in the group description that the group contains B2B guest users.</span><span class="sxs-lookup"><span data-stu-id="8238e-135">It's a good idea to include in the group description that the group contains B2B guest users.</span></span>
5. <span data-ttu-id="8238e-136">Select **Members**.</span><span class="sxs-lookup"><span data-stu-id="8238e-136">Select **Members**.</span></span> 
6. <span data-ttu-id="8238e-137">Do one of the following:</span><span class="sxs-lookup"><span data-stu-id="8238e-137">Do one of the following:</span></span>
   - <span data-ttu-id="8238e-138">If the guest user already exists in the directory, search for the B2B user.</span><span class="sxs-lookup"><span data-stu-id="8238e-138">If the guest user already exists in the directory, search for the B2B user.</span></span> <span data-ttu-id="8238e-139">Select the user, and then click **Select** to add the user to the group.</span><span class="sxs-lookup"><span data-stu-id="8238e-139">Select the user, and then click **Select** to add the user to the group.</span></span>
   - <span data-ttu-id="8238e-140">If the guest user does not already exist in the directory, invite them to the group by typing their email address in the search box, typing an optional personal message, and then clicking **Select**.</span><span class="sxs-lookup"><span data-stu-id="8238e-140">If the guest user does not already exist in the directory, invite them to the group by typing their email address in the search box, typing an optional personal message, and then clicking **Select**.</span></span> <span data-ttu-id="8238e-141">The invitation automatically goes out to the invited user.</span><span class="sxs-lookup"><span data-stu-id="8238e-141">The invitation automatically goes out to the invited user.</span></span>
     
     ![Add invite button to add guest members](./media/add-users-administrator/GroupInvite.png)
   
<span data-ttu-id="8238e-143">You can also use dynamic groups with Azure AD B2B collaboration.</span><span class="sxs-lookup"><span data-stu-id="8238e-143">You can also use dynamic groups with Azure AD B2B collaboration.</span></span> <span data-ttu-id="8238e-144">For more information, see [Dynamic groups and Azure Active Directory B2B collaboration](use-dynamic-groups.md).</span><span class="sxs-lookup"><span data-stu-id="8238e-144">For more information, see [Dynamic groups and Azure Active Directory B2B collaboration](use-dynamic-groups.md).</span></span>

## <a name="add-guest-users-to-an-application"></a><span data-ttu-id="8238e-145">Add guest users to an application</span><span class="sxs-lookup"><span data-stu-id="8238e-145">Add guest users to an application</span></span>

<span data-ttu-id="8238e-146">To add B2B collaboration users to an application as an Azure AD administrator, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="8238e-146">To add B2B collaboration users to an application as an Azure AD administrator, follow these steps:</span></span>

1. <span data-ttu-id="8238e-147">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator.</span><span class="sxs-lookup"><span data-stu-id="8238e-147">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator.</span></span>
2. <span data-ttu-id="8238e-148">In the navigation pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8238e-148">In the navigation pane, select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="8238e-149">Under **Manage**, select **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8238e-149">Under **Manage**, select **Enterprise applications** > **All applications**.</span></span>
4. <span data-ttu-id="8238e-150">Select the application to which you want to add guest users.</span><span class="sxs-lookup"><span data-stu-id="8238e-150">Select the application to which you want to add guest users.</span></span>
5. <span data-ttu-id="8238e-151">On the application's dashboard, select **Total Users** to open the **Users and groups** pane.</span><span class="sxs-lookup"><span data-stu-id="8238e-151">On the application's dashboard, select **Total Users** to open the **Users and groups** pane.</span></span>

    ![Total Users button to add open Users and Groups](./media/add-users-administrator/AppUsersAndGroups.png)

6. <span data-ttu-id="8238e-153">Select **Add user**.</span><span class="sxs-lookup"><span data-stu-id="8238e-153">Select **Add user**.</span></span>
7. <span data-ttu-id="8238e-154">Under **Add Assignment**, select **User and groups**.</span><span class="sxs-lookup"><span data-stu-id="8238e-154">Under **Add Assignment**, select **User and groups**.</span></span>
8. <span data-ttu-id="8238e-155">Do one of the following:</span><span class="sxs-lookup"><span data-stu-id="8238e-155">Do one of the following:</span></span>
   - <span data-ttu-id="8238e-156">If the guest user already exists in the directory, search for the B2B user.</span><span class="sxs-lookup"><span data-stu-id="8238e-156">If the guest user already exists in the directory, search for the B2B user.</span></span> <span data-ttu-id="8238e-157">Select the user, click **Select**, and then click **Assign** to add the user to the app.</span><span class="sxs-lookup"><span data-stu-id="8238e-157">Select the user, click **Select**, and then click **Assign** to add the user to the app.</span></span>
   - <span data-ttu-id="8238e-158">If the guest user does not already exist in the directory, select **Invite**.</span><span class="sxs-lookup"><span data-stu-id="8238e-158">If the guest user does not already exist in the directory, select **Invite**.</span></span>
           
       ![Add invite button to add guest members](./media/add-users-administrator/AppInviteUsers.png)
   
      <span data-ttu-id="8238e-160">Under **Invite a guest**, enter the email address, type an optional personal message, and then select **Invite**.</span><span class="sxs-lookup"><span data-stu-id="8238e-160">Under **Invite a guest**, enter the email address, type an optional personal message, and then select **Invite**.</span></span> <span data-ttu-id="8238e-161">Click **Select**, and then click **Assign** to add the user to the app.</span><span class="sxs-lookup"><span data-stu-id="8238e-161">Click **Select**, and then click **Assign** to add the user to the app.</span></span> <span data-ttu-id="8238e-162">An invitation automatically goes out to the invited user.</span><span class="sxs-lookup"><span data-stu-id="8238e-162">An invitation automatically goes out to the invited user.</span></span>

9. <span data-ttu-id="8238e-163">The guest user appears in the application's **Users and groups** list with the assigned role of **Default Access**.</span><span class="sxs-lookup"><span data-stu-id="8238e-163">The guest user appears in the application's **Users and groups** list with the assigned role of **Default Access**.</span></span> <span data-ttu-id="8238e-164">If you want to change the role, do the following:</span><span class="sxs-lookup"><span data-stu-id="8238e-164">If you want to change the role, do the following:</span></span>
   - <span data-ttu-id="8238e-165">Select the guest user, and then select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="8238e-165">Select the guest user, and then select **Edit**.</span></span> 
   - <span data-ttu-id="8238e-166">Under **Edit Assignment**, click **Select Role**, and select the role you want to assign to the selected user.</span><span class="sxs-lookup"><span data-stu-id="8238e-166">Under **Edit Assignment**, click **Select Role**, and select the role you want to assign to the selected user.</span></span>
   - <span data-ttu-id="8238e-167">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="8238e-167">Click **Select**.</span></span>
   - <span data-ttu-id="8238e-168">Click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="8238e-168">Click **Assign**.</span></span>
 
## <a name="resend-invitations-to-guest-users"></a><span data-ttu-id="8238e-169">Resend invitations to guest users</span><span class="sxs-lookup"><span data-stu-id="8238e-169">Resend invitations to guest users</span></span>

<span data-ttu-id="8238e-170">If a guest user has not yet redeemed their invitation, you can resend the invitation email.</span><span class="sxs-lookup"><span data-stu-id="8238e-170">If a guest user has not yet redeemed their invitation, you can resend the invitation email.</span></span>

1. <span data-ttu-id="8238e-171">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator.</span><span class="sxs-lookup"><span data-stu-id="8238e-171">Sign in to the [Azure portal](https://portal.azure.com) as an Azure AD administrator.</span></span>
2. <span data-ttu-id="8238e-172">In the navigation pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8238e-172">In the navigation pane, select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="8238e-173">Under **Manage**, select **Users**.</span><span class="sxs-lookup"><span data-stu-id="8238e-173">Under **Manage**, select **Users**.</span></span>
5. <span data-ttu-id="8238e-174">Select the user account.</span><span class="sxs-lookup"><span data-stu-id="8238e-174">Select the user account.</span></span>
6. <span data-ttu-id="8238e-175">Under **Manage**, select **Profile**.</span><span class="sxs-lookup"><span data-stu-id="8238e-175">Under **Manage**, select **Profile**.</span></span>
7. <span data-ttu-id="8238e-176">If the user has not yet accepted the invitation, a **Resend invitation** option is available.</span><span class="sxs-lookup"><span data-stu-id="8238e-176">If the user has not yet accepted the invitation, a **Resend invitation** option is available.</span></span> <span data-ttu-id="8238e-177">Select this button to resend.</span><span class="sxs-lookup"><span data-stu-id="8238e-177">Select this button to resend.</span></span>

   ![Resend invitation option in the user profile](./media/add-users-administrator/Resend-Invitation.png)

> [!NOTE]
> <span data-ttu-id="8238e-179">If you resend an invitation that originally directed the user to a specific app, understand that the link in the new invitation takes the user to the top-level Access Panel instead.</span><span class="sxs-lookup"><span data-stu-id="8238e-179">If you resend an invitation that originally directed the user to a specific app, understand that the link in the new invitation takes the user to the top-level Access Panel instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8238e-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="8238e-180">Next steps</span></span>

- <span data-ttu-id="8238e-181">To learn how non-Azure AD admins can add B2B guest users, see [How do information workers add B2B collaboration users?](add-users-information-worker.md)</span><span class="sxs-lookup"><span data-stu-id="8238e-181">To learn how non-Azure AD admins can add B2B guest users, see [How do information workers add B2B collaboration users?](add-users-information-worker.md)</span></span>
- <span data-ttu-id="8238e-182">For information about the invitation email, see [The elements of the B2B collaboration invitation email](invitation-email-elements.md).</span><span class="sxs-lookup"><span data-stu-id="8238e-182">For information about the invitation email, see [The elements of the B2B collaboration invitation email](invitation-email-elements.md).</span></span>

