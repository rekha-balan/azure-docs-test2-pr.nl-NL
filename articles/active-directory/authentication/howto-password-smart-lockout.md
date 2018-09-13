---
title: Preventing brute-force attacks using Azure AD smart lockout
description: Azure Active Directory smart lockout helps protect your organization from brute-force attacks trying to guess passwords
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/18/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: rogoya
ms.openlocfilehash: b0fded9f5543d151091955c0b0d645bf9db16b7d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865062"
---
# <a name="azure-active-directory-smart-lockout"></a><span data-ttu-id="7e66d-103">Azure Active Directory smart lockout</span><span class="sxs-lookup"><span data-stu-id="7e66d-103">Azure Active Directory smart lockout</span></span>

<span data-ttu-id="7e66d-104">Smart lockout uses cloud intelligence to lock out bad actors who are trying to guess your users’ passwords or use brute-force methods to get in.</span><span class="sxs-lookup"><span data-stu-id="7e66d-104">Smart lockout uses cloud intelligence to lock out bad actors who are trying to guess your users’ passwords or use brute-force methods to get in.</span></span> <span data-ttu-id="7e66d-105">That intelligence can recognize sign-ins coming from valid users and treat them differently than ones of attackers and other unknown sources.</span><span class="sxs-lookup"><span data-stu-id="7e66d-105">That intelligence can recognize sign-ins coming from valid users and treat them differently than ones of attackers and other unknown sources.</span></span> <span data-ttu-id="7e66d-106">Smart lockout locks out the attackers, while letting your users continue to access their accounts and be productive.</span><span class="sxs-lookup"><span data-stu-id="7e66d-106">Smart lockout locks out the attackers, while letting your users continue to access their accounts and be productive.</span></span>

<span data-ttu-id="7e66d-107">By default, smart lockout locks the account from sign-in attempts for one minute after ten failed attempts.</span><span class="sxs-lookup"><span data-stu-id="7e66d-107">By default, smart lockout locks the account from sign-in attempts for one minute after ten failed attempts.</span></span> <span data-ttu-id="7e66d-108">The account locks again after each subsequent failed sign-in attempt, for one minute at first and longer in subsequent attempts.</span><span class="sxs-lookup"><span data-stu-id="7e66d-108">The account locks again after each subsequent failed sign-in attempt, for one minute at first and longer in subsequent attempts.</span></span>

<span data-ttu-id="7e66d-109">Smart lockout is always on for all Azure AD customers with these default settings that offer the right mix of security and usability.</span><span class="sxs-lookup"><span data-stu-id="7e66d-109">Smart lockout is always on for all Azure AD customers with these default settings that offer the right mix of security and usability.</span></span> <span data-ttu-id="7e66d-110">Customization of the smart lockout settings, with values specific to your organization, requires Azure AD Basic or higher licenses for your users.</span><span class="sxs-lookup"><span data-stu-id="7e66d-110">Customization of the smart lockout settings, with values specific to your organization, requires Azure AD Basic or higher licenses for your users.</span></span>

<span data-ttu-id="7e66d-111">Smart lockout can be integrated with hybrid deployments, using password hash sync or pass-through authentication to protect on-premises Active Directory accounts from being locked out by attackers.</span><span class="sxs-lookup"><span data-stu-id="7e66d-111">Smart lockout can be integrated with hybrid deployments, using password hash sync or pass-through authentication to protect on-premises Active Directory accounts from being locked out by attackers.</span></span> <span data-ttu-id="7e66d-112">By setting smart lockout policies in Azure AD appropriately, attacks can be filtered out before they reach on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7e66d-112">By setting smart lockout policies in Azure AD appropriately, attacks can be filtered out before they reach on-premises Active Directory.</span></span>

<span data-ttu-id="7e66d-113">When using [pass-through authentication](../connect/active-directory-aadconnect-pass-through-authentication.md), you need to make sure that:</span><span class="sxs-lookup"><span data-stu-id="7e66d-113">When using [pass-through authentication](../connect/active-directory-aadconnect-pass-through-authentication.md), you need to make sure that:</span></span>

   * <span data-ttu-id="7e66d-114">The Azure AD lockout threshold is **less** than the Active Directory account lockout threshold.</span><span class="sxs-lookup"><span data-stu-id="7e66d-114">The Azure AD lockout threshold is **less** than the Active Directory account lockout threshold.</span></span> <span data-ttu-id="7e66d-115">Set the values so that the Active Directory account lockout threshold is at least two or three times longer than the Azure AD lockout threshold.</span><span class="sxs-lookup"><span data-stu-id="7e66d-115">Set the values so that the Active Directory account lockout threshold is at least two or three times longer than the Azure AD lockout threshold.</span></span> 
   * <span data-ttu-id="7e66d-116">The Azure AD lockout duration **in seconds** is **longer** than the Active Directory reset account lockout counter after duration **minutes**.</span><span class="sxs-lookup"><span data-stu-id="7e66d-116">The Azure AD lockout duration **in seconds** is **longer** than the Active Directory reset account lockout counter after duration **minutes**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e66d-117">Currently an administrator can't unlock the users' cloud accounts if they have been locked out by the Smart Lockout capability.</span><span class="sxs-lookup"><span data-stu-id="7e66d-117">Currently an administrator can't unlock the users' cloud accounts if they have been locked out by the Smart Lockout capability.</span></span> <span data-ttu-id="7e66d-118">The administrator must wait for the lockout duration to expire.</span><span class="sxs-lookup"><span data-stu-id="7e66d-118">The administrator must wait for the lockout duration to expire.</span></span>

