---
title: Configure Azure AD Privileged Identity Management | Microsoft Docs
description: A topic that explains what Azure AD Privileged Identity Management is and how to use PIM to improve your cloud security.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1283570e448ad1ae578518c6d582b5dd8bd5b1f5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556563"
---
# <a name="what-is-azure-ad-privileged-identity-management"></a><span data-ttu-id="5f6be-103">What is Azure AD Privileged Identity Management?</span><span class="sxs-lookup"><span data-stu-id="5f6be-103">What is Azure AD Privileged Identity Management?</span></span>
<span data-ttu-id="5f6be-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span><span class="sxs-lookup"><span data-stu-id="5f6be-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="5f6be-105">This includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="5f6be-105">This includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

> [!NOTE]
> <span data-ttu-id="5f6be-106">Privileged Identity Management is available only with the Premium P2 edition of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5f6be-106">Privileged Identity Management is available only with the Premium P2 edition of Azure Active Directory.</span></span> <span data-ttu-id="5f6be-107">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="5f6be-107">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

<span data-ttu-id="5f6be-108">Organizations want to minimize the number of people who have access to secure information or resources, because that reduces the chance of a malicious user getting that access.</span><span class="sxs-lookup"><span data-stu-id="5f6be-108">Organizations want to minimize the number of people who have access to secure information or resources, because that reduces the chance of a malicious user getting that access.</span></span> <span data-ttu-id="5f6be-109">However, users still need to carry out privileged operations in Azure, Office 365, or SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5f6be-109">However, users still need to carry out privileged operations in Azure, Office 365, or SaaS apps.</span></span> <span data-ttu-id="5f6be-110">Organizations give users privileged access in Azure AD without monitoring what those users are doing with their admin privileges.</span><span class="sxs-lookup"><span data-stu-id="5f6be-110">Organizations give users privileged access in Azure AD without monitoring what those users are doing with their admin privileges.</span></span> <span data-ttu-id="5f6be-111">Azure AD Privileged Identity Management helps to resolve this risk.</span><span class="sxs-lookup"><span data-stu-id="5f6be-111">Azure AD Privileged Identity Management helps to resolve this risk.</span></span>  

<span data-ttu-id="5f6be-112">Azure AD Privileged Identity Management helps you:</span><span class="sxs-lookup"><span data-stu-id="5f6be-112">Azure AD Privileged Identity Management helps you:</span></span>  

* <span data-ttu-id="5f6be-113">See which users are Azure AD administrators</span><span class="sxs-lookup"><span data-stu-id="5f6be-113">See which users are Azure AD administrators</span></span>
* <span data-ttu-id="5f6be-114">Enable on-demand, "just in time" administrative access to Microsoft Online Services like Office 365 and Intune</span><span class="sxs-lookup"><span data-stu-id="5f6be-114">Enable on-demand, "just in time" administrative access to Microsoft Online Services like Office 365 and Intune</span></span>
* <span data-ttu-id="5f6be-115">Get reports about administrator access history and changes in administrator assignments</span><span class="sxs-lookup"><span data-stu-id="5f6be-115">Get reports about administrator access history and changes in administrator assignments</span></span>
* <span data-ttu-id="5f6be-116">Get alerts about access to a privileged role</span><span class="sxs-lookup"><span data-stu-id="5f6be-116">Get alerts about access to a privileged role</span></span>

<span data-ttu-id="5f6be-117">Azure AD Privileged Identity Management can manage the built-in Azure AD organizational roles, including (but not limited to):</span><span class="sxs-lookup"><span data-stu-id="5f6be-117">Azure AD Privileged Identity Management can manage the built-in Azure AD organizational roles, including (but not limited to):</span></span>  

* <span data-ttu-id="5f6be-118">Global Administrator</span><span class="sxs-lookup"><span data-stu-id="5f6be-118">Global Administrator</span></span>
* <span data-ttu-id="5f6be-119">Billing Administrator</span><span class="sxs-lookup"><span data-stu-id="5f6be-119">Billing Administrator</span></span>
* <span data-ttu-id="5f6be-120">Service Administrator</span><span class="sxs-lookup"><span data-stu-id="5f6be-120">Service Administrator</span></span>  
* <span data-ttu-id="5f6be-121">User Administrator</span><span class="sxs-lookup"><span data-stu-id="5f6be-121">User Administrator</span></span>
* <span data-ttu-id="5f6be-122">Password Administrator</span><span class="sxs-lookup"><span data-stu-id="5f6be-122">Password Administrator</span></span>

