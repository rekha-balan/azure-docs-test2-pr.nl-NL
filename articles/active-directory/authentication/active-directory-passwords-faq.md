---
title: Self-service password reset FAQ - Azure Active Directory
description: Frequently asked questions about Azure AD self-service password reset
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: 92f9732adadc4eb580d89f8a43cf76177450aeb7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858014"
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="d3e49-103">Password management frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="d3e49-103">Password management frequently asked questions</span></span>

<span data-ttu-id="d3e49-104">The following are some frequently asked questions (FAQ) for all things related to password reset.</span><span class="sxs-lookup"><span data-stu-id="d3e49-104">The following are some frequently asked questions (FAQ) for all things related to password reset.</span></span>

<span data-ttu-id="d3e49-105">If you have a general question about Azure Active Directory (Azure AD) and self-service password reset (SSPR) that's not answered here, you can ask the community for assistance on the [Azure AD forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="d3e49-105">If you have a general question about Azure Active Directory (Azure AD) and self-service password reset (SSPR) that's not answered here, you can ask the community for assistance on the [Azure AD forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="d3e49-106">Members of the community include engineers, product managers, MVPs, and fellow IT professionals.</span><span class="sxs-lookup"><span data-stu-id="d3e49-106">Members of the community include engineers, product managers, MVPs, and fellow IT professionals.</span></span>

<span data-ttu-id="d3e49-107">This FAQ is split into the following sections:</span><span class="sxs-lookup"><span data-stu-id="d3e49-107">This FAQ is split into the following sections:</span></span>

* [<span data-ttu-id="d3e49-108">Questions about password reset registration</span><span class="sxs-lookup"><span data-stu-id="d3e49-108">Questions about password reset registration</span></span>](#password-reset-registration)
* [<span data-ttu-id="d3e49-109">Questions about password reset</span><span class="sxs-lookup"><span data-stu-id="d3e49-109">Questions about password reset</span></span>](#password-reset)
* [<span data-ttu-id="d3e49-110">Questions about password change</span><span class="sxs-lookup"><span data-stu-id="d3e49-110">Questions about password change</span></span>](#password-change)
* [<span data-ttu-id="d3e49-111">Questions about password management reports</span><span class="sxs-lookup"><span data-stu-id="d3e49-111">Questions about password management reports</span></span>](#password-management-reports)
* [<span data-ttu-id="d3e49-112">Questions about password writeback</span><span class="sxs-lookup"><span data-stu-id="d3e49-112">Questions about password writeback</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="d3e49-113">Password reset registration</span><span class="sxs-lookup"><span data-stu-id="d3e49-113">Password reset registration</span></span>

* <span data-ttu-id="d3e49-114">**Q:  Can my users register their own password reset data?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-114">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="d3e49-115">**A:** Yes.</span><span class="sxs-lookup"><span data-stu-id="d3e49-115">**A:** Yes.</span></span> <span data-ttu-id="d3e49-116">As long as password reset is enabled and they are licensed, users can go to the password reset registration portal (https://aka.ms/ssprsetup) to register their authentication information.</span><span class="sxs-lookup"><span data-stu-id="d3e49-116">As long as password reset is enabled and they are licensed, users can go to the password reset registration portal (https://aka.ms/ssprsetup) to register their authentication information.</span></span> <span data-ttu-id="d3e49-117">Users can also register through the Access Panel (http://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d3e49-117">Users can also register through the Access Panel (http://myapps.microsoft.com).</span></span> <span data-ttu-id="d3e49-118">To register through the Access Panel, they need to select their profile picture, select **Profile**, and then select the **Register for password reset** option.</span><span class="sxs-lookup"><span data-stu-id="d3e49-118">To register through the Access Panel, they need to select their profile picture, select **Profile**, and then select the **Register for password reset** option.</span></span>
  >
  >
* <span data-ttu-id="d3e49-119">**Q:  If I enable password reset for a group and then decide to enable it for everyone are my users required re-register?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-119">**Q:  If I enable password reset for a group and then decide to enable it for everyone are my users required re-register?**</span></span>

  > <span data-ttu-id="d3e49-120">**A:** No.</span><span class="sxs-lookup"><span data-stu-id="d3e49-120">**A:** No.</span></span> <span data-ttu-id="d3e49-121">Users who have populated authentication data are not required to re-register.</span><span class="sxs-lookup"><span data-stu-id="d3e49-121">Users who have populated authentication data are not required to re-register.</span></span>
  >
  >
* <span data-ttu-id="d3e49-122">**Q:  Can I define password reset data on behalf of my users?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-122">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="d3e49-123">**A:** Yes, you can do so with Azure AD Connect, PowerShell, the [Azure portal](https://portal.azure.com), or the Office 365 Admin center.</span><span class="sxs-lookup"><span data-stu-id="d3e49-123">**A:** Yes, you can do so with Azure AD Connect, PowerShell, the [Azure portal](https://portal.azure.com), or the Office 365 Admin center.</span></span> <span data-ttu-id="d3e49-124">For more information, see [Data used by Azure AD self-service password reset](howto-sspr-authenticationdata.md).</span><span class="sxs-lookup"><span data-stu-id="d3e49-124">For more information, see [Data used by Azure AD self-service password reset](howto-sspr-authenticationdata.md).</span></span>
  >
  >
* <span data-ttu-id="d3e49-125">**Q:  Can I synchronize data for security questions from on-premises?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-125">**Q:  Can I synchronize data for security questions from on-premises?**</span></span>

  > <span data-ttu-id="d3e49-126">**A:** No, this is not possible today.</span><span class="sxs-lookup"><span data-stu-id="d3e49-126">**A:** No, this is not possible today.</span></span>
  >
  >
* <span data-ttu-id="d3e49-127">**Q:  Can my users register data in such a way that other users can't see this data?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-127">**Q:  Can my users register data in such a way that other users can't see this data?**</span></span>

  > <span data-ttu-id="d3e49-128">**A:** Yes.</span><span class="sxs-lookup"><span data-stu-id="d3e49-128">**A:** Yes.</span></span> <span data-ttu-id="d3e49-129">When users register data by using the password reset registration portal, the data is saved into private authentication fields that are visible only to global administrators and the user.</span><span class="sxs-lookup"><span data-stu-id="d3e49-129">When users register data by using the password reset registration portal, the data is saved into private authentication fields that are visible only to global administrators and the user.</span></span>
  >
  >
* <span data-ttu-id="d3e49-130">**Q:  Do my users have to be registered before they can use password reset?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-130">**Q:  Do my users have to be registered before they can use password reset?**</span></span>

  > <span data-ttu-id="d3e49-131">**A:** No.</span><span class="sxs-lookup"><span data-stu-id="d3e49-131">**A:** No.</span></span> <span data-ttu-id="d3e49-132">If you define enough authentication information on their behalf, users don't have to register.</span><span class="sxs-lookup"><span data-stu-id="d3e49-132">If you define enough authentication information on their behalf, users don't have to register.</span></span> <span data-ttu-id="d3e49-133">Password reset works as long as you have properly formatted the data stored in the appropriate fields in the directory.</span><span class="sxs-lookup"><span data-stu-id="d3e49-133">Password reset works as long as you have properly formatted the data stored in the appropriate fields in the directory.</span></span>
  >
  >
* <span data-ttu-id="d3e49-134">**Q:  Can I synchronize or set the authentication phone, authentication email, or alternate authentication phone fields on behalf of my users?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-134">**Q:  Can I synchronize or set the authentication phone, authentication email, or alternate authentication phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="d3e49-135">**A:** The fields that are able to be set by a Global Administrator are defined in the article [SSPR Data requirements](howto-sspr-authenticationdata.md).</span><span class="sxs-lookup"><span data-stu-id="d3e49-135">**A:** The fields that are able to be set by a Global Administrator are defined in the article [SSPR Data requirements](howto-sspr-authenticationdata.md).</span></span>
  >
  >
* <span data-ttu-id="d3e49-136">**Q:  How does the registration portal determine which options to show my users?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-136">**Q:  How does the registration portal determine which options to show my users?**</span></span>

  > <span data-ttu-id="d3e49-137">**A:** The password reset registration portal shows only the options that you have enabled for your users.</span><span class="sxs-lookup"><span data-stu-id="d3e49-137">**A:** The password reset registration portal shows only the options that you have enabled for your users.</span></span> <span data-ttu-id="d3e49-138">These options are found under the **User Password Reset Policy** section of your directory’s **Configure** tab. For example, if you don't enable security questions, then users are not able to register for that option.</span><span class="sxs-lookup"><span data-stu-id="d3e49-138">These options are found under the **User Password Reset Policy** section of your directory’s **Configure** tab. For example, if you don't enable security questions, then users are not able to register for that option.</span></span>
  >
  >
* <span data-ttu-id="d3e49-139">**Q:  When is a user considered registered?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-139">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="d3e49-140">**A:** A user is considered registered for SSPR when they have registered at least the **Number of methods required to reset** a password that you have set in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3e49-140">**A:** A user is considered registered for SSPR when they have registered at least the **Number of methods required to reset** a password that you have set in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >

## <a name="password-reset"></a><span data-ttu-id="d3e49-141">Password reset</span><span class="sxs-lookup"><span data-stu-id="d3e49-141">Password reset</span></span>

* <span data-ttu-id="d3e49-142">**Q:  Do you prevent users from multiple attempts to reset a password in a short period of time?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-142">**Q:  Do you prevent users from multiple attempts to reset a password in a short period of time?**</span></span>

  > <span data-ttu-id="d3e49-143">**A:** Yes, there are security features built into password reset to protect it from misuse.</span><span class="sxs-lookup"><span data-stu-id="d3e49-143">**A:** Yes, there are security features built into password reset to protect it from misuse.</span></span> 
  >
  > <span data-ttu-id="d3e49-144">Users can try only five password reset attempts within a 24 hour period before they're locked out for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="d3e49-144">Users can try only five password reset attempts within a 24 hour period before they're locked out for 24 hours.</span></span> 
  >
  > <span data-ttu-id="d3e49-145">Users can try to validate a phone number, send a SMS, or validate security questions and answers only five times within an hour before they're locked out for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="d3e49-145">Users can try to validate a phone number, send a SMS, or validate security questions and answers only five times within an hour before they're locked out for 24 hours.</span></span> 
  >
  > <span data-ttu-id="d3e49-146">Users can send an email a maximum of 10 times within a 10 minute period before they're locked out for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="d3e49-146">Users can send an email a maximum of 10 times within a 10 minute period before they're locked out for 24 hours.</span></span>
  >
  > <span data-ttu-id="d3e49-147">The counters are reset once a user resets their password.</span><span class="sxs-lookup"><span data-stu-id="d3e49-147">The counters are reset once a user resets their password.</span></span>
  >
  >
* <span data-ttu-id="d3e49-148">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-148">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="d3e49-149">**A:** Emails, SMS messages, and phone calls should arrive in under a minute.</span><span class="sxs-lookup"><span data-stu-id="d3e49-149">**A:** Emails, SMS messages, and phone calls should arrive in under a minute.</span></span> <span data-ttu-id="d3e49-150">The normal case is 5 to 20 seconds.</span><span class="sxs-lookup"><span data-stu-id="d3e49-150">The normal case is 5 to 20 seconds.</span></span>
    ><span data-ttu-id="d3e49-151">If you don't receive the notification in this time frame:</span><span class="sxs-lookup"><span data-stu-id="d3e49-151">If you don't receive the notification in this time frame:</span></span>
        > * <span data-ttu-id="d3e49-152">Check your junk folder.</span><span class="sxs-lookup"><span data-stu-id="d3e49-152">Check your junk folder.</span></span>
        > * <span data-ttu-id="d3e49-153">Check that the number or email being contacted is the one you expect.</span><span class="sxs-lookup"><span data-stu-id="d3e49-153">Check that the number or email being contacted is the one you expect.</span></span>
        > * <span data-ttu-id="d3e49-154">Check that the authentication data in the directory is correctly formatted, for example, +1 4255551234 or *user@contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="d3e49-154">Check that the authentication data in the directory is correctly formatted, for example, +1 4255551234 or *user@contoso.com*.</span></span> 
  >
  >
* <span data-ttu-id="d3e49-155">**Q:  What languages are supported by password reset?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-155">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="d3e49-156">**A:** The password reset UI, SMS messages, and voice calls are localized in the same languages that are supported in Office 365.</span><span class="sxs-lookup"><span data-stu-id="d3e49-156">**A:** The password reset UI, SMS messages, and voice calls are localized in the same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="d3e49-157">**Q:  What parts of the password reset experience get branded when I set the organizational branding items in my directory’s configure tab?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-157">**Q:  What parts of the password reset experience get branded when I set the organizational branding items in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="d3e49-158">**A:** The password reset portal shows your organization's logo and allows you to configure the "Contact your administrator" link to point to a custom email or URL.</span><span class="sxs-lookup"><span data-stu-id="d3e49-158">**A:** The password reset portal shows your organization's logo and allows you to configure the "Contact your administrator" link to point to a custom email or URL.</span></span> <span data-ttu-id="d3e49-159">Any email that's sent by password reset includes your organization’s logo, colors, and name in the body of the email, and is customized from the settings for that particular name.</span><span class="sxs-lookup"><span data-stu-id="d3e49-159">Any email that's sent by password reset includes your organization’s logo, colors, and name in the body of the email, and is customized from the settings for that particular name.</span></span>
  >
  >
* <span data-ttu-id="d3e49-160">**Q:  How can I educate my users about where to go to reset their passwords?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-160">**Q:  How can I educate my users about where to go to reset their passwords?**</span></span>

  > <span data-ttu-id="d3e49-161">**A:** Try some of the suggestions in our [SSPR deployment](howto-sspr-deployment.md#sample-communication) article.</span><span class="sxs-lookup"><span data-stu-id="d3e49-161">**A:** Try some of the suggestions in our [SSPR deployment](howto-sspr-deployment.md#sample-communication) article.</span></span>
  >
  >
* <span data-ttu-id="d3e49-162">**Q:  Can I use this page from a mobile device?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-162">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="d3e49-163">**A:** Yes, this page works on mobile devices.</span><span class="sxs-lookup"><span data-stu-id="d3e49-163">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="d3e49-164">**Q:  Do you support unlocking local Active Directory accounts when users reset their passwords?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-164">**Q:  Do you support unlocking local Active Directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="d3e49-165">**A:** Yes.</span><span class="sxs-lookup"><span data-stu-id="d3e49-165">**A:** Yes.</span></span> <span data-ttu-id="d3e49-166">When a user resets their password, if password writeback has been deployed through Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span><span class="sxs-lookup"><span data-stu-id="d3e49-166">When a user resets their password, if password writeback has been deployed through Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="d3e49-167">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-167">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="d3e49-168">**A:** If you're an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution.</span><span class="sxs-lookup"><span data-stu-id="d3e49-168">**A:** If you're an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution.</span></span>
  >
  >
* <span data-ttu-id="d3e49-169">**Q:  Can I set different security questions for different locales?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-169">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="d3e49-170">**A:** No, this is not possible today.</span><span class="sxs-lookup"><span data-stu-id="d3e49-170">**A:** No, this is not possible today.</span></span>
  >
  >
* <span data-ttu-id="d3e49-171">**Q:  How many questions can I configure for the security questions authentication option?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-171">**Q:  How many questions can I configure for the security questions authentication option?**</span></span>

  > <span data-ttu-id="d3e49-172">**A:** You can configure up to 20 custom security questions in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3e49-172">**A:** You can configure up to 20 custom security questions in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="d3e49-173">**Q:  How long can security questions be?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-173">**Q:  How long can security questions be?**</span></span>

  > <span data-ttu-id="d3e49-174">**A:** Security questions can be 3 to 200 characters long.</span><span class="sxs-lookup"><span data-stu-id="d3e49-174">**A:** Security questions can be 3 to 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="d3e49-175">**Q:  How long can the answers to security questions be?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-175">**Q:  How long can the answers to security questions be?**</span></span>

  > <span data-ttu-id="d3e49-176">**A:** Answers can be 3 to 40 characters long.</span><span class="sxs-lookup"><span data-stu-id="d3e49-176">**A:** Answers can be 3 to 40 characters long.</span></span>
  >
  >
* <span data-ttu-id="d3e49-177">**Q:  Are duplicate answers to security questions rejected?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-177">**Q:  Are duplicate answers to security questions rejected?**</span></span>

  > <span data-ttu-id="d3e49-178">**A:** Yes, we reject duplicate answers to security questions.</span><span class="sxs-lookup"><span data-stu-id="d3e49-178">**A:** Yes, we reject duplicate answers to security questions.</span></span>
  >
  >
* <span data-ttu-id="d3e49-179">**Q:  Can a user register the same security question more than once?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-179">**Q:  Can a user register the same security question more than once?**</span></span>

  > <span data-ttu-id="d3e49-180">**A:** No.</span><span class="sxs-lookup"><span data-stu-id="d3e49-180">**A:** No.</span></span> <span data-ttu-id="d3e49-181">After a user registers a particular question, they can't register for that question a second time.</span><span class="sxs-lookup"><span data-stu-id="d3e49-181">After a user registers a particular question, they can't register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="d3e49-182">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-182">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="d3e49-183">**A:** Yes, one limit can be set for registration and another for reset.</span><span class="sxs-lookup"><span data-stu-id="d3e49-183">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="d3e49-184">Three to five security questions can be required for registration, and three to five questions can be required for reset.</span><span class="sxs-lookup"><span data-stu-id="d3e49-184">Three to five security questions can be required for registration, and three to five questions can be required for reset.</span></span>
  >
  >
* <span data-ttu-id="d3e49-185">**Q:  I configured my policy to require users to use security questions for reset, but the Azure administrators seem to be configured differently.**</span><span class="sxs-lookup"><span data-stu-id="d3e49-185">**Q:  I configured my policy to require users to use security questions for reset, but the Azure administrators seem to be configured differently.**</span></span>

  > <span data-ttu-id="d3e49-186">**A:** This is the expected behavior.</span><span class="sxs-lookup"><span data-stu-id="d3e49-186">**A:** This is the expected behavior.</span></span> <span data-ttu-id="d3e49-187">Microsoft enforces a strong default two-gate password reset policy for any Azure administrator role.</span><span class="sxs-lookup"><span data-stu-id="d3e49-187">Microsoft enforces a strong default two-gate password reset policy for any Azure administrator role.</span></span> <span data-ttu-id="d3e49-188">This prevents administrators from using security questions.</span><span class="sxs-lookup"><span data-stu-id="d3e49-188">This prevents administrators from using security questions.</span></span> <span data-ttu-id="d3e49-189">You can find more information about this policy in the [Password policies and restrictions in Azure Active Directory](concept-sspr-policy.md) article.</span><span class="sxs-lookup"><span data-stu-id="d3e49-189">You can find more information about this policy in the [Password policies and restrictions in Azure Active Directory](concept-sspr-policy.md) article.</span></span>
  >
  >
* <span data-ttu-id="d3e49-190">**Q:  If a user has registered more than the maximum number of questions required to reset, how are the security questions selected during reset?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-190">**Q:  If a user has registered more than the maximum number of questions required to reset, how are the security questions selected during reset?**</span></span>

  > <span data-ttu-id="d3e49-191">**A:** *N* number of security questions are selected at random out of the total number of questions a user has registered for, where *N* is the amount that is set for the **Number of questions required to reset** option.</span><span class="sxs-lookup"><span data-stu-id="d3e49-191">**A:** *N* number of security questions are selected at random out of the total number of questions a user has registered for, where *N* is the amount that is set for the **Number of questions required to reset** option.</span></span> <span data-ttu-id="d3e49-192">For example, if a user has registered five security questions, but only three are required to reset a password, three of the five questions are randomly selected and are presented at reset.</span><span class="sxs-lookup"><span data-stu-id="d3e49-192">For example, if a user has registered five security questions, but only three are required to reset a password, three of the five questions are randomly selected and are presented at reset.</span></span> <span data-ttu-id="d3e49-193">To prevent question hammering, if the user gets the answers to the questions wrong the selection process starts over.</span><span class="sxs-lookup"><span data-stu-id="d3e49-193">To prevent question hammering, if the user gets the answers to the questions wrong the selection process starts over.</span></span>
  >
  >
* <span data-ttu-id="d3e49-194">**Q:  How long are the email and SMS one-time passcodes valid?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-194">**Q:  How long are the email and SMS one-time passcodes valid?**</span></span>

  > <span data-ttu-id="d3e49-195">**A:** The session lifetime for password reset is 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="d3e49-195">**A:** The session lifetime for password reset is 15 minutes.</span></span> <span data-ttu-id="d3e49-196">From the start of the password reset operation, the user has 15 minutes to reset their password.</span><span class="sxs-lookup"><span data-stu-id="d3e49-196">From the start of the password reset operation, the user has 15 minutes to reset their password.</span></span> <span data-ttu-id="d3e49-197">The email and SMS one-time passcode are invalid after this time period expires.</span><span class="sxs-lookup"><span data-stu-id="d3e49-197">The email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >
* <span data-ttu-id="d3e49-198">**Q:  Can I block users from resetting their password?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-198">**Q:  Can I block users from resetting their password?**</span></span>

  > <span data-ttu-id="d3e49-199">**A:** Yes, if you use a group to enable SSPR, you can remove an individual user from the group that allows users to reset their password.</span><span class="sxs-lookup"><span data-stu-id="d3e49-199">**A:** Yes, if you use a group to enable SSPR, you can remove an individual user from the group that allows users to reset their password.</span></span> <span data-ttu-id="d3e49-200">If the user is a Global Administrator they will retain the ability to reset their password and this cannot be disabled.</span><span class="sxs-lookup"><span data-stu-id="d3e49-200">If the user is a Global Administrator they will retain the ability to reset their password and this cannot be disabled.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="d3e49-201">Password change</span><span class="sxs-lookup"><span data-stu-id="d3e49-201">Password change</span></span>

* <span data-ttu-id="d3e49-202">**Q:  Where should my users go to change their passwords?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-202">**Q:  Where should my users go to change their passwords?**</span></span>

  > <span data-ttu-id="d3e49-203">**A:** Users can change their passwords anywhere they see their profile picture or icon, like in the upper-right corner of their [Office 365](https://portal.office.com) portal or [Access Panel](https://myapps.microsoft.com) experiences.</span><span class="sxs-lookup"><span data-stu-id="d3e49-203">**A:** Users can change their passwords anywhere they see their profile picture or icon, like in the upper-right corner of their [Office 365](https://portal.office.com) portal or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="d3e49-204">Users can change their passwords from the [Access Panel Profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="d3e49-204">Users can change their passwords from the [Access Panel Profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="d3e49-205">Users can also be asked to change their passwords automatically at the Azure AD sign-in page if their passwords have expired.</span><span class="sxs-lookup"><span data-stu-id="d3e49-205">Users can also be asked to change their passwords automatically at the Azure AD sign-in page if their passwords have expired.</span></span> <span data-ttu-id="d3e49-206">Finally, users can browse to the [Azure AD password change portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they want to change their passwords.</span><span class="sxs-lookup"><span data-stu-id="d3e49-206">Finally, users can browse to the [Azure AD password change portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they want to change their passwords.</span></span>
  >
  >
* <span data-ttu-id="d3e49-207">**Q:  Can my users be notified in the Office portal when their on-premises password expires?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-207">**Q:  Can my users be notified in the Office portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="d3e49-208">**A:** Yes, this is possible today if you use Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="d3e49-208">**A:** Yes, this is possible today if you use Active Directory Federation Services (AD FS).</span></span> <span data-ttu-id="d3e49-209">If you use AD FS, follow the instructions in the [Sending password policy claims with AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396) article.</span><span class="sxs-lookup"><span data-stu-id="d3e49-209">If you use AD FS, follow the instructions in the [Sending password policy claims with AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396) article.</span></span> <span data-ttu-id="d3e49-210">If you use password hash synchronization, this is not possible today.</span><span class="sxs-lookup"><span data-stu-id="d3e49-210">If you use password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="d3e49-211">We don't sync password policies from on-premises directories, so it's not possible for us to post expiration notifications to cloud experiences.</span><span class="sxs-lookup"><span data-stu-id="d3e49-211">We don't sync password policies from on-premises directories, so it's not possible for us to post expiration notifications to cloud experiences.</span></span> <span data-ttu-id="d3e49-212">In either case, it's also possible to [notify users whose passwords are about to expire through PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3e49-212">In either case, it's also possible to [notify users whose passwords are about to expire through PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >
* <span data-ttu-id="d3e49-213">**Q:  Can I block users from changing their password?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-213">**Q:  Can I block users from changing their password?**</span></span>

  > <span data-ttu-id="d3e49-214">**A:** For cloud-only users, password changes can't be blocked.</span><span class="sxs-lookup"><span data-stu-id="d3e49-214">**A:** For cloud-only users, password changes can't be blocked.</span></span> <span data-ttu-id="d3e49-215">For on-premises users, you can set the **User cannot change password** option to selected.</span><span class="sxs-lookup"><span data-stu-id="d3e49-215">For on-premises users, you can set the **User cannot change password** option to selected.</span></span> <span data-ttu-id="d3e49-216">The selected users can't change their password.</span><span class="sxs-lookup"><span data-stu-id="d3e49-216">The selected users can't change their password.</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="d3e49-217">Password management reports</span><span class="sxs-lookup"><span data-stu-id="d3e49-217">Password management reports</span></span>

* <span data-ttu-id="d3e49-218">**Q:  How long does it take for data to show up on the password management reports?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-218">**Q:  How long does it take for data to show up on the password management reports?**</span></span>

  > <span data-ttu-id="d3e49-219">**A:** Data should appear on the password management reports in 5 to 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="d3e49-219">**A:** Data should appear on the password management reports in 5 to 10 minutes.</span></span> <span data-ttu-id="d3e49-220">In some instances, it might take up to an hour to appear.</span><span class="sxs-lookup"><span data-stu-id="d3e49-220">In some instances, it might take up to an hour to appear.</span></span>
  >
  >
* <span data-ttu-id="d3e49-221">**Q:  How can I filter the password management reports?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-221">**Q:  How can I filter the password management reports?**</span></span>

  > <span data-ttu-id="d3e49-222">**A:** To filter the password management reports, select the small magnifying glass to the extreme right of the column labels, near the top of the report.</span><span class="sxs-lookup"><span data-stu-id="d3e49-222">**A:** To filter the password management reports, select the small magnifying glass to the extreme right of the column labels, near the top of the report.</span></span> <span data-ttu-id="d3e49-223">If you want to do richer filtering, you can download the report to Excel and create a pivot table.</span><span class="sxs-lookup"><span data-stu-id="d3e49-223">If you want to do richer filtering, you can download the report to Excel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="d3e49-224">**Q: What is the maximum number of events that are stored in the password management reports?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-224">**Q: What is the maximum number of events that are stored in the password management reports?**</span></span>

  > <span data-ttu-id="d3e49-225">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back as far as 30 days.</span><span class="sxs-lookup"><span data-stu-id="d3e49-225">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back as far as 30 days.</span></span> <span data-ttu-id="d3e49-226">We are working to expand this number to include more events.</span><span class="sxs-lookup"><span data-stu-id="d3e49-226">We are working to expand this number to include more events.</span></span>
  >
  >
* <span data-ttu-id="d3e49-227">**Q:  How far back do the password management reports go?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-227">**Q:  How far back do the password management reports go?**</span></span>

  > <span data-ttu-id="d3e49-228">**A:** The password management reports show operations that occurred within the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="d3e49-228">**A:** The password management reports show operations that occurred within the last 30 days.</span></span> <span data-ttu-id="d3e49-229">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span><span class="sxs-lookup"><span data-stu-id="d3e49-229">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="d3e49-230">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-230">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span></span>

  > <span data-ttu-id="d3e49-231">**A:** Yes.</span><span class="sxs-lookup"><span data-stu-id="d3e49-231">**A:** Yes.</span></span> <span data-ttu-id="d3e49-232">A maximum of 75,000 rows can appear on either of the password management reports, whether they are shown in the UI or are downloaded.</span><span class="sxs-lookup"><span data-stu-id="d3e49-232">A maximum of 75,000 rows can appear on either of the password management reports, whether they are shown in the UI or are downloaded.</span></span>
  >
  >
* <span data-ttu-id="d3e49-233">**Q:  Is there an API to access the password reset or registration reporting data?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-233">**Q:  Is there an API to access the password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="d3e49-234">**A:** Yes.</span><span class="sxs-lookup"><span data-stu-id="d3e49-234">**A:** Yes.</span></span> <span data-ttu-id="d3e49-235">To learn how you can access the password reset reporting data stream, see [Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="d3e49-235">To learn how you can access the password reset reporting data stream, see [Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="d3e49-236">Password writeback</span><span class="sxs-lookup"><span data-stu-id="d3e49-236">Password writeback</span></span>

* <span data-ttu-id="d3e49-237">**Q:  How does password writeback work behind the scenes?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-237">**Q:  How does password writeback work behind the scenes?**</span></span>

  > <span data-ttu-id="d3e49-238">**A:** See the article [How password writeback works](howto-sspr-writeback.md) for an explanation of what happens when you enable password writeback and how data flows through the system back into your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="d3e49-238">**A:** See the article [How password writeback works](howto-sspr-writeback.md) for an explanation of what happens when you enable password writeback and how data flows through the system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="d3e49-239">**Q:  How long does password writeback take to work? Is there a synchronization delay like there is with password hash sync?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-239">**Q:  How long does password writeback take to work? Is there a synchronization delay like there is with password hash sync?**</span></span>

  > <span data-ttu-id="d3e49-240">**A:** Password writeback is instant.</span><span class="sxs-lookup"><span data-stu-id="d3e49-240">**A:** Password writeback is instant.</span></span> <span data-ttu-id="d3e49-241">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span><span class="sxs-lookup"><span data-stu-id="d3e49-241">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="d3e49-242">Password writeback allows users to get real-time feedback about the success of their password reset or change operation.</span><span class="sxs-lookup"><span data-stu-id="d3e49-242">Password writeback allows users to get real-time feedback about the success of their password reset or change operation.</span></span> <span data-ttu-id="d3e49-243">The average time for a successful writeback of a password is under 500 ms.</span><span class="sxs-lookup"><span data-stu-id="d3e49-243">The average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="d3e49-244">**Q:  If my on-premises account is disabled, how is my cloud account and access affected?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-244">**Q:  If my on-premises account is disabled, how is my cloud account and access affected?**</span></span>

  > <span data-ttu-id="d3e49-245">**A:** If your on-premises ID is disabled, your cloud ID and access will also be disabled at the next sync interval through Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d3e49-245">**A:** If your on-premises ID is disabled, your cloud ID and access will also be disabled at the next sync interval through Azure AD Connect.</span></span> <span data-ttu-id="d3e49-246">By default, this sync is every 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="d3e49-246">By default, this sync is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="d3e49-247">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change my password?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-247">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change my password?**</span></span>

  > <span data-ttu-id="d3e49-248">**A:** Yes, SSPR relies on and abides by the on-premises Active Directory password policy.</span><span class="sxs-lookup"><span data-stu-id="d3e49-248">**A:** Yes, SSPR relies on and abides by the on-premises Active Directory password policy.</span></span> <span data-ttu-id="d3e49-249">This policy includes the typical Active Directory domain password policy, as well as any defined, fine-grained password policies that are targeted to a user.</span><span class="sxs-lookup"><span data-stu-id="d3e49-249">This policy includes the typical Active Directory domain password policy, as well as any defined, fine-grained password policies that are targeted to a user.</span></span>
  >
  >
* <span data-ttu-id="d3e49-250">**Q:  What types of accounts does password writeback work for?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-250">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="d3e49-251">**A:** Password writeback works for user accounts that are synchronized from on-premises Active Directory to Azure AD, including federated, password hash synchronized, and Pass-Through Autentication Users.</span><span class="sxs-lookup"><span data-stu-id="d3e49-251">**A:** Password writeback works for user accounts that are synchronized from on-premises Active Directory to Azure AD, including federated, password hash synchronized, and Pass-Through Autentication Users.</span></span>
  >
  >
* <span data-ttu-id="d3e49-252">**Q:  Does password writeback enforce my domain’s password policies?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-252">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="d3e49-253">**A:** Yes.</span><span class="sxs-lookup"><span data-stu-id="d3e49-253">**A:** Yes.</span></span> <span data-ttu-id="d3e49-254">Password writeback enforces password age, history, complexity, filters, and any other restriction you might put in place on passwords in your local domain.</span><span class="sxs-lookup"><span data-stu-id="d3e49-254">Password writeback enforces password age, history, complexity, filters, and any other restriction you might put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="d3e49-255">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span><span class="sxs-lookup"><span data-stu-id="d3e49-255">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="d3e49-256">**A:** Yes, password writeback is secure.</span><span class="sxs-lookup"><span data-stu-id="d3e49-256">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="d3e49-257">To read more about the multiple layers of security implemented by the password writeback service, check out the [Password writeback security](concept-sspr-writeback.md#password-writeback-security) section in the [Password writeback overview](howto-sspr-writeback.md) article.</span><span class="sxs-lookup"><span data-stu-id="d3e49-257">To read more about the multiple layers of security implemented by the password writeback service, check out the [Password writeback security](concept-sspr-writeback.md#password-writeback-security) section in the [Password writeback overview](howto-sspr-writeback.md) article.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="d3e49-258">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3e49-258">Next steps</span></span>

* [<span data-ttu-id="d3e49-259">How do I complete a successful rollout of SSPR?</span><span class="sxs-lookup"><span data-stu-id="d3e49-259">How do I complete a successful rollout of SSPR?</span></span>](howto-sspr-deployment.md)
* [<span data-ttu-id="d3e49-260">Reset or change your password</span><span class="sxs-lookup"><span data-stu-id="d3e49-260">Reset or change your password</span></span>](../user-help/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="d3e49-261">Register for self-service password reset</span><span class="sxs-lookup"><span data-stu-id="d3e49-261">Register for self-service password reset</span></span>](../user-help/active-directory-passwords-reset-register.md)
* [<span data-ttu-id="d3e49-262">Do you have a licensing question?</span><span class="sxs-lookup"><span data-stu-id="d3e49-262">Do you have a licensing question?</span></span>](concept-sspr-licensing.md)
* [<span data-ttu-id="d3e49-263">What data is used by SSPR and what data should you populate for your users?</span><span class="sxs-lookup"><span data-stu-id="d3e49-263">What data is used by SSPR and what data should you populate for your users?</span></span>](howto-sspr-authenticationdata.md)
* [<span data-ttu-id="d3e49-264">What authentication methods are available to users?</span><span class="sxs-lookup"><span data-stu-id="d3e49-264">What authentication methods are available to users?</span></span>](concept-sspr-howitworks.md#authentication-methods)
* [<span data-ttu-id="d3e49-265">What are the policy options with SSPR?</span><span class="sxs-lookup"><span data-stu-id="d3e49-265">What are the policy options with SSPR?</span></span>](concept-sspr-policy.md)
* [<span data-ttu-id="d3e49-266">What is password writeback and why do I care about it?</span><span class="sxs-lookup"><span data-stu-id="d3e49-266">What is password writeback and why do I care about it?</span></span>](howto-sspr-writeback.md)
* [<span data-ttu-id="d3e49-267">How do I report on activity in SSPR?</span><span class="sxs-lookup"><span data-stu-id="d3e49-267">How do I report on activity in SSPR?</span></span>](howto-sspr-reporting.md)
* [<span data-ttu-id="d3e49-268">What are all of the options in SSPR and what do they mean?</span><span class="sxs-lookup"><span data-stu-id="d3e49-268">What are all of the options in SSPR and what do they mean?</span></span>](concept-sspr-howitworks.md)
* [<span data-ttu-id="d3e49-269">I think something is broken. How do I troubleshoot SSPR?</span><span class="sxs-lookup"><span data-stu-id="d3e49-269">I think something is broken. How do I troubleshoot SSPR?</span></span>](active-directory-passwords-troubleshoot.md)
