---
title: Risk-based MFA and SSPR with Azure Identity Protection
description: In this tutorial, you will enable Azure Identity Protection integrations, for Multi-Factor Authentication and self-service password reset, to reduce risky behavior.
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: tutorial
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: fb9ec69476253eaa559fe763dcc2c92994505602
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866706"
---
# <a name="tutorial-use-risk-events-to-trigger-multi-factor-authentication-and-password-changes"></a><span data-ttu-id="ba1ea-103">Tutorial: Use risk events to trigger Multi-Factor Authentication and password changes</span><span class="sxs-lookup"><span data-stu-id="ba1ea-103">Tutorial: Use risk events to trigger Multi-Factor Authentication and password changes</span></span>

<span data-ttu-id="ba1ea-104">In this tutorial, you will enable features of Azure Active Directory (Azure AD) Identity Protection, an Azure AD Premium P2 feature that is more than just a monitoring and reporting tool.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-104">In this tutorial, you will enable features of Azure Active Directory (Azure AD) Identity Protection, an Azure AD Premium P2 feature that is more than just a monitoring and reporting tool.</span></span> <span data-ttu-id="ba1ea-105">To protect your organization's identities, you can configure risk-based policies that automatically respond to risky behaviors.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-105">To protect your organization's identities, you can configure risk-based policies that automatically respond to risky behaviors.</span></span> <span data-ttu-id="ba1ea-106">These policies, can either automatically block or initiate remediation, including requiring password changes and enforcing Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-106">These policies, can either automatically block or initiate remediation, including requiring password changes and enforcing Multi-Factor Authentication.</span></span>

<span data-ttu-id="ba1ea-107">Azure AD Identity Protection policies can be used in addition to existing conditional access policies as an extra layer of protection.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-107">Azure AD Identity Protection policies can be used in addition to existing conditional access policies as an extra layer of protection.</span></span> <span data-ttu-id="ba1ea-108">Your users may never trigger a risky behavior requiring one of these policies, but as an administrator you know they are protected.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-108">Your users may never trigger a risky behavior requiring one of these policies, but as an administrator you know they are protected.</span></span>

<span data-ttu-id="ba1ea-109">Some items that may trigger a risk event include:</span><span class="sxs-lookup"><span data-stu-id="ba1ea-109">Some items that may trigger a risk event include:</span></span>

* <span data-ttu-id="ba1ea-110">Users with leaked credentials</span><span class="sxs-lookup"><span data-stu-id="ba1ea-110">Users with leaked credentials</span></span>
* <span data-ttu-id="ba1ea-111">Sign-ins from anonymous IP addresses</span><span class="sxs-lookup"><span data-stu-id="ba1ea-111">Sign-ins from anonymous IP addresses</span></span>
* <span data-ttu-id="ba1ea-112">Impossible travel to atypical locations</span><span class="sxs-lookup"><span data-stu-id="ba1ea-112">Impossible travel to atypical locations</span></span>
* <span data-ttu-id="ba1ea-113">Sign-ins from infected devices</span><span class="sxs-lookup"><span data-stu-id="ba1ea-113">Sign-ins from infected devices</span></span>
* <span data-ttu-id="ba1ea-114">Sign-ins from IP addresses with suspicious activity</span><span class="sxs-lookup"><span data-stu-id="ba1ea-114">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="ba1ea-115">Sign-ins from unfamiliar locations</span><span class="sxs-lookup"><span data-stu-id="ba1ea-115">Sign-ins from unfamiliar locations</span></span>