## <a name="just-in-time-administrator-access"></a><span data-ttu-id="5f6be-123">Just in time administrator access</span><span class="sxs-lookup"><span data-stu-id="5f6be-123">Just in time administrator access</span></span>
<span data-ttu-id="5f6be-124">Historically, you could assign a user to an admin role through the Azure classic portal or Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f6be-124">Historically, you could assign a user to an admin role through the Azure classic portal or Windows PowerShell.</span></span> <span data-ttu-id="5f6be-125">As a result, that user becomes a **permanent admin**, always active in the assigned role.</span><span class="sxs-lookup"><span data-stu-id="5f6be-125">As a result, that user becomes a **permanent admin**, always active in the assigned role.</span></span> <span data-ttu-id="5f6be-126">Azure AD Privileged Identity Management introduces the concept of an **eligible admin**. Eligible admins should be users that need privileged access now and then, but not every day.</span><span class="sxs-lookup"><span data-stu-id="5f6be-126">Azure AD Privileged Identity Management introduces the concept of an **eligible admin**. Eligible admins should be users that need privileged access now and then, but not every day.</span></span> <span data-ttu-id="5f6be-127">The role is inactive until the user needs access, then they complete an activation process and become an active admin for a predetermined amount of time.</span><span class="sxs-lookup"><span data-stu-id="5f6be-127">The role is inactive until the user needs access, then they complete an activation process and become an active admin for a predetermined amount of time.</span></span>

## <a name="enable-privileged-identity-management-for-your-directory"></a><span data-ttu-id="5f6be-128">Enable Privileged Identity Management for your directory</span><span class="sxs-lookup"><span data-stu-id="5f6be-128">Enable Privileged Identity Management for your directory</span></span>
<span data-ttu-id="5f6be-129">You can start using Azure AD Privileged Identity Management in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5f6be-129">You can start using Azure AD Privileged Identity Management in the [Azure portal](https://portal.azure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="5f6be-130">You must be a global administrator with an organizational account (for example, @yourdomain.com), not a Microsoft account (for example, @outlook.com), to enable Azure AD Privileged Identity Management for a directory.</span><span class="sxs-lookup"><span data-stu-id="5f6be-130">You must be a global administrator with an organizational account (for example, @yourdomain.com), not a Microsoft account (for example, @outlook.com), to enable Azure AD Privileged Identity Management for a directory.</span></span>

1. <span data-ttu-id="5f6be-131">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span><span class="sxs-lookup"><span data-stu-id="5f6be-131">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="5f6be-132">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5f6be-132">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="5f6be-133">Select the directory where you will use Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="5f6be-133">Select the directory where you will use Azure AD Privileged Identity Management.</span></span>
3. <span data-ttu-id="5f6be-134">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="5f6be-134">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="5f6be-135">Check **Pin to dashboard** and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5f6be-135">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="5f6be-136">The Privileged Identity Management application opens.</span><span class="sxs-lookup"><span data-stu-id="5f6be-136">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="5f6be-137">If you're the first person to use Azure AD Privileged Identity Management in your directory, then the [security wizard](active-directory-privileged-identity-management-security-wizard.md) walks you through the initial assignment experience.</span><span class="sxs-lookup"><span data-stu-id="5f6be-137">If you're the first person to use Azure AD Privileged Identity Management in your directory, then the [security wizard](active-directory-privileged-identity-management-security-wizard.md) walks you through the initial assignment experience.</span></span> <span data-ttu-id="5f6be-138">After that you automatically become the first **Security administrator** and **Privileged role administrator** of the directory.</span><span class="sxs-lookup"><span data-stu-id="5f6be-138">After that you automatically become the first **Security administrator** and **Privileged role administrator** of the directory.</span></span>

