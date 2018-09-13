---
title: 'FAQ: Azure AD password management | Microsoft Docs'
description: Frequently asked questions (FAQ) about password management in Azure AD, including password reset, registration, reports, and writeback to on-premises Active Directory .
services: active-directory
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: femila
editor: curtand
ms.assetid: 3a157d27-a410-4371-bcbf-8312941ae9d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: joflore
ms.openlocfilehash: 38ecd941fc8f8b210d1776817281b9b67a98c216
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550697"
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="eb84e-103">Password management frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="eb84e-103">Password management frequently asked questions</span></span>
> [!IMPORTANT]
> <span data-ttu-id="eb84e-104">**Are you here because you're having problems signing in?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="eb84e-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span><span class="sxs-lookup"><span data-stu-id="eb84e-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span></span>
>
>

<span data-ttu-id="eb84e-106">The following are some frequently asked questions for all things related to password management.</span><span class="sxs-lookup"><span data-stu-id="eb84e-106">The following are some frequently asked questions for all things related to password management.</span></span>

<span data-ttu-id="eb84e-107">If you find yourself with a question that you don't know the answer to, or are looking for help with a particular problem you are facing, you can read on below to see if we've covered it already.</span><span class="sxs-lookup"><span data-stu-id="eb84e-107">If you find yourself with a question that you don't know the answer to, or are looking for help with a particular problem you are facing, you can read on below to see if we've covered it already.</span></span>  <span data-ttu-id="eb84e-108">If we haven't already, don't worry!</span><span class="sxs-lookup"><span data-stu-id="eb84e-108">If we haven't already, don't worry!</span></span> <span data-ttu-id="eb84e-109">Feel free to ask any question you have that's not covered here on the [Azure AD Forums](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD) and we'll get back to you as soon as we can.</span><span class="sxs-lookup"><span data-stu-id="eb84e-109">Feel free to ask any question you have that's not covered here on the [Azure AD Forums](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD) and we'll get back to you as soon as we can.</span></span>

<span data-ttu-id="eb84e-110">This FAQ is split into the following sections:</span><span class="sxs-lookup"><span data-stu-id="eb84e-110">This FAQ is split into the following sections:</span></span>

