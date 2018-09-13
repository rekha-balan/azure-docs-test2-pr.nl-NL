---
title: Azure AD authentication methods
description: What authentication methods are available in Azure AD for MFA and SSPR
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry, michmcla
ms.openlocfilehash: 7776ca63dd5c02e470ead35e3dad73c051731fd1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857963"
---
# <a name="what-are-authentication-methods"></a><span data-ttu-id="73c3a-103">What are authentication methods?</span><span class="sxs-lookup"><span data-stu-id="73c3a-103">What are authentication methods?</span></span>

<span data-ttu-id="73c3a-104">Azure AD self-service password reset (SSPR) and Multi-Factor Authentication (MFA) may ask for additional information, known as authentication methods or security info, to confirm you are who you say you are when using the associated features.</span><span class="sxs-lookup"><span data-stu-id="73c3a-104">Azure AD self-service password reset (SSPR) and Multi-Factor Authentication (MFA) may ask for additional information, known as authentication methods or security info, to confirm you are who you say you are when using the associated features.</span></span>

<span data-ttu-id="73c3a-105">Administrators can define in policy which authentication methods are available to users of SSPR and MFA.</span><span class="sxs-lookup"><span data-stu-id="73c3a-105">Administrators can define in policy which authentication methods are available to users of SSPR and MFA.</span></span> <span data-ttu-id="73c3a-106">Some authentication methods may not be available to all features.</span><span class="sxs-lookup"><span data-stu-id="73c3a-106">Some authentication methods may not be available to all features.</span></span>

<span data-ttu-id="73c3a-107">Microsoft highly recommends Administrators enable users to select more than the minimum required number of authentication methods in case they do not have access to one.</span><span class="sxs-lookup"><span data-stu-id="73c3a-107">Microsoft highly recommends Administrators enable users to select more than the minimum required number of authentication methods in case they do not have access to one.</span></span>

|<span data-ttu-id="73c3a-108">Authentication Method</span><span class="sxs-lookup"><span data-stu-id="73c3a-108">Authentication Method</span></span>|<span data-ttu-id="73c3a-109">Usage</span><span class="sxs-lookup"><span data-stu-id="73c3a-109">Usage</span></span>|
| --- | --- |
| <span data-ttu-id="73c3a-110">Password</span><span class="sxs-lookup"><span data-stu-id="73c3a-110">Password</span></span> | <span data-ttu-id="73c3a-111">MFA and SSPR</span><span class="sxs-lookup"><span data-stu-id="73c3a-111">MFA and SSPR</span></span> |
| <span data-ttu-id="73c3a-112">Security questions</span><span class="sxs-lookup"><span data-stu-id="73c3a-112">Security questions</span></span> | <span data-ttu-id="73c3a-113">SSPR Only</span><span class="sxs-lookup"><span data-stu-id="73c3a-113">SSPR Only</span></span> |
| <span data-ttu-id="73c3a-114">Email address</span><span class="sxs-lookup"><span data-stu-id="73c3a-114">Email address</span></span> | <span data-ttu-id="73c3a-115">SSPR Only</span><span class="sxs-lookup"><span data-stu-id="73c3a-115">SSPR Only</span></span> |
| <span data-ttu-id="73c3a-116">Microsoft Authenticator app</span><span class="sxs-lookup"><span data-stu-id="73c3a-116">Microsoft Authenticator app</span></span> | <span data-ttu-id="73c3a-117">MFA and Public Preview for SSPR</span><span class="sxs-lookup"><span data-stu-id="73c3a-117">MFA and Public Preview for SSPR</span></span> |
| <span data-ttu-id="73c3a-118">SMS</span><span class="sxs-lookup"><span data-stu-id="73c3a-118">SMS</span></span> | <span data-ttu-id="73c3a-119">MFA and SSPR</span><span class="sxs-lookup"><span data-stu-id="73c3a-119">MFA and SSPR</span></span> |
| <span data-ttu-id="73c3a-120">Voice call</span><span class="sxs-lookup"><span data-stu-id="73c3a-120">Voice call</span></span> | <span data-ttu-id="73c3a-121">MFA and SSPR</span><span class="sxs-lookup"><span data-stu-id="73c3a-121">MFA and SSPR</span></span> |
| <span data-ttu-id="73c3a-122">App passwords</span><span class="sxs-lookup"><span data-stu-id="73c3a-122">App passwords</span></span> | <span data-ttu-id="73c3a-123">MFA only in certain cases</span><span class="sxs-lookup"><span data-stu-id="73c3a-123">MFA only in certain cases</span></span> |

