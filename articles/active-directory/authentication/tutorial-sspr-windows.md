---
title: Azure AD SSPR from the Windows 10 login screen
description: In this tutorial, you will enable password reset at the Windows 10 login screen to reduce helpdesk calls.
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: tutorial
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: 27f271a20af2bb9910f1cf7d63e6033d78e67b83
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868695"
---
# <a name="tutorial-azure-ad-password-reset-from-the-login-screen"></a><span data-ttu-id="63b94-103">Tutorial: Azure AD password reset from the login screen</span><span class="sxs-lookup"><span data-stu-id="63b94-103">Tutorial: Azure AD password reset from the login screen</span></span>

<span data-ttu-id="63b94-104">In this tutorial, you enable users to reset their passwords from the Windows 10 login screen.</span><span class="sxs-lookup"><span data-stu-id="63b94-104">In this tutorial, you enable users to reset their passwords from the Windows 10 login screen.</span></span> <span data-ttu-id="63b94-105">With the new Windows 10 April 2018 Update, users with **Azure AD joined** or **hybrid Azure AD joined** devices can use a “Reset password” link on their login screen.</span><span class="sxs-lookup"><span data-stu-id="63b94-105">With the new Windows 10 April 2018 Update, users with **Azure AD joined** or **hybrid Azure AD joined** devices can use a “Reset password” link on their login screen.</span></span> <span data-ttu-id="63b94-106">When users click this link, they are brought to the same self-service password reset (SSPR) experience they are familiar with.</span><span class="sxs-lookup"><span data-stu-id="63b94-106">When users click this link, they are brought to the same self-service password reset (SSPR) experience they are familiar with.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="63b94-107">Configure Reset password link using Intune</span><span class="sxs-lookup"><span data-stu-id="63b94-107">Configure Reset password link using Intune</span></span>
> * <span data-ttu-id="63b94-108">Optionally configure using the Windows Registry</span><span class="sxs-lookup"><span data-stu-id="63b94-108">Optionally configure using the Windows Registry</span></span>
> * <span data-ttu-id="63b94-109">Understand what your users will see</span><span class="sxs-lookup"><span data-stu-id="63b94-109">Understand what your users will see</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63b94-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="63b94-110">Prerequisites</span></span>

* <span data-ttu-id="63b94-111">Windows 10 April 2018 Update, or newer client that is:</span><span class="sxs-lookup"><span data-stu-id="63b94-111">Windows 10 April 2018 Update, or newer client that is:</span></span>
   * <span data-ttu-id="63b94-112">[Azure AD joined](../device-management-azure-portal.md) or</span><span class="sxs-lookup"><span data-stu-id="63b94-112">[Azure AD joined](../device-management-azure-portal.md) or</span></span> 
   * [<span data-ttu-id="63b94-113">Hybrid Azure AD joined</span><span class="sxs-lookup"><span data-stu-id="63b94-113">Hybrid Azure AD joined</span></span>](../device-management-hybrid-azuread-joined-devices-setup.md)
* <span data-ttu-id="63b94-114">Azure AD self-service password reset must be enabled.</span><span class="sxs-lookup"><span data-stu-id="63b94-114">Azure AD self-service password reset must be enabled.</span></span>

## <a name="configure-reset-password-link-using-intune"></a><span data-ttu-id="63b94-115">Configure Reset password link using Intune</span><span class="sxs-lookup"><span data-stu-id="63b94-115">Configure Reset password link using Intune</span></span>

<span data-ttu-id="63b94-116">Deploying the configuration change to enable password reset from the login screen using Intune is the most flexible method.</span><span class="sxs-lookup"><span data-stu-id="63b94-116">Deploying the configuration change to enable password reset from the login screen using Intune is the most flexible method.</span></span> <span data-ttu-id="63b94-117">Intune allows you to deploy the configuration change to a specific group of machines you define.</span><span class="sxs-lookup"><span data-stu-id="63b94-117">Intune allows you to deploy the configuration change to a specific group of machines you define.</span></span> <span data-ttu-id="63b94-118">This method requires Intune enrollment of the device.</span><span class="sxs-lookup"><span data-stu-id="63b94-118">This method requires Intune enrollment of the device.</span></span>

### <a name="create-a-device-configuration-policy-in-intune"></a><span data-ttu-id="63b94-119">Create a device configuration policy in Intune</span><span class="sxs-lookup"><span data-stu-id="63b94-119">Create a device configuration policy in Intune</span></span>