<span data-ttu-id="5f6be-139">Only a privileged role administrator can manage access for other administrators.</span><span class="sxs-lookup"><span data-stu-id="5f6be-139">Only a privileged role administrator can manage access for other administrators.</span></span> <span data-ttu-id="5f6be-140">You can [give other users the ability to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="5f6be-140">You can [give other users the ability to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="privileged-identity-management-dashboard"></a><span data-ttu-id="5f6be-141">Privileged Identity Management dashboard</span><span class="sxs-lookup"><span data-stu-id="5f6be-141">Privileged Identity Management dashboard</span></span>
<span data-ttu-id="5f6be-142">Azure AD Privileged Identity Manager provides a dashboard that gives you important information such as:</span><span class="sxs-lookup"><span data-stu-id="5f6be-142">Azure AD Privileged Identity Manager provides a dashboard that gives you important information such as:</span></span>

* <span data-ttu-id="5f6be-143">Alerts that point out opportunities to improve security</span><span class="sxs-lookup"><span data-stu-id="5f6be-143">Alerts that point out opportunities to improve security</span></span>
* <span data-ttu-id="5f6be-144">The number of users who are assigned to each privileged role</span><span class="sxs-lookup"><span data-stu-id="5f6be-144">The number of users who are assigned to each privileged role</span></span>  
* <span data-ttu-id="5f6be-145">The number of eligible and permanent admins</span><span class="sxs-lookup"><span data-stu-id="5f6be-145">The number of eligible and permanent admins</span></span>
* <span data-ttu-id="5f6be-146">Ongoing access reviews</span><span class="sxs-lookup"><span data-stu-id="5f6be-146">Ongoing access reviews</span></span>

![PIM dashboard - screenshot][2]

## <a name="privileged-role-management"></a><span data-ttu-id="5f6be-148">Privileged role management</span><span class="sxs-lookup"><span data-stu-id="5f6be-148">Privileged role management</span></span>
<span data-ttu-id="5f6be-149">With Azure AD Privileged Identity Management, you can manage the administrators by adding or removing permanent or eligible administrators to each role.</span><span class="sxs-lookup"><span data-stu-id="5f6be-149">With Azure AD Privileged Identity Management, you can manage the administrators by adding or removing permanent or eligible administrators to each role.</span></span>

![PIM add/remove administrators - screenshot][3]

## <a name="configure-the-role-activation-settings"></a><span data-ttu-id="5f6be-151">Configure the role activation settings</span><span class="sxs-lookup"><span data-stu-id="5f6be-151">Configure the role activation settings</span></span>
<span data-ttu-id="5f6be-152">Using the [role settings](active-directory-privileged-identity-management-how-to-change-default-settings.md) you can configure the eligible role activation properties including:</span><span class="sxs-lookup"><span data-stu-id="5f6be-152">Using the [role settings](active-directory-privileged-identity-management-how-to-change-default-settings.md) you can configure the eligible role activation properties including:</span></span>

* <span data-ttu-id="5f6be-153">The duration of the role activation period</span><span class="sxs-lookup"><span data-stu-id="5f6be-153">The duration of the role activation period</span></span>
* <span data-ttu-id="5f6be-154">The role activation notification</span><span class="sxs-lookup"><span data-stu-id="5f6be-154">The role activation notification</span></span>
* <span data-ttu-id="5f6be-155">The information a user needs to provide during the role activation process</span><span class="sxs-lookup"><span data-stu-id="5f6be-155">The information a user needs to provide during the role activation process</span></span>  

![PIM settings - administrator activation - screenshot][4]

<span data-ttu-id="5f6be-157">Note that in the image, the buttons for **Multi-Factor Authentication** are disabled.</span><span class="sxs-lookup"><span data-stu-id="5f6be-157">Note that in the image, the buttons for **Multi-Factor Authentication** are disabled.</span></span> <span data-ttu-id="5f6be-158">For certain, highly privileged roles, we require MFA for heightened protection.</span><span class="sxs-lookup"><span data-stu-id="5f6be-158">For certain, highly privileged roles, we require MFA for heightened protection.</span></span>

## <a name="role-activation"></a><span data-ttu-id="5f6be-159">Role activation</span><span class="sxs-lookup"><span data-stu-id="5f6be-159">Role activation</span></span>
<span data-ttu-id="5f6be-160">To [activate a role](active-directory-privileged-identity-management-how-to-activate-role.md), an eligible admin requests a time-bound "activation" for the role.</span><span class="sxs-lookup"><span data-stu-id="5f6be-160">To [activate a role](active-directory-privileged-identity-management-how-to-activate-role.md), an eligible admin requests a time-bound "activation" for the role.</span></span> <span data-ttu-id="5f6be-161">The activation can be requested using the **Activate my role** option in Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="5f6be-161">The activation can be requested using the **Activate my role** option in Azure AD Privileged Identity Management.</span></span>

<span data-ttu-id="5f6be-162">An admin who wants to activate a role needs to initialize Azure AD Privileged Identity Management in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5f6be-162">An admin who wants to activate a role needs to initialize Azure AD Privileged Identity Management in the Azure portal.</span></span>

<span data-ttu-id="5f6be-163">Role activation is customizable.</span><span class="sxs-lookup"><span data-stu-id="5f6be-163">Role activation is customizable.</span></span> <span data-ttu-id="5f6be-164">In the PIM settings, you can determine the length of the activation and what information the admin needs to provide to activate the role.</span><span class="sxs-lookup"><span data-stu-id="5f6be-164">In the PIM settings, you can determine the length of the activation and what information the admin needs to provide to activate the role.</span></span>

![PIM administrator request role activation - screenshot][5]

## <a name="review-role-activity"></a><span data-ttu-id="5f6be-166">Review role activity</span><span class="sxs-lookup"><span data-stu-id="5f6be-166">Review role activity</span></span>
<span data-ttu-id="5f6be-167">There are two ways to track how your employees and admins are using privileged roles.</span><span class="sxs-lookup"><span data-stu-id="5f6be-167">There are two ways to track how your employees and admins are using privileged roles.</span></span> <span data-ttu-id="5f6be-168">The first option is using [audit history](active-directory-privileged-identity-management-how-to-use-audit-log.md).</span><span class="sxs-lookup"><span data-stu-id="5f6be-168">The first option is using [audit history](active-directory-privileged-identity-management-how-to-use-audit-log.md).</span></span> <span data-ttu-id="5f6be-169">The audit history logs track changes in privileged role assignments and role activation history.</span><span class="sxs-lookup"><span data-stu-id="5f6be-169">The audit history logs track changes in privileged role assignments and role activation history.</span></span>

![PIM activation history - screenshot][6]

<span data-ttu-id="5f6be-171">The second option is to set up regular [access reviews](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="5f6be-171">The second option is to set up regular [access reviews](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="5f6be-172">These access reviews can be performed by and assigned reviewer (like a team manager) or the employees can review themselves.</span><span class="sxs-lookup"><span data-stu-id="5f6be-172">These access reviews can be performed by and assigned reviewer (like a team manager) or the employees can review themselves.</span></span> <span data-ttu-id="5f6be-173">This is the best way to monitor who still requires access, and who no longer does.</span><span class="sxs-lookup"><span data-stu-id="5f6be-173">This is the best way to monitor who still requires access, and who no longer does.</span></span>

## <a name="azure-ad-pim-at-subscription-expiration"></a><span data-ttu-id="5f6be-174">Azure AD PIM at subscription expiration</span><span class="sxs-lookup"><span data-stu-id="5f6be-174">Azure AD PIM at subscription expiration</span></span>
<span data-ttu-id="5f6be-175">Prior to reaching general availability Azure AD PIM was in preview and there were no license checks for a tenant to preview Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="5f6be-175">Prior to reaching general availability Azure AD PIM was in preview and there were no license checks for a tenant to preview Azure AD PIM.</span></span>  <span data-ttu-id="5f6be-176">Now that Azure AD PIM has reached general availability, a trial or paid subscription must be present in the tenant to continue using PIM after December 2016.</span><span class="sxs-lookup"><span data-stu-id="5f6be-176">Now that Azure AD PIM has reached general availability, a trial or paid subscription must be present in the tenant to continue using PIM after December 2016.</span></span>  <span data-ttu-id="5f6be-177">If your organization does not purchase Azure AD Premium P2 or your subscription expires, then Azure AD PIM will no longer be available in your tenant.</span><span class="sxs-lookup"><span data-stu-id="5f6be-177">If your organization does not purchase Azure AD Premium P2 or your subscription expires, then Azure AD PIM will no longer be available in your tenant.</span></span>  <span data-ttu-id="5f6be-178">You can read more in the [Azure AD PIM subscription requirements](./privileged-identity-management/subscription-requirements.md)</span><span class="sxs-lookup"><span data-stu-id="5f6be-178">You can read more in the [Azure AD PIM subscription requirements](./privileged-identity-management/subscription-requirements.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f6be-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="5f6be-179">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-configure/PIM_RoleActivationSettings.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png