![Authentication methods in use at the sign-in screen](media/concept-authentication-methods/overview-login.png)

|     |
| --- |
| <span data-ttu-id="73c3a-125">Mobile app notification and Mobile app code as methods for Azure AD self-service password reset are public preview features of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="73c3a-125">Mobile app notification and Mobile app code as methods for Azure AD self-service password reset are public preview features of Azure Active Directory.</span></span> <span data-ttu-id="73c3a-126">For more information about previews, see  [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span><span class="sxs-lookup"><span data-stu-id="73c3a-126">For more information about previews, see  [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span></span>|
|     |

## <a name="password"></a><span data-ttu-id="73c3a-127">Password</span><span class="sxs-lookup"><span data-stu-id="73c3a-127">Password</span></span>

<span data-ttu-id="73c3a-128">Your Azure AD password is considered an authentication method.</span><span class="sxs-lookup"><span data-stu-id="73c3a-128">Your Azure AD password is considered an authentication method.</span></span> <span data-ttu-id="73c3a-129">It is the one method that **cannot be disabled**.</span><span class="sxs-lookup"><span data-stu-id="73c3a-129">It is the one method that **cannot be disabled**.</span></span>

## <a name="security-questions"></a><span data-ttu-id="73c3a-130">Security questions</span><span class="sxs-lookup"><span data-stu-id="73c3a-130">Security questions</span></span>

<span data-ttu-id="73c3a-131">Security questions are available **only in Azure AD self-service password reset** to non-administrator accounts.</span><span class="sxs-lookup"><span data-stu-id="73c3a-131">Security questions are available **only in Azure AD self-service password reset** to non-administrator accounts.</span></span>

<span data-ttu-id="73c3a-132">If you use security questions, we recommend using them in conjunction with another method.</span><span class="sxs-lookup"><span data-stu-id="73c3a-132">If you use security questions, we recommend using them in conjunction with another method.</span></span> <span data-ttu-id="73c3a-133">Security questions can be less secure than other methods because some people might know the answers to another user's questions.</span><span class="sxs-lookup"><span data-stu-id="73c3a-133">Security questions can be less secure than other methods because some people might know the answers to another user's questions.</span></span>

> [!NOTE]
> <span data-ttu-id="73c3a-134">Security questions are stored privately and securely on a user object in the directory and can only be answered by users during registration.</span><span class="sxs-lookup"><span data-stu-id="73c3a-134">Security questions are stored privately and securely on a user object in the directory and can only be answered by users during registration.</span></span> <span data-ttu-id="73c3a-135">There is no way for an administrator to read or modify a user's questions or answers.</span><span class="sxs-lookup"><span data-stu-id="73c3a-135">There is no way for an administrator to read or modify a user's questions or answers.</span></span>
>

### <a name="predefined-questions"></a><span data-ttu-id="73c3a-136">Predefined questions</span><span class="sxs-lookup"><span data-stu-id="73c3a-136">Predefined questions</span></span>

* <span data-ttu-id="73c3a-137">In what city did you meet your first spouse/partner?</span><span class="sxs-lookup"><span data-stu-id="73c3a-137">In what city did you meet your first spouse/partner?</span></span>
* <span data-ttu-id="73c3a-138">In what city did your parents meet?</span><span class="sxs-lookup"><span data-stu-id="73c3a-138">In what city did your parents meet?</span></span>
* <span data-ttu-id="73c3a-139">In what city does your nearest sibling live?</span><span class="sxs-lookup"><span data-stu-id="73c3a-139">In what city does your nearest sibling live?</span></span>
* <span data-ttu-id="73c3a-140">In what city was your father born?</span><span class="sxs-lookup"><span data-stu-id="73c3a-140">In what city was your father born?</span></span>
* <span data-ttu-id="73c3a-141">In what city was your first job?</span><span class="sxs-lookup"><span data-stu-id="73c3a-141">In what city was your first job?</span></span>
* <span data-ttu-id="73c3a-142">In what city was your mother born?</span><span class="sxs-lookup"><span data-stu-id="73c3a-142">In what city was your mother born?</span></span>
* <span data-ttu-id="73c3a-143">What city were you in on New Year's 2000?</span><span class="sxs-lookup"><span data-stu-id="73c3a-143">What city were you in on New Year's 2000?</span></span>
* <span data-ttu-id="73c3a-144">What is the last name of your favorite teacher in high school?</span><span class="sxs-lookup"><span data-stu-id="73c3a-144">What is the last name of your favorite teacher in high school?</span></span>
* <span data-ttu-id="73c3a-145">What is the name of a college you applied to but didn't attend?</span><span class="sxs-lookup"><span data-stu-id="73c3a-145">What is the name of a college you applied to but didn't attend?</span></span>
* <span data-ttu-id="73c3a-146">What is the name of the place in which you held your first wedding reception?</span><span class="sxs-lookup"><span data-stu-id="73c3a-146">What is the name of the place in which you held your first wedding reception?</span></span>
* <span data-ttu-id="73c3a-147">What is your father's middle name?</span><span class="sxs-lookup"><span data-stu-id="73c3a-147">What is your father's middle name?</span></span>
* <span data-ttu-id="73c3a-148">What is your favorite food?</span><span class="sxs-lookup"><span data-stu-id="73c3a-148">What is your favorite food?</span></span>
* <span data-ttu-id="73c3a-149">What is your maternal grandmother's first and last name?</span><span class="sxs-lookup"><span data-stu-id="73c3a-149">What is your maternal grandmother's first and last name?</span></span>
* <span data-ttu-id="73c3a-150">What is your mother's middle name?</span><span class="sxs-lookup"><span data-stu-id="73c3a-150">What is your mother's middle name?</span></span>
* <span data-ttu-id="73c3a-151">What is your oldest sibling's birthday month and year?</span><span class="sxs-lookup"><span data-stu-id="73c3a-151">What is your oldest sibling's birthday month and year?</span></span> <span data-ttu-id="73c3a-152">(e.g. November 1985)</span><span class="sxs-lookup"><span data-stu-id="73c3a-152">(e.g. November 1985)</span></span>
* <span data-ttu-id="73c3a-153">What is your oldest sibling's middle name?</span><span class="sxs-lookup"><span data-stu-id="73c3a-153">What is your oldest sibling's middle name?</span></span>
* <span data-ttu-id="73c3a-154">What is your paternal grandfather's first and last name?</span><span class="sxs-lookup"><span data-stu-id="73c3a-154">What is your paternal grandfather's first and last name?</span></span>
* <span data-ttu-id="73c3a-155">What is your youngest sibling's middle name?</span><span class="sxs-lookup"><span data-stu-id="73c3a-155">What is your youngest sibling's middle name?</span></span>
* <span data-ttu-id="73c3a-156">What school did you attend for sixth grade?</span><span class="sxs-lookup"><span data-stu-id="73c3a-156">What school did you attend for sixth grade?</span></span>
* <span data-ttu-id="73c3a-157">What was the first and last name of your childhood best friend?</span><span class="sxs-lookup"><span data-stu-id="73c3a-157">What was the first and last name of your childhood best friend?</span></span>
* <span data-ttu-id="73c3a-158">What was the first and last name of your first significant other?</span><span class="sxs-lookup"><span data-stu-id="73c3a-158">What was the first and last name of your first significant other?</span></span>
* <span data-ttu-id="73c3a-159">What was the last name of your favorite grade school teacher?</span><span class="sxs-lookup"><span data-stu-id="73c3a-159">What was the last name of your favorite grade school teacher?</span></span>
* <span data-ttu-id="73c3a-160">What was the make and model of your first car or motorcycle?</span><span class="sxs-lookup"><span data-stu-id="73c3a-160">What was the make and model of your first car or motorcycle?</span></span>
* <span data-ttu-id="73c3a-161">What was the name of the first school you attended?</span><span class="sxs-lookup"><span data-stu-id="73c3a-161">What was the name of the first school you attended?</span></span>
* <span data-ttu-id="73c3a-162">What was the name of the hospital in which you were born?</span><span class="sxs-lookup"><span data-stu-id="73c3a-162">What was the name of the hospital in which you were born?</span></span>
* <span data-ttu-id="73c3a-163">What was the name of the street of your first childhood home?</span><span class="sxs-lookup"><span data-stu-id="73c3a-163">What was the name of the street of your first childhood home?</span></span>
* <span data-ttu-id="73c3a-164">What was the name of your childhood hero?</span><span class="sxs-lookup"><span data-stu-id="73c3a-164">What was the name of your childhood hero?</span></span>
* <span data-ttu-id="73c3a-165">What was the name of your favorite stuffed animal?</span><span class="sxs-lookup"><span data-stu-id="73c3a-165">What was the name of your favorite stuffed animal?</span></span>
* <span data-ttu-id="73c3a-166">What was the name of your first pet?</span><span class="sxs-lookup"><span data-stu-id="73c3a-166">What was the name of your first pet?</span></span>
* <span data-ttu-id="73c3a-167">What was your childhood nickname?</span><span class="sxs-lookup"><span data-stu-id="73c3a-167">What was your childhood nickname?</span></span>
* <span data-ttu-id="73c3a-168">What was your favorite sport in high school?</span><span class="sxs-lookup"><span data-stu-id="73c3a-168">What was your favorite sport in high school?</span></span>
* <span data-ttu-id="73c3a-169">What was your first job?</span><span class="sxs-lookup"><span data-stu-id="73c3a-169">What was your first job?</span></span>
* <span data-ttu-id="73c3a-170">What were the last four digits of your childhood telephone number?</span><span class="sxs-lookup"><span data-stu-id="73c3a-170">What were the last four digits of your childhood telephone number?</span></span>
* <span data-ttu-id="73c3a-171">When you were young, what did you want to be when you grew up?</span><span class="sxs-lookup"><span data-stu-id="73c3a-171">When you were young, what did you want to be when you grew up?</span></span>
* <span data-ttu-id="73c3a-172">Who is the most famous person you have ever met?</span><span class="sxs-lookup"><span data-stu-id="73c3a-172">Who is the most famous person you have ever met?</span></span>

<span data-ttu-id="73c3a-173">All of the predefined security questions are translated and localized into the full set of Office 365 languages based on the user's browser locale.</span><span class="sxs-lookup"><span data-stu-id="73c3a-173">All of the predefined security questions are translated and localized into the full set of Office 365 languages based on the user's browser locale.</span></span>

### <a name="custom-security-questions"></a><span data-ttu-id="73c3a-174">Custom security questions</span><span class="sxs-lookup"><span data-stu-id="73c3a-174">Custom security questions</span></span>

<span data-ttu-id="73c3a-175">Custom security questions are not localized.</span><span class="sxs-lookup"><span data-stu-id="73c3a-175">Custom security questions are not localized.</span></span> <span data-ttu-id="73c3a-176">All custom questions are displayed in the same language as they are entered in the administrative user interface, even if the user's browser locale is different.</span><span class="sxs-lookup"><span data-stu-id="73c3a-176">All custom questions are displayed in the same language as they are entered in the administrative user interface, even if the user's browser locale is different.</span></span> <span data-ttu-id="73c3a-177">If you need localized questions, you should use the predefined questions.</span><span class="sxs-lookup"><span data-stu-id="73c3a-177">If you need localized questions, you should use the predefined questions.</span></span>

<span data-ttu-id="73c3a-178">The maximum length of a custom security question is 200 characters.</span><span class="sxs-lookup"><span data-stu-id="73c3a-178">The maximum length of a custom security question is 200 characters.</span></span>

### <a name="security-question-requirements"></a><span data-ttu-id="73c3a-179">Security question requirements</span><span class="sxs-lookup"><span data-stu-id="73c3a-179">Security question requirements</span></span>

* <span data-ttu-id="73c3a-180">The minimum answer character limit is three characters.</span><span class="sxs-lookup"><span data-stu-id="73c3a-180">The minimum answer character limit is three characters.</span></span>
* <span data-ttu-id="73c3a-181">The maximum answer character limit is 40 characters.</span><span class="sxs-lookup"><span data-stu-id="73c3a-181">The maximum answer character limit is 40 characters.</span></span>
* <span data-ttu-id="73c3a-182">Users can't answer the same question more than one time.</span><span class="sxs-lookup"><span data-stu-id="73c3a-182">Users can't answer the same question more than one time.</span></span>
* <span data-ttu-id="73c3a-183">Users can't provide the same answer to more than one question.</span><span class="sxs-lookup"><span data-stu-id="73c3a-183">Users can't provide the same answer to more than one question.</span></span>
* <span data-ttu-id="73c3a-184">Any character set can be used to define the questions and the answers, including Unicode characters.</span><span class="sxs-lookup"><span data-stu-id="73c3a-184">Any character set can be used to define the questions and the answers, including Unicode characters.</span></span>
* <span data-ttu-id="73c3a-185">The number of questions defined must be greater than or equal to the number of questions that were required to register.</span><span class="sxs-lookup"><span data-stu-id="73c3a-185">The number of questions defined must be greater than or equal to the number of questions that were required to register.</span></span>

## <a name="email-address"></a><span data-ttu-id="73c3a-186">Email address</span><span class="sxs-lookup"><span data-stu-id="73c3a-186">Email address</span></span>

<span data-ttu-id="73c3a-187">Email address is available **only in Azure AD self-service password reset**.</span><span class="sxs-lookup"><span data-stu-id="73c3a-187">Email address is available **only in Azure AD self-service password reset**.</span></span>

<span data-ttu-id="73c3a-188">Microsoft recommends the use of an email account that would not require the user's Azure AD password to access.</span><span class="sxs-lookup"><span data-stu-id="73c3a-188">Microsoft recommends the use of an email account that would not require the user's Azure AD password to access.</span></span>

## <a name="microsoft-authenticator-app"></a><span data-ttu-id="73c3a-189">Microsoft Authenticator app</span><span class="sxs-lookup"><span data-stu-id="73c3a-189">Microsoft Authenticator app</span></span>

<span data-ttu-id="73c3a-190">The Microsoft Authenticator app provides an additional level of security to your Azure AD work or school account or your Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="73c3a-190">The Microsoft Authenticator app provides an additional level of security to your Azure AD work or school account or your Microsoft account.</span></span>

<span data-ttu-id="73c3a-191">The Microsoft Authenticator app is available for [Android](https://go.microsoft.com/fwlink/?linkid=866594), [iOS](https://go.microsoft.com/fwlink/?linkid=866594), and [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071).</span><span class="sxs-lookup"><span data-stu-id="73c3a-191">The Microsoft Authenticator app is available for [Android](https://go.microsoft.com/fwlink/?linkid=866594), [iOS](https://go.microsoft.com/fwlink/?linkid=866594), and [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071).</span></span>

> [!NOTE]
> <span data-ttu-id="73c3a-192">Users will not have the option to register their mobile app when registering for self-service password reset.</span><span class="sxs-lookup"><span data-stu-id="73c3a-192">Users will not have the option to register their mobile app when registering for self-service password reset.</span></span> <span data-ttu-id="73c3a-193">Instead, users can register their mobile app at [https://aka.ms/mfasetup](https://aka.ms/mfasetup) or in the security info registration preview at [https://aka.ms/setupsecurityinfo](https://aka.ms/setupsecurityinfo).</span><span class="sxs-lookup"><span data-stu-id="73c3a-193">Instead, users can register their mobile app at [https://aka.ms/mfasetup](https://aka.ms/mfasetup) or in the security info registration preview at [https://aka.ms/setupsecurityinfo](https://aka.ms/setupsecurityinfo).</span></span>
>

### <a name="notification-through-mobile-app"></a><span data-ttu-id="73c3a-194">Notification through mobile app</span><span class="sxs-lookup"><span data-stu-id="73c3a-194">Notification through mobile app</span></span>

<span data-ttu-id="73c3a-195">The Microsoft Authenticator app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span><span class="sxs-lookup"><span data-stu-id="73c3a-195">The Microsoft Authenticator app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span></span> <span data-ttu-id="73c3a-196">Users view the notification, and if it's legitimate, select Verify.</span><span class="sxs-lookup"><span data-stu-id="73c3a-196">Users view the notification, and if it's legitimate, select Verify.</span></span> <span data-ttu-id="73c3a-197">Otherwise, they can select Deny.</span><span class="sxs-lookup"><span data-stu-id="73c3a-197">Otherwise, they can select Deny.</span></span>

> [!WARNING]
> <span data-ttu-id="73c3a-198">For self-service password reset when only one method is required for reset, verification code is the only option available to users **to ensure the highest level of security**.</span><span class="sxs-lookup"><span data-stu-id="73c3a-198">For self-service password reset when only one method is required for reset, verification code is the only option available to users **to ensure the highest level of security**.</span></span>
>
> <span data-ttu-id="73c3a-199">When two methods are required users will be able to reset using **EITHER** notification **OR** verification code in addition to any other enabled methods.</span><span class="sxs-lookup"><span data-stu-id="73c3a-199">When two methods are required users will be able to reset using **EITHER** notification **OR** verification code in addition to any other enabled methods.</span></span>
>

<span data-ttu-id="73c3a-200">If you enable the use of both notification through mobile app and verification code from mobile app, users who register the Microsoft Authenticator app using a notification are able to use both notification and code to verify their identity.</span><span class="sxs-lookup"><span data-stu-id="73c3a-200">If you enable the use of both notification through mobile app and verification code from mobile app, users who register the Microsoft Authenticator app using a notification are able to use both notification and code to verify their identity.</span></span>

### <a name="verification-code-from-mobile-app"></a><span data-ttu-id="73c3a-201">Verification code from mobile app</span><span class="sxs-lookup"><span data-stu-id="73c3a-201">Verification code from mobile app</span></span>

<span data-ttu-id="73c3a-202">The Microsoft Authenticator app or other third-party apps can be used as a software token to generate an OATH verification code.</span><span class="sxs-lookup"><span data-stu-id="73c3a-202">The Microsoft Authenticator app or other third-party apps can be used as a software token to generate an OATH verification code.</span></span> <span data-ttu-id="73c3a-203">After entering your username and password, you enter the code provided by the app into the sign-in screen.</span><span class="sxs-lookup"><span data-stu-id="73c3a-203">After entering your username and password, you enter the code provided by the app into the sign-in screen.</span></span> <span data-ttu-id="73c3a-204">The verification code provides a second form of authentication.</span><span class="sxs-lookup"><span data-stu-id="73c3a-204">The verification code provides a second form of authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="73c3a-205">For self-service password reset when only one method is required for reset verification code is the only option available to users **to ensure the highest level of security**.</span><span class="sxs-lookup"><span data-stu-id="73c3a-205">For self-service password reset when only one method is required for reset verification code is the only option available to users **to ensure the highest level of security**.</span></span>
>

## <a name="mobile-phone"></a><span data-ttu-id="73c3a-206">Mobile phone</span><span class="sxs-lookup"><span data-stu-id="73c3a-206">Mobile phone</span></span>

<span data-ttu-id="73c3a-207">Two options are available to users with mobile phones.</span><span class="sxs-lookup"><span data-stu-id="73c3a-207">Two options are available to users with mobile phones.</span></span>

<span data-ttu-id="73c3a-208">If users don't want their mobile phone number to be visible in the directory, but they still want to use it for password reset, administrators should not populate it in the directory.</span><span class="sxs-lookup"><span data-stu-id="73c3a-208">If users don't want their mobile phone number to be visible in the directory, but they still want to use it for password reset, administrators should not populate it in the directory.</span></span> <span data-ttu-id="73c3a-209">Users should populate their **Authentication Phone** attribute via the [password reset registration portal](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="73c3a-209">Users should populate their **Authentication Phone** attribute via the [password reset registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="73c3a-210">Administrators can see this information in the user's profile, but it's not published elsewhere.</span><span class="sxs-lookup"><span data-stu-id="73c3a-210">Administrators can see this information in the user's profile, but it's not published elsewhere.</span></span>

<span data-ttu-id="73c3a-211">To work properly, phone numbers must be in the format *+CountryCode PhoneNumber*, for example, +1 4255551234.</span><span class="sxs-lookup"><span data-stu-id="73c3a-211">To work properly, phone numbers must be in the format *+CountryCode PhoneNumber*, for example, +1 4255551234.</span></span>

> [!NOTE]
> <span data-ttu-id="73c3a-212">There needs to be a space between the country code and the phone number.</span><span class="sxs-lookup"><span data-stu-id="73c3a-212">There needs to be a space between the country code and the phone number.</span></span>
>
> <span data-ttu-id="73c3a-213">Password reset does not support phone extensions.</span><span class="sxs-lookup"><span data-stu-id="73c3a-213">Password reset does not support phone extensions.</span></span> <span data-ttu-id="73c3a-214">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span><span class="sxs-lookup"><span data-stu-id="73c3a-214">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

### <a name="text-message"></a><span data-ttu-id="73c3a-215">Text message</span><span class="sxs-lookup"><span data-stu-id="73c3a-215">Text message</span></span>

<span data-ttu-id="73c3a-216">An SMS is sent to the mobile phone number containing a verification code.</span><span class="sxs-lookup"><span data-stu-id="73c3a-216">An SMS is sent to the mobile phone number containing a verification code.</span></span> <span data-ttu-id="73c3a-217">Enter the verification code provided in the sign-in interface to continue.</span><span class="sxs-lookup"><span data-stu-id="73c3a-217">Enter the verification code provided in the sign-in interface to continue.</span></span>

### <a name="phone-call"></a><span data-ttu-id="73c3a-218">Phone call</span><span class="sxs-lookup"><span data-stu-id="73c3a-218">Phone call</span></span>

<span data-ttu-id="73c3a-219">An automated voice call is made to the phone number you provide.</span><span class="sxs-lookup"><span data-stu-id="73c3a-219">An automated voice call is made to the phone number you provide.</span></span> <span data-ttu-id="73c3a-220">Answer the call and press # in the phone keypad to authenticate</span><span class="sxs-lookup"><span data-stu-id="73c3a-220">Answer the call and press # in the phone keypad to authenticate</span></span>

## <a name="office-phone"></a><span data-ttu-id="73c3a-221">Office phone</span><span class="sxs-lookup"><span data-stu-id="73c3a-221">Office phone</span></span>

<span data-ttu-id="73c3a-222">An automated voice call is made to the phone number you provide.</span><span class="sxs-lookup"><span data-stu-id="73c3a-222">An automated voice call is made to the phone number you provide.</span></span> <span data-ttu-id="73c3a-223">Answer the call and presses # in the phone keypad to authenticate.</span><span class="sxs-lookup"><span data-stu-id="73c3a-223">Answer the call and presses # in the phone keypad to authenticate.</span></span>

<span data-ttu-id="73c3a-224">To work properly, phone numbers must be in the format *+CountryCode PhoneNumber*, for example, +1 4255551234.</span><span class="sxs-lookup"><span data-stu-id="73c3a-224">To work properly, phone numbers must be in the format *+CountryCode PhoneNumber*, for example, +1 4255551234.</span></span>

<span data-ttu-id="73c3a-225">The office phone attribute is managed by your administrator.</span><span class="sxs-lookup"><span data-stu-id="73c3a-225">The office phone attribute is managed by your administrator.</span></span>

> [!NOTE]
> <span data-ttu-id="73c3a-226">There needs to be a space between the country code and the phone number.</span><span class="sxs-lookup"><span data-stu-id="73c3a-226">There needs to be a space between the country code and the phone number.</span></span>
>
> <span data-ttu-id="73c3a-227">Password reset does not support phone extensions.</span><span class="sxs-lookup"><span data-stu-id="73c3a-227">Password reset does not support phone extensions.</span></span> <span data-ttu-id="73c3a-228">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span><span class="sxs-lookup"><span data-stu-id="73c3a-228">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

## <a name="app-passwords"></a><span data-ttu-id="73c3a-229">App Passwords</span><span class="sxs-lookup"><span data-stu-id="73c3a-229">App Passwords</span></span>

<span data-ttu-id="73c3a-230">Certain non-browser apps do not support multi-factor authentication, if a user has been enabled for multi-factor authentication and attempt to use non-browser apps, they are unable to authenticate.</span><span class="sxs-lookup"><span data-stu-id="73c3a-230">Certain non-browser apps do not support multi-factor authentication, if a user has been enabled for multi-factor authentication and attempt to use non-browser apps, they are unable to authenticate.</span></span> <span data-ttu-id="73c3a-231">An app password allows users to continue to authenticate</span><span class="sxs-lookup"><span data-stu-id="73c3a-231">An app password allows users to continue to authenticate</span></span>

<span data-ttu-id="73c3a-232">If you enforce Multi-Factor Authentication through Conditional Access policies and not through per-user MFA, you cannot create app passwords.</span><span class="sxs-lookup"><span data-stu-id="73c3a-232">If you enforce Multi-Factor Authentication through Conditional Access policies and not through per-user MFA, you cannot create app passwords.</span></span> <span data-ttu-id="73c3a-233">Applications that use Conditional Access policies to control access do not need app passwords.</span><span class="sxs-lookup"><span data-stu-id="73c3a-233">Applications that use Conditional Access policies to control access do not need app passwords.</span></span>

<span data-ttu-id="73c3a-234">If your organization is federated for SSO with Azure AD and you are going to be using Azure MFA, then be aware of the following details:</span><span class="sxs-lookup"><span data-stu-id="73c3a-234">If your organization is federated for SSO with Azure AD and you are going to be using Azure MFA, then be aware of the following details:</span></span>

* <span data-ttu-id="73c3a-235">The app password is verified by Azure AD and therefore bypasses federation.</span><span class="sxs-lookup"><span data-stu-id="73c3a-235">The app password is verified by Azure AD and therefore bypasses federation.</span></span> <span data-ttu-id="73c3a-236">Federation is only used when setting up app passwords.</span><span class="sxs-lookup"><span data-stu-id="73c3a-236">Federation is only used when setting up app passwords.</span></span> <span data-ttu-id="73c3a-237">For federated (SSO) users, passwords are stored in the organizational ID.</span><span class="sxs-lookup"><span data-stu-id="73c3a-237">For federated (SSO) users, passwords are stored in the organizational ID.</span></span> <span data-ttu-id="73c3a-238">If the user leaves the company, that info has to flow to organizational ID using DirSync.</span><span class="sxs-lookup"><span data-stu-id="73c3a-238">If the user leaves the company, that info has to flow to organizational ID using DirSync.</span></span> <span data-ttu-id="73c3a-239">Account disable/deletion may take up to three hours to sync, which delays disable/deletion of app passwords in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73c3a-239">Account disable/deletion may take up to three hours to sync, which delays disable/deletion of app passwords in Azure AD.</span></span>
* <span data-ttu-id="73c3a-240">On-premises Client Access Control settings are not honored by App Password.</span><span class="sxs-lookup"><span data-stu-id="73c3a-240">On-premises Client Access Control settings are not honored by App Password.</span></span>
* <span data-ttu-id="73c3a-241">No on-premises authentication logging/auditing capability is available for app passwords.</span><span class="sxs-lookup"><span data-stu-id="73c3a-241">No on-premises authentication logging/auditing capability is available for app passwords.</span></span>
* <span data-ttu-id="73c3a-242">Certain advanced architectural designs may require using a combination of organizational username and passwords and app passwords when using two-step verification with clients, depending on where they authenticate.</span><span class="sxs-lookup"><span data-stu-id="73c3a-242">Certain advanced architectural designs may require using a combination of organizational username and passwords and app passwords when using two-step verification with clients, depending on where they authenticate.</span></span> <span data-ttu-id="73c3a-243">For clients that authenticate against an on-premises infrastructure, you would use an organizational username and password.</span><span class="sxs-lookup"><span data-stu-id="73c3a-243">For clients that authenticate against an on-premises infrastructure, you would use an organizational username and password.</span></span> <span data-ttu-id="73c3a-244">For clients that authenticate against Azure AD, you would use the app password.</span><span class="sxs-lookup"><span data-stu-id="73c3a-244">For clients that authenticate against Azure AD, you would use the app password.</span></span>
* <span data-ttu-id="73c3a-245">By default, users cannot create app passwords.</span><span class="sxs-lookup"><span data-stu-id="73c3a-245">By default, users cannot create app passwords.</span></span> <span data-ttu-id="73c3a-246">If you need to allow users to create app passwords, select the **Allow users to create app passwords to sign into non-browser applications option** under service settings.</span><span class="sxs-lookup"><span data-stu-id="73c3a-246">If you need to allow users to create app passwords, select the **Allow users to create app passwords to sign into non-browser applications option** under service settings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73c3a-247">Next steps</span><span class="sxs-lookup"><span data-stu-id="73c3a-247">Next steps</span></span>

[<span data-ttu-id="73c3a-248">Enable self service password reset for your organization</span><span class="sxs-lookup"><span data-stu-id="73c3a-248">Enable self service password reset for your organization</span></span>](quickstart-sspr.md)

[<span data-ttu-id="73c3a-249">Enable Azure Multi-Factor Authentication for your organization</span><span class="sxs-lookup"><span data-stu-id="73c3a-249">Enable Azure Multi-Factor Authentication for your organization</span></span>](howto-mfa-getstarted.md)

[<span data-ttu-id="73c3a-250">Enable converged registration for Azure Multi-Factor Authentication and Azure AD self-service password reset</span><span class="sxs-lookup"><span data-stu-id="73c3a-250">Enable converged registration for Azure Multi-Factor Authentication and Azure AD self-service password reset</span></span>](concept-registration-mfa-sspr-converged.md)

[<span data-ttu-id="73c3a-251">End-user authentication method configuration documentation</span><span class="sxs-lookup"><span data-stu-id="73c3a-251">End-user authentication method configuration documentation</span></span>](https://aka.ms/securityinfoguide)