1. <span data-ttu-id="63b94-120">Sign in to the [Azure portal](https://portal.azure.com) and click on **Intune**.</span><span class="sxs-lookup"><span data-stu-id="63b94-120">Sign in to the [Azure portal](https://portal.azure.com) and click on **Intune**.</span></span>
2. <span data-ttu-id="63b94-121">Create a new device configuration profile by going to **Device configuration** > **Profiles** > **Create Profile**</span><span class="sxs-lookup"><span data-stu-id="63b94-121">Create a new device configuration profile by going to **Device configuration** > **Profiles** > **Create Profile**</span></span>
   * <span data-ttu-id="63b94-122">Provide a meaningful name for the profile</span><span class="sxs-lookup"><span data-stu-id="63b94-122">Provide a meaningful name for the profile</span></span>
   * <span data-ttu-id="63b94-123">Optionally provide a meaningful description of the profile</span><span class="sxs-lookup"><span data-stu-id="63b94-123">Optionally provide a meaningful description of the profile</span></span>
   * <span data-ttu-id="63b94-124">Platform **Windows 10 and later**</span><span class="sxs-lookup"><span data-stu-id="63b94-124">Platform **Windows 10 and later**</span></span>
   * <span data-ttu-id="63b94-125">Profile type **Custom**</span><span class="sxs-lookup"><span data-stu-id="63b94-125">Profile type **Custom**</span></span>

   <span data-ttu-id="63b94-126">![CreateProfile][CreateProfile]</span><span class="sxs-lookup"><span data-stu-id="63b94-126">![CreateProfile][CreateProfile]</span></span>

3. <span data-ttu-id="63b94-127">Configure **Settings**</span><span class="sxs-lookup"><span data-stu-id="63b94-127">Configure **Settings**</span></span>
   * <span data-ttu-id="63b94-128">**Add** the following OMA-URI Setting to enable the Reset password link</span><span class="sxs-lookup"><span data-stu-id="63b94-128">**Add** the following OMA-URI Setting to enable the Reset password link</span></span>
      * <span data-ttu-id="63b94-129">Provide a meaningful name to explain what the setting is doing</span><span class="sxs-lookup"><span data-stu-id="63b94-129">Provide a meaningful name to explain what the setting is doing</span></span>
      * <span data-ttu-id="63b94-130">Optionally provide a meaningful description of the setting</span><span class="sxs-lookup"><span data-stu-id="63b94-130">Optionally provide a meaningful description of the setting</span></span>
      * <span data-ttu-id="63b94-131">**OMA-URI** set to `./Vendor/MSFT/Policy/Config/Authentication/AllowAadPasswordReset`</span><span class="sxs-lookup"><span data-stu-id="63b94-131">**OMA-URI** set to `./Vendor/MSFT/Policy/Config/Authentication/AllowAadPasswordReset`</span></span>
      * <span data-ttu-id="63b94-132">**Data type** set to **Integer**</span><span class="sxs-lookup"><span data-stu-id="63b94-132">**Data type** set to **Integer**</span></span>
      * <span data-ttu-id="63b94-133">**Value** set to **1**</span><span class="sxs-lookup"><span data-stu-id="63b94-133">**Value** set to **1**</span></span>
      * <span data-ttu-id="63b94-134">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="63b94-134">Click **OK**</span></span>
   * <span data-ttu-id="63b94-135">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="63b94-135">Click **OK**</span></span>
4. <span data-ttu-id="63b94-136">Click **Create**</span><span class="sxs-lookup"><span data-stu-id="63b94-136">Click **Create**</span></span>

### <a name="assign-a-device-configuration-policy-in-intune"></a><span data-ttu-id="63b94-137">Assign a device configuration policy in Intune</span><span class="sxs-lookup"><span data-stu-id="63b94-137">Assign a device configuration policy in Intune</span></span>

#### <a name="create-a-group-to-apply-device-configuration-policy-to"></a><span data-ttu-id="63b94-138">Create a group to apply device configuration policy to</span><span class="sxs-lookup"><span data-stu-id="63b94-138">Create a group to apply device configuration policy to</span></span>

1. <span data-ttu-id="63b94-139">Sign in to the [Azure portal](https://portal.azure.com) and click on **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="63b94-139">Sign in to the [Azure portal](https://portal.azure.com) and click on **Azure Active Directory**.</span></span>
2. <span data-ttu-id="63b94-140">Browse to **Users and groups** > **All groups** > **New group**</span><span class="sxs-lookup"><span data-stu-id="63b94-140">Browse to **Users and groups** > **All groups** > **New group**</span></span>
3. <span data-ttu-id="63b94-141">Provide a name for the group and under **Membership type** choose **Assigned**</span><span class="sxs-lookup"><span data-stu-id="63b94-141">Provide a name for the group and under **Membership type** choose **Assigned**</span></span>
   * <span data-ttu-id="63b94-142">Under **Members**, choose the Azure AD joined Windows 10 devices that you want to apply the policy to.</span><span class="sxs-lookup"><span data-stu-id="63b94-142">Under **Members**, choose the Azure AD joined Windows 10 devices that you want to apply the policy to.</span></span>
   * <span data-ttu-id="63b94-143">Click **Select**</span><span class="sxs-lookup"><span data-stu-id="63b94-143">Click **Select**</span></span>
4. <span data-ttu-id="63b94-144">Click **Create**</span><span class="sxs-lookup"><span data-stu-id="63b94-144">Click **Create**</span></span>

<span data-ttu-id="63b94-145">More information on creating groups can be found in the article [Manage access to resources with Azure Active Directory groups](../fundamentals/active-directory-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="63b94-145">More information on creating groups can be found in the article [Manage access to resources with Azure Active Directory groups](../fundamentals/active-directory-manage-groups.md).</span></span>

#### <a name="assign-device-configuration-policy-to-device-group"></a><span data-ttu-id="63b94-146">Assign device configuration policy to device group</span><span class="sxs-lookup"><span data-stu-id="63b94-146">Assign device configuration policy to device group</span></span>

1. <span data-ttu-id="63b94-147">Sign in to the [Azure portal](https://portal.azure.com) and click on **Intune**.</span><span class="sxs-lookup"><span data-stu-id="63b94-147">Sign in to the [Azure portal](https://portal.azure.com) and click on **Intune**.</span></span>
2. <span data-ttu-id="63b94-148">Find the device configuration profile created previously by going to **Device configuration** > **Profiles** > Click on the profile created earlier</span><span class="sxs-lookup"><span data-stu-id="63b94-148">Find the device configuration profile created previously by going to **Device configuration** > **Profiles** > Click on the profile created earlier</span></span>
3. <span data-ttu-id="63b94-149">Assign the profile to a group of devices</span><span class="sxs-lookup"><span data-stu-id="63b94-149">Assign the profile to a group of devices</span></span> 
   * <span data-ttu-id="63b94-150">Click on **Assignments** > under **Include** > **Select groups to include**</span><span class="sxs-lookup"><span data-stu-id="63b94-150">Click on **Assignments** > under **Include** > **Select groups to include**</span></span>
   * <span data-ttu-id="63b94-151">Select the group created previously and click **Select**</span><span class="sxs-lookup"><span data-stu-id="63b94-151">Select the group created previously and click **Select**</span></span>
   * <span data-ttu-id="63b94-152">Click on **Save**</span><span class="sxs-lookup"><span data-stu-id="63b94-152">Click on **Save**</span></span>

   <span data-ttu-id="63b94-153">![Assignment][Assignment]</span><span class="sxs-lookup"><span data-stu-id="63b94-153">![Assignment][Assignment]</span></span>

<span data-ttu-id="63b94-154">You have now created and assigned a device configuration policy to enable the Reset password link on the login screen using Intune.</span><span class="sxs-lookup"><span data-stu-id="63b94-154">You have now created and assigned a device configuration policy to enable the Reset password link on the login screen using Intune.</span></span>

## <a name="configure-reset-password-link-using-the-registry"></a><span data-ttu-id="63b94-155">Configure Reset password link using the registry</span><span class="sxs-lookup"><span data-stu-id="63b94-155">Configure Reset password link using the registry</span></span>

1. <span data-ttu-id="63b94-156">Log in to the Windows PC using administrative credentials</span><span class="sxs-lookup"><span data-stu-id="63b94-156">Log in to the Windows PC using administrative credentials</span></span>
2. <span data-ttu-id="63b94-157">Run **regedit** as an administrator</span><span class="sxs-lookup"><span data-stu-id="63b94-157">Run **regedit** as an administrator</span></span>
3. <span data-ttu-id="63b94-158">Set the following registry key</span><span class="sxs-lookup"><span data-stu-id="63b94-158">Set the following registry key</span></span>
   * `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\AzureADAccount`
      * `"AllowPasswordReset"=dword:00000001`

## <a name="what-do-users-see"></a><span data-ttu-id="63b94-159">What do users see</span><span class="sxs-lookup"><span data-stu-id="63b94-159">What do users see</span></span>

<span data-ttu-id="63b94-160">Now that the policy is configured and assigned, what changes for the user?</span><span class="sxs-lookup"><span data-stu-id="63b94-160">Now that the policy is configured and assigned, what changes for the user?</span></span> <span data-ttu-id="63b94-161">How do they know that they can reset their password at the login screen?</span><span class="sxs-lookup"><span data-stu-id="63b94-161">How do they know that they can reset their password at the login screen?</span></span>

<span data-ttu-id="63b94-162">![LoginScreen][LoginScreen]</span><span class="sxs-lookup"><span data-stu-id="63b94-162">![LoginScreen][LoginScreen]</span></span>

<span data-ttu-id="63b94-163">When users attempt to log in, they now see a Reset password link that opens the self-service password reset experience at the login screen.</span><span class="sxs-lookup"><span data-stu-id="63b94-163">When users attempt to log in, they now see a Reset password link that opens the self-service password reset experience at the login screen.</span></span> <span data-ttu-id="63b94-164">This functionality allows users to reset their password without having to use another device to access a web browser.</span><span class="sxs-lookup"><span data-stu-id="63b94-164">This functionality allows users to reset their password without having to use another device to access a web browser.</span></span>
<span data-ttu-id="63b94-165">When users attempt to log in, they now see a Reset password link that opens the self-service password reset experience at the login screen.</span><span class="sxs-lookup"><span data-stu-id="63b94-165">When users attempt to log in, they now see a Reset password link that opens the self-service password reset experience at the login screen.</span></span> <span data-ttu-id="63b94-166">This functionality allows users to reset their password without having to use another device to access a web browser.</span><span class="sxs-lookup"><span data-stu-id="63b94-166">This functionality allows users to reset their password without having to use another device to access a web browser.</span></span>

<span data-ttu-id="63b94-167">Your users will find guidance for using this feature in [Reset your work or school password](../user-help/active-directory-passwords-update-your-own-password.md#reset-password-at-sign-in)</span><span class="sxs-lookup"><span data-stu-id="63b94-167">Your users will find guidance for using this feature in [Reset your work or school password](../user-help/active-directory-passwords-update-your-own-password.md#reset-password-at-sign-in)</span></span>

## <a name="common-issues"></a><span data-ttu-id="63b94-168">Common issues</span><span class="sxs-lookup"><span data-stu-id="63b94-168">Common issues</span></span>

<span data-ttu-id="63b94-169">When testing this functionality using Hyper-V, the "Reset password" link does not appear.</span><span class="sxs-lookup"><span data-stu-id="63b94-169">When testing this functionality using Hyper-V, the "Reset password" link does not appear.</span></span>

* <span data-ttu-id="63b94-170">Go to the VM you are using to test click on **View** and then uncheck **Enhanced session**.</span><span class="sxs-lookup"><span data-stu-id="63b94-170">Go to the VM you are using to test click on **View** and then uncheck **Enhanced session**.</span></span>

<span data-ttu-id="63b94-171">When testing this functionality using Remote Desktop, the "Reset password" link does not appear.</span><span class="sxs-lookup"><span data-stu-id="63b94-171">When testing this functionality using Remote Desktop, the "Reset password" link does not appear.</span></span>

* <span data-ttu-id="63b94-172">Password reset is not currently supported from a Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="63b94-172">Password reset is not currently supported from a Remote Desktop.</span></span>

<span data-ttu-id="63b94-173">If the Windows lockscreen is disabled using a registry key or group policy **Reset password** will not be availalbe.</span><span class="sxs-lookup"><span data-stu-id="63b94-173">If the Windows lockscreen is disabled using a registry key or group policy **Reset password** will not be availalbe.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="63b94-174">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="63b94-174">Clean up resources</span></span>

<span data-ttu-id="63b94-175">If you decide you no longer want to use the functionality you have configured as part of this tutorial, delete the Intune device configuration profile that you created or the registry key.</span><span class="sxs-lookup"><span data-stu-id="63b94-175">If you decide you no longer want to use the functionality you have configured as part of this tutorial, delete the Intune device configuration profile that you created or the registry key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63b94-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="63b94-176">Next steps</span></span>

<span data-ttu-id="63b94-177">In this tutorial, you have enabled users to reset their passwords from the Windows 10 login screen.</span><span class="sxs-lookup"><span data-stu-id="63b94-177">In this tutorial, you have enabled users to reset their passwords from the Windows 10 login screen.</span></span> <span data-ttu-id="63b94-178">Continue on to the next tutorial to see how Azure Identity Protection can be integrated into the self-service password reset and Multi-Factor Authentication experiences.</span><span class="sxs-lookup"><span data-stu-id="63b94-178">Continue on to the next tutorial to see how Azure Identity Protection can be integrated into the self-service password reset and Multi-Factor Authentication experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="63b94-179">Evaluate risk at sign in</span><span class="sxs-lookup"><span data-stu-id="63b94-179">Evaluate risk at sign in</span></span>](tutorial-risk-based-sspr-mfa.md)

[CreateProfile]: ./media/tutorial-sspr-windows/create-profile.png "Create Intune device configuration profile to enable Reset password link on the Windows 10 login screen"
[Assignment]: ./media/tutorial-sspr-windows/profile-assignment.png "Assign Intune device configuration policy to a group of Windows 10 devices"
[LoginScreen]: ./media/tutorial-sspr-windows/logon-reset-password.png "Reset password link at the Windows 10 login screen"
