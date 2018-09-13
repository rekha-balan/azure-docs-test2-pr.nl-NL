---
title: Get started Azure MFA in the cloud
description: Microsoft Azure Multi-Factor Authentication get started with conditional access
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 09/01/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: 0408b26e687dd31c408dbccc68f56e8198016c8f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967781"
---
# <a name="deploy-cloud-based-azure-multi-factor-authentication"></a><span data-ttu-id="86be7-103">Deploy cloud-based Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="86be7-103">Deploy cloud-based Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="86be7-104">Getting started with Azure Multi-Factor Authentication (Azure MFA) is a straightforward process.</span><span class="sxs-lookup"><span data-stu-id="86be7-104">Getting started with Azure Multi-Factor Authentication (Azure MFA) is a straightforward process.</span></span>

<span data-ttu-id="86be7-105">Before you start, make sure you have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="86be7-105">Before you start, make sure you have the following prerequisites:</span></span>

* <span data-ttu-id="86be7-106">A global administrator account in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="86be7-106">A global administrator account in your Azure AD tenant.</span></span> <span data-ttu-id="86be7-107">If you need help completing this step, see our article [Get started with Azure AD](../get-started-azure-ad.md).</span><span class="sxs-lookup"><span data-stu-id="86be7-107">If you need help completing this step, see our article [Get started with Azure AD](../get-started-azure-ad.md).</span></span>
* <span data-ttu-id="86be7-108">Correct licenses assigned to users.</span><span class="sxs-lookup"><span data-stu-id="86be7-108">Correct licenses assigned to users.</span></span> <span data-ttu-id="86be7-109">If you need more information see the topic [How to get Azure Multi-Factor Authentication](concept-mfa-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="86be7-109">If you need more information see the topic [How to get Azure Multi-Factor Authentication](concept-mfa-licensing.md).</span></span>

## <a name="choose-how-to-enable"></a><span data-ttu-id="86be7-110">Choose how to enable</span><span class="sxs-lookup"><span data-stu-id="86be7-110">Choose how to enable</span></span>

<span data-ttu-id="86be7-111">**Enabled by conditional access policy** - This method is discussed in this article.</span><span class="sxs-lookup"><span data-stu-id="86be7-111">**Enabled by conditional access policy** - This method is discussed in this article.</span></span> <span data-ttu-id="86be7-112">It is the most flexible means to enable two-step verification for your users.</span><span class="sxs-lookup"><span data-stu-id="86be7-112">It is the most flexible means to enable two-step verification for your users.</span></span> <span data-ttu-id="86be7-113">Enabling using conditional access policy only works for Azure MFA in the cloud and is a premium feature of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86be7-113">Enabling using conditional access policy only works for Azure MFA in the cloud and is a premium feature of Azure AD.</span></span>

<span data-ttu-id="86be7-114">Enabled by Azure AD Identity Protection - This method uses the Azure AD Identity Protection risk policy to require two-step verification based only on sign-in risk for all cloud applications.</span><span class="sxs-lookup"><span data-stu-id="86be7-114">Enabled by Azure AD Identity Protection - This method uses the Azure AD Identity Protection risk policy to require two-step verification based only on sign-in risk for all cloud applications.</span></span> <span data-ttu-id="86be7-115">This method requires Azure Active Directory P2 licensing.</span><span class="sxs-lookup"><span data-stu-id="86be7-115">This method requires Azure Active Directory P2 licensing.</span></span> <span data-ttu-id="86be7-116">More information on this method can be found in [Azure Active Directory Identity Protection](../identity-protection/overview.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="86be7-116">More information on this method can be found in [Azure Active Directory Identity Protection](../identity-protection/overview.md#risky-sign-ins).</span></span>

<span data-ttu-id="86be7-117">Enabled by changing user state - This is the traditional method for requiring two-step verification.</span><span class="sxs-lookup"><span data-stu-id="86be7-117">Enabled by changing user state - This is the traditional method for requiring two-step verification.</span></span> <span data-ttu-id="86be7-118">It works with both Azure MFA in the cloud and Azure MFA Server.</span><span class="sxs-lookup"><span data-stu-id="86be7-118">It works with both Azure MFA in the cloud and Azure MFA Server.</span></span> <span data-ttu-id="86be7-119">Using this method requires users to perform two-step verification **every time** they sign in and overrides conditional access policies.</span><span class="sxs-lookup"><span data-stu-id="86be7-119">Using this method requires users to perform two-step verification **every time** they sign in and overrides conditional access policies.</span></span> <span data-ttu-id="86be7-120">More information on this method can be found in [How to require two-step verification for a user](howto-mfa-userstates.md).</span><span class="sxs-lookup"><span data-stu-id="86be7-120">More information on this method can be found in [How to require two-step verification for a user](howto-mfa-userstates.md).</span></span>

> [!Note]
> <span data-ttu-id="86be7-121">More information about licenses and pricing can be found on the [Azure AD](https://azure.microsoft.com/pricing/details/active-directory/
) and [Multi-Factor Authentication](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) pricing pages.</span><span class="sxs-lookup"><span data-stu-id="86be7-121">More information about licenses and pricing can be found on the [Azure AD](https://azure.microsoft.com/pricing/details/active-directory/
) and [Multi-Factor Authentication](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) pricing pages.</span></span>

## <a name="choose-authentication-methods"></a><span data-ttu-id="86be7-122">Choose authentication methods</span><span class="sxs-lookup"><span data-stu-id="86be7-122">Choose authentication methods</span></span>

<span data-ttu-id="86be7-123">Enable at least one authentication method for your users based on your organization's requirements.</span><span class="sxs-lookup"><span data-stu-id="86be7-123">Enable at least one authentication method for your users based on your organization's requirements.</span></span> <span data-ttu-id="86be7-124">We find that when enabled for users the Microsoft Authenticator app provides the best user experience.</span><span class="sxs-lookup"><span data-stu-id="86be7-124">We find that when enabled for users the Microsoft Authenticator app provides the best user experience.</span></span> <span data-ttu-id="86be7-125">If you need to understand which methods are available and how to set them see the article [What are authentication methods](concept-authentication-methods.md).</span><span class="sxs-lookup"><span data-stu-id="86be7-125">If you need to understand which methods are available and how to set them see the article [What are authentication methods](concept-authentication-methods.md).</span></span>

## <a name="get-users-to-enroll"></a><span data-ttu-id="86be7-126">Get users to enroll</span><span class="sxs-lookup"><span data-stu-id="86be7-126">Get users to enroll</span></span>

<span data-ttu-id="86be7-127">Once you enable the conditional access policy, users will be forced to enroll the next time they use an app protected with the policy.</span><span class="sxs-lookup"><span data-stu-id="86be7-127">Once you enable the conditional access policy, users will be forced to enroll the next time they use an app protected with the policy.</span></span> <span data-ttu-id="86be7-128">If you enable a policy requiring MFA for all users on all cloud apps this action could cause headaches for your users and your helpdesk.</span><span class="sxs-lookup"><span data-stu-id="86be7-128">If you enable a policy requiring MFA for all users on all cloud apps this action could cause headaches for your users and your helpdesk.</span></span> <span data-ttu-id="86be7-129">The recommendation is to ask users to register authentication methods beforehand using the registration portal at [https://aka.ms/mfasetup](https://aka.ms/mfasetup).</span><span class="sxs-lookup"><span data-stu-id="86be7-129">The recommendation is to ask users to register authentication methods beforehand using the registration portal at [https://aka.ms/mfasetup](https://aka.ms/mfasetup).</span></span> <span data-ttu-id="86be7-130">Many organizations find that creating posters, table cards, and email messages helps drive adoption.</span><span class="sxs-lookup"><span data-stu-id="86be7-130">Many organizations find that creating posters, table cards, and email messages helps drive adoption.</span></span>

## <a name="enable-multi-factor-authentication-with-conditional-access"></a><span data-ttu-id="86be7-131">Enable Multi-Factor Authentication with Conditional Access</span><span class="sxs-lookup"><span data-stu-id="86be7-131">Enable Multi-Factor Authentication with Conditional Access</span></span>

<span data-ttu-id="86be7-132">Sign in to the [Azure portal](https://portal.azure.com) using a global administrator account.</span><span class="sxs-lookup"><span data-stu-id="86be7-132">Sign in to the [Azure portal](https://portal.azure.com) using a global administrator account.</span></span>

### <a name="choose-verification-options"></a><span data-ttu-id="86be7-133">Choose verification options</span><span class="sxs-lookup"><span data-stu-id="86be7-133">Choose verification options</span></span>

<span data-ttu-id="86be7-134">Before enabling Azure Multi-Factor Authentication, your organization must determine what verification options they allow.</span><span class="sxs-lookup"><span data-stu-id="86be7-134">Before enabling Azure Multi-Factor Authentication, your organization must determine what verification options they allow.</span></span> <span data-ttu-id="86be7-135">For the purpose of this exercise, you enable call to phone and text message to phone as they are generic options that most are able to use.</span><span class="sxs-lookup"><span data-stu-id="86be7-135">For the purpose of this exercise, you enable call to phone and text message to phone as they are generic options that most are able to use.</span></span> <span data-ttu-id="86be7-136">More information regarding authentication methods, and their usage, can be found in the article, [What are authentication methods?](concept-authentication-methods.md)</span><span class="sxs-lookup"><span data-stu-id="86be7-136">More information regarding authentication methods, and their usage, can be found in the article, [What are authentication methods?](concept-authentication-methods.md)</span></span>

1. <span data-ttu-id="86be7-137">Browse to **Azure Active Directory**, **Users**, **Multi-Factor Authentication**
   ![Accessing the Multi-Factor Authentication portal from Azure AD Users blade in Azure portal](media/howto-mfa-getstarted/users-mfa.png)</span><span class="sxs-lookup"><span data-stu-id="86be7-137">Browse to **Azure Active Directory**, **Users**, **Multi-Factor Authentication**
![Accessing the Multi-Factor Authentication portal from Azure AD Users blade in Azure portal](media/howto-mfa-getstarted/users-mfa.png)</span></span> 
2. <span data-ttu-id="86be7-138">In the new tab that opens browse to **service settings**</span><span class="sxs-lookup"><span data-stu-id="86be7-138">In the new tab that opens browse to **service settings**</span></span>
3. <span data-ttu-id="86be7-139">Under **verification options**, check the following boxes for methods available to users</span><span class="sxs-lookup"><span data-stu-id="86be7-139">Under **verification options**, check the following boxes for methods available to users</span></span>
   * <span data-ttu-id="86be7-140">Call to phone</span><span class="sxs-lookup"><span data-stu-id="86be7-140">Call to phone</span></span>
   * <span data-ttu-id="86be7-141">Text message to phone</span><span class="sxs-lookup"><span data-stu-id="86be7-141">Text message to phone</span></span>

   ![Configuring verification methods in the Multi-Factor Authentication service settings tab](media/howto-mfa-getstarted/mfa-servicesettings-verificationoptions.png)

4. <span data-ttu-id="86be7-143">Click on **Save**</span><span class="sxs-lookup"><span data-stu-id="86be7-143">Click on **Save**</span></span>
5. <span data-ttu-id="86be7-144">Close the **service settings** tab</span><span class="sxs-lookup"><span data-stu-id="86be7-144">Close the **service settings** tab</span></span>

### <a name="create-conditional-access-policy"></a><span data-ttu-id="86be7-145">Create conditional access policy</span><span class="sxs-lookup"><span data-stu-id="86be7-145">Create conditional access policy</span></span>

1. <span data-ttu-id="86be7-146">Sign in to the [Azure portal](https://portal.azure.com) using a global administrator account.</span><span class="sxs-lookup"><span data-stu-id="86be7-146">Sign in to the [Azure portal](https://portal.azure.com) using a global administrator account.</span></span>
1. <span data-ttu-id="86be7-147">Browse to **Azure Active Directory**, **Conditional access**</span><span class="sxs-lookup"><span data-stu-id="86be7-147">Browse to **Azure Active Directory**, **Conditional access**</span></span>
1. <span data-ttu-id="86be7-148">Select **New policy**</span><span class="sxs-lookup"><span data-stu-id="86be7-148">Select **New policy**</span></span>
1. <span data-ttu-id="86be7-149">Provide a meaningful name for your policy</span><span class="sxs-lookup"><span data-stu-id="86be7-149">Provide a meaningful name for your policy</span></span>
1. <span data-ttu-id="86be7-150">Under **users and groups**</span><span class="sxs-lookup"><span data-stu-id="86be7-150">Under **users and groups**</span></span>
   * <span data-ttu-id="86be7-151">On the **Include** tab, select the **All users** radio button</span><span class="sxs-lookup"><span data-stu-id="86be7-151">On the **Include** tab, select the **All users** radio button</span></span>
   * <span data-ttu-id="86be7-152">RECOMMENDED: On the **Exclude** tab, check the box for **Users and groups** and choose a group to be used for exclusions when users do not have access to their authentication methods.</span><span class="sxs-lookup"><span data-stu-id="86be7-152">RECOMMENDED: On the **Exclude** tab, check the box for **Users and groups** and choose a group to be used for exclusions when users do not have access to their authentication methods.</span></span>
   * <span data-ttu-id="86be7-153">Click **Done**</span><span class="sxs-lookup"><span data-stu-id="86be7-153">Click **Done**</span></span>
1. <span data-ttu-id="86be7-154">Under **Cloud apps**, select the **All cloud apps** radio button</span><span class="sxs-lookup"><span data-stu-id="86be7-154">Under **Cloud apps**, select the **All cloud apps** radio button</span></span>
   * <span data-ttu-id="86be7-155">OPTIONALLY: On the **Exclude** tab, choose cloud apps that your organization does not require MFA for.</span><span class="sxs-lookup"><span data-stu-id="86be7-155">OPTIONALLY: On the **Exclude** tab, choose cloud apps that your organization does not require MFA for.</span></span>
   * <span data-ttu-id="86be7-156">Click **Done**</span><span class="sxs-lookup"><span data-stu-id="86be7-156">Click **Done**</span></span>
1. <span data-ttu-id="86be7-157">Under **Conditions** section</span><span class="sxs-lookup"><span data-stu-id="86be7-157">Under **Conditions** section</span></span>
   * <span data-ttu-id="86be7-158">OPTIONALLY: If you have enabled Azure Identity Protection, you can choose to evaluate sign-in risk as part of the policy.</span><span class="sxs-lookup"><span data-stu-id="86be7-158">OPTIONALLY: If you have enabled Azure Identity Protection, you can choose to evaluate sign-in risk as part of the policy.</span></span>
   * <span data-ttu-id="86be7-159">OPTIONALLY: If you have configured trusted locations or named locations, you can specify to include or exclude those locations from the policy.</span><span class="sxs-lookup"><span data-stu-id="86be7-159">OPTIONALLY: If you have configured trusted locations or named locations, you can specify to include or exclude those locations from the policy.</span></span>
1. <span data-ttu-id="86be7-160">Under **Grant**, make sure the **Grant access** radio button is selected</span><span class="sxs-lookup"><span data-stu-id="86be7-160">Under **Grant**, make sure the **Grant access** radio button is selected</span></span>
    * <span data-ttu-id="86be7-161">Check the box for **Require multi-factor authentication**</span><span class="sxs-lookup"><span data-stu-id="86be7-161">Check the box for **Require multi-factor authentication**</span></span>
    * <span data-ttu-id="86be7-162">Click **Select**</span><span class="sxs-lookup"><span data-stu-id="86be7-162">Click **Select**</span></span>
1. <span data-ttu-id="86be7-163">Skip the **Session** section</span><span class="sxs-lookup"><span data-stu-id="86be7-163">Skip the **Session** section</span></span>
1. <span data-ttu-id="86be7-164">Set the **Enable policy** toggle to **On**</span><span class="sxs-lookup"><span data-stu-id="86be7-164">Set the **Enable policy** toggle to **On**</span></span>
1. <span data-ttu-id="86be7-165">Click **Create**</span><span class="sxs-lookup"><span data-stu-id="86be7-165">Click **Create**</span></span>

![Create a conditional access policy to enable MFA for Azure portal users in pilot group](media/howto-mfa-getstarted/conditionalaccess-newpolicy.png)

### <a name="test-azure-multi-factor-authentication"></a><span data-ttu-id="86be7-167">Test Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="86be7-167">Test Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="86be7-168">To confirm that your conditional access policy works, test logging in to a resource that should not require MFA and then to the Azure portal that requires MFA.</span><span class="sxs-lookup"><span data-stu-id="86be7-168">To confirm that your conditional access policy works, test logging in to a resource that should not require MFA and then to the Azure portal that requires MFA.</span></span>

1. <span data-ttu-id="86be7-169">Open a new browser window in InPrivate or incognito mode and browse to [https://account.activedirectory.windowsazure.com](https://account.activedirectory.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="86be7-169">Open a new browser window in InPrivate or incognito mode and browse to [https://account.activedirectory.windowsazure.com](https://account.activedirectory.windowsazure.com).</span></span>
   * <span data-ttu-id="86be7-170">Log in with the test user created as part of the prerequisites section of this article and note that it should not ask you to complete MFA.</span><span class="sxs-lookup"><span data-stu-id="86be7-170">Log in with the test user created as part of the prerequisites section of this article and note that it should not ask you to complete MFA.</span></span>
   * <span data-ttu-id="86be7-171">Close the browser window</span><span class="sxs-lookup"><span data-stu-id="86be7-171">Close the browser window</span></span>
2. <span data-ttu-id="86be7-172">Open a new browser window in InPrivate or incognito mode and browse to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="86be7-172">Open a new browser window in InPrivate or incognito mode and browse to [https://portal.azure.com](https://portal.azure.com).</span></span>
   * <span data-ttu-id="86be7-173">Log in with the test user created as part of the prerequisites section of this article and note that you should now be required to register for and use Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="86be7-173">Log in with the test user created as part of the prerequisites section of this article and note that you should now be required to register for and use Azure Multi-Factor Authentication.</span></span>
   * <span data-ttu-id="86be7-174">Close the browser window</span><span class="sxs-lookup"><span data-stu-id="86be7-174">Close the browser window</span></span>

## <a name="next-steps"></a><span data-ttu-id="86be7-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="86be7-175">Next steps</span></span>

<span data-ttu-id="86be7-176">Congratulations, you have set up Azure Multi-Factor Authentication in the cloud.</span><span class="sxs-lookup"><span data-stu-id="86be7-176">Congratulations, you have set up Azure Multi-Factor Authentication in the cloud.</span></span>

<span data-ttu-id="86be7-177">To configure additional settings like trusted IPs, custom voice messages, and fraud alerts, see the article [Configure Azure Multi-Factor Authentication settings](howto-mfa-mfasettings.md)</span><span class="sxs-lookup"><span data-stu-id="86be7-177">To configure additional settings like trusted IPs, custom voice messages, and fraud alerts, see the article [Configure Azure Multi-Factor Authentication settings](howto-mfa-mfasettings.md)</span></span>

<span data-ttu-id="86be7-178">Information about managing user settings for Azure Multi-Factor Authentication can be found in the article [Manage user settings with Azure Multi-Factor Authentication in the cloud](howto-mfa-userdevicesettings.md)</span><span class="sxs-lookup"><span data-stu-id="86be7-178">Information about managing user settings for Azure Multi-Factor Authentication can be found in the article [Manage user settings with Azure Multi-Factor Authentication in the cloud](howto-mfa-userdevicesettings.md)</span></span>

[<span data-ttu-id="86be7-179">Enable converged registration for Azure Multi-Factor Authentication and Azure AD self-service password reset</span><span class="sxs-lookup"><span data-stu-id="86be7-179">Enable converged registration for Azure Multi-Factor Authentication and Azure AD self-service password reset</span></span>](concept-registration-mfa-sspr-converged.md)