<span data-ttu-id="ba1ea-116">More information about Azure AD Identity Protection can be found in the article [What is Azure AD Identity Protection](../active-directory-identityprotection.md)</span><span class="sxs-lookup"><span data-stu-id="ba1ea-116">More information about Azure AD Identity Protection can be found in the article [What is Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ba1ea-117">Enable Azure MFA registration</span><span class="sxs-lookup"><span data-stu-id="ba1ea-117">Enable Azure MFA registration</span></span>
> * <span data-ttu-id="ba1ea-118">Enable risk-based password changes</span><span class="sxs-lookup"><span data-stu-id="ba1ea-118">Enable risk-based password changes</span></span>
> * <span data-ttu-id="ba1ea-119">Enable risk-based Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ba1ea-119">Enable risk-based Multi-Factor Authentication</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba1ea-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ba1ea-120">Prerequisites</span></span>

* <span data-ttu-id="ba1ea-121">Access to a working Azure AD tenant with at least a trial Azure AD Premium P2 license assigned.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-121">Access to a working Azure AD tenant with at least a trial Azure AD Premium P2 license assigned.</span></span>
* <span data-ttu-id="ba1ea-122">An account with Global Administrator privileges in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-122">An account with Global Administrator privileges in your Azure AD tenant.</span></span>
* <span data-ttu-id="ba1ea-123">Have completed the previous self-service password reset (SSPR) and Multi-Factor Authentication (MFA) tutorials.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-123">Have completed the previous self-service password reset (SSPR) and Multi-Factor Authentication (MFA) tutorials.</span></span>

## <a name="enable-risk-based-policies-for-sspr-and-mfa"></a><span data-ttu-id="ba1ea-124">Enable risk-based policies for SSPR and MFA</span><span class="sxs-lookup"><span data-stu-id="ba1ea-124">Enable risk-based policies for SSPR and MFA</span></span>

<span data-ttu-id="ba1ea-125">Enabling the risk-based policies is a straightforward process.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-125">Enabling the risk-based policies is a straightforward process.</span></span> <span data-ttu-id="ba1ea-126">The steps below will guide you through a sample configuration.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-126">The steps below will guide you through a sample configuration.</span></span>

### <a name="enable-users-to-register-for-multi-factor-authentication"></a><span data-ttu-id="ba1ea-127">Enable users to register for Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ba1ea-127">Enable users to register for Multi-Factor Authentication</span></span>

<span data-ttu-id="ba1ea-128">Azure AD Identity Protection includes a default policy that can hep you to get your users registered for Multi-Factor Authentication and easily identify the current registration status.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-128">Azure AD Identity Protection includes a default policy that can hep you to get your users registered for Multi-Factor Authentication and easily identify the current registration status.</span></span> <span data-ttu-id="ba1ea-129">Enabling this policy does not start requiring users to perform Multi-Factor Authentication, but will ask them to pre-register.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-129">Enabling this policy does not start requiring users to perform Multi-Factor Authentication, but will ask them to pre-register.</span></span>

1. <span data-ttu-id="ba1ea-130">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba1ea-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="ba1ea-131">Click on **All services**, then browse to **Azure AD Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-131">Click on **All services**, then browse to **Azure AD Identity Protection**.</span></span>
1. <span data-ttu-id="ba1ea-132">Click on **MFA registration**.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-132">Click on **MFA registration**.</span></span>
1. <span data-ttu-id="ba1ea-133">Set Enforce Policy to **On**.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-133">Set Enforce Policy to **On**.</span></span>
   1. <span data-ttu-id="ba1ea-134">Setting this policy will require all of your users to register methods to prepare to use by Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-134">Setting this policy will require all of your users to register methods to prepare to use by Multi-Factor Authentication.</span></span>
1. <span data-ttu-id="ba1ea-135">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-135">Click **Save**.</span></span>

   ![Require users to register for MFA at sign-in using Azure AD Identity Protection](./media/tutorial-risk-based-sspr-mfa/risk-based-require-mfa-registration.png)

### <a name="enable-risk-based-password-changes"></a><span data-ttu-id="ba1ea-137">Enable risk-based password changes</span><span class="sxs-lookup"><span data-stu-id="ba1ea-137">Enable risk-based password changes</span></span>

<span data-ttu-id="ba1ea-138">Microsoft works with researchers, law enforcement, various security teams at Microsoft, and other trusted sources to find username and password pairs.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-138">Microsoft works with researchers, law enforcement, various security teams at Microsoft, and other trusted sources to find username and password pairs.</span></span> <span data-ttu-id="ba1ea-139">When one of these pairs matches an account in your environment, a risk-based password change can be triggered using the following policy.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-139">When one of these pairs matches an account in your environment, a risk-based password change can be triggered using the following policy.</span></span>

1. <span data-ttu-id="ba1ea-140">Click on User risk policy.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-140">Click on User risk policy.</span></span>
1. <span data-ttu-id="ba1ea-141">Under **Conditions**, select **User risk**, then choose **Medium and above**.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-141">Under **Conditions**, select **User risk**, then choose **Medium and above**.</span></span>
1. <span data-ttu-id="ba1ea-142">Click "Select" then "Done"</span><span class="sxs-lookup"><span data-stu-id="ba1ea-142">Click "Select" then "Done"</span></span>
1. <span data-ttu-id="ba1ea-143">Under **Access**, choose **Allow access**, and then select **Require password change**.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-143">Under **Access**, choose **Allow access**, and then select **Require password change**.</span></span>
1. <span data-ttu-id="ba1ea-144">Click "Select"</span><span class="sxs-lookup"><span data-stu-id="ba1ea-144">Click "Select"</span></span>
1. <span data-ttu-id="ba1ea-145">Set Enforce Policy to **On**.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-145">Set Enforce Policy to **On**.</span></span>
1. <span data-ttu-id="ba1ea-146">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="ba1ea-146">Click **Save**</span></span>

### <a name="enable-risk-based-multi-factor-authentication"></a><span data-ttu-id="ba1ea-147">Enable risk-based Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ba1ea-147">Enable risk-based Multi-Factor Authentication</span></span>

<span data-ttu-id="ba1ea-148">Most users have a normal behavior that can be tracked, when they fall outside of this norm it could be risky to allow them to just sign in.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-148">Most users have a normal behavior that can be tracked, when they fall outside of this norm it could be risky to allow them to just sign in.</span></span> <span data-ttu-id="ba1ea-149">You may want to block that user or maybe just ask them to perform a Multi-Factor Authentication to prove that they are really who they say they are.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-149">You may want to block that user or maybe just ask them to perform a Multi-Factor Authentication to prove that they are really who they say they are.</span></span> <span data-ttu-id="ba1ea-150">To enable a policy requiring MFA when a risky sign-in is detected, enable the following policy.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-150">To enable a policy requiring MFA when a risky sign-in is detected, enable the following policy.</span></span>

1. <span data-ttu-id="ba1ea-151">Click on Sign-in risk policy</span><span class="sxs-lookup"><span data-stu-id="ba1ea-151">Click on Sign-in risk policy</span></span>
1. <span data-ttu-id="ba1ea-152">Under **Conditions**, select **User risk**, then choose **Medium and above**.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-152">Under **Conditions**, select **User risk**, then choose **Medium and above**.</span></span>
1. <span data-ttu-id="ba1ea-153">Click "Select" then "Done"</span><span class="sxs-lookup"><span data-stu-id="ba1ea-153">Click "Select" then "Done"</span></span>
1. <span data-ttu-id="ba1ea-154">Under **Access**, choose **Allow access**, and then select **Require multi-factor authentication**.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-154">Under **Access**, choose **Allow access**, and then select **Require multi-factor authentication**.</span></span>
1. <span data-ttu-id="ba1ea-155">Click "Select"</span><span class="sxs-lookup"><span data-stu-id="ba1ea-155">Click "Select"</span></span>
1. <span data-ttu-id="ba1ea-156">Set Enforce Policy to **On**.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-156">Set Enforce Policy to **On**.</span></span>
1. <span data-ttu-id="ba1ea-157">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="ba1ea-157">Click **Save**</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="ba1ea-158">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ba1ea-158">Clean up resources</span></span>

<span data-ttu-id="ba1ea-159">If you have completed testing and no longer want to have the risk-based policies enabled, return to each policy you want to disable, and set **Enforce Policy** to **Off**.</span><span class="sxs-lookup"><span data-stu-id="ba1ea-159">If you have completed testing and no longer want to have the risk-based policies enabled, return to each policy you want to disable, and set **Enforce Policy** to **Off**.</span></span>