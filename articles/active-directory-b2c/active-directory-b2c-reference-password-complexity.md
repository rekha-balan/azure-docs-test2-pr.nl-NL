---
title: Password complexity in Azure Active Directory B2C | Microsoft Docs
description: How to configure complexity requirements for passwords supplied by consumers in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/16/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 4b027f6cd57dfa48ba2e230371ffcad97b1f8ec4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870237"
---
# <a name="azure-ad-b2c-configure-complexity-requirements-for-passwords"></a><span data-ttu-id="6a659-103">Azure AD B2C: Configure complexity requirements for passwords</span><span class="sxs-lookup"><span data-stu-id="6a659-103">Azure AD B2C: Configure complexity requirements for passwords</span></span>

> [!NOTE]
> <span data-ttu-id="6a659-104">**This feature is in public preview.**</span><span class="sxs-lookup"><span data-stu-id="6a659-104">**This feature is in public preview.**</span></span>

<span data-ttu-id="6a659-105">Azure Active Directory B2C (Azure AD B2C) supports changing the complexity requirements for passwords supplied by an end user when creating an account.</span><span class="sxs-lookup"><span data-stu-id="6a659-105">Azure Active Directory B2C (Azure AD B2C) supports changing the complexity requirements for passwords supplied by an end user when creating an account.</span></span>  <span data-ttu-id="6a659-106">By default, Azure AD B2C uses `Strong` passwords.</span><span class="sxs-lookup"><span data-stu-id="6a659-106">By default, Azure AD B2C uses `Strong` passwords.</span></span>  <span data-ttu-id="6a659-107">Azure AD B2C also supports configuration options to control the complexity of passwords that customers can use.</span><span class="sxs-lookup"><span data-stu-id="6a659-107">Azure AD B2C also supports configuration options to control the complexity of passwords that customers can use.</span></span>

## <a name="when-password-rules-are-enforced"></a><span data-ttu-id="6a659-108">When password rules are enforced</span><span class="sxs-lookup"><span data-stu-id="6a659-108">When password rules are enforced</span></span>

<span data-ttu-id="6a659-109">During sign-up or password reset, an end user must supply a password that meets the complexity rules.</span><span class="sxs-lookup"><span data-stu-id="6a659-109">During sign-up or password reset, an end user must supply a password that meets the complexity rules.</span></span>  <span data-ttu-id="6a659-110">Password complexity rules are enforced per policy.</span><span class="sxs-lookup"><span data-stu-id="6a659-110">Password complexity rules are enforced per policy.</span></span>  <span data-ttu-id="6a659-111">It is possible to have one policy require a four-digit pin during sign-up while another policy requires a eight character string during sign-up.</span><span class="sxs-lookup"><span data-stu-id="6a659-111">It is possible to have one policy require a four-digit pin during sign-up while another policy requires a eight character string during sign-up.</span></span>  <span data-ttu-id="6a659-112">For example, you may use a policy with different password complexity for adults than for children.</span><span class="sxs-lookup"><span data-stu-id="6a659-112">For example, you may use a policy with different password complexity for adults than for children.</span></span>

<span data-ttu-id="6a659-113">Password complexity is never enforced during sign-in.</span><span class="sxs-lookup"><span data-stu-id="6a659-113">Password complexity is never enforced during sign-in.</span></span>  <span data-ttu-id="6a659-114">Users are never prompted during sign-in to change their password because it doesn't meet the current complexity requirement.</span><span class="sxs-lookup"><span data-stu-id="6a659-114">Users are never prompted during sign-in to change their password because it doesn't meet the current complexity requirement.</span></span>

<span data-ttu-id="6a659-115">Here are the types of policies where password complexity can be configured:</span><span class="sxs-lookup"><span data-stu-id="6a659-115">Here are the types of policies where password complexity can be configured:</span></span>