* [<span data-ttu-id="eb84e-111">**Questions about Password Reset Registration**</span><span class="sxs-lookup"><span data-stu-id="eb84e-111">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="eb84e-112">**Questions about Password Reset**</span><span class="sxs-lookup"><span data-stu-id="eb84e-112">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="eb84e-113">**Questions about Password Change**</span><span class="sxs-lookup"><span data-stu-id="eb84e-113">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="eb84e-114">**Questions about password management Reports**</span><span class="sxs-lookup"><span data-stu-id="eb84e-114">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="eb84e-115">**Questions about password writeback**</span><span class="sxs-lookup"><span data-stu-id="eb84e-115">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="eb84e-116">Password reset registration</span><span class="sxs-lookup"><span data-stu-id="eb84e-116">Password reset registration</span></span>
* <span data-ttu-id="eb84e-117">**Q:  Can my users register their own password reset data?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-117">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="eb84e-118">**A:** Yes, as long as password reset is enabled and they are licensed, they can go to the Password Reset Registration portal at http://aka.ms/ssprsetup to register their authentication information to be used with password reset.</span><span class="sxs-lookup"><span data-stu-id="eb84e-118">**A:** Yes, as long as password reset is enabled and they are licensed, they can go to the Password Reset Registration portal at http://aka.ms/ssprsetup to register their authentication information to be used with password reset.</span></span> <span data-ttu-id="eb84e-119">Users can also register by going to the access panel at http://myapps.microsoft.com, clicking the profile tab, and clicking the Register for Password Reset option.</span><span class="sxs-lookup"><span data-stu-id="eb84e-119">Users can also register by going to the access panel at http://myapps.microsoft.com, clicking the profile tab, and clicking the Register for Password Reset option.</span></span> <span data-ttu-id="eb84e-120">Learn more about how to get your users configured for password reset by reading How to get users configured for password reset.</span><span class="sxs-lookup"><span data-stu-id="eb84e-120">Learn more about how to get your users configured for password reset by reading How to get users configured for password reset.</span></span>
  >
  >
* <span data-ttu-id="eb84e-121">**Q:  Can I define password reset data on behalf of my users?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-121">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="eb84e-122">**A:** Yes, you can do so with DirSync or PowerShell, or through the [Azure Management Portal](https://manage.windowsazure.com) or Office Admin portal.</span><span class="sxs-lookup"><span data-stu-id="eb84e-122">**A:** Yes, you can do so with DirSync or PowerShell, or through the [Azure Management Portal](https://manage.windowsazure.com) or Office Admin portal.</span></span> <span data-ttu-id="eb84e-123">Learn more about this feature on the blog post Improved Privacy for Azure AD MFA and Password Reset Phone Numbers and by reading Learn how data is used by password reset.</span><span class="sxs-lookup"><span data-stu-id="eb84e-123">Learn more about this feature on the blog post Improved Privacy for Azure AD MFA and Password Reset Phone Numbers and by reading Learn how data is used by password reset.</span></span>
  >
  >
* <span data-ttu-id="eb84e-124">**Q:  Can I synchronize data for security questions from on premises?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-124">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="eb84e-125">**A:** No, this is not possible today, but we are considering it.</span><span class="sxs-lookup"><span data-stu-id="eb84e-125">**A:** No, this is not possible today, but we are considering it.</span></span>
  >
  >
* <span data-ttu-id="eb84e-126">**Q:  Can my users register data in such a way that other users cannot see this data?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-126">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="eb84e-127">**A:** Yes, when users register data using the Password Reset Registration Portal it gets saved into private authentication fields that are only visible by Global Administrators and the user himself.</span><span class="sxs-lookup"><span data-stu-id="eb84e-127">**A:** Yes, when users register data using the Password Reset Registration Portal it gets saved into private authentication fields that are only visible by Global Administrators and the user himself.</span></span> <span data-ttu-id="eb84e-128">Learn more about this feature on the blog post Improved Privacy for Azure AD MFA and Password Reset Phone Numbers and by reading Learn how data is used by password reset.</span><span class="sxs-lookup"><span data-stu-id="eb84e-128">Learn more about this feature on the blog post Improved Privacy for Azure AD MFA and Password Reset Phone Numbers and by reading Learn how data is used by password reset.</span></span>
  >
  >
* <span data-ttu-id="eb84e-129">**Q:  Do my users have to be registered before they can use password reset?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-129">**Q:  Do my users have to be registered before they can use password reset?**</span></span>

  > <span data-ttu-id="eb84e-130">**A:** No, if you define enough authentication information on their behalf, users will not have to register.</span><span class="sxs-lookup"><span data-stu-id="eb84e-130">**A:** No, if you define enough authentication information on their behalf, users will not have to register.</span></span> <span data-ttu-id="eb84e-131">Password reset will work just fine as long as you have properly formatted data stored in the appropriate fields in the directory.</span><span class="sxs-lookup"><span data-stu-id="eb84e-131">Password reset will work just fine as long as you have properly formatted data stored in the appropriate fields in the directory.</span></span> <span data-ttu-id="eb84e-132">Learn more about by reading Learn how data is used by password reset.</span><span class="sxs-lookup"><span data-stu-id="eb84e-132">Learn more about by reading Learn how data is used by password reset.</span></span>
  >
  >
* <span data-ttu-id="eb84e-133">**Q:  Can I synchronize or set the Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-133">**Q:  Can I synchronize or set the Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="eb84e-134">**A:** Not currently, but we are considering enabling this capability.</span><span class="sxs-lookup"><span data-stu-id="eb84e-134">**A:** Not currently, but we are considering enabling this capability.</span></span>
  >
  >
* <span data-ttu-id="eb84e-135">**Q:  How does the registration portal know which options to show my users?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-135">**Q:  How does the registration portal know which options to show my users?**</span></span>

  > <span data-ttu-id="eb84e-136">**A:** The password reset registration portal only shows the options that you have enabled for your users under the User Password Reset Policy section of your directory’s Configure tab. This means that if you do not enable, say, security questions, then users will not be able to register for that option.</span><span class="sxs-lookup"><span data-stu-id="eb84e-136">**A:** The password reset registration portal only shows the options that you have enabled for your users under the User Password Reset Policy section of your directory’s Configure tab. This means that if you do not enable, say, security questions, then users will not be able to register for that option.</span></span>
  >
  >
* <span data-ttu-id="eb84e-137">**Q:  When is a user considered registered?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-137">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="eb84e-138">**A:** A user is considered registered when he or she has at least N pieces of authentication info defined, where N is the Number of Authentication Methods Required that you have set in the [Azure Management Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="eb84e-138">**A:** A user is considered registered when he or she has at least N pieces of authentication info defined, where N is the Number of Authentication Methods Required that you have set in the [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="eb84e-139">To learn more, see Customizing User Password Reset Policy.</span><span class="sxs-lookup"><span data-stu-id="eb84e-139">To learn more, see Customizing User Password Reset Policy.</span></span>
  >
  >

## <a name="password-reset"></a><span data-ttu-id="eb84e-140">Password reset</span><span class="sxs-lookup"><span data-stu-id="eb84e-140">Password reset</span></span>
* <span data-ttu-id="eb84e-141">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-141">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="eb84e-142">**A:** Email, SMS messages, and phone calls should arrive in under 1 minute, with the normal case being 5-20 seconds.</span><span class="sxs-lookup"><span data-stu-id="eb84e-142">**A:** Email, SMS messages, and phone calls should arrive in under 1 minute, with the normal case being 5-20 seconds.</span></span> <span data-ttu-id="eb84e-143">If you do not receive the notification in this timeframe, check your junk folder, that the number / email being contacted is the one you expect, and that the authentication data in the directory is correctly formatted.</span><span class="sxs-lookup"><span data-stu-id="eb84e-143">If you do not receive the notification in this timeframe, check your junk folder, that the number / email being contacted is the one you expect, and that the authentication data in the directory is correctly formatted.</span></span> <span data-ttu-id="eb84e-144">To learn more about formatting phone numbers and email addresses for use with password reset see Learn how data is used by password reset.</span><span class="sxs-lookup"><span data-stu-id="eb84e-144">To learn more about formatting phone numbers and email addresses for use with password reset see Learn how data is used by password reset.</span></span>
  >
  >
* <span data-ttu-id="eb84e-145">**Q:  What languages are supported by password reset?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-145">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="eb84e-146">**A:** The password reset UI, SMS messages, and voice calls are localized in the same 40 languages that are supported in Office 365.</span><span class="sxs-lookup"><span data-stu-id="eb84e-146">**A:** The password reset UI, SMS messages, and voice calls are localized in the same 40 languages that are supported in Office 365.</span></span> <span data-ttu-id="eb84e-147">Those are: Arabic, Bulgarian, Chinese Simplified, Chinese Traditional, Croatian, Czech, Danish, Dutch, English, Estonian, Finnish, French, German, Greek, Hebrew, Hindi, Hungarian, Indonesian, Italian, Japanese, Kazakh, Korean, Latvian, Lithuanian, Malay (Malaysia), Norwegian (Bokmål), Polish, Portuguese (Brazil), Portuguese (Portugal), Romanian, Russian, Serbian (Latin), Slovak, Slovenian, Spanish, Swedish, Thai, Turkish, Ukrainian, and Vietnamese.</span><span class="sxs-lookup"><span data-stu-id="eb84e-147">Those are: Arabic, Bulgarian, Chinese Simplified, Chinese Traditional, Croatian, Czech, Danish, Dutch, English, Estonian, Finnish, French, German, Greek, Hebrew, Hindi, Hungarian, Indonesian, Italian, Japanese, Kazakh, Korean, Latvian, Lithuanian, Malay (Malaysia), Norwegian (Bokmål), Polish, Portuguese (Brazil), Portuguese (Portugal), Romanian, Russian, Serbian (Latin), Slovak, Slovenian, Spanish, Swedish, Thai, Turkish, Ukrainian, and Vietnamese.</span></span>
  >
  >
* <span data-ttu-id="eb84e-148">**Q:  What parts of the password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-148">**Q:  What parts of the password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="eb84e-149">**A:** The password reset portal will show your organizational logo and will also allow you to configure the Contact your administrator link to point to a custom email or URL.</span><span class="sxs-lookup"><span data-stu-id="eb84e-149">**A:** The password reset portal will show your organizational logo and will also allow you to configure the Contact your administrator link to point to a custom email or URL.</span></span> <span data-ttu-id="eb84e-150">Any email that gets sent by password reset will include your organization’s logo, colors (in this case red), name in the body of the email, and customized from name.</span><span class="sxs-lookup"><span data-stu-id="eb84e-150">Any email that gets sent by password reset will include your organization’s logo, colors (in this case red), name in the body of the email, and customized from name.</span></span> <span data-ttu-id="eb84e-151">See an example with all the branded elements below.</span><span class="sxs-lookup"><span data-stu-id="eb84e-151">See an example with all the branded elements below.</span></span> <span data-ttu-id="eb84e-152">To learn more, read Customizing Password Reset Look and Feel.</span><span class="sxs-lookup"><span data-stu-id="eb84e-152">To learn more, read Customizing Password Reset Look and Feel.</span></span>
  >
  >

  ![][001]
* <span data-ttu-id="eb84e-153">**Q:  How can I educate my users about where to go to reset their passwords?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-153">**Q:  How can I educate my users about where to go to reset their passwords?**</span></span>

  > <span data-ttu-id="eb84e-154">**A:** You can send your users to https://passwordreset.microsoftonline.com directly, or you can instruct them to click on the Can’t access your account link found on any School or Work ID sign in screen.</span><span class="sxs-lookup"><span data-stu-id="eb84e-154">**A:** You can send your users to https://passwordreset.microsoftonline.com directly, or you can instruct them to click on the Can’t access your account link found on any School or Work ID sign in screen.</span></span> <span data-ttu-id="eb84e-155">You can feel free to publish these links (or create URL redirects to them) in any place that is easily accessible to your users.</span><span class="sxs-lookup"><span data-stu-id="eb84e-155">You can feel free to publish these links (or create URL redirects to them) in any place that is easily accessible to your users.</span></span>
  >
  >
* <span data-ttu-id="eb84e-156">**Q:  Can I use this page from a mobile device?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-156">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="eb84e-157">**A:** Yes, this page works on mobile devices.</span><span class="sxs-lookup"><span data-stu-id="eb84e-157">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="eb84e-158">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-158">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="eb84e-159">**A:** Yes, when a user resets his or her password and password writeback has been deployed with all versions of Azure AD Connect, or versions of Azure AD Sync 1.0.0485.0222 or later, then that user’s account will be automatically unlocked when that user resets his or her password.</span><span class="sxs-lookup"><span data-stu-id="eb84e-159">**A:** Yes, when a user resets his or her password and password writeback has been deployed with all versions of Azure AD Connect, or versions of Azure AD Sync 1.0.0485.0222 or later, then that user’s account will be automatically unlocked when that user resets his or her password.</span></span>
  >
  >
* <span data-ttu-id="eb84e-160">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-160">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="eb84e-161">**A:** This is not possible today.</span><span class="sxs-lookup"><span data-stu-id="eb84e-161">**A:** This is not possible today.</span></span> <span data-ttu-id="eb84e-162">However, if you absolutely need this capability and are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution found therein to solve this requirement.</span><span class="sxs-lookup"><span data-stu-id="eb84e-162">However, if you absolutely need this capability and are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution found therein to solve this requirement.</span></span>
  >
  >
* <span data-ttu-id="eb84e-163">**Q:  Can I set different security questions for different locales?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-163">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="eb84e-164">**A:** No, this is not possible today, but we are considering it.</span><span class="sxs-lookup"><span data-stu-id="eb84e-164">**A:** No, this is not possible today, but we are considering it.</span></span>
  >
  >
* <span data-ttu-id="eb84e-165">**Q:  How many questions can we configure for the Security Questions authentication option?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-165">**Q:  How many questions can we configure for the Security Questions authentication option?**</span></span>

  > <span data-ttu-id="eb84e-166">**A:** You can configure up to 20 custom security questions in the [Azure Management Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="eb84e-166">**A:** You can configure up to 20 custom security questions in the [Azure Management Portal](https://manage.windowsazure.com).</span></span>
  >
  >
* <span data-ttu-id="eb84e-167">**Q:  How long may security questions be?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-167">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="eb84e-168">**A:** Security questions may be between 3 and 200 characters long.</span><span class="sxs-lookup"><span data-stu-id="eb84e-168">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="eb84e-169">**Q:  How long may answers to security questions be?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-169">**Q:  How long may answers to security questions be?**</span></span>

  > <span data-ttu-id="eb84e-170">**A:** Answers may be 3 to 40 characters long.</span><span class="sxs-lookup"><span data-stu-id="eb84e-170">**A:** Answers may be 3 to 40 characters long.</span></span>
  >
  >
* <span data-ttu-id="eb84e-171">**Q:  Are duplicate answers to security questions rejected?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-171">**Q:  Are duplicate answers to security questions rejected?**</span></span>

  > <span data-ttu-id="eb84e-172">**A:** Yes, we reject duplicate answers to security questions.</span><span class="sxs-lookup"><span data-stu-id="eb84e-172">**A:** Yes, we reject duplicate answers to security questions.</span></span>
  >
  >
* <span data-ttu-id="eb84e-173">**Q:  May a user register more than one of the same security question?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-173">**Q:  May a user register more than one of the same security question?**</span></span>

  > <span data-ttu-id="eb84e-174">**A:** No, once a user registers a particular question, he or she may not register for that question a second time.</span><span class="sxs-lookup"><span data-stu-id="eb84e-174">**A:** No, once a user registers a particular question, he or she may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="eb84e-175">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-175">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="eb84e-176">**A:** Yes, one limit can be set for registration and another for reset.</span><span class="sxs-lookup"><span data-stu-id="eb84e-176">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="eb84e-177">3-5 security questions may be required for registration and 3-5 may be required for reset.</span><span class="sxs-lookup"><span data-stu-id="eb84e-177">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="eb84e-178">**Q:  If a user has registered more than the maximum number of questions required to reset, how are security questions selected during reset?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-178">**Q:  If a user has registered more than the maximum number of questions required to reset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="eb84e-179">**A:** N security questions are selected at random out of the total number of questions a user has registered for, where N is the minimum number of questions required for password reset.</span><span class="sxs-lookup"><span data-stu-id="eb84e-179">**A:** N security questions are selected at random out of the total number of questions a user has registered for, where N is the minimum number of questions required for password reset.</span></span> <span data-ttu-id="eb84e-180">For example, if a user has 5 security questions registered, but only 3 are required to reset, 3 of those 5 will be selected randomly and presented to the user at the time of reset.</span><span class="sxs-lookup"><span data-stu-id="eb84e-180">For example, if a user has 5 security questions registered, but only 3 are required to reset, 3 of those 5 will be selected randomly and presented to the user at the time of reset.</span></span> <span data-ttu-id="eb84e-181">If the user gets the answers to the questions wrong, the selection process re-occurs to prevent question hammering.</span><span class="sxs-lookup"><span data-stu-id="eb84e-181">If the user gets the answers to the questions wrong, the selection process re-occurs to prevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="eb84e-182">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-182">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="eb84e-183">**A:** Yes, there are several security features built into password reset.</span><span class="sxs-lookup"><span data-stu-id="eb84e-183">**A:** Yes, there are several security features built into password reset.</span></span> <span data-ttu-id="eb84e-184">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="eb84e-184">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="eb84e-185">Users may only try to validate a phone number 5 times within an hour before being locked out for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="eb84e-185">Users may only try to validate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="eb84e-186">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="eb84e-186">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="eb84e-187">**Q:  For how long are the email and SMS one-time passcode valid?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-187">**Q:  For how long are the email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="eb84e-188">**A:** The session lifetime for password reset is 105 minutes.</span><span class="sxs-lookup"><span data-stu-id="eb84e-188">**A:** The session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="eb84e-189">This means that from the beginning of the password reset operation, the user has 105 minutes to reset his or her password.</span><span class="sxs-lookup"><span data-stu-id="eb84e-189">This means that from the beginning of the password reset operation, the user has 105 minutes to reset his or her password.</span></span> <span data-ttu-id="eb84e-190">The email and SMS one-time passcode are invalid after this time period expires.</span><span class="sxs-lookup"><span data-stu-id="eb84e-190">The email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="eb84e-191">Password change</span><span class="sxs-lookup"><span data-stu-id="eb84e-191">Password change</span></span>
* <span data-ttu-id="eb84e-192">**Q:  Where should my users go to change their passwords?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-192">**Q:  Where should my users go to change their passwords?**</span></span>

  > <span data-ttu-id="eb84e-193">**A:** Users may change their passwords anywhere they see thier profile picture or icon (like in the upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span><span class="sxs-lookup"><span data-stu-id="eb84e-193">**A:** Users may change their passwords anywhere they see thier profile picture or icon (like in the upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="eb84e-194">Users may change their passwords from the [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="eb84e-194">Users may change their passwords from the [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="eb84e-195">Users may also be asked to change their passwords automatically at the Azure AD sign in screen if their passwords have expired.</span><span class="sxs-lookup"><span data-stu-id="eb84e-195">Users may also be asked to change their passwords automatically at the Azure AD sign in screen if their passwords have expired.</span></span> <span data-ttu-id="eb84e-196">Finally, users may navigate to the [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish to change their passwords.</span><span class="sxs-lookup"><span data-stu-id="eb84e-196">Finally, users may navigate to the [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish to change their passwords.</span></span>
  >
  >
* <span data-ttu-id="eb84e-197">**Q:  Can my users be notified in the Office Portal when their on-premises password expires?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-197">**Q:  Can my users be notified in the Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="eb84e-198">**A:** This is possible today if you are using ADFS by following the instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="eb84e-198">**A:** This is possible today if you are using ADFS by following the instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="eb84e-199">If you are using password hash synchronization, this is not possible today.</span><span class="sxs-lookup"><span data-stu-id="eb84e-199">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="eb84e-200">This is because we do not sync password policies from on-premises, so it is not possible for us to post expiry notifications to cloud experiences.</span><span class="sxs-lookup"><span data-stu-id="eb84e-200">This is because we do not sync password policies from on-premises, so it is not possible for us to post expiry notifications to cloud experiences.</span></span> <span data-ttu-id="eb84e-201">In either case, it is also possible to [notify users whose passwords are about to expire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb84e-201">In either case, it is also possible to [notify users whose passwords are about to expire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="eb84e-202">Password management reports</span><span class="sxs-lookup"><span data-stu-id="eb84e-202">Password management reports</span></span>
* <span data-ttu-id="eb84e-203">**Q:  How long does it take for data to show up on the password management reports?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-203">**Q:  How long does it take for data to show up on the password management reports?**</span></span>

  > <span data-ttu-id="eb84e-204">**A:** Data should appear on the password management reports within 5-10 minutes.</span><span class="sxs-lookup"><span data-stu-id="eb84e-204">**A:** Data should appear on the password management reports within 5-10 minutes.</span></span> <span data-ttu-id="eb84e-205">It some instances it may take up to an hour to appear.</span><span class="sxs-lookup"><span data-stu-id="eb84e-205">It some instances it may take up to an hour to appear.</span></span>
  >
  >
* <span data-ttu-id="eb84e-206">**Q:  How can I filter the password management reports?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-206">**Q:  How can I filter the password management reports?**</span></span>

  > <span data-ttu-id="eb84e-207">**A:** You can filter the password management reports by clicking the small magnifying glass to the extreme right of the column labels, towards the top of the report (see screenshot).</span><span class="sxs-lookup"><span data-stu-id="eb84e-207">**A:** You can filter the password management reports by clicking the small magnifying glass to the extreme right of the column labels, towards the top of the report (see screenshot).</span></span> <span data-ttu-id="eb84e-208">If you want to do richer filtering, you can download the report to excel and create a pivot table.</span><span class="sxs-lookup"><span data-stu-id="eb84e-208">If you want to do richer filtering, you can download the report to excel and create a pivot table.</span></span>
  >
  >

  ![][002]
* <span data-ttu-id="eb84e-209">**Q: What is the maximum number of events are stored in the password management reports?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-209">**Q: What is the maximum number of events are stored in the password management reports?**</span></span>

  > <span data-ttu-id="eb84e-210">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back up to 30 days.</span><span class="sxs-lookup"><span data-stu-id="eb84e-210">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back up to 30 days.</span></span>  <span data-ttu-id="eb84e-211">We are working to expand this number to include more events.</span><span class="sxs-lookup"><span data-stu-id="eb84e-211">We are working to expand this number to include more events.</span></span>
  >
  >
* <span data-ttu-id="eb84e-212">**Q:  How far back do the password management reports go?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-212">**Q:  How far back do the password management reports go?**</span></span>

  > <span data-ttu-id="eb84e-213">**A:** The password management reports show operations occurring within the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="eb84e-213">**A:** The password management reports show operations occurring within the last 30 days.</span></span> <span data-ttu-id="eb84e-214">We are currently investigating how to make this a longer time period.</span><span class="sxs-lookup"><span data-stu-id="eb84e-214">We are currently investigating how to make this a longer time period.</span></span> <span data-ttu-id="eb84e-215">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span><span class="sxs-lookup"><span data-stu-id="eb84e-215">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="eb84e-216">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-216">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span></span>

  > <span data-ttu-id="eb84e-217">**A:** Yes, a maximum of 75,000 rows may appear on either of the password management reports, whether they are being shown in the UI or being downloaded.</span><span class="sxs-lookup"><span data-stu-id="eb84e-217">**A:** Yes, a maximum of 75,000 rows may appear on either of the password management reports, whether they are being shown in the UI or being downloaded.</span></span> <span data-ttu-id="eb84e-218">We are currently investigating how to increase this limit.</span><span class="sxs-lookup"><span data-stu-id="eb84e-218">We are currently investigating how to increase this limit.</span></span>
  >
  >
* <span data-ttu-id="eb84e-219">**Q:  Is there an API to access the password reset or registration reporting data?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-219">**Q:  Is there an API to access the password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="eb84e-220">**A:** Yes, please see the following documentation to learn how you can access the password reset reporting data stream.</span><span class="sxs-lookup"><span data-stu-id="eb84e-220">**A:** Yes, please see the following documentation to learn how you can access the password reset reporting data stream.</span></span>  <span data-ttu-id="eb84e-221">[Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="eb84e-221">[Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="eb84e-222">Password writeback</span><span class="sxs-lookup"><span data-stu-id="eb84e-222">Password writeback</span></span>
* <span data-ttu-id="eb84e-223">**Q:  How does password writeback work behind the scenes?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-223">**Q:  How does password writeback work behind the scenes?**</span></span>

  > <span data-ttu-id="eb84e-224">**A:** See [How password writeback works](active-directory-passwords-learn-more.md#how-password-writeback-works) for a detailed explanation of what happens when you enable password writeback, as well as how data flows through the system back into your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="eb84e-224">**A:** See [How password writeback works](active-directory-passwords-learn-more.md#how-password-writeback-works) for a detailed explanation of what happens when you enable password writeback, as well as how data flows through the system back into your on-premises environment.</span></span> <span data-ttu-id="eb84e-225">See [Password writeback security model](active-directory-passwords-learn-more.md#password-writeback-security-model) in How password writeback works to learn how we ensure password writeback is a highly secure service.</span><span class="sxs-lookup"><span data-stu-id="eb84e-225">See [Password writeback security model](active-directory-passwords-learn-more.md#password-writeback-security-model) in How password writeback works to learn how we ensure password writeback is a highly secure service.</span></span>
  >
  >
* <span data-ttu-id="eb84e-226">**Q:  How long does password writeback take to work?  Is there a synchronization delay like with password hash sync?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-226">**Q:  How long does password writeback take to work?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="eb84e-227">**A:** Password writeback is instant.</span><span class="sxs-lookup"><span data-stu-id="eb84e-227">**A:** Password writeback is instant.</span></span> <span data-ttu-id="eb84e-228">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span><span class="sxs-lookup"><span data-stu-id="eb84e-228">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="eb84e-229">Password writeback allows users to get realtime feedback about the success of their password reset or change operation.</span><span class="sxs-lookup"><span data-stu-id="eb84e-229">Password writeback allows users to get realtime feedback about the success of their password reset or change operation.</span></span> <span data-ttu-id="eb84e-230">The average time for a successful writeback of a password is under 500 ms.</span><span class="sxs-lookup"><span data-stu-id="eb84e-230">The average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="eb84e-231">**Q:  What types of accounts does password writeback work for?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-231">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="eb84e-232">**A:** Password writeback works for Federated and Password Hash Sync’d users.</span><span class="sxs-lookup"><span data-stu-id="eb84e-232">**A:** Password writeback works for Federated and Password Hash Sync’d users.</span></span>
  >
  >
* <span data-ttu-id="eb84e-233">**Q:  Does password writeback enforce my domain’s password policies?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-233">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="eb84e-234">**A:** Yes, password writeback enforces password age, history, complexity, filters and any other restriction you may put in place on passwords in your local domain.</span><span class="sxs-lookup"><span data-stu-id="eb84e-234">**A:** Yes, password writeback enforces password age, history, complexity, filters and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="eb84e-235">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-235">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="eb84e-236">**A:** Yes, password writeback is extremely secure.</span><span class="sxs-lookup"><span data-stu-id="eb84e-236">**A:** Yes, password writeback is extremely secure.</span></span> <span data-ttu-id="eb84e-237">To read more about the 4 layers of security implemented by the password writeback service, check out the [Password writeback security model](active-directory-passwords-learn-more.md#password-writeback-security-model) in How password writeback works.</span><span class="sxs-lookup"><span data-stu-id="eb84e-237">To read more about the 4 layers of security implemented by the password writeback service, check out the [Password writeback security model](active-directory-passwords-learn-more.md#password-writeback-security-model) in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="eb84e-238">Next steps</span><span class="sxs-lookup"><span data-stu-id="eb84e-238">Next steps</span></span>
<span data-ttu-id="eb84e-239">Below are links to all of the Azure AD Password Reset documentation pages:</span><span class="sxs-lookup"><span data-stu-id="eb84e-239">Below are links to all of the Azure AD Password Reset documentation pages:</span></span>

* <span data-ttu-id="eb84e-240">**Are you here because you're having problems signing in?**</span><span class="sxs-lookup"><span data-stu-id="eb84e-240">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="eb84e-241">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span><span class="sxs-lookup"><span data-stu-id="eb84e-241">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span></span>
* <span data-ttu-id="eb84e-242">[**How it works**](active-directory-passwords-how-it-works.md) - learn about the six different components of the service and what each does</span><span class="sxs-lookup"><span data-stu-id="eb84e-242">[**How it works**](active-directory-passwords-how-it-works.md) - learn about the six different components of the service and what each does</span></span>
* <span data-ttu-id="eb84e-243">[**Getting started**](active-directory-passwords-getting-started.md) - learn how to allow you users to reset and change their cloud or on-premises passwords</span><span class="sxs-lookup"><span data-stu-id="eb84e-243">[**Getting started**](active-directory-passwords-getting-started.md) - learn how to allow you users to reset and change their cloud or on-premises passwords</span></span>
* <span data-ttu-id="eb84e-244">[**Customize**](active-directory-passwords-customize.md) - learn how to customize the look & feel and behavior of the service to your organization's needs</span><span class="sxs-lookup"><span data-stu-id="eb84e-244">[**Customize**](active-directory-passwords-customize.md) - learn how to customize the look & feel and behavior of the service to your organization's needs</span></span>
* <span data-ttu-id="eb84e-245">[**Best practices**](active-directory-passwords-best-practices.md) - learn how to quickly deploy and effectively manage passwords in your organization</span><span class="sxs-lookup"><span data-stu-id="eb84e-245">[**Best practices**](active-directory-passwords-best-practices.md) - learn how to quickly deploy and effectively manage passwords in your organization</span></span>
* <span data-ttu-id="eb84e-246">[**Get insights**](active-directory-passwords-get-insights.md) - learn about our integrated reporting capabilities</span><span class="sxs-lookup"><span data-stu-id="eb84e-246">[**Get insights**](active-directory-passwords-get-insights.md) - learn about our integrated reporting capabilities</span></span>
* <span data-ttu-id="eb84e-247">[**Troubleshooting**](active-directory-passwords-troubleshoot.md) - learn how to quickly troubleshoot problems with the service</span><span class="sxs-lookup"><span data-stu-id="eb84e-247">[**Troubleshooting**](active-directory-passwords-troubleshoot.md) - learn how to quickly troubleshoot problems with the service</span></span>
* <span data-ttu-id="eb84e-248">[**Learn more**](active-directory-passwords-learn-more.md) - go deep into the technical details of how the service works</span><span class="sxs-lookup"><span data-stu-id="eb84e-248">[**Learn more**](active-directory-passwords-learn-more.md) - go deep into the technical details of how the service works</span></span>

[001]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-faq/001.jpg "Image_001.jpg"
[002]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-faq/002.jpg "Image_002.jpg"