## <a name="verify-on-premises-account-lockout-policy"></a><span data-ttu-id="7e66d-119">Verify on-premises account lockout policy</span><span class="sxs-lookup"><span data-stu-id="7e66d-119">Verify on-premises account lockout policy</span></span>

<span data-ttu-id="7e66d-120">Use the following instructions to verify your on-premises Active Directory account lockout policy:</span><span class="sxs-lookup"><span data-stu-id="7e66d-120">Use the following instructions to verify your on-premises Active Directory account lockout policy:</span></span>

1. <span data-ttu-id="7e66d-121">Open the Group Policy Management tool.</span><span class="sxs-lookup"><span data-stu-id="7e66d-121">Open the Group Policy Management tool.</span></span>
2. <span data-ttu-id="7e66d-122">Edit the group policy that includes your organization's account lockout policy, for example, the **Default Domain Policy**.</span><span class="sxs-lookup"><span data-stu-id="7e66d-122">Edit the group policy that includes your organization's account lockout policy, for example, the **Default Domain Policy**.</span></span>
3. <span data-ttu-id="7e66d-123">Browse to **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Account Policies** > **Account Lockout Policy**.</span><span class="sxs-lookup"><span data-stu-id="7e66d-123">Browse to **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Account Policies** > **Account Lockout Policy**.</span></span>
4. <span data-ttu-id="7e66d-124">Verify your **Account lockout threshold** and **Reset account lockout counter after** values.</span><span class="sxs-lookup"><span data-stu-id="7e66d-124">Verify your **Account lockout threshold** and **Reset account lockout counter after** values.</span></span>

![Modify the on-premises Active Directory account lockout policy using a Group Policy Object](./media/howto-password-smart-lockout/active-directory-on-premises-account-lockout-policy.png)

## <a name="manage-azure-ad-smart-lockout-values"></a><span data-ttu-id="7e66d-126">Manage Azure AD smart lockout values</span><span class="sxs-lookup"><span data-stu-id="7e66d-126">Manage Azure AD smart lockout values</span></span>

<span data-ttu-id="7e66d-127">Based on your organizational requirements, smart lockout values may need to be customized.</span><span class="sxs-lookup"><span data-stu-id="7e66d-127">Based on your organizational requirements, smart lockout values may need to be customized.</span></span> <span data-ttu-id="7e66d-128">Customization of the smart lockout settings, with values specific to your organization, requires Azure AD Basic or higher licenses for your users.</span><span class="sxs-lookup"><span data-stu-id="7e66d-128">Customization of the smart lockout settings, with values specific to your organization, requires Azure AD Basic or higher licenses for your users.</span></span>

<span data-ttu-id="7e66d-129">To check or modify the smart lockout values for your organization, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e66d-129">To check or modify the smart lockout values for your organization, use the following steps:</span></span>

1. <span data-ttu-id="7e66d-130">Sign in to the [Azure portal](https://portal.azure.com), and click on **Azure Active Directory**, then  **Authentication Methods**.</span><span class="sxs-lookup"><span data-stu-id="7e66d-130">Sign in to the [Azure portal](https://portal.azure.com), and click on **Azure Active Directory**, then  **Authentication Methods**.</span></span>
1. <span data-ttu-id="7e66d-131">Set the **Lockout threshold**, based on how many failed sign-ins are allowed on an account before its first lockout.</span><span class="sxs-lookup"><span data-stu-id="7e66d-131">Set the **Lockout threshold**, based on how many failed sign-ins are allowed on an account before its first lockout.</span></span> <span data-ttu-id="7e66d-132">The default is 10.</span><span class="sxs-lookup"><span data-stu-id="7e66d-132">The default is 10.</span></span>
1. <span data-ttu-id="7e66d-133">Set the **Lockout duration in seconds**, to the length in seconds of each lockout.</span><span class="sxs-lookup"><span data-stu-id="7e66d-133">Set the **Lockout duration in seconds**, to the length in seconds of each lockout.</span></span> <span data-ttu-id="7e66d-134">The default is 60 seconds (one minute).</span><span class="sxs-lookup"><span data-stu-id="7e66d-134">The default is 60 seconds (one minute).</span></span>

> [!NOTE]
> <span data-ttu-id="7e66d-135">If the first sign-in after a lockout also fails, the account locks out again.</span><span class="sxs-lookup"><span data-stu-id="7e66d-135">If the first sign-in after a lockout also fails, the account locks out again.</span></span> <span data-ttu-id="7e66d-136">If an account locks repeatedly, the lockout duration increases.</span><span class="sxs-lookup"><span data-stu-id="7e66d-136">If an account locks repeatedly, the lockout duration increases.</span></span>

![Customize the Azure AD smart lockout policy in the Azure portal](./media/howto-password-smart-lockout/azure-active-directory-custom-smart-lockout-policy.png)
## <a name="next-steps"></a><span data-ttu-id="7e66d-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="7e66d-138">Next steps</span></span>

[<span data-ttu-id="7e66d-139">Find out how to ban bad passwords in your organization using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e66d-139">Find out how to ban bad passwords in your organization using Azure AD.</span></span>](howto-password-ban-bad.md)

[<span data-ttu-id="7e66d-140">Configure self-service password reset to allow users to unlock their own accounts.</span><span class="sxs-lookup"><span data-stu-id="7e66d-140">Configure self-service password reset to allow users to unlock their own accounts.</span></span>](quickstart-sspr.md)