* <span data-ttu-id="6a659-116">Sign-up or Sign-in Policy</span><span class="sxs-lookup"><span data-stu-id="6a659-116">Sign-up or Sign-in Policy</span></span>
* <span data-ttu-id="6a659-117">Password Reset Policy</span><span class="sxs-lookup"><span data-stu-id="6a659-117">Password Reset Policy</span></span>
* <span data-ttu-id="6a659-118">Custom Policy ([Configure password complexity in custom policy](active-directory-b2c-reference-password-complexity-custom.md))</span><span class="sxs-lookup"><span data-stu-id="6a659-118">Custom Policy ([Configure password complexity in custom policy](active-directory-b2c-reference-password-complexity-custom.md))</span></span>

## <a name="how-to-configure-password-complexity"></a><span data-ttu-id="6a659-119">How to configure password complexity</span><span class="sxs-lookup"><span data-stu-id="6a659-119">How to configure password complexity</span></span>

1. <span data-ttu-id="6a659-120">Follow these steps to [navigate to Azure AD B2C settings](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="6a659-120">Follow these steps to [navigate to Azure AD B2C settings](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
1. <span data-ttu-id="6a659-121">Open **Sign-up or sign-in polices**.</span><span class="sxs-lookup"><span data-stu-id="6a659-121">Open **Sign-up or sign-in polices**.</span></span>
1. <span data-ttu-id="6a659-122">Select a policy, and click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="6a659-122">Select a policy, and click **Edit**.</span></span>
1. <span data-ttu-id="6a659-123">Open **Password complexity**.</span><span class="sxs-lookup"><span data-stu-id="6a659-123">Open **Password complexity**.</span></span>
1. <span data-ttu-id="6a659-124">Change the password complexity for this policy to **Simple**, **Strong**, or **Custom**.</span><span class="sxs-lookup"><span data-stu-id="6a659-124">Change the password complexity for this policy to **Simple**, **Strong**, or **Custom**.</span></span>

### <a name="comparison-chart"></a><span data-ttu-id="6a659-125">Comparison Chart</span><span class="sxs-lookup"><span data-stu-id="6a659-125">Comparison Chart</span></span>

| <span data-ttu-id="6a659-126">Complexity</span><span class="sxs-lookup"><span data-stu-id="6a659-126">Complexity</span></span> | <span data-ttu-id="6a659-127">Description</span><span class="sxs-lookup"><span data-stu-id="6a659-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6a659-128">Simple</span><span class="sxs-lookup"><span data-stu-id="6a659-128">Simple</span></span> | <span data-ttu-id="6a659-129">A password that is at least 8 to 64 characters.</span><span class="sxs-lookup"><span data-stu-id="6a659-129">A password that is at least 8 to 64 characters.</span></span> |
| <span data-ttu-id="6a659-130">Strong</span><span class="sxs-lookup"><span data-stu-id="6a659-130">Strong</span></span> | <span data-ttu-id="6a659-131">A password that is at least 8 to 64 characters.</span><span class="sxs-lookup"><span data-stu-id="6a659-131">A password that is at least 8 to 64 characters.</span></span> <span data-ttu-id="6a659-132">It requires 3 out of 4 of lowercase, uppercase, numbers, or symbols.</span><span class="sxs-lookup"><span data-stu-id="6a659-132">It requires 3 out of 4 of lowercase, uppercase, numbers, or symbols.</span></span> |
| <span data-ttu-id="6a659-133">Custom</span><span class="sxs-lookup"><span data-stu-id="6a659-133">Custom</span></span> | <span data-ttu-id="6a659-134">This option provides the most control over password complexity rules.</span><span class="sxs-lookup"><span data-stu-id="6a659-134">This option provides the most control over password complexity rules.</span></span>  <span data-ttu-id="6a659-135">It allows configuring a custom length.</span><span class="sxs-lookup"><span data-stu-id="6a659-135">It allows configuring a custom length.</span></span>  <span data-ttu-id="6a659-136">It also allows accepting number-only passwords (pins).</span><span class="sxs-lookup"><span data-stu-id="6a659-136">It also allows accepting number-only passwords (pins).</span></span> |

## <a name="options-available-under-custom"></a><span data-ttu-id="6a659-137">Options available under custom</span><span class="sxs-lookup"><span data-stu-id="6a659-137">Options available under custom</span></span>

### <a name="character-set"></a><span data-ttu-id="6a659-138">Character Set</span><span class="sxs-lookup"><span data-stu-id="6a659-138">Character Set</span></span>

<span data-ttu-id="6a659-139">Allows you to accept digits only (pins) or the full character set.</span><span class="sxs-lookup"><span data-stu-id="6a659-139">Allows you to accept digits only (pins) or the full character set.</span></span>

* <span data-ttu-id="6a659-140">**Numbers only** allows digits only (0-9) while entering a password.</span><span class="sxs-lookup"><span data-stu-id="6a659-140">**Numbers only** allows digits only (0-9) while entering a password.</span></span>
* <span data-ttu-id="6a659-141">**All** allows any letter, number, or symbol.</span><span class="sxs-lookup"><span data-stu-id="6a659-141">**All** allows any letter, number, or symbol.</span></span>

### <a name="length"></a><span data-ttu-id="6a659-142">Length</span><span class="sxs-lookup"><span data-stu-id="6a659-142">Length</span></span>

<span data-ttu-id="6a659-143">Allows you to control the length requirements of the password.</span><span class="sxs-lookup"><span data-stu-id="6a659-143">Allows you to control the length requirements of the password.</span></span>

* <span data-ttu-id="6a659-144">**Minimum Length** must be at least 4.</span><span class="sxs-lookup"><span data-stu-id="6a659-144">**Minimum Length** must be at least 4.</span></span>
* <span data-ttu-id="6a659-145">**Maximum Length** must be greater or equal to minimum length and at most can be 64 characters.</span><span class="sxs-lookup"><span data-stu-id="6a659-145">**Maximum Length** must be greater or equal to minimum length and at most can be 64 characters.</span></span>

### <a name="character-classes"></a><span data-ttu-id="6a659-146">Character classes</span><span class="sxs-lookup"><span data-stu-id="6a659-146">Character classes</span></span>

<span data-ttu-id="6a659-147">Allows you to control the different character types used in the password.</span><span class="sxs-lookup"><span data-stu-id="6a659-147">Allows you to control the different character types used in the password.</span></span>

* <span data-ttu-id="6a659-148">**2 of 4: Lowercase character, Uppercase character, Number (0-9), Symbol** ensures the password contains at least two character types.</span><span class="sxs-lookup"><span data-stu-id="6a659-148">**2 of 4: Lowercase character, Uppercase character, Number (0-9), Symbol** ensures the password contains at least two character types.</span></span> <span data-ttu-id="6a659-149">For example, a number and a lowercase character.</span><span class="sxs-lookup"><span data-stu-id="6a659-149">For example, a number and a lowercase character.</span></span>
* <span data-ttu-id="6a659-150">**3 of 4: Lowercase character, Uppercase character, Number (0-9), Symbol** ensures the password contains at least two character types.</span><span class="sxs-lookup"><span data-stu-id="6a659-150">**3 of 4: Lowercase character, Uppercase character, Number (0-9), Symbol** ensures the password contains at least two character types.</span></span> <span data-ttu-id="6a659-151">For example, a number, a lowercase character and an uppercase character.</span><span class="sxs-lookup"><span data-stu-id="6a659-151">For example, a number, a lowercase character and an uppercase character.</span></span>
* <span data-ttu-id="6a659-152">**4 of 4: Lowercase character, Uppercase character, Number (0-9), Symbol** ensures the password contains all for character types.</span><span class="sxs-lookup"><span data-stu-id="6a659-152">**4 of 4: Lowercase character, Uppercase character, Number (0-9), Symbol** ensures the password contains all for character types.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6a659-153">Requiring **4 of 4** can result in end-user frustration.</span><span class="sxs-lookup"><span data-stu-id="6a659-153">Requiring **4 of 4** can result in end-user frustration.</span></span> <span data-ttu-id="6a659-154">Some studies have shown that this requirement does not improve password entropy.</span><span class="sxs-lookup"><span data-stu-id="6a659-154">Some studies have shown that this requirement does not improve password entropy.</span></span> <span data-ttu-id="6a659-155">See [NIST Password Guidelines](https://pages.nist.gov/800-63-3/sp800-63b.html#appA)</span><span class="sxs-lookup"><span data-stu-id="6a659-155">See [NIST Password Guidelines](https://pages.nist.gov/800-63-3/sp800-63b.html#appA)</span></span>
